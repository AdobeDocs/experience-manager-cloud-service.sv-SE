---
title: Använd RTF-redigeraren [!DNL Adobe Experience Manager] för att skapa innehåll.
description: Använd [!DNL Experience Manager] RTF-redigeraren för att skapa innehåll.
translation-type: tm+mt
source-git-commit: 5a90db8791dd92cceb811b9ed2beda3ecb4a974d
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---


# Använda RTF-redigeraren för att skapa innehåll {#use-rich-text-editor-to-author-content}

RTE (Rich Text Editor) är en grundläggande byggsten för att lägga till textinnehåll [!DNL Adobe Experience Manager]. Många andra komponenter som tillåter redigering baseras på RTE. Utvecklare i Experience Manager kan anpassa RTE och administratörer konfigurerar RTE för författare.

## In-place-redigering {#in-place-editing}

Om du markerar en textbaserad komponent med ett enda klick visas [komponentens verktygsfält](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar).

![Komponentens verktygsfält](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

Om du klickar igen eller först markerar komponenten med ett långsamt dubbelklick öppnas redigering på plats. Redigeringsläget innehåller ett verktygsfält. Du kan redigera innehållet och göra grundläggande formateringsändringar.

![In place editing with the RTE](/help/sites-cloud/authoring/assets/rte-in-place-editing.png)

Verktygsfältet innehåller vanligtvis följande alternativ:

* **Format**: Framhäv text som fet, kursiv eller understruken text.
* **Listor**: Skapa punktlistor eller numrerade listor och ange indrag.
* **Hyperlänk**: Skapa länkar.
* **Bryt länk**: Ta bort hyperlänk.
* **Helskärm**: Öppna redigeraren i helskärmsläge.
* **Stäng**: Sluta redigera.
* **Spara**: Spara ändringar.

## Redigering i helskärmsläge {#full-screen-editing}

För textbaserade komponenter klickar du på fullskärmsläget ![RTE-helskärmsknappen](/help/sites-cloud/authoring/assets/editing-full-screen.png) i [verktygsfältet](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) för att öppna RTF-redigeraren och döljer resten av sidinnehållet.

I helskärmsläge visas alla konfigurerade alternativ som du kan använda för att skapa. Vilka alternativ som är tillgängliga beror på konfigurationen. <!--Full screen mode displays all the configured options that you can use for authoring. The availability of options [depends on the configuration](/help/sites-administering/rich-text-editor.md).-->

![RTE i helskärmsläge](/help/sites-cloud/authoring/assets/rte-full-screen.png)

Fler alternativ för textredigering:

* **Ankarpunkt**: Skapa en ankarpunkt i texten som du senare kan länka till eller skapa en referens till.
* **Vänsterjustera** text.
* **Centrera text**.
* **Högerjustera** text.

Klicka på Minimera för att stänga helskärmsläget.

>[!TIP]
>
>Om du kopierar kapslade listor från [!DNL Microsoft Word] till textredigeraren kan resultatet bli inkonsekvent. Klistra i stället in som text och gör manuell justering.

>[!MORELIKETHIS]
>
>* [Konfigurera textredigerare](/help/implementing/developing/extending/rich-text-editor.md)

