---
title: Köra en pipeline
description: På den här sidan beskrivs hur du kör en pipeline för skärmar som ett Cloud Service-projekt i Cloud Manager.
exl-id: 3203cff7-5668-4f50-a2c5-80ae474b439d
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 1%

---

# Köra en pipeline för skärmar as a Cloud Service program i Cloud Manager {#run-pipeline-screens-cloud}

I det här avsnittet beskrivs hur du kör pipeline och distribuerar koden för ditt program i Cloud Manager.

>[!NOTE]
>Se [Konfigurera CI-CD-pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=en) och [Distribuera koden](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=en) om du vill veta hur du kan köra pipeline för ditt program i Cloud Manager.

## Syfte {#objective}

I följande avsnitt beskrivs hur du konfigurerar CI/CD-flödet och distribuerar koden för programmet i Cloud Manager.

## Steg för att köra en pipeline för ditt skärmsprojekt i Cloud Manager {#steps-branch-creation}

1. När miljökonfigurationen är klar visas uppdateringen av åtgärdskortet i Cloud Managers **Översikt** sida.

   ![bild](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. Klicka **Konfigurera pipeline** från **Översikt** sida.

1. Klicka **Nästa** efter att du har valt grenen.

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. Välj alternativ på **Konfigurera pipeline** guide. Klicka **Spara**.

   >[!NOTE]
   >Mer information om alternativen i guiden Konfigurera pipeline finns i [Konfigurera pipeline-inställningar från Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=en) för mer information.

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. När installationen är klar uppdateras åtgärdskortet.

   >[!NOTE]
   >Mer information om distributionsfaserna i Cloud Manager finns i [Distribuera koden](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=en) för mer information.

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. Klicka **Distribuera**.

1. Klicka **Bygge** för att starta byggprocessen.

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. När byggprocessen är klar visas en länk från **Miljö** Kort från Cloud Managers **Översikt** sida.

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## What&#39;s Next {#whats-next}

När du har lärt dig hur du konfigurerar en miljö för ditt program i Cloud Manager är du redo att gå vidare till nästa steg i introduktionsprocessen: [Navigera till Screens Services Provider](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md).
