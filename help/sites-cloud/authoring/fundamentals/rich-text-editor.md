---
title: Använda RTF-redigeraren i [!DNL Adobe Experience Manager] för att skapa innehåll.
description: Använd [!DNL Experience Manager] RTF-redigerare för att skapa innehåll.
exl-id: 15c175f8-11de-4475-87a9-920219a4c004
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Använda RTF-redigeraren för att skapa innehåll {#use-rich-text-editor-to-author-content}

RTE (Rich Text Editor) är en grundläggande byggsten för att lägga till textinnehåll i [!DNL Adobe Experience Manager]. Många andra komponenter som tillåter redigering är också baserade på RTE. Utvecklare i Experience Manager kan anpassa RTE och administratörer konfigurerar RTE för författare.

## In-place-redigering {#in-place-editing}

Markera en textbaserad komponent med ett enda klick för att visa [komponentverktygsfältet](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar).

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

För textbaserade komponenter klickar du på helskärmsläget ![Knappen RTE i helskärmsläge](/help/sites-cloud/authoring/assets/editing-full-screen.png) från [verktygsfält](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) för att öppna RTF-redigeraren och dölja resten av sidinnehållet.

I helskärmsläge visas alla konfigurerade alternativ som du kan använda för att skapa. Tillgänglighet av alternativ [beror på konfigurationen](/help/implementing/developing/extending/rich-text-editor.md).

![RTE i helskärmsläge](/help/sites-cloud/authoring/assets/rte-full-screen.png)

Fler alternativ för textredigering:

* **Ankarpunkt**: Skapa en ankarpunkt i texten som du senare kan länka till eller skapa en referens till.
* **Vänsterjustera text**.
* **Centrera text**.
* **Högerjustera text**.

Klicka på Minimera för att stänga helskärmsläget.

>[!TIP]
>
>Kopiera kapslade listor från [!DNL Microsoft Word] i RTE kan ge inkonsekventa resultat. Klistra i stället in som text och gör manuell justering.

>[!MORELIKETHIS]
>
>* [Konfigurera textredigerare](/help/implementing/developing/extending/rich-text-editor.md)

