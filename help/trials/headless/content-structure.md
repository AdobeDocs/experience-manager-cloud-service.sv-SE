---
title: Skapa innehållsstrukturen för din app
description: Lär dig hur du skapar en struktur som fungerar som grund för allt ditt headless-innehåll med AEM Content Fragment-modeller.
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
source-git-commit: 4269bc9650f197ae33fcef40a847f8b200097e45
workflow-type: tm+mt
source-wordcount: '1104'
ht-degree: 0%

---

# Skapa innehållsstrukturen för din app {#content-structure}

Med Content Fragments kan du utforma, skapa, strukturera och publicera sidoberoende innehåll. Med hjälp av dem kan ni förbereda innehåll som är klart att användas på flera platser och i flera kanaler, vilket är idealiskt för headless-leverans. Modeller för innehållsfragment används för att definiera innehållets struktur och är det första du behöver skapa för att kunna hantera ditt headless-innehåll.

För att du ska få en bättre förståelse för hur detta görs går den här modulen AEM igenom processen med en snabb, interaktiv genomgång där du först skapar modellen och sedan lägger till dess struktur. Det här dokumentet utgör ett komplement till produktdemon, som omfattar samma steg och länkar till ytterligare resurser där så är lämpligt.

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="Skapa innehållsstrukturen för din app"
>abstract="När du följer vår serie med interaktiva guider lär du dig att skapa strukturen (även kallad innehållsfragmentmodellen) som fungerar som grund för allt ditt headless-innehåll."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide"
>title="Starta modellredigeraren"
>abstract="Skapandet av en modell för innehållsfragment börjar med att skapa ett modellobjekt i modelladministrationsarbetsflödet och sedan lägga till strukturelement i den med hjälp av modellredigeraren för innehållsfragment.<br><br>Klicka nedan för att starta funktionen på en ny flik och följ det här utbildningsdokumentet för att skapa din första innehållsfragmentmodell."
>additional-url="https://video.tv.adobe.com/v/328618" text="Platshållare för inledande video"

## Modellkonsolen för innehållsfragment {#content-fragment-model-console}

Du startar på modellkonsolen för innehållsfragment. Modellkonsolen för innehållsfragment kan ses som ditt modellbibliotek. Du använder konsolen för att skapa nya modeller och hantera befintliga modeller. Konsolen börjar tom, så vi skapar en ny modell!

![Modellkonsolen för innehållsfragment](assets/content-structure/content-fragment-model-console.png)

Om du själv vill navigera till modellkonsolen för innehållsfragment utanför vägledningen i appen visas den med ikonen Adobe längst upp till vänster på sidan. Då öppnas den globala navigeringen för AEM. Här väljer du **verktyg** och sedan **Allmänt** -> **Modeller för innehållsfragment**.

>[!TIP]
>
>Om du vill veta mer om navigering i AEM kan du läsa [Avsnittet Ytterligare resurser](#additional-resources) för mer information om AEM grundläggande hantering.

## Skapa en modell {#create-model}

När du är i modellkonsolen för innehållsfragment kan du skapa en ny modell som representerar ditt eget innehåll utan rubrik.

1. I modellkonsolen för innehållsfragment klickar du på **Skapa** längst upp till höger på skärmen för att börja skapa en modell för innehållsfragment.

1. Guiden Skapa modell startar, som vägleder dig genom att skapa en modell för innehållsfragment.

   ![Modellguide för innehållsfragment](assets/content-structure/model-wizard.png)

   Ange den obligatoriska informationen.

   * **Modelltitel** - Detta är en kort beskrivning av modellen och anger vanligtvis dess syfte.
   * **Aktivera modell** - Det här alternativet är markerat som standard och måste markeras för att det ska gå att skapa innehållsfragment senare baserat på den här modellen.

   Du kan också lägga till en längre **Beskrivning** till modellen **Taggar** för att kategorisera den och särskilja den för dina användare senare i modellkonsolen för innehållsfragment.

   >[!TIP]
   >
   >Om du är intresserad av hur taggar kan ordna ditt innehåll kan du läsa [Avsnittet Ytterligare resurser](#additional-resources) i det här dokumentet om du vill ha mer information om taggning i AEM.

1. När de obligatoriska fälten har fyllts i klickar du på **Skapa** längst upp till vänster för att skapa modellen.

1. The **Lyckades** bekräftar att modellen skapades.

   ![Dialogrutan Slutfört för att skapa en ny modell för innehållsfragment](assets/content-structure/success.png)

1. Innan du kan använda modellen måste du också definiera strukturen för dess data. Klicka **Öppna** i dialogrutan för att öppna den och fortsätta att definiera modellen.

## Lägg till fält i modellen {#configure-model}

Modellen för innehållsfragment är i princip ett schema för dina innehållsfragment. Det definierar alltså vilka fält/datatyper som modellen innehåller.

![Modellredigeraren för innehållsfragment](assets/content-structure/model-editor.png)

Med modellredigeraren för innehållsfragment kan du definiera fält för modellen för innehållsfragment med hjälp av ett dra och släpp-gränssnitt.

1. Dra ett fält från **Datatyper** till höger på skärmen och släpp den i modellen för innehållsfragment. Det finns flera datatyper att välja mellan, till exempel enkelradig text, flerradig text, siffror och referenser till andra fragment.

   ![Lägg till en datatyp](assets/content-structure/drop-fields.png)

   >[!TIP]
   >
   >Om du vill ha mer information om de datatyper som är tillgängliga för dig kan du läsa [Avsnittet Ytterligare resurser](#additional-resources) av det här dokumentet för detaljerad dokumentation om Content Fragment-modeller.

1. När en datatyp har placerats ut **Datatyper** kolumnen ändras automatiskt till **Egenskaper** där du kan definiera information om den datatyp du just placerat.

   ![Fliken Egenskaper för datafältet](assets/content-structure/data-type-properties.png)

   Modellens egenskaper kan omfatta fältets namn, fälttyp, fältets längd, om det är obligatoriskt, osv.

1. Använd **Egenskaper** för den markerade datatypen för att definiera egenskaper som standardvärde, maxlängd, om det är ett obligatoriskt fält, osv.

   >[!TIP]
   >
   >Om du vill ha mer information om de egenskaper som är tillgängliga för dig kan du läsa [Avsnittet Ytterligare resurser](#additional-resources) av det här dokumentet för detaljerad dokumentation om Content Fragment-modeller.

1. När du har lagt till alla fält som behövs för modellen för innehållsfragment klickar du på **Spara** längst upp till höger i fönstret.

1. Modellen sparas och du återgår till modellkonsolen för innehållsfragment där du kan lägga till fler modeller.

![Modulen är klar](assets/content-structure/content-fragment-model-console-populated.png)

## Du har lärt dig att skapa en innehållsfragmentmodell {#conclusion}

I den här modulen lärde du dig att skapa en modell för innehållsfragment som representerar strukturen för dina headless-data. Först skapade du modellen och fyllde den sedan med datatyper och relaterade egenskaper, vilket definierar ett schema för det headfria innehållet.

Nu när du har en egen modell för innehållsfragment kan du använda modellen för att skapa innehållsfragment. Modulen [Skapa nytt innehåll](create-content.md) information om hur du använder den nya Content Fragment-modellen för att skapa headless-innehåll.

Du kan gå tillbaka till startskärmen för testversionen genom att klicka på **Lösningar** knappen längst upp till höger i navigeringsfältet och markera **Experience Manager**.

![Navigera hem](assets/content-structure/home.png)

## Ytterligare resurser {#additional-resources}

Mer information om innehållsfragment och AEM finns i den här extra dokumentationen.

* [Grundläggande hantering](/help/sites-cloud/authoring/getting-started/basic-handling.md) - Dokumentation om hur du navigerar och använder AEM för nya användare
* [Använda taggar](/help/sites-cloud/authoring/features/tags.md) - Dokumentation om hur du använder taggar i AEM för att ordna innehåll
* [Innehållsfragment](/help/assets/content-fragments/content-fragments.md) - Översikt över innehållsfragment och länkar till fullständig dokumentation om innehållsfragment
* [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md) - Fullständig dokumentation om Content Fragment-modeller
* [Modeller för innehållsfragment - datatyper](/help/assets/content-fragments/content-fragments-models.md#data-types) - Information om olika datatyper som är tillgängliga för Content Fragment-modeller
* [Modeller för innehållsfragment - egenskaper](/help/assets/content-fragments/content-fragments-models.md#data-types) - Information om de olika egenskaper som är tillgängliga för datatyperna Content Fragment-modeller
