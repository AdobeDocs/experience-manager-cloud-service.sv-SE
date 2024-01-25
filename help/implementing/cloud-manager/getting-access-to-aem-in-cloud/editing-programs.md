---
title: Hantera och redigera program
description: Lär dig hur du redigerar produktions- och sandlådeprogram för att justera deras alternativ efter att du har skapat dem.
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: 2dfae31e32d375c82c4f690624e48f7f09feb4df
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---


# Hantera och redigera program {#editing-programs}

The **Mina program** sidan innehåller en översikt över alla program som du har tillgång till. När du väljer ett enskilt program visas **Programöversikt** på sidan hittar du snabbt information om programmet.

Från **Programöversikt** kan användare med nödvändig behörighet redigera [produktionsprogram som har skapats i din organisation](creating-production-programs.md) och [sandlådeprogram som har skapats i din organisation.](creating-sandbox-programs.md) Genom att redigera ett program kan du

* Lägg till Sites-lösning i ett befintligt program med Assets och omvänt.
* Ta bort platser eller resurser från ett befintligt program med både platser och resurser.
* Lägg till ett andra, oanvänt lösningsberättigande, antingen till ett befintligt program eller som ett nytt program.
* Ta bort sandlådeprogram.

## Behörigheter {#permissions}

Du måste vara medlem i **Företagsägare** roll för att redigera program eller ta bort sandlådeprogram samt för att få tillgång till License Dashboard.

## Mina program {#my-programs}

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation.

1. The **Mina program** visas en lista med alla program som du har åtkomst till som paneler.

![Sidan Mina program](/help/implementing/cloud-manager/assets/my-programs.png)

### Call-to-Action {#cta}

Överst på sidan finns en uppmaning till åtgärd som är relevant för organisationens status. Om du till exempel har konfigurerat dina program kan statistik över dina aktiviteter under de senaste 90 dagarna visa, inklusive:

* Antal [distributioner](/help/implementing/cloud-manager/deploy-code.md)
* Antal [problem med kodkvalitet](/help/implementing/cloud-manager/code-quality-testing.md) identifierad
* Antal byggen

Eller om du just har börjat konfigurera organisationen kan det finnas tips om nästa steg eller dokumentationsresurser.

### Fliken Program {#programs-tab}

The **Program** I visas kort som representerar de program du har åtkomst till. Tryck eller klicka på ett kort för att komma åt **Programöversikt** sidan med programmet för att få information om programmet.

Använd sorteringsalternativen för att bättre hitta det program du behöver.

![Sorteringsalternativ](/help/implementing/cloud-manager/assets/my-programs-sorting.png)

* Sortera efter
   * Skapad den (standard)
   * Programnamn
   * Status
* Stigande (standard) / Fallande
* Stödrastervisning (standard)
* Listvy

### Fliken Licens {#license-tab}

The **Licens** -fliken ger dig snabb åtkomst till [License Dashboard.](/help/implementing/cloud-manager/license-dashboard.md)

## Programöversikt {#program-overview}

När du har valt ett program i **[Mina program](#my-programs)** öppnar Cloud Manager **Programöversikt** sida för det valda programmet.

![Sidan Programöversikt](/help/implementing/cloud-manager/assets/program-overview.png)

Tryck eller klicka på programnamnet längst upp till vänster på sidan för att snabbt växla till ett annat program eller tillbaka till **[Mina program](#my-programs)** sida. Du kan också [redigera det valda programmet](#editing) eller [lägga till ett program.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

![Programväljare](/help/implementing/cloud-manager/assets/program-switcher.png)

Uppmaningen överst ger dig användbar information beroende på programmets status. För ett nytt program kan du se nästa steg som erbjuds samt en påminnelse om ett publiceringsdatum, [anges när programmet skapas.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)

![Call-to-action för ett nytt program](/help/implementing/cloud-manager/assets/info-banner-new-program.png)

För ett live-program, status för den senaste distributionen med länkar för information och start av en ny distribution.

![Call-to-action](/help/implementing/cloud-manager/assets/info-banner.png)

**Miljö** och **Pipelines** kort ger en snabb översikt över båda delarna i det valda programmet.

![Kort](/help/implementing/cloud-manager/assets/environments-pipelines.png)

The **Prestanda** kortet ger en översikt över **[CDN Dashboard.](/help/implementing/cloud-manager/cdn-performance.md)**

![Prestandakort](/help/implementing/cloud-manager/assets/cdn-performance-dashboard.png)

## Redigera ett program {#editing}

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation.

1. På **[Mina program](#my-programs)** klickar du på det program du vill redigera för att visa information om det.

1. Klicka på programnamnet längst upp till vänster på sidan och välj **Redigera program**.

   ![Redigera programalternativ](assets/edit-program-overview.png)

1. The **Redigera program** sidan öppnas för **Allmänt** -fliken.

   ![fliken Allmänt](assets/edit-program-prod1.png)

1. De alternativ som är tillgängliga för redigering av programmet är desamma som när du skapar programmet.
   * Se dokumenten [Skapa produktionsprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) och [Skapa sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) om du vill ha information om de enskilda alternativen.
   * [Ytterligare alternativ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#options) kan finnas för ditt produktionsprogram beroende på organisationens rättigheter.

1. Klicka **Uppdatera** för att spara ändringarna i programmet.

Ändringarna sparas.

>[!NOTE]
>
>Varje gång ett program redigeras, som att lägga till eller ta bort en lösning eller ett tillägg, börjar ändringarna gälla efter nästa distribution.

## Tar bort sandlådeprogram {#delete-sandbox-program}

Om du tar bort ett sandlådeprogram tas alla miljöer och rörledningar som är kopplade till det bort.

>[!TIP]
>
>Användare med **Företagsägare** eller **Distributionshanteraren** roller kan också ta bort sin produktions- och scenmiljö i stället för hela sandlådeprogrammet.

Så här tar du bort ett sandlådeprogram.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation.

1. På **[Mina program](#my-programs)** klickar du på det program du vill redigera för att visa information om det.

1. Klicka på programnamnet längst upp till vänster på sidan och välj **Ta bort program**.

   ![Ta bort programalternativ](assets/delete-sandbox1.png)

Du kan också klicka på ellipsknappen på programmets kort på översiktssidan för Cloud Manager och välja **Ta bort program**.

![Ta bort sandlåda från programkort](assets/delete-sandbox2.png)

>[!NOTE]
>
>Endast sandlådeprogram kan tas bort. Det går inte att ta bort produktionsprogram.
