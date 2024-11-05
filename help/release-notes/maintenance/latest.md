---
title: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c638039ea957f5f7ae0dc64f49c3ace4381cb040
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs de tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 18459 {#18459}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 18459, som offentliggjordes den 5 november 2024. Den tidigare underhållsversionen var version 18311.

Funktionsaktiveringen i 2024.11.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-18459}

* CQ-4357471: Lägg till stöd för i18n-ordlisteöversättning i AEMaaCS.
* SITES-23591: Content Fragments: Content fragment upgrade for UUID support.
* SITES-25440: Content Fragments: CFM Search API för att visa replikeringsstatus.
* SITES-24369: Content Fragments: Förbättringar av OpenAPI-dokumentation.
* SITES-25478: Content Fragments: Add back-end support for external asset references.
* SITES-26119: Content Fragments: Add support of external asset references in reference type.
* SITES-21199: Edge Delivery med Universal Editor: Lägg till stöd för mallar som skapats från sidor.
* SITES-20311: Edge Delivery med Universal Editor: Lägg till stöd för import av CSV-filer till kalkylblad.
* SITES-24821: Edge Delivery med Universal Editor: Gör aem.page / aem.live till standard för integrering med Edge Delivery.

### Åtgärdade problem {#fixed-issues-18459}

* CQ-4358730: CQPagePreviewGenerator misslyckas när det finns fler än 10 nycklar att översätta.
* FORMS-14978: Aktivera sidinläsning för ett Core Component-baserat formulär för temaredigeraren.
* FORMS-16596: Hjälpmedelsproblem: Inaktiverade knappar som inte känns igen av Reader på skärmen.
* SITES-10575: MSM: Blueprint Bloomfilter Loader försöker läsa in >100 000 rader.
* SITES-20755: Innehållsfragment: Resursreferens med UUID-uppdatering visar inte miniatyrbilden.
* SITES-26253: Content Fragments: UUID migration: Change sling job topic to be generic.
* SITES-21338: Content Fragments: referencedBy endpoint does not return the correct page reference.
* SITES-24421: Innehållsfragment: Redigera CF-slutpunkt fungerar inte för CF som hämtats via GET CF.
* SITES-25461: Innehållsfragment: Filtrera efter modell i sökning efter CF:er ska vara skiftlägeskänsliga.
* SITES-25471: Content Fragments: Fix validation of global models in the ModelValidatorServlet.
* SITES-25795: Content Fragments: CF Model API misslyckas när det inte finns någon cq-datumuppsättning.
* SITES-25817: Content Fragments: Enhance PromoteLaunch: update last campaign for CF Launches.
* SITES-26030: Content Fragments: Endpoint /referencesTree returnerar inte det huvud som behövs.
* SITES-26031: Innehållsfragment: Replikeringsstatusen returnerades inte för CFM-sökslutpunkten.
* SITES-26213: Content Fragments: Unpublish content fragments should only validate published references.
* SITES-26226: Content Fragments: Start workflow issue when none of the given paths are usable.
* SITES-26238: Innehållsfragment: Resursreferenserna som returneras av API:t har en annan ordning än ordningen från JCR.
* SITES-25456: Händelser: När du flyttar en sida genereras en sidborttagen händelse förutom händelsen för sidflyttning.
* SITES-25658: Events: The tier and sourceUrl are not populated in the page content state events.
* SITES-6497: Startar: Det går inte att skapa sidan vid start.
* SITES-25393: Edge Delivery med Universal Editor: Textnoder förloras vid återgivning av formaterad RTF med ett enda stycke.
* SITES-24643: Edge Delivery med Universal Editor: Metadataattribut för OpenGraph och twitter fungerar inte i sidmetadatamodell.

### Kända fel {#known-issues-18459}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-18459}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Inbäddade tekniker {#embedded-tech-18459}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | 1.4.24-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.27.0 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |
