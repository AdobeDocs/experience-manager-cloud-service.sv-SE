---
title: Köra en pipeline
description: På den här sidan beskrivs hur du kör en pipeline för Screens som ett Cloud Service-projekt i Cloud Manager.
exl-id: 3203cff7-5668-4f50-a2c5-80ae474b439d
feature: Screens Deployments
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 2%

---

# Köra en pipeline för Screens as a Cloud Service Program i Cloud Manager {#run-pipeline-screens-cloud}

I det här avsnittet beskrivs hur du kör pipeline och distribuerar koden för ditt program i Cloud Manager.

>[!NOTE]
>Se [Konfigurera CI-CD-pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=sv-SE) och [Distribuera din kod](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=sv-SE) för att lära dig hur du kan köra pipeline för ditt program i Cloud Manager.

## Syfte {#objective}

I följande avsnitt beskrivs hur du konfigurerar CI/CD-flödet och distribuerar koden för programmet i Cloud Manager.

## Steg för att köra en pipeline för ditt Screens-projekt i Cloud Manager {#steps-branch-creation}

1. När miljökonfigurationen är klar visas uppdateringen av åtgärdskortet på Cloud Manager **Översikt** .

   ![bild](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. Klicka på **Konfigurera pipeline** på sidan **Översikt**.

1. Klicka på **Nästa** när du har valt grenen.

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. Välj dina alternativ i guiden **Konfigurera pipeline**. Klicka på **Spara**.

   >[!NOTE]
   >Mer information om alternativen i guiden Konfigurera pipeline finns i [Konfigurera förloppsinställningarna från Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=sv-SE).

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. När installationen är klar uppdateras åtgärdskortet.

   >[!NOTE]
   >Mer information om faserna i distributionen i Cloud Manager finns i [Distribuera din kod](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=sv-SE).

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. Klicka på **Distribuera**.

1. Klicka på **Build** för att starta byggprocessen.

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. När byggprocessen är klar kan du se en författarlänk från **miljökortet** från Cloud Manager **Översikt** .

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## What&#39;s Next {#whats-next}

När du har lärt dig hur du konfigurerar en miljö för ditt program i Cloud Manager är du redo att gå vidare till nästa steg i introduktionsprocessen: [Navigerar till Screens tjänsteleverantör](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md).
