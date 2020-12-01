---
title: SPA
description: Den här artikeln innehåller en omfattande översikt över SPA Editor och hur den fungerar. Den innehåller detaljerade arbetsflöden för interaktion med SPA Editor i AEM.
translation-type: tm+mt
source-git-commit: cdd92032c627740c66de7b2f3836fa1dcd2ee2ca
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 0%

---


# Översikt över SPA{#spa-editor-overview}

Single page applications (SPA) can offer compelling experiences for website users. Utvecklare vill kunna skapa webbplatser med SPA ramverk och författare vill smidigt redigera innehåll i AEM för en webbplats som skapats med sådana ramverk.

SPA Editor erbjuder en omfattande lösning för SPA inom AEM. På den här sidan får du en översikt över hur SPA stöds är uppbyggt i AEM, hur SPA redigeraren fungerar och hur SPA ramverk och AEM är synkroniserade.

## Introduktion {#introduction}

Webbplatser som byggts med vanliga SPA ramverk som React och Angular läser in sitt innehåll via dynamisk JSON och tillhandahåller inte den HTML-struktur som krävs för att den AEM sidredigeraren ska kunna placera redigeringskontroller.

Om du vill kunna redigera SPA i AEM måste du mappa mellan JSON-utdata för SPA och innehållsmodellen i den AEM databasen för att kunna spara ändringar i innehållet.

SPA i AEM innehåller ett tunt JS-lager som interagerar med den SPA JS-koden när den läses in i sidredigeraren. Händelser kan skickas med och platsen för redigeringskontrollerna kan aktiveras för redigering i sitt sammanhang. Den här funktionen bygger på API-slutpunktskonceptet för innehållstjänster eftersom innehållet från SPA måste läsas in via innehållstjänster.

Mer information om SPA i AEM finns i följande dokument:

* [SPA ](blueprint.md) Blueprintför de tekniska kraven för en SPA
* [Komma igång med SPA i AEM med ](getting-started-react.md) Reactför en snabb genomgång av en enkel SPA med React
* [Komma igång med SPA i AEM med ](getting-started-angular.md) Angularer för en snabb genomgång av ett enkelt SPA med hjälp av Angular

## Design {#design}

Sidkomponenten för en SPA tillhandahåller inte HTML-elementen för dess underordnade komponenter via JSP- eller HTML-filen. Den här åtgärden har delegerats till SPA ramverk. Representationen av underordnade komponenter eller modeller hämtas som en JSON-datastruktur från JCR. De SPA komponenterna läggs sedan till på sidan enligt den strukturen. Det här beteendet skiljer sidkomponentens ursprungliga brödkomposition från icke-SPA.

### Sidmodellshantering {#page-model-management}

Sidmodellens upplösning och hantering delegeras till ett angivet `PageModel`-bibliotek. SPA måste använda sidmodellbiblioteket för att kunna initieras och redigeras av SPA. Sidmodellbiblioteket som indirekt tillhandahålls AEM sidkomponenten via `aem-react-editable-components` npm. Sidmodellen är en tolk mellan AEM och SPA och måste därför alltid finnas. När sidan har skapats måste ytterligare ett bibliotek `cq.authoring.pagemodel.messaging` läggas till för att kommunikationen med sidredigeraren ska kunna aktiveras.

Om den SPA sidkomponenten ärver från sidhuvudkomponenten finns det två alternativ för att göra klientbibliotekskategorin `cq.authoring.pagemodel.messaging` tillgänglig:

* Om mallen är redigerbar lägger du till den i sidprincipen.
* Eller lägg till kategorierna med `customfooterlibs.html`.

För varje resurs i den exporterade modellen kommer SPA att mappa en faktisk komponent som gör
återgivning. Modellen, som representeras som JSON, återges sedan med komponentmappningarna i en behållare.

![Modell- och komponentmappning i SPA](assets/model-component-mapping.png)

>[!CAUTION]
>
>Inkluderingen av kategorin `cq.authoring.pagemodel.messaging` bör begränsas till kontexten i SPA Editor.

### Kommunikationsdatatyp {#communication-data-type}

