---
title: SPA Editor - översikt
description: I den här artikeln finns en omfattande översikt över SPA-redigeraren och hur den fungerar. Här finns detaljerade arbetsflöden för samverkan mellan SPA-redigeraren i AEM.
translation-type: tm+mt
source-git-commit: 9b52d94b9f00be30c21dece9b34b0b56056dcbd6
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 0%

---


# SPA Editor - översikt {#spa-editor-overview}

Single page applications (SPAs) can offer compelling experiences for website users. Utvecklare vill kunna skapa webbplatser med SPA-ramverk och författare vill smidigt redigera innehåll i AEM för en webbplats som skapats med sådana ramverk.

SPA-redigeraren är en omfattande lösning för stöd av SPA-program i AEM. Den här sidan ger en översikt över hur stöd för SPA är strukturerat i AEM, hur SPA-redigeraren fungerar och hur SPA-ramverket och AEM synkroniseras.

## Introduktion {#introduction}

Webbplatser som byggts med vanliga SPA-ramverk som React och Angular läser in sitt innehåll via dynamisk JSON och tillhandahåller inte den HTML-struktur som behövs för att AEM Page Editor ska kunna placera redigeringskontroller.

För att göra det möjligt att redigera SPA i AEM måste det finnas en mappning mellan JSON-utdata för SPA och innehållsmodellen i AEM.

Stöd för SPA i AEM introducerar ett tunt JS-lager som interagerar med SPA JS-koden när den läses in i sidredigeraren. Händelser som kan skickas och platsen för redigeringskontrollerna kan aktiveras för redigering i sitt sammanhang. Den här funktionen bygger på API-slutpunktskonceptet för innehållstjänster eftersom innehållet från SPA måste läsas in via innehållstjänster.

Mer information om SPA i AEM finns i följande dokument:

* [SPA Blueprint](blueprint.md) för de tekniska kraven för ett SPA
* [Getting Started with SPAs in AEM using React](getting-started-react.md) for a quick tour of a simple SPA using React
* [Getting Started with SPAs in AEM using Angular](getting-started-angular.md) for a quick tour of a simple SPA using Angular

## Design {#design}

Sidkomponenten för en SPA tillhandahåller inte HTML-elementen för dess underordnade komponenter via JSP- eller HTML-filen. Den här åtgärden har delegerats till SPA-ramverket. Representationen av underordnade komponenter eller modeller hämtas som en JSON-datastruktur från JCR. SPA-komponenterna läggs sedan till på sidan enligt den strukturen. Det här beteendet skiljer sidkomponentens ursprungliga brödkomposition från icke-SPA-motsvarigheter.

### Sidmodellshantering {#page-model-management}

Upplösningen och hanteringen av sidmodellen delegeras till ett angivet `PageModel` bibliotek. SPA måste använda sidmodellbiblioteket för att kunna initieras och redigeras av SPA-redigeraren. Sidmodellbiblioteket som indirekt tillhandahålls AEM sidkomponenten via `cq-react-editable-components` npm. Sidmodellen är en tolk mellan AEM och SPA och måste därför alltid finnas. När sidan har skapats `cq.authoring.pagemodel.messaging` måste ytterligare ett bibliotek läggas till för att kommunikationen med sidredigeraren ska kunna aktiveras.

Om SPA-sidkomponenten ärver från sidhuvudkomponenten finns det två alternativ för att göra klientbibliotekskategorin tillgänglig: `cq.authoring.pagemodel.messaging`

* Om mallen är redigerbar lägger du till den i sidprincipen.
* Eller lägg till kategorierna med hjälp av `customfooterlibs.html`.

För varje resurs i den exporterade modellen kommer SPA att mappa en faktisk komponent som utför återgivningen. Modellen, som representeras som JSON, återges sedan med komponentmappningarna i en behållare.

![Modell- och komponentmappning i SPA](assets/model-component-mapping.png)

>[!CAUTION]
>
>Inkluderingen av `cq.authoring.pagemodel.messaging` kategorin bör begränsas till SPA-redigeraren.

### Kommunikationsdatatyp {#communication-data-type}

När `cq.authoring.pagemodel.messaging` kategorin läggs till på sidan skickas ett meddelande till sidredigeraren för att fastställa JSON-kommunikationens datatyp. När kommunikationsdatatypen är JSON kommunicerar GET-förfrågningarna med Sling Model-slutpunkterna för en komponent. När en uppdatering har gjorts i sidredigeraren skickas JSON-representationen av den uppdaterade komponenten till sidmodellsbiblioteket. Sidmodellbiblioteket informerar sedan SPA om uppdateringar.

![SPA-kommunikation](assets/communication.png)

## Arbetsflöde {#workflow}

Du kan förstå hur interaktionen mellan SPA och AEM ser ut genom att tänka på SPA-redigeraren som en medlare mellan de två.

* Kommunikationen mellan sidredigeraren och SPA görs med JSON i stället för HTML.
* Sidredigeraren tillhandahåller den senaste versionen av sidmodellen till SPA via API:t för iframe och meddelanden.
* Sidmodellhanteraren meddelar redigeraren att den är klar för utgåva och skickar sidmodellen som en JSON-struktur.
* Redigeraren ändrar inte eller har inte ens åtkomst till DOM-strukturen för sidan som författas, utan tillhandahåller den senaste sidmodellen.

![SPA-arbetsflöde](assets/workflow.png)

### Grundläggande arbetsflöde för SPA-redigeraren {#basic-spa-editor-workflow}

Med tanke på de viktigaste elementen i SPA-redigeraren ser det högnivåarbetsflödet för redigering av en SPA i AEM ut för författaren enligt följande.

![Animerat arbetsflöde för SPA](assets/workflow.gif)

1. SPA Editor läses in.
1. SPA läses in i en separat bildruta.
1. SPA begär JSON-innehåll och återger komponenter på klientsidan.
1. SPA Editor identifierar återgivna komponenter och skapar övertäckningar.
1. Författaren klickar på övertäckningen och visar komponentens redigeringsverktygsfält.
1. SPA-redigeraren består av redigeringar med en POST som skickas till servern.
1. SPA Editor begär uppdaterad JSON till SPA Editor, som skickas till SPA med en DOM-händelse.
1. SPA återger den berörda komponenten och uppdaterar dess DOM.

>[!NOTE]
>
>Kom ihåg:
>
>* Det är alltid SPA som ansvarar för visningen.
>* SPA-redigeraren är isolerad från själva SPA-programmet.
>* I produktion (publicering) läses SPA-redigeraren aldrig in.


### Sidredigeringsarbetsflöde för klient-server {#client-server-page-editing-workflow}

Detta är en mer detaljerad översikt över klient-server-interaktionen när du redigerar en SPA.

![Klientserverredigeringsarbetsflöde](assets/client-server-editing.png)

1. SPA initierar sig själv och begär sidmodellen från Sling Model Exporter.
1. Sling Model Exporter begär de resurser som utgör sidan från databasen.
1. Databasen returnerar resurserna.
1. Sling Model Exporter returnerar sidans modell.
1. SPA instansierar sina komponenter baserat på sidmodellen.
1. **6a** Innehållet informerar redigeraren om att det är klart för redigering.

   **6b** Sidredigeraren begär komponentens redigeringskonfigurationer.

   **6c** Sidredigeraren tar emot komponentkonfigurationerna.
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

   **17a** SPA signalerar till sidredigeraren att innehållet är klart.

   **17b** Sidredigeraren förser SPA med komponentkonfigurationer.

   **17c** SPA tillhandahåller uppdaterade komponentkonfigurationer.

### Redigeringsarbetsflöde {#authoring-workflow}

Det här är en mer detaljerad översikt som fokuserar på redigeringsupplevelsen.

![SPA-redigeringsarbetsflöde](assets/authoring-workflow.png)

1. SPA hämtar sidmodellen.
1. **2a** Sidmodellen förser redigeraren med de data som krävs för att skapa.

   **2b** När det meddelas uppdaterar komponentens orchestrator sidans innehållsstruktur.
1. Komponentkoordinatorn efterfrågar mappningen mellan en AEM resurstyp och en SPA-komponent.
1. Komponentkoordinatorn instansierar dynamiskt SPA-komponenten baserat på sidmodellen och komponentmappningen.
1. Sidredigeraren uppdaterar sidmodellen.
1. **6a** Sidmodellen innehåller uppdaterade redigeringsdata för sidredigeraren.

   **6b** Sidmodellen skickar ändringar till komponenten orchestrator.
1. Komponentkoordinatorn hämtar komponentmappningen.
1. Komponentkoordinatorn uppdaterar sidans innehåll.
1. När SPA-filen har uppdaterat innehållet på sidan läses redigeraren in i redigeringsmiljön.

## Krav och begränsningar {#requirements-limitations}

Om du vill att författaren ska kunna använda sidredigeraren för att redigera innehållet i en SPA-fil måste SPA-programmet implementeras för att interagera med AEM SDK för SPA-redigeraren. Se [Komma igång med SPA i AEM med React](getting-started-react.md) -dokument för att få reda på vad du behöver veta för att komma igång.

### Ramverk som stöds {#supported-frameworks}

SPA Editor SDK har stöd för följande minimiversioner:

* Reagera 16.x och uppåt
* Vinkel 6.x och uppåt

Tidigare versioner av dessa ramverk kan fungera med AEM SPA Editor SDK, men stöds inte.

### Ytterligare ramar {#additional-frameworks}

Ytterligare SPA-ramverk kan implementeras för att fungera med AEM SPA Editor SDK. I [SPA-](blueprint.md) designdokumentetfinns information om vilka krav ett ramverk måste uppfylla för att kunna skapa ett ramverksspecifikt lager bestående av moduler, komponenter och tjänster som ska fungera med AEM SPA-redigeraren.

### Använda flera väljare {#multiple-selectors}

Ytterligare anpassade väljare kan definieras och användas som en del av ett SPA som utvecklats för AEM SPA SDK. Detta kräver dock att väljaren är den första väljaren och att tillägget är det som krävs `model` `.json` av JSON-exporteraren.

### Krav för textredigeraren {#text-editor-requirements}

Om du vill använda redigeraren i stället för en textkomponent som skapats i SPA krävs ytterligare konfiguration.

1. Ange ett attribut (det kan vara valfritt) för behållarelementet som innehåller text-HTML. När det gäller WKND SPA-projektet är det ett `<div>` -element och väljaren som har använts är `data-rte-editelement`.
1. Ange konfigurationen `editElementQuery` för motsvarande AEM som pekar på `cq:InplaceEditingConfig` den väljaren, t.ex. `data-rte-editelement`. Detta gör att redigeraren vet vilket HTML-element som omsluter HTML-texten.

Mer information om `editElementQuery` egenskapen och konfigurationen för textredigeraren finns i [Konfigurera textredigeraren.](/help/implementing/developing/extending/rich-text-editor.md)

### Begränsningar {#limitations}

AEM SDK för SPA-redigeraren stöds fullt ut av Adobe och som en ny funktion fortsätter den att förbättras och utökas. Följande AEM stöds ännu inte av SPA-redigeraren:

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
