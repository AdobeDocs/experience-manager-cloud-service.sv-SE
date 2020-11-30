---
title: Konfigurera plugin-programmen [!DNL Adobe Experience Manager]för RTF-redigeraren.
description: Lär dig konfigurera [!DNL Adobe Experience Manager] plugin-program för textredigeraren.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 6db201f00e8f304122ca8c037998b363ff102c1f
workflow-type: tm+mt
source-wordcount: '4279'
ht-degree: 0%

---


# Konfigurera plugin-programmen för RTF-redigeraren {#configure-the-rich-text-editor-plug-ins}

RTE-funktioner är tillgängliga via en serie plugin-program, var och en med features-egenskaper. Du kan konfigurera egenskapen features så att en eller flera RTE-funktioner aktiveras eller inaktiveras. I den här artikeln beskrivs hur du specifikt konfigurerar RTE-plugin-program.

Mer information om de andra RTE-konfigurationerna finns i [Konfigurera RTF-redigeraren](/help/implementing/developing/extending/rich-text-editor.md).

>[!NOTE]
>
>När du arbetar med CRXDE Lite bör du spara ändringarna regelbundet med [!UICONTROL Save All] hjälp av ett alternativ.

## Aktivera ett plugin-program och konfigurera egenskapen features {#activateplugin}

Följ de här stegen för att aktivera ett plugin-program. Vissa steg behövs bara när du konfigurerar ett plugin-program för första gången, eftersom motsvarande noder inte finns.

Som standard aktiveras `format`plugin-program, `link`, `list`, `justify`och `control` alla deras funktioner i RTE.

>[!NOTE]
>
>Motsvarande `rtePlugins` nod kallas `<rtePlugins-node>` för att undvika dubbletter i den här artikeln.

1. Leta reda på textkomponenten för ditt projekt med CRXDE Lite.
1. Skapa den överordnade noden för `<rtePlugins-node>` om den inte finns innan du konfigurerar några RTE-plugin-program:

   * Beroende på vilken komponent du har är de överordnade noderna:

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * en alternativ konfigurationsnod: `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`
   * Är av typen: **jcr:primärType** `cq:Widget`
   * Båda har följande egenskap:

      * **Namn** `name`
      * **Typ** `String`
      * **Värde** `./text`


1. Beroende på vilket gränssnitt du konfigurerar för kan du skapa en nod `<rtePlugins-node>`om den inte finns:

   * **Namn** `rtePlugins`
   * **Typ** `nt:unstructured`

1. Under detta skapar du en nod för varje plugin-program som du vill aktivera:

   * **Typ** `nt:unstructured`
   * **Namnge** plug-in-ID:t för det plugin-program som krävs

När du har aktiverat ett plugin-program följer du de här riktlinjerna för att konfigurera `features` egenskapen.

|  | Aktivera alla funktioner | Aktivera några specifika funktioner. | Inaktivera alla funktioner. |
|---|---|---|---|
| Namn | funktioner | funktioner | funktioner |
| Typ | Sträng | `String` (multisträng; ange Type till `String` och klicka `Multi` i CRXDE Lite) | Sträng |
| Värde | `*` (en asterisk) | Ange ett eller flera funktionsvärden. | - |

## Förstå plugin-programmet findreplace {#findreplace}

Plugin- `findreplace` programmet behöver ingen konfiguration. Det går som det ska.

När du använder funktionen Ersätt bör du ange den ersättningssträng som ska ersättas samtidigt som söksträngen. Du kan dock fortfarande klicka på Sök för att söka efter strängen innan du ersätter den. Om ersättningssträngen anges efter att du klickat på Sök återställs sökningen till början av texten.

Dialogrutan Sök och ersätt blir genomskinlig när du klickar på Sök och blir ogenomskinlig när du klickar på Ersätt. På så sätt kan författaren granska texten som ska ersättas. Om användare klickar på Ersätt alla stängs dialogrutan och visar antalet ersättningar som gjorts.

## Konfigurera inklistringslägen {#pastemodes}

När du använder RTE kan författare klistra in innehåll i något av följande tre lägen:

* **Webbläsarläge**: Klistra in text med webbläsarens standardimplementering för inklistring. Det är inte en rekommenderad metod eftersom den kan medföra oönskad markering.

* **Läge** för oformaterad text: Klistra in urklippsinnehållet som oformaterad text. Alla formatelement från det kopierade innehållet tas bort innan de infogas i [!DNL Experience Manager] komponenten.

* **MS Word-läge**: Klistra in texten, inklusive tabeller, med formatering när du kopierar från MS Word. Det går inte att kopiera och klistra in text från en annan källa, t.ex. en webbsida eller MS Excel, utan endast partiell formatering.

