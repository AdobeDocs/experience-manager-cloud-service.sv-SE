---
title: Konfigurera RTE för att skapa tillgängliga webbsidor och webbplatser.
description: Lär dig konfigurera RTF-redigeraren för att skapa tillgängliga webbplatser i [!DNL Adobe Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 96c59974a868779df6979818bea0d942060cf5bc
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 1%

---


# Konfigurera RTE för att skapa tillgängliga webbplatser {#configure-rte-accessible-sites}

[!DNL Adobe Experience Manager] har stöd för vanliga hjälpmedelsfunktioner, som alternativ text för bilder, och extra funktioner som är tillgängliga när du skapar innehåll. Innehållsförfattare använder dessa funktioner med komponenter som använder textredigeraren. Funktionerna innefattar att lägga till alt-text, strukturinformation via rubriker och styckeelement och så vidare.

Mer information om typiska konfigurationer av RTE finns i [Konfigurera RTE](rich-text-editor.md) och [konfigurera RTE-plugin-program för specifika funktioner](configure-rich-text-editor-plug-ins.md).

Använd RTE-pluginkonfigurationen för att konfigurera och anpassa tillgänglighetsrelaterade funktioner. Du kan t.ex. använda `paraformat` för att lägga till semantiska element på extra blocknivå, inklusive att utöka antalet rubriknivåer som stöds utanför den grundläggande `H1`nivån `H2` och som `H3` anges som standard. RTF-redigeringen är möjlig med många komponenter från redigeringsgränssnittet. De vanligaste komponenterna är text, bilder, nedladdningar och så vidare.

RTE-funktionen kan göras tillgänglig i många komponenter. Den primära komponenten är `Text` komponenten.

För `Text` komponenten i [!DNL Experience Manager]visas följande skärmbild textredigeraren med ett antal plugin-program aktiverade, inklusive `paraformat`:

![Komponenten RTE-text i helskärmsläge](assets/rte-toolbar-full-screen-mode.png)

## Konfigurera plug-in-funktionerna {#configuring-the-plugin-features}

Anvisningar om hur du konfigurerar RTE finns i [Konfigurera RTF-redigeraren](rich-text-editor.md) . Artikeln omfattar

* [Plugin-program och deras funktioner](rich-text-editor.md#aboutplugins)
* [Konfigurationsplatser](rich-text-editor.md#understand-the-configuration-paths-and-locations)
* [Aktivera ett plugin-program och konfigurera egenskapen features](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)
* [Konfigurera andra funktioner i RTE](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)

Om du vill aktivera några eller alla funktioner för ett plugin-program konfigurerar du plugin-programmet i rätt `rtePlugins` underavdelning i CRXDE Lite.

![CRXDE Lite med exempelplugin-programmet](assets/example-rteplugin-crxde-lite.png)

### Exempel på hur du anger styckeformat i markeringsfältet för textredigering {#example-specifying-paragraph-formats-available-in-rte-selection-field}

Nya semantiska blockformat är tillgängliga för markering.

1. Beroende på vilken RTE du använder kan du bestämma och navigera till [konfigurationsplatsen](rich-text-editor.md#understand-the-configuration-paths-and-locations).
1. [Aktivera styckemarkeringsfältet](rich-text-editor.md) genom [att aktivera plugin-programmet](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [Ange de format som du vill ha i styckemarkeringsfältet](rich-text-editor.md).
1. Styckeformaten är sedan tillgängliga för innehållsförfattaren från markeringsfälten i textredigeraren.

Strukturella element som är tillgängliga i textredigeraren via alternativen för styckeformat utgör en bra grund för utveckling av hjälpmedelsanpassat innehåll. [!DNL Experience Manager] Innehållsförfattare kan inte använda textredigeraren för att formatera teckenstorlek, färger eller andra relaterade attribut, vilket förhindrar att textbunden formatering skapas. I stället kan författarna välja lämpliga strukturella element, t.ex. rubriker, och använda globala format som valts med alternativet Format för att säkerställa ren markering och fler alternativ för användare som bläddrar med egna formatmallar och korrekt strukturerat innehåll.

## Användning av funktionen Källredigering {#use-of-the-source-edit-feature}

I vissa fall måste innehållsförfattare granska och justera HTML-källkoden som skapats med RTE. En del innehåll som skapats i en textredigerare kan till exempel kräva mer kod för att säkerställa överensstämmelse med WCAG 2.0. Detta kan du göra med [källredigeringsalternativet](rich-text-editor.md#aboutplugins) i textredigeraren. Du kan ange [`sourceedit` funktionen för `misctools` plugin-programmet](rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>Använd `sourceedit` funktionen noggrant. Skrivfel och funktioner som inte stöds kan orsaka problem.

<!--
TBD ENGREVIEW: Is this only applicable to Classic UI? 

## Adding Support for further HTML Elements and Attributes {#adding-support-for-additional-html-elements-and-attributes}

To further extend the accessibility features of [!DNL Experience Manager], it is possible to extend the existing components based on the RTE (such as the `Text` and `Table` components) with extra elements and attributes.

The following procedure illustrates how to extend the `Table` component with a `Caption` element that provides information about a data table to assistive technology users:

### Example: Add a caption to a table properties dialog {#example-adding-the-caption-to-the-table-properties-dialog}

In the constructor of the `TablePropertiesDialog`, add an extra text input field that is used for editing the caption. Set the `itemId` to `caption` (the DOM attribute’s name) to automatically handle its content.

In a `Table`, set the attribute to the DOM element or or remove it from the DOM element. The dialog in the `config` object passed the value. Set or remove the DOM attributes using the corresponding `CQ.form.rte.Common` methods (`com` is a shortcut for `CQ.form.rte.Common`). Using `CQ.form.rte.Common` methods avoids common pitfalls with browser implementations.

>[!NOTE]
>
>This procedure is only suitable for the classic UI.

### Step-by-step instructions {#step-by-step-instructions}

1. Start CRXDE Lite. For example: [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)

1. Copy `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js` to `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`. Create intermediate folders if those do not exist.

1. Copy `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js` to `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. Open `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js` file to edit.

1. In the `constructor` method, before the mention of `var dialogRef = this;`, add the following code:

   ```javascript
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. Open `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js` file.

1. Add the following code at the end of the `transferConfigToTable` method:

   ```javascript
   /**
    * Adds Caption Element
   */
   var captionElement;
   if (dom.firstChild && dom.firstChild.tagName.toLowerCase() == "caption")
   {
      captionElement = dom.firstChild;
   }
   if (config.caption)
   {
       var captionTextNode = document.createTextNode(config.caption)
       if (captionElement)
       {
          dom.replaceNode(captionElement.firstChild,captionTextNode);
       } else
       {
           captionElement = document.createElement("caption");
           captionElement.appendChild(captionTextNode);
           if (dom.childNodes.length>0)
           {
              dom.insertBefore(captionElement, dom.firstChild);
           } else
           {
              dom.appendChild(captionElement);
           }
       }
   } else if (captionElement)
   {
     dom.removeChild(captionElement);
   }
   ```

1. To save your changes, click **[!UICONTROL Save All]**.

## Best practices and limitations {#best-practices-limitations-tips}

* A plain text field is not the only type of input allowed for the value of the caption element. You can use any ExtJS widget, that provides the caption’s value through its `getValue()` method.
* To add editing capabilities for more elements and attributes, ensure that:

  * The `itemId` property for each corresponding field is set to the name of the appropriate DOM attribute (`TablePropertiesDialog`).
  * The attribute is set and/or removed on the DOM element explicitly (`Table`).
-->

>[!MORELIKETHIS]
>
>* [En snabbguide till WCAG-standarder](/help/onboarding/accessibility/quick-guide-wcag.md)
>* [Skapa tillgängligt innehåll i Experience Manager](/help/sites-cloud/authoring/fundamentals/accessible-content.md)

