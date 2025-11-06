---
title: Hur felsöker man installations- och konfigurationsproblem i AEM Forms as a Cloud Service?
description: Felsökning av installation och konfiguration av AEM Forms as a Cloud Service-miljö.
contentOwner: khsingh
feature: Adaptive Forms
role: User
exl-id: 249ec8f2-4176-428a-bfcf-80b381ec7263
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Konfiguration {#installation-and-configuration}

Följande problem kan uppstå när du konfigurerar en Cloud Service-miljö:

## Forms-alternativet är inte tillgängligt

Alternativet **[!UICONTROL Forms]** är inte tillgängligt på sidan **[!UICONTROL Navigation]**.

![Forms-alternativet är inte tillgängligt](assets/installation-configuration-forms-option-unavailable-troubleshooting.png)

Aktivera alternativet **[!UICONTROL Forms]**:

1. Logga in på [Cloud Manager](https://experience.adobe.com/)
1. Leta upp programmet och klicka på ikonen ![Forms är inte tillgänglig](assets/Smock_Edit_18_N.svg) . Den öppnar sidan Redigera program för ditt program.
1. Öppna fliken **[!UICONTROL Solutions & Add-ons]**.
1. Välj alternativet **[!UICONTROL Forms]** och klicka på **[!UICONTROL Save]**.

   ![Välj alternativet Forms](assets/installation-configuration-select-forms-option.png)

1. [Skapa](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#how-to-use) och [kör](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) både produktions- och icke-produktionspipelines.

När pipelinen har skapats och distribuerats är alternativet **[!UICONTROL Forms]** på sidan **[!UICONTROL Navigation]**.

<!--  
## Environment creation fails {#environment-creation-fails}

Users are unable to create an [!DNL AEM Forms] as a Cloud Service environment. The environment creation fails after running for some time.

A missing profile can lead to environment creation failure. Check that the profile exists in Admin Console. If the profile does not exist, perform the following steps to create the profile:

1. Log in to [Admin Console](https://adminconsole.adobe.com/). Use Adobe ID of administrator provisioned to use Automated Forms Conversion Service to login. Do not any other ID or Federated ID to login.
1. Click the **[!UICONTROL Automated Forms Conversion Service]** option.
1. Click **[!UICONTROL New Profile]** in the Products tab.
1. Specify Name, Display Name, and Description for the profile. Click **[!UICONTROL Done]**. A profile is created.

If the profile exists and issues still persist, contact Adobe Support. -->

## Det gick inte att skapa pipeline {#build-pipeline-fails}

Användarna kan inte köra byggpipeline. Pipelinen fungerar inte när den har körts ett tag.

Du löser problemet genom att öppna Cloud Manager, välja alternativet **[!UICONTROL Update]** för din miljö och köra pipeline.


## Paketen är inte i aktivt läge {#bundles-inactive-state}

Så här löser du problemet:

1. Starta AEM och vänta tills alla paket är klara.
1. Stoppa AEM (Ctrl + C).
1. Placera Forms `.far`-filen i installationsmappen.
1. Starta om AEM-servern.