När kategorin `cq.authoring.pagemodel.messaging` läggs till på sidan skickas ett meddelande till sidredigeraren för att fastställa JSON-kommunikationens datatyp. När kommunikationsdatatypen är JSON kommunicerar GET-förfrågningarna med Sling Model-slutpunkterna för en komponent. När en uppdatering har gjorts i sidredigeraren skickas JSON-representationen av den uppdaterade komponenten till sidmodellsbiblioteket. Sidmodellbiblioteket informerar sedan SPA om uppdateringar.

![SPA](assets/communication.png)

## Arbetsflöde {#workflow}

Du kan förstå interaktionsflödet mellan SPA och AEM genom att tänka på SPA redigerare som en medlare mellan de två.

* Kommunikationen mellan sidredigeraren och SPA görs med JSON i stället för HTML.
* Sidredigeraren tillhandahåller den senaste versionen av sidmodellen till SPA via API:t för iframe och meddelanden.
* Sidmodellhanteraren meddelar redigeraren att den är klar för utgåva och skickar sidmodellen som en JSON-struktur.
* Redigeraren ändrar inte eller har inte ens åtkomst till DOM-strukturen för sidan som författas, utan tillhandahåller den senaste sidmodellen.

![SPA arbetsflöde](assets/workflow.png)

### Grundläggande SPA Editor-arbetsflöde {#basic-spa-editor-workflow}

Med tanke på de viktigaste elementen i SPA Editor visas arbetsflödet på hög nivå för redigering av en SPA i AEM för författaren enligt följande.

![Animerat SPA](assets/workflow.gif)

1. SPA Editor läses in.
1. SPA läses in i en separat ram.
1. SPA begär JSON-innehåll och återger komponenter på klientsidan.
1. SPA Editor identifierar återgivna komponenter och skapar övertäckningar.
1. Författaren klickar på övertäckningen och visar komponentens redigeringsverktygsfält.
1. SPA redigeraren består av en POST som skickas till servern.
1. SPA Editor begär uppdaterad JSON till SPA Editor, som skickas till SPA med en DOM-händelse.
1. SPA återger den berörda komponenten och uppdaterar dess DOM.

>[!NOTE]
>
>Kom ihåg:
>
>* SPA ansvarar alltid för visningen.
>* SPA är isolerad från själva SPA.
>* I produktion (publicera) läses SPA aldrig in.


### Sidredigeringsarbetsflöde för klient-server {#client-server-page-editing-workflow}

Detta är en mer detaljerad översikt över klient-server-interaktionen när du redigerar en SPA.

![Klientserverredigeringsarbetsflöde](assets/client-server-editing.png)

1. SPA initierar sig själv och begär sidmodellen från Sling Model Exporter.
1. Sling Model Exporter begär de resurser som utgör sidan från databasen.
1. Databasen returnerar resurserna.
1. Sling Model Exporter returnerar sidans modell.
1. SPA instansierar sina komponenter baserat på sidmodellen.
1. **6** a Innehållet informerar redigeraren om att det är klart för redigering.

   **6** bSidredigeraren begär komponentredigeringskonfigurationerna.

   **6** cSidredigeraren tar emot komponentkonfigurationerna.
1. När författaren redigerar en komponent skickar sidredigeraren en ändringsbegäran till standardserverprogrammet för POST.
1. Resursen uppdateras i databasen.
1. Den uppdaterade resursen tillhandahålls servertjänsten för POST.
1. Standardserverpaketet informerar sidredigeraren om att POSTEN har uppdaterats.
1. Sidredigeraren begär den nya sidmodellen.
1. Resurserna som utgör sidan begärs från databasen.
1. Resurserna som utgör sidan tillhandahålls av databasen till Sling Model Exporter.
1. Den uppdaterade sidmodellen returneras till redigeraren.
1. Sidredigeraren uppdaterar sidmodellreferensen för SPA.
1. SPA uppdaterar sina komponenter baserat på den nya sidmodellreferensen.
1. Komponentkonfigurationerna för sidredigerarna uppdateras.

   **17** aSPA signalerar till sidredigeraren att innehållet är klart.

   **17** bSidredigeraren tillhandahåller SPA med komponentkonfigurationer.

   **17** cSPA tillhandahåller uppdaterade komponentkonfigurationer.

