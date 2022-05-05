---
title: Provisioneringsprocess - översikt
description: Provisioneringsprocess - översikt
source-git-commit: ffeda76f9c661117ddba50588ebea01d151ee8c3
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 7%

---


# AEM as a Cloud Service: Onboarding och Access

På den här sidan visas självhjälpsresurser om provisioneringsprocessen för Experience Manager as a Cloud Service.

## AEM as a Cloud Service Provisioning Process Overview

Detta avsnitt behandlar de viktigaste artiklarna med fokus på:

* Åtkomst AEM as a Cloud Service
* Adobe Experience Manager as a Cloud Service introduktions- och provisioneringsprocess
* Hjälp och resurser


### Åtkomst AEM as a Cloud Service

När automatisk etablering är klar:

* Beviljade åtkomsträttigheter - Adobe skapar en organisation i Adobe Identity Management System (IMS)
* Utsedd administratör har som standard administratörsbehörighet
* Administratören kan lägga till användare och roller för ytterligare teammedlemmar via Admin Console
* Granska rollbaserade behörigheter för användare för att fastställa behörighetstilldelningar i Cloud Manager

![processurview.jpg](assets/processOverview.jpg)


Mer information finns på [Anordnande av nyanställda på Experience Manager as a Cloud Service på Experience League](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html?lang=en)

### Resurser och länkar

* [IMS-stöd för AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en)
* [Rollbaserade behörigheter i Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/role-based-permissions.html?lang=en#what-is-required)
* [Få tillgång till Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=en#getting-access)


## Adobe Experience Manager as a Cloud Service introduktionsprocess

### 1. Automatisk etablering av utlösare för inköpsorder.

### 2. Anlita organisationer på Adobe Admin Console:

![processurview2.jpg](assets/processOverview2.jpg)

* Systemadministratör:
   * Tillhandahålla AEM program och miljöer.
   * Navigera till Admin Console för administrativa uppgifter.
   * Gör anspråk på en domän för att bekräfta ägarskap till respektive domän
   * Ställer in användarkataloger.
   * IDP-konfiguration.
* AEM-administratör:
   * Hantera lokala grupper, behörigheter och behörigheter.

### 3. Anställ användare och hantera åtkomst i Admin Console:

![processurview3.jpg](assets/processOverview3.jpg)

Tre metoder att introducera användare, beroende på storlek och inställning:
* Skapa användare i Admin Console manuellt
* Överför CSV-fil
* Synkronisera användare från Enterprise Active Directory

### 4. Admin konfigurerar organisationen och ger användare och grupper åtkomst till miljöer

## Hjälp och resurser

* [Inloggning för första gången - Cloud Service](/help/journey-onboarding/sysadmin/learning-path-aem-users.md)
* [Konfigurera åtkomst till AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html?lang=en#accessing)
