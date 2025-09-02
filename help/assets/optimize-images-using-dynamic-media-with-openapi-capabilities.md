---
title: Optimera bilder med Dynamic Media med OpenAPI-funktioner
description: Lär dig optimera bilder i farten före offentlig leverans med hjälp av bildoptimeringsfunktionerna i Dynamic Media med OpenAPI-funktioner
role: Admin
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: 74c5fbda5ee1ad46b5fcab5ba89f0fd96873e3cf
workflow-type: tm+mt
source-wordcount: '1261'
ht-degree: 0%

---


# Optimera bilder med Dynamic Media med OpenAPI-funktioner{#Optimize-images-using-Dynamic-Media-with-OpenAPI-Capabilities}

[!DNL Dynamic Media with OpenAPI capabilities] erbjuder bildoptimeringsfunktioner som [!DNL Smart Crop], [!DNL Image Presets] och [!DNL Smart Imaging]. Dessa funktioner hjälper till att leverera högkvalitativa, responsiva bilder som läses in snabbt mellan olika enheter och nätverk.

## Smart beskärning{#smart-crop-using-dynamic-media-with-openapi-capabilities}

[Smart beskärning](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=smartcrop&t=request) är en dynamisk storleksändring av [!DNL Dynamic Media with OpenAPI capabilities]. [!DNL Smart Crop] är en avancerad bildbehandlingsteknik som använder AI-baserad innehållsmedveten beskärning för att på ett intelligent sätt beskära bilder för olika skärmstorlekar samtidigt som det visuella sammanhanget bevaras i beskurna versioner. AI analyserar bilden för att identifiera fokalpunkten eller den avsedda intressepunkten och beskär sedan automatiskt bilden så att fokalpunkten bibehålls i alla beskurna versioner. [!DNL Smart Crop], ett nyckelelement i responsiv design, är ett kostnadseffektivt och tidseffektivt sätt att beskära bilder.

