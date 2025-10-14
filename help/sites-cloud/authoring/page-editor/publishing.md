---
title: Publicera innehåll med sidredigeraren
description: Lär dig hur sidredigeraren publicerar innehåll.
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 5871e04d3bd78bdd8df55d42e7619c98ea3f38ca
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# Publicera innehåll med webbplatsredigeraren {#publishing}

Lär dig hur sidredigeraren publicerar innehåll.

## Publicera från sidredigeraren {#publishing-from-the-page-editor}

Om du redigerar en sida i [sidredigeraren](/help/sites-cloud/authoring/page-editor/introduction.md) kan den publiceras direkt från redigeraren.

1. Välj ikonen **Sidinformation** för att öppna menyn och sedan alternativet **Publicera sida** .

   ![Publicera en sida via sidalternativ](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. Beroende på om sidan har referenser som behöver publiceras:

   * Sidan publiceras direkt om det inte finns några referenser att publicera.
   * Om sidan innehåller referenser som behöver publiceras visas dessa i guiden **Publicera** där du kan antingen:
      * Ange vilka resurser, eller taggar och så vidare, som du vill publicera tillsammans med sidan och använd sedan **Publicera** för att slutföra processen.
      * Använd **Avbryt** om du vill avbryta åtgärden.

   ![Publicerar referenser med sidan](/help/sites-cloud/authoring/assets/publishing-references.png)

1. Om du väljer **Publicera** replikeras sidan till publiceringsmiljön. I sidredigeraren visas en informationsbanderoll som bekräftar publiceringsåtgärden.

   ![Banderoll för publiceringsstatusinformation](/help/sites-cloud/authoring/assets/publishing-info.png)

   När du visar samma sida i konsolen visas den uppdaterade publiceringsstatusen.

   ![Sidpubliceringsstatus i kolumnvy i webbplatskonsolen](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>Publicering från sidredigeraren är en ytlig publicering, d.v.s. endast den valda sidan/de markerade sidorna publiceras och eventuella underordnade sidor publiceras/inte.

>[!NOTE]
>
>Sidor som används av [alias](/help/sites-cloud/authoring/sites-console/page-properties.md#advanced) i redigeraren kan inte publiceras. Publiceringsalternativen i redigeraren är bara tillgängliga för sidor som du kommer åt via de faktiska sökvägarna.

## Avpublicera från sidredigeraren {#unpublishing}

När du redigerar en sida med sidredigeraren och vill avpublicera sidan väljer du **Avpublicera sida** på menyn **Sidinformation**, på samma sätt som du [publicerar sidan](#publishing-from-the-editor).

>[!NOTE]
>
>Sidor som används av [alias](/help/sites-cloud/authoring/sites-console/page-properties.md#advanced) i redigeraren kan inte avpubliceras. Publiceringsalternativen i redigeraren är bara tillgängliga för sidor som du kommer åt via de faktiska sökvägarna.

## Publicera och avpublicera från Sites Console {#publishing-sites-console}

Du kan också publicera [&#x200B; från webbplatskonsolen &#x200B;](/help/sites-cloud/authoring/sites-console/publishing-pages.md) som kan vara användbar när du vill publicera flera sidor med innehåll eller schemalägga publicering eller avpublicering.
