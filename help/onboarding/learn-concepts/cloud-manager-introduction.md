---
title: Läs vad är Cloud Manager
description: Följ den här sidan om du vill veta mer om Cloud Manager, Cloud Manager-program och miljöer.
source-git-commit: 185a933e12ad81689168ad88574019ed219db06d
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---


# Introduktion till Cloud Manager {#intro-cloud-manager}

Cloud Manager är en viktig komponent i AEM som Cloud Service och fungerar som en enda startpunkt för ditt team.

För att ge stöd åt kunder med företagskonfigurationer kan AEM som Cloud Service helt och hållet integreras med Cloud Manager och dess specialbyggda CI/CD-pipelines, som är utrustade för att säkerställa grundlig testning och högsta kodkvalitet för att leverera enastående upplevelser.

För att säkerställa att kunderna snabbt kan komma igång med AEM som Cloud Service har Cloud Manager allt som behövs för att komma igång på ett självbetjäningssätt, inklusive möjligheten att skapa molnresurser och miljöer. På så sätt kan dina AEM utvecklare få åtkomst till Git-databasen via Cloud Manager. Med hjälp av Cloud Manager kan utvecklingsteam arbeta för att implementera ändringar ofta på ett självbetjäningssätt.

Din systemadministratör ansvarar för att konfigurera ditt Cloud Manager-team, som kommer att innehålla personer som skapar dina molnresurser och utvecklare. Läs [Enterprise Team Development Setup for AEM som Cloud Service](/help/implementing/cloud-manager/enterprise-team-dev-setup.md) om du vill veta hur Cloud Manager stöder i Enterprise Team Development Setup.

## Cloud Manager-program {#cloud-manager-programs}

Cloud Manager-program representerar uppsättningar av Cloud Manager-miljöer som stöder logiska uppsättningar av affärsinitiativ, som vanligtvis motsvarar ett köpt serviceavtal (SLA). Ett program kan t.ex. representera de AEM resurserna för att stödja de globala offentliga webbplatserna, medan ett annat program representerar en intern central DAM. Titta på den här [videon](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en) om du vill veta mer om hur du använder Cloud Manager-program.

En användare kan skapa en **sandlåda** eller ett **Production**-program.

* Ett *produktionsprogram* skapas för att aktivera livstrafik vid rätt tidpunkt i framtiden.
Mer information finns i [Introduktion till produktionsprogram](/help/onboarding/getting-access-to-aem-in-cloud/introduction-production-programs.md).

* Ett *sandlådeprogram* skapas vanligtvis för att användas i utbildningssyfte, köra demo, aktivering, POC eller dokumentation. Den är inte avsedd att transportera livstrafik och kommer att ha begränsningar som ett produktionsprogram inte kommer att ha. Den kommer att innehålla Sites and Assets och levereras automatiskt ifylld med en Git-gren som innehåller exempelkod, en Dev-miljö och en icke-produktionsprocess.
Mer information finns i [Introduktion till sandlådeprogram](/help/onboarding/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md).

## Cloud Manager-miljöer {#cloud-manager-environments}

Dina molnmiljöer skapas, öppnas och visas via Cloud Manager. Det kan vara en produktionsmiljö, scenmiljö eller utvecklingsmiljö. Olika miljöer har stöd för olika syften och kan användas med olika CI/CD-ledningar. Miljöer består av tjänster som:

* [AEM Author Services](#author-services)
* [AEM Publish Services](#publish-services)
* [Dispatcher Services](#dispatcher-services)

   >[!NOTE]
   > Se videon [Använda miljöer för Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en#cloud-manager) om du vill veta mer om de tillgängliga miljöerna. Läs även [Hantera miljöer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en) om du vill veta mer om vilka typer av miljöer en användare kan skapa och hur användaren kan skapa en miljö.

### AEM Author Service {#author-services}

AEM Author Service ingår i en miljö där webbplatsinnehåll och digitala resurser skapas, hanteras och uppdateras. Vanligtvis har bara interna användare åtkomst till författartjänsten och är bakom en inloggningsskärm. Redigeringstjänsten är utformad både som en redigerings- och förhandsvisningsmiljö.

### AEM Publish Service {#publish-services}

AEM Publish Service ingår i en miljö som är värd för slutanvändarens upplevelse, som en webbplats. Det här är den tjänst besökarna på webbplatsen kommer att se och interagera med. Publiceringstjänsten är vanligtvis tillgänglig för alla.

### AEM Dispatcher Service {#dispatcher-services}

Dispatcher är en `Apache HTTP Web server`-modul som tillhandahåller ett säkerhets- och prestandalager som placeras framför AEM Publish Service.