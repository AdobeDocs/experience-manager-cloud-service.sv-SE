---
title: God praxis i Dynamic Media
description: Läs om de bästa sätten att arbeta med bilder och video i Dynamic Media.
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Adaptive Streaming, Best Practices, Smart Imaging, Image Profiles, Rulesets, Viewers, Smart Crop, SEO Optimization, Publishing, Video, Renditions, Asset Management
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
exl-id: 39e491bb-367d-4c72-b4ca-aab38d513ac5
source-git-commit: 3375ffbb18c312e5df0050050ae16d75a12243e6
workflow-type: tm+mt
source-wordcount: '3574'
ht-degree: 0%

---

# Om metodtips i Dynamic Media{#about-dm-best-practices}

<!--**Organizations today must connect with their customers through an ever-growing array of channels and devices.** The customer experience spans physical stores, websites, mobile apps, social media, email, and e-commerce platforms. This diversity requires organizations to create many more versions of each piece of content. Personalization adds complexity by increasing the number of variations needed for each item. Despite budget constraints for content creation, there's still a need to produce more campaigns in the same timeframe, on a global scale. AEM Dynamic Media offers a comprehensive set of tools to meet these challenges, providing consistent, personalized, high-performance, and optimized brand experiences across all channels and devices. 

Key Features of AEM Dynamic Media:

* **Single File Approach:** Save on storage costs by storing just one master file. AEM Dynamic Media generates all size variations and visual effects on-demand, at the time of delivery, eliminating workflow complexity and last-minute creative changes.
* **Global Reach:** With Smart Imaging, images are automatically optimized during delivery, significantly reducing file size and page weight without sacrificing visual quality. This optimization is tailored for network bandwidth and device pixel ratio.
* **AI-Powered Efficiency:** Smart Crop uses AI to automate the cropping of images and videos, focusing on points of interest. This feature saves countless hours of manual editing and is designed for large-scale enterprise production.
* **Video Made Simple:** Upload a master video file and AEM Dynamic Media will adaptively stream it in multiple languages and with descriptive audio, ensuring a broad reach.
* **Customizable Experience Viewer:** Select, customize, and brand the experience viewers for images and videos with ease. These viewers can be seamlessly integrated into any digital experience.
* **Support for Emerging Formats:** AEM Dynamic Media is also your solution for delivering immersive 3D and panoramic experiences.

In the accompanying guide, you'll find a comprehensive list of best practices for maximizing the benefits of AEM Dynamic Media. As you embark on your Dynamic Media journey, make sure to consult these expert recommendations and resources.

Stage Business Problem Best Practice Recommendation: This section will outline specific business challenges and provide targeted best practices and recommendations to address them effectively. -->

Organisationer står inför en explosion av kanaler och enheter för att engagera användarna. Kundresan omfattar fysiska butiker, webben, mobiler, sociala medier, e-post och handel. Dynamic Media på Adobe Experience Manager (AEM) är en heltäckande lösning för att tillgodose detta behov. Det optimerar materialleveransen, hanterar personaliseringen och säkerställer enhetliga, prestandaanpassade och varumärkesanpassade upplevelser i alla kanaler och på alla enheter.

Några av huvudsatserna i Dynamic Media är följande:

* **En filmetod:** Med Dynamic Media lagrar du en primär källfil och alla storleksvariationer och visuella effekter skapas och optimeras dynamiskt vid leveransen. Det här sättet sparar lagringskostnader och eliminerar komplexiteten i arbetsflödet.
* **Helt global:** Smart Imaging, som används vid leverans av innehåll, minskar avsevärt bildstorleken och sidbredden utan att den visuella kvaliteten äventyras. Den är optimerad för nätverksbandbredd och enhetspixelproportioner.
* **AI-baserad:** Smart Crop, en AI-driven funktion, automatiserar beskärning av bilder och video. Det eliminerar manuell arbetsinsats och kan skalas effektivt för större företag.
* **Enkel video:** Ladda upp primära källvideor till Dynamic Media och strömma dem på olika språk med beskrivande ljud.
* **Experience Viewer Library:** Anpassa visningsprogram för varumärkesupplevelser för bilder och videor. De här tittarna kan smidigt integreras i era digitala upplevelser.
* **Stöd för nya format:** Med Dynamic Media kan du leverera 3D-upplevelser och panoramaupplevelser.

