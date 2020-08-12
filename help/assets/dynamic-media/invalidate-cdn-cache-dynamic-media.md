---
title: Invalidera CDN-cachen med hjälp av Dynamic Media
description: Genom att du validerar ditt cachelagrade CDN-innehåll (Content Delivery Network) kan du snabbt uppdatera resurser som levereras av Dynamic Media, i stället för att vänta på att cachen ska förfalla.
translation-type: tm+mt
source-git-commit: aae3dcb0f44ef8e8d1401274fbf1fd47ea718b09
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 0%

---


# Invalidera CDN-cachen med hjälp av Dynamic Media {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

Dynamiska mediefiler cachas av CDN (Content Delivery Network) för snabb leverans till dina kunder. När du uppdaterar dessa resurser kanske du vill att ändringarna ska börja gälla omedelbart på webbplatsen. Genom att rensa eller göra CDN-cachen ogiltig kan du snabbt uppdatera resurser som levereras av Dynamic Media. I stället för att vänta på att cachen ska förfalla med ett TTL-värde (Time To Live) (standard är 10 timmar) kan du skicka en begäran från användargränssnittet i Dynamic Media om att cachen ska förfalla inom några minuter.

>[!IMPORTANT]
>
>Följande steg gäller bara för Dynamic Media på AEM som en Cloud Service. Du måste också använda det färdiga CDN som medföljer AEM Dynamic Media. Någon annan anpassad CDN stöds inte av den här funktionen. <!-- If you are using Dynamic Media in AEM 6.5, Service Pack 5 or earlier to invalidate the CDN cache [use the steps found here](/help/assets/invalidate-cdn-cache-dm-classic.md). -->

Se även Översikt över [cachelagring i Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Inaktivera CDN-cachen med hjälp av dynamiska medier**

*Del 1: Skapa en mall för CDN-invalidering*

1. In AEM as a Cloud Service, tap **[!UICONTROL Tools > Assets > CDN Invalidation Template.]**

   ![CDN-valideringsfunktion](/help/assets/assets-dm/cdn-invalidation-template.png)

1. Gör något av följande på **[!UICONTROL CDN Invalidation Template]** sidan baserat på ditt scenario:

   | Scenario | Alternativ |
   | --- | --- |
   | Jag har redan skapat en mall för CDN-validering med Dynamic Media Classic. | Textfältet är förifyllt med malldata **[!UICONTROL Create Template]** . I så fall kan du antingen redigera mallen eller fortsätta till nästa steg. |
   | Jag måste skapa en mall. Vad ska jag ange? | I **[!UICONTROL Create Template]** textfältet anger du en bild-URL (inklusive bildförinställningar eller modifierare) som refererar `<ID>`i stället för ett specifikt bild-ID som i följande exempel:<br><br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br><br>Om mallen bara innehåller `<ID>`fylls Dynamic Media i `https://<publishserver_name>/is/image` där `<publishserver_name>` är namnet på din Publish Server och `ID` är de valda resurserna som ska göras ogiltiga.<br><br>Endast bilder - d.v.s. `/is/image`-kan formateras automatiskt baserat på mallen. Om du till `/is/content/`exempel lägger till videoklipp eller PDF-filer med resursväljaren genereras inte URL-adresser automatiskt. I stället måste du ange sådana resurser antingen i CDN-valideringsmallen, eller så kan du manuellt lägga till URL:en till sådana resurser i *del 2: Ange alternativ* för CDN-validering.<br>Resursformat som stöds i Dynamic Media kan ogiltigförklaras. Resurser som PowerPoint eller rena textfiler stöds inte för CDN-ogiltigförklaring.<br>När du skapar mallen, men ser till att du är noggrann med syntax och typos; Dynamic Media utför ingen mallvalidering.<br>Följande mallexempel är endast för illustrationsändamål. |

   ![CDN-valideringsmall - Skapa](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. I det övre högra hörnet av sidan CDN-mall för validering trycker du på **[!UICONTROL Save]** och sedan på **[!UICONTROL OK]**.<br>

   ***Del 2: Ange alternativ för CDN-validering***
<br>

1. In AEM as a Cloud Service, tap **[!UICONTROL Tools > Assets > CDN Invalidation.]**

   ![CDN-valideringsfunktion](/help/assets/assets-dm/cdn-invalidation-path.png)

1. På **[!UICONTROL CDN Invalidation]** - **[!UICONTROL Add Details]** sidan väljer du resurser för CDN-ogiltigförklaring.

   ![CDN-validering - Lägg till information](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Om du bestämmer dig för att låta alternativen vara **[!UICONTROL Invalidate asset associated image presets in CDN]***och* **[!UICONTROL Invalidate based on template]** inte markerade, kommer bas-URL:en för de markerade resurserna att bli ogiltig. Du bör endast använda den här alternativa placeringen för bilder.


   | Alternativ | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Invalidate asset associated image presets in CDN]** | (Valfritt) När du markerar det här alternativet kan du välja en eller flera Dynamic Media-resurser, oavsett MIME-typ och deras associerade bildförinställningar för att göra cacheminnet ogiltigt.<br>Resurser och tillhörande fördefinierade URL:er för förinställningar formateras automatiskt för ogiltigförklaring. Det här alternativet fungerar endast för<br>bildresurser. Du kan välja en eller flera mappar som innehåller resurser, men Adobe rekommenderar inte det här tillvägagångssättet. Du bör i stället välja enskilda resursfiler. |
   | **[!UICONTROL Invalidation based on template]** | (Valfritt) Markera det här alternativet om du bara vill använda den definierade mallen för URL-formatering. |
   | **[!UICONTROL Add Assets]** | Använd Resursväljaren för att välja resurser som du vill göra ogiltiga. Du kan välja antingen publicerade eller opublicerade resurser.<br>Du kan få en tom lista när du lägger till resurser. Dynamic Media använder CDN-mallen Ovalidate för att automatiskt skapa en URL som gör CDN ogiltig. Om ingen mall för CDN-validering har skapats får du en tom lista.<br>Cachelagring vid CDN är URL-baserad, inte resursbaserad. Därför måste du vara medveten om de fullständiga URL:erna som finns på webbplatsen. När du har identifierat dessa URL-adresser kan du lägga till dem i mallen.Sedan kan du markera och lägga till dessa resurser och göra URL-adresserna ogiltiga i ett steg. Ett annat alternativ är att lägga till URL:er i CDN-valideringslistan. Om du föredrar det här arbetssättet behöver du inte markera och lägga till resurser innan du trycker **[!UICONTROL Next]** och sedan **[!UICONTROL Submit]** gör dem ogiltiga.<br>Använd det här alternativet tillsammans med **[!UICONTROL Invalidate asset associated image presets in CDN]**, eller **[!UICONTROL Invalidation based on template]**, eller båda. |
   | **[!UICONTROL Add URL]** | Lägg till eller klistra in fullständiga URL-sökvägar manuellt i Dynamic Media-resurser vars CDN-cache du vill ogiltigförklara. Använd det här alternativet om du inte har skapat en mall för CDN-validering i ***del 1: Arbeta med CDN-valideringsmallen*** och har bara ett fåtal resurser att ogiltigförklara.<br> |

1. Near the upper-right corner of the page, tap **[!UICONTROL Next]**.
1. På sidan **[!UICONTROL CDN Invalidation]** - **[!UICONTROL Confirm]** i **[!UICONTROL URLs]** listrutan visas en lista med en eller flera URL:er som genererats från den mall för CDN-validering som du skapade tidigare och de resurser som du nyss lade till.

   Anta till exempel att du har lagt till en resurs med namnet `spinset`när CDN-valideringsmallen redan har skapats. När du trycker på **[!UICONTROL Tools > Assets > CDN Invalidation]** det skapas följande fem genererade URL:er i **[!UICONTROL CDN Invalidation - Confirm]** användargränssnittet:

   ![CDN-validering - Bekräfta](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Om det behövs trycker du på **X** till höger om en URL för att ta bort den från invalideringsprocessen. Du kan ha upp till 1 000 URL-adresser vid en given tidpunkt.

1. I närheten av det övre högra hörnet av sidan trycker du för **[!UICONTROL Submit]** att starta CDN-invalideringsprocessen.

## Felsökning av CDN-valideringsfel

* Med den här funktionen kan du göra upp till 1 000 URL-adresser åt gången ogiltiga. Ett större tal än 1000 resulterar i ett fel som du kan lösa genom att ta bort URL-adresser på **[!UICONTROL CDN Invalidation – Confirm]** sidan.
* I samtliga fall bearbetas hela gruppen för att ogiltigförklaras, eller så misslyckas hela gruppen.

| Fel | Förklaring |
| --- | --- |
| *Det gick inte att hämta URL:er för valda resurser.* | Inträffar om något av följande scenarier uppfylls:<br>- Det går inte att hitta någon dynamisk mediekonfiguration.<br>- Det finns ett undantag när en tjänstanvändare hämtas genom vilket konfigurationen för dynamiska media läses.<br>- Publiceringsservern eller företagsroten som används för att skapa URL-adresserna saknas i Dynamic Media-konfigurationen. |
| *Vissa URL:er är inte korrekt definierade. Korrigera och skicka igen.* | Inträffar om invaliderings-API:t för IPS CDN-cachen returnerar ett fel om att URL:en refererar till ett annat företag eller om URL:en inte är giltig enligt den validering som görs av API:t för CdnCacheInvalidation. |
| *Det gick inte att göra CDN-cachen ogiltig.* | Inträffar om CDN-cachen ogiltigförklarar begäran av någon annan anledning. |
| *Inga URL:er har angetts som ogiltiga.* | Inträffar om det inte finns några URL:er i **[!UICONTROL CDN Invalidation – Confirm page]** och du trycker på **[!UICONTROL Submit]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->