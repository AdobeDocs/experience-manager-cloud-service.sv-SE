---
title: Importera en varumärkesprofil
description: Använd Adobe Governance Agent för att importera en varumärkesprofil
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 94d671ebbd5aeb5992fdbc9d779ffbca51f82585
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 0%

---


# Importera en varumärkesprofil {#how-to-import-a-brand-policy}

## Ökning {#overview}

En varumärkespolicy definierar regler, standarder och begränsningar som säkerställer att allt innehåll som produceras eller uppdateras av Adobe Experience Manager följer företagets varumärkesidentitet. Detta omfattar vanligtvis ton av röst, terminologi, visuella riktlinjer och redigeringsregler.

Styrningsagenten använder varumärkespolicyer som en källa till sanning för att analysera befintliga sidor och vägleda innehållsgenereringen. Kunderna kan tillhandahålla sina egna varumärkesprofiler, som deras styrningsagent automatiskt konverterar till AI-läsbara policykontroller. Dessa kontroller används sedan för att validera innehållet och ge produktionsagenten ett tillförlitligt och verkställbart ramverk för att generera eller uppdatera sidor som fortfarande är anpassade till varumärket.

## Vad är en varumärkespolicy i en statlig agent? {#what-is-a-brand-policy-in-the-governance-agent}

En varumärkespolicy är en strukturerad representation av era varumärkesregler som kan förstås och genomdrivas av AI. I stället för att kräva att kunderna skriver om sina riktlinjer i ett tekniskt format, godkänner Styrningsagenten varumärkespolicyer i sin ursprungliga form (till exempel dokument, riktlinjer eller regelbeskrivningar).

När profilen har importerats omvandlas den till en uppsättning AI-principkontroller som kan:

* Analysera befintliga sidor för att upptäcka varumärkesavvikelser
* Flagga avvikelser från ton, terminologi eller obligatoriska regler
* ge tydliga riktlinjer för nedströmsagenter,
* Se till att det genererade eller uppdaterade innehållet förblir varumärkesanpassat enligt designen

Med den här metoden kan team återanvända sin befintliga varumärkesdokumentation samtidigt som de drar nytta av automatiserad styrning och skalbar innehållsproduktion.

## Hur varumärkesprofiler används {#how-brand-policies-are-used}

När en varumärkesprofil har importerats:

* Styrningsagenten tolkar och normaliserar policyn till verkställbara AI-kontroller
* Sidorna kan analyseras mot policyn för att identifiera luckor eller överträdelser
* Produktionsagenten använder dessa kontroller som begränsningar när innehållet genereras eller uppdateras
* Varumärkesefterlevnaden blir enhetlig, upprepningsbar och kan kontrolleras över alla webbplatser och team


## Importera en varumärkesprofil {#import-a-brand-policy}

Så här importerar du ett varumärke till en statlig agent:

1. Skapa ett varumärke genom att ange ett namn och en huvuddomän. Du kan göra detta genom att klicka på knappen **Styrningskontext** till vänster i Experience Manager hem och sedan trycka på knappen **+ Lägg till varumärke** enligt nedan:

   ![Lägger till ett nytt varumärke](/help/ai-in-aem/agents/governance/assets/add_brand.png){width="70%"}

1. Ange namnet på varumärket och en beskrivning i följande fönster

   ![Namnge varumärket](/help/ai-in-aem/agents/governance/assets/add_brand_dialogue.png){width="60%"}

1. Nya varumärken skapas i utkaststatus. Se till att du ändrar ditt nya varumärke till en aktiv status genom att klicka på ditt varumärkes kort, trycka på redigeringsverktyget (pennan) i skärmens övre högra hörn, ange **status** till **Aktiv** i följande fönster och klicka på **Spara ändringar**. Du måste aktivera varumärkena genom att ange dem som Aktiv innan du kan använda dem.

   ![Ange varumärkets status till Aktiv](/help/ai-in-aem/agents/governance/assets/set_brand_active.png){width="60%"}

