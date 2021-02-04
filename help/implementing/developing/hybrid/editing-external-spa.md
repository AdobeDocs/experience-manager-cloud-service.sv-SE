---
title: Redigera en extern SPA i AEM
description: I det här dokumentet beskrivs de rekommenderade stegen för att överföra en fristående SPA till en AEM, lägga till redigerbara innehållsavsnitt och aktivera redigering.
translation-type: tm+mt
source-git-commit: bb8ab907dbeb422db410328f9c559c6794c16a8f
workflow-type: tm+mt
source-wordcount: '2127'
ht-degree: 0%

---

# Redigera en extern SPA i AEM {#editing-external-spa-within-aem}

När du bestämmer [vilken nivå av integration](/help/implementing/developing/headful-headless.md) du vill ha mellan din externa SPA och AEM behöver du ofta kunna redigera och visa SPA i AEM.

## Översikt {#overview}

I det här dokumentet beskrivs de rekommenderade stegen för att överföra en fristående SPA till en AEM, lägga till redigerbara innehållsavsnitt och aktivera redigering.

## Förutsättningar {#prerequisites}

Förutsättningarna är enkla.

* Kontrollera att en instans av AEM körs lokalt.
* Skapa ett AEM SPA projekt med [den AEM projekttypen.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?#available-properties)
   * Detta kommer att utgöra grunden för det AEM projektet som kommer att uppdateras för att inkludera det externa SPA.
   * För exemplen i det här dokumentet använder vi startpunkten för [WKND-SPA.](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html#spa-editor)
* Ha den fungerande, externa SPA som ni vill integrera till hands.

## Överför SPA till AEM projekt {#upload-spa-to-aem-project}

Först måste du överföra den externa SPA till ditt AEM.

1. Ersätt `src` i `/ui.frontend`-projektmappen med React-programmets `src`-mapp.
1. Inkludera eventuella ytterligare beroenden i programmets `package.json` i `/ui.frontend/package.json`-filen.
   * Kontrollera att SPA SDK-beroenden är av [rekommenderade versioner.](/help/implementing/developing/hybrid/getting-started-react.md#dependencies)
1. Inkludera eventuella anpassningar i mappen `/public`.
1. Inkludera eventuella infogade skript eller format som lagts till i `/public/index.html`-filen.

## Konfigurera SPA {#configure-remote-spa}

Nu när den externa SPA är en del av ditt AEM projekt måste den konfigureras inom AEM.

### Inkludera Adobe SPA SDK-paket {#include-spa-sdk-packages}

För att dra nytta av AEM SPA funktioner finns det beroenden av följande tre paket.

* [`@adobe/aem-react-editable-components`](https://github.com/adobe/aem-react-editable-components)
* [`@adobe/aem-spa-component-mapping`](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)
* [`@adobe/aem-spa-page-model-manager`](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)

`@adobe/aem-spa-page-model-manager` innehåller API:t för att initiera en modellhanterare och hämta modellen från AEM. Den här modellen kan sedan användas för att återge AEM komponenter med API:er från `@adobe/aem-react-editable-components` och `@adobe/aem-spa-component-mapping`.

#### Installation {#installation}

Kör följande npm-kommando för att installera de nödvändiga paketen.

```shell
npm install --save @adobe/aem-spa-component-mapping @adobe/aem-spa-page-model-manager @adobe/aem-react-editable-components
```

### ModelManager-initiering {#model-manager-initialization}

Innan appen återges måste [`ModelManager`](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager) initieras för att hantera skapandet av AEM `ModelStore`.

Detta måste göras i `src/index.js`-filen i programmet eller där programmets rot återges.

För detta kan vi använda `initializationAsync`-API:t från `ModelManager`.

Följande skärmbild visar hur du aktiverar initiering av `ModelManager` i ett enkelt React-program. Den enda begränsningen är att `initializationAsync` måste anropas före `ReactDOM.render()`.

![Initiera ModelManager](assets/external-spa-initialize-modelmanager.png)

I det här exemplet initieras `ModelManager` och en tom `ModelStore` skapas.

`initializationAsync` kan acceptera ett  `options` objekt som en parameter:

* `path` - Vid initiering hämtas modellen vid den definierade sökvägen och lagras i  `ModelStore`. Detta kan användas för att hämta `rootModel` vid initieringen om det behövs.
* `modelClient` - Tillåter att du anger en anpassad klient som ansvarar för att hämta modellen.
* `model` - Ett  `model` objekt som skickas som en parameter som vanligtvis fylls i när  [SSR används.](/help/implementing/developing/hybrid/ssr.md)

### AEM Authorable Leaf Components {#authorable-leaf-components}

1. Skapa/identifiera en AEM som en redigerbar React-komponent ska skapas för. I det här exemplet använder vi WKND-projektets textkomponent.

   ![WKND-textkomponent](assets/external-spa-text-component.png)

1. Skapa en enkel React-textkomponent i SPA. I det här exemplet har en ny fil `Text.js` skapats med följande innehåll.

   ![Text.js](assets/external-spa-textjs.png)

1. Skapa ett konfigurationsobjekt för att ange de attribut som krävs för att aktivera AEM redigering.

   ![Skapa config-objekt](assets/external-spa-config-object.png)

   * `resourceType` är obligatoriskt för att mappa React-komponenten till AEM och aktivera redigering när den öppnas i AEM.

1. Använd adapterfunktionen `withMappable`.

   ![Använd medMappable](assets/external-spa-withmappable.png)

   Den här wrapper-funktionen mappar React-komponenten till AEM `resourceType` som anges i konfigurationen och aktiverar redigeringsfunktioner när den öppnas i AEM. För fristående komponenter hämtas även modellinnehållet för den specifika noden.

   >[!NOTE]
   >
   >I det här exemplet finns det separata versioner av komponenten: AEM inkapslade och oförpackade React-komponenter. Den omslutna versionen måste användas när komponenten används explicit. När komponenten är en del av en sida kan du fortsätta använda standardkomponenten på samma sätt som i SPA.

1. Återge innehåll i komponenten.

   JCR-egenskaperna för textkomponenten visas på följande sätt i AEM.

   ![Egenskaper för textkomponent](assets/external-spa-text-properties.png)

   Dessa värden skickas som egenskaper till den nyligen skapade `AEMText`-komponenten och kan användas för att återge innehållet.

   ```javascript
   import React from 'react';
   import { withMappable } from '@adobe/aem-react-editable-components';
   
   export const TextEditConfig = {
       // Empty component placeholder label
       emptyLabel:'Text', 
       isEmpty:function(props) {
          return !props || !props.text || props.text.trim().length < 1;
       },
       // resourcetype of the AEM counterpart component
       resourceType:'wknd-spa-react/components/text'
   };
   
   const Text = ({ text }) => (<div>{text}</div>);
   
   export default Text;
   
   export const AEMText = withMappable(Text, TextEditConfig);
   ```

   Så här visas komponenten när AEM har konfigurerats.

   ```javascript
   const Text = ({ cqPath, richText, text }) => {
      const richTextContent = () => (
         <div className="aem_text" id={cqPath.substr(cqPath.lastIndexOf('/') + 1)} data-rte-editelement dangerouslySetInnerHTML={{__html: text}}/>
      );
      return richText ? richTextContent() : (<div className="aem_text">{text}</div>);
   };
   ```

   >[!NOTE]
   >
   >I det här exemplet har vi gjort ytterligare anpassningar av den återgivna komponenten för att matcha den befintliga textkomponenten. Detta har dock inget med AEM att göra.

#### Lägg till redigerbara komponenter på sidan {#add-authorable-component-to-page}

När de redigerbara React-komponenterna har skapats kan vi använda dem i hela programmet.

Låt oss ta en exempelsida där vi behöver lägga till en text från WKND-SPA. I det här exemplet vill vi visa texten&quot;Hello World!&quot; på `/content/wknd-spa-react/us/en/home.html`.

1. Ange sökvägen till noden som ska visas.

   * `pagePath`: Sidan som innehåller noden, i vårt exempel  `/content/wknd-spa-react/us/en/home`
   * `itemPath`: Sökväg till noden på sidan, i vårt exempel  `root/responsivegrid/text`
      * Detta består av namnen på de objekt som finns på sidan.

   ![Sökväg till noden](assets/external-spa-path.png)

1. Lägg till en komponent på önskad plats på sidan.

   ![Lägg till komponent på sidan](assets/external-spa-add-component.png)

   Komponenten `AEMText` kan läggas till på önskad plats på sidan med `pagePath`- och `itemPath`-värden angivna som egenskaper. `pagePath` är en obligatorisk egenskap.

#### Verifiera redigering av textinnehåll på AEM {#verify-text-edit}

Vi kan nu testa komponenten på vår AEM som körs.

1. Kör följande Maven-kommando från katalogen `aem-guides-wknd-spa` för att skapa och distribuera projektet till AEM.

```shell
mvn clean install -PautoInstallSinglePackage
```

1. Navigera till `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html` på AEM.

![Redigera SPA i AEM](assets/external-spa-edit-aem.png)

Komponenten `AEMText` är nu AEM.

### AEM sidor {#aem-authorable-pages}

1. Identifiera en sida som ska läggas till för redigering i SPA. I det här exemplet används `/content/wknd-spa-react/us/en/home.html`.
1. Skapa en ny fil (t.ex. `Page.js`) för den redigerbara sidkomponenten. Här kan vi återanvända sidkomponenten som anges i `@adobe/cq-react-editable-components`.
1. Upprepa steg fyra i avsnittet [AEM skrivbara bladkomponenter.](#authorable-leaf-components) Använd wrapper-funktionen  `withMappable` på komponenten.
1. Som tidigare har gjorts använder du `MapTo` på AEM resurstyper för alla underordnade komponenter på sidan.

   ```javascript
   import { Page, MapTo, withMappable } from '@adobe/aem-react-editable-components';
   import Text, { TextEditConfig } from './Text';
   
   export default withMappable(Page);
   
   MapTo('wknd-spa-react/components/text')(Text, TextEditConfig);
   ```

   >[!NOTE]
   >
   >I det här exemplet använder vi den obrutna React-textkomponenten i stället för den omslutna `AEMText` som skapades tidigare. Detta beror på att när komponenten är en del av en sida/behållare och inte fristående, kommer behållaren att hantera rekursiv mappning av komponenten och aktivera redigeringsfunktioner och den extra adaptern behövs inte för varje underordnad.

1. Om du vill lägga till en skrivbar sida i SPA följer du samma steg i avsnittet [Lägg till ändringsbara komponenter på sidan.](#add-authorable-component-to-page) Här kan vi dock hoppa över  `itemPath` egenskapen.

#### Verifiera sidinnehåll på AEM {#verify-page-content}

Verifiera att sidan kan redigeras genom att följa samma steg i avsnittet [Verifiera redigering av textinnehåll på AEM.](#verify-text-edit)

![Redigera en sida i AEM](assets/external-spa-edit-page.png)

Sidan kan nu redigeras på AEM med en layoutbehållare och en underordnad textkomponent.

### Virtuella lövkomponenter {#virtual-leaf-components}

I de föregående exemplen lade vi till komponenter i SPA med befintligt AEM. Det finns emellertid fall där innehåll ännu inte har skapats i AEM, men måste läggas till senare av innehållsförfattaren. För att tillgodose detta kan frontendutvecklaren lägga till komponenter på lämpliga platser i SPA. Komponenterna visar platshållare när de öppnas i redigeraren i AEM. När innehållet har lagts till i platshållarna av innehållsförfattaren skapas noderna i JCR-strukturen och innehållet bevaras. Komponenten som skapas tillåter samma uppsättning åtgärder som de fristående bladkomponenterna.

I det här exemplet återanvänder vi den `AEMText`-komponent som skapades tidigare. Vi vill att ny text ska läggas till under den befintliga textkomponenten på WKND-startsidan. Tillägget av komponenter är detsamma som för normala bladkomponenter. `itemPath` kan dock uppdateras till den sökväg där den nya komponenten måste läggas till.

Eftersom den nya komponenten måste läggas till under den befintliga texten på `root/responsivegrid/text` är den nya sökvägen `root/responsivegrid/{itemName}`.

```html
<AEMText
 pagePath='/content/wknd-spa-react/us/en/home'
 itemPath='root/responsivegrid/text_20' />
```

Komponenten `TestPage` ser ut så här när den virtuella komponenten har lagts till.

![Testa den virtuella komponenten](assets/external-spa-virtual-component.png)

>[!NOTE]
>
>Kontrollera att `AEMText`-komponenten har `resourceType` angivet i konfigurationen för att aktivera den här funktionen.

Du kan nu distribuera ändringarna till AEM genom att följa stegen i avsnittet [Verifiera redigering av textinnehåll på AEM.](#verify-text-edit) En platshållare visas för den  `text_20` nod som inte finns.

![Noden text_20 i aem](assets/external-spa-text20-aem.png)

När innehållsförfattaren uppdaterar den här komponenten skapas en ny `text_20`-nod på `root/responsivegrid/text_20` i `/content/wknd-spa-react/us/en/home`.

![Noden text20](assets/external-spa-text20-node.png)

#### Krav och begränsningar {#limitations}

Det finns ett antal krav på att lägga till virtuella bladkomponenter och vissa begränsningar.

* Egenskapen `pagePath` är obligatorisk för att skapa en virtuell komponent.
* Sidnoden som anges i sökvägen i `pagePath` måste finnas i AEM.
* Namnet på noden som ska skapas måste anges i `itemPath`.
* Komponenten kan skapas på alla nivåer.
   * Om vi anger `itemPath='text_20'` i det föregående exemplet skapas den nya noden direkt under sidan, dvs. `/content/wknd-spa-react/us/en/home/jcr:content/text_20`
* Sökvägen till noden där en ny nod skapas måste vara giltig när den anges via `itemPath`.
   * I det här exemplet måste `root/responsivegrid` finnas så att den nya noden `text_20` kan skapas där.
* Det går bara att skapa lövkomponenter. Virtuell behållare och sida stöds i framtida versioner.

## Ytterligare anpassningar {#additional-customizations}

Om du följde de föregående exemplen går det nu att redigera den externa SPA i AEM. Det finns dock andra aspekter av ditt externa SPA som du kan anpassa ytterligare.

### Rotnods-ID {#root-node-id}

Som standard antar vi att React-programmet återges inuti `div` för element-ID `spa-root`. Om det behövs kan det anpassas.

Anta till exempel att vi har en SPA där programmet återges inuti ett `div`-element-ID `root`. Detta måste återspeglas i tre filer.

1. I `index.js` i React-programmet (eller där `ReactDOM.render()` anropas)

   ![ReactDOM.render() i filen index.js](assets/external-spa-root-index.png)

1. I `index.html` i React-programmet

   ![Programmets index.html](assets/external-spa-index.png)

1. I AEM sidkomponentbrödtext:

   1. Skapa en ny `body.html` för sidkomponenten.

   ![Skapa en ny body.html-fil](assets/external-spa-update-body.gif)

   1. Lägg till det nya rotelementet i den nya `body.html`-filen.

   ![Lägg till rotelementet i body.html](assets/external-spa-add-root.png)

### Redigera en SPA med routning {#editing-react-spa-with-routing}

Om det finns flera sidor i det externa SPA kan det [använda routning för att avgöra vilken sida/komponent som ska återges.](/help/implementing/developing/hybrid/routing.md) Det grundläggande användningsexemplet är att matcha den aktiva URL:en mot sökvägen som anges för ett flöde. Om du vill aktivera redigering för sådana routningsaktiverade program måste sökvägen som ska matchas mot omformas för att rymma AEM information.

I följande exempel har vi ett enkelt React-program med två sidor. Den sida som ska återges bestäms genom att matcha sökvägen som har angetts till routern mot den aktiva URL:en. Om vi till exempel är på `mydomain.com/test` återges `TestPage`.

![Routning i en extern SPA](assets/external-spa-routing.png)

Följande steg krävs för att aktivera redigering i AEM för det här SPA.

1. Identifiera nivån som skulle fungera som AEM.

   * I vårt urval överväger vi wknd-spa-response/us/en som SPA. Det innebär att allt som är före den banan AEM bara sidor/innehåll.

1. Skapa en ny sida på önskad nivå.

   * I det här exemplet är sidan som ska redigeras `mydomain.com/test`. `test` finns i programmets rotsökväg. Detta måste också bevaras när du skapar sidan i AEM. Därför kan vi skapa en ny sida på den rotnivå som definierades i föregående steg.
   * Den nya sidan som skapas måste ha samma namn som sidan som ska redigeras. I det här exemplet för `mydomain.com/test` måste den nya sidan som skapas vara `/path/to/aem/root/test`.

1. Lägg till hjälpredor i SPA.

   * Den nya sidan kommer ännu inte att återge det förväntade innehållet i AEM. Detta beror på att routern förväntar sig en sökväg på `/test` medan den AEM aktiva sökvägen är `/wknd-spa-react/us/en/test`. För att få plats med den AEM delen av URL:en måste vi lägga till några hjälpredor på SPA.

   ![Hjälpprogram för routning](assets/external-spa-router-helper.png)

   * Den `toAEMPath`-hjälp som tillhandahålls av `@adobe/cq-spa-page-model-manager` kan användas för detta. Den omformar sökvägen för routning så att den innehåller AEM delar när programmet är öppet i en AEM. Den godkänner tre parametrar:
      * Sökvägen som krävs för routning
      * Den ursprungliga URL:en för den AEM instansen där SPA redigeras
      * Projektroten på AEM enligt det första steget
   * Dessa värden kan anges som miljövariabler för större flexibilitet.



1. Verifiera redigering av sidan i AEM.

   * Distribuera projektet till AEM och navigera till den nyskapade `test`-sidan. Sidinnehållet återges nu och AEM kan redigeras.

## Ytterligare resurser {#additional-resources}

Följande referensmaterial kan vara användbart för att förstå SPA i samband med AEM.

* [Headless and Headless in AEM](/help/implementing/developing/headful-headless.md)
* [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* [WKND-SPA](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html)
* [Komma igång med SPA i AEM med React](/help/implementing/developing/hybrid/getting-started-react.md)
* [SPA (API-referenser)](/help/implementing/developing/hybrid/reference-materials.md)
* [SPA Blueprint och PageModelManager](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager)
* [SPA](/help/implementing/developing/hybrid/routing.md)
* [SPA- och serveråtergivning](/help/implementing/developing/hybrid/ssr.md)
