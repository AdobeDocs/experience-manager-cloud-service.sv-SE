---
title: Konfigurera översättningsregler
description: Lär dig hur du definierar översättningsregler för att identifiera innehåll för översättning.
index: true
hide: false
hidefromtoc: false
source-git-commit: 08127d72c84d6f47f5058ef631dc3128114f1953
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 0%

---


# Konfigurera översättningsregler {#configure-translation-rules}

Lär dig hur du definierar översättningsregler för att identifiera innehåll för översättning.

## Story hittills {#story-so-far}

I det tidigare dokumentet om AEM Sites översättningsresa lärde du dig [Konfigurera översättningskoppling](configure-connector.md) att installera och konfigurera översättningskopplingen och bör nu:

* Förstå de viktiga parametrarna i översättningsintegreringsramverket i AEM.
* Du kan skapa en egen anslutning till översättningstjänsten.

Nu när du har konfigurerat din koppling tar den här artikeln dig igenom nästa steg för att identifiera vilket innehåll du behöver översätta.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du använder AEM översättningsregler för att identifiera ditt översättningsinnehåll. När du har läst det här dokumentet bör du:

* Förstå vad översättningsreglerna gör.
* Du kan definiera egna översättningsregler.

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

Det finns en **översättningskonsol** tillgänglig för konfigurering av översättningsregler.

Så här kommer du åt den:

1. Navigera till **Verktyg** -> **Allmänt**.
1. Tryck eller klicka på **Översättningskonfiguration**.

AEM skapar automatiskt översättningsregler för allt innehåll. Så här visar du de här reglerna:

1. Välj sammanhanget `/content` och sedan alternativet **Redigera** i verktygsfältet.
1. Översättningsregelredigeraren öppnas med de regler som AEM automatiskt skapades för sökvägen `/content`.

   ![Redigerare för översättningsregler](assets/translation-rules-editor.png)

1. De sidegenskaper som ska översättas finns under avsnittet **Allmänt** i listan. Du kan lägga till eller uppdatera befintliga egenskapsnamn som du vill inkludera explicit i översättning.
   1. Ange egenskapsnamnet i fältet **Ny egenskap**.
   1. Alternativen **Översätt** och **Ärv** kontrolleras automatiskt.
   1. Tryck eller klicka på **Lägg till**.
   1. Upprepa dessa steg för alla fält som du måste översätta.
   1. Tryck eller klicka på **Spara**.

Du har nu konfigurerat dina översättningsregler.

>[!NOTE]
>
>AEM skapar automatiskt översättningsregler. För enkla översättningsinställningar eller för att testa ett översättningsarbetsflöde behöver du inte skapa nya regler eller ändra de befintliga, automatiskt skapade reglerna. Detaljerna om dessa steg presenteras för att förklara hur reglerna fungerar och för att ge sammanhang åt hur AEM behandlar översättningar.

>[!TIP]
>
>Det går också att skapa regler för just din sökväg eller ditt projekt genom att trycka eller klicka på knappen **Lägg till kontext** i översättningskonsolen. Detta ligger utanför den här kundresan.

## Avancerad användning {#advanced-usage}

Det finns ett antal ytterligare egenskaper som kan konfigureras som en del av översättningsreglerna. Dessutom kan du ange regler manuellt som XML, vilket ger större specificitet och flexibilitet.

Sådana funktioner behövs vanligtvis inte för att komma igång med lokaliseringen av ditt innehåll, men du kan läsa mer om dem i [Additional Resources](#additional-resources)-avsnittet om du är intresserad.

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av AEM Sites översättningsresa ska du:

* Förstå vad översättningsreglerna gör.
* Du kan definiera egna översättningsregler.

Bygg vidare på den här kunskapen och fortsätt din översättning till AEM Sites genom att nästa gång läsa dokumentet [Översätt innehåll](translate-content.md) där du får lära dig hur din koppling och dina regler fungerar tillsammans för att översätta innehåll.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av översättningsresan genom att granska dokumentet [Översätt innehåll,](translate-content.md) nedan är ytterligare, valfria resurser som gör en djupdykning i vissa koncept som nämns i det här dokumentet, men de behöver inte fortsätta på resan.

* [Identifiera innehåll som ska översättas](/help/sites-cloud/administering/translation/rules.md)  - Lär dig hur översättningsregler identifierar innehåll som behöver översättas.
