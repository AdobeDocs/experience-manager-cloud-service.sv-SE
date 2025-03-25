---
title: Invalidera cacheminnet för innehållsleveransnätverket med hjälp av dynamiska media
description: Lär dig hur du gör ditt CDN-cachelagrade innehåll (Content Delivery Network) ogiltigt så att du snabbt kan uppdatera resurser som levereras av Dynamic Media, i stället för att vänta på att cachen ska upphöra att gälla.
contentOwner: Rick Brough
feature: Asset Management
role: Admin,User
exl-id: c631079b-8082-4ff7-a122-dac1b20d8acd
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '1310'
ht-degree: 0%

---

# Gör CDN-cachen ogiltig via Dynamic Media {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

Dynamiska mediefiler cachas av CDN (Content Delivery Network) för snabb leverans till dina kunder. När du uppdaterar resurserna vill du dock att ändringarna ska börja gälla omedelbart på webbplatsen. Genom att rensa eller göra CDN-cachen ogiltig kan du snabbt uppdatera resurser som levereras av Dynamic Media. Du behöver inte längre vänta på att cachen ska förfalla med ett TTL-värde (Time To Live) (standard är tio timmar). I stället kan du skicka en begäran från användargränssnittet för Dynamic Media om att cachen ska upphöra att gälla inom några minuter.

>[!NOTE]
>
>Den här funktionen kräver att du använder det Adobe-paket för CDN som medföljer Adobe Experience Manager Dynamic Media. Andra anpassade CDN stöds inte med den här funktionen.

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

Om du har aktiverat [Smart Imaging](/help/assets/dynamic-media/imaging-faq.md) på ditt konto och du använder det Adobe-paketerade CDN, kan du rensa alla URL:er med olika frågesträngar genom att rensa den enskilda bas-URL:en.

Om till exempel `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image` blir ogiltigt blir även följande URL:er ogiltiga:

* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image`
* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image?wid=300`
* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image?$PLP$`
* och så vidare.

Detta ogiltigförklarande gäller dock inte för generiska domäner som inte stöder Smart Imaging, till exempel `s7d1.scene7.com`. Sådana domäner behöver fortfarande den fullständiga URL:en för att ogiltigförklaras.

**Så här gör du CDN-cachen ogiltig via dynamiska media:**

*Del 1 av 2: Skapa en mall för CDN-invalidering*

1. Gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL CDN Invalidation Template]** i Adobe Experience Manager as a Cloud Service.

   ![CDN-verifieringsfunktion](/help/assets/assets-dm/cdn-invalidation-template.png)

1. Gör något av följande på sidan **[!UICONTROL CDN Invalidation template]** baserat på ditt scenario:

   | Scenario | Alternativ |
   | --- | --- |
   | Jag har redan skapat en CDN-invalideringsmall med Dynamic Media Classic. | Textfältet **[!UICONTROL Create Template]** är förifyllt med malldata. I så fall kan du antingen redigera mallen eller fortsätta till nästa steg. |
   | Jag måste skapa en mall. Vad ska jag ange? | I textfältet **[!UICONTROL Create Template]** anger du en bild-URL (inklusive bildförinställningar eller modifierare) som refererar till `<ID>`, i stället för ett specifikt bild-ID som i följande exempel:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Om mallen bara innehåller `<ID>` fylls Dynamic Media i `https://<publishserver_name>/is/image/<company_name>/<ID>` där `<publishserver_name>` är namnet på din Publish Server som definieras i Allmänna inställningar i Dynamic Media Classic. `<company_name>` är namnet på företagsroten som är associerad med den här Experience Manager-instansen, och `<ID>` är de valda resurserna via resursväljaren som ska ogiltigförklaras.<br>Alla förinställningar/modifierare efter `<ID>` kopieras som de är i URL-definitionen.<br>Endast bilder - det vill säga `/is/image` - kan formateras automatiskt baserat på mallen.<br>Om du lägger till resurser som videor eller PDF-filer med resursväljaren för `/is/content/` genereras inte URL-adresser automatiskt. I stället måste du ange sådana resurser antingen i CDN-valideringsmallen, eller så kan du manuellt lägga till URL:en till sådana resurser i *Del 2 av 2: Ange alternativ för CDN-validering*.<br>**Exempel:**<br> I det här första exemplet innehåller ogiltighetsmallen `<ID>` tillsammans med resursens URL som har `/is/content`. Exempel: `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media skapar URL:en baserat på den här sökvägen, där `<ID>` är de resurser som väljs via resursväljaren som du vill ogiltigförklara.<br>I det här andra exemplet innehåller invalideringsmallen den fullständiga URL:en för resursen som används i dina webbegenskaper med `/is/content` (inte beroende av resursväljaren). Exempel: `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` där ryggsäck är resurs-ID.<br>Resursformat som stöds i Dynamic Media kan ogiltigförklaras. Resursfiltyper som *inte* stöds för CDN-ogiltigförklaring är bland annat PostScript®, Encapsulated PostScript®, Adobe Illustrator, Adobe InDesign, Microsoft® PowerPoint, Microsoft® Excel, Microsoft® Word och Rich Text Format.<br><br> ・ När du skapar mallen, men ser till att du är noggrann med syntax och typos. Dynamic Media utför ingen mallvalidering.<br> ・ CDN-valideringsmallen kan spara upp till 2 500 tecken.<br> ・ Ange URL:er för smart beskärning av bilder antingen i den här CDN-valideringsmallen eller i textfältet **[!UICONTROL Add URL]** i *Del 2: Ange CDN-valideringsalternativ.*<br> ・ Varje post i en CDN-valideringsmall måste finnas på en egen rad.<br> ・ Följande exempel på en CDN-valideringsmall är endast avsett som exempel. |

   ![Mall för CDN-invalidering - Skapa](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >CDN-valideringsmallen kan spara upp till 2 500 tecken.

1. I det övre högra hörnet på sidan **[!UICONTROL CDN Invalidation template]** väljer du **[!UICONTROL Save]** och sedan **[!UICONTROL OK]**.<br>
   *Del 2 av 2: Ange alternativ för CDN-validering*
   <br>

1. Gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL CDN Invalidation]** i Experience Manager as a Cloud Service.

   ![CDN-verifieringsfunktion](/help/assets/assets-dm/cdn-invalidation-path.png)

