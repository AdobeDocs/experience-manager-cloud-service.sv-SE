---
title: Lägga till dynamiska medieresurser på sidor
description: Lägga till komponenter för dynamiska media på en sida i AEM
translation-type: tm+mt
source-git-commit: 776b089a322cc4f86fdcb9ddf1c3cc207fc85d39

---


# Lägga till dynamiska medieresurser på sidor{#adding-dynamic-media-assets-to-pages}

Om du vill lägga till funktionen för dynamiska media i resurser som du använder på dina webbplatser kan du lägga till komponenten **Dynamic Media**, **Interactive Media**, **Panoramic Media** eller **Video 360 Media** direkt på sidan. Det gör du genom att gå in i layoutläget och aktivera komponenterna för dynamiska media. Sedan kan du lägga till de här komponenterna på sidan och lägga till resurser i komponenten. Dynamic Media-komponenterna är smarta - de vet om du lägger till en bild eller en video och de tillgängliga konfigurationsalternativen ändras i enlighet med detta.

Du lägger till Dynamic Media-resurser direkt på sidan om du använder AEM som WCM. Om du använder en tredjepartsleverantör för ditt WCM-system kan du antingen [länka](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) eller [bädda in](/help/assets/dynamic-media/embed-code.md) dina resurser. Om du har en responsiv tredjepartswebbplats läser du [i Leverera optimerade bilder till en responsiv webbplats](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>Du måste publicera resurser innan du lägger till dem på sidor i AEM. Se [Publicera dynamiska medieresurser](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Lägga till en Dynamic Media-komponent på en sida {#adding-a-dynamic-media-component-to-a-page}

Att lägga till en Dynamic Media-, Interactive Media-, Panoramic Media- eller Video 360 Media-komponent på en sida är detsamma som att lägga till en komponent på en sida. Komponenterna för dynamiska media beskrivs i följande avsnitt.

**Lägga till en Dynamic Media-komponent på en sida**

1. Öppna sidan där du vill lägga till komponenten Dynamic Media i AEM.
1. Tryck på ikonen **[!UICONTROL Komponenter]** i den vänstra rutan och filtrera sedan efter Dynamic Media.

   Om det inte finns några Dynamic Media-komponenter tillgängliga måste du aktivera eller aktivera Dynamic Media-komponenterna. Mer information finns i [Redigera mallar - Mallförfattare](/help/sites-cloud/authoring/features/templates.md) .

   ![6_5_360video_wcmcomponent](assets/6_5_360video_wcmcomponent.png)

1. Dra en **[!UICONTROL Dynamic Media]** -komponent och släpp den på önskad plats på sidan.

   I exemplet nedan används **[!UICONTROL Video 360 Media]** -komponenten.

   ![6_5_360video_wcmComponentdrag](assets/6_5_360video_wcmcomponentdrag.png)

1. Håll muspekaren direkt på komponenten. När komponenten är omgiven av en blå ruta trycker du en gång för att visa komponentens verktygsfält. Tryck på ikonen **[!UICONTROL Konfiguration (skiftnyckel)]** .

   ![6_5_360video_wcmComponentconfigure](assets/6_5_360video_wcmcomponentconfigure.png)

1. Beroende på vilken Dynamic Media-komponent du släppte på sidan öppnas en konfigurationsdialogruta. [Ange komponentens alternativ](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) efter behov.

   I exemplet nedan visas dialogrutan Dynamic Media **[!UICONTROL Video 360 Media]** Component (Media-komponent) och de alternativ som är tillgängliga i listrutan Viewer Preset (Visningsförinställning).

   ![Video 360 Media-komponent](assets/6_5_360video_wcmcomponentviewerpreset.png)

   Dynamic Media Video 360 Media-komponenten.

1. När du är klar, nära dialogrutans övre högra hörn, trycker du på bockmarkeringen för att spara ändringarna.

## Lokalisera dynamiska mediakomponenter {#localizing-dynamic-media-components}

Du kan lokalisera komponenter för dynamiska media på ett av två sätt:

* Öppna **[!UICONTROL Egenskaper]** på en webbsida i Platser och välj fliken **[!UICONTROL Avancerat]** . Välj språk för lokalisering.

   ![chlimage_1-172](assets/chlimage_1-538.png)

* Välj önskad sida eller sidgrupp i platsväljaren. Tryck på **[!UICONTROL Egenskaper]** och välj fliken **[!UICONTROL Avancerat]** . Välj språk för lokalisering.

   >[!NOTE]
   >
   >Observera att inte alla språk som är tillgängliga på menyn **[!UICONTROL Språk]** har tilldelats tokens.

## Tillgängliga dynamiska mediakomponenter {#dynamic-media-components}

Dynamiska mediekomponenter är tillgängliga när du trycker på ikonen **[!UICONTROL Komponenter]** och sedan filtrerar på **[!UICONTROL Dynamic Media]**.

De dynamiska mediakomponenterna som är tillgängliga omfattar följande:

* **[!UICONTROL Dynamiska media]** - Använd för exempelvis bilder, video, e-kataloger och snurra.
* **[!UICONTROL Interaktiva media]** - Använd för interaktiva resurser som interaktiv video, interaktiva bilder eller karuselluppsättningar.
* **[!UICONTROL Panoramabilder]** - Används för panoramabilder eller panoramabilder från VR.
* **[!UICONTROL Video 360 Media]** - Använd för 360-video och 360-VR-videomaterial.

>[!NOTE]
>
>De här komponenterna är inte tillgängliga som standard och måste göras tillgängliga via mallredigeraren innan du använder dem. När de är tillgängliga i mallredigeraren kan du lägga till komponenterna på sidan på samma sätt som andra AEM-komponenter.

![6_5_dynamicmediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### Komponent:Dynamiska medier {#dynamic-media-component}

Komponenten Dynamic Media är smart. Beroende på om du lägger till en bild eller en video har du olika alternativ. Komponenten har stöd för bildförinställningar, bildbaserade visningsprogram som bilduppsättningar, snurra, blandade medieuppsättningar och video. Dessutom är visningsprogrammet responsivt - skärmstorleken ändras automatiskt baserat på skärmstorleken. Alla visningsprogram är HTML5-visningsprogram.

>[!NOTE]
>
>Om din webbsida har följande:
>
>* Flera instanser av komponenten Dynamic Media används på samma sida.
>* Varje instans använder samma resurstyp.
>
>
Tänk på att det inte går att tilldela olika visningsprogramförinställningar till varje Dynamic Media-komponent på den sidan.
>
>Du kan dock använda samma visningsförinställning för alla komponenter för dynamiska media som använder resurser av samma typ på sidan.

När du lägger till komponenten Dynamic Media och **[!UICONTROL Dynamiska mediainställningar]** är tomma eller du inte kan lägga till en resurs på rätt sätt ska du kontrollera följande:

* Bilden har en pyramidformad fil. Bilder som importerats innan dynamiska medier aktiverats har ingen pyramiddiff-fil.

#### När du arbetar med bilder {#when-working-with-images}

Med komponenten Dynamic Media kan du lägga till dynamiska bilder, inklusive bilduppsättningar, snurpuppsättningar och blandade medieuppsättningar. Du kan zooma in, zooma ut och, om tillämpligt, vrida en bild i en snurra eller välja en bild från en annan typ av uppsättning.

Du kan också konfigurera visningsförinställningen, bildförinställningen eller bildformatet direkt i komponenten. Om du vill göra en bild responsiv kan du antingen ange brytpunkter eller använda en responsiv bildförinställning.

Du kan redigera följande dynamiska mediainställningar genom att trycka på ikonen **[!UICONTROL Redigera]** i komponenten och sedan på **[!UICONTROL Dynamiska mediainställningar]**.

![dm-settings-image-preset](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>Som standard är bildkomponenten för dynamiska media adaptiv. Om du vill göra den till en fast storlek anger du den i komponenten på fliken **[!UICONTROL Avancerat]** med **[!UICONTROL Bredd]** och **[!UICONTROL Höjd]**.

* **[!UICONTROL Visningsförinställning]**- Välj en befintlig visningsförinställning i listrutan. Om den visningsförinställning som du söker efter inte visas kanske du måste göra den synlig. Se Hantera förinställningar för visningsprogram. Du kan inte välja en visningsförinställning om du använder en bildförinställning och vice versa.

   Det här är det enda tillgängliga alternativet om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar. De visningsförinställningar som visas är också smarta - endast relevanta visningsprogramförinställningar visas.

* **[!UICONTROL Modifierare]** för visningsprogram - Modifierare för visningsprogram har formen av namn=värde-par med en &amp;-avgränsare och du kan ändra visningsprogram enligt anvisningarna i referenshandboken för visningsprogram. Ett exempel på en visningsmodifierare är `posterimage=img.jpg&caption=text.vtt,1` som ställer in en annan bild för videominiatyrbilden och kopplar en undertextningsfil till videon.

* **[!UICONTROL Bildförinställning]**- Välj en befintlig bildförinställning i listrutan. Om den bildförinställning du söker inte syns kan du behöva göra den synlig. Se Hantera bildförinställningar. Du kan inte välja en visningsförinställning om du använder en bildförinställning och vice versa.

   Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

* **[!UICONTROL Bildmodifierare]**- Du kan använda bildeffekter genom att ange ytterligare bildkommandon. Dessa beskrivs i Bildförinställningar och i Referens för bildserverkommando.

   Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

* **[!UICONTROL Brytpunkter]**- Om du använder den här resursen på en responsiv webbplats måste du lägga till bildbrytpunkter. Bildbrytpunkter måste avgränsas med kommatecken (,). Det här alternativet fungerar när ingen höjd eller bredd har definierats i en bildförinställning.

   Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

   Du kan redigera följande avancerade inställningar genom att trycka på **[!UICONTROL Redigera]** i komponenten.

* **[!UICONTROL Titel]**- Ändra bildens titel.

* **[!UICONTROL Alt Text]**- Lägg till en titel i bilden för de användare som har inaktiverat grafik.

   Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

* **[!UICONTROL URL, Öppna i]**- Du kan ange att en resurs ska öppna en länk. Ange URL:en och Öppna i anger om du vill att den ska öppnas i samma fönster eller i ett nytt fönster.

   Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

* **[!UICONTROL Bredd]**- Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

* **[!UICONTROL Höjd]**- Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.


#### När du arbetar med video {#when-working-with-video}

Använd komponenten Dynamic Media för att lägga till dynamisk video på dina webbsidor. När du redigerar komponenten kan du välja att använda en fördefinierad videovisningsförinställning för att spela upp videon på sidan.

![chlimage_1-173](assets/chlimage_1-540.png)

Du kan redigera följande dynamiska mediainställningar genom att klicka på **[!UICONTROL Redigera]** i komponenten.

>[!NOTE]
>
>Som standard är videokomponenten för dynamiska media adaptiv. Om du vill göra den till en fast storlek anger du den i komponenten med **[!UICONTROL Bredd]** och **[!UICONTROL Höjd]** på fliken **[!UICONTROL Avancerat]** .

* **[!UICONTROL Viewer preset**- Välj en befintlig förinställning för visningsprogrammet för video i listrutan. Om den visningsförinställning som du söker efter inte visas kanske du måste göra den synlig. Se Hantera förinställningar för visningsprogram.

* **[!UICONTROL Viewer modifiers**- Viewer modifiers har formen av name=value-par med en &amp;-avgränsare och du kan ändra visningsprogram enligt riktlinjerna i referenshandboken för Adobe Viewer. Ett exempel på en visningsmodifierare är `posterimage=img.jpg&caption=text.vtt,1`

   Med visningsmodifierare kan du till exempel göra följande:

   * Associera en bildtextfil med en video: [bildtext](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html)
   * Associera en navigeringsfil med en video: [navigering](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html)
   Du kan redigera följande avancerade inställningar genom att klicka på **[!UICONTROL Redigera]** i komponenten.

* **[!UICONTROL Title**- Ändra videons titel.

* **[!UICONTROL Bredd]**- Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

* **[!UICONTROL Höjd]**- Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

#### När du arbetar med smart beskärning {#when-working-with-smart-crop}

Använd komponenten Dynamic Media för att lägga till bildresurser för smart beskärning på dina webbsidor. När du redigerar komponenten kan du välja att använda en fördefinierad videovisningsförinställning för att spela upp videon på sidan.

Se [Använda smart beskärning med AEM Assets Dynamic Media](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/smart-crop-feature-video-use.html)

Se även [Bildprofiler](/help/assets/dynamic-media/image-profiles.md).

![dm-settings-smart-crop](assets/dm-settings-smart-crop.png)

Du kan redigera följande dynamiska mediainställningar genom att klicka på **[!UICONTROL Redigera]** i komponenten.

>[!NOTE]
>
>Som standard är bildkomponenten för dynamiska media adaptiv. Om du vill göra den till en fast storlek anger du den i komponenten på fliken **[!UICONTROL Avancerat]** med **[!UICONTROL Bredd]** och **[!UICONTROL Höjd]**.

* **[!UICONTROL Bildmodifierare]**- Du kan använda bildeffekter genom att ange ytterligare bildkommandon. Dessa beskrivs i Bildförinställningar och i Referens för bildserverkommando.

   Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

   Du kan redigera följande avancerade inställningar genom att klicka på **[!UICONTROL Redigera]** i komponenten.

* **[!UICONTROL Titel]**- Ändra titeln på bilden för smart beskärning.

* **[!UICONTROL Alt Text]**- Lägg till en titel i den smarta beskärningsbilden för de användare som har inaktiverat grafik.

   Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

* **[!UICONTROL URL, Öppna i]**- Du kan ange att en resurs ska öppna en länk. Ange URL:en och Öppna i anger om du vill att den ska öppnas i samma fönster eller i ett nytt fönster.

   Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

* **[!UICONTROL Bredd]**- Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

* **[!UICONTROL Höjd]**- Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

### Komponent: Interaktiva media {#interactive-media-component}

Komponenten Interactive Media är till för de resurser som har interaktivitet i dem, till exempel hotspot-områden eller bildscheman. Om du har en interaktiv bild, interaktiv video eller karusellbanderoll använder du komponenten **[!UICONTROL Interactive Media]** .

Komponenten Interactive Media är smart. Beroende på om du lägger till en bild eller en video har du olika alternativ. Dessutom är visningsprogrammet responsivt - skärmstorleken ändras automatiskt baserat på skärmstorleken. Alla visningsprogram är HTML5-visningsprogram.

>[!NOTE]
>
>Om din webbsida har följande:
>
>* Flera instanser av komponenten Interactive Media används på samma sida.
>* Varje instans använder samma resurstyp.
>
>
Tänk på att det inte går att tilldela olika visningsprogramförinställningar till varje interaktiv mediekomponent på den sidan.
>
>Du kan dock använda samma visningsförinställning för alla interaktiva mediekomponenter som använder resurser av samma typ på sidan.

![chlimage_1-174](assets/chlimage_1-541.png)

Du kan redigera följande **[!UICONTROL allmänna]** inställningar genom att trycka på **[!UICONTROL Redigera]** i komponenten.

* **[!UICONTROL Visningsförinställning]**- Välj en befintlig visningsförinställning i listrutan. Om den visningsförinställning som du söker efter inte visas kanske du måste göra den synlig. Förinställningar för visningsprogram måste publiceras innan de kan användas. Se Hantera förinställningar för visningsprogram.

* **[!UICONTROL Titel]**- Ändra videons titel.

* **[!UICONTROL Bredd]**- Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

* **[!UICONTROL Höjd]**- Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

   Du kan redigera följande inställningar för **[!UICONTROL Lägg till i kundvagnen]** genom att klicka på **[!UICONTROL Redigera]** i komponenten.

* **[!UICONTROL Visa produktresurs]**- Som standard är det här värdet valt. Produktresursen visar en bild av produkten enligt definitionen i modulen Handel. Avmarkera kryssrutan om du inte vill visa produktresursen.

* **[!UICONTROL Visa produktpris]**- Som standard är det här värdet valt. Produktpriset visar priset för artikeln enligt definitionen i modulen Handel. Avmarkera kryssrutan om du inte vill visa produktpriset.

* **[!UICONTROL Visa produktformulär]**- Som standard är det här värdet inte valt. Produktformuläret innehåller alla produktvarianter som storlek och färg. Avmarkera kryssrutan om du inte vill visa produktvarianterna.

### Komponent: Panoramabilder {#panoramic-media-component}

Komponenten för panoramamedia är avsedd för resurser som är sfäriska panoramabilder. Sådana bilder ger en 360-gradig visningsupplevelse av ett rum, en egenskap, en plats eller ett landskap. För att en bild ska kvalificeras som ett sfäriskt panorama måste den ha antingen ett ELLER båda av följande:

* Proportionerna 2:1.
* Taggad med nyckelorden `equirectangular` eller (`spherical` + `panorama`) eller (`spherical` + `panoramic`). Se [Använda taggar](/help/sites-cloud/authoring/features/tags.md).

Både proportioner och nyckelordskriterier gäller för panoramaresurser för sidan med resursinformation och WCM-komponenten för **[!UICONTROL panoramamabilder]** .

>[!NOTE]
>
>Om din webbsida har följande:
>
>* Flera instanser av **[!UICONTROL panoramakomponenten]** används på samma sida.
>* Varje instans använder samma resurstyp.
>
>
Tänk på att det inte går att tilldela olika visningsförinställningar till varje **[!UICONTROL panoramamediekomponent]** på den sidan.
>
>Du kan dock använda samma visningsförinställning för alla panoramakomponenter som använder resurser av samma typ på sidan.

![panoramabild-media-viewer-preset](assets/panoramic-media-viewer-preset.png)

Du kan redigera följande inställning genom att trycka på **[!UICONTROL Konfigurera]** i komponenten.

* **[!UICONTROL Förinställning]** för visningsprogram - Välj ett befintligt visningsprogram i listrutan med förinställningar för visningsprogram.

Om den visningsförinställning du söker efter inte visas kontrollerar du att den är publicerad. Du måste publicera förinställningarna för visningsprogrammet innan du kan använda dem. Se [Hantera visningsförinställningar](/help/assets/dynamic-media/managing-viewer-presets.md).

### Komponent: Video 360 Media {#video-media-component}

Använd **[!UICONTROL Video 360 Media]** -komponenten för att återge ekvirektangulär video på din webbsida för att få en engagerande upplevelse av ett rum, en egenskap, plats, landskap eller läkarvård.

Vid uppspelning på en platt skärm har användaren kontroll över betraktningsvinkeln. uppspelning på mobila enheter utnyttjar vanligtvis de inbyggda gyroskopiska kontrollerna.

Visningsprogrammet har inbyggt stöd för leverans av 360 videomaterial. Som standard krävs ingen ytterligare konfiguration för visning eller uppspelning. Du levererar 360-video med standardvideotillägg som .mp4, .mkv och .mov. Den vanligaste kodeken är H.264.

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

Du kan redigera följande inställning genom att trycka på **[!UICONTROL Konfigurera]** i komponenten.

* **[!UICONTROL Förinställning]** för visningsprogram - Välj ett befintligt visningsprogram i listrutan med förinställningar för visningsprogram. Använd Video360VR för slutanvändare som använder virtuella verklighetsglasögon. Innehåller grundläggande videouppspelningskontroller och funktioner för sociala medier. Använd Video360_social som innehåller grundläggande videouppspelningskontroller. Videoåtergivning sker i stereoläge. Manuell vypunktskontroll är inaktiverad men gyroskopisk kontroll är aktiverad. Det finns inga funktioner för sociala medier.

Om den visningsförinställning du söker efter inte visas kontrollerar du att den är publicerad. Du måste publicera förinställningarna för visningsprogrammet innan du kan använda dem. Se [Hantera visningsförinställningar](/help/assets/dynamic-media/managing-viewer-presets.md).

### Använda HTTP/2 för att leverera Dynamic Media-resurser {#using-http-to-delivery-dynamic-media-assets}

HTTP/2 är det nya, uppdaterade webbprotokollet som förbättrar kommunikationen mellan webbläsare och servrar. Det ger snabbare överföring av information och minskar mängden processorkraft som behövs. Dynamic Media-material kan nu levereras via HTTP/2 vilket ger bättre respons och laddningstider.

Se [HTTP2 Delivery of Content](/help/assets/dynamic-media/http2.md) för fullständig information om hur du kommer igång med HTTP/2 med ditt Dynamic Media-konto.

>[!MORELIKETHIS]
>
>* [Använda videospelaren i AEM Dynamic Media](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-video-player-feature-video-use.html)
>* [Använda interaktiv video med AEM Dynamic Media](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html)
>* [Så här fungerar resursvisningsprogrammet med AEM Dynamic Media](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-viewer-feature-video-understand.html)
>* [Använda anpassade videominiatyrer med AEM Dynamic Media](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-video-thumbnails-feature-video-use.html)
>* [Färghantering med AEM Dynamic Media](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-color-management-technical-video-setup.html)
>* [Använda bildskärpa med AEM Dynamic Media](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html)

