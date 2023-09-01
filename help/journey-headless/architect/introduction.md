---
title: Innehållsmodellering för AEM som ett headless CMS - en introduktion
description: En introduktion till hur du använder funktionerna i Adobe Experience Manager as a Cloud Service som Headless CMS för att utforma innehåll för ditt projekt.
exl-id: 62061d73-6fdb-440b-a7dd-b0d530d49186
source-git-commit: 94e5d0e84d5c55d0ff61a705e079b4dc8e32a777
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---

# Innehållsmodellering för AEM som ett headless CMS - en introduktion {#architect-headless-introduction}

I den här delen av [AEM Headless Content Architect Journey](overview.md)kan du lära dig de (grundläggande) begrepp och termer som behövs för att förstå innehållsmodellering när du använder Adobe Experience Manager (AEM) as a Cloud Service som Headless CMS.

Det här dokumentet hjälper er att förstå hur headless-innehåll levereras, hur AEM hanterar headless-innehåll och hur innehåll utformas för headless. När du har läst bör du:

* Förstå de grundläggande begreppen för leverans av headless-innehåll.
* Lär dig hur AEM stöder headless och innehållsmodellering.

## Syfte {#objective}

* **Målgrupp**: Nybörjare
* **Syfte**: Presentera de koncept och den terminologi som är relevanta för Headless Content Modeling.

## Leverans av högklassigt innehåll {#full-stack}

Ända sedan de lättanvända, storskaliga CMS:erna (Content Management System) började användas har organisationer använt dem som en central plats för att hantera meddelanden, varumärken och kommunikation. Att använda CMS som en central punkt för att administrera upplevelser har förbättrat effektiviteten genom att eliminera behovet av att duplicera uppgifter i olika system.

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

När vi talar om ett headless CMS hanterar CMS-systemet innehållet och fortsätter att leverera det till konsumenterna. Genom att bara leverera **innehåll** på ett standardiserat sätt utelämnar ett headless CMS den slutliga återgivningen och lämnar kvar **presentation** av innehållet till den konsumerande tjänsten.

![Headless CMS](/help/journey-headless/developer/assets/headless-cms.png)

De konsumerande tjänsterna, oavsett om de är AR-upplevelser, en webshop, mobilupplevelser, progressiva webbappar (PWA) osv., tar in innehåll från det headless CMS-systemet och tillhandahåller sin egen rendering. De ser till att kunna erbjuda sina egna huvuden för ert innehåll.

Om du utelämnar huvudet förenklas CMS-systemet genom att komplexiteten försvinner. När du gör det flyttas även ansvaret för att återge innehållet till de tjänster som faktiskt behöver innehållet och som ofta är bättre lämpade för sådan återgivning.

## Innehållsmodellering {#content-modeling}

Innehållsmodellering (även kallat datamodellering) är din specialitet, så vad behöver du tänka på när du modellerar för headless?

För att headless-programmen ska kunna komma åt ditt innehåll och göra något med det måste innehållet verkligen ha en fördefinierad struktur. Det skulle vara möjligt att ha ert innehåll som fri form, men det skulle göra livet till *mycket* komplicerade för programmen.

För AEM som innehållsarkitekt kommer du att göra innehållsmodelleringen för att utforma en rad olika **Modeller för innehållsfragment**. Dessa definierar strukturen som används när innehållsförfattare skapar **Innehållsfragment** som innehåller innehållet.

### Åtkomst till innehållet {#access-content}

Det här är mer av en detaljfråga - men det kan intressera dig, bara för att slutföra artikeln.

När du har skapat modellerna för innehållsfragment, och dina författare har använt dem för att generera innehållet, måste de headless-program ha tillgång till det här innehållet.

Adobe Experience Manager (AEM) as a Cloud Service kan selektivt komma åt dina innehållsfragment med hjälp av det AEM GraphQL-API:t och returnera endast det innehåll som behövs. Med API:t kan en utvecklare formulera frågor som markerar specifikt innehåll. Den här urvalsprocessen baseras på *din* Modeller för innehållsfragment.

Detta innebär att projektet kan leverera strukturerat material utan extra kostnad för användning i dina program.

## What&#39;s Next {#whats-next}

Nu när du har lärt dig koncept och terminologi är nästa steg att [Lär dig grunderna i modellering med Content Fragment Models](basics.md).

## Ytterligare resurser {#additional-resources}

* AEM Headless Developer Journey
   * [Läs om CMS Headless Development](/help/journey-headless/developer/learn-about.md)
   * [Lär dig modellera ditt innehåll](/help/journey-headless/developer/model-your-content.md)
* [Introduktion till AEM som headless CMS](/help/headless/introduction.md)
* [AEM Developer Portal](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)
* [Tutorials för Headless i AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)
