---
title: Metadata-scheman
description: Metadata-schemat definierar layouten för egenskapssidan och de metadataegenskaper som visas för resurser. Lär dig hur du skapar anpassade metadatamatcheman, redigerar metadatamatchema och hur du använder metadatamatchema på resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff
workflow-type: tm+mt
source-wordcount: '2432'
ht-degree: 12%

---


# Metadatascheman {#metadata-schemas}

I Adobe Experience Manager Resurser (AEM) definieras layouten för egenskapssidan och de metadataegenskaper som visas för resurser som använder det aktuella schemat i ett metadataschema. Metadataegenskaperna innehåller titel, beskrivning, MIME-typer, taggar och så vidare.

Du kan använda Forms-redigeraren för metadatamodeller för att ändra befintliga scheman eller lägga till anpassade metadatamatcheman.

1. Om du vill visa egenskapssidan för en resurs klickar eller trycker du på ikonen **[!UICONTROL View Properties]** från snabbåtgärder på resurspanelen i kortvyn. Du kan också markera resursen i användargränssnittet och sedan klicka på eller trycka på ikonen **[!UICONTROL Properties]** i verktygsfältet.
1. Redigera olika metadataegenskaper under de olika flikarna. Du kan dock inte ändra resurstypen på egenskapssidan.
Om du vill ändra MIME-typen för en resurs använder du ett anpassat metadatamatchschema eller ändrar ett befintligt formulär. Mer information finns i [Redigera metadataschema Forms](#edit-metadata-schema-forms). Om du ändrar metadataschemat för en viss MIME-typ ändras egenskapssidlayouten för resurser med den aktuella MIME-typen och alla resursundertyper. Om du till exempel ändrar ett jpeg-schema under `default/image` ändras bara metadatalayouten (resursegenskaper) för resurser med MIME-typen `image/jpeg`. Om du redigerar standardschemat ändrar du metadatalayouten för alla typer av resurser.

1. Om du vill visa en lista med formulär/mallar klickar du på AEM-logotypen och navigerar sedan till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]**.
AEM innehåller följande mallar:

   * **standard**: Basmetadataschemaformuläret för resurser.

   Följande underordnade formulär ärver egenskaperna för standardformuläret:
i. **bild**: Schemaformulär för resurser med MIME-typen &quot;image&quot;, till exempel `image/jpeg`, `image/png` och så vidare.
&quot;Bildsformuläret har följande underordnade formulärmallar:
a. **jpeg**: Schemaformulär för resurser med undertypen `jpeg`.
b. **tiff**: Schemaformulär för resurserna med undertypen `tiff`.

   ii. **program**: Schemaformulär för resurser med MIME-typ,  `application`till exempel  `application/pdf`,  `application/zip`och så vidare.
a. **pdf**: Schemaformulär för resurser med undertypen `pdf`.

   iii. **video**: Schemaformulär för resurser med MIME-typ  `video`som  `video/avi`,  `video/mp4`osv.

   * **samling**: Schemaformulär för samlingar.
   * **contentFragment:** schemaformulär för innehållsfragment.


>[!NOTE]
>
>Om du vill visa de underordnade formulären för ett schemaformulär klickar/trycker du på schemaformulärets namn.

## Lägg till ett metadatamatchformulär {#add-a-metadata-schema-form}

1. Om du vill lägga till en anpassad mall i listan klickar du på **[!UICONTROL Create]** i verktygsfältet.

   >[!NOTE]
   >
   >Oredigerade mallar har en låsikon framför sig. Om du anpassar någon av mallarna visas låsikonen innan mallen försvinner.

1. I dialogrutan anger du rubriken för schemaformuläret och klickar sedan på **[!UICONTROL Create]** för att slutföra formulärskapandet.

## Redigera metadata-schemaformulär {#edit-metadata-schema-forms}

Du kan redigera ett nyligen tillagt eller befintligt metadatchemaformulär. Metadatchemaformuläret innehåller följande:

* Tabbar
* Formulärobjekt på flikar.

Du kan mappa/konfigurera dessa formulärobjekt till ett fält i en metadatanod i CRX-databasen.

Du kan lägga till nya flikar eller formulärobjekt i metadatchemaformuläret. Flikarna och formulärobjekten som härleds från det överordnade objektet är låsta. Du kan inte ändra dem på underordnad nivå.

1. Markera kryssrutan före ett formulär på sidan Schemaformulär och klicka sedan på ikonen **Redigera** i verktygsfältet.
1. På sidan **[!UICONTROL Metadata Schema Editor]** anpassar du egenskapssidan för resursen genom att dra en eller flera komponenter från listan med komponenttyper på fliken **[!UICONTROL Build Form]** till fliken **[!UICONTROL Basic]**.
1. Om du vill konfigurera en komponent markerar du den och ändrar dess egenskaper på fliken **Inställningar**.

### Komponenter på fliken Skapa formulär {#components-within-the-build-form-tab}

Fliken **[!UICONTROL Build Form]** visar de formulärobjekt som du använder i schemaformuläret. Fliken **[!UICONTROL Settings]** innehåller attributen för varje objekt som du väljer på fliken **[!UICONTROL Build Form]**. Följande tabell visar vilka formulärobjekt som är tillgängliga på fliken **[!UICONTROL Build Form]**:

<table>
 <tbody>
  <tr>
   <td><strong>Komponentnamn</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>Avsnittshuvud</td>
   <td>Lägg till en avsnittsrubrik för en lista med gemensamma komponenter.</td>
  </tr>
  <tr>
   <td>Enkelradstext</td>
   <td>Lägg till en textegenskap för en rad. Den lagras som en sträng.</td>
  </tr>
  <tr>
   <td>Flervärdestext</td>
   <td>Lägg till en textegenskap med flera värden. Den lagras som en strängarray.</td>
  </tr>
  <tr>
   <td>Siffra</td>
   <td>Lägg till en sifferkomponent.</td>
  </tr>
  <tr>
   <td>Date</td>
   <td>Lägg till en datumkomponent.</td>
  </tr>
  <tr>
   <td>Listruta</td>
   <td>Lägg till en listruta.</td>
  </tr>
  <tr>
   <td>Standardtaggar</td>
   <td>Lägg till en tagg. </td>
  </tr>
  <tr>
   <td>Smarta taggar</td>
   <td>Lägg till mer i sökfunktionerna genom att automatiskt lägga till metadatataggar.<br /> </td>
  </tr>
  <tr>
   <td>Dolt fält</td>
   <td>Lägg till ett dolt fält. Den skickas som en POST-parameter när resursen sparas.</td>
  </tr>
  <tr>
   <td>Resurs som refereras av</td>
   <td>Lägg till den här komponenten för att visa en lista över resurser som resursen refererar till.</td>
  </tr>
  <tr>
   <td>Resursreferens</td>
   <td>Lägg till om du vill visa en lista med resurser som refererar till resursen.</td>
  </tr>
  <tr>
   <td>Produktreferenser</td>
   <td>Lägg till om du vill visa listan över produkter som är länkade till resursen.</td>
  </tr>
  <tr>
   <td>Tillgångsklassificering</td>
   <td>Lägg till för att visa alternativ för att klassificera resursen.</td>
  </tr>
  <tr>
   <td>Sammanhangsberoende metadata</td>
   <td>Lägg till för att styra visningen av andra metadataflikar på egenskapssidan för resurser.</td>
  </tr>
 </tbody>
</table>

#### Redigera metadatakomponenten {#edit-the-metadata-component}

Om du vill redigera egenskaperna för en metadatakomponent i formuläret klickar du på komponenten och redigerar alla eller en delmängd av följande egenskaper på fliken **[!UICONTROL Settings]**.

**Fältetikett**: Namnet på metadataegenskapen som visas på egenskapssidan för resursen.

**Mappa till egenskap**: This property specifies the relative path/name to the asset node where it is saved in the CRX database. Den börjar med `./` eftersom den anger att sökvägen finns under objektets nod.

Följande är giltiga värden för den här egenskapen:

* . `/jcr:content/metadata/dc:title`: Lagrar värdet vid resursens metadatanod som egenskapen `dc:title`.

* . `/jcr:created`: Visar jcr-egenskapen vid resursens nod. Om du konfigurerar de här egenskaperna för visning bör du markera dem som Inaktivera redigering, eftersom de är skyddade. Annars inträffar felet ”Det gick inte att ändra resurserna” när du sparar resursens egenskaper.

För att komponenten ska visas korrekt i metadataschemaformuläret bör egenskapssökvägen inte innehålla några blanksteg.

**Platshållare**: Använd den här egenskapen för att ange relevant platshållartext för metadataegenskapen.

**Obligatoriskt**: Använd den här egenskapen för att markera en metadataegenskap som obligatorisk på egenskapssidan.

**Inaktivera redigering**: Använd den här egenskapen för att göra en metadataegenskap som inte kan redigeras på sidan Egenskaper.

**Visa tomt fält i skrivskyddat**: Markera den här egenskapen om du vill visa en metadataegenskap på egenskapssidan även om den inte har något värde. Om en metadataegenskap inte har något värde visas den inte som standard på egenskapssidan.

**Visa sorterad** lista: Använd den här egenskapen för att visa en ordnad lista med alternativ

**Alternativ**: Använd den här egenskapen för att ange alternativ i en lista

**Beskrivning** : Använd den här egenskapen om du vill lägga till en kort beskrivning för metadatakomponenten.

**Klass**: Den objektklass som egenskapen är associerad med.

**Ta bort**: Klicka för att ta bort en komponent från schemaformuläret.

>[!NOTE]
>
>Komponenten Dolt fält innehåller inte dessa attribut. I stället innehåller den egenskaper som till exempel attributnamn, värde, fältetikett och Beskrivning. Värdena för komponenten Dolt fält skickas som en POST-parameter när resursen sparas. Den sparas inte som metadata för resursen.

Om du väljer alternativet **[!UICONTROL Required]** kan du söka efter resurser som saknar obligatoriska metadata. På panelen **[!UICONTROL Filters]** expanderar du predikatet **[!UICONTROL Metadata Validation]** och väljer alternativet **[!UICONTROL Invalid]**. Sökresultatet visar resurser som saknar obligatoriska metadata som du har konfigurerat via schemaformuläret.

Om du lägger till komponenten Sammanhangsbaserade metadata på en flik i ett schemaformulär, visas komponenten som en lista på egenskapssidan med resurser som det aktuella schemat används på. Listan innehåller alla andra flikar förutom den flik som du tillämpade på komponenten Sammanhangsberoende metadata på. För närvarande innehåller den här funktionen grundläggande funktioner för att styra visningen av metadata baserat på sammanhanget.

Om du vill ta med en flik på egenskapssidan förutom fliken där komponenten Sammanhangsberoende metadata används, väljer du fliken i listan. Fliken läggs till på egenskapssidan.

### Ange egenskaper i JSON-filen {#specify-properties-in-json-file}

I stället för att ange egenskaper för alternativen på fliken **[!UICONTROL Settings]** kan du definiera alternativen i en JSON-fil genom att ange motsvarande nyckelvärdespar. Ange sökvägen till JSON-filen i fältet **[!UICONTROL JSON Path]**.

#### Lägg till och ta bort en flik i schemaformuläret {#add-delete-a-tab-in-the-schema-form}

Med schemaredigeraren kan du lägga till eller ta bort en flik. Standardschemaformuläret innehåller som standard flikarna **[!UICONTROL Basic]**, **[!UICONTROL Advanced]**, **[!UICONTROL IPTC]** och **[!UICONTROL IPTC Extension]**.

Klicka på `+` för att lägga till en ny flik i ett schemaformulär. Som standard har den nya fliken namnet `Unnamed-1`. Du kan ändra namnet på fliken **[!UICONTROL Settings]**. Klicka på `X` för att ta bort en flik.

## Tar bort metadata för schemaformulär {#deleting-metadata-schema-forms}

AEM låter dig endast ta bort anpassade schemaformulär. Du kan inte ta bort standardschemaformulär/-mallar. Du kan dock ta bort anpassade ändringar i dessa formulär.

Om du vill ta bort ett formulär markerar du det och klickar på ikonen Ta bort.

>[!NOTE]
>
>När du har tagit bort anpassade ändringar i ett standardformulär, visas låsikonen igen före den i gränssnittet för metadatamatchning för att ange att formuläret har återställts till standardläget.

>[!NOTE]
>
>Du kan inte ta bort metadatamatchschemaformulär i AEM Assets.

## Schemaformulär för MIME-typer {#schema-forms-for-mime-types}

AEM Assets innehåller standardformulär för olika MIME-typer. Du kan dock lägga till anpassade formulär för resurser av olika MIME-typer.

### Lägga till nya formulär för MIME-typer {#adding-new-forms-for-mime-types}

Skapa ett nytt formulär med lämplig formulärtyp. Om du till exempel vill lägga till en ny mall för undertypen **image/png** skapar du formuläret som ett bildformulär. Schemaformulärets titel är undertypsnamnet. I det här fallet är titeln ”png **”**.

#### Använda en befintlig schemamall för olika MIME-typer {#using-an-existing-schema-template-for-various-mime-types}

Du kan använda en befintlig mall för en annan MIME-typ. Använd till exempel formuläret `image/jpeg` för resurser av MIME-typ `image/png`.

I det här fallet skapar du en ny nod på `/etc/dam/metadataeditor/mimetypemappings` i CRX-databasen. Ange ett namn för noden och definiera följande egenskaper:

| **Namn** | **Beskrivning** | **Typ** | **Värde** |
|---|---|---|---|
| `exposedmimetype` | Namnet på det befintliga formulär som ska mappas | Sträng | `image/jpeg` |
| `mimetypes` | Lista över MIME-typer som använder formuläret som definierats i attributet `exposedmimetype` | Sträng | `image/png` |

AEM Assets mappar följande MIME-typer och schemaformulär:

| Schemaformulär | MIME-typer |
|---|---|
| image/jpeg | image/pjpeg |
| bild/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related. type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related. type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related. type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| video/avi | video/avi, video/msvideo, video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| video/flv | video/x-flv |

## Bevilja åtkomst till metadatamappningar {#granting-access-to-metadata-schemas}

Funktionen Metadata Schema är bara tillgänglig för administratörer. Administratörer kan dock ge åtkomst till icke-administratörer genom att ändra vissa behörigheter. Den som inte är administratör bör ha behörighet att skapa, ändra och ta bort i mappen `/conf`.

## Använder mappspecifika metadata {#applying-folder-specific-metadata}

Med AEM Assets kan du definiera en variant av ett metadataram och använda det på en viss mapp.

Du kan t.ex. definiera en variant av standardmetadataschemat och använda det på en mapp. När du använder det ändrade schemat åsidosätter det det ursprungliga standardmetadatarammet som används för resurser i mappen.

Endast resurser som överförts till den mapp som det här schemat tillämpas på kommer att överensstämma med de ändrade metadata som definierats i variantmetadataschemat.

Resurser i andra mappar där det ursprungliga schemat används fortsätter att överensstämma med metadata som definierats i det ursprungliga schemat.

Metadataarv av resurser baseras på det schema som tillämpas på mappen på första nivån i hierarkin. Om en mapp inte innehåller undermappar ärver resurserna i mappen metadata från det schema som används i mappen.

Om mappen har en undermapp ärver resurserna i undermappen metadata från det schema som används på undermappsnivå om ett annat schema används på undermappsnivå. Om inget schema eller samma schema används på undermappsnivå ärver undermappsresurserna metadata från det schema som används på den överordnade mappnivån.

1. Klicka på AEM-logotypen och navigera sedan till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]**. Sidan **[!UICONTROL Metadata Schema Forms]** visas.
1. Markera kryssrutan före ett formulär, till exempel standardformuläret för metadata, och klicka eller tryck på kopieringsikonen och spara det som ett anpassat formulär. Ange ett anpassat namn för formuläret, till exempel `my_default`. Du kan också skapa ett eget formulär.

1. På sidan **[!UICONTROL Metadata Schema Forms]** markerar du formuläret `my_default` och klickar sedan på ikonen **[!UICONTROL Edit]**.
1. Lägg till ett textfält i schemaformuläret på sidan **[!UICONTROL Metadata Schema Editor]**. Lägg till exempel till ett fält med etiketten **[!UICONTROL Category]**.
1. Klicka på **[!UICONTROL Save]**. Det ändrade formuläret visas på sidan **[!UICONTROL Metadata Schema Forms]**.
1. Klicka/tryck på **[!UICONTROL Apply to Folder(s)]** i verktygsfältet för att använda anpassade metadata i en mapp.
1. Välj den mapp som det ändrade schemat ska användas på och klicka/tryck sedan på **[!UICONTROL Apply]**.
1. Om det andra metadataschemat används i mappen visas ett varningsmeddelande om att du håller på att skriva över det befintliga metadataschemat. Klicka på **Skriv över**.
1. Klicka på **OK** för att stänga meddelandet.
1. Navigera till mappen som du tillämpade det ändrade metadataschemat på.

## Definiera obligatoriska metadata {#defining-mandatory-metadata}

Du kan definiera obligatoriska fält på mappnivå, vilket tillämpas på resurser som överförs till mappen. Om du överför resurser som saknar metadata för de obligatoriska fält som definierats tidigare visas en visuell indikation på saknade metadata för resurserna i kortvyn.

>[!NOTE]
>
>Ett metadatafält kan definieras som obligatoriskt baserat på värdet i ett annat fält. I vyn Kort visar AEM inte varningsmeddelandet om att metadata saknas för sådana obligatoriska metadatafält.

1. Klicka på AEM-logotypen och navigera sedan till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]**. Sidan **[!UICONTROL Metadata Schema Forms]** visas.
1. Spara standardformuläret för metadata som ett anpassat formulär. Spara den till exempel som `my_default`.
1. Redigera det anpassade formuläret. Lägg till ett obligatoriskt fält. Lägg till exempel till ett **[!UICONTROL Category]**-fält och gör fältet obligatoriskt.
1. Klicka på **[!UICONTROL Save]**. Det ändrade formuläret visas på sidan **[!UICONTROL Metadata Schema Forms]**. Markera formuläret och klicka eller tryck sedan på **[!UICONTROL Apply to Folder(s)]** i verktygsfältet för att använda anpassade metadata i en mapp.
1. Navigera till mappen och överför vissa resurser med saknade metadata för det obligatoriska fältet som du lade till i det anpassade formuläret. Ett meddelande om saknade metadata för det obligatoriska fältet visas i kortvyn för resursen.
1. (Valfritt) Åtkomst `https://[server]:[port]/system/console/components/`. Konfigurera och aktivera `com.day.cq.dam.core.impl.MissingMetadataNotificationJob`-komponenten som är inaktiverad som standard. Ange en frekvens med vilken AEM kontrollerar om metadata för resurserna är giltiga.

   Den här konfigurationen lägger till egenskapen `hasValidMetadata` i `jcr:content` för resurser. Med den här egenskapen kan AEM filtrera resultatet i en sökning.

   >[!NOTE]
   >
   >Om en resurs läggs till efter den schemalagda kontrollen flaggas resursen inte med `hasValidMetadata` förrän vid nästa schemalagda kontroll. Resurserna visas inte i mellanliggande sökresultat.

   >[!CAUTION]
   >
   >Valideringskontrollerna av metadata är resurskrävande och kan påverka systemets prestanda. Schemalägg kontrollerna därefter. Om servern inte kan hantera inläsningen provar du med att inaktivera det här jobbet
