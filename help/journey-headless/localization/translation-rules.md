---
title: Konfigurera översättningsregler
description: Lär dig hur du definierar översättningsregler för att identifiera innehåll för lokalisering.
source-git-commit: 22ca7c01bfddb407c119de7d9a4d105941772664
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---

# Konfigurera översättningsregler {#configure-translation-rules}

Lär dig hur du definierar översättningsregler för att identifiera innehåll för lokalisering.

## Story hittills {#story-so-far}

I det tidigare dokumentet av den AEM headless-lokaliseringsresan lärde du dig [Konfigurera översättningskopplingen](configure-connector.md) hur du installerar och konfigurerar översättningskopplingen och bör nu:

* Förstå de viktiga parametrarna i översättningsintegreringsramverket i AEM.
* Du kan skapa en egen anslutning till översättningstjänsten.

Nu när du har konfigurerat din koppling tar den här artikeln dig igenom nästa steg för att identifiera vilket innehåll du behöver översätta.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du använder AEM översättningsregler för att identifiera ditt översättningsinnehåll. När du har läst det här dokumentet bör du:

* Förstå vad översättningsreglerna gör.
* Du kan definiera egna översättningsregler.

## Översättningsregler {#translation-rules}

Översättningsregler identifierar innehållet som ingår i, eller utesluts från, översättningsprojekt. När innehållet översätts extraherar AEM innehållet baserat på dessa regler så att det kan skickas till översättningstjänsten via den koppling du redan har konfigurerat.

Översättningsreglerna innehåller följande information:

* Sökvägen till det innehåll som regeln gäller för
   * Regeln gäller även för innehållets underordnade
* Namnen på egenskaperna som innehåller det innehåll som ska översättas
   * Egenskapen kan vara specifik för en viss resurstyp eller för alla resurstyper

Eftersom Content Fragment Models är unik för ditt eget projekt är det viktigt att skapa översättningsregler så AEM vet vilka element i dina innehållsmodeller som ska översättas.

## Skapa översättningsregler {#creating-rules}

Flera regler kan skapas för komplexa översättningskrav. Ett projekt som du kanske arbetar med kräver till exempel att alla fält i modellen översätts, men i andra bara beskrivningsfält måste de översättas medan rubrikerna inte översätts.

Översättningsregler är utformade för att hantera sådana scenarier. I det här exemplet illustrerar vi dock hur man skapar regler genom att fokusera på en enkel konfiguration.

Det finns en **översättningskonsol** tillgänglig för konfigurering av översättningsregler. Så här kommer du åt den:

1. Navigera till **Verktyg** -> **Allmänt**.
1. Tryck eller klicka på **Översättningskonfiguration**.

I gränssnittet **Översättningskonfiguration** finns det ett antal alternativ för översättningsreglerna. Här beskrivs de mest nödvändiga och typiska stegen som krävs för en grundläggande headless-lokaliseringskonfiguration.

1. Tryck eller klicka på **Lägg till kontext**, så kan du lägga till en sökväg. Detta är sökvägen till innehållet som ska påverkas av regeln.
   ![Lägg till kontext](assets/add-translation-context.png)
1. Använd sökvägsläsaren för att välja önskad sökväg och tryck eller klicka på knappen **Bekräfta** för att spara. Kom ihåg att innehållsfragment, som innehåller headless-innehåll, vanligtvis finns under `/content/dam/<your-project>`.
   ![Markera banan](assets/select-context.png)
1. AEM sparar konfigurationen.
1. Du måste markera den kontext du just skapade och sedan trycka eller klicka på **Redigera**. Då öppnas **Översättningsregelredigeraren** för att konfigurera egenskaperna.
   ![Redigerare för översättningsregler](assets/translation-rules-editor.png)
1. Som standard ärvs alla konfigurationer från den överordnade sökvägen, i det här fallet `/content/dam`. Avmarkera alternativet **Ärv från`/content/dam`** om du vill lägga till fler fält i konfigurationen.
1. När det är avmarkerat, under avsnittet **Allmänt** i listan, lägger du till de egenskapsnamn som du [tidigare identifierat som fält för översättning.](getting-started.md#content-models)
   1. Ange egenskapsnamnet i fältet **Ny egenskap**.
   1. Alternativen **Översätt** och **Ärv** kontrolleras automatiskt.
   1. Tryck eller klicka på **Lägg till**.
   1. Upprepa dessa steg för alla fält som du behöver översätta.
   1. Tryck eller klicka på **Spara**.
      ![Lägg till egenskap](assets/add-property.png)

Du har nu konfigurerat dina översättningsregler.

## Avancerad användning {#advanced-usage}

Det finns ett antal ytterligare egenskaper som kan konfigureras som en del av översättningsreglerna. Dessutom kan du ange regler manuellt som XML, vilket ger större specificitet och flexibilitet.

Sådana funktioner behövs vanligtvis inte för att komma igång med lokaliseringen av ditt headless-innehåll, men du kan läsa mer om dem i [Additional Resources](#additional-resources)-avsnittet om du är intresserad.

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av den headless lokaliseringsresan bör du:

* Förstå vad översättningsreglerna gör.
* Du kan definiera egna översättningsregler.

Bygg vidare på den här kunskapen och fortsätt din AEM resa med headless localization genom att nästa gång läsa dokumentet [Översätt innehåll](translate-content.md) där du får lära dig hur din koppling och dina regler fungerar tillsammans för att översätta headless-innehåll.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av den headless-baserade lokaliseringsresan genom att granska dokumentet [Översätt innehåll,](translate-content.md) är följande ytterligare, valfria resurser som gör en djupdykning i vissa koncept som nämns i det här dokumentet, men de behöver inte fortsätta den headless-resan.

* [Identifiera innehåll som ska översättas](/help/sites-cloud/administering/translation/rules.md)  - Lär dig hur översättningsregler identifierar innehåll som behöver översättas.
