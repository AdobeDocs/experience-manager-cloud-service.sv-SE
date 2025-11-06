---
title: SPA Editor - översikt
description: Den här artikeln innehåller en omfattande översikt över SPA-redigeraren och hur den fungerar. Här finns detaljerade arbetsflöden för samverkan mellan SPA-redigeraren i AEM.
exl-id: 9814d86e-8d87-4f7f-84ba-6943fe6da22f
feature: Developing
role: Admin, Developer
index: false
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1633'
ht-degree: 0%

---


# SPA Editor - översikt {#spa-editor-overview}

Single page applications (SPAs) can offer compelling experiences for website users. Utvecklare vill kunna skapa webbplatser med SPA-ramverk och författare vill smidigt redigera innehåll i AEM för en webbplats som byggts med sådana ramverk.

SPA Editor är en omfattande lösning för SPA-program i AEM. På den här sidan får du en översikt över hur SPA-stödet är uppbyggt i AEM, hur SPA-redigeraren fungerar och hur SPA-ramverket och AEM synkroniseras.

{{ue-over-spa}}

## Introduktion {#introduction}

Webbplatser som byggts med vanliga SPA-ramverk som React och Angular läser in sitt innehåll via dynamisk JSON och tillhandahåller inte den HTML-struktur som krävs för att AEM Page Editor ska kunna placera redigeringskontroller.

För att göra det möjligt att redigera SPA i AEM krävs en mappning mellan JSON-utdata för SPA och innehållsmodellen i AEM-databasen för att spara ändringar i innehållet.

Stöd för SPA i AEM introducerar ett tunt JS-lager som interagerar med SPA JS-koden när den läses in i sidredigeraren. Händelserna kan skickas och platsen för redigeringskontrollerna kan aktiveras för redigering i sitt sammanhang. Den här funktionen bygger på API-slutpunktskonceptet för innehållstjänster eftersom innehållet från SPA måste läsas in via innehållstjänster.

Mer information om SPA i AEM finns i:

* [SPA-utkast](blueprint.md) för de tekniska kraven för ett SPA.
* [Komma igång med SPA i AEM med React](getting-started-react.md) om du vill få en snabb genomgång av en enkel SPA med React.
* [Komma igång med SPA i AEM med Angular](getting-started-angular.md) om du vill få en snabb genomgång av ett enkelt SPA med Angular.

## Design {#design}

Sidkomponenten för en SPA tillhandahåller inte HTML-elementen för dess underordnade komponenter via JSP- eller HTML-filen. Den här åtgärden har delegerats till SPA-ramverket. Representationen av underordnade komponenter eller modeller hämtas som en JSON-datastruktur från JCR. SPA-komponenterna läggs sedan till på sidan enligt den strukturen. Det här beteendet skiljer sidkomponentens ursprungliga brödkomposition från icke-SPA-motsvarigheter.

### Sidmodellshantering {#page-model-management}

Upplösningen och hanteringen av sidmodellen har delegerats till ett angivet `PageModel`-bibliotek. SPA måste använda sidmodellbiblioteket så att det kan initieras och redigeras av SPA-redigeraren. Sidmodellbiblioteket tillhandahölls indirekt till AEM Page-komponenten via `aem-react-editable-components` npm. Sidmodellen är en tolk mellan AEM och SPA och måste därför alltid finnas. När sidan har skapats måste ytterligare ett bibliotek `cq.authoring.pagemodel.messaging` läggas till för att möjliggöra kommunikation med sidredigeraren.

Om SPA-sidkomponenten ärver från sidhuvudkomponenten finns det två alternativ för att göra klientbibliotekskategorin `cq.authoring.pagemodel.messaging` tillgänglig:

* Om mallen är redigerbar lägger du till den i sidprincipen.
* Eller lägg till kategorierna med `customfooterlibs.html`.

För varje resurs i den exporterade modellen kommer SPA att mappa en faktisk komponent som gör
återgivning. Modellen, som representeras som JSON, återges sedan med komponentmappningarna i en behållare.

