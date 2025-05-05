---
title: Målväljare för AEM as a Cloud Service
description: Använd AEM målväljare för att visa och välja resurser som du kan använda som en kopia av den ursprungliga resursen.
contentOwner: Adobe
role: Admin, User
exl-id: 7e7bc1ee-d580-4c88-b550-273e8b0620ba
feature: Selectors
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1933'
ht-degree: 0%

---

# Micro-FrontEnd-målväljare {#Overview}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime och Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets-integrering med Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI-utökningsbarhet</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Aktivera Dynamic Media Prime och Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Sök efter bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Metadata - bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamiska media med OpenAPI-funktioner</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets-dokumentation för utvecklare</b></a>
        </td>
    </tr>
</table>

Micro-FrontEnd-målväljaren har ett användargränssnitt i programmet som enkelt kan integreras med [!DNL Experience Manager Assets as a Cloud Service]-databasen. Du kan söka efter eller bläddra till rätt mapp i [!DNL Experience Manager Assets as a Cloud Service]-databasen och överföra resurser från ditt program.

Användargränssnittet Micro-FrontEnd är tillgängligt i programupplevelsen med hjälp av paketet Destination Selector. Alla uppdateringar av paketet importeras automatiskt och den senaste distribuerade målväljaren läses in automatiskt i programmet.

![Översikt](assets/overview-destination-selector.png)

Målväljaren har många fördelar, till exempel:

* Enkel integrering med alla Adobe- eller icke-Adobe-program som använder Vanilla JavaScript-biblioteket.
* Enkelt att underhålla när uppdateringar av målväljarpaketet automatiskt distribueras till målväljaren som är tillgänglig för ditt program. Det finns inga uppdateringar som behövs i programmet för att läsa in de senaste ändringarna.
* Det är enkelt att anpassa eftersom det finns tillgängliga egenskaper som styr hur målväljaren visas i programmet.
* Fulltextsökning för att snabbt navigera till mappar för att överföra resurser från ditt program.
* Möjlighet att skapa mappar, sortera mappar i stigande eller fallande ordning och visa dem i List-, Grid-, Gallery- eller Waterfall-vyn.

Artikelns omfattning är att visa hur du använder målväljaren med ett [!DNL Adobe]-program under Unified Shell eller när du redan har en imsToken genererad för autentisering. Dessa arbetsflöden kallas icke-SUSI-flöde i den här artikeln.

Utför följande uppgifter för att integrera och använda målväljaren med din [!DNL Experience Manager Assets as a Cloud Service]-databas:

