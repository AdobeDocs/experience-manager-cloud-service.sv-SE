---
title: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2021.12.0
description: Det här är versionsinformationen för Cloud Manager i AEM as a Cloud Service release 2021.12.0.
feature: Release Information
source-git-commit: 72853f1278be4dd429be28fd611b5a0cb77bcb3d
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---


# Versionsinformation för Cloud Manager i Adobe Experience Manager as a Cloud Service 2021.12.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.12.0.

>[!NOTE]
>
>Se [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md) för den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Lanseringsdatumet för Cloud Manager i AEM as a Cloud Service 2021.12.0 är 16 december 2021. Nästa version är planerad till januari 2022.

### Nyheter {#what-is-new}

* Den implementerade hashen, som redan är synlig i användargränssnittet, finns nu även i API:t.
* På sidan Activity (Aktivitet) finns nu ett popup-fönster för rörledningar som ger en översikt över pipelineinformationen.
* Uppdateringar för att inkludera ytterligare information som presenteras på aktivitetssidan lades till.
* Fliken Lär dig i Cloud Manager innehåller nu snabb åtkomst till API-guider och associerade resurser.
* En användare med rollen Distributionshanterare kan nu initiera guiden Skapa projekt/gren för en databas utan grenar från åtgärdsmenyn på databassidan.
* Distributionshanteraren, som är i arbetsflödet för att lägga till eller redigera pipeline, får nu information om hur du skapar en gren eller ett projekt om den valda databasen inte har några grenar.
* En ny självbetjäningsfunktion för Cloud Manager har lagts till för att tillåta [lägga till frihandsvariabler och hemligheter på miljönivå.](/help/implementing/cloud-manager/environment-variables.md)
* Med det nya tillägget för referensdemonstrationer (tillgängligt den 17 december 2021) kan de senaste demokodsbaserna för AEM installeras och vara klara att driftsättas via det nya [snabbverktyg för att skapa webbplatser](/help/journey-sites/quick-site/overview.md) i Sites.
* Framtidsrörledningar har nu stöd för rörliga variabler.
* Skärmar kan nu aktiveras i dialogrutan Programredigering för alla sandlådor.
* Vägledningen från anropskortet på översiktssidan har uppdaterats för att korrekt återge dess koppling till produktionsflödet för hela stacken.
* Förbättringar av aktivitetssidan har lagts till i ytterligare information som gäller för rörledningar, inklusive källkod, ID för genomförande osv.
* Mindre uppdateringar gjordes i användargränssnittet när TXT-poster kopierades (&quot;TXT-värde&quot; istället för&quot;TXT-post&quot;) för att undanröja eventuella förvirringar.
* [Dokumentationen som rör certifikatfel](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-errors) har uppdaterats för att omfatta ytterligare exempel tillsammans med felsökningssteg.
* Det finns nu ett alternativ för att avvisa eller godkänna i den främre pipeline-körningen innan distributionen till produktionen.

### Felkorrigeringar {#bug-fixes}

* Funktionella och gränssnittstestartefakter inkluderades inte i byggstegsloggen.
* Loggarna för teststegen för produkten, funktionen och användargränssnittet kunde inte nås via det publika API:t.
* I sällsynta fall är länken från sidan med miljöinformation till publicerings- eller förhandsgranskningstjänsten icke-funktionell.
* Kompletta produktionsledningar för stackproduktion förblir namngivna&quot;Production Pipeline&quot; även när användaren anger ett annat namn i namnfältet.
