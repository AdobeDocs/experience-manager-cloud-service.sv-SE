---
title: Konfigurera molnresurser via Cloud Manager
description: Följ den här sidan för att lära dig hur du konfigurerar molnresurser via Cloud Manager
hide: true
hidefromtoc: true
index: false
source-git-commit: 021146e4e1d65c7fe81ed3dba70b32daf34b9704
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---

# Konfigurera molnresurser via Cloud Manager {#setup-cloud-resources}

Den systemadministratör som tilldelats rollen&quot;Business Owner&quot; bör ha åtkomst till och logga in i Cloud Manager. Därefter måste en teammedlem som tilldelats produktprofilen&quot;Business Owner&quot; logga in på Cloud Manager och skapa ditt molnprogram och miljöer så att ditt expertteam kan komma igång.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur dina molnresurser skapas och vem som kan göra det.

När du har läst det här avsnittet bör du:

* Förstå att en systemadministratör som tilldelats rollen Business Owner måste vara den första som får åtkomst till och inloggning med Cloud Manager
* Förstå hur ditt molnprogram och dina miljöer skapas.

## Introduktion {#introduction}

Din teammedlem som är tilldelad till produktprofilen för Cloud Manager Business Owner lägger till dina molnresurser via Cloud Manager. Den här personen är vanligtvis en person som förstår affärsbehoven och som slutför den ursprungliga installationen av Cloud Manager.

Följ nedanstående avsnitt för att lära dig hur du skapar dina [molntjänstprogram](#create-cloud-service-program) och [miljöer](#create-cloud-environments).

### Krav {#prerequisites}

* Den systemadministratör som tilldelats rollen&quot;Business Owner&quot; ska ha åtkomst till och logga in i Cloud Manager.

* Lär dig navigera och logga in i Cloud Manager

* Bekanta dig med Cloud Manager-produktprofiler

* Förstå vad du bör tänka på när du skapar programmet. I den här videon får du veta mer.

* Förstå begreppen för program och miljöer i Cloud Manager

## Navigera till Cloud Manager {#navigate-cloud-manager}

1. Användaren&quot;Business Owner&quot; får ett välkomstmeddelande där han/hon kan komma igång, eller om han/hon inte hittar det går du direkt till experience.adobe.com och loggar in med din Adobe ID.

1. På Experience Cloud hemsida väljer du Experience Manager:


1. Du kommer nu till AEM startsida. Välj Cloud Manager härifrån:


1. Du kommer nu till landningssidan för Cloud Manager enligt nedan:


1. Verifiera nu att du har tilldelats produktprofilen Business Owner. Välj din profil längst upp till höger så som visas nedan:


1. Välj sedan Användarroller och kontrollera att du är tilldelad till Business Owner.


   Bra jobbat! Du har loggat in på Cloud Manager som företagsägare!

## Creating Cloud Service Program {#create-cloud-service-program}


1. Navigera till landningssidan för Cloud Manager enligt nedan.

   >[!NOTE]
   >Du måste vara en teammedlem som har tilldelats produktprofilen för Cloud Manager Business Owner för att kunna slutföra det här steget.

1. Här väljer du Lägg till program för att starta guiden Lägg till program. I videon får du lära dig hur du skapar AEMaaCS-programmet och viktiga överväganden innan du skapar programmet.

1. Om du vill ha steg-för-steg-anvisningar om hur du använder guiden Lägg till program går du hit.

   >[!CAUTION]
   >Kom ihåg att programnamnet inte kan ändras när det har skapats. Vi rekommenderar att du vet vilket namn du vill ge ditt program.

   Om du måste byta namn på ditt program måste du öppna ett ärende hos Adobe Support eller kontakta Adobe. De kommer att bidra till att effektivt ta bort programmet. Du måste börja om från början igen med potentiell förlust av arbete som teamet har gjort.

1. När ditt molnprogram har skapats kan du navigera till programmet och se programmets översiktssida enligt nedan:

1. Om du inte redan har gjort det är det ett bra tillfälle att lägga till dina utvecklarmedlemmar i ditt Cloud Manager-team, gå till Lägg till användare i Developer-produktprofilen och följ stegen som beskrivs.

1. Medlemmar som är tilldelade till produktprofilen för utvecklare kan logga in på Cloud Manager och Hantera Cloud Manager Git.


   Bra jobbat! Nu när ditt program har skapats är din Cloud Manager Git tillgänglig för dina utvecklare!


## Skapa dina molnmiljöer {#create-cloud-environments}

1. När du har skapat ditt molnprogram skapar du dina molnmiljöer genom att gå till översiktssidan för Cloud Manager och välja Lägg till på miljökortet.

   >[!NOTE]
   >En Cloud Manager-användare i rollen Business Owner eller Deployment Manager måste vara inloggad för att det här steget ska kunna slutföras.

   Titta dessutom på videosjälvstudiekursen för att lära dig mer om Cloud Manager-miljöer och hur du kan lägga till dem i ditt program.

1. Detta startar guiden för att lägga till miljö som hjälper dig att lägga till din miljö. Lägg till din utvecklingsmiljö först för att bekanta dig.

1. Om du inte redan har gjort det kan du lägga till dina utvecklarmedlemmar i ditt Cloud Manager-team nu, gå till Lägg till användare i Developer-produktprofilen och följa stegen som beskrivs. På så sätt kan utvecklarna komma igång med att navigera till Cloud Manager och Managing Cloud Manager Git.


   Grattis! Nu har dina molnmiljöer skapats och dina utvecklare har lagts till i teamet!

## What’s Next {#whats-next}

Nu måste teammedlemmarna beviljas behörighet till instansen eftersom behörighet att administrera Cloud Manager inte räcker. Nu när dina molnresurser har skapats och är klara att användas av ditt team måste systemadministratören utse dina teammedlemmar till AEM som en Cloud Service produktprofiler från Admin Console.

>[!NOTE]
>För att få åtkomst till AEM som Cloud Service måste användare tillhöra någon av produktprofilerna AEM användare eller AEM administratörer. Läs mer.

## Ytterligare resurser {#additional-resources}

Följ de andra resurserna för att lära dig mer om:

* Programtyper och lägga till ett program
* Miljötyper och tillägg av en miljö
* Hantera Cloud Manager Git
* Konfigurera åtkomst till AEM som en Cloud Service från Admin Console
