---
title: Aktivera UI-utökningsbarhet i  [!DNL AEM Assets View]
description: Lär dig mer om UI-utökningsfunktionen i  [!DNL AEM Assets View]. [!DNL AEM Assets View] gränssnittet gör att du kan lägga till anpassade gränssnittskomponenter som uppfyller specifika affärsbehov.
feature: App Builder
role: User, Developer
exl-id: a11f7043-17cf-4331-b76c-d3db099c2411
source-git-commit: a03e6cf842f95f8799f23ed5c7e3b563b092b4e5
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# Aktivera UI-utökningsbarhet i [!DNL AEM Assets View] {#AEM-Assets-View-UI-Extensibility}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime och Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets-integrering med Edge Delivery Services</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Aktivera Dynamic Media Prime och Ultimate</b></a>
        </td>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Sök efter bästa praxis</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Metadata - bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamiska media med OpenAPI-funktioner</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets-dokumentation för utvecklare</b></a>
        </td>
    </tr>
</table>

[!DNL AEM Assets View] har stöd för UI-utbyggbarhet, vilket gör att du kan lägga till anpassade UI-komponenter i [!DNL Assets View]-gränssnittet för specifika arbetsflöden och affärskrav som inte uppfylls av de körklara funktionerna i [!DNL AEM Assets View]. Den här utökningsfunktionen för användargränssnitt i [!DNL AEM Assets View] förbättrar flexibiliteten och gör det möjligt för organisationer att anpassa gränssnittet för specifika arbetsflöden och krav.\
Du kan lägga till dina tillägg på nivån **Resurs**, **Mapp** och **Samling**. Det tillagda tillägget visas på en dedikerad panel på sidan **Resurs**, **Samling** eller **Mapp** **[!UICONTROL Details]**.

>[!IMPORTANT]
>
> * [!DNL AEM Assets View] UI-utbyggbarhet är tillgänglig med [[!DNL Assets Ultimate]](/help/assets/assets-ultimate-overview.md).
> * [Skapa och skicka ett  [!DNL Adobe] kundsupportärende](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) om du vill få åtkomst till [!DNL Assets view] UI-utökningsbarhet.
> * Du kan ge feedback genom att expandera **[!UICONTROL Detailed Feedback options]** och klicka på **[!UICONTROL Report an issue]**.

## <a id="1"></a> Öppna Assets-vyn{#add-UI-Extensibility-in-AEM-Assets-View}

Följ stegen som anges i bilden nedan för att komma åt [!DNL Assets View]:
![ access-assets-view-ui ](/help/assets/assets/access-assets-view.jpg)

## Visa gränssnittstillägg i [!DNL Assets View] {#ui-extensibility-panel-assets-view}

Gå till sidan **[!UICONTROL Details]** för en resurs, mapp eller samling i [!DNL Assets View]. Sidan **[!UICONTROL Details]** visar det tillagda gränssnittstillägget på en dedikerad panel.
![min arbetsyta](/help/assets/assets/my-workspace-assets-view3.png)

## Krav för att lägga till utökningskomponenten{#assets-view-ui-extensibility}

Fyll i följande krav om du vill börja lägga till utökningskomponenten i [!DNL Assets View UI]:

* [Åtkomst till [!DNL Assets View]](#1).
* Åtkomst till [[!DNL Adobe app builder]](https://developer.adobe.com/app-builder/docs/overview/).
* Tillstånd till utvecklare av systemadministratörsrollen inom organisationen. Mer information finns i [den här dokumentationen](https://developer.adobe.com/uix/docs/guides/get-access/).
* [!DNL Adobe IO command line tool (AIO CLI)] är installerat på dina lokala datorer. Det här verktyget är nödvändigt för att skapa och distribuera tilläggsprojekt. Mer information finns i [Skapa ditt första App Builder-program](https://developer.adobe.com/app-builder/docs/get_started/app_builder_get_started/first-app#local-environment-set-up) (kräver autentisering för åtkomst).
* Bra insikt i [!DNL JavaScript]-, [!DNL Node.js]- och [!DNL React]-tekniker.

## Lägg till UI-utökningskomponenten i [!DNL Assets View] {#ui-extensibility-in-assets-view}

1. Se [Komma igång](https://developer.adobe.com/uix/docs/getting-started/) för viktig information om gränssnittstillägg och ramverket [!DNL Adobe App Builder]. Lär dig hur UI Extensibility möjliggör integrering av anpassad logik och gränssnitt i [!DNL Adobe Experience Cloud services] och förstå arkitekturen och arbetsflödet för implementering av UI-tillägg.
1. Se [Stödlinjer](https://developer.adobe.com/uix/docs/guides/) för allmän information om UI-utökningsmöjligheter, inklusive lokal miljöinställning, lokal förhandsgranskning, publicering och hantering.
1. Se [Vanliga koncept för att skapa tillägg](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/) för att förstå grunderna som krävs för att utveckla ett gränssnittstillägg för [!DNL AEM Assets View].
1. Lägg till anpassade sidopaneler i gränssnittet [!DNL Assets View]. Värdprogrammet ([!DNL Assets View]) hanterar de här panelerna för att hantera gränssnittsinteraktioner som växlingar och djuplänkning. Tillägg använder tilläggspunkten `aem/assets/details/1` för att integrera anpassade paneler som anger egenskaper, till exempel panel-ID, rubrik och innehålls-URL. Utvecklare registrerar anpassade paneler med metoden `getPanels()` och skapar vägar för att visa anpassat innehåll. Detaljerad implementering, inklusive API-referenser och kodexempel, finns i [Detaljvy](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/details-view/).
1. Konfigurera den lokala miljön och skapa ditt första användargränssnittstillägg för att få en första upplevelse av processen att utveckla användargränssnittstillägg i [!DNL Assets View]. Mer information finns i [Steg-för-steg-AEM Assets View Extension Development](https://developer.adobe.com/uix/docs/services/aem-assets-view/extension-development/).
1. Konfigurera programmet med AIO CLI för att generera den grundläggande tilläggsstrukturen och den nödvändiga koden. Mer information finns i [kodgenerering för  [!DNL AEM Assets View]](https://developer.adobe.com/uix/docs/services/aem-assets-view/code-generation/).
1. Testa tilläggen lokalt för att kontrollera att de fungerar som förväntat före distributionen. Kör tillägget i en helt isolerad miljö eller med partiell isolering och anslut tillägget till produktionen [!DNL AEM Assets View] för testning. Mer information finns i [Felsökning - [!DNL AEM Assets View] utökningsbarhet](https://developer.adobe.com/uix/docs/services/aem-assets-view/debug/).

## Anpassa snabbåtgärder och åtgärdsfältet i Assets-vyn {#customize-quick-actions-and-actions-bar}

Du kan anpassa de åtgärder som visas när du markerar en eller flera resurser (åtgärdsfältet) i Assets-vyn. I Assets-vyn kan du även anpassa de åtgärder som visas när du klickar på Fler alternativ (..) på resurskortet. Mer information finns i [Bläddra i vyn](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/browse-view/).

## Öppna anpassade dialogrutor i Assets-vyn {#open-custom-dialogs-assets-view}

I Assets-vyn kan du även öppna anpassade dialogrutor med valfri text. Du kan också lägga till länkar till texten. Mer information finns i [Modal API](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/#modal-api).
