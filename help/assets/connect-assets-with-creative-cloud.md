---
title: Anslut AEM Assets till Creative Cloud
description: Lär dig konfigurera och ansluta AEM Assets till Creative Cloud. Anslut till ett Creative Cloud-berättigande som tilldelats en annan IMS-organisation för att enkelt använda de senaste Creative Cloud-integreringarna i AEM Assets, inklusive Express och Creative Cloud Libraries.
exl-id: 880200fe-94b3-49de-802c-34283f7c71bc
feature: Collaboration
role: User
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# Anslut AEM Assets till Creative Cloud  {#cross-org-entitlements}

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

Experience Manager Assets kan ansluta till ett Creative Cloud-berättigande som är etablerat i en annan IMS-organisation för att enkelt använda de senaste Creative Cloud-integreringarna i AEM Assets, inklusive Express och Creative Cloud Libraries.

Om era Creative Cloud-produkter och AEM Assets är avsedda för olika IMS-organisationer kan ni ansluta till en annan Creative Cloud-organisation för att kunna genomföra integrerade arbetsflöden mellan de två lösningarna.

## Förutsättningar {#prerequisites}

* Administratörsrättigheter till Experience Manager Assets

* Aktiv behörighet till Creative Cloud för samma användar-ID som används i Creative Cloud och Experience Manager. Tillstånd till personliga och externa ID:n med samma e-postadress behandlas som olika användar-ID:n.

## Ansluta till en ny Creative Cloud-organisation {#connect-to-creative-cloud-org}

Så här ansluter du till en ny Creative Cloud-organisation:

1. Navigera till **[!UICONTROL Settings]** > **[!UICONTROL Creative Cloud]**.

1. Välj den nya Creative Cloud-organisationen med hjälp av listrutan **[!UICONTROL Select new Creative Cloud org ID]**. I listan visas alla organisationer som du har tillgång till. Välj den organisation som har aktiva Creative Cloud-berättiganden.

1. Klicka på **[!UICONTROL Switch orgs]** för att växla till den nya organisationen.

   ![Korsorganisationsberättiganden](assets/cross-org-entitlements.png)

## Begränsningar {#limitations}

* Du kan ansluta AEM Assets till en Creative Cloud-organisation åt gången. Anslutning till flera Creative Cloud-organisationer samtidigt stöds inte.

* Den Creative Cloud-organisation som du ansluter till inom AEM Assets gäller alla användare inom organisationen.
