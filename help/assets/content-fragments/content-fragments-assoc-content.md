---
title: Associerat innehåll (resurser - innehållsfragment)
description: Förstå hur AEM tillhörande innehållsfunktion tillhandahåller anslutningen så att resurser kan användas tillsammans med fragmentet.
exl-id: 8c8ad768-a210-4d34-bb47-2347599bcac9
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 4%

---

# Associerat innehåll{#associated-content}

Funktionen AEM associerat innehåll tillhandahåller anslutningen så att resurser kan användas tillsammans med fragmentet när det läggs till på en innehållssida. Detta ger flexibilitet vid leverans av headless-innehåll genom att [tillhandahålla en mängd resurser som du kan komma åt när du använder innehållsfragmentet på en sida,](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content) samtidigt som det går snabbare att söka efter rätt resurs.

## Lägga till associerat innehåll {#adding-associated-content}

>[!NOTE]
>
>Det finns olika metoder att lägga till [visuella resurser (till exempel bilder)](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) till fragmentet och/eller sidan.

För att kunna skapa associationen måste du först [lägga till mediefiler i en samling](/help/assets/manage-collections.md). När det är klart kan du:

1. Öppna fragmentet och välj **Associerat innehåll** på sidopanelen.

   ![Associerat innehåll](assets/cfm-assoc-content-01.png)

1. Beroende på om några samlingar redan har associerats eller inte väljer du antingen:

   * **Associera innehåll** - det här är den första associerade samlingen
   * **Associera samling** - associerade samlingar har redan konfigurerats

1. Välj önskad samling.

   Du kan också lägga till själva fragmentet i den valda samlingen; detta hjälper till att spåra.

   ![Välj samling](assets/cfm-assoc-content-02.png)

1. Bekräfta (med **Välj**). Samlingen visas som associerad.

   ![cfm-6420-05](assets/cfm-assoc-content-03.png)

## Redigera associerat innehåll {#editing-associated-content}

När du har kopplat en samling kan du:

* **Ta bort** associationen.
* **Lägg till resurser** till samlingen.
* Välj en resurs för ytterligare åtgärder.
* Redigera resursen.