När du utforskar [Dynamic Media Journey](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-journey/dm-journey-part1)kan du få ut det mesta av programmets funktioner genom att läsa den konsoliderade listan med bästa praxis nedan. Anpassa dessa Dynamic Media bästa metoder efter era specifika sammanhang och projektbehov så att ni kan optimera upplevelserna över olika kanaler och enheter.

<!-- In Dynamic Media on AEM, there are sets of methods, techniques, and guidelines that can help you maximize the potential of your rich media content. These best practices can lead to optimal results and increase efficiency in your use of Dynamic Media. They represent the most efficient and effective courses of action in a particular situation. They also unlock high value for your audience and deliver high-quality, engaging content. -->

>[!IMPORTANT]
>
>Dynamic Media bästa praxis i den här artikeln kan förändras med tiden allt eftersom nya tekniker i Dynamic Media utvecklas. Informationen nedan gäller den senaste versionen av Dynamic Media.


## Importera material till Dynamic Media

**Affärsärende:** *Hantera effektivt stora volymer resurser och se till att endast relevant, godkänt innehåll levereras till slutanvändarna.*

Effektivisera hanteringen av stora mängder resurser. Se till att endast lämpligt, auktoriserat innehåll når slutanvändarna med Dynamic Media **Selektiv synkronisering** och **Selektiv publicering** funktioner.

* **Selektiv synkronisering:**
En proaktiv funktion som låter dig välja vilka resurser som ska synkroniseras med Dynamic Media. Du kan till exempel välja att bara synkronisera de mappar som innehåller resurser som har fått slutligt godkännande. Med det här arbetsflödet får ni kontroll över vilka resurser som förbereds för leverans till era kunder.

* **Selektiv publicering:**
När du har synkroniserat dina resurser får du med Selektiv publicering kontroll över vilka resurser som är synliga för dina kunder. Detta innebär att ni kan styra vilka godkända mediefiler som faktiskt levereras via era kanaler och se till att kunderna bara ser det bästa och mest relevanta innehållet.

Dessa två bästa metoder hjälper er att få bättre kontroll, styrning och produktivitet över ert multimediematerial.

Vill du veta mer? Gå till [Konfigurera selektiv publicering på mappnivå i Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).


## Förbered material för leverans

### Ordna dina resurser

**Affärsärende:** *Ordna material effektivt och effektivisera arbetsflödena.*

Använd en eller flera av följande metoder för effektiv resursorganisation som effektiviserar arbetsflöden:

