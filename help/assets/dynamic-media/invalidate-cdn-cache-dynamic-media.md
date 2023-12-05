---
title: Invalidera Content Delivery Network-cachen med Dynamic Media
description: Lär dig hur du ogiltigförklarar det cachelagrade innehållet i CDN (Content Delivery Network) så att du snabbt kan uppdatera resurser som levereras av Dynamic Media, i stället för att vänta på att cachen ska upphöra att gälla.
contentOwner: Rick Brough
feature: Asset Management
role: Admin,User
exl-id: c631079b-8082-4ff7-a122-dac1b20d8acd
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '1310'
ht-degree: 0%

---

# Invalidera CDN-cachen med Dynamic Media {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

Dynamic Media-resurser cachas av CDN (Content Delivery Network) för snabb leverans till dina kunder. När du uppdaterar resurserna vill du dock att ändringarna ska börja gälla omedelbart på webbplatsen. Genom att rensa eller göra CDN-cachen ogiltig kan du snabbt uppdatera resurser som levereras av Dynamic Media. Du behöver inte längre vänta på att cachen ska förfalla med ett TTL-värde (Time To Live) (standard är tio timmar). Du kan i stället skicka en begäran från Dynamic Media-användargränssnittet om att cachen ska upphöra att gälla inom några minuter.

>[!NOTE]
>
>Den här funktionen kräver att du använder det Adobe-paketerade CDN som medföljer Adobe Experience Manager Dynamic Media. Andra anpassade CDN stöds inte med den här funktionen.

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

Om du har aktiverat [Smart bildbehandling](/help/assets/dynamic-media/imaging-faq.md) på ditt konto och du använder det Adobe-paketerade CDN, kan du rensa alla URL:er med olika frågesträngar genom att rensa den enda bas-URL:en.

Till exempel ogiltigförklara `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image`blir även följande URL:er ogiltiga:

* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image`
* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image?wid=300`
* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image?$PLP$`
* och så vidare.

Detta ogiltigförklarande gäller dock inte för generiska domäner som saknar stöd för Smart Imaging, som `s7d1.scene7.com`. Sådana domäner behöver fortfarande den fullständiga URL:en för att ogiltigförklaras.

**Så här gör du CDN-cachen ogiltig via Dynamic Media:**

*Del 1 av 2: Skapa en mall för CDN-invalidering*

1. I Adobe Experience Manager as a Cloud Service går du till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL CDN Invalidation Template]**.

   ![CDN-valideringsfunktion](/help/assets/assets-dm/cdn-invalidation-template.png)

1. På **[!UICONTROL CDN Invalidation template]** gör du något av följande alternativ baserat på ditt scenario:

   | Scenario | Alternativ |
   | --- | --- |
   | Jag har redan skapat en CDN-invalideringsmall med Dynamic Media Classic. | The **[!UICONTROL Create Template]** textfältet är förifyllt med malldata. I så fall kan du antingen redigera mallen eller fortsätta till nästa steg. |
   | Jag måste skapa en mall. Vad ska jag ange? | I **[!UICONTROL Create Template]** anger du en bild-URL (inklusive bildförinställningar eller modifierare) som refererar till `<ID>`i stället för ett specifikt bild-ID, som i följande exempel:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Om mallen innehåller bara `<ID>`fylls sedan Dynamic Media i `https://<publishserver_name>/is/image/<company_name>/<ID>` där `<publishserver_name>` är namnet på den publiceringsserver som definieras i Allmänna inställningar i Dynamic Media Classic. The `<company_name>` är namnet på den företagsrot som är associerad med den här Experience Manager-instansen, och `<ID>` är de valda resurserna via tillgångsväljaren som ska ogiltigförklaras.<br>Eventuella förinställningar/modifieringar som följer `<ID>` kopieras som de är i URL-definitionen.<br>Endast bilder - det vill säga, `/is/image`-kan formateras automatiskt baserat på mallen.<br>För `/is/content/`Om du lägger till resurser som videor eller PDF med resursväljaren genereras inte URL-adresser automatiskt. I stället måste du ange sådana resurser antingen i CDN-valideringsmallen, eller så kan du lägga till URL-adressen manuellt till sådana resurser i *Del 2 av 2: Ange alternativ för CDN-validering*.<br>**Exempel:**<br> I det här första exemplet innehåller mallen för ogiltigförklaring `<ID>` tillsammans med resursens URL har `/is/content`. Till exempel: `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media formulerar URL:en baserat på denna sökväg med `<ID>` som de resurser som väljs via resursväljaren som du vill ogiltigförklara.<br>I det här andra exemplet innehåller invalideringsmallen den fullständiga URL:en för resursen som används i dina webbegenskaper med `/is/content` (är inte beroende av resursväljaren). Till exempel: `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` där ryggsäck är resurs-ID.<br>Resursformat som stöds i Dynamic Media kan ogiltigförklaras. Resursfiltyper som är *not* CDN-ogiltigförklaring kan göras i följande fall: PostScript®, Encapsulated PostScript®, Adobe Illustrator, Adobe InDesign, Microsoft® PowerPoint, Microsoft® Excel, Microsoft® Word och Rich Text Format.<br><br>・ När du skapar mallen, men är noga med att tänka på syntax och typos, gör inte Dynamic Media någon mallvalidering.<br>・ CDN-valideringsmallen kan spara upp till 2 500 tecken.<br>・ Ange URL:er för smart beskärning av bilder antingen i den här CDN-valideringsmallen eller i **[!UICONTROL Add URL]** textfält i *Del 2: Ange alternativ för CDN-validering.*<br>・ Varje post i en CDN-valideringsmall måste finnas på sin egen rad.<br>・ Följande exempel på en CDN-valideringsmall är endast avsett som exempel. |

   ![CDN-valideringsmall - Skapa](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >CDN-valideringsmallen kan spara upp till 2 500 tecken.

1. I det övre högra hörnet av **[!UICONTROL CDN Invalidation template]** sida, markera **[!UICONTROL Save]** väljer **[!UICONTROL OK]**.<br>
   *Del 2 av 2: Ange alternativ för CDN-validering*
   <br>

1. På Experience Manager as a Cloud Service: **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL CDN Invalidation]**.

   ![CDN-valideringsfunktion](/help/assets/assets-dm/cdn-invalidation-path.png)

