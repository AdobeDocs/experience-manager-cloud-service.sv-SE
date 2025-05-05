---
title: Introduktion till Cloud Manager
description: Läs om hur Cloud Manager stöder AEM genom program, miljöer och rörledningar.
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---


# Introduktion till Cloud Manager {#intro-cloud-manager}

Cloud Manager är en viktig komponent i AEM as a Cloud Service och fungerar som en gemensam startpunkt för ert team. Dess specialbyggda CI/CD-ledningar är utrustade för att säkerställa grundlig testning och högsta kodkvalitet för att leverera exceptionella upplevelser. För att säkerställa att kunderna snabbt kan komma igång med sina projekt tillhandahåller Cloud Manager allt som behövs på ett självbetjäningssätt, inklusive möjligheten att skapa molnresurser och miljöer samt få tillgång till era Git-databaser. De här funktionerna ger stöd för företagsutvecklingsmiljöer så att team kan arbeta för att implementera ändringar ofta, snabbt leverera unika digitala upplevelser och snabba upp time-to-value-processen.

Din systemadministratör ansvarar för att konfigurera ditt Cloud Manager-team, som kommer att innehålla personer som skapar dina molnresurser och utvecklare. Mer information om hur du konfigurerar och skalar ditt Enterprise Development Team och hur AEM as a Cloud Service kan stödja din utvecklingsprocess finns i [Enterprise Team Development Setup for AEM as a Cloud Service](/help/implementing/cloud-manager/managing-code/enterprise-team-dev-setup.md).

## Navigera till Cloud Manager översiktssida {#navigate-cloud-manager}

Följ de här stegen för att navigera till Cloud Manager.

1. Gå till Cloud Manager inloggningssida på [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/).

1. Välj programmet på Cloud Manager **Program- och produktsida** för att öppna sidan **Översikt** .

Du kan även navigera till Cloud Manager hemsida för program och produkter från Adobe Experience Cloud genom att följa dessa steg.

1. Navigera till Adobe Experience Cloud på [`https://experience.adobe.com`](https://experience.adobe.com) och logga in med din Adobe ID.

1. Se till att du är i rätt organisation genom att referera till organisationsnamnet som visas längst upp till höger i verktygsfältet.

1. Välj **Experience Manager**.

1. Klicka på **Starta** på **Cloud Manager**-kortet

## Rollbaserade behörigheter i Cloud Manager {#role-based-permissions}

| Behörighet | Beskrivning | Business Owner | Deployment Manager | Program Manager | Developer |
|--- |--- |--- |--- |--- |--- |
| Lägg till program<br>Redigera program | Lägg till ett nytt program<br>Lägg till eller ta bort lösningar eller tillägg | x |  |  |  |
| Skapa miljö | Skapa produktions-+stagnings- och utvecklingsmiljöer | x | x |  |  |
| Uppdateringsmiljö | Uppdatera produktions-+stagnings- och utvecklingsmiljöer | x | x |  |  |
| Ta bort utvecklingsmiljö | Ta bort utvecklingsmiljöer | x | x |  |  |
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
| Skapa/ändra innehållsuppsättningar | Skapa eller ändra en innehållsuppsättning för innehållskopia |  | x |  |  |
| Starta/avbryt innehållskopia | Starta eller avbryta en innehållskopia |  | x |  |  |

>[!NOTE]
>
>En användare kan tilldelas flera roller. Om du till exempel tilldelar en användare både rollen **Affärsägare** och rollen **Distributionshanterare** får användaren summan av dessa behörigheter.

>[!TIP]
>
>Anpassade behörighetsprofiler med konfigurerbara behörigheter är också tillgängliga. Mer information finns i dokumentet [Anpassade behörigheter](/help/implementing/cloud-manager/custom-permissions.md).

## Cloud Manager-program {#cloud-manager-programs}

Cloud Manager är en uppsättning Cloud Manager-miljöer som stöder logiska grupperingar av affärsinitiativ. Dessa grupperingar motsvarar vanligtvis en inköpt Service level agreement (SLA). Ett program kan t.ex. representera de AEM resurserna för att stödja en organisations offentliga webbplats, medan ett annat program representerar en intern DAM.


Titta på den här [videon](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=sv-SE) om du vill veta mer om hur du använder Cloud Manager-program.

En användare kan skapa en **sandlåda** eller ett **Production**-program.

* Ett **produktionsprogram** skapas för att aktivera livatrafik vid rätt tidpunkt i framtiden.
   * Mer information finns i [Introduktion till produktionsprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md).

* Ett **sandlådeprogram** skapas vanligtvis för att träna, köra demonstrationer, aktivera, skapa POC:er eller för dokumentation.
   * Den är inte avsedd att transportera levande trafik och kommer att ha begränsningar som ett produktionsprogram inte kommer att ha.
   * Den innehåller Sites och Assets och levereras automatiskt ifylld med en Git-gren som innehåller exempelkod, en utvecklingsmiljö och en icke-produktionsprocess.
   * Mer information finns i [Introduktion till sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md).

## Cloud Manager Environment {#cloud-manager-environments}

Dina molnmiljöer skapas, öppnas och visas via Cloud Manager. Dessa miljöer kan vara produktions-, staging- eller utvecklingsmiljöer. Olika miljöer har olika syften och kan användas med olika CI/CD-ledningar. Miljöer består av tjänster som:

* [AEM](#author-services)
* [AEM](#publish-services)
* [Dispatcher Services](#dispatcher-services)

>[!TIP]
>
> Se videon [Använda Adobe Cloud Manager-miljöer](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=sv-SE) med en översikt över tillgängliga miljöer.
>
>Läs [Hantera miljöer](/help/implementing/cloud-manager/manage-environments.md) om du vill veta mer om vilka typer av miljöer en användare kan skapa och hur användaren kan skapa en miljö.

### AEM {#author-services}

En AEM är inkluderad i miljöer där webbplatsinnehåll och digitala resurser skapas, hanteras och uppdateras. Vanligtvis har bara interna användare åtkomst till redigeringstjänsten och den bevaras bakom en inloggningsskärm. Utvecklingstjänsten fungerar både som redigerings- och förhandsvisningsmiljö.

### AEM {#publish-services}

En AEM publiceringstjänst ingår i miljöer som är värdar för slutanvändarens upplevelse, som en webbplats. Det här är den tjänst besökarna på webbplatsen kommer att se och interagera med. Publiceringstjänsten är vanligtvis tillgänglig för allmänheten.

### AEM Dispatcher-tjänst {#dispatcher-services}

Avsändaren är en `Apache HTTP Web server`-modul som tillhandahåller ett säkerhets- och prestandalager som placeras framför den AEM publiceringstjänsten.