### Konfigurera de inklistringsalternativ som finns i verktygsfältet för textredigering  {#configure-paste-options-available-on-the-rte-toolbar}

Du kan ange några, alla eller inga av dessa tre ikoner till författarna i verktygsfältet för textredigering:

* **[!UICONTROL Paste (Ctrl+V)]**: Kan förkonfigureras så att det motsvarar något av de tre inklistringslägena ovan.

* **[!UICONTROL Paste as Text]**: Innehåller funktioner för normalt textläge.

* **[!UICONTROL Paste from Word]**: Tillhandahåller MS Word-funktionalitet.

Följ de här stegen för att konfigurera RTE så att nödvändiga ikoner visas.

1. Navigera till komponenten, till exempel `/apps/<myProject>/components/text`.
1. Navigera till noden `rtePlugins/edit`. Se [Aktivera ett plugin-program](#activateplugin) om noden inte finns.
1. Skapa `features` egenskapen på `edit` noden och lägg till en eller flera funktioner. Spara alla ändringar.

### Konfigurera beteendet för ikonen Klistra in (Ctrl+V) och genvägen {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

Du kan förkonfigurera **[!UICONTROL Paste (Ctrl+V)]** ikonens beteende med följande steg. Den här konfigurationen definierar också beteendet för kortkommandot Ctrl+V som författare använder för att klistra in innehåll.

Konfigurationen tillåter följande tre typer av användningsfall:

* Klistra in text med webbläsarens standardimplementering för inklistring. Det är inte en rekommenderad metod eftersom den kan medföra oönskad markering. Konfigurerad med `browser` nedan.

* Klistra in urklippsinnehållet som oformaterad text. Alla formatelement från det kopierade innehållet tas bort innan de infogas i [!DNL Experience Manager] komponenten. Konfigurerad med `plaintext` nedan.

* Klistra in texten, inklusive tabeller, med formatering när du kopierar från MS Word. Det går inte att kopiera och klistra in text från en annan källa, t.ex. en webbsida eller MS Excel, utan endast partiell formatering. Konfigurerad med `wordhtml` nedan.

1. Navigera till `<rtePlugins-node>/edit` noden i komponenten. Skapa noderna om noderna inte finns. Mer information finns i [Aktivera ett plugin-program](#activateplugin).
1. Skapa en egenskap med följande information i noden: `edit`

   * **Namn** `defaultPasteMode`
   * **Typ** `String`
   * **Värdet** är ett av de obligatoriska inklistringslägena från `browser`, `plaintext`eller `wordhtml` .

### Konfigurera de format som tillåts när innehåll klistras in {#pasteformats}

Läget Klistra in som Microsoft-Word (`paste-wordhtml`) kan konfigureras ytterligare så att du uttryckligen kan tillåta några format när du klistrar in [!DNL Experience Manager] från ett annat program, till exempel [!DNL Microsoft Word].

Om till exempel endast fet stil och listor ska tillåtas när du klistrar in i [!DNL Experience Manager]kan du filtrera bort de andra formaten. Detta kallas konfigurerbar inklistringsfiltrering, vilket kan göras för båda:

* [Text](#pastemodes)
* [Länkar](#linkstyles)

För länkar kan du också definiera de protokoll som automatiskt godkänns.

Så här konfigurerar du vilka format som tillåts när du klistrar in text i [!DNL Experience Manager] från ett annat program:

1. Gå till noden i komponenten `<rtePlugins-node>/edit`. Skapa noderna om noden inte finns. Mer information finns i [Aktivera ett plugin-program](#activateplugin).
1. Skapa en nod under `edit` noden som innehåller HTML-inklistringsreglerna:

   * **Namn** `htmlPasteRules`
   * **Typ** `nt:unstructured`

1. Skapa en nod under `htmlPasteRules`, för information om de grundläggande formaten som tillåts:

   * **Namn** `allowBasics`
   * **Typ** `nt:unstructured`

1. Om du vill styra de enskilda format som accepteras skapar du en eller flera av följande egenskaper på `allowBasics` noden:

   * **Namn** `bold`
   * **Namn** `italic`
   * **Namn** `underline`
   * **Namn** `anchor` (för både länkar och namngivna ankare)
   * **Namn** `image`

   Alla egenskaper är av **typen** `Boolean`, så i rätt **värde** kan du antingen markera eller ta bort markeringen för att aktivera eller inaktivera funktionen.

   >[!NOTE]
   >
   >Om det inte uttryckligen definieras används standardvärdet true och formatet accepteras.

1. Andra format kan också definieras med hjälp av en rad andra egenskaper eller noder, som även kan användas på `htmlPasteRules` noden:

| Egenskap | Typ | Beskrivning |
|--- |--- |--- |
| `allowBlockTags` | `String` | Definierar listan med blocktaggar som tillåts. Några möjliga blocktaggar är rubriker (h1, h2, h3), stycken (p), listor (ol, ul), tabeller (table). |
| `fallbackBlockTag` | `String` | Definierar den blocktagg som används för alla block som har en blocktagg som inte ingår i `allowBlockTags`. Oftast räcker det `p` . |
| `table` | `nt:unstructured` | Definierar beteendet när tabeller klistras in. Den här noden måste ha egenskapen allow (type Boolean) för att definiera om inklistring av tabeller tillåts. Om allow anges till false måste du ange egenskapen ignoreMode (typ String) för att definiera hur inklistrat tabellinnehåll ska hanteras. Giltiga värden för ignoreMode är `remove` att ta bort tabellinnehåll och `paragraph` att omvandla tabellceller till stycken. |
| `list` | `nt:unstructured` | Definierar beteendet när listor klistras in. Måste ha egenskapen `allow` (typ av Boolean) för att definiera om inklistring av listor är tillåten. Om `allow` är inställt på `false`anger du egenskapen `ignoreMode` (typ `String`) för att definiera hur allt listinnehåll som klistras in ska hanteras. Giltiga värden för ignoreMode är `remove` att ta bort listinnehåll och `paragraph` att göra om listobjekt till stycken. |

Ett exempel på en giltig `htmlPasteRules` struktur visas nedan:

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

Författare kan använda format för att ändra utseendet på en del av texten. Formaten baseras på CSS-klasser som du fördefinierar i din CSS-formatmall. Stiliserat innehåll omsluts av `span` -taggar som använder attributet `class` för att referera till CSS-klassen. Till exempel:

`<span class=monospaced>Monospaced Text Here</span>`

När plugin-programmet Styles är aktiverat för första gången finns det inga standardformat. Popup-listan är tom. Så här förser du författarna med formatmallar:

* Aktivera den nedrullningsbara listrutan Format.
* Ange en eller flera platser för formatmallarna.
* Ange de enskilda format som kan väljas i popup-listan för format.

Om du vill lägga till fler format senare, t.ex. följer du bara instruktionerna för att referera till en ny formatmall och ange de ytterligare formaten.

>[!NOTE]
>
>Du kan också definiera format för [tabeller eller tabellceller](configure-rich-text-editor-plug-ins.md#tablestyles). Dessa konfigurationer kräver separata procedurer.

### Aktivera listrutan Format för väljare {#styleselectorlist}

Detta görs genom att plugin-programmet för format aktiveras.

1. Gå till noden i komponenten `<rtePlugins-node>/styles`. Skapa noderna om noderna inte finns. Mer information finns i [Aktivera ett plugin-program](#activateplugin).
1. Skapa `features` egenskapen på `styles` noden:

   * **Namn** `features`
   * **Typ** `String`
   * **Värde** `*` (asterisk)

1. Spara alla ändringar.

>[!NOTE]
>
>När plugin-programmet Format är aktiverat visas listrutan Format i redigeringsdialogrutan. Listan är dock tom eftersom inga format har konfigurerats.

### Ange formatmallens plats {#locationofstylesheet}

Ange sedan platsen/platserna för de formatmallar som du vill referera till:

1. Navigera till textkomponentens rotnod, till exempel `/apps/<myProject>/components/text`.
1. Lägg till egenskapen `externalStyleSheets` i den överordnade noden för `<rtePlugins-node>`:

   * **Namn** `externalStyleSheets`
   * **Typ** `String[]` (multisträng; klicka på **Flera** i CRXDE)
   * **Värden** Sökvägen och filnamnet för alla formatmallar som du vill ta med. Använd databassökvägar.

   >[!NOTE]
   >
   >Du kan när som helst lägga till referenser till ytterligare formatmallar.

1. Spara alla ändringar.

När du använder textredigering i en dialogruta (Classic UI) kan du ange formatmallar som är optimerade för textredigering. På grund av tekniska begränsningar förloras CSS-kontexten i redigeraren, så du kan emulera den här kontexten för att förbättra WYSIWYG-upplevelsen.

I Rich Text Editor används ett behållar-DOM-element med ett ID för `CQrte` som innehåller olika format för att visa och redigera:

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

1. I komponentdefinitionen navigerar du till noden `<rtePlugins-node>/styles`som den skapades i [Aktivera listruteväljaren](#styleselectorlist)för format.
1. Under noden `styles`skapar du en nod (kallas även `styles`) som innehåller listan som görs tillgänglig:

   * **Namn** `styles`
   * **Typ** `cq:WidgetCollection`

1. Skapa en nod under `styles` noden som representerar ett enskilt format:

   * **Namn**, du kan ange namnet, men det bör vara lämpligt för formatet
   * **Typ** `nt:unstructured`

1. Lägg till egenskapen `cssName` i den här noden som referens för CSS-klassen:

   * **Namn** `cssName`
   * **Typ** `String`
   * **Värde** Namnet på CSS-klassen (utan föregående &#39;.&#39;); for example, `cssClass` instead of `.cssClass`)

1. Lägg till egenskapen `text` i samma nod; definierar texten som visas i markeringsrutan:

   * **Namn** `text`
   * **Typ** `String`
   * **Värdebeskrivning** av formatet. visas i den nedrullningsbara listrutan Format.

1. Spara ändringarna.

   Upprepa stegen ovan för alla obligatoriska format.

### Konfigurera RTE för optimala ordbrytningar på japanska {#jpwordwrap}

Författare som använder [!DNL Experience Manager] för att skapa japanskt innehåll kan använda ett format på tecken för att undvika radbrytning där ingen radbrytning behövs. Detta gör att författare kan låta meningarna brytas vid önskad position. Formatet för den här funktionen baseras på CSS-klassen som är fördefinierad i CSS-formatmallen.

Så här skapar du det format som författare kan använda på japansk text:

1. Skapa en nod under noden Styles. Se [Ange ett format](#stylesindropdown).
   * Namn: `jpn-word-wrap`
   * Typ: `nt:unstructure`

1. Lägg till egenskapen `cssName` i noden för att referera till CSS-klassen. Klassnamnet är ett reserverat namn för japansk radbrytning.
   * Namn: `cssName`
   * Typ: `String`
   * Värde: `jpn-word-wrap` (utan föregående `.`)

1. Lägg till egenskapstexten i samma nod. Värdet är namnet på formatet som författarna ser när de väljer formatet.
   * Namn: `text`
*Typ: 
`String`
   * Värde: `Japanese word-wrap`

1. Skapa en formatmall och ange dess sökväg. Se [Ange plats för formatmallen](#locationofstylesheet). Lägg till följande innehåll i formatmallen. Ändra bakgrundsfärgen efter behov.

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![Formatmall som gör japansk radbrytning tillgänglig för författare](assets/rte_jpwordwrap_stylesheet.jpg)

## Konfigurera styckeformat {#paraformats}

All text som har skapats i RTE placeras i en blocktagg med standardvärdet `<p>`. Genom att aktivera plugin-programmet anger du ytterligare blocktaggar som kan tilldelas stycken med hjälp av en nedrullningsbar markeringslista. `paraformat` Styckeformat bestämmer stycketypen genom att tilldela rätt blocktagg. Författaren kan markera och tilldela dem med formatväljaren. Exempelblocktaggarna innehåller bland annat standardstycket &lt;p> och rubrikerna &lt;h1>, &lt;h2> och så vidare.

>[!CAUTION]
>
>Det här plugin-programmet passar inte för innehåll med komplex struktur, till exempel listor eller tabeller.

>[!NOTE]
>
>Om en blocktagg, t.ex. en `<hr>` tagg, inte kan tilldelas till ett stycke är det inte ett giltigt användningsfall för ett `paraformat` plugin-program.

När plugin-programmet Styckeformat är aktiverat för första gången är inga standardstyckeformat tillgängliga. Popup-listan är tom. Så här förser du författarna med styckeformat:

* Aktivera [!UICONTROL Format] popup-väljarlistan.
* Ange de blocktaggar som kan markeras som styckeformat på snabbmenyn.

För senare omkonfigurationer, till exempel för att lägga till fler format, följ bara relevanta delar av instruktionerna.

### Aktivera den nedrullningsbara formatväljaren {#formatselectorlist}

Så här aktiverar du `paraformat` plugin-programmet:

1. Gå till noden i komponenten `<rtePlugins-node>/paraformat`. Skapa noderna om noderna inte finns. Mer information finns i [Aktivera ett plugin-program](#activateplugin).
1. Skapa `features` egenskapen på `paraformat` noden:

   * **Namn** `features`
   * **Typ** `String`
   * **Värde** `*` (asterisk)

>[!NOTE]
>
>Om plugin-programmet inte konfigureras ytterligare är standardformaten som aktiveras Stycke ( `<p>`), Rubrik 1 ( `<h1>`), Rubrik 2 ( `<h2>`), Rubrik 3 ( `<h3>`).

>[!CAUTION]
>
>När du konfigurerar styckeformaten för textredigeraren ska du inte ta bort stycketaggen &lt;p> som ett formateringsalternativ. Om taggen tas bort kan innehållsförfattaren inte välja `<p>` [!UICONTROL Paragraph formats] alternativet även om ytterligare format har konfigurerats.

### Ange tillgängliga styckeformat {#paraformatsindropdown}

Styckeformat blir tillgängliga för markering av:

1. I komponentdefinitionen navigerar du till noden `<rtePlugins-node>/paraformat`som den skapades i [Aktivera listrutan](#styleselectorlist)Format.
1. Skapa en nod under `paraformat` noden för att hålla listan över format:

   * **Namn** `formats`
   * **Typ** `cq:WidgetCollection`

1. Skapa en nod under `formats` noden, som innehåller information om ett enskilt format:

   * **Namn** kan du ange namnet, men det bör vara lämpligt för formatet (till exempel minstycke, minrubrik1).
   * **Typ** `nt:unstructured`

1. I den här noden lägger du till egenskapen för att definiera den blocktagg som används:

   * **Namn** `tag`
   * **Typ** `String`
   * **Värde** för blocktaggen för formatet. till exempel: p, h1, h2 osv.

      Du behöver inte ange avgränsande vinkelparenteser.

1. Om du vill lägga till en annan egenskap för samma nod visas beskrivande text i listrutan:

   * **Namn** `description`
   * **Typ** `String`
   * **Värde** den beskrivande texten för detta format. till exempel Stycke, Rubrik 1, Rubrik 2 och så vidare. Den här texten visas i listan Format.

1. Spara ändringarna.

   Upprepa stegen för alla obligatoriska format.

>[!CAUTION]
Om du definierar anpassade format tas standardformaten (`<p>`, `<h1>`, `<h2>`och `<h3>`) bort. Återskapa `<p>` formatet som det är standardformatet.

## Konfigurera specialtecken {#spchar}

I en standardinstallation, när [!DNL Experience Manager] plugin-programmet är aktiverat för specialtecken ( `misctools``specialchars`) är ett standardval omedelbart tillgängligt för användning. till exempel copyright- och varumärkessymboler.

Du kan konfigurera textredigeraren så att ditt val av tecken blir tillgängligt; antingen genom att definiera distinkta tecken eller en hel sekvens.

>[!CAUTION]
Om du lägger till specialtecken åsidosätts standardvalet. Definiera om de här tecknen i markeringen om det behövs.

### Definiera ett enskilt tecken {#definesinglechar}

1. Gå till noden i komponenten `<rtePlugins-node>/misctools`. Skapa noderna om noderna inte finns. Mer information finns i [Aktivera ett plugin-program](#activateplugin).
1. Skapa `features` egenskapen på `misctools` noden:

   * **Namn** `features`
   * **Typ** `String[]`
   * **Värde** `specialchars`

          (eller `String / *` om du använder alla funktioner för det här plugin-programmet)

1. Under `misctools` Skapa en nod som innehåller specialteckenkonfigurationer:

   * **Namn** `specialCharsConfig`
   * **Typ** `nt:unstructured`

1. Under `specialCharsConfig` Skapa en annan nod som innehåller teckenlistan:

   * **Namn** `chars`
   * **Typ** `nt:unstructured`

1. Under `chars` Lägg till en nod som ska innehålla en enskild teckendefinition:

   * **Namn** som du kan ange, men som ska återspegla tecknet; till exempel hälften.
   * **Typ** `nt:unstructured`

1. Lägg till följande egenskap för den här noden:

   * **Namn** `entity`
   * **Typ** `String`
   * **Värde** HTML-representationen av tecknet som krävs. till exempel `&189;` för bråket en halva.

1. Spara ändringarna.

I CRXDE visas det representerade tecknet när egenskapen har sparats. Se exemplet nedan om hälften. Upprepa stegen ovan om du vill göra fler specialtecken tillgängliga för författare.

![I CRXDE lägger du till ett enda tecken som ska vara tillgängligt i verktygsfältet](assets/chlimage_1-106.png "för textredigeringI CRXDE lägger du till ett enda tecken som ska vara tillgängligt i verktygsfältet textredigering")

### Definiera ett teckenintervall {#definerangechar}

1. Använd steg 1 till 3 från [Definiera ett enskilt tecken](#definesinglechar).
1. Under `chars` Lägg till en nod som innehåller definitionen av teckenintervallet:

   * **Namn** som du kan ange, men som ska återspegla teckenintervallet; t.ex. pennor.
   * **Typ** `nt:unstructured`

1. Lägg till följande två egenskaper under den här noden (namngivna enligt ditt teckenintervall):

   * **Namn** `rangeStart`

      **Typ** `Long`
      **Värde** för [Unicode](https://unicode.org/) -representationen (decimal) för det första tecknet i intervallet

   * **Namn** `rangeEnd`

      **Typ** `Long`
      **Värde** för [Unicode](https://unicode.org/) -representationen (decimal) av det sista tecknet i intervallet

1. Spara ändringarna.

   Om du definierar ett intervall från 9998 till 10000 får du följande tecken.

   ![I CRXDE definierar du ett intervall med tecken som ska vara tillgängliga i RTE](assets/chlimage_1-107.png)

   *Bild: I CRXDE definierar du ett intervall med tecken som ska vara tillgängliga i RTE*

   ![Specialtecken som är tillgängliga i textredigeraren visas för författare i ett popup-](assets/rtepencil.png "fönsterSpecialtecken som är tillgängliga i textredigeraren visas för författare i ett popup-fönster")

## Konfigurera tabellformat {#tablestyles}

Format används vanligtvis på text, men du kan också använda separata formatmallar i en tabell eller i ett fåtal tabellceller. Sådana format är tillgängliga för författare i rutan Formatväljare i antingen dialogrutan Cellegenskaper eller Tabellegenskaper. Stilarna är tillgängliga när du redigerar en tabell i en Text-komponent (eller en variabel) och inte i standardkomponenten för tabeller.

>[!NOTE]
Du kan endast definiera format för tabeller och celler för det klassiska användargränssnittet.

>[!NOTE]
Kopiering och inklistring av tabeller i eller från RTE-komponenten är webbläsarberoende. Det stöds inte i alla webbläsare. Du kan få olika resultat beroende på tabellstruktur och webbläsare. Om du till exempel kopierar och klistrar in en tabell i en RTE-komponent i Mozilla Firefox i Classic UI och Touch UI, bevaras inte tabellens layout.

1. Gå till noden i komponenten `<rtePlugins-node>/table`. Skapa noderna om noderna inte finns. Mer information finns i [Aktivera ett plugin-program](#activateplugin).
1. Skapa `features` egenskapen på `table` noden:

   * **Namn** `features`
   * **Typ** `String`
   * **Värde** `*`

   >[!NOTE]
   Om du inte vill aktivera alla tabellfunktioner kan du skapa `features` egenskapen som:
   * **Typ** `String[]`

   * **Värde** ett eller båda av följande, beroende på vad som krävs:
      * `table` göra det möjligt att redigera tabellegenskaper, inklusive formaten.
      * `cellprops` för att tillåta redigering av cellegenskaper, inklusive format.


1. Definiera platsen för CSS-formatmallar för att referera till dem. Se [Ange platsen för formatmallen](#locationofstylesheet) eftersom detta är samma som när du definierar [format för text](#textstyles). Platsen kan definieras om du har definierat andra format.
1. Skapa följande noder under `table` noden efter behov:

   * Så här definierar du format för hela tabellen (finns under **[!UICONTROL Table properties]**):

      * **Namn** `tableStyles`
      * **Typ** `cq:WidgetCollection`
   * Om du vill definiera format för de enskilda cellerna (som finns under **[!UICONTROL Cell properties]**),

      * **Namn** `cellStyles`
      * **Typ** `cq:WidgetCollection`


1. Skapa en nod (under `tableStyles` eller `cellStyles` nod efter behov) som representerar ett enskilt format,

   * **Namn** som du kan ange, men som ska återspegla formatet.
   * **Typ** `nt:unstructured`

1. Skapa egenskaperna på den här noden:

   * Om du vill definiera CSS-formatet som refereras till

      * **Namn** `cssName`
      * **Typ** `String`
      * **Ange namnet** på CSS-klassen (utan föregående `.`exempel, till exempel `cssClass` istället för `.cssClass`)
   * Om du vill definiera en beskrivande text som ska visas i snabbväljaren

      * **Namn** `text`
      * **Typ** `String`
      * **Ange vilket värde** texten ska visas i urvalslistan


1. Spara alla ändringar.

Upprepa stegen ovan för alla obligatoriska format.

### Konfigurera dolda rubriker i tabeller för tillgänglighet {#hiddenheader}

Ibland kan du skapa datatabeller utan visuell text i en kolumnrubrik om rubrikens syfte beror på kolumnens visuella förhållande till andra kolumner. I det här fallet är det nödvändigt att tillhandahålla dold inre text i cellen i rubrikcellen så att skärmläsare och andra hjälpmedelstekniker kan hjälpa läsare med olika behov att förstå vad kolumnen ska användas till.

RTE har stöd för dolda rubrikceller för att förbättra tillgängligheten i sådana scenarier. Dessutom innehåller den konfigurationsinställningar för dolda rubriker i tabeller. Med de här inställningarna kan du använda CSS-format på dolda rubriker i redigerings- och förhandsgranskningslägena. Om du vill hjälpa författare att identifiera dolda rubriker i redigeringsläget kan du inkludera följande parametrar i koden:

* `hiddenHeaderEditingCSS`: Anger namnet på CSS-klassen som används i den dolda rubrikcellen när RTE redigeras.
* `hiddenHeaderEditingStyle`: Anger en formatsträng som används i cellen med dolda rubriker när textredigeringsredigering används.

Om du anger både CSS och formatsträngen i koden har CSS-klassen företräde framför formatsträngen och kan skriva över alla konfigurationsändringar som formatsträngen gör.

För att hjälpa författare att använda CSS på dolda rubriker i förhandsgranskningsläget kan du inkludera följande parametrar i koden:

* `hiddenHeaderClassName`: Anger namnet på CSS-klassen som används i den dolda rubrikcellen i förhandsgranskningsläge.
* `hiddenHeaderStyle`: Anger en formatsträng som används på cellen med dolda rubriker i förhandsvisningsläget.

Om du anger både CSS och formatsträngen i koden har CSS-klassen företräde framför formatsträngen och kan skriva över alla konfigurationsändringar som formatsträngen gör.

## Lägg till ordlistor för stavningskontrollen {#adddict}

När plugin-programmet för stavningskontroll är aktiverat används lexikon för respektive språk. Dessa väljs sedan enligt webbplatsens språk antingen genom att underträdets language-egenskap används eller genom att språket extraheras från URL:en. till exempel. filialen `/en/` kontrolleras som engelska, `/de/` filialen som tyska.

>[!NOTE]
Meddelandet&quot;Stavningskontrollen misslyckades.&quot; visas om en kontroll görs för ett språk som inte är installerat.

En standardinstallation i Experience Manager innehåller ordlistor för:

* American English (en_us)
* Engelska (en_gb)

>[!NOTE]
Standardordlistorna finns i `/libs/cq/spellchecker/dictionaries`, tillsammans med rätt Viktigt-filer. Ändra inte filerna.

Följ de här stegen om du vill lägga till fler ordlistor, om det behövs.

1. Navigera till sidan [https://extensions.openoffice.org/](https://extensions.openoffice.org/).
1. Välj önskat språk och hämta ZIP-filen med stavningsdefinitionerna. Extrahera innehållet i arkivet i filsystemet.

   >[!CAUTION]
   Endast ordlistor i formatet `MySpell` OpenOffice.org v2.0.1 eller tidigare stöds. Eftersom ordlistorna nu är arkivfiler rekommenderar vi att du kontrollerar arkivet efter nedladdningen.

1. Leta reda på .aff- och .dic-filerna. Behåll filnamnet med gemener. Till exempel `de_de.aff` och `de_de.dic`.
1. Läs in .aff- och .dic-filerna i databasen `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
Stavningskontrollen för textredigering är tillgänglig på begäran. Den körs inte automatiskt när du börjar skriva text.
Om du vill stavningskontrollera trycker/klickar du på stavningskontrollknappen i verktygsfältet. RTE kontrollerar stavningen av ord och markerar felstavade ord.
Om du infogar någon ändring som stavningskontrollen föreslår markeras inte längre textens status och felstavade ord. Om du vill köra stavningskontrollen trycker/klickar du på stavningskontrollknappen igen.

## Konfigurera historikstorlek för ångra- och gör om-åtgärder {#undohistory}

Med RTE kan författare ångra eller göra om några sista redigeringar. Som standard lagras 50 redigeringar i historiken. Du kan konfigurera det här värdet efter behov.

1. Gå till noden i komponenten `<rtePlugins-node>/undo`. Skapa de här noderna om de inte finns. Mer information finns i [Aktivera ett plugin-program](#activateplugin).
1. Skapa egenskapen på `undo` noden:

   * **Namn** `maxUndoSteps`
   * **Typ** `Long`
   * **Ange** det antal ångra-steg som du vill spara i historiken. Standardvärdet är 50. Använd `0` för att helt inaktivera ångra/gör om.

1. Spara ändringarna.

## Konfigurera flikstorleken {#tabsize}

När tabbtecknet trycks ned i en text infogas ett fördefinierat antal blanksteg. Som standard är detta tre fasta mellanslag och ett mellanslag.

Så här definierar du tabbstorleken:

1. Gå till noden i komponenten `<rtePlugins-node>/keys`. Skapa noderna om noderna inte finns. Mer information finns i [Aktivera ett plugin-program](#activateplugin).
1. Skapa egenskapen på `keys` noden:

   * **Namn** `tabSize`
   * **Typ** `String`
   * **Värdet** är det antal blankstegstecken som ska användas för tabulatorn.

1. Spara ändringarna.

## Ange indragsmarginal {#indentmargin}

När indrag är aktiverat (standard) kan du definiera storleken på indraget:

>[!NOTE]
Den här indragsstorleken används endast för textstycken (block). det påverkar inte indraget för faktiska listor.

1. Gå till noden i komponenten `<rtePlugins-node>/lists`. Skapa de här noderna om de inte finns. Mer information finns i [Aktivera ett plugin-program](#activateplugin).
1. Skapa `lists` parametern på `identSize` noden:

   * **Namn**: `identSize`
   * **Typ**: `Long`
   * **Värde**: antal pixlar som krävs för indragsmarginalen.

## Konfigurera höjden på det redigerbara utrymmet {#editablespace}

Du kan ange höjden på det redigerbara området som visas i komponentdialogrutan. Konfigurationen gäller endast när du använder RTE i en dialogruta. Konfigurationen ändrar inte höjden på dialogfönstret.

1. Skapa en egenskap i `../items/text` noden i komponentens dialogrutedefinition:

   * **Namn** `height`
   * **Typ** `Long`
   * **Ange höjden** för redigeringsytan i pixlar.

1. Spara ändringarna.

## Konfigurera format och protokoll för länkar {#linkstyles}

När du lägger till länkar i [!DNL Experience Manager]kan du definiera de CSS-format som ska användas och de protokoll som ska accepteras automatiskt. Om du vill konfigurera hur länkar läggs till i [!DNL Experience Manager] från ett annat program definierar du HTML-reglerna.

1. Leta reda på textkomponenten för ditt projekt med CRXDE Lite.
1. Skapa en nod på samma nivå som `<rtePlugins-node>`, d.v.s. skapa noden under den överordnade noden för `<rtePlugins-node>`:

   * **Namn** `htmlRules`
   * **Typ** `nt:unstructured`

   >[!NOTE]
   Noden har `../items/text` egenskapen:
   * **Namn** `xtype`
   * **Typ** `String`
   * **Värde** `richtext`

   Platsen för `../items/text` noden kan variera beroende på strukturen i dialogrutan. Två exempel är `/apps/myProject>/components/text/dialog/items/text` och `/apps/<myProject>/components/text/dialog/items/panel/items/text`.

1. Skapa en nod `htmlRules`under.

   * **Namn** `links`
   * **Typ** `nt:unstructured`

1. Ange egenskaperna under `links` noden efter behov:

   * CSS-format för interna länkar:

      * **Namn** `cssInternal`
      * **Typ** `String`
      * **Ange ett värde** för CSS-klassens namn (utan föregående &#39;.&#39;); for example, `cssClass` instead of `.cssClass`)
   * CSS-format för externa länkar

      * **Namn** `cssExternal`
      * **Typ** `String`
      * **Ange ett värde** för CSS-klassens namn (utan föregående &#39;.&#39;); for example, `cssClass` instead of `.cssClass`)
   * En array med giltiga **[!UICONTROL protocols]** bl.a. `https://`, `https://`, `file://``mailto:`,

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

      På noden `targetConfig`: definiera de egenskaper som krävs:

      * Ange målläge:

         * **Namn** `mode`
         * **Typ** `String`)
         * **Värde**:

            * `auto`: innebär att ett automatiskt mål har valts

               (anges av egenskapen `targetExternal` för externa länkar eller `targetInternal` för interna länkar).

            * `manual`: inte tillämpligt i detta sammanhang
            * `blank`: inte tillämpligt i detta sammanhang
      * Målet för interna länkar:

         * **Namn** `targetInternal`
         * **Typ** `String`
         * **Värde** målet för interna länkar (används endast när läget är `auto`)
      * Målet för externa länkar:

         * **Namn** `targetExternal`
         * **Typ** `String`
         * **Ange ett värde** för målet för externa länkar (används endast när läget är `auto`).








1. Spara alla ändringar.
