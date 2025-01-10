---
title: Ändringar i synkronisering av användargrupp och produktprofil
description: Lär dig mer om förändringarna i synkroniseringen av användargrupper och produktprofiler som kommer till AEM as a Cloud Service
feature: Security
role: Admin
hide: true
hidefromtoc: true
source-git-commit: 32ce30ce136a714e277e00197d38ea380c777377
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---


# Ändringar i synkronisering av användargrupp och produktprofil {#changes-in-user-group-and-product-profile-synchronization}

När en användare loggar in på AEM as a Cloud Service eller en åtkomsttoken används synkroniseras Adobe Admin Console användargrupper, produktprofiler och produktprofiltjänster i AEM som grupper.

Den 28 januari kommer synkroniseringsbeteendet att ändras, vilket resulterar i att färre grupper visas i AEM för att användargränssnittet ska bli mer rörigt och prestandaoptimerat. Två kategorier AEM grupper kommer att tas bort:

1. AEM med suffixet `GROUP_NAME_SUFFIX`. De här grupperna visas inte i Adobe Developer Console, men visas på AEM Group Management-skärmen (se nedan). Om det osannolika fallet att ditt AEM refererar till dessa grupper måste du referera till Adobe Admin Console användargrupper utan det suffixet i stället.

   ![Borttagna grupper ](/help/security/assets/removed-groups-1.png)

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
