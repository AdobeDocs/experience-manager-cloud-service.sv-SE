---
title: Sök ansikten.
description: I den här artikeln beskrivs hur du skapar, ändrar och använder sökfaktorer i Experience Manager.
feature: Search,Metadata
role: User,Admin
exl-id: f994c1bf-3f9d-4cb2-88f4-72a9ad6fa999
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '2381'
ht-degree: 13%

---

# Sök efter ansikten {#search-facets}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/search-facets.html) |
| AEM as a Cloud Service | Den här artikeln |

En företagsövergripande driftsättning av Adobe Experience Manager Assets har kapacitet att lagra många resurser. Ibland kan det vara besvärligt och tidskrävande att hitta rätt resurs om du bara använder de allmänna sökfunktionerna i Experience Manager.

Använd sökfaktorer på panelen Filter för att göra sökningen mer detaljerad och göra sökfunktionen mer effektiv och flexibel. Sökfaktorer lägger till flera dimensioner (predikat) som gör att du kan utföra mer komplicerade sökningar. Panelen Filter innehåller några standardaspekter. Du kan också lägga till anpassade sökfaktorer.

Med sökfaktorer kan du söka efter resurser på flera olika sätt i stället för i en enda, förutbestämd, taxonisk ordning. Du kan enkelt gå ned till önskad detaljnivå för en mer fokuserad sökning.

Om du till exempel söker efter en bild kan du välja om du vill ha en bitmapp eller en vektorbild. Du kan minska sökningen ytterligare genom att ange MIME-typen för bilden. På samma sätt kan du ange formatet, till exempel PDF eller MS Word, när du söker efter dokument.

## Lägg till ett predikat {#adding-a-predicate}

De sökfaktorer som visas på panelen Filter definieras i det underliggande sökformuläret med hjälp av predikat. Om du vill visa fler eller olika aspekter lägger du till predikat i standardformuläret eller använder ett anpassat formulär som innehåller de egenskaper du vill använda.

Lägg till `Fulltext` förutsäga formuläret. Använd predikatet Egenskap för att söka efter resurser som matchar en enskild egenskap som du anger. Använd predikatet Alternativ för att söka efter resurser som matchar ett eller flera värden för en viss egenskap. Lägg till predikatet för datumintervall för att söka efter resurser som skapats inom ett angivet datumintervall.

1. Klicka på Experience Manager-logotypen och gå sedan till **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. På sidan Sök i Forms väljer du **[!UICONTROL Assets Admin Search Rail]** väljer  **Redigera** ![aemassets_edit](assets/aemassets_edit.png).

   ![Leta reda på och välj Resursadministratörens sökspår](assets/assets_admin_searchrail.png)

1. Dra ett predikat från sidan Redigera sökning i Forms **[!UICONTROL Select Predicate]** till huvudfönstret. Dra till exempel **[!UICONTROL Property Predicate]**.

   ![Markera och flytta ett predikat för att anpassa sökfiltren](assets/drag_predicate.png)

   *Bild: Välj och flytta ett predikat för att anpassa sökfiltren.*

1. Ange en fältetikett, platshållartext och beskrivning för predikatet på fliken Inställningar. Ange ett giltigt namn för metadataegenskapen som du vill associera med predikatet. Rubriketiketten på fliken Inställningar identifierar det valda predikatets typ.

   ![Använd fliken Inställningar för att ange de alternativ som krävs för ett predikat](assets/settings.png)

   *Bild: Använd fliken Inställningar för att ange önskade alternativ för ett predikat.*

1. I fältet **[!UICONTROL Property Name]** anger du ett giltigt namn för den metadataegenskap som du vill associera med predikatet. Det är det namn som sökningen baseras på. Skriv till exempel `jcr:content/metadata/dc:description` eller `./jcr:content/metadata/dc:description`. Du kan också välja en befintlig nod i urvalsdialogrutan.

   ![Associera en metadataegenskap med ett predikat i fältet Egenskapsnamn](assets/property_settings.png)

   *Bild: Associera en metadataegenskap med ett predikat i fältet Egenskapsnamn.*

1. Klicka på **[!UICONTROL Preview]** ![förhandsgranska](assets/preview.png) om du vill generera en förhandsvisning av panelen Filter så som den ser ut när du har lagt till predikatet.
1. Granska layouten för predikatet i förhandsgranskningsläget.

   ![Förhandsgranska sökformuläret innan ändringarna skickas](assets/preview-1.png)

   Förhandsgranska sökformuläret innan ändringarna skickas

1. Om du vill stänga förhandsgranskningen klickar du på **[!UICONTROL Close]** ![stäng](assets/do-not-localize/close_icon.png) i förhandsvisningens övre högra hörn.
1. Välj **[!UICONTROL Done]** för att spara inställningarna.
1. Navigera till sökpanelen i användargränssnittet Resurser. Egenskapspredikatet läggs till på panelen.
1. Ange en beskrivning av resursen som ska genomsökas i textrutan. Ange t.ex. &quot;Adobe.&quot; När du gör en sökning visas resurser med en beskrivning som matchar&quot;Adobe&quot; i sökresultaten.

## Lägg till ett alternativs predikat {#adding-an-options-predicate}

Med predikatet Alternativ kan du lägga till flera sökalternativ på panelen Filter. Du kan välja ett eller flera av dessa alternativ på panelen Filter om du vill söka efter resurser. Om du till exempel vill söka efter resurser baserat på filtyp konfigurerar du alternativ som Bilder, Multimedia, Dokument och Arkiv i sökformuläret. När du har konfigurerat de här alternativen utförs sökningen på resurser av typen GIF, JPEG, PNG och så vidare när du väljer alternativet Bilder på panelen Filter.

Om du vill mappa alternativen till respektive egenskap skapar du en nodstruktur för alternativen och anger sökvägen till den överordnade noden i egenskapen Egenskapsnamn för predikatet Alternativ. Den överordnade noden ska vara av typen `sling`: `OrderedFolder`. Alternativen ska vara av typen `nt:unstructured`. Alternativnoderna ska ha egenskaperna `jcr:title` och `value` konfigurerad.

The `jcr:title` -egenskapen är ett användarvänligt namn på det alternativ som visas på panelen Filter. The `value` fältet används i frågan för att matcha den angivna egenskapen.

När du väljer ett alternativ utförs sökningen baserat på `value` egenskapen för alternativnoden och dess underordnade noder, om sådana finns. Hela trädet under alternativnoden gås igenom och `value` egenskapen för varje underordnad nod kombineras med en OR-åtgärd för att skapa sökfrågan.

Om du till exempel väljer ”Bilder” för filtyper skapas sökfrågan för resurserna genom att egenskapen `value` kombineras med en OR-åtgärd. Sökfrågan efter bilder skapas till exempel genom att kombinera resultaten som matchar *image/jpeg*, *image/gif*, *image/png*, *image/pjpeg* och *image/tiff* för egenskapen `jcr:content/metadata/dc:format` med en OR-åtgärd.

Egenskapen value för en filtyp, som visas i CRXDE, används för att söka i frågor som ska fungera

I stället för att manuellt skapa en nodstruktur för alternativen i CRX-databasen, kan du definiera alternativen i en JSON-fil genom att ange motsvarande nyckelvärdespar. Ange sökvägen till JSON-filen i fältet **[!UICONTROL Property Name]**. Du kan till exempel definiera nyckelvärdesparen `image/bmp`, `image/gif`, `image/jpeg` och `image/png` och ange deras värden så som de visas i följande JSON-exempelfil. I fältet **[!UICONTROL Property Name]** kan du ange CRX-sökvägen för den här filen.

```json
{
    "options" :
 [
          {"value" : "image/bmp","text" : "BMP"},
          {"value" : "image/gif","text" : "GIF"},
          {"value" : "image/jpeg","text" : "JPEG"},
          {"value" : "image/png","text" : "PNG"}
 ]
}
```

Om du vill använda en befintlig nod anger du den i valdialogrutan.

>[!NOTE]
>
>Alternativpredikatet är en anpassad wrapper som innehåller egenskapspredikat som demonstrerar det beskrivna beteendet. För närvarande finns det ingen tillgänglig REST-slutpunkt som stöder funktionen internt.

