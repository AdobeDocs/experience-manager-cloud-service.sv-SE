---
title: SPA Blueprint
description: I detta dokument beskrivs det allmänna, ramverksoberoende kontrakt som alla SPA-ramverk ska uppfylla för att implementera redigerbara SPA-komponenter inom AEM.
translation-type: tm+mt
source-git-commit: f7d90d9cb41077a3a510f97a9f9f89f4b2b13cd9
workflow-type: tm+mt
source-wordcount: '2058'
ht-degree: 0%

---


# SPA Blueprint {#spa-blueprint}

Om du vill att författaren ska kunna använda AEM SPA-redigerare för att redigera innehållet i en SPA-fil, finns det krav som SPA-programmet måste uppfylla.

## Introduktion {#introdcution}

I det här dokumentet beskrivs det allmänna kontraktet att alla SPA-ramverk ska uppfylla (dvs. typ av AEM stödlager) för att implementera redigerbara SPA-komponenter i AEM.

Om du vill att författaren ska kunna använda AEM Page Editor för att redigera data som exponeras av ett ramverk för ett enkelsidigt program, måste ett projekt kunna tolka modellstrukturen som representerar semantiken för data som lagras för ett program i AEM. För att uppnå detta mål finns två ramverksbaserade bibliotek: och `PageModelManager` och `ComponentMapping`.

>[!NOTE]
>
>Följande krav är ramverksoberoende. Om dessa krav är uppfyllda kan ett ramverksspecifikt lager bestående av moduler, komponenter och tjänster tillhandahållas.
>
>**Dessa krav är redan uppfyllda för ramverken React och Angular i AEM.** Kraven i den här planen är bara relevanta om du vill implementera ett annat ramverk för användning med AEM.

>[!CAUTION]
>
>Även om SPA-funktionerna i AEM är ramverksoberoende stöds för närvarande bara ramverken React och Angular.

## PageModelManager {#pagemodelmanager}

Biblioteket `PageModelManager` tillhandahålls som ett NPM-paket som ska användas av ett SPA-projekt. Det medföljer SPA och fungerar som en datamodellshanterare.

För SPA:s räkning tar det bort och hanterar JSON-strukturen som representerar den faktiska innehållsstrukturen. Den ansvarar också för synkroniseringen med SPA för att meddela när komponenterna ska återges på nytt.

Se NPM-paketet [@adobe/aem-spa-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)

När biblioteket initieras `PageModelManager`läser biblioteket först in den angivna rotmodellen för appen (via parameter, metaegenskap eller aktuell URL). Om biblioteket identifierar att den aktuella sidans modell inte är en del av den rotmodell som hämtas, och tar med den som modell för en underordnad sida.

![Konsolidering av sidmodell](assets/page-model-consolidation.png)

### ComponentMapping {#componentmapping}

Modulen `ComponentMapping` tillhandahålls som ett NPM-paket till frontendprojektet. Det lagrar komponenter i gränssnittet och tillhandahåller ett sätt för SPA att mappa komponenter i gränssnittet till AEM resurstyper. Detta aktiverar en dynamisk upplösning för komponenter när JSON-modellen för programmet analyseras.

Varje objekt i modellen innehåller ett `:type` fält som visar en AEM resurstyp. När den är monterad kan den främre komponenten återge sig själv med det fragment av modellen som den har fått från de underliggande biblioteken.

#### Dynamisk mappning av modell till komponent {#dynamic-model-to-component-mapping}

Mer information om hur den dynamiska mappningen av modell till komponent sker i Javascript SPA SDK för AEM finns i artikeln [Dynamic Model to Component Mapping for SPA](model-to-component-mapping.md).

### Ramverksspecifikt lager {#framework-specific-layer}

Ett tredje lager måste implementeras för varje frontramverk. Detta tredje bibliotek ansvarar för interaktionen med de underliggande biblioteken och erbjuder en serie välintegrerade och lättanvända startpunkter för interaktion med datamodellen.

Resten av detta dokument beskriver kraven för det mellanliggande ramverksspecifika lagret och strävar efter att vara ramverksoberoende. Genom att uppfylla följande krav kan ett ramverksspecifikt lager tillhandahållas för projektkomponenterna för interaktion med de underliggande biblioteken som ansvarar för att hantera datamodellen.

## Allmänna begrepp {#general-concepts}

### Sidmodell {#page-model}

