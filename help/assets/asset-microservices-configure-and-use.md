---
title: Konfigurera och använda resursmikrotjänster
description: Konfigurera och använd de molnbaserade resursmeritjänsterna för att bearbeta resurser i stor skala.
contentOwner: AG
feature: Asset Compute Microservices, Asset Processing, Asset Management
role: Architect, Admin
exl-id: 7e01ee39-416c-4e6f-8c29-72f5f063e428
source-git-commit: 979c4accca8b271ba2ff0ba176985c94b6d469c7
workflow-type: tm+mt
source-wordcount: '2863'
ht-degree: 0%

---

# Använda mikrotjänster och bearbetningsprofiler {#get-started-using-asset-microservices}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Resursmikrotjänster ger skalbar och flexibel bearbetning av resurser med molnbaserade program (kallas även arbetare). Adobe hanterar tjänsterna för optimal hantering av olika tillgångstyper och bearbetningsalternativ.

Med tillgångsmikrotjänster kan du bearbeta ett [brett urval av filtyper](/help/assets/file-format-support.md) som omfattar fler format som är körklara än vad som är möjligt med tidigare versioner av [!DNL Experience Manager]. Miniatyrbildextrahering av PSD och PSB-format är nu möjligt men tidigare krävda tredjepartslösningar som [!DNL ImageMagick].

Resursbearbetningen beror på konfigurationen i **[!UICONTROL Processing Profiles]**. Experience Manager har en grundläggande standardinställning och ger administratörer möjlighet att lägga till mer specifik konfiguration för bearbetning av resurser. Administratörer kan skapa, underhålla och ändra konfigurationerna för efterbehandlingsarbetsflöden, inklusive valfri anpassning. Genom att anpassa arbetsflödena kan utvecklarna utöka standarderbjudandet.

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![En högnivåvy över bearbetning av resurser](assets/asset-microservices-flow.png "En högnivåvy över bearbetning av resurser")

>[!NOTE]
>
>Resursbearbetningen som beskrivs här ersätter arbetsflödesmodellen `DAM Update Asset` som finns i tidigare versioner av [!DNL Experience Manager]. Bearbetningen av resursmikrotjänster ersätter de flesta standardgenereringen av återgivningar och metadatarelaterade steg, och efterbearbetningsarbetsflödets konfiguration kan ersätta de återstående stegen, om några sådana finns.

## Förstå alternativ för tillgångsbearbetning {#get-started}

[!DNL Experience Manager] tillåter följande bearbetningsnivåer.

