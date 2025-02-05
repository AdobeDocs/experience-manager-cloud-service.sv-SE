---
title: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsversionsinformation för  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 77d8ebeaa3914f4a91d2cf27ccc5b048e64d6b38
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 0%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs de tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 19352 {#19352}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 19352, som offentliggjordes den 5 februari 2025. Den tidigare underhållsutgåvan släpptes 19149.

Funktionsaktiveringen i 2025.2.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-19352}

* FORMS-13998: Lägg till dragspelskomponent.
* FORMS-17913: Lägg till kortvariant för alternativknappar.
* FORMS-17333: Aktivera HTML-e-postmallar AEM formulärskickning.
* FORMS-17702: Aktivera PDF som genereras i API:er för utdatasynkronisering som ska överföras till Azure Blob Storage.
* SITES-28282: Edge Delivery med Universal Editor: Ange grundsökväg, webbplatsnamn och organisation som sidinformation för alla sidor.
* SITES-27055: Edge Delivery med Universal Editor: Support query parameters in reverse proxy servlet.
* SITES-26796: Edge Delivery med Universal Editor: Stöd för anpassade kolumner för taxonomikalkylbladet.
* SITES-26087: Edge Delivery med Universal Editor: Stöd för CSV-export för kalkylblad.
* SITES-26265: Edge Delivery med Universal Editor: Visa TA-kontot för integrering med Edge Delivery i konfigurationsgränssnittet.
* SITES-20372: Edge Delivery med Universal Editor: Enable basic MSM use case for spreadsheets.
* SITES-26681: Edge Delivery med Universal Editor: Stöd för parametern ?sheet= för taxonomikalkylblad på författaren.
* SITES-26479: [Schema] Contents-Fragment Model Scheduled Publication Status Endpoint.
* SITES-25944: [Livecopy Overview] lägger till statusen&quot;live copy up to date with limited inherance&quot;.
* SITES-28713: [V2] Lägg till stöd för strukturerade data i innehållsskrapa.
* SITES-27896: CommentsTab auto opening on notification.
* SITES-26720: Användaren ska inte kunna välja en hel samling från resursväljaren.
* SITES-27875: Gör alla redigerbara objekt i en behållare flyttbara som standard.
* SITES-28340: Dark Alley Universal Editor Service Plugin.
* SITES-26098: Möjlighet att undvika publicering av refererade sidor när en Content-Fragment publiceras.
* SITES-27789: Stöd för dataattributets data-aue-component i DOM.
* SITES-25997: Förbättra variationer med stöd för ändrade datum.
* SITES-28023: GraphQL-utdata för resursreferenser (databas + resurs-ID).
* SITES-26058: Content-Fragment Model Scheduled Publication Status Endpoint.
* SITES-25108: Modellmigrering för UUID-referenser.
* SITES-26630: Content-Fragment Scheduled Publication Status Endpoint för flera innehållsfragment.
* SITES-23432: Förbättra möjligheten att ta bort referenser.
* SITES-25797: Stöd för externa resursreferenser - GraphQL.
* SITES-17514: Ta bort slutpunktsförbättringar för att avpublicera innehållsfragment.
* SITES-14633: Verifiera Content-Fragment-modellen att skapa nyttolaster före installation - Torr körning.

### Åtgärdade problem {#fixed-issues-19352}

* SITES-28415: Edge Delivery med Universal Editor: Knappen Korrigera öppna egenskaper för kalkylblad.
* SITES-26669: Edge Delivery med Universal Editor: Korrigera problem vid överföring av CSV-filer kodade i UTF-8 med en BOM som kalkylblad.
* SITES-26543: Edge Delivery med Universal Editor: Korrigera tomma block utan att modellåterge felaktig kod.
* SITES-26857: Edge Delivery med Universal Editor: Åtgärda platsautentiseringstoken som visas i användargränssnittet för filbaserade konfigurationer.
* SITES-26662: Edge Delivery med Universal Editor: Åtgärda problem med skiftlägeskänsliga massmetadata.
* SITES-28133: Publish to &quot;Preview&quot; orsakar att innehåll är tillgängligt i produktionen.
* SITES-27187: Schemalagd sid-/resursaktivering med referenser (experimentella) saknar publiceringsreferenser.
* SITES-27264: 2 Content-Fragment-LiveCopy-Creation related Selenium tests are consistent on master.
* SITES-26559: Fäst frågan för Content-Fragment-modeller till cqPageLucene-index.
* SITES-24469: Det interaktiva elementet går inte att komma åt via tangentbordet.
* SITES-24518: Knapparna Namn och Modell i tabellen Överordnad referens är inte tillgängliga via tangentbordet.
* SITES-27937: UISchema-begränsningar anges till null efter att modellen har uppdaterats.
* SITES-27852: Modellen UISchema saknar kategoriseringar.
* SITES-27904: MetadataSchema saknas i list/sök efter Content-Fragment-modeller för fullständig projektion.
* SITES-26827: Listing Fragments blir en oändlig slinga.
* SITES-27678: [Performance] Förhindrar onödig hämtning av _references.
* SITES-27589: UUID-uppgraderingsfel för innehållsfragmentmodeller med flera referensfält för innehåll/fragment.
* SITES-26679: Avpublicera modeller för innehållsfragment bör endast validera publicerade referenser.
* SITES-26666: referencesTree och references endpoint returnerade med olika resultat.
* SITES-26499: Felaktig ordning för taggfältets värde i GET fragment och PATCH randomiserar ordningen.
* SITES-26585: Åtgärda ett litet beskrivningsfel i schemat.
* SITES-26647: Verifieringen av slutpunkten och referensen UnpublishFragments kan misslyckas för icke-adminanvändare.
* SITES-26458: [Sök i Content-Fragment-modell] Korrigera filtrering efter replikeringsstatus.
* SITES-23513: [Modellredigeraren för innehållsfragment] Valideringen misslyckas för egenskapen Fragmentreferens - Tillåten fragmentmodell.
* SITES-26575: PreviewStatus bör uppdateras om du avpublicerar ett fragment från förhandsvisningen.
* SITES-26571: Det går inte att spara sidreferenser när FT_SITES-12435 är aktiverat.
* SITES-26660: Versionsjämförelsen för innehållsfragment kan brytas när @ContentType är av strängtyp.
* SITES-26626: customErrorMessage saknas i numeriska och booleska fält.
* SITES-26268: Felaktig statuskod returnerades om en referens är ogiltig när ett fragment skapades.

### Kända fel {#known-issues-19352}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-19352}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-19352}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar 36 identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-19352}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.72.0 | [Oak API 1.72.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | 1.4.24-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.27.0 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |
