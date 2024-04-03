---
title: Lägga till versioner, kommentarer och anteckningar i ett formulär.
description: Använd adaptiva formulärkärnkomponenter för att lägga till kommentarer, anteckningar och versionshantering i ett adaptivt formulär.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Adaptive Forms, Core Components
hidefromtoc: true
source-git-commit: 4e60d7315fe7a92d608f0858a7108f7590e9aefa
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# Versionshantering, granskning och kommentering i ett adaptivt formulär

<!--Before you can use versionings, comments, and annotations in an Adaptive Form, you must ensure you have [enabled Adaptive Form Core Components](
https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components).-->

<!--Adaptive Form Core Components facilitates to add versionings, comments, and annotations to a form. These features helps form authors and users to enhance the form development process where they can create multiple versions of a form, collaborate and add their comments to a form, and add annotations to form components.-->

<span class="preview"> Det här är en förhandsversion som du kommer åt via vår [kanal för förhandsversion](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>


Med adaptiva Form Core Components kan man lägga in versionshantering, kommentarer och anteckningar i blanketterna. Dessa funktioner effektiviserar formulärutvecklingsprocessen genom att användarna kan skapa och hantera flera versioner av ett formulär, delta i samverkansdiskussioner via kommentarer och bifoga anteckningar till specifika formulärkomponenter, vilket förbättrar den övergripande formuläruppbyggnadsupplevelsen.


## Versionshantering av anpassningsbara formulär {#adaptive-form-versioning}

Med anpassad formulärversionshantering kan du lägga till versioner i ett formulär. Formulärförfattare kan enkelt skapa flera versioner av ett formulär och till slut använda den som passar affärsmålen. Dessutom kan formuläranvändare även återställa formuläret till tidigare versioner. Man kan också jämföra två versioner av ett formulär genom att förhandsgranska dem så att de kan analysera dem bättre ur gränssnittsperspektiv. Låt oss gå in i detalj på varje funktion för anpassad versionshantering av formulär:

### Skapa en formulärversion {#create-a-form-version}

Så här skapar du en version av ett formulär:

1. Skapa ett formulär eller använd ett befintligt formulär.
1. Navigera till AEM **[!UICONTROL Form]**>>**[!UICONTROL Forms & Documents]** och väljer **Formulär**.
1. I listrutan till vänster väljer du **[!UICONTROL Versions]**.
   ![Markera ett formulär](select-a-form.png)
1. Klicka på **tre punkter** i den nedre panelen till vänster klickar du på **[!UICONTROL Save as Version]**.
1. Ange en etikett för formulärversionen och du kan ange information om formuläret via kommentaren.
   ![Skapa en formulärversion](create-a-form-version.png)

### Uppdatera en formulärversion {#update-a-form-version}

När du redigerar och uppdaterar ett anpassat formulär lägger du till en ny version i formuläret. Följ stegen i det sista avsnittet för att namnge en ny version av formuläret så som det visas i bilden:

![Uppdatera en formulärversion](update-a-form-version.png)

### Återställa en formulärversion {#revert-a-form-version}

Om du vill återställa en formulärversion till föregående väljer du en formulärversion och klickar på **[!UICONTROL Revert to this Version]**.

![Återställ formulärversion](revert-form-version.png)

### Jämför formulärversioner {#compare-form-versions}

Formulärförfattare kan jämföra två olika versioner av ett formulär för förhandsgranskning. Om du vill jämföra versioner väljer du en formulärversion och klickar på **[!UICONTROL Compare to Current]**. Den visar två olika formulärversioner i förhandsgranskningsläge.

![Jämför formulärversioner](compare-form-versions.png)

## Lägg till kommentarer {#add-comments}

En granskning är en mekanism som gör att en eller flera granskare kan kommentera i formulär. Alla formuläranvändare kan kommentera i ett formulär eller granska ett formulär med hjälp av kommentarer. Om du vill kommentera ett formulär markerar du **[!UICONTROL Form]** och lägga till en **[!UICONTROL Comment]** till formuläret.

>[!NOTE]
> När du använder kommentarer i adaptiva formulärkärnkomponenter enligt beskrivningen ovan, är formulärfunktionen [Skapa och hantera granskningar av formulär](/help/forms/create-reviews-forms.md) är inaktiverat.


![Lägga till kommentarer i ett formulär](form-comments.png)

## Lägg till anteckningar {#adaptive-form-annotations}

I många fall måste formulärgruppsanvändare lägga till kommentarer i ett formulär för granskning, till exempel på en viss flik i ett formulär eller komponenter i ett formulär. I sådana fall kan författare använda anteckningar. Gör så här om du vill lägga till anteckningar i ett formulär:

1. Öppna ett formulär i **[!UICONTROL Edit]** läge.

1. Klicka på **lägg till ikon** som finns på den övre högra listen enligt bilden.
   ![Anteckning](annotation.png)

1. Klicka på **lägg till ikon** som finns på den övre vänstra listen så som den anges i bilden för att lägga till syntaxen.
   ![Lägg till anteckning](add-annotation.png)

1. Nu kan du lägga till kommentarer, rita skisser med flera färger i formulärkomponenterna.

1. Om du vill se alla dina tillagda anteckningar i ett formulär markerar du formuläret så ser du de tillagda anteckningarna på den vänstra panelen, som i bilden.

   ![Se tillagda anteckningar](see-annotations.png)











