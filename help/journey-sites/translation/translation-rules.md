---
title: Konfigurera översättningsregler
description: Lär dig hur du definierar översättningsregler för att identifiera innehåll för översättning.
index: true
hide: false
hidefromtoc: false
exl-id: 831009b8-8e09-4b0f-b0fd-4e21221c1455
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# Konfigurera översättningsregler {#configure-translation-rules}

Lär dig hur du definierar översättningsregler för att identifiera innehåll för översättning.

## Story hittills {#story-so-far}

I det föregående dokumentet om AEM Sites översättningsresa [Konfigurera översättningskoppling](configure-connector.md) du lärde dig att installera och konfigurera översättningskopplingen och bör nu:

* Förstå de viktiga parametrarna i översättningsintegreringsramverket i AEM.
* Du kan skapa en egen anslutning till översättningstjänsten.

Nu när du har konfigurerat din koppling tar den här artikeln dig igenom nästa steg för att identifiera vilket innehåll du behöver översätta.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du använder AEM översättningsregler för att identifiera ditt översättningsinnehåll. När du har läst det här dokumentet bör du:

* Förstå vad översättningsreglerna gör.
* Ange egna översättningsregler.

## Översättningsregler {#translation-rules}

AEM Sites sidor kan innehålla mycket information. Beroende på dina projektbehov är det troligt att inte all information på en sida behöver översättas.

Översättningsregler identifierar innehållet som ingår i, eller utesluts från, översättningsprojekt. När innehåll översätts extraherar AEM eller skördar innehållet baserat på dessa regler. På så sätt skickas endast innehåll som måste översättas till översättningstjänsten.

Översättningsreglerna innehåller följande information:

* Sökvägen till det innehåll som regeln gäller för
   * Regeln gäller även för innehållets underordnade
* Namnen på egenskaperna som innehåller det innehåll som ska översättas
   * Egenskapen kan vara specifik för en viss resurstyp eller för alla resurstyper

AEM skapar automatiskt översättningsregler för webbplatssidor, men eftersom varje projekts krav är olika är det viktigt att du vet hur du granskar och anpassar reglerna efter ditt projekt.

## Skapa översättningsregler {#creating-rules}

Flera regler kan skapas för komplexa översättningskrav. Ett projekt som du arbetar med kräver till exempel att all sidinformation översätts, men på en annan sida måste bara beskrivningar översättas medan rubrikerna inte översätts.

Översättningsregler är utformade för att hantera sådana scenarier. I det här exemplet illustrerar vi dock hur du skapar regler genom att fokusera på en enkel konfiguration.

Det finns en **Översättningskonfiguration** konsolen är tillgänglig för konfigurering av översättningsregler.

Så här kommer du åt den:

1. Navigera till **verktyg** -> **Allmänt**.
1. Tryck eller klicka **Översättningskonfiguration**.

AEM skapar automatiskt översättningsregler för allt innehåll. Så här visar du de här reglerna:

1. Välj `/content` kontext och sedan **Redigera** i verktygsfältet.
1. Översättningsregelredigeraren öppnas med de regler som AEM automatiskt har skapats för `/content` bana.

   ![Redigerare för översättningsregler](assets/translation-rules-editor.png)

1. De översatta sidegenskaperna finns under **Allmänt** i listan. Du kan lägga till eller uppdatera befintliga egenskapsnamn som du vill inkludera explicit i översättning.
   1. Ange egenskapsnamnet i dialogrutan **Ny egenskap** fält.
   1. Alternativen **Översätt** och **Inherit** kontrolleras automatiskt.
   1. Tryck eller klicka **Lägg till**.
   1. Upprepa dessa steg för alla fält som du måste översätta.
   1. Tryck eller klicka **Spara**.

Du har nu konfigurerat dina översättningsregler.

>[!NOTE]
>
>AEM skapar automatiskt översättningsregler. För enkla översättningsinställningar eller för att testa ett översättningsarbetsflöde behöver du inte skapa nya regler eller ändra de befintliga, automatiskt skapade reglerna. Detaljerna om dessa steg presenteras för att förklara hur reglerna fungerar och för att ge sammanhang åt hur AEM behandlar översättningar.

>[!TIP]
>
>Du kan också skapa regler för just din bana eller ditt projekt genom att trycka eller klicka på **Lägg till kontext** i översättningskonsolen. Detta ligger utanför den här kundresan.

## Avancerad användning {#advanced-usage}

Det finns ett antal ytterligare egenskaper som kan konfigureras som en del av översättningsreglerna. Dessutom kan du ange regler manuellt som XML, vilket ger större specificitet och flexibilitet.

Sådana funktioner behövs vanligtvis inte för att komma igång med lokalisering av ditt innehåll, men du kan läsa mer om dem i [Ytterligare resurser](#additional-resources) om du är intresserad.

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av AEM Sites översättningsresa ska du:

* Förstå vad översättningsreglerna gör.
* Ange egna översättningsregler.

Bygg vidare på den här kunskapen och fortsätt din översättning till AEM Sites genom att granska nästa gång dokumentet [Översätta innehåll](translate-content.md) där du lär dig hur era kontakter och regler fungerar tillsammans för att översätta innehåll.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av översättningsresan genom att granska dokumentet [Översätta innehåll,](translate-content.md) Nedan följer ytterligare, valfria resurser som fördjupar sig i några koncept som nämns i det här dokumentet, men som inte behöver fortsätta på resan.

* [Identifiera innehåll som ska översättas](/help/sites-cloud/administering/translation/rules.md) - Lär dig hur översättningsregler identifierar innehåll som behöver översättas.
