---
title: Innehållssökning och indexering
description: Lär dig mer om innehållssökning och indexering på AEM as a Cloud Service.
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '2428'
ht-degree: 0%

---

# Innehållssökning och indexering {#indexing}

## Ändringar i AEM as a Cloud Service {#changes-in-aem-as-a-cloud-service}

Med AEM as a Cloud Service går Adobe från en AEM instanscentrerad modell till en tjänstebaserad vy med n-x-AEM-behållare, som drivs av CI/CD-pipelines i Cloud Manager. I stället för att konfigurera och underhålla index för enskilda AEM måste indexkonfigurationen anges före en distribution. Konfigurationsförändringar i produktionen bryter helt klart CI/CD-reglerna. Detsamma gäller för indexändringar eftersom det kan påverka systemets stabilitet och prestanda om det inte anges testat och omindexerat innan de tas i produktion.

Nedan finns en lista över de viktigaste ändringarna jämfört med AEM 6.5 och tidigare versioner:

1. Användare har inte åtkomst till Indexhanteraren för en enskild AEM instans för att felsöka, konfigurera eller underhålla indexering längre. Det används endast för lokal utveckling och lokal driftsättning.
1. Användare ändrar inte index för en enskild AEM och behöver inte längre bekymra sig om konsekvenskontroller eller omindexering.
1. I allmänhet inleds indexändringar innan produktionen påbörjas för att inte kringgå kvalitetsgatewayer i Cloud Managers CI/CD-pipelines och inte påverka affärs-KPI:er i produktionen.
1. Alla relaterade mätvärden, inklusive sökresultat i produktion, är tillgängliga för kunder vid körning för att ge en helhetsbild av ämnen som sökning och indexering handlar om.
1. Kunderna kan skapa varningar efter behov.
1. SRE övervakar systemets hälsa dygnet runt, alla dagar i veckan och åtgärder vidtas så tidigt som möjligt.
1. Indexkonfigurationen ändras via distributioner. Ändringar av indexdefinitioner konfigureras på samma sätt som andra innehållsändringar.
1. På en hög nivå på AEM as a Cloud Service, med introduktionen av [driftsättningsmodell](#index-management-using-rolling-deployments)finns det två uppsättningar index: en för den gamla versionen och en för den nya versionen.
1. Kunderna kan se om indexeringsjobbet är klart på Cloud Managers byggsida och får ett meddelande när den nya versionen är klar att börja trafikera.

Begränsningar:

* För närvarande stöds indexhantering på AEM as a Cloud Service bara för index av typen `lucene`.
* Endast standardanalysatorer stöds (det vill säga analysatorer som levereras tillsammans med produkten). Anpassade analysatorer stöds inte.
* Internt kan andra index konfigureras och användas för frågor. Till exempel frågor som skrivs mot `damAssetLucene` index kan på Skyline faktiskt köras mot en Elasticsearch-version av detta index. Skillnaden är vanligtvis inte synlig för programmet och användaren, men vissa verktyg, som `explain` rapportera ett annat index. Skillnader mellan Lucene-index och Elastic Index finns i [den elastiska dokumentationen i Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). Kunderna behöver inte, och kan inte, konfigurera Elasticsearch-index direkt.
* Sök efter liknande funktionsvektorer (`useInSimilarity = true`) stöds inte.

>[!TIP]
>
>Mer information om indexering och frågor, inklusive en detaljerad beskrivning av avancerade sök- och indexeringsfunktioner, finns i [Apache Oak-dokumentation](https://jackrabbit.apache.org/oak/docs/query/query.html).


## Användning {#how-to-use}

Indexdefinitioner kan kategoriseras i tre primära användningsområden:

1. **Lägg till** en ny anpassad indexdefinition.
2. **Uppdatera** en befintlig indexdefinition genom att lägga till en ny version.
3. **Ta bort** en indexdefinition som inte längre behövs.

För båda punkterna 1 och 2 ovan måste du skapa en indexdefinition som en del av din anpassade kodbas i respektive Cloud Manager-utgåva. Mer information finns i [Distribuera till AEM as a Cloud Service](/help/implementing/deploying/overview.md) dokumentation.

## Indexnamn {#index-names}

En indexdefinition kan delas in i någon av följande kategorier:

1. OTB-index (Out-of-the-box). Till exempel: `/oak:index/cqPageLucene-2` eller `/oak:index/damAssetLucene-8`.

2. Anpassning av ett OOTB-index. Dessa indikeras genom tillägg `-custom-` följt av en numerisk identifierare till det ursprungliga indexnamnet. Till exempel: `/oak:index/damAssetLucene-8-custom-1`.

3. Helt anpassat index: Det går att skapa ett helt nytt index från grunden. Deras namn måste ha ett prefix för att namnkonflikter ska undvikas. Till exempel: `/oak:index/acme.product-1-custom-2`, där prefixet är `acme.`

>[!NOTE]
>
>Nu kommer nya index på `dam:Asset` nodtype (speciellt fulltextindex) rekommenderas inte eftersom dessa kan skapa konflikter med OOTB-funktioner, vilket kan leda till funktions- och prestandaproblem. I allmänhet läggs ytterligare egenskaper till i den aktuella `damAssetLucene-*` indexversionen är det lämpligaste sättet att indexera frågor på `dam:Asset` nodetype (dessa ändringar sammanfogas automatiskt till en ny produktversion av indexet om det släpps senare). Om du är osäker kan du kontakta Adobe Support för råd.

## Förbereder den nya indexdefinitionen {#preparing-the-new-index-definition}

>[!NOTE]
>
>Om du till exempel anpassar ett index som inte finns i kartongen `damAssetLucene-8`, kopierar den senaste körklara indexdefinitionen från en *Cloud Service* med hjälp av CRX DE Package Manager (`/crx/packmgr/`) . Byt namn på den till `damAssetLucene-8-custom-1` (eller senare) och lägg till anpassningar i XML-filen. Detta säkerställer att de nödvändiga konfigurationerna inte tas bort av misstag. Till exempel `tika` nod under `/oak:index/damAssetLucene-8/tika` krävs i det anpassade indexet som distribueras till en AEM Cloud Service-miljö, men inte på den lokala AEM SDK:n.

Om du vill anpassa ett OOTB-index förbereder du ett nytt paket som innehåller den faktiska indexdefinitionen som följer namnmönstret:

`<indexName>-<productVersion>-custom-<customVersion>`

För ett helt anpassat index skapar du ett nytt indexdefinitionspaket som innehåller indexdefinitionen som följer detta namnmönster:

`<prefix>.<indexName>-<productVersion>-custom-<customVersion>`

<!-- Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`. -->

>[!NOTE]
>
>Alla innehållspaket som innehåller indexdefinitioner bör ha följande egenskaper angivna i egenskapsfilen för innehållspaketet, som finns på `<package_name>/META-INF/vault/properties.xml`:
>
> * `noIntermediateSaves=true`
>
> * `allowIndexDefinitions=true`

## Distribuera anpassade indexdefinitioner {#deploying-custom-index-definitions}

Så här illustrerar du hur en anpassad version av det körklara indexvärdet används `damAssetLucene-8`kommer vi att tillhandahålla en stegvis guide. I det här exemplet byter vi namn på den till `damAssetLucene-8-custom-1`. Sedan är processen följande:

1. Skapa en ny mapp med det uppdaterade indexnamnet i `ui.apps` katalog:
   * Exempel: `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/`

2. Lägg till en konfigurationsfil `.content.xml` med de anpassade konfigurationerna i den nya mappen. Nedan visas ett exempel på en anpassning: Filnamn: `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/.content.xml`

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:dam="http://www.day.com/dam/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0" xmlns:oak="http://jackrabbit.apache.org/oak/ns/1.0" xmlns:rep="internal"
       jcr:mixinTypes="[rep:AccessControllable]"
       jcr:primaryType="oak:QueryIndexDefinition"
       async="[async,nrt]"
       compatVersion="{Long}2"
       evaluatePathRestrictions="{Boolean}true"
       includedPaths="[/content/dam]"
       maxFieldLength="{Long}100000"
       type="lucene">
       <facets
           jcr:primaryType="nt:unstructured"
           secure="statistical"
           topChildren="100"/>
       <indexRules jcr:primaryType="nt:unstructured">
           <dam:Asset jcr:primaryType="nt:unstructured">
               <properties jcr:primaryType="nt:unstructured">
                   <cqTags
                       jcr:primaryType="nt:unstructured"
                       name="jcr:content/metadata/cq:tags"
                       nodeScopeIndex="{Boolean}true"
                       propertyIndex="{Boolean}true"
                       useInSpellcheck="{Boolean}true"
                       useInSuggest="{Boolean}true"/>
               </properties>
           </dam:Asset>
       </indexRules>
       <tika jcr:primaryType="nt:folder">
           <config.xml jcr:primaryType="nt:file"/>
       </tika>
   </jcr:root>
   ```

3. Lägg till en post i FileVault-filtret i `ui.apps/src/main/content/META-INF/vault/filter.xml`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       ...
       <filter root="/oak:index/damAssetLucene-8-custom-1"/> 
   </workspaceFilter>
   ```

4. Lägg till en konfigurationsfil för Apache Tika i: `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/tika/config.xml`:

   ```xml
   <properties>
       <detectors>
           <detector class="org.apache.tika.detect.TypeDetector"/>
       </detectors>
       <parsers>
           <parser class="org.apache.tika.parser.DefaultParser">
           <mime>text/plain</mime>
           </parser>
       </parsers>
       <service-loader initializableProblemHandler="ignore" dynamic="true"/>
   </properties>
   ```

5. Kontrollera att konfigurationen uppfyller riktlinjerna i [Projektkonfiguration](#project-configuration) -avsnitt. Gör nödvändiga anpassningar i enlighet med detta.

## Projektkonfiguration

Vi rekommenderar starkt att du använder version >= `1.3.2` av Jackrabbit `filevault-package-maven-plugin`. Så här implementerar du den i ditt projekt:

1. Uppdatera versionen på den översta nivån `pom.xml`:

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           ...
           <version>1.3.2</version>
       ...
   </plugin>
   ```

2. Lägg till följande på den översta nivån `pom.xml`:

   ```xml
   <jackrabbit-packagetype>
       <options>   
           <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
       </options>
   </jackrabbit-packagetype>
   ```

   Här är ett exempel på projektets högsta nivå `pom.xml` fil med de ovannämnda konfigurationerna:

   Filnamn: `pom.xml`

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           ...
           <version>1.3.2</version>
           <configuration>
               ...
               <validatorsSettings>
                   <jackrabbit-packagetype>
                       <options>
                           <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
                       </options>
                   </jackrabbit-packagetype>
                   ...
               ...
   </plugin>
   ```

3. I `ui.apps/pom.xml` och `ui.apps.structure/pom.xml` måste du aktivera `allowIndexDefinitions` och `noIntermediateSaves` i `filevault-package-maven-plugin`. Aktivering `allowIndexDefinitions` möjliggör anpassade indexdefinitioner, medan `noIntermediateSaves` säkerställer att konfigurationerna läggs till automatiskt.

   Filnamn: `ui.apps/pom.xml` och `ui.apps.structure/pom.xml`

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           <configuration>
               <allowIndexDefinitions>true</allowIndexDefinitions>
               <properties>
                   <cloudManagerTarget>none</cloudManagerTarget>
                   <noIntermediateSaves>true</noIntermediateSaves>
               </properties>
       ...
   </plugin>
   ```

4. Lägg till ett filter för `/oak:index` in `ui.apps.structure/pom.xml`:

   ```xml
   <filters>
       ...
       <filter><root>/oak:index</root></filter>
   </filters>
   ```

När du har lagt till den nya indexdefinitionen distribuerar du det nya programmet med Cloud Manager. Distributionen initierar två jobb som ansvarar för att lägga till (och sammanfoga om det behövs) indexdefinitionerna i MongoDB och Azure Segment Store för författare respektive publicering. Före bytet omindexeras de underliggande databaserna med de uppdaterade indexdefinitionerna.

>[!TIP]
>
>Mer information om den paketstruktur som krävs för AEM as a Cloud Service finns i [AEM projektstruktur](/help/implementing/developing/introduction/aem-project-content-package-structure.md).

## Indexhantering med rullande distributioner {#index-management-using-rolling-deployments}

### Vad är indexhantering? {#what-is-index-management}

Indexhantering handlar om att lägga till, ta bort och ändra index. Ändra *definition* för ett index är snabbt, men det tar lång tid att tillämpa ändringen (kallas ofta&quot;skapa ett index&quot; eller&quot;omindexering&quot; för befintliga index). Det är inte omedelbart: databasen måste genomsökas för att data ska kunna indexeras.

### Vad är rullande distributioner? {#what-are-rolling-deployments}

En rullande driftsättning kan minska driftstoppen. Det ger även inga driftavbrott och ger snabba återställningar. Den gamla versionen av programmet körs samtidigt som den nya versionen av programmet.

### Skrivskyddade och skrivskyddade områden {#read-only-and-read-write-areas}

Vissa delar av databasen (skrivskyddade delar av databasen) kan vara olika i den gamla och den nya versionen av programmet. De skrivskyddade områdena i databasen är vanligtvis `/app` och `/libs`. I följande exempel används kursiv för att markera skrivskyddade områden, medan fetstil används för skrivskyddade områden.

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

### Indexhantering utan rullande distributioner {#index-management-without-rolling-deployments}

Under utvecklingen, eller när du använder lokala installationer, kan index läggas till, tas bort eller ändras under körningen. Index används när de är tillgängliga. Om ett index ännu inte används i den gamla versionen av programmet skapas det vanligtvis under en schemalagd driftstopp. Samma sak händer när du tar bort ett index eller ändrar ett befintligt index. När du tar bort ett index blir det otillgängligt när det tas bort.

### Indexhantering med rullande distributioner {#index-management-with-rolling-deployments}

Med rullande driftsättningar sker inga driftavbrott. Under en uppdatering körs både den gamla versionen (till exempel version 1) av programmet och den nya versionen (version 2) samtidigt mot samma databas. Om version 1 kräver att ett visst index är tillgängligt får detta index inte tas bort i version 2. Indexet bör tas bort senare, t.ex. i version 3, där det är garanterat att version 1 av programmet inte längre körs. Dessutom bör program skrivas så att version 1 fungerar bra, även om version 2 körs, och om det finns index för version 2.

När uppgraderingen till den nya versionen är klar kan gamla index samlas in av systemet. De gamla indexen kan fortfarande finnas kvar en tid för att påskynda återställningen (om en återställning behövs).

I följande tabell visas fem indexdefinitioner: index `cqPageLucene` används i båda versionerna medan index `damAssetLucene-custom-1` används endast i version 2.

>[!NOTE]
>
>The `<indexName>-custom-<customerVersionNumber>` är nödvändigt för AEM as a Cloud Service att markera som en ersättning för ett befintligt index.

| Index | Index som inte finns i systemet | Använd i version 1 | Använd i version 2 |
|---|---|---|---|
| /oak:index/damAssetLucene | Ja | Ja | Nej |
| /oak:index/damAssetLucene-custom-1 | Ja (anpassad) | Nej | Ja |
| /oak:index/acme.product-custom-1 | Nej | Ja | Nej |
| /oak:index/acme.product-custom-2 | Nej | Nej | Ja |
| /oak:index/cqPageLucene | Ja | Ja | Ja |

Versionsnumret ökas stegvis varje gång indexvärdet ändras. För att undvika att egna indexnamn kolliderar med indexnamnen för själva produkten måste anpassade index och ändringar i färdiga index sluta med `-custom-<number>`.

### Ändringar av färdiga index {#changes-to-out-of-the-box-indexes}

Efter att Adobe har ändrat ett index som inte finns med i kartongen, som &quot;damAssetLucene&quot; eller &quot;cqPageLucene&quot;, ett nytt index med namnet `damAssetLucene-2` eller `cqPageLucene-2` skapas. Om indexet redan har anpassats sammanfogas den anpassade indexdefinitionen med ändringarna i det körklara indexet, vilket visas nedan. Ändringarna sammanfogas automatiskt. Det innebär att du inte behöver göra något om ett index som inte finns i kartongen ändras. Det går dock att anpassa indexet igen senare.

| Index | Index som inte finns i systemet | Använd i version 2 | Använd i version 3 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | Ja (anpassad) | Ja | Nej |
| /oak:index/damAssetLucene-2-custom-1 | Ja (sammanfogas automatiskt från damAssetLucene-custom-1 och damAssetLucene-2) | Nej | Ja |
| /oak:index/cqPageLucene | Ja | Ja | Nej |
| /oak:index/cqPageLucene-2 | Ja | Nej | Ja |

### Aktuella begränsningar {#current-limitations}

Indexhantering stöds bara för index av typen `lucene`, med `compatVersion` ange till `2`. Internt kan andra index konfigureras och användas för frågor, till exempel Elasticsearch-index. Frågor som skrivs mot `damAssetLucene` på AEM as a Cloud Service kan indexet faktiskt köras mot en Elasticsearch-version av detta index. Skillnaden är osynlig för programslutanvändaren, men vissa verktyg, som `explain` funktionen rapporterar ett annat index. Skillnader mellan indexen Lucene och Elasticsearch finns i [Elasticsearch dokumentation i Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). Kunder kan inte och behöver inte konfigurera Elasticsearch-index direkt.

Endast inbyggda analysatorer stöds (det vill säga analysatorer som levereras tillsammans med produkten). Anpassade analysatorer stöds inte.

För bästa prestanda bör index inte vara alltför stora. Den totala storleken för alla index kan användas som vägledning. Om den här storleken ökar med mer än 100 % efter att anpassade index har lagts till och standardindex har justerats i en utvecklingsmiljö, bör anpassade indexdefinitioner justeras. AEM as a Cloud Service kan förhindra användning av index som skulle påverka systemets stabilitet och prestanda negativt.

### Lägga till ett index {#adding-an-index}

Lägga till ett helt anpassat index med namnet `/oak:index/acme.product-custom-1`För att kunna användas i en ny version av programmet och senare måste indexet konfigureras på följande sätt:

`acme.product-1-custom-1`

Den här konfigurationen fungerar genom att en anpassad identifierare försätts i indexnamnet, följt av en punkt (**`.`**). Identifieraren ska vara mellan 2 och 5 tecken lång.

Som ovan säkerställer den här konfigurationen att indexet bara används av den nya versionen av programmet.

### Ändra ett index {#changing-an-index}

När ett befintligt index ändras måste ett nytt index läggas till med den ändrade indexdefinitionen. Ta till exempel det befintliga indexet `/oak:index/acme.product-custom-1` ändras. Det gamla indexet lagras under `/oak:index/acme.product-custom-1`och det nya indexet lagras under `/oak:index/acme.product-custom-2`.

I den gamla versionen av programmet används följande konfiguration:

`/oak:index/acme.product-custom-1`

I den nya versionen av programmet används följande (ändrade) konfiguration:

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>Indexdefinitioner på AEM as a Cloud Service kanske inte helt matchar indexdefinitionerna på en lokal utvecklingsinstans. Utvecklingsinstansen har ingen Tika-konfiguration, medan instanser av AEM as a Cloud Service har en. Om du anpassar ett index med en Tika-konfiguration behåller du Tika-konfigurationen.

### Ångra en ändring {#undoing-a-change}

Ibland behöver du ångra en ändring i en indexdefinition. Detta kan bero på ett oavsiktligt fel eller på att ändringen inte längre behövs. Ta till exempel indexdefinitionen `damAssetLucene-8-custom-3,` som har skapats av misstag och redan har distribuerats. Därför vill du återgå till den tidigare indexdefinitionen, `damAssetLucene-8-custom-2.` För att uppnå detta måste du infoga ett nytt index med namnet `damAssetLucene-8-custom-4` som innehåller definitionen från föregående index, `damAssetLucene-8-custom-2.`

### Ta bort ett index {#removing-an-index}

Följande gäller bara för anpassade index. Produktindex kan inte tas bort eftersom de används av AEM.

Om ett index tas bort i en senare version av programmet kan du definiera ett tomt index (ett tomt index som aldrig används och som inte innehåller några data) med ett nytt namn. I det här exemplet kan du ge det ett namn `/oak:index/acme.product-custom-3`. Det här namnet ersätter indexet `/oak:index/acme.product-custom-2`. Efter `/oak:index/acme.product-custom-2` tas bort av systemet, det tomma indexet `/oak:index/acme.product-custom-3` kan sedan tas bort. Ett exempel på ett sådant tomt index är:

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

Om det inte längre behövs någon anpassning av ett index som inte finns i kartongen måste du kopiera indexdefinitionen. Om du till exempel redan har distribuerat `damAssetLucene-8-custom-3`, men behöver inte längre anpassningar och vill växla tillbaka till standardinställningen `damAssetLucene-8` index, måste du lägga till ett index `damAssetLucene-8-custom-4` som innehåller indexdefinitionen för `damAssetLucene-8`.

## Optimeringar av index och frågor {#index-query-optimizations}

Apache Jackrabbit Oak möjliggör flexibla indexkonfigurationer för att effektivt hantera sökfrågor. Index är särskilt viktiga för större databaser. Se till att alla frågor backas upp av ett lämpligt index. Frågor utan lämpligt index kan läsa tusentals noder, som sedan loggas som en varning.

Se [det här dokumentet](query-and-indexing-best-practices.md) för information om hur frågor och index kan optimeras.
