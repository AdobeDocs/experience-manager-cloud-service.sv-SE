---
title: Hantera metadata
seo-title: Manage [!DNL AEM Forms] metadata
description: Metadata gör det enklare att kategorisera och ordna resurser och hjälper användare som letar efter en viss resurs.
seo-description: Metadata allows for easier categorization and organization of assets and helps users who are looking for a specific asset.
exl-id: 8527246a-37f0-4d43-a49e-1c76c265514e
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1640'
ht-degree: 0%

---

# Lägga till, ta bort eller redigera metadata i ett anpassat formulär {#manage-form-metadata}

Metadata gör det enklare att kategorisera och ordna resurser och hjälper användare som letar efter en viss resurs.

[!DNL AEM Forms]som standard innehåller en definierad uppsättning metadata för varje resurstyp. Utöver standardmetadata kan du lägga till anpassade metadata för varje resurstyp. [!DNL AEM Forms] ger dig även rätt sätt att skapa, hantera och utbyta alla dessa metadata effektivt för dina formulär.

<!-- If you're a developer or a site owner, you can customize Forms Portal, the end-user interface for [!DNL AEM Forms] to reflect the metadata you're using in your organization. For more information abouts Forms Portal, see [Introduction to publishing forms on a portal](introduction-publishing-forms.md). -->

## Metadata i [!DNL AEM Forms] {#metadata-in-aem-forms}

I [!DNL AEM Forms], beror listan med metadataegenskaper som är associerade med en resurs på dess typ. Om du lägger till en anpassad metadataegenskap läggs den till i alla resurser av den typ som de anpassade metadata lades till i.

### Resurstyper {#asset-types}

Följande resurstyper stöds i [!DNL AEM Forms]:

* Formulärmallar (XFA-formulär)
* PDF forms
* Dokument (flat PDF)
* Adaptiv Forms
* Forms datamodell
* XFS

#### Omfattande lista med metadata {#extensive-list-of-metadata}

Nedan följer en omfattande lista över metadataegenskaper som stöds i [!DNL AEM Forms]:

<table>
 <tbody> 
  <tr> 
   <td><strong>Egenskapsnamn</strong></td> 
   <td><strong>Tillgångstyp</strong></td> 
   <td><strong>Beskrivning</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>Titel</td> 
   <td>Alla utom resurser</td> 
   <td>Visningsnamn för resursen.<br /> </td> 
  </tr> 
  <tr> 
   <td>Beskrivning</td> 
   <td>Alla utom resurser</td> 
   <td>Beskrivning av tillgången. Användaren kan ange det här värdet.<br /> </td> 
  </tr> 
  <tr> 
   <td>Typ</td> 
   <td>Alla</td> 
   <td><p>Ett skrivskyddat värde som anger resurstypen. Den kan ha något av följande värden:</p> 
    <ul> 
     <li>Formulärmall</li> 
     <li>formulär PDF, formulär PDF (Acrobat) eller formulär PDF (signerat)</li> 
     <li>Dokument, dokument (signerat)</li> 
     <li>Adaptiv form</li> 
     <li>Formulärdatamodell</li>
     <li>Resurs</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Skapad</td> 
   <td>Alla</td> 
   <td>Ett skrivskyddat värde som anger när resursen skapades.</td> 
  </tr> 
  <tr> 
   <td>Senaste ändringsdatum</td> 
   <td>Alla</td> 
   <td>Ett skrivskyddat värde som anger när resursen senast ändrades.</td> 
  </tr> 
  <tr> 
   <td>Författare</td> 
   <td>Alla utom resurser</td> 
   <td><p>Ett skrivskyddat värde som automatiskt beräknas baserat på formulärtypen.</p> 
    <ul> 
     <li>PDF/Formulärmall/Dokument - hämtas från den överförda binära filen.</li> 
     <li>Anpassat formulär - Inloggad användare när formuläret skapas.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Status</td> 
   <td>Alla utom resurser</td> 
   <td><p> Ett skrivskyddat värde som definierar ett av följande lägen i ett formulär:</p> 
    <ul> 
     <li>Inget värde: Om ett formulär aldrig har publicerats.</li> 
     <li>Publicerat: När ett formulär publiceras.</li> 
     <li>Ändrad: När ett formulär ändrades efter att ha publicerats en gång.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Senaste publiceringsdatum</td> 
   <td>Alla utom resurser</td> 
   <td>Ett skrivskyddat värde som anger när formuläret senast publicerades.</td> 
  </tr> 
  <tr> 
   <td>Publicera på/av-tid</td> 
   <td>Alla utom resurser</td> 
   <td><p>Tidpunkt då formuläret schemaläggs att automatiskt publiceras/avpubliceras. Användaren anger det här värdet när metadata redigeras.</p> 
    <ul> 
     <li>Både Publicera på- och Av-tid ska ligga efter aktuellt datum. </li> 
     <li>Publiceringstiden för publicering ska vara längre än publiceringstiden i tid. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Skicka URL</td> 
   <td><p>Formulärmall</p> <p>PDF form</p> </td> 
   <td><p>Så här konfigurerar du en användardefinierad URL för att skicka formulärdata till en server.</p> <p>Skicka-URL kan konfigureras med någon av följande metoder, listade i prioritetsordning:</p> 
    <ul> 
     <li>Ange en skicka-URL direkt i en formulärmall genom att använda HTTP-knappen när du skapar ett XFA-formulär i AEM Forms Designer.</li> 
     <li>I AEM Forms-användargränssnittet markerar du ett formulär och anger en Skicka-URL när du redigerar metadataegenskaperna.</li> 
     <!-- <li>In Forms Portal, edit the Search &amp; Lister component and specify a submit URL under the Form Link tab.</li> -->
    </ul> </td> 
  </tr> 
  <tr> 
   <td>HTML renderingsprofil</td> 
   <td>Formulärmall</td> 
   <td>Den återgivningsprofil för HTML som används vid återgivning av en formulärmall i HTML-format.</td> 
  </tr> 
  <tr> 
   <td>Återgivningsformat</td> 
   <td><p>Formulärmall</p> <p>Adaptiv form</p> </td> 
   <td><p>Med det här alternativet kan användaren ange formulärets återgivningsformat när formulären publiceras:</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li>Båda</li> 
    </ul> <p>Det här alternativet används endast för att begränsa formulärens återgivningsformat på formulärportalen där de är synliga för slutanvändaren.</p> </td> 
  </tr> 
  <tr> 
   <td>Taggar</td> 
   <td>Alla utom resurser</td> 
   <td>Etiketter som är kopplade till formuläret för att underlätta snabb och enkel sökning.</td> 
  </tr> 
  <tr> 
   <td>Referenser</td> 
   <td><p>Adaptiv form</p> <p>Formulärmall</p> <p>Resurs</p> </td> 
   <td><p>Lista över resurser (andra formulär eller resurser) som det här formuläret är relaterat till. Dessa resurser kan delas in i följande två kategorier:</p> 
    <ul> 
     <li>Referenser: Resurser som det aktuella formuläret refererar till.</li> 
     <li>Refereras av: Resurser som refererar till den aktuella tillgången.</li> 
    </ul> <p>De här resurserna visas som länkar och deras metadata kan du komma åt direkt genom att klicka på dem.<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>Val av formulärmodell (XDP/XSD)</td> 
   <td>Adaptiv form</td> 
   <td><p>Anger vilken formulärmodell som används när det adaptiva formuläret skapas. Den här egenskapen kan ha följande värden:</p> 
    <ul> 
      <li>Formulärdatamodell </li>
      <li>Schema: En XML med JSON-schema</li>
     <!-- <li>Form template: A form template is selected from the ones existing in the repository. This value can be updated.</li> 
     <li>XML schema: An XSD file is uploaded. This value can be updated.</li> -->
     <li>Ingen</li> 
    </ul> 
    <div>
      En formulärmodell som har valts kan uppdateras men inte tas bort. 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## Visa formulärmetadata {#view-form-metadata}

Resurser har befintliga egenskapsvärden som kan visas i skrivskyddat läge. Dessa metadata kommer från när formuläret överförs eller när formuläret skapas.

1. Navigera till platsen för resursen som du vill visa metadata för.

1. Öppna egenskapssidan på något av följande sätt:

   * Klicka på **[!UICONTROL Properties]** ![Egenskaper](assets/Smock_Info_18_N.svg) -ikon från snabbåtgärder.

     >[!NOTE]
     >
     >Snabbåtgärder är de åtgärdsobjekt som visas över en miniatyrbild när du håller muspekaren.

   * Markera formuläret och klicka på knappen **[!UICONTROL Properties]** ![Egenskaper](assets/Smock_Info_18_N.svg) som visas i verktygsfältet.
   * Navigera till sidan med formulärinformation genom att klicka på miniatyrbilden för formuläret när det inte är i markeringsläget. Klicka på ![Egenskaper](assets/Smock_Info_18_N.svg) ögonikonen i det övre högra hörnet och klicka sedan på Egenskaper i listan nedanför.

1. Egenskapssidan som öppnas visar ett schema som bara innehåller de metadataegenskaper som innehåller vissa värden.

   <!-- The properties page has a toolbar containing two action icons:

    * Edit: ![Edit](assets/Smock_Edit_18_N.svg) Edit the metadata property values
    * View: ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) Navigate to the form details page, which opens the form in the preview mode. -->

   Innehållsdelen är uppdelad i två delar:

   * Den vänstra panelen innehåller en miniatyrbild av formuläret
   * Den högra panelen innehåller metadataegenskaper i skrivskyddat läge, som är fördelade på olika flikar.

## Lägg till/uppdatera värden för formulärmetadata {#add-update-form-metadata-values}

Du kan redigera värdet för befintliga metadataegenskaper eller lägga till nya värden i ett befintligt egenskapsfält för metadata (till exempel när ett metadatafält är tomt).

<!-- ### Update metadata property values {#update-metadata-property-values}

1. Follow the steps mentioned in the previous section to open the properties page where existing metadata of the selected form can be viewed.  

1. From the toolbar, click the Edit icon ![Edit](assets/Smock_Edit_18_N.svg) to change the mode of the page from read-only to read/write.  

1. The properties page that opens holds a schema that contains a mix of editable input fields and static text.  

1. The properties displayed in static text are the ones that you cannot edit.  

1. You can navigate to other tabs to find input fields for metadata properties placed under them.

   This page has a toolbar containing two action icons different from those in view mode:

    * Cancel: ![aem6forms_close](assets/aem6forms_close.svg_w24.png) Cancel any changes made to metadata property values so far
    * Done: ![aem6forms_check](assets/aem6forms_check.png) Save all the changes made to metadata property values so far

   Both these actions direct the user back to read-only mode of the properties page containing the updated values.-->

### Uppdatera formulärminiatyrbilden {#update-the-form-thumbnail}

På den vänstra panelen på egenskapssidan visas miniatyrbilden för formuläret. Som standard visas den miniatyrbild som genereras när formuläret skapas (anpassat formulär) eller när formuläret överförs.

För alla formulärtyper kan du överföra en bild genom att klicka på **[!UICONTROL Upload Image]** och bläddra efter en bildfil från den lokala katalogen. Den markerade bilden används som miniatyrbild i stället för som standardbild.

För Adaptiv Forms finns ytterligare funktioner som gör att användaren kan generera en miniatyrbild som en ögonblicksbild av den aktuella förhandsvisningen av adaptiva formulär. Sedan [!DNL AEM Forms] har också stöd för utveckling av Adaptiv Forms. Förhandsgranskningen av den adaptiva formen kan ändras varje gång du ändrar den adaptiva formen. Den här funktionen för att generera en miniatyrbild hjälper dig att få en ny miniatyrbild för det adaptiva formuläret baserat på den aktuella förhandsvisningsstatusen. Klicka **[!UICONTROL Generate Preview]** att genomföra denna åtgärd.

>[!NOTE]
>
>* Använd en fyrkantig bild som miniatyrbild. När du använder en bild som inte är fyrkantig och visar miniatyrbilden i listvyn visas miniatyrbilden som bortklippt.
>* När en ny bild har överförts eller genererats ersätts miniatyrbilden av den här bilden och kan inte återställas till den föregående bilden.
>

## Lägg till anpassade metadata {#add-custom-metadata}

Förutom de metadata som anges i kartongen [!DNL AEM Forms] har stöd för nya anpassade metadata.

Ett verktyg (redigeringsprogram för metadataschema) finns för att definiera schemat för metadatalayouten. det vill säga layouten för det som visas i **[!UICONTROL Properties]** sida i ett formulär. Med metadatarameditor kan du lägga till eller ändra ett anpassat schema för dina resurser.

[!DNL AEM Forms] visar metadatamatcheman för de formulärtyper som stöds i det här verktyget. På så sätt kan du komma åt dessa scheman och använda funktionerna som finns i redigeraren för metadatamatchning för att lägga till anpassade egenskaper.

### Navigera i metadatamodeditorn {#navigate-the-metadata-schema-editor}

1. Navigera till **[!UICONTROL Tools > Assets > Metadata Schemas]**.

1. Klicka **[!UICONTROL forms]** från listade schemaformulär.

1. I listan som öppnas klickar du på resurstypen som du vill lägga till anpassade metadata för.

   >[!NOTE]
   >
   >Dessa scheman innehåller metadataegenskaper som anges utanför rutan och får inte ändras/redigeras (markera kryssrutan och klicka på Redigera från verktygsfältet) för att undvika funktionsproblem.

1. Alla resurstyper som du klickar på öppnas en lista som innehåller `extendedmetadata` alternativ. Redigera det här schemat.

1. Markera kryssrutan bredvid `extendedmetadata` och klicka sedan på Redigera ![Redigera](assets/Smock_Edit_18_N.svg) som visas i verktygsfältet.

1. [!DNL AEM Forms] öppnar metadataschredigeraren/formulärbyggaren för den valda resurstypen (i det här fallet Adaptiv form).

   Metadataredigerare

   1. Den vänstra panelen innehåller flikade avsnitt där fälten är placerade och den högra panelen visar alla tillgängliga gränssnittskomponenter och egenskaperna för fältet som är markerat från den vänstra panelen.

   1. Det låsta avsnittet går inte att redigera och innehåller fält för alla metadataegenskaper som anges i rutan.

   1. Du kan lägga till fler flikar genom att klicka på +-symbolen.

   1. Du kan lägga till ett anpassat fält av önskad typ genom att dra fältkomponenten från **[!UICONTROL Build Form]** till schemasidan.
   1. Specifikationerna för detta fält kan anges i **[!UICONTROL Settings]** efter att du klickat på fältet.

### Lägg till anpassad metadataegenskap i schemaredigeraren {#add-custom-metadata-property-in-schema-editor}

1. Navigera till fliken (befintlig eller ny) där du vill lägga till den anpassade egenskapen.

1. Dra en komponent av önskad typ från **[!UICONTROL Build Form]** till vänster och placera på en lämplig plats.

   >[!NOTE]
   >
   >Du kan inte flytta de låsta avsnitten, men du kan placera komponenten i något av de tomma utrymmena.

1. Klicka på en komponent som du just har dragit. Fyll i information för följande fält på fliken Inställningar som öppnas i den högra panelen:

   1. Ange en fältetikett som ska användas som visningsnamn ovanför fältet som placeras i schemat (till exempel: Avdelning)
   1. I egenskapsfältet Mappa till kan du se ett förifyllt värde **&#39;./jcr:content/metadata/default&#39;**. Ändra &#39;**standard**&#39; till ett önskat egenskapsnamn, som används för att lagra egenskapen i crx-databasen (till exempel: &#39;./jcr:content/metadata/dec&#39;)

      >[!NOTE]
      >
      >Ändra inte prefixet &#39;./jcr:content/metadata/&#39; när den definierar sökvägen där egenskapen lagras.
      >
      >Egenskapsnamnet måste också vara unikt för att du inte ska kunna skriva värden för två eller flera egenskaper på samma plats i databasen. Vi rekommenderar att du ändrar värdet &#39;default&#39;.

   1. Fyll i andra inställningar baserat på behov. Till exempel: Välj alternativet Obligatoriskt om du vill göra fältet obligatoriskt.
   1. Om du vill ta bort ett fält som du har lagt till markerar du fältet och klickar sedan på borttagningen ![Ta bort](assets/Smock_Delete_18_N.svg) ikon.

1. Om det behövs följer du steg 1-3 för att lägga till en annan egenskap.
1. Klicka **[!UICONTROL Save]** efter att ha gjort alla ändringar.

   Du har lagt till en anpassad metadataegenskap.

Alla adaptiva Forms i [!DNL AEM Forms] innehåller nu den här extra metadataegenskapen. Du kan redigera den från egenskapssidan.
