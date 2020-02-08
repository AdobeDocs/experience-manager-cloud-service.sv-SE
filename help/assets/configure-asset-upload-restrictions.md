---
title: Konfigurera begränsningar för överföring av resurser
description: Lär dig hur du konfigurerar Adobe Experience Manager-resurser (AEM) för att begränsa vilken typ av resurser (filer) som användare kan överföra.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Konfigurera begränsningar för överföring av resurser {#configuring-asset-upload-restrictions}

Du kan konfigurera Adobe Experience Manager-resurser (AEM) för att begränsa vilken typ av resurser (filer) som användare kan överföra. Den här funktionen hjälper dig att eliminera möjligheten för användare att överföra resurser i ett oönskat format eller överföra skadliga filer. Med `Day CQ DAM Asset Upload Restriction` tjänsten kan du styra vilken typ av filer som användare kan överföra. Som standard tillåter AEM Resurser användare att överföra resurser av alla MIME-typer. Du kan dock konfigurera tjänsten så att den begränsar användare till att överföra filer av specifika MIME-typer.

1. Öppna Configuration Manager-webbkonsolen. Åtkomst `https://[aem_server]:[port]/system/console/configMgr`.
1. Öppna tjänsten **[!UICONTROL Dag CQ DAM Asset Upload Restriction]** i redigeringsläget. Som standard är alternativet **Tillåt alla MIME** markerat, vilket gör att användare kan överföra filer av alla MIME-typer.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Om du vill begränsa användare till att överföra filer av vissa MIME-typer avmarkerar du **[!UICONTROL alternativet Tillåt alla MIME]** och anger tillåtna MIME-typer i fälten **[!UICONTROL Tillåtna MIME-filer (regex)]** med reguljära uttryck.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Klicka/tryck på **[!UICONTROL Spara]** för att spara ändringarna. Om du anger MIME-strängar för tillåtna MIME-typer misslyckas överföringen för alla resurser med MIME-typ som inte matchar de konfigurerade MIME-strängarna i dessa fält.

