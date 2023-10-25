---
title: Redigeringsprogram
description: Lär dig hur du redigerar produktions- och sandlådeprogram för att justera deras alternativ efter att du har skapat dem.
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: ecb168e9261b3e3ed89e4cbe430b3da9f777a795
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Redigeringsprogram {#editing-programs}

Användare med nödvändig behörighet kan redigera [produktionsprogram som har skapats i din organisation](creating-production-programs.md) och [sandlådeprogram som har skapats i din organisation.](creating-sandbox-programs.md) Genom att redigera ett program kan du

* Lägg till Sites-lösning i ett befintligt program med Assets och omvänt.
* Ta bort platser eller resurser från ett befintligt program med både platser och resurser.
* Lägg till ett andra, oanvänt lösningsberättigande, antingen till ett befintligt program eller som ett nytt program.
* Ta bort sandlådeprogram.

## Behörigheter {#permissions}

Du måste vara medlem i **Företagsägare** roll för att redigera program eller ta bort sandlådeprogram.

## Redigera ett program {#editing}

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation.

1. Klicka på det program som du vill redigera för att visa information om det.

1. Klicka på programnamnet längst upp till vänster på sidan och välj **Redigera program**.

   ![Redigera programalternativ](assets/edit-program-overview.png)

1. The **Redigera program** sidan öppnas. På **Allmänt** redigerar du programnamnet och beskrivningen.

   * Minst en lösning måste väljas för ett program.

   ![fliken Allmänt](assets/edit-program-prod1.png)

1. På **Lösningar och tillägg** ändrar du lösningarna för programmet.

   ![Välj lösningar](assets/edit-prg.png)

1. Klicka på nedtryckningen före lösningsnamnet för att visa valfria tillägg, som att välja **Handel** tilläggsalternativ under **Webbplatser**.

   ![Redigera tillägg](assets/edit-program-add-on.png)

1. På **Go live settings** ändrar du det planerade publiceringsdatumet för programmet.

   ![Redigera inställningar för publicering](assets/edit-program-go-live.png)

   * Detta datum är endast avsett som information. Den aktiverar Go Live-widgeten på programöversiktssidan. Det innehåller i sin tur länkar till Adobe Experience Manager (AEM) as a Cloud Service best practice-dokumentation för att passa in i kundresan, vilket leder till en lyckad Go Live-upplevelse.
   * Den här fliken är inte tillgänglig för sandlådeprogram.

1. Om de begärda berättigandena finns tillgängliga för programmet, **Säkerhet** visas var du kan ändra säkerhetsalternativen för programmet.

   ![Redigera säkerhetsinställningar](assets/edit-program-security.png)

   * HIPAA kan inte aktiveras eller inaktiveras efter [skapa program.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
      * [Läs mer](https://www.adobe.com/go/hipaa-ready) om implementering av Adobe HIPAA-klar lösning.
   * När det är aktiverat kan WAF-DDOS-skyddet sedan konfigureras genom att konfigurera en [icke-produktionsrörledning.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

   {{waf-limited-release}}

1. Klicka **Uppdatera** för att spara ändringarna i programmet.

Varje gång ett program redigeras, som att lägga till eller ta bort en lösning eller ett tillägg, börjar ändringarna gälla efter nästa distribution.

## Tar bort sandlådeprogram {#delete-sandbox-program}

Om du tar bort ett sandlådeprogram tas alla miljöer och rörledningar som är kopplade till det bort.

>[!TIP]
>
>Användare med **Företagsägare** eller **Distributionshanteraren** roller kan också ta bort sin produktions- och scenmiljö i stället för hela sandlådeprogrammet.

Så här tar du bort ett sandlådeprogram.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation.

1. Klicka på det program som du vill redigera för att visa information om det.

1. Klicka på programnamnet uppe till vänster på sidan och välj **Ta bort program**.

   ![Ta bort programalternativ](assets/delete-sandbox1.png)

Du kan också klicka på ellipsknappen på programmets kort på översiktssidan för Cloud Manager och välja **Ta bort program**.

![Ta bort sandlåda från programkort](assets/delete-sandbox2.png)

>[!NOTE]
>
>Endast sandlådeprogram kan tas bort. Det går inte att ta bort produktionsprogram.
