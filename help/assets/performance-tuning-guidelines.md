---
title: Justeringshandbok för resursprestanda
description: Viktiga fokusområden kring AEM-konfiguration, ändringar av maskinvara, programvara och nätverkskomponenter för att ta bort flaskhalsar och optimera prestanda för AEM Assets.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Justeringshandbok för resursprestanda{#assets-performance-tuning-guide}

En AEM-konfiguration (Adobe Experience Manager) innehåller ett antal maskinvaru-, programvaru- och nätverkskomponenter. Beroende på ditt driftsättningsscenario kan du behöva specifika konfigurationsändringar för maskinvara, programvara och nätverkskomponenter för att ta bort flaskhalsar i prestandan.

Genom att identifiera och följa vissa riktlinjer för optimering av maskinvara och programvara kan du dessutom skapa en stabil grund som gör att driftsättningen av AEM Assets kan uppfylla förväntningarna på prestanda, skalbarhet och tillförlitlighet.

Dåliga prestanda i AEM Assets kan påverka användarupplevelsen när det gäller interaktiva prestanda, bearbetning av resurser, nedladdningshastighet och andra områden.

Prestandaoptimering är en grundläggande uppgift som du utför innan du fastställer målvärden för ett projekt.

Här är några viktiga fokusområden där du kan identifiera och åtgärda prestandaproblem innan de påverkar användarna.

## Platform {#platform}

AEM stöds på ett antal plattformar, men Adobe har funnit det bästa stödet för inbyggda verktyg i Linux och Windows, vilket ger optimala prestanda och förenklad implementering. Det bästa är att driftsätta ett 64-bitars operativsystem för att uppfylla de höga minneskraven för en AEM Assets-driftsättning. Precis som för alla AEM-distributioner bör du implementera tarMK där det är möjligt. Även om TonaMK inte kan skalas bortom en enda författarinstans, fungerar det bättre än MongoMK. Du kan lägga till instanser av TjärMK-avlastning för att öka arbetsflödets bearbetningskraft i din AEM Assets-distribution.

### Tillfällig mapp {#temp-folder}

Om du vill förbättra överföringstiden för resurser använder du lagring med höga prestanda för den tillfälliga Java-katalogen. I Linux och Windows kan en RAM-enhet eller SSD användas. I molnbaserade miljöer kan en motsvarande typ av höghastighetslagring användas. I till exempel Amazon EC2 kan en [&quot;kortdisk&quot;](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) -enhet användas för den tillfälliga mappen.

Om servern har tillräckligt med minne konfigurerar du en RAM-enhet. Kör följande kommandon i Linux för att skapa en 8 GB RAM-enhet:

```
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

I Windows måste du använda en drivrutin från tredje part för att skapa en RAM-enhet eller bara använda lagring med höga prestanda, som SSD.

När den tillfälliga volymen med höga prestanda är klar anger du JVM-parametern -Djava.io.tmpdir. Du kan till exempel lägga till JVM-parametern nedan till variabeln CQ_JVM_OPTS i skriptet bin/start för AEM:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java-konfiguration {#java-configuration}

### Java-version {#java-version}

Eftersom Oracle har slutat släppa uppdateringar för Java 7 från och med april 2015 rekommenderar Adobe att man driftsätter AEM Assets på Java 8. I vissa fall har den visat bättre prestanda.

### JVM-parametrar {#jvm-parameters}

Du bör ange följande JVM-parametrar:

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## Datalagring och minneskonfiguration {#data-store-and-memory-configuration}

### Konfiguration av fillagring {#file-data-store-configuration}

Du bör separera datalagret från segmentlagret för alla AEM Resurser-användare. Dessutom kan konfigurering av parametrarna `maxCachedBinarySize` och `cacheSizeInMB` hjälpa till att maximera prestandan. Ange `maxCachedBinarySize` den minsta filstorlek som kan sparas i cachen. Ange storleken på den minnescache som ska användas för datalagret i `cacheSizeInMB`. Adobe rekommenderar att du anger det här värdet mellan 2 och 10 procent av den totala stackstorleken. Inläsnings-/prestandatestning kan dock hjälpa till att fastställa den idealiska inställningen.

### Konfigurera maximal storlek för buffrad bildcache {#configure-the-maximum-size-of-the-buffered-image-cache}

När du överför stora mängder resurser till Adobe Experience Manager kan du minska den konfigurerade maxstorleken för buffrat bildcacheminne för att undvika oväntade ökningar i minnesanvändningen och för att förhindra att JVM misslyckas med OutOfMemoryErrors. Tänk dig ett exempel på att du har ett system med en högsta heap (- `Xmx`param) på 5 GB, en Oak BlobCache inställd på 1 GB och dokumentcache inställd på 2 GB. I det här fallet tar den buffrade cachen upp till 1,25 GB och minne, vilket innebär att endast 0,75 GB minne återstår för oväntade toppar.

Konfigurera den buffrade cachestorleken i OSGi-webbkonsolen. Vid `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`anger du egenskapen `cq.dam.image.cache.max.memory` i byte. 1073741824 är till exempel 1 GB (1 024 x 1 024 x 1 024 = 1 GB).

Om du använder en nod för att konfigurera den här egenskapen från AEM 6.1 SP1 måste du ange datatypen Long om du använder en `sling:osgiConfig` nod. Mer information finns i [CQBufferedImageCache förbrukar heap under överföring](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html)av resurser.

### Gemensamma datalager {#shared-data-stores}

Implementering av ett S3- eller delat fildatalager kan bidra till att spara diskutrymme och öka nätverkets genomströmning i storskaliga implementeringar.

### S3-datalager {#s-data-store}

Följande S3 Data Store-konfiguration ( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`) hjälper Adobe att extrahera 12,8 TB binära stora objekt (BLOB) från ett befintligt arkiv till ett S3-datalager på en kunds webbplats:

```
accessKey=<snip>
 secretKey=<snip>
 s3Bucket=<snip>
 s3Region=us-standard
 s3EndPoint=<a href="https://s3.amazonaws.com/">s3.amazonaws.com</a>
 connectionTimeout=120000
 socketTimeout=120000
 maxConnections=80
 writeThreads=60
 concurrentUploadsThreads=30
 asyncUploadLimit=30
 maxErrorRetry=1000
 path=/opt/author/crx-quickstart/repository/datastore
 s3RenameKeys=false
 s3Encryption=SSE_S3
 proactiveCaching=true
 uploadRetries=1000
 migrateFailuresCount=400
```

## Nätverksoptimering {#network-optimization}

Adobe rekommenderar att du aktiverar HTTPS eftersom många företag har brandväggar som fångar upp HTTP-trafik, vilket påverkar överföringar negativt och skadar filer. För stora filöverföringar måste användarna ha kabelanslutna anslutningar till nätverket eftersom ett WiFi-nätverk snabbt blir mättat. Information om hur du utvärderar nätverksprestanda genom att analysera nätverkstopologi finns i [Resurser för nätverksaspekter](/help/assets/assets-network-considerations.md).

Din nätverksoptimeringsstrategi är i första hand beroende av hur mycket bandbredd som är tillgänglig och hur stor belastning din AEM-instans har. Gemensamma konfigurationsalternativ, inklusive brandväggar och proxies, kan förbättra nätverkets prestanda. Här följer några viktiga punkter att tänka på:

* Beroende på vilken instanstyp du har (liten, måttlig, stor) kontrollerar du att du har tillräcklig nätverksbandbredd för AEM-instansen. Lämplig bandbreddsallokering är särskilt viktig om AEM ligger på AWS.
* Om din AEM-instans finns på AWS kan du dra nytta av en mångsidig skalningspolicy. Överför instansen om användarna förväntar sig hög belastning. Minska storleken för måttlig/låg belastning.
* HTTPS: De flesta användare har brandväggar som tolkar HTTP-trafik, vilket kan påverka överföringen av filer negativt eller till och med skada filer under överföringen.
* Stora filöverföringar: Se till att användarna har kabelanslutna anslutningar till nätverket (WiFi-anslutningar blir snabbt mättade).

## Arbetsflöden {#workflows}

### Övergående arbetsflöden {#transient-workflows}

Ställ in arbetsflödet DAM Update Asset på Transient när det är möjligt. Inställningen minskar avsevärt de allmänna kostnader som krävs för att bearbeta arbetsflöden, eftersom arbetsflöden i det här fallet inte behöver passera genom de normala spårnings- och arkiveringsprocesserna.

>[!NOTE]
>
>Som standard är arbetsflödet för DAM-uppdatering av tillgångar inställt på Transient i AEM 6.3. I så fall kan du hoppa över följande procedur.

1. Navigera till */miscadmin* i den AEM-instans som ska konfigureras (t.ex. [https://localhost:4502/miscadmin)](https://localhost:4502/miscadmin).
1. Expandera **Verktyg** > **Arbetsflöde** > **Modeller** > **dam** i navigeringsträdet.
1. Dubbelklicka på **DAM Update Asset**.
1. Gå till fliken **Sida** på den flytande verktygspanelen och klicka sedan på **Sidegenskaper...**
1. Välj **Övergående arbetsflöde** och klicka sedan på **OK**.

   >[!NOTE]
   >
   >Vissa funktioner har inte stöd för tillfälliga arbetsflöden. Om din AEM Assets-distribution kräver dessa funktioner ska du inte konfigurera tillfälliga arbetsflöden.

   Om det inte går att använda tillfälliga arbetsflöden kör du regelbundet arbetsflödesrensning för att ta bort arkiverade arbetsflöden för DAM Update Asset för att säkerställa att systemprestanda inte försämras.

   Vanligtvis bör du köra rensningsarbetsflöden varje vecka. I resurskrävande scenarier, till exempel vid omfattande tillgångsinhämtning, kan du dock köra det oftare.

   Om du vill konfigurera rensning av arbetsflöden lägger du till en ny Adobe Granite Workflow Renge-konfiguration via OSGi-konsolen. Konfigurera och schemalägg arbetsflödet som en del av veckounderhållsperioden.

   Om tömningen är för lång så tar det för lång tid. Därför bör du se till att rensningsjobben är fullständiga för att undvika situationer där rensningsarbetsflödena misslyckas på grund av det stora antalet arbetsflöden.

   När du har kört flera icke-tillfälliga arbetsflöden (som skapar arbetsflödesinstansnoder) kan du köra [ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) på ad hoc-basis. Det tar bort överflödiga, slutförda arbetsflödesinstanser direkt i stället för att vänta på att schemaläggaren för rensning av arbetsflödet i Adobe Granite ska köras.

### Maximalt antal parallella jobb {#maximum-parallel-jobs}

Som standard kör AEM ett maximalt antal parallella jobb som motsvarar antalet processorer på servern. Problemet med den här inställningen är att under perioder med hög belastning används alla processorer av arbetsflödena för DAM Update Asset, vilket gör att användargränssnittet tar längre tid och förhindrar att AEM kör andra processer som skyddar serverns prestanda och stabilitet. Det är en god vana att ange det här värdet till hälften av de processorer som är tillgängliga på servern genom att utföra följande steg:

1. På AEM Author går du till [https://localhost:4502/system/console/slingevent](https://localhost:4702/system/console/slingevent).
1. Klicka på Redigera i varje arbetsflödeskö som är relevant för implementeringen, till exempel Bevilja tillfällig arbetsflödeskö.
1. Ändra värdet för Maximalt antal parallella jobb och klicka på Spara.

Att ställa in en kö på hälften av de tillgängliga processorerna är en användbar lösning att börja med. Du kan dock behöva öka eller minska det här antalet för att få maximal genomströmning och justera det efter miljö. Det finns separata köer för tillfälliga och icke-tillfälliga arbetsflöden samt andra processer, till exempel externa arbetsflöden. Om flera köer är inställda på 50 % av processorerna aktiva samtidigt kan systemet snabbt bli överbelastat. De köer som används ofta varierar mycket mellan olika implementeringar. Därför kan du behöva konfigurera dem noggrant för maximal effektivitet utan att ge avkall på serverstabiliteten.

### DAM-uppdateringskonfiguration {#dam-update-asset-configuration}

Arbetsflödet för DAM-uppdatering av resurser innehåller en komplett serie steg som är konfigurerade för uppgifter, till exempel Scene7 PTIFF-generering och InDesign Server-integrering. De flesta användare behöver dock inte utföra flera av dessa steg. Adobe rekommenderar att du skapar en anpassad kopia av arbetsflödesmodellen DAM Update Asset och tar bort alla onödiga steg. I det här fallet ska du uppdatera startarna för DAM Update Asset så att de pekar på den nya modellen.

>[!NOTE]
>
>Om du kör arbetsflödet DAM Update Asset kraftigt kan du öka storleken på filens datalager. Resultaten från ett experiment som Adobe har utfört har visat att datalagrets storlek kan öka med ungefär 400 GB om ca 500 arbetsflöden utförs inom 8 timmar.
>
>Det är en tillfällig ökning och datalagret återställs till den ursprungliga storleken när du har kört skräpinsamlingsaktiviteten för datalagret.
>
>Vanligtvis körs skräpinsamlingsaktiviteten för datalager varje vecka tillsammans med andra schemalagda underhållsaktiviteter.
>
>Om du har begränsat diskutrymme och kör arbetsflöden för DAM-uppdatering av resurser intensivt bör du överväga att schemalägga skräpinsamlingen oftare.

#### Generering av rendering vid körning {#runtime-rendition-generation}

Kunderna använder bilder av olika storlek och format på sin webbplats eller för att distribuera dem till affärspartners. Eftersom varje återgivning ökar utrymmet för resursen i databasen rekommenderar Adobe att du använder funktionen noggrant. Om du vill minska mängden resurser som behövs för att bearbeta och lagra bilder kan du generera dessa bilder vid körning i stället för som återgivningar vid importen.

Många webbplatskunder implementerar en bildservett som ändrar storlek på och beskär bilder när de begärs, vilket medför ytterligare belastning på publiceringsinstansen. Så länge dessa bilder kan cachas kan utmaningen dock mildras.

Ett annat sätt är att använda Scene7-teknik för att helt och hållet överlåta bildbearbetning. Dessutom kan ni distribuera varumärkesportalen som inte bara tar över ansvaret för återgivningsgenerering från AEM-infrastrukturen, utan även hela publiceringsnivån.

### XMP-tillbakaskrivning {#xmp-writeback}

XMP-tillbakaskrivning uppdaterar originalresursen när metadata ändras i AEM, vilket ger följande resultat:

* Själva tillgången ändras
* En version av resursen skapas
* DAM Update Asset körs mot resursen

De listade resultaten kräver stora resurser. Därför rekommenderar Adobe att du [inaktiverar XMP-återställning](https://helpx.adobe.com/experience-manager/kb/disable-xmp-writeback.html)om det inte behövs.

Om du importerar en stor mängd metadata kan det leda till resurskrävande XMP-återskrivningsaktivitet om körningsarbetsflödesflaggan är markerad. Planera en sådan import under begränsad serveranvändning så att prestanda för andra användare inte påverkas.

## Replikering {#replication}

När du replikerar resurser till ett stort antal publiceringsinstanser, till exempel i en webbplatsimplementering, rekommenderar Adobe att du använder kedjereplikering. I det här fallet replikeras författarinstansen till en enda publiceringsinstans som i sin tur replikeras till de andra publiceringsinstanserna och frigör författarinstansen.

### Konfigurera kedjereplikering {#configure-chain-replication}

1. Välj vilken publiceringsinstans du vill använda för att länka replikeringarna till
1. På den publiceringsinstansen lägger du till replikeringsagenter som pekar på andra publiceringsinstanser
1. På var och en av dessa replikeringsagenter aktiverar du&quot;Vid mottagning&quot; på fliken&quot;Utlösare&quot;

>[!NOTE]
>
>Adobe rekommenderar inte att resurser aktiveras automatiskt. Om det behövs rekommenderar Adobe att du gör detta som det sista steget i ett arbetsflöde, vanligtvis DAM Update Asset.

## Sökindex {#search-indexes}

Se till att du implementerar de senaste Service Pack-uppdateringarna och prestandarelaterade snabbkorrigeringar eftersom de ofta innehåller uppdateringar av systemindex. Se tips [för prestandajustering| 6.x](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) för vissa indexoptimeringar som kan tillämpas, beroende på vilken version av AEM du har.

<!--
Create custom indexes for queries that you run often. For details, see [methodology for analyzing slow queries](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) and [crafting custom indexes](/help/sites-deploying/queries-and-indexing.md). For additional insights around query and index best practices, see [Best Practices for Queries and Indexing](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
-->

### Lucene-indexkonfigurationer {#lucene-index-configurations}

Vissa optimeringar kan göras för Oak-indexkonfigurationer som kan förbättra prestanda för AEM Assets:

Uppdatera indexkonfigurationer för att förbättra omindexeringstiden:

1. Öppna CRXDe /crx/de/index.jsp och logga in som administrativ användare
1. Bläddra till /oak:index/lucene
1. Lägg till en String[] -egenskap med namnet &quot;excludePaths&quot; med värdena &quot;/var&quot;, &quot;/etc/workflow/instances&quot; och &quot;/etc/replication&quot;
1. Bläddra till /oak:index/damAssetLucene
1. Lägg till en String[] -egenskap med namnet &quot;includedPaths&quot; med värdet &quot;/content/dam&quot;
1. Spara

(Endast AEM6.1 och 6.2) Uppdatera indexet ntBaseLucene för att förbättra prestanda vid borttagning och flyttning av resurser:

1. Bläddra till */läs:index/ntBaseLucene/indexRules/nt:base/properties*
1. Lägg till två nt:ostrukturerade noder &quot;slingResource&quot; och &quot;damResolvedPath&quot; under */oak:index/ntBaseLucene/indexRules/nt:base/properties*
1. Ange egenskaperna nedan på noderna (där ordnade egenskaper och propertyIndex-egenskaper är av typen *Boolean*:
slingResourceName=&quot;sling:resource&quot;ordered=falsepropertyIndex= truetype=&quot;String&quot;damResolvedPathname=&quot;dam:resolvedPath&quot;ordered=falsepropertyIndex=truetype=&quot;String&quot;

1. På noden /oak:index/ntBaseLucene anger du egenskapen *reindex=true*
1. Klicka på Spara alla
1. Övervaka error.log för att se när indexeringen är klar:
Omindexering har slutförts för index: [/ek:index/ntBaseLucene]
1. Du kan också se att indexeringen har slutförts genom att uppdatera noden /oak:index/ntBaseLucene i CRXDe eftersom egenskapen reindex skulle återgå till false
1. När indexeringen är klar går du tillbaka till CRXDe och anger att type-egenskapen ska inaktiveras för dessa två index

   * */oak:index/slingResource*
   * */oak:index/damResolvedPath*

1. Klicka på Spara alla

<!--
Disable Lucene Text Extraction:

If your users don't need to be able to search the contents of assets, for example, searching the text contained in PDF documents, then you can improve index performance by disabling this feature.

1. Go to the AEM package manager /crx/packmgr/index.jsp
1. Upload and install the package below

[Get File](assets/disable_indexingbinarytextextraction-10.zip)
-->

### Gissa totalt {#guess-total}

När du skapar frågor som genererar stora resultatuppsättningar bör du använda parametern för att undvika att använda mycket minne när du kör dem. `guessTotal`

## Kända fel {#known-issues}

### Stora filer {#large-files}

Det finns två viktiga kända fel som rör stora filer i AEM. När filer når större storlekar än 2 GB kan synkronisering med vänteläge i kallt läge hamna i en situation där minnet är slut. I vissa fall förhindras att standby-synkronisering körs. I andra fall kraschar den primära instansen. Detta scenario gäller alla filer i AEM som är större än 2 GB, inklusive innehållspaket.

På samma sätt kan det ta lite tid innan filen är helt beständig från cachen till filsystemet om filen är 2 GB stor när ett delat S3-datalager används. Detta innebär att om du använder en binär replikering utan binärfiler kan det hända att binära data inte har befunnits beständiga innan replikeringen slutförs. Denna situation kan leda till problem, särskilt om datatillgängligheten är viktig.

## Prestandatestning {#performance-testing}

För varje AEM-driftsättning måste ni skapa ett system för prestandatestning som snabbt kan identifiera och lösa flaskhalsar. Här är några nyckelområden att fokusera på.

### Nätverkstestning {#network-testing}

Utför följande uppgifter för alla problem med nätverkets prestanda från kunden:

* Testa nätverksprestanda inifrån kundens nätverk
* Testa nätverksprestanda inifrån Adobe. För AMS-kunder kan du arbeta med din CSE för att testa inifrån Adobe-nätverket.
* Testa nätverksprestanda från en annan åtkomstpunkt
* Genom att använda ett prestandatest för nätverk
* Testa mot dispatchern

### AEM-instanstestning {#aem-instance-testing}

För att minimera latens och uppnå hög genomströmning genom effektiv processoranvändning och lastdelning ska du regelbundet övervaka AEM-instansens prestanda. Särskilt gäller följande:

* Kör inläsningstester mot AEM-instansen
* Övervaka uppladdningsprestanda och gränssnittsvarstider

## Prestandakontrolllista för AEM Resurser och påverkan av resurshanteringsåtgärder {#checklist}

* Gör det möjligt för HTTPS att kringgå HTTP-trafiksnuttar
* Använd en kabelanslutning för överföring av stora resurser
* Driftsätt med Java 8.
* Ange optimala JVM-parametrar
* Konfigurera ett datalager i filsystemet eller ett S3 DataStore
* Aktivera tillfälliga arbetsflöden
* Justera Granite-arbetsflödesköer för att begränsa samtidiga jobb
* Konfigurera ImageMagick för att begränsa resursförbrukningen
* Ta bort onödiga steg från arbetsflödet för DAM-uppdatering
* Konfigurera arbetsflöde och versionsrensning
* Optimera index med de senaste servicepaketen och snabbkorrigeringarna. Kontakta Adobe Support för eventuella ytterligare indexoptimeringar.
* Använd gissningTotal för att optimera frågeprestanda.
* Om du konfigurerar AEM för att identifiera filtyper från filernas innehåll (genom att aktivera **[!UICONTROL Day CQ DAM Mime Type Service]** i **[!UICONTROL AEM Web Console]**) överför du många filer samtidigt under icke-toppade tider eftersom det är resurskrävande.

