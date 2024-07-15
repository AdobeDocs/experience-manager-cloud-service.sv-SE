---
title: Associerat innehåll (Assets - innehållsfragment)
description: Förstå hur den associerade innehållsfunktionen för AEM innehållsfragment tillhandahåller anslutningen så att resurser kan användas tillsammans med fragmentet.
exl-id: 8c8ad768-a210-4d34-bb47-2347599bcac9
feature: Content Fragments
role: User
solution: Experience Manager Sites
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# Associerat innehåll{#associated-content}

För innehållsfragment i Adobe Experience Manager (AEM) as a Cloud Service ger den tillhörande innehållsfunktionen (som är tillgänglig i den ursprungliga redigeraren) anslutningen så att resurser kan användas tillsammans med fragmentet. Detta ger flexibilitet genom att [tillhandahåller ett intervall med resurser som du kan komma åt när du använder innehållsfragmentet](/help/assets/content-fragments/content-fragments.md#using-associated-content), samtidigt som det minskar tiden som krävs för att söka efter rätt resurs. Den här funktionen kan användas både för innehållsleverans utan rubrik och för att skapa sidor.

>[!NOTE]
>
>Innehållsfragment är en webbplatsfunktion, men lagras som **Assets**.
>
>Det finns två redigerare för att skapa innehållsfragment. I det här avsnittet beskrivs den ursprungliga redigeraren, som huvudsakligen nås från **Assets**-konsolen.

## Lägga till associerat innehåll {#adding-associated-content}

>[!NOTE]
>
>Det finns olika metoder för att lägga till [visuella resurser (till exempel bilder)](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) till avsnittet och/eller sidan.

För att kunna skapa associationen måste du först [lägga till dina medieresurser i en samling](/help/assets/manage-collections.md). När det är klart kan du:

1. Öppna fragmentet och välj **Associerat innehåll** på sidopanelen.

   ![Associerat innehåll](assets/cfm-assoc-content-01.png)

1. Beroende på om några samlingar redan har associerats eller inte väljer du antingen:

   * **Associera innehåll** - det här är den första associerade samlingen
   * **Associate Collection** - associerade samlingar har redan konfigurerats

1. Välj önskad samling.

   Du kan också lägga till själva fragmentet i den valda samlingen. Detta hjälper till att spåra.

   ![Välj samling](assets/cfm-assoc-content-02.png)

1. Bekräfta (med **Markera**). Samlingen visas som associerad.

   ![Bekräftad association](assets/cfm-assoc-content-03.png)

## Redigera associerat innehåll {#editing-associated-content}

När du har kopplat en samling kan du:

* **Ta bort** associationen.
* **Lägg till Assets** i samlingen.
* Välj en resurs för ytterligare åtgärder.
* Redigera resursen.
