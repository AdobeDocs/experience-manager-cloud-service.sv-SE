---
title: Skapa innehållsstrukturen för din app
description: Lär dig hur du använder AEM Content Fragment-modeller för att skapa en innehållsstruktur som fungerar som grund för ditt headless-innehåll.
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
source-git-commit: ac94981e477e1fe8b883460ed9be009b4c1c088d
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---


# Skapa innehållsstrukturen för din app {#content-structure}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="Skapa innehållsstrukturen för din app"
>abstract="När du följer den här serien med interaktiva stödlinjer lär du dig att skapa en struktur (som kallas Content Fragment-modellen) som fungerar som grundstruktur för ditt headless-innehåll."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide"
>title="Starta modellkonsolen"
>abstract="Låt oss utforska hur du skapar ett återanvändbart schema, som kallas Content Fragment-modell, för ditt innehåll i Adobe Experience Manager as a Cloud Service. Se videon för att förstå varför detta är ett viktigt steg. <br><br>I den här utbildningsmodulen ska vi använda en resewebbplats som exempel och gå igenom hur vi skapar en modell som representerar en resa.<br><br>Starta den här modulen på en ny flik genom att klicka på knappen nedan och sedan följa den här guiden."
>additional-url="https://video.tv.adobe.com/v/3413261" text="Innehållsstruktur i video"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_footer"
>title="Grattis! Du lärde dig att skapa en modell för innehållsfragment som representerar strukturen för dina rubrikfria data och tog det första steget mot att leverera flerkanalsinnehåll på ett skalat och standardbaserat sätt."
>abstract=""

## Skapa en modell {#create-model}

Modellkonsolen för innehållsfragment öppnas på en ny flik. Tänk på modellkonsolen för innehållsfragment som ditt bibliotek med modeller, där du skapar nya modeller och hanterar befintliga modeller.

Vi kommer till exempel att skapa en modell som representerar datastrukturen för en resa som visas på en resewebbplats. Vi kommer att använda den här modellen som en resa **Adventure**.

1. Klicka på **Skapa** längst upp till höger på skärmen för att börja skapa en modell för innehållsfragment.

1. Guiden Skapa modell startar, som vägleder dig genom att skapa din modell. Ange den obligatoriska informationen.

   * **Modelltitel** - Detta är en kort etikett på modellen och anger vanligtvis syftet med modellen. Vi kallar vår nya modell `Adventure`.
   * **Aktivera modell** - Det här alternativet är markerat som standard och måste markeras för att det ska gå att skapa innehållsfragment baserat på den här modellen.

1. När de obligatoriska fälten har fyllts i klickar du på **Skapa** längst upp till vänster för att skapa modellen.

1. The **Lyckades** bekräftar att modellen skapades. Klicka **Öppna** i dialogrutan för att öppna den nya innehållsfragmentmodellen i redigeraren på en ny flik. Fortsätt sedan till nästa steg för att lägga till datafält i modellen.

![Steg 2 och 3 av att skapa en modell för innehållsfragment](assets/do-not-localize/create-model.png)

## Använda modellredigeraren {#configure-model}

Vi har nu en modell som heter **Adventure**, men har inga detaljer som varaktighet, destination, aktiviteter osv. Innan du kan använda modellen måste du definiera datastrukturen.

I redigeraren för innehållsfragmentmodellen konfigurerar du de datatyper och egenskaper som definierar innehållet i modellen.

>[!TIP]
>
>Det är viktigt att du följer namngivningsscheman i följande instruktioner eftersom vi kommer att referera till dessa specifika namn i senare moduler.

1. Dra en **Enkelradig text** fält från **Datatyper** till höger om redigeraren och släpp den i modellen för innehållsfragment.

1. När en datatyp har placerats ut **Datatyper** kolumnen ändras automatiskt till **Egenskaper** där du kan definiera information om den datatyp du just placerat. För det första fältet vill vi lagra titeln på resan eller äventyret. Ange följande egenskaper.

   * **Återge som:** **Textfält** - När du skapar ett äventyr lagrar det här fältet titeln på äventyret.
   * **Fältetikett:** `Title` - Det här är den etikett som visas för det här fältet när du skapar ett nytt äventyr.

1. När du har definierat egenskaperna för fältet kan du växla tillbaka till **Datatyper** i den högra panelen och lägga till ytterligare fält genom att dra och släppa.

På så sätt kan du lägga till så många fält som behövs i modellen för att stödja den typ av datastruktur du behöver. Typerna av datafält varierar, men processen att lägga till dem i modellen är densamma.

Fortsätt till nästa avsnitt för att lägga till de fält som krävs för att slutföra och spara **Adventure** modell

![Steg ett, två och tre av de fält som läggs till i modellen](assets/do-not-localize/define-model-fields.png)

## Lägg till fält i modellen {#additional-fields}

Du har redan ett fält för titeln på äventyret. Nu behöver du lägga till fält för att fånga beskrivningen, priset och en representativ bild av äventyret.

>[!TIP]
>
>The **Adventure** Modellen baseras på WKND-exempelwebbplatsen för AEM. Du kan [besök webbplatsen här](https://wknd.site/us/en/adventures/yosemite-backpacking.html) för att se innehåll som använder **Adventure** modell.

Följ samma steg som ovan för att lägga till dessa ytterligare fält. Den enda skillnaden är de egenskaper som du måste ange.

1. Lägg till ett fält för att lagra beskrivningen av äventyret genom att dra och släppa en **Flerradstext** och ange följande egenskaper:

   * **Återge som:** **Textområde** - När du skapar ett äventyr lagrar det här fältet en kort beskrivning av resan.
   * **Fältetikett:** `Description` - Det här är den etikett som visas för det här fältet när du skapar ett nytt äventyr.

1. Lägg till ett fält för att lagra priset på äventyret genom att dra och släppa en **Enkelradig text** och ange följande egenskaper:

   * **Återge som:** **Textfält** - När du skapar ett äventyr lagrar det här fältet priset på resan.
   * **Fältetikett:** `Price` - Det här är den etikett som visas för det här fältet när du skapar ett nytt äventyr.

1. Lägg till ett fält för att lagra en bild som representerar resan. Bilder i AEM lagras som en annan typ av innehåll som kallas **Resurser**. För att skapa ett fält åt dem måste du dra och släppa en **Innehållsreferens** fält som ska referera till bildresursen.

   * **Återge som:** **Innehållsreferens** - När du skapar ett äventyr pekar det här fältet på den bildresurs som representerar den här resan.
   * **Fältetikett:** `Image` - Det här är den etikett som visas för det här fältet när du skapar ett nytt äventyr.

1. När du har lagt till alla fält som behövs för modellen för innehållsfragment klickar du på **Spara** längst upp till höger i fönstret.

1. Modellen sparas och du återgår till modellkonsolen för innehållsfragment.
