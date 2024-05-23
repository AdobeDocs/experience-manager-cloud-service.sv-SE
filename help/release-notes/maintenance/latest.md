---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: d107f40c4bc43837db9d8fab3d06627d9e930620
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 0%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 16357 {#release-16357}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 16357, som offentliggjordes den 22 maj 2024. Den tidigare underhållsversionen var version 16145.

2024.5.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) för mer information.

### Förbättringar {#enhancements-16357}

* SITES-19579: Java API för att migrera innehållsfragment från en modell till en annan.
* SITES-19698: [Öppna API] Skapa läsåtgärd för att hantera ett UI-schema per modell i OpenAPI-definitionen.
* SITES-19834: Adobe I/O-händelse saknar id för publicering/avpublicering.
* SITES-20146: Aktivera förhandsgranskningsversion/Jämför för flyttade sidor.
* SITES-19973: Implementering av CFM Search API.
* SITES-2033: Förbättra valideringen när du skapar innehållsfragment.
* SITES-20334: Förbättra valideringen när du redigerar modeller för innehållsfragment.
* SITES-20585: Förbättra API:t för innehållsfragmentsökning för att filtrera efter språkområde.
* SITES-20594: Returnera det fullständiga namnet för användaren som skapar/ändrar/replikerar en resurs.
* SITES-2001: [OpenAPI] Uppdatera CF Search API så att endast underordnade innehållsfragment kan hämtas.
* 20656: [BE] Ange ett alternativ som matchar skiftläget när en sträng ersätts.
* SITES-20405: [Xwalk] Stöd för mimeType för radkomprimering.
* SITES-17854: Stöd för UUID för CF- och resursreferenser (Pfizer MVP).
* SITES-19555: Simple Model API for UI schema.
* SITES-19611: [Öppna API] Skapa skriv-/uppdateringsåtgärd för att hantera ett UI-schema per modell i OpenAPI-definitionen.
* SITES-19614: [Xwalk] Sidnumrering av kalkylblad/oändlig rullning.
* SITES-2005: Författarpipelinen ska ha en konfigurerbar händelsefördröjning.
* SITES-20121: Allow defaultValue for enum fields.
* 20342: [Backend] Publicera på mappnivå - lägg till filter för att bara publicera CF:er.
* SITES-20355: Ta bort innehållsfragmentmodeller och API-behörighetsservrar.
* SITES-20387: Om du navigerar i tagadmin beräknas alltid tagganvändningen.
* 20495: [BE] Möjlighet att få behörighet att publicera på mappnivå.
* 20653: [Xwalk] lägg till experimentellt startdatum och slutdatum.
* SITES-2066: [Xwalk] Experimentets ska vara inaktiverat som standard vid redigering.
* 20752: [cq-wcm-core] Apple Launches for CFs.
* SITES-20946: Lägg till tagg som en egenskap i LIST-modellens slutpunkt.
* SITES-20947: [beständighet] hämta underuppgift efter innehållets fragment-ID.
* SITES-21012: Metadata-schema för sammanfogningsmodell till produkt.
* SITES-21769: Använd sökvägsprefixet /jcr:id/ för att hämta resurs-för-id.
* ASSETS-30379: DRM License check walks entire tree of assets being downloaded.
* ASSETS-35535: [DAA-adapterfel] Tomma resurshämtningar måste ignoreras för v1-händelser.
* 21550: [Xwalk] Anpassade metadata: tal, datum, tid, tidsfält.
* SITES-20149: RTC: [cq-wcm-launches-core] Exportera nytt API för startprogram för CF:er.
* SITES-20150: RTC: [cq-command] Lägg till nya metoder i befintligt API.
* SITES-20451: Add sidecar plugin to wcm-commons.
* 2049: [MSM][Async] Extrahera koden från AsyncOperationServlet till en verktygsklass.
* SITES-20763: Uppdatera API-slutpunkter för leverans i webbplatsintegrering.
* SITES-20583: Lägg till tagg som egenskap i `LIST`/sökfragment.
* CQ-4356445: Event Producer &amp; Schema Implementation.
* CQ-4356625: Förbättra behörighetskontrollen för language-opyrendercondition.jsp.
* CQ-4356629: Förbättra auktoriseringskontrollen i isWorkflowUser rendercondition.
* CQ-4356934: Förenkla API:t för RequestProcessor när du arbetar med ResponseEntities.
* CQ-4357214: Begärandeprocessorer får inte vara beroende av serverlogik.
* SITES-16392: Det gick inte att starta programmet, det får inte lämna skräpinnehåll.
* 20238: [RTC] Pfizer MVP - Lägg till CF API för att matcha CF-sökvägar till ID:n och vice versa.
* SITES-2043: [CF][launches] Prestandaförbättringar för Cloud Service på sidoport.
* SITES-2044: [CF][launches] Asynkron redigering av nyttolastsimplementering till Cloud Service på sidoporten.
* FORMS-7483: AEM Forms JSON Schema Parser har nu stöd för JSON-schema (2020-12).
* FORMS-13209: En hanterare ingår för att åsidosätta adaptiva Forms standardhanterare för skickning av lyckade och misslyckade överföringar. Du kan konfigurera de här hanterarna via Adaptiv Forms regelredigerare.
* FORMS-13612: Skärmläsare läser nu felmeddelanden, korta beskrivningar och långa beskrivningar för fält i viktiga komponentbaserade adaptiva Forms. Dessutom har stöd lagts till för att göra anpassade formulärindata ogiltiga när formuläret innehåller fel och inte är giltigt för att skickas.
* FORMS-12052: En formulärförfattare kan nu använda anpassade funktioner för att förbearbeta data innan de skickas in.
* FORMS-11295: Stöd för SHA256 har lagts till med ECDSA-algoritmen för AEM Forms Digital Signature.
* FORMS-9432: En ytterligare innehållstyp (REST Endpoint) har lagts till i molnkonfigurationen för datakällan. Den gör det möjligt att skicka data i nyckelvärdepar till en autentiserad slutpunkt.

