---
title: Konfigurera och använda resursmikrotjänster för bearbetning av resurser
description: Lär dig hur du konfigurerar och använder molnbaserade resursmeritjänster för att bearbeta resurser i stor skala.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# Komma igång med mikrotjänster för material {#get-started-using-asset-microservices}

<!--
* Current capabilities of asset microservices offered. If workers have names then list the names and give a one-liner description. (The feature-set is limited for now and continues to grow. So will this article continue to be updated.)
* How to access the microservices. UI. API. Is extending possible right now?
* Detailed list of what file formats and what processing is supported by which workflows/workers process.
* How/where can admins check what's already configured and provisioned.
* How to create new config or request for new provisioning/purchase.

* [DO NOT COVER?] Exceptions or limitations or link back to lack of parity with AEM 6.5.
-->

Resursmikrotjänsterna erbjuder en skalbar och flexibel bearbetning av resurser med hjälp av molntjänster. Adobe hanterar tjänsterna för optimal hantering av olika resurstyper och bearbetningsalternativ.

Resursbearbetningen beror på konfigurationen i **[!UICONTROL Bearbeta profiler]**, som tillhandahåller en standardinställning, och gör det möjligt för en administratör att lägga till en mer specifik konfiguration för resursbearbetning. Administratörer kan skapa och underhålla konfigurationer för efterbehandlingsarbetsflöden, inklusive valfri anpassning. Genom att anpassa arbetsflöden kan du utöka och göra fullständiga anpassningar.

Ett högnivåflöde för bearbetning av tillgångar är under.

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![asset-microservices-flow](assets/asset-microservices-flow.png)

>[!NOTE]
>
> Resursbearbetningen som beskrivs här ersätter arbetsflödesmodellen som finns i tidigare versioner av Experience Manager. `DAM Update Asset` De flesta standardstegen för generering av återgivning och metadatarelaterade steg ersätts av bearbetningen av resursmikrotjänsterna, och eventuella återstående steg kan ersättas av arbetsflödeskonfigurationen för efterbearbetning.

## Kom igång med resurshantering {#get-started}

Resursbearbetning med tillgångsmikrotjänster är förkonfigurerad med en standardkonfiguration, vilket säkerställer att de standardåtergivningar som krävs av systemet är tillgängliga. Dessutom kan du försäkra dig om att metadataextrahering och textrahering är tillgängliga. Användare kan börja ladda upp eller uppdatera resurser direkt och grundläggande bearbetning är tillgänglig som standard.

För specifika krav på återgivningsgenerering eller resursbearbetning kan en AEM-administratör skapa ytterligare [!UICONTROL bearbetningsprofiler]. Användarna kan tilldela en eller flera av de tillgängliga profilerna till specifika mappar för att få ytterligare bearbetning. Exempel: skapa webb-, mobil- och surfplattesspecifika renderingar. I följande video visas hur du skapar och använder [!UICONTROL bearbetningsprofiler] och hur du får tillgång till de återgivningar som skapas.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)

Information om hur du ändrar en befintlig profil finns i [konfigurationer för resursmikrotjänster](#configure-asset-microservices).
Mer information om hur du skapar anpassade bearbetningsprofiler som är specifika för dina egna behov, t.ex. för integrering med andra system, finns i [Efterbehandlingsarbetsflöden](#post-processing-workflows).

## Konfigurationer för tillgångsmikrotjänster {#configure-asset-microservices}

För att konfigurera resursmikrotjänster kan administratörer använda konfigurationsgränssnittet under **[!UICONTROL Verktyg > Resurser > Bearbeta profiler]**.

### Standardkonfiguration {#default-config}

Med standardkonfigurationen konfigureras bara standardbearbetningsprofilen. Standardbearbetningsprofilen visas inte i användargränssnittet och du kan inte ändra den. Det körs alltid för att bearbeta överförda resurser. En standardbearbetningsprofil säkerställer att all grundläggande bearbetning som krävs av Experience Manager är slutförd för alla resurser.

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png) -->

Standardbearbetningsprofilen ger följande bearbetningskonfiguration:

* Standardminiatyrbilder som används i gränssnittet Resurs (48, 140 och 319 px)
* Stor förhandsgranskning (webbåtergivning - 1 280 pixlar)
* Extrahering av metadata
* Textextrahering

### Filformat som stöds {#supported-file-formats}

Resursmikrotjänsterna har stöd för en mängd olika filformat när det gäller möjligheten att generera återgivningar eller extrahera metadata. En fullständig lista finns i [filformat](file-format-support.md) som stöds.

### Lägga till ytterligare bearbetningsprofiler {#processing-profiles}

Ytterligare bearbetningsprofiler kan läggas till med åtgärden **[!UICONTROL Skapa]** .

Varje bearbetningsprofilskonfiguration innehåller en lista med återgivningar. För varje återgivning kan du ange följande:

* Återgivningsnamn.
* Återgivningsformat som stöds, till exempel JPEG, PNG eller GIF.
* Återgivningens bredd och höjd i pixlar. Om den inte anges används den fullständiga pixelstorleken för den ursprungliga bilden.
* Återgivningskvalitet för JPEG i procent.
* Inkluderade och exkluderade MIME-typer för att definiera en profils tillämplighet.

![processing-profiles-adding](assets/processing-profiles-adding.png)

När du skapar och sparar en ny bearbetningsprofil läggs den till i listan med konfigurerade bearbetningsprofiler. Du kan använda de här bearbetningsprofilerna på mappar i mapphierarkin för att göra dem effektiva vid överföring av resurser och bearbetning av resurser.

<!-- Removed per cqdoc-15624 request by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) -->

