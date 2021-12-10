---
title: Experience Manager [!DNL AEM Forms] as a Cloud Service arkitektur
description: Förstå arkitekturen i [!DNL AEM Forms] as a Cloud Service att lära sig om plattformens skalbarhet, flexibilitet och prestanda.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 5%

---


# [!DNL AEM] as a Cloud Service arkitektur {#architecture}

[!DNL AEM Forms] as a Cloud Service standardiserar distributionsarkitekturen för alla kunder, med målet att helt frigöra kunderna från arkitekturöverväganden. Även om den nya AEM as a Cloud Service arkitekturen fortfarande bygger på begreppet mikrokärnor för uthållighet behöver kunderna inte bekymra sig om vilken mikrokärna de ska välja bland. Mikrokernelerna som används både på författaren och på publiceringssidan är unika för [!DNL AEM Cloud Service] och på annat sätt inte tillgängligt för kunder för anläggningsinstallationer.

AEM as a Cloud Service har en dynamisk arkitektur med ett varierande antal AEM instanser. Den innehåller miljöer för utveckling, fas, produktion och demonstration. Det innehåller verktyg för att hantera AEM instanser (Cloud Manager), upprätthålla användare och autentiseringar (Admin Console och IMS-system (Adobe Identity Management)), konfigurera cachelagring (Fast CDN) och molnbaserad utvecklingsmiljö. Mer information om arkitektur finns i [En introduktion till arkitekturen i [!DNL Adobe Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html?lang=en).

## Cloud Manager{#cloud-manager}

Cloud Manager är en viktig komponent i [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en). Varje ny innehavare av [!DNL AEM Forms] as a Cloud Service etableras först för åtkomst till Cloud Manager. Cloud Manager är den enda ingångspunkten för våra kunders operationer och utvecklarprofiler. Det är den plats där AEM program och miljöer kan hanteras. Cloud Manager har utvecklats till en självbetjäningsportal där huvudkomponenterna i AEM as a Cloud Service kan skapas och konfigureras:

* Skapa och hantera program
* Skapa och hantera AEM miljöer i programmen
* Skapa och hantera pipelines för distribution av kundkoden och konfigurationen till en viss miljö
* Få meddelanden om viktiga livscykelhändelser för dessa komponenter (t.ex. produktuppdateringar) Mer information om Cloud Manager finns i [Förstå Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html) och [Introduktion till Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html).

## Användare och autentisering {#users-and-authentication}

AEM as a Cloud Service har stöd för Admin Console för AEM och IMS-baserad autentisering (Adobe Identity Management System). Med Admin Console kan administratörer hantera alla Experience Cloud-användare centralt. Användare och grupper kan tilldelas produktprofiler som är kopplade till instanser i AEM as a Cloud Service, vilket gör att de kan logga in på instansen. Mer information om användare, autentisering och åtkomst av en instans av AEM as a Cloud Service finns i [IMS-stöd för [!DNL Adobe Experience Manager] as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#introduction).

Olika personer är involverade i en typisk [!DNL AEM Forms] projekt. När du har loggat in på [!DNL AEM Forms] as a Cloud Service instans, du kan [lägg till användare i Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html) för personuppgifter som gäller för din organisation eller ditt projekt och [tilldela användare till inbyggda grupper](forms-groups-privileges-tasks.md) för att ge dem nödvändiga behörigheter.

Att lära sig olika inbyggda [!DNL AEM Forms] specifika användargrupper och behörigheter tillgängliga för [!DNL AEM Forms] som en Cloud Services-instans, se [Konfigurera, användare, roller och grupper](forms-groups-privileges-tasks.md).

## Developer Experience {#developer-experience}

Den nya arkitekturen som stöder AEM as a Cloud Service medför några viktiga förändringar i den övergripande utvecklingsupplevelsen. Ett av de främsta målen med förändringen av utvecklarupplevelsen är att möjliggöra migrering till AEM as a Cloud Service så snabbt som möjligt, med små ändringar av befintlig anpassad kod.

## Molnutveckling {#cloud-development}

Här följer riktlinjerna för att köra befintlig kod smidigt i AEM as a Cloud Service miljö:

* Lagra kod och konfigurationer i Git-databasen för det associerade Cloud Manager-programmet. Det gör det enkelt att hantera och integrera kod med CI/CD.
* Gör programkod och konfiguration kompatibel med baslinjen [!DNL AEM Forms] bilder. Med de senaste API:erna kan du skapa snabbare och säkrare applikationer.
* Använd Cloud Manager-pipeline som är kopplad till Cloud Manager-miljön för att skapa och distribuera program. Det hjälper dig att få de senaste funktionerna och felen åtgärdade för [!DNL AEM Forms] as a Cloud Service för din miljö.
* Testa att dina anpassade program klarar alla kodkvalitets-, säkerhets- och prestandaggar som används i pipeline. Det hjälper till att bygga säkra och bättre fungerande applikationer som leder till bättre kundupplevelser. Du kan alltid använda användargränssnittet i Cloud Manager för att hoppa över vissa kontroller.
Den här processen kallas ofta för utveckling i molnet först. [!DNL AEM Forms] as a Cloud Service tillhandahåller också en SDK som stöder snabb utveckling innan väntande kodändringar och konfigurationsändringar görs i molnet.
Vissa gränssnitt som tidigare var en del av AEM QuickStart är inte längre tillgängliga för användare i den AEM as a Cloud Service miljön. Till exempel webbkonsolen där OSGI-paket och tillhörande konfiguration hanteras. Webbläsaren för CRXDE Lite-innehållslager blir bara tillgänglig för icke-produktionsmiljöer. En delmängd av de Web Console-funktioner som utvecklare behöver, särskilt när det gäller diagnostik och status, är tillgängliga via en ny utvecklarkonsol.
Ett av de vanligaste kraven för utvecklare är snabb åtkomst till loggfilerna för olika miljöer. Med [!DNL AEM Cloud Service], görs loggfilerna för de olika noderna i Författaren, Publicera tillgängliga via Cloud Manager, antingen i form av filer som kan hämtas eller via API:er för att anpassa loggarna. På grund av den tydliga åtskillnaden mellan kod och innehåll kan utvecklare utnyttja en viss process för att uppdatera innehåll som en del av en distribution. De typiska användningsområdena för innehåll som kan ändras är:
* Standardinnehåll som ingår i kundprojektet (t.ex. mappar, mallar, arbetsflöden).
* Definitioner för sökindex
* Listor för åtkomstkontroll och behörighet
* Tjänstanvändare och användargrupper
Konfigurera utvecklingsmiljön, [Konfigurera CI/CD-pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html)och lära sig [distribuera kod](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) på miljön.

## Lokal utveckling {#local-development}

När du konfigurerar och konfigurerar [!DNL AEM Forms] i en as a Cloud Service miljö kan du skapa utvecklings-, staging- och produktionsmiljöer. Konfigurera dessutom en lokal utvecklingsmiljö för snabb utveckling och upprepningar. Du kan hämta och konfigurera AEM SDK och [!DNL AEM Forms] arkiv med tilläggsfunktioner för att konfigurera en lokal [!DNL Forms] as a Cloud Service utvecklingsmiljö.  Detaljerade anvisningar finns i [Konfigurera en lokal utvecklingsmiljö](setup-local-development-environment.md).

## Felsökning {#debugging}

AEM as a Cloud Service använder självbetjäning, skalbar, molninfrastruktur. Det kräver att AEM utvecklare förstår och felsöker olika aspekter av AEM as a Cloud Service, från att bygga och distribuera till att få information om AEM program som körs. Mer information finns i [Felsökning AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en).
