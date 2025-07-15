---
title: Egenskaper för resursväljare för anpassning
description: Använd resursväljaren för att söka efter, hitta och hämta resursers metadata och återgivningar i programmet.
role: Admin, User
exl-id: cd5ec1de-36b0-48a5-95c9-9bd22fac9719
source-git-commit: c2ced432f3f0bd393bf5e8e7485c0e973c451b7a
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 0%

---

# Egenskaper för resursväljare {#asset-selector-properties}

Du kan använda egenskaperna för resursväljaren för att anpassa hur resursväljaren återges. I följande tabell visas de egenskaper som du kan använda för att anpassa och använda resursväljaren.

| Egenskap | Typ | Obligatoriskt | Standard | Beskrivning |
|---|---|---|---|---|
| *järnväg* | Boolean | Nej | Falskt | Om den är markerad som `true` återges resursväljaren i en vänsterrälsvy. Om den är markerad som `false` återges resursväljaren i modal vy. |
| *imsOrg* | Sträng | Ja | | Adobe Identity Management System (IMS) ID som tilldelas när [!DNL Adobe Experience Manager] etableras som [!DNL Cloud Service] för din organisation. Nyckeln `imsOrg` krävs för att autentisera om organisationen du försöker få åtkomst till är under Adobe IMS eller inte. |
| *imsToken* | Sträng | Nej | | IMS-innehavartoken används för autentisering. `imsToken` krävs om du använder ett [!DNL Adobe]-program för integreringen. |
| *apiKey* | Sträng | Nej | | API-nyckel som används för åtkomst till AEM Discovery-tjänsten. `apiKey` krävs om du använder en [!DNL Adobe]-programintegrering. |
| *filterSchema* | Array | Nej | | Modell som används för att konfigurera filteregenskaper. Detta är användbart när du vill begränsa vissa filteralternativ i Resursväljaren. |
| *filterFormulärutkast* | Objekt | Nej | | Ange de filteregenskaper som du behöver använda för att förfina sökningen. För! Exempel: MIME-typ JPG, PNG, GIF. |
| *selectedAssets* | Matris `<Object>` | Nej |                 | Ange valt Assets när resursväljaren återges. Det krävs en array med objekt som innehåller en id-egenskap för resurserna. `[{id: 'urn:234}, {id: 'urn:555'}]` En resurs måste till exempel vara tillgänglig i den aktuella katalogen. Om du behöver använda en annan katalog anger du även ett värde för egenskapen `path`. |
| *acvConfig* | Objekt | Nej | | Resurssamlingens visningsegenskap som innehåller objekt med anpassad konfiguration som åsidosätter standardvärden. Den här egenskapen används också med egenskapen `rail` för att aktivera spårningsvisning av resursvyn. |
| *i18nSymboler* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | Nej |                 | Om OTB-översättningarna inte är tillräckliga för ditt programs behov kan du visa ett gränssnitt genom vilket du kan skicka dina egna anpassade, lokaliserade värden via `i18nSymbols`-proppen. Om du skickar ett värde genom det här gränssnittet åsidosätts standardöversättningarna och i stället används dina egna. Om du vill utföra åsidosättningen måste du skicka ett giltigt [Message Descriptor](https://formatjs.io/docs/react-intl/api/#message-descriptor)-objekt till nyckeln för `i18nSymbols` som du vill åsidosätta. |
| *intl* | Objekt | Nej | | Resursväljaren innehåller OOTB-standardöversättningar. Du kan välja översättningsspråk genom att ange en giltig språksträng via `intl.locale`-utkastet. Till exempel: `intl={{ locale: "es-es" }}` </br></br> De språksträngar som stöds följer [ ISO 639 - Koder ](https://www.iso.org/iso-639-language-codes.html) för att representera namn på språkstandarder. </br></br> Lista över språk som stöds: engelska - en-us (standard) spanska - es-es&#39; German - de-de&#39; French - fr-fr&#39; Italian - it-it&#39; Japanese - ja-jp&#39; Korean - ko-kr&#39; Portuguese - pt-br&#39; Chinese (Traditional) - zh-cn&#39; Chinese (Taiwan) - zh-tw |
| *databaseId* | Sträng | Nej | &#39; | Databas från vilken resursväljaren läser in innehållet. |
| *additionalAemSolutions* | `Array<string>` | Nej | [ ] | Här kan du lägga till en lista med ytterligare AEM-databaser. Om ingen information anges i den här egenskapen beaktas endast mediebibliotek eller AEM Assets-databaser. |
| *hideTreeNav* | Boolean | Nej |  | Anger om navigeringssidofältet för resursträd ska visas eller döljas. Den används endast i modal vy och därför har den här egenskapen ingen effekt i järnvägsvy. |
| *onDrop* | Funktion | Nej | | Funktionen för att släppa används för att dra en resurs och släppa den på ett särskilt släppområde. Det möjliggör interaktiva användargränssnitt där resurser kan flyttas och bearbetas sömlöst. |
| *dropOptions* | `{allowList?: Object}` | Nej | | Konfigurerar släppningsalternativ med tillåtelselista. |
| *colorScheme* | Sträng | Nej | | Konfigurera temat (`light` eller `dark`) för resursväljaren. |
| *Tema* | Sträng | Nej | Standard | Använd temat för resursväljarprogrammet mellan `default` och `express`. Det har även stöd för `@react-spectrum/theme-express`. |
| *handleSelection* | Funktion | Nej | | Anropas med en array med tillgångsobjekt när resurser har valts och knappen `Select` på spärren klickas. Den här funktionen anropas bara i modal vy. Använd funktionerna `handleAssetSelection` eller `onDrop` för spårvyn. Exempel: <pre>handleSelection=(assets: Asset[])=> {...}</pre> Mer information finns i [Val av resurser](/help/assets/asset-selector-customization.md#selection-of-assets). |
| *handleAssetSelection* | Funktion | Nej | | Anropas med en array med objekt när resurserna markeras eller avmarkeras. Detta är användbart när du vill lyssna efter resurser när användaren väljer dem. Exempel: <pre>handleSelection=(assets: Asset[])=> {...}</pre> Mer information finns i [Val av resurser](/help/assets/asset-selector-customization.md#selection-of-assets). |
| *onClose* | Funktion | Nej | | Anropas när knappen `Close` i modal vy trycks ned. Detta anropas bara i vyn `modal` och ignoreras i vyn `rail`. |
| *onFilterSubmit* | Funktion | Nej | | Anropas med filterobjekt när användaren ändrar olika filtervillkor. |
| *selectionType* | Sträng | Nej | Enkelt | Konfiguration för `single` eller `multiple` urval av resurser åt gången. |
| *dragOptions.tillåtelselista* | boolesk | Nej | | Egenskapen används för att tillåta eller neka att resurser som inte kan markeras dras. Se [egenskapen dragOptions](/help/assets/asset-selector-customization.md#drag-options-property) |
| *aemTierType* | Sträng | Nej |  | Du kan välja om du vill visa resurser från leveransnivå, författarnivå eller både och. <br><br> Syntax: `aemTierType:[0]: "author" 1: "delivery"` <br><br> Om till exempel båda `["author","delivery"]` används visas alternativ för både författare och leverans i databasväljaren. |
| *handleNavigateToAsset* | Funktion | Nej | | Det är en återanropsfunktion som hanterar markering av en resurs. |
| *noWrap* | Boolean | Nej | | Egenskapen *noWrap* hjälper till att återge resursväljaren på sidopanelen. Om den här egenskapen inte nämns återges *dialogvyn* som standard. |
| *dialogSize* | liten, medelstor, stor, helskärmsbild eller helskärmsövergång | Sträng | Valfritt | Du kan styra layouten genom att ange dess storlek med de angivna alternativen. |
| *colorScheme* | Ljus eller mörk | Nej | | Den här egenskapen används för att ange temat för ett resursväljarprogram. Du kan välja mellan ljust eller mörkt tema. |
| *filterRepoList* | Funktion | Nej |  | Du kan använda callback-funktionen `filterRepoList` som anropar Experience Manager-databasen och returnerar en filtrerad lista med databaser. |
| *expirationOptions* | Funktion | | | Du kan använda mellan följande två egenskaper: **getExpiryStatus** som anger status för en utgången resurs. Funktionen returnerar `EXPIRED`, `EXPIRING_SOON` eller `NOT_EXPIRED` baserat på förfallodatumet för en resurs som du anger. Se [anpassa utgångna resurser](/help/assets/asset-selector-customization.md#customize-expired-assets). Dessutom kan du använda **allowSelectionAndDrag** där värdet för funktionen antingen kan vara `true` eller `false`. När värdet är `false` kan resursen som har gått ut inte markeras eller dras på arbetsytan. |
| *showToast* | | Nej | | Det gör det möjligt för resursväljaren att visa ett anpassat popup-meddelande för den utgångna resursen. |
| *uploadConfig* | Objekt | | | Det är ett objekt som innehåller en anpassad konfiguration för överföringen. Se [överföringskonfiguration](#asset-selector-customization.md#upload-config) för användbarhet. |
| *metadataSchema* | Array | Nej | | Den här egenskapen är kapslad under egenskapen `uploadConfig`. Lägg till en array med fält som du anger för att samla in metadata från användaren. Med den här egenskapen kan du även använda dolda metadata som tilldelas till en resurs automatiskt men inte är synliga för användaren. |
| *onMetadataFormChange* | Återanropsfunktion | Nej | | Den här egenskapen är kapslad under egenskapen `uploadConfig`. Det består av `property` och `value`. `Property` är lika med *mapToProperty* för fältet som skickas från *metadataSchema* vars värde uppdateras. `value` är lika med det nya värdet som anges som indata. |
| *targetUploadPath* | Sträng |  | `"/content/dam"` | Den här egenskapen är kapslad under egenskapen `uploadConfig`. Målets överföringssökväg för de filer som har standardvärdet root of the assets database. |
| *hideUploadButton* | Boolean | | Falskt | Den ser till att den interna överföringsknappen döljs eller inte. Den här egenskapen är kapslad under egenskapen `uploadConfig`. |
| *onUploadStart* | Funktion | Nej |  | Det är en callback-funktion som används för att skicka överföringskällan till Dropbox, OneDrive eller lokal. Syntaxen är `(uploadInfo: UploadInfo) => void`. Den här egenskapen är kapslad under egenskapen `uploadConfig`. |
| *importSettings* | Funktion | | | Det aktiverar stöd för import av resurser från tredje parts källa. `sourceTypes` använder en array med de importkällor som du vill aktivera. Källorna som stöds är Onedrive och Dropbox. Syntaxen är `{ sourceTypes?: ImportSourceType[]; apiKey?: string; }`. Dessutom är den här egenskapen kapslad under egenskapen `uploadConfig`. |
| *onUploadComplete* | Funktion | Nej | | Det är en återanropsfunktion som används för att skicka filöverföringsstatus bland lyckade, misslyckade eller duplicerade filer. Syntaxen är `(uploadStats: UploadStats) => void`. Dessutom är den här egenskapen kapslad under egenskapen `uploadConfig`. |
| *onFilesChange* | Funktion | Nej | | Den här egenskapen är kapslad under egenskapen `uploadConfig`. Det är en återanropsfunktion som används för att visa hur överföringen fungerar när en fil ändras. Den skickar den nya arrayen med filer som väntar på överföring och källtypen för överföringen. Source-typen kan vara null om fel uppstår. Syntaxen är `(newFiles: File[], uploadType: UploadType) => void` |
| *uploadingPlaceholder* | Sträng | | | Det är en platshållarbild som ersätter metadataformuläret när en överföring av resursen initieras. Syntaxen är `{ href: string; alt: string; }`. Dessutom är den här egenskapen kapslad under egenskapen `uploadConfig`. |
| *featureSet* | Array | Sträng | | Egenskapen `featureSet:[ ]` används för att aktivera eller inaktivera en viss funktion i resursväljarprogrammet. Om du vill aktivera komponenten eller en funktion kan du skicka ett strängvärde i arrayen eller lämna arrayen tom för att inaktivera komponenten.  Om du till exempel vill aktivera överföringsfunktioner i resursväljaren använder du syntaxen `featureSet:[0:"upload"]`. På samma sätt kan du använda `featureSet:[0:"collections"]` för att aktivera samlingar i resursväljaren. Använd dessutom `featureSet:[0:"detail-panel"]` för att aktivera [informationspanelen](overview-asset-selector.md#asset-details-and-metadata) för en resurs. Syntaxen är `featureSet:["upload", "collections", "detail-panel"]` om du vill använda de här funktionerna tillsammans. |

<!--
| *selectedRendition* | Object | | | This property allows users to define and control which renditions of an asset are displayed when the panel is accessed. This customization enhances user experience by filtering out unnecessary renditions and showcasing only the most relevant renditions. For example, `CopyUrlHref` allows you to use Dynamic Media renditions in your Asset Selector application (delivery URL). |
| *featureSet* | Array | String | | The `featureSet:[ ]` property is used to enable or disable a particular functionaly in the Asset Selector application. To enable the component or a feature, you can pass a string value in the array or leave the array empty to disable that component. For example, you want to enable upload functionality in the Asset Selector, use the syntax `featureSet:[0:"upload"]`. Similarly, you can use `featureSet:[0:"collections"]` to enable collections in the Asset Selector. Addidionally, use `featureSet:[0:"detail-panel"]` to enable [details panel](overview-asset-selector.md#asset-details-and-metadata) of an asset. Also, `featureSet:[0:"dm-renditions"]` to show Dynamic Media renditions of an asset.|
| *rootPath* | String | No | /content/dam/ | Folder path from which Asset Selector displays your assets. `rootPath` can also be used in the form of encapsulation. For example, given the following path, `/content/dam/marketing/subfolder/`, Asset Selector does not allow you to traverse through any parent folder, but only displays the children folders. |
| *path* | String | No | | Path that is used to navigate to a specific directory of assets when the Asset Selector is rendered. |
| *expirationDate* | Function | No | | This function is used to set the usability period of an asset. |
| *disableDefaultBehaviour* | Boolean | No | False | It is a function that is used to enable or disable the selection of an expired asset. You can customize the default behavior of an asset that is set to expire. See [customize expired assets](/help/assets/asset-selector-customization.md#customize-expired-assets). |
-->

>[!MORELIKETHIS]
>
>* [Anpassningar av resursväljare](/help/assets/asset-selector-customization.md)
>* [Integrera resursväljare med olika program](/help/assets/integrate-asset-selector.md)
>* [Integrera resursväljare med dynamiska media med OpenAPI-funktioner](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
>* [Integrera resursväljaren med program från tredje part](/help/assets/integrate-asset-selector-non-adobe-app.md)
