---
title: Versionsinformation för Cloud Manager 2025.1.0 i Adobe Experience Manager as a Cloud Service
description: Läs om Cloud Manager 2025.1.0 i AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: f6c1aa32647bcabeb0781973f81b75c11edc6a5d
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager 2025.1.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3389843928 -->

Läs om Cloud Manager 2025.1.0 i AEM (Adobe Experience Manager) as a Cloud Service.

>[!NOTE]
>
>Se [aktuell versionsinformation för Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Releasedatum {#release-date}

Lanseringsdatumet för Cloud Manager 2025.1.0 i AEM as a Cloud Service är onsdagen den 22 januari 2025.

Nästa planerade version är torsdagen den 13 februari 2025.


## Nyheter {#what-is-new}

* **Kodkvalitetsregler - SonarQube Server Upgrade:** Cloud Manager Code Quality step kommer att börja använda SonarQube Server 9.9 med Cloud Manager 2025.2.0, som är planerad till torsdagen den 13 februari 2025.

Uppdaterade SonarQube-regler finns nu tillgängliga på [Kodkvalitetsregler](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules) för att förbereda.

Du kan kontrollera de nya reglerna tidigt genom att ange följande textvariabel för pipeline:

`CM_BUILD_IMAGE_OVERRIDE` = `self-service-build:sonar-99-upgrade-java17or21`

Ange dessutom följande variabel för att säkerställa att kodkvalitetssteget körs för samma implementering (som normalt hoppas över för samma `commitId`):

`CM_DISABLE_BUILD_REUSE` = `true`

![Konfigurationssida för variabler](/help/implementing/cloud-manager/release-notes/assets/variables-config.png)

>[!NOTE]
>
>Adobe rekommenderar att du skapar en ny CI/CD Code Quality-pipeline som är konfigurerad till samma gren som huvudproduktionsflödet. Ställ in lämpliga variabler *före* den 13 februari 2025 för att verifiera att de nya tvingande reglerna inte inför blockerare.

* Stöd för **Java 17 och Java 21:** Kunder kan nu bygga med Java 17 eller Java 21 och få tillgång till prestandaförbättringar och nya språkfunktioner. Konfigurationssteg, inklusive uppdatering av projekt- och biblioteksversioner för Maven, finns i [Byggmiljö](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). När build-versionen är inställd på Java 17 eller Java 21 är den distribuerade miljön Java 21.

   * **Funktionsaktivering**
      * Den här funktionen kommer att aktiveras för alla kunder torsdagen den 13 februari 2025, vilket sammanfaller med den förvalda lanseringen av den nya SonarQube-versionen.
      * Kunder kan aktivera den *omedelbart* genom att ställa in de två variabelkonfigurationer som beskrivs ovan för uppgradering av SonarQube 9.9-versionen.

   * **Java 21 runtime-distribution**
      * Java 21-miljön distribueras när du skapar med Java 17 eller Java 21.
      * Den gradvisa lanseringen av alla Cloud Manager-miljöer börjar i februari för sandlådor och utvecklingsmiljöer och omfattar även produktionsmiljöer i april.
      * Kunder som bygger med Java 11 och som vill använda Java 21-miljön *tidigare* kan kontakta Adobe på [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com).

* **CDN-konfigurationer har bytt namn till Domänmappningar:** Som en del av förbättringarna i användargränssnittet i AEM Cloud Manager har namnet CDN-konfigurationer ändrats till Domänmappningar för att underlätta terminologisk justering med funktioner. <!-- CMGR-64738 -->

  ![&quot;CDN Configurations&quot; bytte namn till &quot;Domain Mappings&quot; i användargränssnittet ](/help/implementing/cloud-manager/release-notes/assets/domain-mappings.png)


<!-- ## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->

<!-- ## Bug fixes -->




<!-- ## Known issues {#known-issues} -->
