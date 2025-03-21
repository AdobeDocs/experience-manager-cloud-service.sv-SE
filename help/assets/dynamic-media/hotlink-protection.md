---
title: Aktivera hotlink-skydd i Dynamic Media
description: Lär dig hur du aktiverar hotlink-skydd i Dynamic Media.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 0198b3a3-173e-46ca-a845-3f58f8eab769
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# Aktivera hotlink-skydd i Dynamic Media {#activating-hotlink-protection-in-dynamic-media}

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

Aktiv länkning är när en tredjepartswebbplats använder HTML-kod för att visa en bild från din webbplats. De använder din bandbredd varje gång bilden efterfrågas eftersom besökarens webbläsare öppnar den direkt från servern. Hotlink *protection* är en metod som förhindrar att andra webbplatser direkt länkar till bilder, CSS eller JavaScript på dina webbsidor. Den här typen av skydd minskar onödig bandbreddsanvändning under ditt Dynamic Media-konto.

[Adobe kundsupport](https://experienceleague.adobe.com/?support-solution=Experience+Manager#home) kan konfigurera ett referensfilter på CDN-nivå. På så sätt säkerställs att Dynamic Media-innehåll endast kan användas på webbplatser i din lista över tillåtna webbplatser för domänen.

>[!NOTE]
>
>Den här funktionen kräver att du använder det färdiga CDN som medföljer Adobe Experience Manager Dynamic Media. Andra anpassade CDN stöds inte med den här funktionen. För att aktivera aktivering av hot link-skydd måste en administratör skapa en supportbiljett för att begära konfigurationsändringen av ditt Dynamic Media-konto. Det kostar inget mer att aktivera skydd av aktiva länkar.
