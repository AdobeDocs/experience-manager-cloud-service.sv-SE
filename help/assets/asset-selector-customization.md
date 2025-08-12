---
title: Anpassa programmet Resursväljare
description: Använd funktioner för att anpassa resursväljaren i programmet.
role: Admin, User
exl-id: 0fd0a9f7-8c7a-4c21-9578-7c49409df609
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 0%

---

# Anpassningar av resursväljare {#asset-selector-customization}

Med Resursväljaren kan du anpassa olika komponenter efter inställningar, krav eller funktionella behov. Du kan anpassa följande komponenter: [Micro-Frontend Asset Selector](#overview-asset-selector.md):

* [Anpassa filterpanelen](#customize-filter-panel)
* [Anpassa information i modal vy](#customize-info-in-modal-view)
* [Aktivera eller inaktivera dra och släpp-läge](#enable-disable-drag-and-drop)
* [Val av Assets](#selection-of-assets)
* [Anpassa utgångna resurser](#customize-expired-assets)
* [Sammanhangsberoende anropsfilter](#contextual-invocation-filter)
* [dragOptions, egenskap](#drag-options-property)

Du måste definiera förutsättningarna i filen **index.html** eller en liknande fil i programimplementeringen för att definiera autentiseringsinformationen för att få åtkomst till databasen [!DNL Experience Manager Assets]. När du är klar kan du lägga till kodfragment efter dina behov.

## Anpassa filterpanelen {#customize-filter-panel}

Du kan lägga till följande kodfragment i objektet `assetSelectorProps` för att anpassa filterpanelen:

```
filterSchema: [
    {
    header: 'File Type',
    groupKey: 'TopGroup',
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    {
    label: 'Images',
    value: '<comma separated mimetypes, without space, that denote all images, for e.g., image/>',
    },
    {
    label: 'Videos',
    value: '<comma separated mimetypes, without space, that denote all videos for e.g., video/,model/vnd.mts,application/mxf>'
    }
    ]
    }
    ]
    },
    {
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    { label: 'JPG', value: 'image/jpeg' },
    { label: 'PNG', value: 'image/png' },
    { label: 'TIFF', value: 'image/tiff' },
    { label: 'GIF', value: 'image/gif' },
    { label: 'MP4', value: 'video/mp4' }
    ],
    columns: 3,
    },
    ],
    header: 'Mime Types',
    groupKey: 'MimeTypeGroup',
    },
    {
    fields: [
    {
    element: 'checkbox',
    name: 'property=metadata.application.xcm:keywords.value',
    options: [
    { label: 'Fruits', value: 'fruits' },
    { label: 'Vegetables', value: 'vegetables'}
    ],
    columns: 3,
    },
    ],
    header: 'Food Category',
    groupKey: 'FoodCategoryGroup',
    }
],
```

## Anpassa information i modal vy {#customize-info-in-modal-view}

Du kan anpassa informationsvyn för en resurs genom att klicka på ikonen ![info](assets/info-icon.svg) . Kör koden nedan:

```
// Create an object infoPopoverMap and set the property `infoPopoverMap` with it in assetSelectorProps
const infoPopoverMap = (map) => {
// for example, to skip `path` from the info popover view
let defaultPopoverData = PureJSSelectors.getDefaultInfoPopoverData(map);
return defaultPopoverData.filter((i) => i.label !== 'Path')
};
assetSelectorProps.infoPopoverMap = infoPopoverMap;
```

## Aktivera eller inaktivera dra och släpp-läge {#enable-disable-drag-and-drop}

Lägg till följande egenskaper i `assetSelectorProp` för att aktivera dra och släpp-läget. Om du vill inaktivera dra och släpp ersätter du parametern `true` med `false`.

```
rail: true,
acvConfig: {
dragOptions: {
allowList: {
'*': true,
},
},
selectionType: 'multiple'
}

// the drop handler to be implemented
function drop(e) {
e.preventDefault();
// following helps you get the selected assets – an array of objects.
const data = JSON.parse(e.dataTransfer.getData('collectionviewdata'));
}
```

## Val av Assets {#selection-of-assets}

Den valda resurstypen är en array med objekt som innehåller resursinformationen när funktionerna `handleSelection`, `handleAssetSelection` och `onDrop` används.

Utför följande steg för att konfigurera valet av en eller flera resurser:

```
acvConfig: {
selectionType: 'multiple' // 'single' for single selection
}
// the `handleSelection` callback, always gets you the array of selected assets
```

**Schemasyntax**

```
interface SelectedAsset {
    'repo:id': string;
    'repo:name': string;
    'repo:path': string;
    'repo:size': number;
    'repo:createdBy': string;
    'repo:createDate': string;
    'repo:modifiedBy': string; 
    'repo:modifyDate': string; 
    'dc:format': string; 
    'tiff:imageWidth': number;
    'tiff:imageLength': number;
    'repo:state': string;
    computedMetadata: Record<string, any>;
    _links: {
        'https://ns.adobe.com/adobecloud/rel/rendition': Array<{
            href: string;
            type: string;
            'repo:size': number;
            width: number;
            height: number;
            [others: string]: any;
        }>;
    };
}
```

I följande tabell beskrivs några av de viktiga egenskaperna för det valda resursobjektet.

| Egenskap | Typ | Beskrivning |
|---|---|---|
| *repo:repositoryId* | string | Unik identifierare för databasen där resursen lagras. |
| *repo:id* | string | Unik identifierare för tillgången. |
| *repo:assetClass* | string | Klassificeringen av resursen (till exempel bild eller video, dokument). |
| *repo:name* | string | Namnet på resursen, inklusive filtillägget. |
| *repo:size* | tal | Resursens storlek i byte. |
| *repo:path* | string | Platsen för resursen i databasen. |
| *repo:ancestors* | `Array<string>` | En array med överordnade objekt för resursen i databasen. |
| *repo:state* | string | Aktuellt läge för resursen i databasen (t.ex. aktiv, borttagen och så vidare). |
| *repo:createdBy* | string | Användaren eller systemet som skapade resursen. |
| *repo:createDate* | string | Datum och tid då tillgången skapades. |
| *repo:modifiedBy* | string | Den användare eller det system som senast ändrade resursen. |
| *repo:modifyDate* | string | Datum och tid då tillgången senast ändrades. |
| *dc:format* | string | Resursens format, t.ex. filtyp (t.ex. JPEG, PNG och så vidare). |
| *tiff:imageWidth* | tal | Bredden på en resurs. |
| *tiff:imageLength* | tal | En tillgångs höjd. |
| *computedMetadata* | `Record<string, any>` | Ett objekt som representerar en bucket för alla resursens metadata av alla slag (databas, program eller inbäddade metadata). |
| *_links* | `Record<string, any>` | Hypermedialänkar för den associerade resursen. Innehåller länkar för resurser som metadata och återgivningar. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition>`* | `Array<Object>` | En array med objekt som innehåller information om återgivningar av resursen. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].href>`* | string | URI:n till återgivningen. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].type>`* | string | Återgivningens MIME-typ. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].repo:size>`* | tal | Återgivningens storlek i byte. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].width>`* | tal | Återgivningens bredd. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].height>`* | tal | Återgivningens höjd. |

### Hantera urval av Assets med objektschema {#handling-selection}

Egenskapen `handleSelection` används för att hantera enstaka eller flera markeringar av Assets i Assets Selector. I exemplet nedan anges syntaxen för användning av `handleSelection`.

![handle-selection](assets/handling-selection.png)

### Inaktivera val av Assets {#disable-selection}

Inaktivera markering används för att dölja eller inaktivera att resurser eller mappar kan markeras. Den döljer kryssrutan välj från kortet eller resursen som inte gör att den markeras. Om du vill använda den här funktionen kan du deklarera positionen för en resurs eller mapp som du vill inaktivera i en array. Om du till exempel vill inaktivera valet av en mapp som visas vid den första positionen kan du lägga till följande kod:
`disableSelection: [0]:folder`

Du kan förse arrayen med en lista med MIME-typer (till exempel bild, mapp, fil eller andra MIME-typer, till exempel image/jpeg) som du vill inaktivera. Mime-typerna som du deklarerar mappas till attributen `data-card-type` och `data-card-mimetype` för en resurs.

Dessutom kan Assets med inaktiverad markering dras. Om du vill inaktivera dra och släpp av en viss resurstyp kan du använda egenskapen `dragOptions.allowList`.

Syntaxen för inaktiverad markering är följande:

```
(args)=> {
    return(
        <ASDialogWrapper
            {...args}
            disableSelection={args.disableSelection}
            handleAssetSelection={action('handleAssetSelection')}
            handleSelection={action('handleSelection')}
            selectionType={args.selectionType}
        />
    );
}
```

>[!NOTE]
>
> Om det gäller en resurs är kryssrutan select dold, men om det gäller en mapp går det inte att markera mappen, men navigeringen för den aktuella mappen visas fortfarande.

<!--For a complete list of properties and detailed example, visit [Asset Selector Code Example](https://github.com/adobe/aem-assets-selectors-mfe-examples).-->

## Anpassa utgångna resurser {#customize-expired-assets}

Med Resursväljaren kan du styra hur en resurs som har gått ut används. Du kan anpassa den utgångna resursen med märket **Förfaller snart** som kan hjälpa dig att i förväg få reda på vilka resurser som kommer att förfalla inom 30 dagar från dagens datum. Dessutom kan detta anpassas efter behov. Du kan också välja en resurs som har gått ut på arbetsytan eller vice versa. Du kan anpassa en resurs som har gått ut med hjälp av vissa kodfragment på olika sätt:

<!--{
    getExpiryStatus: function, // to control Expired/Expiring soon badges of the asset
    allowSelectionAndDrag: boolean, // set true to allow the selection of expired assets on canvas, set false, otherwise.
}-->

```
expiryOptions: {
    getExpiryStatus: getExpiryStatus;
}
```

### Val av utgången tillgång {#selection-of-expired-asset}

Du kan anpassa användningen av en resurs som har gått ut så att den antingen kan markeras eller inte kan markeras. Du kan anpassa om du vill tillåta att en resurs dras och släpps på arbetsytan Resursväljaren eller inte. Om du vill göra det använder du följande parametrar för att göra en resurs omarkerbar på arbetsytan:

```
expiryOptions:{
    allowSelectionAndDrop: false;
}
```

<!--
Additionally, To do this, navigate to **[!UICONTROL Disable default expiry behavior]** under the [!UICONTROL Controls] tab and set the boolean value to `true` or `false` as per the requirement. If `true` is selected, you can see the select box over the expired asset, otherwise it remains unselected. You can hover to the info icon of an asset to know the details of an expired asset. 

![Disable default expiry behavior](assets/disable-default-expiry-behavior.png)-->

### Ange varaktigheten för en utgången tillgång {#set-duration-of-expired-asset}

Följande kodfragment hjälper dig att ange märket **Förfaller snart** för de resurser som förfaller inom fem dagar: <!--The `expirationDate` property is used to set the expiration duration of an asset. Refer to the code snippet below:-->

```
/**
  const getExpiryStatus = async (asset) => {
  if (!asset.expirationDate) {
    return null;
  }
  const currentDate = new Date();
  const millisecondsInDay = 1000 * 60 * 60 * 24;
  const fiveDaysFromNow = new Date(value: currentDate.getTime() + 5 * millisecondsInDay);
  const expirationDate = new Date(asset.expirationDate);
  if (expirationDate.getTime() < currentDate.getTime()) {
    return 'EXPIRED';
  } else if (expirationDate.getTime() < fiveDaysFromNow.getTime()) {
    return 'EXPIRING_SOON';
  } else {
    return 'NOT_EXPIRED';
  }
};
```

<!--In the above code snippet, the `getExpiryStatus` function is used to show the **Expiring soon** badge that have expiration date stored in `customExpirationDate`. Additionally, it sets the expiration date of an asset to five days from the current date. The `millisecondsInDay` helps you set expiry of an asset by specifying the time range in milliseconds. You can replace milliseconds with hours directly or customize function as per the requirement. Whereas, the `getTime()` function returns the number of milliseconds for the mentioned date. See [properties](#asset-selector-properties) to know about `expirationDate` property.-->

Se följande exempel för att förstå hur egenskapen fungerar för att hämta aktuellt datum och tid:

```
const currentData = new Date();
currentData.getTime(),
```

returnerar `1718779013959` enligt datumformatet 2024-06-19T06:36:53.959Z.

### Anpassa popup-meddelande för en utgången resurs {#customize-toast-message}

Egenskapen `showToast` används för att anpassa popup-meddelandet som du vill visa för en resurs som har gått ut.

Syntax:

```
{
    type: 'ERROR', 'NEUTRAL', 'INFO', 'SUCCESS',
    message: '<message to be shown>',
    timeout: optional,
}
```

Standardtidsgränsen är 500 millisekunder. Du kan ändra den efter behov. Om du dessutom skickar värdet `timeout: 0` förblir popup öppen tills du klickar på kryssknappen.

Nedan visas ett exempel som visar ett popup-meddelande när det krävs för att inte tillåta val för en mapp och visa ett motsvarande meddelande:

```
const showToast = {
    type: 'ERROR',
    message: 'Folder cannot be selected',
    timeout: 5000,
}
```

Använd följande kodutdrag för att visa popup-meddelanden om hur en resurs som har gått ut används:

```
(args) => {
    const [selectedAssets, setSelectedAssets] = useState([]);
    const [showToast, setShowToast] = React.useState(false);
    const handleAssetSelection = (assets) => {
        let directorySelectedFlag = false;
        const temp = assets.filter((asset) => {
            if (asset['repo:assetClass'] === 'directory') {
                directorySelectedFlag = true;
                setShowToast(true);
            }
            return !(asset['repo:assetClass'] === 'directory');
        });
        if (!directorySelectedFlag) {
            setShowToast(false);
        }
        setSelectedAssets(temp);
    };
    return (
        <ASDialogWrapper
            {...args}
            showToast={showToast ? args.showToast : null}
            selectedAssets={selectedAssets}
            handleAssetSelection={handleAssetSelection}
        />
    );
}
```

## Sammanhangsberoende anropsfilter{#contextual-invocation-filter}

Med resursväljaren kan du lägga till ett taggväljarfilter. Den har stöd för en tagggrupp som kombinerar alla relevanta taggar till en viss tagggrupp. Dessutom kan du välja ytterligare taggar som motsvarar den resurs du söker efter. Dessutom kan du ange standardtagggrupper under det kontextuella anropsfiltret som du använder mest så att de är tillgängliga oavsett var du är.

>
>
> * Du måste lägga till sammanhangsberoende kodfragment för att kunna aktivera taggningsfilter i sökningen.
> * Det är obligatoriskt att använda namnegenskapen som motsvarar tagggruppstypen `(property=xcm:keywords.id=)`.

Syntax:

```
const filterSchema=useMemo(() => {
    return: [
        {
            element: 'taggroup',
            name: 'property=xcm:keywords.id='
        },
    ];
}, []);
```

Om du vill lägga till tagggrupper på filterpanelen måste du lägga till minst en tagggrupp som standard. Använd dessutom kodfragmentet nedan för att lägga till de standardtaggar som är förmarkerade från tagggruppen.

```
export const WithAssetTags = (props) = {
const [selectedTags, setSelectedTags] = useState (
new Set(['orientation', 'color', 'facebook', 'experience-fragments:', 'dam', 'monochrome'])
const handleSelectTags = (selected) => {
setSelectedTags (new Set (selected)) ;
};
const filterSchema = useMemo ((); => {
    return {
        schema: [
            ｛
                fields: [
                    {
                    element: 'checkbox', 
                    name: 'property=xcm:keywords=', 
                    defaultValue: Array. from(selectedTags), 
                    options: assetTags, 
                    orientation: 'vertical',
                    },
                ],
    header: 'Asset Tags', 
    groupkey: 'AssetTagsGroup',
        ],
    },
｝；
}, [selectedTags]);
```

![tagggruppsfilter](assets/tag-group.gif)

## Överför i resursväljaren {#upload-in-asset-selector}

Du kan överföra filer eller mappar till resursväljaren från det lokala filsystemet. Om du vill överföra filer med det lokala filsystemet behöver du i allmänhet använda en överföringsfunktion från ett front-end-program för resursväljare. De `upload` olika kodfragment som krävs för att anropa överföring i resursväljaren omfattar:

* [Grundläggande uppladdning av formulärkodfragment](#basic-upload)
* [Överför konfiguration](#upload-config)
* [Överför med metadata](#upload-with-metadata)
* [Anpassad överföring](#customized-upload)
* [Överför med tredjepartskällor](#upload-using-third-party-source)

### Grundläggande överföringsformulär {#basic-upload}

```
import { AllInOneUpload } from '@assets/upload';
import { TextField, ContextualHelp } from '@adobe/react-spectrum';

const repoId = 'author-p52554-e145207-cmstg.adobeaemcloud.com'
const apiToken = 'eyJhbG....';
const targetUploadPath = '/content/dam/hydrated-assets/cq/as/cq-assets-upload-storybook-testing';

export const UploadExample = () => {
    return (
        <>
            <TextField
                marginStart="size-200"
                width="size-6000"
                isDisabled={true}
                label="Target Upload Path"
                value={targetUploadPath}
                contextualHelp={
                    <ContextualHelp>
                        <Content>Use Storybook Controls panel to change the default upload location</Content>
                    </ContextualHelp>
                }
            />
            <AllInOneUpload
                repositoryId={repoId}
                apiToken={apiToken}
                targetUploadPath={targetUploadPath}
            />
        <>
    )
}
```

### Överför konfiguration {#upload-config}

```
uploadConfig: {
        onUploadStart: action('onUploadStart'),
        onUploadComplete: action('onUploadComplete'),
        metadataSchema: [
            {
                mapToProperty: 'dam:assetStatus',
                value: 'approved',
                element: 'hidden',
            },
        ],
        ... more properties
     }, 
```

*Fler egenskaper är `metadataSchema`, `onMetadataFormChange`, `targetUploadPath`, `hideUploadButton`, `onUploadStart`, `importSettings` `onUploadComplete`, `onFilesChange`,`uploadingPlaceholder`*. Mer information finns i [Egenskaper för resursväljare](#asset-selector-properties.md).

### Överför med metadata {#upload-with-metadata}

```
import { AllInOneUpload } from '@assets/upload';

const repoId = 'author-p52554-e145207-cmstg.adobeaemcloud.com'
const apiToken = 'eyJhbG....';
const targetUploadPath = '/content/dam/hydrated-assets/cq/as/cq-assets-upload-storybook-testing';

/**
 * see https://git.corp.adobe.com/CQ/assets-upload/blob/main/packages/@assets/upload/stories/data/SampleMetadataSchemas.ts
 * for full schema shape used in rendered example below
 */
const metadataSchema = [
    {
        mapToProperty: 'gmo:lineofBusiness',
        label: 'Line of Business',
        placeholder: 'Select one',
        required: true,
        element: 'dropdown',
        dropdownOptions: [
            {
                id: 'corporate',
                name: 'Corporate',
            },
            {
                id: 'digital-media-dme',
                name: 'Digital Media (DMe)',
            },
            {
                id: 'digital-experience-dx',
                name: 'Digital Experience (DX)',
            },
            {
                id: 'business-solutions',
                name: 'Business Solutions',
            },
        ],
    },
    // ... see link above for full schema
    {
        mapToProperty: 'dam:assetStatus',
        value: 'approved',
        // hidden metadata element, this metadata will be applied to the asset without rendering UI for user input
        element: 'hidden',
    },
];

const handleMetadataFormChange = (event: MetadataChangeEvent) => {
    const { property, value } = event;

    console.log({ property, value });
}

const UploadExampleWithMetadataForm = () => {
    return (
        <AllInOneUpload
            repositoryId={repoId}
            apiToken={apiToken}
            targetUploadPath={targetUploadPath}
            metadataSchema={sampleMetadataSchema}
            onMetadataFormChange={handleMetadataFormChange}
        />
    )
}
```

### Anpassad överföring {#customized-upload}

```
const MultipleAllInOneUploadExample = () => {
    const mfeRef = React.useRef<{ iframeRef: { current: HTMLIFrameElement } }>(null);

    return (
        <>
            <Button
                onPress={() => UploadCoordinator.initiateUpload(mfeRef.current?.iframeRef?.current)}
            >
                External Initiate Upload
            </Button>
            <AllInOneUpload
                {...otherProps}
                ref={mfeRef}
            />
        <>
    );
}
```

### Överför med tredjepartskällor {#upload-using-third-party-source}

```
import { useState, useRef } from 'react';
import { AllInOneUpload, UploadCoordinator } from '@assets/upload';
import { Button, Flex, Divider } from '@adobe/react-spectrum';
import { sampleMetadataSchema } from './SampleMetadataSchemas';

const repoId = 'author-p52554-e145207-cmstg.adobeaemcloud.com'
const apiToken = 'eyJhbG....';
const targetUploadPath = '/content/dam/hydrated-assets/cq/as/cq-assets-upload-storybook-testing';

const defaultFiles = [
    new File(['file-content'], 'Controlled File 1'),
    new File(['file-content-with-more'], 'Controlled File 2')
];

const ControlledUploadExample = () => {
    const [controlledFiles, setControlledFiles] = useState<File[]>(defaultFiles)
    const inputRef = React.useRef<HTMLInputElement>(null);

    const handleFileInputChange = useCallback((e: ChangeEvent<HTMLInputElement>) => {
        if (e.target.files) {
            setMyFiles([...e.target.files]);
        }
    }, []);

    return (
        <Flex height="100%" alignItems="center" direction="column">
            <Flex direction="row" alignItems="center" justifyContent="center">
                <Button
                    variant="accent"
                    onPress={() => UploadCoordinator.initiateUpload()}
                    isDisabled={files.length < 1}
                >
                    External Initiate Upload
                </Button>
                <Button
                    variant="secondary"
                    onPress={() => {
                        inputRef.current?.click();
                    }}
                >
                    External Browse files
                </Button>
            </Flex>
            <Divider size="M" marginTop="size-200" />
            <AllInOneUpload
                repositoryId={repoId}
                apiToken={apiToken}
                targetUploadPath={targetUploadPath}
                files={controlledFiles}
                onFilesChange={setControlledFiles}
                hideUploadButton={true}
                metadataSchema={sampleMetadataSchema}
            />
            <input
                ref={inputRef}
                type="file"
                style={{ display: 'none' }}
                onChange={handleFileInputChange}
                multiple={true}
            />
        </Flex>
    )
}
```

### dragOptions, egenskap {#drag-options-property}

```
dragOptions: {
            allowList: {
                '*': true,          // allow all types to be dragged
                'folder': false,    // except those explicitly set to disallow
                'image/jpeg': false // or those with specific mimeTypes
            },
         }
```

>[!MORELIKETHIS]
>
>* [Egenskaper för resursväljare](/help/assets/asset-selector-properties.md)
>* [Integrera resursväljare med olika program](/help/assets/integrate-asset-selector.md)
>* [Egenskaper för resursväljare](/help/assets/asset-selector-properties.md)
>* [Integrera resursväljare med dynamiska media med OpenAPI-funktioner](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