| Alternativ | Beskrivning | Användningsexempel som täcks |
|---|---|---|
| [Standardkonfiguration](#default-config) | Den är tillgänglig som den är och kan inte ändras. Den här konfigurationen har en grundläggande funktion för att skapa renderingar. | <ul> <li>Standardminiatyrbilder som används i användargränssnittet för [!DNL Assets] (48, 140 och 319 pixlar) </li> <li> Stor förhandsgranskning (webbåtergivning - 1 280 pixlar) </li><li> Metadata och textrahering.</li></ul> |
| [Anpassad konfiguration](#standard-config) | Konfigureras av administratörer via användargränssnittet. Fler alternativ finns för generering av återgivning genom att utöka standardalternativet. Utöka det färdiga alternativet om du vill ha olika format och renderingar. | <ul><li>FPO-återgivning (endast för placering). </li> <li>Ändra filformat och upplösning för bilder</li> <li> Tillämpa villkoren på konfigurerade filtyper. </li> </ul> |
| [Egen profil](#custom-config) | Konfigureras av administratörer via användargränssnittet för att använda anpassad kod via anpassade program för att anropa [Asset Compute-tjänsten](https://experienceleague.adobe.com/en/docs/asset-compute/using/introduction). Stöder mer komplexa krav med en molnbaserad och skalbar metod. | Se [tillåtna användningsfall](#custom-config). |

<!-- To create custom processing profiles specific to your custom requirements, say to integrate with other systems, see [post-processing workflows](#post-processing-workflows).
-->

## Filformat som stöds {#supported-file-formats}

Resursmikrotjänsterna har stöd för en mängd olika filformat för att bearbeta, generera renderingar eller extrahera metadata. I [filformat som stöds](file-format-support.md) finns en fullständig lista över MIME-typer och de funktioner som stöds för varje typ.

## Standardkonfiguration {#default-config}

Vissa standardinställningar är förkonfigurerade för att säkerställa att standardåtergivningarna som krävs i Experience Manager är tillgängliga. Standardkonfigurationen ser också till att metadataextrahering och textrahering är tillgängliga. Användare kan börja ladda upp eller uppdatera resurser direkt och grundläggande bearbetning är tillgänglig som standard.

Med standardkonfigurationen konfigureras bara den mest grundläggande bearbetningsprofilen. En sådan bearbetningsprofil visas inte i användargränssnittet och du kan inte ändra den. Det körs alltid för att bearbeta överförda resurser. En sådan standardbearbetningsprofil ser till att den grundläggande bearbetning som krävs av [!DNL Experience Manager] har slutförts för alla resurser.

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## Standardkonfiguration {#standard-config}

[!DNL Experience Manager] innehåller funktioner för att generera mer specifika återgivningar för vanliga format utifrån användarens behov. En administratör kan skapa ytterligare [!UICONTROL Processing Profiles] för att underlätta skapandet av en sådan återgivning. Användarna tilldelar sedan en eller flera av de tillgängliga profilerna till specifika mappar för att få den ytterligare bearbetningen klar. Den extra bearbetningen kan till exempel generera renderingar för webben, mobiler och surfplattor. I följande video visas hur du skapar och använder [!UICONTROL Processing Profiles] och hur du får åtkomst till de återgivningar som skapas.

* **Återgivningsbredd och -höjd**: I specifikationen för återgivningsbredd och -höjd finns maximala storlekar för den genererade utdatabilden. Resursmikrotjänsterna försöker skapa den största möjliga återgivningen, som inte är större än den angivna bredden och höjden. Proportionerna bevaras, det vill säga de ursprungliga. Ett tomt värde innebär att resursbearbetningen baseras på originalets pixeldimension.

* **Inkluderingsregler för MIME-typ**: När en resurs med en viss MIME-typ bearbetas kontrolleras MIME-typen först mot det utelämnade MIME-typvärdet för återgivningsspecifikationen. Om den matchar den listan genereras inte den här specifika återgivningen för resursen (blockeringslista). Annars kontrolleras MIME-typen mot den inkluderade MIME-typen, och om den matchar listan genereras återgivningen (tillåtelselista).

* **Särskild FPO-återgivning**: När stora resurser från [!DNL Experience Manager] monteras i [!DNL Adobe InDesign] -dokument väntar en kreatör en avsevärd tid efter att de [har placerat ut en resurs](https://helpx.adobe.com/indesign/using/placing-graphics.html). Under tiden har användaren blockerats från att använda [!DNL InDesign]. Detta stör det kreativa flödet och påverkar användarupplevelsen negativt. Med Adobe kan du tillfälligt placera små återgivningar i [!DNL InDesign]-dokument till att börja med, vilket kan ersättas med högupplösta resurser på begäran senare. [!DNL Experience Manager] innehåller återgivningar som bara används för placering. Dessa FPO-återgivningar har en liten filstorlek men har samma proportioner.

Bearbetningsprofilen kan innehålla en FPO-återgivning (endast för placering). Läs [!DNL Adobe Asset Link] [dokumentationen](https://helpx.adobe.com/se/enterprise/using/manage-assets-using-adobe-asset-link.html) om du behöver aktivera den för din bearbetningsprofil. Mer information finns i den fullständiga dokumentationen för [Adobe-resurslänken](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html).

### Skapa en standardprofil {#create-standard-profile}

Så här skapar du en standardbearbetningsprofil:

1. Administratörer har åtkomst till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Processing Profiles]**. Klicka på **[!UICONTROL Create]**.
1. Ange ett namn som hjälper dig att identifiera profilen unikt när du använder den i en mapp.
1. Aktivera **[!UICONTROL Create FPO Rendition]** på fliken **[!UICONTROL Image]** om du vill generera FPO-återgivningar. Ange ett **[!UICONTROL Quality]**-värde från 1-100.
1. Om du vill generera andra återgivningar klickar du på **[!UICONTROL Add New]** och anger följande information:

   * Filnamn för varje återgivning.
   * Filformat (PNG, JPEG, GIF eller WebP) för varje återgivning.
   * Bredd och höjd i pixlar för varje återgivning. Om värdena inte anges används den ursprungliga bildens fullständiga pixelstorlek.
   * Kvalitet i procent av varje JPEG- och WebP-återgivning.
   * Inkluderade och exkluderade MIME-typer för att definiera en profils tillämplighet.

   ![processing-profiles-adding](assets/processing-profiles-image.png)

1. Klicka på **[!UICONTROL Save]**.

<!-- TBD: Update the video link when a new video is available from Tech Marketing.

The following video demonstrates the usefulness and usage of standard profile.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)
-->

<!-- This image was removed per cqdoc-15624, as requested by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## Anpassade profil- och användningsfall {#custom-config}

[!DNL Asset Compute Service] har stöd för en mängd olika användningsfall, inklusive standardbearbetning och bearbetning av Adobe-specifika format som Photoshop-filer. Det gör det även möjligt att implementera anpassad eller organisationsspecifik bearbetning. Den anpassning av arbetsflödet för DAM-uppdatering av tillgångar som tidigare krävdes hanteras antingen automatiskt eller genom att konfigurationen för profiler bearbetas. Om dessa bearbetningsalternativ inte uppfyller dina affärsbehov rekommenderar Adobe att du utvecklar och använder [!DNL Asset Compute Service] för att utöka standardfunktionerna. En översikt finns i [Förstå utökningsmöjligheter och när du ska använda dem](https://experienceleague.adobe.com/en/docs/asset-compute/using/extend/understand-extensibility).

>[!NOTE]
>
>Adobe rekommenderar att du bara använder ett anpassat program när affärskraven inte kan uppfyllas med standardkonfigurationerna eller standardprofilen.

Det kan omvandla bild, video, dokument och andra filformat till olika renderingar, bland annat miniatyrbilder, extraherad text och metadata samt arkiv.

Utvecklare kan använda [!DNL Asset Compute Service] för att [skapa anpassade program](https://experienceleague.adobe.com/en/docs/asset-compute/using/extend/develop-custom-application) för de användningsområden som stöds. [!DNL Experience Manager] kan anropa dessa anpassade program från användargränssnittet med hjälp av anpassade profiler som administratörer konfigurerar. [!DNL Asset Compute Service] har stöd för följande användningsfall för anrop av externa tjänster:

* Använd [ImageCutout API](https://developer.adobe.com/photoshop/photoshop-api-docs/) för [!DNL Adobe Photoshop] och spara resultatet som en återgivning.
* Anropa tredjepartssystem för att göra ändringar, till exempel ett PIM-system.
* Använd API:t [!DNL Photoshop] för att skapa en mängd olika återgivningar baserade på Photoshop-mallen.
* Använd [Adobe Lightroom API](https://developer.adobe.com/photoshop/photoshop-api-docs/) för att optimera de kapslade resurserna och spara dem som återgivningar.

>[!NOTE]
>
>Du kan inte redigera standardmetadata med de anpassade programmen. Du kan bara ändra anpassade metadata.

### Skapa en anpassad profil {#create-custom-profile}

Så här skapar du en anpassad profil:

1. Administratörer har åtkomst till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Processing Profiles]** > **[!UICONTROL Create]**.
1. Klicka på fliken **[!UICONTROL Custom]** på sidan Bearbeta profil och klicka sedan på **[!UICONTROL Add New]**.
1. I textfältet Namn skriver du önskat filnamn för återgivningen och anger sedan följande information.

   * Filnamn för varje återgivning och ett filtillägg som stöds.
   * [Slutpunkts-URL för en anpassad App Builder-app](https://experienceleague.adobe.com/en/docs/asset-compute/using/extend/deploy-custom-application). Appen måste komma från samma organisation som Experience Manager-kontot.
   * Lägg till tjänstparametrar i [skicka extra information eller parametrar till det anpassade programmet](https://experienceleague.adobe.com/en/docs/asset-compute/using/extend/develop-custom-application#extend).
   * Inkluderade och exkluderade MIME-typer för att begränsa bearbetningen till ett fåtal specifika filformat.

1. Klicka på **[!UICONTROL Save]** i det övre högra hörnet på sidan.

De anpassade programmen är headless [Project App Builder](https://developer.adobe.com/app-builder/docs/overview/)-appar. Ditt anpassade program hämtar alla angivna filer om de har konfigurerats med en bearbetningsprofil. Programmet måste filtrera filerna.

>[!CAUTION]
>
>Om App Builder-programmet och [!DNL Experience Manager]-kontot inte kommer från samma organisation fungerar inte integreringen.

### Ett exempel på en anpassad profil {#custom-profile-example}

För att illustrera hur den anpassade profilen används ska vi överväga ett användningsexempel för att använda anpassad text på kampanjbilder. Du kan skapa en bearbetningsprofil som använder Photoshop API för att redigera bilderna.

Integrering med Asset Compute Service gör att Experience Manager kan skicka dessa parametrar till det anpassade programmet med hjälp av fältet [!UICONTROL Service Parameters]. Det anpassade programmet anropar sedan Photoshop API och skickar dessa värden till API:t. Du kan till exempel skicka teckensnittsnamn, textfärg, textvikt och textstorlek för att lägga till den anpassade texten i kampanjbilder.

<!-- TBD: Check screenshot against the interface. -->

![custom-processing-profile](assets/custom-processing-profile.png)

*Figur: Använd fältet [!UICONTROL Service Parameters] för att skicka tillagd information till fördefinierade parametrar som byggs in i det anpassade programmet. I det här exemplet uppdateras bilderna med `Jumanji` text i `Arial-BoldMT` font när kampanjbilder överförs.*

## Använda bearbetningsprofiler för att bearbeta resurser {#use-profiles}

Skapa och använd ytterligare egna bearbetningsprofiler för specifika mappar. Med det här arbetsflödet kan Experience Manager bearbeta resurser som har överförts till eller uppdaterats i dessa mappar. Den inbyggda standardbearbetningsprofilen körs alltid som standard, men visas inte i användargränssnittet. Om du lägger till en anpassad profil används båda profilerna för att bearbeta de överförda resurserna.

Använd bearbetningsprofiler på mappar på något av följande sätt:

* Administratörer kan välja en bearbetningsprofildefinition i **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Processing Profiles]** och använda åtgärden **[!UICONTROL Apply Profile to Folders]**. Den öppnar en innehållsläsare där du kan navigera till specifika mappar och markera dem och sedan bekräfta hur profilen används.
* Användare kan välja en mapp i Assets användargränssnitt och använda åtgärden **[!UICONTROL Properties]** för att öppna skärmen för mappegenskaper. På fliken **[!UICONTROL Asset Processing]** kan de välja lämplig bearbetningsprofil för den mappen i listan [!UICONTROL Processing Profile]. Klicka på **[!UICONTROL Save & Close]** om du vill spara ändringarna.
  ![Använd bearbetningsprofil på en mapp från fliken Resursegenskaper](assets/folder-properties-processing-profile.png)

* Användare kan välja mappar eller specifika resurser i Assets användargränssnitt för att tillämpa en bearbetningsprofil och sedan välja alternativet ![Ikon för ombearbetning av resurser](assets/do-not-localize/reprocess-assets-icon.png) **[!UICONTROL Reprocess Assets]** bland de tillgängliga alternativen överst.

>[!TIP]
>
>Endast en bearbetningsprofil kan användas för en mapp. Om du vill generera fler återgivningar lägger du till fler återgivningsdefinitioner i den befintliga bearbetningsprofilen.

När en bearbetningsprofil har tillämpats på en mapp bearbetas alla nya resurser som har överförts (eller uppdaterats) i den här mappen eller någon av dess undermappar med hjälp av den extra bearbetningsprofil som har konfigurerats. Den här bearbetningen är utöver standardprofilen.

>[!NOTE]
>
>En bearbetningsprofil som tillämpas på en mapp fungerar för hela trädet, men kan åsidosättas av en annan profil som tillämpas på en undermapp. När resurser överförs till en mapp kontrollerar Experience Manager egenskaperna för den innehållande mappen för att hitta en bearbetningsprofil. Om ingen används kontrolleras en överordnad mapp i hierarkin för att en bearbetningsprofil ska användas.

Kontrollera att resurserna bearbetas genom att förhandsgranska de genererade återgivningarna i vyn [!UICONTROL Renditions] i den vänstra listen. Öppna förhandsgranskningen av resursen och öppna den vänstra listen för att komma åt vyn **[!UICONTROL Renditions]**. De specifika återgivningarna i bearbetningsprofilen, för vilka den specifika resursens typ matchar reglerna för MIME-typinkludering, bör vara synliga och tillgängliga.

![extra-renderingar](assets/renditions-additional-renditions.png)

*Bild: Exempel på två extra återgivningar som genereras av en bearbetningsprofil som tillämpas på den överordnade mappen.*

## Efterbehandlingsarbetsflöden {#post-processing-workflows}

Om det krävs ytterligare bearbetning av resurser som inte kan utföras med bearbetningsprofilerna kan ytterligare efterbearbetningsarbetsflöden läggas till i konfigurationen. Med efterbearbetning kan du lägga till helt anpassad bearbetning utöver den konfigurerbara bearbetningen med hjälp av objektmikrotjänster.

När bearbetningen av mikrotjänsterna har slutförts kör [!DNL Experience Manager] automatiskt efterbearbetningsarbetsflöden, eller [Autostart-arbetsflöden](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/configuring/auto-start-workflows) om dessa har konfigurerats. Du behöver inte lägga till startprogram för arbetsflöden manuellt för att utlösa arbetsflödena. Exemplen innehåller:

* Anpassade arbetsflödessteg för att bearbeta resurser.
* Integreringar för att lägga till metadata eller egenskaper i resurser från externa system, till exempel produkt- eller processinformation.
* Ytterligare bearbetning utförs av externa tjänster.

Så här lägger du till en arbetsflödeskonfiguration för efterbearbetning i [!DNL Experience Manager]:

* Skapa en eller flera arbetsflödesmodeller. Dessa anpassade modeller kallas *efterbearbetningsarbetsflödesmodeller* i den här dokumentationen. De är vanliga [!DNL Experience Manager] arbetsflödesmodeller.
* Lägg till de arbetsflödessteg som krävs till dessa modeller. Granska stegen från standardarbetsflödet och lägg till alla nödvändiga standardsteg i det anpassade arbetsflödet. Stegen körs på resurserna baserat på en arbetsflödesmodellkonfiguration. Om du till exempel vill att smart taggning ska ske automatiskt när resurser överförs lägger du till steget i den anpassade arbetsflödesmodellen för efterbearbetning.
* Lägg till steget [!UICONTROL DAM Update Asset Workflow Completed Process] i slutet. Om du lägger till det här steget vet Experience Manager när bearbetningen avslutas och resursen kan markeras som bearbetad. Det innebär att *Nytt* visas på resursen.
* Skapa en konfiguration för tjänsten Custom Workflow Runner som gör att du kan konfigurera körning av en arbetsflödesmodell för efterbearbetning antingen med en sökväg (mappsökväg) eller med ett reguljärt uttryck.

Mer information om vilket standardarbetsflödessteg som kan användas i efterbearbetningsarbetsflödet finns i [arbetsflödessteg i efterbearbetningsarbetsflödet](developer-reference-material-apis.md#post-processing-workflows-steps) i utvecklarreferensen.

### Skapa arbetsflödesmodeller för efterbearbetning {#create-post-processing-workflow-models}

Arbetsflödesmodeller för efterbearbetning är vanliga [!DNL Experience Manager] arbetsflödesmodeller. Skapa olika modeller om du behöver olika bearbetning för olika databasplatser eller resurstyper.

Bearbetningsstegen läggs till efter behov. Du kan använda både de steg som stöds och alla anpassade arbetsflödessteg som är tillgängliga.

Kontrollera att det sista steget i varje efterbearbetningsarbetsflöde är `DAM Update Asset Workflow Completed Process`. I det sista steget ser du till att Experience Manager tar reda på när behandlingen av tillgångar är slutförd.

### Konfigurera arbetsflödeskörning efter bearbetning {#configure-post-processing-workflow-execution}

När objektets mikrotjänster har slutfört bearbetningen av de överförda resurserna kan du definiera ett arbetsflöde för efterbearbetning för att bearbeta resurserna mer. Om du vill konfigurera efterbearbetning med arbetsflödesmodeller kan du göra något av följande:

* [Använd en arbetsflödesmodell i mappen Egenskaper](#apply-workflow-model-to-folder).
* [Konfigurera tjänsten Custom Workflow Runner](#configure-custom-workflow-runner-service).

#### Tillämpa en arbetsflödesmodell på en mapp {#apply-workflow-model-to-folder}

För vanliga fall av efterbearbetning bör du överväga att använda metoden för att tillämpa ett arbetsflöde på en mapp. Så här använder du en arbetsflödesmodell i mappen [!UICONTROL Properties]:

1. Skapa en arbetsflödesmodell.
1. Välj en mapp, klicka på **[!UICONTROL Properties]** i verktygsfältet och klicka sedan på fliken **[!UICONTROL Assets Processing]**.
1. Under **[!UICONTROL Auto-start Workflow]** väljer du önskat arbetsflöde, anger en rubrik för arbetsflödet och sparar sedan ändringarna.

   ![Tillämpa ett efterbearbetningsarbetsflöde på en mapp i dess egenskaper](assets/post-processing-profile-workflow-for-folders.png)

#### Konfigurera tjänsten Custom Workflow Runner {#configure-custom-workflow-runner-service}

Du kan konfigurera tjänsten Custom Workflow Runner för de avancerade konfigurationer som inte kan uppfyllas med en enkel metod genom att tillämpa ett arbetsflöde på en mapp. Ett arbetsflöde som använder ett reguljärt uttryck. Adobe CQ DAM Custom Workflow Runner (`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`) är en OSGi-tjänst. Det innehåller följande två konfigurationsalternativ:

* Efterbehandlingsarbetsflöden efter sökväg (`postProcWorkflowsByPath`): Flera arbetsflödesmodeller kan listas baserat på olika databassökvägar. Separera banor och modeller med ett kolon. Enkla databassökvägar stöds. Mappa dem till en arbetsflödesmodell i sökvägen `/var`. Till exempel: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* Efterbearbetningsarbetsflöden efter uttryck (`postProcWorkflowsByExpression`): Flera arbetsflödesmodeller kan listas baserat på olika reguljära uttryck. Separata uttryck och modeller med kolon. Peka det reguljära uttrycket mot noden Resurs direkt, inte någon av återgivningarna eller filerna. Till exempel: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

Mer information om hur du distribuerar en OSGi-konfiguration finns i [Distribuera till [!DNL Experience Manager]](/help/implementing/deploying/overview.md).

#### Inaktivera arbetsflödeskörning efter bearbetning

När efterbearbetning inte behövs skapar och använder du en tom arbetsflödesmodell i **Automatisk start av arbetsflöde** -valet.

##### Skapa arbetsflödesmodellen Inaktiverad autostart

1. Navigera till **Verktyg** > **Arbetsflöde** > **Modeller**.
1. Klicka på **Skapa** > **Skapa modell** i det övre åtgärdsfältet.
1. Ange en titel och ett namn för den nya arbetsflödesmodellen, till exempel:
   * Titel: Inaktivera autostart av arbetsflöde
   * Namn: disable-auto-start-workflow
1. Klicka på **Klar** för att skapa arbetsflödesmodellen.
1. Markera och redigera den skapade arbetsflödesmodellen
1. I arbetsflödesmodellredigeraren klickar du på **Steg 1** i modelldefinitionen och tar bort den.
1. Klicka på **Steg** på sidopanelen.
1. Dra steget **DAM Update Asset Workflow Completed** till modelldefinitionen.
1. Klicka på **Sidinformation** (bredvid växlingsknappen **Side Panel**) och klicka på **Öppna egenskaper**.
1. Klicka på **Övergående arbetsflöde** på fliken Grundläggande.
1. Klicka på **Spara och stäng** i det övre åtgärdsfältet.
1. Klicka på **Synkronisera** i det övre åtgärdsfältet.
1. Stäng arbetsflödesmodellredigeraren.

##### Använda arbetsflödesmodellen Inaktiverad autostart

Följ stegen som beskrivs i [tillämpa en arbetsflödesmodell på en mapp](#apply-workflow-model-to-folder) och ange **Inaktivera autostart av arbetsflöde** som **autostart av arbetsflöde** för mappar som inte kräver efterbearbetning av resurser.

## Bästa praxis och begränsningar {#best-practices-limitations-tips}

* Tänk på dina behov av alla typer av återgivningar när du utformar arbetsflöden. Om du inte förutser att en återgivning behövs i framtiden tar du bort steget när du skapar den från arbetsflödet. Återgivningar kan inte tas bort gruppvis efteråt. Oönskade återgivningar kan ta upp stora mängder lagringsutrymme efter långvarig användning av [!DNL Experience Manager]. För enskilda resurser kan du ta bort återgivningar manuellt från användargränssnittet. För flera resurser kan du antingen anpassa [!DNL Experience Manager] för att ta bort specifika återgivningar eller ta bort resurserna och överföra dem igen.
* Stödet är för närvarande begränsat till att generera renderingar. Generering av ny resurs stöds inte.
* För närvarande är filstorleksgränsen för metadataextrahering ungefär 15 GB. När du överför mycket stora resurser misslyckas ibland metadataextraheringen.

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publish Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Introduktion till tjänsten Asset Compute](https://experienceleague.adobe.com/en/docs/asset-compute/using/introduction).
>* [Förstå utökningsmöjligheterna och när de ska användas](https://experienceleague.adobe.com/en/docs/asset-compute/using/extend/understand-extensibility).
>* [Skapa anpassade program](https://experienceleague.adobe.com/en/docs/asset-compute/using/extend/develop-custom-application).
>* [MIME-typer som stöds för olika användningsfall](/help/assets/file-format-support.md).

<!-- TBD: 
* How/where can admins check what's already configured and provisioned.
* How/where to request for new provisioning/purchase.
-->
