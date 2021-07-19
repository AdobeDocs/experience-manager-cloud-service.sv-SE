---
title: Lär dig mer om headless-innehåll och hur du lokaliserar i AEM
description: Lär dig headless-koncept, hur de mappas till AEM och teorin om AEM lokalisering.
source-git-commit: 22ca7c01bfddb407c119de7d9a4d105941772664
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# Lär dig mer om headless-innehåll och hur du lokaliserar i AEM {#learn-about}

Lär dig headless-koncept, hur de mappas till AEM och teorin om AEM lokalisering.

## Syfte {#objective}

Det här dokumentet hjälper er att förstå hur headless-innehåll levereras, hur AEM stöder headless-funktioner och hur sådant innehåll kan lokaliseras. När du har läst bör du:

* Förstå de grundläggande begreppen för leverans av headless-innehåll.
* Lär dig hur AEM hanterar headless och lokalisering.

## Leverans av högklassigt innehåll {#full-stack}

Ända sedan de lättanvända, storskaliga CMS-systemen (Content Management System) började användas har organisationer utnyttjat dem som en central plats för att hantera meddelanden, varumärken och kommunikation. Att använda CMS som en central punkt för att administrera upplevelser har förbättrat effektiviteten genom att eliminera behovet av att duplicera uppgifter i olika system.

![Klassisk CMS i full hög](/help/journey-headless/developer/assets/full-stack.png)

I ett CMS-system i full hög finns alla funktioner för att hantera innehåll i CMS-systemet. Systemets funktioner består av olika komponenter i CMS-stacken. Lösningen i full hög har många fördelar.

* Det finns ett system att underhålla.
* Innehållet hanteras centralt.
* Alla tjänster i systemet är integrerade.
* Det går smidigt att skapa innehåll.

Om en ny kanal behöver läggas till eller stöd för nya typer av upplevelser krävs, kan en (eller flera) ny komponent infogas i högen och det finns bara en plats att göra ändringar på.

![Lägga till en ny kanal i högen](/help/journey-headless/developer/assets/adding-channel.png)

Komplexiteten i beroendena i högen blir snabbt tydlig eftersom andra objekt i högen måste justeras för att passa ändringarna.

## Huvudet utan huvud {#the-head}

Huvudet för alla system är vanligtvis systemets utdatarenderare, vanligtvis i form av ett grafiskt gränssnitt eller andra grafiska utdata.

När vi talar om ett headless CMS hanterar CMS-systemet innehållet och fortsätter att leverera det till konsumenterna. Om du bara levererar **innehållet** på ett standardiserat sätt utelämnar ett headless CMS-system den slutliga återgivningen och lämnar presentationen **av innehållet till den förbrukande tjänsten.**

![Headless CMS](/help/journey-headless/developer/assets/headless-cms.png)

De konsumerande tjänsterna, oavsett om de är AR-upplevelser, en webshop, mobilupplevelser, progressiva webbappar (PWA) osv., tar in innehåll från det headless CMS-systemet och tillhandahåller sin egen rendering. De ser till att kunna erbjuda sina egna huvuden för ert innehåll.

Om du utelämnar huvudet förenklas CMS-systemet genom att komplexiteten försvinner. När du gör det flyttas även ansvaret för att återge innehållet till de tjänster som faktiskt behöver innehållet och som ofta är bättre lämpade för sådan återgivning.

## Lokalisera Headless-innehåll i AEM {#localizing-in-aem}

Förutom kraftfulla verktyg för att skapa, hantera och leverera traditionella webbsidor i full hög erbjuder AEM även möjligheten att skapa fristående innehållsmarkeringar och leverera dem utan problem.

Tack vare AEM kan det leverera innehåll antingen utan huvud eller stackar eller i båda modellerna samtidigt. För lokaliseringsspecialisten kan samma uppsättning lokaliseringsverktyg användas för båda typerna av innehåll, vilket ger en enhetlig metod för översättning av ditt innehåll.

## What&#39;s Next {#what-is-next}

Tack för att du kom igång med din AEM onaturliga lokaliseringsresa! Nu när du läser det här dokumentet bör du:

* Förstå de grundläggande begreppen för leverans av headless-innehåll.
* Lär dig hur AEM hanterar headless och lokalisering.

Bygg vidare på den här kunskapen och fortsätt din AEM resa med headlesslokalisering genom att gå igenom dokumentet [Kom igång med AEM headless localization](getting-started.md) där du får en översikt över hur AEM hanterar headless-innehåll och lär dig mer om dess lokaliseringsverktyg.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av den headless-baserade lokaliseringsresan genom att granska dokumentet [Kom igång med AEM headless-lokalisering,](getting-started.md), men följande är ytterligare, valfria resurser som gör en djupdykning i vissa koncept som nämns i det här dokumentet, men de behöver inte fortsätta den headless-resan.

* [MSM och översättning](/help/sites-cloud/administering/msm-and-translation.md)  - Information om AEM Multi-Site Manager och hur det fungerar med översättningsverktygen
