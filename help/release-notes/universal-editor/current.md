---
title: Versionsinformation om Universal Editor 2025.10.30
description: Detta är versionsinformationen för version 2025.10.30 av Universal Editor.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: e3e571bef450ddc09eb30ab7d73b144ea521a87b
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# Versionsinformation om Universal Editor 2025.10.30 {#release-notes}

Det här är versionsinformationen för den 30 oktober 2025-versionen av Universal Editor.

>[!TIP]
>
>Om du vill testa de **kommande** funktionerna i den universella redigeraren innan de släpps, se [Versionsinformationen om den universella redigeraren.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service finns på [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Nyheter {#what-is-new}

* [Den nya textredigeraren](#new-rte) kan nu infoga bilder.
   * Den här funktionen är inaktiverad för OpenB och måste aktiveras explicit via en [filterdefinition.](/help/implementing/universal-editor/configure-rte.md#toolbar)

## Funktioner för tidig användning {#early-adopter}

Om du är intresserad av att testa dessa kommande funktioner och dela med dig av dina synpunkter skickar du ett e-postmeddelande till din Adobe Customer Success Manager från den e-postadress som är kopplad till din Adobe ID.

### Ny RTE {#new-rte}

Den nya ProseMirror RTE med en sidväljare i länkdialogrutan är nu tillgänglig på den högra panelen. [RTE har flexibla konfigurationsalternativ.](/help/implementing/universal-editor/configure-rte.md)

## Andra förbättringar {#other-improvements}

* Uppdateringshändelsen informeras nu om åtgärden har ångrats.
* Strängen `No results` är nu beroende av webbläsarens språkområde i Universella redigeringstaggar.
* En extra radbrytning har korrigerats i Universal Editors publiceringsknapp.
* Rensning gjordes för att korrigera API.
* Knappen Välj innehåll visas nu i Safari.
* RPM-bygget har åtgärdats.
* CORS uppdaterar för att undvika att uppdatera den redigerade texten igen när du har sparat.
