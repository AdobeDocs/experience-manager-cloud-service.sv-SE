---
title: Konfigurera översättningsregler för Headless-innehåll
description: Lär dig hur du definierar översättningsregler för att identifiera innehåll för översättning.
exl-id: 878ffd5d-0f10-4990-9779-bdf55cd95fac
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# Konfigurera översättningsregler {#configure-translation-rules}

Lär dig hur du definierar översättningsregler för att identifiera innehåll för översättning.

## Story hittills {#story-so-far}

I det tidigare dokumentet av den AEM översättningsresan [Konfigurera översättningsintegrering](configure-connector.md) lärde du dig att installera och konfigurera översättningsintegrationen och bör nu:

* Förstå de viktiga parametrarna i översättningsintegreringsramverket i AEM.
* Du kan skapa en egen anslutning till översättningstjänsten.

Nu när integreringen är klar tar den här artikeln dig igenom nästa steg för att identifiera vilket innehåll du behöver översätta.

>[!CAUTION]
>
>Det här steget i dokumentationsresan är bara nödvändigt om du inte använder flaggan **Översättningsbar** i innehållsfragment.
>
>* Flaggan **Översättningsbar** skapar automatiskt översättningsregler åt dig och kräver ingen åtgärd.
>* Flaggan **Översättningsbar** används bara om konfigurationen för översättningsintegreringsramverket är inställd på **[Aktivera fält för innehållsmodell för översättning](/help/sites-cloud/administering/translation/integration-framework.md)**.
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
>Innehållsarkitekten förser översättningsexperten med **egenskapsnamn** för alla fält som behövs för översättning. Dessa namn behövs för att konfigurera översättningsregler. Som översättningsspecialist kan du [hitta dessa **egenskapsnamn** för dig själv](getting-started.md#content-modlels) som tidigare beskrivits under den här resan.

## Skapa översättningsregler {#creating-rules}

Flera regler kan skapas för komplexa översättningskrav. Ett projekt som du kanske arbetar med kräver att alla fält i modellen översätts, men i andra bara beskrivningsfält måste de översättas medan rubrikerna inte översätts.

Översättningsregler är utformade för att hantera sådana scenarier. I det här exemplet illustrerar vi dock hur du skapar regler genom att fokusera på en enkel konfiguration.

Det finns en **översättningskonsol** tillgänglig för konfigurering av översättningsregler. Så här kommer du åt den:

1. Navigera till **Verktyg** > **Allmänt**.
1. Välj **Översättningskonfiguration**.

I användargränssnittet för **översättningskonfiguration** finns det flera tillgängliga alternativ för översättningsreglerna. Här beskrivs de mest nödvändiga och typiska stegen som krävs för en grundläggande headless-lokaliseringskonfiguration.

1. Välj **Lägg till kontext** om du vill lägga till en sökväg. Detta är sökvägen till innehållet som påverkas av regeln.
   ![Lägg till kontext](assets/add-translation-context.png)
1. Använd sökvägsläsaren för att välja den sökväg som krävs och välj **Bekräfta** för att spara. Kom ihåg att innehållsfragment, som innehåller headless-innehåll, vanligtvis finns under `/content/dam/<your-project>`.
   ![Markera banan](assets/select-context.png)
1. Markera kontexten som du skapade och välj sedan **Redigera**. Då öppnas **Redigeraren för översättningsregler** för att konfigurera egenskaperna.
   ![Redigerare för översättningsregler](assets/translation-rules-editor.png)
1. Som standard ärvs alla konfigurationer från den överordnade sökvägen, i det här fallet `/content/dam`. Avmarkera alternativet **Ärv från`/content/dam`** så att du kan lägga till fler fält i konfigurationen.
1. Om du inte markerar det här alternativet, under avsnittet **Allmänt** i listan, lägger du till egenskapsnamnen för de innehållsfragmentmodeller som du [tidigare identifierade som fält för översättning](getting-started.md#content-models).
   1. Ange egenskapsnamnet i fältet **Ny egenskap**. Observera att alternativen **Översätt** och **Ärv** kontrolleras automatiskt.
   1. Välj **Lägg till**.
   1. Upprepa dessa steg för alla fält som du måste översätta.
   1. Välj **Spara**.

      ![Lägg till egenskap](assets/add-property.png)

Du har nu konfigurerat dina översättningsregler.

## Avancerad användning {#advanced-usage}

Det finns flera andra egenskaper som kan konfigureras som en del av översättningsreglerna. Dessutom kan du ange regler manuellt som XML, vilket ger större specificitet och flexibilitet.

Sådana funktioner behövs vanligtvis inte för att komma igång med lokalisering av ditt headless-innehåll, men du kan läsa mer om dem i avsnittet [Ytterligare resurser](#additional-resources) om du är intresserad.

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av den headless översättningsresan ska du:

* Förstå vad översättningsreglerna gör.
* Ange egna översättningsregler.

Bygg vidare på den här kunskapen och fortsätt din AEM headless-översättning genom att nästa gång du granskar dokumentet [Översätt innehåll](translate-content.md) där du får lära dig hur integrering och regler fungerar tillsammans för att översätta rubrikfritt innehåll.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av den headless-översättningsresan genom att granska dokumentet [Översätt innehåll](translate-content.md), men följande är ytterligare, valfria resurser som gör en djupdykning i vissa koncept som nämns i det här dokumentet, men de behöver inte fortsätta på den headless-resan.

* [Identifierar innehåll som ska översättas](/help/sites-cloud/administering/translation/rules.md) - Lär dig hur översättningsregler identifierar innehåll som behöver översättas.