### Redigeringsarbetsflöde {#authoring-workflow}

Det här är en mer detaljerad översikt som fokuserar på redigeringsupplevelsen.

![Arbetsflöde för SPA](assets/authoring-workflow.png)

1. SPA hämtar sidmodellen.
1. **2** aSidmodellen förser redigeraren med de data som krävs för redigering.

   **2** bNär det visas ett meddelande uppdaterar komponentens orchestrator sidans innehållsstruktur.
1. Komponentkoordinatorn efterfrågar mappningen mellan en AEM resurstyp och en SPA.
1. Komponentkoordinatorn instansierar SPA dynamiskt baserat på sidmodell och komponentmappning.
1. Sidredigeraren uppdaterar sidmodellen.
1. **6** a Sidmodellen innehåller uppdaterade redigeringsdata för sidredigeraren.

   **6** bSidmodellen skickar ändringar till komponenten orchestrator.
1. Komponentkoordinatorn hämtar komponentmappningen.
1. Komponentkoordinatorn uppdaterar sidans innehåll.
1. När SPA har uppdaterat sidans innehåll läses redigeraren in i redigeringsmiljön.

## Krav och begränsningar {#requirements-limitations}

Om du vill att författaren ska kunna använda sidredigeraren för att redigera innehållet i en SPA måste ditt SPA program implementeras för att interagera med AEM SDK för SPA. Se dokumentet [Getting Started with SPA in AEM using React](getting-started-react.md) för att se om det finns information om hur du kommer igång.

### Ramverk som stöds {#supported-frameworks}

SPA Editor SDK har stöd för följande minimiversioner:

* Reagera 16.x och uppåt
* Vinkel 6.x och uppåt

Tidigare versioner av dessa ramverk kan fungera med AEM SDK för redigeraren, men stöds inte.

### Ytterligare bildrutor {#additional-frameworks}

Ytterligare SPA kan implementeras för att fungera med AEM SPA Editor SDK. Se dokumentet [SPA Blueprint](blueprint.md) för de krav som ett ramverk måste uppfylla för att skapa ett ramverksspecifikt lager bestående av moduler, komponenter och tjänster som ska fungera med AEM SPA.

### Använda flera väljare {#multiple-selectors}

Ytterligare anpassade väljare kan definieras och användas som en del av en SPA som utvecklats för AEM SDK. Det här stödet kräver dock att `model`-väljaren är den första väljaren och tillägget är `.json` enligt JSON-exporteraren.

### Krav för textredigeraren {#text-editor-requirements}

Om du vill använda redigeraren i stället för en textkomponent som skapats i SPA måste du konfigurera ytterligare.

1. Ange ett attribut (det kan vara valfritt) för behållarelementet som innehåller text-HTML. För WKND SPA Project är det ett `<div>`-element och väljaren som har använts är `data-rte-editelement`.
1. Ange konfigurationen `editElementQuery` för motsvarande AEM `cq:InplaceEditingConfig` som pekar på den väljaren, t.ex. `data-rte-editelement`. Detta gör att redigeraren vet vilket HTML-element som omsluter HTML-texten.

Mer information om egenskapen `editElementQuery` och konfigurationen för textredigeraren finns i [Konfigurera textredigeraren.](/help/implementing/developing/extending/rich-text-editor.md)

### Begränsningar {#limitations}

AEM SPA Editor SDK stöds fullt ut av Adobe och som en ny funktion fortsätter den att förbättras och utökas. Följande AEM stöds ännu inte av SPA Editor:

* Målläge
* ContextHub
* Redigering av infogad bild
* Redigera konfigurationer (t.ex. avlyssnare)
* Formatsystem
* Ångra/Gör om
* Sidskillnader och tidsförvrängning
* Funktioner som utför HTML-omskrivning på serversidan, t.ex. Länkkontroll, CDN-omskrivartjänst, URL-förkortning etc.
* Utvecklarläge
* AEM
