---
title: Konfigurera och använda resursmikrotjänster för bearbetning av resurser
description: Lär dig hur du konfigurerar och använder molnbaserade resursmeritjänster för att bearbeta resurser i stor skala.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 253231d2c9bafbba72696db36e9ed46b8011c9b3
workflow-type: tm+mt
source-wordcount: '2197'
ht-degree: 0%

---


# Använda mikrotjänster och bearbetningsprofiler {#get-started-using-asset-microservices}

<!--
* Current capabilities of asset microservices offered. If workers have names then list the names and give a one-liner description. (The feature-set is limited for now and continues to grow. So will this article continue to be updated.)
* How to access the microservices. UI. API. Is extending possible right now?
* Detailed list of what file formats and what processing is supported by which workflows/workers process.
* How/where can admins check what's already configured and provisioned.
* How to create new config or request for new provisioning/purchase.

* [DO NOT COVER?] Exceptions or limitations or link back to lack of parity with AEM 6.5.
-->

Resursmikrotjänsterna erbjuder skalbar och flexibel bearbetning av resurser med hjälp av molntjänster. Adobe hanterar tjänsterna för optimal hantering av olika tillgångstyper och bearbetningsalternativ.

Resursbearbetningen beror på konfigurationen i **[!UICONTROL Processing Profiles]**, som tillhandahåller en standardinställning, och gör det möjligt för en administratör att lägga till en mer specifik konfiguration för bearbetning av resurser. Administratörer kan skapa och underhålla konfigurationer för efterbehandlingsarbetsflöden, inklusive valfri anpassning. Genom att anpassa arbetsflöden kan du utöka och göra fullständiga anpassningar.

Med tillgångsmikrotjänster kan du bearbeta ett [stort antal filtyper](/help/assets/file-format-support.md) som omfattar fler format som är klara att användas än vad som är möjligt med tidigare versioner av Experience Manager. Exempelvis är det nu möjligt att extrahera PSD- och PSB-format med miniatyrbilder som tidigare krävde tredjepartslösningar som ImageMagick.

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![En högnivåvy över](assets/asset-microservices-flow.png "bearbetning av tillgångarEn högnivåvy över bearbetning av tillgångar")

>[!NOTE]
>
>Resursbearbetningen som beskrivs här ersätter arbetsflödesmodellen som finns i tidigare versioner av `DAM Update Asset` [!DNL Experience Manager]. De flesta standardstegen för generering av återgivning och metadatarelaterade steg ersätts av bearbetningen av resursmikrotjänsterna, och eventuella återstående steg kan ersättas av arbetsflödeskonfigurationen för efterbearbetning.

## Förstå alternativ för tillgångsbearbetning {#get-started}

Experience Manager tillåter följande bearbetningsnivåer.

