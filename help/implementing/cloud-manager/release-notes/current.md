---
title: Versionsinformation för Cloud Manager 2025.2.0 i Adobe Experience Manager as a Cloud Service
description: Läs om Cloud Manager 2025.2.0 i AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: aaef376b733c10643e44205e55a0921c22008990
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager 2025.2.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3389843928 -->

Läs om Cloud Manager 2025.2.0 i AEM (Adobe Experience Manager) as a Cloud Service.


Se även [aktuell versionsinformation för Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Releasedatum {#release-date}

Lanseringsdatumet för Cloud Manager 2025.2.0 i AEM as a Cloud Service är torsdagen den 13 februari 2025.

Nästa planerade version är torsdagen den 13 mars 2025.

## Nyheter {#what-is-new}

* **Uppdatera till regler för kodkvalitet**

  Från och med torsdagen den 13 februari 2025 använder Cloud Manager kodkvalitetssteg nu SonarQube 9.9.5.90363.

  De uppdaterade reglerna, som är tillgängliga för Cloud Manager på AEM as a Cloud Service på [den här länken](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules), avgör säkerhetspoängen och kodkvaliteten för Cloud Manager-pipelines.

* SonarQube 9.9 är nu standardmotor för kodkvalitetskontroll för alla kunder.

* **Stöd för Java 17 och Java 21**

  Kunderna kan nu bygga med Java 17 eller Java 21 och få tillgång till prestandaförbättringar och nya språkfunktioner. Konfigurationssteg, inklusive uppdatering av projekt- och biblioteksversioner för Maven, finns i [Byggmiljö](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). När build-versionen är inställd på Java 17 eller Java 21 är den distribuerade miljön Java 21.

* **99,99% SLA-rapportering för Edge Delivery Services**

  99,99 % av drifttiden är nu tillgänglig för berättigande Edge Delivery Services-program. För att den här funktionen ska kunna användas måste man kunna lägga upp Edge Delivery Services webbplatser och använda 99,99 % Service level agreement (SLA) i Cloud Manager.

  Se även [SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla).

* **Förbättrad användarinbjudan för Edge Delivery Services**

  Upplevelsen med att bjuda in användare till innehållsarkivet som är kopplat till Edge Delivery Services har förbättrats. <!-- CMGR-65331 -->

* **Skapa administratörsprofiler automatiskt på publiceringsinstanser**

  Tidigare tillät Cloud Manager att administrationsprofiler skapades manuellt på publiceringsinstanser, men hade inte stöd för automatisk generering som standard. Med den här uppdateringen skapas nu administratörsprofiler automatiskt för publiceringsinstanser, vilket förbättrar användbarheten och minskar installationstiden för kunderna.

  Mer information finns i [Anpassade behörigheter](/help/implementing/cloud-manager/custom-permissions.md).

  ![Filtrering av pipeline-aktiviteter](/help/implementing/cloud-manager/release-notes/assets/product-profiles.png)

* **Övergång till OAuth för Cloud Service-miljöer**

  Nya Cloud Service-miljöer använder nu OAuth-baserad tjänst-till-tjänst-autentisering för Adobe Developer Console-integrationsprojekt i stället för den tidigare använda JWT-autentiseringsmetoden. JWT-autentisering är föråldrat och planeras att upphöra i juni 2025.

* **Stöd för privata nycklar för EC (Elliptisk kurva) (secp384r1)**

  Cloud Manager har nu stöd för `secp384r1` privata nycklar för elliptiska kurvor (EC), vilket ger förbättrad säkerhet och efterlevnad för kundhanterade OV/EV SSL-certifikat.
Mer information finns i [Krav för kundhanterade OV/EV SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements). <!-- CMGR-63636 -->

* **Specialiserade testmiljöer**

  En ny utvecklingsmiljö med utökade resurser kommer att finnas tillgänglig för tidiga användare från och med den 27 februari 2025.


<!--
## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->


## Felkorrigeringar

* **(UI) Ett problem som förhindrar CDN-konfiguration för domäner i Cloud Manager har korrigerats.**
Kunder som försöker lägga till en CDN-konfiguration i Cloud Manager påträffade ett skärmfel när de valde en domän i listrutan. Detta användargränssnittsfel förhindrade domänmappning i produktionsmiljöer och blockerade konfigurationsprocessen.

  Dessutom var vissa domäner oåtkomliga i serverdelen, trots att de togs bort från användargränssnittet. Detta problem ledde till konflikter med befintliga CDN-konfigurationer.

  Med den här korrigeringen kan du nu välja en domän i listrutan utan utan att stöta på något fel. Inkonsekvenser i bakgrunden som hindrade omkonfigurering av domäner har åtgärdats. Slutligen säkerställer den förbättrade valideringen nu att motstridiga domäner tas bort korrekt innan de läggs till igen.<!-- CMGR-64888 -->
* **(Backend) Korrigerade ett problem som medförde att SSL-förfallomeddelanden skickades flera gånger.**
Ett fel identifierades där SSL-schemaläggaren för förfallomeddelanden, som är avsedd att köras en gång dagligen vid midnatt, felaktigt utlöstes två gånger per dag vid midnatt och en gång till kl. 12.30. Detta problem medförde att flera redundanta meddelanden skickades om att SSL-certifikat skulle upphöra att gälla.

  Schemaläggaren för meddelanden körs nu korrekt bara en gång per dag som det ska. Du får inte längre några dubbletter av meddelanden om att SSL-förfallodatum. <!-- CMGR-64748 -->




<!-- ## Known issues {#known-issues} -->
