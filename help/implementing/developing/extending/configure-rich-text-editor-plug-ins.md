---
title: Konfigurera plugin-programmen för RTF-redigeraren i [!DNL Adobe Experience Manager].
description: Lär dig att konfigurera plugin-program för  [!DNL Adobe Experience Manager] RTF-redigering.
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

Mer information om de andra RTE-konfigurationerna finns i [konfigurera RTF-redigeraren](/help/implementing/developing/extending/rich-text-editor.md).

>[!NOTE]
>
>När du arbetar med CRXDE Lite bör du spara ändringarna regelbundet med alternativet [!UICONTROL Save All].

## Aktivera ett plugin-program och konfigurera egenskapen {#activateplugin} för funktioner

Följ de här stegen för att aktivera ett plugin-program. Vissa steg behövs bara när du konfigurerar ett plugin-program för första gången, eftersom motsvarande noder inte finns.

Som standard är `format`, `link`, `list`, `justify` och `control` plugin-program och alla deras funktioner aktiverade i RTE.

>[!NOTE]
>
>Motsvarande `rtePlugins`-nod kallas `<rtePlugins-node>` för att undvika dubbletter i den här artikeln.

1. Leta reda på textkomponenten för ditt projekt med CRXDE Lite.
1. Skapa den överordnade noden `<rtePlugins-node>` om den inte finns, innan du konfigurerar några RTE-plugin-program:

   * Beroende på vilken komponent du har är de överordnade noderna:

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * en alternativ konfigurationsnod: `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`
   * Är av typen: **jcr:primaryType** `cq:Widget`
   * Båda har följande egenskap:

      * **Namn** `name`
      * **Typ** `String`
      * **Värde** `./text`


1. Beroende på vilket gränssnitt du konfigurerar för skapar du en nod `<rtePlugins-node>`, om den inte finns:

   * **Namn** `rtePlugins`
   * **Typ** `nt:unstructured`

1. Under detta skapar du en nod för varje plugin-program som du vill aktivera:

   * **Typ** `nt:unstructured`
   * **Ange** namnet på plug-in-programmets ID

När du har aktiverat ett plugin-program följer du de här riktlinjerna för att konfigurera egenskapen `features`.

|  | Aktivera alla funktioner | Aktivera några specifika funktioner. | Inaktivera alla funktioner. |
|---|---|---|---|
| Namn | funktioner | funktioner | funktioner |
| Typ | Sträng | `String` (multisträng; ställ in Type  `String` och klicka  `Multi` i CRXDE Lite) | Sträng |
| Värde | `*` (en asterisk) | Ange ett eller flera funktionsvärden. | - |

## Förstå plugin-programmet findreplace {#findreplace}

Plugin-programmet `findreplace` behöver ingen konfiguration. Det går som det ska.

När du använder funktionen Ersätt bör du ange den ersättningssträng som ska ersättas samtidigt som söksträngen. Du kan dock fortfarande klicka på Sök för att söka efter strängen innan du ersätter den. Om ersättningssträngen anges efter att du klickat på Sök återställs sökningen till början av texten.

Dialogrutan Sök och ersätt blir genomskinlig när du klickar på Sök och blir ogenomskinlig när du klickar på Ersätt. På så sätt kan författaren granska texten som ska ersättas. Om användare klickar på Ersätt alla stängs dialogrutan och visar antalet ersättningar som gjorts.

## Konfigurera inklistringslägena {#pastemodes}

När du använder RTE kan författare klistra in innehåll i något av följande tre lägen:

* **Webbläsarläge**: Klistra in text med webbläsarens standardimplementering för inklistring. Det är inte en rekommenderad metod eftersom den kan medföra oönskad markering.

* **Läge** för oformaterad text: Klistra in urklippsinnehållet som oformaterad text. Alla formatelement och formateringselement i det kopierade innehållet tas bort innan de infogas i [!DNL Experience Manager]-komponenten.

* **MS Word-läge**: Klistra in texten, inklusive tabeller, med formatering när du kopierar från MS Word. Det går inte att kopiera och klistra in text från en annan källa, t.ex. en webbsida eller MS Excel, utan endast partiell formatering.

### Konfigurera de alternativ för Klistra in som finns i verktygsfältet RTE {#configure-paste-options-available-on-the-rte-toolbar}

Du kan ange några, alla eller inga av dessa tre ikoner till författarna i verktygsfältet för textredigering:

* **[!UICONTROL Paste (Ctrl+V)]**: Kan förkonfigureras så att det motsvarar något av de tre inklistringslägena ovan.

* **[!UICONTROL Paste as Text]**: Innehåller funktioner för normalt textläge.

* **[!UICONTROL Paste from Word]**: Tillhandahåller MS Word-funktionalitet.

Följ de här stegen för att konfigurera RTE så att nödvändiga ikoner visas.

1. Navigera till komponenten, till exempel `/apps/<myProject>/components/text`.
1. Navigera till noden `rtePlugins/edit`. Se [aktivera ett plugin-program](#activateplugin) om noden inte finns.
1. Skapa egenskapen `features` på noden `edit` och lägg till en eller flera funktioner. Spara alla ändringar.

### Konfigurera beteendet för ikonen Klistra in (Ctrl+V) och genvägen {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

Du kan förkonfigurera beteendet för **[!UICONTROL Paste (Ctrl+V)]**-ikonen genom att följa de här stegen. Den här konfigurationen definierar också beteendet för kortkommandot Ctrl+V som författare använder för att klistra in innehåll.

Konfigurationen tillåter följande tre typer av användningsfall:

* Klistra in text med webbläsarens standardimplementering för inklistring. Det är inte en rekommenderad metod eftersom den kan medföra oönskad markering. Konfigurerad med `browser` nedan.

* Klistra in urklippsinnehållet som oformaterad text. Alla formatelement och formateringselement i det kopierade innehållet tas bort innan de infogas i [!DNL Experience Manager]-komponenten. Konfigurerad med `plaintext` nedan.

* Klistra in texten, inklusive tabeller, med formatering när du kopierar från MS Word. Det går inte att kopiera och klistra in text från en annan källa, t.ex. en webbsida eller MS Excel, utan endast partiell formatering. Konfigurerad med `wordhtml` nedan.

1. Gå till noden `<rtePlugins-node>/edit` i komponenten. Skapa noderna om noderna inte finns. Mer information finns i [aktivera ett plugin-program](#activateplugin).
1. I noden `edit` skapar du en egenskap med följande information:

   * **Namn** `defaultPasteMode`
   * **Typ** `String`
   * **Värdet** är ett av de obligatoriska inklistringslägena från  `browser`,  `plaintext`eller  `wordhtml` lägen.

### Konfigurera de format som tillåts när innehåll klistras in {#pasteformats}

Läget Klistra in som Microsoft-Word (`paste-wordhtml`) kan konfigureras ytterligare så att du uttryckligen kan tillåta ett fåtal format när du klistrar in i [!DNL Experience Manager] från ett annat program, till exempel [!DNL Microsoft Word].

Om till exempel endast fet stil och listor ska tillåtas när du klistrar in i [!DNL Experience Manager] kan du filtrera bort de andra formaten. Detta kallas konfigurerbar inklistringsfiltrering, vilket kan göras för båda:

* [Text](#pastemodes)
* [Länkar](#linkstyles)

För länkar kan du också definiera de protokoll som automatiskt godkänns.

Så här konfigurerar du vilka format som tillåts när du klistrar in text i [!DNL Experience Manager] från ett annat program:

1. Gå till noden `<rtePlugins-node>/edit` i komponenten. Skapa noderna om noden inte finns. Mer information finns i [aktivera ett plugin-program](#activateplugin).
1. Skapa en nod under noden `edit` som innehåller HTML-inklistringsreglerna:

   * **Namn** `htmlPasteRules`
   * **Typ** `nt:unstructured`

1. Skapa en nod under `htmlPasteRules` som innehåller information om de grundläggande formaten som tillåts:

   * **Namn** `allowBasics`
   * **Typ** `nt:unstructured`

1. Om du vill styra de enskilda format som accepteras skapar du en eller flera av följande egenskaper på noden `allowBasics`:

   * **Namn** `bold`
   * **Namn** `italic`
   * **Namn** `underline`
   * **Namn** `anchor`  (för både länkar och namngivna ankare)
   * **Namn** `image`

   Alla egenskaper är av **typ** `Boolean`, så i lämpligt **värde** kan du antingen markera eller ta bort markeringen för att aktivera eller inaktivera funktionen.

   >[!NOTE]
   >
   >Om det inte uttryckligen definieras används standardvärdet true och formatet accepteras.

1. Andra format kan också definieras med hjälp av ett intervall av andra egenskaper eller noder, som även kan användas på noden `htmlPasteRules`:

| Egenskap | Typ | Beskrivning |
|--- |--- |--- |
| `allowBlockTags` | `String` | Definierar listan med blocktaggar som tillåts. Några möjliga blocktaggar är rubriker (h1, h2, h3), stycken (p), listor (ol, ul), tabeller (table). |
| `fallbackBlockTag` | `String` | Definierar den blocktagg som används för alla block med en blocktagg som inte ingår i `allowBlockTags`. Vanligtvis är `p` tillräckligt. |
| `table` | `nt:unstructured` | Definierar beteendet när tabeller klistras in. Den här noden måste ha egenskapen allow (type Boolean) för att definiera om inklistring av tabeller tillåts. Om allow anges till false måste du ange egenskapen ignoreMode (typ String) för att definiera hur inklistrat tabellinnehåll ska hanteras. Giltiga värden för ignoreMode är `remove` för att ta bort tabellinnehåll och `paragraph` för att omvandla tabellceller till stycken. |
| `list` | `nt:unstructured` | Definierar beteendet när listor klistras in. Måste ha egenskapen `allow` (typ Boolean) för att definiera om inklistring av listor är tillåten. Om `allow` är `false` anger du egenskapen `ignoreMode` (typ `String`) för att definiera hur allt listinnehåll som klistras in ska hanteras. Giltiga värden för ignoreMode är `remove` som tar bort listinnehåll och `paragraph` som förvandlar listobjekt till stycken. |

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

När plugin-programmet Styles är aktiverat för första gången finns det inga standardformat. Popup-listan är tom. Så här förser du författarna med formatmallar:

* Aktivera den nedrullningsbara listrutan Format.
* Ange en eller flera platser för formatmallarna.
* Ange de enskilda format som kan väljas i popup-listan för format.

Om du vill lägga till fler format senare, t.ex. följer du bara instruktionerna för att referera till en ny formatmall och ange de ytterligare formaten.

>[!NOTE]
>
>Format kan också definieras för [tabeller eller tabellceller](configure-rich-text-editor-plug-ins.md#tablestyles). Dessa konfigurationer kräver separata procedurer.

### Aktivera listrutan Format {#styleselectorlist}

Detta görs genom att plugin-programmet för format aktiveras.

1. Gå till noden `<rtePlugins-node>/styles` i komponenten. Skapa noderna om noderna inte finns. Mer information finns i [aktivera ett plugin-program](#activateplugin).
1. Skapa egenskapen `features` på noden `styles`:

   * **Namn** `features`
   * **Typ** `String`
   * **Värde** `*`  (asterisk)

1. Spara alla ändringar.

>[!NOTE]
>
>När plugin-programmet Format är aktiverat visas listrutan Format i redigeringsdialogrutan. Listan är dock tom eftersom inga format har konfigurerats.

### Ange formatmallens plats {#locationofstylesheet}

Ange sedan platsen/platserna för de formatmallar som du vill referera till:

1. Navigera till rotnoden för textkomponenten, till exempel `/apps/<myProject>/components/text`.
1. Lägg till egenskapen `externalStyleSheets` i den överordnade noden för `<rtePlugins-node>`:

   * **Namn** `externalStyleSheets`
   * **Type** `String[]` (multi-string; klicka på  **** Multiin CRXDE)
   * **Värden**  Sökvägen och filnamnet för alla formatmallar som du vill ta med. Använd databassökvägar.

   >[!NOTE]
   >
   >Du kan när som helst lägga till referenser till ytterligare formatmallar.

1. Spara alla ändringar.

När du använder textredigering i en dialogruta (Classic UI) kan du ange formatmallar som är optimerade för textredigering. På grund av tekniska begränsningar förloras CSS-kontexten i redigeraren, så du kan emulera den här kontexten för att förbättra WYSIWYG-upplevelsen.

RTF-redigeraren använder ett behållar-DOM-element med ID `CQrte` som innehåller olika format för att visa och redigera:

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

1. I komponentdefinitionen navigerar du till noden `<rtePlugins-node>/styles`, som den skapades i [Aktivera listrutan för formatet](#styleselectorlist).
1. Under noden `styles` skapar du en nod (kallas även `styles`) som innehåller listan som ska göras tillgänglig:

   * **Namn** `styles`
   * **Typ** `cq:WidgetCollection`

1. Skapa en nod under noden `styles` som representerar ett enskilt format:

   * **Namn**, du kan ange namnet, men det bör vara lämpligt för formatet
   * **Typ** `nt:unstructured`

1. Lägg till egenskapen `cssName` i den här noden som referens för CSS-klassen:

   * **Namn** `cssName`
   * **Typ** `String`
   * **** ValueNamnet på CSS-klassen (utan föregående &quot;.&quot;; till exempel `cssClass` i stället för `.cssClass`)

1. Lägg till egenskapen `text` i samma nod; definierar texten som visas i markeringsrutan:

   * **Namn** `text`
   * **Typ** `String`
   * **** ValueDescription of the style; visas i den nedrullningsbara listrutan Format.

1. Spara ändringarna.

   Upprepa stegen ovan för alla obligatoriska format.

### Konfigurera RTE för optimala ordbrytningar på japanska {#jpwordwrap}

Författare som använder [!DNL Experience Manager] för att skapa japanskt innehåll kan använda ett format på tecken för att undvika radbrytning där radbrytning inte krävs. Detta gör att författare kan låta meningarna brytas vid önskad position. Formatet för den här funktionen baseras på CSS-klassen som är fördefinierad i CSS-formatmallen.

Så här skapar du det format som författare kan använda på japansk text:

1. Skapa en nod under noden Styles. Se [ange ett format](#stylesindropdown).
   * Namn: `jpn-word-wrap`
   * Typ: `nt:unstructure`

1. Lägg till egenskapen `cssName` i noden som referens för CSS-klassen. Klassnamnet är ett reserverat namn för japansk radbrytning.
   * Namn: `cssName`
   * Typ: `String`
   * Värde: `jpn-word-wrap` (utan föregående `.`)

1. Lägg till egenskapstexten i samma nod. Värdet är namnet på formatet som författarna ser när de väljer formatet.
   * Namn: `text`
*Typ: 
`String`
   * Värde: `Japanese word-wrap`

1. Skapa en formatmall och ange dess sökväg. Se [ange plats för formatmall](#locationofstylesheet). Lägg till följande innehåll i formatmallen. Ändra bakgrundsfärgen efter behov.

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![Formatmall som gör japansk radbrytning tillgänglig för författare](assets/rte_jpwordwrap_stylesheet.jpg)

## Konfigurera styckeformaten {#paraformats}

All text som har skapats i RTE placeras i en blocktagg och standardvärdet är `<p>`. Genom att aktivera plugin-programmet `paraformat` anger du ytterligare blocktaggar som kan tilldelas stycken med hjälp av en nedrullningsbar markeringslista. Styckeformat bestämmer stycketypen genom att tilldela rätt blocktagg. Författaren kan markera och tilldela dem med formatväljaren. Exempelblocktaggarna innehåller bland annat standardstycket &lt;p> och rubrikerna &lt;h1>, &lt;h2> och så vidare.

>[!CAUTION]
>
>Det här plugin-programmet passar inte för innehåll med komplex struktur, till exempel listor eller tabeller.

>[!NOTE]
>
>Om en blocktagg, till exempel en `<hr>`-tagg, inte kan tilldelas till ett stycke, är det inte ett giltigt användningsfall för ett `paraformat`-plugin-program.

När plugin-programmet Styckeformat är aktiverat för första gången är inga standardstyckeformat tillgängliga. Popup-listan är tom. Så här förser du författarna med styckeformat:

* Aktivera popup-väljarlistan [!UICONTROL Format].
* Ange de blocktaggar som kan markeras som styckeformat på snabbmenyn.

För senare omkonfigurationer, till exempel för att lägga till fler format, följ bara relevanta delar av instruktionerna.

### Aktivera den nedrullningsbara formatväljaren {#formatselectorlist}

Så här aktiverar du plugin-programmet `paraformat`:

1. Gå till noden `<rtePlugins-node>/paraformat` i komponenten. Skapa noderna om noderna inte finns. Mer information finns i [aktivera ett plugin-program](#activateplugin).
1. Skapa egenskapen `features` på noden `paraformat`:

   * **Namn** `features`
   * **Typ** `String`
   * **Värde** `*`  (asterisk)

>[!NOTE]
>
>Om plugin-programmet inte konfigureras ytterligare är standardformaten som aktiveras Stycke ( `<p>`), Rubrik 1 ( `<h1>`), Rubrik 2 ( `<h2>`), Rubrik 3 ( `<h3>`).

>[!CAUTION]
>
>När du konfigurerar styckeformaten för textredigeraren ska du inte ta bort stycketaggen &lt;p> som ett formateringsalternativ. Om taggen `<p>` tas bort kan innehållsförfattaren inte välja alternativet [!UICONTROL Paragraph formats] även om ytterligare format har konfigurerats.

### Ange tillgängliga styckeformat {#paraformatsindropdown}

Styckeformat blir tillgängliga för markering av:

1. I komponentdefinitionen navigerar du till noden `<rtePlugins-node>/paraformat`, som den skapades i [Aktivera listrutan för formatet](#styleselectorlist).
1. Under noden `paraformat` skapar du en nod som innehåller listan med format:

   * **Namn** `formats`
   * **Typ** `cq:WidgetCollection`

1. Skapa en nod under noden `formats`, som innehåller information om ett enskilt format:

   * **Namn** kan du ange namnet, men det bör vara lämpligt för formatet (till exempel minstycke, minrubrik1).
   * **Typ** `nt:unstructured`

1. I den här noden lägger du till egenskapen för att definiera den blocktagg som används:

   * **Namn** `tag`
   * **Typ** `String`
   * **** VärdeBlocktaggen för formatet. till exempel: p, h1, h2 osv.

      Du behöver inte ange avgränsande vinkelparenteser.

1. Om du vill lägga till en annan egenskap för samma nod visas beskrivande text i listrutan:

   * **Namn** `description`
   * **Typ** `String`
   * **** VärdeDen beskrivande texten för detta format. till exempel Stycke, Rubrik 1, Rubrik 2 och så vidare. Den här texten visas i listan Format.

1. Spara ändringarna.

   Upprepa stegen för alla obligatoriska format.

>[!CAUTION]
Om du definierar anpassade format tas standardformaten (`<p>`, `<h1>`, `<h2>` och `<h3>`) bort. Återskapa formatet `<p>` eftersom det är standardformatet.

## Konfigurera specialtecken {#spchar}

När plugin-programmet `misctools` är aktiverat för specialtecken (`specialchars`) är standardvalet i en [!DNL Experience Manager]-standardinstallation omedelbart tillgängligt för användning. till exempel copyright- och varumärkessymboler.

Du kan konfigurera textredigeraren så att ditt val av tecken blir tillgängligt; antingen genom att definiera distinkta tecken eller en hel sekvens.

>[!CAUTION]
Om du lägger till specialtecken åsidosätts standardvalet. Definiera om de här tecknen i markeringen om det behövs.

### Definiera ett enskilt tecken {#definesinglechar}

1. Gå till noden `<rtePlugins-node>/misctools` i komponenten. Skapa noderna om noderna inte finns. Mer information finns i [aktivera ett plugin-program](#activateplugin).
1. Skapa egenskapen `features` på noden `misctools`:

   * **Namn** `features`
   * **Typ** `String[]`
   * **Värde** `specialchars`

          (eller `String / *` om alla funktioner för det här plugin-programmet används)

1. Under `misctools` skapar du en nod för specialteckenkonfigurationer:

   * **Namn** `specialCharsConfig`
   * **Typ** `nt:unstructured`

1. Under `specialCharsConfig` skapar du en annan nod som innehåller teckenlistan:

   * **Namn** `chars`
   * **Typ** `nt:unstructured`

1. Under `chars` lägger du till en nod för en enskild teckendefinition:

   * **Du** kan ange namnet, men det ska återspegla tecknet; till exempel hälften.
   * **Typ** `nt:unstructured`

1. Lägg till följande egenskap för den här noden:

   * **Namn** `entity`
   * **Typ** `String`
   * **Värde** HTML-representationen av tecknet som krävs. till exempel  `&189;` för bråket en halva.

1. Spara ändringarna.

I CRXDE visas det representerade tecknet när egenskapen har sparats. Se exemplet nedan om hälften. Upprepa stegen ovan om du vill göra fler specialtecken tillgängliga för författare.

![I CRXDE lägger du till ett enda tecken som ska vara tillgängligt i verktygsfältet ](assets/chlimage_1-106.png "för textredigeringI CRXDE lägger du till ett enda tecken som ska vara tillgängligt i verktygsfältet textredigering")

### Definiera ett teckenintervall {#definerangechar}

1. Använd steg 1 till 3 från [Definiera ett enskilt tecken](#definesinglechar).
1. Under `chars` lägger du till en nod som ska innehålla definitionen av teckenintervallet:

   * **Du** kan ange namnet, men det bör återspegla teckenintervallet; t.ex. pennor.
   * **Typ** `nt:unstructured`

1. Lägg till följande två egenskaper under den här noden (namngivna enligt ditt teckenintervall):

   * **Namn** `rangeStart`

      **Typ** `Long`
      **Värde** för  [](https://unicode.org/) Unicoderepresentation (decimal) för det första tecknet i intervallet

   * **Namn** `rangeEnd`

      **Typ** `Long`
      **Värde** för  [](https://unicode.org/) Unicoderepresentation (decimal) för det sista tecknet i intervallet

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

1. Gå till noden `<rtePlugins-node>/table` i komponenten. Skapa noderna om noderna inte finns. Mer information finns i [aktivera ett plugin-program](#activateplugin).
1. Skapa egenskapen `features` på noden `table`:

   * **Namn** `features`
   * **Typ** `String`
   * **Värde** `*`

   >[!NOTE]
   Om du inte vill aktivera alla tabellfunktioner kan du skapa egenskapen `features` som:
   * **Typ** `String[]`

   * **Värde** ett eller båda av följande, beroende på vad som krävs:
      * `table` göra det möjligt att redigera tabellegenskaper, inklusive formaten.
      * `cellprops` för att tillåta redigering av cellegenskaper, inklusive format.


1. Definiera platsen för CSS-formatmallar för att referera till dem. Se [Ange platsen för formatmallen](#locationofstylesheet) eftersom detta är samma som när du definierar [format för text](#textstyles). Platsen kan definieras om du har definierat andra format.
1. Skapa följande noder under `table`-noden efter behov:

   * Så här definierar du format för hela tabellen (finns under **[!UICONTROL Table properties]**):

      * **Namn** `tableStyles`
      * **Typ** `cq:WidgetCollection`
   * Om du vill definiera format för de enskilda cellerna (som är tillgängliga under **[!UICONTROL Cell properties]**),

      * **Namn** `cellStyles`
      * **Typ** `cq:WidgetCollection`


1. Skapa en nod (under noden `tableStyles` eller `cellStyles` efter behov) som representerar ett enskilt format,

   * **Du** kan ange ett namn, men det bör återspegla formatet.
   * **Typ** `nt:unstructured`

1. Skapa egenskaperna på den här noden:

   * Om du vill definiera CSS-formatet som refereras till

      * **Namn** `cssName`
      * **Typ** `String`
      * **Värde** namnet på CSS-klassen (utan föregående  `.`exempel,  `cssClass` i stället för  `.cssClass`)
   * Om du vill definiera en beskrivande text som ska visas i snabbväljaren

      * **Namn** `text`
      * **Typ** `String`
      * **Ange** värden för texten som ska visas i urvalslistan


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

När plugin-programmet för stavningskontroll är aktiverat används lexikon för respektive språk. Dessa väljs sedan enligt webbplatsens språk antingen genom att underträdets language-egenskap används eller genom att språket extraheras från URL:en. till exempel. grenen `/en/` kontrolleras som engelsk, grenen `/de/` som tysk.

>[!NOTE]
Meddelandet&quot;Stavningskontrollen misslyckades.&quot; visas om en kontroll görs för ett språk som inte är installerat.

En standardinstallation i Experience Manager innehåller ordlistor för:

* American English (en_us)
* Engelska (en_gb)

>[!NOTE]
Standardordlistorna finns på `/libs/cq/spellchecker/dictionaries` tillsammans med rätt ReadMe-filer. Ändra inte filerna.

Följ de här stegen om du vill lägga till fler ordlistor, om det behövs.

1. Gå till sidan [https://extensions.openoffice.org/](https://extensions.openoffice.org/).
1. Välj önskat språk och hämta ZIP-filen med stavningsdefinitionerna. Extrahera innehållet i arkivet i filsystemet.

   >[!CAUTION]
   Endast ordlistor i formatet `MySpell` för OpenOffice.org v2.0.1 eller tidigare stöds. Eftersom ordlistorna nu är arkivfiler rekommenderar vi att du kontrollerar arkivet efter nedladdningen.

1. Leta reda på .aff- och .dic-filerna. Behåll filnamnet med gemener. Till exempel `de_de.aff` och `de_de.dic`.
1. Läs in .aff- och .dic-filerna i databasen vid `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
Stavningskontrollen för textredigering är tillgänglig på begäran. Den körs inte automatiskt när du börjar skriva text.
Om du vill stavningskontrollera trycker/klickar du på stavningskontrollknappen i verktygsfältet. RTE kontrollerar stavningen av ord och markerar felstavade ord.
Om du infogar någon ändring som stavningskontrollen föreslår markeras inte längre textens status och felstavade ord. Om du vill köra stavningskontrollen trycker/klickar du på stavningskontrollknappen igen.

## Konfigurera historikstorleken för ångra- och gör om-åtgärder {#undohistory}

Med RTE kan författare ångra eller göra om några sista redigeringar. Som standard lagras 50 redigeringar i historiken. Du kan konfigurera det här värdet efter behov.

1. Gå till noden `<rtePlugins-node>/undo` i komponenten. Skapa de här noderna om de inte finns. Mer information finns i [aktivera ett plugin-program](#activateplugin).
1. Skapa egenskapen på `undo`-noden:

   * **Namn** `maxUndoSteps`
   * **Typ** `Long`
   * **Värdet är** antalet ångra-steg som du vill spara i historiken. Standardvärdet är 50. Använd `0` för att helt inaktivera ångra/gör om.

1. Spara ändringarna.

## Konfigurera flikstorleken {#tabsize}

När tabbtecknet trycks ned i en text infogas ett fördefinierat antal blanksteg. Som standard är detta tre fasta mellanslag och ett mellanslag.

Så här definierar du tabbstorleken:

1. Gå till noden `<rtePlugins-node>/keys` i komponenten. Skapa noderna om noderna inte finns. Mer information finns i [aktivera ett plugin-program](#activateplugin).
1. Skapa egenskapen på `keys`-noden:

   * **Namn** `tabSize`
   * **Typ** `String`
   * **Ange** värdet för det antal blankstegstecken som ska användas för tabulatorn.

1. Spara ändringarna.

## Ange indragsmarginal {#indentmargin}

När indrag är aktiverat (standard) kan du definiera storleken på indraget:

>[!NOTE]
Den här indragsstorleken används endast för textstycken (block). det påverkar inte indraget för faktiska listor.

1. Gå till noden `<rtePlugins-node>/lists` i komponenten. Skapa de här noderna om de inte finns. Mer information finns i [aktivera ett plugin-program](#activateplugin).
1. Skapa parametern `identSize` på `lists`-noden:

   * **Namn**:  `identSize`
   * **Typ**:  `Long`
   * **Värde**: antal pixlar som krävs för indragsmarginalen.

## Konfigurera höjden på det redigerbara utrymmet {#editablespace}

Du kan ange höjden på det redigerbara området som visas i komponentdialogrutan. Konfigurationen gäller endast när du använder RTE i en dialogruta. Konfigurationen ändrar inte höjden på dialogfönstret.

1. I noden `../items/text` skapar du en egenskap i dialogdefinitionen för komponenten:

   * **Namn** `height`
   * **Typ** `Long`
   * **Ange** höjden på arbetsytan i pixlar.

1. Spara ändringarna.

## Konfigurera format och protokoll för länkar {#linkstyles}

När du lägger till länkar i [!DNL Experience Manager] kan du definiera de CSS-format som ska användas och de protokoll som ska accepteras automatiskt. Om du vill konfigurera hur länkar läggs till i [!DNL Experience Manager] från ett annat program definierar du HTML-reglerna.

1. Leta reda på textkomponenten för ditt projekt med CRXDE Lite.
1. Skapa en nod på samma nivå som `<rtePlugins-node>`, d.v.s. skapa noden under den överordnade noden `<rtePlugins-node>`:

   * **Namn** `htmlRules`
   * **Typ** `nt:unstructured`

   >[!NOTE]
   Noden `../items/text` har egenskapen:
   * **Namn** `xtype`
   * **Typ** `String`
   * **Värde** `richtext`

   Platsen för `../items/text`-noden kan variera beroende på strukturen i dialogrutan. Två exempel är `/apps/myProject>/components/text/dialog/items/text` och `/apps/<myProject>/components/text/dialog/items/panel/items/text`.

1. Skapa en nod under `htmlRules`.

   * **Namn** `links`
   * **Typ** `nt:unstructured`

1. Under `links`-noden definierar du egenskaperna efter behov:

   * CSS-format för interna länkar:

      * **Namn** `cssInternal`
      * **Typ** `String`
      * **Värde** namnet på CSS-klassen (utan föregående &quot;.&quot;; till exempel `cssClass` i stället för `.cssClass`)
   * CSS-format för externa länkar

      * **Namn** `cssExternal`
      * **Typ** `String`
      * **Värde** namnet på CSS-klassen (utan föregående &quot;.&quot;; till exempel `cssClass` i stället för `.cssClass`)
   * En matris med giltiga **[!UICONTROL protocols]** som `https://`, `https://`, `file://`, `mailto:` med flera,

      * **Namn** `protocols`
      * **Typ** `String[]`
      * **Värde** ett eller flera protokoll
   * **defaultProtocol** (egenskap av typen  **String**): Protokoll som ska användas om användaren inte uttryckligen angav ett.

      * **Namn** `defaultProtocol`
      * **Typ** `String`
      * **Värde** ett eller flera standardprotokoll
   * Definition av hur målattributet för en länk ska hanteras. Skapa en nod:

      * **Namn** `targetConfig`
      * **Typ** `nt:unstructured`

      På noden `targetConfig`: definiera de egenskaper som krävs:

      * Ange målläge:

         * **Namn** `mode`
         * **Text** `String`)
         * **Värde** :

            * `auto`: innebär att ett automatiskt mål har valts

               (anges av egenskapen `targetExternal` för externa länkar eller `targetInternal` för interna länkar).

            * `manual`: inte tillämpligt i detta sammanhang
            * `blank`: inte tillämpligt i detta sammanhang
      * Målet för interna länkar:

         * **Namn** `targetInternal`
         * **Typ** `String`
         * **Värde** målet för interna länkar (används bara när läget är  `auto`)
      * Målet för externa länkar:

         * **Namn** `targetExternal`
         * **Typ** `String`
         * **Värde** målet för externa länkar (används bara när läget är  `auto`).








1. Spara alla ändringar.
