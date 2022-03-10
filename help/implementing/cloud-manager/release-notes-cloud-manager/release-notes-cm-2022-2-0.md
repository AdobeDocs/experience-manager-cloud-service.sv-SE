---
title: Versionsinformation för Cloud Manager i AEM as a Cloud Service version 2022.02.0
description: Det här är versionsinformationen för Cloud Manager i AEM as a Cloud Service release 2022.02.0.
feature: Release Information
source-git-commit: f89e1942f63db0b1c57a9d87b051b6a3935ee7cd
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Versionsinformation om Cloud Manager i Adobe Experience Manager as a Cloud Service 2022.02.0 {#release-notes}

På den här sidan beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2022.02.0.

>[!NOTE]
>
>Se [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md) för den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2022.0 är 10 februari 2022. Nästa version är planerad till den 10 mars 2022.

## Nyheter {#what-is-new}

* Ny accelererad [Rörledningar för Web Tier Config](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) har introducerats för att exklusivt distribuera HTTPD/dispatcher-konfiguration.
   * Du måste ha AEM version `2021.12.6151.20211217T120950Z` eller nyare och [välja det flexibla läget för dispatcherverktygen](/help/implementing/dispatcher/disp-overview.md#validation-debug) om du vill använda den här funktionen.
   * Den här funktionen kommer att introduceras stegvis under de två veckorna efter version 2022.02.0.
* Molnhanterarens landningssida har uppdaterats för att ge förbättrad navigering, enkel växling mellan rutnät-/rutvyer och popup-fönster för snabb programsammanfattning.
* Ett nytt tröskelvärde för misslyckande (`< D`) har lagts till i [tillförlitlighetsmått.](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)
   * Kunder med allvarliga kvalitetsproblem som påverkar systemstabiliteten, främst relaterade till ogiltiga index och arbetsflödesprocesser, kommer inte att kunna distribuera förrän dessa problem har lösts.
* Allvarlighetsgraden i `BannedPath` [kvalitetsregel](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules) har ändrats från blockerare till kritiskt.
* Pipeline-guiden informerar användaren om när en AEM behöver uppdateras innan du konfigurerar en [Rörledningar för Web Tier Config](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) som är kopplade till den.

## Felkorrigeringar {#bug-fixes}

* Gamla Git-databaslösenord blir nu alltid ogiltiga när ett nytt lösenord skapas.
* Uppdatering av miljövariabler via API:t stör inte längre en pipeline-körning i sällsynta fall.
