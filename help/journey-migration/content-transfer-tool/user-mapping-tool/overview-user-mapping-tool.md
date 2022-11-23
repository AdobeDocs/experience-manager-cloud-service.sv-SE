---
title: Översikt över verktyget Mappning av användare
description: Översikt över verktyget Mappning av användare
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
source-git-commit: 99af299c3f401ce898366a75563d2b933f120e40
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 7%

---

# Översikt över verktyget Mappning av användare {#overview-user-mapping-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Verktyg för användarmappning"
>abstract="Med verktyget Innehållsöverföring kan du flytta användare och grupper från ditt befintliga AEM till AEM as a Cloud Service. Befintliga användare och grupper måste mappas till sina IMS-ID:n för att undvika dubbletter av användare och grupper i Cloud Servicens författarinstans."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Viktigt att tänka på när du använder verktyget för användarmappning"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Använda verktyget för användarmappning"

## Introduktion {#introduction}

Som en del av övergången till Adobe Experience Manager (AEM) as a Cloud Service måste du flytta användare och grupper från ditt befintliga AEM till AEM as a Cloud Service. Detta görs med verktyget Innehållsöverföring.

En stor förändring i AEM as a Cloud Service är den helt integrerade användningen av Adobe ID:n för åtkomst till redigeringsmiljön.  Detta kräver att [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html) för hantering av användare och användargrupper. Användarprofilsinformationen är centraliserad i Adobe Identity Management System (IMS) som möjliggör enkel inloggning i alla Adobe-molnprogram. Mer information finns i [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management). På grund av den här ändringen måste befintliga användare och grupper mappas till sina IMS-ID:n för att undvika dubbletter av användare och grupper på Cloud Servicens författarinstans.

## Verktyg för användarmappning {#mapping-tool}

Verktyget Innehållsöverföring (utan användarmappning) migrerar alla användare och grupper som är kopplade till innehållet som migreras. Verktyget för användarmappning är en del av verktyget för innehållsöverföring, och dess enda syfte är att modifiera användarna så att de kan identifieras korrekt av IMS, den enkelinloggningsfunktion som används av AEM as a Cloud Service. När ändringarna är klara migrerar verktyget Innehållsöverföring det angivna innehållets användare och grupper som vanligt.

### What’s Next {#whats-next}

När du har lärt dig vad ett verktyg för användarmappning är du nu redo att granska viktiga överväganden och exceptionella fall innan du använder verktyget för användarmappning. Se [Viktigt att tänka på när du ska mappa användare](/help/journey-migration/content-transfer-tool/user-mapping-tool/considerations-user-mapping-tool.md) för mer information.
