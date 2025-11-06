---
title: Migrerar stängda användargrupper
description: Läs mer om de speciella överväganden som krävs för att aktivera stängda användargrupper efter att du har migrerat innehåll till Adobe Experience Manager as a Cloud Service.
hide: true
hidefromtoc: true
exl-id: f62ed751-d5e2-4a01-8910-c844afab5733
feature: Migration
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---


# Migrerar stängda användargrupper {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="Migrering av stängda användargrupper"
>abstract="För migrering av stängda användargrupper (CUG) krävs för närvarande några kontroller och steg för att den ska fungera efter en migrering."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html" text="Stängda användargrupper i AEM"

För närvarande behöver stängda användargrupper (CUG) några ytterligare steg för att fungera i målmiljön för en migrering. I det här dokumentet förklaras scenariot och de steg som krävs för att skydda noderna på det avsedda sättet.

## Migrering av stängda användargrupper

Grupper inkluderas automatiskt i en CTT/CAM-migrering till Adobe Experience Manager as a Cloud Service om de är kopplade till det migrerade innehållet via det innehållets ACL-lista eller dess CUG-principnod. Verifiering av att gruppen och dess medlemmar finns bör göras innan publicering görs. Grupper som refereras till i en CUG-policy kallas här för&quot;CUG-grupper&quot;.

Om du vill använda CUG-filer i AEM as a Cloud Service måste användarna finnas på Author-instansen och vara medlemmar i de relevanta CUG-grupperna.  Detta kan göras med paket, eller om CUG-användarna är IMS-användare kanske de redan är närvarande.  CUG-användare måste sedan bli medlemmar i AEM CUG-grupper.

Om du vill aktivera CUG-beteenden i Publish-instansen

1. CUG-grupperna måste aktiveras (vilket replikerar dem och deras medlemmar till Publish-instansen),
1. *Alla* sidor som skyddas med CUG-principer måste avpubliceras (för att ta bort det globala CUG-antalet) och
1. Sidorna som skyddas med CUG-profiler måste sedan publiceras (vilket aktiverar Publish-instansen och spårar profilerna).
1. När alla sidor har publicerats kontrollerar du funktionerna för varje CUG-skyddad sida.

Mer information finns i [Stängda användargrupper](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html).
