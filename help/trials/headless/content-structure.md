---
title: Skapa innehållsstrukturen för din app
description: Lär dig hur du skapar en struktur som fungerar som grund för allt ditt headless-innehåll med AEM Content Fragment-modeller.
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
source-git-commit: bcab02cbd84955ecdc239d4166ae38e5f79b3264
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Skapa innehållsstrukturen för din app {#content-structure}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="Skapa innehållsstrukturen för din app"
>abstract="När du följer den här serien med interaktiva guider lär du dig att skapa en struktur (som kallas Content Fragment-modellen) som fungerar som grund för ditt headless-innehåll."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide"
>title="Starta modellkonsolen"
>abstract="Låt oss utforska hur du skapar ett återanvändbart schema, som kallas Content Fragment-modell, för ditt innehåll i Adobe Experience Manager as a Cloud Service. Se videon för att förstå varför detta är ett viktigt steg. <br><br>Starta den här modulen på en ny flik genom att klicka på knappen nedan och sedan följa den här guiden."
>additional-url="https://video.tv.adobe.com/v/3413261" text="Innehållsstruktur i video"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_footer"
>title="Grattis! Du lärde dig att skapa en modell för innehållsfragment som representerar strukturen för dina rubrikfria data och tog det första steget mot att leverera flerkanalsinnehåll på ett skalat och standardbaserat sätt."
>abstract=""

## Skapa en modell {#create-model}

Klicka på **Starta modellkonsolen** ovan öppnar konsolen för modeller av innehållsfragment på en ny flik.

![Modellkonsolen för innehållsfragment](assets/content-structure/content-fragment-model-console.png)

Tänk på modellkonsolen Content Fragment som ditt modellbibliotek, där du skapar nya modeller och hanterar befintliga modeller. Konsolen börjar tom, så vi skapar en ny modell!

1. I modellkonsolen för innehållsfragment klickar du på **Skapa** längst upp till höger på skärmen för att börja skapa en modell för innehållsfragment.

1. Guiden Skapa modell startar.

   ![Modellguide för innehållsfragment](assets/content-structure/model-wizard.png)

   Ange den obligatoriska informationen.

   * **Modelltitel** - Detta är en kort beskrivning av modellen och anger vanligtvis syftet med modellen.
   * **Aktivera modell** - Det här alternativet är markerat som standard och måste markeras för att det ska gå att skapa innehållsfragment baserat på den här modellen.

1. När de obligatoriska fälten har fyllts i klickar du på **Skapa** längst upp till vänster för att skapa modellen.

1. The **Lyckades** bekräftar att modellen skapades.

   ![Dialogrutan Slutfört för att skapa en ny modell för innehållsfragment](assets/content-structure/success.png)

## Lägg till fält i modellen {#configure-model}

Innan du kan använda modellen måste du definiera datastrukturen.

1. Klicka **Öppna** i **Lyckades** i föregående steg för att öppna den nya modellen i modellredigeraren för innehållsfragment där du kan definiera dess fält.

1. Dra ett fält från **Datatyper** till höger om redigeraren och släpp den i modellen för innehållsfragment.

   ![Lägg till en datatyp](assets/content-structure/drop-fields.png)

1. När en datatyp har placerats ut **Datatyper** kolumnen ändras automatiskt till **Egenskaper** där du kan definiera information om den datatyp du just placerat.

   ![Fliken Egenskaper för datafältet](assets/content-structure/data-type-properties.png)

1. När du har lagt till alla fält som behövs för modellen för innehållsfragment klickar du på **Spara** längst upp till höger i fönstret.

Modellen sparas och du återgår till modellkonsolen för innehållsfragment där du kan lägga till fler modeller om det behövs.

![Modulen är klar](assets/content-structure/content-fragment-model-console-populated.png)
