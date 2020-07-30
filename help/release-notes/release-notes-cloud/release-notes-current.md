---
title: Versionsinformation för 2020.7.0-utgåvan [!DNL Adobe Experience Manager] av en Cloud Service.
description: '[!DNL Adobe Experience Manager] som Cloud Service versionsinformation för 2020.7.0.'
translation-type: tm+mt
source-git-commit: 3dc0d1d77595f7b3e890fb4b390eef5bcf84ecd8
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 2%

---


# Versionsinformation för [!DNL Adobe Experience Manager] som Cloud Service 2020.7.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för Experience Manager som Cloud Service 2020.7.0.

## Releasedatum {#release-date}

Releasedatum för [!DNL Experience Manager] Cloud Service 2020.7.0 är 30 juli 2020.

## Adobe Experience Manager Sites som Cloud Service {#cloud-services-sites}

### What&#39;s New {#what-is-new-sites}

[!DNL Experience Manager] som en Cloud Service-koppling för [!DNL Adobe Target] och [!DNL Adobe Analytics] förbättras på följande sätt:

* En ny implementering av användargränssnittet ersätter implementeringen som baseras på det klassiska användargränssnittet.

* Förenklade dialogrutor i användargränssnittet, vilket gör att ramverket skapas för variabelmappning och andra konfigurationer [!DNL Adobe Launch].

* Konfigurationer lagras nu i `/conf` stället `/etc/cloudsettings` för i Experience Manager-databasen.

## Adobe Experience Manager Assets as a Cloud Service {#assets}

>[!NOTE]
>AEM Assets som Cloud Service kommer att lanseras under de närmaste dagarna.

### What&#39;s New {#what-is-new-assets}

* [!DNL Asset Compute Service] är en skalbar och utbyggbar tjänst för att bearbeta resurser. Administratörer kan konfigurera Experience Manager att anropa anpassad arbetare som skapats med [!DNL Asset Compute Service]. Utvecklare kan använda tjänsten för att skapa specialarbetare som klarar komplexa användningsfall. Den här webbtjänsten kan generera miniatyrbilder för olika filtyper, bildåtergivning av hög kvalitet från filformat i Adobe, koda videor (framtida), extrahera metadata, extrahera full text som prekursor för indexering och köra en resurs via alla tillgängliga Sensei-tjänster. se [Använda mikrotjänster och bearbetningsprofiler](/help/assets/asset-microservices-configure-and-use.md).

* Den initiala konfigurationen av [!DNL Dynamic Media] som Cloud Service i [!DNL Experience Manager] förbättras för att bli mer robust. Det ger nu administratörerna förlopp för processerna.

* Publicering av resurser till [!DNL Dynamic Media] förenklas och görs mer robust genom att göra det till en integrerad del av den övergripande processen för bearbetning av tillgångar med hjälp av mikrotjänster och genom att förbättra batchpubliceringen.

* Arbetsflödessteg som inte är kompatibla med en Cloud Service-distribution har nu markerats med en varning i [!UICONTROL workflow model] redigeraren. När du kör de befintliga arbetsflödena i Cloud Service-miljön hoppas dessutom de inkompatibla arbetsflödesstegen över.

* Arbetsflödesmodeller som skapats av kunder som distribueras till `/conf/global` i Git-projektet som är kopplat till miljön i Cloud Manager distribueras automatiskt till `/var` och är därmed tillgängliga i Experience Manager. Arbetsflödesmodellerna för produkter `/libs` som ändrats av kunden distribueras inte automatiskt till `/var`.

## Kärnkomponenter {#core-components}

### What&#39;s New {#what-is-new-core-components}

Version 2.11.0 av [AEM Core Components](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) finns nu som en del av AEM Sites, inklusive:

* Introduktion till en ny [PDF Viewer-komponent](https://aemcomponents.dev/content/core-components-examples/library/page-authoring/pdf-viewer.html).

* Stödet för AMP (Accelerated Mobile Pages) i Core Components hjälper till att skapa snabbare kundupplevelser genom att göra sidövergången direkt när du kommer in på webbplatsen från ett Google Mobile Search-resultat, vilket förbättrar användarengagemanget och SEO.

* Kompatibilitet med version 1.0.2 av [Adobe-klientdatalagret](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/data-layer/overview.html).

* Felkorrigeringar och förbättringar av kodkvaliteten.

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för [!UICONTROL Cloud Manager] version 2020.7.0 är 9 juli 2020.

### What&#39;s New {#what-is-new-cloud-manager}

* Miljösidan har gjorts om.

* Vilolägen miljöer har nu en diskret status i Cloud Manager när de är i viloläge.

* Antalet miljövariabler per miljö har ökat till 200.

* Molnhanterarens pipelines har nu stöd för kundspecifika variabler och hemligheter.

   Mer information finns i [Pipeline-variabler](/help/onboarding/getting-access-to-aem-in-cloud/creating-aem-application-project.md#pipeline-variables) .

### Bug Fixes {#bug-fixes-cm}

* Länken från Cloud Manager till Developer Console var felaktigt aktiv innan miljöerna skapades helt.

* Länken till Developer Console direkt från Cloud Manager visar inte alternativet att avplacera/viloläge för sandlådeprogrammets miljö.

* Alternativen **Avbryt** och **Spara** på redigeringssidan för icke-produktionsförlopp visas inte alltid.

* Vissa fel i kodkvalitetsprocessen kan leda till att loggfilen inte genereras korrekt.

* När du skapar ett nytt program returnerar det föreslagna namnet ibland en dubblett av ett befintligt programnamn.

* Vissa stora stegloggar för pipeline kunde inte hämtas konsekvent via användargränssnittet.

* Valideringen av miljönamn innehöll ett fel av typen&quot;off-one&quot;.

* På miljösidan visas ibland segment för publicering och utskickning när det inte finns några.

### Kända fel {#known-issues}

* På grund av en förändring i hur kodens täckning beräknas är den *lägsta* versionen av Jacoco-pluginprogrammet nu 0.7.5.201505241946 (släppt i maj 2015). Kunder som uttryckligen hänvisar till en äldre version får ett felmeddelande i kodkvalitetsprocessen.


## Adobe Experience Manager as a Cloud Service Foundation {#cloud-foundation}

### What&#39;s New {#what-is-new-foundations}

* [Loggar kan vidarebefordras till Splunk-konton](/help/implementing/developing/introduction/logging.md#splunk-logs), vilket gör att organisationer kan utnyttja sin Splunk-investering.

* [En statisk, dedikerad IP-adress](/help/implementing/developing/introduction/development-guidelines.md#dedicated-egress-ip-address) för utgångstrafik som programmeras i Java-kod kan tilldelas, vilket kan vara användbart för vissa integreringar.

* Ported AEM Analytics cloud service UI from Classic UI to new AEM UI. Platsen för Analytics molntjänst i AEM från `/etc` till `/conf`och i linje med andra AEM cloud services har också flyttats.

* Ported AEM Target cloud service UI from Classic UI to new AEM UI. Platsen för Target molntjänst i AEM från `/etc` till `/conf`och i linje med andra AEM cloud services har också flyttats.

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Cloud Readiness Analyzer version 1.0.2.

### Bug Fixes {#cra-bug-fixes}

* Tidigare version av CRA kunde inte köras på Adobe Experience Manager (AEM) 6.1. Explicit stöd för att tillåta användare i administratörsgruppen har lagts till.

   Mer information finns i [Installera CRA på AEM 6.1](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61) .

* Den förfallotidsstämpel som visades i sammanfattningsrapporten var felaktig.

* CRA upptäckte dubbletter av anpassade komponenter.

* AEM 6.1 avslutades innehållsinspektionen innan den fullständiga undersökningen slutfördes. Undantagshantering har lagts till så att inspektören kan hoppa över och fortsätta tills den fullständiga inspektionen är slutförd.
