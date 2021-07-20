---
title: 'Tilldela teammedlemmar AEM som en Cloud Service produktprofiler '
description: Följ den här sidan för att lära dig hur du tilldelar teammedlemmar till AEM som en Cloud Service produktprofiler
hide: true
hidefromtoc: true
index: false
source-git-commit: b45d5824afee9e2d540ea7cb41b199b517f26b25
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---


# Tilldela till AEM som en Cloud Service produktprofiler {#assign-team-members-cloud-service}

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå de steg som systemadministratören måste ta för att utse dina teammedlemmar till AEM som produktprofiler för Cloud Service och varför det är viktigt att dina AEM-författare kan ge sig ut på sin resa med AEM.

När du har läst det här avsnittet bör du:

* Förstå varför och hur teammedlemmarna tilldelas AEM som produktprofiler för Cloud Service
* Lär dig hur du lägger till teammedlemmar AEM användarproduktprofilen
* Lär dig hur du lägger till teammedlemmar AEM administratörernas produktprofil


## Introduktion {#introduction}

För att få åtkomst till AEM som Cloud Service måste användare tillhöra en av två produktprofiler, AEM användare eller AEM administratörer. Teammedlemmarna måste beviljas behörigheter till AEM eftersom behörighet att administrera Cloud Manager inte räcker. Läs mer.

>[!NOTE]
>Alla användare som tilldelas AEM användarproduktprofilen av systemadministratören har (skrivskyddad) åtkomst till Cloud Manager.

## Krav {#prerequisites}

* AEM som produktprofiler för Cloud Service
* Bekanta dig med Admin Console
* Produktprofiler för Cloud Manager har tilldelats dina teammedlemmar efter behov, och molnresurserna har konfigurerats
* Information om teammedlemmen: Systemadministratören måste ha namn och e-postadresser samt roller och ansvar för de teammedlemmar som behöver åtkomst till AEM som Cloud Service. För att komma igång rekommenderar vi att du först lägger till användare som ska delta i de omedelbara uppgifterna, till exempel administratörer, utvecklare och innehållsförfattare. Du kan fortsätta med resten av introduktionen utan att lägga till alla användare. När du är klar med introduktionen kan du skala till ett större antal användare senare.


1. Logga in i Admin Console
(Samma som tidigare)

1. Granska AEM som en Cloud Service produktprofiler
Från Admin Console kan du se en lista med Cloud Manager-profiler. Så här gör du:

1. När du har loggat in på Adobe Admin Console väljer du Adobe Experience Manager som en molntjänst på kortet Produkter och tjänster:

1. Navigera till och markera instansen (Author instance of Development environment) som visas i bilden nedan.



   Nu kan du se listan över AEM som en produktprofil för Cloud Service som måste tilldelas en användare baserat på deras roll. Läs mer om dessa AEM som produktprofiler för Cloud Service.




## Lägg till teammedlemmar i AEM användar- eller AEM administratörsproduktprofil {#add-team-members}

För att beviljas åtkomst till AEMaaCS-instansanvändare måste tillhöra någon av produktprofilerna AEM Users eller AEM Administrators.

>[!NOTE]
>Du måste ha behörighet för instansen. Behörigheter att administrera Cloud Manager räcker inte. Läs mer.

Stegen nedan måste följas av systemadministratören som också har rollen Business Owner.

1. Navigera från Cloud Manager till Cloud Manager och välj knappen Hantera åtkomst i den miljö som är av intresse enligt nedan:

1. När du klickar på Hantera åtkomst, navigerar en ny flik till Admin Console från den plats där du har tillgång till författarinstansen av miljön. Välj&quot;AEM administratörer&quot; eller&quot;AEM användare&quot; baserat på de behörigheter som den enskilda personen måste ge. Läs mer om AEM som produktprofiler för Cloud Service.

1. Välj Lägg till användare enligt nedan och skicka den information som krävs för att lägga till teammedlemmen:


1. Du vill upprepa dessa steg för alla miljöer, inklusive utveckling, scen och produktion, om du har information om teammedlemmar som behöver åtkomst till dem.

   Användaren du lade till har nu åtkomst till AEM som Cloud Service Author-tjänster!


## What’s Next {#whats-next}

De användare du tilldelade till AEMaaCS-produktprofilerna är nu redo att lära sig hur du kommer åt Författaren och lär dig mer om hur du skapar sidor i AEM som en Cloud Service. Läs mer.

## Ytterligare resurser {#additional-resources}

Konfigurera åtkomst till AEM (videoutgång)
Snabbstartsguide till framtagning av sidor
