---
title: Associerat innehåll
description: Förstå hur den associerade innehållsfunktionen för innehållsfragment skapar anslutningen för resurser som (valfritt) ska användas med fragmentet, vilket ger ytterligare flexibilitet vid både sidredigering och leverans av rubrikfritt innehåll.
feature: Content Fragments
role: User
exl-id: eb524872-1403-42d1-b735-eaab382cf313
source-git-commit: 944665bc7cac1f00811187a508a18800c3d73f2a
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 4%

---

# Associerat innehåll{#associated-content}

Funktionen AEM associerat innehåll tillhandahåller anslutningen så att resurser kan användas med fragmentet när det läggs till på en innehållssida av [tillhandahålla en mängd resurser som du kan komma åt när du använder innehållsfragmentet på en sida,](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content) samtidigt som det går snabbare att söka efter rätt resurs. Detta ger också flexibilitet för leverans av headless-material.

## Lägga till associerat innehåll {#adding-associated-content}

>[!NOTE]
>
>Det finns olika metoder att lägga till [visuella resurser (t.ex. bilder)](/help/sites-cloud/administering/content-fragments/content-fragments.md#fragments-with-visual-assets) till fragmentet och/eller sidan.

För att kunna skapa associationen måste du först [lägga till mediefiler i en samling](/help/assets/manage-collections.md). När det är klart kan du:

1. Öppna fragmentet och välj **Associerat innehåll** på sidopanelen.

   ![Associerat innehåll](assets/cfm-assoc-content-01.png)

1. Beroende på om några samlingar redan har associerats eller inte väljer du antingen:

   * **Associera innehåll** - det här blir den första associerade samlingen
   * **Associera samling** - associerade samlingar har redan konfigurerats

1. Välj önskad samling.

   Du kan också lägga till själva fragmentet i den valda samlingen; detta hjälper till att spåra.

   ![Välj samling](assets/cfm-assoc-content-02.png)

1. Bekräfta (med **Välj**). Samlingen listas som associerad.

   ![cfm-6420-05](assets/cfm-assoc-content-03.png)

## Redigera associerat innehåll {#editing-associated-content}

När du har kopplat en samling kan du:

* **Ta bort** associationen.
* **Lägg till resurser** till samlingen.
* Välj en resurs för ytterligare åtgärder.
* Redigera resursen.
