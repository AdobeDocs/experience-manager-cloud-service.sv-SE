---
title: Översikt över verktyget Användarmappning (äldre)
description: Översikt över verktyget Användarmappning (äldre)
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
hide: true
hidefromtoc: true
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Översikt över verktyget Användarmappning (äldre) {#overview-user-mapping-tool}

>[!INFO]
>
>Den här dokumentationen refererar till en inaktuell version av verktyget. Mer information om den senaste versionen finns i [Användarmappning och huvudmigrering](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

<!-- Alexandru: drafting this for now

NOTE: "LEGACY" for user mapping includes everything before (that is, not including) 2.0.16 of CTT.

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="User Mapping Tool"
>abstract="The Content Transfer Tool helps you move users and groups from your existing AEM system to AEM as a Cloud Service. Existing users and groups need to be mapped to their IMS IDs to avoid duplicate users and groups on the Cloud Service author instance."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html#important-considerations" text="Important Considerations for using User Mapping Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html#using-user-mapping-tool" text="Using User Mapping Tool"

-->

## Introduktion {#introduction}

Som en del av övergången till Adobe Experience Manager (AEM) as a Cloud Service måste du flytta användare och grupper från ditt befintliga AEM till AEM as a Cloud Service. Den här migreringen görs med verktyget Innehållsöverföring.

En stor förändring av AEM as a Cloud Service är den helintegrerade användningen av Adobe ID:n för åtkomst till författarnivån. Den här integreringen kräver att du använder [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html) för hantering av användare och användargrupper. Användarprofilinformationen är centraliserad i Adobe Identity Management System (IMS) som gör att du kan logga in på alla molnprogram i Adobe. Mer information finns i [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management). På grund av den här ändringen måste befintliga användare och grupper mappas till sina IMS-ID:n för att undvika dubbletter av användare och grupper på Cloud Servicens författarinstans.

## Verktyg för användarmappning {#mapping-tool}

Verktyget Innehållsöverföring (utan användarmappning) migrerar alla användare och grupper som är kopplade till det innehåll som migreras. Verktyget för användarmappning är en del av verktyget för innehållsöverföring. Dess enda syfte är att redigera användarna så att de identifieras korrekt av IMS, den enkla inloggningsfunktionen som används av AEM as a Cloud Service. När ändringarna är klara migrerar verktyget Innehållsöverföring det angivna innehållets användare och grupper som vanligt.

### What&#39;s Next {#whats-next}

När du har lärt dig vad ett verktyg för användarmappning är du nu redo att granska viktiga överväganden och exceptionella fall innan du använder verktyget för användarmappning. Se [Viktigt att tänka på när du ska mappa användare](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md) för mer information.
