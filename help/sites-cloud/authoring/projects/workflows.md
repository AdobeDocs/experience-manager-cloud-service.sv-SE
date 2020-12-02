---
title: Arbeta med projektarbetsflöden
description: Det finns en mängd olika projektarbetsflöden att välja mellan.
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 12%

---


# Arbeta med projektarbetsflöden {#working-with-project-workflows}

De projektarbetsflöden som är tillgängliga från paketet innehåller följande:

* **Arbetsflöde**  för projektgodkännande - Med det här arbetsflödet kan du tilldela innehåll till en användare, granska och sedan godkänna.
* **Begär start**  - Ett arbetsflöde som begär start.
* **Begär landningssida**  - Den här arbetsflödet begär en landningssida.
* **Begär e-post**  - Arbetsflöde för att begära e-post.
* **DAM Skapa och översätt kopia och DAM Skapa språkkopia**  - Skapar översatta binärfiler, metadata och taggar för resurser och mappar.

Beroende på vilken projektmall du väljer finns det vissa arbetsflöden:

|  | **Enkelt projekt** | **Medieprojekt** | **Översättningsprojekt** |
|---|:-:|:-:|:-:|
| Begär kopia |  | x |  |
| Fotofotografering |  | x |  |
| Projektgodkännande | x |  |  |
| Begär start | x |  |  |
| Begär landningssida | x |  |  |
| Begär e-post | x |  |  |
| DAM - skapa språkkopia&amp;ast; |  |  | x |
| DAM Skapa och översätt språkkopia&amp;ast; |  |  | x |

>[!NOTE]
>
>&amp;ast; Dessa arbetsflöden startas inte från **arbetsflödets**-panel i Projekt. Se Skapa språkkopior för resurser.
<!--
>&ast; These workflows are not started from the **Workflow** tile in Projects. See [Creating Language Copies for Assets.](/help/sites-administering/tc-manage.md)
-->

Stegen för att starta och slutföra arbetsflöden är desamma oavsett vilket arbetsflöde du väljer. Bara stegen ändras.

Du startar ett arbetsflöde direkt i Projekt (förutom för DAM Create Language Copy eller DAM Create och Translate Language Copy). Information om väntande uppgifter i ett projekt visas i rutan **Uppgifter**. Meddelanden om uppgifter som behöver slutföras visas bredvid användarikonen.

Mer information om hur du arbetar med arbetsflöden i AEM finns i:

* [Delta i arbetsflöden](/help/sites-cloud/authoring/workflows/participating.md)
* [Tillämpa arbetsflöden på sidor](/help/sites-cloud/authoring/workflows/applying.md)
* Konfigurera arbetsflöden <!--* [Configuring workflows](/help/sites-administering/workflows.md)-->

I det här avsnittet beskrivs de arbetsflöden som är tillgängliga för projekt.

## Arbetsflödet Begär kopia {#request-copy-workflow}

Med det här arbetsflödet kan du begära ett manuskript från en användare och sedan godkänna det. Så här startar du arbetsflödet för begärandekopia:

1. I medieprojektet väljer du plustecknet (**+**) i rutan **Arbetsflöden** och väljer **arbetsflödet Begär kopiering**.
1. Ange en titel och en kort sammanfattning av vad du begär. Ange ett målordsantal, uppgiftsprioritet och ett förfallodatum om tillämpligt.

   ![Arbetsflödet Begär kopia](/help/sites-cloud/authoring/assets/projects-request-copy.png)

1. Klicka på **Skapa**. Arbetsflödet startar. Aktiviteten visas i rutan **Aktiviteter**.

   ![Begärankopia har lagts till](/help/sites-cloud/authoring/assets/projects-request-copy-add.png)

## Arbetsflöde för projektgodkännande {#project-approval-workflow}

I arbetsflödet för projektgodkännande tilldelar du innehåll till en användare, granskar och godkänner sedan innehållet.

1. I ditt enkla projekt väljer du **`+`**-tecknet i rutan **Arbetsflöden** och väljer **Arbetsflöde för projektgodkännande**.
1. Ange en titel och välj vem du vill tilldela den till i grupplistan. Ange en beskrivning, innehållssökväg, uppgiftsprioritet och ett förfallodatum om tillämpligt.

   ![Begär godkännande](/help/sites-cloud/authoring/assets/projects-approval.png)

1. Klicka på **Skapa**. Arbetsflödet startar. Aktiviteten visas i rutan **Aktiviteter**.

   ![Godkännande av begäran har lagts till](/help/sites-cloud/authoring/assets/projects-approval-add.png)

## Begär startarbetsflöde {#request-launch-workflow}

Med det här arbetsflödet kan du begära att programmet startas.

1. I det enkla projektet väljer du plustecknet (**+**) i rutan **Arbetsflöden** och väljer **arbetsflödet Begär start**.
1. Ange en rubrik för startprogrammet och ange startkällans sökväg. Du kan också lägga till en beskrivning och ett live-datum, om du vill. Välj Ärv källsidans livedata eller exkludera undersidor beroende på hur du vill att startsidan ska fungera.

   ![Begär start](/help/sites-cloud/authoring/assets/projects-request-launch.png)

1. Klicka på **Skapa**. Arbetsflödet startar. Arbetsflödet visas i listan **Arbetsflöden** (klicka på ellipser **..).** på panelen **Arbetsflöden** för att komma åt den här listan).

## Skapa (och översätt) språkkopieringsarbetsflöde för resurser {#create-and-translate-language-copy-workflow-for-assets}

Arbetsflödena **Skapa språkkopia** och **Skapa och översätt språkkopia** beskrivs i detalj när du skapar språkkopior för resurser.
