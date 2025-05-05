---
title: Konfigurera plugin-programmen för RTF-redigeraren i  [!DNL Adobe Experience Manager].
description: Lär dig konfigurera  [!DNL Adobe Experience Manager] plugin-programmen för textredigeraren.
contentOwner: AG
mini-toc-levels: 1
exl-id: 91619662-e865-47d1-8bec-0739f402353a
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '4281'
ht-degree: 0%

---

# Konfigurera plugin-programmen för RTF-redigeraren {#configure-the-rich-text-editor-plug-ins}

RTE-funktioner är tillgängliga via en serie plugin-program, var och en med features-egenskaper. Du kan konfigurera egenskapen features så att en eller flera RTE-funktioner aktiveras eller inaktiveras. I den här artikeln beskrivs hur du specifikt konfigurerar RTE-plugin-program.

Mer information om de andra RTE-konfigurationerna finns i [Konfigurera RTF-redigeraren](/help/implementing/developing/extending/rich-text-editor.md).

>[!NOTE]
>
>När du arbetar med CRXDE Lite bör du spara ändringarna regelbundet med alternativet [!UICONTROL Save All].

## Aktivera ett plugin-program och konfigurera egenskapen features {#activateplugin}

Följ de här stegen för att aktivera ett plugin-program. Vissa steg behövs bara när du konfigurerar ett plugin-program för första gången, eftersom motsvarande noder inte finns.

Som standard är plugin-programmen `format`, `link`, `list`, `justify` och `control` och alla deras funktioner aktiverade i RTE.

>[!NOTE]
>
>Motsvarande `rtePlugins`-nod kallas `<rtePlugins-node>` för att undvika dubbletter i den här artikeln.

1. Leta reda på textkomponenten för ditt projekt med CRXDE Lite.
1. Skapa den överordnade noden `<rtePlugins-node>` om den inte finns innan du konfigurerar några RTE-plugin-program:

   * Beroende på vilken komponent du har är de överordnade noderna:

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * en alternativ konfigurationsnod: `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`

   * Är av typen: **jcr:primärType** `cq:Widget`
   * Båda har följande egenskap:

      * **Namn** `name`
      * **Typ** `String`
      * **Värde** `./text`

1. Beroende på vilket gränssnitt du konfigurerar för skapar du en nod `<rtePlugins-node>`, om den inte finns:

   * **Namn** `rtePlugins`
   * **Typ** `nt:unstructured`

1. Under detta skapar du en nod för varje plugin-program som du vill aktivera:

   * **Typ** `nt:unstructured`
   * **Namn** plug-in-ID:t för plug-in-programmet krävs

När du har aktiverat ett plugin-program följer du de här riktlinjerna för att konfigurera egenskapen `features`.

| | Aktivera alla funktioner | Aktivera några specifika funktioner. | Inaktivera alla funktioner. |
|---|---|---|---|
| Namn | funktioner | funktioner | funktioner |
| Typ | Sträng | `String` (multi-string; ange Type till `String` och klicka på `Multi` i CRXDE Lite) | Sträng |
| Värde | `*` (en asterisk) | Ange ett eller flera funktionsvärden. | - |

## Förstå plugin-programmet findreplace {#findreplace}

Plugin-programmet `findreplace` behöver ingen konfiguration. Det går som det ska.

När du använder ersättningsfunktionen bör du ange ersättningssträngen samtidigt som söksträngen. Du kan dock fortfarande klicka på Sök för att söka efter strängen innan du ersätter den. Om ersättningssträngen anges efter att du klickat på Sök återställs sökningen till början av texten.

Dialogrutan Sök och ersätt blir genomskinlig när du klickar på Sök och blir ogenomskinlig när du klickar på Ersätt. På så sätt kan författaren granska den text som ska ersättas. Om användare klickar på Ersätt alla stängs dialogrutan och visar antalet ersättningar som gjorts.

## Konfigurera inklistringslägena {#pastemodes}

När du använder RTE kan författare klistra in innehåll i något av följande tre lägen:

* **Webbläsarläge**: Klistra in text med webbläsarens standardimplementering för inklistring. Det är inte en rekommenderad metod eftersom den kan medföra oönskad markering.

* **Oformaterad text**: Klistra in urklippsinnehållet som oformaterad text. Den raderar alla formatelement från det kopierade innehållet innan den infogas i komponenten [!DNL Experience Manager].

* **MS Word-läge**: Klistra in texten, inklusive tabeller, med formatering vid kopiering från MS Word. Det går inte att kopiera och klistra in text från en annan källa, t.ex. en webbsida eller MS Excel, utan endast partiell formatering.

### Konfigurera de inklistringsalternativ som finns i verktygsfältet RTE  {#configure-paste-options-available-on-the-rte-toolbar}

Du kan ange några, alla eller inga av dessa tre ikoner till författarna i verktygsfältet för textredigering:

* **[!UICONTROL Paste (Ctrl+V)]**: Kan förkonfigureras så att det motsvarar något av de tre inklistringslägena ovan.

* **[!UICONTROL Paste as Text]**: Tillhandahåller funktioner för normalt textläge.

* **[!UICONTROL Paste from Word]**: Tillhandahåller MS Word-lägesfunktioner.

Följ de här stegen för att konfigurera RTE så att nödvändiga ikoner visas.

1. Navigera till komponenten, till exempel `/apps/<myProject>/components/text`.
1. Navigera till noden `rtePlugins/edit`. Se [aktivera ett plugin-program](#activateplugin) om noden inte finns.
1. Skapa egenskapen `features` på noden `edit` och lägg till en eller flera funktioner. Spara alla ändringar.

### Konfigurera beteendet för ikonen Klistra in (Ctrl+V) och genvägen {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

Du kan förkonfigurera beteendet för ikonen **[!UICONTROL Paste (Ctrl+V)]** med följande steg. Den här konfigurationen definierar också beteendet för kortkommandot Ctrl+V som författare använder för att klistra in innehåll.

Konfigurationen tillåter följande tre typer av användningsfall:

* Klistra in text med webbläsarens standardimplementering för inklistring. Det är inte en rekommenderad metod eftersom den kan medföra oönskad markering. Konfigurerad med `browser` nedan.

* Klistra in urklippsinnehållet som ren text. Den raderar alla formatelement från det kopierade innehållet innan den infogas i komponenten [!DNL Experience Manager]. Konfigurerad med `plaintext` nedan.

* Klistra in texten, inklusive tabeller, med formatering när du kopierar från MS Word. Det går inte att kopiera och klistra in text från en annan källa, t.ex. en webbsida eller MS Excel, utan endast partiell formatering. Konfigurerad med `wordhtml` nedan.

1. Gå till noden `<rtePlugins-node>/edit` i komponenten. Skapa noderna om noderna inte finns. Mer information finns i [Aktivera ett plugin-program](#activateplugin).
1. Skapa en egenskap i noden `edit` med följande information:

   * **Namn** `defaultPasteMode`
   * **Typ** `String`
   * **Värde** är ett av de obligatoriska inklistringslägena från `browser`, `plaintext` eller `wordhtml`.

### Konfigurera de format som tillåts när innehåll klistras in {#pasteformats}

Läget Klistra in som Microsoft-Word (`paste-wordhtml`) kan konfigureras ytterligare så att du uttryckligen kan tillåta några format när du klistrar in i [!DNL Experience Manager] från ett annat program, till exempel [!DNL Microsoft Word].

Om till exempel endast fet stil och listor ska tillåtas när du klistrar in i [!DNL Experience Manager] kan du filtrera bort de andra formaten. Detta kallas konfigurerbar inklistringsfiltrering, vilket kan göras för båda:

* [Text](#pastemodes)
* [Länkar](#linkstyles)

För länkar kan du också definiera de protokoll som automatiskt godkänns.

Så här konfigurerar du vilka format som tillåts när du klistrar in text i [!DNL Experience Manager] från ett annat program:

1. Gå till noden `<rtePlugins-node>/edit` i din komponent. Skapa noderna om noden inte finns. Mer information finns i [Aktivera ett plugin-program](#activateplugin).
1. Skapa en nod under noden `edit` som innehåller inklistringsreglerna för HTML:

   * **Namn** `htmlPasteRules`
   * **Typ** `nt:unstructured`

1. Skapa en nod under `htmlPasteRules` som innehåller information om de grundläggande formaten som tillåts:

   * **Namn** `allowBasics`
   * **Typ** `nt:unstructured`

1. Om du vill kontrollera vilka enskilda format som accepteras skapar du en eller flera av följande egenskaper på noden `allowBasics`:

   * **Namn** `bold`
   * **Namn** `italic`
   * **Namn** `underline`
   * **Namn** `anchor` (för både länkar och namngivna ankare)
   * **Namn** `image`

   Alla egenskaper har typen **Type** `Boolean`, så i rätt **Value** kan du antingen markera eller ta bort markeringen för att aktivera eller inaktivera funktionen.

   >[!NOTE]
   >
   >Om det inte uttryckligen definieras används standardvärdet true och formatet accepteras.

1. Andra format kan också definieras med hjälp av ett intervall av andra egenskaper eller noder, som även tillämpas på noden `htmlPasteRules`:

| Egenskap | Typ | Beskrivning |
|--- |--- |--- |
| `allowBlockTags` | `String` | Definierar listan med blocktaggar som tillåts. Några möjliga blocktaggar är rubriker (h1, h2, h3), stycken (p), listor (ol, ul), tabeller (table). |
| `fallbackBlockTag` | `String` | Definierar den blocktagg som används för alla block med en blocktagg som inte ingår i `allowBlockTags`. Oftast räcker `p`. |
| `table` | `nt:unstructured` | Definierar beteendet när tabeller klistras in. Den här noden måste ha egenskapen allow (type Boolean) för att definiera om inklistring av tabeller tillåts. Om allow anges till false måste du ange egenskapen ignoreMode (typ String) för att definiera hur inklistrat tabellinnehåll ska hanteras. Giltiga värden för ignoreMode är `remove` för att ta bort tabellinnehåll och `paragraph` för att omvandla tabellceller till stycken. |
| `list` | `nt:unstructured` | Definierar beteendet när listor klistras in. Måste ha egenskapen `allow` (boolesk typ) för att definiera om inklistring av listor är tillåten. Om `allow` är inställt på `false` anger du egenskapen `ignoreMode` (typ `String`) för att definiera hur allt listinnehåll som klistras in ska hanteras. Giltiga värden för ignoreMode är `remove` som tar bort listinnehåll och `paragraph` som omvandlar listobjekt till stycken. |

Ett exempel på en giltig `htmlPasteRules`-struktur visas nedan:

```xml
"htmlPasteRules": {
    "allowBasics": {
        "italic": true,
        "link": true
    },
    "allowBlockTags": [
        "p", "h1", "h2", "h3"
    ],
    "list": {
        "allow": false,
        "ignoreMode": "paragraph"
    },
    "table": {
        "allow": true,
        "ignoreMode": "paragraph"
    }
}
```

1. Spara alla ändringar.

## Konfigurera textformat {#textstyles}

Författare kan använda format för att ändra utseendet på en del av texten. Formaten baseras på CSS-klasser som du fördefinierar i din CSS-formatmall. Stiliserat innehåll omges av `span`-taggar som använder attributet `class` för att referera till CSS-klassen. Till exempel:

`<span class=monospaced>Monospaced Text Here</span>`

När plugin-programmet Styles är aktiverat för första gången finns det inga standardformat. Popup-listan är tom. Så här ger du författarna formatmallar:

* Aktivera den nedrullningsbara listrutan Format.
* Ange en eller flera platser för formatmallarna.
* Ange de enskilda format som kan väljas i popup-listan för format.

Om du vill lägga till fler format senare, t.ex. följer du bara instruktionerna för att referera till en ny formatmall och ange de ytterligare formaten.

>[!NOTE]
>
>Format kan också definieras för [tabeller eller tabellceller](configure-rich-text-editor-plug-ins.md#tablestyles). Dessa konfigurationer kräver separata procedurer.

### Aktivera den nedrullningsbara listan Format för väljare {#styleselectorlist}

Detta görs genom att plugin-programmet för format aktiveras.

1. Gå till noden `<rtePlugins-node>/styles` i din komponent. Skapa noderna om noderna inte finns. Mer information finns i [Aktivera ett plugin-program](#activateplugin).
1. Skapa egenskapen `features` på noden `styles`:

   * **Namn** `features`
   * **Typ** `String`
   * **Värde** `*` (asterisk)

1. Spara alla ändringar.

>[!NOTE]
>
>När plugin-programmet Format är aktiverat visas listrutan Format i redigeringsdialogrutan. Listan är dock tom eftersom inga format har konfigurerats.

### Ange formatmallens plats {#locationofstylesheet}

Ange sedan platsen/platserna för de formatmallar som du vill referera till:

1. Navigera till rotnoden för textkomponenten, till exempel `/apps/<myProject>/components/text`.
1. Lägg till egenskapen `externalStyleSheets` i den överordnade noden för `<rtePlugins-node>`:

   * **Namn** `externalStyleSheets`
   * **Typ** `String[]` (flersträng; klicka på **Flera** i CRXDE)
   * **Värden** Sökvägen och filnamnet för alla formatmallar som du vill ta med. Använd databassökvägar.

   >[!NOTE]
   >
   >Du kan när som helst lägga till referenser till ytterligare formatmallar.

1. Spara alla ändringar.

När du använder textredigering i en dialogruta (Classic UI) kan du ange formatmallar som är optimerade för textredigering. På grund av tekniska begränsningar förloras CSS-kontexten i redigeraren, så du kan emulera den här kontexten för att förbättra WYSIWYG-upplevelsen.

I Rich Text Editor används ett behållar-DOM-element med ID `CQrte` som tillhandahåller olika format för att visa och redigera:

```css
#CQ td {
// defines the style for viewing
 }
```

```css
#CQrte td {
 // defines the style for editing
 }
```

### Ange tillgängliga format i popup-listan {#stylesindropdown}

1. I komponentdefinitionen går du till noden `<rtePlugins-node>/styles`, som den har skapats i [Aktivera listruteväljaren för format](#styleselectorlist).
1. Skapa en nod (kallas även `styles`) under noden `styles` för att hålla listan tillgänglig:

   * **Namn** `styles`
   * **Typ** `cq:WidgetCollection`

1. Skapa en nod under noden `styles` som representerar ett enskilt format:

   * **Namn**, du kan ange namnet, men det bör vara lämpligt för formatet
   * **Typ** `nt:unstructured`

1. Lägg till egenskapen `cssName` i den här noden för att referera till CSS-klassen:

   * **Namn** `cssName`
   * **Typ** `String`
   * **Värde** Namnet på CSS-klassen (utan föregående &#39;.&#39;); till exempel `cssClass` i stället för `.cssClass`)

1. Lägg till egenskapen `text` i samma nod. Detta definierar texten som visas i markeringsrutan:

   * **Namn** `text`
   * **Typ** `String`
   * **Värde** Beskrivning av formatet. Det visas i den nedrullningsbara listrutan Format.

1. Spara ändringarna.

   Upprepa stegen ovan för alla obligatoriska format.

### Konfigurera RTE för optimala ordbrytningar på japanska {#jpwordwrap}

Författare som använder [!DNL Experience Manager] för att skapa japanskt språkinnehåll kan använda ett format på tecken för att undvika radbrytning där en radbrytning inte krävs. Detta gör att författare kan låta meningarna brytas vid den önskade positionen. Formatet för den här funktionen baseras på CSS-klassen som är fördefinierad i CSS-formatmallen.

Så här skapar du det format som författare kan använda på japansk text:

1. Skapa en nod under noden Styles. Se [ange ett format](#stylesindropdown).
   * Namn: `jpn-word-wrap`
   * Typ: `nt:unstructure`

1. Lägg till egenskapen `cssName` i noden för att referera till CSS-klassen. Klassnamnet är ett reserverat namn för japansk radbrytning.
   * Namn: `cssName`
   * Typ: `String`
   * Värde: `jpn-word-wrap` (utan föregående `.`)

1. Lägg till egenskapstexten i samma nod. Värdet är namnet på formatet som författarna ser när de väljer formatet.
   * Namn: `text`
*Typ: `String`
   * Värde: `Japanese word-wrap`

1. Skapa en formatmall och ange dess sökväg. Se [ange plats för formatmallen](#locationofstylesheet). Lägg till följande innehåll i formatmallen. Ändra bakgrundsfärgen efter behov.

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![Formatmall för att göra japansk radbrytning tillgänglig för författare](assets/rte_jpwordwrap_stylesheet.jpg)

## Konfigurera styckeformat {#paraformats}

All text som har skapats i RTE placeras i en blocktagg, standardvärdet är `<p>`. Genom att aktivera plugin-programmet `paraformat` anger du ytterligare blocktaggar som kan tilldelas stycken med hjälp av en nedrullningsbar markeringslista. Styckeformat bestämmer stycketypen genom att tilldela rätt blocktagg. Författaren kan markera och tilldela dem med formatväljaren. Exempelblocktaggarna innehåller bland annat standardstycket &lt;p> och rubrikerna &lt;h1>, &lt;h2> och så vidare.

>[!CAUTION]
>
>Det här plugin-programmet passar inte för innehåll med komplex struktur, till exempel listor eller tabeller.

>[!NOTE]
>
>Om en blocktagg, till exempel en `<hr>`-tagg, inte kan tilldelas till ett stycke, är det inte ett giltigt användningsfall för ett `paraformat` -plugin-program.

När plugin-programmet Styckeformat är aktiverat för första gången är inga standardstyckeformat tillgängliga. Popup-listan är tom. Så här förser du författarna med styckeformat:

* Aktivera listan [!UICONTROL Format] för snabbväljare.
* Ange de blocktaggar som kan markeras som styckeformat på snabbmenyn.

För senare omkonfigurationer, till exempel för att lägga till fler format, följ bara relevanta delar av instruktionerna.

### Aktivera den nedrullningsbara formatväljaren {#formatselectorlist}

Så här aktiverar du plugin-programmet `paraformat`:

1. Gå till noden `<rtePlugins-node>/paraformat` i din komponent. Skapa noderna om noderna inte finns. Mer information finns i [Aktivera ett plugin-program](#activateplugin).
1. Skapa egenskapen `features` på noden `paraformat`:

   * **Namn** `features`
   * **Typ** `String`
   * **Värde** `*` (asterisk)

>[!NOTE]
>
>Om plugin-programmet inte har konfigurerats ytterligare är standardformaten som aktiveras Stycke ( `<p>`), Rubrik 1 ( `<h1>`), Rubrik 2 ( `<h2>`), Rubrik 3 ( `<h3>`).

>[!CAUTION]
>
>När du konfigurerar styckeformaten för textredigeraren ska du inte ta bort stycketaggen &lt;p> som ett formateringsalternativ. Om taggen `<p>` tas bort kan innehållsförfattaren inte välja alternativet [!UICONTROL Paragraph formats] även om ytterligare format har konfigurerats.

### Ange tillgängliga styckeformat {#paraformatsindropdown}

Styckeformat blir tillgängliga för markering av:

1. I komponentdefinitionen går du till noden `<rtePlugins-node>/paraformat`, som den har skapats i [Aktivera listruteväljaren för format](#styleselectorlist).
1. Under noden `paraformat` skapar du en nod som innehåller listan med format:

   * **Namn** `formats`
   * **Typ** `cq:WidgetCollection`

1. Skapa en nod under noden `formats`. Detta innehåller information om ett enskilt format:

   * **Namn**, du kan ange namnet, men det bör vara lämpligt för formatet (till exempel minstycke, minrubrik1).
   * **Typ** `nt:unstructured`

1. I den här noden lägger du till egenskapen för att definiera den blocktagg som används:

   * **Namn** `tag`
   * **Typ** `String`
   * **Värde** Blocktaggen för formatet, till exempel p, h1, h2 och så vidare.

     Du behöver inte ange vinkelavgränsare.

1. Om du vill lägga till en annan egenskap för samma nod visas beskrivande text i listrutan:

   * **Namn** `description`
   * **Typ** `String`
   * **Värde** Den beskrivande texten för det här formatet, till exempel Stycke, Rubrik 1, Rubrik 2 och så vidare. Den här texten visas i listan Format.

1. Spara ändringarna.

   Upprepa stegen för alla obligatoriska format.

>[!CAUTION]
>
>Om du definierar anpassade format tas standardformaten (`<p>`, `<h1>`, `<h2>` och `<h3>`) bort. Återskapa formatet `<p>` eftersom det är standardformatet.

## Konfigurera specialtecken {#spchar}

I en standardinstallation av [!DNL Experience Manager], när plugin-programmet `misctools` är aktiverat för specialtecken (`specialchars`), är ett standardval omedelbart tillgängligt för användning, till exempel copyright- och varumärkessymboler.

Du kan konfigurera textredigeraren så att ditt val av tecken blir tillgängligt, antingen genom att definiera distinkta tecken eller en hel sekvens.

>[!CAUTION]
>
>Om du lägger till specialtecken åsidosätts standardvalet. Om det behövs definierar du om de här tecknen i markeringen.

### Definiera ett enskilt tecken {#definesinglechar}

1. Gå till noden `<rtePlugins-node>/misctools` i din komponent. Skapa noderna om noderna inte finns. Mer information finns i [Aktivera ett plugin-program](#activateplugin).
1. Skapa egenskapen `features` på noden `misctools`:

   * **Namn** `features`
   * **Typ** `String[]`
   * **Värde** `specialchars`

         (eller `String / *` om du använder alla funktioner för det här plugin-programmet)

1. Under `misctools` skapar du en nod som innehåller specialteckenkonfigurationer:

   * **Namn** `specialCharsConfig`
   * **Typ** `nt:unstructured`

1. Under `specialCharsConfig` skapar du en annan nod som innehåller teckenlistan:

   * **Namn** `chars`
   * **Typ** `nt:unstructured`

1. Under `chars` lägger du till en nod för en enskild teckendefinition:

   * **Namn** kan du ange namnet, men det ska återspegla tecknet, till exempel hälften.
   * **Typ** `nt:unstructured`

1. Lägg till följande egenskap för den här noden:

   * **Namn** `entity`
   * **Typ** `String`
   * **Värde** är HTML-representationen av det obligatoriska tecknet, till exempel `&189;` för bråket i halva.

1. Spara ändringarna.

I CRXDE visas det representerade tecknet när egenskapen har sparats. Se exemplet nedan. Upprepa stegen ovan om du vill göra fler specialtecken tillgängliga för författare.

![I CRXDE lägger du till ett enda tecken som ska vara tillgängligt i RTE-verktygsfältet](assets/chlimage_1-106.png "I CRXDE lägger du till ett enda tecken som ska vara tillgängligt i RTE-verktygsfältet")

### Definiera ett teckenintervall {#definerangechar}

1. Använd steg 1 till 3 från [Definiera ett enskilt tecken](#definesinglechar).
1. Under `chars` lägger du till en nod som innehåller definitionen av teckenintervallet:

   * **Namn** kan du ange namnet, men det bör återspegla teckenintervallet, till exempel pennor.
   * **Typ** `nt:unstructured`

1. Lägg till följande två egenskaper under den här noden (namngivna enligt ditt teckenintervall):

   * **Namn** `rangeStart`

     **Typ** `Long`
     **Värde** för [Unicode](https://unicode.org/)-representationen (decimal) av det första tecknet i intervallet

   * **Namn** `rangeEnd`

     **Typ** `Long`
     **Värde** för [Unicode](https://unicode.org/)-representationen (decimal) av det sista tecknet i intervallet

1. Spara ändringarna.

   Om du definierar ett intervall från 9998 till 10000 får du följande tecken.

   ![I CRXDE definierar du ett teckenintervall som ska vara tillgängligt i RTE](assets/chlimage_1-107.png)

   *Bild: I CRXDE definierar du ett teckenintervall som ska vara tillgängligt i RTE*

   ![Specialtecken som är tillgängliga i textredigeraren visas för författare i ett popup-fönster](assets/rtepencil.png "Specialtecken som är tillgängliga i textredigeraren visas för författare i ett popup-fönster")

## Konfigurera tabellformat {#tablestyles}

Format används vanligtvis på text, men du kan också använda separata formatmallar i en tabell eller i ett fåtal tabellceller. Sådana format är tillgängliga för författare i rutan Formatväljare i antingen dialogrutan Cellegenskaper eller Tabellegenskaper. Stilarna är tillgängliga när du redigerar en tabell i en Text-komponent (eller en variabel) och inte i standardkomponenten för tabeller.

>[!NOTE]
>
>Du kan endast definiera format för tabeller och celler för det klassiska användargränssnittet.

>[!NOTE]
>
>Kopiering och inklistring av tabeller i eller från RTE-komponenten är webbläsarberoende. Det stöds inte i alla webbläsare. Du kan få olika resultat beroende på tabellstruktur och webbläsare. Om du till exempel kopierar och klistrar in en tabell i en RTE-komponent i Mozilla Firefox i Classic UI och Touch UI, bevaras inte tabellens layout.

1. Gå till noden `<rtePlugins-node>/table` i komponenten. Skapa noderna om noderna inte finns. Mer information finns i [Aktivera ett plugin-program](#activateplugin).
1. Skapa egenskapen `features` på noden `table`:

   * **Namn** `features`
   * **Typ** `String`
   * **Värde** `*`

   >[!NOTE]
   >
   >Om du inte vill aktivera alla tabellfunktioner kan du skapa egenskapen `features` som:
   >
   >* **Typ** `String[]`
   >
   >* **Värde**, eller båda, av följande, efter behov:
   >* `table` om du vill tillåta redigering av tabellegenskaper, inklusive format.
   >* `cellprops` om du vill tillåta redigering av cellegenskaper, inklusive format.

1. Definiera platsen för CSS-formatmallar för att referera till dem. Se [Ange platsen för formatmallen](#locationofstylesheet) eftersom detta är samma som när du definierar [format för text](#textstyles). Platsen kan definieras om du har definierat andra format.
1. Skapa följande noder under noden `table` efter behov:

   * Så här definierar du format för hela tabellen (tillgänglig under **[!UICONTROL Table properties]**):

      * **Namn** `tableStyles`
      * **Typ** `cq:WidgetCollection`

   * Om du vill definiera format för de enskilda cellerna (tillgängliga under **[!UICONTROL Cell properties]**),

      * **Namn** `cellStyles`
      * **Typ** `cq:WidgetCollection`

1. Skapa en nod (under noden `tableStyles` eller `cellStyles` efter behov) som representerar ett enskilt format,

   * **Namn** kan du ange namnet, men det bör återspegla formatet.
   * **Typ** `nt:unstructured`

1. Skapa egenskaperna på den här noden:

   * Om du vill definiera CSS-formatet som refereras till

      * **Namn** `cssName`
      * **Typ** `String`
      * **Värde** namnet på CSS-klassen (utan föregående `.`, till exempel `cssClass` i stället för `.cssClass`)

   * Om du vill definiera en beskrivande text som ska visas i snabbväljaren

      * **Namn** `text`
      * **Typ** `String`
      * **Värde** den text som ska visas i markeringslistan

1. Spara alla ändringar.

Upprepa stegen ovan för alla obligatoriska format.

### Konfigurera dolda rubriker i tabeller för tillgänglighet {#hiddenheader}

Ibland kan du skapa datatabeller utan visuell text i en kolumnrubrik om rubrikens syfte beror på kolumnens visuella förhållande till andra kolumner. I det här fallet är det nödvändigt att tillhandahålla dold inre text i cellen i rubrikcellen så att skärmläsare och andra hjälpmedelstekniker kan hjälpa läsare med olika behov att förstå vad kolumnen ska användas till.

RTE har stöd för dolda rubrikceller för att förbättra tillgängligheten i sådana scenarier. Dessutom innehåller den konfigurationsinställningar för dolda rubriker i tabeller. Med de här inställningarna kan du använda CSS-format på dolda rubriker i redigerings- och förhandsgranskningslägena. Om du vill hjälpa författare att identifiera dolda rubriker i redigeringsläget kan du inkludera följande parametrar i koden:

* `hiddenHeaderEditingCSS`: Anger namnet på CSS-klassen som används i den dolda rubrikcellen när RTE redigeras.
* `hiddenHeaderEditingStyle`: Anger en formatsträng som används i den dolda rubrikcellen när textredigeringsmatrisen redigeras.

Om du anger både CSS och formatsträngen i koden har CSS-klassen företräde framför formatsträngen och kan skriva över alla konfigurationsändringar som formatsträngen gör.

För att hjälpa författare att använda CSS på dolda rubriker i förhandsgranskningsläget kan du inkludera följande parametrar i koden:

* `hiddenHeaderClassName`: Anger namnet på CSS-klassen som används i den dolda rubrikcellen i förhandsgranskningsläge.
* `hiddenHeaderStyle`: Anger en formatsträng som används i cellen med dolda rubriker i förhandsgranskningsläget.

Om du anger både CSS och formatsträngen i koden har CSS-klassen företräde framför formatsträngen och kan skriva över alla konfigurationsändringar som formatsträngen gör.

## Lägg till ordlistor för stavningskontrollen {#adddict}

När plugin-programmet för stavningskontroll är aktiverat används lexikon för respektive språk. Dessa väljs sedan enligt webbplatsens språk genom att antingen använda språkegenskapen för underträdet eller genom att extrahera språket från URL:en, till exempel. grenen `/en/` kontrolleras som engelsk, grenen `/de/` som tysk.

>[!NOTE]
>
>Meddelandet&quot;Stavningskontrollen misslyckades.&quot; visas om en kontroll görs för ett språk som inte är installerat.

En standardinstallation i Experience Manager innehåller ordlistor för:

* American English (en_us)
* Engelska (en_gb)

>[!NOTE]
>
>Standardordlistorna finns på `/libs/cq/spellchecker/dictionaries` tillsammans med rätt ReadMe-filer. Ändra inte filerna.

Följ de här stegen om du vill lägga till fler ordlistor, om det behövs.

1. Navigera till sidan [https://extensions.openoffice.org/](https://extensions.openoffice.org/).
1. Välj önskat språk och hämta ZIP-filen med stavningsdefinitionerna. Extrahera innehållet i arkivet i filsystemet.

   >[!CAUTION]
   >
   >Endast ordlistor i formatet `MySpell` för OpenOffice.org v2.0.1 eller tidigare stöds. Eftersom ordlistorna nu är arkivfiler rekommenderar vi att du kontrollerar arkivet efter nedladdningen.

1. Leta reda på .aff- och .dic-filerna. Behåll filnamnet med gemener. Till exempel `de_de.aff` och `de_de.dic`.
1. Läs in .aff- och .dic-filerna i databasen på `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
>
>Stavningskontrollen för textredigering är tillgänglig på begäran. Den körs inte automatiskt när du börjar skriva text.
>
>Om du vill stavningskontrollera väljer du stavningskontrollknappen i verktygsfältet. RTE kontrollerar stavningen av ord och markerar felstavade ord.
>
>Om du infogar någon ändring som stavningskontrollen föreslår markeras inte längre textens status och felstavade ord. Om du vill stavningskontrollera väljer du stavningskontrollknappen igen.

## Konfigurera historikstorlek för ångra- och gör om-åtgärder {#undohistory}

Med RTE kan författare ångra eller göra om några sista redigeringar. Som standard lagras 50 redigeringar i historiken. Du kan konfigurera det här värdet efter behov.

1. Gå till noden `<rtePlugins-node>/undo` i komponenten. Skapa de här noderna om de inte finns. Mer information finns i [Aktivera ett plugin-program](#activateplugin).
1. Skapa egenskapen på noden `undo`:

   * **Namn** `maxUndoSteps`
   * **Typ** `Long`
   * **Värde** anger antalet ångra-steg som du vill spara i historiken. Standardvärdet är 50. Använd `0` för att helt inaktivera ångra/gör om.

1. Spara ändringarna.

## Konfigurera flikstorleken {#tabsize}

När tabbtecknet trycks ned i en text infogas ett fördefinierat antal mellanslag. Som standard är detta tre fasta mellanslag och ett mellanslag.

Så här definierar du tabbstorleken:

1. Gå till noden `<rtePlugins-node>/keys` i din komponent. Skapa noderna om noderna inte finns. Mer information finns i [Aktivera ett plugin-program](#activateplugin).
1. Skapa egenskapen på noden `keys`:

   * **Namn** `tabSize`
   * **Typ** `String`
   * **Värde** anger antalet blankstegstecken som ska användas för tabulatorn.

1. Spara ändringarna.

## Ange indragsmarginal {#indentmargin}

När indrag är aktiverat (standard) kan du definiera storleken på indraget:

>[!NOTE]
>
>Den här indragsstorleken används bara för stycken (block) i text. Den påverkar inte indraget för verkliga listor.

1. Gå till noden `<rtePlugins-node>/lists` i komponenten. Skapa de här noderna om de inte finns. Mer information finns i [Aktivera ett plugin-program](#activateplugin).
1. Skapa parametern `identSize` på noden `lists`:

   * **Namn**: `identSize`
   * **Typ**: `Long`
   * **Värde**: antal pixlar som krävs för indragsmarginalen.

## Konfigurera höjden på det redigerbara utrymmet {#editablespace}

Du kan ange höjden på det redigerbara området som visas i komponentdialogrutan. Konfigurationen gäller endast när du använder RTE i en dialogruta. Konfigurationen ändrar inte höjden på dialogfönstret.

1. Skapa en egenskap i dialogdefinitionen för komponenten i noden `../items/text`:

   * **Namn** `height`
   * **Typ** `Long`
   * **Värdet** är höjden på arbetsytan för redigering i pixlar.

1. Spara ändringarna.

## Konfigurera format och protokoll för länkar {#linkstyles}

När du lägger till länkar i [!DNL Experience Manager] kan du definiera de CSS-format som ska användas och de protokoll som ska accepteras automatiskt. Om du vill konfigurera hur länkar läggs till i [!DNL Experience Manager] från ett annat program definierar du reglerna för HTML.

1. Leta reda på textkomponenten för ditt projekt med CRXDE Lite.
1. Skapa en nod på samma nivå som `<rtePlugins-node>`, d.v.s. skapa noden under den överordnade noden `<rtePlugins-node>`:

   * **Namn** `htmlRules`
   * **Typ** `nt:unstructured`

   >[!NOTE]
   >
   >Noden `../items/text` har egenskapen:
   >
   >* **Namn** `xtype`
   >* **Typ** `String`
   >* **Värde** `richtext`
   >
   >Platsen för noden `../items/text` kan variera beroende på strukturen i dialogrutan. Två exempel är `/apps/myProject>/components/text/dialog/items/text` och `/apps/<myProject>/components/text/dialog/items/panel/items/text`.

1. Skapa en nod under `htmlRules`.

   * **Namn** `links`
   * **Typ** `nt:unstructured`

1. Definiera egenskaperna under noden `links` efter behov:

   * CSS-format för interna länkar:

      * **Namn** `cssInternal`
      * **Typ** `String`
      * **Värde** namnet på CSS-klassen (utan föregående &#39;.&#39;); till exempel `cssClass` i stället för `.cssClass`)

   * CSS-format för externa länkar

      * **Namn** `cssExternal`
      * **Typ** `String`
      * **Värde** namnet på CSS-klassen (utan föregående &#39;.&#39;); till exempel `cssClass` i stället för `.cssClass`)

   * En matris med giltiga **[!UICONTROL protocols]** inklusive `https://`, `https://`, `file://`, `mailto:` med flera,

      * **Namn** `protocols`
      * **Typ** `String[]`
      * **Värde** ett eller flera protokoll

   * **defaultProtocol** (egenskap av typen **String**): Protokoll som ska användas om användaren inte uttryckligen angav ett.

      * **Namn** `defaultProtocol`
      * **Typ** `String`
      * **Värde** ett eller flera standardprotokoll

   * Definition av hur målattributet för en länk ska hanteras. Skapa en nod:

      * **Namn** `targetConfig`
      * **Typ** `nt:unstructured`

     På noden `targetConfig`: definiera de nödvändiga egenskaperna:

      * Ange målläge:

         * **Namn** `mode`
         * **Typ** `String`)
         * **Värde** :

            * `auto`: betyder att ett automatiskt mål har valts

              (anges av egenskapen `targetExternal` för externa länkar eller `targetInternal` för interna länkar).

            * `manual`: gäller inte i den här kontexten
            * `blank`: gäller inte i den här kontexten

      * Målet för interna länkar:

         * **Namn** `targetInternal`
         * **Typ** `String`
         * **Värde** målet för interna länkar (används endast när läget är `auto`)

      * Målet för externa länkar:

         * **Namn** `targetExternal`
         * **Typ** `String`
         * **Värde** är målet för externa länkar (används endast när läget är `auto`).

1. Spara alla ändringar.