Innehållsstrukturen för sidan lagras i AEM. Sidans modell används för att mappa och instansiera SPA-komponenter. SPA-utvecklarna skapar SPA-komponenter som de mappar till AEM. För att göra detta använder de resurstypen (eller sökvägen till AEM) som en unik nyckel.

SPA-komponenterna måste vara synkroniserade med sidmodellen och uppdateras om innehållet ändras i enlighet med detta. Ett mönster som utnyttjar dynamiska komponenter måste användas för att instansiera komponenter i farten efter den angivna sidmodellstrukturen.

### Metafält {#meta-fields}

Sidmodellen utnyttjar JSON-modellens exporterare, som i sin tur är baserad på API:t för [segmenteringsmodellen](https://sling.apache.org/documentation/bundles/models.html) . De exporterbara snedsättningsmodellerna visar följande fältlista för att de underliggande biblioteken ska kunna tolka datamodellen:

* `:type`: Typ av AEM (standard = resurstyp)
* `:children`: Hierarkiska underordnade för den aktuella resursen. Underordnade är inte en del av den aktuella resursens inre innehåll (kan hittas på objekt som representerar en sida)
* `:hierarchyType`: Hierarkisk typ av en resurs. Den `PageModelManager` aktuella sidtypen stöds

* `:items`: Underordnade innehållsresurser för den aktuella resursen (kapslad struktur, endast i behållare)
* `:itemsOrder`: Ordnad lista över de underordnade. JSON-mappningsobjektet garanterar inte fältordningen. Genom att ha både kartan och den aktuella arrayen får API-konsumenten fördelarna med båda strukturerna
* `:path`: Innehållssökväg för ett objekt (finns i objekt som representerar en sida)

Se även [Komma igång med AEM Content Services.](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-with-aem-headless/overview.html)

### Ramverksspecifik modul {#framework-specific-module}

Separata hänsyn underlättar projektgenomförandet. Därför bör ett npm-specifikt paket tillhandahållas. Det här paketet innehåller information om hur du samlar och exponerar basmoduler, tjänster och komponenter. Dessa komponenter måste kapsla in hanteringslogiken för datamodellen och ge åtkomst till data som projektkomponenten väntar sig. Modulen är också ansvarig för att tillfälligt exponera användbara startpunkter i underliggande bibliotek.

För att underlätta bibliotekens driftskompatibilitet rekommenderar Adobe den ramverksspecifika modulen att paketera följande bibliotek. Om det behövs kan lagret kapsla in och anpassa de underliggande API:erna innan de exponeras för projektet.

* [@adobe/aem-spa-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)
* [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

#### Implementeringar {#implementations}

#### Reagera {#react}

npm-modul: [@adobe/aem-rea-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### Vinkel {#angular}

npm-modul: [@adobe/cq-angular-editable-components](https://www.npmjs.com/package/@adobe/cq-angular-editable-components)

## Huvudsakliga tjänster och komponenter {#main-services-and-components}

Följande enheter bör genomföras i enlighet med de riktlinjer som är specifika för varje ramverk. Implementeringen kan variera mycket beroende på ramverkets arkitektur, men de beskrivna funktionerna måste tillhandahållas.

### Modellprovidern {#the-model-provider}

Projektkomponenter måste delegera åtkomst till en modells fragment till en modellprovider. Modellprovidern ansvarar sedan för att lyssna efter ändringar som gjorts i det angivna fragmentet i modellen och returnerar den uppdaterade modellen till den delegerande komponenten.

För att göra detta måste modellprovidern registrera sig hos [`PageModelManager`](#pagemodelmanager). När en ändring inträffar tar den emot och skickar den uppdaterade informationen till den delegerande komponenten. Egenskapen som gjorts tillgänglig för den delegerande komponenten som ska bära fragmentet av modellen namnges `cqModel`. Implementeringen kan fritt tillhandahålla den här egenskapen till komponenten men bör beakta aspekter som integrering med ramverksarkitekturen, upptäckbarhet och användarvänlighet.

### Komponentens HTML-dekorator {#the-component-html-decorator}

Komponentdekoratorn ansvarar för att dekorera den yttre HTML-koden för elementet i varje komponentinstans med en serie dataattribut och klassnamn som förväntas av sidredigeraren.

#### Komponentdeklaration {#component-declaration}

Följande metadata måste läggas till i det yttre HTML-elementet som skapas av projektkomponenten. De gör att sidredigeraren kan hämta motsvarande redigeringskonfiguration.

* `data-cq-data-path`: Sökväg till resursen i förhållande till `jcr:content`

#### Funktionsdeklaration och platshållare för redigering {#editing-capability-declaration-and-placeholder}

Följande metadata och klassnamn måste läggas till i det yttre HTML-elementet som skapas av projektkomponenten. De gör att sidredigeraren kan erbjuda relaterade funktioner.

* `cq-placeholder`: Klassnamn som identifierar platshållaren för en tom komponent
* `data-emptytext`: Etikett som ska visas av övertäckningen när en komponentinstans är tom

**Platshållare för tomma komponenter**

Varje komponent måste utökas med en funktion som dekorerar det yttre HTML-elementet med dataattribut och klassnamn som är specifika för platshållare och relaterade övertäckningar när komponenten identifieras som tom.

**Om en komponents tomhet**

* Är komponenten logiskt tom?
* Vilken etikett ska visas av övertäckningen när komponenten är tom?

### Behållare {#container}

En behållare är en komponent som ska innehålla och återge underordnade komponenter. För att göra det itererar behållaren över modellens `:itemsOrder``:items` och `:children` egenskaper.

Behållaren hämtar de underordnade komponenterna dynamiskt från arkivet i [`ComponentMapping`](#componentmapping) biblioteket. Behållaren utökar sedan den underordnade komponenten med modellproviderfunktionerna och instansierar den till slut.

### Sidan {#page}

Komponenten utökar `Page` `Container` komponenten. En behållare är en komponent som är avsedd att innehålla och återge underordnade komponenter, inklusive underordnade sidor. För att göra det itererar behållaren över modellens `:itemsOrder`, `:items`och `:children` egenskaper. Komponenten hämtar de underordnade komponenterna dynamiskt från `Page` [`ComponentMapping`](#componentmapping) bibliotekets arkiv. Den `Page` ansvarar för att instansiera underordnade komponenter.

### Responsivt rutnät {#responsive-grid}

Komponenten för responsivt stödraster är en behållare. Den innehåller en specifik variant av modellprovidern som representerar dess kolumner. Det responsiva stödrastret och dess kolumner ansvarar för att dekorera det yttre HTML-elementet i projektets komponent med de specifika klassnamnen som finns i modellen.

Komponenten för responsivt stödraster bör mappas i förväg till den AEM motsvarigheten eftersom komponenten är komplex och sällan anpassad.

#### Specifika modellfält {#specific-model-fields}

* `gridClassNames:` Angivna klassnamn för det responsiva rutnätet
* `columnClassNames:` Angivna klassnamn för den responsiva kolumnen

Se även npm-resursen [@adobe/aem-rea-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### Platshållare för det responsiva rutnätet {#placeholder-of-the-responsive-grid}

SPA-komponenten mappas till en grafisk behållare som t.ex. det responsiva stödrastret och måste lägga till en virtuell underordnad platshållare när innehållet skapas. När innehållet i SPA-filen redigeras av sidredigeraren bäddas innehållet in i redigeraren med en iframe och attributet läggs till i dokumentnoden för det innehållet `data-cq-editor` . När attributet finns med måste behållaren innehålla ett HTMLElement som representerar det område som författaren interagerar med när en ny komponent infogas på sidan. `data-cq-editor`

Till exempel:

```
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>Klassnamnen som används i exemplet krävs för närvarande av sidredigeraren.
>
>* `"new section"`: Anger att det aktuella elementet är behållarens platshållare
>* `"aem-Grid-newComponent"`: Normaliserar komponenten för layoututveckling

>



#### Komponentmappning {#component-mapping}

Det underliggande [`Component Mapping`](#componentmapping) biblioteket och dess `MapTo` funktion kan kapslas in och utökas för att ge funktioner i förhållande till redigeringskonfigurationen som finns bredvid den aktuella komponentklassen.

```
const EditConfig = {

    emptyLabel: 'My Component',

    isEmpty: function() {
        return !this.props || !this.props.cqModel || this.props.cqModel.isEmpty;
    }
};

class MyComponent extends Component {

    render() {
        return <div className={'my-component'}></div>;
    }
}

MapTo('component/resource/path')(MyComponent, EditConfig);
```

I implementeringen ovan utökas projektkomponenten med tomrumsfunktionen innan den registreras i [komponentmappningsarkivet](#componentmapping) . Detta gör du genom att kapsla in och utöka [`ComponentMapping`](#componentmapping) biblioteket för att ge stöd för `EditConfig` konfigurationsobjektet:

```
/**
 * Configuration object in charge of providing the necessary data expected by the page editor to initiate the authoring. The provided data will be decorating the associated component
 *
 * @typedef {{}} EditConfig
 * @property {String} [dragDropName]       If defined, adds a specific class name enabling the drag and drop functionality
 * @property {String} emptyLabel           Label to be displayed by the placeholder when the component is empty. Optionally returns an empty text value
 * @property {function} isEmpty            Should the component be considered empty. The function is called using the context of the wrapper component giving you access to the component model
 */

/**
 * Map a React component with the given resource types. If an {@link EditConfig} is provided the <i>clazz</i> is wrapped to provide edition capabilities on the AEM Page Editor
 *
 * @param {string[]} resourceTypes                      - List of resource types for which to use the given <i>clazz</i>
 * @param {class} clazz                                 - Class to be instantiated for the given resource types
 * @param {EditConfig} [editConfig]                     - Configuration object for enabling the edition capabilities
 * @returns {class}                                     - The resulting decorated Class
 */
ComponentMapping.map = function map (resourceTypes, clazz, editConfig) {};
```

## Arbeta med sidredigeraren {#contract-with-the-page-editor}

Projektkomponenterna måste generera minst följande dataattribut så att redigeraren kan interagera med dem.

* `data-cq-data-path`: Komponentens relativa sökväg enligt `PageModel` (t.ex. `"root/responsivegrid/image"`). Det här attributet ska inte läggas till på sidor.

Sammanfattningsvis, för att sidredigeraren ska kunna tolka som redigerbar, måste en projektkomponent respektera följande kontrakt:

* Ange de förväntade attributen för att associera en komponentinstans i början till en AEM resurs.
* Ange den förväntade serie attribut och klassnamn som gör att tomma platshållare kan skapas.
* Ange de förväntade klassnamnen för att aktivera dra och släpp av resurser.

### Vanlig HTML-elementstruktur {#typical-html-element-structure}

Följande fragment illustrerar den typiska HTML-representationen av en sidinnehållsstruktur. Här är några viktiga punkter:

* Det responsiva rutnätselementet innehåller klassnamn med prefixet `aem-Grid--`
* Det responsiva kolumnelementet innehåller klassnamn som föregås av `aem-GridColumn--`
* Ett responsivt stödraster som också är kolumnen i ett överordnat stödraster kapslas, t.ex. de två föregående prefixen visas inte i samma element
* Element som motsvarar redigerbara resurser har en `data-cq-data-path` egenskap. Se [Kontrakt med sidredigeraren](#contract-wtih-the-page-editor) i det här dokumentet.

```
<div data-cq-data-path="/content/page">
    <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
        <div class="aem-container aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/content/page/jcr:content/root/responsivegrid">
            <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
                <div class="cmp-image cq-dd-image aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/root/responsivegrid/image">
                    <img src="/content/we-retail-spa-sample/react/jcr%3acontent/root/responsivegrid/image.img.jpeg/1512113734019.jpeg">
                </div>
            </div>
        </div>
    </div>
</div>
```

## Navigering och routning {#navigation-and-routing}

Appen äger routningen. Utvecklaren måste först implementera en Navigation-komponent (mappas till en AEM navigeringskomponent). Den här komponenten återger URL-länkar som ska användas tillsammans med en serie vägar som visar eller döljer innehållsfragment.

Det underliggande [`PageModelManager`](#pagemodelmanager) biblioteket och dess [`ModelRouter`](routing.md) modul (aktiverad som standard) ansvarar för förhämtning och ger åtkomst till modellen som är kopplad till en given resurssökväg.

De två entiteterna relaterar till begreppet routning, men [`ModelRouter`](routing.md) är bara ansvariga för att läsa in [`PageModelManager`](#pagemodelmanager) med en datamodell som är strukturerad synkroniserad med det aktuella programtillståndet.

Mer information finns i artikeln [SPA-modellroutning](routing.md) .

## SPA in action {#spa-in-action}

Se hur en enkel SPA fungerar och experimentera med en SPA själv genom att fortsätta med följande dokument:

* [Getting Started with SPAs in AEM Using React](getting-started-react.md).
* [Komma igång med SPA i AEM med hjälp av Vinkel](getting-started-angular.md).

## Ytterligare läsning {#further-reading}

Mer information om SPA i AEM finns i följande dokument:

* [Översikt över](editor-overview.md) SPA-redigeraren för en översikt över SPA-program i AEM och kommunikationsmodellen

