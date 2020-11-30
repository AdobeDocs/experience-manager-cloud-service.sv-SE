---
title: Förhandsgranska 3D-resurser
description: Lär dig hur du förhandsgranskar 3D-resurser
translation-type: tm+mt
source-git-commit: d84a6692f2d0aae496bd2bd98ac99c2663f3fe52
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 4%

---


# Förhandsgranska 3D-resurser i AEM{#previewing-3d-assets}

Adobe Experience Manager stöder överföring, leverans och interaktiv förhandsgranskning av 3D-resurser som en del av utvecklingsprocessen.

Det interaktiva 3D-visningsprogrammet är tillgängligt från sidan med resursinformation i AEM. Visningsprogrammet innehåller bland annat en samling interaktiva kamerakontroller som du kan använda för att rotera, zooma och panorera 3D-resursen.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/dynamic-media/assets-3d.md). -->

## Format som stöds för 3D-förhandsgranskning i AEM{#supported-3d-previewing-assets}

Interaktiv 3D-förhandsvisning i AEM har stöd för följande filformat:

| 3D-filtillägg | Filformat | MIME-typ | Anteckningar |
|---|---|---|---|
| GLB | Binär GL-överföring | model/gltf-binary |  |
| GLTF | GL-överföringsformat | model/gltf+json | Se **anmärkningen** nedan. |
| OBJ | WaveFront 3D-objektfil | application/x-tgif |  |
| STL | Stereolitografi | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | Stöd endast för förtäring. förhandsgranskning är inte tillgänglig. |
| USDZ | Zip-arkiv för universell scenbeskrivning | model/vnd.usdz+zip | Stöd endast för förtäring. förhandsgranskning är inte tillgänglig. |

**Obs**: Om materialet inte återges i förhandsgranskningen av en gLTF-modell måste du se till att de har rätt namn och finns i en `textures` mapp i samma rotmapp som modellen, som i följande:

    Resurs (mapp)
    modell.
    gltfmodel.
    bintextures (mapp)
    material_0_baseColor.
    jpegmaterial_0_normal.jpeg

## Prestandaöverväganden när du förhandsgranskar 3D-resurser i AEM{#performance-3d-previewing-assets}

Hur lång tid det tar att öppna en 3D-resurs på visningssidan för resursinformation beror på flera faktorer, till exempel bandbredd, bildkomplexitet och fördröjningar för servern.

Dessutom är funktioner i klientdatorn - t.ex. en arbetsstation, bärbar dator eller en mobil touchenhet - också viktiga att tänka på när du manipulerar kameran interaktivt. Ett relativt kraftfullt system med bra grafikfunktioner kan göra den interaktiva 3D-visningen smidigare och mer gynnsam.

**Förhandsgranska 3D-resurser i AEM**

1. Se till att du har överfört 3D-resurser till AEM.
See [Supported formats for 3D preview](#supported-3d-previewing-assets) and [Uploading assets](/help/assets/manage-digital-assets.md#uploading-assets).
1. Tryck på AEM på **[!UICONTROL Navigation]** sidan **[!UICONTROL Assets > Files]**.

   ![Navigeringssida](/help/assets/dynamic-media/assets/navigation-assets.png)

1. I närheten av det övre högra hörnet på sidan trycker du på **[!UICONTROL Card View]** i listrutan Visa och navigerar sedan till en 3D-resurs som du vill förhandsgranska.

   ![Välj 3D-kort](/help/assets/dynamic-media/assets/3d-card-select.png)
   _I kortvyn: tryck på kortet för den 3D-resurs som du vill förhandsgranska._

1. Tryck på kortet för 3D-resursen för att öppna den på sidan med vyn för resursinformation.

   ![Interaktiv förhandsvisning av 3D](/help/assets/dynamic-media/assets/3d-preview.png)
   _Interaktiv förhandsgranskning av en 3D-resurs på sidan med resursinformationsvyn._
1. Gör något av följande på sidan med resursinformationsvyn för 3D-resursen:
   * **Vrid kameran**- Du kan rotera vyn runt 3D-scenen och objekten.
      * _Mus_: Vänsterklicka och dra.
      * _Pekskärm_: Tryck med ett finger och dra.
   * **Panorera kameran**- Panorera åt vänster, åt höger, uppåt eller nedåt.
      * _Mus_: Högerklicka och dra.
      * _Pekskärm_: Tryck med två fingrar och dra.
   * **Zooma kameran**- Zooma kameran för att flytta in i och ut från områden i 3D-scenen.
      * _Mus_: Rullningshjul.
      * _Pekskärm_: Nyp med två fingrar.
   * **Centrera kameran** igen - Centrera kameran igen och placera den vid en punkt på ett objekt i 3D-scenen.
      * _Mus_: Dubbelklicka.
      * _Pekskärm_: Dubbeltryck.
   * **Återställ**- I närheten av det nedre högra hörnet av sidan trycker du på ikonen Återställ för att återställa vymålpunkten till mitten av 3D-resursen. Återställ flyttar också kameran närmare eller längre bort för att visa resursen i dess helhet och med en rimlig visningsstorlek.
   * **Helskärmsläge**- Tryck på ikonen Helskärm i det nedre högra hörnet av sidan för att öppna helskärmsläget.

1. When you are finished, near the upper-right corner of the page, tap **[!UICONTROL Close]**.
