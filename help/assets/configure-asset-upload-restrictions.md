---
title: Konfigurera överföringsbegränsningar för resurser
description: Konfigurera Adobe Experience Manager Assets för att begränsa vilken typ av resurser som användare kan överföra baserat på MIME-typen. Det förhindrar oavsiktliga överföringar av oönskade format och skadliga filer.
exl-id: 094c31f3-f2e9-4b44-9995-c76fb78ca458
source-git-commit: 472b670623e77957ff9a366359ebef8c6c0604ae
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 1%

---

# Konfigurera överföringsbegränsningar för resurser {#configure-asset-upload-restrictions}

Du kan konfigurera Adobe Experience Manager Assets för att begränsa vilken typ av resurser som användare kan överföra baserat på MIME-typen.

>[!IMPORTANT]
>
>Som standard tillåter Experience Manager Assets användare att överföra resurser av alla MIME-typer. Du kan dock konfigurera inställningarna så att användarna endast kan överföra filer av särskilda MIME-typer.

## Förutsättningar {#prerequisites-asset-upload-restrictions}

Du måste ha administratörsbehörighet för att konfigurera överföringsbegränsningar för resurser.

## Använd begränsningar för överföringar av resurser {#apply-restrictions-asset-uploadsssssss}

Konfigurera [!DNL Experience Manager] för att begränsa användare till att överföra filer av särskilda MIME-typer:

1. Navigera till **[!UICONTROL Tools > Assets > Assets Configurations]**.

1. Klicka på **[!UICONTROL Upload Restrictions]**.

1. Klicka **[!UICONTROL Add]** för att definiera tillåtna MIME-typer.

1. Ange MIME-typen i textrutan. Du kan klicka **[!UICONTROL Add]** igen för att ange fler tillåtna MIME-typer. Du kan också klicka ![ta bort ikon](assets/delete-icon.svg) om du vill ta bort en MIME-typ från listan.

1. Klicka på **[!UICONTROL Save]**.

**Exempel 1: Tillåt överföring av alla bilder och PDF-filer till Experience Manager Assets**

Om du vill tillåta överföring av bilder i alla format och PDF till Experience Manager Assets gör du följande inställningar:

![Begränsningar för överföring av tillgångar](assets/asset-upload-restrictions.png)

`image/*` som MIME-typen tillåter överföring av bilder i alla format. `application/pdf` som MIME-typen tillåter överföring av PDF-filer till Experience Manager Assets.

**Exempel 2: Tillåt överföring av specifika bildformat till Experience Manager Assets**

Om du vill lägga till särskilda bildformat i de tillåtna MIME-typerna och begränsa överföringen av alla andra resursformat, gör du följande inställningar:

![Resursbegränsningar](assets/asset-restrictions.png)

Baserat på de inställningar som avbildas i bilden kan du överföra bilder i formaten .JPG, .PNG och .GIF till Experience Manager Assets.