Läs artikeln [Dynamiska mediebildprofiler](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles) om du vill lära dig hur du [skapar smarta beskärningsåtergivningar](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#creating-image-profiles) i [!DNL Admin View], [använder dem i mappar](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#applying-an-image-profile-to-folders) eller [redigerar återgivningar](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#editing-the-smart-crop-or-smart-swatch-of-a-single-image) som redan används i en bild eller i en mapp. Lär dig att skapa en [!DNL Smart Crop] steg för steg i den här [videon](https://experienceleague.adobe.com/sv/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use).

Parametern [!DNL Smart Crop] förväntar sig att det finns namngivna/smartcrop-profiler och att de har tillämpats på resursen. Läs [Smart Crop-profiler](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=smartcrop&t=request) om du vill veta mer om parametern [!DNL Smart Crop] och hur namngivna [!DNL Smart Crop]-profiler används.

>[!IMPORTANT]
>
> Du kan bara skapa [!DNL Smart Crop] återgivningar i administrationsvyn.

## Bildförinställningar{#image-presets-using-dynamic-media-with-openapi-capabilities}

Omforma bilder snabbt med funktionen [Bildförinställningar](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=preset&t=request) i [!DNL Dynamic Media with OpenAPI capabilities]. En [!DNL image preset] är en fördefinierad uppsättning storleks- och formateringsregler för en utdatabild.

[!DNL Dynamic Media with OpenAPI capabilities] använder förinställningsnamn för att omvandla en bild i farten och generera återgivningen direkt. När du begär en bild via en [!DNL Dynamic Media with OpenAPI]-leverans-URL som innehåller en förinställd parameter, använder [!DNL DM with OpenAPI] förinställningens omformningar, skapar återgivningen på begäran och skickar den till användaren.

Du kan använda en enda förinställning på flera bilder via deras [!DNL Dynamic Media with OpenAPI]-leveransadresser. På så sätt får du konsekvent formatering i alla resurser utan att behöva redigera var och en av dem manuellt.

Läs artikeln [Hantera bildförinställningar](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets) om du vill veta mer om [hur du skapar bildförinställningar i administratörsvyn](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets#creating-image-presets) och [hur du skapar responsiva bildförinställningar](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets#creating-a-responsive-image-preset) som automatiskt anpassar resurser så att de passar olika skärmstorlekar.

### Fördelar med att använda bildförinställningar{#benefits-of-image-presets}

[!DNL Image Presets] har flera fördelar med att hantera och leverera bilder i [!DNL Dynamic Media with OpenAPI]. Några av fördelarna är följande:

* Förinställningar gör att URL:er för bildleverans blir kortare. Använd en enda förinställning i stället för att lägga till flera bildmodifierare som gör leverans-URL:en längre. Kortare URL:er är enklare att hantera och säkerställa enhetlig bildleverans på webbplatser, i mobilappar, via e-post och i andra kanaler.
* Bildförinställningar skapar just-in-time-renderingar från en källbildfil. Denna funktion för återgivning på begäran eliminerar behovet av att skapa och lagra flera statiska återgivningar av samma fil, vilket sparar både tid och lagring.
* Använd en enda förinställning på en stor uppsättning resurser samtidigt, och slipp manuell redigering på varje resurs separat, vilket ger enhetlig formatering och möjliggör skalbarhet.
* När du uppdaterar en förinställnings parametrar formateras alla bilder som använder den förinställningen om automatiskt. Detta effektiviserar redigeringen genom att centralisera formateringsuppdateringarna, så att man slipper redigera enskilda resurser eller webbkod på nytt.
* Förbättrar effektiviteten och prestandan med dynamiska renderingar som cachas av CDN, vilket ger snabbare inläsning och optimerade prestanda på olika enheter och nätverk.

### Använda bildförinställningar{#use-image-presets-using-dynamic-media-with-openapi-capabilities}

När du har skapat [!DNL Image Presets] kan du använda dem för följande arbetsflöden:
* [Använd förinställningar i URL:en för bildleverans för att skapa återgivningar direkt innan de skickas till slutanvändaren](#use-presets-in-delivery-urls)
* [Använda förinställningar vid redigering i AEM Sites](#use-presets-during-authoring-in-aem-sites)

#### Använd förinställningar i URL för bildleverans{#use-presets-in-delivery-urls}

Med förinställningar blir URL:erna för leverans kortare och enklare att använda.  Varje förinställningsnamn fungerar som en unik identifierare i leveransadressen. I stället för att lägga till flera modifierare till en tillgångs leverans-URL ska du referera till förinställningsnamnet för att generera återgivningen omedelbart. [Lär dig hur du använder förinställningar för dynamiska mediabilder på din bild](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-presets).
I följande exempel jämförs en URL med en förinställning med en URL utan en förinställning.

**URL utan förinställning (lång URL)**:

`https://delivery-p30902-e145436-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:393d5579-5be2-49a5-ac5f-8fed72bfb614/as/AdobeStock_63266433.avif?width=400&height=300&fit=crop&qualit=85&sharpen=true`

**URL med en förinställning (kort URL)**:

`https://delivery-p30902-e145436-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:393d5579-5be2-49a5-ac5f-8fed72bfb614/as/AdobeStock_63266433.avif?preset=thumbnail`.
Den förinställda miniatyrbilden innehåller samma bildmodifieringsinställningar.

#### Använda förinställningar vid redigering i AEM Sites{#use-presets-during-authoring-in-aem-sites}

Författare kan välja [!DNL Image Presets] under sidredigering på [!DNL AEM Sites]-redigeringssidan när [!DNL Dynamic Media]-stöd är aktiverat.
Utför följande steg för att använda bildförinställningar på redigeringssidan:
1. Navigera till webbplatsredigeringssidan.
1. Utför stegen i avsnittet [Åtkomst till fjärrresurser i AEM Page Editor](/help/assets/integrate-remote-approved-assets-with-sites.md#access-remote-assets-in-aem-page-editor) för att använda panelen [!DNL Asset Selector] för att välja en resurs.
1. Bläddra nedåt till [!DNL asset selector] på panelen **[!UICONTROL &#x200B; Preset type]** och ange `Preset=Preset Name` i fältet **[!UICONTROL Image Modifiers]**.
   ![förinställning](/help/assets/assets/preset-in-asset-selector-panel.png)

## Smart bildbehandling{#use-smart-imaging-using-dynamic-media-with-openapi-capabilities}

När du använder [!DNL Dynamic Media with OpenAPI capabilities] för bildleverans optimeras bilderna automatiskt med [Smart bildbehandling](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/). Optimerad leverans gör att bilderna läses in snabbare, har maximal visuell kvalitet och minimal filstorlek. Detta ger snabb sidinläsning och konsekvent hög visuell kvalitet på olika enheter och nätverk, samtidigt som minimalt med bandbredd används, vilket gör webbplatsen snabbare och mer responsiv.

[!DNL Smart Imaging] innehåller följande funktioner:
* [Automatisk formatkonvertering](#auto-format-conversion)
* [Optimering av nätverksbandbredd](#network-bandwidth-optimisation)

### Automatisk formatkonvertering{#auto-format-conversion}

[!DNL Dynamic Media with OpenAPI] [konverterar automatiskt bilder till moderna, webboptimerade format som AVIF eller WEBP](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=auto-format&t=request). Konverteringen beror på webbläsarens funktioner och [licensberättigande](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-prime-ultimate), oavsett vilket format som efterfrågas.
AVIF- och WEBP-formaten ger bättre komprimering, vilket gör bilderna mindre och snabbare att leverera och läsa in. AVIF används som standardformat eftersom det hanterar alla webbläsarfunktioner.
[!DNL Dynamic Media with OpenAPI] använder frågeparametern `auto-format` för att styra webbläsarens beteende när en bild konverteras till olika format för optimerad leverans. Autoformatkonvertering inkluderar **automatisk befordran** och **automatisk degradering**. När systemet befordrar ett webboptimerat format (AVIF eller WEBP) över JPEG eller PNG för leverans, kallas det för autobefordran.

Frågeparametern `auto-format` är som standard inställd på `true`. När `auto-format` är aktiverat (true) ignorerar systemet det begärda formatet och väljer automatiskt ett webboptimerat format (AVIF eller WEBP) baserat på bildegenskaper, webbläsarfunktioner och [licensberättigande](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-prime-ultimate).

När `auto-format` är true skickar systemet bildformatet i följande sekvens:
* ***AVIF***: AVIF levereras om webbläsaren stöder det och licensen tillåter det. Detta kallas för autobefordran.
* ***WEBP***: WEBP levereras om AVIF inte stöds eller är licensierat. Det här är också automatisk befordran.
* ***JPEG***: JPEG levereras endast när AVIF och WEBP inte stöds och bilden inte har någon alfakanal (genomskinlighet). Detta kallas för automatisk degradering.
* ***PNG***: PNG levereras när webbläsaren inte stöder moderna format och bilden har alfakanal (genomskinlighet). Detta kallas även för automatisk degradering.

Inaktivera `auto-format` genom att ange frågeparametern till `false` och ange sedan det format som krävs för att få bilden levererad i det formatet.

### Optimering av nätverksbandbredd{#network-bandwidth-optimisation}

Bilderna optimeras automatiskt baserat på klientens nätverksförhållanden för att säkerställa snabbare leverans och smidig inläsning. Parametrarna [Kvalitet](#quality-parameter) och [Max-quality](#max-quality-parameter) justerar automatiskt kvaliteten genom att styra bildens komprimeringsnivåer, med värden mellan 1 och 100.

Se följande nyckelbeteenden för `quality` och `max-quality `parametrar:

* Om både [!DNL quality] och [!DNL max-quality] anges har [!DNL quality] företräde.
* Om bara [!DNL quality] anges levereras kvaliteten oavsett inläsningstid baserat på nätverkshastigheten.
* Om bara [!DNL max-quality] anges justeras bildkvaliteten automatiskt baserat på nätverksförhållanden, vilket ger bästa möjliga kvalitet upp till det angivna [!DNL max-quality]-värdet.
* Om inget av dem anges används dynamisk optimering med standardvärdet `max-quality` för `85`.

#### Kvalitetsparameter{#quality-parameter}

Kvalitetsparametern prioriterar bildkvalitet framför inläsningshastighet. Den korrigerar kvaliteten på utdatabilden till det begärda värdet (mellan 1 och 100) och ignorerar nätverksförhållandena. Läs mer om parametern [quality](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=quality&t=request).

#### Parametern Max-quality{#max-quality-parameter}

Maximal kvalitet balanserar bildkvalitet och inläsningstid baserat på klientens nätverkshastighet. Den prioriterar snabbare inläsningstider genom att sänka bildkvaliteten i långsammare nätverk samtidigt som den ger högsta möjliga kvalitet (1-100) för de angivna nätverksförhållandena. Läs mer om parametern [max-quality](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=quality&t=request).



