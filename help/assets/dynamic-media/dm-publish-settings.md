---
title: Konfigurera Dynamic Media Publish Setup för Image Server
description: Lär dig hur du konfigurerar Publishing i Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: b0891095-e4a9-4dd5-8dfd-a576bc47d082
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '3238'
ht-degree: 0%

---

# Konfigurera Dynamic Media Publish Setup för Image Server

<!-- hide: yes
hidefromtoc: yes -->

Konfigurera Dynamic Media Publish Setup är endast tillgängligt om:

* Du har en *befintlig* **[!UICONTROL Dynamic Media Configuration]** (in **[!UICONTROL Cloud Services]**) i Adobe Experience Manager as a Cloud Service. Se [Skapa en Dynamic Media-konfiguration i Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
* Du är systemadministratör för Experience Manager med administratörsbehörighet.

Dynamic Media Publish Setup är avsedd för erfarna webbplatsutvecklare och programmerare. Adobe Dynamic Media rekommenderar användare som ändrar dessa publiceringsinställningar att känna till Adobe Dynamic Media, HTTP-protokollets standarder och konventioner samt grundläggande bildbehandlingsteknik.

På sidan Dynamic Media Publish Setup (Publiceringsinställningar) anges standardinställningar som avgör hur resurser levereras från Adobe Dynamic Media-servrar till webbplatser eller program. Om ingen inställning har angetts levererar Adobe Dynamic Media-servern en resurs enligt en standardinställning som har konfigurerats på Dynamic Media publiceringskonfiguration.

Se även [Valfritt - Konfigurera och konfigurera Dynamic Media-inställningar](/help/assets/dynamic-media/config-dm.md#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings) för fler valfria konfigurationsuppgifter.

>[!NOTE]
>
>Vill du uppgradera från Dynamic Media Classic till Dynamic Media på Adobe Experience Manager as a Cloud Service? The [Allmänna inställningar](/help/assets/dynamic-media/dm-general-settings.md) sidan och sidan Publiceringsinställningar i Dynamic Media är förifyllda med värdena från ditt Dynamic Media Classic-konto. Undantag är alla värden som anges under **[!UICONTROL Default upload options]** på sidan Allmänna inställningar. Dessa värden finns redan i Experience Manager. Alla ändringar du gör under **[!UICONTROL Default upload options]**, på vilken av de fem flikarna som helst, via användargränssnittet i Experience Manager, visas i Dynamic Media, inte i Dynamic Media Classic. Alla andra inställningar och värden i dialogrutan [Allmänna inställningar](/help/assets/dynamic-media/dm-general-settings.md) och sidan Publiceringsinställningar finns mellan Dynamic Media Classic och Dynamic Media på Experience Manager.

**Så här konfigurerar du Dynamic Media Publish Setup Image Server:**

1. I läget Experience Manager Author väljer du logotypen Experience Manager för att komma åt den globala navigeringskonsolen.
1. Välj ikonen Verktyg i den vänstra listen och gå sedan till **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media Publish Setup]**.
1. Ange din Image Server - publiceringskontext på sidan Image Server och använd sedan de fem flikarna för att konfigurera standardpubliceringsinställningarna.

   * [Bildserver](#image-server)
      * [Säkerhet](#security-tab) tab
      * [Kataloghantering](#catalog-management-tab) tab
      * [Attribut för begäran](#request-attributes-tab) tab
      * [Vanliga miniatyrattribut](#common-thumbnail-attributes-tab) tab
      * [Färghanteringsattribut](#color-management-attributes-tab) tab

   ![Dynamic Media Publish Setup page](/help/assets/assets-dm/dm-publish-setup.png)
   *Dynamic Media Publish Setup-sidan med **[!UICONTROL Request Attributes]**har valts.*<br><br>

1. När du är klar väljer du **[!UICONTROL Save]**.

## Bildserver {#image-server}

Sidan Image Server används för att ange standardinställningar för att leverera bilder från bildservrar. Inställningarna är tillgängliga i fem kategorier

| Publicera kontext | Beskrivning |
| --- | --- |
| Bildredigering | Anger kontext för publiceringsinställningar. |
| Testa bildvisning | Anger kontexten för testning av publiceringsinställningar.<br>Endast för nya Dynamic Media-konton är standardvärdet **[!UICONTROL Client address]** fältet är inställt på `127.0.0.1` automatiskt.<br>Se [Testa resurser innan du gör dem offentliga](#test-assets-before-making-public). |

### Fliken Säkerhet {#security-tab}

**[!UICONTROL Client address]** - Gör att du kan ange en eller flera IP-adresser eller IP-adressintervall. När det anges avvisas begäranden till den här bildkatalogen som kommer från en klient till en IP-adress som inte finns med i listan. Den här regeln gäller både för leverans av bilder och återgivna bilder.

![Fliken Säkerhet ](/help/assets/assets-dm/dm-ipallowlist.png)<br>*Fliken Säkerhet som visar IP-fältet&quot;allow&quot;.*


### Fliken Kataloghantering {#catalog-management-tab}

**[!UICONTROL Rule set definition file path]** - Anger filen som innehåller regeluppsättningsdefinitionerna för bildkatalogen.

Se även [RuleSetFile](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) i referenshandboken för Dynamic Media Viewer.

>[!NOTE]
>
>Om ditt Dynamic Media Classic-konto redan har en **[!UICONTROL Rule set definition file path]** markerat (enligt **[!UICONTROL Setup]** > **[!UICONTROL Application]** > **[!UICONTROL Publish setup]**, under **[!UICONTROL Catalog Management]** (grupp), ditt Dynamic Media-konto på Experience Manager hämtar filen från Dynamic Media Classic. Filen lagras och blir tillgänglig i det här fältet när du öppnar **[!UICONTROL Dynamic Media Publish Setup]** för första gången.

### Fliken Attribut för begäran {#request-attributes-tab}

De här inställningarna gäller standardutseendet för bilder.

| Inställning | Beskrivning |
| --- | --- |
| **[!UICONTROL Reply image size limit]** | Obligatoriskt.<br>Endast för nya Dynamic Media-konton anges standardstorleksgränsen automatiskt till Bredd: `3000` och höjd: `3000` för båda **[!UICONTROL Image Serving]** och **[!UICONTROL Test Image Serving]**.<br>Anger den maximala svarsbildens bredd och höjd som returneras till klienten. Servern returnerar ett fel om en begäran orsakar en svarsbild vars bredd, höjd eller båda är större än den här inställningen.<br>Se även [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Request obfuscation mode]** | Aktivera om du vill att base64-kodning ska användas på giltiga begäranden.<br>Se även [RequestObfuscation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Request locking mode]** | Aktivera om du vill att ett enkelt hash-lås ska inkluderas i begäranden.<br>Se även [RequestLock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Default Request Attributes]** | |
| **[!UICONTROL Default image file suffix]** | Obligatoriskt.<br>Standarddatafiltillägg som läggs till i fältvärdena katalogsökväg och MaskPath om sökvägen inte innehåller något filsuffix.<br>Se även [DefaultExt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Default font face name]** | Anger vilket teckensnitt som ska användas om inget teckensnitt anges i en textlagerbegäran. Om du anger det måste det vara ett giltigt teckensnittsnamnvärde i teckensnittskartan för den här bildkatalogen eller i teckensnittskartan för standardkatalogen.<br>Se även [DefaultFont](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Default image]** | Tillhandahåller en standardbild som returneras som svar på en begäran där den begärda bilden inte hittas.<br>Se även [DefaultImage](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) i referenshandboken för Dynamic Media Viewer.<br>**ANMÄRKNING**: Om ditt Dynamic Media Classic-konto redan har en **[!UICONTROL Default image]** markerat (enligt **[!UICONTROL Setup]** > **[!UICONTROL Application]** > **[!UICONTROL Publish setup]**, under **[!UICONTROL Default Request Attributes]** (grupp), ditt Dynamic Media-konto på Experience Manager hämtar filen från Dynamic Media Classic. Filen lagras och blir tillgänglig i det här fältet när du öppnar **[!UICONTROL Dynamic Media Publish Setup]** för första gången. |
| **[!UICONTROL Default image mode]** | När skjutreglaget är aktiverat (skjutreglage till höger) visas **[!UICONTROL Default image]** ersätter varje lager som saknas i källbilden med standardbilden och returnerar den sammansatta bilden som vanligt. När skjutreglaget är inaktiverat (skjutreglage till vänster) ersätter standardbilden hela den sammansatta bilden, även om den saknade bilden bara är ett av flera lager.<br>Se även [DefaultImageMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Default view size]** | Obligatoriskt.<br>Endast för nya Dynamic Media-konton anges standardvisningsstorleken automatiskt till Bredd: `1280` och höjd: `1280` för båda **[!UICONTROL Image Serving]** och **[!UICONTROL Test Image Serving]**.<br>Servern begränsar svarsbilderna till att inte vara större än den här bredden och höjden om begäran inte uttryckligen anger visningsstorleken med `wid=`, `hei=`, eller `scl=`.<br>Se även [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Default thumbnail size]** | Obligatoriskt.<br>Används i stället för attribut **[!UICONTROL Default view size]** för miniatyrbegäranden (`req=tmb`). Servern begränsar svarsbilderna så att de inte är större än den här bredden och höjden, om en miniatyrbildsbegäran (`req=tmb`) anger inte storleken explicit med `wid=`, `hei=`, eller `scl=`.<br>Se även [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Default background color]** | Anger RGB som används för att fylla i områden i en svarsbild som inte innehåller verkliga bilddata.<br>Se även [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL JPEG Encoding Attributes]** |  |
| **[!UICONTROL Quality]** | <br>Anger standardattributen för svarsbilder i JPEG.<br>Endast för nya Dynamic Media-konton finns **[!UICONTROL Quality]** standardvärdet anges automatiskt till `80` för båda **[!UICONTROL Image Serving]** och **[!UICONTROL Test Image Serving]**.<br>Det här fältet definieras i intervallet 1-100.<br>Se även [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Chromatically downsampling]** | Aktivera eller inaktivera kromatisk nedsampling som används av JPEG-kodare. |
| **[!UICONTROL Default resampling mode]** | Anger de standardattribut för omsampling och interpolation som ska användas för skalning av bilddata. Använd när `resMode` har inte angetts i en begäran.<br>Endast för nya Dynamic Media-konton är standardläget för omsampling automatiskt inställt på `Sharp2` för båda **[!UICONTROL Image Serving]** och **[!UICONTROL Test Image Serving]**.<br>Se även [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) i referenshandboken för Dynamic Media Viewer. |

### fliken Vanliga miniatyrattribut {#common-thumbnail-attributes-tab}

De här inställningarna gäller för miniatyrbildernas standardutseende och -justering.

| Inställning | Beskrivning |
| --- | --- |
| **[!UICONTROL Default background color for thumbnail]** | Anger det RGB-värde som används för att fylla i en miniatyrbilds utdataområde som inte innehåller verkliga bilddata. Används endast för miniatyrbildsbegäranden (`req=tmb`) och när **[!UICONTROL Default Thumbnail Type]** inställningen är inställd på **[!UICONTROL Fit]** eller **[!UICONTROL Texture]**.<br>Se även [ThumbBkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Horizontal alignment]** | Anger den vågräta justeringen för miniatyrbilden i svarsbildsrektangeln som anges av `wid=` och `hei=` värden.<br>Används endast för miniatyrbildsbegäranden (`req=tmb`) och när **[!UICONTROL Default Thumbnail Type]** inställningen är inställd på **[!UICONTROL Fit]**.<br>Det finns tre horisontella justeringar att välja mellan: **[!UICONTROL Center alignment]**, **[!UICONTROL Left alignment]** och **[!UICONTROL Right alignment]**.<br>Se även [ThumbHorizAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Vertical alignment]** | Anger den lodräta justeringen för miniatyrbilden i svarsbildsrektangeln som anges av `wid=` och `hei=` värden. Används endast för miniatyrbildsbegäranden (`req=tmb`) och när **[!UICONTROL Default Thumbnail Type]** inställningen är inställd på **[!UICONTROL Fit]**.<br>Det finns tre lodräta justeringar att välja mellan: **[!UICONTROL Top alignment]**, **[!UICONTROL Center alignment]** och **[!UICONTROL Bottom alignment]**.<br>Se även [ThumbVertAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Default cache time to live]** | Anger ett standardutgångsintervall i timmar om en viss katalogpost inte innehåller ett giltigt värde för katalogförfallotid. Ange till `-1` för att markera som aldrig förfaller. <br>Se även [Förfaller](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Default thumbnail type]** | Anger ett standardvärde för miniatyrbildstypen om en viss katalogpost inte innehåller ett giltigt katalogvärde för ThumbType. Används endast för miniatyrbildsbegäranden (`req=tmb`).<br>Det finns tre typer av miniatyrer att välja bland: **[!UICONTROL Crop]**, **[!UICONTROL Fit]** och **[!UICONTROL Texture]**.<br>Se även [ThumbType](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Default thumbnail resolution]** | Anger ett standardvärde för upplösningen av miniatyrbildobjektet om en viss katalogpost inte innehåller ett giltigt ThumbRes-katalogvärde. Används endast för miniatyrbildsbegäranden (`req=tmb`) och när **[!UICONTROL Default thumbnail type]** inställningen är inställd på **[!UICONTROL Texture]**.<br>Se även [ThumbRes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) i referenshandboken för Dynamic Media Viewer. |

### Fliken Färghanteringsattribut {#color-management-attributes-tab}

De här inställningarna avgör vilka ICC-färgprofiler som används för bilder.

**Återgivningsmetod för färgkonvertering**
En färgkonverteringsåtergivningsmetod tillåter åsidosättning av standardåtergivningsmetoden för arbetsprofilerna för att bestämma hur källfärgerna justeras. Används när:

1. En av standardprofilerna för ICC är målfärgrymden för en färgkonvertering.
1. En utdataenhet (skrivare eller bildskärm) kännetecknas av den här profilen.
1. Den angivna återgivningsmetoden gäller även för den här profilen.

Olika återgivningsmetoder använder olika regler för att bestämma hur källfärgerna justeras.

Se även [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) i referenshandboken för Dynamic Media Viewer.

>[!NOTE]
>
>I allmänhet är det bäst att använda standardåtergivningsmetoden för den valda färginställningen, som har testats av Adobe för att uppfylla branschstandarder. Om du t.ex. väljer en färginställning för Nordamerika eller Europa är standardåtergivningsmetoden för färgkonvertering **[!UICONTROL Relative Colorimetric]**. Om du väljer en färginställning för Japan är standardåtergivningsmetoden för färgkonvertering **[!UICONTROL Perceptual]**.

| Inställning | Egenskaper |
| --- | --- |
| **[!UICONTROL CMYK default color space]** | Anger namnet på ICC-färgprofilen som ska användas som arbetsprofil för CMYK-data. If **[!UICONTROL None Specified]** väljs inaktiveras färghantering för den här bildkatalogen när det gäller CMYK-källbilder. Alla CMYK-arbetsfärgrymder är enhetsberoende, vilket innebär att de baseras på faktiska kombinationer av bläck och papper. CMYK-arbetsfärgrymderna Adobe bygger på standardtryckeriet.<br> Se även [IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Gray-Scale default color space]** | Anger namnet på ICC-färgprofilen som ska användas som arbetsprofil för gråskaledata. If **[!UICONTROL None Specified]** väljs inaktiveras färghantering för den här bildkatalogen när källbilder i gråskala används.<br>Se även [IccProfileGray](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL RGB default color space]** | Anger namnet på ICC-färgprofilen som ska användas som arbetsprofil för RGB data. If **[!UICONTROL None Specified]** väljs inaktiveras färghantering för den här bildkatalogen när bilder från RGB-källor används. I allmänhet är det bäst att välja **[!UICONTROL Adobe RGB]** eller **[!UICONTROL sRGB]** i stället för profilen för en viss enhet (till exempel en bildskärmsprofil). **[!UICONTROL sRGB]** rekommenderas när du förbereder bilder för webben eller mobila enheter, eftersom färgrymden definieras för den standardbildskärm som används för att visa bilder på webben. **[!UICONTROL sRGB]** är också ett bra val när du arbetar med bilder från vanliga digitalkameror, eftersom sRGB används som standardfärgrymd i de flesta av dessa.<br>Se även [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) i referenshandboken för Dynamic Media Viewer. |
| **[!UICONTROL Color conversion rendering intent]** | **[!UICONTROL Perceptual]** - Avsikten är att bevara den visuella relationen mellan färger så att de uppfattas som naturliga för det mänskliga ögat, även om färgvärdena i sig kan ändras. Den här metoden är lämplig för fotografiska bilder med många ej tryckbara färger. Den här inställningen är standardåtergivningsmetoden för den japanska tryckeribranschen. |
|  | **[!UICONTROL Relative Colorimetric]** - Jämför de extrema färgerna i källfärgrymden med målfärgrymden och anpassar färgerna. Färger utanför färgomfånget ändras till den närmast reproducerbara färgen i målfärgrymden. Med Relativa färgvärden bevaras mer av de ursprungliga färgerna i en bild än med Perceptuell. Den här inställningen är standardåtergivningsmetoden för utskrift i Nordamerika och Europa. |
|  | **[!UICONTROL Saturation]** - Försöker producera levande färger i en bild på bekostnad av färgnoggrannheten. Den här återgivningsmetoden är lämplig för affärsgrafik som diagram och diagram där klara, mättade färger är viktigare än det exakta förhållandet mellan färger. |
|  | **[!UICONTROL Absolute Colorimetric]** - Ändrar inte färger som ligger inom målfärgomfånget. Ej tryckbara färger beskärs. Ingen skalning av färger till målvitpunkten utförs. Den här metoden syftar till att bibehålla färgnoggrannheten på bekostnad av att förhållandet mellan färger bevaras och är lämplig för korrektur för att simulera utdata från en viss enhet. Den här metoden är användbar när du vill förhandsgranska hur pappersfärgen påverkar tryckta färger. |

## Testa resurser innan du gör dem offentliga {#test-assets-before-making-public}

Säker testning hjälper er att definiera en säker testmiljö och bygga en robust affärs-till-business-lösning som bygger på en konfigurerbar uppsättning IP-adresser och intervall. Med den här funktionaliteten kan ni matcha era Adobe Dynamic Media-installationer med arkitekturen i ert innehållshantering och affärssystem.

Med Säker testning kan du förhandsgranska testversionen av webbplatsen med opublicerat innehåll.

Om du vill kan du skapa en staging-miljö i stället för att göra resurserna allmänt tillgängliga av följande skäl:

* Förhandsgranska webbplatser innan den offentliga lanseringen (testwebbplatsen).
* Tjäna resurser som kräver begränsad åtkomst, till exempel e-kataloger som visar priser i B2B-webbprogram.
* Använd material bakom en brandvägg som en del av produktinformationshanteringssystemet, kundtjänstprogrammet, utbildningswebbplatsen osv.

>[!NOTE]
>
>Säker testning påverkar inte åtkomsten till Adobe Dynamic Media Classic. Adobe Dynamic Media Classic säkerhet är konsekvent och kräver de vanliga inloggningsuppgifterna för åtkomst till Adobe Dynamic Media Classic och relaterade webbtjänster.

### Så här fungerar säkra tester {#how-test-assets-works}

De flesta företag använder internet bakom en brandvägg. Tillgång till Internet är möjlig via vissa vägar och vanligtvis via ett begränsat antal offentliga IP-adresser.

I företagsnätverket kan du räkna ut din offentliga IP-adress med webbplatser som [https://www.whatismyip.com](https://www.whatismyip.com/) eller begär den här informationen från IT-avdelningen.

Med säker testning skapar Adobe Dynamic Media en dedikerad Image Server för testmiljöer eller interna program. Alla förfrågningar till den här servern kontrollerar den ursprungliga IP-adressen. Om den inkommande begäran inte finns i den godkända listan över IP-adresser returneras ett felsvar. Adobe Dynamic Media företagsadministratör konfigurerar den godkända listan över IP-adresser för företagets säkra testmiljö.

Eftersom platsen för den ursprungliga begäran måste bekräftas, dirigeras inte trafiken för tjänsten för säker testning via ett nätverk för innehållsdistribution, t.ex. offentlig Dynamic Media Image Server-trafik. Begäranden till tjänsten för säker testning har en något högre fördröjning än de offentliga Dynamic Media Image-servrarna.

Opublicerade resurser är omedelbart tillgängliga från tjänsterna för säker testning, utan att behöva publicera. På så sätt kan du köra en förhandsvisning innan resurser publiceras på den offentliga bildservern.

>[!NOTE]
>
>Tjänster för säker testning använder katalogservern som är konfigurerad med en intern publiceringskontext. Om ditt företag är konfigurerat att publicera till Säker testning blir därför alla överförda resurser i Adobe Dynamic Media omedelbart tillgängliga på Säker testning. Den här funktionen är sann oavsett om resurserna har markerats för publicering vid överföring.

Tjänster för säker testning stöder för närvarande följande resurstyper och funktioner:

* Bilder.
* Vinjetter (renderingsserverbegäranden).
* Rendera serverförfrågningar (stöds, men måste begäras uttryckligen av kunden).
* Uppsättningar, inklusive bilduppsättningar, eCatalog, renderingsuppsättningar och medieuppsättningar.
* Adobe Dynamic Media multimedievisningsprogram som standard.
* Adobe Dynamic Media OnDemand JSP pages.
* Statiskt innehåll, till exempel PDF-filer och progressivt levererade videor.
* HTTP-videoströmning.
* Progressiv videoströmning.

Följande tillgångstyper och funktioner stöds för närvarande inte:

* Adobe Dynamic Media Classic Info- eller eCatalog-sökning
* RTMP-videoströmning
* Webb-till-tryck
* UGC-tjänster (användargenererat innehåll)

  >[!IMPORTANT]
  >
  >Från och med 1 maj 2023 är UGC-resurser i Dynamic Media tillgängliga för användning upp till 60 dagar från överföringsdatumet. Efter 60 dagar tas resurserna bort.

  >[!NOTE]
  >
  >Stöd för nya eller befintliga UGC-vektorbildresurser i Adobe Dynamic Media upphörde den 30 september 2021.

### Testa tjänsten för säker testning {#test-secure-testing-service}

Så här ser du till att tjänsten Secure Testing fungerar som förväntat:

#### Förbered ditt konto

1. Kontakta Adobe kundtjänst och begär att de aktiverar säker testning på ditt konto.
1. I Adobe Experience Manager väljer du **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media Publish Setup]**.
1. På sidan Image Server finns **[!UICONTROL Publish Context]** nedrullningsbar lista, välja **[!UICONTROL Test Image Serving]**.
1. Välj **[!UICONTROL Security]** -fliken.
1. För **[!UICONTROL Client address]** filter, markera **[!UICONTROL Add]**.
1. I **[!UICONTROL IP Address]** anger du en IP-adress.
1. I **[!UICONTROL Mask]** skriver du en nätmask.

   >[!NOTE]
   >
   >Om du lägger till mer än en IP-adress och nätmask tillåts *alla* IP-adresser för att göra tillgångsanrop, och de visas alla.

1. Gör något av följande:

   * Om du vill lägga till fler IP-adresser upprepar du de tre föregående stegen.
   * Fortsätt till nästa steg.

1. I det övre högra hörnet på sidan Image Server väljer du **[!UICONTROL Save]**.
1. Ladda upp bilderna till ditt Adobe Dynamic Media-konto.

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. Se till att vissa bilder är markerade för publicering och att andra är omarkerade och skicka sedan publiceringsjobbet.

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. Bestäm namnet på tjänsten för säker testning genom att gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media General Setting]**.
1. På **[!UICONTROL Server]** sidan, hitta servernamnet till höger om **[!UICONTROL Published Server Name]**.

Kontakta Adobe Care om servernamnet saknas eller om URL:en till inte fungerar.

#### Förbered webbplatsvarianter

Du behöver två varianter av en webbplats som länkar de publicerade och opublicerade resurserna:

* Offentlig version - Länka resurser med den traditionella URL-syntaxen för Adobe Dynamic Media.
* Mellanlagringsversion - Länka resurser med samma syntax men med namnet på platsen för säker testning.

#### Kör testerna

Utför följande tester:

1. Kontrollera om resurser är synliga inifrån företagets nätverk.

   I företagsnätverket som identifieras av det tidigare definierade IP-adressintervallet visar mellanlagringsversionen av webbplatsen alla bilder, oavsett om de är markerade för publicering eller inte. Därför kan du testa utan att oavsiktligt göra bilder tillgängliga innan du förhandsgranskar eller startar produkten.

   Bekräfta att den offentliga versionen av din webbplats visar publicerade resurser så som de har varit med Adobe Dynamic Media tidigare.

1. Verifiera att icke-publicerade resurser (dvs. omärkta för publicering) är skyddade från åtkomst från tredje part utanför företagets nätverk.

   Få åtkomst till nätverket från utsidan (till exempel från din hemdator eller via en 4G/5G-anslutning) och kontrollera sedan att den offentliga versionen av webbplatsen visar alla publicerade resurser, men inget av det opublicerade innehållet.

   Bekräfta att mellanlagringsversionen inte visar någon resurs eftersom du använder tjänsten för säker testning från en ej godkänd IP-adress.
