---
title: Innehållssökning och indexering
description: Innehållssökning och indexering
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: 3682426cc333414a9fd20000e4d021fc622ff3b5
workflow-type: tm+mt
source-wordcount: '2420'
ht-degree: 1%

---

# Innehållssökning och indexering {#indexing}

## Ändringar i AEM as a Cloud Service {#changes-in-aem-as-a-cloud-service}

Med AEM as a Cloud Service går Adobe från en AEM instanscentrerad modell till en tjänstebaserad vy med n-x-AEM-behållare, som drivs av CI/CD-pipelines i Cloud Manager. I stället för att konfigurera och underhålla index för enskilda AEM måste indexkonfigurationen anges före en distribution. Konfigurationsförändringar i produktionen bryter helt klart CI/CD-reglerna. Detsamma gäller för indexändringar eftersom det kan påverka systemets stabilitet och prestanda om det inte anges testat och omindexerat innan de tas i produktion.

Nedan finns en lista över de viktigaste ändringarna jämfört med AEM 6.5 och tidigare versioner:

1. Användare har inte längre åtkomst till indexhanteraren för en enskild AEM för att felsöka, konfigurera eller underhålla indexering. Det används endast för lokal utveckling och lokal driftsättning.

1. Användare ändrar inte index för en enskild AEM och behöver inte längre bekymra sig om konsekvenskontroller eller omindexering.

1. I allmänhet inleds indexändringar innan produktionen påbörjas för att inte kringgå kvalitetsgatewayer i Cloud Managers CI/CD-pipelines och inte påverka affärs-KPI:er i produktionen.

1. Alla relaterade mätvärden, inklusive sökresultat i produktion, kommer att vara tillgängliga för kunder vid körning för att ge en helhetsbild av ämnen som sökning och indexering handlar om.

1. Kunderna kan skapa varningar efter behov.

1. SRE övervakar systemets hälsa dygnet runt, alla dagar i veckan och kommer att vidta åtgärder efter behov och så tidigt som möjligt.

1. Indexkonfigurationen ändras via distributioner. Ändringar av indexdefinitioner konfigureras på samma sätt som andra innehållsändringar.

1. På en hög nivå på AEM as a Cloud Service, med införandet av [Blå-grön distributionsmodell](#index-management-using-blue-green-deployments) två uppsättningar index kommer att finnas: en uppsättning för den gamla versionen (blå) och en uppsättning för den nya versionen (grön).

1. Kunderna kan se om indexeringsjobbet är klart på Cloud Managers byggsida och får ett meddelande när den nya versionen är klar att börja trafikera.

1. Begränsningar:
* För närvarande stöds indexhantering på AEM as a Cloud Service bara för index av typen `lucene`.
* Endast standardanalysatorer stöds (dvs. de som levereras tillsammans med produkten). Anpassade analysatorer stöds inte.
* Internt kan andra index konfigureras och användas för frågor. Till exempel frågor som skrivs mot `damAssetLucene` index kan på Skyline faktiskt köras mot en Elasticsearch-version av detta index. Skillnaden är vanligtvis inte synlig för programmet och användaren, men vissa verktyg som `explain` funktionen rapporterar ett annat index. Skillnader mellan Lucene-index och Elastic Index finns i [den elastiska dokumentationen i Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). Kunderna behöver inte, och kan inte, konfigurera Elasticsearch-index direkt.

## Användning {#how-to-use}

Att definiera index kan omfatta följande tre användningsområden:

1. Lägga till en ny kundindexdefinition.
1. Uppdaterar en befintlig indexdefinition. Det innebär att en ny version av en befintlig indexdefinition läggs till.
1. Tar bort ett befintligt index som är överflödigt eller föråldrat.

För båda punkterna 1 och 2 ovan måste du skapa en ny indexdefinition som en del av din anpassade kodbas i respektive Cloud Manager-utgåva. Mer information finns i [Distribuera till AEM as a Cloud Service dokumentation](/help/implementing/deploying/overview.md).

## Indexnamn {#index-names}

En indexdefinition kan vara:

1. Ett körklart index. Ett exempel är `/oak:index/cqPageLucene-2`.
1. En anpassning av ett körklart index. Sådana anpassningar definieras av kunden. Ett exempel är `/oak:index/cqPageLucene-2-custom-1`.
1. Ett helt anpassat index. Ett exempel är `/oak:index/acme.product-1-custom-2`. För att undvika namnkonflikter kräver vi att helt anpassade index har ett prefix, t.ex. `acme.`

Observera att både anpassning av ett körklart index och helt anpassade index måste innehålla `-custom-`. Endast helt anpassade index får börja med ett prefix.

## Förbereder den nya indexdefinitionen {#preparing-the-new-index-definition}

>[!NOTE]
>
>Om du till exempel anpassar ett index som inte finns i kartongen `damAssetLucene-6`, please copy the latest out-of-box index definition from a *Cloud Service* utvecklingsmiljö med hjälp av CRX DE Package Manager (`/crx/packmgr/`) . Byt sedan namn på konfigurationen, till exempel för att `damAssetLucene-6-custom-1`och lägg till anpassningar överst. Detta säkerställer att nödvändiga konfigurationer inte tas bort av misstag. Till exempel `tika` nod under `/oak:index/damAssetLucene-6/tika` krävs i det anpassade indexvärdet för molntjänsten. Den finns inte i molnet-SDK:n.

Du måste förbereda ett nytt indexdefinitionspaket som innehåller den faktiska indexdefinitionen, enligt namnmönstret:

`<indexName>[-<productVersion>]-custom-<customVersion>`

som sedan måste gå under `ui.apps/src/main/content/jcr_root`. Underrotmappar stöds inte för närvarande.

Filtret för paketet måste anges så att befintliga (ej låsta) index behålls. I filen `ui.apps/src/main/content/META-INF/vault/filter.xml`måste varje anpassat (eller anpassat) index listas, till exempel som `<filter root="/oak:index/damAssetLucene-6-custom-1"/>`. Om indexversionen ändras senare måste filtret justeras.

Paketet från exemplet ovan byggs som `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`.

>[!NOTE]
>
>Alla innehållspaket som innehåller indexdefinitioner bör ha följande egenskap angiven i egenskapsfilen för innehållspaketet, som finns på `/META-INF/vault/properties.xml`:
>
>`noIntermediateSaves=true`

## Distribuera indexdefinitioner {#deploying-index-definitions}

>[!NOTE]
>
>Det finns ett känt fel med Jackrabbit Filevault Maven Package Plugin **1.1.0** som inte tillåter att du lägger till `oak:index` till moduler `<packageType>application</packageType>`. Du bör uppdatera till en senare version av det plugin-programmet.

Indexdefinitioner har nu markerats som anpassade och versionsindelade:

* Själva indexdefinitionen (till exempel `/oak:index/ntBaseLucene-custom-1`)

För att kunna distribuera ett index måste därför indexdefinitionen (`/oak:index/definitionname`) måste levereras via `ui.apps` via Git och Cloud Manager-distributionsprocessen.

När den nya indexdefinitionen har lagts till måste det nya programmet distribueras via Cloud Manager. När distributionen är klar startas två jobb som ansvarar för att lägga till (och sammanfoga vid behov) indexdefinitionerna i MongoDB och Azure Segment Store för författare respektive publicering. De underliggande databaserna omindexeras med de nya indexdefinitionerna, innan den blå-gröna växlingen äger rum.

>[!TIP]
>
>Mer information om den paketstruktur som krävs för AEM as a Cloud Service finns i dokumentet [AEM projektstruktur.](/help/implementing/developing/introduction/aem-project-content-package-structure.md)

## Indexhantering med användning av blå-gröna distributioner {#index-management-using-blue-green-deployments}

### Vad är indexhantering? {#what-is-index-management}

Indexhantering handlar om att lägga till, ta bort och ändra index. Ändra *definition* för ett index är snabbt, men det tar lång tid att tillämpa ändringen (kallas ofta&quot;skapa ett index&quot; eller&quot;omindexering&quot; för befintliga index). Det är inte omedelbart: databasen måste genomsökas för att data ska kunna indexeras.

### Vad är Blue-Green Deployment? {#what-is-blue-green-deployment}

Blue-Green-driftsättning kan minska driftstoppen. Det ger även inga driftavbrott och ger snabba återställningar. Den gamla versionen av programmet (blå) körs samtidigt som den nya versionen av programmet (grön).

### Skrivskyddade och skrivskyddade områden {#read-only-and-read-write-areas}

Vissa delar av databasen (skrivskyddade delar av databasen) kan vara olika i den gamla (blå) och den nya (gröna) versionen av programmet. De skrivskyddade områdena i databasen är vanligtvis`/app`&quot; och &quot;`/libs`&quot;. I följande exempel används kursiv för att markera skrivskyddade områden, medan fetstil används för skrivskyddade områden.

* **/**
* */apps (skrivskyddad)*
* **/content**
* */libs (skrivskyddad)*
* **/oak:index**
* **/oak:index/acme.**
* **/jcr:system**
* **/system**
* **/var**

Databasens läs- och skrivområden delas mellan alla programversioner, medan det för varje programversion finns en specifik uppsättning `/apps` och `/libs`.

### Indexhantering utan blå-grön driftsättning {#index-management-without-blue-green-deployment}

Under utvecklingen, eller vid användning av lokala installationer, kan index läggas till, tas bort eller ändras under körningen. Index används så snart de är tillgängliga. Om ett index inte ska användas i den gamla versionen av programmet än, skapas indexet vanligtvis under en schemalagd driftstopp. Samma sak händer när du tar bort ett index eller ändrar ett befintligt index. När du tar bort ett index blir det otillgängligt så fort det tas bort.

### Indexhantering med blå-grön driftsättning {#index-management-with-blue-green-deployment}

Med blågröna installationer blir det inga driftstopp. Under en uppgradering körs både den gamla versionen (till exempel version 1) av programmet och den nya versionen (version 2) samtidigt mot samma databas. Om version 1 kräver att ett visst index är tillgängligt får detta index inte tas bort i version 2: indexet bör tas bort senare, till exempel i version 3, där det garanteras att version 1 av programmet inte längre körs. Dessutom bör program skrivas så att version 1 fungerar bra, även om version 2 körs, och om det finns index för version 2.

När uppgraderingen till den nya versionen är klar kan gamla index samlas in av systemet. De gamla indexen kan fortfarande finnas kvar en tid för att påskynda återställningen (om en återställning behövs).

I följande tabell visas fem indexdefinitioner: index `cqPageLucene` används i båda versionerna medan index `damAssetLucene-custom-1` används endast i version 2.

>[!NOTE]
>
>`<indexName>-custom-<customerVersionNumber>` är nödvändigt för AEM as a Cloud Service att markera detta som en ersättning för ett befintligt index.

| Index | Index som inte är tillgängligt | Använd i version 1 | Använd i version 2 |
|---|---|---|---|
| /oak:index/damAssetLucene | Ja | Ja | Nej |
| /oak:index/damAssetLucene-custom-1 | Ja (anpassad) | Nej | Ja |
| /oak:index/acme.product-custom-1 | Nej | Ja | Nej |
| /oak:index/acme.product-custom-2 | Nej | Nej | Ja |
| /oak:index/cqPageLucene | Ja | Ja | Ja |

Versionsnumret ökas stegvis varje gång indexvärdet ändras. För att undvika att egna indexnamn kolliderar med indexnamnen för själva produkten måste anpassade index, liksom ändringar i index utanför rutan, sluta med `-custom-<number>`.

### Ändringar av färdiga index {#changes-to-out-of-the-box-indexes}

När Adobe ändrar ett index som inte finns med i kartongen som &quot;damAssetLucene&quot; eller &quot;cqPageLucene&quot;, ett nytt index med namnet `damAssetLucene-2` eller `cqPageLucene-2` skapas eller, om indexet redan har anpassats, sammanfogas den anpassade indexdefinitionen med ändringarna i det körklara indexet enligt nedan. Ändringarna sammanfogas automatiskt. Det innebär att du inte behöver göra något om ett index som inte finns i kartongen ändras. Det går dock att anpassa indexet igen senare.

| Index | Index som inte är tillgängligt | Använd i version 2 | Använd i version 3 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | Ja (anpassad) | Ja | Nej |
| /oak:index/damAssetLucene-2-custom-1 | Ja (sammanfogas automatiskt från damAssetLucene-custom-1 och damAssetLucene-2) | Nej | Ja |
| /oak:index/cqPageLucene | Ja | Ja | Nej |
| /oak:index/cqPageLucene-2 | Ja | Nej | Ja |

### Aktuella begränsningar {#current-limitations}

Indexhantering stöds för närvarande bara för index av typen `lucene`. Internt kan andra index konfigureras och användas för frågor, till exempel elastiska index.

### Lägga till ett index {#adding-an-index}

Lägga till ett helt anpassat index med namnet `/oak:index/acme.product-custom-1` för att kunna användas i en ny version av programmet och senare, måste indexet konfigureras på följande sätt:

`acme.product-1-custom-1`

Detta fungerar genom att en anpassad identifierare förskjuts till indexnamnet, följt av en punkt (**`.`**). Identifieraren ska vara mellan 2 och 5 tecken lång.

Som ovan säkerställer detta att indexet bara används av den nya versionen av programmet.

### Ändra ett index {#changing-an-index}

När ett befintligt index ändras måste ett nytt index läggas till med den ändrade indexdefinitionen. Ta till exempel det befintliga indexet `/oak:index/acme.product-custom-1` ändras. Det gamla indexet lagras under `/oak:index/acme.product-custom-1`och det nya indexet lagras under `/oak:index/acme.product-custom-2`.

I den gamla versionen av programmet används följande konfiguration:

`/oak:index/acme.product-custom-1`

I den nya versionen av programmet används följande (ändrade) konfiguration:

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>Indexdefinitioner på AEM as a Cloud Service kanske inte helt matchar indexdefinitionerna på en lokal utvecklingsinstans. Utvecklingsinstansen har ingen Tika-konfiguration, medan AEM as a Cloud Service instanser har en. Om du anpassar ett index med en Tika-konfiguration bör du behålla Tika-konfigurationen.

### Ångra en ändring {#undoing-a-change}

Ibland behöver en ändring i en indexdefinition återställas. Orsaken kan vara att en ändring har gjorts av misstag eller att en ändring inte längre behövs. Indexdefinitionen `damAssetLucene-8-custom-3` skapades av misstag och har redan distribuerats. Därför kanske du vill återgå till den tidigare indexdefinitionen `damAssetLucene-8-custom-2`. Om du vill göra det måste du lägga till ett nytt index som kallas `damAssetLucene-8-custom-4` som innehåller definitionen av föregående index, `damAssetLucene-8-custom-2`.

### Ta bort ett index {#removing-an-index}

Följande gäller bara för anpassade index. Produktindex kan inte tas bort eftersom de används av AEM.

Om ett index ska tas bort i en senare version av programmet kan du definiera ett tomt index (ett tomt index som aldrig används och som inte innehåller några data) med ett nytt namn. I det här exemplet kan du ge det ett namn `/oak:index/acme.product-custom-3`. Detta ersätter indexvärdet `/oak:index/acme.product-custom-2`. En gång `/oak:index/acme.product-custom-2` tas bort av systemet, det tomma indexet `/oak:index/acme.product-custom-3` kan sedan också tas bort. Ett exempel på ett sådant tomt index är:

```xml
<acme.product-custom-3
        jcr:primaryType="oak:QueryIndexDefinition"
        async="async"
        compatVersion="2"
        includedPaths="/dummy"
        queryPaths="/dummy"
        type="lucene">
        <indexRules jcr:primaryType="nt:unstructured">
            <rep:root jcr:primaryType="nt:unstructured">
                <properties jcr:primaryType="nt:unstructured">
                    <dummy
                        jcr:primaryType="nt:unstructured"
                        name="dummy"
                        propertyIndex="{Boolean}true"/>
                </properties>
            </rep:root>
        </indexRules>
    </acme.product-custom-3>
```

Om det inte längre behövs någon anpassning av ett index som inte finns i kartongen måste du kopiera indexdefinitionen som finns i kartongen. Om du till exempel redan har distribuerat `damAssetLucene-8-custom-3`, men behöver inte längre anpassningar och vill växla tillbaka till standardinställningen `damAssetLucene-8` index, måste du lägga till ett index `damAssetLucene-8-custom-4` som innehåller indexdefinitionen för `damAssetLucene-8`.

## Indexoptimeringar {#index-optimizations}

Apache Jackrabbit Oak möjliggör flexibla indexkonfigurationer för att effektivt hantera sökfrågor. Index är särskilt viktiga för större databaser. Se till att alla frågor backas upp av ett lämpligt index. Frågor utan lämpligt index kan läsa tusentals noder, som sedan loggas som en varning. Sådana frågor bör identifieras genom analys av loggfilerna så att indexdefinitionerna kan optimeras. Se [den här sidan](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html?lang=en#tips-for-creating-efficient-indexes) för mer information.

### Lucene fulltextindex på AEM as a Cloud Service {#index-lucene}

fulltextindexet `/oak:index/lucene-2` kan bli mycket stor eftersom den indexerar alla noder i AEM som standard.  Efter Adobe planer på att ta tillbaka detta index kommer det inte längre att användas på produktsidan i AEM as a Cloud Service och det bör inte krävas att kundkoden körs. För AEM as a Cloud Service miljöer med gemensamma Lucene-index arbetar Adobe med kunder var för sig för att kompensera för detta index och för att använda bättre, optimerade index. Kunderna behöver inte vidta några åtgärder utan vidare besked från Adobe. AEM as a Cloud Service kunder kommer att informeras av Adobe när det finns behov av åtgärder för denna optimering. Om det här indexet behövs för anpassade frågor, som en tillfällig lösning, bör en kopia av indexet skapas med ett annat namn, till exempel `/oak:index/acme.lucene-1-custom-1`, enligt beskrivning [här](/help/operations/indexing.md).
Optimeringen gäller som standard inte andra AEM miljöer som lagras lokalt eller hanteras av Adobes hanterade tjänster.

## Frågeoptimeringar {#index-query}

The **Frågeprestanda** kan du observera både vanliga och långsamma JCR-frågor. Dessutom kan programmet analysera frågor och visa olika information om, särskilt om ett index används för frågan eller inte.

Till skillnad från i AEM lokalt visas inte AEM as a Cloud Service **Frågeprestanda** i användargränssnittet längre. Istället är den nu tillgänglig via Developer Console (i Cloud Manager) på [Frågor](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html#queries) -fliken.
