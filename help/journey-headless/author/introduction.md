---
title: Om du skriver för AEM som Headless CMS - en introduktion
description: En introduktion till hur du använder Adobe Experience Manager as a Cloud Service som Headless CMS för att skapa projektinnehåll.
exl-id: 065b00cb-a82d-4bcb-b2c9-44542cee6303
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---

# Om du skriver för AEM som Headless CMS - en introduktion {#author-headless-introduction}

I den här delen av [AEM Headless Content Author Journey](overview.md) kan du lära dig de (grundläggande) begrepp och termer som behövs för att förstå hur du skapar innehåll när du använder Adobe Experience Manager (AEM) as a Cloud Service som Headless CMS. Det handlar om att strukturera och skapa innehåll för leverans av headless-innehåll.

## Syfte {#objective}

* **Målgrupp**: Nybörjare
* **Mål**: Introducera de koncept och termer som är relevanta för Headless Authoring.

## Content Management System (CMS) {#content-management-system}

Vad är ett innehållshanteringssystem?

Ett innehållshanteringssystem (CMS) är precis vad det sägs vara - ett datorsystem som används för att hantera innehåll. Det är lite allmänt, så för att vara mer exakt används det (vanligtvis) för att hantera innehåll som du vill göra tillgängligt på dina webbplatser.

## Headless CMS {#headless-cms}

Headless är en term som används för att beskriva system som effektivt skiljer innehållet från hur det visas på webben.

Traditionellt sett hanterar du materialet i CMS och samma CMS ansvarar för återgivningen av materialet på webbsidorna.

Nu innebär headless att ditt innehåll kan hanteras i CMS och sedan nås av ett eller flera (oberoende) program.

Det innebär att innehållet kan levereras till alla enheter i en mängd olika format. Detta gör hela processen mycket mer flexibel och innebär också att du inte behöver bekymra dig om layout och formatering.

>[!NOTE]
>
>Om du vill veta mer om den tekniska informationen om Headless CMS kan du läsa mer på Learn About CMS Headless Development.

## Adobe Experience Manager as a Cloud Service {#aem-cloud-service}

Så vad är AEM?

Först och främst är AEM ett innehållshanteringssystem med många olika funktioner som också kan anpassas efter dina behov.

Detta innebär att det kan användas som

* Headless CMS
   * För headless kan ditt innehåll redigeras som **Innehållsfragment**.
Dessa är självständiga innehållsobjekt som kan nås direkt av ett antal program, eftersom de har en fördefinierad struktur som baseras på **modeller för innehållsfragment**.
Det innebär att innehållet kan nå ut till en mängd olika enheter, i en mängd olika format och med ett stort urval av funktioner.
(Och som en dubbelpanorering kan dessa fragment också användas när du skapar AEM webbsidor - om du vill.)

* &quot;Traditionell&quot; CMS
   * Innehåll skapas för webbsidor med hjälp av en rad komponenter som definierar hur innehållet återges på webbplatsen. Även här är AEM extremt flexibelt eftersom projektteamet kan utveckla anpassade komponenter.

## Innehållsmodellering {#content-modeling}

Innehållsmodellering (även kallat datamodellering) är alltså en annan teknisk term - varför ska det intressera dig som författare?

För att de headless-appar ska kunna komma åt ditt innehåll och göra något med det måste innehållet verkligen ha en fördefinierad struktur. Det skulle vara möjligt att ha ditt innehåll som en ledig form, men det skulle göra livet *mycket* komplicerat för programmen.

Processen att definiera strukturen för ditt innehåll som ska följas inbegriper att utforma en modell - och detta kallas datamodellering.

För AEM utför rollen Innehållsarkitektur (ofta en annan person) datamodelleringen för att utforma ett intervall av **modeller för innehållsfragment** som du sedan använder som grund för ditt innehåll med **Innehållsfragment**.

>[!NOTE]
>
>Om du vill veta mer om datamodellering kan du läsa mer under AEM Headless Content Architect Journey.

## What&#39;s Next {#whats-next}

Nu när du har lärt dig koncept och terminologi är nästa steg att [Lär dig grunderna i att skapa innehållsfragment](basics.md). Då introduceras den grundläggande hanteringen av AEM tillsammans med hur du skapar innehållsfragment.

## Ytterligare resurser {#additional-resources}

* [Introduktion till AEM som Headless CMS](/help/headless/introduction.md)

* [Självstudiekurser för Headless i AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=sv-SE)

* AEM Headless Developer Journey
   * [Läs om CMS Headless Development](/help/journey-headless/developer/learn-about.md)
   * [Lär dig modellera ditt innehåll](/help/journey-headless/developer/model-your-content.md)

* [AEM Developer Portal](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=sv-SE)

* [AEM Headless Content Architect Journey](/help/journey-headless/architect/overview.md)

* [AEM Headless Content Translation Journey](/help/journey-headless/translation/overview.md)
