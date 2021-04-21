---
title: Video
description: Lär dig hur du arbetar med video i Dynamic Media.
feature: Videoprofiler
role: Business Practitioner
exl-id: 0d5fbb3e-b763-415f-8c69-ea36445f882b
translation-type: tm+mt
source-git-commit: e94289bccc09ceed89a2f8b926817507eaa19968
workflow-type: tm+mt
source-wordcount: '9133'
ht-degree: 6%

---

# Video{#video}

I det här avsnittet beskrivs hur du arbetar med video i Dynamic Media.

## Snabbstart: Videoklipp {#quick-start-videos}

Följande steg-för-steg-beskrivning av arbetsflödet hjälper dig att komma igång snabbt med anpassningsbara videouppsättningar i Dynamic Media. Efter varje steg finns korsreferenser till ämnesrubriker där du kan hitta mer information.

>[!NOTE]
>
>Innan du arbetar med video i Dynamic Media måste du kontrollera att Adobe Experience Manager-administratören redan har aktiverat och konfigurerat Dynamic Media-Cloud Services.
>
>* Se [Konfigurera Dynamic Media-Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) i Konfigurera Dynamic Media och [Felsöka Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md).

>



1. **Ladda upp dina Dynamic Media-** filmer genom att göra följande:

   * Skapa en egen videokodningsprofil. Du kan också helt enkelt använda den fördefinierade _adaptiva videokodningsprofilen_ som medföljer Dynamic Media.

      * [Skapa en videokodningsprofil](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * Läs mer om [Bästa tillvägagångssätt för videokodning](#best-practices-for-encoding-videos).
   * Koppla videobearbetningsprofilen till en eller flera mappar där du ska överföra dina primära källvideor.

      * [Tillämpa en videoprofil på mappar](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).
      * Läs mer om [Bästa tillvägagångssätt för att ordna digitala resurser så att du kan använda bearbetningsprofiler](/help/assets/dynamic-media/best-practices-for-file-management.md).
      * Läs mer om [Organisera digitala resurser](/help/assets/organize-assets.md).
   * Överför dina primära källvideor till mapparna. Du kan överföra videofiler som är upp till 15 GB vardera. När du lägger till videofilmer i mappen kodas de enligt den videobearbetningsprofil som du tilldelade mappen.

      * [Ladda upp videor](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).
      * Läs mer om [Indatafilformat](/help/assets/file-format-support.md) som stöds.
   * Övervaka hur [videokodningen fortskrider](#monitoring-video-encoding-and-youtube-publishing-progress) antingen från resursvyn eller arbetsflödesvyn.




1. **Hantera dina Dynamic Media-** filmer på något av följande sätt:

   * Ordna, bläddra bland och söka efter videomaterial

      * [Organisera digitalt ](/help/assets/organize-assets.md)
materialLäs mer om  [Bästa metoder för att ordna digitala resurser för att använda bearbetningsprofiler](/help/assets/dynamic-media/best-practices-for-file-management.md)

      * [Söka efter ](/help/assets/search-assets.md#custompredicates) videomaterial eller  [söka resurser](/help/assets/manage-digital-assets.md#search-assets)
   * Förhandsgranska och publicera videomaterial

      * Visa källvideon och de kodade återgivningarna av videon tillsammans med tillhörande miniatyrer:
         [Förhandsgranska ](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) videoklipp eller  [förhandsgranska resurser](/help/assets/dynamic-media/previewing-assets.md)
         [Hantera videoåtergivningar](/help/assets/manage-digital-assets.md#managing-renditions)


<!-- Commented video-renditions.md as the file is not published yet and will lead to broken link.
        * View the source video and encoded renditions of the video along with its associated thumbnails:
          [Previewing videos](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) or [Previewing assets](/help/assets/dynamic-media/previewing-assets.md)
          [Viewing video renditions](/help/assets/video-renditions.md)
          [Managing video renditions](/help/assets/manage-digital-assets.md#managing-renditions) -->

    * [Hantera förinställningar för visningsprogram](/help/assets/dynamic-media/managing-viewer-presets.md)
    * [Publicera resurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
    
    * Arbeta med videometadata

<!--      * View the properties of an encoded video rendition such as frame rate, audio and video bitrate, and codec:
          [Viewing video rendition properties](/help/assets/video-renditions.md) -->

    * Redigera egenskaperna för videon, t.ex. titel, beskrivning och taggar, egna metadatafält:
    [Redigera videoegenskaper](/help/assets/manage-digital-assets.md#editing-properties)
    
    * [Hantera metadata för digitala resurser](/help/assets/manage-metadata.md)
    * [Metadata scheme](/help/assets/metadata-schemas.md)
    
    * Granska, godkänn och kommentera videoklipp och behåll fullständig versionskontroll
    
    * [Anteckna videoklipp](/help/assets/manage-video-assets.md#annotate-video-assets) eller [Anteckningsresurser](/help/assets/manage-digital-assets.md#annotating)
    
    * [Skapa en version](/help/assets/manage-digital-assets.md#asset-versioning)
    * [Starta ett arbetsflöde för en resurs](/help/assets/manage-digital-assets.md#starting-a-workflow-on-an-asset)

<!-- Removing assets-workflow.md file link as it is not applicable anymore. Workflows are replaced by processing profiles.
        * [Creating a version](/help/assets/manage-digital-assets.md#asset-versioning)
        * [Applying workflows to assets](/help/assets/assets-workflow.md) or see [Starting a workflow on an asset](/help/assets/manage-digital-assets.md#starting-a-workflow-on-an-asset)
-->

    * [Granska mappresurser](/help/assets/bulk-approval.md)
    * [Projekt](/help/sites-cloud/authoring/projects/overview.md)

1. **Publicera dina Dynamic Media-** filmer genom att göra något av följande:

   * Om du använder Experience Manager som WCM-system (Web Content Management) kan du lägga till videofilmer direkt på dina webbsidor.

      * [Lägga till videoklipp på webbsidor](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).
   * Om du använder ett webbinnehållshanteringssystem från en annan leverantör kan du länka eller bädda in videor på dina webbsidor.

      * Integrera video med URL:
         [Länka URL till ett webbprogram](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md).

      * Integrera video med inbäddad kod på webbsidan:
         [Bädda in videovisningsprogrammet på en webbsida](/help/assets/dynamic-media/embed-code.md).
   * [Publicera videor på YouTube](#publishing-videos-to-youtube).
   * [Genererar videorapporter](#viewing-video-reports).

   * [Lägga till bildtexter i videon](#adding-captions-to-video).



## Arbeta med video i Dynamic Media {#working-with-video-in-dynamic-media}

Video i Dynamic Media är en totallösning som gör det enkelt att publicera högkvalitativ adaptiv video för direktuppspelning på flera skärmar, inklusive datorer, iOS, Android™, BlackBerry® och Windows®-enheter. En adaptiv videouppsättning grupperar versioner av samma video som är kodade med olika bithastigheter och format som 400 kbit/s, 800 kbit/s och 1 000 kbit/s. Den stationära datorn eller mobila enheten känner av den tillgängliga bandbredden.

På en iOS-mobil enhet upptäcker den till exempel en bandbredd som 3G, 4G eller Wi-Fi. Sedan väljs automatiskt rätt kodad video bland de olika videobithastigheterna i den adaptiva videouppsättningen. Videon strömmas till datorer, mobila enheter eller surfplattor.

Dessutom ändras videokvaliteten dynamiskt automatiskt om nätverksförhållandena ändras på datorn eller den mobila enheten. Om en kund går över till helskärmsläge på en stationär dator svarar den adaptiva videouppsättningen med en bättre upplösning, vilket förbättrar kundens tittarupplevelse. Med adaptiva videouppsättningar får du bästa möjliga uppspelning för kunder som spelar upp Dynamic Media-video på flera skärmar och enheter.

Den logik som en videospelare använder för att avgöra vilken kodad video som ska spelas upp eller väljas under uppspelningen baseras på följande algoritm:

1. Videospelaren läser in det inledande videofragmentet baserat på den bithastighet som ligger närmast värdet som är inställt för&quot;inledande bithastighet&quot; i spelaren.
1. Videospelaren växlar baserat på ändringar av bandbreddshastigheten med följande kriterier:

   1. Spelaren väljer den högsta bandbreddsströmmen under eller lika med den beräknade bandbredden.
   1. Spelaren hanterar bara 80 % av den tillgängliga bandbredden. Men om den byter upp sig är det mer försiktigt med bara 70 % för att undvika överskattning och omedelbart gå tillbaka.

Detaljerad teknisk information om algoritmen finns i [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

Följande stöds för hantering av enstaka video och adaptiva videouppsättningar:

* Överföra video från ett antal videoformat och ljudformat som stöds och koda video till MP4 H.264-format för uppspelning på flera skärmar. Du kan använda fördefinierade adaptiva videoförinställningar, enskilda videokodningsförinställningar eller anpassa din egen kodning för att styra videons kvalitet och storlek.

   * När en adaptiv videouppsättning genereras innehåller den MP4-videor.
   * **Obs**: Primära videor/källvideor läggs inte till i en adaptiv videouppsättning.

* Videobildtext i alla HTML5-videovisningsprogram.
* Ordna, bläddra bland och sök videoklipp med fullt stöd för metadata för effektiv hantering av videomaterial.
* Leverera adaptiva videouppsättningar till webben och datorer samt till mobila enheter som iPhone, iPad, Android™, BlackBerry® och Windows®.

Adaptiv videoströmning stöds på olika iOS-plattformar. Se [Referenshandbok för Dynamic Media-visningsprogram](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference.html).

Dynamic Media har stöd för videouppspelning i mobiler för MP4 H.264-video. Du kan hitta BlackBerry®-enheter som stöder det här videoformatet på följande: [Videoformat som stöds på BlackBerry®](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

Följande Windows®-enheter har stöd för det här videoformatet: [Videoformat som stöds på Windows® Phone](https://msdn.microsoft.com/library/windows/apps/ff462087%28v=vs.105%29.aspx)

* Spela upp videon med Dynamic Media Video Viewer Presets, inklusive följande:

   * Enstaka videovisningsprogram.
   * Visningsprogram för blandade media som kombinerar både video- och bildinnehåll.

* Konfigurera videospelare för att tillgodose era varumärkesbehov.
* Integrera video på webbplatsen, mobilsajten eller mobilapplikationen med en enkel URL eller inbäddningskod.

Se [Exempel på dynamisk videouppspelning](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&amp;config=GeoRetail/Universal_Video1&amp;stageSize=640,480).

Se även [Visningsprogram för Experience Manager Assets och Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) och [Endast visningsprogram för Experience Manager Assets](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only) i [Dynamic Media Viewer Reference Guide](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html).

## Bästa praxis: Använda HTML5-videovisningsprogrammet {#best-practice-using-the-html-video-viewer}

Förinställningarna för visningsprogrammet för Dynamic Media HTML5-video är robusta videospelare. Du kan använda dem för att undvika många vanliga problem som är kopplade till videouppspelning i HTML5 och problem som är kopplade till mobila enheter. Exempel: brist på adaptiv strömning och begränsad webbläsarräckvidd.

På designsidan av spelaren kan du utforma videospelarens funktioner med standardverktyg för webbutveckling. Du kan till exempel utforma knappar, kontroller och anpassad förhandsgranskningsbildbakgrund med HTML5 och CSS så att du kan nå dina kunder med ett anpassat utseende.

På visningsprogrammets uppspelningssida identifieras webbläsarens videokapacitet automatiskt. Sedan visas videon med HLS (HTTP Live Streaming), som också kallas adaptiv videoströmning. Om leveransmetoderna saknas används i stället HTML5 progressiv.

Du kan kombinera möjligheten att utforma uppspelningskomponenterna med HTML5 och CSS i en enda spelare. Den kan ha inbäddad uppspelning och använda adaptiv och progressiv strömning beroende på webbläsarens kapacitet. Alla dessa funktioner innebär att du kan utöka räckvidden för ditt multimedieinnehåll till både dator- och mobilanvändare och få en smidig videoupplevelse.

Se även [Endast visningsprogram för Experience Manager-resurser](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only) i [referenshandboken för Dynamic Media-visningsprogram](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html).

### Uppspelning av video på stationära datorer och mobila enheter med HTML5-videovisningsprogrammet {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

För strömning av anpassningsbara video för datorer och mobilenheter baseras de videor som används för växling av bithastighet på alla MP4-videor i den adaptiva videouppsättningen.

Videouppspelning sker med HLS eller progressiv videohämtning. I tidigare versioner av Experience Manager, som 6.0, 6.1 och 6.2, strömmades videofilmer via HTTP.

I Experience Manager 6.3 och senare direktuppspelas videor nu via HTTPS (dvs. HLS) eftersom DM-gatewaytjänstens URL alltid använder HTTPS. Det här standardbeteendet påverkar inte kunderna. Det innebär att direktuppspelning av video alltid sker via HTTPS, såvida det inte stöds av webbläsaren. (se följande tabell). Därför returnerar

* Om du har en HTTPS-webbplats med HTTPS-videoströmning går det bra att strömma.
* Om du har en HTTP-webbplats med HTTPS-videoströmning går det bra att strömma och det finns inga blandade innehållsproblem i webbläsaren.

HLS är en Apple-standard för adaptiv videoströmning som automatiskt justerar uppspelningen baserat på nätverkets bandbreddskapacitet. Man kan också &quot;söka&quot; till valfri punkt i videon utan att behöva vänta på att resten av videon ska laddas ned.

Progressiv video levereras genom att videon hämtas och lagras lokalt på en användares dator eller mobila enhet.

I följande tabell beskrivs enheten, webbläsaren och uppspelningsmetoden för videofilmer på stationära datorer och mobila enheter med [Dynamic Media HTML5 Video Viewer](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video.html#interactive-video).

<table>
 <tbody>
  <tr>
   <td><strong>Enhet</strong></td>
   <td><strong>Webbläsare</strong></td>
   <td><strong>Videouppspelningsläge</strong></td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Internet Explorer 9 och 10</td>
   <td>Progressiv nedladdning.</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Internet Explorer 11+</td>
   <td>I Windows® 8 och Windows® 10 - Tvinga användning av HTTPS när HLS begärs. Känd begränsning: HTTP på HLS fungerar inte i den här kombinationen av webbläsare/operativsystem<br /> <br /> I Windows® 7 - progressiv nedladdning. Använder standardlogik för att välja HTTP- eller HTTPS-protokoll.</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Firefox 23-44</td>
   <td>Progressiv nedladdning.</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Firefox 45 eller senare</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Krom</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Safari (Mac)</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Chrome (Android™ 6 eller tidigare)</td>
   <td>Progressiv nedladdning.</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Chrome (Android™ 7 eller senare)</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Android™ (standardwebbläsare)</td>
   <td>Progressiv nedladdning.</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Safari (iOS)</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Chrome (iOS)</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>BlackBerry®</td>
   <td>HLS</td>
  </tr>
 </tbody>
</table>

## Arkitektur för Dynamic Media videolösning {#architecture-of-dynamic-media-video-solution}

Följande bild visar det övergripande arbetsflödet för redigering av videoklipp som har överförts och kodats med hjälp av DMGGateway (i Dynamic Media Hybrid-läge) och som har gjorts tillgängliga för offentlig användning.

![chlimage_1-427](assets/chlimage_1-427.png)

## Hybrid publiceringsarkitektur för videor {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## Metodtips för att koda videofilmer {#best-practices-for-encoding-videos}

Arbetsflödet **Dynamic Media Encode Video** kodar video om du har aktiverat Dynamic Media och konfigurerat Cloud Services för video. Det här arbetsflödet innehåller information om arbetsflödets processhistorik och fel. Se [Övervaka videokodning och publiceringsförlopp på YouTube](#monitoring-video-encoding-and-youtube-publishing-progress). Om du har aktiverat Dynamic Media och konfigurerat Cloud Services för video börjar arbetsflödet **[!UICONTROL Dynamic Media Encode Video]** automatiskt gälla när du överför en video. (Om du inte använder Dynamic Media börjar arbetsflödet **[!UICONTROL DAM Update Asset]** gälla.)

Nedan följer några tips om hur du kodar källvideofiler.

Mer information om videokodning finns i:

* [Direktuppspelning 101: Grundläggande - kodekar, bandbredd, datahastighet och upplösning](https://www.adobe.com/go/learn_s7_streaming101_en).
* [Grunderna](https://www.adobe.com/go/learn_s7_encoding_en) i videokodning.

### Källvideofiler {#source-video-files}

När du kodar en videofil ska du använda en källvideofil med högsta möjliga kvalitet. Undvik att använda tidigare kodade videofiler eftersom dessa filer redan är komprimerade, och ytterligare kodning skapar en video med delkvalitet.

I följande tabell beskrivs rekommenderad storlek, proportioner och lägsta bithastighet som källvideofilerna måste ha innan du kodar dem:

| Storlek | Proportioner | Minsta bithastighet |
|--- |--- |--- |
| 1024 x 768 | 4:3 | 4 500 kbit/s för de flesta videoklipp. |
| 1280 x 720 | 16:9 | 3 000 - 6 000 kbit/s, beroende på mängden rörelse i videon. |
| 1920 x 1080 | 16:9 | 6000 - 8 000 kbit/s, beroende på mängden rörelse i videon. |

### Hämta metadata för en fil {#obtaining-a-file-s-metadata}

Du kan hämta metadata för en fil genom att visa dess metadata med ett videoredigeringsverktyg eller med ett program som utformats för att hämta metadata. Nedan följer instruktioner om hur du använder MediaInfo, ett tredjepartsprogram, för att hämta videofilens metadata:

1. Gå till den här webbsidan: [https://mediainfo.sourceforge.net/en/Download](https://mediainfo.sourceforge.net/en/Download).
1. Välj och hämta installationsprogrammet för den grafiska användargränssnittsversionen och följ installationsanvisningarna.
1. Efter installationen högerklickar du på videofilen (endast Windows®) och väljer MediaInfo, eller så öppnar du MediaInfo och drar videofilen till programmet. Alla metadata som är associerade med videofilen, inklusive bredd, höjd och fps, visas.

### Proportioner {#aspect-ratio}

När du väljer eller skapar en förinställning för videokodning för den primära källvideofilen måste du se till att förinställningen har samma proportioner som den primära källvideofilen. Proportionerna är proportionerna mellan videons bredd och höjd.

Om du vill ta reda på videofilens proportioner hämtar du filens metadata och noterar filens bredd och höjd (se Hämta filens metadata ovan). Använd sedan den här formeln för att bestämma proportionerna:

width/height = aspect ratio

I följande tabell beskrivs hur formelresultaten översätts till vanliga alternativ för proportioner:

| Formelresultat | Proportioner |
|--- |--- |
| 1,33 | 4:3 |
| 0,75 | 3:4 |
| 1,78 | 16:9 |
| 0,56 | 9:16 |

En video som till exempel är 1440 bredd x 1080 höjd har proportionerna 1440/1080 eller 1,33. I det här fallet väljer du en förinställning för videokodning med 4:3-proportioner för att koda videofilen.

### Bithastighet {#bitrate}

Bithastighet är den mängd data som kodas för att skapa en enda sekund av videouppspelning. Bithastigheten mäts i kilobit per sekund (kbit/s).

>[!NOTE]
>
>Eftersom förlustgivande komprimering används för alla kodekar är bithastigheten den viktigaste faktorn i videokvaliteten. Ju mer du komprimerar en videofil desto sämre blir kvaliteten. Därför är alla andra egenskaper lika (upplösning, bildrutehastighet och kodek), ju lägre bithastighet, desto lägre kvalitet får den komprimerade filen.

När du väljer en bithastighetskodning kan du välja mellan två typer:

* **[!UICONTROL Constant Bitrate Encoding]** (CBR) - Under CBR-kodning är bithastigheten eller antalet bitar per sekund densamma under hela kodningsprocessen. CBR-kodning bevarar den angivna datahastigheten enligt inställningen för hela videon. CBR-kodning optimerar inte heller mediefiler för kvalitet utan sparar på lagringsutrymmet.
Använd CBR om videon innehåller en liknande rörelsenivå i hela videon. CBR används oftast för direktuppspelat videoinnehåll. Se även [Använda egna parametrar för videokodning](/help/assets/dynamic-media/video-profiles.md#using-custom-added-video-encoding-parameters).

* **[!UICONTROL Variable Bitrate Encoding]** (VBR) - VBR-kodning justerar datahastigheten nedåt och till den övre gräns som du anger, baserat på de data som krävs av kompressorn. Den här funktionen innebär att under en VBR-kodningsprocess ökar eller minskar bithastigheten för mediefilen dynamiskt beroende på mediafilens behov av bithastighet.
VBR tar längre tid att koda men ger det mest fördelaktiga resultatet. mediefilens kvalitet är överlägsen. VBR används oftast för http-progressiv leverans av videoinnehåll.

När använder du VBR jämfört med CRB?
När du väljer VBR jämfört med CBR rekommenderar vi nästan alltid att du använder VBR för dina mediefiler. VBR ger filer av högre kvalitet med konkurrenskraftiga bithastigheter. När du använder VBR måste du vara säker på att du använder kodning i två omgångar och ställa in den maximala bithastigheten till 1,5 gånger målvideobithastigheten.

När du väljer en förinställning för videokodning måste du ta hänsyn till målanvändarens anslutningshastighet. Välj en förinställning med en datahastighet som är 80 % av den hastigheten. Om målanvändarens anslutningshastighet till exempel är 1 000 kbit/s är den bästa förinställningen en med en videodatahastighet på 800 kbit/s.

I den här tabellen beskrivs datahastigheten för typiska anslutningshastigheter.

| Hastighet (kbit/s) | Anslutningstyp |
|--- |--- |
| 256 | Uppringd anslutning. |
| 800 | Vanlig mobilanslutning. För den här anslutningen anger du en datahastighet mellan 400 och maximalt 800 för 3G-upplevelser som mål. |
| 2000 | Vanlig anslutning till stationär bredbandsuppkoppling. För den här anslutningen anger du en datahastighet i intervallet 800-2000 kbit/s med de flesta mål som är i genomsnitt 1200-1500 kbit/s. |
| 5000 | Vanlig bredbandsanslutning. Kodning i det här övre intervallet rekommenderas inte eftersom videoleverans i den här hastigheten inte är tillgänglig för de flesta konsumenter. |

### Upplösning {#resolution}

**Upplösning** beskriver videofilens höjd och bredd i pixlar. Den mesta källvideon lagras med hög upplösning (till exempel 1 920 x 1 080). Vid direktuppspelning komprimeras källvideo till en lägre upplösning (640 x 480 eller lägre).

Upplösning och datahastighet är två sammankopplade faktorer som avgör videokvaliteten. Om du vill behålla samma videokvalitet måste datahastigheten vara högre ju fler pixlar en videofil har (ju högre upplösning). Ta till exempel antalet pixlar per bildruta i en 320 x 240-upplösning och en 640 x 480-upplösningsvideofil:

| Upplösning | Pixlar per bildruta |
|--- |--- |
| 320 x 240 | 76 800 |
| 640 x 480 | 307 200 |

Filen på 640 x 480 har fyra gånger fler pixlar per bildruta. För att uppnå samma datahastighet för dessa två exempelupplösningar tillämpar du fyra gånger komprimeringen på 640 x 480-filen, vilket kan minska videons kvalitet. En videodatahastighet på 250 kbit/s ger därför en högkvalitativ bild med upplösningen 320 x 240, men inte med upplösningen 640 x 480.

I allmänhet gäller att ju högre datahastighet du använder, desto bättre utseende på videon och ju högre upplösning du använder, desto högre datahastighet måste du behålla visningskvaliteten (jämfört med lägre upplösningar).

Eftersom upplösning och datahastighet är länkade finns det två alternativ när du kodar video:

* Välj en datahastighet och koda sedan med den högsta upplösningen som ser bra ut med den datahastighet du väljer.
* Välj en upplösning och koda sedan med den datahastighet som krävs för att få en video med hög kvalitet med den upplösning du väljer.

När du väljer (eller skapar) en förinställning för videokodning för den primära källvideofilen använder du den här tabellen för att ange rätt upplösning:

| Upplösning | Höjd (pixlar) | Skärmstorlek |
|--- |--- |--- |
| 240p | 240 | Liten skärm |
| 300p | 300 | Liten skärm för mobila enheter |
| 360p | 360 | Liten skärm |
| 480p | 480 | Medelstor skärm |
| 720p | 720 | Stor skärm |
| 1080p | 1080 | Stor HD-skärm |

### Fps (bildrutor per sekund) {#fps-frames-per-second}

I USA och Japan spelas de flesta videoklipp in med 29,97 bildrutor per sekund (fps). i Europa spelas de flesta videoklipp in med 25 bildrutor per sekund. Film filmas med 24 fps.

Välj en förinställning för videokodning som matchar fps-hastigheten för den primära källvideofilen. Om den primära källvideon till exempel är 25 fps väljer du en kodningsförinställning med 25 fps. Som standard används den primära källvideofilens fps för all anpassad kodning. Därför behöver du inte uttryckligen ange fps-inställningen när du skapar en förinställning för videokodning.

### Videokodningsdimensioner {#video-encoding-dimensions}

För bästa resultat väljer du kodningsdimensioner så att källvideon är en hel multipel av alla dina kodade videor.

Om du vill beräkna förhållandet dividerar du källbredden med den kodade bredden för att få breddförhållandet. Sedan dividerar du källhöjden med kodad höjd för att få höjdförhållandet.

Om förhållandet är ett heltal betyder det att videon är optimalt skalad. Om den resulterande kvoten inte är ett heltal påverkas videokvaliteten genom att kvarvarande pixelartefakter lämnas kvar på skärmen. Effekten märks mest när videon innehåller text.

Anta till exempel att källvideon är 1 920 x 1 080. I följande tabell ger de tre kodade videoklippen de optimala kodningsinställningarna som kan användas.

| Videotyp | Bredd x höjd | Breddförhållande | Höjdförhållande |
|--- |--- |--- |--- |
| Källa | 1920 x 1080 | 1 | 1 |
| Kodad | 960 x 540 | 2 | 2 |
| Kodad | 640 x 360 | 3 | 1 |
| Kodad | 480 x 270 | 4 | 4 |

### Kodat videofilformat {#encoded-video-file-format}

Dynamic Media rekommenderar att du använder MP4 H.264-videokodningsförinställningar. Eftersom MP4-filer använder H.264-videokodeken ger den video med hög kvalitet men i en komprimerad filstorlek.

## Publicera videofilmer till YouTube {#publishing-videos-to-youtube}

Du kan publicera videoresurser som hanteras i Experience Manager Assets direkt i en YouTube-kanal som du tidigare har skapat.

Om du vill publicera videomaterial till YouTube taggar du videomaterial i Experience Manager Assets med taggar. Du kopplar dessa taggar till en YouTube-kanal. Om videoresursens tagg matchar taggen för en YouTube-kanal publiceras videon till YouTube. Publicera till YouTube sker tillsammans med en normal publicering av videon så länge en associerad tagg används.

YouTube gör sin egen kodning. Det innebär att den ursprungliga videofilen som överfördes till Experience Manager publiceras till YouTube i stället för någon videoåtergivning som Dynamic Media kodning har skapat. Även om det inte krävs för att bearbeta videofilmer med Dynamic Media förväntas de göra det om en visningsförinställning behövs för uppspelning.

När du åsidosätter videobearbetningsprofilen och publicerar direkt till YouTube innebär det helt enkelt att videomaterialet i Experience Manager Asset inte får någon miniatyrbild som kan visas. Det innebär också att videoklipp som inte är kodade inte fungerar med någon av Dynamic Media resurstyper.

När du publicerar videomaterial till YouTube-servrar utför du följande uppgifter för att säkerställa säker server-till-server-autentisering med YouTube:

1. [Konfigurera inställningar för Google Cloud](#configuring-google-cloud-settings)
1. [Skapa en YouTube-kanal](#creating-a-youtube-channel)
1. [Lägga till taggar för publicering](#adding-tags-for-publishing)
1. [Konfigurera YouTube i Experience Manager](#setting-up-youtube-in-aem)
1. [(Valfritt) Automatisera inställningen av YouTube standardegenskaper för dina överförda videofilmer](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [Publicera videor i din YouTube-kanal](#publishing-videos-to-your-youtube-channel)
1. [(Valfritt) Verifiera publicerad video på YouTube](/help/assets/dynamic-media/video.md#optional-verifying-the-published-video-on-youtube)
1. [Länka YouTube-URL:er till ditt webbprogram](#linking-youtube-urls-to-your-web-application)

Du kan även [avpublicera videoklipp för att ta bort dem från YouTube](#unpublishing-videos-to-remove-them-from-youtube).

### Konfigurera inställningar för Google Cloud {#configuring-google-cloud-settings}

Du behöver ett Google-konto för att publicera till YouTube. Om du har ett GMAIL-konto har du redan ett Google-konto; Om du inte har något Google-konto kan du enkelt skapa ett. Du behöver kontot eftersom du behöver inloggningsuppgifter för att publicera videoresurser på YouTube. Om du redan har skapat ett konto hoppar du över den här uppgiften och fortsätter direkt till [Skapa en YouTube-kanal](#creating-a-youtube-channel).

Kontot som används med Google Cloud och Google-kontot som används för YouTube behöver inte vara samma.

Google ändrar regelbundet användargränssnittet. Stegen för att publicera videofilmer till YouTube kan därför variera något från vad som beskrivs nedan. Denna caveat gäller även YouTube när du försöker kontrollera om videoklipp har överförts till det.

>[!NOTE]
>
>Följande steg var korrekta när detta skrevs. Google uppdaterar dock regelbundet sina webbplatser utan föregående meddelande. De här stegen kan därför vara något annorlunda.

Så här konfigurerar du Google Cloud-inställningar:

1. Skapa ett Google-konto.
   [https://accounts.google.com/SignUp?service=mail](https://accounts.google.com/SignUp?service=mail)

   Om du redan har ett Google-konto går du vidare till nästa steg.

1. Gå till [https://cloud.google.com/](https://cloud.google.com/).
1. På Google Cloud-sidan uppe till höger klickar du på **[!UICONTROL Console]**.

   Om det behövs kan du **[!UICONTROL Sign in]** använda inloggningsuppgifterna för ditt Google-konto för att se alternativet **[!UICONTROL Console]**.

1. Klicka på listrutan Projekt till höger om **[!UICONTROL Google Cloud Platform]** på sidan Kontrollpanel för att öppna dialogrutan Välj ett projekt.
1. Tryck på **[!UICONTROL New Project]** i dialogrutan Välj ett projekt.

   ![6_5_googleaccount-newproject](assets/6_5_googleaccount-newproject.png)

1. Skriv namnet på det nya projektet i fältet Projektnamn i dialogrutan Nytt projekt.

   Ditt projekt-ID baseras på ditt projektnamn. Välj projektnamnet noggrant. den kan inte ändras efter att den har skapats. Du måste även ange samma projekt-ID igen när du konfigurerar YouTube i Experience Manager senare. Skriv därför ned den.

1. Klicka på **[!UICONTROL Create]**.

1. Gör något av följande:

   * Tryck på **[!UICONTROL Explore and enable APIs]** på Komma igång-kortet på Dashboard för ditt projekt.
   * Tryck på **[!UICONTROL Go to APIs overview]** i API-kortet på Dashboard för ditt projekt.

   ![6_5_googleaccount-apis-enable2](assets/6_5_googleaccount-apis-enable2.png)

1. Tryck på **[!UICONTROL Enable APIs and Services]** längst upp på sidan API:er och tjänster.
1. Tryck på **[!UICONTROL Category]** till vänster på sidan API-bibliotek. **[!UICONTROL YouTube]** Tryck på **[!UICONTROL YouTube Data API]** till höger på sidan.
1. Tryck på **[!UICONTROL Enable]** på sidan YouTube Data API v3.

   ![6_5_googleaccount-apis-enable3](assets/6_5_googleaccount-apis-enable3.png)

1. Om du vill använda API:t måste du ha autentiseringsuppgifter. Om det behövs klickar du på **[!UICONTROL Create Credentials]**.

   ![6_5_googleaccount-apis-createcredentials](assets/6_5_googleaccount-apis-createcredentials.png)

1. Gör följande på sidan **[!UICONTROL Add credentials to your project]**, steg 1:

   * I listrutan **[!UICONTROL Which API are you using?]** väljer du **[!UICONTROL YouTube Data API v3]**.

   * I listrutan **[!UICONTROL Where are you calling the API from?]** väljer du **[!UICONTROL Web Server (for example, node.js, Tomcat)]**.

   * Tryck på **[!UICONTROL User data]** i listrutan **[!UICONTROL What data are you accessing?]**.

   ![6_5_googleaccount-apis-createcredentials2](assets/6_5_googleaccount-apis-createcredentials2.png)

1. Tryck på **[!UICONTROL What credentials do I need?]**
1. I steg 2 på sidan **[!UICONTROL Add credentials to your project]** anger du ett unikt namn i fältet Namn under rubriken **[!UICONTROL Create an OAuth 2.0 client ID]**. Du kan också använda standardnamnet som anges av Google.
1. Under rubriken **[!UICONTROL Authorized JavaScript™ origins]** anger du följande sökväg i textfältet, ersätter din egen domän och portnummer i sökvägen och trycker sedan på **[!UICONTROL Enter]** för att lägga till sökvägen i listan:

   `https://<servername.domain>:<port_number>`

   Till exempel, `https://1a2b3c.mycompany.com:4321`

   **Obs**: Banexemplen ovan är endast avsedda som illustrationer.

   ![6_5_googleaccount-apis-createcredentials-oauth](assets/6_5_googleaccount-apis-createcredentials-oauth.png)

1. Under rubriken **[!UICONTROL Authorized redirect URIs]** anger du följande sökväg i textfältet, ersätter din egen domän och portnummer i sökvägen och trycker sedan på **[!UICONTROL Enter]** för att lägga till sökvägen i listan:

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   Till exempel, `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   **Obs**: Banexemplet ovan är endast avsett för illustrationsändamål.

1. Klicka på **[!UICONTROL Create OAuth client ID]**.
1. På sidan **[!UICONTROL Add credentials to your project]**, steg 3, under rubriken **[!UICONTROL Set up the OAuth 2.0 consent screen]**, väljer du den Gmail-e-postadress som du för närvarande använder.

   ![6_5_googleaccount-apis-createcredentials-consentscreen](assets/6_5_googleaccount-apis-createcredentials-consentscreen.png)

1. Under rubriken **[!UICONTROL Product name shown to users]**, i textfältet, anger du det du vill visa på godkännandeskärmen.

   Medgivandeskärmen visas för Experience Manager-administratören när de autentiserar sig för YouTube. Experience Manager kontaktar YouTube för tillstånd.

1. Klicka på **[!UICONTROL Continue]**.
1. Gå till sidan Lägg till inloggningsuppgifter för projektet och i steg 4, under rubriken **[!UICONTROL Download credentials]**, trycker du på **[!UICONTROL Download]**.

   ![6_5_googleaccount-apis-createcredentials-downloadcredentials](assets/6_5_googleaccount-apis-createcredentials-downloadcredentials.png)

1. Spara `client_id.json`-filen.

   Du behöver den här hämtade JSON-filen när du konfigurerar YouTube i Adobe Experience Manager senare.

1. Klicka på **[!UICONTROL Done]**.

   Logga ut från ditt Google-konto. Skapa nu en YouTube-kanal.

### Skapa en YouTube-kanal {#creating-a-youtube-channel}

Du måste ha en eller flera kanaler för att kunna publicera videofilmer på YouTube. Om du redan har skapat en YouTube-kanal kan du hoppa över den här uppgiften och gå till [Adding tags for publishing](/help/assets/dynamic-media/video.md#adding-tags-for-publishing).

>[!CAUTION]
>
>Kontrollera att du redan har konfigurerat en eller flera kanaler i YouTube *innan* du lägger till kanaler under YouTube Settings i Experience Manager (se [Konfigurera YouTube i Experience Manager](#setting-up-youtube-in-aem) nedan). Om du misslyckas med kanalkonfigurationen får du ingen varning om att det inte finns några befintliga kanaler. Google-autentisering sker dock fortfarande när du lägger till en kanal, men det finns inget alternativ för att välja vilken kanal videon skickas till.

Så här skapar du en YouTube-kanal:

1. Gå till [https://www.youtube.com](https://www.youtube.com/) och logga in med inloggningsuppgifterna för ditt Google-konto.
1. Klicka på din profilbild i det övre högra hörnet på YouTube-sidan (den kan också visas som en bokstav i en enfärgad cirkel) och tryck sedan på **[!UICONTROL YouTube settings]** (den runda kugghjulsikonen).
1. På sidan Översikt, under rubriken Ytterligare funktioner, trycker du på **[!UICONTROL See all my channels or create a new channel]**.
1. Tryck på **[!UICONTROL Create a new channel]** på sidan Kanaler.
1. På sidan Varumärkeskonto anger du ett företagsnamn eller ett annat kanalnamn som du väljer där du vill publicera videoresurserna i fältet Märkeskontonamn. Klicka sedan på **[!UICONTROL Create]**.

   Kom ihåg namnet som du anger här eftersom du måste ange det igen när du konfigurerar YouTube i Experience Manager.

1. (Valfritt) Lägg till fler kanaler om det behövs.

   Nu lägger du till taggar för publicering.

### Lägga till taggar för publicering {#adding-tags-for-publishing}

Om du vill publicera till dina videofilmer på YouTube associerar Experience Manager taggar till en eller flera YouTube-kanaler. Mer information om hur du lägger till taggar för publicering finns i [Administrera taggar](/help/sites-cloud/authoring/features/tags.md).

Om du tänker använda standardtaggarna i Experience Manager kan du hoppa över den här uppgiften och gå till [Konfigurera YouTube i Experience Manager](#setting-up-youtube-in-aem).

>[!NOTE]
>
>När Cloud Servicen har konfigurerats krävs ingen annan konfiguration för att aktivera YouTube Publish-replikeringsagenten. Orsaken är att den aktiverades när Cloud Servicens konfiguration sparades.

<!-- ### Enabling the YouTube Publish replication agent {#enabling-the-youtube-publish-replication-agent}

After you enable the YouTube Publish replication agent, if you want to test the connection to the Google Cloud account, tap **[!UICONTROL Test Connection]**. A browser tab displays the connection results. If you have added YouTube Channels, then a listing of those is displayed as part of the test.

1. In the upper-left corner of Experience Manager, click the Experience Manager logo, then in the left rail, click **[!UICONTROL Tools]** &gt; **[!UICONTROL Deployment]** &gt; **[!UICONTROL Replication]** &gt; **[!UICONTROL Agents on Author]**.
1. On the Agents of Author page, click **[!UICONTROL YouTube Publish (youtube)]**.
1. On the toolbar, to the right of Settings, click **[!UICONTROL Edit]**.
1. Select the **[!UICONTROL Enabled]** checkbox to turn on the replication agent.
1. Click **[!UICONTROL OK]**. -->

### Konfigurera YouTube i Experience Manager {#setting-up-youtube-in-aem}

Från och med Experience Manager 6.4 introducerades en ny pekgränssnittsmetod för att konfigurera YouTube-publicering i Experience Manager. Baserat på den installerade instansen av Experience Manager som du använder gör du något av följande:

* Information om hur du konfigurerar YouTube i Experience Manager före 6.4 finns i [Konfigurera YouTube i Experience Manager före 6.4](/help/assets/dynamic-media/video.md#setting-up-youtube-in-aem-before).
* Information om hur du konfigurerar YouTube i Experience Manager 6.4 eller senare finns i [Konfigurera YouTube i Experience Manager 6.4 och senare](#setting-up-youtube-in-aem-and-later).

#### Konfigurera YouTube i Experience Manager 6.4 och senare {#setting-up-youtube-in-aem-and-later}

1. Se till att du loggar in på din instans av Dynamic Media som administratör.
1. I det övre vänstra hörnet av Experience Manager trycker du på logotypen för Experience Manager och sedan på **[!UICONTROL Tools]**(hammer icon) > **[!UICONTROL Cloud Services]** > **[!UICONTROL YouTube Publishing Configuration]** i det vänstra hörnet.
1. Tryck på **[!UICONTROL global]** (markera det inte).

1. I det övre högra hörnet av den globala sidan trycker du på **[!UICONTROL Create]**.
1. På sidan Skapa YouTube-konfiguration anger du Googles projekt-ID under Inställningar för Google Cloud-plattform i fältet **[!UICONTROL Application Name]**.

   Du angav projekt-ID när du konfigurerade Google Cloud-inställningarna tidigare.
Lämna sidan Skapa YouTube-konfiguration öppen; du återgår till det om en stund.

   ![6_5_youtubepublish-createUtubeConfiguration](assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. Öppna JSON-filen som du hämtade och sparade tidigare i uppgiften [Konfigurera inställningarna för Google Cloud](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings) med en vanlig textredigerare.
1. Markera och kopiera hela JSON-texten.
1. Återgå till dialogrutan YouTube-kontoinställningar Klistra in JSON-texten i fältet **[!UICONTROL JSON Config]**.
1. Tryck på **[!UICONTROL Save]** i sidans övre högra hörn.

   Nu ska du konfigurera YouTube-kanaler i Experience Manager.

1. Tryck på **[!UICONTROL Add Channel]**.
1. I fältet Kanalnamn anger du namnet på kanalen som du skapade i uppgiften **[!UICONTROL Adding one or more channels to YouTube]** tidigare.

   Om du vill kan du lägga till en beskrivning.

1. Tryck på **[!UICONTROL Add]**.
1. YouTube/Google-autentisering visas. Om du inte redan är inloggad på Google Cloud-kontot hoppar du över det här steget.

   * Ange det Google-användarnamn och lösenord som är kopplat till Googles projekt-ID och JSON-texten ovan.
   * Beroende på hur många kanaler ditt konto har visas två eller flera objekt. Välj en kanal. Ange inte e-postadressen. det är inte en kanal.
   * På nästa sida trycker du på **[!UICONTROL Accept]** för att tillåta åtkomst till den här kanalen.

1. Tryck på **[!UICONTROL Allow]**.

   Du kommer nu att konfigurera taggar för publicering.

1. **[!UICONTROL Setting up tags for publishing]** - Tryck på pennikonen på Cloud Services > YouTube för att redigera listan med taggar som du vill använda.
1. Om du vill visa en lista med tillgängliga taggar i Experience Manager trycker du på ikonen för nedrullningsbar lista (cirkumflex upp och ned).
1. Om du vill lägga till dem trycker du på en eller flera taggar.

   Om du vill ta bort en tagg som du har lagt till markerar du taggen och trycker på **[!UICONTROL X]**.

1. När du är klar med att lägga till de taggar du vill ha trycker du på **[!UICONTROL Save]**.

   Nu kan du publicera videor i din YouTube-kanal.

#### Konfigurera YouTube i Experience Manager före 6.4 {#setting-up-youtube-in-aem-before}

1. Se till att du loggar in på din instans av Dynamic Media som administratör.

1. I det övre vänstra hörnet av Experience Manager trycker du på logotypen för Experience Manager och sedan på **[!UICONTROL Tools]** (hammarikon) > **[!UICONTROL Deployment]** > **[!UICONTROL Cloud Services]** till vänster.
1. Tryck på **[!UICONTROL Configure now]** under rubriken Tredjepartstjänster, under YouTube.
1. I dialogrutan Skapa konfiguration anger du en rubrik (obligatoriskt) och ett namn (valfritt) i respektive fält.
1. Tryck på **[!UICONTROL Create]**.
1. I dialogrutan YouTube-kontoinställningar anger du Googles projekt-ID i fältet **[!UICONTROL Application Name]**.

   Du angav projekt-ID när du först [konfigurerade Google Cloud-inställningar](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings) tidigare.
Lämna dialogrutan YouTube Kontoinställning öppen; du återgår till det om en stund.

1. Öppna JSON-filen som du hämtade och sparade tidigare i uppgiften Konfigurera inställningarna för Google Cloud med en vanlig textredigerare.
1. Markera och kopiera hela JSON-texten.
1. Återgå till dialogrutan YouTube-kontoinställningar Klistra in JSON-texten i fältet **[!UICONTROL JSON Config]**.
1. Tryck på **[!UICONTROL OK]**.

   Nu ska du konfigurera YouTube-kanaler i Experience Manager.

1. Till höger om **[!UICONTROL Available Channels]** trycker du på **+** (plustecknet).
1. I dialogrutan YouTube-kanalinställningar, i fältet Titel, anger du namnet på kanalen som du skapade i uppgiften **[!UICONTROL Adding one or more channels to YouTube]** tidigare.

   Om du vill kan du lägga till en beskrivning.

1. Tryck på **[!UICONTROL OK]**.
1. YouTube/Google-autentisering visas. Om du inte redan är inloggad på Google Cloud-kontot hoppar du över det här steget.

   * Ange det Google-användarnamn och lösenord som är kopplat till Googles projekt-ID och JSON-texten ovan.
   * Beroende på hur många kanaler ditt konto har visas två eller flera objekt. Välj en kanal. Ange inte e-postadressen. det är inte en kanal.
   * På nästa sida trycker du på **[!UICONTROL Accept]** för att tillåta åtkomst till den här kanalen.

1. Tryck på **[!UICONTROL Allow]**.

   Du kommer nu att konfigurera taggar för publicering.

1. **[!UICONTROL Setting up tags for publishing]** - Tryck på pennikonen på Cloud Services > YouTube för att redigera listan med taggar som du vill använda.
1. Om du vill visa en lista med tillgängliga taggar i Experience Manager trycker du på ikonen för nedrullningsbar lista (cirkumflex upp och ned).
1. Om du vill lägga till dem trycker du på en eller flera taggar.

   Om du vill ta bort en tagg som du har lagt till markerar du taggen och trycker på **X**.

1. När du är klar med att lägga till de taggar du vill ha trycker du på **[!UICONTROL OK]**.

   Nu kan du publicera videor i din YouTube-kanal.

### (Valfritt) Automatisera inställningen av YouTube standardegenskaper för dina överförda videofilmer {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

Du kan även automatisera inställningen av YouTube-egenskaper när du överför videoklipp. Skapa en metadatabearbetningsprofil i Experience Manager.

Om du vill skapa en profil för metadatabearbetning kopierar du först värden från fälten **[!UICONTROL Field Label]**, **[!UICONTROL Map to property]** och **[!UICONTROL Choices]**, som alla finns i metadatascheman för video. Sedan skapar du en YouTube-metadatabearbetningsprofil för video genom att lägga till dessa värden.

Så här automatiserar du inställningen av YouTube standardegenskaper för överförda videofilmer:

1. Klicka på Experience Manager-logotypen i det övre vänstra hörnet av Experience Manager och klicka sedan på **[!UICONTROL Tools]** (hammarikon) > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]** i det vänstra hörnet.
1. Klicka på **[!UICONTROL default]**. (Lägg inte till en bockmarkering i markeringsrutan till vänster om &quot;standard&quot;.)
1. Markera rutan till vänster om **[!UICONTROL video]** på **[!UICONTROL default]**-sidan och klicka sedan på **[!UICONTROL Edit]**.
1. Klicka på fliken **[!UICONTROL Advanced]** på sidan Redigerare för metadatamodeller.
1. Under rubriken YouTube-publicering klickar du på **[!UICONTROL YouTube Category]**.
1. Till höger på sidan, under fliken **[!UICONTROL Settings]**, gör du följande:

   * Markera och kopiera värdet i textfältet **[!UICONTROL Map to property]**.
Klistra in det kopierade värdet i den öppna textredigeraren. Du kommer att behöva det här värdet senare när du skapar din metadatabearbetningsprofil. Låt textredigeraren vara öppen.

   * Under **[!UICONTROL Choices]** markerar och kopierar du standardvärdet som du vill använda (till exempel Folk &amp; bloggar eller Vetenskap och teknik).
Klistra in det kopierade värdet i den öppna textredigeraren. Du kommer att behöva det här värdet senare när du skapar din metadatabearbetningsprofil. Låt textredigeraren vara öppen.

1. Under rubriken YouTube-publicering klickar du på **[!UICONTROL YouTube Privacy]**.
1. Till höger på sidan, under fliken **[!UICONTROL Settings]**, gör du följande:

   * Markera och kopiera värdet i textfältet **[!UICONTROL Map to property]**.
Klistra in det kopierade värdet i den öppna textredigeraren. Du kommer att behöva det här värdet senare när du skapar din metadatabearbetningsprofil. Låt textredigeraren vara öppen.

   * Under **[!UICONTROL Choices]** markerar och kopierar du standardvärdet som du vill använda. Observera att alternativen grupperas i par om två. Det undre fältet i paret är standardvärdet som du vill kopiera, till exempel public, unlisted eller private.
Klistra in det kopierade värdet i den öppna textredigeraren. Du kommer att behöva det här värdet senare när du skapar din metadatabearbetningsprofil. Låt textredigeraren vara öppen.

1. Klicka på **[!UICONTROL Cancel]** i det övre högra hörnet på sidan för redigering av metadatamodell.
1. I det övre vänstra hörnet av Experience Manager trycker du på logotypen för Experience Manager och sedan på **[!UICONTROL Tools]** (hammarikon) > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]** till vänster.

1. Klicka på **[!UICONTROL Create]** längst upp till höger på sidan Metadataprofiler.
1. I dialogrutan Lägg till metadataprofil i textfältet **[!UICONTROL Profile title]** anger du namnet `YouTube Video` och sedan klickar du på **[!UICONTROL Create]**.
1. Klicka på fliken **[!UICONTROL Advance]** på sidan Redigerare för metadataprofil.
1. Lägg till de kopierade YouTube Publishing-värdena i profilen genom att göra följande:

   * Klicka på fliken **[!UICONTROL Build Form]** till höger på sidan.
   * (Valfritt) Dra komponenten **[!UICONTROL Section Header]** till vänster och släpp den i formulärområdet.
   * (Valfritt) Klicka på **[!UICONTROL Field Label]** för att markera komponenten.
   * (Valfritt) Till höger på sidan skriver du `YouTube Publishing` under fliken Inställningar i textfältet Fältetikett.
   * Klicka på fliken **[!UICONTROL Build Form]** och dra sedan komponenten **[!UICONTROL Multi Value Text]** och släpp den under rubriken **[!UICONTROL YouTube Publishing]** som du skapade.

   * Om du vill markera komponenten klickar du på **[!UICONTROL Field Label]**.
   * Till höger på sidan, under fliken Inställningar, klistrar du in de YouTube Publishing-värden (Field Label-värde och Map to property-värde) som du kopierade tidigare i deras respektive fält i formuläret. Klistra in alternativvärdet i fältet Standardvärde.

1. Lägg till de kopierade sekretessvärdena för YouTube till profilen genom att göra följande:

   * Klicka på fliken **[!UICONTROL Build Form]** till höger på sidan.
   * (Valfritt) Dra komponenten **[!UICONTROL Section Header]** till vänster och släpp den i formulärområdet.
   * (Valfritt) Klicka på **[!UICONTROL Field Label]** för att markera komponenten.
   * (Valfritt) Till höger på sidan skriver du `YouTube Privacy` under fliken Inställningar i textfältet Fältetikett.
   * Klicka på fliken **[!UICONTROL Build Form]** och dra sedan komponenten **[!UICONTROL Multi Value Text]** och släpp den under rubriken **[!UICONTROL YouTube Privacy]** som du skapade.

   * Om du vill markera komponenten klickar du på **[!UICONTROL Field Label]**.
   * Till höger på sidan, under fliken Inställningar, klistrar du in de YouTube Publishing-värden (Field Label-värde och Map to property-värde) som du kopierade tidigare i deras respektive fält i formuläret. Klistra in alternativvärdet i fältet Standardvärde.

1. Klicka på **[!UICONTROL Save]** i det övre högra hörnet på sidan.
1. Använd metadataprofilen för YouTube Publishing på de mappar där du ska överföra videoklipp. Du måste ha angett både Metadataprofil och Videoprofil.

   Se [Metadataprofiler](/help/assets/metadata-profiles.md) och [Videoprofiler](/help/assets/dynamic-media/video-profiles.md).

### Publicera videor i din YouTube-kanal {#publishing-videos-to-your-youtube-channel}

Nu kopplar du taggarna som du lade till tidigare till videoresurser. På så sätt kan Experience Manager veta vilka mediefiler som ska publiceras i din YouTube-kanal.

>[!NOTE]
>
>Publicera direkt publicerar inte automatiskt till YouTube. När Dynamic Media har konfigurerats finns det två publiceringsalternativ att välja mellan, **[!UICONTROL Immediately]** och **[!UICONTROL Upon Activation]**.
>
>**[!UICONTROL Publish Immediately]** betyder att den överförda resursen - efter att den har synkroniserats med IPS - automatiskt publiceras till leveranssystemet. Det gäller Dynamic Media, men inte YouTube. Om du vill publicera till YouTube måste du publicera via Experience Manager Author.

>[!NOTE]
För att publicera innehåll från YouTube använder Experience Manager arbetsflödet **[!UICONTROL Publish to YouTube]**, som gör att du kan övervaka förloppet och visa felinformation.
Se [Övervaka videokodning och publiceringsförlopp på YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).
Mer detaljerad förloppsinformation finns i YouTube-loggen som replikeras. Tänk dock på att sådan övervakning kräver administratörsåtkomst.

**Så här publicerar du videor i din YouTube-kanal**:

1. I Experience Manager navigerar du till en videoresurs som du vill publicera i din YouTube-kanal.
1. Välj videoresurs (den adaptiva videouppsättningen).
1. Klicka på **[!UICONTROL Properties]** i verktygsfältet.
1. Klicka på **[!UICONTROL Open Selection Dialog]** till höger om fältet Taggar under rubriken Metadata på fliken Grundläggande.
1. På sidan Välj taggar navigerar du till de taggar du vill använda och markerar sedan en eller flera taggar.

   Kom ihåg att taggarna måste kopplas till YouTube-kanalen.

1. Klicka på **[!UICONTROL Select]** i det övre högra hörnet på sidan.
1. Klicka på **[!UICONTROL Save and Close]** i det övre högra hörnet på egenskapssidan för videon.
1. Klicka på **[!UICONTROL Quick Publish]** i verktygsfältet.

   Se även [Använda Publiceringshantering med Experience Manager Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html#page-authoring).

   Du kan även verifiera den publicerade videon på din YouTube-kanal.

### (Valfritt) Verifiera den publicerade videon på YouTube {#optional-verifying-the-published-video-on-youtube}

Du kan också övervaka förloppet för din YouTube-publicering (eller avpublicering).

Se [Övervaka videokodning och publiceringsförlopp på YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

Publiceringstiderna kan variera avsevärt beroende på olika faktorer, bland annat formatet för den primära källvideon, filstorleken och överföringstrafiken. Publiceringsprocessen kan ta från några minuter till flera timmar. Högre upplösningsformat återges dessutom mycket långsammare. 720p och 1080p tar till exempel längre tid att visa än 480p.

Efter åtta timmar, om du fortfarande ser ett statusmeddelande som säger **[!UICONTROL Uploaded (processing, please wait)]**, kan du försöka ta bort videon från webbplatsen och överföra den igen.

### Länka YouTube URL:er till ditt webbprogram {#linking-youtube-urls-to-your-web-application}

Du kan hämta en YouTube URL-sträng som genereras av Dynamic Media när du har publicerat videon. När du kopierar YouTube-URL:en markeras den i Urklipp så att du kan klistra in den på sidor på webbplatsen eller i programmet.

>[!NOTE]
YouTube-URL:en kan inte kopieras förrän du har publicerat videoresursen till YouTube.

Så här länkar du YouTube URL:er till ditt webbprogram:

1. Navigera till den *YouTube-publicerade* videoresurs vars URL du vill kopiera och markera den.

   Kom ihåg att YouTube URL:er endast är tillgängliga för kopiering *efter* att du först *har publicerat* videomaterialet till YouTube.

1. Klicka på **[!UICONTROL Properties]** i verktygsfältet.
1. Klicka på fliken **[!UICONTROL Advanced]**.
1. Under rubriken YouTube Publishing (Publicering), i YouTube URL List, markerar och kopierar du URL-texten till webbläsaren för att förhandsgranska resursen eller lägga till den på webbinnehållssidan.

### Avpublicerar videoklipp för att ta bort dem från YouTube {#unpublishing-videos-to-remove-them-from-youtube}

När du avpublicerar en videoresurs i Experience Manager tas videon bort från YouTube.

>[!CAUTION]
Om du tar bort en video direkt från YouTube är Experience Manager inte medveten om det och fortsätter att bete sig som om videon fortfarande publiceras till YouTube. Avpublicera alltid en videoresurs från YouTube via Experience Manager.

>[!NOTE]
Experience Manager använder arbetsflödet **[!UICONTROL Unpublish from YouTube]** för att ta bort innehåll från YouTube, vilket gör att du kan övervaka förloppet och visa felinformation.
Se [Övervaka videokodning och publiceringsförlopp på YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

Så här avpublicerar du videoklipp för att ta bort dem från YouTube:

1. Navigera till de videoresurser som du vill avpublicera från din YouTube-kanal.
1. Välj en eller flera publicerade videoresurser i ett resursurvalsläge.
1. Klicka på **[!UICONTROL Manage Publication]** i verktygsfältet. Tryck vid behov på ikonen med tre punkter (. . .) i verktygsfältet för att se **[!UICONTROL Manage Publication]**.
1. Tryck på **[!UICONTROL Unpublish]** på sidan Hantera publikation.
1. Tryck på **[!UICONTROL Next]** i det övre högra hörnet på sidan.
1. Tryck på **[!UICONTROL Unpublish]** i det övre högra hörnet på sidan.

## Övervaka videokodning och YouTube publiceringsförlopp {#monitoring-video-encoding-and-youtube-publishing-progress}

När du överför en ny video till en mapp där videokodning används eller publicerar videon till YouTube, ska du övervaka hur videokodningen/YouTube-publiceringen fortskrider (eller misslyckas). Publiceringsförloppet för YouTube är endast tillgängligt via loggarna. Oavsett om det misslyckas eller lyckas visas det på andra sätt som beskrivs i följande procedur. Dessutom får du e-postmeddelanden när en YouTube-publiceringsarbetsgång eller videokodning har slutförts eller avbrutits.

### Övervaka förlopp {#monitoring-progress}

Så här övervakar du förloppet (inklusive misslyckad kodning/YouTube-publicering):

1. Visa kodningsförloppet för video i resursmappen:

   * I kortvyn visas videokodningsförloppet för resursen i procent. Om ett fel uppstår visas även den här informationen på resursen.

   ![chlimage_1-429](assets/chlimage_1-429.png)

   * I listvyn visas videokodningsförloppet i kolumnen **[!UICONTROL Processing Status]**. Om ett fel uppstår visas det här meddelandet i samma kolumn.

   ![chlimage_1-430](assets/chlimage_1-430.png)

   Den här kolumnen visas inte som standard. Om du vill aktivera kolumnen väljer du **[!UICONTROL View Settings]** i listrutan Vyer, lägger till kolumnen **[!UICONTROL Processing Status]** och trycker eller klickar på **[!UICONTROL Update]**.

   ![chlimage_1-431](/help/assets/dynamic-media/assets/chlimage_1-431.png)

1. Visa förloppet i tillgångsinformationen. När du trycker eller klickar på en resurs öppnar du den nedrullningsbara menyn och väljer **[!UICONTROL Timeline]**. Om du vill begränsa det till arbetsflödesaktiviteter som kodning eller YouTube-publicering väljer du **[!UICONTROL Workflows]**.

   ![chlimage_1-432](assets/chlimage_1-432.png)

   All arbetsflödesinformation, till exempel kodning, visas på tidslinjen. För YouTube-publicering innehåller tidslinjen för arbetsflödet även namnet på YouTube-kanalen och YouTube video-URL:en. Dessutom visas felmeddelanden på tidslinjen i arbetsflödet när publiceringen är klar.

   >[!NOTE]
   Det kan ta lång tid innan fel-/felmeddelanden slutligen registreras på grund av flera arbetsflödeskonfigurationer på **[!UICONTROL retries]**, **[!UICONTROL retry delay]** och **[!UICONTROL timeout]** från [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), till exempel:
   * Konfiguration av Apache Sling-jobbkö
   * Adobe Granite Workflow External Process Job Handler
   * Timeoutkö för Granite-arbetsflöde

   Du kan justera egenskaperna **[!UICONTROL retries]**, **[!UICONTROL retry delay]** och **[!UICONTROL timeout]** i dessa konfigurationer.

1. Information om pågående arbetsflöden finns i Arbetsflödesinstanser som är tillgängliga i **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Instances]**.

   >[!NOTE]
   Du behöver administratörsbehörighet för att komma åt **[!UICONTROL Tools]**-menyn.

   ![chlimage_1-433](assets/chlimage_1-433.png)

   Markera instansen och tryck eller klicka på **[!UICONTROL Open History]**.

   ![chlimage_1-434](/help/assets/dynamic-media/assets/chlimage_1-434.png)

   I området Arbetsflödesinstanser kan du även göra uppehåll i, avsluta eller byta namn på arbetsflöden. Mer information finns i [Administrera arbetsflöden](/help/sites-cloud/authoring/workflows/overview.md).

1. Information om misslyckade jobb finns i Arbetsflödesfel i **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Failures]**. I listan **[!UICONTROL Workflow Failure]** visas alla misslyckade arbetsflödesaktiviteter.

   >[!NOTE]
   Du behöver administratörsbehörighet för att komma åt **[!UICONTROL Tools]**-menyn.

   ![chlimage_1-435](assets/chlimage_1-435.png)

   >[!NOTE]
   Det kan ta lång tid innan felmeddelandet slutligen spelas in på grund av flera arbetsflödeskonfigurationer på **[!UICONTROL retries]**, **[!UICONTROL retry delay]** och **[!UICONTROL timeout]** från [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), till exempel:
   * Konfiguration av Apache Sling-jobbkö
   * Adobe Granite Workflow External Process Job Handler
   * Timeoutkö för Granite-arbetsflöde

   Du kan justera egenskaperna **[!UICONTROL retries]**, **[!UICONTROL retry delay]** och **[!UICONTROL timeout]** i dessa konfigurationer.

1. Information om slutförda arbetsflöden finns i Arbetsflödesarkiv som är tillgängligt från **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Archive]**. **[!UICONTROL Workflow Archive]** visar alla slutförda arbetsflödesaktiviteter.

   >[!NOTE]
   Du behöver administratörsbehörighet för att komma åt **[!UICONTROL Tools]**-menyn.

   ![chlimage_1-436](assets/chlimage_1-436.png)

1. Du får e-postmeddelanden om avbrutna eller misslyckade arbetsflödesjobb. Dessa e-postmeddelanden kan konfigureras av en administratör. Se [Konfigurera e-postmeddelanden](#configuring-e-mail-notifications).

<!-- EMAIL NOT AVAILABLE IN SKYLINE

#### Configuring e-mail notifications {#configuring-e-mail-notifications}

>[!NOTE]
>
>You may need administrative rights to access the **[!UICONTROL Tools]** menu.

How you configure notification depends on whether you want notifications for YouTube publishing jobs.

* For encoding jobs, you can access the configuration page for all Experience Manager workflow email notifications at **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]** and by searching for **[!UICONTROL Day CQ Workflow Email Notification Service]**. You can select or clear the check boxes for **[!UICONTROL Notify on Abort]** or **[!UICONTROL Notify on Complete]** accordingly.

For YouTube publishing jobs, do the following:

1. In Experience Manager, tap **[!UICONTROL Tools]** &gt; **[!UICONTROL Workflow]** &gt; **[!UICONTROL Models]**.
1. On the Workflow Models page, select **[!UICONTROL Publish to YouTube]**, then tap **[!UICONTROL Edit]** on the toolbar.
1. Near the upper-right corner of the Publish to YouTube workflow page, tap **[!UICONTROL Edit]**.
1. Hover the mouse pointer on the YouTube Upload component, then tap once to display the inline toolbar.

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. On the inline toolbar, tap the Configuration icon (wrench). Click the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. In the YouTube Upload Process - Step Properties dialog box, tap the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. You can select or clear the following check boxes:

    * Publish Start
    * Publish Failure
    * Publish Completion - includes information on channels and URLs

   Clearing a check box means that you will not receive the specified email notification from the YouTube Publish workflow.

   >[!NOTE]
   >
   >These emails are specific to YouTube and are in addition to the generic workflow email notifications. As a result, you may receive two sets of email notification - the generic notification available in the **[!UICONTROL Day CQ Workflow Email Notification Service]** and one specific to YouTube depending on your configuration settings.

1. When you are finished, near the upper-right corner of the dialog box, tap the **[!UICONTROL Done]** icon (check mark).
1. On the Publish to YouTube workflow page, near the upper-right corner, tap **[!UICONTROL Sync]**.

-->

## Visa videorapporter {#viewing-video-reports}

>[!NOTE]
Videorapporter är bara tillgängliga när du kör Dynamic Media - hybrid-läge.

Videorapporter visar flera aggregerade mätvärden för en angiven period så att du kan övervaka att *publicerade* enskilda och aggregerade videor fungerar som förväntat. Följande viktigaste mätdata samlas in för alla publicerade videor på hela webbplatsen:

* Video börjar
* Slutförandefrekvens
* Genomsnittlig tid för video
* Total tid för video
* Videor per besök

En tabell över alla *publicerade* videoklipp listas också så att du kan spåra de mest visade videoklippen på din webbplats baserat på den totala videostarten.

När du trycker på ett videonamn i listan visas videons rapport för att behålla tittare (bortfall) i form av ett linjediagram. Diagrammet visar antalet vyer för en given tidpunkt under videouppspelning. När du spelar upp videon synkroniseras det lodräta strecket med tidsindikatorn i spelaren. Släppningar i linjediagramdata indikerar var publiken slutar intressera sig.

Om videon kodades utanför Adobe Experience Manager Dynamic Media är inte data för målgruppsinnehållande (bortfall) och uppspelningsprocent tillgängliga i tabellen.

>[!NOTE]
Spårnings- och rapportdata baseras uteslutande på Dynamic Media egen videospelare och tillhörande videospelarförinställning. Därför kan du inte spåra och rapportera om videofilmer som spelas upp med andra videospelare.

Första gången du anger Videorapporter visas som standard videodata från och med den första i den aktuella månaden och till och med den aktuella månadens datum. Du kan dock åsidosätta standarddatumintervallet genom att ange ett eget datumintervall. Nästa gång du anger Videorapporter används det datumintervall du har angett.

För att videorapporter ska fungera på rätt sätt skapas ett Report Suite-ID automatiskt när Dynamic Media-Cloud Services konfigureras. Samtidigt skickas Report Suite-ID:t till publiceringsservern så att det är tillgängligt för funktionen Kopiera URL när du förhandsgranskar resurser. Den här funktionen kräver dock att publiceringsservern redan har konfigurerats. Om publiceringsservern inte är konfigurerad kan du fortfarande publicera för att se videorapporten. Du måste dock gå tillbaka till Dynamic Media Cloud Configuration och trycka på **[!UICONTROL OK]**.

Så här visar du videorapporter:

1. I det övre vänstra hörnet av Experience Manager trycker du på logotypen för Experience Manager och sedan på **[!UICONTROL Tools]** (hammarikon) > **[!UICONTROL Assets]** > **[!UICONTROL Video Reports]** till vänster.
1. Gör något av följande på sidan Videorapporter:

   * I närheten av det övre högra hörnet trycker du på ikonen **[!UICONTROL Refresh Video Report]**.
Använd bara Uppdatera om rapportens slutdatum är den aktuella dagen. Med den här funktionen ser du till att du ser videospårningen som har utförts sedan du senast körde rapporten.

   * I närheten av det övre högra hörnet trycker du på ikonen **[!UICONTROL Date Picker]**.
Ange start- och slutdatumintervallet som du vill ha videodata för och tryck sedan på **[!UICONTROL Run Report]**.

   I grupprutan Top Metrics (Toppvärden) identifieras olika aggregerade mått för alla *publicerade *videor på webbplatsen.

1. I tabellen som visar de publicerade videoklippen trycker du på ett videonamn för att spela upp videon och ser även videons återgivningsrapport.

<!-- OBSOLETE CONTENT OBSOLETE CONTENT - SDK ONLY AVAILABLE INTERNALLY NOW 
### Viewing video reports based on a video viewer that you created using the Dynamic Media HTML5 Viewer SDK {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

If you are using an out-of-box video viewer provided by Dynamic Media, or if you created a custom viewer preset based off of an out-of-box video viewer, then no additional steps are required to view video reports. However, if you have created your own video viewer based off the Dynamic Media HTML5 Viewer SDK, then use the following steps to ensure the your video viewer is sending tracking events to Dynamic Media Video Reports.

Use the Dynamic Media Viewers Reference and the Dynamic Media HTML5 Viewers SDK to create your own video viewers.

See [Dynamic Media Viewers Reference Guide](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html?lang=en).

Download the Scene7 HTML Viewer SDK from Adobe Developer Connection.

See [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html).

**To view Video Reports based on a video viewer that you created using the Dynamic Media HTML5 Viewer SDK:**

1. Navigate to any published video asset.
1. Near the upper-left corner of the asset's page, from the drop-down list, select **[!UICONTROL Viewers]**.
1. Select any video viewer preset and copy the embed code.
1. In the embed code, find the line with the following:

   `videoViewer.setParam("config2", "<value>");`

   The `config2` parameter enables tracking in HTML5 Viewers. It is also a company-specific preset that contains the configuration information for Video Reporting, and for customer-specific Adobe Analytics configurations.

   The correct value for the config2 parameter is found in both the **[!UICONTROL Embed Code]** and in the copy **[!UICONTROL URL]** function. In the URL from the copy **[!UICONTROL URL]** command, the parameter to look for is `&config2=<value>` . The value is almost always `companypreset`, but in some instances it can also be `companypreset-1`, `companypreset-2`, and so forth.

1. In your custom video viewer code, add AppMeasurementBridge .jsp to the viewer page by doing the following:

    * First, determine if you need the `&preset` parameter.
      If the `config2` parameter is `companypreset`, you do *not *need `&preset=parameter`.
      If `config2` is anything else, set the preset parameter the same as the `config2` parameter. For example, if `config2=companypreset-2`, add `&param2=companypreset-2` to the AppMeasurmentBridge.jsp URL.

    * Then, add the AppMeasurementBridge.jsp script:
      `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. Create the TrackingManager component by doing the following:

    * After calling `s7sdk.Utils.init();` create a TrackingManager instance to track events by adding the following:
      `var trackingManager = new s7sdk.TrackingManager();`

    * Connect components to TrackingManager by doing the following:
      In the `s7sdk.Event.SDK_READY` event handler, attach the component you want to track to the TrackingManager.
      For example, if the component is `videoPlayer`, add
      `trackingManager.attach(videoPlayer);`
      to attach the component to the trackingManager. To track multiple viewers on a page, use multiple tracking mangaer components.

    * Create the AppMeasurementBridge object by adding the following:

      ```
      var appMeasurementBridge = new AppMeasurementBridge(); appMeasurementBridge.setVideoPlayer(videoPlayer);
      ```

    * Add the tracking function by adding the following:

      ```
      trackingManager.setCallback(appMeasurementBridge.track,
       appMeasurementBridge);
      ```

   The appMeasurementBridge object has a built-in track function. OBSOLETE However, you can provide your own to support multiple tracking systems or other functionality.

   For more information, see *Using the TrackingManager Component* in the *Scene7 HTML5 Viewer SDK User Guide* available for download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html).
 -->

## Lägga till bildtexter i videon {#adding-captions-to-video}

Du kan utöka räckvidden för dina videor till globala marknader genom att lägga till bildtexter till enskilda videor eller till adaptiva videouppsättningar. Genom att lägga till bildtext undviker du behovet av att duplicera ljudet, eller behovet av att använda inbyggda högtalare för att spela in ljudet igen för varje språk. Videon spelas upp på det språk den spelades in på. Undertexter på främmande språk visas så att personer på olika språk fortfarande kan förstå ljuddelen.

Bildtext ger också bättre tillgänglighet genom att använda undertexter för personer som är döva eller hörselskadade.

>[!NOTE]
Den videospelare som du använder måste ha stöd för visning av bildtexter.

Dynamic Media kan konvertera bildtextfiler till JSON-format (JavaScript™ Object Notation). Den här konverteringen innebär att du kan bädda in JSON-texten på en webbsida som en dold men fullständig utskrift av videon. Sökmotorerna kan sedan crawla och indexera innehållet så att videoklippen blir lättare att hitta och ge kunderna mer information om videoinnehållet.

Mer information om hur du använder JSON-funktionen i en URL finns i [Servera statiskt (icke-bildinnehåll)](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents.html#image-serving-api).

**Så här lägger du till bildtexter eller undertexter till video:**

1. Använd ett program eller en tjänst från tredje part för att skapa en undertextningsfil för video.

   Kontrollera att filen du skapar följer standarden WebVTT (Web Video Text Tracks). Bildtextens filnamnstillägg är .VTT. Du kan läsa mer om bildtextstandarden WebVTT.

   Se [WebVTT: Textspårningsformatet för webbvideo](https://dev.w3.org/html5/webvtt/).

   Det finns både kostnadsfria och premiumverktyg och tjänster som du kan använda för att skapa bildtexter/undertexter utanför Dynamic Media. Om du till exempel vill skapa en enkel videobeskrivningsfil utan formatering kan du använda följande kostnadsfria redigerings- och redigeringsverktyg för bildtexter online:

   [WebVTT Caption Maker](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   Du får bäst resultat om du använder verktyget i Internet Explorer 9 eller senare, Google Chrome eller Safari.

   Klistra in den kopierade URL-adressen för videofilen i fältet **[!UICONTROL Enter URL of video file]** i verktyget och klicka sedan på **[!UICONTROL Load]**. Se [Hämta en URL för en resurs](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) för att hämta URL-adressen till själva videofilen som du sedan kan klistra in i **[!UICONTROL Enter URL of video file field]**. Internet Explorer, Chrome och Safari kan sedan spela upp videon direkt.

   Följ nu instruktionerna på skärmen för att skapa och spara WebVTT-filen. När du är klar kopierar du bildtextfilens innehåll och klistrar in det i en vanlig textredigerare och sparar det med filnamnstillägget .VTT.

   >[!NOTE]
   För globalt stöd för videoundertexter på flera språk kräver WebVTT-standarden att du skapar separata VTT-filer och anropar varje språk som du vill ha stöd för.

   Vanligtvis vill du ge bildtexten VTT ett namn som är detsamma som videofilen och bifoga den med språkinställningen -EN, -FR eller -DE. Genom att göra det kan det hjälpa dig att automatisera genereringen av video-URL:er med ditt befintliga system för hantering av webbinnehåll.

1. I Experience Manager överför du WebVTT-bildtextfilen till DAM.
1. Navigera till den *publicerade* videoresurs som du vill associera med bildtextfilen som du överförde.

   Kom ihåg att URL:er endast går att kopiera *efter* att du har *publicerat* resurserna.

   Se [Publicera resurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

1. Gör något av följande:

   * Tryck på **[!UICONTROL URL]** om du vill visa ett videoklipp. I dialogrutan URL-adress markerar och kopierar du URL-adressen till Urklipp och sedan förbi URL-adressen till en enkel textredigerare. Lägg till den kopierade URL:en för videon med följande syntax:

      `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

      Observera `,1` i slutet av bildtextsökvägen. Omedelbart efter filnamnstillägget .VTT i sökvägen kan du aktivera (aktivera) eller inaktivera (inaktivera) den stängda bildtextsknappen i videospelarfältet genom att ange `,1` eller `,0`.

   * Tryck på **[!UICONTROL Embed Code]** om du vill få en inbäddad videoredigeringsfunktion. I dialogrutan Bädda in kod markerar och kopierar du den inbäddade koden till Urklipp och klistrar sedan in koden i en enkel textredigerare. Lägg till den kopierade inbäddningskoden med följande syntax:

      `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

      Observera `,1` i slutet av bildtextsökvägen. Omedelbart efter filnamnstillägget .VTT i sökvägen kan du aktivera (aktivera) eller inaktivera (inaktivera) den stängda bildtextsknappen i videospelarfältet genom att ange `,1` eller `,0`.

## Lägga till kapitelmarkörer i video {#adding-chapter-markers-to-video}

Du kan göra det enklare att titta på och navigera i videoklipp med långa formulär genom att lägga till kapitelmarkörer i enstaka videor eller i adaptiva videouppsättningar. När en användare spelar upp videon kan han/hon klicka på kapitelmarkörerna på tidslinjen (kallas även videobandspelare). De kan enkelt navigera till sin intressepunkt eller direkt gå till nytt innehåll, demonstrationer och självstudiekurser.

>[!NOTE]
Den videospelare som används måste ha stöd för kapitelmarkörer. Dynamic Media videospelare har stöd för kapitelmarkörer, men det är inte säkert att tredjepartsvideospelare används.

<!-- OBSOLETE CONTENT OBSOLETE CONTENT If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading “Customizing Behavior Using Modifiers” under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

Du skapar en kapitellista för videon på ungefär samma sätt som du skapar bildtexter. Det innebär att du skapar en WebVTT-fil. Observera dock att den här filen måste vara separat från alla WebVTT-beskrivningsfiler. Du kan inte kombinera bildtexter och kapitel i en WebVTT-fil.

Du kan använda följande exempel som exempel på det format du använder för att skapa en WebVTT-fil med kapitelnavigering:

### WebVTT-fil med videokapitelnavigering {#webvtt-file-with-video-chapter-navigation}

```xml
WEBVTT
Chapter 1
00:00.000 --> 01:04.364
The bicycle store behind it all.
Chapter 2
01:04.364 --> 02:00.944
Creative Cloud.
Chapter 3
02:00.944 --> 03:02.937
Ease of management for a working solution.
Chapter 4
03:02.937 --> 03:35.000
Cost-efficient access to rapidly evolving technology.
```

I exemplet ovan är `Chapter 1` referensidentifieraren och valfri. Referenstiden på `00:00:000 --> 01:04:364` anger kapitlets start- och sluttid i `00:00:000`-format. De sista tre siffrorna är millisekunder och kan lämnas som `000` om det behövs. Kapiteltiteln för `The bicycle store behind it all` är den faktiska beskrivningen av kapitlets innehåll. Referensidentifieraren, startreferenstiden och kapiteltiteln visas alla i ett popup-fönster i videospelaren när en användare håller muspekaren över en visuell referenspunkt i tidslinjen.

Eftersom du använder ett HTML5-videovisningsprogram bör du kontrollera att den kapitelfil du skapar följer standarden WebVTT (Web Video Text Tracks). Kapitelfilnamnstillägget är .VTT. Du kan läsa mer om bildtextstandarden WebVTT.

Se [WebVTT: Textspårningsformatet för webbvideo](https://dev.w3.org/html5/webvtt/)

**Så här lägger du till kapitelmarkörer i video:**

1. Spara .VTT-filen i UTF8-kodning för att undvika problem med teckenåtergivning i kapiteltiteltexten.

   Vanligtvis vill du ge kapitlet VTT-filen samma namn som videofilen och bifoga den med kapitel. Genom att göra det kan det hjälpa dig att automatisera genereringen av video-URL:er med ditt befintliga system för hantering av webbinnehåll.
1. Ladda upp din WebVTT-kapitelfil i Experience Manager.

   Se [Överför resurser](/help/assets/manage-digital-assets.md#uploading-assets).

1. Gör något av följande:

   <table>
     <tbody>
      <tr>
       <td>För en popup-video</td>
       <td>
       <ol>
       <li>Navigera till den <i>publicerade </i>videoresursen som du vill associera med den överförda kapitelfilen. Kom ihåg att URL:er endast går att kopiera <i>efter</i> att du har <i>publicerat</i> resurserna. Se <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">Publicera resurser.</a></li>
       <li>Klicka eller tryck på <strong>Visare</strong> i listrutan.</li>
       <li>Tryck eller klicka på förinställningsnamnet för videovisningsprogrammet i den vänstra listen. En förhandsgranskning av videon öppnas på en separat sida.</li>
       <li>Klicka på <strong>URL</strong> längst ned i den vänstra listen.</li>
       <li>I dialogrutan URL-adress markerar och kopierar du URL-adressen till Urklipp och sedan förbi URL-adressen till en enkel textredigerare.</li>
       <li>Lägg till den kopierade URL:en för videon med följande syntax för att associera den med den kopierade URL:en till din kapitelfil:<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>För en inbäddad videoupplevelse<br /> </td>
       <td>
       <ol>
       <li>Navigera till den <i>publicerade </i>videoresursen som du vill associera med den överförda kapitelfilen. Kom ihåg att URL:er endast går att kopiera <i>efter</i> att du har <i>publicerat</i> resurserna. Se <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">Publicera resurser.</a></li>
       <li>Klicka eller tryck på <strong>Visare</strong> i listrutan.</li>
       <li>Tryck eller klicka på förinställningsnamnet för videovisningsprogrammet i den vänstra listen. En förhandsgranskning av videon öppnas på en separat sida.</li>
       <li>Klicka på <strong>Bädda in</strong> längst ned i den vänstra listen.</li>
       <li>I dialogrutan Bädda in kod markerar och kopierar du hela koden till Urklipp och klistrar sedan in den i en enkel textredigerare.</li>
       <li>Lägg till videons inbäddningskod med följande syntax för att koppla den till den kopierade URL:en till din kapitelfil:<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt&gt;"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>

<!--

## About video thumbnails {#about-video-thumbnails}

A video thumbnail is a reduced-size version of a video frame or an image asset representing the video to the customer. The thumbnail should serve to encourage a customer to click on the video.

All videos in Experience Manager must have an associated thumbnail; you cannot delete a thumbnail without replacing it. By default, when you upload a video to Experience Manager, the first frame is used as the thumbnail. However, you can customize the thumbnail for branding purposes or visual search, for example. When you customize a video thumbnail, you can either play the video and pause on the frame you want to use, or you can select an image asset that you have already uploaded and *published* in your digital asset manager.

Note that a custom video thumbnail image that you select from a video is not extracted and saved in the DAM as a separate and distinct asset. However, a custom video thumbnail that you select from an existing image asset is saved to the JCR. The path of the selected asset gets stored under the video asset's node as in the following example path:

`/content/dam/*<folder_name*>/<*video_name*>/jcr:content/manualThumbnail`

The ability to customize a video thumbnail is only available after you have applied a video profile to the folder where the video is located.

### Adding a custom video thumbnail {#adding-a-custom-video-thumbnail}

1. Be sure you have already done the following:

    * Created a folder for your video assets.
    * [Applied a video profile to the folder](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

    * [Uploaded your videos to the folder](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).

1. Navigate to an uploaded video asset whose thumbnail image you want to change.
1. In asset selection mode either from **[!UICONTROL List View]** or **[!UICONTROL Card View]**, tap the video asset.
1. On the toolbar, tap the **[!UICONTROL Properties** icon (a circle with an "i" in it).
1. On the video's Properties page, tap **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, do one of the following:

    * To use a frame from the video as the new thumbnail:

        * On the toolbar, tap **[!UICONTROL Select Frame from video]**.
        * Tap the Play button, then tap the Pause button on the frame you want to capture as the video's new thumbnail.

    * To use an image asset as the new thumbnail:

        * On the toolbar, tap **[!UICONTROL Select Thumbnail from Assets]**.
        * Tap **[!UICONTROL Select Thumbnail]**.
        * Navigate to a previously uploaded and published image asset you want to use. Note that the asset will automatically be resized to serve as a thumbnail image for the video.
        * Select the image asset, then tap **[!UICONTROL Select]**.

1. On the Change Thumbnail page, tap **[!UICONTROL Save Change]**.
1. On the video's Properties page, in the upper-right corner, tap **[!UICONTROL Save & Close]**.

-->

<!--

## About video thumbnails in Dynamic Media Hybrid mode{#about-video-thumbnails-in-dynamic-media-hybrid-mode}

You can choose from one of ten thumbnail images automatically generated by Dynamic Media to add to your video. The video player displays your selected thumbnail when a video asset is used with the Dynamic Media component in the authoring environment of Experience Manager Sites, Experience Manager Mobile, or Experience Manager Screens. The thumbnail serves as a static picture that best represents the contents of your entire video and further encourages users to click the Play button.

Based on the total time of the video, Dynamic Media captures ten (default) thumbnail images at 1%, 11%, 21%, 31%, 41%, 51%, 61%, 71%, 81%, and 91% into the video. The ten thumbnails persist meaning that if you decide to choose a different thumbnail later on, you do not need to regenerate the series. You preview the ten thumbnail images and then select the one you want to use with your video. If you want to change to default you can use CRXDE Lite to configure the time interval that thumbnail images are generated. For example, if you only wanted to generate a series of four evenly spaced thumbnail images from your video, you can configure the interval time at 24%, 49%, 74%, and 99%.

Ideally, you can add a video thumbnail anytime after you upload your video but before you publish the video on your website.

If you prefer, you can choose to upload a custom thumbnail to represent your video instead of using a thumbnail generated by Dynamic Media. For example, you could create a custom thumbnail image that has the title of your video, an eye-catching opening image, or a very specific image captured from your video. The custom video thumbnail image that you upload should have a maximum resolution of 1280 x 720 pixels (minimum width of 640 pixels) and be no larger than 2MB.

See also [About video thumbnails](/help/assets/dynamic-media/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

-->

<!--

### Adding a video thumbnail {#adding-a-video-thumbnail}

1. Navigate to an uploaded video asset that you want to add a video thumbnail.
1. In asset selection mode either from the List View or the Card View, tap the video asset.
1. On the toolbar, tap the **[!UICONTROL View Properties]** icon (a circle with an "i" in it).
1. On the video's Properties page, tap **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, on the toolbar, tap **[!UICONTROL Select Frame]**.

   Dynamic Media generates a series thumbnail images from your video, based on the default time interval or time interval you customized.

1. Preview the generated thumbnail images, then select the one you want to add to your video.
1. Tap **[!UICONTROL Save Change]**.

   The video's thumbnail image is updated to use the thumbnail you selected. If you later decide to change the thumbnail image, you can return to the **[!UICONTROL Change Thumbnail]** page and select a new one.

   If you configured new default time intervals, or you uploaded a new video to replace the existing video, you will need to have Dynamic Media regenerate the thumbnails.

   See [Configuring the default time interval that video thumbnails are generated](#configuring-the-default-time-interval-that-video-thumbnails-are-generated).

-->

<!--

#### Configuring the default time interval that video thumbnails are generated {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

When you configure and save the new default time interval, your change automatically applies only to videos that you upload in the future. It does not automatically apply the new default to videos that you previously uploaded. For existing videos, you must regenerate the thumbnails.

See [Adding a video thumbnail](#adding-a-video-thumbnail).

**To configure the default time interval that video thumbnails are generated,**

1. In Experience Manager, tap **[!UICONTROL Tools]** &gt; **[!UICONTROL General]** &gt; **[!UICONTROL CRXDE Lite]**.

1. In the CRXDE Lite page, in the directory panel on the left, navigate t `o etc/dam/imageserver/configuration/jcr:content/settings.`

   if the directory panel is not visible, you may need to tap the &gt;&gt; icon to the left of the Home tab.

1. On the lower-right panel, in the Properties tab, double-tap `thumbnailtime`.
1. In the Edit thumbnailtime dialog box, use the text fields to enter interval values as percentages.

    * Tap the plus sign (+) icon to add one or more interval value fields. You may need to scroll to the bottom of the dialog box to see the icon.
    * Tap the minus sign (-) icon to the right of an interval value field to delete it from the list.
    * Tap the up arrow icon and the down arrow icon to reorder the interval values.

1. Tap **[!UICONTROL OK]** to return to the Properties tab.
1. Near the upper-left corner of the CRXDE Lite page, tap **[!UICONTROL Save All]**, then tap the Back Home icon in the upper-left corner to return to Experience Manager.

   See [Adding a video thumbnail](#adding-a-video-thumbnail).

-->

<!--

### Adding a custom video thumbnail {#adding-a-custom-video-thumbnail-1}

These steps apply only to Dynamic Media running in Hybrid mode.

T**o add a custom video thumbnail**,

1. Navigate to an uploaded video asset that you want to add a custom video thumbnail.
1. In asset selection mode either from the List View or the Card View, tap the video asset.
1. On the toolbar, tap the **[!UICONTROL View Properties]** icon (a circle with an "i" in it).
1. On the video's Properties page, tap **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, on the toolbar, tap **[!UICONTROL Upload New Thumbnail]**.
1. Navigate to a thumbnail image you want to use, select it, then tap **[!UICONTROL Open]** to begin uploading the image into Experience Manager. Following the upload, be sure you publish the image.
1. After you have successfully uploaded and published the image, in the Change Thumbnail page, tap **[!UICONTROL Save Changes]**.

   The custom thumbnail is added to your video.

-->
