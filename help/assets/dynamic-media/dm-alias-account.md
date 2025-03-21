---
title: Konfigurera ett konto för företaget Dynamic Media
description: Lär dig hur du konfigurerar ett företagalias-konto i Dynamic Media.
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 886063d4-71dd-48c8-a342-884ad2c111ca
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# Konfigurera ett Dynamic Media-företagskonto {#about-dm-alias-acct}

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
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI-utökningsbarhet</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Aktivera Dynamic Media Prime och Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Sök efter bästa praxis</b></a>
        </td>
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

<!-- hide: yes
hidefromtoc: yes -->

<!-- >[!NOTE]
>
>This feature to create a Dynamic Media company alias account is in the Prerelease Channel for January 2022. See [Prerelease Channel documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=en#enable-prerelease) for information on how to enable the feature for your environment. The feature is generally available in the February 2022 release. -->

Dynamic Media-URL:er och visningsprogrammets inbäddningskod innehåller företagskontots namn. Det här kontonamnet skapades när Dynamic Media etablerades. Det kan finnas scenarier där ditt företag har genomgått ett förvärv, en omprofilering eller där du bara vill använda ett mer minnesvärt namn. I sådana fall är det inte enkelt att manuellt uppdatera företagskontots namn i alla URL:er och visningsprogrammets inbäddningskod som kommer ut ur kartongen. Dessutom finns det en möjlighet att du kan påverka din befintliga Dynamic Media-databas eller påverka livematerialet. Du kan lösa det här problemet genom att konfigurera ett Dynamic Media-företagskonto.

Ett Dynamic Media-företagskonto som alias ser till att alla färdiga dynamiska medie-URL:er och visningsprogramkod i användargränssnittet återspeglar alla uppdateringar som gjorts i ditt företagskontext, till exempel omprofilering. Ett aliaskonto har också en positiv effekt på SEO (sökmotoroptimering) eftersom Dynamic Media-URL:er och visningsprogrammets inbäddningskod återspeglar det nya företagskontots namn.

Tänk på följande när du konfigurerar ett Dynamic Media-företagskonto:

* Alla befintliga dynamiska medie-URL:er eller visningsprograminbäddningskod för dina *live*-digitala egenskaper måste uppdateras manuellt för att återspegla det nya aliasnamnet. Alla URL-adresser och visningsprogram bäddar in kod med det ursprungliga dynamiska mediets företagsnamn och fortsätter att fungera för befintliga eller nya resurser.
* Funktionen för ett Dynamic Media-företagskonto är begränsad till Experience Manager Assets redigeringsläge och leverans. Företagets aliasnamn fungerar inte med Experience Manager Sites. WCM-komponenter (Web Content Management) har inte uppdaterats för den här ändringen. Dessa komponenter fortsätter att fungera med det ursprungliga företaget Dynamic Media för att hämta dynamiska medieresurser.
* Du kan bara konfigurera ett företagalias-konto på sidan **[!UICONTROL Edit Dynamic Media Configuration]**. Du kan dock skapa så många alias-konton för företag genom ett supportärende och manuellt spegla det nödvändiga aliasnamnet i Dynamic Media URL:er eller visningsprogrammets inbäddningskod.
* Funktionen [Cacheinvalidering](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md) i Dynamic Media som är klar att användas gör URL:erna ogiltiga med både företagskonton och företagskonton konfigurerade på sidan Dynamisk mediekonfiguration i molntjänster.
* När du konfigurerar ett företagalias-konto på sidan **[!UICONTROL Edit Dynamic Media Configuration]** måste du göra URL:er för *både* **[!UICONTROL Company]**-kontot och **[!UICONTROL Company Alias]** ogiltiga samtidigt för att cacheminnet ska lyckas.

Se även [Skapa en dynamisk mediekonfiguration i molntjänster](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)

## Konfigurera ett konto för företaget Dynamic Media {#configure-dm-alias-account}

Du börjar konfigurera ett Dynamic Media-företagskonto genom att först skicka ett supportärende. Det här steget är obligatoriskt.

1. [Använd Admin Console för att skapa ett supportärende](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).
1. Ange följande information i ditt supportärende:

   * Det namn på företaget Dynamic Media som du vill använda. Namnet får bara innehålla ** bokstäver (blandat skiftläge tillåts), siffror, bindestreck och understreck.
   * Din region.
   * Anger om någon [regeluppsättning](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md) används tidigare för att visa hur dynamiskt medieinnehåll kan hanteras via ett alternativt företagskontonamn för Dynamic Media.

1. När Dynamic Media-aliaskontot har skapats av Support väljer du Experience Manager as a Cloud Service logotyp i Experience Manager as a Cloud Service Author. Då öppnas den globala navigeringskonsolen.
1. Till vänster om konsolen väljer du verktygsikonen och går till **[!UICONTROL Cloud Services > Dynamic Media Configuration]**.
1. På sidan Dynamic Media Configuration Browser väljer du **[!UICONTROL global]** i den vänstra rutan (markera inte mappikonen till vänster om **[!UICONTROL global]**). Välj sedan **[!UICONTROL Edit]**.

   ![Textfältet Alias för företag för dynamiska media](/help/assets/assets-dm/dm-company-alias.png)

1. På sidan **[!UICONTROL Edit Dynamic Media Configuration]** skriver du det namn på kontot för det dynamiska mediaalias som du angav i ditt supportärende tidigare i textfältet **[!UICONTROL Company Alias]**.
1. Välj **[!UICONTROL Save]** i det övre högra hörnet på sidan.
Aliaskontot för företaget Dynamic Media har nu sparats och aktiverats. Alla URL:er och visningsprogrammets inbäddningskod för befintliga och nya resurser återspeglar nu företagets nya aliasnamn.