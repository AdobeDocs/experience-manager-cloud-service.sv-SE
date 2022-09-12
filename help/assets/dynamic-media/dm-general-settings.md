---
title: Konfigurera allmänna inställningar för Dynamic Media
description: Lär dig hur du hanterar allmänna inställningar i Dynamic Media. Du kan ange namnet på publiceringsservern och namnet på den ursprungliga servern här och ange ett alternativ för att skriva över bilder. Det finns också standardalternativ för överföring av oskarp maskering av bilder och överföringsalternativ för hur du vill bearbeta PostScript-, Adobe Photoshop-, PDF- och Adobe Illustrator-filer.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: a4d28786-cffa-42ab-98d3-90a15313e401
source-git-commit: ccd52d147b1739330c3cb5a7d1952a7e9eec71ad
workflow-type: tm+mt
source-wordcount: '2334'
ht-degree: 0%

---

# Konfigurera allmänna inställningar för Dynamic Media

<!-- hide: yes
hidefromtoc: yes -->

Konfigurerar **[!UICONTROL Dynamic Media General Settings]** är bara tillgängligt om:

* Du har en *befintlig* **[!UICONTROL Dynamic Media Configuration]** (in **[!UICONTROL Cloud Services]**) i Adobe Experience Manager as a Cloud Service. Se [Skapa en Dynamic Media-konfiguration i Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
* Du är systemadministratör för Experience Manager med administratörsbehörighet.

Allmänna inställningar i Dynamic Media är avsedda att användas av erfarna webbplatsutvecklare och programmerare. Adobe Dynamic Media rekommenderar användare som ändrar dessa publiceringsinställningar att känna till Dynamic Media om Adobe Experience Manager och grundläggande bildbehandlingsteknik.

När du skapar ett konto tillhandahåller Adobe Dynamic Media automatiskt de tilldelade servrarna för ditt företag. De här servrarna används för att skapa URL-strängar för din webbplats och dina program. Dessa URL-anrop är specifika för ditt konto.

På sidan Dynamic Media Publish Setup (Publiceringsinställningar) anges standardinställningar som avgör hur resurser levereras från Adobe Dynamic Media-servrar till webbplatser eller program. Om ingen inställning har angetts levererar Adobe Dynamic Media-servern en resurs enligt en standardinställning som har konfigurerats på Dynamic Media publiceringskonfiguration.

Se även [Valfritt - Konfigurera och konfigurera Dynamic Media-inställningar](/help/assets/dynamic-media/config-dm.md#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings) för fler valfria konfigurationsuppgifter.

>[!NOTE]
>
>Vill du uppgradera från Dynamic Media Classic till Dynamic Media på Adobe Experience Manager? Sidan Allmänna inställningar och [Publiceringsinställningar](/help/assets/dynamic-media/dm-publish-settings.md) sidan i Dynamic Media är förifylld med värdena från ditt Dynamic Media Classic-konto. Undantag är alla värden som anges under **[!UICONTROL Default upload options]** på sidan Allmänna inställningar. Dessa värden finns redan i Experience Manager. Alla ändringar du gör under **[!UICONTROL Default upload options]**, på vilken av de fem flikarna som helst, via användargränssnittet i Experience Manager, visas i Dynamic Media, inte i Dynamic Media Classic. Alla andra inställningar och värden på sidan Allmänna inställningar och på sidan [Publiceringsinställningar](/help/assets/dynamic-media/dm-publish-settings.md) mellan Dynamic Media Classic och Dynamic Media på Experience Manager.

**Så här konfigurerar du allmänna inställningar för Dynamic Media:**

1. I läget Experience Manager Author väljer du logotypen Experience Manager för att komma åt den globala navigeringskonsolen.
1. Välj ikonen Verktyg i den vänstra listen och gå sedan till **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media General Settings]**.
1. Ange din **[!UICONTROL Published Server Name]** och **[!UICONTROL Origin Server Name]** och använd sedan de fem flikarna för att konfigurera standardalternativ för överföring av bildredigering och för PostScript-, Photoshop-, PDF- och Illustrator-filer.

   * [Server](#server-general-setting)
   * [Överför till program](#upload-to-application)
   * [Bildredigering](#image-editing-tab) tab
   * [PostScript](#postscript-tab) tab
   * [Photoshop](#photoshop-tab) tab
   * [PDF](#pdf-tab) tab
   * [Illustrator](#illustrator-tab) tab

   ![Dynamic Media General Settings page](/help/assets/assets-dm/dm-general-settings.png)
   *Dynamic Media General Settings page, with the **[!UICONTROL Image Editing]**har valts.*<br><br>

1. När du är klar väljer du **[!UICONTROL Save]**.

## Server {#server-general-setting}

När du skapar ett konto tillhandahåller Adobe Dynamic Media automatiskt de tilldelade servrarna för ditt företag. De här servrarna används för att skapa URL-strängar för din webbplats och dina program. Dessa URL-anrop är specifika för ditt konto.

| Alternativ | Beskrivning |
| --- | --- |
| **[!UICONTROL Published Server Name]** | Krävs.<br>Namnet måste använda `https://` i banan.<br>Den här servern är den CDN-server (Content Deliver Network) som används i alla systemgenererade URL-anrop som är specifika för ditt konto. Ändra inte det här servernamnet om du inte har fått instruktioner om att göra det av Adobe tekniska support. |
| **[!UICONTROL Origin Server Name]** | Krävs.<br>Den här servern används endast för kvalitetstestning. Ändra inte det här servernamnet om du inte har fått instruktioner om att göra det från Adobe tekniska support. |

## Överför till program {#upload-to-application}

* **[!UICONTROL Overwrite Images]**

   Adobe Dynamic Media tillåter inte att två filer har samma namn. Varje objekts Adobe Dynamic Media-ID (bildnamn minus filnamnstillägg) måste vara unikt. På grund av den här regeln **[!UICONTROL Upload to Application]** har en överskrivning. Den exakta effekten av det här alternativet beror på det angivna alternativet Skriv över bilder som du har valt. De här alternativen anger hur ersättningsbilder överförs: om de ersätter originalbilderna eller blir dubblettbilder. Namnet på duplicerade bilder ändras med ett `-1`. Till exempel: `chair.tif` har bytt namn `chair-1.tif`. De här alternativen påverkar bilder som har överförts till en annan mapp än den ursprungliga eller bilder med ett annat filnamnstillägg än den ursprungliga, till exempel JPG, TIF eller PNG.

   >[!NOTE]
   >
   >Om du vill behålla konsekvensen med Experience Manager markerar du alternativet Skriv över bilder **[!UICONTROL Overwrite in current folder, same base name/extension]**.

   | Skriv över bilder, alternativ | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Overwrite in current folder, same base name/extension]** | *Standard* endast för nya Dynamic Media-konton.<br>Det här alternativet är den striktaste regeln för ersättning. Det kräver att du överför ersättningsbilden till samma mapp som originalbilden och att ersättningsbilden har samma filnamnstillägg som originalbilden. Om dessa krav inte uppfylls skapas en dubblett.<br>*Välj det här alternativet om du vill att Experience Manager ska vara konsekvent*. |
   | **[!UICONTROL Overwrite in current folder, same base name regardless of extension]** | Kräver att du överför ersättningsbilden till samma mapp som originalet, men filnamnstillägget kan skilja sig från originalet. Till exempel ersätter stol.tif stol.jpg. |
   | **[!UICONTROL Overwrite in any folder, same base asset name/extension]** | Kräver att ersättningsbilden har samma filnamnstillägg som den ursprungliga bilden (t.ex. måste stol.jpg ersätta stol.jpg, inte stol.tif). Du kan dock överföra ersättningsbilden till en annan mapp än den ursprungliga. Den uppdaterade bilden finns i den nya mappen; filen inte längre kan hittas på sin ursprungliga plats. |
   | **[!UICONTROL Overwrite in any folder, same base asset name regardless of extension]** | Det här alternativet är den mest omfattande ersättningsregeln. Du kan överföra en ersättningsbild till en annan mapp än den ursprungliga, överföra en fil med ett annat filnamnstillägg och ersätta den ursprungliga filen. Om originalfilen finns i en annan mapp finns ersättningsbilden i den nya mappen som den överfördes till. |

* **[!UICONTROL Preserve Crop]**

   Kontrollerar bevarande av befintliga manuella beskärningsdefinitioner.

   Se även `preserveCrop` in [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) och [ÅterbearbetaResurserJobb](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html), båda i referenshandboken för Dynamic Media Viewer.

## Standardalternativ för överföring {#default-upload-options}

### Fliken Bildredigering {#image-editing-tab}

Med det här filtret kan du finjustera en skärpefiltereffekt på den slutliga nedsamplade bilden. Det hjälper dig att styra intensiteten i effekten, radien för effekten (mätt i pixlar) och ett tröskelvärde för kontrast som ignoreras.

För effekten Oskarp mask används samma alternativ som för filtret Oskarp mask i Photoshop. Till skillnad från vad namnet antyder är Oskarp mask ett skärpefilter.

| Oskarp mask, alternativ | Beskrivning |
| --- | --- |
| **[!UICONTROL Amount]** | Krävs.<br>Styr mängden kontrast som används på kantpixlar.<br>Tänk på det som intensiteten i effekten. Den största skillnaden mellan mängdvärdena för Oskarp mask i Adobe Dynamic Media och mängdvärdena i Adobe Photoshop är att Photoshop har ett intervall på 1 till 500 %. I Adobe Dynamic Media är värdeintervallet `0.0` till `5.0`. Värdet 5.0 i Adobe Dynamic Media motsvarar 500 % i Photoshop. värdet 0,9 motsvarar 90 % och så vidare. |
| **[!UICONTROL Radius]** | Krävs.<br>Styr radien för effekten.<br>Värdeintervallet är `0` till `250`. Effekten körs på alla pixlar i en bild och strålar ut från alla pixlar i alla riktningar. Radien mäts i pixlar. Om du till exempel vill få en liknande skärpeeffekt för en bild på 2 000 x 2 000 pixlar och en bild på 500 x 500 pixlar anger du en radie på två pixlar för bilden på 2 000 x 2 000 pixlar. Ange sedan radien 1 pixel på bilden med 500 x 500 pixlar. Ett större värde används för en bild som har fler pixlar. |
| **[!UICONTROL Threshold]** | Krävs.<br>Tröskelvärde är ett kontrastintervall som ignoreras när filtret Oskarp mask används. Den här effekten är viktig så att inget &quot;brus&quot; uppstår i en bild när filtret används. Värdeintervallet är `0` - `255`, vilket är antalet steg för intensitet i en gråskalebild. `0`=svart, `128`=50% grå och `255`=vitt.<br>Ett tröskelvärde på `12` ignorerar små variationer i hudtonens ljusstyrka för att undvika att lägga till brus, men ändå ger kantkontrast till kontrastrika områden som där ögonfransar möter hud.<br>Om du har ett foto av någon annans ansikte påverkar Oskarp mask de kontrastrika delarna av bilden. Till exempel där ögonfransar och hud möts för att skapa ett tydligt kontrastområde och den utjämnade huden. Även den jämnaste huden uppvisar subtila förändringar i intensitetsvärden. Om du inte använder ett tröskelvärde framhäver filtret dessa subtila ändringar i hudpixlar. En brus och oönskad effekt skapas i sin tur medan kontrasten på ögonfransarna ökar, vilket ökar skärpan.<br>För att undvika det här problemet introduceras ett tröskelvärde som instruerar filtret att ignorera pixlar som inte förändrar kontrasten dramatiskt, som mjuk hud.<br>Lägg märke till texturen bredvid dragkedjan i zippargrafiken som visades tidigare. Bildbrus visas eftersom tröskelvärdena var för låga för att undertrycka bruset. |
| **[!UICONTROL Monochrome]** | Markera för att få bildintensiteten oskarp mask (intensitet).<br>Avmarkera alternativet om du vill skapa en oskarp mask för varje färgkomponent separat. |

Se även [Öka skärpan i bilder i Adobe Dynamic Media och på Image Server](https://experienceleague.adobe.com/docs/experience-manager-65/assets/sharpening_images.pdf?lang=en).

### PostScript-flik {#postscript-tab}

Du kan rastrera Adobe PostScript®-filer, behålla genomskinliga bakgrunder, välja en upplösning och välja en färgrymd.

Du kan använda Adobe PostScript®-filer (EPS) i Adobe Dynamic Media. I Adobe Dynamic Media finns kommandon för att konfigurera de här filerna när du överför dem.

När du överför PostScript-bildfiler (EPS) kan du formatera dem på olika sätt. Du kan rastrera filerna, behålla den genomskinliga bakgrunden, välja en upplösning och välja en färgrymd.

| PostScript, alternativ | Beskrivning |
| --- | --- |
| **[!UICONTROL Processing]** | Välj Rastrera om du vill konvertera vektorgrafik i filen till bitmappsformat. |
| **[!UICONTROL Maintain transparent background in rendered images]** | Bevarar filens genomskinlighet i bakgrunden. |
| **[!UICONTROL Resolution (pixel/inch)]** | Anger upplösningsinställningen. Den här inställningen avgör hur många pixlar som visas per tum i filen. |
| **[!UICONTROL Color space]** | ・ **[!UICONTROL Detect automatically]** - Behåller filens färgrymd.<br>・ **[!UICONTROL Force as RGB]** - Konverterar till färgmodellen RGB.<br>・ **[!UICONTROL Force as CMYK]** - Konverterar till CMYK-färgmodellen.<br>・ **[!UICONTROL Force as Grayscale]** - Konverterar till färgmodellen Gråskala. |

### Fliken Photoshop {#photoshop-tab}

Du kan skapa mallar från Adobe® Photoshop®-filer, behålla lager, ange hur lager ska namnges, extrahera text och ange hur bilder ska förankras i mallar.

| Photoshop | Beskrivning |
| --- | --- |
| **[!UICONTROL Maintain layers]** | Rippar lagren i PSD, om det finns några, till enskilda resurser. Resurslagren förblir kopplade till PSD. Du kan visa dem genom att öppna filen PSD i detaljvyn och välja lagerpanelen. Se Visa och redigera lager i en PSD-fil. |
| **[!UICONTROL Create template]** | Skapar en mall från lagren i filen PSD. |
| **[!UICONTROL Extract text]** | Extraherar texten så att användare kan söka efter text i ett visningsprogram. |
| **[!UICONTROL Extend layers to background size]** | Utökar storleken på överlappade bildlager till storleken på bakgrundslagret. |
| **[!UICONTROL Layer naming]** | Utökar storleken på överlappade bildlager till storleken på bakgrundslagret.<br>・ **[!UICONTROL Layer name]** - Namnger bilderna efter deras lagernamn i filen PSD. Ett lager med namnet Price Tag i den ursprungliga PSD-filen blir till exempel en bild med namnet Price Tag. Om lagernamnen i filen PSD är Photoshop standardlagernamn (Bakgrund, Lager 1, Lager 2 och så vidare) får bilderna namn efter sina lagernummer i filen PSD. <br>・ **[!UICONTROL Photoshop and layer number]** - Namnger bilderna efter deras lagernummer i filen PSD och ignorerar de ursprungliga lagernamnen. Bilderna får samma namn som Photoshop-filnamnet och ett nummer i det tillagda lagret. Det andra lagret i en fil med namnet `Spring Ad.psd` är namngiven `Spring Ad_2` även om det har ett icke-standardnamn i Photoshop.<br>・ **[!UICONTROL Photoshop and layer name]** - Namnger bilderna efter PSD-filen följt av lagernamnet eller lagernumret. Lagernumret används om lagernamnen i filen PSD är Photoshop standardlagernamn. Ett lager med namnet `Price Tag` i en PSD-fil med namnet `SpringAd` är namngiven `Spring Ad_Price Tag`. Ett lager med standardnamnet Lager2 anropas `Spring Ad_2`. |
| **[!UICONTROL Anchor]** | Ange hur bilder ska förankras i mallar som genereras från lagerkompositionen som skapas från filen PSD. Som standard är ankarpunkten i mitten. Med en central ankarpunkt kan ersättningsbilder bäst fylla samma område, oavsett ersättningsbildens proportioner. Bilder med en annan aspekt som ersätter den här bilden upptar i själva verket samma utrymme när de refererar till mallen och använder parameterersättning. Ändra till en annan inställning om ditt program kräver att ersättningsbilderna fyller ut det tilldelade utrymmet i mallen. |

### PDF, flik {#pdf-tab}

Det högsta antalet sidor för en PDF som ska övervägas för extrahering är 5000 för nya överföringar. Denna gräns kommer att ändras till 100 sidor (för alla PDF) den 31 december 2022. Se även [Dynamic Media begränsningar](/help/assets/dynamic-media/limitations.md).

Du kan välja att rastrera filerna, extrahera sökord och länkar, ange upplösning och välja en färgrymd.

| PDF, alternativ | Beskrivning |
| --- | --- |
| **[!UICONTROL Processing]** | ・ **[!UICONTROL None]** - Ingen bearbetning av PDF görs.<br>・ **[!UICONTROL Thumbnail]** - Rippar varje sida i filen PDF och konverterar den till en miniatyrbild.<br> ・ **[!UICONTROL Rasterize]** - Rippar sidorna i PDF-filen och konverterar vektorgrafik till bitmappsbilder. Välj det här alternativet om du vill skapa en e-katalog. |
| **[!UICONTROL Extract]** | ・ **[!UICONTROL None]** - Inga sökord eller länkar extraheras från PDF.<br>・ **[!UICONTROL Search words]** - Extraherar sökord från PDF-filen så att filen kan genomsökas efter nyckelord i en eCatalog Viewer.<br>・ **[!UICONTROL Links]** - Extraherar länkar från PDF-filerna och konverterar dem till Image Maps som används i en eCatalog Viewer.<br>・ **[!UICONTROL Search words and links]** - Extraherar både sökord och länkar för användning i ett eCatalog-visningsprogram. |
| **[!UICONTROL Resolution (pixel/inch)]** | Anger upplösningsinställningen. Den här inställningen avgör hur många pixlar som visas per tum i filen PDF. Standardvärdet är 150. |
| **[!UICONTROL Color space]** | ・ **[!UICONTROL Detect automatically]** - Behåller färgrymden för PDF-filen.<br>・ **[!UICONTROL Force as RGB]** - Konverterar till färgmodellen RGB.<br>・ **[!UICONTROL Force as CMYK]** - Konverterar till CMYK-färgmodellen.<br>・ **[!UICONTROL Force as Grayscale]** - Konverterar till färgmodellen Gråskala. |

### Fliken Illustrator {#illustrator-tab}

Du kan rastrera Adobe Illustrator®-filer, behålla genomskinliga bakgrunder, välja en upplösning och välja en färgrymd.

Du kan använda Adobe® Illustrator®-filer (AI) i Adobe Dynamic Media. I Adobe Dynamic Media finns kommandon för att konfigurera de här filerna när du överför dem.

När du överför Illustrator-bildfiler (AI) kan du formatera dem på olika sätt. Du kan rastrera filerna, behålla den genomskinliga bakgrunden, välja en upplösning och välja en färgrymd. Formateringsalternativ för PostScript- och Illustrator-filer finns på överföringsskärmen under PostScript-alternativ och Illustrator-alternativ i rutan Överför jobbalternativ.


| Illustrator | Beskrivning |
| --- | --- |
| **[!UICONTROL Processing]** | Välj Rastrera om du vill konvertera vektorgrafik i filen till bitmappsformat. |
| **[!UICONTROL Maintain transparent background in rendered images]** | Bevarar filens genomskinlighet i bakgrunden. |
| **[!UICONTROL Resolution (pixel/inch)]** | Anger upplösningsinställningen. Den här inställningen avgör hur många pixlar som visas per tum i filen. |
| **[!UICONTROL Color space]** | ・ **[!UICONTROL Detect automatically]** - Behåller filens färgrymd.<br>・ **[!UICONTROL Force as RGB]** - Konverterar till färgmodellen RGB.<br>・ **[!UICONTROL Force as CMYK]** - Konverterar till CMYK-färgmodellen.<br>・ **[!UICONTROL Force as Grayscale]** - Konverterar till färgmodellen Gråskala. |
