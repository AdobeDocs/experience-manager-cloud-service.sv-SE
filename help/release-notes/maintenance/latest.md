---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 1a128e35be06d018ec25fb0e6a479cfd0d242dbd
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 0%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 14227 {#release-14227}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 14227, som offentliggjordes den 9 november 2023. Den här underhållsversionen är en uppdatering från den tidigare underhållsversionen 14029. Underhållsutgåva 14227 ersätter 14157 för att åtgärda ett problem.

2023.11.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) för mer information.

### Förbättringar {#enhancements-14227}

<!--* ASSETS-29631: Assets Cloud: Use dam:roles for secure delivery/search.-->
* CQ-4354515: Translations: Option to Suppress translation of referenced resources.
* FORMS-9993: Definiera steg för att flytta Forms Core-komponenter till Skyline.
* FORMS-10570: Inbyggt EC API:er i API - första routern.
* GRANITE-48143: Uppgradera Sling ResourceMerger till 1.4.4.
* SITES-14874: Eventing: Expandera CFM-trädet för modellhändelser för att inkludera metadataändringar.
* SITES-2719: Content Fragments: Tagging support for Content Fragment Variations (re-enabled).
* SITES-3619: Innehållsfragment: GraphQL CF-varianttaggar returnerar i JSON och filtrerar efter varianttagg (återaktiverat).
* SITES-13750: Content Fragments: Delete tags for a Content Fragment Model.
* SITES-13920: Content Fragments: Support for minItems config for multiple fields (prerelease).
* SITES-14080: Content Fragments: Delete tag of a Content Fragment Variation.
* SITES-14770: Innehållsfragment: Fragmentvarianten ska innehålla egenskapen fieldTags.
* SITES-15356: Content Fragments: Returnerar tagg som svarshuvud när en resurs skapas.
* SITES-15357: Content Fragments: Allow publishing of fragments without their references.
* SITES-15938: Content Fragments: Missing content reference metadata.
* SITES-16078: Content Fragments: Fill in the validation result property of the variation when a fragment is hämtad.
* SITES-16545: Innehållsfragment: Lägg till slutpunkt för hämtning av referenser för variationen för ett innehållsfragment.
* SITES-16853: Content Fragments: Remove /adobe/sites/cf/fragments/{fragmentId}/variation/{name}/tags slutpunkt.

### Åtgärdade problem {#fixed-issues-14227}

