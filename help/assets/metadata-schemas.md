---
title: Metadata-scheman definierar layouten för metadataegenskapssida
description: Metadata-schemat definierar layouten för egenskapssidan och de metadataegenskaper som visas för resurser. Lär dig hur du skapar anpassade metadatamatcheman, redigerar metadatamatchema och hur du använder metadatamatchema på resurser.
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: 9e94afeb-1c54-4653-bf52-b0910c0cb6c1
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '2543'
ht-degree: 5%

---

# Metadata-scheman {#metadata-schemas}

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

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-schemas.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |

Organisationer har en metadatamodell som förbättrar tillgångsidentifiering, användning, interoperabilitet och så vidare. Korrigera metadataprogram är akrossbart för att underhålla metadatadrivna arbetsflöden och processer. Om du vill följa en metadatastrategi och standarder för hela organisationen kan du använda metadatamodeller som hjälper DAM-användare att anpassa sig. Med [!DNL Adobe Experience Manager] kan du enkelt och flexibelt skapa, underhålla och använda metadatamodeller.

I [!DNL Adobe Experience Manager Assets] innehåller scheman specifika fält för specifik information som ska fyllas i. Den innehåller även layoutinformation för att visa metadatafält på ett användarvänligt sätt. Metadataegenskaperna innehåller titel, beskrivning, MIME-typer, taggar med mera. Du kan använda redigeraren [!UICONTROL Metadata Schema Forms] för att ändra befintliga scheman eller lägga till anpassade metadatamatcheman.

Så här visar och redigerar du egenskapssidan för en resurs:

1. Klicka på alternativet **[!UICONTROL View Properties]** i snabbåtgärderna på resurspanelen i kortvyn. Du kan också markera en resurs och sedan klicka på **[!UICONTROL Properties]** ![visa egenskaper](assets/do-not-localize/info-circle-icon.png) i verktygsfältet.

1. Du kan redigera de olika redigerbara metadataegenskaperna under de tillgängliga flikarna. Du kan dock inte ändra resursen [!UICONTROL Type] på egenskapssidan på fliken [!UICONTROL Basic].

   ![Fliken Grundläggande i resursegenskaper, där resurstypen inte kan ändras](assets/asset-properties-basic-tab.png)

   *Figur: Fliken Grundläggande för resursen [!UICONTROL Properties].*

   Om du vill ändra MIME-typen för en resurs använder du ett anpassat metadatamatchschema eller ändrar ett befintligt formulär. Mer information finns i [Redigera metadataschema-Forms](#edit-metadata-schema-forms). Om du ändrar metadatamatchemat för en MIME-typ ändras egenskapens sidlayout för resurserna och alla undertyper. Om du till exempel ändrar ett jpeg-schema under `default/image` ändras endast metadatalayouten (resursegenskaper) för resurser med MIME-typen `image/jpeg`. Om du redigerar standardschemat ändrar du metadatalayouten för alla typer av resurser.

## Metadata Schema-formulär {#default-metadata-schema-forms}

Om du vill visa en lista med formulär eller mallar går du till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]** i [!DNL Experience Manager]-gränssnittet.

[!DNL Experience Manager] innehåller följande formulärmallar för metadataschema.

| Mallar | | Beskrivning |
|---|---|---|
| [!UICONTROL default] | | Basmetadatamatchschemaformuläret för resurser. |
| | Följande underordnade formulär ärver egenskaperna för formuläret [!UICONTROL default]: | |
| | <ul><li>[!UICONTROL dm_video]</li></ul> | Schemaformulär för Dynamic Media-videor. |
| | <ul><li>[!UICONTROL image]</li></ul> | Schemaformulär för bilder med MIME-typen som `image/jpeg` och `image/png`. <br> Formuläret [!UICONTROL image] har följande underordnade formulärmallar: <ul><li> [!UICONTROL jpeg]: Schemaformulär för resurser med undertypen [!UICONTROL jpeg].</li> <li>[!UICONTROL tiff]: Schemaformulär för resurserna med undertypen TIFF.</li></ul> |
| | <ul><li>[!UICONTROL application]</li></ul> | Schemaformulär för resurser med MIME-typ som `application/pdf` och `application/zip`. <br>[!UICONTROL pdf]: Schemaformulär för resurser med undertypen PDF. |
| | <ul><li>[!UICONTROL video]</li></ul> | Schemaformulär för videoresurser med MIME-typ som `video/avi` och `video/mp4`. |
| [!UICONTROL collection] | | Schemaformulär för samlingar. |
| [!UICONTROL contentfragment] | | Schemaformulär för innehållsfragment. |
| [!UICONTROL forms] | | Det här schemaformuläret gäller [!DNL Adobe Experience Manager Forms]. |
| [!UICONTROL ugc_contentfragment] | | Schemaformulär för användargenererade innehållskomponenter och resurser som är integrerade i Experience Manager från sociala medier. |

>[!NOTE]
>
>Om du vill visa de underordnade formulären för ett schemaformulär klickar du på schemaformulärets namn.

## Lägg till ett metadatamatchformulär {#add-a-metadata-schema-form}

Följ de här stegen för att lägga till ett metadataschemaformulär:

1. Om du vill lägga till en anpassad mall i listan klickar du på **[!UICONTROL Create]** i verktygsfältet.

   >[!NOTE]
   >
   >En låssymbol visas med de oredigerade mallarna. Om du anpassar en mall är den inte låst ![låst](assets/do-not-localize/lock_closed_icon.svg).

1. Ange schemaformulärets rubrik i dialogrutan och klicka på **[!UICONTROL Create]** för att slutföra formulärskapandet.

## Redigera metadatamappningsformulär {#edit-metadata-schema-forms}

Du kan redigera ett nyligen tillagt eller befintligt metadatchemaformulär. Metadatchemaformuläret innehåller flikar och formulärobjekt på flikar. Du kan mappa/konfigurera dessa formulärobjekt till ett fält i en metadatanod i CRX-databasen. Du kan lägga till flikar eller formulärobjekt i metadatchemaformuläret. Flikarna och formulärobjekten som härleds från det överordnade objektet är låsta. Du kan inte ändra dem på underordnad nivå.

1. Markera ett formulär på sidan [!UICONTROL Metadata Schema Forms] och klicka på **[!UICONTROL Edit]** i verktygsfältet.

1. Anpassa metadataformuläret på sidan **[!UICONTROL Metadata Schema Form Editor]**. Dra de nödvändiga komponenterna från fliken **[!UICONTROL Build Form]** till en av flikarna.

   ![Metadata Schema Editor för att anpassa sidan Egenskaper för resurser](assets/metadata-schema-editor.png)

   *Figur: En [!UICONTROL Metadata Schema Form Editor]-sida med tillgängliga flikar.*

1. Om du vill konfigurera en komponent markerar du den och ändrar dess egenskaper på fliken **[!UICONTROL Settings]**.

### Komponenter på fliken [!UICONTROL Build Form] {#components-within-the-build-form-tab}

Fliken **[!UICONTROL Build Form]** visar formulärobjekt som du använder i ditt schemaformulär. Fliken **[!UICONTROL Settings]** innehåller attributen för varje objekt som du väljer på fliken **[!UICONTROL Build Form]**. I följande tabell visas de formulärobjekt som är tillgängliga på fliken **[!UICONTROL Build Form]**:

| Komponentnamn | Beskrivning |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| [!UICONTROL Section Header] | Lägg till en avsnittsrubrik för en lista med gemensamma komponenter. |
| [!UICONTROL Single Line Text] | Lägg till en textegenskap för en rad. Den lagras som en sträng. |
| [!UICONTROL Multi Value Text] | Lägg till en textegenskap med flera värden. Den lagras som en strängarray. |
| [!UICONTROL Number] | Lägg till en sifferkomponent. |
| [!UICONTROL Date] | Lägg till en datumkomponent. |
| [!UICONTROL Dropdown] | Lägg till en listruta. |
| [!UICONTROL Standard Tags] | Lägg till en tagg. |
| [!UICONTROL Smart Tags] | Förbättra sökfunktionerna genom att automatiskt lägga till metadatataggar. |
| [!UICONTROL Hidden Field] | Lägg till ett dolt fält. Den skickas som en POST-parameter när resursen sparas. |
| [!UICONTROL Asset Referenced By] | Lägg till den här komponenten för att visa en lista över resurser som resursen refererar till. |
| [!UICONTROL Asset Referencing] | Lägg till om du vill visa en lista med resurser som refererar till resursen. |
| [!UICONTROL Products References] | Lägg till om du vill visa listan över produkter som är länkade till resursen. |
| [!UICONTROL Contextual Metadata] | Lägg till för att styra visningen av andra metadataflikar på egenskapssidan för resurser. |

<!-- TBD: Ratings are not available in Experience Manager as a Cloud Service. Removed via cqdoc-18089 ticket. 
| [!UICONTROL Asset Rating]        | Add to display options for rating the asset.                                       |
-->

#### Redigera metadatakomponenten {#edit-the-metadata-component}

Om du vill redigera egenskaperna för en metadatakomponent i formuläret klickar du på komponenten för att redigera alla eller en delmängd av följande egenskaper på fliken **[!UICONTROL Settings]**. Vi rekommenderar att du bara mappar ett fält till en viss egenskap i metadataschemat. I annat fall hämtas det senast tillagda fältet som är mappat till egenskapen av systemet.

**Fältetikett**: Namnet på metadataegenskapen som visas på egenskapssidan för resursen.

**Mappa till egenskap**: Den här egenskapen anger den relativa sökvägen till eller namnet på resursnoden där den sparas i CRX-databasen. Den börjar med `./` för att ange att sökvägen finns under resursens nod.

Nedan följer exempel på giltiga värden för en egenskap:

* `./jcr:content/metadata/dc:title`: Lagrar värdet vid resursens metadatanod som egenskapen `dc:title`.

* `./jcr:created`: Lagrar datum och tid för när en resurs skapades. Det är en skyddad egenskap. Om du konfigurerar de här egenskaperna bör du markera dem som Inaktivera redigering. Annars inträffar felet ”Det gick inte att ändra resurserna” när du sparar resursens egenskaper.

För att komponenten ska visas korrekt i metadataschemaformuläret bör egenskapssökvägen inte innehålla några blanksteg.

* **Platshållare**: Använd den här egenskapen för att ange relevant platshållartext för metadataegenskapen.
* **Obligatoriskt**: Använd den här egenskapen för att markera en metadataegenskap som obligatorisk på egenskapssidan.
* **Inaktivera redigering**: Använd den här egenskapen om du inte vill tillåta redigeringar av en egenskap på egenskapssidan.
* **Visa tomt fält i skrivskyddat**: Markera den här egenskapen om du vill visa en metadataegenskap på egenskapssidan även om den inte har något värde. Om en metadataegenskap inte har något värde visas den inte som standard på egenskapssidan.
* **Visa lista sorterad**: Använd den här egenskapen om du vill visa en ordnad lista med alternativ.
* **Alternativ**: Använd den här egenskapen om du vill ange alternativ i en lista.
* **Beskrivning** : Använd den här egenskapen om du vill lägga till en kort beskrivning för metadatakomponenten.
* **Klass**: Objektklass som egenskapen är associerad med.
* **Ta bort**: Klicka på [!UICONTROL Delete] om du vill ta bort en komponent från schemaformuläret.

>[!NOTE]
>
>Komponenten [!UICONTROL Hidden Field] innehåller inte dessa attribut. I stället innehåller den egenskaper som till exempel attributnamn, värde, fältetikett och Beskrivning. Värdena för komponenten Dolt fält skickas som en POST-parameter när resursen sparas. Den sparas inte som metadata för resursen.

Om du väljer alternativet **[!UICONTROL Required]** kan du söka efter resurser som saknar obligatoriska metadata. På panelen **[!UICONTROL Filters]** expanderar du predikatet **[!UICONTROL Metadata Validation]** och väljer alternativet **[!UICONTROL Invalid]**. Sökresultatet visar resurser som saknar obligatoriska metadata som du har konfigurerat via schemaformuläret.

Om du lägger till komponenten Sammanhangsbaserade metadata på en flik i ett schemaformulär, visas komponenten som en lista på egenskapssidan med resurser som det aktuella schemat används på. Listan innehåller alla andra flikar förutom den flik som du tillämpade på komponenten Sammanhangsberoende metadata på. För närvarande innehåller den här funktionen grundläggande funktioner för att styra visningen av metadata baserat på sammanhanget.

Om du vill visa en flik på egenskapssidan förutom fliken där komponenten Sammanhangsberoende metadata används, väljer du fliken i listan. Fliken läggs till på egenskapssidan.

### Ange egenskaper i JSON-filen {#specify-properties-in-json-file}

I stället för att ange egenskaper för alternativen på fliken **[!UICONTROL Settings]** kan du definiera alternativen i en JSON-fil genom att ange motsvarande nyckelvärdespar. Ange sökvägen till JSON-filen i fältet **[!UICONTROL JSON Path]**.

#### Lägga till eller ta bort en flik i schemaformuläret {#add-delete-a-tab-in-the-schema-form}

Med schemaredigeraren kan du lägga till eller ta bort en flik. Standardschemaformuläret innehåller flikarna **[!UICONTROL Basic]**, **[!UICONTROL Advanced]**, **[!UICONTROL IPTC]** och **[!UICONTROL IPTC Extension]**.

![Standardflikar i metadataschemaformulär](assets/metadata-schema-form-tabs.png)

Klicka på `+` om du vill lägga till en flik i ett schemaformulär. Som standard har den nya fliken namnet `Unnamed-1`. Du kan ändra namnet på fliken **[!UICONTROL Settings]**. Klicka på `X` om du vill ta bort en flik.

![Lägga till eller ta bort en flik med metadatamodigeraren](assets/metadata-schema-form-new-tab.png)

## Ta bort metadata-schemaformulär {#deleting-metadata-schema-forms}

Med Experience Manager kan du bara ta bort anpassade schemaformulär. Du kan inte ta bort standardschemaformulär/-mallar. Du kan dock ta bort anpassade ändringar i dessa formulär.

Om du vill ta bort ett formulär markerar du det och klickar på ikonen Ta bort.

>[!NOTE]
>
>När du har tagit bort anpassade ändringar i ett standardformulär, visas låsikonen igen före den i gränssnittet för metadatamatchning för att ange att formuläret har återställts till standardläget.

>[!NOTE]
>
>* När du har tagit bort anpassade ändringar i ett standardformulär visas låset ![lock stängt](assets/do-not-localize/lock_closed_icon.svg) igen före formuläret. Det anger att formuläret återställs till standardläget.
>* Du kan inte ta bort standardmetadatamatchformulären i [!DNL Assets].

## Schemaformulär för MIME-typer {#schema-forms-for-mime-types}

[!DNL Experience Manager] innehåller standardformulär för olika MIME-typer. Du kan dock lägga till anpassade formulär för resurser av olika MIME-typer.

### Lägg till nya formulär för MIME-typer {#adding-new-forms-for-mime-types}

Skapa ett formulär under lämplig formulärtyp. Om du till exempel vill lägga till en mall för undertypen `image/png` skapar du formuläret under bildformulären. Schemaformulärets titel är undertypsnamnet. I det här fallet är titeln `png`.

#### Använd en befintlig schemamall för olika MIME-typer {#use-an-existing-schema-template-for-various-mime-types}

Du kan använda en befintlig mall för en annan MIME-typ. Använd till exempel formuläret `image/jpeg` för resurser av MIME-typen `image/png`.

I det här fallet skapar du en nod på `/etc/dam/metadataeditor/mimetypemappings` i CRX-databasen. Ange ett namn för noden och definiera följande egenskaper:

| Namn | Beskrivning | Typ | Värde |
|------|-------------|------|-------|
| `exposedmimetype` | Namnet på det befintliga formulär som ska mappas | `String` | `image/jpeg` |
| `mimetypes` | Lista över MIME-typer som använder formuläret som definierats i attributet `exposedmimetype` | `String` | `image/png` |

[!DNL Assets] mappar följande MIME-typer och schemaformulär:

| Schemaformulär | MIME-typer |
|---|---|
| image/jpeg | image/pjpeg |
| bild/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| video/avi | video/avi, video/msvideo, video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| video/flv | video/x-flv |

## Bevilja åtkomst till metadatamappningar {#grant-access-to-metadata-schemas}

Funktionen Metadata Schema är bara tillgänglig för administratörer. Administratörer kan dock ge åtkomst till icke-administratörer genom att ändra vissa behörigheter. Ange att icke-administratörsanvändare skapar, ändrar och tar bort behörigheter i mappen `/conf`.

## Använd mappspecifika metadata {#applying-folder-specific-metadata}

Med [!DNL Assets] kan du definiera en variant av ett metadataram och tillämpa det på en viss mapp.

Du kan t.ex. definiera en variant av standardmetadataschemat och använda det på en mapp. När du använder det ändrade schemat åsidosätter det det ursprungliga standardmetadatarammet som tillämpas på resurser i mappen.

Endast resurser som har överförts till den mapp som det här schemat används på följer de ändrade metadata som har definierats i variantmetadataschemat. [!DNL Assets] i andra mappar där det ursprungliga schemat används fortsätter att överensstämma med metadata som definierats i det ursprungliga schemat.

Metadatarv av resurser baseras på det schema som tillämpas på den översta mappen i hierarkin. Samma schema tillämpas på eller ärvs av undermapparna. Om ett annat schema används på undermappsnivå avbryts arvet.

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]** i gränssnittet [!DNL Experience Manager]. Sidan **[!UICONTROL Metadata Schema Forms]** visas.
1. Markera kryssrutan före ett formulär, till exempel standardformuläret för metadata, och klicka på **[!UICONTROL Copy]** och spara det som ett anpassat formulär. Ange ett anpassat namn för formuläret, till exempel `my_default`. Du kan också skapa ett eget formulär.

1. Markera formuläret `my_default` på sidan **[!UICONTROL Metadata Schema Forms]** och klicka sedan på **[!UICONTROL Edit]**.
1. Lägg till ett textfält i schemaformuläret på sidan **[!UICONTROL Metadata Schema Editor]**. Lägg till exempel till ett fält med etiketten **[!UICONTROL Category]**.
1. Klicka på **[!UICONTROL Save]**. Det ändrade formuläret visas på sidan **[!UICONTROL Metadata Schema Forms]**.
1. Välj **[!UICONTROL Apply to Folders]** i verktygsfältet om du vill använda anpassade metadata i en mapp.
1. Markera mappen som det ändrade schemat ska tillämpas på och välj sedan **[!UICONTROL Apply]**.
1. Om det andra metadataschemat används i mappen visas ett varningsmeddelande om att du håller på att skriva över det befintliga metadataschemat. Klicka på **Skriv över**.
1. Klicka på **OK** för att stänga meddelandet.
1. Navigera till mappen som du tillämpade det ändrade metadataschemat på.

## Definiera obligatoriska metadata {#defining-mandatory-metadata}

Du kan definiera obligatoriska fält på mappnivå, vilket tillämpas på resurser som överförs till mappen. Om du överför resurser som saknar metadata för de obligatoriska fält som definierats tidigare visas en visuell indikation på saknade metadata för resurserna i kortvyn.

>[!NOTE]
>
>Ett metadatafält kan definieras som obligatoriskt baserat på värdet i ett annat fält. I vyn Kort visar inte Experience Manager varningsmeddelandet om att metadata saknas för sådana obligatoriska metadatafält.

1. Klicka på Experience Manager logotyp och navigera sedan till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]**. Sidan **[!UICONTROL Metadata Schema Forms]** visas.
1. Spara standardformuläret för metadata som ett anpassat formulär. Spara det som `my_default`.
1. Redigera det anpassade formuläret. Lägg till ett obligatoriskt fält. Lägg till exempel till ett **[!UICONTROL Category]**-fält och gör fältet obligatoriskt.
1. Klicka på **[!UICONTROL Save]**. Det ändrade formuläret visas på sidan **[!UICONTROL Metadata Schema Forms]**. Markera formuläret och välj sedan **[!UICONTROL Apply to Folders]** i verktygsfältet för att använda anpassade metadata i en mapp.
1. Navigera till mappen och överför vissa resurser med saknade metadata för det obligatoriska fältet som du lade till i det anpassade formuläret. Ett meddelande om saknade metadata för det obligatoriska fältet visas i kortvyn för resursen.
1. (Valfritt) Åtkomst `https://[server]:[port]/system/console/components/`. Konfigurera och aktivera komponenten `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` som är inaktiverad som standard. Ange en frekvens som Experience Manager ska kontrollera om metadata för resurserna är giltiga.

   Den här konfigurationen lägger till egenskapen `hasValidMetadata` i `jcr:content` med resurser. Med den här egenskapen kan Experience Manager filtrera resultatet i en sökning.

   >[!NOTE]
   >
   >Om en resurs läggs till efter den schemalagda kontrollen flaggas resursen inte med `hasValidMetadata` förrän vid nästa schemalagda kontroll. Resurserna visas inte i mellanliggande sökresultat.

   >[!CAUTION]
   >
   >Valideringskontrollerna av metadata är resurskrävande och kan påverka systemets prestanda. Schemalägg kontrollerna därefter. Om servern inte kan hantera inläsningen kan du försöka inaktivera det här jobbet

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publicera Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)