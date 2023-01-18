---
title: Anpassa innehåll i en exempelapp
description: Använd en React-exempelapp för att lära dig hur du anpassar innehåll med hjälp av den headless-funktion som finns i AEM as a Cloud Service.
hidefromtoc: true
index: false
exl-id: 32290ad4-d915-41b7-a073-2637eb38e978
source-git-commit: bcab02cbd84955ecdc239d4166ae38e5f79b3264
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 0%

---


# Anpassa innehåll i en exempelapp {#customize-app}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_react_app"
>title="Anpassa innehåll i en exempelapp för React"
>abstract="Din AEM headless-testversion är integrerad med en React-app som du kan anpassa."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_react_app_guide"
>title="Starta redigeraren för innehållsfragment"
>abstract="Din AEM headless-testversion är integrerad med en React-app så att du kan se hur enkelt det är för alla att hantera innehåll utan utvecklingstid.<br><br>Starta den här modulen på en ny flik genom att klicka nedan och följ sedan den här guiden."
>additional-url="https://video.tv.adobe.com/v/328618" text="Anpassa appen till video"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_react_app_guide_footer"
>title="I den här modulen lärde du dig att anpassa en exempelapp för React.<br><br>time to market: Snabbare!<br>Utvecklingscykler: Reducerat!<br><br>Nu förstår du hur enkelt det är att hantera headless-innehåll för webbplatser och appar som har AEM headless-funktioner."
>abstract=""

## Förhandsgranska appen {#preview}

Klicka på **Starta redigeraren för innehållsfragment** knappen ovan öppnar redigeraren för innehållsfragment på en ny flik.

![Redigera innehållsfragment](assets/customize-app/content-fragment-editor.png)

Exempelappen som medföljer din AEM headless-testversion drivs av innehållsfragment som levereras via GraphQL. Använd Content Fragment-redigeraren för att bekanta dig med innehållet genom att förhandsgranska exemplet.

1. Tryck eller klicka på **Förhandsgranska** längst upp till höger på redigeringsskärmen.

1. Demonstrationsappen öppnas på en ny flik. Appen är till för WKND:s påhittade livsstilsmärke. Klicka runt för att navigera i exempelinnehållet.

   ![Förhandsgranskning av demoapp](assets/customize-app/preview-demo-app.png)

1. Gå tillbaka till webbläsarfliken i Content Fragment-redigeraren för att fortsätta.

## Redigera ett sidhuvud i appen {#edit-app}

Innehållsfragmentsredigeraren visar programmets grundläggande layout som ett sidinnehållsfragment. The **Paneler** representerar olika sidor i programmet, som var och en är sin egen innehållsfragment. Genom att ändra dessa fragment kan du ändra innehållet i appen.

1. Tryck eller klicka **Mtn Biker i Canyon** i **Paneler** -avsnitt.

   ![Tryck på Mtn Biker i Canyon-fragment](assets/customize-app/mtn-biker-in-canyon.png)

1. Redigeraren öppnar programmets rubrikpanel för bergsbudgivaren. Varje panel består av lager som representerar olika bilder och text som utgör upplevelsen.

   ![Paneler](assets/customize-app/panels.png)

1. Markera textlagret **Mtn Biker i Canyon Text Layer**. Då öppnas detaljerna för lagret i redigeraren. Lagret består av flera innehållsfragment som styr texten som visas på den här panelen i programmet.

   ![Välj Mtn Biker i Canyon Title](assets/customize-app/mtn-biker-in-canyon-text-layer.png)

1. Välj **Mtn Biker in Canyon Title** textobjekt. Då öppnas Content Fragment-redigeraren.

   ![Välj Mtn Biker i textobjektet för cellanimering](assets/customize-app/mtn-biker-in-canyon-title.png)

1. Ändra texten från `Your next great adventure is calling` till `Choose your own adventure`. Ändringen sparas automatiskt av redigeraren.

1. Tryck eller klicka **Förhandsgranska** i fönstrets övre högra hörn för att se ändringarna. Förhandsgranskningen av demoappen öppnas på en ny flik.

   ![Förhandsgranskning av demoapp](assets/customize-app/preview-demo-app-text.png)

Så enkelt är det att uppdatera innehåll i en React-app när den är integrerad i AEM headless CMS.

## Växla en bild i appen {#change-image}

Nu när du har ändrat en rubrik i appen kan du prova att ändra en bild.

1. Gå tillbaka till fliken Webbläsare i redigeraren för innehållsfragment.

