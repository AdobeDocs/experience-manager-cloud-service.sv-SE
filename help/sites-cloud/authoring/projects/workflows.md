---
title: Arbeta med projektarbetsflöden
description: Det finns en mängd olika projektarbetsflöden att välja mellan.
exl-id: a5c9a6df-7def-43f3-b41b-524a4f4211e9
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 10%

---

# Arbeta med projektarbetsflöden {#working-with-project-workflows}

De projektarbetsflöden som är tillgängliga från paketet innehåller följande:

* **Arbetsflöde för projektgodkännande** - Med det här arbetsflödet kan du tilldela innehåll till en användare, granska och sedan godkänna.
* **Begär start** - Ett arbetsflöde som begär en start.
* **Begär landningssida** - Det här arbetsflödet begär en landningssida.
* **Begär e-post** - Arbetsflöde för att begära e-post.
* **DAM Skapa och översätt kopia och DAM Skapa språkkopia** - Skapar översatta binärfiler, metadata och taggar för resurser och mappar.

Beroende på vilken projektmall du väljer finns det vissa arbetsflöden:

|   | **Enkelt projekt** | **Översättningsprojekt** |
|---|:-:|:-:|
| Arbetsflöde för projektgodkännande | x |  |
| Begär start | x |  |
| Begär landningssida | x |  |
| Begär e-post | x | |
| DAM - skapa &amp;språkkopia; |  | x |
| DAM Skapa och översätt &amp;språkkopia; |   | x |

>[!NOTE]
>
>&amp;ast; De här arbetsflödena har inte startats från **Arbetsflöde** i Projekt. Se [Skapa språkkopior för resurser](/help/sites-cloud/administering/translation/managing-projects.md).

Stegen för att starta och slutföra arbetsflöden är desamma oavsett vilket arbetsflöde du väljer. Bara stegen ändras.

Du startar ett arbetsflöde direkt i Projekt (förutom för DAM Create Language Copy eller DAM Create och Translate Language Copy). Information om utestående uppgifter i ett projekt finns i **Uppgifter** platta. Meddelanden om uppgifter som behöver slutföras visas bredvid användarikonen.

Mer information om hur du arbetar med arbetsflöden i AEM finns i:

* [Delta i arbetsflöden](/help/sites-cloud/authoring/workflows/participating.md)
* [Tillämpa arbetsflöden på sidor](/help/sites-cloud/authoring/workflows/applying.md)
* [Konfigurera arbetsflöden](/help/sites-cloud/administering/workflows-administering.md)

I det här avsnittet beskrivs de arbetsflöden som är tillgängliga för projekt.

## Arbetsflöde för projektgodkännande {#project-approval-workflow}

I arbetsflödet för projektgodkännande tilldelar du innehåll till en användare, granskar och godkänner sedan innehållet.

1. I ditt enkla projekt väljer du **`+`** logga in på **Arbetsflöden** platta och markera **Arbetsflöde för projektgodkännande**.
1. Ange en titel och välj vem du vill tilldela den till i grupplistan. Ange en beskrivning, innehållssökväg, uppgiftsprioritet och ett förfallodatum om tillämpligt.

   ![Begär godkännande](/help/sites-cloud/authoring/assets/projects-approval.png)

1. Klicka **Skapa**. Arbetsflödet startar. Uppgiften visas i **Uppgifter** platta.

## Arbetsflödet Begär start {#request-launch-workflow}

Med det här arbetsflödet kan du begära att programmet startas.

1. I det enkla projektet väljer du plustecknet (**+**) i rutan **Arbetsflöden** och väljer **arbetsflödet Begär start**.
1. Ange en rubrik för startprogrammet och ange startkällans sökväg. Du kan också lägga till en beskrivning och ett live-datum, om du vill. Välj Ärv källsidans livedata eller exkludera undersidor beroende på hur du vill att startsidan ska fungera.

   ![Begär start](/help/sites-cloud/authoring/assets/projects-request-launch.png)

1. Klicka **Skapa**. Arbetsflödet startar. Arbetsflödet visas i **Arbetsflöden** lista (klicka på ovaler) **...** på **Arbetsflöden** för att komma åt den här listan).

## Skapa (och översätt) språkkopieringsarbetsflöde för resurser {#create-and-translate-language-copy-workflow-for-assets}

Arbetsflödena **Skapa språkkopia** och **Skapa och översätt språkkopia**[ beskrivs i detalj när du skapar språkkopior för resurser](/help/assets/translate-assets.md).
