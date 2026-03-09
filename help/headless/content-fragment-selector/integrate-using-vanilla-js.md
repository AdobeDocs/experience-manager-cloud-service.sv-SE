---
title: Integrera väljaren för innehållsfragment med Vanilla JS
description: Integrera väljaren för innehållsfragment med olika Adobe-, icke-Adobe- och tredjepartsprogram.
role: Admin, User, Developer
source-git-commit: 592e443928f2c9c18ac281027026132b1c877ce3
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Integrera väljaren för innehållsfragment med Vanilla JS {#integrate-content-fragment-selector-using-vanilla-js}

Du kan integrera alla Adobe- och icke-Adobe-program med Adobe Experience Manager (AEM) som en molndatabas och välja Innehållsfragment inifrån det programmet.

Integreringen görs genom att du importerar Content Fragment Selector-paketet och ansluter till AEM as a Cloud Service med vanilj JavaScript-biblioteket. Redigera en `index.html` eller en lämplig fil i programmet till:

* Definiera autentiseringsinformationen
* Åtkomst till AEM as a Cloud Service-databasen
* Konfigurera visningsegenskaperna för innehållsfragmentväljaren

Du kan utföra autentisering utan att definiera några IMS-egenskaper om du:

* integrerar ett Adobe-program på [Unified Shell](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell)
* har redan en IMS-token genererad för autentisering
