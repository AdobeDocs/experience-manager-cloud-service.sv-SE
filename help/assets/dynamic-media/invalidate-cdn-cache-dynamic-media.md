---
title: CDN-cachen har inte verifierats via Dynamic Media
description: '"Lär dig hur du ogiltigförklarar det cachelagrade innehållet i CDN (Content Delivery Network) så att du snabbt kan uppdatera resurser som levereras av Dynamic Media, i stället för att vänta på att cachen ska upphöra att gälla."'
feature: Asset Management
topic: Business Practitioner
role: Administrator,Business Practitioner
exl-id: c631079b-8082-4ff7-a122-dac1b20d8acd
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 0%

---

# CDN-cachen har inte verifierats med Dynamic Media {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

Dynamic Media-resurser cachas av CDN (Content Delivery Network) för snabb leverans till dina kunder. När du uppdaterar resurserna vill du dock att ändringarna ska börja gälla omedelbart på webbplatsen. Genom att rensa eller göra CDN-cachen ogiltig kan du snabbt uppdatera resurser som levereras av Dynamic Media. Du behöver inte längre vänta på att cachen ska förfalla med ett TTL-värde (Time To Live) (standard är tio timmar). Du kan i stället skicka en begäran från Dynamic Media-användargränssnittet om att cachen ska upphöra att gälla inom några minuter.

>[!NOTE]
>
>Den här funktionen kräver att du använder det färdiga CDN som medföljer Adobe Experience Manager Dynamic Media. Eventuellt annat anpassat CDN stöds inte med den här funktionen.

