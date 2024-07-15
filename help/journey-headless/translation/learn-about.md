---
title: Lär dig mer om Headless-innehåll och översättning i AEM
description: Lär dig headless-koncept, hur de AEM och teorin om AEM översättning.
exl-id: 72bb6646-e573-4576-8d17-49787d8c8c7f
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 0%

---

# Lär dig mer om headless-innehåll och hur du översätter det i AEM {#learn-about}

Lär dig headless-koncept, hur de AEM och teorin om AEM översättning.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur headless-innehåll levereras, hur AEM hanterar headless-innehåll och hur sådant innehåll kan översättas. När du har läst bör du:

* Förstå de grundläggande begreppen för leverans av headless-innehåll.
* Lär dig hur AEM hanterar headless och translation.

## Leverans av högklassigt innehåll {#full-stack}

Ända sedan de lättanvända, storskaliga CMS:erna (Content Management System) började användas har organisationer använt dem som en central plats för att hantera meddelanden, varumärken och kommunikation. Att använda CMS som en central punkt för att administrera upplevelser har förbättrat effektiviteten genom att eliminera behovet av att duplicera uppgifter i olika system.

![Klassisk CMS i full hög](/help/journey-headless/developer/assets/full-stack.png)

I ett CMS-system i full hög finns funktionen för att hantera innehåll i CMS-systemet. Systemets funktioner består av olika komponenter i CMS-stacken. Lösningen i full hög har många fördelar.

* Det finns ett system att underhålla.
* Innehållet hanteras centralt.
* Alla tjänster i systemet är integrerade.
* Det går smidigt att skapa innehåll.

Om en ny kanal måste läggas till eller stöd för nya typer av upplevelser krävs, kan en (eller flera) ny komponent infogas i högen och det finns bara en plats att göra ändringar på.

![Lägger till en ny kanal i högen](/help/journey-headless/developer/assets/adding-channel.png)

Men komplexiteten i beroendena i högen blir snabbt uppenbar eftersom andra objekt i högen måste justeras för att passa ändringarna.

## Huvudet utan huvud {#the-head}

Huvudet för alla system är vanligtvis systemets utdatarenderare, vanligtvis i form av ett grafiskt gränssnitt eller andra grafiska utdata.

När vi talar om ett headless CMS hanterar CMS-systemet innehållet och fortsätter att leverera det till konsumenterna. Om **content** endast levereras på ett standardiserat sätt utesluter dock ett headless CMS den slutliga utdatarenderingen och **presentationen** av innehållet lämnas till den förbrukande tjänsten.

![Headless CMS](/help/journey-headless/developer/assets/headless-cms.png)

De konsumerande tjänsterna, oavsett om de är AR-upplevelser, en webbutik, mobilupplevelser, progressiva webbappar (PWA) och så vidare, tar in innehåll från det headless CMS-systemet och tillhandahåller sin egen rendering. De ser till att kunna erbjuda sina egna huvuden för ert innehåll.

Om du utelämnar huvudet förenklas CMS-systemet genom att komplexiteten försvinner. När du gör det flyttas även ansvaret för att återge innehållet till de tjänster som faktiskt behöver innehållet och som ofta är bättre lämpade för sådan återgivning.

## Översätta rubrikfritt innehåll i AEM {#translating-in-aem}

Förutom kraftfulla verktyg för att skapa, hantera och leverera traditionella webbsidor i full hög erbjuder AEM även möjligheten att skapa fristående innehållsmarkeringar och leverera dem utan problem.

Tack vare AEM kan det leverera innehåll antingen utan huvud eller stackar eller i båda modellerna samtidigt. För översättningsexperten kan samma uppsättning översättningsverktyg användas för båda typerna av innehåll, vilket ger en enhetlig metod för översättning av ditt innehåll.

Lär dig mer om hur AEM översätter innehåll, men på en hög nivå är konceptet enkelt:

1. Definiera en anslutning till en översättningstjänst genom att konfigurera översättningsintegreringsramverket.
1. Definiera vilket innehåll som ska översättas med översättningsregler.
1. Skapa ett översättningsprojekt för att hämta innehållet, skicka det till översättningstjänsten och få resultaten.
1. Granska och publicera det översatta innehållet.

## What&#39;s Next {#what-is-next}

Tack för att du kom igång med din AEM översättningsresa utan trassel! Nu när du läser det här dokumentet bör du:

* Förstå de grundläggande begreppen för leverans av headless-innehåll.
* Lär dig hur AEM hanterar headless och translation.

Bygg vidare på den här kunskapen och fortsätt din AEM översättningsresa utan rubriker genom att gå igenom dokumentet [Kom igång med AEM översättningen](getting-started.md) där du får en översikt över hur AEM hanterar innehåll utan rubriker och lär dig dess översättningsverktyg.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av den headless-översättningsresan genom att granska dokumentet [Kom igång med AEM headless-översättning](getting-started.md), men följande är ytterligare, valfria resurser som gör en djupdykning i vissa koncept som nämns i det här dokumentet, men de behöver inte fortsätta på den headless-resan.

* [MSM och översättning](/help/sites-cloud/administering/msm-and-translation.md) - Information om hur du AEM Multi-Site Manager och hur det fungerar med översättningsverktygen
* [Introduktion till AEM som headless CMS](/help/headless/introduction.md)
* [Tutorials för Headless i AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)