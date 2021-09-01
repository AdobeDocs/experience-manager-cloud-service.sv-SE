---
title: AEM Headless Content Architect Journey
description: En introduktion till de kraftfulla och flexibla headless-funktionerna i Adobe Experience Manager som Cloud Service och hur du modellerar innehåll för ditt projekt.
index: true
hide: false
hidefromtoc: false
source-git-commit: 6605349c698325d432479fac0253a6fd53d7f175
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---


# Innehållsmodellering för Headless med AEM - en introduktion {#architect-headless-introduction}

I den här delen av [AEM Headless Content Architect Journey](overview.md) kan du lära dig de (grundläggande) begrepp och termer som behövs för att förstå innehållsmodellering för headless content delivery med Adobe Experience Manager (AEM) som Cloud Service.

Det här dokumentet hjälper er att förstå hur headless-innehåll levereras, hur AEM hanterar headless-innehåll och hur innehåll utformas för headless. När du har läst bör du:

* Förstå de grundläggande begreppen för leverans av headless-innehåll.
* Lär dig hur AEM stöder headless och innehållsmodellering.

## Syfte {#objective}

* **Målgrupp**: Nybörjare
* **Mål**: Lägg in de koncept och termer som är relevanta för Headless Content Modeling.

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

Men komplexiteten i beroendena i högen blir snabbt tydlig eftersom andra objekt i högen måste justeras för att kunna anpassa ändringarna.

## Huvudet utan huvud {#the-head}

Huvudet för alla system är vanligtvis systemets utdatarenderare, vanligtvis i form av ett grafiskt gränssnitt eller andra grafiska utdata.

När vi talar om ett headless CMS hanterar CMS-systemet innehållet och fortsätter att leverera det till konsumenterna. Om du bara levererar **innehållet** på ett standardiserat sätt utelämnar ett headless CMS-system den slutliga återgivningen och lämnar presentationen **av innehållet till den förbrukande tjänsten.**

![Headless CMS](/help/journey-headless/developer/assets/headless-cms.png)

De konsumerande tjänsterna, oavsett om de är AR-upplevelser, en webshop, mobilupplevelser, progressiva webbappar (PWA) osv., tar in innehåll från det headless CMS-systemet och tillhandahåller sin egen rendering. De ser till att kunna erbjuda sina egna huvuden för ert innehåll.

Om du utelämnar huvudet förenklas CMS-systemet genom att komplexiteten försvinner. När du gör det flyttas även ansvaret för att återge innehållet till de tjänster som faktiskt behöver innehållet och som ofta är bättre lämpade för sådan återgivning.

## Innehållsmodellering {#content-modeling}

Innehållsmodellering (även kallat datamodellering) är din specialitet, så vad behöver du tänka på när du modellerar för headless?

För att headless-programmen ska kunna komma åt ditt innehåll och göra något med det måste innehållet verkligen ha en fördefinierad struktur. Det skulle vara möjligt att ha ditt innehåll som friform, men det skulle göra livet *mycket* komplicerat för programmen.

För AEM som innehållsarkitekt kommer du att göra innehållsmodelleringen för att utforma ett intervall av **modeller för innehållsfragment**. Dessa definierar den struktur som används när innehållsförfattarna skapar de **innehållsfragment** som innehåller innehållet.

### Åtkomst till innehållet {#access-content}

Det här är mer av en detalj - men det kan intressera dig, bara för att slutföra artikeln.

När du har skapat modellerna för innehållsfragment, och dina författare har använt dem för att generera innehållet, måste de headless-program ha tillgång till det här innehållet.

Adobe Experience Manager (AEM) som Cloud Service kan selektivt komma åt dina innehållsfragment med AEM GraphQL API, och returnera endast det innehåll som behövs. Med API:t kan en utvecklare formulera frågor som markerar specifikt innehåll. Den här urvalsprocessen baseras på *dina* modeller för innehållsfragment.

Detta innebär att projektet kan leverera strukturerat material utan extra kostnad för användning i dina program.

## What&#39;s Next {#whats-next}

Nu när du har lärt dig koncept och terminologi är nästa steg att [Lär dig grunderna i modellering med Content Fragment Models](basics.md).

## Ytterligare resurser {#additional-resources}

* AEM Headless Developer Journey
   * [Läs om CMS Headless Development](/help/journey-headless/developer/learn-about.md)
   * [Lär dig modellera ditt innehåll](/help/journey-headless/developer/model-your-content.md)
