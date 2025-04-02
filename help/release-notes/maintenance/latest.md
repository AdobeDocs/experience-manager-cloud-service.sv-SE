---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 7d93af706d8b0556e9e26282d339794447eb0a41
workflow-type: tm+mt
source-wordcount: '1514'
ht-degree: 0%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Utgåva 2013 {#20133}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 2013, som offentliggjordes den 1 april 2025. Den tidigare underhållsutgåvan släpptes 19823.

Funktionsaktiveringen i 2025.4.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

### Förbättringar {#enhancements-20133}

* ASSETS-47850: Begränsa möjligheten att lägga till Scene7-konfigurationer om AEM CS är aktiverat.
* CQ-4359547: Fullständig borttagning av Guava från https://git.corp.adobe.com/target-sdk/tsdk-core.
* FORMS-17551: Stöd för DoR (Document of Record) för SharePoint listintegreringar.
* FORMS-18432: Implementerad formulärspecifik (regex-baserad) konfiguration av förifyllning på klientsidan för att möjliggöra selektiv förifyllning utan ändringar på OSGI-nivå.
* FORMS-18513: Implementerat stöd för dataträdsomvandling i AEP Connector för att förbättra guidefunktioner och datahanteringsfunktioner.
* FORMS-19068: Stöd har lagts till för AEP Connector-åtgärder i Forms Manager-API:er för att förbättra integreringsfunktionerna för formulärdata.
* GRANITE-57717: Uppdatera klientpaket i AEM.
* SITES-10469: AdapterFactory ska alltid returnera samma PageManager-instans.
* SITES-25130: Release Core Components 2.28.0.
* SITES-25433: Stöd för helsidesrendering vid jämförelse av gamla versioner.
* SITES-25923: LinkInfoStorageImpl kan blockera när inga URL:er längre lagras.
* SITES-26208: Om du tar bort ett innehållsfragment via arbetsflöde kan du nu välja att uppdatera referensresurser genom att ta bort det nyligen borttagna fragmentet.
* SITES-26500: Lägger till alternativet att flytta innehållsfragment via arbetsflöde - `move-fragments`.
* SITES-26711: Rollout Trigger - Länkarna uppdateras inte.
* SITES-27583: Upplev att fragment förlorar versionshistorik när de har flyttats.
* SITES-27618: Om du söker efter referenser för ett fragment på sidor returneras inte alla resultat.
* SITES-27781: Implementerad validering på modellnivå för Content Fragment-referenser, som tillåter validering av refererade fragment mot deras modellbegränsningar och obligatoriska taggar.
* SITES-27784: Uppdatera SQL-frågegenerering så att PATH-funktionen används i stället för `jcr:path`.
* SITES-28040: Adobe Target ExperienceFragmentsReplicationListener har brutits.
* SITES-28051: Hämta den aktuella användarens behörigheter för ett innehållsfragment: GET /cf/fragments/{fragmentId}/permissions.
* SITES-28190: Setup for Preview Integration Test.
* SITES-28227: När du lägger till resurser som referenser till ett fragment validerar vi att resursen finns.
* SITES-28248: Växla platshändelser baserat på OSGI-konfiguration.
* SITES-28255: Fullständigt namn saknas i alla tre granskningsegenskaperna: skapad, ändrad, publicerad.
* SITES-28390: PageImpl: Optimize hasContent().
* SITES-28404: Om du tar bort sidor från författaren avpubliceras de från förhandsgranskningstjänsten.
* SITES-28446: Två nya fält lades till som inte var synliga i svaret - platshållaren i NumberModelField och tillåtna modeller från LongTextModelField.
* SITES-28536: Skapa `RENAME`-slutpunkt för innehållsfragment.
* SITES-28537: Lägger till alternativet att byta namn på innehållsfragment via arbetsflöde - `rename-fragments`.
* SITES-28538: Referenser måste publiceras om för att giltigt innehåll ska kunna bevaras vid författaren och publiceringen.
* SITES-28549: Skapa `/cf/domains` för att returnera domän-ID baserat på AEM-nivå.
* SITES-29026: En valfri parameter som anger språkinställningen för innehållsfragmentet har lagts till med hjälp av språk- och landskoden.
* SITES-29031: Förbättrad logik för PATCH-fragment, vilket ger bättre prestanda.
* SITES-29169: Alla publicerade resurser (oavsett om de har statusen PUBLISHED eller MODIFIED) publiceras på nytt om de refererar till en resurs som har flyttats, bytt namn eller tagits bort.
* SITES-29376: Add Code toggle to validation of published resource delete.
* SITES-29417: Uppdatera /libs/cq/Page/proxy.jsp för att vidarebefordra begäran till jcr:content-noden i stället för att inkludera.
* SITES-2947: Skapa/ändra visualisering för banor för att jämföra publiceringsraser.
* SITES-29733: Förbättrade prestanda för modellsökning med taggar för innehållsfragment.
* SITES-8316: Content Policies: Cache the ContentPolicyManager.
* SITES-24906: Edge Delivery med Universal Editor: Stöd för kalkylblad som skapats av upphovsmannen utan mappning (tidig åtkomst)
* SITES-24907: Edge Delivery with Universal Editor: Support publishing Assets to multiple sites for MSM use case (tidig åtkomst)
* SITES-27956: Edge Delivery med Universal Editor: Förbättra publiceringsflödet (tidig åtkomst)
* SITES-27956: Edge Delivery med Universal Editor: Förbättra felhanteringen vid publicering till Edge Delivery Services (tidig åtkomst)

### Åtgärdade problem {#fixed-issues-20133}

* CQ-4358378: Hantera licensfel vid översättningskörningen.
* CQ-4359263: Inget meddelande visas i dialogrutan när jobbet är klart.
* CQ-4359386: Det går inte att lägga till i18n-ordlista i översättningsprojekt i AEMaaCS.
* FORMS-18068: Fet textåtergivningsproblem i DoR (Document of Record) för alternativknappar och kryssrutegrupper med hjälp av RTF-fält.
* FORMS-18189: Anpassad funktionshantering som förhindrar felloggning för tomma klientbibliotek och förbättrar felvisningen i användargränssnittet.
* FORMS-18213: Implementerad funktion för att dölja/exkludera inaktiverade fält från DoR (Document of Record) för att förbättra dokumentets tydlighet och användarupplevelsen.
* FORMS-18271: Forms Theme Editor visar olokaliserade felmeddelanden som påverkar användarupplevelsen när det gäller formulärkonfiguration och temaanpassning.
* FORMS-18304: PDF/A-1b-dokument som godkänts i Acrobat och LiveCycle ES4 flaggas felaktigt som icke-kompatibla i AEM 6.5 Forms på grund av enhetsberoende färgfel.
* FORMS-18325: Adobe Experience Platform (AEP) Cloud-konfiguration har lagts till för att förbättra integrationen av formulärdata och bearbetningskapaciteten.
* FORMS-18360: Förbättrad SharePoint listomfattningshantering för gruppwebbplatser i Forms Document Management för att förbättra dataorganisationen och åtkomstkontrollen.
* FORMS-18375: Formulär som baseras på Foundation-komponenter markerar felaktigt reaptcha-konfigurationer från mappen `conf/global` när ingen specifik konfigurationsbehållare har valts.
* FORMS-18426: SharePoint listsökningsfunktion misslyckas när listnamn innehåller specialtecken (till exempel &#39;-&#39;), vilket påverkar formulärintegrationen med SharePoint-listor.
* FORMS-19028: Förifyllningsfunktionen på klientsidan bryter hanteringen av formulärhändelser, vilket förhindrar Value commit- och DOMContentLoaded-händelser från att aktiveras korrekt vid formulärinläsning.
* FORMS-6950: Nödvändiga ARIA-roller och attribut har lagts till i komponenter för filsystemets navigatortreeview för att förbättra skärmläsarens tillgänglighet och uppfylla WCAG 4.1.2-standarden Namn, roll, värde (nivå A).
* FORMS-7016: Tangentbordsfokusordningen i formulärredigeraren följer inte logisk navigering.
* SITES-1960: Förbättrade prestanda för JSON-förhandsgranskning i Content Fragment Editor.
* SITES-24308: Vågrät rullningslist visas när innehållet ändrar storlek till 400 %.
* SITES-24493: Det interaktiva elementet har inte den roll som krävs.
* SITES-24669: Det går inte att komma åt kortkommandon med hjälp av Rail Window Splitter.
* SITES-26881: AEMaaCS Accessibility Bug - Incorrect Role is provided for the &quot;Three dots&quot; Icon which side comment input field.
* SITES-26956: Följ upp på SITES-24920 Det går inte att flytta sidan i produktionsmiljön.
* SITES-27707: Content Finder-tillgångslista misslyckas på grund av problem med resursnamn (6.5 SP22-regression).
* SITES-27757: Edge Delivery med Universal Editor: Rewrite icons enligt helix-html-pipeline-semantik.
* SITES-27780: Oväntad &lt;br>-tagg visas i RTE med Plaintext DefaultPasteMode i SP22.
* SITES-27958: Länkkontroll ger felmeddelanden om att sessionen har stängts.
* SITES-28149: Custom ExperienceFragmentLinkRewriterProvider utlöses inte vid XF-export till mål.
* SITES-28449: Arbetsflödeswidgetens gränssnittsfel - inkludera underordnade sidor som inte visar alla underordnade sidor i AEM.
* SITES-28456: Meddelande saknas i användargränssnittet om felaktig beständig fråga skulle sparas i GraphiQL Explorer (Följ upp - SITES-28313).
* SITES-28464: Uppdatera fragmentfrågan så att formaterade datum med millisekunder används.
* SITES-28486: In-place editing in the new Content Fragment Editor does not redirect to old editor.
* SITES-28570: Metadata för saknade resurser hanteras korrekt av Content Fragment&#39;s GraphQL.
* SITES-28580: Classic Image Asset Finder fungerar inte efter SP2-uppgradering.
* SITES-28600: Startar - duplicerat innehåll.
* SITES-28668: Det går inte att höja upp Launch med LaunchPromotionParameters.
* SITES-28820: Launch-prefix har lagts till två gånger i nya varianter som skapats i Rebase.
* SITES-28877: UE URL Service utlöser ett undantag när lokal extern slutpunkt inte har definierats.
* SITES-28956: En varning visas när taggen tas bort, om den refereras av innehållsfragment.
* SITES-29208: Referenser och varianter returneras korrekt när ett referensfält innehåller en ogiltig sökväg.
* SITES-29363: Knappen Återställ live-kopia fungerar inte för kapslad innehållshierarki för live-kopia.
* SITES-29369: Assets Event Issue in AIO | Felaktigt utlösa publicerade/opublicerade händelser för sida.
* SITES-29972: Åtgärder för att ta bort och byta namn resulterar ibland i felaktiga arbetsflödeskommentarer.

### Kända fel {#known-issues-20133}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-20133}

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

#### Ändringar i synkronisering av användargrupp och produktprofil {#changes-user-groups}

När du använder Adobe Admin Console för behörighetshantering FÅR följande grupper INTE användas eftersom de inte längre kommer att synkroniseras med AEM:
* AEM-grupper som slutar med _GROUP_NAME_SUFFIX.
* Produktprofiler från andra miljöer, program eller produkter.

Mer information finns i [Ändringar i användargruppen och produktprofilssynkroniseringen](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization).

#### Borttagning av SPA-redigeraren {#deprecate-spa-editor}

[SPA-redigeraren](/help/implementing/developing/hybrid/introduction.md) har tagits bort för nya projekt från och med version 2025.4.0. SPA-redigeraren stöds fortfarande för befintliga projekt, men bör inte användas för nya projekt.

De redigerare som rekommenderas för att hantera headless-innehåll i AEM är:

* [Den universella redigeraren](/help/edge/wysiwyg-authoring/authoring.md) för visuell redigering.
* [Innehållsfragmentsredigeraren](/help/assets/content-fragments/content-fragments-managing.md) för formulärbaserad redigering.

Mer information om den här borttagningen finns i dokumentet [Borttagning av SPA-redigerare.](/help/implementing/developing/hybrid/spa-editor-deprecation.md)

### Säkerhetskorrigeringar {#security-20133}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Denna underhållsrelease åtgärdar 34 identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-20133}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.76.0 | [Oak API 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 ](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.28.0 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |
