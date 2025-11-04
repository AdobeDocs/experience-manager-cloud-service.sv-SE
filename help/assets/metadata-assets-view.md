---
title: Hur hanterar man metadata i Assets-vyn?
description: Lär dig hur du hanterar metadata i Assets-vyn. Bättre metadatahantering gör materialet mer tillgängligt, enklare att hantera och komplett.
role: User, Leader, Admin, Architect, Developer
contentOwner: AG
exl-id: 7264e8d1-fc8f-4eb3-93a9-a6066ca3f851
feature: Metadata
source-git-commit: 5dbad509f5a5a9addfe6b52c3c3dd7ce5fa3229d
workflow-type: tm+mt
source-wordcount: '2120'
ht-degree: 0%

---


# Metadata i Assets View {#metadata}

Metadata innebär data eller beskrivning av data. Dina bilder som en resurs kan t.ex. innehålla information om kameran som användaren klickade på eller copyright-information. Den här informationen är bildens metadata. Metadata är avgörande för effektiv resurshantering. Metadata är en samling av alla data som är tillgängliga för en tillgång, men de kanske inte nödvändigtvis finns i den tillgången.

Metadata hjälper er att kategorisera resurser ytterligare och är till hjälp när mängden digital information växer. Det går att hantera några hundra filer baserat på bara filnamn, miniatyrbilder och minne. Den här metoden är dock inte skalbar. Den blir kort när antalet inblandade personer och antalet hanterade resurser ökar.

Med hjälp av metadata ökar värdet på en digital resurs eftersom resursen blir:

* Mer åtkomligt - system och användare hittar det enkelt.
* Enklare att hantera - du kan hitta resurser med samma uppsättning egenskaper enklare och använda ändringarna på dem.
* Fullständigt - materialet innehåller mer information och sammanhang med fler metadata.

Därför erbjuder Assets rätt sätt att skapa, hantera och utbyta metadata för digitala resurser.

## Visa metadata {#view-metadata}

Om du vill visa metadata för en resurs bläddrar du till resursen eller söker efter resursen, markerar resursen och klickar på **[!UICONTROL Details]** i verktygsfältet.

![Visa metadata för en resurs](assets/metadata-view.png)

*Figur: Om du vill visa en resurs och dess metadata klickar du på&#x200B;**[!UICONTROL Details]**i verktygsfältet eller dubbelklickar på resursen.*

Grundläggande metadata som titel, beskrivning och överföringsdatum är tillgängliga på fliken [!UICONTROL Basic]. Fliken [!UICONTROL Advanced] innehåller mer avancerade metadata som kameramodell, objektivinformation och geotaggar. Fliken [!UICONTROL Tags] innehåller automatiskt tillämpade taggar baserat på bildens innehåll.

## Uppdatera metadata {#update-metadata}

När administratören har konfigurerat metadataformuläret kan andra fält uppdateras manuellt. Du kanske vill ändra detta eftersom det bara läses baserat på metadataformuläret som finns i rutan.

## Smarta taggar {#smart-tags}

[!DNL Experience Manager Assets] använder artificiell intelligens från [Adobe Sensei](https://www.adobe.com/sensei.html) för att automatiskt tillämpa relevanta taggar på alla dina överförda resurser. Dessa taggar, som kallas smarta taggar, ökar innehållshastigheten i dina projekt genom att hjälpa dig att snabbt hitta relevanta resurser. De smarta taggarna är ett exempel på metadata som inte finns i bilden.

De smarta taggarna används nästan i realtid och genereras baserat på bildens innehåll. När du överför en resurs visas [!UICONTROL Processing] på miniatyrbilden för resursen en tid. När bearbetningen är klar kan du [visa metadata](#view-metadata) och smarta taggar.

![Visa smarta taggar för en resurs](assets/metadata-view-tags.png)

*Figur: Om du vill visa smarta taggar för en resurs klickar du på&#x200B;**[!UICONTROL Details]**i verktygsfältet eller dubbelklickar på resursen.*

Smarta taggar innehåller också ett konfidensintervall som ett procenttal. Det anger förtroendet som är kopplat till den tillämpade taggen. Du kan moderera de automatiskt tillämpade smarta taggarna.

## Lägga till eller uppdatera nyckelord {#manually-tag}

Du kan lägga till fler taggar i dina resurser, utöver de smarta taggar som läggs till automatiskt med den smarta tjänsten [!DNL Adobe Sensei]. Öppna en resurs för förhandsgranskning, klicka på [!UICONTROL Tags] och skriv önskade nyckelord i fältet [!UICONTROL Keywords]. Om du vill lägga till taggen trycker du på Retur. [!DNL Assets view] indexerar nyckelordet i nästan realtid och ditt team kan snart söka efter uppdaterade resurser med de nya nyckelorden.

Du kan också ta bort taggar från avsnittet [!UICONTROL Smart Tags] som automatiskt läggs till av [!DNL Assets view] till alla överförda resurser.

## Taxonomihantering {#taxonomy-management}

Taggar kan också kapslas i en hierarki för att stödja relationer som kategori och underkategori. Om du behöver infoga hierarkiska taggar hanteras de enkelt av Administratör i [!UICONTROL Taxonomy Management]-avsnittet i [!UICONTROL Settings]. Du kan skapa en styrd uppsättning namnutrymmen och taggar som alla användare kan använda när de beskriver innehållet. Det är bara administratörer som kan konfigurera tagghierarkier i [!UICONTROL Taxonomy Manager] och se till att värdena kontrolleras och används på ett konsekvent sätt.

## Konfigurera metadata-Forms {#metadata-forms}

>[!CONTEXTUALHELP]
>id="assets_metadata_forms"
>title="Metadata Forms"
>abstract="[!DNL Experience Manager Assets] innehåller många standardmetadatafält som standard. Organisationer har ytterligare metadatabehov och behöver fler metadatafält för att kunna lägga till företagsspecifika metadata. Med metadataformulär kan företag lägga till anpassade metadatafält på sidan Detaljer för en resurs. De företagsspecifika metadata förbättrar styrningen och identifieringen av dess resurser."

I Assets-vyn finns många standardmetadatafält som standard. Organisationer har ytterligare metadatabehov och behöver fler metadatafält för att kunna lägga till företagsspecifika metadata. Med metadataformulär kan företag lägga till anpassade metadatafält på sidan [!UICONTROL Details] för en resurs. De företagsspecifika metadata förbättrar styrningen och identifieringen av dess resurser. Du kan skapa formulär från grunden eller återanvända ett befintligt formulär.

Du kan konfigurera metadataformulär för olika typer av resurser (olika MIME-typer). Använd samma formulärnamn som filens MIME-typ. Assets-vyn matchar automatiskt MIME-typen för överförda resurser med namnet på formuläret och uppdaterar metadata för överförda resurser baserat på formulärfälten.
<!--
For example, if a metadata form by the name `PDF` or `pdf` exists, then the uploaded PDF documents contain metadata fields as defined in the form.
-->
I Assets-vyn används följande sekvens för att söka efter befintliga metadataformulärnamn för att tillämpa metadatafälten på de överförda resurserna av en viss typ:

MIME-undertyp > MIME-typ > `default`-formulär > Formulär som inte finns i kartongen

Om det till exempel finns ett metadataformulär med namnet `PDF` eller `pdf` innehåller de överförda PDF-dokumenten metadatafält som definierats i formuläret. Om det inte finns något metadataformulär med namnet `PDF` eller `pdf` matchar Assets-vyn om det finns ett metadataformulär med namnet `application`. Om det finns ett metadataformulär med namnet `application` innehåller de överförda PDF-dokumenten metadatafält som definierats i formuläret. Om Assets-vyn fortfarande inte hittar något matchande metadataformulär söker den efter metadataformuläret `default` för att använda metadatafält som definierats i formuläret på de överförda PDF-dokumenten. Om inget av dessa steg fungerar använder Assets-vyn metadatafält som är definierade i det färdiga formuläret för alla överförda PDF-dokument.
Om du vill tilldela ett metadataformulär till en mapp [se](#assign-metadata-form-folder).

>[!IMPORTANT]
>
>Det nya metadataformuläret för en viss filtyp ersätter helt standardmetadataformuläret som [!DNL Assets view] tillhandahåller. Om du tar bort eller byter namn på ett metadataformulär är standardmetadatafälten igen tillgängliga för nya resurser.

Så här skapar du ett metadataformulär:

1. Klicka på **[!UICONTROL Settings]** > **[!UICONTROL Metadata Forms]** i den vänstra listen.

   Alternativet ![metadataformulär i det vänstra sidofältet](assets/metadata-forms-sidebar.png)

1. Klicka på **[!UICONTROL Create]** i det övre högra hörnet av användargränssnittet.
1. Ange ett namn för formuläret och klicka på **[!UICONTROL Create]**.
1. Ange ett namn för fliken i **[!UICONTROL Settings]** i den högra listen.
1. Dra de nödvändiga komponenterna från den **[!UICONTROL Components]** som finns i den vänstra listen på en flik i formuläret. Dra komponenterna i önskad sekvens.

   Alternativet ![metadataformulär i det vänstra sidofältet](assets/metadata-form-new.png)

   *Figur: Gränssnitt för att skapa metadataformulär med alternativ för att lägga till komponenter och alternativ för att förhandsgranska formuläret.*

1. För varje komponent anger du ett namn i **[!UICONTROL Settings]** i den högra listen och anger en mappning med de egenskaper som stöds.
1. Om du vill kan du för en komponent välja **[!UICONTROL Required]** för att göra metadatafältet obligatoriskt och välja **[!UICONTROL Read-Only]** för att göra fältet icke-redigerbart på sidan för resursen [!UICONTROL Details].
1. Du kan också klicka på **[!UICONTROL Preview]** om du vill förhandsgranska formuläret som du skapar.
1. Du kan också lägga till fler flikar och de nödvändiga komponenterna på varje flik.
1. Klicka på **[!UICONTROL Save]** när formuläret är klart.

I den här videon visas stegsekvensen:

>[!VIDEO](https://video.tv.adobe.com/v/341275)

När ett formulär har skapats används det automatiskt när användare överför en resurs av den matchande MIME-typen.

Om du vill återanvända ett befintligt formulär för att skapa ett nytt, markerar du ett metadataformulär, klickar på **[!UICONTROL Copy]** i verktygsfältet, anger ett namn och klickar på **[!UICONTROL Confirm]**. Du kan redigera ett metadataformulär om du vill ändra det. När du ändrar ett formulär används det för resurser som överförts efter ändringen. De befintliga resurserna ändras inte.

### Egenskapskomponenter {#property-components}

Du kan anpassa metadataformuläret med någon av följande egenskapskomponenter. Dra och släpp komponenttypen i formuläret där du vill ha den och ändra komponentinställningarna.
Nedan visas en översikt över varje egenskapstyp och hur de lagras.

| Komponentnamn | Beskrivning |
|---|---|
| Dragspelsbehållare | Lägg till en rubrik för en lista med gemensamma komponenter och egenskaper. Den kan expanderas eller komprimeras som standard. |
| Enkelradig text | Lägg till en enkelradig textegenskap. |
| Flerradstext | Lägg till flera textrader eller ett stycke. Den utökas som en användartyp och innehåller allt innehåll. |
| Text med flera värden | Lägg till en textegenskap med flera värden. |
| Nummer | Lägg till en sifferkomponent. |
| Kryssruta | Lägg till ett booleskt värde. Lagras som TRUE eller FALSE när ett värde har sparats. |
| Datum | Lägg till en datumkomponent. |
| Nedrullningsbar meny | Lägg till en listruta. |
| Läge | Lägg till egenskapen för databastillstånd (mappas till repo:state) |
| Resursstatus | Lägg till standardegenskapen Resursstatus (mappad till dam:assetStatus) |
| Taggar | Lägg till en tagg från värden som lagras i taxonomihantering (mappas till xcm:tags). |
| Nyckelord | Lägg till nyckelord med valfri form (mappas till dc:subject). |
| Smarta taggar | Förbättra sökfunktionerna genom att automatiskt lägga till metadatataggar. |

### Tilldela metadataformulär till en mapp {#assign-metadata-form-folder}

Du kan också tilldela ett metadataformulär till en mapp i din Assets-vydistribution. Metadataformuläret som tilldelats en mapp enligt MIME-typen skrivs över när du tillämpar ett metadataformulär manuellt på en mapp. Alla resurser i mappen, inklusive resurser i undermapparna, visar sedan egenskaper som definierats i metadataformuläret.

Så här tilldelar du ett metadataformulär till en mapp:

1. Navigera till **[!UICONTROL Settings]** > **[!UICONTROL Metadata Forms]** och markera ett metadataformulär.

2. Klicka på **[!UICONTROL Assign to Folder]**.

3. Markera mappen och klicka på **[!UICONTROL Assign]**. Du kan markera mapparna genom att klicka på mappnamnen.

   ![tilldela metadataformulär till en mapp](assets/assign-to-folder.png)

   Du kan också navigera till mappinformationssidan och välja ett metadataformulär från mappegenskaperna som är tillgängliga i den högra rutan för att tilldela metadataformuläret till mappen.

   ![Metadataformulär från mappegenskaper](assets/metadata-from-folder-props.png)

### Ta bort metadataformulär från mappar {#remove-metadata-form-folder}

När du har tilldelat ett metadataformulär till en eller flera mappar kan du även ta bort metadataformulär från de markerade mapparna i Experience Manager Assets.

Så här tar du bort ett metadataformulär från en mapp:

1. Navigera till **[!UICONTROL Settings]** > **[!UICONTROL Metadata Forms]** och markera ett metadataformulär.

1. Klicka på **[!UICONTROL Remove from Folder(s)]**. Listan med tilldelade mappar för metadataformulärvisningen.

1. Markera mappen och klicka på **[!UICONTROL Remove]**. Du kan också välja flera mappar i listan.

Du kan också navigera till sidan med mappinformation och välja **[!UICONTROL System mapped Metadata Form]** i fältet **[!UICONTROL Metadata Forms]** för att ta bort det tilldelade metadataformuläret från en mapp.

### Arbeta med komponenten Länk i metadataformulär {#link-component-metadata-form}

Länkkomponenten används för att aktivera externa URL-adresser som lagringslänkar, copyrightinformation, kontaktformulär och så vidare. Om du vill använda länkkomponenten i metadataformulär måste du [konfigurera metadataformuläret](#metadata-forms).

Följ stegen nedan för att använda länkkomponenten i metadataformuläret:

1. Gå till sidan med resursinformation och navigera till **[!UICONTROL Link URL]**.
1. Lägg till en URL som du vill använda för att omdirigera den valda resursen.
1. Klicka på **[!UICONTROL Add link]**. Utför någon av följande åtgärder:
   * Klicka på ikonen ![kopiera](assets/do-not-localize/copy.svg) för att kopiera URL:en.
   * Klicka på ![redigeringsikonen](assets/do-not-localize/edit.svg) om du vill redigera URL-adressen.
1. Klicka på **[!UICONTROL Save]** om du vill spara ändringarna.

### Arbeta med taggkomponenten i metadataformulär {#tag-component-metadata-form}

Rotelementet representerar trädstrukturen för de taggar som du kan associera med resurserna, vilket hjälper till att identifiera resursen baserat på taggen som tilldelats den. Dessutom kan du begränsa åtkomsten till en viss taxonomi när du konfigurerar metadataformuläret i metadataredigeraren.

#### Konfiguration av taggkomponent {#tags-component-configuration}

Konfigurera taggkomponenten genom att utföra följande steg:

1. Gå till metadataredigeraren och navigera till **[!UICONTROL Tags]** och placera den på arbetsytan.
1. Byt namn på komponenten på arbetsytan. Det gör du genom att gå till **[!UICONTROL Label]** under [!UICONTROL Metadata property] på inställningspanelen och lägga till texten för identifieringen.
1. Under [!UICONTROL Metadata property] på inställningspanelen söker du efter metadataegenskapen som du vill tilldela komponenten.
1. Klicka på **[!UICONTROL Restrict to specific taxonomy]** om du vill begränsa taxonomins rotsökväg. Det gör du genom att bläddra bland taggarna och välja taxonomin till den specifika sökvägen.
1. Klicka på **[!UICONTROL Save]** om du vill spara ändringarna.

   ![Konfiguration av rottaggar](assets/root-tag-config.png)

1. [Tilldela metadata till mappar](#assign-metadata-form-folder).

<!--
#### Mapping between assets and taxonomy {#asset-taxonomy-mapping}

See [Assign metadata form to folders](#assign-metadata-form-folder). Follow the steps below to perform mapping between folder and taxonomy:

1. Go back to the Settings and click **[!UICONTROL Metadata forms]** 
1. Select a Metadata form that needs mapping. 
1. Click **[!UICONTROL Assign to folder(s)]**. **[!UICONTROL Select Folder(s)]** screen appears. 
1. Navigate to the folder that you want to assign to the metadata form. You can select multiple folders.
1. Click **[!UICONTROL Assign]**.
-->

Om du vill visa de konfigurerade rottaggarna går du till objektets informationssida där mappningen mellan metadataformuläret och rottaggarna utförs.

## Redigera metadata-Forms {#edit-metadata-forms}

Så här redigerar du ett metadataformulär:

1. Navigera till startsidan för [!DNL Assets View] och välj **[!DNL Metadata Forms]** för att visa en lista med metadataformulär.
1. Markera ett formulär och klicka på **[!UICONTROL Edit]** för att öppna sidan [!DNL Metadata Form Editor]. Den här sidan visar komponenter i metadataformuläret i den vänstra rutan, flikar som Grundläggande, Avancerat, Taggar med mera i den mellersta rutan och inställningspanelen för redigering av metadataegenskaperna i den högra rutan.
1. Öppna en flik (**[!DNL Basic]**, **[!DNL Advanced]** eller **[!DNL Tags]**).
1. Välj en metadataegenskap om du vill redigera dess inställningar på panelen **[!UICONTROL Settings]**. Du kan uppdatera egenskapsmappningar, byta namn på etiketter, ändra eller lägga till egenskapsvärden och utföra fler sådana redigeringar på panelen **[!UICONTROL Settings]**.
1. Klicka på **[!UICONTROL Preview]** om du vill granska ändringarna i formuläret innan du sparar ändringarna.
1. Klicka på **[!UICONTROL Save]** för att tillämpa ändringarna.

## Nästa steg {#next-steps}

* [Titta på en video om hur du hanterar metadataformulär i Assets-vyn](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/configuring/metadata-forms.html)

* Ge produktfeedback med alternativet [!UICONTROL Feedback] som finns i användargränssnittet i Assets-vyn

* Ge feedback om dokumentationen med [!UICONTROL Edit this page] ![redigera sidan](assets/do-not-localize/edit-page.png) eller [!UICONTROL Log an issue] ![skapa ett GitHub-problem](assets/do-not-localize/github-issue.png) som är tillgängligt på den högra sidopanelen

* Kontakta [kundtjänst](https://experienceleague.adobe.com/?support-solution=General#support)

<!-- TBD: Cannot create a form using the second option. Documenting only the first option for now.
To reuse an existing form to create a form, do one of these:

* Select a metadata form and click **[!UICONTROL Copy]** from the toolbar, provide a name, and click **[!UICONTROL Confirm]**.

* Click **[!UICONTROL Create]**, select **[!UICONTROL Use existing form structure as template]** option, and select an existing form. 
-->

<!-- TBD: Queries for PM and engg.

Can we edit the existing metadata in any form?

How to moderate smart tags?

Allow or deny list for smart tags?

What about Tags displayed just above Smart Tags in the UI?

Is there a detailed metadata tab. Where do the other details of an asset go?

How can one search based strictly on the metadata. Similar to AEM Assets GQL queries.
-->

<!-- TBD: Link to related articles if any.

>[!MORELIKETHIS]
>
>* [Search assets](search.md).
-->