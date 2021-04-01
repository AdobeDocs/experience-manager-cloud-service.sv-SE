---
title: Söka efter fasetter.
description: I den här artikeln beskrivs hur du skapar, ändrar och använder sökfaktorer i AEM.
feature: Sök,Metadata
role: Affärsledare,Administratör
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '2268'
ht-degree: 18%

---


# Söka efter fasetter {#search-facets}

En företagsövergripande driftsättning av Adobe Experience Manager (AEM) Assets har kapacitet att lagra många resurser. Ibland kan det vara besvärligt och tidskrävande att hitta rätt resurs om du bara använder de allmänna sökfunktionerna i AEM.

Använd sökfaktorer på panelen Filter för att göra sökningen mer detaljerad och göra sökfunktionen mer effektiv och flexibel. Sökfaktorer lägger till flera dimensioner (predikat) som gör att du kan utföra mer komplicerade sökningar. Panelen Filter innehåller några standardaspekter. Du kan också lägga till anpassade sökfaktorer.

Med sökfaktorer kan du söka efter resurser på flera olika sätt i stället för i en enda, förutbestämd, taxonisk ordning. Du kan enkelt gå ned till önskad detaljnivå för en mer fokuserad sökning.

Om du till exempel söker efter en bild kan du välja om du vill ha en bitmapp eller en vektorbild. Du kan minska sökningen ytterligare genom att ange MIME-typen för bilden. På samma sätt kan du ange formatet när du söker efter dokument, till exempel PDF eller MS Word.

## Lägg till ett predikat {#adding-a-predicate}

De sökfaktorer som visas på panelen Filter definieras i det underliggande sökformuläret med hjälp av predikat. Om du vill visa fler eller olika aspekter lägger du till predikat i standardformuläret eller använder ett anpassat formulär som innehåller de egenskaper du vill använda.

För textsökningar lägger du till `Fulltext`-predikatet i formuläret. Använd predikatet Egenskap för att söka efter resurser som matchar en enskild egenskap som du anger. Använd predikatet Alternativ för att söka efter resurser som matchar ett eller flera värden för en viss egenskap. Lägg till predikatet för datumintervall för att söka efter resurser som skapats inom ett angivet datumintervall.

1. Klicka på AEM-logotypen och gå sedan till **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. På sidan Sök i Forms väljer du **[!UICONTROL Assets Admin Search Rail]** och trycker sedan på **Redigera** ![aemassets_edit](assets/aemassets_edit.png).

   ![Leta reda på och välj Resursadministratörens sökspår](assets/assets_admin_searchrail.png)

1. På sidan Redigera sökning i Forms drar du ett predikat från fliken **[!UICONTROL Select Predicate]** till huvudrutan. Dra till exempel **[!UICONTROL Property Predicate]**.

   ![Markera och flytta ett predikat för att anpassa sökfiltren](assets/drag_predicate.png)

   *Bild: Välj och flytta ett predikat för att anpassa sökfiltren.*

1. Ange en fältetikett, platshållartext och beskrivning för predikatet på fliken Inställningar. Ange ett giltigt namn för metadataegenskapen som du vill associera med predikatet. Rubriketiketten på fliken Inställningar identifierar det valda predikatets typ.

   ![Använd fliken Inställningar för att ange de alternativ som krävs för ett predikat](assets/settings.png)

   *Bild: Använd fliken Inställningar för att ange önskade alternativ för ett predikat.*

1. I fältet **[!UICONTROL Property Name]** anger du ett giltigt namn för den metadataegenskap som du vill associera med predikatet. Det är det namn som sökningen baseras på. Skriv till exempel `jcr:content/metadata/dc:description` eller `./jcr:content/metadata/dc:description`. Du kan också välja en befintlig nod i urvalsdialogrutan.

   ![Associera en metadataegenskap med ett predikat i fältet Egenskapsnamn](assets/property_settings.png)

   *Bild: Associera en metadataegenskap med ett predikat i fältet Egenskapsnamn.*

1. Klicka på **[!UICONTROL Preview]** ![förhandsvisning](assets/preview.png) för att generera en förhandsgranskning av panelen Filter så som den visas när du har lagt till predikatet.
1. Granska layouten för predikatet i förhandsgranskningsläget.

   ![Förhandsgranska sökformuläret innan ändringarna skickas](assets/preview-1.png)

   Förhandsgranska sökformuläret innan ändringarna skickas

1. Om du vill stänga förhandsgranskningen klickar du på **[!UICONTROL Close]** ![close](assets/do-not-localize/close_icon.png) i det övre högra hörnet av förhandsvisningen.
1. Tryck på **[!UICONTROL Done]** för att spara inställningarna.
1. Navigera till sökpanelen i användargränssnittet Resurser. Egenskapspredikatet läggs till på panelen.
1. Ange en beskrivning av resursen som ska genomsökas i textrutan. Ange t.ex. &quot;Adobe.&quot; När du gör en sökning visas resurser med en beskrivning som matchar&quot;Adobe&quot; i sökresultaten.

## Lägg till ett Alternativpredikat {#adding-an-options-predicate}

Med predikatet Alternativ kan du lägga till flera sökalternativ på panelen Filter. Du kan välja ett eller flera av dessa alternativ på panelen Filter om du vill söka efter resurser. Om du till exempel vill söka efter resurser baserat på filtyp konfigurerar du alternativ som Bilder, Multimedia, Dokument och Arkiv i sökformuläret. När du har konfigurerat de här alternativen utförs sökningen på resurser av typen GIF, JPEG, PNG och så vidare när du väljer alternativet Bilder på panelen Filter.

Om du vill mappa alternativen till respektive egenskap skapar du en nodstruktur för alternativen och anger sökvägen till den överordnade noden i egenskapen Egenskapsnamn för predikatet Alternativ. Den överordnade noden ska vara av typen `sling`: `OrderedFolder`. Alternativen ska vara av typen `nt:unstructured`. Alternativnoderna ska ha egenskaperna `jcr:title` och `value` konfigurerade.

Egenskapen `jcr:title` är ett användarvänligt namn för alternativet som visas på panelen Filter. Fältet `value` används i frågan för att matcha den angivna egenskapen.

När du väljer ett alternativ utförs sökningen baserat på egenskapen `value` för alternativnoden och dess eventuella underordnade noder. Hela trädet under alternativnoden gås igenom och egenskapen `value` för varje underordnad nod kombineras med en OR-åtgärd för att skapa sökfrågan.

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

1. Tryck på AEM logotyp och gå sedan till **[!UICONTROL Tools > General > Search Forms]**.
1. På sidan **[!UICONTROL Search Forms]** väljer du **[!UICONTROL Assets Admin Search Rail]** och trycker sedan på ikonen Redigera.
1. På sidan **[!UICONTROL Edit Search Form]** drar du **[!UICONTROL Options Predicate]** från fliken **[!UICONTROL Select Predicate]** till huvudrutan.
1. Ange en etikett och ett namn för egenskapen på fliken **[!UICONTROL Settings]**. Om du till exempel vill söka efter resurser baserat på deras format anger du ett användarvänligt namn på etiketten, till exempel **[!UICONTROL File Type]**. Ange egenskapen som ska användas för sökningen i egenskapsfältet, till exempel `jcr:content/metadata/dc:format.`
1. Gör något av följande:

   * I fältet **[!UICONTROL Property Name]** anger du sökvägen till JSON-filen där du definierar noderna för alternativen och anger motsvarande nyckelvärdepar.
   * Tryck på ![ikonen Lägg till resurser](assets/do-not-localize/aem_assets_add_icon.png) bredvid fältet Alternativ för att ange visningstexten och värdet för de alternativ du vill ange i panelen Filter. Om du vill lägga till ytterligare ett alternativ trycker/klickar du på ![ikonen Lägg till ](assets/do-not-localize/aem_assets_add_icon.png) för resurser och upprepar steget.

1. Kontrollera att **[!UICONTROL Single Select]** är avmarkerat så att användaren kan välja flera alternativ för filtyper samtidigt (till exempel bilder, dokument, multimedia och arkiv). Om du väljer **[!UICONTROL Single Select]** kan användaren bara välja ett alternativ åt gången för olika filtyper.

   ![De tillgängliga fälten i Alternativpaletten](assets/options_predicate.png)

   De tillgängliga fälten i Alternativpaletten

1. I fältet **Beskrivning** anger du en valfri beskrivning och klickar sedan på **[!UICONTROL Done]**.
1. Navigera till sökpanelen. Alternativpredikatet läggs till på panelen **Sök**. Alternativen för **[!UICONTROL File Type]** visas som kryssrutor.

## Lägg till ett egenskapspredikat för flera värden {#adding-a-multi-value-property-predicate}

Med `Multi Value Property`-predikatet kan du söka efter flera värden i resurser. Tänk dig ett scenario där du har bilder på flera produkter i AEM Assets och där metadata för varje bild innehåller ett SKU-nummer som är kopplat till produkten. Du kan använda det här predikatet för att söka efter produktbilder baserat på flera SKU-nummer.

1. Klicka på AEM-logotypen och gå sedan till **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. På sidan Sök i Forms väljer du **[!UICONTROL Assets Admin Search Rail]** och trycker på **Redigera** ![aemassets_edit](assets/aemassets_edit.png).
1. På sidan Redigera sökformulär drar du **[!UICONTROL Multi Value Property Predicate]** från fliken **[!UICONTROL Select Predicate]** till huvudrutan.
1. På fliken **[!UICONTROL Settings]** anger du en etikett och platshållartext för predikatet. Ange egenskapsnamnet som ska användas för sökningen i egenskapsfältet, till exempel `jcr:content/metadata/dc:value`. Du kan också använda valdialogrutan för att välja en nod.
1. Kontrollera att **[!UICONTROL Delimiter Support]** är markerat. I fältet **[!UICONTROL Input Delimiters]** anger du avgränsare för att separera enskilda värden. Som standard anges kommatecken som avgränsare. Du kan ange en annan avgränsare.
1. I fältet **Beskrivning** anger du en valfri beskrivning och trycker sedan på **[!UICONTROL Done]**.
1. Navigera till panelen Filter i Assets-gränssnittet. Predikatet **[!UICONTROL Multi Value Property]** läggs till på panelen.
1. Ange flera värden i fältet Flervärde avgränsat med avgränsarna och utför sökningen. Predikatet hämtar en exakt textmatchning för de värden du anger.

