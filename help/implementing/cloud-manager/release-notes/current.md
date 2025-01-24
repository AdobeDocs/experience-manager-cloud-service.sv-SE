---
title: Versionsinformation för Cloud Manager 2025.1.0 i Adobe Experience Manager as a Cloud Service
description: Läs om Cloud Manager 2025.1.0 i AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 9850a52626c2bd80f7528931d23691dff1dd3eb2
workflow-type: tm+mt
source-wordcount: '811'
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

* **&quot;CDN-konfigurationer&quot; har bytt namn till &quot;Domänmappningar&quot;:** Som en del av förbättringarna av användargränssnittet i AEM Cloud Manager har etiketten &quot;CDN-konfigurationer&quot; nu bytt namn till &quot;Domänmappningar&quot;. Den här ändringen förbättrar terminologisk justering med funktioner. <!-- CMGR-64738 -->

  ![&quot;CDN Configurations&quot; bytte namn till &quot;Domain Mappings&quot; i användargränssnittet ](/help/implementing/cloud-manager/release-notes/assets/domain-mappings.png)

* **Tillhandahåller en Edge Delivery-webbplats med ett klick:** Cloud Manager tillåter nu användare med rätt behörigheter och licenser att skapa en exempelwebbplats för Edge Delivery Services med bara ett klick. Denna smidiga process erbjuder följande automatiska funktioner:

   * **GitHub-integrering** - Skapar automatiskt en GitHub-databas inom en befintlig organisation, förkonfigurerad med en standardmall för Edge Delivery Services.
   * **AEM Installation av appen för kodsynkronisering** - Installerar programmet för AEM kodsynkronisering i databasen, vilket garanterar smidig synkronisering och distribution.
   * **Innehåll Collaboration Setup** - Länkar en angiven Google Drive-mapp för innehållslagring, vilket ger en samarbetsmiljö för innehållshantering.
   * **Innehållspublicering** - Nu kan användare publicera innehåll för tilldelade webbplatser direkt från Cloud Manager användargränssnitt, vilket förenklar arbetsflödena och förbättrar effektiviteten.
   * **Förbättrad Collaboration** - Med den här plattformen kan användare lägga till flera medarbetare i Google Drive-innehållslagringsmappen, vilket underlättar teamarbete och innehållsinsatser.

  Dessa förbättringar syftar till att förbättra automatiseringen, förenkla installationsprocesserna och förbättra samarbetet för Edge Delivery Services. <!-- CMGR-59362 -->

  ![Etablerar en Edge Delivery-webbplats](/help/implementing/cloud-manager/release-notes/assets/eds-one-click-60.png)

  ![Dialogrutan etablerar Edge Delivery-webbplats](/help/implementing/cloud-manager/release-notes/assets/eds-provision-60.png)

* **Utökat stöd för Edge Delivery Services:** Cloud Manager har nu stöd för nyanställda på webbplatser för de senaste Edge Delivery Servicens. Uppdateringen innehåller en omfattande omfaktorisering av CDN och leveransstack, vilket ger ökad tillförlitlighet och underhållbarhet.

* **Tidig uppdatering av Adobe-program - PR-valideringsstöd för Bitbucket och GitLab:** Cloud Manager har nu stöd för Pull Request (PR)-validering för både Cloud och självhanterade versioner av Bitbucket och GitLab. Med den här funktionen kan kunderna testa sina kodändringar mot kvalitetströsklar för Adobe innan de sammanfogar en PR. Genom att säkerställa högre kodkvalitet före sammanslagningen förbättras kodsändringar i produktionspipelinerna avsevärt, vilket minskar time to market och effektiviserar utvecklingsarbetsflödena.

* **Avancerade filtreringsalternativ för pipelines:** Cloud Manager har nu avancerade filtreringsalternativ på sidan för pipelines, vilket gör att du snabbt kan komma åt relevanta data och förbättra driftsättningseffektiviteten. Några av de viktigaste funktionerna är:

   * **Flervillkorsfiltrering:** Förfina sökresultaten med filter som pipeline-namn, miljö och distribuera kod.
   * **Smidig Pipeline-sökning:** Hitta enkelt specifika pipelines för snabbare navigering och förbättrad arbetsflödeshantering.

  Tillsammans gör dessa förbättringar att hanteringen och driftsättningen av rörledningar blir effektivare och användarvänligare.

  ![Funktionen Pipelinefilter](/help/implementing/cloud-manager/release-notes/assets/pipeline-filters.png)

* **Självbetjäning-CDN-konfiguration för Edge Delivery-tjänst:** Nya användare av Edge Delivery Service kan nu konfigurera sitt CDN separat via Cloud Manager. Den här uppdateringen utökar stödet från `.hlx.page/live` till nya `.aem.page/live`, vilket ger större flexibilitet och effektiviserad konfiguration för användare.


<!-- ## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->

<!-- ## Bug fixes -->




<!-- ## Known issues {#known-issues} -->
