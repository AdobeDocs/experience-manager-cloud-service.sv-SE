---
title: Migrerar stängda användargrupper
description: På den här sidan finns de nödvändiga, speciella överväganden som krävs för att aktivera stängda användargrupper efter att innehåll har migrerats till Adobe Experience Manager as a Cloud Service.
hide: true
hidefromtoc: true
source-git-commit: ca3c4bae2e652d75190d68c76b1dd4e09239f16c
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# Migrerar stängda användargrupper {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="Migrering av stängda användargrupper"
>abstract="Migrering av stängda användargrupper (CUG) kräver för närvarande några kontroller och steg för att kunna genomföra migreringen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html" text="Stängda användargrupper i AEM"

För närvarande behöver stängda användargrupper (CUG) några ytterligare steg för att fungera i målmiljön för en migrering.  I det här dokumentet förklaras scenariot och de steg som krävs för att skydda noderna på det avsedda sättet.

## Migrering av grupper

Huvudposter (inklusive grupper) inkluderas automatiskt i en migrering till Adobe Experience Manager as a Cloud Service om de är kopplade till det migrerade innehållet via det innehållets åtkomstkontrollista.

## Stängda användargrupper under migrering

För närvarande, associerade grupper *endast* med en CUG-princip (Closed User Group) *not* ingår automatiskt i intaget. Om de är kopplade till något innehåll via en ACL, som nämnts ovan, kommer de att migreras. Verifiering av att gruppen finns bör göras innan live-publicering görs. Huvudrapporten, som hämtas via förslagsjobbvyn, kan användas för att se om den aktuella gruppen inkluderades eller inte var eftersom den inte fanns i en åtkomstkontrollista. Om gruppen inte finns bör den skapas i Author-instansen, inklusive tillägg av lämpliga medlemmar, och aktiveras så att den finns på Publish-instansen.

Slutligen måste processerna aktiveras för att CUG ska aktiveras. Om du vill göra det publicerar du om innehållet som innehåller CUG-principen. Så om det i dina normala testprocesser upptäcks att CUG inte fungerar, publicerar du innehållet igen (och ser till att det publiceras även om det inte ändras).

Detta bör aktivera CUG-principer vid publicering, och innehållet är endast tillgängligt för autentiserade användare som är medlemmar i gruppen som är kopplad till profilerna.

## Aktiv utveckling

Migreringsteamet arbetar med att få CUG-policyer att migreras och fungera automatiskt, utan några ytterligare steg efter att innehållet har importerats.
Det är tillrådligt att inkludera CUG-funktioner i alla testprocesser innan du försöker publicera.

## Sammanfattning

Sammanfattningsvis är det här stegen för att aktivera CUG efter en migrering:

1. Kontrollera att varje grupp som används i CUG-principer finns vid publicering efter migreringen.
   - En grupp kan redan finnas om den ingår i ett migrerat innehålls åtkomstkontrollista.
   - Om den inte gör det kan du använda paket för att installera den på målinstansen (eller skapa den manuellt där) och aktivera den och dess medlemmar. Kontrollera sedan att den finns vid publicering.
1. Om CUG-principen ännu inte skyddar noden publicerar du sidan igen (ser till att den publiceras även om inga ändringar gjorts på sidan).
   - Kontrollera för varje CUG-skyddad nod.
