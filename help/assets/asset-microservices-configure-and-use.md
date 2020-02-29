---
title: Konfigurera och använda resursmikrotjänster för bearbetning av resurser
description: Lär dig hur du konfigurerar och använder molnbaserade resursmeritjänster för att bearbeta resurser i stor skala.
contentOwner: AG
translation-type: tm+mt
source-git-commit: f2e257ff880ca2009c3ad6c8aadd055f28309289

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

Resursmikrotjänsterna erbjuder en skalbar och flexibel bearbetning av resurser med hjälp av molntjänster, som hanteras av Adobe för optimal hantering av olika resurstyper och bearbetningsalternativ.

Resursbearbetningen utförs baserat på konfigurationen i **[!UICONTROL Bearbetningsprofiler]**, som tillhandahåller en standardinställning, och som gör att administratören kan lägga till mer specifik konfiguration för bearbetning av resurser. För att möjliggöra utbyggbarhet och fullständig anpassning kan en valfri konfiguration av efterbehandlingsarbetsflöden användas, som sedan skapas och underhålls av administratören.

Ett arbetsflöde på hög nivå för bearbetning av resurser i Experience Manager som en molntjänst presenteras nedan.

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![asset-microservices-flow](assets/asset-microservices-flow.png)

>[!NOTE]
>
> För kunder som uppdaterar från tidigare versioner av Experience Manager ersätter resursbearbetningen som beskrivs i det här avsnittet arbetsflödesmodellen&quot;DAM Update Asset&quot; som används för tillgångsbearbetning tidigare. De flesta standardstegen för generering av återgivning och metadatarelaterade steg ersätts av bearbetningen av resursmikrotjänsterna, och eventuella återstående steg kan ersättas av arbetsflödeskonfigurationen för efterbearbetning.

## Kom igång med resurshantering {#get-started}

Resursbearbetning med tillgångsmikrotjänster är förkonfigurerad med en standardkonfiguration, vilket säkerställer att de standardåtergivningar som krävs av systemet är tillgängliga. Dessutom kan du försäkra dig om att metadataextrahering och textrahering är tillgängliga. Användare kan börja ladda upp eller uppdatera resurser direkt och grundläggande bearbetning är tillgänglig som standard.

För specifika krav på återgivningsgenerering eller resursbearbetning kan en AEM-administratör skapa ytterligare [!UICONTROL bearbetningsprofiler]. Användarna kan tilldela en eller flera av de tillgängliga profilerna till specifika mappar för att få ytterligare bearbetning. Exempel: skapa webb-, mobil- och surfplattesspecifika renderingar. I följande video visas hur du skapar och använder [!UICONTROL bearbetningsprofiler] och hur du får tillgång till de återgivningar som skapas.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)

Information om hur du ändrar en befintlig profil finns i [konfigurationer för resursmikrotjänster](#configure-asset-microservices).
Mer information om hur du skapar anpassade bearbetningsprofiler som är specifika för dina egna behov, t.ex. för integrering med andra system, finns i [Efterbehandlingsarbetsflöden](#post-processing-workflows).

## Konfigurationer för tillgångsmikrotjänster {#configure-asset-microservices}

För att konfigurera resursmikrotjänster kan administratörer använda konfigurationsgränssnittet under **[!UICONTROL Verktyg > Resurser > Bearbeta profiler]**.

### Standardkonfiguration {#default-config}

Med standardkonfigurationen konfigureras bara [!UICONTROL standardbearbetningsprofilen] . Den är inbyggd och kan inte ändras. Den körs alltid för att säkerställa att all bearbetning som krävs för programmet utförs.

![processing-profiles-standard](assets/processing-profiles-standard.png)

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

* renderingsnamn
* återgivningsformat (JPEG, PNG eller GIF stöds)
* återgivningens bredd och höjd i pixlar (om inget anges antas den fullständiga pixelstorleken för originalet)
* återgivningskvalitet (för JPEG) i procent
* MIME-typer som ingår och utesluts definierar vilka tillgångstyper som bearbetningsprofilen gäller för

![processing-profiles-adding](assets/processing-profiles-adding.png)

När en ny bearbetningsprofil sparas läggs den till i listan med konfigurerade bearbetningsprofiler. Dessa bearbetningsprofiler kan sedan användas på mappar i mapphierarkin för att göra dem effektiva vid överföringar av resurser och resurser som görs där.

![processing-profiles-list](assets/processing-profiles-list.png)

#### Återgivningens bredd och höjd {#rendition-width-height}

Specifikationen för återgivningens bredd och höjd ger maximala storlekar för den genererade utdatabilden. Resursmikrotjänsten försöker skapa den största möjliga återgivningen, som inte är större än den angivna bredden och höjden. Proportionerna bevaras, det vill säga de ursprungliga.

Ett tomt värde innebär att resursbearbetningen baseras på originalets pixeldimension.

#### Inkluderingsregler för MIME-typ {#mime-type-inclusion-rules}

När en resurs med en viss MIME-typ bearbetas kontrolleras MIME-typen först mot det utelämnade MIME-typvärdet för återgivningsspecifikationen. Om den matchar den listan genereras inte den här specifika återgivningen för resursen (&quot;svartlistning&quot;).

I annat fall kontrolleras MIME-typen mot den inkluderade MIME-typen, och om den matchar listan genereras återgivningen (&quot;vitlista&quot;).

#### Särskild FPO-återgivning {#special-fpo-rendition}

Bearbetningsprofilen kan innehålla en särskild FPO-återgivning, som används när [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) används med Adobe InDesign för att placera direkta länkar till resurser från Experience Manager i InDesign-dokument.

Läs Adobe Asset Link- [dokumentationen](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) om du behöver aktivera den för din bearbetningsprofil.

## Använd resursmikrotjänster för att bearbeta resurser {#use-asset-microservices}

När ytterligare bearbetningsprofiler har skapats måste de tillämpas på specifika mappar för Experience Manager för att de ska kunna användas vid resursbearbetning för resurser som har överförts eller uppdaterats i dessa mappar. Den inbyggda standardbearbetningsprofilen körs alltid.

Det finns två sätt att använda bearbetningsprofiler på mappar:

* Administratörer kan välja en bearbetningsprofildefinition i **[!UICONTROL Verktyg > Resurser > Bearbeta profiler]** och sedan använda åtgärden **[!UICONTROL Använd profil på]** mappar. Den öppnar en innehållsläsare där du kan navigera till specifika mappar, markera dem och bekräfta programmet för profilen.
* Användarna kan välja en mapp i Assets-användargränssnittet, använda åtgärden **[!UICONTROL Egenskaper]** för att öppna fönstret för mappegenskaper, klicka på fliken **[!UICONTROL Bearbeta profiler]** och i listrutan välja rätt bearbetningsprofil för den mappen. Alternativet sparas vid åtgärden **[!UICONTROL Spara och stäng]** .

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

### Skapa arbetsflödesmodeller för efterbearbetning

Arbetsflödesmodeller för efterbearbetning är vanliga AEM-arbetsflödesmodeller. Skapa olika om du behöver olika typer av bearbetning för olika databasplatser eller resurstyper.

Bearbetningssteg ska läggas till baserat på behov. Du kan använda alla färdiga steg som stöds, samt anpassade arbetsflödessteg.

Det sista steget i alla efterbehandlingsarbetsflöden måste vara `DAM Update Asset Workflow Completed Process`. Detta säkerställer att resursen markeras som&quot;bearbetningen har slutförts&quot;.

### Konfigurera körning av arbetsflöde efter bearbetning

Om du vill konfigurera arbetsflödesmodellerna för efterbearbetning som ska köras för resurser som har överförts eller uppdaterats i systemet efter att bearbetningen av resursmikrotjänsterna har slutförts, måste tjänsten Custom Workflow Runner konfigureras.

Tjänsten Custom Workflow Runner (`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`) är en OSGi-tjänst och har två konfigurationsalternativ:

* Efterbehandlingsarbetsflöden efter sökväg (`postProcWorkflowsByPath`): Flera arbetsflödesmodeller kan listas baserat på olika databassökvägar. Banor och modeller ska separeras med kolon. Enkla databassökvägar stöds och bör mappas till en arbetsflödesmodell i `/var` sökvägen. Exempel: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* Efterbehandlingsarbetsflöden efter uttryck (`postProcWorkflowsByExpression`): Flera arbetsflödesmodeller kan listas baserat på olika reguljära uttryck. Uttryck och modeller ska separeras med ett kolon. Det reguljära uttrycket ska peka direkt på resursnoden och inte på en av återgivningarna eller filerna. Exempel: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

>[!NOTE]
>
>Konfigurationen av Custom Workflow Runner är en konfiguration av en OSGi-tjänst. Mer information om hur du distribuerar en OSGi-konfiguration finns i [Distribuera till Experience Manager](/help/implementing/deploying/overview.md) .
> OSGi-webbkonsolen, till skillnad från AEM-driftsättningar på plats och hanterade tjänster, är inte direkt tillgänglig i distributionen av molntjänster.

Mer information om vilka av de standardarbetsflödesstegen som kan användas i efterbearbetningsarbetsflödet finns i [Arbetsflödessteg i efterbearbetningsarbetsflödet](developer-reference-material-apis.md#post-processing-workflows-steps) i utvecklarreferensen.
