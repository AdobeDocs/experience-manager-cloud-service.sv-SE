---
title: Video i Dynamic Media
description: Lär dig arbeta med video i Dynamic Media. Granska de bästa sätten att koda videofilmer, publicera videofilmer på YouTube, visa videorapporter och lägga till undertexter eller kapitelmarkörer i videofilmer.
contentOwner: Rick Brough
feature: Video Profiles,Best Practices
role: User
exl-id: 0d5fbb3e-b763-415f-8c69-ea36445f882b
source-git-commit: 6cc21d0e7330b3dd4254ad15b64dc94c065417f7
workflow-type: tm+mt
source-wordcount: '9687'
ht-degree: 1%

---

# Video {#video}

I det här avsnittet beskrivs hur du arbetar med video i Dynamic Media.

## Snabbstart: Videor {#quick-start-videos}

Följande steg-för-steg-beskrivning av arbetsflödet hjälper dig att komma igång snabbt med adaptiva videouppsättningar i Dynamic Media. Efter varje steg finns det korsreferenser till ämnesrubriker där du kan hitta mer information.

>[!NOTE]
>
>Innan du arbetar med video i Dynamic Media måste du kontrollera att Adobe Experience Manager-administratören redan har aktiverat och konfigurerat Dynamic Media Cloud Services.
>
>* Se [Konfigurera Dynamic Media Cloud-tjänster](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) i Konfigurera dynamiska media och [Felsök dynamiska media](/help/assets/dynamic-media/troubleshoot-dm.md).
>

