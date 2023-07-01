---
title: Lägga till Dynamic Media Assets på sidor
description: Lär dig hur du lägger till Dynamic Media-komponenter på en sida i Adobe Experience Manager as a Cloud Service.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 2f2fd6cb-8b53-4167-a7e3-453f27549109
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '3053'
ht-degree: 5%

---

# Lägga till Dynamic Media Assets på sidor{#adding-dynamic-media-assets-to-pages}

Om du vill lägga till Dynamic Media-funktionalitet i resurser som du använder på dina webbplatser kan du lägga till **Dynamic Media**, **Interaktiva media**, **Panoramabilder**, eller **Video 360 Media** direkt på sidan. Du aktiverar layoutläget och Dynamic Media-komponenterna. Sedan lägger du till de här komponenterna på sidan och lägger till resurser i komponenten. Dynamic Media-komponenterna är smarta – de känner av om du lägger till en bild eller en video och konfigurationsalternativen ändras i enlighet med detta.

Du lägger till Dynamic Media-resurser direkt på sidan om du använder [!DNL Adobe Experience Manager] som din WCM. Om ni använder en annan leverantör för innehållshanteringssystemet kan ni antingen [länka](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) eller [bädda in](/help/assets/dynamic-media/embed-code.md) resurserna. En responsiv tredjepartswebbplats finns på [leverera optimerade bilder till en responsiv webbplats](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>Publicera resurser innan du lägger till dem på sidor i [!DNL Experience Manager]. Se [Publicera Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Lägga till en Dynamic Media-komponent på en sida {#adding-a-dynamic-media-component-to-a-page}

Att lägga till en 3D-mediekomponent, Dynamic Media, Interactive Media, Panoramic Media, Smart Crop Video eller Video 360 Media på en sida är detsamma som att lägga till en komponent på en sida.

**Så här lägger du till en Dynamic Media-komponent på en sida:**

1. I [!DNL Experience Manager]öppnar du sidan där du vill lägga till Dynamic Media-komponenten.
1. I den vänstra rutan väljer du **[!UICONTROL Components]** och sedan filtrera efter Dynamic Media.

   Om det inte finns någon lista över Dynamic Media-komponenter måste du troligen aktivera de Dynamic Media-komponenter som du vill använda. Se [Aktivera Dynamic Media-komponenter](#enabling-dynamic-media-components).

   ![6_5_360video_wcmcomponent](assets/6_5_360video_wcmcomponent.png)

1. Dra en **[!UICONTROL Dynamic Media]** och släpp den på önskad plats på sidan.

1. Håll pekaren direkt på komponenten. När komponenten omges av en blå ruta väljer du en gång för att visa komponentens verktygsfält. Välj **[!UICONTROL Configuration (wrench)]** ikon.

   ![6_5_360video_wcmComponentconfigure](assets/6_5_360video_wcmcomponentconfigure.png)

1. Beroende på vilken Dynamic Media-komponent du släppte på sidan öppnas en konfigurationsdialogruta. [Ange komponentens alternativ](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) vid behov.

   I exemplet nedan visas Dynamic Media **[!UICONTROL Video 360 Media]** och de alternativ som är tillgängliga i listrutan för visningsförinställningar.

   ![Video 360 Media-komponent](assets/6_5_360video_wcmcomponentviewerpreset.png)

   Dynamic Media Video 360 Media-komponenten.

1. När du är klar markerar du bockmarkeringen i dialogrutans övre högra hörn för att spara ändringarna.

### Aktivera Dynamic Media-komponenter {#enabling-dynamic-media-components}

Om det inte finns några Dynamic Media-komponenter att lägga till på en sida betyder det troligtvis att du måste aktivera de komponenter som du vill använda.

1. I [!DNL Experience Manager]öppnar du sidan där du vill lägga till Dynamic Media-komponenten.
1. Till vänster om verktygsfältet uppe på sidan väljer du ikonen Sidinformation och väljer sedan **[!UICONTROL Edit Template]** i listrutan.

   ![edit-template](/help/assets/assets-dm/edit-template.png)

1. På höger sida av verktygsfältet uppe på sidan väljer du **[!UICONTROL Structure]**.

   ![Policy](/help/assets/assets-dm/structure-mode.png)

1. Långt ned på sidan väljer du **[!UICONTROL Layout Container]** för att öppna verktygsfältet och sedan välja ikonen Policy.
1. På **[!UICONTROL Layout Container]** sida, under **[!UICONTROL Properties]** måste du se till att **[!UICONTROL Allowed Components]** -fliken är markerad.

   ![Tillåtna komponenter](/help/assets/assets-dm/allowed-components.png)

1. Rulla tills du ser **[!UICONTROL Dynamic Media]**.
1. Välj >-ikonen till vänster om **[!UICONTROL Dynamic Media]** markerar du de Dynamic Media-komponenter som du vill aktivera.

   ![Lista över komponenter i Dynamic Media](/help/assets/assets-dm/dm-components-select.png)

1. Nära det övre högra hörnet av **[!UICONTROL Layout Container]** väljer du ikonen Klar (bockmarkering).

1. På höger sida av verktygsfältet uppe på sidan väljer du **[!UICONTROL Initial Content]**.
1. [Lägga till en Dynamic Media-komponent på en sida](#adding-a-dynamic-media-component-to-a-page) som vanligt.

## Lokalisera Dynamic Media-komponenter {#localizing-dynamic-media-components}

Du kan lokalisera Dynamic Media-komponenter på ett av två sätt:

* Från en webbsida i Sites öppnar du **[!UICONTROL Properties]** och väljer fliken **[!UICONTROL Advanced]**. Välj språk för lokalisering.

  ![chlimage_1-172](assets/chlimage_1-538.png)

* Välj önskad sida eller sidgrupp i platsväljaren. Välj **[!UICONTROL Properties]** och väljer **[!UICONTROL Advanced]** -fliken. Välj språk för lokalisering.

  >[!NOTE]
  >
  >Inte alla språk som är tillgängliga i **[!UICONTROL Language]** menyn har för närvarande tilldelade variabler.

## Tillgängliga Dynamic Media-komponenter {#dynamic-media-components}

Dynamic Media-komponenter är tillgängliga när du väljer **[!UICONTROL Components]** ikon, filtrera sedan på **[!UICONTROL Dynamic Media]**.

Följande Dynamic Media-komponenter är tillgängliga:

* **[!UICONTROL Dynamic Media]** – Används för t.ex. bilder, video, e-kataloger och rotationsuppsättningar.
* **[!UICONTROL Interactive Media]** - Använd för interaktiva resurser som interaktiv video, interaktiva bilder eller karuselluppsättningar.
* **[!UICONTROL Panoramic Media]** - Används för panoramabilder eller panoramabilder från VR.
* **[!UICONTROL Video 360 Media]** - Används för 360-video och 360-VR-videomaterial.

>[!NOTE]
>
>De här komponenterna är inte tillgängliga som standard och måste göras tillgängliga via mallredigeraren innan du använder dem. När de har gjorts tillgängliga i mallredigeraren kan du lägga till komponenterna på sidan precis som andra komponenter [!DNL Experience Manager] -komponenten.

![6_5_dynamicmediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### Komponent: Dynamic Media {#dynamic-media-component}

Dynamic Media-komponenten är smart. Oavsett om du lägger till en bild eller en video har du olika alternativ. Komponenten har stöd för bildförinställningar, bildbaserade visningsprogram som bilduppsättningar, snurra, blandade medieuppsättningar och video. Dessutom är visningsprogrammet responsivt - skärmstorleken ändras automatiskt baserat på skärmstorleken. Alla visningsprogram är HTML5-visningsprogram.

>[!NOTE]
>
>Om din webbsida har följande:
>
>* Flera instanser av Dynamic Media-komponenten som används på samma sida.
>* Varje instans använder samma resurstyp.
>
>Det går inte att tilldela olika visningsprogramförinställningar till varje Dynamic Media-komponent på den sidan.
>
>Du kan dock använda samma visningsförinställning för alla Dynamic Media-komponenter som använder resurser av samma typ på sidan.

När du lägger till Dynamic Media-komponenten och **[!UICONTROL Dynamic Media Settings]** är tom eller du inte kan lägga till en resurs på rätt sätt, kontrollera följande:

* Bilden har en pyramidformad fil. Bilder som importeras innan du aktiverar Dynamic Media saknar en pyramidformad fil.

#### När du arbetar med bilder {#when-working-with-images}

Med Dynamic Media-komponenten kan du lägga till dynamiska bilder, inklusive bilduppsättningar, snurremsor och blandade medieuppsättningar. Du kan zooma in, zooma ut och, om tillämpligt, vrida en bild i en snurra eller välja en bild från en annan typ av uppsättning.

Du kan också konfigurera visningsförinställningen, bildförinställningen eller bildformatet direkt i komponenten. Om du vill göra en bild responsiv kan du antingen ange brytpunkter eller använda en responsiv bildförinställning.

Du kan redigera följande Dynamic Media-inställningar genom att välja **[!UICONTROL Edit]** -ikonen i komponenten och sedan **[!UICONTROL Dynamic Media Settings]**.

![Inställningar för Dynamic Media-bildförinställningar](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>Som standard är Dynamic Media-bildkomponenten adaptiv. Om du vill att den ska ha en fast storlek anger du det i komponenten på fliken **[!UICONTROL Advanced]** med **[!UICONTROL Width]** och **[!UICONTROL Height]**.

* **[!UICONTROL Viewer preset]** - Välj en befintlig visningsförinställning i listrutan. Om den visningsförinställning du söker efter inte visas måste du göra den synlig. Se Hantera förinställningar för visningsprogram. Du kan inte välja en visningsförinställning om du använder en bildförinställning och omvänt.

  Det här alternativet är det enda tillgängliga alternativet om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar. De visningsförinställningar som visas är även förinställningar som bara är smarta och relevanta för visningsprogrammet visas.

* **[!UICONTROL Viewer modifiers]** - Visningsmodifierare har formen av namn=värde-par med en &amp;-avgränsare och du kan ändra visningsprogram enligt riktlinjerna i referenshandboken för visningsprogrammen. Ett exempel på en visningsmodifierare är `posterimage=img.jpg&caption=text.vtt,1` som anger en annan bild för videominiatyrbilden och associerar en undertextningsfil med videon.

* **[!UICONTROL Image preset]** - Välj en befintlig bildförinställning i listrutan. Om den bildförinställning du söker inte syns måste du göra den synlig. Se Hantera bildförinställningar. Du kan inte välja en visningsförinställning om du använder en bildförinställning och omvänt.

  Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

* **[!UICONTROL Image Modifiers]** - Du kan använda bildeffekter genom att ange fler bildkommandon. Dessa kommandon beskrivs i Bildförinställningar och i Referens för bildserverkommando.

  Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

* **[!UICONTROL Breakpoints]** - Om du använder den här resursen på en responsiv webbplats måste du lägga till bildbrytpunkter. Bildbrytpunkter måste avgränsas med kommatecken (,). Det här alternativet fungerar när ingen höjd eller bredd har definierats i en bildförinställning.

  Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

  Du kan redigera följande avancerade inställningar genom att välja **[!UICONTROL Edit]** i komponenten.

* **[!UICONTROL Optimize for higher resolution devices]** - Markera (standard) kryssrutan för att tillåta optimering av DPR (Device Pixel Ratio).

  The **[!UICONTROL Optimize for higher resolution devices]** visas bara när följande är sant:
   * Under Förinställningstyp, **[!UICONTROL Image Preset]** är markerat och **[!UICONTROL RESS_IP]** är markerat i **[!UICONTROL Image Preset]** nedrullningsbar lista.

  ![inställning för enhetens pixelproportioner för bildförinställning](/help/assets/dynamic-media/assets/dpr-ress-ip.png)

  Se även [Om optimering av enhetens pixelproportioner](/help/assets/dynamic-media/imaging-faq.md#dpr).

  Alla [!DNL Experience Manager] DPR-värden för Dynamic Media Smart Imaging ignoreras.

* **[!UICONTROL Title]** - Ändra bildens titel.

* **[!UICONTROL Alt Text]** - Lägg till en titel i bilden för de användare som har inaktiverat grafik.

  Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

* **[!UICONTROL URL, Open in]** - Du kan ange att en resurs ska öppna en länk. Ange URL:en och Öppna i anger om du vill att den ska öppnas i samma fönster eller i ett nytt fönster.

  Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

* **[!UICONTROL Width]** - Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

* **[!UICONTROL Height]** - Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

#### När du arbetar med video {#when-working-with-video}

Använd Dynamic Media-komponenten för att lägga till dynamisk video på dina webbsidor. När du redigerar komponenten kan du välja att använda en fördefinierad videovisningsförinställning för att spela upp videon på sidan.

![chlimage_1-173](assets/chlimage_1-540.png)

Du kan redigera följande Dynamic Media-inställningar genom att välja **[!UICONTROL Edit]** i komponenten.

>[!NOTE]
>
>Som standard är videokomponenten i Dynamic Media adaptiv. Om du vill göra den till en fast storlek anger du den i komponenten med **[!UICONTROL Width]** och **[!UICONTROL Height]** i **[!UICONTROL Advanced]** -fliken.

* **[!UICONTROL Viewer preset]** - Välj en befintlig förinställning för visningsprogrammet för video i listrutan. Om den visningsförinställning du söker efter inte visas måste du göra den synlig. Se Hantera förinställningar för visningsprogram.

* **[!UICONTROL Viewer modifiers]** - Granskningsmodifierare har formen av `name=value` par med `&` avgränsare. De gör att du kan ändra visningsprogram enligt anvisningarna i referenshandboken för Adobe-visningsprogram. Ett exempel på en visningsmodifierare är `posterimage=img.jpg&caption=text.vtt,1`

  Med visningsmodifierare kan du till exempel göra följande:

   * Associera en bildtextfil med en video: [bildtext](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html)
   * Associera en navigeringsfil med en video: [navigering](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html)

     Du kan redigera följande avancerade inställningar genom att välja **[!UICONTROL Edit]** i komponenten.

* **[!UICONTROL Title]** - Ändra videons titel.

* **[!UICONTROL Width]** - Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

* **[!UICONTROL Height]** - Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

#### När du arbetar med smart beskärning {#when-working-with-smart-crop}

Använd Dynamic Media-komponenten för att lägga till bildresurser för Smart beskärning på dina webbsidor. När du redigerar komponenten kan du välja att använda en fördefinierad videovisningsförinställning för att spela upp videon på sidan.

Se [Använda Smart Crop med Experience Manager Assets Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use.html)

Se även [Bildprofiler](/help/assets/dynamic-media/image-profiles.md).

![Dynamic Media inställningar för smart beskärning](assets/dm-settings-smart-crop.png)

Du kan redigera följande Dynamic Media-inställningar genom att välja **[!UICONTROL Edit]** i komponenten.

>[!NOTE]
>
>Som standard är Dynamic Media-bildkomponenten adaptiv. Om du vill att den ska ha en fast storlek anger du det i komponenten på fliken **[!UICONTROL Advanced]** med **[!UICONTROL Width]** och **[!UICONTROL Height]**.

* **[!UICONTROL Image Modifiers]** - Du kan använda bildeffekter genom att ange fler bildkommandon. Dessa kommandon beskrivs i Bildförinställningar och i Referens för bildserverkommando.

  Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

  Du kan redigera följande avancerade inställningar genom att välja **[!UICONTROL Edit]** i komponenten.

* **[!UICONTROL Enable Aspect Ration match]** - Välj det här alternativet om du vill att Dynamic Media ska välja en smart beskärningsåtergivning med de proportioner som bäst matchar originalbildens proportioner.

* **[!UICONTROL Optimize for higher resolution devices]** - Markera (standard) kryssrutan för att tillåta optimering av DPR (Device Pixel Ratio).

  The **[!UICONTROL Optimize for higher resolution devices]** visas bara när följande är sant:

   * Under Förinställningstyp, **[!UICONTROL Smart Crop]** är markerat.

  ![inställning för enhetspixelproportioner för smart beskärning](/help/assets/dynamic-media/assets/dpr-smartcrop.png)

  Se även [Om optimering av enhetens pixelproportioner](/help/assets/dynamic-media/imaging-faq.md#dpr).

  Alla [!DNL Experience Manager] DPR-värden för Dynamic Media Smart Imaging ignoreras.

* **[!UICONTROL Title]** - Ändra titeln på bilden för smart beskärning.

* **[!UICONTROL Alt Text]** - Lägg till en titel i den smarta beskärningsbilden för de användare som har inaktiverat grafik.

  Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

* **[!UICONTROL URL, Open in]** - Du kan ange att en resurs ska öppna en länk. Ange URL:en och Öppna i anger om du vill att den ska öppnas i samma fönster eller i ett nytt fönster.

  Det här alternativet är inte tillgängligt om du visar bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar.

* **[!UICONTROL Width]** - Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

* **[!UICONTROL Height]** - Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

### Komponent: Interaktiva media {#interactive-media-component}

Komponenten Interactive Media är till för de resurser som har interaktivitet i dem, till exempel hotspot-områden eller bildscheman. Om du har en interaktiv bild, interaktiv video eller karusellbanderoll använder du **[!UICONTROL Interactive Media]** -komponenten.

Komponenten Interactive Media är smart. Oavsett om du lägger till en bild eller en video har du olika alternativ. Dessutom är visningsprogrammet responsivt - skärmstorleken ändras automatiskt baserat på skärmstorleken. Alla visningsprogram är HTML5-visningsprogram.

>[!NOTE]
>
>Om din webbsida har följande:
>
>* Flera instanser av komponenten Interactive Media används på samma sida.
>* Varje instans använder samma resurstyp.
>
>Det går inte att tilldela olika visningsprogramförinställningar till varje interaktiv mediekomponent på den sidan.
>
>Du kan dock använda samma visningsförinställning för alla interaktiva mediekomponenter som använder resurser av samma typ på sidan.

![chlimage_1-174](assets/chlimage_1-541.png)

Du kan redigera följande **[!UICONTROL General]** inställningar genom att välja **[!UICONTROL Edit]** i komponenten.

* **[!UICONTROL Viewer preset]** - Välj en befintlig visningsförinställning i listrutan. Om den visningsförinställning du söker efter inte visas måste du göra den synlig. Förinställningar för visningsprogram måste publiceras innan de kan användas. Se Hantera förinställningar för visningsprogram.

* **[!UICONTROL Title]** - Ändra videons titel.

* **[!UICONTROL Width]** - Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

* **[!UICONTROL Height]** - Ange värdet i pixlar om du vill att bilden ska ha en fast storlek. Om du lämnar det här värdet tomt anpassas resursen.

  Du kan redigera följande **[!UICONTROL Add To Cart]** inställningar genom att välja **[!UICONTROL Edit]** i komponenten.

* **[!UICONTROL Show Product Asset]** - Som standard är det här värdet valt. Produktresursen visar en bild av produkten enligt definitionen i modulen Handel. Avmarkera kryssrutan om du inte vill visa produktresursen.

* **[!UICONTROL Show Product Price]** - Som standard är det här värdet valt. Produktpriset visar priset för artikeln enligt definitionen i modulen Handel. Avmarkera kryssrutan om du inte vill visa produktpriset.

* **[!UICONTROL Show Product Form]** - Som standard är det här värdet inte markerat. Produktformuläret innehåller alla produktvarianter som storlek och färg. Avmarkera kryssrutan om du inte vill visa produktvarianterna.

### Komponent: Panoramabilder {#panoramic-media-component}

Komponenten för panoramamedia är avsedd för resurser som är sfäriska panoramabilder. Sådana bilder ger en 360-gradig visningsupplevelse av ett rum, en egenskap, en plats eller ett landskap. För att en bild ska kvalificeras som ett sfäriskt panorama måste den ha antingen ett ELLER båda av följande:

* Proportionerna 2:1.
* Taggad med nyckelorden `equirectangular` eller (`spherical` + `panorama`) eller (`spherical` + `panoramic`). Se [Använda taggar](/help/sites-cloud/authoring/features/tags.md).

Kriterierna för proportioner och nyckelord gäller även för panoramaresurser på sidan med resursinformation och för komponenten **[!UICONTROL Panoramic Media]** i innehållshanteringssystemet.

>[!NOTE]
>
>Om din webbsida har följande:
>
>* Flera instanser av **[!UICONTROL Panoramic Media]** som används på samma sida.
>* Varje instans använder samma resurstyp.
>
>Tilldela olika visningsprogramförinställningar till varje **[!UICONTROL Panoramic Media]** på den sidan stöds inte.
>
>Du kan dock använda samma visningsförinställning för alla panoramakomponenter som använder resurser av samma typ på sidan.

![Förinställning för visningsprogram för panoramabilder](assets/panoramic-media-viewer-preset.png)

Du kan redigera följande inställning genom att markera **[!UICONTROL Configure]** i komponenten.

* **[!UICONTROL Viewer Preset]** - Välj ett befintligt visningsprogram i listrutan med visningsförinställningar.

Om den visningsförinställning du söker efter inte visas kontrollerar du att den är publicerad. Publicera förinställningar för visningsprogrammet innan du använder dem. Se [Hantera visningsförinställningar](/help/assets/dynamic-media/managing-viewer-presets.md).

### Komponent: Video 360 Media {#video-media-component}

Använd **[!UICONTROL Video 360 Media]** för att återge ekvirektangulär video på webbsidan. På så sätt får du en engagerande tittarupplevelse av ett rum, en egendom, en plats, ett landskap eller en medicinsk procedur.

Vid uppspelning på en platt skärm har användaren kontroll över betraktningsvinkeln. för uppspelning på mobila enheter används vanligtvis de inbyggda gyroskopiska kontrollerna.

Visningsprogrammet har inbyggt stöd för leverans av 360 videomaterial. Som standard krävs ingen ytterligare konfiguration för visning eller uppspelning. Du levererar 360-video med standardvideotillägg som .mp4, .mkv och .mov. Den vanligaste kodeken är H.264.

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

Du kan redigera följande inställning genom att markera **[!UICONTROL Configure]** i komponenten.

* **[!UICONTROL Viewer Preset]** - Välj ett befintligt visningsprogram i listrutan med visningsförinställningar. Använd Video360VR för slutanvändare som använder virtuella verklighetsglasögon. Innehåller grundläggande videouppspelningskontroller och funktioner för sociala medier. Använd Video360_social som innehåller grundläggande videouppspelningskontroller. Videoåtergivning sker i stereoläge. Manuell vypunktskontroll är inaktiverad men gyroskopisk kontroll är aktiverad. Det finns inga funktioner för sociala medier.

Om den visningsförinställning du söker efter inte visas kontrollerar du att den är publicerad. Publicera förinställningar för visningsprogrammet innan du använder dem. Se [Hantera visningsförinställningar](/help/assets/dynamic-media/managing-viewer-presets.md).

### Använd HTTP/2 för att leverera Dynamic Media-material {#using-http-to-delivery-dynamic-media-assets}

HTTP/2 är det nya, uppdaterade webbprotokollet som förbättrar kommunikationen mellan webbläsare och servrar. Det ger snabbare överföring av information och minskar mängden processorkraft som behövs. Dynamic Media-material kan nu levereras via HTTP/2 vilket ger bättre respons och laddningstider.

Se [HTTP2-leverans av innehåll](/help/assets/dynamic-media/http2faq.md) om du vill ha fullständig information om hur du kommer igång med HTTP/2 med ditt Dynamic Media-konto.

>[!MORELIKETHIS]
>
>* [Använda videospelaren i Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-video-player-feature-video-use.html)
>* [Använd interaktiv video med Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-interactive-video-feature-video-use.html)
>* [Förstå resursvisningsprogrammet med Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/viewers/dynamic-media-viewer-feature-video-understand.html)
>* [Använd anpassad videominiatyr med Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-video-thumbnails-feature-video-use.html)
>* [Förstå färghantering med Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-color-management-technical-video-setup.html#dynamic-media)
>* [Använd bildskärpa med Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use.html)
