---
title: Konfigurera RTF-redigeraren så att innehåll i [!DNL Adobe Experience Manager] skapas som en Cloud Service.
description: Konfigurera RTF-redigeraren för att skapa innehåll i [!DNL Adobe Experience Manager] som en Cloud Service.
contentOwner: AG
exl-id: 1f0ff800-5e95-429a-97f2-221db0668170
source-git-commit: f5f2c7c4dfacc113994c380e8caa37508030ee92
workflow-type: tm+mt
source-wordcount: '1964'
ht-degree: 0%

---

# Konfigurera RTF-redigeraren {#configure-the-rich-text-editor}

Med RTF-redigeraren får författarna ett stort antal funktioner för att redigera textinnehåll. Ikoner, markeringsrutor, verktygsfält och menyer finns för WYSIWYG-textredigering. Administratörer konfigurerar RTE för att aktivera, inaktivera och utöka de funktioner som är tillgängliga i redigeringskomponenterna. Se hur författare [använder RTE för att skapa](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md) webbinnehåll.

De RTE-begrepp och -steg som krävs för att konfigurera den listas nedan.

| Förstå RTE-begrepp | Aktivera nödvändiga funktioner | Konfigurera enskilda funktioner |
|---|---|---|
| [Förstå gränssnittet](#understand-rte-ui) | [Förstå och ange konfigurationsplatser](#understand-the-configuration-paths-and-locations) | [Konfigurera plugin-program](#enable-rte-functionalities-by-activating-plug-ins) |
| [Olika typer av redigeringslägen](#editingmodes) | [Aktivera plugin-program](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin) | [Ange funktionsegenskaper](#aboutplugins) |
| [Om plugin-program](#aboutplugins) | [Konfigurera RTE-verktygsfält](#dialogfullscreen) | [Konfigurera inklistringslägen](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles) |

## Förstå användargränssnittet som är tillgängligt för författare {#understand-rte-ui}

RTE-gränssnittet erbjuder en [responsiv design](/help/sites-cloud/authoring/features/responsive-layout.md) för redigeringsmiljön. Gränssnittet är utformat för att användas på enheter med pekskärm och stationära datorer.

![Verktygsfältet för textredigeraren](assets/rte-toolbar-full-screen-mode.png)

*Bild: Verktygsfältet för textredigeraren med alla tillgängliga alternativ aktiverade.*

Verktygsfältet innehåller alternativ för WYSIWYG-redigering. [!DNL Experience Manager] administratörer kan konfigurera de alternativ som är tillgängliga i verktygsfältet i gränssnittet. En omfattande uppsättning redigeringsalternativ finns som standard i [!DNL Experience Manager]. Utvecklare kan anpassa [!DNL Experience Manager] och lägga till fler redigeringsalternativ.

## Olika redigeringslägen {#editingmodes}

Författare kan skapa och redigera textinnehåll i [!DNL Experience Manager] med hjälp av de olika komponentlägena. Alternativen i verktygsfältet för att skapa och formatera innehåll och användarupplevelsen i komponenter med RTE-funktioner i olika redigeringslägen varierar beroende på RTE-konfigurationer.

| Redigeringsläge | Redigeringsområde | Rekommenderade funktioner som ska aktiveras |
|--- |--- |--- |
| Textbunden | On-place editing for quick, minor edits; Formatera utan att öppna en dialogruta. | Minimala RTE-funktioner. |
| RTE i helskärmsläge | Täcker hela sidan. | Alla nödvändiga RTE-funktioner. |
| Dialog | Dialogrutan visas ovanpå sidinnehållet men täcker inte hela sidan. | Aktivera funktioner i jakt. |
| Dialogruta i helskärmsläge | Samma som helskärmsläge, innehåller fält i dialogrutan vid sidan om RTE. | Alla nödvändiga RTE-funktioner. |

>[!NOTE]
>
>Funktionen för källredigering är inte tillgänglig i infogat redigeringsläge. Du kan inte dra bilder i helskärmsläge. Alla andra funktioner fungerar i alla lägen.

### Inline-redigering {#inline-editing}

Om du vill redigera innehållet på en sida öppnar du innehållet med ett långsamt dubbelklick . Ett kompakt verktygsfält med grundläggande alternativ visas.

![Inline-redigering med grundläggande alternativ i verktygsfältet](assets/inline-editing-mode-basic-options.png)

*Bild: Inline-redigering med grundläggande alternativ i verktygsfältet.*

### Helskärmsredigering {#full-screen-editing}

[!DNL Experience Manager] -komponenter kan öppnas i helskärmsläge som döljer sidinnehållet och tar upp den tillgängliga skärmen. Överväg att redigera i helskärmsläge som en detaljerad version av den infogade redigeringen eftersom den erbjuder de flesta redigeringsalternativen. Du kan öppna den genom att klicka på ikonen ![för att öppna RTE i helskärmsläge](assets/rte_fullscreen.png) i det kompakta verktygsfältet när du använder det infogade redigeringsläget.

I dialogrutans helskärmsläge, tillsammans med ett detaljerat verktygsfält för textredigering, är även de alternativ och komponenter som är tillgängliga i en dialogruta tillgängliga. Det gäller endast för en dialogruta som innehåller RTE tillsammans med andra komponenter.

![Det detaljerade verktygsfältet för textredigering när du redigerar i helskärmsläge](assets/rte-toolbar-full-screen-mode.png)

*Bild: Det detaljerade verktygsfältet för textredigering när du redigerar i helskärmsläge.*

### Dialogruteredigering {#dialog-editing}

När du dubbelklickar på en komponent öppnas en dialogruta där du kan redigera innehållet. Dialogrutan öppnas ovanpå den befintliga sidan. I vissa specifika scenarier öppnas dialogrutan som ett popup-fönster. Om en textkomponent till exempel är en del av en kolumn i en sidlayout med flera kolumner och området som är tillgängligt för dialogrutan är mindre.

![Dialogruteredigeringsläge](assets/dialog_editing_modetouchui.png)

*Bild: Dialogruteredigeringsläge.*

## Om RTE-plugin-program och associerade funktioner {#aboutplugins}

Funktionerna är tillgängliga via ett antal plugin-program, var och en med:

* En `features`-egenskap som är

   * Används för att aktivera eller inaktivera grundläggande funktioner för det plugin-programmet.
   * Konfigureras med en standardiserad procedur.

* I tillämpliga fall krävs specialkonfigurering för fler egenskaper och alternativ.

Grundfunktionerna i textredigeraren aktiveras, eller inaktiveras, av värdet för egenskapen `features` på en nod som är specifik för det aktuella plugin-programmet.

I följande tabell visas de aktuella plugin-programmen:

* Plugin-ID:n med en länk till API-dokumentationen. ID används som nodnamn när [ett plugin-program](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin) aktiveras.
* Tillåtna värden för egenskapen `features`.
* En beskrivning av de funktioner som tillhandahålls av plugin-programmet.

| Plug-in-ID | funktioner | Beskrivning |
|--- |--- |--- |
| redigera | `cut`,  `copy`,  `paste-default`,  `paste-plaintext`,  `paste-wordhtml` | [Klipp ut, kopiera och, de tre inklistringslägena](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles). |
| [findreplace](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FindReplacePlugin) | `find`, `replace` | Sök och ersätt. |
| [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FormatPlugin) | `bold`, `italic`, `underline` | [Grundläggande textformatering](configure-rich-text-editor-plug-ins.md#textstyles). |
| [bild](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ImagePlugin) | `image` | Grundläggande bildstöd (dra från innehåll eller Innehållssökning). Beroende på webbläsaren har stödet olika beteenden för författare |
| [tangenter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.KeyPlugin) | - | Mer information om hur du definierar det här värdet finns i [tabbstorlek](configure-rich-text-editor-plug-ins.md#tabsize). |
| [justera](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.JustifyPlugin) | `justifyleft`,  `justifycenter`,  `justifyright` | Styckejustering. |
| [länkar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.LinkPlugin) | `modifylink`,  `unlink`,  `anchor` | [Hyperlänkar och ankare](configure-rich-text-editor-plug-ins.md#linkstyles). |
| [listor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ListPlugin) | `ordered`, `unordered`, `indent`, `outdent` | Denna plugin kontrollerar både [indrag och listor](configure-rich-text-editor-plug-ins.md#indentmargin); inklusive kapslade listor. |
| [felverktyg](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.MiscToolsPlugin) | `specialchars`,  `sourceedit` | Med andra verktyg kan författare ange [specialtecken](configure-rich-text-editor-plug-ins.md#spchar) eller redigera HTML-källan. Du kan också lägga till ett [intervall med specialtecken](configure-rich-text-editor-plug-ins.md#definerangechar) om du vill definiera en egen lista. |
| Paraformat | `paraformat` | Standardstyckeformaten är Stycke, Rubrik 1, Rubrik 2 och Rubrik 3 (`<p>`, `<h1>`, `<h2>` och `<h3>`). Du kan [lägga till fler styckeformat](configure-rich-text-editor-plug-ins.md#paraformats) eller utöka listan. |
| stavningskontroll | `checktext` | [Språkmedveten stavningskontroll](configure-rich-text-editor-plug-ins.md#adddict). |
| stilar | `styles` | Stöd för formatering med en CSS-klass. [Lägg till ett nytt ](configure-rich-text-editor-plug-ins.md#textstyles) textformat om du vill lägga till (eller utöka) egna format för användning med text. |
| nedsänkt | `subscript`,  `superscript` | Tillägg till de grundläggande formaten, med underskript och superskript. |
| tabell | `table`,  `removetable`,  `insertrow`,  `removerow`,  `insertcolumn`,  `removecolumn`,  `cellprops`,  `mergecells`,  `splitcell`,  `selectrow`,  `selectcolumns` | Se [konfigurera tabellformat](configure-rich-text-editor-plug-ins.md#tablestyles) för att lägga till egna format för hela tabeller eller enskilda celler. |
| ångra | `undo`,  `redo` | Historikstorlek för [ångra och gör om](configure-rich-text-editor-plug-ins.md#undohistory)-åtgärder. |

>[!NOTE]
>
>Plugin-programmet för helskärmsläge stöds inte i dialogruteläge. Använd inställningen `dialogFullScreen` för att konfigurera verktygsfältet för helskärmsläge.

## Förstå konfigurationssökvägar och -platser {#understand-the-configuration-paths-and-locations}

[RTE-redigeringsläget och gränssnittet](#editingmodes) som du anger för författarna bestämmer platsen för konfigurationsinformationen när du [aktiverar RTE-plugin-program](configure-rich-text-editor-plug-ins.md#activateplugin). Platserna är:

* Textbundet läge: `cq:editConfig/cq:inplaceEditing`.
* Helskärmsläge: `cq:editConfig/cq:inplaceEditing`.
* Dialogruteläge: `cq:dialog`.
* Dialogruteläge för helskärm: `cq:dialog`.

>[!NOTE]
>
>Ge inte noden namnet `cq:inplaceEditing` som `config`. Definiera följande egenskaper på `cq:inplaceEditing`-noden:
>
>* **Namn**:  `configPath`
>* **Typ**:  `String`
>* **Värde**: sökväg till noden som innehåller den faktiska konfigurationen

>
>
Ge inte RTE-konfigurationsnoden namnet `config`. Annars gäller RTE-konfigurationerna bara för administratörerna och inte för användarna i gruppen `content-author`.

Konfigurera följande egenskaper som gäller i redigeringsläget för dialogrutor:

* `useFixedInlineToolbar`: Du kan ange att verktygsfältet RTE ska vara fast i stället för flytande. Ange den här booleska egenskapen som definierats på RTE-noden med sling:resourceType= `cq/gui/components/authoring/dialog/richtext` till `True`. När den här egenskapen är inställd på `True` startas textredigeringen för händelsen `foundation-contentloaded`. Du kan förhindra detta genom att ange egenskapen `customStart` till `True` och utlösa händelsen `rte-start` för att starta RTE-redigering. När den här egenskapen är `true` startar inte RTE vid klickning och detta är standardbeteendet.

* `customStart`: Ställ in den här booleska egenskapen som definierats på noden RTE till  `True`, för att styra när RTE ska startas genom att händelsen utlöses  `rte-start`.

* `rte-start`: Utlös den här händelsen i  `contenteditable-div` slutet av textredigeringsredigeringen när textredigeringsredigeringen ska börja. Det fungerar bara om `customStart` har angetts till `true`.

När RTE används i dialogrutan med pekfunktioner anger du egenskapen `useFixedInlineToolbar` till `true` för att undvika problem.

## Aktivera RTE-funktioner genom att aktivera plugin-program {#enable-rte-functionalities-by-activating-plug-ins}

RTE-funktioner är tillgängliga via en serie plugin-program, var och en med features-egenskaper. Du kan konfigurera egenskapen features för att aktivera eller inaktivera de olika funktionerna i varje plugin-program.

Detaljerade konfigurationer av RTE-plugin-program finns i [hur du aktiverar och konfigurerar RTE-plugin-program](configure-rich-text-editor-plug-ins.md).

<!-- TBD ENGREVIEW: To confirm if the sample works in CS or not?
**Sample**: Download [this sample configuration](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) that illustrates how to configure RTE. In this package all the features are enabled. -->

Med textkomponenten [Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor) kan mallredigerare konfigurera många RTE-plugin-program som använder användargränssnittet som innehållsprinciper, vilket eliminerar behovet av teknisk konfiguration. Innehållsprinciper kan fungera med gränssnittskonfigurationer för textredigering enligt beskrivningen i det här dokumentet. Mer information finns i [skapa sidmallar](/help/sites-cloud/authoring/features/templates.md) och i [dokumentationen till utvecklaren av kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html).

>I referenssyfte finns textstandardkomponenterna (levereras som en del av en standardinstallation) på:
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`

>
>
Om du vill skapa en egen textkomponent kopierar du ovanstående komponent i stället för att redigera de här komponenterna.

## Verktygsfältet Konfigurera RTE {#dialogfullscreen}

[!DNL Experience Manager] I kan du konfigurera gränssnittet för textredigeraren på ett annat sätt för de olika redigeringslägena. Standardinställningarna anges nedan. Du kan åsidosätta dessa standardinställningar baserat på dina behov. Du anpassar bara de verktygsfältsfunktioner som du vill ge författarna. Du behöver inte ange alla verktygsfältskonfigurationer.

Använd följande exempelkonfiguration om du vill konfigurera verktygsfältet för `dialogFullScreen`.

```java
<uiSettings jcr:primaryType="nt:unstructured">
  <cui jcr:primaryType="nt:unstructured">
    <inline
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,#justify,#lists,links#modifylink,links#unlink,#paraformat]">
      <popovers jcr:primaryType="nt:unstructured">
        <justify
          jcr:primaryType="nt:unstructured"
          items="[justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify]"
          ref="justify"/>
        <lists
          jcr:primaryType="nt:unstructured"
          items="[lists#unordered,lists#ordered,lists#outdent,lists#indent]"
          ref="lists"/>
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </inline>
    <dialogFullScreen
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify,lists#unordered,lists#ordered,lists#outdent,lists#indent,links#modifylink,links#unlink,table#createoredit,#paraformat,image#imageProps]">
      <popovers jcr:primaryType="nt:unstructured">
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </dialogFullScreen>
    <tableEditOptions
      jcr:primaryType="nt:unstructured"
      toolbar="[table#insertcolumn-before,table#insertcolumn-after,table#removecolumn,-,table#insertrow-before,table#insertrow-after,table#removerow,-,table#mergecells-right,table#mergecells-down,table#mergecells,table#splitcell-horizontal,table#splitcell-vertical,-,table#selectrow,table#selectcolumn,-,table#ensureparagraph,-,table#modifytableandcell,table#removetable,-,undo#undo,undo#redo,-,table#exitTableEditing,-]">
    </tableEditOptions>
  </cui>
</uiSettings>
```

Olika gränssnittsinställningar används för infogat läge och helskärmsläge. Egenskapen toolbar anger verktygsfältets alternativ.

Om alternativet i sig själv är en funktion (till exempel `Bold`) anges det som `PluginName#FeatureName` (till exempel `links#modifylink`).

Om alternativet är en snabbmeny (som innehåller vissa funktioner i ett plugin-program) anges det som `#PluginName` (till exempel `#format`).

Avgränsare (`|`) mellan en grupp med alternativ kan anges med `-`.

Popup-noden under infogat läge eller helskärmsläge innehåller en lista över de popup-fönster som används. Varje underordnad nod under noden `popovers` namnges efter plugin-programmet (till exempel format). Den har egenskapen &quot;items&quot; som innehåller en lista med funktioner för plugin-programmet (till exempel format#bold).

## RTE-inställningar (User Interface Settings) och innehållsprinciper {#rtecontentpolicies}

Administratörer kan styra textredigeringsalternativen med hjälp av innehållsprinciper, till exempel i stället för att göra konfigurationen enligt beskrivningen ovan. Innehållsprofiler definierar designegenskaperna för en komponent när de används som en del av en [redigerbar mall](/help/sites-cloud/authoring/features/templates.md). Om en textkomponent som använder textredigeraren till exempel används med en redigerbar mall kan innehållsprincipen definiera att det feta alternativet är tillgängligt och att några styckeformateringsalternativ är tillgängliga. Innehållsprofilerna kan återanvändas och kan tillämpas på flera mallar.

De tillgängliga alternativen i textredigeraren flödar nedåt från användargränssnittskonfigurationerna till innehållsprinciperna.

* Konfigurationsinställningarna för användargränssnittet definierar vilka alternativ som är tillgängliga för innehållsprinciperna.
* Om användargränssnittskonfigurationen för textredigeraren har tagits bort eller inte aktiverar ett objekt kan innehållsprincipen inte konfigurera det.
* En författare har bara tillgång till funktioner som är tillgängliga i användargränssnittskonfigurationerna och i innehållsprinciperna.

Du kan till exempel se [dokumentationen för textkärnkomponenten](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor).

## Anpassa mappningen mellan verktygsfältsikoner och kommandon {#iconstoolbar}

Du kan anpassa mappningen mellan koralikonerna som visas i verktygsfältet för textredigering och de tillgängliga kommandona. Du kan inte använda några andra ikoner förutom kornikoner.

1. Skapa en nod med namnet `icons` under `uiSettings/cui`.

1. Skapa noder för enskilda ikoner under den.
1. På varje enskild ikonnod anger du en korallikon och ett kommando som ska kopplas till ikonen.

Nedan visas ett exempelfragment som mappar kommandot `Bold` till koralikonen `textItalic`.

```java
<text jcr:primaryType="nt:unstructured" sling:resourceType="cq/gui/components/authoring/dialog/richtext" name="./text" useFixedInlineToolbar="{Boolean}true">
    <rtePlugins jcr:primaryType="nt:unstructured">
        <format jcr:primaryType="nt:unstructured" features="bold,italic"/>
    </rtePlugins>
    <uiSettings jcr:primaryType="nt:unstructured">
        <cui jcr:primaryType="nt:unstructured">
            <inline jcr:primaryType="nt:unstructured"
                toolbar="[format#bold,format#italic,format#underline,links#modifylink,links#unlink]">
            </inline>
            <icons jcr:primaryType="nt:unstructured">
                <bold jcr:primaryType="nt:unstructured"
                    command="format#bold"
                    icon="textItalic"/>
            </icons>
        </cui>
    </uiSettings>
</text>
```

## Kända begränsningar {#known-limitations}

[!DNL Experience Manager] RTE-kapacitet har följande begränsningar:

* RTE-funktioner stöds endast i [!DNL Experience Manager]-komponentdialogrutor. RTE stöds inte i guider eller Foundation-formulär.

* [!DNL Experience Manager] fungerar inte på hybridenheter.  <!-- TBD: Check. This is not mentioned in Known Issue /help/release-notes/known-issues.md-->

* Ge inte RTE-konfigurationsnoden namnet `config`. Annars gäller RTE-konfigurationen bara för administratörerna och inte för användarna i gruppen `content-author`.

* RTE stöder inte inbäddning av innehåll i en textbunden ram eller en iframe.

## God praxis och tips {#best-practices-and-tips}

* Aktivera bara plugin-program utan popup-dialogruta för en flytande dialogruta. Plugin-program utan popup-fönster är mindre och lämpar sig bäst för en flytande dialogruta.
* Aktivera plugin-program med större popup-fönster, till exempel `Paste`, endast i helskärmsläge eller i helskärmsläge. Plugin-program med stor popup-meny behöver mer utrymme på skärmen för att kunna skapa på ett bra sätt.
* Om du använder anpassade plugin-program för CoralUI3 RTE använder du `rte.coralui3`-biblioteket.

>[!MORELIKETHIS]
>
>* [Konfigurera RTE-plugin-program](configure-rich-text-editor-plug-ins.md)
* [Använd RTF-redigerare för att skapa](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md)
* [Konfigurera RTE för hjälpmedelsanpassade webbplatser](rte-accessible-content.md)