1. När varumärket har skapats skapar du en huvuddomän i följande fönster genom att trycka på länken **Domäner** till vänster:

   ![Konfigurera en domän för varumärket](/help/ai-in-aem/agents/governance/assets/add_domain.png)

   >[!IMPORTANT]
   >
   >Precis som nya varumärken skapas nya domäner med standardstatusen Utkast. Om du vill ändra detta går du till ditt varumärke, klickar på **Domäner**, redigerar din domän med pennikonen och anger statusen till **Aktiv**.

1. När du har konfigurerat huvuddomänen kan du överföra varumärkesprofildokumentet genom att gå till **Profiler** i fönstrets övre vänstra hörn och trycka på knappen **+ Lägg till profil** .

   ![Lägger till en profil från varumärkeskortet](/help/ai-in-aem/agents/governance/assets/add_policy_treeview.png)

   >[!NOTE]
   >
   >Du kan också lägga till profiler genom att växla till fliken **Profiler** och trycka på länken **+ Lägg till princip** .

1. I nästa fönster trycker du på **Överför PDF-filer** och väljer varumärkesprofilerade dokument i PDF-format

   ![Överför ditt varumärkespolicydokument](/help/ai-in-aem/agents/governance/assets/upload_brand_policy_document.png){width="70%"}

   Styrningsagenten kommer att analysera er varumärkespolicy med hjälp av naturligt språk och extrahera de kontroller som görs i dokumentet och översätta dem till verkliga uppgifter. När dokumentet har bearbetats kan du visa en sammanfattning av importen, inklusive antalet kontroller och statusen för profilen, vilket visas nedan:

   ![Ett översiktsfönster med varumärkesprofilens status](/help/ai-in-aem/agents/governance/assets/policy_status.png)

1. När varumärket har skapats och ditt policydokument har överförts kan du få en detaljerad bild per varumärke genom att gå till fliken **Varumärken** och klicka på ett varumärkes kort. Det här är vyn som du vill använda för att skapa kategorier med kontroller, genom att trycka på de tre punkterna bredvid en befintlig kategori och välja **+ Lägg till kategori**, vilket visas på skärmbilden nedan:

   ![Lägg till kategori](/help/ai-in-aem/agents/governance/assets/add_category.png)

   Du kan också använda den här vyn för att skapa, redigera och ta bort kontroller, som vi kommer att beskriva i stegen nedan.

1. Om du vill få en mer detaljerad vy över varje enskild kontroll kan du växla till fliken **Kontroller** och visa en lista över varje enskild kontroll som har extraherats från dina stöddokument. Du kan filtrera kontroller baserat på märke eller status:

   ![Se enskilda varumärkeskontroller](/help/ai-in-aem/agents/governance/assets/see_brand_checks.png)

   Dessutom kan du visa ytterligare information om varje enskild kontroll genom att klicka på de tre punkterna (**...**) till vänster om kontrollen och trycka på **Visa information**. Då öppnas ett nytt fönster med mer information om kontrollen:

   ![Visa information om enskild kontroll](/help/ai-in-aem/agents/governance/assets/view_check_details.png)

   Du kan också ta bort kontroller genom att trycka på **Ta bort** på samma menyplats, eller redigera dem genom att trycka på **Redigera**:

   ![Redigera en kontroll](/help/ai-in-aem/agents/governance/assets/edit_check.png)

1. Du kan lägga till en kontroll manuellt genom att trycka på **Lägg till kontroll** i det övre vänstra hörnet av fönstret Kontroller:

   ![Lägger till en kontroll](/help/ai-in-aem/agents/governance/assets/add_check.png)

   På följande skärm kan du konfigurera information som:

   * Namnet på kontrollen
   * Regeln, som beskrivs på naturligt språk
   * Kategorin
   * Det eller de omfång som det gäller

   ![Konfigurerar kontrollinformationen](/help/ai-in-aem/agents/governance/assets/add_check_window.png)

1. Slutligen, om du vill se en lista över domäner och de varumärken de är kopplade till kan du trycka på fliken **Domäner**. I det här avsnittet kan du lägga till, ta bort eller ändra domäner i listan.