1. På sidan **[!UICONTROL CDN Invalidation]** - **[!UICONTROL Add Details]** väljer du resurser för CDN-ogiltigförklaring.

   ![CDN-invalidering - Lägg till detaljer](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Om du bestämmer dig för att låta alternativen **[!UICONTROL Invalidate asset associated image presets in CDN]** *och* **[!UICONTROL Invalidate based on template]** vara omarkerade, kommer bas-URL:en för de valda resurserna att formas för ogiltigförklaring. Använd endast detta alternativ för bilder.


   | Alternativ | Beskrivning |
   | --- | --- |
   | **[!UICONTROL Invalidate asset associated image presets in CDN]** | (Valfritt) När du markerar det här alternativet formateras markerade resurser och alla deras associerade förinställda URL:er automatiskt för cacheogiltigförklaring.<br>Assets och tillhörande fördefinierade URL:er för förinställningar formateras automatiskt för ogiltigförklaring. Det här alternativet fungerar bara för bildresurser. |
   | **[!UICONTROL Invalidation based on template]** | (Valfritt) Markera det här alternativet om du bara vill använda den definierade mallen för URL-formatering. |
   | **[!UICONTROL Add Assets]** | Använd Resursväljaren för att välja resurser som du vill göra ogiltiga. Du kan välja antingen publicerade eller opublicerade resurser.<br>Cachelagring vid CDN är URL-baserad, inte resursbaserad. Därför måste du vara medveten om de fullständiga URL:erna som finns på webbplatsen. När du har fastställt dessa URL-adresser kan du lägga till dem i mallen. Sedan kan du markera och lägga till resurserna och göra URL-adresserna ogiltiga i ett enda steg. <br>Använd det här alternativet med **[!UICONTROL Invalidate asset associated image presets in CDN]**, **[!UICONTROL Invalidation based on template]** eller båda. |
   | **[!UICONTROL Add URL]** | Lägg till eller klistra in fullständiga URL-sökvägar manuellt i Dynamic Media-resurser vars CDN-cache du vill ogiltigförklara. Använd det här alternativet om du inte har skapat någon CDN-valideringsmall i ***Del 1 av 2: Skapa en CDN-valideringsmall*** och bara har ett fåtal resurser att göra ogiltig.<br>**Viktigt!** Varje URL som du lägger till måste finnas på en egen rad.<br>Du kan göra upp till 1 000 URL-adresser ogiltiga åt gången. Om antalet URL:er i textfältet **[!UICONTROL Add URL]** är större än 1 000 kan du inte välja **[!UICONTROL Next]**. I sådana fall måste du markera **[!UICONTROL X]** till höger om en markerad resurs eller en manuellt tillagd URL för att ta bort den från listan över ogiltigförklaringar.<br>Ange URL:er för smart beskärning av bilder antingen i CDN-valideringsmallen eller i det här **[!UICONTROL Add URL]**-textfältet. |

1. Välj **[!UICONTROL Next]** i sidans övre högra hörn.
1. På sidan **[!UICONTROL CDN Invalidation]** - **[!UICONTROL Confirm]** i listrutan **[!UICONTROL URLs]** visas en lista med en eller flera URL:er som genererats från CDN-valideringsmallen som du skapade tidigare och de resurser som du just lade till.

   Anta att du har lagt till en enskild resurs med namnet `spinset` med hjälp av exemplet med mallen för CDN-validering som visades i stegen tidigare. När du går till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL CDN Invalidation]** resulterar det i följande fem genererade URL:er i användargränssnittet för **[!UICONTROL CDN Invalidation - Confirm]**:

   ![CDN-invalidering - Bekräfta](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Om det behövs väljer du **X** till höger om en URL för att ta bort den från ogiltigförklaringsprocessen.

1. I närheten av det övre högra hörnet av sidan väljer du **[!UICONTROL Submit]** för att starta CDN-invalideringsprocessen.

## Felsöka CDN-valideringsfel

I samtliga fall bearbetas hela gruppen för att ogiltigförklaras, eller så misslyckas hela gruppen.

| Fel | Förklaring |
| --- | --- |
| *Det gick inte att hämta URL:er för valda resurser.* | Inträffar om något av följande scenarier uppfylls:<br>- Det går inte att hitta någon dynamisk mediekonfiguration.<br> - Det finns ett undantag när en tjänstanvändare hämtas genom vilket konfigurationen för dynamiska media läses.<br> - Publiceringsservern eller företagsroten som används för att skapa URL:er saknas i Dynamic Media-konfigurationen. |
| *Vissa URL:er är inte korrekt definierade. Korrigera och skicka om.* | Inträffar om invaliderings-API:t för IPS CDN-cache returnerar ett fel. Felet anger att URL:en refererar till ett annat företag eller att URL:en inte är giltig enligt den validering som görs av API:t för cdnCacheInvalidation i IPS. |
| *Det gick inte att ogiltigförklara CDN-cachen.* | Inträffar om CDN-cachen ogiltigförklarar begäran av någon annan anledning. |
| *Inga URL:er har angetts som ogiltiga.* | Inträffar om det inte finns några URL:er på sidan **[!UICONTROL CDN Invalidation]** - **[!UICONTROL Confirm]** och du väljer **[!UICONTROL Submit]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. While you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
