---
title: Använda arbetsflöden på sidor
description: När du redigerar kan du anropa arbetsflöden för att göra något på sidorna; det går även att använda mer än ett arbetsflöde.
translation-type: tm+mt
source-git-commit: b551a0b0d85d264feabf78942a381c4239fdbadb
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 11%

---


# Använda arbetsflöden på sidor {#applying-workflows-to-pages}

När du redigerar kan du anropa arbetsflöden för att göra något på sidorna; det går även att använda mer än ett arbetsflöde.

När du använder arbetsflödet anger du följande information:

* Det arbetsflöde som ska användas.
   * Du kan använda vilket arbetsflöde som helst (som du fått tillgång till av AEM-administratören).
* Alternativt kan du använda en titel som hjälper till att identifiera arbetsflödesinstansen i en användares inkorg.
* Arbetsflödets nyttolast. detta kan vara en eller flera sidor.

Arbetsflöden kan startas från:

* [Sites-konsolen](#starting-a-workflow-from-the-sites-console).
* [när du redigerar en sida, från Sidinformation](#starting-a-workflow-from-the-page-editor).

>[!NOTE]
>
>Se även:
>
>* Använda arbetsflöden för DAM-resurser.
>* [Arbeta med projektarbetsflöden](/help/sites-cloud/authoring/projects/workflows.md).


<!-- 
>* [How to apply workflows to DAM assets](/help/assets/assets-workflow.md).
>* [Working with Project Workflows](/help/sites-cloud/authoring/projects/workflows.md).
-->

>[!NOTE]
>
>AEM-administratörer kan starta arbetsflöden på flera andra sätt.

<!-- 
>AEM administrators can [start workflows using several other methods](/help/sites-administering/workflows-starting.md).
-->

## Starta ett arbetsflöde från platskonsolen {#starting-a-workflow-from-the-sites-console}

Du kan starta ett arbetsflöde från:

* [alternativet Skapa i verktygsfältet](#starting-a-workflow-from-the-sites-toolbar)Platser.
* [tidslinjen i webbplatskonsolen](#starting-a-workflow-from-the-timeline).

I båda fallen måste du:

* [Ange arbetsflödesinformation i guiden](#specifying-workflow-details-in-the-create-workflow-wizard)Skapa arbetsflöde.

### Starta ett arbetsflöde från verktygsfältet Platser {#starting-a-workflow-from-the-sites-toolbar}

Du kan starta ett arbetsflöde från verktygsfältet i **webbplatskonsolen** :

1. Navigera till och markera önskad sida.

1. Från alternativet **Skapa** i verktygsfältet kan du nu välja **Arbetsflöde**.

   ![Skapa arbetsflöde från verktygsfältet](/help/sites-cloud/authoring/assets/workflows-create-from-toolbar.png)

1. Guiden **Skapa arbetsflöde** hjälper dig att [ange arbetsflödesinformation](#specifying-workflow-details-in-the-create-workflow-wizard).

### Starta ett arbetsflöde från tidslinjen {#starting-a-workflow-from-the-timeline}

Från **tidslinjen** kan du starta ett arbetsflöde som ska användas för den valda resursen.

1. [Markera resursen](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) och öppna [tidslinjen](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) (eller öppna tidslinjen och välj sedan resursen).
1. Pilen i kommentarfältet kan användas för att visa **startarbetsflödet**:

   ![Skapa arbetsflöde från tidslinjen](/help/sites-cloud/authoring/assets/workflows-create-from-timeline.png)

1. Guiden **Skapa arbetsflöde** hjälper dig att [ange arbetsflödesinformation](#specifying-workflow-details-in-the-create-workflow-wizard).

### Ange arbetsflödesinformation i guiden Skapa arbetsflöde {#specifying-workflow-details-in-the-create-workflow-wizard}

Guiden **Skapa arbetsflöde** hjälper dig att välja arbetsflöde och ange nödvändig information.

När du har öppnat guiden **Skapa arbetsflöde** från:

* [alternativet Skapa i verktygsfältet](#starting-a-workflow-from-the-sites-toolbar)Platser.
* [tidslinjen i webbplatskonsolen](#starting-a-workflow-from-the-timeline).

Du kan ange information:

1. I steget **Egenskaper** definieras de grundläggande alternativen för arbetsflödet:

   * **Arbetsflödesmodell**
   * **Arbetsflödets titel**

      * Du kan ange en titel för den här instansen så att du lättare kan identifiera den i ett senare skede.

   Beroende på arbetsflödesmodellen är följande alternativ också tillgängliga. Dessa gör att det paket som skapas som nyttolast kan behållas när arbetsflödet har slutförts.

   * **Behåll arbetsflödespaket**
   * **Pakettitel**

      * Du kan ange en rubrik för paketet för att underlätta identifieringen.
   >[!NOTE]
   >
   >Alternativet **Behåll arbetsflödespaket** är tillgängligt när arbetsflödet har konfigurerats med stöd för flera resurser och flera resurser har valts.

   <!--
   >The **Keep workflow package** option is available when the workflow has been configured for [Multi Resource Support](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) and multiple resources have been selected.
   -->

   När du är klar använder du **Nästa** för att fortsätta.

   ![Ange arbetsflödesegenskaper](/help/sites-cloud/authoring/assets/workflows-properties.png)

1. I steget **Omfång** kan du välja:

   * **Lägg till innehåll** för att öppna [sökvägsläsaren](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser) och välja ytterligare resurser, när du är i webbläsaren klickar/trycker du på **Välj** för att lägga till innehållet i arbetsflödesinstansen.

   * En befintlig resurs som visar ytterligare åtgärder:

      * **Inkludera underordnade objekt** för att ange att underordnade resurser ska inkluderas i arbetsflödet.
En dialogruta öppnas där du kan förfina markeringen enligt:

         * Inkludera endast omedelbara barn.
         * Inkludera endast ändrade sidor.
         * Inkludera endast redan publicerade sidor.

         Alla underordnade objekt läggs till i listan över resurser som arbetsflödet gäller för.

      * **Ta bort markeringen** för att ta bort resursen från arbetsflödet.

   ![Definiera arbetsflödesomfång](/help/sites-cloud/authoring/assets/workflows-scope.png)

   >[!NOTE]
   >
   >Om du lägger till ytterligare resurser kan du använda **Bakåt** för att justera inställningen för **Behåll arbetsflödespaket** i steget **Egenskaper**.

1. Använd **Skapa** för att stänga guiden och skapa arbetsflödesinstansen. Ett meddelande visas i webbplatskonsolen.

## Starta ett arbetsflöde från sidredigeraren {#starting-a-workflow-from-the-page-editor}

När du redigerar en sida kan du välja **Sidinformation** i verktygsfältet. Listrutan har alternativet **Starta i arbetsflöde**. Då öppnas en dialogruta där du kan ange önskat arbetsflöde, tillsammans med en titel om det behövs:

![Starta ett arbetsflöde från sidredigeraren](/help/sites-cloud/authoring/assets/workflows-create-page-editor.png)
