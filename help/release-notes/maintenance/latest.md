---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: d16d908d39df3c7d72dc48ac877c1543d2442416
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 0%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 15262 {#release-15262}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 15262, som offentliggjordes den 6 mars 2024. Den tidigare underhållsversionen var version 14697.

2024.3.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) för mer information.

### Förbättringar {#enhancements-15262}

* ASSETS-30632: En separat kolumn för publiceringsstatus för Brand Portal har lagts till i listvyn.
* ASSETS-30934: Stöd för `Iptc4xmpCore:AltTextAccessibility` och `Iptc4xmpCore:ExtDescrAccessibility` egenskaper till Resursmetadataredigeraren.
* ASSETS-31297: Förbättra kontrollerna för att förhindra att kopierade resurser tas bort från dynamiska medier.
* ASSETS-33246: Definition av versionsindex `damAssetLucene-10`.
* ASSETS-33590: Lägg till stöd för webbåtergivningar för videor i bearbetningsprofiler.
* GRANITE-36205: Uppdatera ekversionen till 1.60-T2024013102219-0cde853.
* SITES-19326: Uppdatera länkarna i Assets UI så att CF öppnas i den nya CF Editor.
* GUIDES-12945: AI-baserade smarta förslag för att lägga till innehållsreferenser när innehåll redigeras
* GUIDES-12706: Den förbättrade funktionen för versionshistorik i Web Editor
* GUIDES-14948: Förbättrad användarupplevelse på panelen Översättning
* GUIDES-8782: Förbättrad söklogik i dialogrutan Infoga element
* GUIDES-14681: Möjlighet att publicera flera förinställningar med dynamiska baslinjer
* En fullständig lista över förbättringar i AEM finns i: [Nyheter i AEM](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/whats-new-2024-2-0.html?lang=en#release-info)

### Åtgärdade problem {#fixed-issues-15262}

* ASSETS-15977: Ta bort inaktuella v1-sökhändelser och pipeline-producent.
* ASSETS-18088: Uppgradera batik-biblioteksberoenden till 1.17.
* ASSETS-21965: Arbetsflödet för återskrivning av metadata får bara startas vid ändringar av metadata för resurser.
* ASSETS-26368: Schemalagda massimportjobb har inte tagits bort om jobbkonfigurationen inte finns.
* ASSETS-26549: Resurser/noder med&quot;jcr:lastModifiedBy&quot;:&quot;workflow-process-service&quot; visas som&quot;extern användare&quot; i listvyn.
* ASSETS-26842: Uppdatera Firefly-text till att läsa App Builder i Bearbeta profil.
* ASSETS-28708: Mycket långsamt svar för vissa IMS-tokenbegäranden.
* ASSETS-28767: Inkonsekvent publiceringstillstånd för resurser om mappen innehåller large no. av publicerade tillgångar.
* ASSETS-29011: Smart beskärning visas för skrivskyddade användare.
* ASSETS-29348: AssetMoveEventHandler kan använda för mycket minne.
* ASSETS-29738: Resursöverföringsbegränsningen misslyckas med NullPointerException för woff-filer.
* ASSETS-30068: Massimportera väsentliga resurser för att inkludera statusen COMPLETED_WITH_ERROR för&quot;jobbet har slutförts, men med fel&quot;.
* ASSETS-30261: Felaktigt imsUserId skickades till pipeline för resurshändelser.
* ASSETS-30538: Alternativet Visa sida saknas efter att en PDF-fil har flyttats.
* ASSETS-30626: Det gick inte att skapa leveransbegäran som rapporterats för resurser med tomt assetId.
* ASSETS-30756: Åtgärden för guiden Flytta resurs misslyckas när mappnamnet slutar i html.
* ASSETS-30810: Sanera taggar innan du återger en äldre YouTube-konfiguration.
* ASSETS-31015: Det går inte att överföra resurser med filnamnstillägget .msg.
* ASSETS-31038: Aktivitetshändelser som tas emot av meddelandetjänsten bearbetas inte.
* ASSETS-31097: Inaktivera Async Copy för WCM-innehåll för att undvika genomgående frågevarningar.
* ASSETS-31256: Resurser/noder med&quot;jcr:lastModifiedBy&quot;:&quot;workflow-process-service&quot; visas som&quot;extern användare&quot; i listvyn.
* ASSETS-31260: Listrutan Formulär för resursmetadata fungerar inte korrekt när den nedrullningsbara menyn JSON har en stor lista.
* ASSETS-31280: Gör så att resurser hämtas i en förenklad struktur när de läggs till i en samling.
* ASSETS-31301: `dynamicmedia_sly.js` kan inte instansieras korrekt av Use API.
* ASSETS-31330: ko_KR: Olokaliserade strängar i undertexter och ljudspår.
* ASSETS-31405: InDesign serverbearbetning misslyckas för layouter med stor InDesign.
* ASSETS-31570: Enhetligt gränssnitt - resursinformationen &quot;Spara och stäng&quot;, &quot;Avbryt&quot;-knapparna måste tryckas ned mer än en gång för att fungera.
* ASSETS-31673: Massimport misslyckades för stora Dropbox-filer.
* ASSETS-32108: AEM Assets sparar inte användardefinierad kortstorlek i visningsinställningarna.
* ASSETS-32230: Uppgradera lägsta runtime-version av paketet com.adobe.aem.repoapi.
* ASSETS-32544: Export av metadata misslyckas ibland.
* ASSETS-32679: Cachelagring av resursförhandsvisningar (PDF).
* ASSETS-32754: Det går inte att tilldela uppgifter till användare som inte har loggat in tidigare.
* ASSETS-32755: Konfigurera com/adobe/cq/dam/assetmove-jobbämne för att använda en ordnad kö.
* ASSETS-32899: Det går mycket långsamt att söka i samlingar.
* ASSETS-33098: AEM Assets sökfacets &quot;Tags predikate&quot; fungerar inte som förväntat.
* ASSETS-33454: Aktiviteten Granska uppgift och kommentarer visas inte i tidslinjen.
* ASSETS-34088: PDF preview fungerar inte på AEM Assets.
* ASSETS-34155: Dynamic Media - Updated AEM Viewers / 2024.1.0.
* ASSETS-34684: Hantera multivalue dc:title i innehållsträdet.
* ASSETS-34789: Åtgärda normaliseringsproblem vid kontroll av filnamnskonflikt.
* DXML-13276: AEM stödlinjer - integrera index i GraniteContent och ta bort dem från biblioteket.
* GRANITE-47995: Borttagningsåtgärder kan misslyckas på grund av konflikter med egenskapen &quot;cq:isDelised&quot;.
* GRANITE-48079: Aktivera POST-begäranden för OAuth-onlinetokenvalidering.
* GRANITE-48143: Uppgradera org.apache.sling.resourceemerger till 1.4.4.
* GRANITE-49031: Uppdatering till Jackson 2.16.1.
* SCRNS-3961: Skärmar - Sekvenskanal: Jquery-animering som används i Tona-övergång leder till svart skärm.
* SITES-15868: Förbättra prestanda för att lista fragment.
* SITES-16079: `/fragments/{id}/references` började returnera dubbletter.
* SITES-16118: Om ett fragment har korrigerats och ett fragmentfält saknas i modellen genereras ett undantag.
* SITES-16121: Ett undantag genereras vid hämtning av ett modelldatumfält.
* SITES-16207: Åtgärden POST /adobe/sites/cf/models returnerar två olika OK-statuskoder.
* SITES-17361: Bädda in Jsoup igen i webbplatsernas headless-paket.
* SITES-17768: GraphQL to output Dynamic Media URL for assets referenced in Content Fragments.
* SKYOPS-66622: Författardistribution kraschar efter körning av en pipeline som stöder buildTransform.
* SKYOPS-69977: Adaptiv bildserver läser inte in bilden efter den senaste uppdateringen.
* GUIDES-15045: Stavningskontrollen i redigeraren tillåter inte val av förslag.
* GUIDES-14968: Den globala navigeringsknappen fungerar inte och instrumentpanelen kan inte läsas in.
* GUIDES-14943: I Native PDF går det inte att använda anpassade attribut i villkorsförinställningar för Native PDF.
* GUIDES-15085: Vid publicering i PDF löses inte nyckelreferenser i december 2023-utgåvan av Adobe Experience Manager Guides.
* GUIDES-13486: **Baslinjefilter** filer fungerar inte med Filnamn i Web Editor.
* En fullständig lista över problem som har åtgärdats AEM guiderna finns i: [Åtgärdade problem AEM stödlinjer](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/fixed-issues-2024-2-0.html?lang=en#release-info)

### Kända fel {#known-issues-15262}

* ASSETS-35923: `UnsupportedClassVersionError` i CM-pipeline Bygg steg efter uppgradering `aem-sdk-api` version till `2024.2.15262.20240224T002940Z-231200`. **Kräver kundåtgärd för att ange CM Java-versionen till 11**, se [Bygg miljö / Ställa in JDK-versionen av Maven](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/build-environment-details.html?lang=en#alternate-maven-jdk-version)
* ASSETS-35860: Felaktig konvertering av tidszon i AEM Assets kolumnvy.
* SCRNS-4171: Windows-skärmar blir tomma och slutar fungera när du uppgraderar till 15262 och publicerar en kanal.
* GRANITE-50774: GraniteContent bör använda deterministisk ordning för egenskapsvärden vid initieringstidpunkten.

### Ändringsmeddelande {#change-notice-15262}

**Åtgärder krävs**

#### Ange CM Java-versionen till 11 {#set-java-version-11}

Den nya versionen av aem-sdk-api innehåller klasser som kompilerats med ett Java 11-mål, vilket inte är kompatibelt med JDK version 1.8 som är standard i Creative Manager Build-miljön. Denna uppdatering kräver att Maven körs med JDK 11.

Vi rekommenderar att man lägger till en `.cloudmanager/java-version` till roten av Git-rapporten med innehållet: `11`. [Bygg miljö / Ställa in JDK-versionen av Maven](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/build-environment-details.html?lang=en#alternate-maven-jdk-version)

#### Uppdatera aem-cloud-testing-clients till 1.2.1 {#update-aem-cloud-testing-clients}

Kommande ändringar kräver biblioteket [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) som används i dina anpassade funktionstester för att uppdateras till åtminstone en version **1.2.1**

Se till att ditt beroende `it.tests/pom.xml` har uppdaterats.

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

Denna ändring kommer att krävas efter den 6 april 2024.

Om du inte uppdaterar beroendebiblioteket kommer det att uppstå ett pipeline-fel i steget&quot;Custom Functional Testing&quot;.

### Inbäddade tekniker {#embedded-tech-15262}

| Teknik | Version | Länk |
|---|---|---|
| AEM | 1.60-T20240131102219-0cde853 | [Oak API 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| AEM SLING API | Version 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | Version 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | Version 2.23.4 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |
