---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9303ecadea38d83bd71ed0d440067bae5c419940
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 0%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs de tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 16971 {#release-16971}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsreleasen 16971, som offentliggjordes den 3 juli 2024. Den tidigare underhållsversionen var version 16799.

2024.7.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) för mer information.

### Förbättringar {#enhancements-16971}

* SITES-22948: Ta bort handelsreferenser i grundinnehållet för AEM CS.
* 22141: [Innehållsfragment] SegmentNotFoundException från CFM ModelChangeRepositoryImpl efter OnRC.
* SITES-21893: Image Cropping Issue on Author Instance.
* 21788: [Innehållsfragment] Visa NOTE i CF- och CF-modellredigeraren när uiSchema är aktiverat för modellen.
* SITES-21688: MSM-utrullningen uppdaterar inte XF-sökvägen (Experience fragment) på live-kopieringssidor.
* SITES-21659: Returnera det fullständiga namnet för användaren som skapar/ändrar/replikerar en modellresurs.
* SITES-21609: OpenAPI-slutpunkt för att migrera innehållsfragment från en modell till en annan.
* 21598: [Öppna API] Skapa CFM - returfel om den angivna konfigurationssökvägen inte finns.
* 21491: [Öppna API] CF-slutpunkten för PATCH bör respektera liverelationer på fältnivå.
* 21434: [Öppna API] CF-GETENS slutpunkt ska respektera liverelationer på fältnivå.
* SITES-21415: CF Editor - stöder UUID-referenser.
* 21326: [Öppna API] Ange information om det finns referenser för ett innehållsfragment.
* 21310: [Öppna API] Lägg till ID för innehållsfragment i översättnings-API-svar.
* SITES-20859: CF Open API - Returnera referenser när ett fragment hämtas via sökväg.
* 20687: [Öppna API] Slutpunkt för hämtning av batchbearbetningsstatus.
* 20657: [Öppna API] Ange alternativ för hela match-ord när en sträng ersätts med `FindAndReplace` slutpunkt.
* 20587: [Öppna API] Skapa `COPY` slutpunkt för innehållsfragment.
* 20584: [Öppna API] Optimera hämtning av referenser.
* SITES-2003: [Öppna API] Aktivera gruppbearbetning för API.
* SITES-1976: [Öppna API] Allmänt användargränssnittsschema för villkorliga fält.
* SITES-19556 [Innehållsfragment] Uppdatera uiSchema om det finns när modellen redigeras.
* SITES-18056: [Öppna API] Inkludera referenser när du publicerar ett innehållsfragment till Förhandsgranska.
* SITES-16898: [Schema] OpenAPI-slutpunkt för att migrera innehållsfragment från en modell till en annan.
* SITES-16609: List Launches endpoint.
* SITES-16606: Create Launch Endpoint.
* 21617: [Xwalk] Gör Sidegenskaper/metadata redigerbara i UE.
* SITES-19614: [Xwalk] Sidindelning av kalkylbladsredigerare och oändlig rullning.
* 22163: [Xwalk] Förbättrat stöd för innehåll som hanteras från publiceringsnivå för Edge Delivery Sites.
* 22109: [Xwalk] Förbättrad hantering av efterbearbetning av avancerad textmarkering.
* SITES-2035: [Xwalk] Förbättrad hantering av MSM och Launches.
* 21839: [Xwalk] Förbättrad sökvägsmappning och sanering för innehåll som inte hanteras av Edge Delivery.

### Åtgärdade problem {#fixed-issues-16971}

* CQ-4356898: [Översättning] outOfMemory-fel för CF som innehåller ett ovanligt stort antal länkar.
* CQ-4357055: [Översättning] Automatisk översättning fungerar inte med Rest API.
* CQ-4353931: [Översättning] Lägg till jcr:uuid på översättningskällsidan/xf/resurs när den saknas.
* CQ-4357591: [Översättning] Ändra arbetsflödet Associera JCR:UID så att det fungerar för sidor/XF.
* FORMS-14844: Adaptiv Forms tillåter att formulär skickas trots att reCAPTCHA-verifiering misslyckas.
* FORMS-14984: Forms med CAPTCHA hoppar över validering om &quot;submitMetaData&quot; saknas i skickade data.
* FORMS-14477: Alternativen &quot;Är efter&quot; och &quot;Är före&quot; i regelredigeraren fungerar inte i datumväljarens validering.
* FORMS-14019: Regelredigerarens &quot;Invoke Service&quot;-funktion fungerar inte i Universal Editor.
* FORMS-14336: När inget formulärfält är markerat öppnas redigeraren med fokus på hela formulärelementet.
* FORMS-15061: Loader-cirkeln kvarstår oändligt när tjänstalternativet anropas i regelredigeraren.
* SITES-22457: Källinnehåll uppdateras inte när en lansering som inte är djup initieras.
* 22748: [Innehållsfragment] Förbättra felhanteringen för uppdateringsjobb för innehållsfragment
* 22349: [Innehållsfragment] ContentType för tomma cf-element med flera rader kan inte ändras.
* 22343: [Innehållsfragment] Den semantiska typen &quot;enumeration&quot; är bruten.
* SITES-22194: När omdirigeringen har angetts fungerar inte model.json längre.
* 21953: [Öppna API] Etag ändras baserat på ordningen för validationStatus.
* 21894: [Öppna API] Förbättra valideringen av den överordnade sökvägen när du skapar CF:er.
* 21887: [Öppna API] Ogiltig ETag returnerades av POSTENS variantslutpunkt.
* 21657: [Öppna API] Förbättra valideringen på egenskapen CF Search Path.
* SITES-21949: Ogiltig söknings-API:er returnerar 500.
* SITES-20927: Söknings-API:er returnerar 500 när frågan saknas.
* 20544: [Öppna API] Ändra genereringen av publiceringspaketnamn för att undvika ekningskonflikter.
* SITES-19710: CVE-2022-47937 - Ta bort all användning av org.apache.sling.Commons.json från sidredigeraren.
* SITES-1992: [Tillgänglighet] Väljarknappen för anteckningsfärgruta saknar ett hjälpmedelsnamn.
* SITES-10979: [Tillgänglighet] Etiketten är inte beständig.
* SITES-10962: [Tillgänglighet] Knapp: Knappen har ingen roll.
* SITES-10905: [Tillgänglighet] Den aktiva komponentens tillstånd saknar kontrastförhållande 3 till 1.
* 2974:  [Tillgänglighet] - Vågrät rullning med bredden 320px.
* SITES-22026: Det går inte att flytta Experience Fragments mellan mappar i AEM
* SITES-22106: Funktionsproblem för språkväxling i den nya redigeraren för innehållsfragment
* SITES-21980: Inkonsekvent hantering för UUID-baserade referenstyper.
* SITES-7257: NPE in ThumbnailServlet.

### Kända fel {#known-issues-16971}

Ingen.

### Ändringsmeddelande {#change-notice-16971}

* Från och med september 2024 kommer AEM as a Cloud Service att inaktivera serialiseringen av resurslösare via Sling Model Exporter-ramverket. Se [dokumentationen](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) för mer information.

### Föråldrade funktioner och API:er {#deprecated-16971}

Om du vill veta vad som är föråldrat eller borttaget i AEM as a Cloud Service går du till [Föråldrade och borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Inbäddade tekniker {#embedded-tech-16971}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.64.0 | [Oak API 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| AEM SLING API | 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | 1.4.22-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.25.4 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |
