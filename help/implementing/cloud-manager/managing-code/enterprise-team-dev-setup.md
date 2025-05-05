---
title: Installation av Enterprise Development Team
description: Lär dig hur du konfigurerar och skalar ditt utvecklingsteam och se hur AEM as a Cloud Service kan stödja din utvecklingsprocess.
exl-id: 85f8779b-12cb-441b-a34d-04641184497a
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: cbeb3d8f5fa5cbf1839e1e8c5e651329b06e60a4
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 0%

---

# Installation av AEM as a Cloud Service i utvecklingsteamet {#enterprise-setup}

Lär dig hur du konfigurerar och skalar ditt utvecklingsteam och se hur AEM (Adobe Experience Manager) as a Cloud Service kan stödja din utvecklingsprocess.

## Introduktion {#introduction}

För att ge stöd åt kunder med företagskonfigurationer är AEM as a Cloud Service helt integrerat med Cloud Manager och dess [avsiktliga CI/CD-pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md). Dessa pipelines och tjänster byggs baserat på bästa praxis, vilket garanterar grundlig [testning och högsta kodkvalitet](/help/implementing/cloud-manager/code-quality-testing.md).

## Cloud Manager support vid konfiguration av utveckling av Enterprise-team {#cloud-manager}

För att säkerställa snabb introduktion tillhandahåller Cloud Manager allt som krävs för att komma igång med att utveckla digitala upplevelser direkt, inklusive en Git-databas för att lagra anpassningar som sedan byggs, verifieras och driftsätts av Cloud Manager.

Med Cloud Manager kan utvecklingsteamen arbeta för att implementera ändringar ofta utan att vara beroende av Adobe personal.

Det finns tre typer av miljöer i Cloud Manager.

* Utveckling
* Scen
* Produktion

Kod kan distribueras till utvecklingsmiljöer med hjälp av ett icke-produktionsflöde. För miljöer med staging och produktion, som alltid hänger ihop och därmed säkerställer validering före driftsättning som bästa praxis, använder en produktionspipeline [kvalitetsportar](/help/implementing/cloud-manager/custom-code-quality-rules.md) för att validera programkoden och konfigurationsändringarna.

Produktionspipelinen distribuerar koden och konfigurationen till staging-miljön först, testar programmet och distribuerar slutligen till produktionen.

En Cloud Service-SDK som alltid uppdateras med de senaste AEM as a Cloud Service-förbättringarna möjliggör lokal utveckling direkt med utvecklarens lokala maskinvara. Detta tillvägagångssätt möjliggör snabb utveckling med mycket låg vändningstid. Det innebär att utvecklare kan vara kvar i sin hemtama lokala miljö och välja bland en mängd olika utvecklingsverktyg och gå över till utvecklingsmiljöer eller produktion när de vill.

Cloud Manager har stöd för flexibla konfigurationer för flera team som kan anpassas efter företagets behov. För att säkerställa stabil driftsättning i flera team validerar och testar Cloud Manager avsiktliga pipeline koden från alla team tillsammans. Med den här metoden kan du förhindra situationer där ett teams ändringar påverkar produktionen för alla team.

## Exempel på verkliga livet {#real-world-example}

Varje företag har olika behov, inklusive olika arbetsflöden för teamkonfiguration, processer och utveckling. Konfigurationen som beskrivs nedan används av Adobe för flera projekt som levererar upplevelser utöver AEM as a Cloud Service.

Adobe Creative Cloud-programmen, till exempel Adobe Photoshop och Adobe Illustrator, innehåller t.ex. självstudiekurser, exempel och guider som är tillgängliga för slutanvändarna. Klientapplikationer konsumerar material från AEM as a Cloud Service utan extra kostnad. De gör API-anrop till AEM Cloud-publiceringsnivån för att hämta strukturerat innehåll som JSON-strömmar. Dessutom används [CDN (Content Delivery Network) i AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#content-delivery) för att leverera både strukturerat och ostrukturerat innehåll med optimala prestanda.

De team som bidrar till projektet följer följande process.

Varje team använder sitt eget utvecklingsarbetsflöde och har en separat Git-databas. Ytterligare en delad Git-databas används för introduktionsprojekt. Den här Git-databasen innehåller rotstrukturen för Cloud Manager Git-databasen, inklusive den delade Dispatcher-konfigurationen.

För att ett nytt projekt ska kunna introduceras måste det finnas en lista i projektfilen för reaktorn Maven i roten av den delade Git-databasen. För Dispatcher-konfigurationer skapas en ny konfigurationsfil i Dispatcher-projektet. Huvudkonfigurationen för Dispatcher innehåller sedan den här filen. Varje team ansvarar för sin egen Dispatcher-konfigurationsfil. Ändringar i den delade Git-databasen är ovanliga och behövs vanligtvis bara när ett nytt projekt har påbörjats. Huvudarbetet utförs av varje projektteam i deras egna Git-arkiv.

![Arbetsflödesdiagram](/help/implementing/cloud-manager/assets/team-setup1.png)

Git-databasen för var och en konfigureras med [AEM Project Archettype](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/developing/archetype/overview) och följer därför de bästa sätten att konfigurera AEM Projects. Det enda undantaget är Dispatcher-konfigurationen, som görs i den delade Git-databasen enligt ovan.

Varje team använder ett förenklat Git-arbetsflöde med två + N-grenar, enligt Git-flödesmodellen:

* En statisk versionsgren innehåller produktionskoden.

* En utvecklingsgren innehåller den senaste utvecklingen.

* För varje funktion skapas en ny gren.

Utvecklingen görs i en funktionsgren. När funktionen matas in sammanfogas den i utvecklingsgrenen. Slutförda och validerade funktioner väljs från utvecklingsgrenen och sammanfogas i den stabila grenen.

Alla ändringar görs via PR (Pull Requests). Kvalitetsportar validerar automatiskt varje PR. Sonar används för kvalitetskontroll av koden och en uppsättning testsviter körs för att säkerställa att den nya koden inte inför någon regression.

Inställningarna i Cloud Manager Git-databasen har två grenar.

* En stabil releasegren innehåller produktionskoden från alla team.
* En utvecklingsgren innehåller utvecklingskoden från alla team.

Varje push till ett teams Git-databas i antingen utvecklingen eller den stabila grenen utlöser en [GitHub-åtgärd](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md#managing-code).

Alla projekt följer samma inställningar för den stabila grenen. Ett push-steg till den stabila grenen av ett projekt överförs automatiskt till den stabila grenen i Cloud Manager Git-databasen. En knuff till den stabila grenen utlöser produktionsflödet i Cloud Manager. Alla påfrestningar som teamet gör till en stabil gren utlöser produktionsflödet. Produktionsdistributionen uppdateras om alla kvalitetsportar godkänns.

![Push-diagram](/help/implementing/cloud-manager/assets/team-setup2.png)

Överföringar till utvecklingsgrenen hanteras annorlunda. En push-överföring till en utvecklargren i ett teams Git-databas utlöser också en GitHub-åtgärd. Den här åtgärden överför automatiskt koden till utvecklingsgrenen i Cloud Manager Git-databasen. Den här kodpush-åtgärden utlöser dock inte automatiskt den icke-produktionsrelaterade pipelinen. Ett anrop till Cloud Manager API utlöser det.

I produktionsflödet kontrolleras koden för alla team via de angivna kvalitetspunkterna. När koden har distribuerats till scenen körs testerna och granskningarna så att allt fungerar som det ska. När alla portar har passerats förs ändringarna vidare till produktionen utan avbrott eller driftavbrott.

För lokal utveckling används [SDK för AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md#developing). Med SDK kan en lokal författare, publicering och Dispatcher konfigureras. Det här arbetsflödet möjliggör offlineutveckling och snabb vändningstid. Ibland används bara författarmiljön för utveckling, men om du snabbt konfigurerar Dispatcher- och publiceringsmiljöer kan du testa allt lokalt innan du tar dig in i Git-databasen.

Medlemmar i varje team checkar vanligtvis ut koden från den delade Git-koden för sin egen projektkod. Du behöver inte checka ut andra projekt eftersom projekten är oberoende.

![Lokal utcheckning och SDK](/help/implementing/cloud-manager/assets/team-setup3.png)

Denna verkliga konfiguration kan användas som en plan och sedan anpassas efter ett företags behov. Det flexibla förgrenade och sammanfogade konceptet i Git möjliggör variationer av arbetsflödena ovan, anpassade efter alla teamets behov. AEM as a Cloud Service stöder alla dessa variationer utan att offra kärnvärdet i Cloud Manager pipeline.

>[!TIP]
>
>Mer information om den här konfigurationen finns i [Arbeta med flera Source Git-databaser](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-manager/content/managing-code/multiple-git-repos#managing-code).

### Att tänka på vid konfiguration av flera team {#considerations}

Med Cloud Manager Git-lagringsplats och produktionsflödet passerar den fullständiga produktionskoden alltid genom alla kvalitetsportar och behandlar den som en driftsättningsenhet. På så sätt fungerar produktionssystemet alltid utan avbrott eller driftavbrott.

Utan ett sådant system finns det däremot en risk för att en uppdatering från ett team kan leda till produktionsstabilitetsproblem eftersom varje team kan driftsätta separat. Dessutom krävs samordning och planerad driftstopp för att lansera uppdateringar. Med ett ökande antal team blir samordningen mycket mer komplex och snabbt ohanterlig.

Om ett problem upptäcks i kvalitetsportarna påverkas inte produktionen, och problemet kan upptäckas och åtgärdas utan att Adobe personal behöver gå in i programmet. Utan Cloud Service och utan att alltid testa hela distributionen kan partiella distributioner orsaka avbrott som kräver en begäran om återställning eller till och med en fullständig återställning från en säkerhetskopia. Partiell testning kan också leda till ytterligare problem som måste lösas senare och som återigen kräver samordning och stöd från Adobe personal.

>[!TIP]
>
>För varje konfiguration av flera team är det viktigt att definiera en styrningsmodell och en uppsättning standarder som alla team måste följa. Den tidigare planen för en konfiguration för flera team tillåter skalning i ett större antal team, som du kan använda som utgångspunkt.
