---
title: Migrerar stängda användargrupper
description: Läs mer om de speciella överväganden som krävs för att aktivera stängda användargrupper efter att du har migrerat innehåll till Adobe Experience Manager as a Cloud Service.
hide: true
hidefromtoc: true
exl-id: f62ed751-d5e2-4a01-8910-c844afab5733
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '461'
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

Huvudposter (inklusive grupper) inkluderas automatiskt i en migrering till Adobe Experience Manager as a Cloud Service om de är kopplade till det migrerade innehållet via det innehållets åtkomstkontrollista.

## Stängda användargrupper under migrering

För närvarande, associerade grupper *endast* med en CUG-princip (Closed User Group) *not* ingår automatiskt i intaget. Som nämnts ovan migreras de om de är kopplade till något innehåll via en ACL. Verifiering av gruppen och dess medlemmar ska göras innan publicering inleds. Huvudrapporten, som hämtas via förslagsjobbvyn, kan användas för att se om den aktuella gruppen inkluderades eller inte var eftersom den inte fanns i en åtkomstkontrollista. Om gruppen inte finns bör den skapas i Author-instansen, inklusive tillägg av lämpliga medlemmar, och aktiveras så att den finns i Publish-instansen. Detta kan göras med paket som skapats på källan.

Slutligen måste processerna aktiveras och egenskaper anges för att aktivera CUG-grupper. Det gör du genom att publicera om alla sidor som är kopplade till en CUG-princip. Detta kalibrerar Publish-instansen för att spåra profilerna.

Detta aktiverar CUG-profiler vid publicering, och innehållet är bara tillgängligt för autentiserade användare som är medlemmar i gruppen som är kopplad till profilerna.

## Aktiv utveckling

Migreringsteamet arbetar med att få CUG-policyer att migreras och fungera automatiskt, utan några ytterligare steg efter att innehållet har importerats.
Inkludera CUG-funktioner i testprocesser innan du försöker publicera.

## Sammanfattning

Sammanfattningsvis är det här stegen för att aktivera CUG efter en migrering:

1. Kontrollera att varje grupp som används i CUG-principer finns vid publicering efter migreringen.
   - Det kan finnas en grupp om den ingår i det migrerade innehållets åtkomstkontrollista.
   - Om den inte gör det kan du använda Paket för att installera den på målinstansen (eller skapa den manuellt där) och aktivera den och dess medlemmar. Kontrollera sedan att den finns vid publicering.
1. Publicera om alla sidor som är kopplade till en CUG-princip och kontrollera att den publiceras, till exempel genom att redigera sidan först. Det är viktigt att publicera om alla.
   - När alla sidor har publicerats om kontrollerar du att de fungerar för varje CUG-skyddad sida.
