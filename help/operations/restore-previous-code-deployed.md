---
title: Återställ tidigare distribuerad Source-kod
description: Lär dig hur du återställer en miljö till den senast slutförda bygg&emarginalen; ingen pipeline-körning krävs.
feature: Operations
role: Admin
badge: label="Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
exl-id: 8f804f55-a66d-47ad-a48d-61b861cef4f7
source-git-commit: 2fa7005eec0a53f632e1b1cb2f5cc5910bbf21f8
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# Återställ tidigare källkod som distribuerats i AEM as a Cloud Service {#restore-previous-code-deployed}

>[!NOTE]
>
>Funktionen som beskrivs i den här artikeln är endast tillgänglig via betaprogrammet. Information om hur du registrerar dig för betaversionen finns i [Enklicksåterställning för pipeline-distributioner](/help/implementing/cloud-manager/release-notes/current.md##one-click-rollback).

Använd **Återställ tidigare kod som distribuerats** för att omedelbart återställa en miljö till den senaste lyckade versionen - ingen pipeline-körning krävs.

Du öppnar bara den markerade miljöns meny ![Mer ikon eller ikonen för ellipsmenyn](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) och väljer **Återställ** > **Föregående kod som distribuerats** för att återställa den senast distribuerade källkoden på några sekunder.

>[!TIP]
>
>Du kan visa den aktiva källkodsversionen som används i informationsvyn i miljön, på fliken **Allmänt** . Se [Visa information om en miljö](/help/implementing/cloud-manager/manage-environments.md#viewing-environment).
>
>![Source-kodversionen används](/help/operations/assets/environments-view-details-sourcecodeversion.png)

**Återställ tidigare kod som distribuerats** blir bara tillgänglig när följande villkor uppfylls:

* Endast en återställning tillåts per lyckad pipeline-körning. Om du vill återställa igen kan du slutföra en annan lyckad pipeline-körning.
* Du har **behörighet att återställa miljön**. Mer information om hur du hanterar behörigheter finns i [Anpassade behörigheter](/help/implementing/cloud-manager/custom-permissions.md).
* Din organisation är registrerad i betaprogrammet och funktionsflaggan är aktiverad.
* Programmet körs på AEM as a Cloud Service.
* Den senaste pipeline för den miljön slutfördes och kördes för **mindre än 30 dagar** sedan.
* Miljöstatusen är *Körs* och ingen pipeline pågår.
* **Du kan återställa tidigare kod som distribuerats** i en `Development` -miljö, `Stage`-miljö eller en `Specialized Testing Environment` -miljö.

Om en kontroll misslyckas öppnar Cloud Manager följande dialogruta med en eller flera villkor som inte uppfylls och **Bekräfta** inaktiveras, vilket förhindrar återställning.

![Dialogrutan Återställ tidigare kod för distribuerat fel](/help/operations/assets/restore-previous-code-deployment-not-allowed.png).

Om du bara vill återställa data, som har gått förlorade, skadats eller av misstag tagits bort, till det ursprungliga villkoret, kan du använda [Återställ innehåll i AEM as a Cloud Service](/help/operations/restore.md). Återställningsprocessen påverkar bara innehållet och källkoden och versionen av AEM ändras inte.

**Så här återställer du tidigare distribuerad kod:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Klicka på det program som du vill starta en återställning för.

1. Visa alla miljöer för programmet genom att göra något av följande:

   * På den vänstra menyn, under **Tjänster**, klickar du på ![Dataikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Miljö**.

     ![Fliken Miljö](assets/environments-1.png)

   * Klicka på **Översikt** under **Program** på den vänstra menyn och klicka sedan på **Arbetsflödesikonen** ![Visa alla](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) på **miljökortet** .

     ![Visa alla alternativ](assets/environments-2.png)

     >[!NOTE]
     >
     >Kortet **Environment** innehåller endast tre miljöer. Klicka på **Visa alla** på kortet för att visa *alla* miljöer för programmet.

1. I miljötabellen, till höger om en miljö vars källkod du vill återställa, klickar du på ikonen ![Mer eller Ellips ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) och sedan på **Återställ** > **Tidigare kod som distribuerats**.

   ![Återställ tidigare alternativ för koddistribution från ellipsmenyn](/help/operations/assets/restore-previous-code-deployed-menu.png)

1. Granska den distribuerade versionen och versionen som du vill återställa i dialogrutan **Återställ tidigare kod som distribuerats** och klicka sedan på **Bekräfta**.

   ![Återställ föregående dialogruta för koddistribution](/help/operations/assets/restore-previous-code-deployed-dialogbox.png)

1. Cloud Manager återställer miljön till den tidigare versionen, bibehåller innehåll och konfiguration och markerar miljön **Återställning** på sidan Miljöer tills distributionen är klar.

   ![Återställer aktiveringen](/help/operations/assets/restore-previous-code-deployed-restoring.png)