1. **Överför dina dynamiska medievideor** genom att göra följande:

   * Skapa en egen videokodningsprofil. Eller så kan du helt enkelt använda den fördefinierade _adaptiva videokodningsprofilen_ som medföljer Dynamic Media.

      * [Skapa en videokodningsprofil](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * Den maximala utdatakodningsupplösningen är 8 192 × 4 320 eller 4 320 × 8 192.md.
      * Läs mer om [Bästa tillvägagångssätt för videokodning](#best-practices-for-encoding-videos).

   * Koppla videobearbetningsprofilen till en eller flera mappar där du ska överföra dina primära källvideor.

      * [Använd en videoprofil för mappar](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).
      * Läs mer om [Ordna digitala resurser](/help/assets/organize-assets.md).

   * Överför dina primära källvideor till de angivna mapparna. När du har lagt till videofilmerna kodas de enligt den videobearbetningsprofil som tilldelats mappen.

      * Dynamic Media har stöd för i första hand videor i kort form med en maxlängd på 30 minuter och en minimiupplösning som är större än 25 × 25.
      * Den högsta videoupplösningen som stöds är 16 384 × 16 384.
      * Du kan överföra videofiler som är upp till 15 GB vardera.
      * [Överför dina videor](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).
      * Läs mer om [Indatafilformat som stöds](/help/assets/file-format-support.md).

   * Övervaka hur [videokodningen fortskrider](#monitoring-video-encoding-and-youtube-publishing-progress) antingen från resursvyn eller arbetsflödesvyn.

1. **Hantera dina dynamiska medievideor** genom att göra något av följande:

   * Ordna, bläddra bland och söka efter videomaterial

      * [Ordna digitala resurser](/help/assets/organize-assets.md)
      * [Söka efter videomaterial](/help/assets/search-assets.md#custompredicates) eller [Söka efter resurser](/help/assets/manage-digital-assets.md#search-assets)

   * Förhandsgranska och publicera videomaterial

      * Visa källvideon och de kodade återgivningarna av videon tillsammans med tillhörande miniatyrer:

        [Förhandsgranska videoklipp](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) eller [Förhandsgranska resurser](/help/assets/dynamic-media/previewing-assets.md)
        [Hantera videorenderingar](/help/assets/manage-digital-assets.md#managing-renditions)

      * [Hantera förinställningar för visningsprogram](/help/assets/dynamic-media/managing-viewer-presets.md)
      * [Publicera resurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)

   * Arbeta med videometadata

      * Redigera egenskaperna för video, till exempel titel, beskrivning och taggar, anpassade metadatafält:

        [Redigera videoegenskaper](/help/assets/manage-digital-assets.md#editing-properties)

      * [Hantera metadata för digitala resurser](/help/assets/manage-metadata.md)
      * [Metadata-scheman](/help/assets/metadata-schemas.md)

   * Granska, godkänn och kommentera videoklipp och behåll fullständig versionskontroll

      * [Anteckna videoklipp](/help/assets/manage-video-assets.md#annotate-video-assets) eller [Anteckna resurser](/help/assets/manage-digital-assets.md#annotating)

      * [Skapa en version](/help/assets/manage-digital-assets.md#asset-versioning)
      * [Starta ett arbetsflöde för en resurs](/help/assets/manage-digital-assets.md#starting-a-workflow-on-an-asset)

      * [Granska mappresurser](/help/assets/bulk-approval.md)
      * [Projekt](/help/sites-cloud/authoring/projects/overview.md)

1. **Publicera dina dynamiska medievideor** genom att göra något av följande:

   * Om du använder Experience Manager som WCM-system (Web Content Management) kan du lägga till videofilmer direkt på dina webbsidor.

      * [Lägg till videofilmer på dina webbsidor](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

   * Om du använder ett WCM-system från en annan leverantör kan du länka eller bädda in videor på dina webbsidor.

      * Integrera video med URL:

        [Länka URL:er till ditt webbprogram](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md).

      * Integrera video med inbäddad kod på en webbsida:

        [Bädda in videovisningsprogrammet på en webbsida](/help/assets/dynamic-media/embed-code.md).

   * [Generera videorapporter](#viewing-video-reports).

   * [Lägg till flera bildtexter och ljudspår i en video](#about-msma).

## Arbeta med video i Dynamic Media {#working-with-video-in-dynamic-media}

Video in Dynamic Media är en totallösning som gör det enkelt att publicera högkvalitativ adaptiv video för direktuppspelning på flera skärmar, inklusive stationära datorer, surfplattor och mobila enheter. En adaptiv videouppsättning grupperar versioner av samma video som är kodade med olika bithastigheter och format som 400 kbit/s, 800 kbit/s och 1 000 kbit/s. Datorns eller mobilenhetens tillgängliga bandbredd identifieras.

På en mobilenhet från iOS identifieras t.ex. en bandbredd som 3G, 4G eller Wi-Fi. Sedan väljs automatiskt rätt kodad video bland de olika videobithastigheterna i den adaptiva videouppsättningen. Videon strömmas till datorer, mobila enheter eller surfplattor.

Dessutom ändras videokvaliteten dynamiskt automatiskt om nätverksförhållandena ändras på datorn eller den mobila enheten. Om en kund går över till helskärmsläge på en stationär dator svarar den adaptiva videouppsättningen med en bättre upplösning, vilket förbättrar kundens tittarupplevelse. Med adaptiva videouppsättningar får du bästa möjliga tittarupplevelse för kunder som spelar upp Dynamic Media-video på flera skärmar och enheter.

Den logik som en videospelare använder för att avgöra vilken kodad video som ska spelas upp eller väljas under uppspelningen baseras på följande algoritm:

1. Videospelaren läser in det inledande videofragmentet baserat på den bithastighet som ligger närmast värdet som är inställt för&quot;inledande bithastighet&quot; i själva spelaren.
1. Videospelaren växlar baserat på ändringar av bandbreddshastigheten med följande kriterier:

   1. Spelaren väljer den högsta bandbreddsströmmen under eller lika med den beräknade bandbredden.
   1. Spelaren hanterar bara 80 % av den tillgängliga bandbredden. Men om den byter upp sig är det mer försiktigt med bara 70 % för att undvika överskattning och omedelbart gå tillbaka.

Detaljerad teknisk information om algoritmen finns på [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

Följande stöds när du hanterar enstaka video och adaptiva videouppsättningar:

* Överföra video från ett antal videoformat och ljudformat som stöds. Kodning av video till MP4 H.264-format för uppspelning på flera skärmar. Du kan använda fördefinierade adaptiva videoförinställningar, enskilda videokodningsförinställningar eller anpassa din egen kodning för att styra videons kvalitet och storlek.

   * När en adaptiv videouppsättning genereras innehåller den MP4-videor.
   * **Obs!**: Primära videoklipp/källvideoklipp läggs inte till i en adaptiv videouppsättning.

* Videoklipp i alla HTML5-videovisningsprogram.
* Ordna, bläddra bland och sök videoklipp med fullt stöd för metadata för effektiv hantering av videomaterial.
* Leverera adaptiva videouppsättningar till webben, datorer, surfplattor och mobila enheter.

Adaptiv videoströmning stöds på olika iOS-plattformar. Se [Referenshandbok för dynamiska mediavisare](https://experienceleague.adobe.com/sv/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference).

<!-- OUTDATED 2/28/22 BASED ON CQDOC-18692 Dynamic Media supports mobile video playback for MP4 H.264 video. You can find BlackBerry&reg; devices that support this video format at the following: [Supported video formats on BlackBerry&reg;](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

OUTDATED 2/28/22 BASED ON CQDOC-18692 You can find Windows&reg; devices that support this video format at the following [Supported video formats on Windows&reg; Phone](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs). -->

* Spela upp videon med Dynamic Media Video Viewer Presets, inklusive följande:

   * Enstaka videovisningsprogram.
   * Visningsprogram för blandade media som kombinerar både video- och bildinnehåll.

* Konfigurera videospelare för att tillgodose era varumärkesbehov.
* Integrera video på webbplatsen, mobilsajten eller mobilapplikationen med en enkel URL eller inbäddningskod.

<!-- GIVES a 404 See [Dynamic video playback](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&config=GeoRetail/Universal_Video1&stageSize=640,480) sample. -->

Se även [Visningsprogram för Experience Manager Assets och Dynamic Media Classic](https://experienceleague.adobe.com/sv/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers#viewers-aem-assets-dmc) och [Endast för Experience Manager Assets](https://experienceleague.adobe.com/sv/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers#viewers-for-aem-assets-only) i [referenshandboken för dynamiska mediavisare](https://experienceleague.adobe.com/sv/docs/dynamic-media-developer-resources).

## Bästa praxis: Använda videovisningsprogrammet för HTML5 {#best-practice-using-the-html-video-viewer}

Förinställningarna för videovisningsprogrammet HTML5 för Dynamic Media är robusta videospelare. Du kan använda dem för att undvika många vanliga problem som är kopplade till videouppspelning i HTML5 och problem som är kopplade till mobila enheter. Exempel: brist på strömmande bithastighet och begränsad webbläsarräckvidd.

På designsidan av spelaren kan du utforma videospelarens funktioner med standardverktyg för webbutveckling. Du kan till exempel utforma knapparna, kontrollerna och den anpassade bakgrunden för förhandsvisningsbilder med HTML5 och CSS så att du kan nå dina kunder med ett anpassat utseende.

På visningsprogrammets uppspelningssida identifieras webbläsarens videokapacitet automatiskt. Sedan visas videon med HLS eller DASH, som också kallas adaptiv videoströmning. Eller, om leveransmetoderna inte finns, används progressiv i HTML5 i stället.

Du kan kombinera möjligheten att utforma uppspelningskomponenterna med HTML5 och CSS i en enda spelare. Den kan ha inbäddad uppspelning och använda adaptiv och progressiv strömning beroende på webbläsarens kapacitet. Alla dessa funktioner innebär att du kan utöka räckvidden för ditt multimediematerial till både dator- och mobilanvändare och få en smidig videoupplevelse.

Se även [Endast visningsprogram för Experience Manager Assets](https://experienceleague.adobe.com/sv/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers#viewers-for-aem-assets-only) i [referenshandboken för dynamiska medievyer](https://experienceleague.adobe.com/sv/docs/dynamic-media-developer-resources).


### Uppspelning av video på stationära datorer och mobila enheter med videovisningsprogrammet för HTML5 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

För strömning av anpassningsbara video för datorer och mobilenheter baseras de videor som används för växling av bithastighet på alla MP4-videor i den adaptiva videouppsättningen.

Videouppspelning sker med HLS eller DASH, eller progressiv videouppspelning. I tidigare versioner av Experience Manager, till exempel 6.0, 6.1 och 6.2, strömmades videofilmer via HTTP.

I Experience Manager 6.3 och senare direktuppspelas videor nu via HTTPS (dvs. HLS eller DASH) eftersom DM-gatewaytjänstens URL alltid använder HTTPS. Det här standardbeteendet påverkar inte kunderna. Videoströmning sker alltid över HTTPS om webbläsaren stöder det. Se följande tabell.

Därför bör

* Om du har en HTTPS-webbplats med HTTPS-videoströmning går det bra att strömma.
* Om du har en HTTP-webbplats med HTTPS-videoströmning går det bra att strömma och det finns inga blandade innehållsproblem i webbläsaren.

DASH är den internationella standarden och HLS är en Apple-standard. Båda används för adaptiv videoströmning. Och båda teknikerna justerar automatiskt uppspelningen baserat på bandbreddskapaciteten i nätverket. Man kan också &quot;söka&quot; till valfri punkt i videon utan att behöva vänta på att resten av videon ska laddas ned.

Progressiv video levereras genom att videon hämtas och lagras lokalt på en användares dator eller mobila enhet.

I följande tabell beskrivs enheten, webbläsaren och uppspelningsmetoden för videofilmer på stationära datorer och mobila enheter med [Dynamic Media HTML5 Video Viewer](https://experienceleague.adobe.com/sv/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video#interactive-video).

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
   <td>I Windows® 8 och Windows® 10 - Tvinga användning av HTTPS när DASH eller HLS begärs. Känd begränsning: HTTP på DASH eller HLS fungerar inte i den här kombinationen av webbläsare/operativsystem <br /> <br /> i Windows® 7 - progressiv nedladdning. Använder standardlogik för HTTP- och HTTPS-protokoll.</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Firefox 23-44</td>
   <td>Progressiv hämtning.</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Firefox 45 eller senare</td>
   <td>HLS eller DASH* adaptiv bithastighetsströmning</td>
  </tr>
  <tr>
   <td>Skrivbord</td>
   <td>Chrome</td>
   <td>HLS eller DASH* adaptiv bithastighetsströmning</td>
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
   <td>HLS eller DASH* adaptiv bithastighetsströmning/td&gt;
  </tr>
  <tr>
   <td>Mobil</td>
   <td>Android™ (webbläsare)</td>
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

<!--  THIS LINE WAS REMOVED FROM THE TABLE ABOVE ON FEB 28, 2022 BASED ON CQDOC 18692 -RSB <tr>
   <td>Mobile</td>
   <td>BlackBerry&reg;</td>
   <td>HLS or DASH</td>
  </tr>
 -->

## Arkitektur för Dynamic Media Video Solution {#architecture-of-dynamic-media-video-solution}

I följande bild visas det övergripande arbetsflödet för redigering av videoklipp som överförs och kodas via DMG-gatewayen (i Dynamic Media Hybrid-läge) och görs tillgängliga för offentlig användning.

![chlimage_1-427](assets/chlimage_1-427.png)

## Hybrid publiceringsarkitektur för videor {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## Bästa tillvägagångssätt för att koda videofilmer {#best-practices-for-encoding-videos}

Arbetsflödet **Dynamic Media Encode Video** kodar video om du har aktiverat Dynamic Media och konfigurerat Video Cloud Services. Det här arbetsflödet innehåller information om arbetsflödets processhistorik och fel. Om du har aktiverat Dynamic Media och konfigurerat Video Cloud Services börjar arbetsflödet **[!UICONTROL Dynamic Media Encode Video]** automatiskt att gälla när du överför en video. (Om du inte använder Dynamic Media börjar arbetsflödet **[!UICONTROL DAM Update Asset]** gälla.)

Nedan följer några tips om hur du kodar källvideofiler.

<!-- For advice about video encoding, see the following:

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en).
* [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en). -->

### Source videofiler {#source-video-files}

När du kodar en videofil ska du använda en källvideofil med högsta möjliga kvalitet. Undvik att använda tidigare kodade videofiler eftersom dessa filer redan är komprimerade, och ytterligare kodning skapar en video med delkvalitet.

* Dynamic Media har stöd för i första hand videor i kort form med en maxlängd på 30 minuter och en minimiupplösning som är större än 25 × 25.
* Du kan överföra primära källvideofiler som är upp till 15 GB vardera.

I följande tabell beskrivs rekommenderad storlek, proportioner och lägsta bithastighet som källvideofilerna måste ha innan du kodar dem:

| Storlek | Proportioner | Minsta bithastighet |
|--- |--- |--- |
| 1024 × 768 | 4:3 | 4 500 kbit/s för de flesta videofilmer. |
| 1280 × 720 | 16:9 | 3 000 - 6 000 kbit/s, beroende på mängden rörelse i videon. |
| 1920 × 1080 | 16:9 | 6000 - 8 000 kbit/s, beroende på mängden rörelse i videon. |

### Hämta metadata för en fil {#obtaining-a-file-s-metadata}

Du kan hämta metadata för en fil genom att visa dess metadata med ett redigeringsverktyg för videoklipp eller med ett program som utformats för att hämta metadata. Nedan följer instruktioner om hur du använder MediaInfo, ett tredjepartsprogram, för att hämta videofilens metadata:

1. Gå till [Hämta MediaInfo](https://mediaarea.net/en/MediaInfo/Download).
1. Välj och hämta installationsprogrammet för den grafiska användargränssnittsversionen och följ installationsanvisningarna.
1. Efter installationen högerklickar du på videofilen (endast Windows®) och väljer MediaInfo, eller så öppnar du MediaInfo och drar videofilen till programmet. Alla metadata som är associerade med videofilen, inklusive bredd, höjd och fps, visas.

### Proportioner {#aspect-ratio}

När du väljer eller skapar en förinställning för videokodning för den primära källvideofilen måste du se till att förinställningen har samma proportioner. Det här arbetssättet säkerställer konsekvens med den primära källvideofilen. Proportionerna är proportionerna mellan videons bredd och höjd.

Om du vill ta reda på videofilens proportioner hämtar du filens metadata. Observera filens bredd och höjd (se Hämta metadata för en fil ovan). Använd sedan den här formeln för att bestämma proportionerna:

width/height = aspect ratio

I följande tabell beskrivs hur formelresultaten översätts till vanliga alternativ för proportioner:

| Formelresultat | Proportioner |
|--- |--- |
| 1,33 | 4:3 |
| 0,75 | 3:4 |
| 1,78 | 16:9 |
| 0,56 | 9:16 |

En video som till exempel är 1440 bredd × 1080 höjd har proportionerna 1440/1080 eller 1,33. I det här fallet väljer du en förinställning för videokodning med 4:3-proportioner för att koda videofilen.

### Bithastighet {#bitrate}

Bithastigheten är den mängd data som kodas för att skapa en enda sekund av videouppspelningen. Bithastigheten mäts i kilobit per sekund (kbit/s).

>[!NOTE]
>
>Eftersom förlustgivande komprimering används för alla kodekar är bithastigheten den viktigaste faktorn i videokvaliteten. Ju mer du komprimerar en videofil desto sämre blir kvaliteten. Därför är alla andra egenskaper lika (upplösning, bildrutehastighet och kodek), ju lägre bithastighet, desto lägre kvalitet får den komprimerade filen.

När du väljer en bithastighetskodning kan du välja mellan två typer:

* **[!UICONTROL Constant Bitrate Encoding]** (CBR) - Under CBR-kodning är bithastigheten, eller antalet bitar per sekund, densamma under hela kodningsprocessen. CBR-kodning bevarar den angivna datahastigheten enligt inställningen för hela videon. CBR-kodning optimerar inte heller mediefiler för kvalitet utan sparar på lagringsutrymmet.
Använd CBR om videon innehåller en liknande rörelsenivå i hela videon. CBR används oftast för direktuppspelat videoinnehåll. Se även [Använda egna videokodningsparametrar](/help/assets/dynamic-media/video-profiles.md#using-custom-added-video-encoding-parameters).

* **[!UICONTROL Variable Bitrate Encoding]** (VBR) - VBR-kodning justerar datahastigheten nedåt och till den övre gräns som du anger, baserat på de data som krävs av kompressorn. Den här funktionen innebär att under en VBR-kodningsprocess ökar eller minskar bithastigheten för mediefilen dynamiskt beroende på mediefilens behov av bithastighet.
Det tar längre tid att koda VBR men ger det bästa resultatet. Kvaliteten på mediefilen är bättre. VBR används oftast för http-progressiv leverans av videoinnehåll.

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

**Upplösning** beskriver videofilens höjd och bredd i pixlar. Den mesta källvideon lagras med hög upplösning (till exempel 1920 × 1080). Vid direktuppspelning komprimeras källvideo till en lägre upplösning (640 × 480 eller lägre).

Upplösning och datahastighet är två sammankopplade faktorer som avgör videokvaliteten. Om du vill behålla samma videokvalitet måste datahastigheten vara högre ju fler pixlar en videofil har (ju högre upplösning). Ta till exempel antalet pixlar per bildruta i en 320 × 240-upplösning och en 640 × 480-upplösningsvideofil:

| Upplösning | Pixlar per bildruta |
|--- |--- |
| 320 × 240 | 76 800 |
| 640 × 480 | 307 200 |

Filen 640 × 480 har fyra gånger fler pixlar per bildruta. För att uppnå samma datahastighet för dessa två exempelupplösningar använder du fyra gånger så hög komprimering på 640 × 480-filen, vilket kan minska videons kvalitet. En videodatahastighet på 250 kbit/s ger därför en högkvalitativ bild med upplösningen 320 × 240, men inte med upplösningen 640 × 480.

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
| 480p | 480 | Medium |
| 720p | 720 | Stor skärm |
| 1080p | 1080 | Stor HD-skärm |

Den högsta videoupplösningen som stöds är 16 384 × 16 384. Den maximala utdatakodningsupplösningen för video är 8 192 × 4 320 eller 4 320 × 8 192.

### Fps (bildrutor per sekund) {#fps-frames-per-second}

I USA och Japan spelas de flesta videoklipp in med 29,97 bildrutor per sekund. I Europa spelas de flesta videoklipp in med 25 bildrutor per sekund. En film filmas med 24 fps.

Välj en förinställning för videokodning som matchar fps-hastigheten för den primära källvideofilen. Om den primära källvideon till exempel är 25 fps väljer du en kodningsförinställning med 25 fps. Som standard används den primära källvideofilens fps för all anpassad kodning. Därför behöver du inte ange fps-inställningen explicit när du skapar en förinställning för videokodning.

### Videokodningsdimensioner {#video-encoding-dimensions}

För bästa resultat väljer du kodningsdimensioner så att källvideon är en hel multipel av alla dina kodade videor.

Om du vill beräkna förhållandet dividerar du källbredden med den kodade bredden för att få breddförhållandet. Sedan dividerar du källhöjden med kodad höjd för att få höjdförhållandet.

Om förhållandet är ett heltal betyder det att videon är optimalt skalad. Om den resulterande kvoten inte är ett heltal påverkas videokvaliteten genom att kvarvarande pixelartefakter lämnas kvar på skärmen. Effekten märks mest när videon innehåller text.

Anta till exempel att källvideon är 1 920 × 1 080. I följande tabell ger de tre kodade videoklippen de optimala kodningsinställningarna som kan användas.

| Videotyp | Bredd × höjd | Breddförhållande | Höjdförhållande |
|--- |--- |--- |--- |
| Source | 1920 × 1080 | 1 | 1 |
| Kodad | 960 × 540 | 2 | 2 |
| Kodad | 640 × 360 | 3 | 3 |
| Kodad | 480 × 270 | 4 | 4 |

### Kodat videofilformat {#encoded-video-file-format}

Dynamic Media rekommenderar att du använder MP4 H.264-videokodningsförinställningar. Eftersom MP4-filer använder H.264-videokodeken ger den video med hög kvalitet men i en komprimerad filstorlek.

## Visa videorapporter {#viewing-video-reports}

>[!NOTE]
>
>Videorapporter är bara tillgängliga när du kör Dynamic Media - hybrid-läge.

Videorapporter visar flera sammanställda värden för en angiven period, så att du kan övervaka att *publicerade* enskilda och sammanställda videor fungerar som förväntat. Följande viktigaste mätdata samlas in för alla publicerade videor på hela webbplatsen:

* Video börjar
* Slutförandefrekvens
* Genomsnittlig tid för video
* Total tid för video
* Videor per besök

En tabell över alla *publicerade* videor visas också, så att du kan spåra de mest visade videoklippen på webbplatsen baserat på den totala videostarten.

När du väljer ett videonamn i listan visas videons rapport om målgruppsinnehållande (bortfall) i form av ett linjediagram. Diagrammet visar antalet vyer för en given tidpunkt under videouppspelning. När du spelar upp videon synkroniseras det lodräta strecket med tidsindikatorn i spelaren. Släppningar i linjediagramdata indikerar var publiken slutar intressera sig.

Om videon kodades utanför Adobe Experience Manager Dynamic Media är inte målgruppsinnehållandediagrammet (drop-off) och uppspelningsprocentdata i tabellen tillgängliga.

>[!NOTE]
>
>Spårnings- och rapportdata baseras uteslutande på användningen av Dynamic Medias egen videospelare och tillhörande videospelarförinställning. Därför kan du inte spåra och rapportera videoklipp som spelas upp av andra videospelare.

Första gången du anger Videorapporter visas som standard videodata från och med den första i den aktuella månaden och till och med den aktuella månadens datum. Du kan dock åsidosätta standarddatumintervallet genom att ange ett eget datumintervall. Nästa gång i Videorapporter används det angivna datumintervallet.

För att videorapporter ska fungera på rätt sätt skapas ett Report Suite-ID automatiskt när Dynamic Media Cloud Services konfigureras. Samtidigt skickas Report Suite-ID:t till publiceringsservern så att det är tillgängligt för funktionen Kopiera URL när du förhandsgranskar resurser. Den här funktionen kräver dock att publiceringsservern redan har konfigurerats. Om publiceringsservern inte är konfigurerad kan du fortfarande publicera för att se videorapporten. Du måste dock gå tillbaka till Dynamic Media Cloud Configuration och välja **[!UICONTROL OK]**.

**Så här visar du videorapporter:**

1. I Experience Manager övre vänstra hörn väljer du Experience Manager logotyp. Klicka på ikonen ![Hammer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) > **[!UICONTROL Assets]** > **[!UICONTROL Video Reports]** i den vänstra listen.
1. Gör något av följande på sidan Videorapporter:

   * I närheten av det övre högra hörnet väljer du ikonen **[!UICONTROL Refresh Video Report]**.
Du kan bara använda Uppdatera om rapportens slutdatum är den aktuella dagen. Med den här funktionen ser du till att du kan se videospårningen som har utförts sedan du senast körde rapporten.

   * I närheten av det övre högra hörnet väljer du ikonen **[!UICONTROL Date Picker]**.
Ange start- och slutdatumintervallet som du vill ha videodata för och välj sedan **[!UICONTROL Run Report]**.

   I grupprutan Top Metrics (Toppvärden) identifieras olika aggregerade mått för alla *publicerade* videor på webbplatsen.

1. I tabellen som listar de publicerade videoklippen väljer du ett videonamn för att spela upp videon och ser även videons återgivningsrapport.

<!-- OBSOLETE CONTENT OBSOLETE CONTENT - SDK ONLY AVAILABLE INTERNALLY NOW 
### Viewing video reports based on a video viewer that you created using the Dynamic Media HTML5 Viewer SDK {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

If you are using an out-of-box video viewer provided by Dynamic Media, or if you created a custom viewer preset based off of an out-of-box video viewer, then no additional steps are required to view video reports. However, if you have created your own video viewer based off the Dynamic Media HTML5 Viewer SDK, then use the following steps to ensure the your video viewer is sending tracking events to Dynamic Media Video Reports.

Use the Dynamic Media Viewers Reference and the Dynamic Media HTML5 Viewers SDK to create your own video viewers.

See [Dynamic Media Viewers Reference Guide](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html?lang=sv-SE).

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

## Stöd för flera bildtexter och ljudspår för video i Dynamic Media{#about-msma}

Med funktioner för flera bildtexter och ljudspår i Dynamic Media kan du enkelt lägga till flera ljudspår. Du kan också lägga till flera bildtextfiler med antingen dina egna `.vtt`-filer (Video Text Track) eller AI-genererade bildtextfiler. AI-genererade bildtexter i Dynamic Media är utformade för att förbättra videons tillgänglighet och engagemang genom att automatiskt generera korrekta och synkroniserade undertexter. Den här tekniken använder avancerade AI-algoritmer för att transkribera talat innehåll till text, som sedan visas som bildtexter på videon. Några viktiga funktioner i den här tekniken är:

* **Automatisk transkription:** AI-systemet transkriberar talade ord till text i realtid, vilket säkerställer att bildtexter genereras snabbt och korrekt.
* **Flerspråksstöd:** Bildtexter kan levereras automatiskt på mer än 60 språk, vilket gör det enklare att nå en global publik.
* **Förbättrad tillgänglighet:** Genom att tillhandahålla beskrivningar blir videoklipp mer tillgängliga för tittare som är döva eller hörselskadade, eller personer som föredrar att titta på videoklipp med ljudet avaktiverat.
* **Förbättrat engagemang:** Bildtexter kan hjälpa till att bevara läsarens uppmärksamhet och förbättra förståelsen, särskilt i högljudda miljöer eller när tittarens modersmål skiljer sig från videons språk.

Dessa funktioner gör AI-baserade bildtexter till ett värdefullt verktyg för innehållsskapare som vill förbättra sitt videomaterial och göra det mer tillgängligt och engagerande.

![Fliken Bildtexter och ljudspår i Dynamic Media tillsammans med en tabell som visar överförda VTT-bildtextfiler och överförda MP3-ljudspårsfiler för en video.](/help/assets/dynamic-media/assets/msma-caption-audiotracks-tab2.png)

Några av användningsområdena för att lägga till flera bildtexter och ljudspår i den primära videon är bland annat följande:

| Typ | Använd skiftläge |
|--- |--- |
| **Bildtexter** | Stöd för flera språk |
|  | Beskrivande text för tillgänglighet |
| **Ljudspår** | Stöd för flera språk |
|  | Kommentarspår |
|  | Beskrivande ljud |

Alla [videoformat som stöds i Dynamic Media](/help/assets/file-format-support.md) och alla videovisningsprogram för Dynamic Media - utom i visningsprogrammet för Dynamic Media *Video_360* - stöds för användning med flera bildtexter och ljudspår.

### Lägga till flera bildtexter och ljudspår i videon {#add-msma}

Innan du lägger till flera bildtexter och ljudspår i videon måste du kontrollera att du redan har följande på plats:

* Dynamic Media är konfigurerat i en AEM-miljö.
* En [dynamisk medievideoprofil används i mappen där videoklippen har importerats](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

Tillagda bildtexter stöds med formaten WebVTT och Adobe VTT. Dessutom stöds tillagda ljudspårsfiler med MP3-format.

>[!IMPORTANT]
>
>För videofilmer som har överförts *före* och som aktiverar stöd för flera bildtexter/ljudspår eller AI-genererade bildtexter på ditt Dynamic Media-konto [måste du bearbeta dem på nytt](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). Detta steg säkerställer att dessa videor kan använda flera funktioner för beskrivning/ljudspår och AI-genererad bildtext. Efter ombearbetningen fortsätter URL-adresserna för video att fungera och spelas upp som vanligt.

**Så här lägger du till flera bildtexter och ljudspår i videon:**

1. [Överför din primära video till en mapp](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) som redan har tilldelats en videoprofil.
1. Navigera till den överförda videoresursen som du vill lägga till flera bildtexter och ljudspår.
1. Välj videoresursen i resursurvalsläget, antingen från ![Visa kortikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (kortvy) eller ![Visa listikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (listvy).
1. Klicka på ![Info-ikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Egenskaper i verktygsfältet.
   ![Markerad videoresurs med bockmarkering över videominiatyrbild och Visa egenskaper markerade i verktygsfältet.](/help/assets/dynamic-media/assets/msma-selectedasset-propertiesbutton.png)*Markerad videoresurs i kortvyn.*
1. Välj fliken **[!UICONTROL Captions & Audio Tracks]** på videons egenskapssida.

   >[!TIP]
   >Om du inte ser fliken **[!UICONTROL Captions & Audio Tracks]** betyder det något av två:
   >
   >* Mappen där den valda videon finns har ingen tilldelad videoprofil. I så fall, se [Använda en videoprofil i mappen](/help/assets/dynamic-media/video-profiles.md#applying-video-profiles-to-specific-folders)
   >* Eller så måste Dynamic Media bearbeta videon igen. I så fall ska du läsa [Bearbeta dynamiska medieresurser igen i en mapp](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).
   >
   >När du har slutfört någon av ovanstående åtgärder går du tillbaka till dessa steg.

   ![Fliken Bildtexter och ljudspår på sidan Egenskaper.](/help/assets/dynamic-media/assets/msma-audiotracks.png)
   *Fliken Bildtexter och ljudspår på videons egenskapssida.*

1. Så här lägger du till ett eller flera ljudspår i en video:
   1. Välj **[!UICONTROL Upload Audio Tracks]**.
   1. Navigera till och markera en eller flera .mp3-filer och öppna dem.
   1. För att ljudspår ska kunna visas i popup-listan **[!UICONTROL Select audio or caption]** i mediespelaren måste du lägga till nödvändig information om varje ljudspårsfil. Om du gör det ser du till att alla ljudspår visas på rätt sätt och är tillgängliga. Klicka på ikonen ![Rita](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg) till höger om namnet på en ljudspårsfil. Ange följande obligatoriska information i dialogrutan **Redigera ljudspår**:

      | Metadata för ljudspår | Beskrivning |
      |--- |--- |
      | Filnamn | Standardfilnamnet härleds från det ursprungliga filnamnet. Filnamnet kan bara ändras under överföring och kan inte ändras senare. Teckenkraven för filnamn är desamma som för AEM Assets.<br>Samma filnamn kan inte användas för ytterligare ljudspårfiler eller bildtextfiler. |
      | Språk | Välj rätt språk för ljudspåret. |
      | Typ | Välj vilken typ av ljudspår du använder.<br>**Original** - Ljudspåret som ursprungligen var kopplat till videon och representerades som `[Original]` i etiketten med språket `English` markerat som standard. **[!UICONTROL Label]** och **[!UICONTROL Language]** kan ändras i dialogrutan **[!UICONTROL Edit Audio Track]**, men standardvärdet är de ursprungliga värdena om den primära videon bearbetas om.<br>**Standard** - Ett tilläggsljudspår för ett annat språk än det ursprungliga språket.<br>**Ljudbeskrivning** - Ett ljudspår som även innehåller en beskrivande berättarröst för icke-verbala åtgärder och gester i videon, vilket gör innehållet mer tillgängligt för personer med nedsatt syn. |
      | Etikett | Den text som visas som ljudspårets namn i popup-listan **[!UICONTROL Select audio or caption]** i mediespelaren. Etiketten är det kunden ser och motsvarar ett ljudspår. Exempel: `English [Original]`. Etiketten för ljud som är kopplat till en video är som standard `[Original]`. |

      Om det behövs kan du ändra eller redigera metadata för ljudspåret senare. När videon publiceras återspeglas dessa uppgifter på offentliga URL:er i publicerade videor.

   1. Klicka på **[!UICONTROL Save]** i den övre högra hörnet av sidan i listrutan **[!UICONTROL Save & Close]**.
   1. Gör något av följande:
      * Upprepa den här processen för varje ljudspårsfil som du överför.
      * Fortsätt till nästa steg om du vill lägga till bildtexter i en video.

1. Om du vill lägga till en eller flera beskrivningsfiler till en video väljer du vilket av följande användningsfall som passar ditt scenario bäst:

   |  | Använd skiftläge | Alternativet Skapa beskrivning som ska användas |
   | --- | --- | --- |
   | **Alternativ 1** | Jag har mina egna bildtextfiler som finns på de språk jag vill använda.<br>Se **Alternativ 1** nedan. | **[!UICONTROL Upload Files]** |
   | **Alternativ 2** | Jag vill att AI ska generera bildtextfiler på flera språk.<br>Se **Alternativ 2** nedan. | **[!UICONTROL Convert audio tracks]** |
   | **Alternativ 3** | Texten i en bildtextfil (`.vtt`) måste korrigeras, överföras igen för att ersätta den gamla `.vtt`-filen och sedan få AI att översätta den korrigerade filen.<br>Se **Alternativ 3** nedan. | **[!UICONTROL Translate caption]** |

   ![Alternativ för att skapa bildtexter.](/help/assets/dynamic-media/assets/msma-createcaption.png)
   *Listrutan Skapa beskrivning innehåller tre alternativ: Överför filer, Konvertera ljudspår och Översätt bildtext.*

+++**Alternativ 1:** *Jag har egna bildtextfiler som finns på de språk som jag vill använda* (**[!UICONTROL Upload Files]** alternativ)

   1. Klicka på **[!UICONTROL Create Caption]** > **[!UICONTROL Upload files]** uppe till höger på sidan.
   1. Navigera till och markera en eller flera av dina befintliga `.vtt`-filer och öppna dem.
   1. För att bildtexter ska kunna visas i mediespelaren måste du *lägga till den nödvändiga informationen om* varje *bildtextfil som du överför.* Klicka på ikonen ![Rita](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg) till höger om namnet på en bildtextfil. Ange följande obligatoriska information om filen i dialogrutan **Redigera beskrivning**:

      | Bildtextmetadata | Beskrivning |
      |--- |--- |
      | Filnamn | Standardfilnamnet härleds från det ursprungliga filnamnet. Filnamnet kan bara ändras under överföring och kan inte ändras senare. Teckenkraven för filnamn är desamma som för AEM Assets.<br>Samma filnamn kan inte användas för ytterligare bildtextfiler och ljudspårsfiler. |
      | Språk | Välj språk för bildtexten. När en bildtextfil har bearbetats går det inte att redigera det här språkfältet (nedtonat) |
      | Typ | Välj den typ av bildtext som du använder.<br>**Underrubrik** - Bildtexten som visas med videon som översätter eller transkriberar dialogrutan.<br>**Bildtext** - Bildtexten innehåller bakgrundsljud, talardifferentiering och andra relevanta detaljer, tillsammans med dialog eller transkription, vilket förbättrar tillgängligheten för personer som är döva eller hörselskadade. |
      | Etikett | Den text som visas för bildtextens namn i popup-listan **[!UICONTROL Select audio or caption]** i mediespelaren. Etiketten är det som kunden ser och som motsvarar ett underrubrik- eller bildtextspår. Exempel: `English (CC)`. |

      Om det behövs kan du ändra eller redigera bildtextens metadata senare. När videon publiceras återspeglas dessa uppgifter på offentliga URL:er i publicerade videor.

   1. Klicka på **[!UICONTROL Save]** i den övre högra hörnet av sidan i listrutan **[!UICONTROL Save & Close]**. Filerna överförs och metadatabearbetningen börjar, vilket visas i kolumnen **Status** i gränssnittet.

      >[!NOTE]
      >
      >Beroende på inställningarna för cachning för instansen kan metadatabearbetningen ta flera minuter innan den visas i förhandsgranskningen och i publicerade URL:er.

   1. Om du valde **[!UICONTROL Save & Close]** i föregående steg kan du fortfarande visa bearbetningsstatusen för de överförda filerna i stället för att välja **[!UICONTROL Save]**. Se [Visa livscykelstatus för överförda beskrivnings- och ljudspårsfiler](#lifecycle-status-video).
   1. Fortsätt till steg 8.

+++

+++**Alternativ 2:** *Jag vill att AI ska generera mina bildtextfiler på flera språk* (**[!UICONTROL Convert audio tracks]** alternativ)

   1. Klicka **[!UICONTROL Create Caption]** > **[!UICONTROL Convert audio tracks]** i sidans övre högra hörn.

      ![Dialogrutan Konvertera ljudspår.](/help/assets/dynamic-media/assets/msma-convertaudiotracks.png)
      *I dialogrutan Konvertera ljudspår används AI för att generera bildtextfiler på flera språk.*

   1. Ange följande alternativ i dialogrutan **Konvertera ljudspår**:

      | Alternativ | Beskrivning |
      |--- |--- |
      | Ljudspår som ska konverteras | Klicka på ikonen ![Knivrängning nedåt](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) och välj sedan den överförda ljudspårsfilen som du vill att bildtexter ska skapas från med AI. |
      | Utdataspråk | Klicka på ikonen ![Knivrängning nedåt](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) och välj sedan ett eller flera språk som du vill att bildtextfilen ska visas på.<br>Klicka på ikonen ![Stäng](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg) om du vill ta bort ett valt språk.<br>Under videouppspelning visas en lista med språk i mediespelaren i den ordning som du väljer dem här. |

   1. Klicka på **[!UICONTROL Done]**.
   1. Klicka på **[!UICONTROL Save]** i den övre högra hörnet av sidan i listrutan **[!UICONTROL Save & Close]**.
   1. Klicka på fliken **[!UICONTROL Captions & Audio tracks]** igen. En eller flera bildtextfiler skapas och bearbetningen börjar, vilket visas i kolumnen **Status** i gränssnittet. Se även [Visa livscykelstatus för överförda beskrivnings- och ljudspårsfiler](#lifecycle-status-video).

      >[!NOTE]
      >
      >Beroende på inställningarna för cachning för instansen kan metadatabearbetningen ta flera minuter innan den visas i förhandsgranskningen och i publicerade URL:er.

   1. (Valfritt) Klicka på ikonen ![Rita](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg) till höger om namnet på en bildtextfil. I dialogrutan **Redigera beskrivning** kan du redigera följande information om filen:

      | Bildtextmetadata | Beskrivning |
      | --- | --- |
      | Typ | Välj den typ av bildtext som du använder.<br>**Underrubrik** - Bildtexten som visas med videon som översätter eller transkriberar dialogrutan.<br>**Bildtext** - Bildtexten innehåller bakgrundsljud och talardifferentiering. Det innehåller även annan relevant information tillsammans med översättningen eller transkriberingen av dialogrutan. Detta gör innehållet mer tillgängligt för personer som är döva eller hörda. |
      | Etikett | Den text som visas för bildtextens namn i popup-listan **[!UICONTROL Select audio or caption]** i mediespelaren. Etiketten är det som kunden ser och som motsvarar ett underrubrik- eller bildtextspår. Exempel: `English (CC)`. |

      Du kan ändra eller redigera vissa bildtextmetadata senare om det behövs. När videon publiceras återspeglas dessa metadatadetaljer i offentliga URL:er i publicerade videor.
   1. Fortsätt till steg 8.

+++

+++**Alternativ 3:** *Text i en bildtextfil (`.vtt`) måste korrigeras, överföras igen för att ersätta den gamla `.vtt`-filen och sedan låta AI översätta den korrigerade filen* (**[!UICONTROL Translate captions]** alternativ)

   1. Klicka på **[!UICONTROL Create Caption]** > **[!UICONTROL Translate captions]**. Det här alternativet är tillgängligt om en eller flera bildtextfiler redan har lagts till och bearbetats.

      ![Dialogrutan Översätt beskrivningar.](/help/assets/dynamic-media/assets/msma-translate-captions.png)
      *I dialogrutan Översätt bildtexter kan du använda en befintlig bildtextfil för att generera nya bildtextfiler på flera språk.*

   1. Ange följande alternativ i dialogrutan **Översätt beskrivningar**:

      | Alternativ | Beskrivning |
      |--- |--- |
      | Bildtext som ska översättas | Klicka på ikonen ![Knivrängning nedåt](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) och välj sedan en bildtextfil som du vill att bildtexterna ska genereras med hjälp av AI. |
      | Utdataspråk | Klicka på ikonen ![Knivrängning nedåt](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) och välj sedan ett eller flera språk som du vill att bildtextfilen ska visas på.<br>Klicka på ikonen ![Stäng](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg) om du vill ta bort ett valt språk.<br>Under videouppspelning visas en lista med språk i mediespelaren i den ordning som du väljer dem här. |

   1. Klicka på **[!UICONTROL Done]**.
   1. Klicka på **[!UICONTROL Save]** i den övre högra hörnet av sidan i listrutan **[!UICONTROL Save & Close]**.
   1. Klicka på fliken **[!UICONTROL Captions & Audio tracks]** igen. En eller flera bildtextfiler skapas och bearbetningen börjar, vilket visas i kolumnen **Status** i gränssnittet. Se även [Visa livscykelstatus för överförda beskrivnings- och ljudspårsfiler](#lifecycle-status-video).

      >[!NOTE]
      >
      >Beroende på inställningarna för cachning för instansen kan metadatabearbetningen ta flera minuter innan den visas i förhandsgranskningen och i publicerade URL:er.

   1. (Valfritt) Klicka på ikonen ![Rita](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg) till höger om namnet på en bildtextfil. I dialogrutan **Redigera beskrivning** kan du redigera följande information om filen:

      | Bildtextmetadata | Beskrivning |
      | --- | --- |
      | Typ | Välj den typ av bildtext som du använder.<br>**Underrubrik** - Bildtexten som visas med videon som översätter eller transkriberar dialogrutan.<br>**Bildtext** - Bildtexten innehåller även bakgrundsljud, talardifferentiering. Det innehåller även annan relevant information tillsammans med översättningen eller transkriberingen av dialogrutan. Detta gör innehållet mer tillgängligt för personer som är döva eller hörda. |
      | Etikett | Den text som visas för bildtextens namn i popup-listan **[!UICONTROL Select audio or caption]** i mediespelaren. Etiketten är det som kunden ser och som motsvarar ett underrubrik- eller bildtextspår. Exempel: `English (CC)`. |

      Du kan ändra eller redigera vissa bildtextmetadata senare om det behövs. När videon publiceras återspeglas dessa metadatadetaljer i offentliga URL:er i publicerade videor.

   1. Fortsätt till steg 8.

+++

1. (Valfritt) Förhandsgranska videon innan du publicerar för att kontrollera att beskrivningarna och ljudet fungerar som förväntat. Se [Förhandsgranska en video som har flera bildtexter och ljudspår](#preview-video-audio-subtitle).
1. Publicera videon. Se [Publicera resurser](publishing-dynamicmedia-assets.md).

#### Lägga till beskrivnings- och ljudspårsfiler i en video som redan är publicerad

När du har överfört ytterligare beskrivnings- eller ljudspårsfiler till en publicerad video får de här filerna statusen `Processed` när de har förberetts. Du kan sedan förhandsgranska videon i Dynamic Media för att se eller höra de nya filerna.

Efter förhandsgranskningen måste du *publicera* videon igen för att de nya bildtextfilerna eller ljudspårsfilerna ska kunna publiceras. Efter publiceringen blir beskrivningarna eller ljudet tillgängliga med den offentliga Dynamic Media-URL:en.

>[!NOTE]
>
>Baserat på cachelagringsinställningarna för din instans kan metadatauppdateringar ta flera minuter innan de visas i förhandsgranskningen och i publicerade URL:er.

Om du har konfigurerat Dynamic Media för omedelbar publicering utlöses en publicering av videon omedelbart när ytterligare bildtext- eller ljudfiler överförs efter att bildtext- eller ljudfiler har överförts.

>[!CAUTION]
>
>När du överför bildtextfiler eller ljudfiler till en video som antingen är publicerad eller opublicerad, tas filerna bort om du [*bearbetar om*](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets) videon. Endast videons ursprungliga ljud förblir intakt. I så fall måste du ladda upp bildtextfilerna och ljudspårsfilerna till videon igen.

#### Lägga till flera bildtexter i en video som har en befintlig URL med bildtextmodifierare

Dynamic Media har stöd för att lägga till en enda bildtext med video via en URL-modifierare. Se [Lägga till bildtexter i videon](#adding-captions-to-video).

Ändringar av flera bildtexter har företräde framför en bildtext som har lagts till med en URL-modifierare för publicerade videor.

**Så här lägger du till flera bildtexter i en video som har en befintlig URL med bildtextmodifierare:**

1. Överför bildtextfilen som redan har lagts till som modifierare till videon, så att du kan hantera filen explicit.
1. Överför eventuella ytterligare bildtextfiler.
1. Publicera videon som vanligt.
Den befintliga URL:en med bildtextmodifieraren kan nu läsa in flera bildtexter.

### Visa livscykelstatus för överförda beskrivnings- och ljudspårsfiler {#lifecycle-status-video}

Du kan följa livscykelstatusen för alla beskrivnings- eller ljudspårsfiler som överförts till den primära videon. Det kan du göra på fliken **Bildtexter och ljudspår** i **Egenskaper**.

**Så här visar du livscykelstatusen för en video:**

1. Navigera till den videoresurs vars livscykelstatus du vill visa.
1. Välj videoresursen i resursurvalsläget, antingen från ![Visa kortikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (kortvy) eller ![Visa listikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (listvy).
1. Klicka på ![Info-ikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Egenskaper i verktygsfältet.
1. Välj fliken **[!UICONTROL Captions & Audio Tracks]** på sidan **Egenskaper**.
1. Observera status för varje bildtext eller ljudfil i kolumnen **[!UICONTROL Status]**.

| Status för beskrivningar och ljudspår | Beskrivning |
| --- | --- |
| Bearbetar | När en ny beskrivnings- eller ljudspårsfil läggs till och sparas, försätts den i tillståndet&quot;Bearbetar&quot;. Dynamic Media bearbetar filen genom att bifoga strömningsmanifestet till den primära videon. |
| Behandlad | När bearbetningen är klar visas beskrivnings- eller ljudspårsfilen, eller det ursprungliga ljudspåret som är associerat med den primära videon, i läget Behandlad. Du kan förhandsgranska beskrivnings- och ljudspårsfiler som visas som &quot;Behandlad&quot; *innan* du publicerar videon live. |
| Publicerad | Ett publicerat läge representerar ett läge som liknar publicerat för en primär video. Assets publiceras när den primära videon publiceras och är tillgänglig på den offentliga Dynamic Media-URL:en. |
| Misslyckades | Ett &quot;Misslyckat&quot;-läge betyder att bearbetningen av en beskrivnings- eller ljudspårsfil inte slutfördes. Ta bort beskrivnings- eller ljudspårsfilen och överför igen. |
| Opublicerad | När en publicerad primär video avpubliceras explicit avpubliceras även eventuella beskrivnings- eller ljudspårsfiler som du har lagt till i videon. |


### Ange standardljud för en video som har flera ljudspår

Som standard anges videons ursprungliga ljud som standardljud som ska spelas upp.

Alla överförda ljudspårsfiler kan dock anges som standardljud som spelas upp när en video har lästs in i visningsprogrammet. I egenskapsgränssnittet, under fliken **Bildtexter och ljudspår**, används etiketten `Default` till höger om ljudspårsfilen för videouppspelning.

>[!NOTE]
>
>Uppspelningen av standardljud kan också bero på vad som är inställt i följande webbläsare:
>
>* Chrome - Det standardljud som ställs in i videon spelas upp.
>* Safari - Om standardspråket är inställt i Safari spelas ljudet upp med det angivna standardspråket, om tillgängligt med videons manifest. I annat fall spelas det standardljud som är inställt som en del av en videos egenskaper upp.

**Så här anger du standardljud för en video som har flera ljudspår:**

1. Navigera till den videoresurs vars standardljudspår du vill ställa in.
1. Välj videoresursen i resursurvalsläget, antingen från ![Visa kortikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (kortvy) eller ![Visa listikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (listvy).
1. Klicka på ![Info-ikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Egenskaper i verktygsfältet.
1. Välj fliken **[!UICONTROL Captions & Audio Tracks]** på sidan Egenskaper.
1. Under rubriken **Ljudspår** väljer du den ljudspårsfil som du vill ange som videons standard.
1. Klicka på ![Ljudikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Audio_18_N.svg) **[!UICONTROL Set as default]**.
1. Klicka på **[!UICONTROL Replace]** i dialogrutan **Ange som standard**.

   ![Rubriken Ljudspår med namnet på den valda ljudspårsfilen och markerad&quot;Ange som standard&quot;-knapp.](/help/assets/dynamic-media/assets/msma-defaultaudiotrack.png)*Anger standardljudspåret för en video.*

1. Klicka på **[!UICONTROL Save & Close]** i det övre högra hörnet.
1. Publicera videon. Se [Publicera resurser](publishing-dynamicmedia-assets.md).

### Förhandsgranska en video med flera bildtexter och ljudspår {#preview-video-audio-subtitle}

När bildtextfiler och ljudspårsfiler har överförts till en video och bearbetats kan du använda videovisningsprogrammet för dynamiska media för att förhandsgranska alla olika spår. Om du gör det blir det lättare att se hur videon ser ut och låter som den är för kunderna, och du kan vara säker på att den beter sig som förväntat.

När du är nöjd med videon kan du [publicera den](publishing-dynamicmedia-assets.md) på något av följande sätt.

Se [Bädda in video- eller bildvisningsprogrammet på en webbsida](/help/assets/dynamic-media/embed-code.md).
Se [Länka URL:er till ditt webbprogram](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Den URL-baserade länkningsmetoden är inte möjlig om det interaktiva innehållet har länkar till relativa URL-adresser, särskilt länkar till Experience Manager Sites-sidor.
Se [Lägg till Assets för dynamiska media på sidor](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

>[!NOTE]
>
>På standardfliken Experience Manager Preview visas inte flera beskrivnings- och ljudspår. Orsaken är att dessa spår är kopplade till Dynamic Media och bara kan ses med förhandsvisning i Dynamic Media Viewer.

**Så här förhandsgranskar du en video som har flera bildtexter och ljudspår:**

1. I **[!UICONTROL Assets]** navigerar du till en befintlig video som du har lagt till flera bildtexter och ljudspår.
1. Klicka på videoresursen för att öppna den i förhandsgranskningsläge.
1. Klicka på ikonen ![Till vänster (höger)](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg) ![ikon ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) och välj sedan **[!UICONTROL Viewers]** på förhandsvisningssidan, nära det övre vänstra hörnet på sidan.

   ![Listruta med alternativet Visare.](/help/assets/dynamic-media/assets/msma-selectviewers.png)

1. I närheten av det övre vänstra hörnet av sidan klickar du på ikonen ![Till vänster om skenet](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg) Visare ![Knivrängen nedåt](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) och väljer sedan ett visningsprogram som du vill använda för videoförhandsvisningen.

1. Klicka på ikonen för pratbubblan i det nedre högra hörnet av sidan och välj sedan ljudet eller underrubriken/bildtexten som du vill höra eller se, eller båda.

   ![Popup-listan Ljud och beskrivningar i videoredigeraren.](/help/assets/dynamic-media/assets/msma-selectaudiosubtitle.png)*Simulering av en användare som väljer ljud och bildtext för videouppspelning.*

1. Klicka på ![PLay-ikonen](https://spectrum.adobe.com/static/icons/workflow_22/Smock_PlayCircle_22_N.svg) för att påbörja uppspelningen.
Om du vill kan du klicka på ikonen ![Maximera](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Maximize_22_N.svg) för att maximera visningsfönstret.
Lägg märke till knapparna **[!UICONTROL URL]** och **[!UICONTROL Embed]** i sidans nedre vänstra hörn. Använd de här knapparna för att [länka videons URL till ditt webbprogram](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) eller för att [bädda in videon på en webbsida](/help/assets/dynamic-media/embed-code.md).
1. Klicka på **[!UICONTROL Close]** i det övre högra hörnet på förhandsgranskningssidan.

### Ta bort beskrivnings- eller ljudspårsfiler från en video

Du kan ta bort beskrivnings- eller ljudspårfiler från en video. Borttagning av publicerade bildtexter eller ljudspårsfiler återspeglas automatiskt i videons publicerade URL.

Det går inte att ta bort det ursprungliga ljudspåret som har extraherats från en primär video.

**Så här tar du bort beskrivnings- eller ljudspårsfiler från en video:**

1. Navigera till den videoresurs vars standardljudspår du vill ställa in.
1. Välj videoresursen i resursurvalsläget, antingen från ![Visa kortikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (kortvy) eller ![Visa listikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (listvy).
1. Klicka på ![Info-ikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Egenskaper i verktygsfältet.
1. Välj fliken **[!UICONTROL Captions & Audio Tracks]** på sidan Egenskaper.
1. Gör något av följande:

   * Bildtexter - Under rubriken **Bildtexter** markerar du en eller flera bildtextfiler som du vill ta bort från videon och klickar sedan på ikonen ![Ta bort](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Delete_22_N.svg) **[!UICONTROL Delete]** .
   * Ljudspår - Under rubriken **Ljudspår** markerar du en eller flera ljudspårsfiler som du vill ta bort från videon och klickar sedan på ikonen ![Ta bort](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Delete_22_N.svg) **[!UICONTROL Delete]** .

1. Klicka på **[!UICONTROL OK]** i dialogrutan Ta bort.
1. Publicera videon.

### Hämta beskrivnings- eller ljudspårsfiler som har överförts till en video

Du kan hämta alla beskrivnings- och ljudspårsfiler som du har överfört för en video. Du kan antingen hämta alla markerade filer som `.zip` eller skapa en separat hämtningsmapp för varje fil.

Det går inte att hämta det ursprungliga ljudspåret som har extraherats från en primär videofil.

**Användningsfall:** Det kan vara nödvändigt att hämta en bildtextfil om du upptäcker ett fel i en `.vtt`-fil. Hämta bara den felaktiga `.vtt`-filen, öppna den i en vanlig textredigerare och gör dina korrigeringar. När du har sparat filen `.vtt` överför du den igen. Använd sedan alternativet **[!UICONTROL Translate Captions]** för att översätta den korrigerade `.vtt`-filen igen.

**Så här hämtar du beskrivnings- eller ljudspårsfiler som har överförts till en video:**

1. Navigera till den videoresurs vars standardljudspår du vill ställa in.
1. Välj videoresursen i resursurvalsläget, antingen från ![Visa kortikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (kortvy) eller ![Visa listikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (listvy).
1. Klicka på ![Info-ikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Egenskaper i verktygsfältet.
1. Välj fliken **[!UICONTROL Captions & Audio Tracks]** på sidan **Egenskaper**.
1. Gör något av följande:

   * Bildtexter - Under rubriken **Bildtexter** väljer du en eller flera bildtextfiler som du vill hämta från videon och klickar sedan på ![Ikonen Hämta](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Download_22_N.svg) **[!UICONTROL Download]** .
   * Ljudspår - Under rubriken **Ljudspår** markerar du en eller flera ljudspårsfiler som du vill hämta från videon och klickar sedan på ![Ikonen Hämta](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Download_22_N.svg) **[!UICONTROL Download]** .

1. Ange följande alternativ i dialogrutan Hämta:

   | Hämtningsalternativ | Beskrivning |
   |--- |--- |
   | Spara som | Använd standardfilnamnet som anges i textfältet Spara som eller ange ett eget namn. |
   | Skapa en separat mapp för varje resurs | Skapa en mapp för varje bildtextfil eller ljudspårsfil som du valde för hämtning. |
   | E-post | Använd ditt standardprogram för e-post för att skicka ZIP-filen till en angiven e-postadress. |
   | Assets | Anger antalet filer som du hämtar och den sammanlagda storleken för alla markerade filer. Om du avmarkerar det här alternativet tonas knappen **[!UICONTROL Download]** ned (inaktiveras), vilket förhindrar att du hämtar någon fil. |
   | Återgivningar | En återgivning är en alternativ version eller en förhandsvisning av originalfilen, vanligtvis en mindre eller lågupplöst version. Om den visas som 0 B betyder det troligtvis att det inte finns någon alternativ version tillgänglig eller att den är för liten för att registrera en storlek. |

1. Välj **[!UICONTROL Download]**.
1. Publicera videon. Se [Publicera resurser](publishing-dynamicmedia-assets.md).

<!-- ## About AI-generated captions for videos in Dynamic Media

AI-powered captions in Dynamic Media are designed to enhance video accessibility and engagement by automatically generating accurate and synchronized subtitles. This technology uses advanced AI algorithms to transcribe spoken content into text, which is then displayed as captions on the video. Here are some key features.

* **Automatic Transcription:** The AI system transcribes spoken words from an existing audio file into text in real-time, ensuring that captions are generated quickly and accurately.
* **Multilingual Support:** It supports more than 60 languages, making it easier to reach a global audience. You can even translate your existing captions to different languages.
* **Enhanced Accessibility:** By providing captions, videos become more accessible to viewers who are deaf or hard of hearing, as well as those who prefer to watch videos with the sound off.
* **Improved Engagement:** Captions can help retain viewer attention and improve comprehension, especially in noisy environments or when the viewer's native language is different from the video's language.

These features in Dynamic Media make AI-powered video aptions a valuable tool for content creators looking to enhance their video content's accessibility and engagement. -->

## Lägga till undertexter till video {#adding-captions-to-video}

Du kan utöka räckvidden för dina videor till globala marknader genom att lägga till undertexter till enskilda videor eller till adaptiva videouppsättningar. Genom att lägga till undertextning slipper du att duplicera ljudet eller att du behöver använda inbyggda högtalare för att spela in ljudet igen för varje språk. Videon spelas upp på det språk den spelades in på. Undertexter på främmande språk visas så att personer på olika språk fortfarande kan förstå ljuddelen.

Undertexter ger också bättre tillgänglighet för personer som är döva eller hörselskadade.

>[!NOTE]
>
>Den videospelare som du använder måste ha stöd för visning av undertexter.

Se även [Hjälpmedel i dynamiska media](/help/assets/dynamic-media/accessibility-dm.md).

Dynamic Media kan konvertera bildtextfiler till JSON-format (JavaScript Object Notation). Den här konverteringen innebär att du kan bädda in JSON-texten på en webbsida som en dold men fullständig utskrift av videon. Sökmotorer kan sedan crawla/indexera innehållet för att göra videoklippen lättare att hitta och ge kunderna mer information om videoinnehållet.

Mer information om hur du använder JSON-funktionen i en URL finns i [Serverar statiskt (icke-bildinnehåll)](https://experienceleague.adobe.com/sv/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents#image-serving-api).

**Så här lägger du till bildtexter i en video:**

1. Använd ett program eller en tjänst från tredje part för att skapa videobeskrivningsfilen.

   Kontrollera att filen du skapar följer standarden WebVTT (Web Video Text Track). Bildtextens filnamnstillägg är `.vtt`. Du kan läsa mer om bildtextstandarden WebVTT.

   Se [WebVTT: Textspår för webbvideo ](https://w3c.github.io/webvtt/).

   Det finns många webbplatser som innehåller både kostnadsfria och premiumverktyg och tjänster som du kan använda för att skapa WebVTT-bildtextfiler utanför Dynamic Media.

Följ instruktionerna på skärmen för att skapa och spara WebVTT-filen. När du är klar kopierar du bildtextfilens innehåll och klistrar in det i en vanlig textredigerare och sparar det med filnamnstillägget VTT.

>[!NOTE]
>
>Om du vill ha globalt stöd för videobeskrivningar på flera språk kräver WebVTT-standarden att du skapar separata `.vtt`-filer och anropar varje språk som du vill ha stöd för.

Vanligtvis vill du ge bildtexten `.vtt` samma namn som videofilen och bifoga den med språkinställningen -EN, -FR eller -DE. På så sätt kan det hjälpa dig att automatisera genereringen av video-URL:er med ditt befintliga WCM-system.

1. Överför WebVTT-bildtextfilen till DAM i Experience Manager.
1. Navigera till den *publicerade* videoresursen för att associera den med bildtextfilen som du överförde.

   Kom ihåg att URL:er endast går att kopiera *efter* att du har *publicerat* resurserna.

   Se [Publicera resurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

1. Gör något av följande:

   * Klicka på knappen **[!UICONTROL URL]** om du vill visa en videoklipp. I dialogrutan URL-adress markerar och kopierar du URL-adressen till Urklipp och sedan förbi URL-adressen till en enkel textredigerare. Lägg till den kopierade URL:en för videon med följande syntax:

     `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

     Observera `,1` i slutet av bildtextssökvägen. Omedelbart efter VTT-filnamnstillägget i sökvägen kan du aktivera (aktivera) eller inaktivera (inaktivera) den stängda bildtextsknappen i videospelarfältet genom att ställa in på `,1` respektive `,0`.

   * Klicka på **[!UICONTROL Embed Code]** om du vill visa en inbäddad videoupplevelse. I dialogrutan Bädda in kod markerar och kopierar du den inbäddade koden till Urklipp och klistrar sedan in koden i en enkel textredigerare. Lägg till den kopierade inbäddningskoden med följande syntax:

     `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

     Observera `,1` i slutet av bildtextssökvägen. Omedelbart efter VTT-filnamnstillägget i sökvägen kan du aktivera (aktivera) eller inaktivera (inaktivera) den stängda bildtextsknappen i videospelarfältet genom att ställa in på `,1` respektive `,0`.

## Lägga till kapitelmarkörer i video {#adding-chapter-markers-to-video}

Du kan göra dina videoklipp i långa format enklare att titta på och navigera genom att lägga till kapitelmarkörer i enstaka videor eller i adaptiva videouppsättningar. När en användare spelar upp videon kan han/hon välja kapitelmarkörer på tidslinjen (kallas även videobandspelare). De kan enkelt navigera till sin intressepunkt eller direkt gå över till nytt innehåll, ny utbildning och nya demonstrationer.

>[!NOTE]
>
>Den videospelare som används måste ha stöd för kapitelmarkörer. Dynamiska mediespelare har stöd för kapitelmarkörer, men det är inte säkert att tredjepartsvideospelare används.

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

I exemplet ovan är `Chapter 1` referensidentifieraren och valfri. Referenstiden på `00:00:000 --> 01:04:364` anger kapitlets start- och sluttid i `00:00:000`-format. De sista tre siffrorna är millisekunder och kan lämnas som `000` om det behövs. Kapiteltiteln för `The bicycle store behind it all` är den faktiska beskrivningen av kapitlets innehåll. Referensidentifieraren, startreferenstiden och kapiteltiteln visas alla i ett popup-fönster i videospelaren när en användare håller muspekaren över en visuell referenspunkt i tidslinjen.

Eftersom du använder ett videovisningsprogram för HTML5 bör du kontrollera att den kapitelfil du skapar följer standarden WebVTT (Web Video Text Tracks). Kapitelfiltillägget är `.vtt`. Du kan läsa mer om bildtextstandarden WebVTT.

Se [WebVTT: Textspår för webbvideo ](https://w3c.github.io/webvtt/).

**Så här lägger du till kapitelmarkörer i en video:**

1. Spara filen `.vtt` i UTF8-kodning så att du slipper problem med teckenåtergivning i kapiteltiteltexten.

   Vanligtvis vill du ge den kapitelbaserade VTT-filen samma namn som videofilen och bifoga den med kapitel. På så sätt kan det hjälpa dig att automatisera genereringen av video-URL:er med ditt befintliga WCM-system.
1. Överför din WebVTT-kapitelfil till Experience Manager.

   Se [Överför resurser](/help/assets/manage-digital-assets.md#uploading-assets).

1. Gör något av följande:

   <table>
     <tbody>
      <tr>
       <td>För en popup-video som visar</td>
       <td>
       <ol>
       <li>Navigera till den <i>publicerade </i>videoresursen om du vill associera den med den överförda kapitelfilen. Kom ihåg att URL:er endast går att kopiera <i>efter</i> att du har <i>publicerat</i> resurserna. Se <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">Publicera Assets.</a></li>
       <li>Välj sedan <strong>Visare</strong> i listrutan.</li>
       <li>Markera namnet på visningsförinställningen för videon i den vänstra listen. En förhandsgranskning av videon öppnas på en separat sida.</li>
       <li>Klicka på knappen <strong>URL</strong> längst ned i den vänstra listen.</li>
       <li>I dialogrutan URL-adress markerar och kopierar du URL-adressen till Urklipp och sedan förbi URL-adressen till en enkel textredigerare.</li>
       <li>Lägg till den kopierade URL:en för videon med följande syntax så att du kan associera den med den kopierade URL:en till din kapitelfil:<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>Om du vill visa en inbäddad video kan du <br /> </td>
       <td>
       <ol>
       <li>Navigera till den <i>publicerade </i>videoresursen om du vill associera den med den överförda kapitelfilen. Kom ihåg att URL:er endast går att kopiera <i>efter</i> att du har <i>publicerat</i> resurserna. Se <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">Publicera Assets.</a></li>
       <li>Välj sedan <strong>Visare</strong> i listrutan.</li>
       <li>Markera namnet på visningsförinställningen för videon i den vänstra listen. En förhandsgranskning av videon öppnas på en separat sida.</li>
       <li>Välj <strong>Bädda in</strong> längst ned i den vänstra listen.</li>
       <li>I dialogrutan Bädda in kod markerar och kopierar du hela koden till Urklipp och klistrar sedan in den i en enkel textredigerare.</li>
       <li>Lägg till videofilens inbäddningskod med följande syntax så att du kan koppla den till den kopierade URL:en till din kapitelfil:<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt>"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>


## Om videominiatyrer {#about-video-thumbnails}

En videominiatyr är en version med reducerad storlek av en videobildruta eller en bildresurs som representerar videon för kunden. Miniatyrbilden bör uppmuntra kunden att välja videon.

Alla videofilmer i Experience Manager måste ha en tillhörande miniatyrbild. Som standard används den första bildrutan som miniatyrbild när du överför en video till Experience Manager. Du kan dock anpassa miniatyrbilden för varumärke eller visuell sökning. När du anpassar en videominiatyr kan du spela upp videon och pausa den bildruta som du vill använda. Du kan också välja en bildresurs som du redan har överfört och *publicerat* i din Digital Asset Manager.

När miniatyrbilden ändras för en video hoppas miniatyrbildsgenerering över med hjälp av Asset Compute Service när videon bearbetas om.

Möjligheten att anpassa en videominiatyr är endast tillgänglig efter att du har tillämpat en videoprofil på den mapp där videon finns.

### Lägga till en anpassad videominiatyr {#adding-a-custom-video-thumbnail}

1. Kontrollera att du redan har gjort följande:

   * Skapade en mapp för dina videoresurser.
   * [En videoprofil har använts i mappen](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

   * [Dina videofilmer har överförts till mappen](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).


1. Navigera till en överförd videoresurs vars miniatyrbild du vill ändra.
1. Välj videoresursen i resursurvalsläget, antingen från ![Visa kortikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (kortvy) eller ![Visa listikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (listvy).
1. Klicka på ![Info-ikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Egenskaper i verktygsfältet.
1. Klicka på **[!UICONTROL Change Thumbnail]** på videons egenskapssida.
1. Gör något av följande i dialogrutan Ändra miniatyrbild:

   * Så här använder du en bildruta från videon som ny miniatyrbild:

      * Klicka på fliken **[!UICONTROL Select Frame from video]** i verktygsfältet.
      * Klicka på ikonen ![Spela upp](https://spectrum.adobe.com/static/icons/workflow_22/Smock_PlayCircle_22_N.svg).
      * Klicka på ikonen ![Paus](https://spectrum.adobe.com/static/icons/workflow_22/Smock_PauseCircle_22_N.svg) i bildrutan som du vill hämta som videons nya miniatyrbild.

   * Så här använder du en bildresurs som ny miniatyrbild:

      * Klicka på fliken **[!UICONTROL Select Thumbnail from Assets]** i verktygsfältet.
      * Klicka på knappen **[!UICONTROL Select thumbnail]**.
      * Navigera till en tidigare överförd och publicerad bildresurs som du vill använda. Storleken på resursen ändras automatiskt så att den fungerar som en miniatyrbild för videon.
      * Markera bildresursen och klicka sedan på **[!UICONTROL Select]**.

1. Klicka på **[!UICONTROL Save Change]** i dialogrutan Ändra miniatyrbild.
1. Klicka på **[!UICONTROL Save & Close]** eller **[!UICONTROL Save]** i det övre högra hörnet på videons egenskapssida.



<!--

## About video thumbnails in Dynamic Media Hybrid mode{#about-video-thumbnails-in-dynamic-media-hybrid-mode}

You can choose from one of ten thumbnail images automatically generated by Dynamic Media to add to your video. The video player displays your selected thumbnail when a video asset is used with the Dynamic Media component in the authoring environment of Experience Manager Sites, Experience Manager Mobile, or Experience Manager Screens. The thumbnail serves as a static picture that best represents the contents of your entire video and further encourages users to select the Play button.

Based on the total time of the video, Dynamic Media captures ten (default) thumbnail images at 1%, 11%, 21%, 31%, 41%, 51%, 61%, 71%, 81%, and 91% into the video. The ten thumbnails persist meaning that if you decide to choose a different thumbnail later on, you do not need to regenerate the series. You preview the ten thumbnail images and then select the one you want to use with your video. If you want to change to default you can use CRXDE Lite to configure the time interval that thumbnail images are generated. For example, if you only wanted to generate a series of four evenly spaced thumbnail images from your video, you can configure the interval time at 24%, 49%, 74%, and 99%.

Ideally, you can add a video thumbnail anytime after you upload your video but before you publish the video on your website.

If you prefer, you can choose to upload a custom thumbnail to represent your video instead of using a thumbnail generated by Dynamic Media. For example, you could create a custom thumbnail image that has the title of your video, an eye-catching opening image, or a very specific image captured from your video. The custom video thumbnail image that you upload should have a maximum resolution of 1280 &times; 720 pixels (minimum width of 640 pixels) and be no larger than 2MB.

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

   If you configured new default time intervals, or you uploaded a new video to replace the existing video, you need to have Dynamic Media regenerate the thumbnails.

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

1. On the lower-right panel, in the Properties tab, double-select `thumbnailtime`.
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

## Ändra URL för dynamiska media för dynamiska medieresurser

Färdiga visningsprogram kan spela upp videor som bearbetats i Dynamic Media. Du kan även spela upp dem genom att gå direkt till manifest-URL:erna och använda dina egna anpassade visningsprogram. Nedan följer API:t för hämtning av manifest-URL:er för en video.

### Om API:t getVideoManifestURI

API:t `getVideoManifestURI` exponeras via c`q-scene7-api:com.day.cq.dam.scene7.api` och kan användas för att generera följande manifest-URL:er:

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
| `resource` | Resursen som motsvarar videon som Dynamic Media har kapslat. |
| `manifestType` | Kan vara antingen `ManifestType.DASH` eller `ManifestType.HLS` |
| `onlyIfPublished` | Ange som true om manifest-URI bara genereras om den är publicerad och tillgänglig på leveransnivån. |

Om du vill hämta manifest-URL:er för videoklipp med metoden ovan lägger du till en [videokodningsprofil](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) i en mapp för överföring av videoklipp. Dynamic Media bearbetar dessa videoklipp baserat på kodningarna i den videokodningsfil som tilldelats mappen. Nu kan du anropa ovanstående API för att hämta manifest-URL:er för de överförda videoklippen.

### Felscenarier

API:t returnerar null om det finns fel. Undantag loggas i Experience Manager felloggar. Alla sådana loggade fel börjar med `Could not generate Video Manifest URI`. Följande scenarier kan orsaka sådana fel:

* En `IllegalArgumentException` loggas för något av följande:

   * Parametern `resource` som skickades är null.
   * Den `resource`-parameter som skickades är inte en video.
   * Parametern `manifestType` som skickades är null.
   * Parametern `onlyIfPublished` skickas som true, men videon publiceras inte.
   * Videon har inte importerats med en adaptiv videouppsättning från dynamiska media.

* `IOException` loggas när det uppstår ett problem med att ansluta till Dynamic Media.
* `UnsupportedOperationException` loggas när en `manifestType`-parameter som skickas är `ManifestType.DASH`, medan videon inte har bearbetats i DASH-format.

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


<!-- REMOVED THE FOLLOWING TOPIC AS PER EMAIL FROM RIYA MIDHA, WEDNESDAY, MARCH 5, 2025; TOPIC IS OBSOLETE/NO LONGER NEEDED BECAUSE THE FEATURES IT DESCRIBES ARE NOW GA WITHIN THE SOFTWARE

## Enable DASH, multi-captions and multi-audio tracks, and AI-generated captions support on your Dynamic Media account {#enable-dash}

You can enable support in Dynamic Media for:

* DASH
* Multi-captions and audio tracks
* AI-generated captions (Limited Availability)

By creating and submitting an Adobe Customer Support case. 

Enabling any of the above three capabilities, enables all of them. So, if you only want DASH enabled, you are actually enabling all three capabilities listed above.  

| Capability | Description |
| --- | --- |
| DASH | DASH (Digital Adaptive Streaming over HTTP) is the international standard for video streaming and is widely adopted across different video viewers. When DASH is enabled on your account, you get the option to choose from either DASH or HLS for adaptive video streaming. Or, you can opt for both with automatic switching between players when **[!UICONTROL auto]** is selected as the playback type in the Viewer preset.<br>Some key benefits from enabling DASH on your account include the following:<ul><li>Package DASH stream video for adaptive bitrate streaming. This method leads to higher efficiency of delivery. Adaptive streaming ensures the best viewing experience for your customers.</li><li>Browser optimized streaming with Dynamic Media players switches between HLS and DASH streaming to ensure the best quality of service. The video player auto-switches to HLS when a Safari browser is used.</li><li>You can configure your preferred streaming method (HLS or DASH) by editing the video viewer preset.</li><li>Optimized video encoding ensures that no additional storage is used while enabling DASH capability. A single set of video encodings is created for both HLS and DASH to optimize video storage costs.</li><li>Helps make video delivery more accessible for your customers.</li><li>Get the streaming URL by way of APIs, too.</li></ul>|
| Multi-captions and audio tracks | You can benefit from having multiple caption and audio track support automatically enabled. After enablement, all subsequent videos that you upload are processed with a new backend architecture that includes support for adding multiple caption and audio tracks to your videos. |
| AI-generated captions (Limited Availability) | Create captions for your videos powered by AI. Using AI, it creates the transcript of the video and converts it into captions. Even the timeline is defined, too. |

>[!IMPORTANT]
>
>Any videos that you uploaded *before* enabling multiple caption and audio track support on your Dynamic Media account, [must be reprocessed](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). This video reprocessing step is necessary so that multiple caption and audio track capability is available to them. The video URLs continue to work and play as usual, after reprocessing.

**To enable DASH, multi-captions and multi-audio tracks, and AI-generated captions support on your Dynamic Media account:** 

1. [Use the Admin Console to start the creation of a new support case](https://helpx.adobe.com/se/enterprise/using/support-for-experience-cloud.html).
1. To create a support case, follow the instructions while ensuring you provide the following information:

    * Primary contact name, email, phone.
    * Your Cloud Services environment (program ID and environment ID).
    * Your Dynamic Media company account name.
    * Your Dynamic Media region: North America (NA), Asia-Pacific (APAC), or Europe-Middle East-Asia (EMEA).
    * Specify that you want DASH, multi-captions and multi-audio tracks, and AI-generated captions (Limited Availability) support enabled on your Dynamic Media account, on AEM as a Cloud Service.
   
1. Adobe Customer Support adds you to the Customer Wait List based on the order in which requests are submitted.
1. When Adobe is ready to handle your request, Customer Support contacts you to coordinate and set a target date for enablement.
1. Adobe Customer Support notifies you after completion.
1. Now, do one or more of the following:

    * Create your [video viewer preset](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset) as usual.
    * Create your [video profile](/help/assets/dynamic-media/video-profiles.md) as usual.
    * [Add multiple captions and audio tracks](#add-msma) to your video. -->


<!-- 
## About multiple caption and audio track support for videos in Dynamic Media{#about-msma}

With multiple caption and audio track capability in Dynamic Media, you can easily add multiple captions and audio tracks to a primary video. This capability means that your videos are accessible to a global audience. You can customize a single, published primary video to a global audience in multiple languages and adhere with accessibility guidelines for different geographical regions. Authors can also manage the captions and audio tracks from a single tab in the user interface.

   ![Captions and audio tracks tab in Dynamic Media along with a table showing uploaded .VTT caption files and uploaded .MP3 audio track files for a video.](/help/assets/dynamic-media/assets/msma-caption-audiotracks-tab2.png)


Some of the use cases to consider for adding multiple captions and audio tracks to your primary video include the following:

| Type | Use case | 
| --- | --- |
| Captions | Multiple language support<br>Descriptive text for accessibility |
| Audio tracks | Multiple language support<br>Commentary tracks<br>Descriptive audio |


All [video formats supported in Dynamic Media](/help/assets/file-format-support.md) and all Dynamic Media video viewers-except the Dynamic Media Video_360 viewer-are supported for use with multiple captions and audio tracks.

Multi-caption and multi-audio track capability is available for your Dynamic Media account by way of a feature toggle that must be enabled (turned on) by Adobe Customer Support.

### Add multiple captions and audio tracks to your video {#add-msma}

Before you add multiple caption and audio tracks to your video, be sure you already have the following in-place:

* Dynamic Media is set up in an AEM environment.
* A [Dynamic Media Video profile is applied to the folder where your videos are ingested](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).
* [Multi-caption, and multi-audio track is enabled on your Dynamic Media account](/help/assets/dynamic-media/video.md#enable-dash).

Added captions and captions are supported with WebVTT and Adobe VTT formats. And, added audio track files are supported with MP3 format.

>[!IMPORTANT]
>
>Any videos that you uploaded before enabling multiple caption and audio track support on your Dynamic Media account, [must be reprocessed](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). This video reprocessing step is necessary so that multiple caption and audio track capability is available to them. The video URLs continue to work and play as usual, after reprocessing.

**To add multiple captions and audio tracks to your video:**

1. [Upload your primary video to a folder](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) that already has a video profile assigned to it.
1. Navigate to the uploaded video asset that you want to add multiple caption and audio tracks.
1. In asset selection mode, either from the List View or the Card View, select the video asset.
1. On the toolbar, select the Properties icon (a circle with an "i" in it). 

   ![Asset properties button.](/help/assets/dynamic-media/assets/msma-selectedasset-propertiesbutton.png)*Selected video asset in Card View.*

1. On the video's Properties page, select the **[!UICONTROL Captions & Audio Tracks]** tab.


   >[!TIP]
   >If you do not see the [!UICONTROL Captions & Audio Tracks] tab, it means either one of two things:
   >* The folder in which the selected video resides does not have a video profile assigned to it. In which case, see [Apply a video profile to the folder](/help/assets/dynamic-media/video-profiles.md#applying-video-profiles-to-specific-folders)
   >* Or, Dynamic Media must reprocess the video. In which case, see [Reprocess Dynamic Media assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

    When you have completed either one of the above tasks, return to these steps.

   ![Asset properties](/help/assets/dynamic-media/assets/msma-audiotracks.png)*Captions and audio tracks tab on the video's Properties page.*

1. (Optional) To add one or more caption files to a video, do the following:

    * Select **[!UICONTROL Upload Captions]**.
    * Navigate to, and select, one or more `.vtt` (Video Text Tracks) files and open them.
    * For captions to be visible on the media player, you must add required details (metadata) about each caption file that you uploaded. Select the pencil icon to the right of a caption file name. In the Edit Caption dialog box, enter the following required details about the file, then select **[!UICONTROL Save]**. Repeat this process for each caption file that you uploaded:


    | Caption metadata | Description | 
    | --- | --- | 
    Filename | The default filename is derived from the original filename. The filename can be changed only while uploading and cannot be changed later. Filename character requirements are the same as for AEM Assets.<br>The same filename cannot be used for additional caption files and audio track files. |
    | Language | Select the language of the caption. |
    | Type | Select the type of caption that you are using.<br>**Subtitle** - The caption text displayed with the video that translates or transcribes the dialogue.<br>**Caption** - The caption text includes background noises and speaker identification. It also includes other relevant details alongside the translation or transcription of dialogue. This functionality makes the content more accessible to individuals who are deaf or hard of hearing. |
    | Label | The text that is displayed for the caption's name in the **[!UICONTROL Select audio or caption]** pop-up list in the media player. The label is what a customer sees that corresponds to a subtitle or caption track. For example, English (CC). |

    You can change or edit caption metadata later, if necessary. When the video is published, these details are reflected on public URLs in published videos.

1. (Optional) To add one or more audio tracks to a video, do the following:

    * Select **[!UICONTROL Upload Audio Tracks]**.
    * Navigate to, and select, one or more .mp3 files and open them.
    * To make audio tracks visible in the **[!UICONTROL Select audio or caption]** pop-up list on the media player, add the required details for each audio track file. Ensure you include all necessary information for proper display. Select the pencil icon to the right of an audio track file name. In the Edit Audio Track dialog box, enter the following required details, then select **[!UICONTROL Save]**. Repeat this process for each audio track file that you uploaded.

    | Audio Track metadata | Description |
    | --- | --- |
    | Filename | The default filename is derived from the original filename. The filename can be changed only while uploading and cannot be changed later. Filename character requirements are the same as for AEM Assets.<br>The same filename cannot be used for additional audio track files or caption files.| 
    | Language | Select the language of the audio track. |
    | Type | Select the type of audio track that you are using.<br>**Original** - The audio track originally attached to the video and represented as `[Original]` in the label with English language selected by default. While **[!UICONTROL Label]** and **[!UICONTROL Language]** can be changed in the **[!UICONTROL Edit Audio Track]** dialog box, it defaults to the original values if the primary video is reprocessed.<br>**Standard** - An add-on audio track for a language other than the original.<br>**Audio description** - An audio track that also includes a descriptive narration of non-verbal actions and gestures in the video, making content more accessible for individuals who are visually impaired. |
    | Label | The text that is displayed as the audio track's name in the **[!UICONTROL Select audio or caption]** pop-up list in the media player. The label is what a customer sees that corresponds to an audio track. For example, `English [Original]`. The label of audio attached to a video is set to `[Original]` by default. |

    You can change or edit this audio track metadata later, if necessary. When the video is published, these details are reflected on public URLs in published videos.

1. In the upper-right corner of the page, from the **[!UICONTROL Save & Close]** drop-down list, select **[!UICONTROL Save]**. The files are uploaded and metadata processing begins, as seen in the Status column of the interface.

    >[!NOTE]
    >
    >Based on the caching settings of your instance, the metadata processing can take several minutes before it is reflected in preview and in published URLs.

1. (Optional) If you selected **[!UICONTROL Save & Close]** in the previous step, instead of selecting **[!UICONTROL Save]**, you can still view the processing status of the uploaded files. See [View the lifecycle status of uploaded caption and audio track files](/help/assets/dynamic-media/video.md#lifecycle-status-video).

1. (Optional) Preview the video before publishing to ensure the captions and audio work as expected. See [Preview a video that has multiple captions and audio tracks](/help/assets/dynamic-media/video.md#preview-video-audio-subtitle).

1. Publish the video. See [Publish assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md). -->