## Lägg till ett taggpredikat {#adding-a-tags-predicate}

Med `Tags`-predikatet kan du utföra taggbaserade sökningar efter resurser. Som standard söker AEM Assets efter resurser efter en eller flera taggar som matchar baserat på de taggar du anger. Med andra ord utför sökfrågan en ELLER-åtgärd med de angivna taggarna. Du kan dock använda alternativet Matcha alla taggar för att söka efter resurser som innehåller alla taggar som du anger.

1. Klicka på AEM-logotypen och gå sedan till **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. På sidan Sök i Forms väljer du **[!UICONTROL Assets Admin Search Rail]** och trycker sedan på **Redigera** ![aemassets_edit](assets/aemassets_edit.png).
1. På sidan Redigera sökformulär drar du **[!UICONTROL Tags Predicate]** från fliken Välj predikat till huvudrutan.
1. Ange en platshållartext för predikatet på fliken Inställningar. Ange egenskapsnamnet som ska användas för sökningen i egenskapsfältet, till exempel `jcr:content/metadata/cq:tags`. Du kan också välja en nod i CRXDE i urvalsdialogrutan.
1. Konfigurera sökvägsegenskapen för rottaggar för det här predikatet för att fylla i olika taggar i listan Taggar.
1. Välj **[!UICONTROL Show match all tags option]** om du vill söka efter resurser som innehåller alla taggar du anger.

   ![Vanliga inställningar för taggar-predikat](assets/tags_predicate.png)

1. Ange en valfri beskrivning i fältet **[!UICONTROL Description]** och klicka/tryck sedan på **[!UICONTROL Done]**.
1. Navigera till sökpanelen. **[!UICONTROL Tags]**-predikatet läggs till i sökpanelen.
1. Ange taggar baserat på vilka du vill söka efter resurser eller välj från listan med förslag.
1. Välj **[!UICONTROL Match all]** om du vill söka efter matchningar som innehåller alla taggar som du anger.

## Lägger till andra predikat {#adding-other-predicates}

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
   <td>Sök på predikatet för att utföra fullständig textsökning på en hel objektnod. Den mappas med operatorn <code>jcr</code>:<code>contains</code>. Du kan ange en relativ sökväg om du vill utföra en fullständig textsökning på en viss del av resursnoden.</td>
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
   <td><p>Date</p> </td>
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
   <td>Klassificering</td>
   <td>Sökprediktion för att söka efter resurser baserat på deras genomsnittliga klassificering </td>
   <td>
    <ul>
     <li>Etikett</li>
     <li>Egenskapsnamn</li>
     <li>Alternativ bana</li>
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

## Återställ standardsökfaktorer {#restoring-default-search-facets}

Som standard visas en låsikon före **[!UICONTROL Assets Admin Search Rail]** på **[!UICONTROL Search Forms]**-sidan. Ikonen Lås försvinner om du lägger till sökfaktorer i formuläret, vilket anger att standardformuläret har ändrats.

Låsikonen mot ett alternativ på söksidan i Forms anger att standardinställningarna är intakta och inte anpassade.

Så här återställer du standardsökaspekten:

1. Välj **[!UICONTROL Assets Admin Search Rail]** på sidan **[!UICONTROL Search Forms]**.
1. Tryck på **[!UICONTROL Delete]** ![borttagningsikonen](assets/do-not-localize/deleteoutline.png) i verktygsfältet.
1. I bekräftelsedialogrutan trycker du på **[!UICONTROL Delete]** för att ta bort de anpassade ändringarna.

   När du har tagit bort de anpassade ändringarna för sökfasetter visas låsikonen igen före **[!UICONTROL Assets Admin Search Rail]** på sidan **[!UICONTROL Search Forms]**.

## Användarbehörigheter {#user-permissions}

Om du inte har tilldelats en administratörsroll finns det en lista med behörigheter som du behöver för att utföra redigerings-, borttagnings- och förhandsgranskningsåtgärder som omfattar sökfaktorer.

| Åtgärd | Behörighet |
|---|---|
| Redigera | Läs- och skrivbehörigheter på `/apps`-noden i CRX. |
| Ta bort | Läsa, skriva och ta bort behörigheter på `/apps`-noden i CRX. |
| Förhandsgranska | Läsa, skriva och ta bort behörigheter på `/var/dam/content`-noden i CRX. Läs- och skrivbehörigheter på noden `/apps`. |

>[!MORELIKETHIS]
>
>* [Sök efter digitala resurser](search-assets.md).