1. På **[!UICONTROL CDN Invalidation]** - **[!UICONTROL Add Details]** väljer du resurser för CDN-ogiltigförklaring.

   ![CDN-validering - Lägg till information](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Om du bestämmer dig för att lämna alternativen **[!UICONTROL Invalidate asset associated image presets in CDN]** *och* **[!UICONTROL Invalidate based on template]** om det inte är markerat formas bas-URL:en för de valda resurserna för ogiltigförklaring. Använd endast detta alternativ för bilder.


   | Alternativ | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Invalidate asset associated image presets in CDN]** | (Valfritt) När du markerar det här alternativet formateras markerade resurser och alla deras associerade förinställda URL:er automatiskt för cacheogiltigförklaring.<br>Resurser och tillhörande fördefinierade URL:er för förinställningar formateras automatiskt för ogiltigförklaring. Det här alternativet fungerar bara för bildresurser. |
   | **[!UICONTROL Invalidation based on template]** | (Valfritt) Markera det här alternativet om du bara vill använda den definierade mallen för URL-formatering. |
   | **[!UICONTROL Add Assets]** | Använd Resursväljaren för att välja resurser som du vill göra ogiltiga. Du kan välja antingen publicerade eller opublicerade resurser.<br>Cachelagring vid CDN är URL-baserad, inte resursbaserad. Därför måste du vara medveten om de fullständiga URL:erna som finns på webbplatsen. När du har fastställt dessa URL-adresser kan du lägga till dem i mallen. Sedan kan du markera och lägga till resurserna och göra URL-adresserna ogiltiga i ett enda steg. <br>Använd det här alternativet med **[!UICONTROL Invalidate asset associated image presets in CDN]**, eller **[!UICONTROL Invalidation based on template]** eller båda. |
   | **[!UICONTROL Add URL]** | Lägg till eller klistra in fullständiga URL-sökvägar manuellt i Dynamic Media-resurser vars CDN-cache du vill ogiltigförklara. Använd det här alternativet om du inte har skapat en mall för CDN-invalidering i ***Del 1 av 2: Skapa en mall för CDN-invalidering***, och har bara ett fåtal resurser att ogiltigförklara.<br>**Viktigt:** Varje URL som du lägger till måste finnas på en egen rad.<br>Du kan göra upp till 1 000 URL-adresser ogiltiga samtidigt. Om antalet URL-adresser i **[!UICONTROL Add URL]** textfältet är större än 1000, du kan inte markera **[!UICONTROL Next]**. I sådana fall måste du välja **[!UICONTROL X]** till höger om en markerad resurs eller en manuellt tillagd URL-adress för att ta bort den från listan över ogiltigförklaringar.<br>Ange URL:er för smart beskärning av bilder antingen i CDN-valideringsmallen eller i den här **[!UICONTROL Add URL]** textfält. |

1. I sidans övre högra hörn väljer du **[!UICONTROL Next]**.
1. På **[!UICONTROL CDN Invalidation]** - **[!UICONTROL Confirm]** sida, på **[!UICONTROL URLs]** visas en lista med en eller flera URL:er som genererats från CDN-valideringsmallen som du skapade tidigare och de resurser som du just lade till.

   Anta att du har lagt till en enskild resurs med namnet med hjälp av exemplet med CDN-mall för invalidering som visades i stegen ovan `spinset`. När du går till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL CDN Invalidation]** resulterar det i följande fem genererade URL:er i **[!UICONTROL CDN Invalidation - Confirm]** användargränssnitt:

   ![CDN-validering - Bekräfta](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Välj vid behov **X** till höger om en URL för att ta bort den från ogiltigförklaringsprocessen.

1. I sidans övre högra hörn väljer du **[!UICONTROL Submit]** för att inleda CDN-invalideringsprocessen.

## Felsöka CDN-valideringsfel

I samtliga fall bearbetas hela gruppen för att ogiltigförklaras, eller så misslyckas hela gruppen.

| Fel | Förklaring |
| --- | --- |
| *Det gick inte att hämta URL:er för valda resurser.* | Inträffar om något av följande scenarier uppfylls:<br>- Det gick inte att hitta någon Dynamic Media-konfiguration.<br>- Det finns ett undantag när en tjänstanvändare hämtas genom vilket Dynamic Media-konfigurationen läses.<br>- Publiceringsservern eller företagsroten som används för att skapa URL-adresserna saknas i Dynamic Media-konfigurationen. |
| *Vissa URL:er är inte korrekt definierade. Korrigera och skicka igen.* | Inträffar om invaliderings-API:t för IPS CDN-cache returnerar ett fel. Felet anger att URL:en refererar till ett annat företag eller att URL:en inte är giltig enligt den validering som görs av API:t för cdnCacheInvalidation i IPS. |
| *Det gick inte att göra CDN-cachen ogiltig.* | Inträffar om CDN-cachen ogiltigförklarar begäran av någon annan anledning. |
| *Inga URL:er har angetts som ogiltiga.* | Inträffar om det inte finns några URL:er i **[!UICONTROL CDN Invalidation]** - **[!UICONTROL Confirm]** sida och du väljer **[!UICONTROL Submit]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. While you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
