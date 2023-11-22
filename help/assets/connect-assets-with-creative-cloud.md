---
title: Anslut AEM Assets till Creative Cloud
description: Lär dig hur du konfigurerar och ansluter AEM Assets till Creative Cloud. Anslut till ett berättigande för Creative Cloud som har tilldelats en annan IMS-organisation för att enkelt kunna använda de senaste Creative Cloud-integreringarna i AEM Assets, inklusive Express och Creative Cloud Libraries.
exl-id: 880200fe-94b3-49de-802c-34283f7c71bc
source-git-commit: 237b4a8e01af74dbaac0ba1715b5fa95c931be7c
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 1%

---

# Anslut AEM Assets till Creative Cloud  {#cross-org-entitlements}

Experience Manager Assets kan ansluta till ett berättigande för Creative Cloud som är etablerat i en annan IMS-organisation för att enkelt kunna använda de senaste Creative Cloud-integreringarna i AEM Assets, inklusive Express och Creative Cloud Libraries.

Om dina Creative Cloud-produkter och AEM Assets har tilldelats separata IMS-organisationer kan du ansluta till en annan Creative Cloud-organisation för att kunna köra integrerade arbetsflöden mellan de två lösningarna.

## Förutsättningar {#prerequisites}

* Administratörsrättigheter till Experience Manager Assets

* Aktivt berättigande till Creative Cloud för samma användar-ID som används i Creative Cloud och Experience Manager. Tillstånd till personliga och externa ID:n med samma e-postadress behandlas som olika användar-ID:n.

## Ansluta till en ny Creative Cloud-organisation {#connect-to-creative-cloud-org}

Så här ansluter du till en ny Creative Cloud-organisation:

1. Navigera till **[!UICONTROL Settings]** > **[!UICONTROL Creative Cloud]**.

1. Markera den nya Creative Cloud-organisationen med **[!UICONTROL Select new Creative Cloud org ID]** listruta. I listan visas alla organisationer som du har tillgång till. Markera organisationen med aktiva Creative Cloud-berättiganden.

1. Klicka **[!UICONTROL Switch orgs]** för att byta till den nya organisationen.

   ![Korsorganisation](assets/cross-org-entitlements.png)

## Begränsningar {#limitations}

* Du kan ansluta AEM Assets till en Creative Cloud-organisation åt gången. Anslutning till flera Creative Cloud-organisationer samtidigt stöds inte.

* Den Creative Cloud-organisation som du ansluter till inom AEM Assets gäller alla användare inom din organisation.
