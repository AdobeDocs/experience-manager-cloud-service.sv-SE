---
title: Versionsinformation om 2020.7.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] Versionsinformation om as a Cloud Service för 2020.7.0.'
exl-id: 75d354a3-6987-4de0-aec8-24043461c516
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 1%

---

# Versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service 2020.7.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för Experience Manager as a Cloud Service 2020.7.0.

## Releasedatum {#release-date}

Lanseringsdatumet för [!DNL Experience Manager] as a Cloud Service 2020.7.0 är 30 juli 2020.

## Adobe Experience Manager Sites as a Cloud Service {#cloud-services-sites}

### Nyheter {#what-is-new-sites}

[!DNL Experience Manager] as a Cloud Service-anslutningar för [!DNL Adobe Target] och [!DNL Adobe Analytics] har förbättrats på följande sätt:

* En ny implementering av användargränssnittet ersätter implementeringen som baseras på det klassiska användargränssnittet.

* Förenklade dialogrutor för användargränssnitt, vilket gör att ramverket skapas för variabelmappning och andra konfigurationer till [!DNL Adobe Launch]. Se [Integrera Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/integrations/integrating-adobe-analytics.html) och [Integrera Adobe Target](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/integrations/integrating-adobe-target.html).

* Konfigurationer lagras nu i `/conf` i stället för `/etc/cloudsettings` i Experience Manager-databasen.

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Nyheter i [!DNL Assets] {#what-is-new-assets}

* [!DNL Asset Compute Service] är en skalbar och utökningsbar tjänst för att bearbeta resurser. Administratörer kan konfigurera [!DNL Experience Manager] att anropa anpassade program som skapats med [!DNL Asset Compute Service]. Utvecklare kan använda tjänsten för att skapa specialanpassade program som klarar komplexa användningsfall. Den här webbtjänsten kan generera miniatyrer för olika filtyper, bildåtergivning av hög kvalitet från Adobe-filformat, koda videor (framtida), extrahera metadata, extrahera full text som prekursor för indexering och köra en resurs via alla tillgängliga [!DNL AI]-tjänster. se [använda resursmikrotjänster och bearbetningsprofiler](/help/assets/asset-microservices-configure-and-use.md).

* Den inledande konfigurationen av [!DNL Dynamic Media] i [!DNL Experience Manager] as a Cloud Service har förbättrats för att bli mer robust. Det ger nu administratörerna förlopp för processerna.

* Publicering av resurser till [!DNL Dynamic Media] förenklas och görs mer robust genom att göra det till en integrerad del av den övergripande bearbetningen av resurser med hjälp av mikrotjänster och genom att förbättra grupppubliceringsbackend.

* Arbetsflödessteg som inte är kompatibla med en Cloud Service-distribution har nu markerats med en varning i [!UICONTROL workflow model]-redigeraren. När du kör befintliga arbetsflöden i Cloud Service-miljön hoppas de inkompatibla arbetsflödesstegen över.

* Arbetsflödesmodeller som skapats av kunder som har distribuerats till `/conf/global` i Git-projektet som är kopplat till miljön i [!DNL Cloud Manager] distribueras automatiskt till `/var` och är därmed tillgängliga i [!DNL Experience Manager]. Produktarbetsflödesmodellerna under `/libs` som ändrades av kunden distribueras inte automatiskt till `/var`.

### Fel har åtgärdats {#assets-bugs-fixed}

* Guiden Flytta resurs läses inte in som förväntat för resurserna som ingår i samlingar. (CQ-4296756)
* Värdena för `dam:size` och `dam:sha1` är exkluderade från XMP-tillbakaskrivning. (CQ-4237355)
* När resurser avpubliceras i grupp genererar [!DNL Brand Portal] ett fel som anger att URI:n för begäran är för lång. (CQ-4299474)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Nyheter {#what-is-new-commerce}

AEM Commerce finns nu på Cloud Service.

Mer information finns i [Komma igång med AEM Commerce as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/commerce/getting-started.html).

## Kärnkomponenter {#core-components}

### Nyheter {#what-is-new-core-components}

Version 2.11.0 av [AEM Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) är nu tillgänglig som en del av AEM Sites, inklusive:

* Introduktion av en ny [PDF Viewer-komponent](https://www.aemcomponents.dev/content/core-components-examples/library/core-content/pdf-viewer.html).

* Stöd för AMP (Accelerated Mobile Pages) för kärnkomponenter finns nu. Det hjälper till att skapa snabbare kundupplevelser genom att göra sidövergången direkt när du kommer in på webbplatsen från ett mobilsökresultat från Google, vilket förbättrar användarengagemanget och SEO.
Mer information finns i [AMP-stöd för kärnkomponenterna](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html).

* Kompatibilitet med version 1.0.2 av [Adobe Client Data Layer](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html).

* Felkorrigeringar och förbättringar av kodkvaliteten.

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för [!UICONTROL Cloud Manager] version 2020.7.0 är 9 juli 2020.

### Nyheter {#what-is-new-cloud-manager}

* Miljösidan har gjorts om.

* Vilolägen miljöer har nu en diskret status i Cloud Manager när de är i viloläge.

* Antalet miljövariabler per miljö har ökat till 200.

* Cloud Manager rörledningar har nu stöd för variabler och hemligheter som kunderna ställer in.

  Mer information finns i Förloppsvariabler.

* Stöd finns nu för autentiseringsbundna privata Maven-databaser.

* Cloud Manager byggbehållare stöder nu både Java 8 och Java 11.
Mer information finns i Använda Java 11-stöd.

### Felkorrigeringar {#bug-fixes-cm}

* Länken från Cloud Manager till Developer Console var inkorrekt aktiv innan miljöerna skapades helt.

* Länken till Developer Console direkt från Cloud Manager visade inte möjligheten att avviloläge/viloläge för sandlådeprogrammets miljö.

* Alternativen **Avbryt** och **Spara** på redigeringssidan för icke-produktionsförlopp är inte alltid synliga.

* Vissa fel i kodkvalitetsprocessen kan leda till att loggfilen inte genereras korrekt.

* När du skapar ett program returnerar det föreslagna namnet ibland en dubblett av ett befintligt programnamn.

* Vissa stora stegloggar för pipeline kunde inte hämtas konsekvent via användargränssnittet.

* Valideringen av miljönamn innehöll ett fel av typen&quot;off-one&quot;.

* På miljösidan visas ibland segment för publicering och utskickning när det inte finns några.

### Kända fel {#known-issues}

* På grund av en ändring i hur kodsatsen beräknas är versionen *minimum* av Jacoco-pluginprogrammet nu 0.7.5.201505241946 (släppt i maj 2015). Kunder som uttryckligen hänvisar till en äldre version får ett felmeddelande i kodkvalitetsprocessen.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-foundation}

### Nyheter {#what-is-new-foundations}

* [Loggar kan vidarebefordras till Splunk-konton](/help/implementing/developing/introduction/logging.md#splunk-logs), som gör att organisationer kan använda sin Splunk-investering.

* [En statisk, dedikerad IP-adress ](/help/implementing/developing/introduction/development-guidelines.md#dedicated-egress-ip-address) kan tilldelas för utgående trafik som programmeras i Java-kod, vilket kan vara användbart för vissa integreringar.

* Portat AEM Analytics-molntjänstgränssnitt från Classic-användargränssnitt till nytt AEM-gränssnitt. Platsen för Analytics-molntjänsten i AEM-databasen har också flyttats från `/etc` till `/conf` för att anpassas till andra AEM molntjänster.

* Portat AEM Target-molntjänstgränssnitt från Classic UI till nytt AEM-gränssnitt. Platsen för Target-molntjänsten i AEM-databasen har också flyttats från `/etc` till `/conf`, för att anpassas till andra AEM molntjänster.

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Cloud Readiness Analyzer version 1.0.2.

### Felkorrigeringar {#cra-bug-fixes}

* Tidigare version av CRA kunde inte köras på Adobe Experience Manager (AEM) 6.1. Explicit stöd för att tillåta användare i administratörsgruppen har lagts till.

  Mer information finns i [Installera CRA på AEM 6.1](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61).

* Den förfallotidsstämpel som visades i sammanfattningsrapporten var felaktig.

* CRA upptäckte dubbletter av anpassade komponenter.

* I AEM 6.1 avslutades innehållsinspektionen innan den fullständiga undersökningen slutfördes. Undantagshantering har lagts till så att inspektören kan hoppa över och fortsätta tills den fullständiga inspektionen är slutförd.
