---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 5474d0c4295cf8eb576cc416589727c67ffafac7
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 0%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Utgåva 23320 {#23320}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåva 23320, som offentliggjordes den 12 november 2025. Den tidigare underhållsversionen var version 22943.

Funktionsaktiveringen i 2025.11.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/sv/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

>[!NOTE]
>
>Version 23122 har gjorts privat den 3 november.

### Förbättringar {#enhancements-23320}

* CQ-4361363: De senaste översättningarna från AEM och Granite.
* FORMS-21594: Aktivera låsning av innehåll och layout för interaktiva kommunikationsmallar för innehållsförfattare.
* FORMS-20385: Stöd för XDP-redigering i Interactive Communications Editor.
* FORMS-10883: Stöd för JSON med XHTML-namnområdestaggar i DoR-generering för korrekt återgivning av RTF-data som skickas via API:er.
* FORMS-21751: Funktioner på arbetsytan - Textspill, gränssnitt för sidbrytning.
* FORMS-22049: Interactive Communications Editor - Migration to Spectrum 2.
* FORMS-22050: Stöd för dynamisk sidnumrering i Interactive Communications Editor.
* FORMS-21606: Public OSGi Render SPI för interaktiv kommunikation.
* FORMS-21613: Transaktionsrapportering och prestandaloggning för Render Interactive Communications SPIs.
* GRANITE-62394: Uppdaterad joda-time till 2.12.7.
* GRANITE-36205: Uppdatera Oak till 1.88.0.
* GRANITE-62020: Förbättra återförsöksprincipen för `RepositoryServiceHttpClient`.
* GRANITE-62169: Uppdatera Commons-lang till 3.19.0.
* SITES-35092: Content Fragments - New mixin and upgrade procedure for semantic search.
* SITES-32319: Delivery OpenAPI - referens till supportsidan.
* SITES-20123: GraphQL: Stöd för upphöjda element i JSON-svar.
* SITES-34744: Ny kortegenskap i Content Fragment-svaret som innehåller data som kan användas för återgivning av en miniatyrbild.
* SITES-34571: Tillåt att uppräkningsfält är tomma.
* SITES-34812: Lagt till möjlighet att hämta ett innehållsfragment utan referenser genom att använda parametern &quot;references&quot; med värdet &quot;none&quot;.
* SITES-35176: Om du checkar ut ett innehållsfragment via Touch-gränssnittet går det nu inte att redigera innehållsfragmentet i den nya redigeraren av andra användare.
* SITES-30371: Stöd för uuid-baserade referensfält har lagts till.
* SITES-19309: Hämta högst 150 referenser när du öppnar guiden Flytta sida.
* SITES-32515: Edge Delivery med Universal Editor - Lägg till stöd för flera fält och sammansatta multifält (tidig åtkomst).
* SITES-33784: Edge Delivery med Universal Editor - Lägg till stöd för ld-json i sidmetadata.
* SITES-34832: Edge Delivery med Universal Editor - Lägg till en offentlig sökväg till ett sidinfoserverletssvar.
* SITES-25893: Edge Delivery med Universal Editor - Lägg till stöd för stark och framhävd textåtergivning i block.
* SITES-26158: Edge Delivery med Universal Editor - Lägg till stöd för tabellmarkeringar i block och kolumner (tidig åtkomst).
* SITES-27949: Edge Delivery with Universal Editor - Make path mapping optional.
* SITES-35811: Använd nytt index i frågor för innehållsfragment.
* SKYOPS-120857: Uppdatera filevault till 4.1.4.
* SKYOPS-118390: Uppdatera JCR-resursen till 3.3.6.
* SKYOPS-121082: Uppdatera versioner av `org.apache.sling.discovery.standalone`, `org.apache.sling.jcr.packageinit` och `org.apache.sling.commons.fsclassloader` sling bundles.

### Åtgärdade problem {#fixed-issues-23320}

* ASSETS-58926: Korrigera funktionen för att ändra videons miniatyrbild i DM.
* ASSETS-58623: Korrigera pe i omnissearch när config finns.
* CQ-4361144: Korrigerat hoppande av innehållsfragment från översättningsjobb.
* CQ-4355446: Korrigerade den olokaliserade strängen i ett översättningsprojekt som inträffade i dialogrutan Avbryt översättningsjobb.
* CQ-4360747: Åtgärda ett fel där repeterbara översättningsjobb skapar tomma nyttolaster och utlöser för ofta.
* GRANITE-61318: Åtgärda ett fel där guiden bara markerar obligatoriska fält på fliken Grundläggande.
* GRANITE-60514: Åtgärda ett fel där schemalagda publikationer stoppades under en pipeline i full hög.
* GRANITE-61019: Åtgärda problem med global katalog vid första körningen efter AEM omstart.
* GRANITE-60456: Åtgärda problem när administratören öppnar en användares egenskapssida.
* SITES-34555: GraphQL - QueryValidationError efter distributioner.
* SITES-35077: Innehållsfragment - Det går inte att avpublicera för fragment med parenteser på grund av felaktig URL-kodning.
* SITES-35374: Content Fragments - Edited Content Fragment disappears after Navigating Back.
* SITES-36130: NPE i `EditorRestrictionsStatusImpl`.
* SITES-35810: NullPointerException i startblocken publishEdgeDeliverySubscriber queue.
* SITES-34368: AEM CIF genererar 12 GraphQL-alias - överskrider Magento 2.4.6-P12-gränsen på 10.
* SITES-36193: Korrigeringar för CCS-anslutning.
* SITES-35169: Ett problem som orsakade felaktig sidnumrering när ogiltiga fragmentresurser returnerades av sökningen har åtgärdats.
* SITES-34574: Korrigerade ett fel där markören i vissa fall inte returnerades av API:t för innehållsfragmentsökning.
* SITES-35520: Korrigerade ett fel som orsakade ClassCastException eller timeout vid försök att publicera innehåll.
* SITES-35210: Korrigerade ett NullPointerException som skulle inträffa vid försök att publicera ett brutet fragment med ett tomt referensfilter.
* SITES-35933: Korrigerade ett fel som skulle resultera i tomma arbetsflöden för begäran om aktivering efter att innehållsfragmentet publicerades.
* SITES-35925: Korrigerade ett fel som gällde korrigering av modeller för innehållsfragment som skulle ta bort egenskaperna &quot;translatable&quot; och &quot;showThumbnail&quot; från modellen.
* SITES-35409: Korrigerade ett fel som förhindrade återpublicering av justerade fragment när en sida flyttades.
* SITES-15757: Korrigerade ett fel som förhindrade återpublicering av justerade sidor när en sida flyttades.
* SITES-34638: Korrigerade ett fel där egenskaper från överordnade sidor inte skulle inkluderas när nya versioner skapades.
* SITES-35071: CSV-export returnerar ofiltrerade resultat när citattecken används vid sökning.
* SITES-32182: Edge Delivery med Universal Editor - åtgärda kodningsproblem med URL:er som innehåller redan kodade frågeparametrar.
* SITES-34324: Edge Delivery with Universal Editor - fix rendering of links with a tel: protocol.
* SITES-35333: Edge Delivery with Universal Editor - fix asset rendition selection for images in page metadata.
* SITES-35549: Edge Delivery med Universal Editor - korrigera dubbelkodade html-entiteter i sidmetadata.

#### AEM Guides {#guides-23320}

* GUIDES-33597: Om ett tomt `prop`-element utan attribut eller värden läggs till i en DITAVAL-fil kan ytterligare `prop`-element inte läggas till.
* GUIDES-33693: När du överför en redigerad bild igen via Experience Manager Guides-gränssnittet uppdateras bildens ursprungliga återgivning, men det tillhörande DITA-innehållet fortsätter att visa den tidigare versionen av bilden.
* GUIDES-35607: Felloggar som genereras när en resurs överförs via Assets-gränssnittet eller när en ny fil skapas från redigeringsgränssnittet, använder felaktigt termen `predecessor` i stället för `successor` i loggmeddelandet.
* GUIDES-37649: När en DITA-karta publiceras med baslinje på AEM Sites (med äldre komponentmappning) publiceras även mappningselementen med attributet `processing-role = resource-only`.

Mer information om de nya och förbättrade funktionerna och problemen som har åtgärdats i den här versionen finns i [Experience Manager Guides-lanseringens färdplan](https://experienceleague.adobe.com/sv/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).


### Kända fel {#known-issues-23320}

* FORMS-22633: Formuläröverföringar kan misslyckas om anpassad kod som är beroende av API:erna för GuideBridge (`getData` eller `getDataXML`) används. Kontakta Adobe Support om du får problem.

### Föråldrade funktioner och API:er {#deprecated-23320}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-23320}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar 31 identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-23320}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.88.0 | [Oak 1.8.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.88/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 &#x200B;](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Apache HTTP-server | 2.4.65 | [Apache HTTP 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Grundläggande komponenter i AEM | 2.30.2 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (standard) | [Node.js-versioner som stöds](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