Se även [Översikt över cachelagring i Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Inaktivera CDN-cachen med Dynamic Media**

*Del 1 av 2: Skapa en mall för CDN-invalidering*

1. Tryck på **[!UICONTROL Tools > Assets > CDN Invalidation Template]** i AEM som Cloud Service.

   ![CDN-valideringsfunktion](/help/assets/assets-dm/cdn-invalidation-template.png)

1. Gör något av följande på **[!UICONTROL CDN Invalidation template]**-sidan baserat på ditt scenario:

   | Scenario | Alternativ |
   | --- | --- |
   | Jag har redan skapat en CDN-invalideringsmall med Dynamic Media Classic. | Textfältet **[!UICONTROL Create Template]** är förifyllt med malldata. I så fall kan du antingen redigera mallen eller fortsätta till nästa steg. |
   | Jag måste skapa en mall. Vad ska jag ange? | I textfältet **[!UICONTROL Create Template]** anger du en bild-URL (inklusive bildförinställningar eller modifierare) som refererar till `<ID>` i stället för ett specifikt bild-ID som i följande exempel:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Om mallen bara innehåller `<ID>` fylls Dynamic Media i `https://<publishserver_name>/is/image/<company_name>/<ID>` där `<publishserver_name>` är namnet på din publiceringsserver som definieras i Allmänna inställningar i Dynamic Media Classic. `<company_name>` är namnet på företagsroten som är associerad med den här AEM instansen, och `<ID>` är de valda resurserna via resursväljaren som ska ogiltigförklaras.<br>Alla inlägg av förinställningar/modifierare  `<ID>` kopieras som de är i URL-definitionen.<br>Endast bilder - d.v.s.  `/is/image`-kan formateras automatiskt baserat på mallen.<br>Om du till  `/is/content/`exempel lägger till videoklipp eller PDF-filer med resursväljaren genereras inte URL-adresser automatiskt. I stället måste du ange sådana resurser antingen i CDN-valideringsmallen, eller så kan du manuellt lägga till URL:en till sådana resurser i *del 2 av 2: Ange alternativ för CDN-validering*.<br>**Exempel:**<br> I det här första exemplet innehåller ogiltighetsmallen  `<ID>` tillsammans med resursens URL som har  `/is/content`. Till exempel, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media skapar URL:en baserat på den här sökvägen, där `<ID>` är de resurser som väljs via resursväljaren som du vill ogiltigförklara.<br>I det andra exemplet innehåller invalideringsmallen den fullständiga URL:en för resursen som används i dina webbegenskaper med  `/is/content` (inte beroende av resursväljaren). Exempel: `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` där ryggsäck är resurs-ID.<br>Resursformat som stöds i Dynamic Media kan ogiltigförklaras. Resursfiltyper som *inte* stöds för CDN-ogiltigförklaring är bland annat PostScript®, Encapsulated PostScript®, Adobe Illustrator, Adobe InDesign, Microsoft PowerPoint, Microsoft Excel, Microsoft Word och Rich Text Format.<br>När du skapar mallen, men ser till att du är noggrann med syntax och typos; Dynamic Media utför ingen mallvalidering.<br>Ange URL:er för smart beskärning av bilder antingen i den här CDN-valideringsmallen eller i  **[!UICONTROL Add URL]** textfältet i  *del 2: Ange alternativ för CDN-validering.*<br>**Viktigt:**Varje post i en CDN-valideringsmall måste finnas på en egen rad.<br>*Följande mallexempel är endast för illustrationsändamål.* |

   ![CDN-valideringsmall - Skapa](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. I det övre högra hörnet på sidan **[!UICONTROL CDN Invalidation template]** trycker du på **[!UICONTROL Save]** och sedan på **[!UICONTROL OK]**.<br>

   *Del 2 av 2: Ange alternativ för CDN-validering*
   <br>

1. Tryck på **[!UICONTROL Tools > Assets > CDN Invalidation]** i AEM som Cloud Service.

   ![CDN-valideringsfunktion](/help/assets/assets-dm/cdn-invalidation-path.png)

1. På sidan **[!UICONTROL CDN Invalidation]** - **[!UICONTROL Add Details]** markerar du resurserna för CDN-ogiltigförklaring.

   ![CDN-validering - Lägg till information](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Om du bestämmer dig för att inte markera alternativen **[!UICONTROL Invalidate asset associated image presets in CDN]** *och* **[!UICONTROL Invalidate based on template]** är bas-URL:en för de valda resurserna formgiven för ogiltigförklaring. Använd endast detta alternativ för bilder.


   | Alternativ | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Invalidate asset associated image presets in CDN]** | (Valfritt) När du markerar det här alternativet formateras markerade resurser och alla deras associerade förinställda URL:er automatiskt för cacheogiltigförklaring.<br>Resurser och tillhörande fördefinierade URL:er för förinställningar formateras automatiskt för ogiltigförklaring. Det här alternativet fungerar bara för bildresurser. |
   | **[!UICONTROL Invalidation based on template]** | (Valfritt) Markera det här alternativet om du bara vill använda den definierade mallen för URL-formatering. |
   | **[!UICONTROL Add Assets]** | Använd Resursväljaren för att välja resurser som du vill göra ogiltiga. Du kan välja antingen publicerade eller opublicerade resurser.<br>Cachelagring vid CDN är URL-baserad, inte resursbaserad. Därför måste du vara medveten om de fullständiga URL:erna som finns på webbplatsen. När du har fastställt dessa URL-adresser kan du lägga till dem i mallen. Sedan kan du markera och lägga till resurserna och göra URL-adresserna ogiltiga i ett enda steg. <br>Använd det här alternativet med  **[!UICONTROL Invalidate asset associated image presets in CDN]**, eller  **[!UICONTROL Invalidation based on template]**, eller båda. |
   | **[!UICONTROL Add URL]** | Lägg till eller klistra in fullständiga URL-sökvägar manuellt i Dynamic Media-resurser vars CDN-cache du vill ogiltigförklara. Använd det här alternativet om du inte skapade en CDN-valideringsmall i ***Del 1 av 2: Skapar en CDN-valideringsmall*** och har bara några resurser att ogiltigförklara.<br>**Viktigt:** Varje URL som du lägger till måste finnas på en egen rad.<br>Du kan göra upp till 1 000 URL-adresser ogiltiga samtidigt. Om antalet URL:er i textfältet **[!UICONTROL Add URL]** är större än 1000 kan du inte trycka på **[!UICONTROL Next]**. I sådana fall måste du trycka på **[!UICONTROL X]** till höger om en markerad resurs eller en manuellt tillagd URL för att ta bort den från ogiltiglistan.<br>Ange URL:er för smart beskärning av bilder antingen i CDN-valideringsmallen eller i det här  **[!UICONTROL Add URL]** textfältet. |

1. Tryck på **[!UICONTROL Next]** i sidans övre högra hörn.
1. På sidan **[!UICONTROL CDN Invalidation]** - **[!UICONTROL Confirm]** i listrutan **[!UICONTROL URLs]** visas en lista med en eller flera URL:er som genererats från CDN-valideringsmallen som du skapade tidigare och de resurser som du just lade till.

   Anta att du har lagt till en enskild resurs med namnet `spinset` med exemplet med mallen för CDN-invalidering som visades i stegen ovan. När du trycker på **[!UICONTROL Tools > Assets > CDN Invalidation]** resulterar det i följande fem genererade URL:er i **[!UICONTROL CDN Invalidation - Confirm]**-användargränssnittet:

   ![CDN-validering - Bekräfta](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Om det behövs trycker du på **X** till höger om en URL för att ta bort den från ogiltigförklaringsprocessen.

1. I närheten av det övre högra hörnet av sidan trycker du på **[!UICONTROL Submit]** för att påbörja CDN-invalideringsprocessen.

## Felsökning av CDN-valideringsfel

I samtliga fall bearbetas hela gruppen för att ogiltigförklaras, eller så misslyckas hela gruppen.

| Fel | Förklaring |
| --- | --- |
| *Det gick inte att hämta URL:er för valda resurser.* | Inträffar om något av följande scenarier uppfylls:<br>- Det går inte att hitta någon Dynamic Media-konfiguration.<br>- Det finns ett undantag när en tjänstanvändare hämtas genom vilket Dynamic Media-konfigurationen läses.<br>- Publiceringsservern eller företagsroten som används för att skapa URL-adresserna saknas i Dynamic Media-konfigurationen. |
| *Vissa URL:er är inte korrekt definierade. Korrigera och skicka om.* | Inträffar om invaliderings-API:t för IPS CDN-cache returnerar ett fel. Felet anger att URL:en refererar till ett annat företag eller att URL:en inte är giltig enligt den validering som görs av API:t för cdnCacheInvalidation i IPS. |
| *Det gick inte att göra CDN-cachen ogiltig.* | Inträffar om CDN-cachen ogiltigförklarar begäran av någon annan anledning. |
| *Inga URL:er har angetts som ogiltiga.* | Inträffar om det inte finns några URL:er på sidan **[!UICONTROL CDN Invalidation]** - **[!UICONTROL Confirm]** och du trycker på **[!UICONTROL Submit]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