1. Du måste gå tillbaka till rätt plats i Content Fragment-redigeraren. Bröderna högst upp till vänster i redigeraren visar var du befinner dig i innehållshierarkin. Tryck eller klicka **Mtn Biker i Canyon** i vägbeskrivningarna för att återgå till den sidan.

   ![Breadcrumbs](assets/customize-app/breadcrumbs.png)

1. Välj **Mtn Biking - Biker** bildlager. Då öppnas Content Fragment-redigeraren

   ![Redigera bildfragment](assets/customize-app/mtn-biking-biker.png)

1. Tryck eller klicka på **X** om du vill ta bort den större bilden. Bilden försvinner och redigeraren visar ett fel eftersom bilden krävs för den här modellen för innehållsfragment.

   ![Bild borttagen från fragment](assets/customize-app/mtn-biking-biker-no-image.png)

1. Tryck eller klicka **Lägg till resurs**.

1. The **Välj resurs** öppnas och sökvägen **sample-wknd-app** > **en** > **bildfiler** väljs automatiskt åt dig.

1. Markera bilden `biker-yellow.png` och sedan trycka eller klicka **Välj**.

   ![Välj resurs](assets/customize-app/select-asset.png)

1. Bilden på den här färgväljaren ersätts med den valda bilden. Redigeraren sparar ändringarna automatiskt.

   ![Redigerat fragment av budgivarbild](assets/customize-app/mtn-biking-biker-edited.png)

1. Tryck eller klicka **Förhandsgranska** i fönstrets övre högra hörn för att se ändringarna. Förhandsgranskningen av demoappen öppnas på en ny flik. Klicka på Uppdatera i webbläsaren så ser du din nya bikerbild med gula kortkommandon i appen.

Det är så enkelt att uppdatera bilder och resurser i apparna med AEM headless CMS.

## Lägga till en referens till ett nytt innehållsfragment i appen {#create-moment}

Nu när du har uppdaterat bilden av budgivaren ska vi gå igenom hur man lägger till nytt innehåll i en app genom att skapa och referera till ett nytt innehållsfragment. Du kommer att lägga till ett produktsamtal som hanteras av innehållsfragmentet&quot;köpbart ögonblick&quot; på den andra panelen i programmet.

![Exempel på en köpbar stund](assets/customize-app/example-shoppable-moment.png)

1. Gå tillbaka till fliken Webbläsare i redigeraren för innehållsfragment.

1. Du måste gå tillbaka till rätt plats i Content Fragment-redigeraren. Bröderna högst upp till vänster i redigeraren visar var du befinner dig i innehållshierarkin. Tryck eller klicka **WKND - startsida** i vägbeskrivningarna för att återgå till den sidan.

   ![Gå tillbaka till layoutskärmen](assets/customize-app/breadcrumbs-2.png)

1. Välj **Mtn Biker på WKND Gul** -panelen.

   ![Skapa en shoppingupplevelse](assets/customize-app/mtn-biker-on-wknd-yellow.png)

1. Välj **Mtn Biking - köpbar** lager.

   ![Markera köpbart snabblager](assets/customize-app/mtn-biking-shoppable.png)

1. Om du vill skapa en ny utlysning på den här panelen måste du skapa en ny Content Fragment som kan köpas. Tryck eller klicka på **+ Skapa nytt fragment** -knappen.

   ![Lägg till en köpbar stund](assets/customize-app/create-new-fragment.png)

1. Du måste först välja en modell som det nya innehållsfragmentet ska baseras på. Välj **Moment som kan köpas** modell från **Modell för innehållsfragment** nedrullningsbar meny.

1. Ge Content Fragment ett namn. Skriv till exempel `Shorts` till **Namn** fält.

   ![Ge kunderna ett namn](assets/customize-app/new-content-fragment.png)

1. Tryck eller klicka **Skapa och öppna**.

1. Redigeraren öppnas för ditt nya innehållsfragment.

1. Ge shoppingstunden ett namn i **Text** fält som `Yellow shorts`.

1. Ange värden för **X** och **Y**. Här ska denna utlysning läggas över panelen. Ändringar i avsnittet sparas automatiskt av redigeraren
   * **X**: `-18`
   * **Y**: `-28`

   ![Redigera shoppingögonblicket](assets/customize-app/edit-shoppable-moment.png)

1. Tryck eller klicka **Förhandsgranska** i fönstrets övre högra hörn för att se ändringarna. Förhandsgranskningen av demoappen öppnas på en ny flik. Klicka på Uppdatera i webbläsaren för att testa placeringen och göra de justeringar som behövs i redigeraren.

Nu förstår du hur du kan skapa nytt innehåll och referera till det som ett innehållsfragment i appen utan några utvecklingscykler.
