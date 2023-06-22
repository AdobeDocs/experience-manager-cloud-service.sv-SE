---
title: Marknadsföra Launches
description: Du måste befordra startsidor för att kunna flytta tillbaka innehållet till källan (produktionen) innan du publicerar.
exl-id: 5f5ed17c-43db-4ef6-ab79-c491326fa01c
source-git-commit: 635f4c990c27a7646d97ebd08b453c71133f01b3
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 1%

---

# Marknadsföra Launches {#promoting-launches}

Du måste befordra startsidor för att kunna flytta tillbaka innehållet till källan (produktionen) innan du publicerar. När en startsida befordras ersätts motsvarande sida på källsidorna med innehållet på den befordrade sidan. Följande alternativ är tillgängliga när du befordrar en startsida:

* Anger om bara den aktuella sidan eller hela programstarten ska befordras.
* Anger om underordnade sidor för den aktuella sidan ska befordras.
* Anger om en fullständig start ska erbjudas eller endast sidor som har ändrats.
* Anger om starten ska tas bort efter att den har befordrats.

>[!NOTE]
>
>När du har befordrat startsidorna till målet (**Produktion**) kan du aktivera **Produktion** sidor som en enhet (för att göra processen snabbare). Lägg till sidorna i ett arbetsflödespaket och använd det som nyttolast för ett arbetsflöde som aktiverar ett sidpaket. Du måste skapa arbetsflödespaketet innan du befordrar starten. Se [Bearbeta befordrade sidor med AEM](#processing-promoted-pages-using-aem-workflow).

>[!CAUTION]
>
>En enstaka programstart kan inte befordras samtidigt. Det innebär att två befordra åtgärder samtidigt vid samma programstart kan resultera i ett fel - `Launch could not be promoted` (tillsammans med konfliktfel i loggen).

>[!CAUTION]
>
>När du befordrar starter för *ändrad* sidor, ändringar i både käll- och startgrenarna beaktas.

## Marknadsför startsidor {#promoting-launch-pages}

>[!NOTE]
>
>Detta omfattar den manuella åtgärden att marknadsföra startsidor när det bara finns en startnivå. Se:
>
>* [Befordra en kapslad start](#promoting-a-nested-launch) när det finns mer än en start i strukturen.
>* [Startar - ordningen för händelser](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events) om du vill ha mer information om automatiska kampanjer och publiceringar.
>

Du kan befordra starter från **Webbplatser** konsolen eller **Startar** konsol:

1. Öppna:
   * The **Webbplatser** konsol vid navigering på källsidor:
      1. Öppna [referenser, räl](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) och välj en källsida med [markeringsläge](/help/sites-cloud/authoring/getting-started/basic-handling.md) (eller markera och öppna referenslinjen är ordningen inte viktig). Alla referenser visas.
      1. Välj **Startar** (t.ex. Launches (1)) för att visa en lista över specifika starter.
      1. Välj den specifika starten för att visa tillgängliga åtgärder.
      1. Välj **Befordra lansering** för att öppna guiden.
   * The **Webbplatser** konsol vid navigering på startsidor:
      1. Välj önskad startsida med [markeringsläge](/help/sites-cloud/authoring/getting-started/basic-handling.md).
      1. The **Befordra** finns i verktygsfältet.
   * The **Startar** konsol:
      1. Välj start (tryck/klicka på miniatyrbilden).
      1. Välj **Befordra**.
1. I det första steget kan du ange:
   * **Mål**
      * **Ta bort start efter befordran**
   * **Omfång**
      * **Befordra en fullständig lansering**
      * **Befordra ändrade sidor**
      * **Befordra godkända sidor** - beroende av arbetsflödet för godkännande vid start
      * **Höj upp aktuell sida**
      * **Befordra aktuella sidor och undersidor**

     Om du t.ex. väljer att bara befordra ändrade sidor:

     ![Starta kampanj](/help/sites-cloud/authoring/assets/launches-promote.png)

     >[!NOTE]
     >
     >Detta omfattar en enstaka programstart, om du har kapslade programstarter, se [Befordra en kapslad start](#promoting-a-nested-launch).
1. Välj **Nästa** för att fortsätta.
1. Du kan granska de sidor som ska befordras; dessa beror på vilket sidintervall du har valt:

   ![Granska kampanj](/help/sites-cloud/authoring/assets/launches-promote-review.png)

1. Välj **Befordra**.

## Befordra startsidor vid redigering {#promoting-launch-pages-when-editing}

När du redigerar en startsida visas **Promote Launch** åtgärd är också tillgänglig från **Sidinformation**. Guiden öppnas för att samla in den information som behövs.

![Befordra lansering från webbplatsinformation](/help/sites-cloud/authoring/assets/launches-promote-page-info.png)

>[!NOTE]
>
>Detta är tillgängligt för enstaka och [kapslade starter](#promoting-a-nested-launch).

## Befordra en kapslad start {#promoting-a-nested-launch}

När du har skapat en kapslad start kan du befordra den tillbaka till någon av källorna, inklusive rotkällan (produktionen).

![En kapslad start](/help/sites-cloud/authoring/assets/launches-promoting-nested.png)

1. Precis som när du skapar en kapslad start går du till och väljer önskad start i antingen **Startar** konsolen eller **Referenser** järnväg.
1. Välj **Befordra lansering** för att öppna guiden.
1. Ange nödvändig information:
   * **Mål**
      * **Erbjudandemål** - Du kan göra reklam för alla källor.
      * **Ta bort start efter befordran** - Efter befordran tas den markerade starten och alla kapslade starter bort.
   * **Omfång** - Här kan du välja om du vill befordra hela programstarten eller bara de sidor som faktiskt har redigerats. Om det är det senare alternativet kan du välja att ta med/exkludera underordnade sidor. Standardkonfigurationen är att endast befordra sidändringar för den aktuella sidan:
      * **Befordra en fullständig lansering**
      * **Befordra ändrade sidor**
      * **Befordra godkända sidor** - beroende av arbetsflödet för godkännande vid start
      * **Höj upp aktuell sida**
      * **Befordra aktuella sidor och undersidor**

   ![Befordra startinställningar](/help/sites-cloud/authoring/assets/launches-promote-settings.png)

1. Välj **Nästa**.
1. Granska kampanjinformationen innan du väljer **Befordra**:

   ![Granska kampanjinställningar](/help/sites-cloud/authoring/assets/launches-promote-review-2.png)

   >[!NOTE]
   >
   >Vilka sidor som visas beror på **Omfång** definierade och eventuellt de sidor som har redigerats.

1. Ändringarna befordras och återspeglas i **Startar** konsol:

   ![Startar konsolen](/help/sites-cloud/authoring/assets/launches-console.png)

## Bearbeta befordrade sidor med AEM Workflow {#processing-promoted-pages-using-aem-workflow}

Använd arbetsflödesmodeller för att utföra massbearbetning av befordrade startsidor:

1. Skapa ett arbetsflödespaket.
1. När författare befordrar startsidor lagrar de dem i arbetsflödespaketet.
1. Starta en arbetsflödesmodell med paketet som nyttolast.

Om du vill starta ett arbetsflöde automatiskt när sidor befordras konfigurerar du en startfunktion för arbetsflödet för paketnoden. <!--To start a workflow automatically when pages are promoted, [configure a workflow launcher](/help/sites-administering/workflows-starting.md#workflows-launchers) for the package node.-->

Du kan t.ex. automatiskt generera begäranden om sidaktivering när författare befordrar startsidor. Konfigurera en startfunktion för arbetsflödet för aktivering av begäran när paketnoden ändras.

![Erbjudandearbetsflöde](/help/sites-cloud/authoring/assets/launches-create-workflow.png)
