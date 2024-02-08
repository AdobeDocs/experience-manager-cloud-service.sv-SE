---
title: Skapa innehållsstrukturen för din app
description: Lär dig hur du använder AEM Content Fragment-modeller för att skapa en innehållsstruktur som fungerar som grund för ditt headless-innehåll.
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
source-git-commit: 07f61a3f6a794e18bc2e02e966392cdce3103a81
workflow-type: tm+mt
source-wordcount: '1002'
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
>abstract="Låt oss utforska hur du skapar ett återanvändbart schema, som kallas Content Fragment-modell, för ditt innehåll i Adobe Experience Manager as a Cloud Service. Titta på videon så att du förstår varför det här steget är viktigt. <br><br>I den här utbildningsmodulen använder du en resewebbplats som exempel och går igenom hur du skapar en modell som representerar en resa.<br><br>Starta den här modulen på en ny flik genom att klicka på knappen nedan och sedan följa den här guiden."
>additional-url="https://video.tv.adobe.com/v/3413261" text="Innehållsstruktur i video"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_footer"
>title="Grattis! Du lärde dig att skapa en modell för innehållsfragment som representerar strukturen för dina rubrikfria data och tog det första steget mot att leverera flerkanalsinnehåll på ett skalat och standardbaserat sätt."
>abstract=""

## Skapa en modell {#create-model}

Modellkonsolen för innehållsfragment öppnas på en ny flik. Tänk på modellkonsolen för innehållsfragment som ditt bibliotek med modeller, där du skapar modeller och hanterar befintliga modeller.

Du kan till exempel skapa en modell som representerar datastrukturen för en resa som visas på en resewebbplats. En resa som använder den här modellen kallas för en **Adventure**.

1. Klicka på i skärmens övre högra hörn **Skapa** för att börja skapa en modell för innehållsfragment.

1. Guiden Skapa modell vägleder dig genom att skapa din modell. Ange den obligatoriska informationen.

   * **Modelltitel** - En kort etikett på modellen och anger vanligtvis syftet med modellen. Du kan anropa den nya modellen `Adventure`.
   * **Aktivera modell** - Det här alternativet är markerat som standard och måste markeras för att det ska gå att skapa innehållsfragment baserat på den här modellen.

1. När de obligatoriska fälten har fyllts i klickar du **Skapa** längst upp till höger för att skapa modellen.

1. The **Lyckades** bekräftar att modellen har skapats. Klicka **Öppna** i dialogrutan så att du kan öppna den nya innehållsfragmentmodellen i redigeraren på en ny flik. Fortsätt sedan till nästa steg för att lägga till datafält i modellen.

![Steg 2 och 3 av att skapa en modell för innehållsfragment](assets/do-not-localize/create-model.png)

## Använda modellredigeraren {#configure-model}

Du har nu en modell som heter **Adventure**, men det finns inga detaljer som varaktighet, mål och aktiviteter. Innan du kan använda modellen måste du definiera datastrukturen.

I redigeraren för innehållsfragmentmodellen konfigurerar du de datatyper och egenskaper som definierar innehållet i modellen.

>[!TIP]
>
>Det är viktigt att du följer namnschemat i följande instruktioner eftersom dessa specifika namn hänvisas till i senare moduler.

1. Dra en **Enkelradig text** fält från **Datatyper** till höger om redigeraren och släpp den i innehållsfragmentmodellen.

1. När en datatyp har placerats ut **Datatyper** kolumnen ändras automatiskt till **Egenskaper** där du kan definiera information om den datatyp du placerat ut. För det här första fältet vill du lagra titeln på resan eller äventyret. Ange följande egenskaper.

   * **Återge som:** **Textfält** - När du skapar ett äventyr lagrar det här fältet titeln på äventyret.
   * **Fältetikett:** `Title` - Den etikett som visas för det här fältet när du skapar ett äventyr.

1. När du har definierat egenskaperna för fältet kan du växla tillbaka till **Datatyper** i den högra panelen och lägga till ytterligare fält genom att dra och släppa.

På så sätt kan du lägga till så många fält som behövs i modellen för att stödja den datastruktur du behöver. Typerna av datafält varierar, men processen att lägga till dem i modellen är densamma.

Fortsätt till nästa avsnitt så att du kan lägga till de fält som behövs för att slutföra och spara **Adventure** modell

![Steg ett, två och tre av de fält som läggs till i modellen](assets/do-not-localize/define-model-fields.png)

## Lägg till fält i modellen {#additional-fields}

Du har redan ett fält för titeln på äventyret. Nu måste du lägga till fält för att fånga beskrivningen, priset och en representativ bild av äventyret.

>[!TIP]
>
>The **Adventure** Modellen baseras på WKND-exempelwebbplatsen för AEM. Du kan [besök webbplatsen här](https://wknd.site/us/en/adventures/yosemite-backpacking.html) för att se innehåll som använder **Adventure** modell.

Följ samma steg som ovan för att lägga till dessa ytterligare fält. Den enda skillnaden är de egenskaper som du måste ange.

1. Lägg till ett fält så att du kan lagra beskrivningen av äventyret genom att dra och släppa en **Flerradstext** och ange följande egenskaper:

   * **Återge som:** **Textområde** - När du skapar ett äventyr lagrar det här fältet en kort beskrivning av resan.
   * **Fältetikett:** `Description` - Den etikett som visas för det här fältet när du skapar ett äventyr.

1. Lägg till ett fält så att du kan lagra priset på äventyret genom att dra och släppa en **Enkelradig text** och ange följande egenskaper:

   * **Återge som:** **Textfält** - När du skapar ett äventyr lagrar det här fältet priset på resan.
   * **Fältetikett:** `Price` - Den etikett som visas för det här fältet när du skapar ett äventyr.

1. Lägg till ett fält så att du kan lagra en bild som representerar resan. Bilder i AEM lagras som en annan typ av innehåll som kallas **Resurser**. Om du vill skapa ett fält åt dem drar och släpper du en **Innehållsreferens** fält som refererar till bildresursen.

   * **Återge som:** **Innehållsreferens** - När du skapar ett äventyr pekar det här fältet på bildresursen som representerar den här resan.
   * **Fältetikett:** `Image` - Den etikett som visas för det här fältet när du skapar ett äventyr.
   * **Rotsökväg:** `/content/dam/aem-demo-assets/en` - Detta anger en startpunktssökväg när du bläddrar efter resurser med resursväljaren.

1. När du har lagt till de nödvändiga fälten för modellen för innehållsfragment, klickar du på längst upp till höger i fönstret **Spara**.

1. Modellen sparas och du återgår till modellkonsolen för innehållsfragment.
