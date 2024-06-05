---
title: Migrerar stängda användargrupper
description: Läs mer om de speciella överväganden som krävs för att aktivera stängda användargrupper efter att du har migrerat innehåll till Adobe Experience Manager as a Cloud Service.
hide: true
hidefromtoc: true
exl-id: f62ed751-d5e2-4a01-8910-c844afab5733
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# Migrerar stängda användargrupper {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="Migrering av stängda användargrupper"
>abstract="För migrering av stängda användargrupper (CUG) krävs för närvarande några kontroller och steg för att den ska fungera efter en migrering."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html" text="Stängda användargrupper i AEM"

För närvarande behöver stängda användargrupper (CUG) några ytterligare steg för att fungera i målmiljön för en migrering. I det här dokumentet förklaras scenariot och de steg som krävs för att skydda noderna på det avsedda sättet.

## Migrering av grupper

Objekt (inklusive grupper) inkluderas automatiskt i en migrering till Adobe Experience Manager as a Cloud Service om de är kopplade till det migrerade innehållet via det innehållets åtkomstkontrollista, och de inkluderas också om de refereras till i en CUG-princip för det innehållet.

## Stängda användargrupper under migrering

Verifiering av gruppen och dess medlemmar ska göras innan publicering inleds. Huvudrapporten, som hämtas via förslagsjobbsvyn, kan användas för att se om gruppen i fråga ingick eller inte eftersom den inte fanns i en ACL- eller CUG-princip.

Därefter måste processerna aktiveras och egenskaperna anges för att aktivera CUG-grupper. Det gör du genom att publicera om alla sidor som är kopplade till en CUG-princip. Detta kalibrerar Publish-instansen för att spåra profilerna.

Detta aktiverar CUG-profiler vid publicering, och innehållet är bara tillgängligt för autentiserade användare som är medlemmar i gruppen som är kopplad till profilerna.

## Sammanfattning

Sammanfattningsvis är det här stegen för att aktivera CUG efter en migrering:

1. Kontrollera att varje grupp som används i CUG-principer finns vid publicering efter migreringen.
   - Det kan finnas en grupp om den ingår i ett migrerat innehålls CUG-princip eller i innehållets ACL.
   - Om den inte gör det kan du använda Paket för att installera den på målinstansen (eller skapa den manuellt där) och aktivera den och dess medlemmar. Kontrollera sedan att den finns vid publicering.
1. Publicera om alla sidor som är kopplade till en CUG-princip och kontrollera att den publiceras, till exempel genom att redigera sidan först. Det är viktigt att publicera om alla.
   - När alla sidor har publicerats om kontrollerar du att de fungerar för varje CUG-skyddad sida.
