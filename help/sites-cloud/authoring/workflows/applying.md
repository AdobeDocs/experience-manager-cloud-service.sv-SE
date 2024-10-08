---
title: Använda arbetsflöden på sidor
description: När du redigerar kan du anropa arbetsflöden för att agera på sidorna. Det går också att använda mer än ett arbetsflöde.
exl-id: 86e71f0e-e53e-40bc-901d-2a1ab347bd0a
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 9%

---

# Använda arbetsflöden på sidor {#applying-workflows-to-pages}

När du redigerar kan du anropa arbetsflöden för att agera på sidorna. Det går också att använda mer än ett arbetsflöde.

När du använder arbetsflödet anger du följande information:

* Det arbetsflöde som ska användas.
   * Du kan använda vilket arbetsflöde som helst (som du fått tillgång till av AEM-administratören).
* Alternativt kan du använda en titel som hjälper till att identifiera arbetsflödesinstansen i en användares inkorg.
* Arbetsflödets nyttolast. Det kan vara en eller flera sidor.

Arbetsflöden kan startas från:

* [Platskonsolen](#starting-a-workflow-from-the-sites-console).
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
>AEM kan starta arbetsflöden på flera andra sätt.

<!-- 
>AEM administrators can [start workflows using several other methods](/help/sites-administering/workflows-starting.md).
-->

## Starta ett arbetsflöde från platskonsolen {#starting-a-workflow-from-the-sites-console}

Du kan starta ett arbetsflöde från:

* [alternativet Skapa i verktygsfältet Platser](#starting-a-workflow-from-the-sites-toolbar).
* [tidslinjen i webbplatskonsolen](#starting-a-workflow-from-the-timeline).

I båda fallen måste du [ange arbetsflödesinformation i guiden Skapa arbetsflöde](#specifying-workflow-details-in-the-create-workflow-wizard).

### Starta ett arbetsflöde från verktygsfältet Platser {#starting-a-workflow-from-the-sites-toolbar}

Du kan starta ett arbetsflöde från verktygsfältet i konsolen **Platser**:

1. Navigera till och markera önskad sida.

1. Från alternativet **Skapa** i verktygsfältet kan du nu välja **Arbetsflöde**.

   ![Skapa arbetsflöde från verktygsfältet](/help/sites-cloud/authoring/assets/workflows-create-from-toolbar.png)

1. Guiden **Skapa arbetsflöde** hjälper dig att [ange arbetsflödesinformation](#specifying-workflow-details-in-the-create-workflow-wizard).

### Starta ett arbetsflöde från tidslinjen {#starting-a-workflow-from-the-timeline}

Från **tidslinjen** kan du starta ett arbetsflöde som ska användas för den valda resursen.

1. [Markera resursen](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources) och öppna [Tidslinjen](/help/sites-cloud/authoring/basic-handling.md#timeline) (eller öppna tidslinjen och välj sedan resursen).
1. Pilen i kommentarfältet kan användas för att visa **Start Workflow**:

   ![Skapa arbetsflöde från tidslinjen](/help/sites-cloud/authoring/assets/workflows-create-from-timeline.png)

1. Guiden **Skapa arbetsflöde** hjälper dig att [ange arbetsflödesinformation](#specifying-workflow-details-in-the-create-workflow-wizard).

### Ange arbetsflödesinformation i guiden Skapa arbetsflöde {#specifying-workflow-details-in-the-create-workflow-wizard}

Guiden **Skapa arbetsflöde** hjälper dig att välja arbetsflöde och ange nödvändig information.

När guiden **Skapa arbetsflöde** har öppnats från antingen:

* [alternativet Skapa i verktygsfältet Platser](#starting-a-workflow-from-the-sites-toolbar).
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

   När det är klart använder du **Nästa** för att fortsätta.

   ![Ange arbetsflödesegenskaper](/help/sites-cloud/authoring/assets/workflows-properties.png)

1. I steget **Omfång** kan du välja:

   * **Lägg till innehåll** om du vill öppna [sökvägsläsaren](/help/sites-cloud/authoring/path-selection.md) och välja ytterligare resurser. I webbläsaren väljer du **Markera** om du vill lägga till innehållet i arbetsflödesinstansen.

   * En befintlig resurs som visar ytterligare åtgärder:

      * **Inkludera underordnade** för att ange att underordnade för den resursen ska inkluderas i arbetsflödet.
En dialogruta öppnas där du kan förfina markeringen enligt:

         * Inkludera endast omedelbara barn.
         * Inkludera endast ändrade sidor.
         * Inkludera endast redan publicerade sidor.

        Alla underordnade objekt läggs till i listan över resurser som arbetsflödet gäller för.

      * **Ta bort markering** om du vill ta bort resursen från arbetsflödet.

   ![Definiera arbetsflödesomfång](/help/sites-cloud/authoring/assets/workflows-scope.png)

   >[!NOTE]
   >
   >Om du lägger till ytterligare resurser kan du använda **Bakåt** för att justera inställningen för **Behåll arbetsflödespaket** i steget **Egenskaper**.

1. Använd **Skapa** för att stänga guiden och skapa arbetsflödesinstansen. Ett meddelande visas i webbplatskonsolen.

## Starta ett arbetsflöde från sidredigeraren {#starting-a-workflow-from-the-page-editor}

När du redigerar en sida kan du välja **Sidinformation** i verktygsfältet. Listrutan har alternativet **Starta i arbetsflöde**. Då öppnas en dialogruta där du kan ange önskat arbetsflöde, tillsammans med en titel om det behövs:

![Starta ett arbetsflöde från sidredigeraren](/help/sites-cloud/authoring/assets/workflows-create-page-editor.png)
