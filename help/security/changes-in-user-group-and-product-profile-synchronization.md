---
title: Ändringar i synkronisering av användargrupp och produktprofil
description: Lär dig mer om förändringarna i synkroniseringen av användargrupper och produktprofiler som kommer till AEM as a Cloud Service
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 0b097ab3-bf1d-4d43-9e19-d544594844ef
source-git-commit: 5c103fcce1ae47bc89f4f572d89967c62c1f7603
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Ändringar i synkronisering av användargrupp och produktprofil {#changes-in-user-group-and-product-profile-synchronization}

När en användare loggar in på AEM as a Cloud Service eller en åtkomsttoken används synkroniseras Adobe Admin Console användargrupper, produktprofiler och produktprofiltjänster i AEM som grupper.

Från och med AEM Maintenance Release 19149 ändras gruppsynkroniseringsbeteendet för att minska användargränssnittets oskärpa och optimera prestandan. I synnerhet kommer användargruppsmedlemskapet i följande två kategorier av AEM inte längre att synkroniseras:

1. AEM med suffixet `GROUP_NAME_SUFFIX`. De här grupperna visas inte i Adobe Developer Console, men visas på AEM Group Management-skärmen (se nedan). Om det osannolika fallet att ditt AEM refererar till dessa grupper måste du referera till Adobe Admin Console användargrupper utan det suffixet i stället.

   ![Borttagna grupper &#x200B;](/help/security/assets/removed-groups-1.png)

1. AEM som är kopplade till Adobe Admin Console produktprofiler som inte har med den specifika miljön att göra. Detta kan omfatta produktprofiler som är:

   * för andra Adobe-produkter
   * relaterade till andra AEM program
   * som rör andra AEM miljöer i samma AEM
   * relaterat till Cloud Manager (till exempel `Business Owner - Cloud Service`)

   I bilden nedan finns till exempel många rader med mönstret `AEM Administrators-<suffix>` eller `AEM Users-<suffix>` där suffixet inte är relaterat till den aktuella miljön.

   ![Borttagna grupper 2](/help/security/assets/removed-groups-2.png)

Du kan kontrollera vilket suffix som är relaterat till den aktuella miljön genom att välja Hantera **Åtkomst - Författarprofiler** (eller **Publish-profiler**) i miljöns åtgärdsmeny i Cloud Manager.

![Kontrollera suffix](/help/security/assets/suffix-check.png)

På så sätt navigerar du till Adobe Admin Console enligt skärmbilden nedan. Observera att `<suffix>` kan vara en slumpmässig teckenuppsättning eller snarare nivå- och program- och miljö-ID (till exempel `author - Program 12345 - Environment 45678`).

![Suffix i Admin Console](/help/security/assets/admin-console-profile-suffixes.png)

Om det osannolika fallet är att ditt AEM-program refererar till en grupp som inte längre visas i AEM ska du i stället antingen använda i) en produktprofil från den högra AEM eller ii) en Adobe Admin Console-användargrupp.

Användarens gruppmedlemskap synkroniseras när de loggar in i miljön och tas bort från grupper som inte är relaterade till den aktuella miljön. Själva grupperna finns kvar och innehåller användare som inte har loggat in sedan funktionen aktiverades.
