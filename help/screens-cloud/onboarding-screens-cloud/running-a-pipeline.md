---
title: Köra en pipeline
description: På den här sidan beskrivs hur du kör en pipeline för skärmar som ett Cloud Service-projekt i Cloud Manager.
exl-id: 3203cff7-5668-4f50-a2c5-80ae474b439d
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 1%

---

# Köra en pipeline för skärmar as a Cloud Service program i Cloud Manager {#run-pipeline-screens-cloud}

I det här avsnittet beskrivs hur du kör pipeline och distribuerar koden för ditt program i Cloud Manager.

>[!NOTE]
>Se [Konfigurera CD-CD-pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en) och [Distribuera koden](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en) om du vill veta hur du kan köra pipeline för ditt program i Cloud Manager.

## Syfte {#objective}

I följande avsnitt beskrivs hur du konfigurerar CI/CD-flödet och distribuerar koden för programmet i Cloud Manager.

## Steg för att köra en pipeline för ditt skärmsprojekt i Cloud Manager {#steps-branch-creation}

1. När miljökonfigurationen är klar visas uppdateringen av åtgärdskortet i Cloud Managers **Översikt** sida.

   ![bild](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. Klicka på **Konfigurera pipeline** från **Översikt** sida.

1. Klicka på **Nästa** efter att du har valt grenen.

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. Välj alternativ på **Konfigurera pipeline** guide. Klicka på **Spara**.

   >[!NOTE]
   >Mer information om alternativen i guiden Konfigurera pipeline finns i [Konfigurera pipeline-inställningar från Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en) för mer information.

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. När installationen är klar uppdateras åtgärdskortet enligt figuren nedan. Klicka på Distribuera.

   >[!NOTE]
   >Mer information om distributionsfaserna i Cloud Manager finns i [Distribuera koden](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en) för mer information.

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. Klicka på **Bygge** för att starta byggprocessen.

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. När byggprocessen är klar visas en länk från **Miljö** Kort från Cloud Managers **Översikt** sida.

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## What&#39;s Next {#whats-next}

När du har lärt dig hur du konfigurerar en miljö för ditt program i Cloud Manager är du nu redo att gå vidare till nästa steg i introduktionsprocessen, det vill säga, [Navigera till Screens Services Provider](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md).
