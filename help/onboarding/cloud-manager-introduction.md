---
title: Introduktion till Cloud Manager
description: Läs om hur Cloud Manager stöder ditt AEM genom program, miljöer och rörledningar.
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: 33d587baba27ad54b1c9e34a36fadbd1dc56e3f5
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 4%

---

# Introduktion till Cloud Manager {#intro-cloud-manager}

Cloud Manager är en viktig komponent i AEM as a Cloud Service och fungerar som en enda startpunkt för ditt team. Dess specialbyggda CI/CD-ledningar är utrustade för att säkerställa grundlig testning och högsta kodkvalitet för att leverera exceptionella upplevelser. För att kunderna snabbt ska kunna starta sina projekt tillhandahåller Cloud Manager allt som behövs på ett självbetjäningssätt, inklusive möjligheten att skapa molnresurser och miljöer samt få tillgång till era Git-databaser. De här funktionerna ger stöd för företagsutvecklingsmiljöer så att team kan arbeta för att implementera ändringar ofta, snabbt leverera unika digitala upplevelser och snabba upp time-to-value-processen.

Din systemadministratör ansvarar för att konfigurera ditt Cloud Manager-team, som kommer att innehålla personer som skapar dina molnresurser och utvecklare. Mer information om hur du konfigurerar och skalar ditt utvecklingsteam och hur AEM as a Cloud Service kan stödja din utvecklingsprocess finns i dokumentet [Enterprise Team Development Setup för AEM as a Cloud Service.](/help/implementing/cloud-manager/managing-code/enterprise-team-dev-setup.md)

## Navigera till översiktssidan för Cloud Manager {#navigate-cloud-manager}

Följ de här stegen för att navigera till Cloud Manager.

1. Navigera till inloggningssidan för Cloud Manager på [`https://my.cloudmanager.adobe.com`.](https://my.cloudmanager.adobe.com/).

1. Välj programmet från Cloud Managers **Program och produkter** sidan som startar **Översikt** sida.

Du kan även navigera till Cloud Managers program- och produktsida från Adobe Experience Cloud hemsida genom att följa dessa steg.

1. Navigera till Adobe Experience Cloud på [`https://experience.adobe.com`](https://experience.adobe.com) och logga in med din Adobe ID.

1. Se till att du är i rätt organisation genom att referera till organisationsnamnet som visas längst upp till höger i verktygsfältet.

1. Välj **Experience Manager**.

1. På **Cloud Manager** kort, klicka på **Starta**

## Rollbaserade behörigheter i Cloud Manager {#role-based-permissions}

| Behörighet | Beskrivning | Business Owner | Deployment Manager | Program Manager | Developer |
|--- |--- |--- |--- |--- |--- |
| Lägg till program<br>Redigera program | Lägg till ett nytt program<br>Lägga till eller ta bort lösningar eller tillägg | x |  |  |  |
| Skapa miljö | Skapa produktions-+stagnings- och utvecklingsmiljöer | x | x |  |  |
| Uppdateringsmiljö | Uppdatera produktions-+stagnings- och utvecklingsmiljöer | x | x |  |  |
| Ta bort Dev-miljö | Ta bort utvecklingsmiljöer | x | x |  |  |
| Inställningar för pipeline | Konfigurera och redigera rörledningar |  | x |  |  |
| Körning av pipeline | Starta rörledningar | x | x |  |  |
| Körning av pipeline | Avvisa/godkänn viktiga fel med 3-skiktskvalitet | x | x | x |  |
| Körning av pipeline | Ge live-godkännande | x | x | x |  |
| Körning av pipeline | Schemalägg produktionsdistributioner | x | x | x |  |
| Ta bort pipeline | Tillåt radering av pipeline |  | x |  |  |
| Avbryt körning | Avbryt aktuell körning |  | x |  |  |
| Generera token för personlig åtkomst | Åtkomstgit |  | x |  | x |
| Skapa RDE | Skapa en snabb utvecklingsmiljö | x |  |  | x |
| Återställ RDE | Återställ en snabb utvecklingsmiljö | x |  |  | x |

>[!NOTE]
>
>En användare kan tilldelas flera roller. Till exempel tilldela båda **Företagsägare** och **Distributionshanteraren** roller till en användare ger användaren summan av dessa behörigheter.

## Cloud Manager-program {#cloud-manager-programs}

Cloud Manager-program representerar en uppsättning Cloud Manager-miljöer som stöder logiska grupperingar av affärsinitiativ. Dessa grupperingar motsvarar vanligtvis ett köpt servicenivåavtal (SLA). Ett program kan t.ex. representera de AEM resurserna för att stödja en organisations offentliga webbplats, medan ett annat program representerar en intern DAM.


Titta på detta [video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) om du vill veta mer om hur du använder Cloud Manager-program.

En användare kan skapa **Sandbox** eller en **Produktion** program.

* A **produktionsprogram** skapas för att möjliggöra livstrafik vid rätt tidpunkt i framtiden.
   * Se dokumentet [Introduktion till produktionsprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md) för mer information.

* A **sandlådeprogram** skapas vanligtvis för utbildning, löpande demonstrationer, aktivering, skapande av POC eller för dokumentation.
   * Den är inte avsedd att transportera levande trafik och kommer att ha begränsningar som ett produktionsprogram inte kommer att ha.
   * Den innehåller Sites and Assets och levereras automatiskt ifylld med en Git-gren som innehåller exempelkod, en utvecklingsmiljö och en icke-produktionsprocess.
   * Se dokumentet [Introduktion till sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) för mer information.

## Cloud Manager-miljöer {#cloud-manager-environments}

Dina molnmiljöer skapas, öppnas och visas via Cloud Manager. Dessa miljöer kan vara produktions-, staging- eller utvecklingsmiljöer. Olika miljöer har olika syften och kan användas med olika CI/CD-ledningar. Miljöer består av tjänster som:

* [AEM](#author-services)
* [AEM](#publish-services)
* [Dispatcher Services](#dispatcher-services)

>[!TIP]
>
> Se videon [Använda Adobe Cloud Manager-miljöer](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) en översikt över tillgängliga miljöer.
>
>Se dokumentet [Hantera miljöer](/help/implementing/cloud-manager/manage-environments.md) om du vill veta mer om de typer av miljöer som en användare kan skapa och hur användaren kan skapa en miljö.

### AEM {#author-services}

En AEM är inkluderad i miljöer där webbplatsinnehåll och digitala resurser skapas, hanteras och uppdateras. Vanligtvis har bara interna användare åtkomst till redigeringstjänsten och den bevaras bakom en inloggningsskärm. Utvecklingstjänsten fungerar både som redigerings- och förhandsvisningsmiljö.

### AEM {#publish-services}

En AEM publiceringstjänst ingår i miljöer som är värdar för slutanvändarens upplevelse, som en webbplats. Det här är den tjänst besökarna på webbplatsen kommer att se och interagera med. Publiceringstjänsten är vanligtvis tillgänglig för allmänheten.

### AEM Dispatcher Service {#dispatcher-services}

Avsändaren är en `Apache HTTP Web server` som tillhandahåller ett säkerhets- och prestandalager som placeras framför den AEM publiceringstjänsten.