| Konfiguration | Beskrivning | Användningsexempel |
|---|---|---|
| [Standardkonfiguration](#default-config) | Den är tillgänglig som den är och kan inte ändras. Den här konfigurationen har mycket grundläggande funktioner för att skapa renderingar. | Standardminiatyrbilder som används i [!DNL Assets] användargränssnittet (48, 140 och 319 px). Stor förhandsgranskning (webbåtergivning - 1 280 pixlar); Metadata och textrahering. |
| [Standardkonfiguration](#standard-config) | Konfigureras endast av administratörer via användargränssnittet. Ger fler alternativ för generering av återgivning än standardkonfigurationen ovan. | Ändra bildformat och upplösning, generera FPO-återgivningar. |
| [Anpassad konfiguration](#custom-config) | Konfigureras av administratörer via användargränssnittet för att anropa anpassade arbetare som stöder mer komplexa krav. Utnyttjar ett molnbaserat [!DNL Asset Compute Service]program. | Se [tillåtna användningsfall](#custom-config). |

Mer information om hur du skapar anpassade bearbetningsprofiler som är specifika för dina egna behov, t.ex. för integrering med andra system, finns i [Efterbehandlingsarbetsflöden](#post-processing-workflows).

## Filformat som stöds {#supported-file-formats}

Resursmikrotjänsterna har stöd för en mängd olika filformat när det gäller möjligheten att generera återgivningar eller extrahera metadata. En fullständig lista finns i [filformat](file-format-support.md) som stöds.

## Standardkonfiguration {#default-config}

Vissa standardinställningar är förkonfigurerade för att säkerställa att standardåtergivningarna som krävs i Experience Manager är tillgängliga. Standardkonfigurationen ser också till att metadataextrahering och textrahering är tillgängliga. Användare kan börja ladda upp eller uppdatera resurser direkt och grundläggande bearbetning är tillgänglig som standard.

Med standardkonfigurationen konfigureras bara den mest grundläggande bearbetningsprofilen. En sådan bearbetningsprofil visas inte i användargränssnittet och du kan inte ändra den. Det körs alltid för att bearbeta överförda resurser. En sådan standardbearbetningsprofil ser till att den grundläggande bearbetning som krävs av [!DNL Experience Manager] slutförs för alla resurser.

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## Standardprofil {#standard-config}

[!DNL Experience Manager] har funktioner för att generera mer specifika renderingar för vanliga format efter användarens behov. En administratör kan skapa ytterligare [!UICONTROL Processing Profiles] för att underlätta skapandet av en sådan återgivning. Användarna tilldelar sedan en eller flera av de tillgängliga profilerna till specifika mappar för att få den ytterligare bearbetningen klar. Den extra bearbetningen kan till exempel generera renderingar för webben, mobiler och surfplattor. I följande video visas hur du skapar och använder [!UICONTROL Processing Profiles] och hur du får tillgång till de återgivningar som skapas.

* **Återgivningens bredd och höjd**: Specifikationen för återgivningens bredd och höjd ger maximala storlekar för den genererade utdatabilden. Resursmikrotjänsterna försöker skapa den största möjliga återgivningen, som inte är större än den angivna bredden och höjden. Proportionerna bevaras, det vill säga de ursprungliga. Ett tomt värde innebär att resursbearbetningen baseras på originalets pixeldimension.

* **Inkluderingsregler** för MIME-typ: När en resurs med en viss MIME-typ bearbetas kontrolleras MIME-typen först mot det utelämnade MIME-typvärdet för återgivningsspecifikationen. Om den matchar den listan genereras inte den här specifika återgivningen för resursen (blockeringslista). Annars kontrolleras MIME-typen mot den inkluderade MIME-typen, och om den matchar listan genereras återgivningen (tillåtelselista).

* **Särskild FPO-återgivning**: När man monterar stora resurser från [!DNL Experience Manager] till [!DNL Adobe InDesign] dokument väntar kreatörerna en hel tid efter att de har [monterat materialet](https://helpx.adobe.com/indesign/using/placing-graphics.html). Användaren kan inte använda [!DNL InDesign]. Detta stör det kreativa flödet och påverkar användarupplevelsen negativt. Med Adobe kan du tillfälligt placera små återgivningar i [!DNL InDesign] dokument till att börja med, vilket kan ersättas med högupplösta resurser vid behov senare. [!DNL Experience Manager] innehåller återgivningar som endast används för placering (FPO). Dessa FPO-återgivningar har en liten filstorlek men har samma proportioner.

Bearbetningsprofilen kan innehålla en FPO-återgivning (endast för placering). Se [!DNL Adobe Asset Link] dokumentationen [](https://helpx.adobe.com/se/enterprise/using/manage-assets-using-adobe-asset-link.html) för att ta reda på om du behöver aktivera den för din bearbetningsprofil. Mer information finns i [Adobe Asset Link, fullständig dokumentation](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html).

### Skapa standardprofil {#create-standard-profile}

Så här skapar du en standardbearbetningsprofil:

1. Administratörer har åtkomst **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Processing Profiles]**. Klicka på **[!UICONTROL Create]**.
1. Ange ett namn som hjälper dig att identifiera profilen unikt när du använder den i en mapp.
1. Aktivera på fliken **[!UICONTROL Standard]** om du vill generera FPO-återgivningar **[!UICONTROL Create FPO Rendition]**. Ange ett **[!UICONTROL Quality]** värde mellan 1 och 100.
1. Om du vill generera andra återgivningar klickar du på **[!UICONTROL Add New]** och anger följande information:

   * Filnamn för varje återgivning.
   * Filformat (PNG, JPEG eller GIF) för varje återgivning.
   * Bredd och höjd i pixlar för varje återgivning. Om värdena inte anges används den ursprungliga bildens fullständiga pixelstorlek.
   * Kvalitet i procent av varje JPEG-återgivning.
   * Inkluderade och exkluderade MIME-typer för att definiera en profils tillämplighet.

![processing-profiles-adding](assets/processing-profiles-adding.png)

1. Klicka på **[!UICONTROL Save]**.

I följande video visas hur användbar och användbar standardprofilen är.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)

<!-- Removed per cqdoc-15624 request by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## Anpassade profil- och användningsfall {#custom-config}

**TBD-objekt**:

* Övergripande korslänkning med utökningsbart innehåll.
* Ange hur du hämtar URL för arbetare. Arbetar-URL för Dev-, Stage- och Prod-miljöer.
* Omnämnande av mappning av tjänstparametrar. Länk till datortjänstartikeln.
* Granska från flödesperspektiv som delas i Jira-biljett.

Vissa användningsområden för avancerad tillgångsbearbetning kan inte utföras med standardkonfigurationer eftersom organisationens behov varierar. Adobe erbjuder [!DNL Asset Compute Service] sådana användningsområden. Det är en skalbar och utbyggbar tjänst för bearbetning av digitala resurser. Det kan omvandla bild, video, dokument och andra filformat till olika renderingar, bland annat miniatyrer, extraherad text och metadata samt arkiv.

Utvecklare kan använda tjänsten Resursberäkning för att skapa specialanpassade medarbetare som klarar fördefinierade, komplexa användningsfall. [!DNL Experience Manager] kan anropa dessa anpassade arbetare från användargränssnittet med hjälp av anpassade profiler som administratörer konfigurerar. [!DNL Asset Compute Service] har stöd för följande användningsområden:

* Skapa egna smarta taggar för digitalt material med Adobe Sensei.
* Generera en beskärningsmask för ett objekt med Adobe Sensei.
* Hämta produktmetadatainformation från PIM-systemet och gör metadatan till en del av resursens binära fil när resursen används.
* Ändra bakgrundsfärgen för en genomskinlig bild med [!DNL Adobe Photoshop] API.
* Retuschera en bild med [!DNL Photoshop] API.
* Räta upp en bild med [!DNL Adobe Lightroom] API.

>[!NOTE]
>
>Du kan inte redigera standardmetadata med hjälp av anpassade arbetare. Du kan bara ändra anpassade metadata.

### Skapa en anpassad profil {#create-custom-profile}

Så här skapar du en anpassad profil:

1. Administratörer har åtkomst **[!UICONTROL Tools > Assets > Processing Profiles]**. Klicka på **[!UICONTROL Create]**.
1. Klicka på fliken **[!UICONTROL Custom]**. Klicka på **[!UICONTROL Add New]**. Ange önskat filnamn för återgivningen.
1. Ange följande information och klicka på **[!UICONTROL Save]**.

   * Filnamn för varje återgivning och ett filtillägg som stöds.
   * Slutpunkts-URL för en standardanpassad app. Appen måste komma från samma organisation som Experience Manager-kontot.
   * Lägg till tjänstparametrar efter behov.
   * Inkluderade och exkluderade MIME-typer för att definiera en profils tillämplighet.

![custom-processing-profile](assets/custom-processing-profile.png)

>[!CAUTION]
>
>Om appen och [!DNL Experience Manager] kontot Fireworks inte kommer från samma organisation fungerar inte integreringen.

## Använda bearbetningsprofiler för att bearbeta resurser {#use-profiles}

Skapa och använd de extra anpassade bearbetningsprofilerna på specifika mappar som Experience Manager kan bearbeta för resurser som har överförts till eller uppdaterats i dessa mappar. Den inbyggda standardbearbetningsprofilen körs alltid som standard, men visas inte i användargränssnittet. Om du lägger till en anpassad profil används båda profilerna för att bearbeta de överförda resurserna.

Använd bearbetningsprofiler på mappar på något av följande sätt:

* Administratörer kan välja en bearbetningsprofildefinition i **[!UICONTROL Tools > Assets > Processing Profiles]** och använda **[!UICONTROL Apply Profile to Folder(s)]** åtgärd. Den öppnar en innehållsläsare där du kan navigera till specifika mappar, markera dem och bekräfta programmet för profilen.
* Users can select a folder in the Assets user interface, use **[!UICONTROL Properties]** action to open folder properties screen, click on the **[!UICONTROL Processing Profiles]** tab, and in the popup list, select the correct processing profile for that folder. Spara ändringarna genom att klicka på **[!UICONTROL Save & Close]**.

>[!NOTE]
>
>Endast en bearbetningsprofil kan användas för en viss mapp. Om du vill generera fler återgivningar lägger du till fler återgivningsdefinitioner i den befintliga bearbetningsprofilen.

När en bearbetningsprofil har tillämpats på en mapp bearbetas alla nya resurser som har överförts (eller uppdaterats) i den här mappen eller någon av dess undermappar med hjälp av den extra bearbetningsprofil som har konfigurerats. Den här bearbetningen är utöver standardprofilen. Om du tillämpar flera profiler på en mapp bearbetas de överförda eller uppdaterade resurserna med hjälp av var och en av dessa profiler.

>[!NOTE]
>
>En bearbetningsprofil som används på en mapp fungerar för hela trädet, men kan åsidosättas om en annan profil används på en undermapp. När resurser överförs till en mapp kontrollerar Experience Manager egenskaperna för den innehållande mappen för att hitta en bearbetningsprofil. Om ingen används kontrolleras en överordnad mapp i hierarkin för att en bearbetningsprofil ska användas.

Användarna kan kontrollera att bearbetningen faktiskt utfördes genom att öppna en nyligen överförd resurs som bearbetningen är klar för, öppna förhandsgranskningen av resursen och klicka på den vänstra **[!UICONTROL Renditions]** spårens vy. De specifika återgivningarna i bearbetningsprofilen, för vilka den specifika resursens typ matchar reglerna för MIME-typinkludering, bör vara synliga och tillgängliga.

![additional-renditions](assets/renditions-additional-renditions.png)

*Bild: Exempel på två extra återgivningar som genereras av en bearbetningsprofil som tillämpas på den överordnade mappen.*

## Efterbehandlingsarbetsflöden {#post-processing-workflows}

Om det krävs ytterligare bearbetning av resurser som inte kan utföras med bearbetningsprofilerna, kan ytterligare efterbearbetningsarbetsflöden läggas till i konfigurationen. Detta gör att du kan lägga till helt anpassad bearbetning utöver den konfigurerbara bearbetningen med hjälp av objektmikrotjänster.

Efterbehandlingsarbetsflöden, om de är konfigurerade, körs automatiskt av AEM när bearbetningen av mikrotjänsterna har slutförts. Du behöver inte lägga till startprogram för arbetsflöden manuellt för att utlösa dem. Exemplen innehåller:

* Anpassade arbetsflödessteg för att bearbeta resurser.
* Integreringar för att lägga till metadata eller egenskaper i resurser från externa system, till exempel produkt- eller processinformation.
* Ytterligare bearbetning utförd av externa tjänster.

Att lägga till en arbetsflödeskonfiguration efter bearbetning i Experience Manager består av följande steg:

* Skapa en eller flera arbetsflödesmodeller. I dokumenten anges det som *arbetsflödesmodeller* för efterbearbetning, men dessa är vanliga arbetsflödesmodeller för Experience Manager.
* Lägg till specifika arbetsflödessteg i dessa modeller. Stegen körs på resurserna baserat på en arbetsflödesmodellkonfiguration.
* Lägg till [!UICONTROL DAM Update Asset Workflow Completed Process] steg i slutet. Om du lägger till det här steget vet Experience Manager när bearbetningen avslutas och resursen kan markeras som bearbetad, vilket innebär att *Nytt* visas på resursen.
* Skapa en konfiguration för tjänsten Custom Workflow Runner som gör att du kan konfigurera körning av en arbetsflödesmodell efter bearbetning antingen med en sökväg (mappsökväg) eller med ett reguljärt uttryck.

### Skapa arbetsflödesmodeller för efterbearbetning {#create-post-processing-workflow-models}

Arbetsflödesmodeller för efterbearbetning är vanliga AEM arbetsflödesmodeller. Skapa olika modeller om du behöver olika bearbetning för olika databasplatser eller resurstyper.

Bearbetningssteg ska läggas till baserat på behov. Du kan använda alla steg som stöds, samt alla anpassade arbetsflödessteg.

Se till att det sista steget i varje efterbearbetningsarbetsflöde är `DAM Update Asset Workflow Completed Process`. I det sista steget ser du till att Experience Manager vet när bearbetningen av mediefiler är klar.

### Konfigurera arbetsflödeskörning efter bearbetning {#configure-post-processing-workflow-execution}

Om du vill konfigurera arbetsflödesmodellerna för efterbearbetning som ska köras för resurser som har överförts eller uppdaterats i systemet efter att bearbetningen av resursmikrotjänsterna har slutförts, måste tjänsten Custom Workflow Runner konfigureras.

Tjänsten Custom Workflow Runner (`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`) är en OSGi-tjänst och har två konfigurationsalternativ:

* Efterbehandlingsarbetsflöden efter sökväg (`postProcWorkflowsByPath`): Flera arbetsflödesmodeller kan listas baserat på olika databassökvägar. Banor och modeller ska separeras med kolon. Enkla databassökvägar stöds och bör mappas till en arbetsflödesmodell i `/var` sökvägen. Till exempel: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* Efterbehandlingsarbetsflöden efter uttryck (`postProcWorkflowsByExpression`): Flera arbetsflödesmodeller kan listas baserat på olika reguljära uttryck. Uttryck och modeller ska separeras med ett kolon. Det reguljära uttrycket ska peka direkt på resursnoden och inte på en av återgivningarna eller filerna. Till exempel: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

>[!NOTE]
>
>Konfigurationen av Custom Workflow Runner är en konfiguration av en OSGi-tjänst. Mer information om hur du distribuerar en OSGi-konfiguration finns i [Distribuera till Experience Manager](/help/implementing/deploying/overview.md) .
>OSGi-webbkonsolen är inte direkt tillgänglig i distributioner av molntjänster, till skillnad från vid installation på plats och för hanterade AEM.

Mer information om vilket standardarbetsflödessteg som kan användas i efterbearbetningsarbetsflödet finns i [arbetsflödessteg i efterbearbetningsarbetsflödet](developer-reference-material-apis.md#post-processing-workflows-steps) i utvecklarreferensen.

## God praxis och begränsningar {#best-practices-limitations-tips}

* Tänk på dina behov av alla typer av återgivningar när du utformar arbetsflöden. Om du inte förutser att en återgivning behövs i framtiden tar du bort steget när du skapar den från arbetsflödet. Det går inte att ta bort återgivningar gruppvis efteråt. Oönskade återgivningar kan ta upp mycket lagringsutrymme efter långvarig användning av [!DNL Experience Manager]. För enskilda resurser kan du ta bort återgivningar manuellt från användargränssnittet. För flera resurser kan du antingen anpassa [!DNL Experience Manager] för att ta bort specifika återgivningar eller ta bort resurserna och överföra dem igen.