#### Återgivningens bredd och höjd {#rendition-width-height}

Specifikationen för återgivningens bredd och höjd ger maximala storlekar för den genererade utdatabilden. Resursmikrotjänsten försöker skapa den största möjliga återgivningen, som inte är större än den angivna bredden och höjden. Proportionerna bevaras, det vill säga de ursprungliga.

Ett tomt värde innebär att resursbearbetningen baseras på originalets pixeldimension.

#### Inkluderingsregler för MIME-typ {#mime-type-inclusion-rules}

När en resurs med en viss MIME-typ bearbetas kontrolleras MIME-typen först mot det utelämnade MIME-typvärdet för återgivningsspecifikationen. Om den matchar den listan genereras inte den här specifika återgivningen för resursen (&quot;svartlistning&quot;).

I annat fall kontrolleras MIME-typen mot den inkluderade MIME-typen, och om den matchar listan genereras återgivningen (&quot;vitlista&quot;).

#### Särskild FPO-återgivning {#special-fpo-rendition}

När du monterar stora resurser från AEM i Adobe InDesign-dokument måste den som arbetar med design vänta en hel del efter att de [monterat materialet](https://helpx.adobe.com/indesign/using/placing-graphics.html). Under tiden är användaren blockerad från att använda InDesign. Detta stör det kreativa flödet och påverkar användarupplevelsen negativt. Adobe gör det möjligt att tillfälligt placera små återgivningar i InDesign-dokument till att börja med, vilket kan ersättas med högupplösta resurser vid behov senare. Experience Manager innehåller renderingar som bara används för placering (FPO). Dessa FPO-återgivningar har en liten filstorlek men har samma proportioner.

Bearbetningsprofilen kan innehålla en FPO-återgivning (endast för placering). Läs [dokumentationen](https://helpx.adobe.com/se/enterprise/using/manage-assets-using-adobe-asset-link.html) om Adobe Asset Link om du behöver aktivera den för din bearbetningsprofil. Mer information finns i den fullständiga dokumentationen för [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html).

## Använd resursmikrotjänster för att bearbeta resurser {#use-asset-microservices}

Skapa och använd de anpassade bearbetningsprofilerna på specifika mappar för Experience Manager för att bearbeta resurser som har överförts till eller uppdaterats i dessa mappar. Den inbyggda standardbearbetningsprofilen körs alltid som standard, men visas inte i användargränssnittet. Om du lägger till en anpassad profil används båda profilerna för att bearbeta de överförda resurserna.

Det finns två sätt att använda bearbetningsprofiler på mappar:

* Administratörer kan välja en bearbetningsprofildefinition i **[!UICONTROL Verktyg > Resurser > Bearbeta profiler]** och sedan använda åtgärden **[!UICONTROL Använd profil på]** mappar. Den öppnar en innehållsläsare där du kan navigera till specifika mappar, markera dem och bekräfta programmet för profilen.
* Users can select a folder in the Assets user interface, use **[!UICONTROL Properties]** action to open folder properties screen, click on the **[!UICONTROL Processing Profiles]** tab, and in the drop-down, select the right processing profile for that folder. The choice will be save upon **[!UICONTROL Save &amp; Close]** action.

>[!NOTE]
>
>Endast en bearbetningsprofil kan användas för en viss mapp. Om du behöver fler genererade återgivningar kan du lägga till fler återgivningsdefinitioner i bearbetningsprofilen.

När en bearbetningsprofil har tillämpats på en mapp bearbetas alla nya resurser som har överförts (eller uppdaterats) i den här mappen eller någon av dess undermappar med hjälp av den extra bearbetningsprofil som har konfigurerats. Den här extra bearbetningen är utöver standardprofilen. Om du tillämpar flera profiler på en mapp bearbetas de överförda eller uppdaterade resurserna med hjälp av var och en av dessa profiler.

>[!NOTE]
>
>När resurser överförs till en mapp kontrollerar Experience Manager om det finns en bearbetningsprofil för den innehållande mappens egenskaper. Om ingen används går den upp i mappträdet tills den hittar en bearbetningsprofil som används och använder den för resursen. Det innebär att en bearbetningsprofil som används för en mapp fungerar för hela trädet, men kan åsidosättas om en annan profil används för en undermapp.

Användarna kan kontrollera att bearbetningen faktiskt utfördes genom att öppna en nyligen överförd resurs som bearbetningen är klar för, öppna förhandsgranskningen av resursen och klicka på den vänstra fältets vy **[!UICONTROL Återgivningar]** . De specifika återgivningarna i bearbetningsprofilen, för vilka den specifika resursens typ matchar reglerna för MIME-typinkludering, bör vara synliga och tillgängliga.

![additional-renditions](assets/renditions-additional-renditions.png)*Figure: Exempel på två extra återgivningar som genereras av en bearbetningsprofil som tillämpas på den överordnade mappen*

## Efterbehandlingsarbetsflöden {#post-processing-workflows}

Om det krävs ytterligare bearbetning av resurser som inte kan utföras med bearbetningsprofilerna, kan ytterligare efterbearbetningsarbetsflöden läggas till i konfigurationen. Detta gör att du kan lägga till helt anpassad bearbetning utöver den konfigurerbara bearbetningen med hjälp av objektmikrotjänster.

Efterbehandlingsarbetsflöden, om de är konfigurerade, körs automatiskt av AEM när bearbetningen av mikrotjänsterna har slutförts. Du behöver inte lägga till startprogram för arbetsflöden manuellt för att utlösa dem.

Exempel:

* anpassade arbetsflödessteg för att bearbeta resurser, till exempel Java-kod, för att generera återgivningar från egna filformat.
* integreringar för att lägga till metadata eller egenskaper i resurser från externa system, till exempel produkt- eller processinformation.
* ytterligare bearbetning utförd av externa tjänster

Att lägga till en arbetsflödeskonfiguration efter bearbetning i Experience Manager består av följande steg:

* Skapa en eller flera arbetsflödesmodeller. Vi kallar dem&quot;arbetsflödesmodeller för efterbearbetning&quot;, men de är vanliga arbetsflödesmodeller för AEM.
* Lägga till specifika arbetsflödessteg i dessa modeller. De här stegen körs på resurserna baserat på arbetsflödesmodellkonfigurationen.
* Det sista steget i en sådan modell måste vara `DAM Update Asset Workflow Completed Process` steget. Detta krävs för att säkerställa att AEM vet att bearbetningen har avslutats och att resursen kan markeras som bearbetad (&quot;Nytt&quot;)
* Skapa en konfiguration för tjänsten Custom Workflow Runner, som gör att du kan konfigurera körning av en arbetsflödesmodell efter bearbetning, antingen efter sökväg (mappsökväg) eller reguljärt uttryck

### Skapa arbetsflödesmodeller för efterbearbetning {#create-post-processing-workflow-models}

Arbetsflödesmodeller för efterbearbetning är vanliga AEM-arbetsflödesmodeller. Skapa olika modeller om du behöver olika bearbetning för olika databasplatser eller resurstyper.

Bearbetningssteg ska läggas till baserat på behov. Du kan använda alla steg som stöds, samt alla anpassade arbetsflödessteg.

Se till att det sista steget i varje efterbearbetningsarbetsflöde är `DAM Update Asset Workflow Completed Process`. Det sista steget hjälper till att säkerställa att Experience Manager vet när mediebearbetningen är klar.

### Konfigurera arbetsflödeskörning efter bearbetning {#configure-post-processing-workflow-execution}

Om du vill konfigurera arbetsflödesmodellerna för efterbearbetning som ska köras för resurser som har överförts eller uppdaterats i systemet efter att bearbetningen av resursmikrotjänsterna har slutförts, måste tjänsten Custom Workflow Runner konfigureras.

Tjänsten Custom Workflow Runner (`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`) är en OSGi-tjänst och har två konfigurationsalternativ:

* Efterbehandlingsarbetsflöden efter sökväg (`postProcWorkflowsByPath`): Flera arbetsflödesmodeller kan listas baserat på olika databassökvägar. Banor och modeller ska separeras med kolon. Enkla databassökvägar stöds och bör mappas till en arbetsflödesmodell i `/var` sökvägen. Exempel: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* Efterbehandlingsarbetsflöden efter uttryck (`postProcWorkflowsByExpression`): Flera arbetsflödesmodeller kan listas baserat på olika reguljära uttryck. Uttryck och modeller ska separeras med ett kolon. Det reguljära uttrycket ska peka direkt på resursnoden och inte på en av återgivningarna eller filerna. Exempel: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

>[!NOTE]
>
>Konfigurationen av Custom Workflow Runner är en konfiguration av en OSGi-tjänst. Mer information om hur du distribuerar en OSGi-konfiguration finns i [Distribuera till Experience Manager](/help/implementing/deploying/overview.md) .
> OSGi-webbkonsolen, till skillnad från AEM-driftsättningar på plats och hanterade tjänster, är inte direkt tillgänglig i distributionen av molntjänster.

Mer information om vilket standardarbetsflödessteg som kan användas i efterbearbetningsarbetsflödet finns i [arbetsflödessteg i efterbearbetningsarbetsflödet](developer-reference-material-apis.md#post-processing-workflows-steps) i utvecklarreferensen.