* Flera tillgänglighetsproblem har åtgärdats
* ASSETS-31015: Det går inte att överföra filer till Assets med okända filtillägg.
* ASSETS-24739: Inaktivera den anpassade åtgärdsslutpunkten Frame.io vid publicering.
* CMGR-49845: Innehållsomformning: Problem med att identifiera rätt rotsökväg för angiven kontrollpunkt.
* CMGR-49709: Innehållsomformning: Uppdatera egenskapsfiltret om du vill ignorera ytterligare egenskaper.
* CQ-4354503: Adobe IMS-konfiguration tas bort slumpmässigt.
* CQ-4354414: ConfigurationReplicationEventHandler skapar många enskilda tömningsåtgärder.
* CQ-4354401: Översättningar: Resurser som skapats av projekt måste sparas innan resursbearbetningen startar.
* CQ-4354430: Översättningar: Hämtar ett fel när resurser som inte ingår i en språkmappstruktur läggs till i ett översättningsprojekt.
* CQ-4354412: Översättningar: Om översättningsjobbsinnehåll tas bort tas inte allt refererat innehåll bort.
* CQ-4354636: Översättningar: Att skapa en språkkopia på språkets rotnivå justerar inte sökvägarna på sidan.
* CQ-4354700: Arbetsflöden: Arbetsflödets nyttolastskärm läses inte in.
* CQ-4354834: Arbetsflöden: Det går inte att lägga till kommentarer i inkorg för arbetsflöde.
* FORMS-11302: Rubriken på komponenten som redigeras i RTE visas felaktigt i den adaptiva formulärredigeraren > Regelredigeraren.
* GRANITE-45706: i18n-import misslyckas om nyckelvärdet har &quot;kappa&quot;) och &quot;katt&quot;.
* SITES-14156: Eventing: Publish events skickas inte alltid.
* SITES-14520: GraphQL: Dåliga prestanda med paginerade grafikfrågor på grund av FT_SITES-2719.
* SITES-16444: GraphQL: DataFetchingException för samma namnfält som saknas i GraphQL-frågan.
* SITES-16225: GraphQL: Innehållstyper för modellfält och RTE-fragmentfält som returneras av Java API är inte korrekta.
* SITES-15373: Content Fragments: The /adobe/sites/cf/fragments/{fragmentId}/variation/{name}/tags slutpunkten använder inte rätt resursnamnkonventioner.
* SITES-15709: Content Fragments: Create Model endpoint issue when creating Boolean Field.
* SITES-15727: Content Fragments: Field of type &quot;Tag&quot; kan bara läggas till en gång i modellredigeraren.
* SITES-15782: Content Fragments: Missing unique property from field model of Enumeration type.
* SITES-15786: Content Fragments: Content Fragment cannot be created in folder containing &#39;.
* SITES-15790: Content Fragments: Update Location header for Version Creation.
* SITES-15923: Innehållsfragment: CF Admin visar inte alla mappar.
* SITES-15987: Content Fragments: Getting 500 while creating variant.
* SITES-16067: Content Fragments: MIME-typen för fält med långt textfragment kan inte ändras.
* SITES-16074: Content Fragments: Taggfält som inte är String[] kan inte hämtas från JCR.
* SITES-16079: Content Fragments: /fragments/{id}/references började returnera dubbletter.
* SITES-16118: Innehållsfragment: Om ett fragment är patchat och ett fragmentfält saknas i modellen genereras ett undantag.
* SITES-16119: Innehållsfragment: Om fragmentets metadata innehåller okända fält genereras ett undantag.
* SITES-16121: Innehållsfragment: Ett undantag genereras vid hämtning av ett modelldatumfält.
* SITES-16123: Innehållsfragment: Om en resurs inte är ett innehållsfragment genereras ett undantag vid slutpunkten för get fragments.
* SITES-16208: Content Fragments: ContentFragmentModelIdentifier visar en vilseledande title-egenskap.
* SITES-16707: Content Fragments: Content Fragment Models data types are not correctly read.
* SITES-16818: Content Fragments: Perform delete only when tags present.
* SITES-16207: Innehållsfragment: Åtgärden POST /adobe/sites/cf/models returnerar två olika OK-statuskoder.
* SITES-15616: Innehållsfragment: Publiceringsslutpunkten publicerar inte ibland alla referenser för ett innehållsfragment.
* SITES-16027: Innehållsfragment: Variationsreferensinformation saknas i fragmentsvar.
* SITES-16243: Innehållsfragment: Sök och ersätt fungerar inte med fält med återgivning som: Flera.
* SITES-16250: Content Fragments: Patching a CF returnerar ibland ett felaktigt tagghuvud.
* SITES-16686: Content Fragments: Content Fragment non-fragment references serialized when parent reference is at max depth.
* SITES-12880: Fast-Track: Korrigera lokalisering för platser > Konfigurationsanalys.
* SITES-16103: Experience Fragments: Målalternativen visas inte under Cloud Service på grund av ett konsolfel.
* SITES-16001: MSM: Möjlighet att utesluta komponenter för flera fält från utrullningskonfigurationen när Live Copy skapas.
* SITES-16559: MSM: Rollout configs removed during rollout process for experience fragments.
* SITES-16797: MSM: Fast återaktiveringsarv för ett CF-fält i Redigeraren.
* SITES-16273: Page Editor: Copy paste error inside aem sites pages from the clipboard.
* SITES-16126: Sites Admin: Det tar lång tid för icke-administratörer att redigera efter SITES-10288.
* FORMS-10534: Ett fel inträffar i regelredigeraren när alternativet Boolean-operand väljs.
* FORMS-10248: I en adaptiv form, när datavärdet är av typen Boolean, kan reglerna inte ange korrekta värden för alternativknappar eller kryssrutekomponenter.
* FORMS-11361: Den nedrullningsbara komponenten väljer automatiskt det första alternativet i listan.
* FORMS-11413: Ett fel relaterat till Forms Portal-förifyllningstjänsten aktiveras av Adaptive Forms, även när tjänsten inte används.
* FORMS-11433: När en komponent som inte är en formulärkomponent ingår i ett adaptivt formulär slutförs inte överföringsprocessen.
* FORMS-11206: När en användare försöker schemalägga ett publiceringsarbetsflöde för ett adaptivt formulär fungerar det inte som förväntat.
* FORMS-11546: En ARIA-etikett saknas för upprepade paneler i adaptiv form, vilket påverkar tillgängligheten.
* FORMS-11095: Attributet ARIA är felaktigt definierat för fält för telefonnummer, e-postadress och nummer, vilket leder till problem med tillgänglighet.

### Kända fel {#known-issues-14227}

Ingen.

### Inbäddade tekniker {#embedded-tech-14227}

| Teknik | Version | Länk |
|---|---|---|
| AEM | 1.56-T20230927085643-189caed | [Oak API 1.56.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.56.0/index.html) |
| AEM SLING API | Version 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | Version 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | Version 2.23.4 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |
