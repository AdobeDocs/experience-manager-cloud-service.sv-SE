---
title: Innehållssökning och indexering
description: Innehållssökning och indexering
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '1475'
ht-degree: 2%

---


# Innehållssökning och indexering {#indexing}

## Changes in AEM as a Cloud Service {#changes-in-aem-as-a-cloud-service}

Med AEM som Cloud Service går Adobe från en AEM-instanscentrerad modell till en tjänstbaserad vy med n-x AEM Containers, som drivs av CI/CD-ledningar i Cloud Manager. I stället för att konfigurera och underhålla index för enskilda AEM-instanser måste indexkonfigurationen anges före en distribution. Konfigurationsförändringar i produktionen bryter helt klart CI/CD-reglerna. Detsamma gäller för indexändringar eftersom det kan påverka systemets stabilitet och prestanda om det inte anges testat och omindexerat innan de tas i produktion.

Nedan finns en lista över de viktigaste ändringarna jämfört med AEM 6.5 och tidigare versioner:

1. Användare har inte längre åtkomst till indexhanteraren för en enskild AEM-instans för att felsöka, konfigurera eller underhålla indexering. Det används endast för lokal utveckling och lokal driftsättning.

1. Användare ändrar inte index för en enskild AEM-instans och behöver inte längre bekymra sig om konsekvenskontroller eller omindexering.

1. I allmänhet inleds indexändringar innan produktionen påbörjas för att inte kringgå kvalitetsgatewayer i Cloud Managers CI/CD-pipelines och inte påverka affärs-KPI:er i produktionen.

1. Alla relaterade mätvärden, inklusive sökresultat i produktion, kommer att vara tillgängliga för kunder vid körning för att ge en helhetsbild av ämnen som sökning och indexering handlar om.

1. Kunderna kan skapa varningar efter behov.

1. SRE övervakar systemets hälsa dygnet runt, alla dagar i veckan och kommer att vidta åtgärder efter behov och så tidigt som möjligt.

1. Indexkonfigurationen ändras via distributioner. Ändringar av indexdefinitioner konfigureras på samma sätt som andra innehållsändringar.

1. På en hög nivå på AEM som Cloud Service kommer två uppsättningar index att finnas i och med introduktionen av [Blue-Green-distributionsmodellen](#index-management-using-blue-green-deployments) : en uppsättning för den gamla versionen (blå) och en uppsättning för den nya versionen (grön).

1. Kunderna kan se om indexeringsjobbet är klart på Cloud Managers byggsida och får ett meddelande när den nya versionen är klar att börja trafikera.

1. Begränsningar: För närvarande stöds indexhantering på AEM som en Cloud Service endast för index av typen lucene.

<!-- ## Sizing Considerations {#sizing-considerations}

AEM as a Cloud Service comes with a default capacity model to provide sufficient performance for average web applications. This "average" measure relates to the repository size and even more relevant to the indexing size. If we have reasons to believe that we need extended capacity for a specific customer project, an evaluation with SREs and Engineering will take place to determine the required capacity settings.

AS NOTE: the above is internal for now.

-->

## Användning {#how-to-use}

Definitionen av index kan omfatta tre användningsfall:

1. Lägga till en ny kundindexdefinition
1. Uppdaterar en befintlig indexdefinition. Detta innebär att en ny version av en befintlig indexdefinition läggs till
1. Tar bort ett befintligt index som är överflödigt eller föråldrat.

För båda punkterna 1 och 2 ovan måste du skapa en ny indexdefinition som en del av din anpassade kodbas i respektive Cloud Manager-utgåva. Mer information finns i [Distribuera till AEM som Cloud Service-dokumentation](/help/implementing/deploying/overview.md).

### Förbereder den nya indexdefinitionen {#preparing-the-new-index-definition}

Du måste förbereda ett nytt indexdefinitionspaket som innehåller den faktiska indexdefinitionen, enligt namnmönstret:

`<indexName>[-<productVersion>]-custom-<customVersion>`

som sedan måste gå under `ui.apps/src/main/content/jcr_root`. Underrotmappar stöds inte för närvarande.

<!-- need to review and link info on naming convention from https://wiki.corp.adobe.com/display/WEM/Merging+Customer+and+OOTB+Index+Changes?focusedCommentId=1784917629#comment-1784917629 -->

Paketet från exemplet ovan byggs som `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`.

### Distribuera indexdefinitioner {#deploying-index-definitions}

>[!NOTE]
>
>Det finns ett känt fel med Jackrabbit Filevault Maven Package Plugin version **1.1.0** som inte tillåter tillägg `oak:index` till moduler i `<packageType>application</packageType>`. Använd version **1.0.4** för att undvika detta.

Indexdefinitioner har nu markerats som anpassade och versionsindelade:

* Själva indexdefinitionen (till exempel `/oak:index/ntBaseLucene-custom-1`)

För att kunna distribuera ett index måste därför indexdefinitionen (`/oak:index/definitionname`) levereras via `ui.apps` Git och Cloud Manager-distributionsprocessen.

När den nya indexdefinitionen har lagts till måste det nya programmet distribueras via Cloud Manager. När distributionen är klar startas två jobb som ansvarar för att lägga till (och sammanfoga vid behov) indexdefinitionerna i MongoDB och Azure Segment Store för författare respektive publicering. De underliggande databaserna omindexeras med de nya indexdefinitionerna, innan den blå-gröna växlingen äger rum.

>[!TIP]
>
>Mer information om den paketstruktur som krävs för AEM som Cloud Service finns i dokumentet [AEM Project Structure.](/help/implementing/developing/introduction/aem-project-content-package-structure.md)

## Indexhantering med användning av blå-gröna distributioner {#index-management-using-blue-green-deployments}

### Vad är indexhantering? {#what-is-index-management}

Indexhantering handlar om att lägga till, ta bort och ändra index. Det går snabbt att ändra *definitionen* för ett index, men det tar lång tid att tillämpa ändringen (kallas ofta&quot;skapa ett index&quot; eller&quot;omindexering&quot; för befintliga index). Det är inte omedelbart: databasen måste genomsökas för att data ska kunna indexeras.

### Vad är Blue-Green Deployment? {#what-is-blue-green-deployment}

Blue-Green-driftsättning kan minska driftstoppen. Det ger även inga driftavbrott och ger snabba återställningar. Den gamla versionen av programmet (blå) körs samtidigt som den nya versionen av programmet (grön).

### Skrivskyddade och skrivskyddade områden {#read-only-and-read-write-areas}

Vissa delar av databasen (skrivskyddade delar av databasen) kan vara olika i den gamla (blå) och den nya (gröna) versionen av programmet. De skrivskyddade områdena i databasen är vanligtvis&quot;`/app`&quot; och&quot;`/libs`&quot;. I följande exempel används kursiv för att markera skrivskyddade områden, medan fetstil används för skrivskyddade områden.

* **/**
* */apps (skrivskyddad)*
* **/content**
* */libs (skrivskyddad)*
* **/oak:index**
* **/oak:index/acme**
* **/jcr:system**
* **/system**
* **/var**

Databasens läs- och skrivområden delas mellan alla programversioner, medan det för varje programversion finns en specifik uppsättning `/apps` och `/libs`.

### Indexhantering utan blå-grön driftsättning {#index-management-without-blue-green-deployment}

Under utvecklingen, eller vid användning av lokala installationer, kan index läggas till, tas bort eller ändras under körningen. Index används så snart de är tillgängliga. Om ett index inte ska användas i den gamla versionen av programmet än, skapas indexet vanligtvis under en schemalagd driftstopp. Samma sak händer när du tar bort ett index eller ändrar ett befintligt index. När du tar bort ett index blir det otillgängligt så fort det tas bort.

### Indexhantering med blå-grön driftsättning {#index-management-with-blue-green-deployment}

Med blågröna installationer blir det inga driftstopp. För indexhantering kräver detta dock att index bara används av vissa versioner av programmet. Om du till exempel lägger till ett index i version 2 av programmet, vill du inte att det ska användas av version 1 av programmet än. Det motsatta är fallet när ett index tas bort: ett index som tagits bort i version 2 behövs fortfarande i version 1. När du ändrar en indexdefinition vill vi att den gamla versionen av indexet bara ska användas för version 1 och att den nya versionen av indexet bara ska användas för version 2.

I följande tabell visas fem indexdefinitioner: index `cqPageLucene` används i båda versionerna medan index endast `damAssetLucene-custom-1` används i version 2.

>[!NOTE]
>
>`<indexName>-custom-<customerVersionNumber>` krävs för AEM som Cloud Service för att markera detta som en ersättning för ett befintligt index.

| Index | Index som inte är tillgängligt | Använd i version 1 | Använd i version 2 |
|---|---|---|---|
| /oak:index/damAssetLucene | Ja | Ja | Nej |
| /oak:index/damAssetLucene-custom-1 | Ja (anpassad) | Nej | Ja |
| /oak:index/acmeProduct-custom-1 | Nej | Ja | Nej |
| /oak:index/acmeProduct-custom-2 | Nej | Nej | Ja |
| /oak:index/cqPageLucene | Ja | Ja | Ja |

Versionsnumret ökas stegvis varje gång indexvärdet ändras. För att undvika att egna indexnamn kolliderar med indexnamnen för själva produkten måste anpassade index samt ändringar i index utanför rutan avslutas med `-custom-<number>`.

### Ändringar av färdiga index {#changes-to-out-of-the-box-indexes}

När Adobe ändrar ett körklart index som &quot;damAssetLucene&quot; eller &quot;cqPageLucene&quot; skapas ett nytt index med namnet `damAssetLucene-2` eller `cqPageLucene-2` om indexet redan har anpassats sammanfogas den anpassade indexdefinitionen med ändringarna i det körklara indexet enligt nedan. Ändringarna sammanfogas automatiskt. Det innebär att du inte behöver göra något om ett index som inte finns i kartongen ändras. Det går dock att anpassa indexet igen senare.

| Index | Index som inte är tillgängligt | Använd i version 2 | Använd i version 3 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | Ja (anpassad) | Ja | Nej |
| /oak:index/damAssetLucene-2-custom-1 | Ja (sammanfogas automatiskt från damAssetLucene-custom-1 och damAssetLucene-2) | Nej | Ja |
| /oak:index/cqPageLucene | Ja | Ja | Nej |
| /oak:index/cqPageLucene-2 | Ja | Nej | Ja |

### Begränsningar {#limitations}

Indexhantering stöds för närvarande bara för index av typen `lucene`.

### Ta bort ett index {#removing-an-index}

Om ett index ska tas bort i en senare version av programmet kan du definiera ett tomt index (ett index utan data att indexera) med ett nytt namn. Du kan till exempel ge den ett namn `/oak:index/acmeProduct-custom-3`. Detta ersätter indexvärdet `/oak:index/acmeProduct-custom-2`. När systemet har `/oak:index/acmeProduct-custom-2` tagit bort det tomma indexet `/oak:index/acmeProduct-custom-3` kan det också tas bort.

### Lägga till ett index {#adding-an-index}

Om du vill lägga till ett index med namnet &quot;/oak:index/acmeProduct-custom-1&quot; som ska användas i en ny version av programmet och senare, måste indexet konfigureras enligt följande:

`*mk.*assetLuceneIndex-1-custom-1`

Detta fungerar genom att en anpassad identifierare försätts i indexnamnet, följt av en punkt (**.**). Identifieraren måste vara mellan 1 och 4 tecken lång.

Som ovan säkerställer detta att indexet bara används av den nya versionen av programmet.

### Ändra ett index {#changing-an-index}

När ett befintligt index ändras måste ett nytt index läggas till med den ändrade indexdefinitionen. Anta till exempel att det befintliga indexet &quot;/eke:index/acmeProduct-custom-1&quot; ändras. Det gamla indexet lagras under `/oak:index/acmeProduct-custom-1`och det nya indexet lagras under `/oak:index/acmeProduct-custom-2`.

I den gamla versionen av programmet används följande konfiguration:

`/oak:index/acmeProduct-custom-1`

I den nya versionen av programmet används följande (ändrade) konfiguration:

`/oak:index/acmeProduct-custom-2`