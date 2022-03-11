---
title: Läs vad är Cloud Manager
description: Följ den här sidan om du vill veta mer om Cloud Manager, Cloud Manager-program och miljöer.
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: c206bc241bccf6f8a5bfb4946d6231f53438861a
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 3%

---

# Introduktion till Cloud Manager {#intro-cloud-manager}

Cloud Manager är en viktig komponent i AEM as a Cloud Service och fungerar som en enda startpunkt för ditt team.

För att ge stöd åt kunder med företagskonfigurationer kan AEM as a Cloud Service integreras helt med Cloud Manager och dess specialbyggda CI/CD-pipelines, som är utrustade för att säkerställa grundlig testning och högsta kodkvalitet för att leverera enastående upplevelser.

För att säkerställa att kunderna kan komma igång snabbt med AEM as a Cloud Service har Cloud Manager allt som behövs för att komma igång på ett självbetjäningssätt, inklusive möjligheten att skapa molnresurser och miljöer. På så sätt kan dina AEM utvecklare få åtkomst till Git-databasen via Cloud Manager. Med hjälp av Cloud Manager kan utvecklingsteam arbeta för att implementera ändringar ofta på ett självbetjäningssätt.

Din systemadministratör ansvarar för att konfigurera ditt Cloud Manager-team, som kommer att innehålla personer som skapar dina molnresurser och utvecklare. Se [Inställningar för utveckling av Enterprise-team för AEM as a Cloud Service](/help/implementing/cloud-manager/managing-code/enterprise-team-dev-setup.md) om du vill veta mer om hur Cloud Manager kan användas i installationsprogrammet för Enterprise Team Development.

## Navigera till översiktssidan för Cloud Manager {#navigate-cloud-manager}

Följ stegen nedan för att navigera till Cloud Manager:

1. Navigera direkt till inloggningssidan för Cloud Manager från [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

   >[!NOTE]
   >Bokmärk den här sidan för framtida referens och för att hjälpa dig att navigera direkt till Cloud Managers landningssida.

1. Välj program från Cloud Managers **Program och produkter** sidan som startar **Översikt** sida.

Dessutom kan du gå till sidan Program och produkter i Cloud Manager från Adobe Experience Cloud hemsida. Följ stegen nedan:

1. Navigera direkt till [Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home) och logga in med din Adobe ID.

1. Välj **Experience Manager**.

1. Klicka på **Starta** från Cloud Manager-kortet. När du har loggat in på Cloud Manager är du redo att använda användargränssnittet.

   När inloggningen är klar dirigeras du till landningssidan för Cloud Manager.

## Rollbaserade behörigheter i Cloud Manager {#role-based-permissions}

| Behörighet | Beskrivning | Business Owner | Deployment Manager | Program Manager | Developer |
|--- |--- |--- |--- |--- |--- |
| Lägg till program<br>Redigera program | Lägg till ett nytt program.<br>Redigera ett program - Lägg till eller ta bort lösningar eller tillägg | x |  |  |  |
| Skapa miljö | Skapa prod+stage, dev, environment. | x | x |  |  |
| Uppdateringsmiljö | Uppdatera Prod+Stage, Dev, Environmental. | x | x |  |  |
| Ta bort Dev-miljö | Ta bort Dev-miljöer. | x | x |  |  |
| Inställningar för pipeline | Konfigurera eller redigera pipeline. |  | x |  |  |
| Körning av pipeline | Starta rörledningen. | x | x |  |  |
| Körning av pipeline | Avvisa/godkänn viktiga 3-nivåfel. | x | x | x |  |
| Körning av pipeline | Godkänn GoLive. | x | x | x |  |
| Körning av pipeline | Schemalägg produktionsdistribution. | x | x | x |  |
| Ta bort pipeline | Tillåter borttagning av en pipeline. |  | x |  |  |
| Avbryt körning | Avbryt aktuell körning. |  | x |  |  |
| Generera token för personlig åtkomst | Access Git. |  | x |  | x |

>[!NOTE]
>En användare kan tilldelas flera roller. Om du till exempel tilldelar både Business Owner- och Deployment Manager-roller till en användare får användaren en kombination av eller summan av dessa behörigheter.

## Cloud Manager-program {#cloud-manager-programs}

Cloud Manager-program representerar uppsättningar av Cloud Manager-miljöer som stöder logiska uppsättningar av affärsinitiativ, vilket vanligtvis motsvarar ett köpt serviceavtal (SLA). Ett program kan t.ex. representera de AEM resurserna för att stödja de globala offentliga webbplatserna, medan ett annat program representerar en intern central DAM. Titta på detta [video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en) om du vill veta mer om hur du använder Cloud Manager-program.

En användare kan skapa **Sandbox** eller en **Produktion** program.

* A *Produktionsprogram* skapas för att möjliggöra livstrafik vid rätt tidpunkt i framtiden.
Se [Introduktion till produktionsprogram](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/production-programs/introduction-production-programs.html?lang=en) för mer information.

* A *Sandbox Program* skapas vanligtvis för utbildning, för att köra demonstrationer, aktivering, POC:er eller dokumentation. Den är inte avsedd att transportera livstrafik och kommer att ha begränsningar som ett produktionsprogram inte kommer att ha. Den kommer att innehålla Sites and Assets och levereras automatiskt ifylld med en Git-gren som innehåller exempelkod, en Dev-miljö och en icke-produktionsprocess.
Se [Introduktion till sandlådeprogram](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sandbox-programs/introduction-sandbox-programs.html?lang=en) för mer information.

## Cloud Manager-miljöer {#cloud-manager-environments}

Dina molnmiljöer skapas, öppnas och visas via Cloud Manager. Det kan vara en produktionsmiljö, scenmiljö eller utvecklingsmiljö. Olika miljöer har stöd för olika syften och kan användas med olika CI/CD-ledningar. Miljöer består av tjänster som:

* [AEM Author Services](#author-services)
* [AEM Publish Services](#publish-services)
* [Dispatcher Services](#dispatcher-services)

   >[!NOTE]
   > Se videon [Använda Adobe Cloud Manager-miljöer](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en#cloud-manager) om du vill veta mer om de tillgängliga miljöerna. Mer information finns i [Hantera miljöer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en) om du vill veta mer om de typer av miljöer som en användare kan skapa och hur användaren kan skapa en miljö.

### AEM Author Service {#author-services}

AEM Author Service ingår i en miljö där webbplatsinnehåll och digitala resurser skapas, hanteras och uppdateras. Vanligtvis har bara interna användare åtkomst till författartjänsten och är bakom en inloggningsskärm. Redigeringstjänsten är utformad både som en redigerings- och förhandsvisningsmiljö.

### AEM Publish Service {#publish-services}

AEM Publish Service ingår i en miljö som är värd för slutanvändarens upplevelse, som en webbplats. Det här är den tjänst besökarna på webbplatsen kommer att se och interagera med. Publiceringstjänsten är vanligtvis tillgänglig för alla.

### AEM Dispatcher Service {#dispatcher-services}

Dispatcher är en `Apache HTTP Web server` som tillhandahåller ett säkerhets- och prestandalager som placeras framför AEM Publish Service.