![Modell- och komponentmappning i SPA](assets/model-component-mapping.png)

>[!CAUTION]
>
>Inkluderingen av kategorin `cq.authoring.pagemodel.messaging` bör begränsas till SPA-redigerarens kontext.

### Kommunikationsdatatyp {#communication-data-type}

När kategorin `cq.authoring.pagemodel.messaging` läggs till på sidan skickas ett meddelande till sidredigeraren för att fastställa JSON-kommunikationens datatyp. När kommunikationsdatatypen är JSON kommer GET-begäranden att kommunicera med Sling Model-slutpunkterna för en komponent. När en uppdatering har gjorts i sidredigeraren skickas JSON-representationen av den uppdaterade komponenten till sidmodellsbiblioteket. Sidmodellbiblioteket informerar sedan SPA om uppdateringar.

![SPA-kommunikation](assets/communication.png)

## Arbetsflöde {#workflow}

Du kan förstå hur interaktionen mellan SPA och AEM ser ut genom att tänka på SPA-redigeraren som en medlare mellan de båda.

* Kommunikationen mellan sidredigeraren och SPA görs med JSON i stället för HTML.
* Sidredigeraren tillhandahåller den senaste versionen av sidmodellen till SPA via API:t för iframe och meddelanden.
* Sidmodellhanteraren meddelar redigeraren att den är klar för utgåva och skickar sidmodellen som en JSON-struktur.
* Redigeraren ändrar inte eller har inte ens åtkomst till DOM-strukturen för sidan som författas, utan tillhandahåller den senaste sidmodellen.

![SPA-arbetsflöde](assets/workflow.png)

### Grundläggande SPA-redigeringsarbetsflöde {#basic-spa-editor-workflow}

Med tanke på de viktigaste elementen i SPA-redigeraren ser det högnivåarbetsflödet för redigering av en SPA i AEM ut för författaren enligt följande.

![Animerat SPA-arbetsflöde](assets/workflow.gif)

1. SPA Editor läses in.
1. SPA läses in i en separat bildruta.
1. SPA begär JSON-innehåll och återger komponenter på klientsidan.
1. SPA Editor identifierar återgivna komponenter och skapar övertäckningar.
1. Författaren klickar på övertäckningen och visar komponentens redigeringsverktygsfält.
1. SPA Editor består av redigeringar med en POST-begäran till servern.
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

![Redigeringsarbetsflöde för klient-server](assets/client-server-editing.png)

1. SPA initierar sig själv och begär sidmodellen från Sling Model Exporter.
1. Sling Model Exporter begär de resurser som utgör sidan från databasen.
1. Databasen returnerar resurserna.
1. Sling Model Exporter returnerar sidans modell.
1. SPA instansierar sina komponenter baserat på sidmodellen.
1. **6a** Innehållet informerar redigeraren om att det är klart för redigering.

   **6b** Sidredigeraren begär komponentredigeringskonfigurationerna.

   **6c** Sidredigeraren tar emot komponentkonfigurationerna.
1. När författaren redigerar en komponent skickar sidredigeraren en ändringsbegäran till standardservern för POST.
1. Resursen uppdateras i databasen.
1. Den uppdaterade resursen tillhandahålls POST-servern.
1. Standardservern för POST informerar sidredigeraren om att resursen har uppdaterats.
1. Sidredigeraren begär den nya sidmodellen.
1. Resurserna som utgör sidan begärs från databasen.
1. Resurserna som utgör sidan tillhandahålls av databasen till Sling Model Exporter.
1. Den uppdaterade sidmodellen returneras till redigeraren.
1. Sidredigeraren uppdaterar sidmodellreferensen för SPA.
1. SPA uppdaterar sina komponenter baserat på den nya sidmodellreferensen.
1. Komponentkonfigurationerna för sidredigerarna uppdateras.

   **17a** SPA signalerar till sidredigeraren att innehållet är klart.

   **17b** Sidredigeraren tillhandahåller SPA med komponentkonfigurationer.

   **17c** SPA tillhandahåller uppdaterade komponentkonfigurationer.

### Redigeringsarbetsflöde {#authoring-workflow}

Det här är en mer detaljerad översikt som fokuserar på redigeringsupplevelsen.

![Arbetsflöde för SPA-redigering](assets/authoring-workflow.png)

1. SPA hämtar sidmodellen.
1. **2a** Sidmodellen förser redigeraren med de data som krävs för redigering.

   **2b** När du får ett meddelande uppdaterar komponentens koordinator sidans innehållsstruktur.
1. Komponentkoordinatorn efterfrågar mappningen mellan en AEM-resurstyp och en SPA-komponent.
1. Komponentkoordinatorn instansierar dynamiskt SPA-komponenten baserat på sidmodellen och komponentmappningen.
1. Sidredigeraren uppdaterar sidmodellen.
1. **6a** Sidmodellen innehåller uppdaterade redigeringsdata för sidredigeraren.

   **6b** Sidmodellen skickar ändringar till komponenten orchestrator.
1. Komponentkoordinatorn hämtar komponentmappningen.
1. Komponentkoordinatorn uppdaterar sidans innehåll.
1. När SPA-filen har uppdaterat innehållet på sidan läses redigeraren in i redigeringsmiljön.

## Krav och begränsningar {#requirements-limitations}

Om du vill att författaren ska kunna använda sidredigeraren för att redigera innehållet i en SPA-fil måste SPA-programmet implementeras för att interagera med AEM SPA-redigeraren SDK. Se dokumentet [Getting Started with SPAs in AEM using React](getting-started-react.md) för att se om det finns information om hur du kommer igång.

### Ramverk som stöds {#supported-frameworks}

SPA Editor SDK har stöd för följande minimiversioner:

* Reagera 16.x och uppåt
* Angular 6.x och senare

Tidigare versioner av dessa ramverk kan fungera med AEM SPA Editor SDK, men stöds inte.

### Ytterligare ramar {#additional-frameworks}

Ytterligare SPA-ramverk kan implementeras för att fungera med AEM SPA Editor SDK. I dokumentet [SPA-utkast](blueprint.md) finns information om vilka krav ett ramverk måste uppfylla för att kunna skapa ett ramverksspecifikt lager som består av moduler, komponenter och tjänster för att fungera med AEM SPA-redigeraren.

### Använda flera väljare {#multiple-selectors}

Ytterligare anpassade väljare kan definieras och användas som en del av ett SPA-program som utvecklats för AEM SPA SDK. Det här stödet kräver dock att väljaren `model` är den första väljaren och tillägget är `.json` enligt JSON-exportörens krav.

### Krav för textredigeraren {#text-editor-requirements}

Om du vill använda redigeraren i stället för en textkomponent som skapats i SPA krävs ytterligare konfiguration.

1. Ange ett attribut (det kan vara valfritt) för behållarelementet som innehåller texten HTML. För WKND SPA-projektet är det ett `<div>`-element och väljaren som har använts är `data-rte-editelement`.
1. Ange konfigurationen `editElementQuery` för den motsvarande AEM-textkomponentens `cq:InplaceEditingConfig` som pekar på den väljaren, till exempel `data-rte-editelement`. På så sätt kan redigeraren veta vilket HTML-element som omsluter HTML-texten.

Mer information om egenskapen `editElementQuery` och konfigurationen av RTF-redigeraren finns i [Konfigurera RTF-redigeraren](/help/implementing/developing/extending/rich-text-editor.md).

### Begränsningar {#limitations}

AEM SPA Editor SDK har fullt stöd av Adobe och fortsätter att förbättras och utökas. Följande AEM-funktioner stöds ännu inte av SPA-redigeraren:

* Målläge
* ContextHub
* Redigering av infogad bild
* Redigera konfigurationer (till exempel avlyssnare)
* Ångra/Gör om
* Sidskillnader och tidsförskjutning
* Funktioner som utför HTML-omskrivning på serversidan, till exempel [Länkkontroll, ](/help/operations/link-checker.md) CDN-omskrivartjänst, URL-förkortning och så vidare.
* Utvecklarläge
* AEM Launches
