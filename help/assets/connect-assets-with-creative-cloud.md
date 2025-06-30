---
title: Anslut AEM Assets till Creative Cloud
description: Lär dig konfigurera och ansluta AEM Assets till Creative Cloud. Anslut till ett Creative Cloud-berättigande som tilldelats en annan IMS-organisation för att enkelt använda de senaste Creative Cloud-integreringarna i AEM Assets, inklusive Express och Creative Cloud Libraries.
exl-id: 880200fe-94b3-49de-802c-34283f7c71bc
feature: Collaboration
role: User
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Anslut AEM Assets till Creative Cloud  {#cross-org-entitlements}

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