* **Ordna resurser i mappar:**
När du organiserar resurser måste du kategorisera dem i mappar, ungefär som när du ordnar filer på en dator. För att resurshanteringen ska bli så effektiv som möjligt är det viktigt att du namnger, strukturerar undermappar och hanterar filer i dessa mappar. Implementering av systematiska namnkonventioner och metadatarutiner maximerar nyttan med ert digitala resurslager.
Vill du veta mer? Gå till [Ordna resurser i mappar](/help/assets/organize-assets.md#organize-using-folders).
* **Ordna resurser med taggar:**
Taggning av resurser förbättrar sökbarheten, skapar samlingar och rankar sökningar. Adobe Sensei AI använder en självlärande algoritm för exakt taggning, vilket möjliggör snabb hämtning av resurser. Adobe Sensei identifierar och tilldelar även relevanta taggar - inklusive anpassade taggar - till resurser, vilket förenklar resurshanteringen med automatisk, beskrivande taggning.
Vill du veta mer? Gå till [Ordna resurser med hjälp av taggar](/help/assets/organize-assets.md#use-tags-to-organize-assets).
* **Ordna resurser som samlingar:**
Med Dynamic Media och Experience Manager Assets kan du effektivt skapa, redigera och dela resurssamlingar mellan användare. Du kan skapa olika samlingstyper, bland annat statiska listor och dynamiska, sökbaserade kompileringar. De här samlingstyperna kan delas mellan olika platser med anpassningsbar åtkomst och redigeringsbehörighet.
Vill du veta mer? Gå till [Ordna resurser som samlingar](/help/assets/manage-collections.md).
* **Ordna resurser med hjälp av profiler:**
En bearbetningsprofil automatiserar hanteringen av resurser i särskilt angivna mappar och effektiviserar organisationen. Genom att standardisera metadata, filnamn och mappstrukturer kan du använda profilerna på ett konsekvent och exakt sätt när din digitala resurssamling utökas.
Vill du veta mer? Gå till [Ordna resurser med hjälp av profiler](/help/assets/organize-assets.md#organize-to-use-profiles).



### Optimera bildkvaliteten

**Affärsärende:** *Hämta bilder från Dynamic Media.*

För att förbättra bildkvaliteten måste du ta hänsyn till olika faktorer noga. Det kan vara en tidskrävande process. Det finns dock några beprövade metoder som kan hjälpa dig att uppnå önskvärda resultat. En del av de bästa sätten är att få optimal bildstorlek, bildskärpa och de bästa bildformaten att använda.

Vill du veta mer? Gå till [Bästa tillvägagångssätt för att optimera bildkvaliteten](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md).

Eftersom uppfattningen av bildkvaliteten varierar från människa till människa, kan ibland en systematisk undersökningsmetod vara nödvändig för att uppnå önskvärda resultat. Adobe Experience Manager hjälper dig med mer än 100 Dynamic Media-kommandon för bildförbättring.

Vill du veta mer? Titta [Dynamic Media Snapshot](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot) (3 minuter, 17 sekunder).

Om du vill utvärdera hur de olika kommandona påverkar bildkvaliteten kan du överföra en bild till Dynamic Media, använda verktygets gränssnitt på den angivna URL-adressen och använda de kommandon som du vill testa.

Vill du prova det? Starta [Dynamic Media Snapshot](https://snapshot.scene7.com/)

### Standardisera med format som används på bilder

**Affärsärende:** *Standardisera effektivt den stil och omformning som används på bildobjekten.*

Använd bildförinställningar regelbundet i Dynamic Media så att du kan justera bildstorlekar, format och egenskaper på ett konsekvent och dynamiskt sätt. Tänk på en bildförinställning som ett makro: det är en namngiven uppsättning kommandon för att ändra storlek och formatera. Om din webbplats till exempel behöver produktbilder i olika storlekar och format, med speciell komprimering för datorer och mobila enheter, kan du automatisera den här processen på ett effektivt sätt med Image Presets.

Vill du prova det? Gå till [Grundläggande om att skapa bildförinställningar för att återge resurser](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-e)

### Justera fokus och inramning för bilder och videor

**Affärsärende:** *Se till att huvudpunkten för mina bilder eller videor förblir i fokus på olika enheter.*

Smart Crop är en funktion i Dynamic Media som använder Adobe Sensei, Adobe AI och maskininlärningsramverk för att automatisera beskärningen av bilder och videor. Det identifierar och fokuserar på huvudmotivet eller intressepunkten i en bild eller video på ett intelligent sätt. Denna intelligens ser till att fokalpunkten bibehålls i olika skärmstorlekar på stationära datorer och mobila enheter.

Ett tips är att skapa en bildprofil med Smart beskärning. I profilen kan du definiera olika skärmstorlekar och låta Adobe Sensei göra resten, så att dina bilder och videor alltid är optimerade för visningsprogrammets enhet.

Vill du veta mer? Titta [Använda Smart Crop med AEM Assets Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use) (6 minuter, 35 sekunder) och [Använda Dynamic Media Smart Crop för video](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-smart-crop-video) (6 minuter, 22 sekunder).

### Förbättra SEO-rankningarna

**Affärsärende:** *Konfigurera Dynamic Media för förbättrad SEO-rankning.*

Använd följande rekommendationer regelbundet för att säkerställa att dina bilder bidrar effektivt till den övergripande SEO-strategin.

* **Bildfilsnamn:**
Använd beskrivande filnamn som återspeglar bildinnehållet. Exempel:
   * use `myCompany-Silver-Wrist-Watch`
   * *undvik* `myCompany_Silver_Wrist_Watch` eller `myCompanySilverWristWatch`

  Om du gör det blir det lättare för sökmotorer att förstå bildkontexten och det blir enklare att välja sökmotoroptimering. Google föredrar bindestreck framför understreck och blanksteg i ett filnamn. Undvik också att sammanfoga ord i ett filnamn.
* **Anpassad domän:**
Implementera en anpassad domän som innehåller ert företags- eller varumärkesnamn för att förstärka varumärkesigenkänningen och förtroendet. Exempel:
   * use `http://images.mycompany.com/is/image/companyname/`
   * *undvik* `https://s7d1.scene7.com/is/image/folder/AdobeStock_28563982`
* **Sökvänlig mappstruktur:**
Organisera bilderna i en mappstruktur som innehåller företagets namn eller varumärke för bättre indexering, som `http://images.mycompany.com/is/image/companyname/`.
* **Dynamic Media regeluppsättningar:**
Lär dig hur du villkorligt kan omvandla URL:er baserat på olika faktorer, vilket förbättrar SEO och användarupplevelsen.
Vill du veta mer? Gå till [Använd regeluppsättningar för att omforma URL:er](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md).
* **Smart bildbehandling och smart beskärning:**
Använd funktionerna för smart bildbehandling och smart beskärning i Dynamic Media för att hantera optimerade och responsiva bilder. Detta förbättrar inte bara sidinläsningstiden utan bidrar också positivt till SEO-rankningarna.
Vill du veta mer? Gå till [Smart bildbehandling](/help/assets/dynamic-media/imaging-faq.md), eller bevaka [Använda Smart Crop med AEM Assets Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use) (6 minuter, 35 sekunder).

Kom ihåg att de här bästa sätten är anpassade efter Google metoder för SEO för bilder. Sådana metoder betonar vikten av att ge kontext och tydlighet till sökmotorer genom lämpliga namnkonventioner, strukturerade data och optimerad bildleverans.

Vill du veta mer? Gå till [Bästa praxis för URL-struktur för Google](https://developers.google.com/search/docs/crawling-indexing/url-structure) och [Bästa praxis för SEO för Google-bilder](https://developers.google.com/search/docs/appearance/google-images)


### Förbättra bilder dynamiskt och skapa visuella effekter med kommandon

**Affärsärende:** *Lägg in visuella effekter i bilderna.*

Dynamic Media har en uppsättning kommandon för att redigera bilder och skapa visuella effekter dynamiskt, utan att behöva använda flera statiska resurser. Nedan följer några korta förklaringar av några av dessa processer och några exempel som kan vägleda dig:

#### Effekter i källbilden

| Uppgift | Vad du ska göra |
| --- | --- |
| **Överför och publicera originalbilden** | ・ Börja med att ladda upp originalbilden till Dynamic Media.<br>・ Kontrollera att den är publicerad och tillgänglig via en URL.<br>・ I det här exemplet överförs en stockbild av en klocka med vit bakgrund (vi kallar den &quot;Bild X&quot;) till Dynamic Media.<br>[https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer](https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer) |
| **Skapa en mask** | ・ Skapa en mask som definierar motivet (det område där du vill använda effekter) och bakgrunden (det område som du vill ändra).<br>[https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer-maskps](https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer-maskps)<br>・ Masker är vanligen gråskalebilder, där vitt representerar motivet och svart representerar bakgrunden. Du kan skapa masker med verktyg som Adobe Photoshop.<br>Vill du veta mer? Gå till [Skapa och redigera en snabbmask i Photoshop](https://helpx.adobe.com/in/photoshop/using/create-temporary-quick-mask.html).<br>・ För&quot;Bild X&quot; skapar du en mask som exakt markerar det motiv du vill förbättra. Exempel: en person, ett objekt och så vidare. |
| **Använd Dynamic Media URL-kommandon för effekter** | När du har skapat masken använder du URL-kommandon för att lägga på effekter som skuggor eller ändra bakgrundsfärgen till &quot;Bild X&quot;. Här är två exempel:<br><br> ・ **Skugga:**<br> Om du vill lägga till en skuggeffekt längs objektets gräns redigerar du URL-adressen så här:<br>[https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&amp;maskUse=invert&amp;effect=-1&amp;pos=100,100&amp;op_blur=75&amp;op_grow=1&amp;opac=25](https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&amp;maskUse=invert&amp;effect=-1&amp;pos=100,100&amp;op_blur=75&amp;op_grow=1&amp;opac=25)<br>I den här URL:en `$shadow$` skapar skuggeffekten, och `color=0,0,0` anger att skuggfärgen ska vara svart.<br>・ **Ändring av bakgrundsfärg:**<br> Om du vill ändra bakgrundsfärgen använder du URL-adressen med ett annat bakgrundsfärgvärde:<br>[https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&amp;maskUse=invert&amp;maskUse=invert&amp;color=255,255,0](https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&amp;maskUse=invert&amp;maskUse=invert&amp;color=255,255,0)<br> I detta exempel `color=255,255,0` anger att bakgrundsfärgen ska vara gul. Redigera bakgrunden till en viss färg för visuell påverkan. |

#### Lägga till en bildkant

Med Dynamic Media kan du hantera bilder direkt via webbadresser, vilket gör det till ett kraftfullt verktyg för att skapa dynamiska digitala upplevelser. Här följer några exempel. Vi börjar med följande ursprungliga bild-URL: [https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel).

| Uppgift | Vad du ska göra |
| --- | --- |
| **Vit kantlinje** | Använd följande URL för att lägga till en vit kantlinje:<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10)<br>I den här URL:en `extend=10,10,10,10` parameter anger kantstorleken på tio pixlar på alla sidor. |
| **Oskärpa längs den vita kanten** | Om du vill lägga till en oskärpeeffekt längs den vita kanten kan du redigera URL-adressen på följande sätt:<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;op_blur=60&amp;color=0,0,0](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;op_blur=60&amp;color=0,0,0)<br>I den här URL:en `effect=-1` parametern använder oskärpeeffekten, och `op_blur=60` styr oskärpeintensiteten. |
| **Skugga längs den yttre gränsen** | Använd den här URL:en om du vill lägga till en skuggeffekt längs den yttre gränsen:<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;$shadow$&amp;color=0,0,0](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&amp;extend=10,10,10,10&amp;effect=-1&amp;$shadow$&amp;color=0,0,0)<br>The `$shadow$` skapar skuggeffekten, och `color=0,0,0` anger att skuggfärgen ska vara svart. |

Experimentera fritt med dessa URL:er för att få de visuella effekter du vill.

#### Skapa bildövertäckningar

Om du vill lägga en logotyp eller ikon ovanpå en befintlig bild är Dynamic Media ett enkelt sätt att uppnå detta med hjälp av URL-kommandon. Vi bryter ned stegen.

| Steg | Vad du ska göra |
| --- | --- |
| **Överför och publicera basbilden** | Ladda först upp och publicera den basbild som du vill lägga logotypen eller ikonen ovanpå. Du kan använda vilken bild som helst som bas.<br>Här är till exempel en basbild:<br>[https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa). |
| **Överför och publicera logotypen eller ikonbilden** | Ladda sedan upp och publicera bilden som du vill lägga ovanpå basbilden. Den här bilden ska vara en genomskinlig PNG-bild med den logotyp eller ikon som du vill täcka över.<br>Här är den genomskinliga PNG-bilden för ett stjärnobjekt med genomskinlighetseffekter som kommer att läggas ovanpå:<br>[https://s7g2.scene7.com/is/image/genaibeta/decorate-star](https://s7g2.scene7.com/is/image/genaibeta/decorate-star) |
| **Använd Dynamic Media URL** | Skapa nu en Dynamic Media-URL som kombinerar basbilden med logotypen eller ikonbilden. Du kan använda URL-kommandon för att uppnå den här effekten.<br>URL-strukturen ser ut ungefär så här:<br>[https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa?layer=1&amp;src=decorate-star&amp;scale=1.25&amp;posN=0.33,-.25&amp;fmt=png](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa?layer=1&amp;src=decorate-star&amp;scale=1.25&amp;posN=0.33,-.25&amp;fmt=png)<br>där<br>・ `hotspotRetailBaseImage` är basbilden.<br>・ `starxp` är logotypen/ikonbilden.<br>・ `layer=1` anger att logotypen eller ikonen ska placeras i lager över basbilden.<br>・ `scale=1.25` justerar storleken på logotypen/ikonen.<br>・ `posN=0.33,-.25` anger logotypens/ikonens position i förhållande till basbilden.<br>・ `fmt=png` säkerställer att utdata är i PNG-format. |

Vad ska jag lära dig mer? Gå till [src](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-src) om du vill ha mer information om `src` och andra Dynamic Media URL-kommandon.


#### Ersätta kampanjtext

Nedan beskrivs stegen för att täcka över ett reklamtextmeddelande på en bild med HTML och CSS.

| Steg | Vad du ska göra |
| --- | --- |
| **Överför och publicera basbilden** | Ladda först upp och publicera den basbild som du vill lägga över texten på. Du kan använda vilken bild du vill. Här är ett exempel på en basbild:<br>[https://s7g2.scene7.com/is/image/genaibeta/leather-sofa](https://s7g2.scene7.com/is/image/genaibeta/leather-sofa)<br> |
| **Använda Dynamic Media-textoperatorer** | Med Dynamic Media kan du använda textoperatorer för att täcka över dynamisk text direkt i bilden. Följande exempel-URL visar på detta:<br>[https://s7g10.scene7.com/is/image/genaibeta/leather-sofa?layer=1&amp;posN=-0.3,-0.455&amp;text=%7b\rtf1\ansi%7b\fonttbl%7b\f0+Arial;%7d%7d%7b\colortbl+\red255\green255\blue255;%7d\copyfit1000\vertalc\qc%7b\cf0\fs42+New+Collection%7d%7d&amp;size=370,70&amp;textAttr=130&amp;bgcolor=FF3 333&amp;wid=600&amp;hei=600](https://s7g10.scene7.com/is/image/genaibeta/leather-sofa?layer=1&amp;posN=-0.3,-0.455&amp;text=%7b\rtf1\ansi%7b\fonttbl%7b\f0+Arial;%7d%7d%7b\colortbl+\red255\green255\blue255;%7d\copyfit1000\vertalc\qc%7b\cf0\fs42+New+Collection%7d%7d&amp;size=370,70&amp;textAttr=130&amp;bgcolor=FF3 333&amp;wid=600&amp;hei=600) |

#### Storleksändring och beskärning för olika användningsområden

##### Grundläggande om storleksändring av bilder

När du ändrar storlek på en bild måste du ändra bildens mått, upplösning och filstorlek. Här är några viktiga saker att tänka på:

* **Pixeldisposition:**
Digitala bilder består av små punkter som kallas pixlar. När en bild skapas har den ett visst antal pixlar. Att ändra storlek innebär att lägga till eller ta bort pixlar för att ändra bildens mått, upplösning och filstorlek.
* **Proportioner:**
Att bibehålla proportionerna (förhållandet mellan bredd och höjd) är avgörande för att förhindra förvrängning. Vare sig du gör en bild större (uppskalning) eller mindre (nedskalning) kan du bevara proportionerna för att säkerställa visuell enhetlighet.
* **Kvalitetsaspekter:**
Storleksändring kan påverka bildkvaliteten. Undvik drastisk uppskalning eftersom det kan leda till pixelering. Överväg i stället att återge bilden med en större storlek och upplösning. För mindre bilder använder du lämpliga verktyg för att behålla upplösningen.

##### Beskära jämfört med att ändra storlek

Beskärning och storleksändring är tekniker i Dynamic Media som gör att du kan omforma bilder så att de passar olika användningsområden, oavsett om du skapar miniatyrer, produktvisningsbilder eller banners.

* **Beskärning:**
Involverar borttagning av en del av en bild för att ändra dess komposition och ramning. Den ändrar inte de övergripande dimensionerna utan fokuserar på ett visst område.
* **Storleksändring:**
Justerar hela bildens mått, upplösning och filstorlek samtidigt som proportionerna behålls.

Låt oss titta på ett exempel som innehåller följande bild av vardagsrummet:

* **Ursprunglig bild i vardagsrummet:**
  [https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa)
* **Miniatyrbild (200 x 200 px):**
En mindre version som passar för snabb inläsning eller visning.
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;fit=crop)
* **Miniatyrbild med beskärning (200 px x 200 px):**
Beskuren för att fokusera på soffområdet.
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;cropN=.24,.24,.6,.72&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&amp;hei=200&amp;cropN=.24,.24,.6,.72&amp;fit=crop)
* **Produktvisningsbild (800 x 600 px):**
Beskuren och storleksändrad för att visa upp soffan.
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=800&amp;hei=600&amp;cropN=.24,.24,.6,.72&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=800&amp;hei=600&amp;cropN=.24,.24,.6,.72&amp;fit=crop)
* **Banderoll (1720 px x 820 px):**
Härledd från originalbilden, vilket betonar rummet.
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=1720&amp;hei=820&amp;cropN=0,.1,1,1&amp;fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=1720&amp;hei=820&amp;cropN=0,.1,1,1&amp;fit=crop)

Experimentera med olika varianter efter just dina behov.
Vill du veta mer om de kommandon som finns i en URL? Gå till [Kommandoreferens](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference).

### Publicera en video för min webbplats

**Affärsärende:** *Publicera snabbt en video för en marknadsföringswebbplats.*

* **Välj en videoprofil:**
I Dynamic Media bör du först välja en lämplig videoprofil. Du kan välja *Adaptiv videokodning* profil som är tillgänglig i AEM Assets under Videoprofiler. Dessa fördefinierade kodningsinställningar säkerställer att videon är optimerad för uppspelning på olika enheter och under olika bandbreddsförhållanden. Du kan också skapa en egen adaptiv videoprofil.
* **Tilldela profilen:**
Tilldela den valda videoprofilen till de mappar där videon ska överföras. Detta steg säkerställer att rätt kodningsinställningar används under överföringsprocessen.
* **Ladda upp originalvideon:**
Överför den ursprungliga videofilen. Se till att det är en högupplöst video med hög kvalitet. Ju bättre källvideo, desto bättre slutresultat.
* **Förhandsgranska och publicera:**
Förhandsgranska videon så att du kan vara säker på att allt ser ut som förväntat. När du är nöjd publicerar du den. Det här steget gör videon tillgänglig för din publik.
* **Länka eller bädda in:**
Efter publiceringen har du två alternativ.
   * **Länka direkt:**
Använd den angivna URL:en för att länka direkt till videon. Hyperlänka det på rätt sätt på er marknadsföringswebbplats.
   * **Bädda in videon:**
Kopiera inbäddningskoden och klistra in den HTML på webbsidan där du vill att videon ska visas. Om du gör det kan videon spelas upp direkt på din webbplats.

Vill du veta mer? Gå till [Video](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/video).

### Konfigurera videoklipp för optimal kvalitet och engagemang

**Affärsärende:** *Ställ in videor för bästa kvalitet och engagemang.*

För att säkerställa bästa kvalitet och engagemang för dina videor bör du implementera en kombination av följande strategier för bästa praxis:

* **Använd det inbyggda HTML5-visningsprogrammet:**
Förinställningarna för videovisningsprogrammet för Dynamic Media HTML5 är robusta videospelare. Använd dem för att undvika vanliga problem med HTML 5-videouppspelning och mobila enheter.
Dessa förinställningar åtgärdar utmaningar som strömning med adaptiv bithastighet och begränsad räckvidd för datorwebbläsare.
Vill du veta mer? Gå till [Bästa tillvägagångssätt: Använda videovisningsprogrammet för HTML 5](/help/assets/dynamic-media/video.md#best-practice-using-the-html-video-viewer).

* **Använd Dynamic Media videoprofiler:**
Videoprofiler i Dynamic Media hjälper till med effektiv videohantering, jämn kvalitet och adaptiv strömning.
Vill du veta mer? Gå till [Dynamic Media videoprofiler](/help/assets/dynamic-media/video-profiles.md).

* **Följ bästa praxis för videokodning:**
Använd videokodningsprofiler som bibehåller den ursprungliga videokvaliteten utan alltför stor nedskalning under kodningen.
Vill du veta mer? Gå till [Bästa tillvägagångssätt för att koda videofilmer](/help/assets/dynamic-media/video.md#best-practices-for-encoding-videos).

* **Använd adaptiv strömning i stället för progressiv strömning:**
Adaptiv strömning justerar videokvaliteten baserat på tittarens internetanslutning och enhetens funktioner.
Den använder protokoll som HLS (HTTP Live Streaming) eller DASH (`Dynamic Adaptive Streaming over HTTP`) för optimal uppspelningskvalitet.
Till skillnad från progressiv direktuppspelning, som levererar videoklipp linjärt, minimerar adaptiv direktuppspelning buffring och ger en smidig visningsupplevelse.

* **Aktivera DASH på ditt konto (Digital Adaptive Streaming over HTTP):**
DASH levererar dynamiskt videomaterial genom adaptiv strömning.
Om du vill aktivera DASH skapar du en supportbiljett för din miljö.
Vill du veta mer? Gå till [Aktivera DASH på ditt Dynamic Media-konto](/help/assets/dynamic-media/video.md#enable-dash).

### Internationalisering av videor för flerspråkig användning

**Affärsärende:** *Gör videor färdiga för flerspråkig användning.*

Internationalisering av videor för flerspråkig konsumtion är nödvändigt för att nå en global publik. Dynamic Media har funktioner som kan hjälpa dig att uppnå detta.

* **Ladda upp dina videor:**
   * Skapa först en videokodningsprofil. Du kan antingen använda den fördefinierade adaptiva videokodningsprofilen som medföljer Dynamic Media eller skapa en egen anpassad profil.
   * Associera videobearbetningsprofilen med en eller flera mappar där du överför dina primära källvideofilmer.
   * Överför dina primära källvideor till dessa mappar. Dynamic Media kodar dem baserat på den tilldelade videobearbetningsprofilen.
   * Dynamic Media har främst stöd för videoklipp i kort form (upp till 30 minuter) med en lägsta upplösning som är högre än 25 × 25. Videofiler på upp till 15 GB kan laddas upp1 vardera.

* **Hantera videoklipp:**
   * Ordna, bläddra bland och sök videomaterial i AEM.
   * Förhandsgranska och publicera videomaterial.
   * Visa källvideon och dess kodade återgivningar tillsammans med tillhörande miniatyrbilder.
   * Redigera videoegenskaper som titel, beskrivning och taggar2.

* **Lokalisering:**
   * Skapa ljudspår och undertexter för varje målområde/språk.
   * Lägg till dessa ljud- och undertextspår i videoklipp från AEM.
   * När användarna spelar upp videoklippen kan de välja vilket språk som ska användas för ljud och undertexter.

* **Publicering:**
   * Om du använder AEM som Web Content Management-system (WCM) kan du lägga till videor direkt på dina webbsidor.
   * Om du använder ett WCM-system från tredje part kan du länka eller bädda in videor på dina webbsidor med hjälp av URL:er eller inbäddningskoder.

Vill du veta mer? Gå till [Stöd för flera bildtexter och ljudspår för videofilmer i Dynamic Media](/help/assets/dynamic-media/video.md#about-msma) eller bevaka [Lägga till flera bildtexter och ljudspår i en video](https://delivery-p106302-e1008131.adobeaemcloud.com/adobe/assets/urn:aaid:aem:daf9a222-9f7f-4333-b167-98cb4c63a1f8/play) (1 minut, 41 sekunder).


## Leverera resurser till kunder

### Optimera bildstorlekar och minimera sidinläsningstider

**Affärsärende:** *Optimera storleken på bilder för alla webbläsare och skärmar och minska sidinläsningstiden.*

Dynamic Media Smart Imaging är ett kraftfullt verktyg som förbättrar bildleveransen genom att automatiskt optimera bildens format, storlek och kvalitet baserat på klientens webbläsarfunktioner.

Adobe rekommenderar att du använder funktionerna i Smart Imaging i stället för att ställa in bildformatet manuellt till `webp` eller `avif`. Här är varför:

* **Webbläsarkompatibilitet:**
Smart Imaging säkerställer att det levererade bildformatet är kompatibelt med användarens webbläsare.
* **Optimal komprimering:**
Det väljer det bästa formatet för komprimering baserat på webbläsaren, nätverksförhållandena och skärmupplösningen.
* **Moderna format:**
while `avif` är ett nyare format som ger bättre komprimering och som ännu inte stöds av alla webbläsare.
* **God praxis:**
För att garantera det bästa webboptimerade formatet kan du lita på att Smart Imaging gör formatvalet i stället för att använda kommandona manuellt `fmt=webp` eller `fmt=avif`.

Genom att förlita dig på Smart Imaging kan du se till att dina bilder levereras på ett så effektivt sätt som möjligt, skräddarsytt efter varje användares webbläsarmiljö. Den här metoden förenklar processen och kan leda till bättre prestanda i fråga om bildinläsningstider och övergripande användarupplevelse.

Vill du veta mer? Gå till [Smart bildbehandling](/help/assets/dynamic-media/imaging-faq.md).
