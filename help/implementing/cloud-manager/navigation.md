---
title: Navigera i användargränssnittet i Cloud Manager
description: Läs om hur Cloud Manager användargränssnitt är organiserat och hur du navigerar för att hantera program och miljöer.
exl-id: 3f3d7631-2bc9-440b-9888-50f6529bcd42
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: a5179851af8ec88e23d79a74265b10cbce2d50f1
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 0%

---

# Navigera i gränssnittet för molnhanteraren {#navigation}

Läs om hur Cloud Manager användargränssnitt är organiserat och hur du navigerar för att hantera program och miljöer.

Användargränssnittet för molnhantering består huvudsakligen av två grafiska gränssnitt:

* [Konsolen Mina program](#my-programs) där du kan visa och hantera alla program.
* [Fönstret Programöversikt](#program-overview) där du kan se information om och hantera ett enskilt program.

>[!TIP]
>
>Se även [introduktionsdokumentationsresan](/help/journey-onboarding/overview.md) för en fullständig översikt över hur du kommer igång med AEM as a Cloud Service med Cloud Manager.

## My Programs Console {#my-programs}

När du loggar in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och väljer lämplig organisation, kommer du till konsolen **Mina program**.

![Konsolen Mina program](assets/my-programs-console.png)

Konsolen Mina program ger en översikt över alla program som du har tillgång till i den valda organisationen. Den består av flera delar.

1. [Verktygsfält](#toolbars-my-programs-toolbars) för organisationsval, aviseringar och kontoinställningar
1. [Statistik och uppmaning](#statistics) för en översikt över din senaste aktivitet
1. [Program och licens](#programs-license) för att förstå din aktuella licensstatus och hantera dina program
1. [Snabblänkar](#quick-links) för enkel åtkomst till relaterade resurser

>[!TIP]
>
>Mer information om program finns i dokumentet [Program och programtyper](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

### Verktygsfält {#my-programs-toolbars}

Det finns två verktygsfält ovanpå varandra.

#### Cloud Manager Header {#cloud-manager-header}

Det första är Cloud Manager-rubriken som är beständig när du navigerar i Cloud Manager. Det är en ankarpunkt som ger dig tillgång till inställningar och information som gäller för alla Cloud Manager-program.

![Experience Cloud-huvudet](assets/experience-cloud-header.png)

1. Med Cloud Manager-knappen kommer du tillbaka till My Programs-konsolen i Cloud Manager oavsett var du befinner dig i Cloud Manager.
1. Tryck eller klicka på knappen Feedback för att ge Adobe feedback om Cloud Manager.
1. Organisationsväljaren visar den organisation du är inloggad på (i det här exemplet Foundation Internal). Tryck eller klicka för att växla till en annan organisation om din Adobe ID är kopplad till flera.
1. Om du trycker eller klickar på lösningens väljare kan du snabbt gå över till andra Experience Cloud-lösningar.
1. Hjälpikonen ger snabb åtkomst till utbildningsresurser och supportresurser.
1. Aviseringsikonen är märkt med antalet för närvarande tilldelade ofullständiga [meddelanden.](/help/implementing/cloud-manager/notifications.md)
1. Välj den ikon som representerar användaren för att få åtkomst till dina användarinställningar. Om du inte har konfigurerat någon användarbild tilldelas ikonen slumpmässigt.

#### Verktygsfältet Program {#program-toolbar}

Verktygsfältet Program innehåller länkar för att växla mellan Cloud Manager-program och åtgärder som passar just det sammanhanget.

![Verktygsfältet Program](assets/program-toolbar.png)

1. Programväljaren öppnas i en listruta där du snabbt kan välja andra program eller vidta sammanhangsberoende åtgärder som att skapa ett nytt program
1. Länken Komma igång ger dig tillgång till [dokumentationsresan för introduktion](/help/journey-onboarding/overview.md) så att du kan komma igång med Cloud Manager.
1. Åtgärdsknappen innehåller sammanhangsberoende åtgärder som att skapa ett nytt program.

### Statistik {#statistics}

Statistikavsnittet innehåller sammanställda data för din organisation, t.ex. om du har konfigurerat dina program kan statistik över dina aktiviteter under de senaste 90 dagarna visa, inklusive:

* Antal [distributioner](/help/implementing/cloud-manager/deploy-code.md)
* Antal [kodkvalitetsproblem](/help/implementing/cloud-manager/code-quality-testing.md) som identifierats
* Antal byggen

Eller om du just har börjat konfigurera organisationen kan det finnas tips om nästa steg eller dokumentationsresurser.

### Program och licenser {#programs-license}

Huvudinnehållet i My Programs-konsolen är listan över program och licensens status.

#### Fliken Program {#programs}

På fliken **Program** visas kort som representerar de program du har åtkomst till. Tryck eller klicka på ett kort för att komma åt sidan **Programöversikt** i programmet för mer information om programmet.

Använd sorteringsalternativen för att bättre hitta det program du behöver.

![Sorteringsalternativ](/help/implementing/cloud-manager/assets/my-programs-sorting.png)

* Sortera efter
   * Skapad den (standard)
   * Programnamn
   * Status
* Stigande (standard) / Fallande
* Stödrastervisning (standard)
* Listvy

Varje program representeras av ett kort (eller en rad i en tabell) som ger en översikt över programmet och snabblänkar för att vidta åtgärder.

![Programkort](assets/program-card.png)

* Programavbildning (om den är konfigurerad)
* Programnamn
* Tjänsttyp: **Experience Manager Cloud** för AEM som ett *-Cloud Service-program eller [**Experience Manager** för AMS-program](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/introduction)
* [Programtyp](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md): Sandbox eller produktion
* Status
* Konfigurerade lösningar
* Skapad den

Beroende på vilka alternativ du väljer när du skapar programmet kan ett produktionsprogram märkas för att visa ytterligare funktioner.

* [HIPAA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

  ![HIPAA-märke](assets/hipaa.png)

* [Skydd mot WAF-DDOS](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

  ![WAF-DDOS, märke](assets/waf-ddos-protection.png)

* [99,99 % SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)

  ![99.99% SLA-märke](assets/9999-sla.png)

Informationsikonen ger dig även snabb åtkomst till ytterligare information om programmet (användbart i listvyn).

![Information](assets/information-list-view.png)

Ellipsikonen ger dig tillgång till ytterligare åtgärder som du kan vidta i programmet.

![Ellipsknappen för program](assets/program-ellipsis.png)

* Navigera till en viss [miljö](/help/implementing/cloud-manager/manage-environments.md) i programmet
* Öppna [programöversikt](#program-overview)
* [Redigera programmet](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#editing)
* [Ta bort ett sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#delete-sandbox-program)

>[!TIP]
>
>Mer information om program samt hur du skapar och hanterar program finns i följande dokument.
>
>* [Program och programtyper](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)
>* [Skapar sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)
>* [Skapar produktionsprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

#### Fliken Licens {#license-tab}

Fliken **Licens** ger dig snabb åtkomst till [License Dashboard.](/help/implementing/cloud-manager/license-dashboard.md)

### Snabblänkar {#quick-links}

I avsnittet med snabblänkar får du tillgång till resurser som du använder ofta.

## Programöversiktsfönster {#program-overview}

När du har valt ett program i konsolen Mina program visas programöversikten.

![Programöversikt](assets/program-overview.png)

Programöversikten ger dig tillgång till alla detaljer i ett Cloud Manager-program. Precis som My Programs-konsolen består den av flera delar.

1. [Verktygsfält](#program-overview-toolbar) om du snabbt vill gå tillbaka till Mina program-konsolen och navigera i programmet
1. [Tabbar](#program-tabs) för att växla mellan olika aspekter av programmet
1. En [uppmaning till åtgärd](#cta) baserad på de senaste åtgärderna i programmet
1. En [översikt över programmets miljöer](#environments)
1. En [översikt över programmets pipelines](#pipelines)
1. En [översikt över programmets prestanda](#performance)
1. Länkar till [användbara resurser](#useful-resources)

### Verktygsfält {#program-overview-toolbar}

Verktygsfälten för programöversikten liknar de i [Min programkonsol.](#my-programs-toolbars) Endast skillnaderna illustreras här.

#### Cloud Manager Header {#cloud-manager-header-2}

Cloud Manager header har en hamburger-meny som automatiskt öppnas och visar de navigerbara flikarna i programöversikten.

![Cloud Manager hamburger-meny](assets/cloud-manager-hamburger.png)

Tryck eller klicka på menyikonen för hamburgaren för att dölja flikarna.

#### Verktygsfältet Program {#program-toolbar-2}

Verktygsfältet för program ger dig fortfarande möjlighet att snabbt växla till andra program, men ger även tillgång till sammanhangsberoende åtgärder som att lägga till och redigera programmet.

![Verktygsfältet Program](assets/cloud-manager-program-toolbar.png)

Verktygsfältet innehåller dessutom alltid den flik som du är på om du har valt att dölja flikarna med hjälp av hamburgmenyn.

### Programflikar {#program-tabs}

Varje program har många alternativ och data kopplade till sig. Dessa data samlas in på flikar för att underlätta navigeringen i programmet. Flikarna ger dig tillgång till:

* Översikt - Programöversikt enligt beskrivningen i det aktuella dokumentet
* [Aktivitet](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity) - Historiken för programmets pipeline-körningar
* [Pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines) - Alla pipelines har konfigurerats för programmet
* [Databaser](/help/implementing/cloud-manager/managing-code/managing-repositories.md) - Alla databaser har konfigurerats för programmet
* [Rapporter](/help/implementing/cloud-manager/sla-reporting.md) - Mätvärden som SLA-data
* [Miljö](/help/implementing/cloud-manager/manage-environments.md) - Alla miljöer konfigurerade för programmet
* [Innehållsuppsättningar](/help/implementing/developing/tools/content-copy.md) - Innehållsuppsättningar som skapats för kopieringsändamål
* [Kopiera innehållsaktivitet](/help/implementing/developing/tools/content-copy.md) - aktiviteter för innehållskopiering
* Utbildningsvägar - ytterligare utbildningsresurser om Cloud Manager

Som standard visas fliken **Översikt** när du öppnar ett program. Den aktuella fliken markeras. Välj en annan flik om du vill visa information om den.

Använd hamburger-menyn i [Cloud Manager-huvudet](#cloud-manager-header-2) för att dölja flikarna.

### Call-to-Action {#cta}

I avsnittet om uppmaning att ringa in får du användbar information beroende på programmets status. För ett nytt program kan du se nästa steg som erbjuds och en påminnelse om ett publiceringsdatum, [som anges när programmet skapas.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)

![Call-to-action för ett nytt program](/help/implementing/cloud-manager/assets/info-banner-new-program.png)

För ett live-program, status för den senaste distributionen med länkar för information och start av en ny distribution.

![Call-to-action](/help/implementing/cloud-manager/assets/info-banner.png)

### Miljökort {#environments}

Kortet **Environment** ger dig en översikt över dina miljöer samt länkar till snabba åtgärder.

Kortet **Environment** innehåller endast tre miljöer. Klicka på **Visa alla** om du vill visa alla miljöer i programmet.

Mer information om hur du hanterar dina miljöer finns i dokumentet [Hantera miljöer](/help/implementing/cloud-manager/manage-environments.md).

### Förloppskort {#pipelines}

Kortet **Pipelines** ger dig en översikt över dina pipelines samt länkar för snabbåtgärder.

Kortet **Pipelines** innehåller endast tre pipelines. Klicka på **Visa alla** om du vill visa alla rörledningar för programmet.

Se dokumentet [Hantera pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) för mer information om hur du hanterar dina pipelines.

### Prestandakort {#performance}

Kortet **Performance** ger en översikt över **[CDN-instrumentpanelen.](/help/implementing/cloud-manager/cdn-performance.md)**

![Prestandakort](/help/implementing/cloud-manager/assets/cdn-performance-dashboard.png)

### Användbara resurser {#useful-resources}

Avsnittet **Användbara resurser** innehåller länkar till ytterligare utbildningsresurser för Cloud Manager.