1. Markera Experience Manager-logotypen och gå sedan till **[!UICONTROL Tools > General > Search Forms]**.
1. Från **[!UICONTROL Search Forms]** sida, markera **[!UICONTROL Assets Admin Search Rail]** väljer du sedan ikonen Redigera.
1. På sidan **[!UICONTROL Edit Search Form]** drar du **[!UICONTROL Options Predicate]** från fliken **[!UICONTROL Select Predicate]** till huvudrutan.
1. Ange en etikett och ett namn för egenskapen på fliken **[!UICONTROL Settings]**. Om du till exempel vill söka efter resurser baserat på deras format anger du ett användarvänligt namn för etiketten, till exempel: **[!UICONTROL File Type]**. Ange egenskapen som ska användas för att utföra sökningen i egenskapsfältet, till exempel `jcr:content/metadata/dc:format.`
1. Gör något av följande:

   * I **[!UICONTROL Property Name]** anger du sökvägen till JSON-filen där du definierar noderna för alternativen och anger motsvarande nyckelvärdepar.
   * Välj ![Ikon för att lägga till resurser](assets/do-not-localize/aem_assets_add_icon.png) bredvid fältet Alternativ för att ange visningstext och värde för de alternativ som du vill ange på panelen Filter. Om du vill lägga till ytterligare ett alternativ väljer du ![Ikon för att lägga till resurser](assets/do-not-localize/aem_assets_add_icon.png) och upprepa steget.

1. Kontrollera att **[!UICONTROL Single Select]** är avmarkerat så att användaren kan välja flera alternativ för filtyper samtidigt (till exempel bilder, dokument, multimedia och arkiv). Om du väljer **[!UICONTROL Single Select]** kan användaren bara välja ett alternativ åt gången för olika filtyper.

   ![De tillgängliga fälten i Alternativpaletten](assets/options_predicate.png)

   De tillgängliga fälten i Alternativpaletten

1. I **Beskrivning** ange en valfri beskrivning och klicka sedan på **[!UICONTROL Done]**.
1. Navigera till sökpanelen. Alternativpredikatet läggs till i **Sök** -panelen. Alternativen för **[!UICONTROL File Type]** visas som kryssrutor.

## Lägg till ett egenskapspredikat för flera värden {#adding-a-multi-value-property-predicate}

The `Multi Value Property` kan du söka efter flera värden i resurser. Tänk dig ett scenario där du har bilder på flera produkter i [!DNL Assets] och metadata för varje bild innehåller ett SKU-nummer som är kopplat till produkten. Du kan använda det här predikatet för att söka efter produktbilder baserat på flera SKU-nummer.

1. Klicka på Experience Manager-logotypen och gå sedan till **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. På sidan Sök i Forms väljer du **[!UICONTROL Assets Admin Search Rail]** väljer **Redigera** ![aemassets_edit](assets/aemassets_edit.png).
1. På sidan Redigera sökformulär drar du **[!UICONTROL Multi Value Property Predicate]** från fliken **[!UICONTROL Select Predicate]** till huvudrutan.
1. I **[!UICONTROL Settings]** anger du en etikett och platshållartext för predikatet. Ange egenskapsnamnet som ska användas för att utföra sökningen i egenskapsfältet, till exempel `jcr:content/metadata/dc:value`. Du kan också använda valdialogrutan för att välja en nod.
1. Kontrollera att **[!UICONTROL Delimiter Support]** är markerat. I fältet **[!UICONTROL Input Delimiters]** anger du avgränsare för att separera enskilda värden. Som standard anges kommatecken som avgränsare. Du kan ange en annan avgränsare.
1. I **Beskrivning** fält, ange en valfri beskrivning och välj **[!UICONTROL Done]**.
1. Navigera till panelen Filter i Assets-gränssnittet. Predikatet **[!UICONTROL Multi Value Property]** läggs till på panelen.
1. Ange flera värden i fältet Flervärde avgränsat med avgränsarna och utför sökningen. Predikatet hämtar en exakt textmatchning för de värden du anger.

## Lägg till ett taggpredikat {#adding-a-tags-predicate}

The `Tags` kan du göra taggbaserade sökningar efter resurser. Som standard [!DNL Assets] söker efter resurser efter en eller flera taggar som matchar baserat på de taggar du anger. Med andra ord utför sökfrågan en ELLER-åtgärd med de angivna taggarna. Du kan dock använda alternativet Matcha alla taggar för att söka efter resurser som innehåller alla taggar som du anger.

1. Klicka på Experience Manager-logotypen och gå sedan till **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. På sidan Sök i Forms väljer du **[!UICONTROL Assets Admin Search Rail]** och sedan **Redigera** ![aemassets_edit](assets/aemassets_edit.png).
1. Dra på sidan Redigera sökformulär **[!UICONTROL Tags Predicate]** från fliken Välj predikat till huvudrutan.
1. Ange en platshållartext för predikatet på fliken Inställningar. Ange egenskapsnamnet som ska användas för att utföra sökningen i egenskapsfältet, till exempel `jcr:content/metadata/cq:tags`. Du kan också välja en nod i CRXDE i urvalsdialogrutan.
1. Konfigurera sökvägsegenskapen för rottaggar för det här predikatet för att fylla i olika taggar i listan Taggar.
1. Välj **[!UICONTROL Show match all tags option]** om du vill söka efter resurser som innehåller alla taggar du anger.

   ![Vanliga inställningar för taggar-predikat](assets/tags_predicate.png)

1. I **[!UICONTROL Description]** fält, ange en valfri beskrivning och välj **[!UICONTROL Done]**.
1. Navigera till sökpanelen. The **[!UICONTROL Tags]** predikatet läggs till på sökpanelen.
1. Ange taggar baserat på vilka du vill söka efter resurser eller välj från listan med förslag.
1. Välj **[!UICONTROL Match all]** om du vill söka efter matchningar som innehåller alla taggar som du anger.

Du kan sortera taggstrukturen i stigande eller fallande ordning baserat på **[!UICONTROL Name]** (i alfabetisk ordning), **[!UICONTROL Created]** datum, eller **[!UICONTROL Modified]** datum. I följande bild sorteras taggstrukturen i bokstavsordning baserat på **[!UICONTROL Name]**.

![add-tags](assets/add-tags-to-asset.png)


## Lägga till andra predikat {#adding-other-predicates}

På samma sätt som du lägger till ett egenskapsprediat eller ett alternativpredikat kan du lägga till följande ytterligare predikat på sökpanelen:

<table>
 <tbody>
  <tr>
   <td><p><strong>Predikatnamn</strong></p> </td>
   <td><p><strong>Beskrivning</strong></p> </td>
   <td><p><strong>Egenskaper</strong></p> </td>
  </tr>
  <tr>
   <td><p>Fulltext</p> </td>
   <td>Sök på predikatet för att utföra fullständig textsökning på en hel objektnod. Den mappas med <code>jcr</code>:<code>contains</code> -operator. Du kan ange en relativ sökväg om du vill utföra en fullständig textsökning på en viss del av resursnoden.</td>
   <td>
    <ul>
     <li>Etikett</li>
     <li>Platshållare</li>
     <li>Egenskapsnamn</li>
     <li>Beskrivning</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Sökvägsläsaren</td>
   <td>Sökpredikat för att söka efter resurser i mappar och undermappar på en förkonfigurerad rotsökväg</td>
   <td>
    <ul>
     <li>Platshållare</li>
     <li>Rotsökväg</li>
     <li>Beskrivning</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Bana</p> </td>
   <td><p>Använd den för att filtrera resultaten på plats. Du kan ange olika banor som alternativ.</p> </td>
   <td>
    <ul>
     <li>Etikett</li>
     <li>Bana</li>
     <li>Beskrivning</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Publiceringsstatus</p> </td>
   <td><p>Sök efter predikat för att söka efter resurser baserat på deras publiceringsstatus</p> </td>
   <td>
    <ul>
     <li>Etikett</li>
     <li>Egenskapsnamn</li>
     <li>Beskrivning</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Relativt datum</p> </td>
   <td><p>Sökpredikatet för att söka efter resurser baserat på det relativa datumet då de skapades. Du kan till exempel konfigurera alternativ som för 2 månader sedan, för 3 veckor sedan och så vidare. </p> </td>
   <td>
    <ul>
     <li>Etikett</li>
     <li>Egenskapsnamn</li>
     <li>Relativt datum</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Intervall</p> </td>
   <td><p>Sök på predikatet för att söka efter resurser som ligger inom ett angivet intervall. På sökpanelen kan du ange lägsta och högsta värden för intervallet.</p> </td>
   <td>
    <ul>
     <li>Etikett</li>
     <li>Egenskapsnamn</li>
     <li>Beskrivning</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Datumintervall</p> </td>
   <td><p>Sökpredikatet för att söka efter resurser som skapats inom ett angivet intervall efter en datumegenskap. På sökpanelen kan du ange start- och slutdatum med datumväljare.</p> </td>
   <td>
    <ul>
     <li>Etikett</li>
     <li>Platshållare</li>
     <li>Egenskapsnamn</li>
     <li>Intervalltext (från)</li>
     <li>Intervalltext (till)</li>
     <li>Beskrivning</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Datum</p> </td>
   <td><p>Sökpredikatet för en skjutreglagebaserad sökning efter resurser baserat på en date-egenskap.</p> </td>
   <td>
    <ul>
     <li>Etikett</li>
     <li>Egenskapsnamn</li>
     <li>Beskrivning</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Filstorlek</p> </td>
   <td><p>Sök efter predikatorn för att söka efter resurser baserat på deras storlek. Det är ett sifferbaserat predikat där du väljer skjutreglagealternativ från en konfigurerbar nod. Standardalternativen finns i /libs/dam/options/preates/filesize i CRX-databasen. Filstorleken anges i byte.</p> </td>
   <td>
    <ul>
     <li>Etikett</li>
     <li>Egenskapsnamn</li>
     <li>Bana</li>
     <li>Beskrivning</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Senast ändrad resurs</td>
   <td>Sök efter predikat för att söka efter nyligen ändrade resurser </td>
   <td>
    <ul>
     <li>Egenskapsnamn</li>
     <li>Egenskapsvärde</li>
     <li>Beskrivning</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Publiceringsstatus</td>
   <td>Sök efter predikat för att söka efter resurser baserat på deras publiceringsstatus </td>
   <td>
    <ul>
     <li>Etikett</li>
     <li>Egenskapsnamn</li>
     <li>Beskrivning</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Förfallostatus</td>
   <td>Sök efter predikat för att söka efter resurser baserat på deras förfallostatus </td>
   <td>
    <ul>
     <li>Etikett</li>
     <li>Egenskapsnamn</li>
     <li>Beskrivning</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dold</td>
   <td>Sökpredikat som definierar en dold fältegenskap för att söka efter resurser</td>
   <td>
    <ul>
     <li>Egenskapsnamn</li>
     <li>Egenskapsvärde</li>
     <li>Beskrivning</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Ta bort standardsökfaktorer {#removing-default-search-facets}

Adobe rekommenderar att du är försiktig när du tar bort standardsökfaktorer för att undvika prestandaproblem. Om du tar bort standardsökfaktorer kan det också påverka standardfunktionen.

Ta inte bort följande dolda fält eftersom det orsakar ett frågeprestandaproblem med OmniSearch och smarta samlingar:

* group.2_group.type=dam:Asset

* group.1_group.type=nt:folder

* group.p.or=true

## Återställ standardsökfaktorer {#restoring-default-search-facets}

Som standard visas en låsikon före **[!UICONTROL Assets Admin Search Rail]** i **[!UICONTROL Search Forms]** sida. Ikonen Lås försvinner om du lägger till sökfaktorer i formuläret, vilket anger att standardformuläret har ändrats.

Låsikonen mot ett alternativ på söksidan i Forms anger att standardinställningarna är intakta och inte anpassade.

Så här återställer du standardsökaspekten:

1. Välj **[!UICONTROL Assets Admin Search Rail]** i **[!UICONTROL Search Forms]** sida.
1. Välj **[!UICONTROL Delete]** ![ta bort ikon](assets/do-not-localize/deleteoutline.png) i verktygsfältet.
1. I bekräftelsedialogrutan väljer du **[!UICONTROL Delete]** för att ta bort de anpassade ändringarna.

   När du har tagit bort de anpassade ändringarna för sökfasetter visas låsikonen igen före **[!UICONTROL Assets Admin Search Rail]** på sidan **[!UICONTROL Search Forms]**.

## Användarbehörigheter {#user-permissions}

Om du inte har tilldelats en administratörsroll finns det en lista med behörigheter som du behöver för att utföra redigerings-, borttagnings- och förhandsgranskningsåtgärder som omfattar sökfaktorer.

| Åtgärd | Behörighet |
|---|---|
| Redigera | Läsa och skriva behörigheter på `/apps` i CRX. |
| Ta bort | Läsa, skriva och ta bort behörigheter på `/apps` i CRX. |
| Förhandsgranska | Läsa, skriva och ta bort behörigheter på `/var/dam/content` i CRX. Dessutom kan du läsa och skriva behörigheter på `/apps` nod. |

**Se även**

* [Sök efter bästa praxis](search-best-practices.md)
* [Översätt resurser](translate-assets.md)
* [Resurser för HTTP API](mac-api-assets.md)
* [Resurser som stöds i filformat](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [Söka efter digitala resurser](search-assets.md).
