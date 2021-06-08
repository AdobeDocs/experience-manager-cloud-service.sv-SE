---
title: Köra en pipeline
description: På den här sidan beskrivs hur du kör en pipeline för skärmar som ett Cloud Service-projekt i Cloud Manager.
hide: true
hidefromtoc: true
index: false
source-git-commit: 371cfaeb0e526197fdf98dea65ed5bc2ca0481a2
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 1%

---


# Köra en pipeline för skärmar som ett Cloud Service-program i Cloud Manager {#run-pipeline-screens-cloud}

I det här avsnittet beskrivs hur du kör pipeline och distribuerar koden för ditt program i Cloud Manager.

>[!NOTE]
>Läs [Konfigurera din CD-CD-pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en) och [Distribuera koden](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en) om du vill veta hur du kan köra pipeline för ditt program i Cloud Manager.

## Syfte {#objective}

I följande avsnitt beskrivs hur du konfigurerar CI/CD-flödet och distribuerar koden för programmet i Cloud Manager.

## Steg för att köra en pipeline för ditt skärmsprojekt i Cloud Manager {#steps-branch-creation}

1. När miljökonfigurationen är klar visas uppdateringen av anropskortet i Cloud Managers **översiktssida**.

   ![bild](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. Klicka på **Konfigurera pipeline** på sidan **Översikt**.

1. Klicka på **Nästa** när du har valt grenen.

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. Välj dina alternativ i guiden **Konfigurera pipeline**. Klicka på **Spara**.

   >[!NOTE]
   >Mer information om alternativen i guiden Konfigurera pipeline finns i [Konfigurera förloppsinställningarna från Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en) för mer information.

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. När installationen är klar uppdateras åtgärdskortet enligt figuren nedan. Klicka på Distribuera.

   >[!NOTE]
   >Mer information om distributionsfaserna i Cloud Manager finns i [Distribuera koden](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en).

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. Klicka på **Build** för att starta byggprocessen.

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. När byggprocessen är klar ser du en länk från **Environmental** Card från sidan **Översikt** i Cloud Manager.

   ![bild](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## What&#39;s Next {#whats-next}

När du har lärt dig hur du kör pipeline för ditt program i Cloud Manager är du nu redo att gå vidare till nästa steg. Nästa steg är att konfigurera och konfigurera skärmsprojekt.