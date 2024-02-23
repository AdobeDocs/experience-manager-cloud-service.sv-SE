---
title: Konfigurera RTF-redigeraren för att skapa innehåll i [!DNL Adobe Experience Manager] as a Cloud Service.
description: Konfigurera RTF-redigeraren för att skapa innehåll i [!DNL Adobe Experience Manager] as a Cloud Service.
contentOwner: AG
exl-id: 1f0ff800-5e95-429a-97f2-221db0668170
source-git-commit: a868bf4d4acf4fbae7ccaf55b03319ba0617f9a4
workflow-type: tm+mt
source-wordcount: '1858'
ht-degree: 0%

---

# Konfigurera RTF-redigeraren {#configure-the-rich-text-editor}

Med RTF-redigeraren får författarna ett stort antal funktioner för att redigera textinnehåll. Ikoner, markeringsrutor, verktygsfält och menyer finns för WYSIWYG-textredigering. Administratörer konfigurerar RTE för att aktivera, inaktivera och utöka de funktioner som är tillgängliga i redigeringskomponenterna. Se hur författare [använd RTE för redigering](/help/sites-cloud/authoring/page-editor/rich-text-editor.md) webbinnehåll.

De RTE-begrepp och -steg som krävs för att konfigurera den listas nedan.

| Förstå RTE-koncept | Aktivera nödvändiga funktioner | Konfigurera enskilda funktioner |
|---|---|---|
| [Förstå gränssnittet](#understand-rte-ui) | [Förstå och ange konfigurationsplatser](#understand-the-configuration-paths-and-locations) | [Konfigurera plugin-program](#enable-rte-functionalities-by-activating-plug-ins) |
| [Olika typer av redigeringslägen](#editingmodes) | [Aktivera plugin-program](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin) | [Ange funktionsegenskaper](#aboutplugins) |
| [Om plugin-program](#aboutplugins) | [Konfigurera RTE-verktygsfält](#dialogfullscreen) | [Konfigurera inklistringslägena](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles) |

## Förstå användargränssnittet som är tillgängligt för författare {#understand-rte-ui}

RTE-gränssnittet erbjuder en [responsiv design](/help/sites-cloud/authoring/page-editor/responsive-layout.md) för redigeringsmiljön. Gränssnittet är utformat för att användas på enheter med pekskärm och stationära datorer.

![Verktygsfältet för textredigeraren](assets/rte-toolbar-full-screen-mode.png)

*Bild: Verktygsfältet för textredigeraren med alla tillgängliga alternativ aktiverade.*

Verktygsfältet innehåller alternativ för WYSIWYG-redigering. [!DNL Experience Manager] administratörer kan konfigurera de alternativ som är tillgängliga i verktygsfältet i gränssnittet. En omfattande uppsättning redigeringsalternativ finns som standard i [!DNL Experience Manager]. Utvecklare kan anpassa [!DNL Experience Manager] om du vill lägga till fler redigeringsalternativ.

## Olika redigeringslägen {#editingmodes}

Författare kan skapa och redigera textinnehåll i [!DNL Experience Manager] med de olika komponentlägena. Alternativen i verktygsfältet för att skapa och formatera innehåll och användarupplevelsen i komponenter med RTE-funktioner i olika redigeringslägen varierar beroende på RTE-konfigurationer.

| Redigeringsläge | Redigeringsområde | Rekommenderade funktioner som ska aktiveras |
|--- |--- |--- |
| Textbunden | Redigera på plats för snabba smärre redigeringar. Formatera utan att öppna en dialogruta. | Minimala RTE-funktioner. |
| RTE helskärm | Täcker hela sidan. | Alla nödvändiga RTE-funktioner. |
| Dialog | Dialogrutan visas ovanpå sidinnehållet men täcker inte hela sidan. | Aktivera funktioner i jakt. |
| Dialogruta i helskärmsläge | Samma som helskärmsläge; innehåller fält i dialogrutan tillsammans med RTE. | Alla nödvändiga RTE-funktioner. |

>[!NOTE]
>
>Funktionen för källredigering är inte tillgänglig i infogat redigeringsläge. Du kan inte dra bilder i helskärmsläge. Alla andra funktioner fungerar i alla lägen.

### Redigering direkt {#inline-editing}

Om du vill redigera innehållet på en sida öppnar du innehållet med ett långsamt dubbelklick . Ett kompakt verktygsfält med grundläggande alternativ visas.

![Direktredigering med grundläggande alternativ i verktygsfältet](assets/inline-editing-mode-basic-options.png)

*Bild: Inline-redigering med grundläggande alternativ i verktygsfältet.*

### Redigering i helskärmsläge {#full-screen-editing}

[!DNL Experience Manager] -komponenter kan öppnas i helskärmsläge som döljer sidinnehållet och tar upp den tillgängliga skärmen. Överväg att redigera i helskärmsläge som en detaljerad version av den infogade redigeringen eftersom den erbjuder de flesta redigeringsalternativen. Du kan öppna den genom att klicka ![Ikon för att öppna RTE i helskärmsläge](assets/rte_fullscreen.png)från det kompakta verktygsfältet när du använder det infogade redigeringsläget.

I dialogrutans helskärmsläge, tillsammans med ett detaljerat verktygsfält för textredigering, är även de alternativ och komponenter som är tillgängliga i en dialogruta tillgängliga. Det gäller endast för en dialogruta som innehåller RTE tillsammans med andra komponenter.

![Det detaljerade verktygsfältet för textredigering när du redigerar i helskärmsläge](assets/rte-toolbar-full-screen-mode.png)

*Bild: Det detaljerade verktygsfältet för textredigering när du redigerar i helskärmsläge.*

### Dialogruteredigering {#dialog-editing}

När du dubbelklickar på en komponent öppnas en dialogruta där du kan redigera innehållet. Dialogrutan öppnas ovanpå den befintliga sidan. I vissa specifika scenarier öppnas dialogrutan som ett popup-fönster. Om en textkomponent till exempel är en del av en kolumn i en sidlayout med flera kolumner och området som är tillgängligt för dialogrutan är mindre.

![Dialogruteredigeringsläge](assets/dialog_editing_modetouchui.png)

*Bild: Dialogruteredigeringsläge.*

## Om RTE-plugin-program och associerade funktioner {#aboutplugins}

Funktionerna är tillgängliga via ett antal plugin-program, var och en med:

* A `features` egenskap som är

   * Används för att aktivera eller inaktivera grundläggande funktioner för det plugin-programmet.
   * Konfigureras med en standardiserad procedur.

* I tillämpliga fall krävs specialkonfigurering för fler egenskaper och alternativ.

Grundfunktionerna i textredigeringsprojektet aktiveras, eller inaktiveras, av värdet på `features` på en nod som är specifik för rätt plugin-program.

I följande tabell visas de aktuella plugin-programmen:

* Plugin-ID:n med en länk till API-dokumentationen. ID används som nodnamn när [aktivera ett plugin-program](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin).
* Tillåtna värden för `features` -egenskap.
* En beskrivning av de funktioner som tillhandahålls av plugin-programmet.

| Plug-in-ID | funktioner | Beskrivning |
|--- |--- |--- |
| redigera | `cut`, `copy`, `paste-default`, `paste-plaintext`, `paste-wordhtml` | [Klipp ut, kopiera och, de tre inklistringslägena](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles). |
| findreplace | `find`, `replace` | Sök och ersätt. |
| format | `bold`, `italic`, `underline` | [Grundläggande textformatering](configure-rich-text-editor-plug-ins.md#textstyles). |
| image | `image` | Grundläggande bildstöd (dra från innehåll eller Innehållssökning). Beroende på webbläsaren har stödet olika beteenden för författare |
| tangenter | - | Information om hur du definierar det här värdet finns i [tabbstorlek](configure-rich-text-editor-plug-ins.md#tabsize). |
| justera | `justifyleft`, `justifycenter`, `justifyright` | Styckejustering. |
| länkar | `modifylink`, `unlink`, `anchor` | [Hyperlänkar och ankarpunkter](configure-rich-text-editor-plug-ins.md#linkstyles). |
| listor | `ordered`, `unordered`, `indent`, `outdent` | Detta plugin-program kontrollerar båda [indrag och listor](configure-rich-text-editor-plug-ins.md#indentmargin); inklusive kapslade listor. |
| felverktyg | `specialchars`, `sourceedit` | Med andra verktyg kan man skriva [specialtecken](configure-rich-text-editor-plug-ins.md#spchar) eller redigera HTML-källan. Du kan också lägga till en [intervall med specialtecken](configure-rich-text-editor-plug-ins.md#definerangechar) om du vill definiera en egen lista. |
| Paraformat | `paraformat` | Standardstyckeformaten är Stycke, Rubrik 1, Rubrik 2 och Rubrik 3 (`<p>`, `<h1>`, `<h2>`och `<h3>`). Du kan [lägga till fler styckeformat](configure-rich-text-editor-plug-ins.md#paraformats) eller utöka listan. |
| stavningskontroll | `checktext` | [Språkmedveten stavningskontroll](configure-rich-text-editor-plug-ins.md#adddict). |
| stilar | `styles` | Stöd för formatering med en CSS-klass. [Lägga till nya textformat](configure-rich-text-editor-plug-ins.md#textstyles) om du vill lägga till (eller utöka) egna format för användning med text. |
| nedsänkt | `subscript`, `superscript` | Tillägg till de grundläggande formaten, med underskript och superskript. |
| table | `table`, `removetable`, `insertrow`, `removerow`, `insertcolumn`, `removecolumn`, `cellprops`, `mergecells`, `splitcell`, `selectrow`, `selectcolumns` | Se [konfigurera tabellformat](configure-rich-text-editor-plug-ins.md#tablestyles) om du vill lägga till egna format för hela tabeller eller enskilda celler. |
| ångra | `undo`, `redo` | Historikstorlek för [ångra och göra om](configure-rich-text-editor-plug-ins.md#undohistory) åtgärder. |

>[!NOTE]
>
>Plugin-programmet för helskärmsläge stöds inte i dialogruteläge. Användning av `dialogFullScreen` inställning för att konfigurera verktygsfältet för helskärmsläge.

## Förstå konfigurationssökvägar och -platser {#understand-the-configuration-paths-and-locations}

The [RTE-redigeringsläge och gränssnitt](#editingmodes) som du anger för författarna bestämmer var konfigurationsinformationen ska placeras när du är [aktivera RTE-plugin-program](configure-rich-text-editor-plug-ins.md#activateplugin). Platserna är:

* Textbunden: `cq:editConfig/cq:inplaceEditing`.
* Helskärmsläge: `cq:editConfig/cq:inplaceEditing`.
* Dialogruteläge: `cq:dialog`.
* Dialogruteläge för helskärm: `cq:dialog`.

>[!NOTE]
>
>Namnge inte noden under `cq:inplaceEditing` as `config`. På `cq:inplaceEditing` -nod definierar du följande egenskaper:
>
>* **Namn**: `configPath`
>* **Typ**: `String`
>* **Värde**: sökväg till noden som innehåller den faktiska konfigurationen
>
>Ge inte RTE-konfigurationsnoden namnet `config`. I annat fall gäller RTE-konfigurationerna bara för administratörerna och inte för användarna i gruppen `content-author`.

Konfigurera följande egenskaper som gäller i redigeringsläget för dialogrutor:

* `useFixedInlineToolbar`: Du kan göra så att verktygsfältet RTE är fast i stället för flytande. Ange den här booleska egenskapen som är definierad på RTE-noden med sling:resourceType= `cq/gui/components/authoring/dialog/richtext` till `True`. När den här egenskapen är inställd på `True`, är textredigeringen startad på `foundation-contentloaded` -händelse. Du kan förhindra detta genom att ange egenskapen `customStart` till `True` och aktivera `rte-start` -händelse för att starta RTE-redigering. När den här egenskapen `true`, RTE startar inte vid klickning och detta är standardbeteendet.

* `customStart`: Ange den här booleska egenskapen som definieras på RTE-noden till `True`för att styra när RTE ska startas genom att händelsen utlöses `rte-start`.

* `rte-start`: Utlös den här händelsen på `contenteditable-div` av RTE, när redigering av RTE ska börja. Fungerar bara om `customStart` har angetts till `true`.

När textredigeraren används i dialogrutan med pekfunktioner anger du egenskapen `useFixedInlineToolbar` till `true` för att undvika problem.

## Aktivera RTE-funktioner genom att aktivera plugin-program {#enable-rte-functionalities-by-activating-plug-ins}

RTE-funktioner är tillgängliga via en serie plugin-program, var och en med features-egenskaper. Du kan konfigurera egenskapen features för att aktivera eller inaktivera de olika funktionerna i varje plugin-program.

Detaljerade konfigurationer av RTE-plugin-program finns i [aktivera och konfigurera RTE-plugin-program](configure-rich-text-editor-plug-ins.md).

<!-- TBD ENGREVIEW: To confirm if the sample works in CS or not?
**Sample**: Download [this sample configuration](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) that illustrates how to configure RTE. In this package all the features are enabled. -->

The [Textkomponent för kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor) I kan mallredigerare konfigurera många RTE-plugin-program med användargränssnittet som innehållsprinciper, vilket eliminerar behovet av teknisk konfiguration. Innehållsprinciper kan fungera med gränssnittskonfigurationer för textredigering enligt beskrivningen i det här dokumentet. Mer information finns i [skapa sidmallar](/help/sites-cloud/authoring/sites-console/templates.md) och [Dokumentation för grundkomponentutvecklare](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html).

>I referenssyfte finns textstandardkomponenterna (levereras som en del av en standardinstallation) på:
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>Om du vill skapa en egen textkomponent kopierar du ovanstående komponent i stället för att redigera de här komponenterna.

## Verktygsfältet Konfigurera RTE {#dialogfullscreen}

[!DNL Experience Manager] I kan du konfigurera gränssnittet för RTF-redigeraren på ett annat sätt för de olika redigeringslägena. Standardinställningarna anges nedan. Du kan åsidosätta dessa standardinställningar baserat på dina behov. Du anpassar bara de verktygsfältsfunktioner som du vill ge författarna. Du behöver inte ange alla verktygsfältskonfigurationer.

Konfigurera verktygsfältet för `dialogFullScreen`använder du följande exempelkonfiguration.

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

Om till exempel själva alternativet är en funktion (till exempel `Bold`), anges som `PluginName#FeatureName` (till exempel `links#modifylink`).

Om alternativet är ett popup-fönster (som innehåller vissa funktioner i ett plugin-program) anges det som `#PluginName` (till exempel `#format`).

Avgränsare (`|`) mellan en grupp alternativ kan anges med `-`.

Popup-noden under infogat läge eller helskärmsläge innehåller en lista över de popup-fönster som används. Varje underordnad nod under `popovers` Noden namnges efter plugin-programmet (till exempel format). Den har egenskapen &quot;items&quot; som innehåller en lista med funktioner för plugin-programmet (till exempel format#bold).

## RTE-inställningar (User Interface Settings) och innehållsprinciper {#rtecontentpolicies}

Administratörer kan styra textredigeringsalternativen med hjälp av innehållsprinciper, till exempel i stället för att göra konfigurationen enligt beskrivningen ovan. Innehållsprofiler definierar designegenskaperna för en komponent när de används som en del av en [redigerbar mall](/help/sites-cloud/authoring/sites-console/templates.md). Om en textkomponent som använder textredigeraren till exempel används med en redigerbar mall kan innehållsprincipen definiera att det feta alternativet är tillgängligt och att några styckeformateringsalternativ är tillgängliga. Innehållsprofilerna kan återanvändas och kan tillämpas på flera mallar.

De tillgängliga alternativen i textredigeraren flödar nedåt från användargränssnittskonfigurationerna till innehållsprinciperna.

* Konfigurationsinställningarna för användargränssnittet definierar vilka alternativ som är tillgängliga för innehållsprinciperna.
* Om användargränssnittskonfigurationen för textredigeraren har tagits bort eller inte aktiverar ett objekt kan innehållsprincipen inte konfigurera det.
* En författare har bara tillgång till funktioner som är tillgängliga i användargränssnittskonfigurationerna och i innehållsprinciperna.

Du kan till exempel se [Dokumentation för komponenten Text Core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor).

## Anpassa mappningen mellan verktygsfältsikoner och kommandon {#iconstoolbar}

Du kan anpassa mappningen mellan koralikonerna som visas i verktygsfältet för textredigering och de tillgängliga kommandona. Du kan inte använda några andra ikoner förutom kornikoner.

1. Skapa en nod med namnet `icons` under `uiSettings/cui`.

1. Skapa noder för enskilda ikoner under den.
1. På varje enskild ikonnod anger du en korallikon och ett kommando som ska kopplas till ikonen.

Nedan finns ett exempelfragment som mappar kommandot `Bold` till korallikonen med namnet `textItalic`.

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

* RTE-funktioner stöds endast i [!DNL Experience Manager] komponentdialogrutor. RTE stöds inte i guider eller Foundation-formulär.

* [!DNL Experience Manager] fungerar inte på hybridenheter. <!-- TBD: Check. This is not mentioned in Known Issue /help/release-notes/known-issues.md-->

* Namnge inte RTE-konfigurationsnoden `config`. I annat fall gäller RTE-konfigurationen bara för administratörerna och inte för användarna i gruppen `content-author`.

* RTE stöder inte inbäddning av innehåll i en textbunden ram eller en iframe.

## God praxis och tips {#best-practices-and-tips}

* Aktivera bara plugin-program utan dialogruta för en flytande dialogruta. Plugin-program utan popup-fönster är mindre och lämpar sig bäst för en flytande dialogruta.
* Aktivera plugin-programmen med större popup-fönster, till exempel `Paste` plugin-program, endast i helskärmsläge eller helskärmsläge. Plugin-program med stor popup-meny behöver mer utrymme på skärmen för att kunna skapa på ett bra sätt.
* Om du använder anpassade plugin-program för CoralUI3 RTE ska du använda `rte.coralui3` bibliotek.

>[!MORELIKETHIS]
>
>* [Konfigurera RTE-plugin-program](configure-rich-text-editor-plug-ins.md)
>* [Använd RTF-redigerare för att skapa](/help/sites-cloud/authoring/page-editor/rich-text-editor.md)
>* [Konfigurera RTE för hjälpmedelsanpassade webbplatser](rte-accessible-content.md)
