---
title: Konfigurera översättningsregler för Headless-innehåll
description: Lär dig hur du definierar översättningsregler för att identifiera innehåll för översättning.
exl-id: 878ffd5d-0f10-4990-9779-bdf55cd95fac
source-git-commit: f4e28d89023e8f326e6816ebd8168e1e31e772ce
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# Konfigurera översättningsregler {#configure-translation-rules}

Lär dig hur du definierar översättningsregler för att identifiera innehåll för översättning.

## Story hittills {#story-so-far}

I det föregående dokumentet om den AEM översättningsresan utan headless [Konfigurera översättningsintegrering](configure-connector.md) du lärde dig att installera och konfigurera översättningsintegrationen och bör nu:

* Förstå de viktiga parametrarna i översättningsintegreringsramverket i AEM.
* Du kan skapa en egen anslutning till översättningstjänsten.

Nu när integreringen är klar tar den här artikeln dig igenom nästa steg för att identifiera vilket innehåll du behöver översätta.

>[!CAUTION]
>
>Det här steget i dokumentationsresan är bara nödvändigt om du inte använder **Översättningsbar** flagga på innehållsfragment.
>
>* The **Översättningsbar** flagga skapar automatiskt översättningsregler åt dig och kräver ingen åtgärd.
>* The **Översättningsbar** -flaggan används bara om konfigurationen för översättningsintegreringsramverket är inställd på **[Aktivera fält för innehållsmodell för översättning](/help/sites-cloud/administering/translation/integration-framework.md)**.
>* Om du aktiverar det här alternativet i TIF-konfigurationen ersätts eventuella manuellt skapade översättningsregler.|

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du använder AEM översättningsregler för att identifiera ditt översättningsinnehåll. När du har läst det här dokumentet bör du:

* Förstå vad översättningsreglerna gör.
* Ange egna översättningsregler.

## Översättningsregler {#translation-rules}

Content Fragments, som representerar ditt headless-innehåll, kan innehålla mycket information som är ordnad efter strukturerade fält. Beroende på dina projektbehov är det troligt att inte alla fält i ett innehållsfragment måste översättas.

Översättningsregler identifierar innehållet som ingår i, eller utesluts från, översättningsprojekt. När innehåll översätts extraherar AEM eller skördar innehållet baserat på dessa regler. På så sätt skickas endast innehåll som måste översättas till översättningstjänsten.

Översättningsreglerna innehåller följande information:

* Sökvägen till det innehåll som regeln gäller för
   * Regeln gäller även för innehållets underordnade
* Namnen på egenskaperna som innehåller det innehåll som ska översättas
   * Egenskapen kan vara specifik för en viss resurstyp eller för alla resurstyper

Eftersom modeller för innehållsfragment, som definierar strukturen för dina innehållsfragment, är unika för ditt eget projekt, är det viktigt att skapa översättningsregler så att AEM vet vilka element i dina innehållsmodeller som ska översättas.

>[!TIP]
>
>Innehållsarkitekten förser översättningsspecialisten med **Egenskapsnamn**&#x200B;är en del av alla fält som behövs för översättning. Dessa namn behövs för att konfigurera översättningsregler. Som översättningsspecialist [kan hitta dessa **Egenskapsnamn**&#x200B;är dig själv](getting-started.md#content-modlels) som tidigare beskrivits under denna resa.

## Skapa översättningsregler {#creating-rules}

Flera regler kan skapas för komplexa översättningskrav. Ett projekt som du kanske arbetar med kräver att alla fält i modellen översätts, men i andra bara beskrivningsfält måste de översättas medan rubrikerna inte översätts.

Översättningsregler är utformade för att hantera sådana scenarier. I det här exemplet illustrerar vi dock hur du skapar regler genom att fokusera på en enkel konfiguration.

Det finns en **Översättningskonfiguration** konsolen är tillgänglig för konfigurering av översättningsregler. Så här kommer du åt den:

1. Navigera till **verktyg** -> **Allmänt**.
1. Tryck eller klicka **Översättningskonfiguration**.

I **Översättningskonfiguration** Det finns ett antal alternativ för översättningsreglerna. Här beskrivs de mest nödvändiga och typiska stegen som krävs för en grundläggande headless-lokaliseringskonfiguration.

1. Tryck eller klicka **Lägg till kontext**så att du kan lägga till en bana. Detta är sökvägen till innehållet som påverkas av regeln.
   ![Lägg till kontext](assets/add-translation-context.png)
1. Använd sökvägsläsaren för att välja önskad sökväg och tryck eller klicka på **Bekräfta** knappen som ska sparas. Kom ihåg att innehållsfragment, som innehåller headless-innehåll, vanligtvis finns under `/content/dam/<your-project>`.
   ![Markera banan](assets/select-context.png)
1. AEM sparar konfigurationen.
1. Du måste välja den kontext du just skapade och sedan trycka eller klicka **Redigera**. Då öppnas **Redigerare för översättningsregler** för att konfigurera egenskaperna.
   ![Redigerare för översättningsregler](assets/translation-rules-editor.png)
1. Som standard ärvs alla konfigurationer från den överordnade sökvägen, i det här fallet `/content/dam`. Avmarkera alternativet **Ärv från`/content/dam`** så att du kan lägga till fler fält i konfigurationen.
1. När avmarkerat, under **Allmänt** i listan lägger du till egenskapsnamnen för de innehållsfragmentmodeller som du [som tidigare identifierats som fält för översättning.](getting-started.md#content-models)
   1. Ange egenskapsnamnet i dialogrutan **Ny egenskap** fält.
   1. Alternativen **Översätt** och **Inherit** kontrolleras automatiskt.
   1. Tryck eller klicka **Lägg till**.
   1. Upprepa dessa steg för alla fält som du måste översätta.
   1. Tryck eller klicka **Spara**.
      ![Lägg till egenskap](assets/add-property.png)

Du har nu konfigurerat dina översättningsregler.

## Avancerad användning {#advanced-usage}

Det finns ett antal ytterligare egenskaper som kan konfigureras som en del av översättningsreglerna. Dessutom kan du ange regler manuellt som XML, vilket ger större specificitet och flexibilitet.

Sådana funktioner behövs vanligtvis inte för att komma igång med lokalisering av ditt headless-innehåll, men du kan läsa mer om dem i [Ytterligare resurser](#additional-resources) om du är intresserad.

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av den headless översättningsresan ska du:

* Förstå vad översättningsreglerna gör.
* Ange egna översättningsregler.

Bygg vidare på den här kunskapen och fortsätt din AEM resa med headless translation genom att nästa gång du granskar dokumentet [Översätta innehåll](translate-content.md) där du får lära dig hur integrering och regler fungerar tillsammans för att översätta headless-innehåll.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av den headless-översättningsresan genom att granska dokumentet [Översätta innehåll,](translate-content.md) Nedan följer ytterligare, valfria resurser som gör en djupdykning i vissa koncept som nämns i det här dokumentet, men som inte behöver fortsätta på den headless-resan.

* [Identifiera innehåll som ska översättas](/help/sites-cloud/administering/translation/rules.md) - Lär dig hur översättningsregler identifierar innehåll som behöver översättas.
