---
title: Versionsinformation om 2020.7.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
description: '"[!DNL Adobe Experience Manager] as a Cloud Service Release Notes for 2020.7.0."'
exl-id: 75d354a3-6987-4de0-aec8-24043461c516
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 1%

---

# Versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service 2020.7.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för Experience Manager as a Cloud Service 2020.7.0.

## Releasedatum {#release-date}

Releasedatum för [!DNL Experience Manager] as a Cloud Service 2020.7.0 är 30 juli 2020.

## Adobe Experience Manager Sites as a Cloud Service {#cloud-services-sites}

### Nyheter {#what-is-new-sites}

[!DNL Experience Manager] as a Cloud Service anslutningar för [!DNL Adobe Target] och [!DNL Adobe Analytics] har förbättrats på följande sätt:

* En ny implementering av användargränssnittet ersätter implementeringen som baseras på det klassiska användargränssnittet.

* Förenklade dialogrutor för användargränssnitt, där man kan skapa ramverk för variabelmappning och andra konfigurationer för [!DNL Adobe Launch]. Se [Integrera Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/integrations/integrating-adobe-analytics.html) och [Integrera Adobe Target](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/integrations/integrating-adobe-target.html).

* Konfigurationer lagras nu i `/conf` i stället för `/etc/cloudsettings` i Experience Manager-databasen.

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Nyheter i [!DNL Assets] {#what-is-new-assets}

* [!DNL Asset Compute Service] är en skalbar och utbyggbar tjänst för att bearbeta resurser. Administratörer kan konfigurera [!DNL Experience Manager] för att anropa anpassade program som skapats med [!DNL Asset Compute Service]. Utvecklare kan använda tjänsten för att skapa specialanpassade program som klarar komplexa användningsfall. Den här webbtjänsten kan generera miniatyrbilder för olika filtyper, bildåtergivning av hög kvalitet från filformat i Adobe, koda videofilmer (framtida), extrahera metadata, extrahera full text som prekursor för indexering och köra en mediefil genom alla tillgängliga [!DNL Sensei] tjänster. se [använda mikrotjänster och bearbetningsprofiler](/help/assets/asset-microservices-configure-and-use.md).

* Den inledande konfigurationen av [!DNL Dynamic Media] in [!DNL Experience Manager] as a Cloud Service har förbättrats för att bli mer robust. Det ger nu administratörerna förlopp för processerna.

* Publicera resurser på [!DNL Dynamic Media] förenklas och görs mer robust genom att göra det till en integrerad del av den övergripande processen för bearbetning av tillgångar med hjälp av mikrotjänster och genom att förbättra grupppubliceringsbackend.

* Arbetsflödessteg som inte är kompatibla med en Cloud Service-distribution markeras nu med en varning i [!UICONTROL workflow model] redigerare. När du kör de befintliga arbetsflödena i Cloud Service-miljön hoppas dessutom de inkompatibla arbetsflödesstegen över.

* Arbetsflödesmodeller som skapats av kunder som distribueras till `/conf/global` i Git-projektet som är kopplat till miljön i [!DNL Cloud Manager] distribueras automatiskt till `/var` och därmed tillgängliga i [!DNL Experience Manager]. Arbetsflödesmodellerna för produkter i `/libs` som ändrats av kunden inte automatiskt distribueras till `/var`.

### Fel har åtgärdats {#assets-bugs-fixed}

* Guiden Flytta resurs läses inte in som förväntat för resurserna som ingår i samlingar. (CQ-4296756)
* Värdena för `dam:size` och `dam:sha1` är exkluderade från XMP. (CQ-4237355)
* När resurser avpubliceras i grupp [!DNL Brand Portal] genererar ett fel som tyder på att URI:n för begäran är för lång. (CQ-4299474)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Nyheter {#what-is-new-commerce}

AEM Commerce är nu tillgänglig i Cloud Service.

Se [Komma igång med AEM Commerce as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/commerce/getting-started.html) för mer information.

## Kärnkomponenter {#core-components}

### Nyheter {#what-is-new-core-components}

Version 2.11.0 av [AEM kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) ingår nu som en del av AEM Sites:

* Introduktion till en ny [PDF Viewer Component](https://aemcomponents.dev/content/core-components-examples/library/page-authoring/pdf-viewer.html).

* Stöd för AMP (Accelerated Mobile Pages) för kärnkomponenter finns nu. Det hjälper till att skapa snabbare kundupplevelser genom att göra sidövergången direkt när du kommer in på webbplatsen från ett mobilsökresultat från Google, vilket förbättrar användarengagemanget och SEO.
Se [AMP-stöd för kärnkomponenterna](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) för mer information.

* Kompatibilitet med version 1.0.2 av [Adobe-klientdatalager](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html).

* Felkorrigeringar och förbättringar av kodkvaliteten.

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för [!UICONTROL Cloud Manager] Version 2020.7.0 är 9 juli 2020.

### Nyheter {#what-is-new-cloud-manager}

* Miljösidan har gjorts om.

* Vilolägen miljöer har nu en diskret status i Cloud Manager när de är i viloläge.

* Antalet miljövariabler per miljö har ökat till 200.

* Molnhanterarens pipelines har nu stöd för kundspecifika variabler och hemligheter.

   Mer information finns i Pipeline-variabler.

* Stöd finns nu för autentiseringsbundna privata Maven-databaser.

* Molnhanterarens byggbehållare har nu stöd för både Java 8 och Java 11.
Mer information finns i Använda Java 11-stöd.

### Felkorrigeringar {#bug-fixes-cm}

* Länken från Cloud Manager till Developer Console var felaktigt aktiv innan miljöerna skapades helt.

* Länken till Developer Console direkt från Cloud Manager visar inte alternativet att avplacera/viloläge för sandlådeprogrammets miljö.

* The **Avbryt** och **Spara** på redigeringssidan för icke-produktionsförlopp var inte alltid synliga.

* Vissa fel i kodkvalitetsprocessen kan leda till att loggfilen inte genereras korrekt.

* När du skapar ett nytt program returnerar det föreslagna namnet ibland en dubblett av ett befintligt programnamn.

* Vissa stora stegloggar för pipeline kunde inte hämtas konsekvent via användargränssnittet.

* Valideringen av miljönamn innehöll ett fel av typen&quot;off-one&quot;.

* På miljösidan visas ibland segment för publicering och utskickning när det inte finns några.

### Kända fel {#known-issues}

* På grund av en förändring i hur kodsatsen beräknas kan *minimum* versionen av Jacoco-pluginprogrammet är nu 0.7.5.201505241946 (släppt i maj 2015). Kunder som uttryckligen hänvisar till en äldre version får ett felmeddelande i kodkvalitetsprocessen.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-foundation}

### Nyheter {#what-is-new-foundations}

* [Loggar kan vidarebefordras till Splunk-konton](/help/implementing/developing/introduction/logging.md#splunk-logs), som gör det möjligt för organisationer att utnyttja Splunk-investeringen.

* [En statisk, dedikerad IP-adress för utgångar](/help/implementing/developing/introduction/development-guidelines.md#dedicated-egress-ip-address) kan tilldelas för utgående trafik som programmeras i Java-kod, vilket kan vara användbart för vissa integreringar.

* Ported AEM Analytics cloud service UI from Classic UI to new AEM UI. Platsen för Analytics-molntjänsten i AEM från `/etc` till `/conf`, för att anpassa sig till andra AEM-molntjänster.

* Portat AEM molntjänstgränssnitt från Classic UI till nytt AEM. Platsen för målmolntjänsten i AEM från har också flyttats `/etc` till `/conf`, för att anpassa sig till andra AEM-molntjänster.

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Cloud Readiness Analyzer version 1.0.2.

### Felkorrigeringar {#cra-bug-fixes}

* Tidigare version av CRA kunde inte köras på Adobe Experience Manager (AEM) 6.1. Explicit stöd för att tillåta användare i administratörsgruppen har lagts till.

   Se [Installera CRA på AEM 6.1](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61) för mer information.

* Den förfallotidsstämpel som visades i sammanfattningsrapporten var felaktig.

* CRA upptäckte dubbletter av anpassade komponenter.

* AEM 6.1 avslutades innehållsinspektionen innan den fullständiga undersökningen slutfördes. Undantagshantering har lagts till så att inspektören kan hoppa över och fortsätta tills den fullständiga inspektionen är slutförd.
