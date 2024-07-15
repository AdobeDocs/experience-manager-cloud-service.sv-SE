---
title: Förhandsgranska 3D-resurser
description: Lär dig hur du förhandsgranskar 3D-resurser i Experience Manager.
contentOwner: Rick Brough
feature: 3D Assets
role: User
exl-id: e873bd25-f841-4063-824f-7e48f40bb678
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# Förhandsgranska 3D-resurser i Adobe Experience Manager{#previewing-3d-assets}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/previewing-3d-assets.html?lang=en) |
| AEM as a Cloud Service | Den här artikeln |

Experience Manager Assets hanterar, förhandsvisar och levererar 3D-resurser.

Du kan förhandsgranska 3D-resurser med de automatiskt genererade miniatyrbildsrenderingarna eller det interaktiva 3D-visningsprogrammet. Det interaktiva 3D-visningsprogrammet finns på sidan med resursinformation i Experience Manager. Visningsprogrammet innehåller bland annat en samling interaktiva kamerakontroller som gör att du kan rotera, zooma och panorera runt 3D-scenen.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/dynamic-media/assets-3d.md). -->

## Format som stöds för miniatyrförhandsvisning i Experience Manager{#supported-thumbnail-previewing-assets}

Experience Manager genererar miniatyrbilder för följande filformat som standard:

| 3D-filtillägg | Filformat | MIME-typ | Anteckningar |
|---|---|---|---|
| GLB | Binär GL-överföring | model/gltf-binary |  |
| FBX | Autodesk FBX | application/octet-stream |  |
| OBJ | WaveFront 3D-objektfil | application/x-tgif |  |
| 3DS | 3D Studio Model | application/x-3ds |  |
| USDz | Universal Scene Description | model/vnd.usdz+zip |  |

## Format som stöds för interaktiv 3D-förhandsgranskning i Experience Manager{#supported-3d-previewing-assets}

Experience Manager har stöd för interaktiv 3D-förhandsgranskning i följande filformat:

| 3D-filtillägg | Filformat | MIME-typ | Anteckningar |
|---|---|---|---|
| GLB | Binär GL-överföring | model/gltf-binary |  |
| GLTF | GL-överföringsformat | model/gltf+json | Se **Anteckning** nedan. |
| OBJ | WaveFront 3D-objektfil | application/x-tgif |  |
| STL | Stereolithografi | application/vnd.ms-pki.stl |  |


>[!NOTE]
>
>Om material inte återges i förhandsgranskning av en gLTF-modell kontrollerar du att de har rätt namn och finns i en `textures`-mapp i samma rotmapp som modellen, som i följande:

    Resurs (mapp)
    model.gltf
    model.bin
    textures (mapp)
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## Prestandaöverväganden när du förhandsgranskar 3D-resurser i Experience Manager{#performance-3d-previewing-assets}

Hur lång tid det tar att öppna en 3D-resurs på visningssidan för resursinformation beror på flera faktorer, till exempel bandbredd, bildkomplexitet och fördröjningar för servern.

Dessutom är funktioner i klientdatorn - som en arbetsstation, bärbar dator eller mobil touchenhet - också viktiga att tänka på när du manipulerar kameran interaktivt. Ett relativt kraftfullt system med bra grafikfunktioner kan göra den interaktiva 3D-visningen smidigare och mer gynnsam.

**Så här förhandsgranskar du 3D-resurser i Experience Manager:**

1. Se till att du har överfört 3D-resurser till Experience Manager.
Se [Format som stöds för 3D-förhandsgranskning](#supported-3d-previewing-assets) och [Överför resurser](/help/assets/manage-digital-assets.md#uploading-assets).
1. Gå till **[!UICONTROL Assets]** > **[!UICONTROL Files]** från Experience Manager på sidan **[!UICONTROL Navigation]**.

   ![Navigeringssida](/help/assets/dynamic-media/assets/navigation-assets.png)

1. I den nedrullningsbara listan Visa i det övre högra hörnet av sidan väljer du **[!UICONTROL Card View]** och navigerar sedan till en 3D-resurs som du vill förhandsgranska.

   ![Val av 3D-kort](/help/assets/dynamic-media/assets/3d-card-select.png)
   _I kortvyn väljer du kortet för den 3D-resurs som du vill förhandsgranska._

1. Välj kortet för 3D-resursen.

   ![Interaktiv 3D-förhandsvisning](/help/assets/dynamic-media/assets/3d-preview.png)
   _Interaktiv förhandsgranskning av en 3D-resurs på sidan med resursinfo._
1. Gör något av följande på sidan med resursinformationsvyn för 3D-resursen:

   | Visa | Beskrivning | Musåtgärd | Åtgärd på pekskärmen |
   | --- | --- | --- | --- |
   | **Vrid kameran** | Ordna vyn runt 3D-scenen och objekt. | Vänsterklicka och dra. | Tryck med ett finger och dra. |
   | **Panorera kameran** | Panorera vyn åt vänster, åt höger, uppåt eller nedåt. | Högerklicka och dra. | Tryck med två fingrar och dra. |
   | **Zooma kameran** | Flytta in och ut från områden i 3D-scenen. | Rullningshjul. | Nyp med två fingrar. |
   | **Ange kameran igen** | Centrera kameran igen till en punkt på ett objekt i 3D-scenen. | Dubbelklicka. | Dubbelmarkera. |
   | **Återställ** | I närheten av det nedre högra hörnet av sidan väljer du ikonen Återställ om du vill återställa målpunkten till mitten av 3D-resursen. Återställ flyttar också kameran närmare eller längre bort för att visa resursen i dess helhet och med en rimlig visningsstorlek. |   |   |
   | **Helskärmsläge** | Om du vill aktivera helskärmsläget väljer du Helskärmsikonen längst ned till höger på sidan. |   |   |

1. När du är klar väljer du **[!UICONTROL Close]** i sidans övre högra hörn.