### Åtgärdade problem {#fixed-issues-16357}

* SITES-20608: Experience Fragment:er med personalisering aktiverat när de ingår i en mall orsakar en oändlig slinga.
* SITES-1954: [Xwalk] Kalkylbladsredigeraren: Det går inte att tömma en cell.
* SITES-19971: Korrigering av ett CFM som innehåller flikar ändrar fältordningen.
* SITES-20168: Content Fragment Model `locked` fältet har inte uppdaterats korrekt.
* SITES-20522: Corrupted Content Fragments break /adobe/sites/cf/fragments endpoint.
* SITES-20816: CF OpenAPI - utdatainkonsekvens med saknad modell för refererat fragment.
* SITES-21239: Remove ContentFragmentSearchService cirkelberoende.
* SITES-20582: Sökning och listning av innehållsfragment bör tillåta djupet 0.
* SITES-20559: [MSM][XF][Lufthansa] Referenser uppdateras inte när Experience Fragments distribueras från mallar/språk till land/språk.
* SITES-17772: AEM: Användare med administratörsgrupp kan inte låsa upp sidor som en annan användare har låst.
* SITES-2001: [Xwalk] Avsnittsmetadata stöder inte flervärdesegenskaper.
* 21391: [OpenAPI-händelse] Inga händelser utlöses när titeln eller taggarna (egenskaperna) för en Content Fragment-modell ändras.
* SKYOPS-73234: Ökning av antalet fel i felloggen i AEM Assets Global DAM-programuppgradering till AEM version 1553 och PR ID 35362.
* SKYOPS-75341: NosådanMethodError i distribution av Crosswalk-paket.
* SCRNS-3945: Skyline: Olokaliserad &quot;Scheduled&quot;-sträng i skärmar.
* SITES-20586: Mallen&quot;Published&quot; timestamp not updated.
* SITES-16674: Kryssrutan Inherit rollout configs fungerar inte med live copy-egenskaper.
* SITES-18680: Det går inte att hämta referensvariationer i en grafisk fråga (Apple).
* 21233: [CoreCmp] Dragspelsfel för GS1 US efter uppgradering till 15860.
* SITES-20367: Issue with Deleting Launches in AEM.
* CQ-4357161: AEM Inbox Nyttolastskärm returnerar 404.
* SITES-20214: AEM problem med konfigurationssekvensen för utrullning vid sparande.
* SITES-20364: 302 dirigerar om Arbeta inte med väljaren i URL.
* SITES-20547: Trunkerade banor i listan Uteslutna sökvägar i Live Copy på AEM as a Cloud Service.
* SITES-20691: Experience Fragment Template Restriction Not Honoring cq:allowedTemplates.
* SITES-21122: AEM CS Live Copy Defect with Content Fragments.
* ASSETS-38723: NPE genereras av MetadataRulesProviderImpl när getReadRulesForMetadataChildNodes() anropas innan this.readRules initieras.
* SITES-11727: [GQL] Fullständig hydrering av innehållsfragmentreferenser saknar data.
* SITES-19462: Resurssökning fungerar inte som den ska i AEM Cloud.
* SITES-19994: Close button clocking when users try to close Content Fragment.
* SITES-20029: Versioner för innehållsfragment skapas direkt efter att de stängts utan att innehållet ändras.
* SITES-21316: Fragment Preview: preview failed due to code changes from SITES-11727.
* SITES-20023: Fileupload fungerar inte för Remote(Next gen assets)-resurser i multifält.
* ASSETS-37611: Arbetsflödet&quot;Request to Complete Move Operation&quot; aktiveras för opublicerade resurser.
* CQ-4357278: DispatcherServlet returnerar NPE om getRequestBodyType returnerar null.
* CQ-4357279: Bearbetning av begäranden misslyckas när det inte finns någon pathInfo för en begäran.
* 20496: [Xwalk] Inga egenskapsalternativ när du väljer kalkylblad i webbplatsadministratören.
* FORMS-13827: I den adaptiva Forms-regelredigeraren stöder WHEN-åtgärden för närvarande inte olika typer av fält med datumväljare.
* FORMS-13786: I den anpassningsbara Forms-regelredigeraren fungerar inte dra och släpp-funktionen för anpassade funktioner.
* FORMS-13587: I den adaptiva Forms-redigeraren fungerar inte enhetsemulatorfunktionen korrekt för Core Components-baserade Adaptive Forms.
* FORMS-14376 När en användare trycker på Återställ-knappen resulterar det i konsolfel om den statiska texten är markerad som obunden.
* FORMS-13801: Även om villkorskomponenten är inaktiverad är motsvarande kryssruta fortfarande aktiverad.
* FORMS-11952: När ett formulär skickas börjar den Skicka-URL som genereras av formuläret med /content/ i stället för /portale/, vilket dirigerar om begäran fel. Detta förhindrar att begäran når de avsedda servrarna.
* FORMS-13616: Datumväljaren visar det aktuella datumet som en dag efter, troligen på grund av ett tidszonsproblem, och det är svårt att ställa in rätt datumformat på grund av den här inkonsekvensen och ett ytterligare problem med visningsmönster.
* FORMS-13829: Listrutan, som styrs av regler för att efterlikna alternativknappsfunktioner, fylls inte i korrekt när en markering har rensats och markerats igen. Det önskade beteendet är att enskilda kryssrutor fungerar som alternativknappar, vilket innebär att endast en markering åt gången tillåts och att alla alternativ avmarkeras.
* FORMS-14244: I ett adaptivt formulär som baseras på en XDP-fil med inbäddade skript i kryssrutor körs inte skripten för element efter sådana kryssrutor.
* FORMS-14267: Användarna får konsekventa timeoutfel när de skickar API-begäranden i utvecklings-, scen- och produktionsmiljöer. Dessa begäranden är relaterade till generering av PDF, ibland med data ifyllda med databindning. Säkerhetsluckan resulterar i en process som så småningom tar slut men som lyckas när du försöker igen efter felet.
* FORMS-11589: För användare som bara har AEM Forms-lösningen (utan andra lösningar) fungerar inte frontpipeline.
* FORMS-13896: I DoR-utdata (Document of Record) visas datum och tal på arabiska oavsett om indata sammanfogas med gregorianska siffror.

### Kända fel {#known-issues-16357}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-16357}

Om du vill veta vad som är föråldrat eller borttaget i AEM as a Cloud Service kan du läsa [Föråldrade och borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Inbäddade tekniker {#embedded-tech-16357}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.62.0 | [API för Oak API 1.62.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | 1.4.22-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.25.4 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |
