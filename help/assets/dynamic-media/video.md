---
title: Video i Dynamic Media
description: Lär dig arbeta med video i Dynamic Media. Granska de bästa sätten att koda videofilmer, publicera videofilmer på YouTube, visa videorapporter och lägga till undertexter eller kapitelmarkörer i videofilmer.
contentOwner: Rick Brough
feature: Video Profiles
role: User
exl-id: 0d5fbb3e-b763-415f-8c69-ea36445f882b
source-git-commit: 00cd62aa64c183a0560326feaacda1db70627858
workflow-type: tm+mt
source-wordcount: '9316'
ht-degree: 1%

---

# Video {#video}

I det här avsnittet beskrivs hur du arbetar med video i Dynamic Media.

## Snabbstart: Videor {#quick-start-videos}

Följande steg-för-steg-beskrivning av arbetsflödet hjälper dig att komma igång snabbt med anpassningsbara videouppsättningar i Dynamic Media. Efter varje steg finns det korsreferenser till ämnesrubriker där du kan hitta mer information.

>[!NOTE]
>
>Innan du arbetar med video i Dynamic Media måste du kontrollera att Adobe Experience Manager-administratören redan har aktiverat och konfigurerat Dynamic Media-Cloud Service.
>
>* Se [Konfigurera Dynamic Media-Cloud Service](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) i Konfigurera Dynamic Media och [Felsöka Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md).
>

1. **Ladda upp dina Dynamic Media-filmer** genom att göra följande:

   * Skapa en egen videokodningsprofil. Du kan också helt enkelt använda den fördefinierade _Adaptiv videokodning_ profil som medföljer Dynamic Media.

      * [Skapa en videokodningsprofil](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * Läs mer om [Bästa tillvägagångssätt för videokodning](#best-practices-for-encoding-videos).

   * Koppla videobearbetningsprofilen till en eller flera mappar där du ska överföra dina primära källvideor.

      * [Använda en videoprofil på mappar](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).
      * Läs mer om [Ordna digitala resurser](/help/assets/organize-assets.md).

   * Överför dina primära källvideor till mapparna. När du lägger till videofilmer i mappen kodas de enligt den videobearbetningsprofil som du tilldelade mappen.

      * Dynamic Media har främst stöd för videoklipp i kort form med en maxlängd på 30 minuter och en minimiupplösning på mer än 25 x 25.
      * Du kan överföra videofiler som är upp till 15 GB vardera.
      * [Ladda upp videor](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).
      * Läs mer om [Indatafilformat som stöds](/help/assets/file-format-support.md).

   * Övervaka hur [videokodning pågår](#monitoring-video-encoding-and-youtube-publishing-progress) antingen från resursen eller arbetsflödesvyn.

1. **Hantera dina Dynamic Media-filmer** genom att göra något av följande:

   * Ordna, bläddra bland och söka efter videomaterial

      * [Ordna digitala resurser](/help/assets/organize-assets.md)
      * [Söka efter videoresurser](/help/assets/search-assets.md#custompredicates) eller [Söka efter resurser](/help/assets/manage-digital-assets.md#search-assets)

   * Förhandsgranska och publicera videomaterial

      * Visa källvideon och de kodade återgivningarna av videon tillsammans med tillhörande miniatyrer:
        [Förhandsgranska videoklipp](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) eller [Förhandsgranska resurser](/help/assets/dynamic-media/previewing-assets.md)
        [Hantera videoåtergivningar](/help/assets/manage-digital-assets.md#managing-renditions)

      * [Hantera förinställningar för visningsprogram](/help/assets/dynamic-media/managing-viewer-presets.md)
      * [Publicera resurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)

   * Arbeta med videometadata

      * Redigera egenskaperna för video, till exempel titel, beskrivning och taggar, anpassade metadatafält:
        [Redigera videoegenskaper](/help/assets/manage-digital-assets.md#editing-properties)

      * [Hantera metadata för digitala resurser](/help/assets/manage-metadata.md)
      * [Metadata-scheman](/help/assets/metadata-schemas.md)

   * Granska, godkänn och kommentera videoklipp och behåll fullständig versionskontroll

      * [Kommentera videoklipp](/help/assets/manage-video-assets.md#annotate-video-assets) eller [Anteckna resurser](/help/assets/manage-digital-assets.md#annotating)

      * [Skapa en version](/help/assets/manage-digital-assets.md#asset-versioning)
      * [Starta ett arbetsflöde för en resurs](/help/assets/manage-digital-assets.md#starting-a-workflow-on-an-asset)

      * [Granska mappresurser](/help/assets/bulk-approval.md)
      * [Projekt](/help/sites-cloud/authoring/projects/overview.md)

1. **Publicera dina Dynamic Media-filmer** genom att göra något av följande:

   * Om du använder Experience Manager som WCM-system (Web Content Management) kan du lägga till videofilmer direkt på dina webbsidor.

      * [Lägga till videoklipp på webbsidor](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

   * Om du använder ett webbinnehållshanteringssystem från en annan leverantör kan du länka eller bädda in videor på dina webbsidor.

      * Integrera video med URL:
        [Länka URL:er till ditt webbprogram](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md).

      * Integrera video med inbäddad kod på webbsidan:
        [Bädda in videovisningsprogrammet på en webbsida](/help/assets/dynamic-media/embed-code.md).

   * [Generera videorapporter](#viewing-video-reports).

   * [Lägga till bildtexter i video](#adding-captions-to-video).

## Arbeta med video i Dynamic Media {#working-with-video-in-dynamic-media}

Video i Dynamic Media är en totallösning som gör det enkelt att publicera högkvalitativ adaptiv video för direktuppspelning på flera skärmar, inklusive stationära datorer, surfplattor och mobila enheter. En adaptiv videouppsättning grupperar versioner av samma video som är kodade med olika bithastigheter och format som 400 kbit/s, 800 kbit/s och 1 000 kbit/s. Datorns eller mobilenhetens tillgängliga bandbredd identifieras.

På en mobilenhet från iOS identifieras t.ex. en bandbredd som 3G, 4G eller Wi-Fi. Sedan väljs automatiskt rätt kodad video bland de olika videobithastigheterna i den adaptiva videouppsättningen. Videon strömmas till datorer, mobila enheter eller surfplattor.

Dessutom ändras videokvaliteten dynamiskt automatiskt om nätverksförhållandena ändras på datorn eller den mobila enheten. Om en kund går över till helskärmsläge på en stationär dator svarar den adaptiva videouppsättningen med en bättre upplösning, vilket förbättrar kundens tittarupplevelse. Med adaptiva videouppsättningar får du bästa möjliga uppspelning för kunder som spelar upp Dynamic Media-video på flera skärmar och enheter.

Den logik som en videospelare använder för att avgöra vilken kodad video som ska spelas upp eller väljas under uppspelningen baseras på följande algoritm:

1. Videospelaren läser in det inledande videofragmentet baserat på den bithastighet som ligger närmast värdet som är inställt för&quot;inledande bithastighet&quot; i spelaren.
1. Videospelaren växlar baserat på ändringar av bandbreddshastigheten med följande kriterier:

   1. Spelaren väljer den högsta bandbreddsströmmen under eller lika med den beräknade bandbredden.
   1. Spelaren hanterar bara 80 % av den tillgängliga bandbredden. Men om den byter upp sig är det mer försiktigt med bara 70 % för att undvika överskattning och omedelbart gå tillbaka.

Detaljerad teknisk information om algoritmen finns i [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

Följande stöds för hantering av enstaka video och adaptiva videouppsättningar:

* Ladda upp video från ett antal videoformat och ljudformat som stöds och koda video till MP4 H.264-format för uppspelning på flera skärmar. Du kan använda fördefinierade adaptiva videoförinställningar, enskilda videokodningsförinställningar eller anpassa din egen kodning för att styra videons kvalitet och storlek.

   * När en adaptiv videouppsättning genereras innehåller den MP4-videor.
   * **Anteckning**: Primära videoklipp/källvideoklipp läggs inte till i en adaptiv videouppsättning.

* Videobildtext i alla HTML5-videovisningsprogram.
* Ordna, bläddra bland och sök videoklipp med fullt stöd för metadata för effektiv hantering av videomaterial.
* Leverera adaptiva videouppsättningar till webben, datorer, surfplattor och mobila enheter.

Adaptiv videoströmning stöds på olika iOS-plattformar. Se [Referenshandbok för Dynamic Media Viewer](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference.html).

<!-- OUTDATED 2/28/22 BASED ON CQDOC-18692 Dynamic Media supports mobile video playback for MP4 H.264 video. You can find BlackBerry&reg; devices that support this video format at the following: [Supported video formats on BlackBerry&reg;](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

OUTDATED 2/28/22 BASED ON CQDOC-18692 You can find Windows&reg; devices that support this video format at the following [Supported video formats on Windows&reg; Phone](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs). -->

* Spela upp videon med Dynamic Media Video Viewer Presets, inklusive följande:

   * Enstaka videovisningsprogram.
   * Visningsprogram för blandade media som kombinerar både video- och bildinnehåll.

* Konfigurera videospelare för att tillgodose era varumärkesbehov.
* Integrera video på webbplatsen, mobilsajten eller mobilapplikationen med en enkel URL eller inbäddningskod.

Se [Dynamisk videouppspelning](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&amp;config=GeoRetail/Universal_Video1&amp;stageSize=640,480) exempel.

Se även [Tittare för Experience Manager Assets och Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) och [Endast visningsprogram för Experience Manager Assets](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only) i [Referenshandbok för Dynamic Media Viewer](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).

## Bästa praxis: Använda videovisningsprogrammet för HTML5 {#best-practice-using-the-html-video-viewer}

Förinställningarna för videovisningsprogrammet i Dynamic Media HTML 5 är robusta videospelare. Du kan använda dem för att undvika många vanliga problem som är kopplade till HTML5-videouppspelning och problem som är kopplade till mobila enheter. Exempel: brist på strömmande bithastighet och begränsad webbläsarräckvidd.

På designsidan av spelaren kan du utforma videospelarens funktioner med standardverktyg för webbutveckling. Du kan till exempel utforma knapparna, kontrollerna och den anpassade bakgrunden för förhandsvisningsbilder med HTML5 och CSS så att du kan nå dina kunder med ett anpassat utseende.

På visningsprogrammets uppspelningssida identifieras webbläsarens videokapacitet automatiskt. Sedan visas videon med HLS eller DASH, som också kallas adaptiv videoströmning. Om leveransmetoderna inte finns används HTML5 progressiv i stället.

>[!NOTE]
>
>Om du vill använda DASH för dina videor måste det först aktiveras av Adobe tekniska support på ditt konto. Se [Aktivera DASH på ditt konto](#enable-dash).

Du kan kombinera möjligheten att utforma uppspelningskomponenterna med HTML 5 och CSS till en enda spelare. Den kan ha inbäddad uppspelning och använda adaptiv och progressiv strömning beroende på webbläsarens kapacitet. Alla dessa funktioner innebär att du kan utöka räckvidden för ditt multimedieinnehåll till både dator- och mobilanvändare och få en smidig videoupplevelse.

Se även [Endast visningsprogram för Experience Manager Assets](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only) i [Referenshandbok för Dynamic Media Viewer](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).


### Uppspelning av video på stationära datorer och mobila enheter med videovisningsprogrammet HTML5 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

För strömning av anpassningsbara video för datorer och mobilenheter baseras de videor som används för växling av bithastighet på alla MP4-videor i den adaptiva videouppsättningen.

Videouppspelning sker med HLS eller DASH, eller progressiv videouppspelning. I tidigare versioner av Experience Manager, som 6.0, 6.1 och 6.2, strömmades videofilmer via HTTP.

I Experience Manager 6.3 och senare direktuppspelas videor nu via HTTPS (dvs. HLS eller DASH) eftersom DM-gatewaytjänstens URL alltid använder HTTPS. Det här standardbeteendet påverkar inte kunderna. Det innebär att direktuppspelning av video alltid sker via HTTPS, såvida det inte stöds av webbläsaren. Se följande tabell.

Därför bör

* Om du har en HTTPS-webbplats med HTTPS-videoströmning går det bra att strömma.
* Om du har en HTTP-webbplats med HTTPS-videoströmning går det bra att strömma och det finns inga blandade innehållsproblem i webbläsaren.

DASH är den internationella standarden och HLS är en Apple-standard. Båda används för adaptiv videoströmning. Och båda teknikerna justerar automatiskt uppspelningen baserat på bandbreddskapaciteten i nätverket. Man kan också &quot;söka&quot; till valfri punkt i videon utan att behöva vänta på att resten av videon ska laddas ned.

Progressiv video levereras genom att videon hämtas och lagras lokalt på en användares dator eller mobila enhet.

I följande tabell beskrivs enheten, webbläsaren och uppspelningsmetoden för videoklipp på stationära datorer och mobila enheter med [Dynamic Media HTML5 Video Viewer](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video.html#interactive-video).

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
   <td>Progressiv hämtning.</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Internet Explorer 11+</td>
   <td>I Windows® 8 och Windows® 10 - Tvinga användning av HTTPS när DASH eller HLS begärs. Känd begränsning: HTTP på DASH eller HLS fungerar inte i den här kombinationen av webbläsare och operativsystem<br /> <br /> I Windows® 7 - progressiv nedladdning. Använder standardlogik för att välja HTTP- eller HTTPS-protokoll.</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Firefox 23-44</td>
   <td>Progressiv hämtning.</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Firefox 45 eller senare</td>
   <td>HLS- eller DASH*-strömning med adaptiv bithastighet</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Krom</td>
   <td>HLS- eller DASH*-strömning med adaptiv bithastighet</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Safari (Mac)</td>
   <td>HLS adaptiv bithastighetsströmning</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Chrome (Android™ 6 eller tidigare)</td>
   <td>Progressiv hämtning.</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Chrome (Android™ 7 eller senare)</td>
   <td>HLS- eller DASH* adaptive bitrate streaming/td&gt;
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Android™ (standardwebbläsare)</td>
   <td>Progressiv hämtning.</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Safari (iOS)</td>
   <td>HLS adaptiv bithastighetsströmning</td>
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Chrome (iOS)</td>
   <td>HLS adaptiv bithastighetsströmning</td>
  </tr>
 </tbody>
</table>

>[!IMPORTANT]
>
>*Om du vill använda DASH för dina videor måste det först aktiveras av Adobe tekniska support på ditt konto. Se [Aktivera DASH på ditt konto](#enable-dash).)

<!--  THIS LINE WAS REMOVED FROM THE TABLE ABOVE ON FEB 28, 2022 BASED ON CQDOC 18692 -RSB <tr>
   <td>Mobile</td>
   <td>BlackBerry&reg;</td>
   <td>HLS or DASH</td>
  </tr>
 -->

## Arkitektur för Dynamic Media videolösning {#architecture-of-dynamic-media-video-solution}

Följande bild visar det övergripande arbetsflödet för redigering av videoklipp som har överförts och kodats med hjälp av DMGGateway (i Dynamic Media Hybrid-läge) och som har gjorts tillgängliga för offentlig användning.

![chlimage_1-427](assets/chlimage_1-427.png)

## Hybrid publiceringsarkitektur för videor {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## Bästa tillvägagångssätt för att koda videofilmer {#best-practices-for-encoding-videos}

The **Dynamic Media Encode Video** arbetsflödet kodar video om du har aktiverat Dynamic Media och konfigurerat videoCloud Service. Det här arbetsflödet innehåller information om arbetsflödets processhistorik och fel. Om du har aktiverat Dynamic Media och konfigurerat Cloud Service för video, **[!UICONTROL Dynamic Media Encode Video]** arbetsflödet aktiveras automatiskt när du överför en video. (Om du inte använder Dynamic Media **[!UICONTROL DAM Update Asset]** arbetsflödet börjar gälla.)

Nedan följer några tips om hur du kodar källvideofiler.

<!-- For advice about video encoding, see the following:

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en).
* [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en). -->

### Källvideofiler {#source-video-files}

När du kodar en videofil ska du använda en källvideofil med högsta möjliga kvalitet. Undvik att använda tidigare kodade videofiler eftersom dessa filer redan är komprimerade, och ytterligare kodning skapar en video med delkvalitet.

* Dynamic Media har främst stöd för videoklipp i kort form med en maxlängd på 30 minuter och en minimiupplösning på mer än 25 x 25.
* Du kan överföra primära källvideofiler som är upp till 15 GB vardera.

I följande tabell beskrivs rekommenderad storlek, proportioner och lägsta bithastighet som källvideofilerna måste ha innan du kodar dem:

| Storlek | Proportioner | Minsta bithastighet |
|--- |--- |--- |
| 1024 x 768 | 4:3 | 4 500 kbit/s för de flesta videofilmer. |
| 1280 x 720 | 16:9 | 3 000 - 6 000 kbit/s, beroende på mängden rörelse i videon. |
| 1920 x 1080 | 16:9 | 6000 - 8 000 kbit/s, beroende på mängden rörelse i videon. |

### Hämta metadata för en fil {#obtaining-a-file-s-metadata}

Du kan hämta metadata för en fil genom att visa dess metadata med ett redigeringsverktyg för videoklipp eller med ett program som utformats för att hämta metadata. Nedan följer instruktioner om hur du använder MediaInfo, ett tredjepartsprogram, för att hämta videofilens metadata:

1. Gå till [MediaInfo-hämtning](https://mediaarea.net/en/MediaInfo/Download).
1. Välj och hämta installationsprogrammet för den grafiska användargränssnittsversionen och följ installationsanvisningarna.
1. Efter installationen högerklickar du på videofilen (endast Windows®) och väljer MediaInfo, eller så öppnar du MediaInfo och drar videofilen till programmet. Alla metadata som är associerade med videofilen, inklusive bredd, höjd och fps, visas.

### Proportioner {#aspect-ratio}

När du väljer eller skapar en förinställning för videokodning för den primära källvideofilen måste du se till att förinställningen har samma proportioner som den primära källvideofilen. Proportionerna är proportionerna mellan videons bredd och höjd.

Om du vill ta reda på videofilens proportioner hämtar du filens metadata och noterar filens bredd och höjd (se Hämta filens metadata ovan). Använd sedan den här formeln för att bestämma proportionerna:

width/height = aspect ratio

I följande tabell beskrivs hur formelresultaten översätts till vanliga alternativ för proportioner:

| Formelresultat | Proportioner |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

En video som till exempel är 1440 bredd x 1080 höjd har proportionerna 1440/1080 eller 1,33. I det här fallet väljer du en förinställning för videokodning med 4:3-proportioner för att koda videofilen.

### Bithastighet {#bitrate}

Bithastighet är den mängd data som kodas för att skapa en enda sekund av videouppspelningen. Bithastigheten mäts i kilobit per sekund (kbit/s).

>[!NOTE]
>
>Eftersom förlustgivande komprimering används för alla kodekar är bithastigheten den viktigaste faktorn i videokvaliteten. Ju mer du komprimerar en videofil desto sämre blir kvaliteten. Därför är alla andra egenskaper lika (upplösning, bildrutehastighet och kodek), ju lägre bithastighet, desto lägre kvalitet får den komprimerade filen.

När du väljer en bithastighetskodning kan du välja mellan två typer:

* **[!UICONTROL Constant Bitrate Encoding]** (CBR) - Under CBR-kodning är bithastigheten eller antalet bitar per sekund densamma under hela kodningsprocessen. CBR-kodning bevarar den angivna datahastigheten enligt inställningen för hela videon. CBR-kodning optimerar inte heller mediefiler för kvalitet utan sparar på lagringsutrymmet.
Använd CBR om videon innehåller en liknande rörelsenivå i hela videon. CBR används oftast för direktuppspelat videoinnehåll. Se även [Använda egna parametrar för videokodning](/help/assets/dynamic-media/video-profiles.md#using-custom-added-video-encoding-parameters).

* **[!UICONTROL Variable Bitrate Encoding]** (VBR) - VBR-kodning justerar datahastigheten nedåt och till den övre gräns som du anger, baserat på de data som krävs av kompressorn. Den här funktionen innebär att under en VBR-kodningsprocess ökar eller minskar bithastigheten för mediefilen dynamiskt beroende på mediafilens behov av bithastighet.
Det tar längre tid att koda VBR men ger det bästa resultatet. Kvaliteten på mediefilen är bättre. VBR används oftast för http-progressiv leverans av videoinnehåll.

När använder du VBR jämfört med CRB?
När du väljer VBR jämfört med CBR rekommenderar vi nästan alltid att du använder VBR för dina mediefiler. VBR ger filer av högre kvalitet med konkurrenskraftiga bithastigheter. När du använder VBR måste du vara säker på att du använder kodning i två omgångar och ställa in den maximala bithastigheten till 1,5 gånger målvideobithastigheten.

När du väljer en förinställning för videokodning måste du ta hänsyn till målanvändarens anslutningshastighet. Välj en förinställning med en datahastighet som är 80 % av den hastigheten. Om målanvändarens anslutningshastighet till exempel är 1000 kbit/s är den bästa förinställningen en med en videodatahastighet på 800 kbit/s.

I den här tabellen beskrivs datahastigheten för typiska anslutningshastigheter.

| Hastighet (kbit/s) | Anslutningstyp |
|--- |--- |
| 256 | Uppringd anslutning. |
| 800 | Vanlig mobilanslutning. För den här anslutningen anger du en datahastighet mellan 400 och maximalt 800 för 3G-upplevelser som mål. |
| 2000 | Vanlig anslutning till stationär bredbandsuppkoppling. För den här anslutningen anger du en datahastighet i intervallet 800-2000 kbit/s med de flesta mål som är i genomsnitt 1200-1500 kbit/s. |
| 5000 | Vanlig bredbandsanslutning. Kodning i det här övre intervallet rekommenderas inte eftersom videoleverans i den här hastigheten inte är tillgänglig för de flesta konsumenter. |

### Upplösning {#resolution}

**Upplösning** beskriver en videofils höjd och bredd i pixlar. Den mesta källvideon lagras med hög upplösning (till exempel 1 920 x 1 080). Vid direktuppspelning komprimeras källvideo till en lägre upplösning (640 x 480 eller lägre).

Upplösning och datahastighet är två sammankopplade faktorer som avgör videokvaliteten. Om du vill behålla samma videokvalitet måste datahastigheten vara högre ju fler pixlar en videofil har (ju högre upplösning). Ta till exempel antalet pixlar per bildruta i en 320 x 240-upplösning och en 640 x 480-upplösningsvideofil:

| Upplösning | Pixlar per bildruta |
|--- |--- |
| 320 x 240 | 76,800 |
| 640 x 480 | 307,200 |

Filen på 640 x 480 har fyra gånger fler pixlar per bildruta. För att uppnå samma datahastighet för dessa två exempelupplösningar tillämpar du fyra gånger komprimeringen på 640 x 480-filen, vilket kan minska videons kvalitet. En videodatahastighet på 250 kbit/s ger därför en högkvalitativ bild med upplösningen 320 x 240, men inte med upplösningen 640 x 480.

I allmänhet gäller att ju högre datahastighet du använder, desto bättre visas videon och ju högre upplösning du använder, desto högre datahastighet måste du behålla visningskvaliteten (jämfört med lägre upplösningar).

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

I USA och Japan spelas de flesta videoklipp in med 29,97 bildrutor per sekund (fps). I Europa spelas de flesta videoklipp in med 25 fps. Film filmas med 24 fps.

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
| Kodad | 640 x 360 | 3 | 3 |
| Kodad | 480 x 270 | 4 | 4 |

### Kodat videofilformat {#encoded-video-file-format}

Dynamic Media rekommenderar att du använder MP4 H.264-videokodningsförinställningar. Eftersom MP4-filer använder H.264-videokodeken ger den video med hög kvalitet men i en komprimerad filstorlek.

## Visa videorapporter {#viewing-video-reports}

>[!NOTE]
>
>Videorapporter är bara tillgängliga när du kör Dynamic Media - hybrid-läge.

Videorapporter visar flera aggregerade mått över en viss period så att du kan övervaka att *publicerad* individuella och aggregerade videor fungerar som förväntat. Följande viktigaste mätdata samlas in för alla publicerade videor på hela webbplatsen:

* Video börjar
* Slutförandefrekvens
* Genomsnittlig tid för video
* Total tid för video
* Videor per besök

En tabell med alla *publicerad* videofilmer visas också i en lista så att du kan spåra de mest visade videofilmerna på webbplatsen baserat på hur många videostarter som har gjorts.

När du väljer ett videonamn i listan visas videons rapport om målgruppsinnehållande (bortfall) i form av ett linjediagram. Diagrammet visar antalet vyer för en given tidpunkt under videouppspelning. När du spelar upp videon synkroniseras det lodräta strecket med tidsindikatorn i spelaren. Släppningar i linjediagramdata indikerar var publiken slutar intressera sig.

Om videon kodades utanför Adobe Experience Manager Dynamic Media är inte data för målgruppsinnehållande (bortfall) och uppspelningsprocent tillgängliga i tabellen.

>[!NOTE]
>
>Spårnings- och rapportdata baseras uteslutande på Dynamic Media egen videospelare och tillhörande videospelarförinställning. Därför kan du inte spåra och rapportera om videofilmer som spelas upp med andra videospelare.

Första gången du anger Videorapporter visas som standard videodata från och med den första i den aktuella månaden och till och med den aktuella månadens datum. Du kan dock åsidosätta standarddatumintervallet genom att ange ett eget datumintervall. Nästa gång du anger Videorapporter används det datumintervall du har angett.

För att videorapporter ska fungera korrekt skapas ett Report Suite-ID automatiskt när Dynamic Media-Cloud Service konfigureras. Samtidigt skickas Report Suite-ID:t till publiceringsservern så att det är tillgängligt för funktionen Kopiera URL när du förhandsgranskar resurser. Den här funktionen kräver dock att publiceringsservern redan har konfigurerats. Om publiceringsservern inte är konfigurerad kan du fortfarande publicera för att se videorapporten. Du måste dock gå tillbaka till Dynamic Media Cloud-konfigurationen och välja **[!UICONTROL OK]**.

**Så här visar du videorapporter:**

1. I det övre vänstra hörnet av Experience Manager väljer du logotypen Experience Manager och navigerar sedan till **[!UICONTROL Tools]** (hammarikon) > **[!UICONTROL Assets]** > **[!UICONTROL Video Reports]**.
1. Gör något av följande på sidan Videorapporter:

   * I närheten av det övre högra hörnet väljer du **[!UICONTROL Refresh Video Report]** -ikon.
Använd bara Uppdatera om rapportens slutdatum är den aktuella dagen. Med den här funktionen ser du till att du ser videospårningen som har utförts sedan du senast körde rapporten.

   * I närheten av det övre högra hörnet väljer du **[!UICONTROL Date Picker]** -ikon.
Ange start- och slutdatumintervallet som du vill ha videodata för och välj sedan **[!UICONTROL Run Report]**.

   Grupprutan Övre mått identifierar olika aggregerade mått för alla *publicerad* videor på hela webbplatsen.

1. I tabellen som listar de publicerade videoklippen väljer du ett videonamn för att spela upp videon och ser även videons återgivningsrapport.

<!-- OBSOLETE CONTENT OBSOLETE CONTENT - SDK ONLY AVAILABLE INTERNALLY NOW 
### Viewing video reports based on a video viewer that you created using the Dynamic Media HTML5 Viewer SDK {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

If you are using an out-of-box video viewer provided by Dynamic Media, or if you created a custom viewer preset based off of an out-of-box video viewer, then no additional steps are required to view video reports. However, if you have created your own video viewer based off the Dynamic Media HTML5 Viewer SDK, then use the following steps to ensure the your video viewer is sending tracking events to Dynamic Media Video Reports.

Use the Dynamic Media Viewers Reference and the Dynamic Media HTML5 Viewers SDK to create your own video viewers.

See [Dynamic Media Viewers Reference Guide](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html).

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





### Aktivera stöd för DASH, multi-subtitle och multi-audio-spår på ditt Dynamic Media-konto {#enable-dash}

**Aktivera DASH-stöd för ditt konto**
DASH (Digital Adaptive Streaming over HTTP) är den internationella standarden för direktuppspelad video och används i stor utsträckning av olika videovisningsprogram. När DASH är aktiverat för ditt konto kan du välja mellan DASH eller HLS för adaptiv videoströmning. Eller så kan du välja båda med automatisk växling mellan spelare när **[!UICONTROL auto]** är valt som uppspelningstyp i visningsförinställningen.

Några viktiga fördelar med att aktivera DASH på ditt konto är följande:

* Paketera DASH-strömvideo för strömning med adaptiv bithastighet. Den här metoden leder till ökad effektivitet vid leverans. Adaptiv strömning ger bästa möjliga tittarupplevelse för dina kunder.
* Webbläsaroptimerad direktuppspelning med Dynamic Media-spelare växlar mellan HLS- och DASH-strömning för att säkerställa bästa möjliga servicekvalitet. Videospelaren växlar automatiskt till HLS när en Safari-webbläsare används.
* Du kan konfigurera den direktuppspelningsmetod (HLS eller DASH) som du föredrar genom att redigera förinställningen för visningsprogrammet för video.
* Optimerad videokodning säkerställer att ingen ytterligare lagring används samtidigt som DASH-funktionen aktiveras. En enda uppsättning videokodningar skapas för både HLS och DASH för att optimera lagringskostnaderna för video.
* Gör videomaterialet mer tillgängligt för kunderna.
* Hämta strömnings-URL:en via API:er också.

Du aktiverar DASH-support för ditt konto via ett Adobe-kundsupportärende som du skapar och skickar in.

**Aktivera stöd för flera undertexter och flerljudspår på ditt konto**

Samtidigt som du skapar ett Adobe Support-ärende där DASH är aktiverat på ditt konto kan du också dra nytta av att ha stöd för multi-subtitle och multi-audio track automatiskt aktiverat. När du har aktiverat bearbetas alla efterföljande videor som du överför med en ny serverdelsarkitektur som har stöd för att lägga till spår med flera undertexter och flera ljud i videoklipp.

>[!IMPORTANT]
>
>Alla videofilmer som du har överfört *före* stöd för flera undertexter och flerljudspår på ditt Dynamic Media-konto, [måste bearbetas på nytt](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). Det här steget för videoombearbetning är nödvändigt för att de ska kunna använda spår med flera undertexter och flera ljud. Video-URL:erna fortsätter att fungera och spelas upp som vanligt efter ombearbetningen.

**Så här aktiverar du stöd för DASH, multi-subtitle och multi-audio-spår på ditt Dynamic Media-konto:**

1. [Använd Admin Console för att börja skapa ett nytt supportärende](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).
1. Om du vill skapa ett supportärende följer du instruktionerna och ser till att du anger följande information:

   * Primärt kontaktnamn, e-postadress, telefon.
   * Ditt program-ID och ditt miljö-ID.
   * Namn på ditt Dynamic Media-konto.
   * Ange att stöd för DASH, multi-subtitle och multi-audio-spår ska aktiveras på ditt Dynamic Media-konto på Experience Manager 6.5.

1. Adobe kundsupport lägger till dig i kundens väntelista baserat på i vilken ordning förfrågningarna skickas.
1. När Adobe är redo att hantera din begäran kontaktar kundsupporten dig för att koordinera och ange ett måldatum för aktiveringen.
1. Du meddelas när du är klar av kundsupporten.
1. Nu kan du göra något av följande:

   * Skapa [videovisningsförinställning](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset) som vanligt.
   * [Lägga till flera undertexter och flerljudspår](#add-msma) till videon.


## Stöd för flerrubriks- och flerljudspår för videofilmer i Dynamic Media{#about-msma}

Med funktioner för multi-subtitle och multi-audio track i Dynamic Media kan du enkelt lägga till flera undertexter och ljudspår i en primär video. Detta innebär att videoklippen är tillgängliga för alla mottagare världen över. Du kan anpassa en enda publicerad primär video till en global publik på flera språk och följa riktlinjer för tillgänglighet för olika geografiska regioner. Författare kan också hantera undertexter och ljudspår från en enda flik i användargränssnittet.

![Undertexter och ljudspår i Dynamic Media tillsammans med en tabell som visar överförda VTT-undertextfiler och överförda MP3-ljudspårfiler för en video.](/help/assets/dynamic-media/assets/msma-subtitle-audiotracks-tab.png)

Några av användningsområdena för att lägga till multiundertexter och flerljudspår i den primära videon är bland annat följande:

| Typ | Använd skiftläge |
|--- |--- |
| **Undertexter** | Stöd för flera språk |
|  | Beskrivande text för tillgänglighet |
| **Ljudspår** | Stöd för flera språk |
|  | Kommentarspår |
|  | Beskrivande ljud |

Alla [videoformat som stöds i Dynamic Media](/help/assets/file-format-support.md) och alla videovisningsprogram från Dynamic Media - förutom Dynamic Media *Video_360* visningsprogram - kan användas med multiundertexter och flerljudspår.

Funktioner för flera undertexter och flerljudspår är tillgängliga för ditt Dynamic Media-konto via en funktion som måste aktiveras (aktiveras) av Adobe kundsupport.

### Lägga till flera undertexter och flera ljudspår i videon {#add-msma}

Innan du lägger till spår med flera undertexter och flera ljud i videon måste du kontrollera att du redan har följande på plats:

* Dynamic Media är konfigurerat i en AEM miljö.
* A [Dynamic Media videoprofil används på den mapp där videoklippen har importerats](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).
* [Spår för flera undertexter och flera ljud är aktiverat på ditt Dynamic Media-konto](#enable-dash).

Undertexter och bildtexter som lagts till stöds i formaten WebVTT och Adobe VTT. Dessutom stöds tillagda ljudspårsfiler med MP3-format.

>[!IMPORTANT]
>
>Alla videofilmer som du har överfört *före* stöd för flera undertexter och flerljudspår på ditt Dynamic Media-konto, [måste bearbetas på nytt](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). Det här steget för videoombearbetning är nödvändigt för att de ska kunna använda spår med flera undertexter och flera ljud. Video-URL:erna fortsätter att fungera och spelas upp som vanligt efter ombearbetningen.

**Så här lägger du till multiundertexter och flerljudspår i videon:**

1. [Överför din primära video till en mapp](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) som redan har tilldelats en videoprofil.
1. Navigera till den överförda videoresursen som du vill lägga till spår med flera undertexter och flera ljud.
1. Välj videoresurs i resursurvalsläget, antingen från listvyn eller kortvyn.
1. I verktygsfältet väljer du ikonen Egenskaper (en cirkel med &quot;i&quot;).
   ![Markerad videoresurs med bockmarkering över videominiatyrbild och Visa egenskaper markerade i verktygsfältet.](/help/assets/dynamic-media/assets/msma-selectedasset-propertiesbutton.png)*Markerad videoresurs i kortvyn.*
1. På videons egenskapssida väljer du **[!UICONTROL Subtitles & Audio Tracks]** -fliken.

   >[!TIP]
   >Om du inte ser **[!UICONTROL Subtitles & Audio Tracks]** betyder det något av två:
   >
   >* Mappen där den valda videon finns har ingen tilldelad videoprofil. I så fall, se [Använda en videoprofil på mappen](/help/assets/dynamic-media/video-profiles.md#applying-video-profiles-to-specific-folders)
   >* Eller så måste videon bearbetas på nytt av Dynamic Media. I så fall, se [Bearbeta Dynamic Media-resurser igen i en mapp](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).
   >
   >När du har slutfört någon av ovanstående åtgärder går du tillbaka till dessa steg.

   ![Undertexter och ljudspår på egenskapssidan.](/help/assets/dynamic-media/assets/msma-audiotracks.png)*Underrubriker och fliken Ljudspår på videons egenskapssida.*

1. (Valfritt) Gör så här om du vill lägga till en eller flera undertextningsfiler i en video:
   * Välj **[!UICONTROL Upload Subtitles]**.
   * Navigera till och markera en eller flera VTT-filer (Video Text Tracks) och öppna dem.
   * För att underrubriker ska vara synliga i mediespelaren *måste* lägg till nödvändig information (metadata) om *var* undertextfil som du överförde. Välj pennikonen till höger om namnet på en undertextfil. I **Redigera underrubrik** anger du följande obligatoriska information om filen och väljer **[!UICONTROL Save]**. Upprepa den här processen för varje undertitelfil som du överförde:

     | Underrubriksmetadata | Beskrivning |
     |--- |--- |
     | Filnamn | Standardfilnamnet härleds från det ursprungliga filnamnet. Filnamnet kan bara ändras under överföring och kan inte ändras senare. Teckenkraven för filnamn är desamma som för AEM Assets.<br>Samma filnamn kan inte användas för ytterligare undertextningsfiler och ljudspårsfiler. |
     | Språk | Välj språk för underrubriken. |
     | Typ | Välj den typ av underrubrik som du använder.<br>**Underrubrik** - Undertexten som visas med videon som översätter eller transkriberar dialogrutan.<br>**Bildtext** - Bildtexten innehåller även bakgrundsljud, talardifferentiering och annan relevant information, tillsammans med översättningen eller transkriberingen av dialogen, som gör innehållet mer tillgängligt för personer som är döva eller hörselskadade. |
     | Etikett | Den text som visas för undertextens namn i **[!UICONTROL Select audio or caption]** popup-lista i mediespelaren. Etiketten är det som kunden ser och som motsvarar ett underrubrik- eller bildtextspår. Till exempel, `English (CC)`. |

     Om det behövs kan du ändra eller redigera metadata för underrubriken senare. När videon publiceras återspeglas dessa uppgifter på offentliga URL:er i publicerade videor.

1. (Valfritt) Gör följande om du vill lägga till ett eller flera ljudspår i en video:
   * Välj **[!UICONTROL Upload Audio Tracks]**.
   * Navigera till och markera en eller flera .mp3-filer och öppna dem.
   * För att ljudspår ska vara synliga i **[!UICONTROL Select audio or caption]** popup-lista på mediespelaren, *måste* lägg till nödvändig information om *var* ljudspårsfil som du har lagt till. Välj pennikonen till höger om namnet på en ljudspårsfil. I **Redigera ljudspår** anger du följande obligatoriska uppgifter och väljer **[!UICONTROL Save]**. Upprepa den här processen för varje ljudspårsfil som du överförde.

     | Metadata för ljudspår | Beskrivning |
     |--- |--- |
     | Filnamn | Standardfilnamnet härleds från det ursprungliga filnamnet. Filnamnet kan bara ändras under överföring och kan inte ändras senare. Teckenkraven för filnamn är desamma som för AEM Assets.<br>Samma filnamn kan inte användas för ytterligare ljudspårfiler eller undertextfiler. |
     | Språk | Välj språk för ljudspåret. |
     | Typ | Välj vilken typ av ljudspår du använder.<br>**Original** - Ljudspåret som ursprungligen var kopplat till videon och representeras som `[Original]` i etiketten med `English` som är valt som standard. while **[!UICONTROL Label]** och **[!UICONTROL Language]** kan ändras i **[!UICONTROL Edit Audio Track]** används de ursprungliga värdena om den primära videon bearbetas om.<br>**Standard** - Ett tilläggsljudspår för ett annat språk än originalspråket.<br>**Ljudbeskrivning** - Ett ljudspår som även innehåller en beskrivande berättarröst för icke-verbala händelser och gester i videon, vilket gör innehållet mer tillgängligt för personer med nedsatt syn. |
     | Etikett | Texten som visas som ljudspårets namn i **[!UICONTROL Select audio or caption]** popup-lista i mediespelaren. Etiketten är det kunden ser och motsvarar ett ljudspår. Till exempel, `English [Original]`. Etiketten för ljud som är kopplat till en video är inställd på `[Original|` som standard. |

     Om det behövs kan du ändra eller redigera metadata för ljudspåret senare. När videon publiceras återspeglas dessa uppgifter på offentliga URL:er i publicerade videor.

1. I det övre högra hörnet på sidan, från **[!UICONTROL Save & Close]** nedrullningsbar lista, välja **[!UICONTROL Save]**. Filerna överförs och metadatabearbetningen börjar, vilket visas i **Status** -kolumn i gränssnittet.

   >[!NOTE]
   >
   >Beroende på inställningarna för cachning för instansen kan metadatabearbetningen ta flera minuter innan den visas i förhandsgranskningen och i publicerade URL:er.

1. (Valfritt) Om du har valt **[!UICONTROL Save & Close]** i föregående steg, i stället för att markera **[!UICONTROL Save]** kan du fortfarande visa de överförda filernas bearbetningsstatus. Se [Visa livscykelstatus för överförda undertitel- och ljudspårfiler](#lifecycle-status-video).
1. (Valfritt) Förhandsgranska videon före publicering för att kontrollera att undertexterna och ljudet fungerar som förväntat. Se [Förhandsgranska en video med flera undertexter och ljudspår](#preview-video-audio-subtitle)
1. Publicera videon. Se [Publicera resurser](publishing-dynamicmedia-assets.md).

#### Lägga till undertitel- och ljudspårfiler i en video som redan är publicerad

När du överför ytterligare undertextningsfiler eller ljudspårsfiler till en video som redan är publicerad innebär det att dessa filer har en `Processed` status efter att de har förberetts, efter överföring. Då kan du förhandsgranska videon i Dynamic Media för att se eller höra de nyligen överförda filerna.

Efter förhandsgranskning måste du dock *publicera* videon igen för att de nya undertitel- eller ljudspårsfilerna också ska publiceras. Efter publiceringen blir undertexterna eller ljudet tillgängliga med den offentliga Dynamic Media-URL:en.

>[!NOTE]
>
>Baserat på cachelagringsinställningarna för din instans kan metadatauppdateringar ta flera minuter innan de visas i förhandsgranskningen och i publicerade URL:er.

Om du har konfigurerat Dynamic Media för omedelbar publicering kommer överföringen av ytterligare undertitel- eller ljudfiler omedelbart att starta en publicering av videon efter överföringen av undertitel- eller ljudfiler.

>[!CAUTION]
>
>När du överför undertextningsfiler eller ljudfiler till en video som antingen är publicerad eller opublicerad tas filerna bort om du [*ombearbeta*](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets) videon. Endast videons ursprungliga ljud förblir intakt. I så fall måste du ladda upp undertextningsfilerna och ljudspårsfilerna till videon igen.

#### Lägga till flera bildtexter i en video som har en befintlig URL med bildtextmodifierare

Dynamic Media har stöd för att lägga till en enda bildtext med video via en URL-modifierare. Se [Lägga till bildtexter i video](#adding-captions-to-video).

Ändringar av flera bildtexter har företräde framför en bildtext som har lagts till med en URL-modifierare för publicerade videor.

**Så här lägger du till flera bildtexter i en video som har en befintlig URL med bildtextmodifierare:**

1. Överför bildtextfilen som redan har lagts till som modifierare till videon, så att du kan hantera filen explicit.
1. Överför eventuella ytterligare undertitel-/bildtextfiler.
1. Publicera videon som vanligt.
Den befintliga URL:en med bildtextmodifieraren kan nu läsa in flera bildtexter.

### Visa livscykelstatus för överförda undertitel- och ljudspårfiler{#lifecycle-status-video}

Du kan följa livscykelstatusen för alla undertexter eller ljudspårsfiler som överförts till den primära videon från **Undertexter och ljudspår** flik för **Egenskaper**.

**Så här visar du livscykelstatusen för en video:**

1. Navigera till den videoresurs vars livscykelstatus du vill visa.
1. Välj videoresurs i resursurvalsläget, antingen från listvyn eller kortvyn.
1. I verktygsfältet väljer du ikonen Egenskaper (en cirkel med &quot;i&quot;).
1. På sidan Egenskaper väljer du **[!UICONTROL Subtitles & Audio Tracks]** -fliken. Observera status för varje underrubrik eller ljudfil i kolumnen Status.

| Status för underrubrik eller ljudspår | Beskrivning |
| --- | --- |
| Bearbetar | När en ny undertitel- eller ljudspårsfil läggs till och sparas, försätts den i tillståndet&quot;Bearbetar&quot;. Dynamic Media bearbetar filen genom att bifoga det direktuppspelade manifestet till den primära videon. |
| Behandlad | När bearbetningen är klar visas undertextnings- eller ljudspårsfilen, eller det ursprungliga ljudspåret som är associerat med den primära videon, i läget Behandlad. Du kan förhandsgranska undertitel- och ljudspårsfiler som visas som &quot;Behandlad&quot; *före* publicerar du videon live. |
| Publicerad | Ett publicerat läge representerar ett läge som liknar publicerat för en primär video. Resurser publiceras när den primära videon publiceras och är tillgängliga på den offentliga Dynamic Media-URL:en. |
| Misslyckades | Ett &quot;Misslyckat&quot;-läge innebär att bearbetningen av en undertitel- eller ljudspårsfil inte slutfördes. Ta bort undertitel- eller ljudspårsfilen och överför igen. |
| Opublicerad | När en publicerad primär video avpubliceras explicit avpubliceras även eventuella undertitel- eller ljudspårsfiler som du har lagt till i videon. |

![Statuskolumnen är markerad för fälten Undertexter och Ljudspår.](/help/assets/dynamic-media/assets/msma-lifecycle-status.png)*Livscykelstatus för varje överförd undertitel- och ljudspårfil.*

### Ange standardljud för en video som har flera ljudspår

Som standard anges videons ursprungliga ljud som standardljud som ska spelas upp.

Alla överförda ljudspårsfiler kan dock anges som standardljud som spelas upp när en video har lästs in i visningsprogrammet. I användargränssnittet för Egenskaper, under **Undertexter och ljudspår** -fliken, `Default` -etiketten används till höger om ljudspårsfilen för videouppspelning.

>[!NOTE]
>
>Uppspelningen av standardljud kan också bero på vad som är inställt i följande webbläsare:
>
>* Chrome - Det standardljud som ställs in i videon spelas upp.
* Safari - Om standardspråket är inställt i Safari spelas ljudet upp med det angivna standardspråket, om tillgängligt med videons manifest. I annat fall spelas det standardljud som är inställt som en del av en videos egenskaper upp.

**Så här anger du standardljud för en video som har flera ljudspår:**

1. Navigera till den videoresurs vars standardljudspår du vill ställa in.
1. Välj videoresurs i resursurvalsläget, antingen från listvyn eller kortvyn.
1. I verktygsfältet väljer du ikonen Egenskaper (en cirkel med &quot;i&quot;).
1. På sidan Egenskaper väljer du **[!UICONTROL Subtitles & Audio Tracks]** -fliken.
1. Under **Ljudspår** väljer du ljudspårsfilen som du vill ange som videostandardfil.
1. Välj **[!UICONTROL Set as default]**.
I **Ange som standard** väljer **[!UICONTROL Replace]**.

   ![Rubriken Ljudspår med ett valt namn på ljudspårsfilen och markerad&quot;Ange som standard&quot;-knapp.](/help/assets/dynamic-media/assets/msma-defaultaudiotrack.png)*Ställa in standardljudspåret för en video.*

1. I det övre högra hörnet väljer du **[!UICONTROL Save & Close]**.
1. Publicera videon. Se [Publicera resurser](publishing-dynamicmedia-assets.md).

### Förhandsgranska en video med flera undertexter och ljudspår{#preview-video-audio-subtitle}

När du har överfört undertextningsfiler och ljudspårsfiler till en video och bearbetat dem kan du använda Dynamic Media videovisningsprogram för att förhandsgranska alla olika spår. Om du gör det blir det lättare att se hur videon ser ut och låter som den är för kunderna, och du kan vara säker på att den beter sig som förväntat.

När du är nöjd med videon kan du [publicera](publishing-dynamicmedia-assets.md) med någon av följande metoder.

Se [Bädda in video- eller bildvisningsprogrammet på en webbsida](/help/assets/dynamic-media/embed-code.md).
Se [Länka URL:er till ditt webbprogram](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Den URL-baserade länkningsmetoden är inte möjlig om det interaktiva innehållet har länkar till relativa URL-adresser, särskilt länkar till Experience Manager Sites-sidor.
Se [Lägga till Dynamic Media Assets på sidor](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

>[!NOTE]
>
På standardfliken för förhandsgranskning i Experience Manager visas inte flera undertext- och ljudspår. Orsaken är att dessa spår är kopplade till Dynamic Media och bara kan visas med förhandsvisningen i Dynamic Media Viewer.

**Så här förhandsgranskar du en video som har flera undertexter och ljudspår:**

1. I **[!UICONTROL Assets]** navigera till en befintlig video som du har lagt till flera undertexter och ljudspår.
1. Klicka på videoresursen så att du kan öppna den i förhandsgranskningsläge.
1. Markera listrutan på förhandsvisningssidan, i det övre vänstra hörnet på sidan, och välj sedan **[!UICONTROL Viewers]**.

   ![Listruta med alternativet Visare.](/help/assets/dynamic-media/assets/msma-selectviewers.png)

1. Välj ett visningsprogram som du vill använda för videoförhandsvisningen i listan Visare. I följande skärmbild visas **[!UICONTROL Video]** visningsprogrammet väljs.

   ![Välj Video Viewer i listrutan Viewer.](/help/assets/dynamic-media/assets/msma-dmviewerselected.png)

1. I närheten av det nedre högra hörnet, till vänster om volymikonen, väljer du ikonen för pratbubblan och sedan det ljud eller den underrubrik som du vill höra eller se eller båda. Om du vill kan du under Underrubriker välja **[!UICONTROL Off]** om du inte vill visa några undertexter eller bildtexter.

   ![Popup-listan Ljud och underrubriker i Video Viewer.](/help/assets/dynamic-media/assets/msma-selectaudiosubtitle.png)*Simulering av en användare som väljer ljud och undertext för videouppspelning.*

1. För att börja spela upp väljer du videons **[!UICONTROL Play]** -knappen.
Anteckna **[!UICONTROL URL]** och **[!UICONTROL Embed]** i det nedre vänstra hörnet. Använd de här knapparna för att [länka videons URL till ditt webbprogram](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) eller till [bädda in videon på en webbsida](/help/assets/dynamic-media/embed-code.md), respektive
1. I det övre högra hörnet av förhandsvisningssidan väljer du **[!UICONTROL Close]**.

### Ta bort undertitel- eller ljudspårsfiler från en video

Du kan ta bort undertitel- eller ljudspårsfiler från en video. Borttagning av publicerade undertitel- eller ljudspårsfiler återspeglas automatiskt i videons publicerade URL.

Det går inte att ta bort det ursprungliga ljudspåret som har extraherats från en primär video.

**Så här tar du bort undertitel- eller ljudspårfiler från en video:**

1. Navigera till den videoresurs vars standardljudspår du vill ställa in.
1. Välj videoresurs i resursurvalsläget, antingen från listvyn eller kortvyn.
1. I verktygsfältet väljer du ikonen Egenskaper (en cirkel med &quot;i&quot;).
1. På sidan Egenskaper väljer du **[!UICONTROL Subtitles & Audio Tracks]** -fliken.
1. Gör något av följande:

   * Undertexter - under **Undertexter** rubrik, markera en eller flera underrubriksfiler som du vill ta bort från videon och välj sedan **[!UICONTROL Delete]**.
   * Ljudspår - under **Ljudspår** rubrik, markera en eller flera ljudspårsfiler som du vill ta bort från videon och välj sedan **[!UICONTROL Delete]**.

1. I dialogrutan Ta bort väljer du **[!UICONTROL OK]**.
1. Publicera videon.

### Hämta undertitel- eller ljudspårsfiler som överförts till en video

Du kan hämta en eller flera undertitel- eller ljudspårsfiler som du har överfört för användning med en video. Du kan antingen hämta alla markerade filer som en ZIP-fil eller skapa en separat hämtningsmapp för varje fil.

Det går inte att hämta det ursprungliga ljudspåret som har extraherats från en primär fil.

**Så här hämtar du undertitel- eller ljudspårfiler från en video:**

1. Navigera till den videoresurs vars standardljudspår du vill ställa in.
1. Välj videoresurs i resursurvalsläget, antingen från listvyn eller kortvyn.
1. I verktygsfältet väljer du ikonen Egenskaper (en cirkel med &quot;i&quot;).
1. På sidan Egenskaper väljer du **[!UICONTROL Subtitles & Audio Tracks]** -fliken.
1. Gör något av följande:

   * Undertexter - under **Undertexter** rubrik, välj en eller flera undertextningsfiler som du vill hämta från videon och välj sedan **[!UICONTROL Download]**.
   * Ljudspår - under **Ljudspår** välj en eller flera ljudspårsfiler som du vill hämta från videon och välj sedan **[!UICONTROL Download]**.

1. Ange följande alternativ i dialogrutan Hämta:

   | Alternativ | Beskrivning |
   |--- |--- |
   | Spara som | Använd standardfilnamnet som anges i textfältet Spara som eller ange ett eget namn. |
   | Skapa en separat mapp för varje resurs | Skapa en mapp för varje undertextfil eller ljudspårsfil som du valde för hämtning. |
   | E-post | Använd ditt standardprogram för e-post för att skicka ZIP-filen till en angiven e-postadress. |
   | Assets | Anger antalet filer som du hämtar och den sammanlagda storleken för alla markerade filer. Om du avmarkerar det här alternativet tonas (inaktiveras) **[!UICONTROL Download]** så att du inte kan hämta filer. |
1. Välj **[!UICONTROL Download]**.
1. Publicera videon. Se [Publicera resurser](publishing-dynamicmedia-assets.md).






## Lägga till undertexter till video {#adding-captions-to-video}

>[!IMPORTANT]
>
Adobe rekommenderar att du [möjliggör funktioner för flera undertexter och flerljudspår](#enable-dash) på ditt Dynamic Media-konto. På så sätt kan du dra nytta av den senaste Dynamic Media backend-arkitekturen och ett förenklat arbetsflöde för att lägga till bildtexter, undertexter och ljudspår i videoklipp.

Du kan utöka räckvidden för dina videor till globala marknader genom att lägga till undertexter till enskilda videor eller till adaptiva videouppsättningar. Genom att lägga till undertextning slipper du att duplicera ljudet eller att du behöver använda inbyggda högtalare för att spela in ljudet igen för varje språk. Videon spelas upp på det språk den spelades in på. Undertexter på främmande språk visas så att personer på olika språk fortfarande kan förstå ljuddelen.

Undertexter ger också bättre tillgänglighet för personer som är döva eller hörselskadade.

>[!NOTE]
>
Den videospelare som du använder måste ha stöd för visning av undertexter.

Se även [Tillgänglighet i Dynamic Media](/help/assets/dynamic-media/accessibility-dm.md).

Dynamic Media kan konvertera bildtextfiler till JSON-format (JavaScript Object Notation). Den här konverteringen innebär att du kan bädda in JSON-texten på en webbsida som en dold men fullständig utskrift av videon. Sökmotorer kan sedan crawla/indexera innehållet för att göra videoklippen lättare att hitta och ge kunderna mer information om videoinnehållet.

Se [Hantera statiskt innehåll (inte bildinnehåll)](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents.html#image-serving-api) om du vill ha mer information om hur du använder JSON-funktionen i en URL.

**Så här lägger du till bildtexter eller undertexter till video:**

1. Använd ett program eller en tjänst från tredje part för att skapa en undertextningsfil för video.

   Kontrollera att filen du skapar följer standarden WebVTT (Web Video Text Tracks). Bildtextens filnamnstillägg är .VTT. Du kan läsa mer om bildtextstandarden WebVTT.

   Se [WebVTT: Textspår för webbvideo](https://w3c.github.io/webvtt/).

   Det finns både kostnadsfria och premiumverktyg och tjänster som du kan använda för att skapa bildtexter/undertexter utanför Dynamic Media. Om du till exempel vill skapa en enkel videobildtextfil utan formatering kan du använda följande kostnadsfria redigerings- och redigeringsverktyg för bildtexter online:

   [WebVTT Caption Maker](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   Du får bäst resultat om du använder verktyget i Internet Explorer 9 eller senare, Google Chrome eller Safari.

   I verktyget, i **[!UICONTROL Enter URL of video file]** -fält, klistra in den kopierade URL-adressen för videofilen och markera sedan **[!UICONTROL Load]**. Se [Hämta en URL för en resurs](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) för att hämta URL:en till själva videofilen som du sedan kan klistra in i **[!UICONTROL Enter URL of video file field]**. Internet Explorer, Chrome och Safari kan sedan spela upp videon direkt.

   Följ nu instruktionerna på skärmen för att skapa och spara WebVTT-filen. När du är klar kopierar du bildtextfilens innehåll och klistrar in det i en vanlig textredigerare och sparar det med filnamnstillägget VTT.

   >[!NOTE]
   >
   För globalt stöd för videoundertexter på flera språk kräver WebVTT-standarden att du skapar separata .vtt-filer och anropar varje språk som du vill ha stöd för.

   Vanligtvis vill du ge bildtexten VTT ett namn som är detsamma som videofilen och bifoga den med språkinställningen -EN, -FR eller -DE. Genom att göra det kan det hjälpa dig att automatisera genereringen av video-URL:er med ditt befintliga system för hantering av webbinnehåll.

1. I Experience Manager överför du WebVTT-bildtextfilen till DAM.
1. Navigera till *publicerad* videoresurs som du vill associera med bildtextfilen som du överförde.

   Kom ihåg att URL:er endast går att kopiera *efter* att du har *publicerat* resurserna.

   Se [Publicera resurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

1. Gör något av följande:

   * Om du vill visa en popup-video väljer du **[!UICONTROL URL]**. I dialogrutan URL-adress markerar och kopierar du URL-adressen till Urklipp och sedan förbi URL-adressen till en enkel textredigerare. Lägg till den kopierade URL:en för videon med följande syntax:

     `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

     Anteckna `,1` i slutet av bildtextbanan. Omedelbart efter filnamnstillägget VTT i sökvägen kan du aktivera (aktivera) eller inaktivera (inaktivera) knappen för undertexter i videospelarfältet genom att ställa in på `,1` eller `,0`, respektive

   * Om du vill visa en inbäddad video väljer du **[!UICONTROL Embed Code]**. I dialogrutan Bädda in kod markerar och kopierar du den inbäddade koden till Urklipp och klistrar sedan in koden i en enkel textredigerare. Lägg till den kopierade inbäddningskoden med följande syntax:

     `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

     Anteckna `,1` i slutet av bildtextbanan. Omedelbart efter filnamnstillägget VTT i sökvägen kan du aktivera (aktivera) eller inaktivera (inaktivera) knappen för undertexter i videospelarfältet genom att ställa in på `,1` eller `,0`, respektive

## Lägga till kapitelmarkörer i video {#adding-chapter-markers-to-video}

Du kan göra det enklare att titta på och navigera i videoklipp med långa formulär genom att lägga till kapitelmarkörer i enstaka videor eller i adaptiva videouppsättningar. När en användare spelar upp videon kan han/hon välja kapitelmarkörer på tidslinjen (kallas även videobandspelare). De kan enkelt navigera till sin intressepunkt eller direkt gå över till nytt innehåll, ny utbildning och nya demonstrationer.

>[!NOTE]
>
Den videospelare som används måste ha stöd för kapitelmarkörer. Dynamic Media videospelare har stöd för kapitelmarkörer, men det är inte säkert att tredjepartsvideospelare används.

<!-- OBSOLETE CONTENT OBSOLETE CONTENT If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading "Customizing Behavior Using Modifiers" under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

Du skapar en kapitellista för videon på ungefär samma sätt som du skapar bildtexter. Det innebär att du skapar en WebVTT-fil. Observera dock att den här filen måste vara separat från alla WebVTT-beskrivningsfiler. Du kan inte kombinera bildtexter och kapitel i en WebVTT-fil.

Du kan använda följande exempel som exempel på det format du använder för att skapa en WebVTT-fil med kapitelnavigering:

### WebVTT-fil med videokapitelnavigering {#webvtt-file-with-video-chapter-navigation}

```xml {.line-numbers}
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

I exemplet ovan `Chapter 1` är referensidentifieraren och är valfri. Referenstiden för `00:00:000 --> 01:04:364` anger kapitlets starttid och sluttid, i `00:00:000` format. De tre sista siffrorna är millisekunder och kan lämnas som `000`, om så önskas. Kapiteltiteln för `The bicycle store behind it all` är den faktiska beskrivningen av kapitlets innehåll. Referensidentifieraren, startreferenstiden och kapiteltiteln visas alla i ett popup-fönster i videospelaren när en användare håller muspekaren över en visuell referenspunkt i tidslinjen.

Eftersom du använder ett HTML5-videovisningsprogram bör du kontrollera att den kapitelfil du skapar följer standarden WebVTT (Web Video Text Tracks). Kapitelfilnamnstillägget är .VTT. Du kan läsa mer om bildtextstandarden WebVTT.

Se [WebVTT: Textspår för webbvideo](https://w3c.github.io/webvtt/).

**Så här lägger du till kapitelmarkörer i video:**

1. Spara VTT-filen i UTF8-kodning så att du slipper problem med teckenåtergivning i kapiteltiteltexten.

   Vanligtvis vill du ge den kapitelbaserade VTT-filen samma namn som videofilen och bifoga den med kapitel. Genom att göra det kan det hjälpa dig att automatisera genereringen av video-URL:er med ditt befintliga system för hantering av webbinnehåll.
1. Ladda upp din WebVTT-kapitelfil i Experience Manager.

   Se [Överför resurser](/help/assets/manage-digital-assets.md#uploading-assets).

1. Gör något av följande:

   <table>
     <tbody>
      <tr>
       <td>För en popup-video</td>
       <td>
       <ol>
       <li>Navigera till <i>publicerad </i>videoresurs som du vill associera med den kapitelfil som du har överfört. Kom ihåg att URL:er endast går att kopiera <i>efter</i> att du har <i>publicerat</i> resurserna. Se <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">Publicera resurser.</a></li>
       <li>Välj <strong>Tittare</strong>.</li>
       <li>Markera namnet på visningsförinställningen för videon i den vänstra listen. En förhandsgranskning av videon öppnas på en separat sida.</li>
       <li>I den vänstra listen längst ned väljer du <strong>URL</strong>.</li>
       <li>I dialogrutan URL-adress markerar och kopierar du URL-adressen till Urklipp och sedan förbi URL-adressen till en enkel textredigerare.</li>
       <li>Lägg till den kopierade URL:en för videon med följande syntax så att du kan koppla den till den kopierade URL:en till din kapitelfil:<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>För en inbäddad videoupplevelse<br /> </td>
       <td>
       <ol>
       <li>Navigera till <i>publicerad </i>videoresurs som du vill associera med den kapitelfil som du har överfört. Kom ihåg att URL:er endast går att kopiera <i>efter</i> att du har <i>publicerat</i> resurserna. Se <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">Publicera resurser.</a></li>
       <li>Välj <strong>Tittare</strong>.</li>
       <li>Markera namnet på visningsförinställningen för videon i den vänstra listen. En förhandsgranskning av videon öppnas på en separat sida.</li>
       <li>I den vänstra listen längst ned väljer du <strong>Bädda in</strong>.</li>
       <li>I dialogrutan Bädda in kod markerar och kopierar du hela koden till Urklipp och klistrar sedan in den i en enkel textredigerare.</li>
       <li>Lägg till videofilens inbäddningskod med följande syntax så att du kan koppla den till den kopierade URL:en till din kapitelfil:<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt>"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>



## Om videominiatyrer {#about-video-thumbnails}

En videominiatyr är en version med reducerad storlek av en videobildruta eller en bildresurs som representerar videon för kunden. Miniatyrbilden bör uppmuntra kunden att välja videon.

Alla videofilmer i Experience Manager måste ha en associerad miniatyrbild. Du kan inte ta bort en miniatyrbild utan att ersätta den. Som standard används den första bildrutan som miniatyrbild när du överför en video till Experience Manager. Du kan dock anpassa miniatyrbilden för exempelvis varumärke eller visuell sökning. När du anpassar en videominiatyr kan du antingen spela upp videon och pausa den bildruta som du vill använda. Du kan också välja en bildresurs som du redan har överfört och *publicerad* i er Digital Asset Manager.

När miniatyrbilden ändras för en video hoppas miniatyrbildsgenerering över med hjälp av Asset compute-tjänsten när videon bearbetas om.

Möjligheten att anpassa en videominiatyr är endast tillgänglig efter att du har tillämpat en videoprofil på den mapp där videon finns.

### Lägga till en anpassad videominiatyr {#adding-a-custom-video-thumbnail}

1. Kontrollera att du redan har gjort följande:

   * Skapade en mapp för dina videoresurser.
   * [En videoprofil har använts på mappen](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

   * [Dina videoklipp har överförts till mappen](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).

1. Navigera till en överförd videoresurs vars miniatyrbild du vill ändra.
1. I resursurvalsläget antingen från **[!UICONTROL List View]** eller **[!UICONTROL Card View]** väljer du videoresursen.
1. Välj **[!UICONTROL Properties]** (en cirkel med&quot;i&quot;).
1. På videons egenskapssida väljer du **[!UICONTROL Change Thumbnail]**.
1. Gör något av följande på sidan Ändra miniatyrbild:

   * Så här använder du en bildruta från videon som ny miniatyrbild:

      * I verktygsfältet väljer du **[!UICONTROL Select Frame from video]**.
      * Välj uppspelningsknappen och sedan pausknappen för bildrutan som du vill spela in som videons nya miniatyrbild.

   * Så här använder du en bildresurs som ny miniatyrbild:

      * I verktygsfältet väljer du **[!UICONTROL Select Thumbnail from Assets]**.
      * Välj **[!UICONTROL Select Thumbnail]**.
      * Navigera till en tidigare överförd och publicerad bildresurs som du vill använda. Storleken på resursen ändras automatiskt så att den fungerar som en miniatyrbild för videon.
      * Markera bildresursen och välj sedan **[!UICONTROL Select]**.

1. På sidan Ändra miniatyrbild väljer du **[!UICONTROL Save Change]**.
1. På videons egenskapssida, i det övre högra hörnet, väljer du **[!UICONTROL Save & Close]**.



<!--

## About video thumbnails in Dynamic Media Hybrid mode{#about-video-thumbnails-in-dynamic-media-hybrid-mode}

You can choose from one of ten thumbnail images automatically generated by Dynamic Media to add to your video. The video player displays your selected thumbnail when a video asset is used with the Dynamic Media component in the authoring environment of Experience Manager Sites, Experience Manager Mobile, or Experience Manager Screens. The thumbnail serves as a static picture that best represents the contents of your entire video and further encourages users to select the Play button.

Based on the total time of the video, Dynamic Media captures ten (default) thumbnail images at 1%, 11%, 21%, 31%, 41%, 51%, 61%, 71%, 81%, and 91% into the video. The ten thumbnails persist meaning that if you decide to choose a different thumbnail later on, you do not need to regenerate the series. You preview the ten thumbnail images and then select the one you want to use with your video. If you want to change to default you can use CRXDE Lite to configure the time interval that thumbnail images are generated. For example, if you only wanted to generate a series of four evenly spaced thumbnail images from your video, you can configure the interval time at 24%, 49%, 74%, and 99%.

Ideally, you can add a video thumbnail anytime after you upload your video but before you publish the video on your website.

If you prefer, you can choose to upload a custom thumbnail to represent your video instead of using a thumbnail generated by Dynamic Media. For example, you could create a custom thumbnail image that has the title of your video, an eye-catching opening image, or a very specific image captured from your video. The custom video thumbnail image that you upload should have a maximum resolution of 1280 x 720 pixels (minimum width of 640 pixels) and be no larger than 2MB.

See also [About video thumbnails](/help/assets/dynamic-media/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

-->

<!--

### Adding a video thumbnail {#adding-a-video-thumbnail}

1. Navigate to an uploaded video asset that you want to add a video thumbnail.
1. In asset selection mode either from the List View or the Card View, select the video asset.
1. On the toolbar, select the **[!UICONTROL View Properties]** icon (a circle with an "i" in it).
1. On the video's Properties page, select **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, on the toolbar, select **[!UICONTROL Select Frame]**.

   Dynamic Media generates a series thumbnail images from your video, based on the default time interval or time interval you customized.

1. Preview the generated thumbnail images, then select the one you want to add to your video.
1. Select **[!UICONTROL Save Change]**.

   The video's thumbnail image is updated to use the thumbnail you selected. If you later decide to change the thumbnail image, you can return to the **[!UICONTROL Change Thumbnail]** page and select a new one.

   If you configured new default time intervals, or you uploaded a new video to replace the existing video, you will need to have Dynamic Media regenerate the thumbnails.

   See [Configuring the default time interval that video thumbnails are generated](#configuring-the-default-time-interval-that-video-thumbnails-are-generated).

-->

<!--

#### Configuring the default time interval that video thumbnails are generated {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

When you configure and save the new default time interval, your change automatically applies only to videos that you upload in the future. It does not automatically apply the new default to videos that you previously uploaded. For existing videos, you must regenerate the thumbnails.

See [Adding a video thumbnail](#adding-a-video-thumbnail).

**To configure the default time interval that video thumbnails are generated,**

1. In Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.

1. In the CRXDE Lite page, in the directory panel on the left, navigate t `o etc/dam/imageserver/configuration/jcr:content/settings.`

   if the directory panel is not visible, you may need to select the >> icon to the left of the Home tab.

1. On the lower-right panel, in the Properties tab, double-tap `thumbnailtime`.
1. In the Edit thumbnailtime dialog box, use the text fields to enter interval values as percentages.

    * Select the plus sign (+) icon to add one or more interval value fields. You may need to scroll to the bottom of the dialog box to see the icon.
    * Select the minus sign (-) icon to the right of an interval value field to delete it from the list.
    * Select the up arrow icon and the down arrow icon to reorder the interval values.

1. Select **[!UICONTROL OK]** to return to the Properties tab.
1. Near the upper-left corner of the CRXDE Lite page, select **[!UICONTROL Save All]**, then select the Back Home icon in the upper-left corner to return to Experience Manager.

   See [Adding a video thumbnail](#adding-a-video-thumbnail).

-->

<!--

### Adding a custom video thumbnail {#adding-a-custom-video-thumbnail-1}

These steps apply only to Dynamic Media running in Hybrid mode.

T**o add a custom video thumbnail**,

1. Navigate to an uploaded video asset that you want to add a custom video thumbnail.
1. In asset selection mode either from the List View or the Card View, select the video asset.
1. On the toolbar, select the **[!UICONTROL View Properties]** icon (a circle with an "i" in it).
1. On the video's Properties page, select **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, on the toolbar, select **[!UICONTROL Upload New Thumbnail]**.
1. Navigate to a thumbnail image you want to use, select it, then select **[!UICONTROL Open]** to begin uploading the image into Experience Manager. Following the upload, be sure you publish the image.
1. After you have successfully uploaded and published the image, in the Change Thumbnail page, select **[!UICONTROL Save Changes]**.

   The custom thumbnail is added to your video.

-->

## Ändra Dynamic Media URL för Dynamic Media-resurser

Videor som bearbetas i Dynamic Media kan användas i färdiga visningsprogram och även genom direktåtkomst till manifest-URL:er och uppspelning av dem via egna visningsprogram. Nedan följer API:t för hämtning av manifest-URL:er för en video.

### Om API:t getVideoManifestURI

The `getVideoManifestURI`API exponeras via c`q-scene7-api:com.day.cq.dam.scene7.api` och kan användas för att generera följande manifest-URL:er:

```java
/**   
* Returns the manifest url for videos 
* @param resource video resource 
* @param manifestType type of video streaming manifest being requested 
* @param onlyIfPublished return a manifest only if the video is published 
* @return the manifest url for videos 
* 
* @throws Exception 
*/
@Nullable 
String getVideoManifestURI(Resource resource, ManifestType manifestType, boolean onlyIfPublished) throws Exception;
```

#### getVideoManifestURI API-parametrar

Detta API har följande tre parametrar:

| Parameter | Beskrivning |
| --- | --- |
| `resource` | Resursen som motsvarar videon som Dynamic Media har inhämtat. |
| `manifestType` | Kan vara antingen `ManifestType.DASH` eller `ManifestType.HLS` |
| `onlyIfPublished` | Ange som true om manifest-URI bara genereras om den är publicerad och tillgänglig på leveransnivån. |

Om du vill hämta manifest-URL:er för videofilmer med metoden ovan lägger du till en [videokodningsprofil](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) till mappen&quot;upload videos&quot;. Dynamic Media bearbetar dessa videofilmer baserat på kodningarna i den videokodningsfil som tilldelats mappen. Nu kan du anropa ovanstående API för att hämta manifest-URL:er för de överförda videoklippen.

### Felscenarier

API:t returnerar null om det finns fel. Undantag loggas i felloggarna i Experience Manager. Alla sådana loggade fel börjar med `Could not generate Video Manifest URI`. Följande scenarier kan orsaka sådana fel:

* An `IllegalArgumentException` loggas för något av följande:

   * The `resource` parametern som skickades är null.
   * The `resource` Den skickade parametern är inte en video.
   * The `manifestType` parametern som skickades är null.
   * The `onlyIfPublished` -parametern skickas som true, men videon publiceras inte.
   * Videon har inte importerats med en adaptiv videouppsättning från Dynamic Media.

* `IOException` loggas när det uppstår ett problem med att ansluta till Dynamic Media.
* `UnsupportedOperationException` loggas när en `manifestType` parametern som skickas är `ManifestType.DASH`, medan videon inte har bearbetats i DASH-format.

<!-- THE REMAINING SECTION IS FOR 6.5 ONLY 

The following is an example of the above API using servlets written in *HTTPWhiteBoard* specification. Select each tab for the code syntax.

>[!BEGINTABS]

>[!TAB Add dependency in pom.xml]

+++**Add dependency in pom.xml** 

```java
dependency> 
     <groupId>com.day.cq.dam</groupId> 
     <artifactId>cq-scene7-api</artifactId> 
     <version>5.12.64</version> 
     <scope>provided</scope> 
</dependency> 
```

+++

>[!TAB Sample servlet]

+++**Sample servlet** 

```java
@Component
        service = Servlet.class 
) 
@HttpWhiteboardServletPattern(value = ManifestServlet.SERVLET_PATTERN) 
@HttpWhiteboardContextSelect(value = Constants.SERVLET_CONTEXT_SELECTOR) 
public class ManifestServlet extends HttpServlet { 

   private static final Logger LOGGER = LoggerFactory.getLogger(ManifestServlet.class); 

   private final ObjectMapper objectMapper; 

    @Reference 
    private Scene7Service scene7Service; 

   public static final String SERVLET_PATTERN = Constants.VIDEO_API_PREFIX + "/manifestUrl"; 

   public ManifestServlet() {
         this.objectMapper = new ObjectMapper(); 
         objectMapper.setSerializationInclusion(JsonInclude.Include.NON_NULL); 
   }

   @Override 

   protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        final ResourceResolver resolver = getResourceResolver(request); 
        String assetPath = request.getParameter("assetPath"); 
        String manifest = request.getParameter("manifestType"); 
        String onlyIfPublished = request.getParameter("onlyIfPublished"); 
        Resource resource = resolver.getResource(assetPath); 
        response.setCharacterEncoding(StandardCharsets.UTF_8.toString()); 
        response.setContentType("application/json"); 
        if(resource == null) { 
            LOGGER.info("could not retrieve the resource from JCR"); 
            error("could not retrieve the resource from JCR", response); 
            return; 
        }

        String manifestUri = null; 

        try{ 
            ManifestType manifestType =  ManifestType.DASH; 
            if(manifest != null) { 
                manifestType = ManifestType.valueOf(manifest); 
            } 
            manifestUri = scene7Service.getVideoManifestURI(resource, manifestType, onlyIfPublished != null); 
            objectMapper.writeValue(response.getWriter(), new ManifestUrl(manifestUri)); 
            response.setContentType("application/json"); 
        } catch (Exception e) { 
            LOGGER.error(e.getMessage(), e); 
            error(String.format("Unable to get the manifest url for %s. %s", assetPath, e.getMessage()), response); 
        } 
    } 

    private ResourceResolver getResourceResolver(HttpServletRequest request) { 
        Object rr = request.getAttribute(AuthenticationSupport.REQUEST_ATTRIBUTE_RESOLVER); 
        if (!(rr instanceof ResourceResolver)) { 
            throw new IllegalStateException( 
                    "The request does not seem to have been created via Apache Sling's authentication mechanism."); 
        } else { 
            return (ResourceResolver) rr; 
        } 
    } 

    private void error(String errorMessage, HttpServletResponse response) throws IOException { 
        ManifestUrl errorManifest = new ManifestUrl(null); 
        errorManifest.setErrorMessage(errorMessage); 
        response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR); 
        objectMapper.writeValue(response.getWriter(), errorManifest); 
    } 
} 
```

+++

>[!TAB Response Class for servlet]

+++**Response Class for servlet** 

```java
public class ManifestUrl extends VideoResponse { 
     String manifestUrl; 
     public ManifestUrl(String manifestUrl) { 
         this.manifestUrl = manifestUrl; 
     } 
     public String getManifestUrl() { 
         return manifestUrl; 
     } 
} 

public abstract class VideoResponse { 
     String errorString; 

     public String getErrorString() { 
         return errorString; 
     } 

     public void setErrorMessage(String errorString) { 
         this.errorString = errorString; 
     } 
} 
```

+++

>[!TAB Constants file referenced in servlet]

+++**Constants file referenced in servlet** 

```java
public final class Constants { 

     private Constants() { 
     } 

     public static final String VIDEO_API_PREFIX = "/dynamicmedia/video"; 
     public static final String SERVLET_CONTEXT_SELECTOR = "(" + HttpWhiteboardConstants.HTTP_WHITEBOARD_CONTEXT_NAME + "=" + 
             DMSampleApiHttpContext.CONTEXT_NAME + ")"; 

 } 
```

+++

>[!TAB ServletContext]

+++**ServletContext** 

Mount the above servlet using a `servletContext`. The following is an example of `servletContext`. 

```java
public class DMSampleApiHttpContext extends ServletContextHelper { 

 public static final String CONTEXT_NAME = "com.adobe.dmSample"; 
 public static final String CONTEXT_PATH = "/dmSample"; 

 private final MimeTypeService mimeTypeService; 

 private final AuthenticationSupport authenticationSupport; 

 /** 
  * Constructs a new context that will use the given dependencies. 
  * 
  * @param mimeTypeService Used when providing mime type of requests. 
  * @param authenticationSupport Used to authenticate requests with sling. 
  */ 
 @Activate 
 public DMSampleApiHttpContext(@Reference final MimeTypeService mimeTypeService, 
                               @Reference final AuthenticationSupport authenticationSupport) { 
     this.mimeTypeService = mimeTypeService; 
     this.authenticationSupport = authenticationSupport; 
 } 

 // ---------- HttpContext interface ---------------------------------------- 
 /** 
  * Returns the MIME type as resolved by the <code>MimeTypeService</code> or 
  * <code>null</code> if the service is not available. 
  */ 
 @Override 
 public String getMimeType(String name) { 
     MimeTypeService mtservice = mimeTypeService; 
     if (mtservice != null) { 
         return mtservice.getMimeType(name); 
     } 
     return null; 
 } 

 /** 
  * Returns the real context path that is used to mount this context. 
  * @param req servlet request 
  * @return the context path 
  */ 
 public static String getRealContextPath(HttpServletRequest req) { 
     final String path = req.getContextPath(); 
     if (path.equals(CONTEXT_PATH)) { 
         return ""; 
     } 
     return path.substring(CONTEXT_PATH.length()); 
 } 

 /** 
  * Returns a request wrapper that transforms the context path back to the original one 
  * @param req request 
  * @return the request wrapper 
  */ 
 public static HttpServletRequest createContextPathAdapterRequest(HttpServletRequest req) { 
     return new HttpServletRequestWrapper(req) { 

         @Override 
         public String getContextPath() { 
             return getRealContextPath((HttpServletRequest) getRequest()); 
         } 

     }; 

 } 

 /** 
  * Always returns <code>null</code> because resources are all provided 
  * through individual endpoint implementations. 
  */ 
 @Override 
 public URL getResource(String name) { 
     return null; 
 } 

 /** 
  * Tries to authenticate the request using the 
  * <code>SlingAuthenticator</code>. If the authenticator or the Repository 
  * is missing this method returns <code>false</code> and sends a 503/SERVICE 
  * UNAVAILABLE status back to the client. 
  */ 
 @Override 
 public boolean handleSecurity(HttpServletRequest request, 
                               HttpServletResponse response) throws IOException { 

     final AuthenticationSupport authenticator = this.authenticationSupport; 
     if (authenticator != null) { 
         return authenticator.handleSecurity(createContextPathAdapterRequest(request), response); 
     } 

     // send 503/SERVICE UNAVAILABLE, flush to ensure delivery 
     response.sendError(HttpServletResponse.SC_SERVICE_UNAVAILABLE, 
             "AuthenticationSupport service missing. Cannot authenticate request."); 
     response.flushBuffer(); 

     // terminate this request now 
     return false; 
 } 
}
```

+++

>[!ENDTABS]



### Use the sample servlet

You invoke the servlet by performing a `GET` operation at `/dmSample/dynamicmedia/video/manifestUrl`. The following query parameters are passed: 

| Query parameter | Description |
| --- | --- |
| `assetPath` | Mandatory. The path to the video for which `manifestUrl` is generated. |
| `manifestType` | Optional. Parameter can be DASH or HLS. If it is not passed, it defaults to DASH. |
| `onlyIfPublished` | Optional. If passed, the `manifestUrl` is returned only if the video is published.  |

In this example, let us assume the following setup: 

* The company is `samplecompany`.
* The authoring instance is `http://sample-aem-author.com`.
* The folder `/content/dam/video-example` has a video encoding profile applied to it. 
* The video `scenery.mp4` is uploaded to the folder `/content/dam/video-example`.

You can invoke the servlet in following ways: 
     
| Type | Description |
| :--- | --- |
| HLS | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=HLS&assetPath=/content/dam/video-example/scenery.mp4`<br><br>In case DASH delivery is enabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8?packagedStreaming=true"}`<br><br>In case DASH delivery is disabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8"}` |
| DASH | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scenery.mp4`<br><br>In case DASH delivery is enabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.mpd"}`<br><br>In case DASH delivery is disabled:<br>`{}` |
| Error: asset path is wrong | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scennnnnnery.mp4`<br><br>`{"errorString":"could not retrieve the resource from JCR"}` |

-->