* [Integrera målväljaren med Vanilla JS](#integration-with-vanilla-js)
* [Definiera visningsegenskaper för målväljare](#destination-selector-properties)
* [Använd målväljare](#using-destination-selector)

## Integrera målväljaren med Vanilla JS {#integration-with-vanilla-js}

Du kan integrera ett [!DNL Adobe]- eller icke-Adobe-program med [!DNL Experience Manager Assets] som en [!DNL Cloud Service]-databas och välja resurser inifrån programmet.

Integreringen görs genom att du importerar målväljarpaketet och ansluter till Assets as a Cloud Service med Vanilla JavaScript-biblioteket. Du måste redigera en `index.html` eller en lämplig fil i programmet för att kunna -

* Definiera autentiseringsinformationen
* Öppna Assets as a Cloud Service-arkivet
* Konfigurera visningsegenskaperna för målväljaren

Du kan utföra autentisering utan att definiera några IMS-egenskaper om:

* Du integrerar ett [!DNL Adobe]-program i [Enhetligt gränssnitt](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=sv-SE).
* Du har redan en IMS-token genererad för autentisering.

## Förutsättningar {#prerequisites}

Definiera förutsättningarna i filen `index.html` eller en liknande fil i programimplementeringen för att definiera autentiseringsinformationen för att få åtkomst till [!DNL Experience Manager Assets] som en [!DNL Cloud Service]-databas. Förutsättningarna är följande:

* imsOrg
* imsToken
* apikey

## Installation {#installation}

Målväljaren är tillgänglig via både ESM CDN (till exempel version [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)) och version [UMD](https://github.com/umdjs/umd).

I webbläsare som använder **UMD-version** (rekommenderas):

I webbläsare som använder **UMD-version** (rekommenderas):

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

I webbläsare med `import maps`-stöd och **ESM CDN-version**:

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
</script>
```

I Deno/Webpack Module Federation med **ESM CDN version**:

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
```

### Markerat mål {#selected-destination}

Målväljaren tar emot ett återanrop från `onItemSelect`, `onTreeToggleItem` eller `onTreeSelectionChange` med den valda katalogen som innehåller objektet (katalog, bild osv.).

**Schemasyntax**

```
interface SelectedDestination {
  id: string;
  children: SelectedDestination[];
  'repo:repositoryId': string;
  'dc:format': string;
  'repo:assetClass': string;
  'storage:directoryType': string;
  'storage:region': string;
  'repo:name': string;
  'repo:path': string;
  'repo:ancestors': string[];
  'repo:createDate': string;
  'storage:assignee':

  { type: string; id: string; }
  ;
  'repo:assetId': string;
  'aem:published': boolean;
  'repo:createdBy': string;
  'repo:state': string;
  'repo:id': string;
  'repo:modifyDate': string;
  _page:

  { orderBy: string; count: number; };
}
```

I följande tabell beskrivs några av de viktiga egenskaperna för det valda målet.

| Egenskap | Typ | Förklaring |
|---|---|---|
| *repo:databaseId* | string | Unik identifierare för databasen där resursen lagras. |
| *repo:id* | string | Unik identifierare för tillgången. |
| *repo:assetClass* | string | Klassificeringen av resursen (till exempel bild eller video, dokument). |
| *repo:name* | string | Namnet på resursen, inklusive filtillägget. |
| *repo:size* | tal | Resursens storlek i byte. |
| *repo:path* | string | Platsen för resursen i databasen. |
| *repo:överordnade* | `Array<string>` | En array med överordnade objekt för resursen i databasen. |
| *repo:state* | string | Aktuellt läge för resursen i databasen (t.ex. aktiv, borttagen och så vidare). |
| *repo:createdBy* | string | Användaren eller systemet som skapade resursen. |
| *repo:createDate* | string | Datum och tid då tillgången skapades. |
| *repo:modifiedBy* | string | Den användare eller det system som senast ändrade resursen. |
| *repo:modifyDate* | string | Datum och tid då tillgången senast ändrades. |
| *dc:format* | string | Tillgångens format. |
| *_page* | orderBy: string; count: number; | Inkluderar dokumentets sidnummer. |

En fullständig lista över egenskaper och detaljerade exempel finns på [Exempel på målväljarkod](https://github.com/adobe/aem-assets-selectors-mfe-examples).

### Exempel på icke-SUSI-flöde {#non-ims-vanilla}

I det här exemplet visas hur du använder målväljaren med ett icke-SUSI-flöde när du kör ett [!DNL Adobe]-program under Unified Shell eller när du redan har `imsToken` genererats för autentisering.

Inkludera paketet med målväljare i koden med taggen `script`, vilket visas i _raderna 6-15_ i exemplet nedan. När skriptet har lästs in är den globala variabeln `PureJSSelectors` tillgänglig för användning. Definiera målväljaren [egenskaper](#destination-selector-properties) så som visas på _raderna 16-23_. Egenskaperna `imsOrg` och `imsToken` krävs båda för autentisering i icke-SUSI-flöde. Egenskapen `handleSelection` används för att hantera de valda resurserna. Om du vill återge målväljaren anropar du funktionen `renderDestinationSelector` så som anges på _rad 17_. Målväljaren visas i behållarelementet `<div>`, vilket visas på _rader 21 och 22_.

Genom att följa de här stegen kan du använda målväljaren med ett icke-SUSI-flöde i ditt [!DNL Adobe]-program.

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Destination Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>
    <script>
        // get the container element in which we want to render the DestinationSelector component
        const container = document.getElementById('destination-selector-container');
        // imsOrg and imsToken are required for authentication in non-SUSI flow
        const destinationSelectorProps = {
            imsOrg: 'example-ims@AdobeOrg',
            imsToken: "example-imsToken",
            apiKey: "example-apiKey-associated-with-imsOrg",
            handleSelection: (assets: SelectedAssetType[]) => {},
        };
        // Call the `renderDestinationSelector` available in PureJSSelectors globals to render DestinationSelector
        PureJSSelectors.renderDestinationSelector(container, destinationselectorprops);
    </script>
</head>

<body>
    <div id="destination-selector-container" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
    </div>
</body>

</html>
```

Detaljerade exempel finns på [Exempel på målväljarkod](https://github.com/adobe/aem-assets-selectors-mfe-examples).

## Använd egenskaper för målväljare {#destination-selector-properties}

Du kan använda egenskaperna för målväljaren för att anpassa hur målväljaren återges. I följande tabell visas de egenskaper som du kan använda för att anpassa och använda målväljaren:

| Egenskap | Typ | Obligatoriskt | Standard | Beskrivning |
|---|---|---|---|---|
| *imsOrg* | string | Ja | | Adobe Identity Management System (IMS) ID som tilldelas när [!DNL Adobe Experience Manager] etableras som [!DNL Cloud Service] för din organisation. Nyckeln `imsOrg` krävs för att autentisera om organisationen du försöker få åtkomst till är under Adobe IMS eller inte. |
| *imsToken* | string | Nej | | IMS-innehavartoken används för autentisering. `imsToken` krävs inte om du använder SUSI-flödet. Det är dock nödvändigt om du använder ett icke-SUSI-flöde. |
| *apiKey* | string | Nej | | API-nyckel som används för åtkomst till AEM Discovery-tjänsten. `apiKey` krävs inte om du använder SUSI-flödet. Det krävs dock i icke-SUSI-flöden. |
| *rootPath* | string | Nej | /content/dam/ | Mappsökväg som målväljaren visar dina resurser från. `rootPath` kan också användas som inkapsling. Med följande sökväg, `/content/dam/marketing/subfolder/`, tillåter målväljaren inte att du går igenom någon överordnad mapp, utan bara de underordnade mapparna. |
| *hasMore* | boolesk | Nej | | När programmet har mer innehåll att visa kan du använda den här egenskapen för att lägga till en inläsare som läser in innehållet för att göra det synligt i programmet. Det är en indikator som anger att inläsning av innehåll pågår. |
| *orgName* | boolesk | Nej | | Det är namnet på organisationen (troligtvis orgID) som är associerad med AEM |
| *initRepoID* | string | Nej | | Det är sökvägen till resurskatalogen som du vill använda i en inledande standardvy |
| *onCreateFolder* | string | Nej | | Med egenskapen `onCreateFolder` kan du lägga till en ikon som lägger till en ny mapp i programmet. |
| *onConfirm* | string | Nej | | Det är ett återanrop när du trycker på bekräftelseknappen. |
| *confirmDisabled* | string | Nej | | Den här egenskapen styr omkopplaren av bekräftelseknappen. |
| *viewType* | string | Nej | | Egenskapen `viewType` används för att ange de vyer som du använder för att visa resurser. |
| *viewTypeOptions* | string | Nej | | Den här egenskapen är relaterad till egenskapen `viewType`. du kan ange en eller flera vyer för att visa resurser. Tillgängliga viewTypeOptions är: listvy, stödrastervy, gallerivy, vattenfallsvy och trädvy. |
| *itemNameFormatter* | string | Nej | | Med den här egenskapen kan du formatera objektnamnet |
| *i18nSymboler* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | Nej |  | Om OTB-översättningarna inte är tillräckliga för ditt programs behov kan du visa ett gränssnitt genom vilket du kan skicka dina egna anpassade lokaliserade värden via `i18nSymbols`-proppen. Om du skickar ett värde genom det här gränssnittet åsidosätts standardöversättningarna och i stället används dina egna.  Om du vill utföra åsidosättningen måste du skicka ett giltigt [Message Descriptor](https://formatjs.io/docs/react-intl/api/#message-descriptor)-objekt till nyckeln för `i18nSymbols` som du vill åsidosätta. |
| *inlineAlertSetup* | string | Nej | | Det lägger till ett varningsmeddelande som du vill skicka i programmet. Du kan till exempel lägga till ett varningsmeddelande om att du inte har behörighet att komma åt den här mappen. |
| *intl* | Objekt | Nej | | Målväljaren innehåller standardöversättningar, OOTB. Du kan välja översättningsspråk genom att ange en giltig språksträng via `intl.locale`-utkastet. Till exempel: `intl={{ locale: "es-es" }}` </br></br> De språksträngar som stöds följer [ ISO 639 - Koder ](https://www.iso.org/iso-639-language-codes.html) för att representera namn på språkstandarder. </br></br> Lista över språk som stöds: engelska - en-us (standard) spanska - es-es&#39; German - de-de&#39; French - fr-fr&#39; Italian - it-it&#39; Japanese - ja-jp&#39; Korean - ko-kr&#39; Portuguese - pt-br&#39; Chinese (Traditional) - zh-cn&#39; Chinese (Taiwan) - zh-tw |

## Exempel på hur du använder egenskaper för målväljare {#usage-examples}

Du kan definiera målväljarens [egenskaper](#destination-selector-properties) i filen `index.html` om du vill anpassa hur målväljaren visas i programmet.

### Exempel 1: Skapa en mapp i målväljaren

Med målväljaren kan du skapa en mapp för att överföra, flytta eller kopiera resurser på en viss plats.

![create-folder-destination-selector](assets/create-folder-destination-selector.png)

### Exempel 2: Ange vytyp för målväljare

Målväljaren visar en stor mängd resurser i fyra olika vyer, bland annat listvyn, stödrastervyn, gallerivyn och vattenfallsvyn. Om du vill ange standardvytyp kan du använda egenskapen `viewType`. Egenskapen `viewTypeOptions` används tillsammans med egenskapen `viewType` för att ange andra vytyper så att andra alternativ för visningstyp kan visas i en listruta. Ett argument kan användas om du bara vill att ett alternativ ska visas.

![viewtype-destination-selector](assets/viewtype-destination-selector.png)

### Exempel 3: Initiera sökvägen till Assets-mappen

Använd egenskapen `path` för att definiera mappnamnet som visas automatiskt när målväljaren återges.

![initialize-folder-path](assets/initialize-folder-path.png)

## Använda målväljaren {#using-destination-selector}

När målväljaren har konfigurerats och du autentiserats för att använda målväljaren med [!DNL Adobe Experience Manager] som ett [!DNL Cloud Service] -program, kan du välja resurser eller utföra olika åtgärder för att söka efter dina resurser i databasen.

![using-destination-selector](assets/using-destination-selector.png)

* **A**: [Sökfältet](#search-bar)
* **B**: [Sortering](#sorting)
* **C**: [Assets](#assets-repo)
* **D**: [Lägg till suffix eller prefix](#add-suffix-or-prefix)
* **E**: [Skapa ny mapp](#create-new-folder)
* **F**: [Visa](#types-of-view)
* **G**: [Info](#info)
* **H**: [Välj mapp](#select-folder)

### Sökfältet {#search-bar}

Med målväljaren kan du utföra fullständig textsökning av resurser i den valda databasen. Om du till exempel skriver nyckelordet `wave` i sökfältet visas alla resurser med nyckelordet `wave` som nämns i någon av metadataegenskaperna.

### Sortering {#sorting}

Du kan sortera resurser i målväljaren efter namn, dimension eller storlek för en resurs. Du kan också sortera resurserna i stigande eller fallande ordning.

### Assets Repository {#assets-repo}

Med målväljaren kan du även visa valfria databasdata som finns i AEM. Du kan använda egenskapen `repositoryID` för att initiera sökvägen till målmappen som du vill visa vid den första instansen av målväljaren.

### Lägg till suffix eller prefix {#add-suffix-or-prefix}

Det är ett exempel på egenskapen `optionsFormSetup`. Du kan använda den här för att bekräfta markeringen. Den skickas till händelsen `onConfirm`.

### Skapa en mapp {#create-new-folder}

Du kan skapa en mapp i målmappen för [!DNL Adobe Experience Manager] som en [!DNL Cloud Service].

### Typer av vy {#types-of-view}

Med målväljaren kan du visa resursen i fyra olika vyer:

* ![listvy](assets/do-not-localize/list-view.png) [!UICONTROL **listvy**]: I listvyn visas rullningsbara filer och mappar i en enda kolumn.
* ![stödrastervy](assets/do-not-localize/grid-view.png) [!UICONTROL **Stödrastervy**]: I stödrastervyn visas rullningsbara filer och mappar i ett stödraster med rader och kolumner.
* ![gallerivy](assets/do-not-localize/gallery-view.png) [!UICONTROL **Gallerivy**]: Gallerivyn visar filer eller mappar i en centrerad vågrät lista.
* ![vattenfallsvy](assets/do-not-localize/waterfall-view.png) [!UICONTROL **Vattenfallsvy**]: I vattenfallsvyn visas filer eller mappar i form av en Bridge.

### Info {#info}

Med informations- eller informationsikonen kan du visa metadata för den valda resursen. Den innehåller olika detaljer som dimensioner, storlek, beskrivning, sökväg, ändringsdatum och skapad den. Metadatainformationen tillhandahålls när du överför eller kopierar eller skapar en resurs.

### Välj mapp {#select-folder}

Med knappen Välj mapp kan du välja resurser för olika åtgärder som är kopplade till [egenskaper](#destination-selector-properties) i målväljaren.
