---
title: Publicera sidor
description: Lär dig hur du publicerar och avpublicerar sidor med olika mekanismer i AEM.
exl-id: 89f2363c-7922-4ca5-92cb-cbee6a393ee3
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1801'
ht-degree: 5%

---

# Publicera sidor {#publishing-pages}

När du har skapat och granskat ditt innehåll i författarmiljön är målet att [göra den tillgänglig på din offentliga webbplats](/help/sites-cloud/authoring/getting-started/concepts.md) (publiceringsmiljön).

Detta kallas att publicera en sida. När du vill ta bort en sida från publiceringsmiljön kallas det för att avpublicera. När sidan publiceras och avpubliceras är den fortfarande tillgänglig i redigeringsmiljön för ytterligare ändringar tills du tar bort den.

Du kan publicera/avpublicera en sida direkt eller vid ett fördefinierat datum/tid i framtiden.

>[!NOTE]
>
>När du publicerar ett Experience Fragment följer du i princip samma procedur som när du publicerar en sida, även om du väljer Experience Fragments-konsolen eller redigeraren.

## Terminologi {#terminology}

Du kan stöta på olika termer om publicering när du arbetar med Adobe Experience Manager (AEM) as a Cloud Service.

* **Publicera/avpublicera**
   * Detta är de primära villkoren för de åtgärder som gör innehållet tillgängligt för allmänheten i publiceringsmiljön (eller inte).
   * Detta är de termer som används i AEM.
* **Aktivera/inaktivera**
   * Dessa termer är synonyma med publicera/avpublicera.
   * Dessa termer användes i tidigare versioner av AEM.
* **Replikering/replikering**
   * Detta är de tekniska termer som beskriver hur data flyttas (till exempel sidinnehåll, filer, kod, användarkommentarer) från en miljö till en annan när du publicerar en sida.
   * Dessa termer används främst av utvecklare.

## Publicera sidor {#publishing-pages-1}

Beroende på din plats kan du publicera:

* [Från sidredigeraren](#publishing-from-the-editor)
* [Från webbplatskonsolen](#publishing-from-the-console)

>[!NOTE]
>
>Om du inte har behörighet att publicera en viss sida:
>
>* Ett arbetsflöde aktiveras för att meddela lämplig person om din begäran om publicering.
>* Det här arbetsflödet kan ha anpassats av ditt utvecklingsteam.
>* Ett meddelande visas kort för att meddela dig att arbetsflödet har utlösts.

>[!NOTE]
>
> Fler möjligheter finns på **I tid** och **Fråntid** i [Fliken Grundläggande i Sidegenskaper](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)

### Publicera från Redigeraren {#publishing-from-the-editor}

Om du redigerar en sida kan den publiceras direkt från redigeraren.

1. Välj **Sidinformation** -ikonen för att öppna menyn och sedan **Publicera sida** alternativ.

   ![Publicera en sida via sidalternativ](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. Beroende på om sidan har referenser som behöver publiceras:

   * Sidan publiceras direkt om det inte finns några referenser att publicera.
   * Om sidan innehåller referenser som behöver publiceras visas dessa i **Publicera** guide, där du kan
      * Ange vilket av resurserna/taggarna/etc. du vill publicera tillsammans med sidan och sedan använda **Publicera** för att slutföra processen.
      * Använd **Avbryt** om du vill avbryta åtgärden.

   ![Publicera referenser med sidan](/help/sites-cloud/authoring/assets/publishing-references.png)

1. Markera **Publicera** kommer att replikera sidan till publiceringsmiljön. I sidredigeraren visas en informationsbanderoll som bekräftar publiceringsåtgärden.

   ![Banderoll för publiceringsstatusinformation](/help/sites-cloud/authoring/assets/publishing-info.png)

   När du visar samma sida i konsolen visas den uppdaterade publiceringsstatusen.

   ![Sidpubliceringsstatus i kolumnvy i platskonsolen](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>Publicering från redigeraren är en ytlig publicering, d.v.s. bara den eller de markerade sidorna publiceras och eventuella underordnade sidor publiceras/publiceras inte.

>[!NOTE]
>
>Sidor som används av [alias](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced) i redigeraren kan inte publiceras. Publiceringsalternativen i redigeraren är bara tillgängliga för sidor som du kommer åt via de faktiska sökvägarna.

### Publicera från konsolen {#publishing-from-the-console}

I platskonsolen finns det två alternativ för publicering:

* [Snabbpublicering](#quick-publish)
* [Hantera publikation](#manage-publication)

#### Snabbpublicering {#quick-publish}

**Snabbpublicering** är för enkla fall och publicerar den eller de markerade sidorna omedelbart utan ytterligare interaktion. Därför kommer alla icke-publicerade referenser också att publiceras automatiskt.

Så här publicerar du en sida med Snabbpublicering:

1. Markera sidan eller sidorna i webbplatskonsolen och klicka på **Snabbpublicering** -knappen.

   ![Välja sidor för publicering](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. Bekräfta publikationen genom att klicka på **Publicera** eller avbryta genom att klicka på **Avbryt**. Kom ihåg att alla opublicerade referenser också publiceras automatiskt.

   ![Snabbpubliceringsbekräftelse](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. När sidan publiceras visas en varning som bekräftar publiceringen.

>[!NOTE]
>
>Snabbpublicering är en ytlig publicering, d.v.s. endast den valda sidan/de markerade sidorna publiceras och inga underordnade sidor publiceras.

#### Hantera publikation {#manage-publication}

**Hantera publikation** erbjuder fler alternativ än **Snabbpublicering**, vilket gör det möjligt att inkludera underordnade sidor, anpassa referenserna och starta eventuella arbetsflöden och erbjuda möjlighet att publicera vid ett senare datum.

Så här publicerar eller avpublicerar du en sida med Hantera publikation:

1. Markera sidan eller sidorna i webbplatskonsolen och klicka på **Hantera publikation** -knappen.

   ![Välja sidor för publicering](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. Guiden **Hantera publikation** startar. Det första steget **Alternativ** kan du:

   * **Åtgärd**

     Välj om du vill publicera eller avpublicera de markerade sidorna.

   * **Schemaläggning**

     Välj om du vill utföra åtgärden nu eller vid ett senare datum.

     När du publicerar senare startas ett arbetsflöde för publicering av den eller de valda sidorna vid den angivna tidpunkten. Om du inte publicerar senare startas ett arbetsflöde för att avpublicera den eller de valda sidorna vid en viss tidpunkt.

     >[!NOTE]
     >
     >Om du vill avbryta en publicering/avpublicering senare går du till [Arbetsflödeskonsol](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) för att avsluta motsvarande arbetsflöde.

   ![Hantera publikationsalternativ](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

1. Klicka **Nästa** för att fortsätta.

1. I nästa steg i guiden Hantera publikation **Omfång** kan du definiera omfattningen för publikationen/avpublikationen, t.ex. inkludera underordnade sidor och/eller inkludera referenser.

   ![Hantera publikationsomfång](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   **Lägg till innehåll**

   Du kan använda knappen **Lägg till innehåll** för att lägga till ytterligare sidor i listan över sidor som ska publiceras, om du inte valde någon innan du startade guiden Hantera publikation.

   Markera **Lägg till innehåll** knappen startar [sökvägsläsare](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser) för att tillåta innehållsval.

   Markera önskade sidor och klicka sedan på **Välj** för att lägga till innehåll i guiden eller **Avbryt** om du vill avbryta markeringen och återgå till guiden.

   **Ta bort markering**

   I guiden kan du markera ett objekt i listan för att ta bort det från markeringen.

   ![Hantera publikationsmarkering av sidor](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **Publicerade referenser**

   Du kan visa och ändra referenserna som ska publiceras eller inte publiceras för en sida genom att markera den och sedan klicka på **Publicerade referenser** -knappen.

   ![Hantera publikationsalternativ](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   The **Publicerade referenser** visas referenserna för det markerade innehållet. Som standard är alla markerade och publicerade/opublicerade, men du kan avmarkera dem genom att avmarkera dem så att de inte tas med i funktionsmakrot.

   Klicka **Klar** för att spara dina ändringar eller **Avbryt** om du vill avbryta markeringen och återgå till guiden.

   Tillbaka i guiden **Referenser** kolumnen uppdateras för att återspegla ditt val av referenser som ska publiceras eller inte publiceras.

   ![Hantera publikationsmarkering av sidor](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **Inkludera underordnade**

   >[!NOTE]
   >
   >Se [Publicera och avpublicera ett träd](#publishing-and-unpublishing-a-tree)

   Klicka **Inkludera underordnade** öppnar en dialogruta där du kan:

   * **Inkludera underordnade**
   * **Inkludera endast omedelbart underordnade**
   * **Inkludera endast ändrade sidor**
   * **Inkludera endast redan publicerade sidor**

   Aktivera önskade alternativ och bekräfta med **OK** om du vill lägga till de underordnade sidorna i listan med sidor som ska publiceras eller avpubliceras baserat på markeringsalternativen. Klicka **Avbryt** om du vill avbryta markeringen och återgå till guiden.

   ![Hantera publikation inklusive underordnade](/help/sites-cloud/authoring/assets/publishing-include-children.png)

1. Klicka **Publicera** för att slutföra.

   I webbplatskonsolen bekräftar ett meddelande publikationen.

1. Om de publicerade sidorna är kopplade till arbetsflöden kan de visas i en **Arbetsflöden** steg i guiden.

   ![Hantera publikationsmarkering av sidor](/help/sites-cloud/authoring/assets/publishing-manage-publication-workflow.png)

   >[!NOTE]
   >
   >The **Arbetsflöden** visas baserat på vilka rättigheter din användare har eller inte har. Se föregående kommentar på den här sidan om publiceringsrättigheter och Hantera åtkomst till arbetsflöden och [Använda arbetsflöden på sidor](/help/sites-cloud/authoring/workflows/applying.md) för mer information.

   Resurserna grupperas efter de arbetsflöden som utlöses och de olika alternativen:

   * Definiera arbetsflödets rubrik.
   * Behåll arbetsflödespaketet, förutsatt att arbetsflödet har stöd för flera resurser.
   * Definiera en titel på arbetsflödespaketet om alternativet att behålla arbetsflödespaketet har valts.

1. Klicka på **Publicera** eller **Publicera senare** för att slutföra publiceringen.

## Avpublicerar sidor {#unpublishing-pages}

Om du avpublicerar en sida tas den bort från publiceringen, eller [förhandsgranska](/help/sites-cloud/authoring/fundamentals/previewing-content.md), så att den inte längre är tillgänglig för läsarna.

I en [liknande publiceringssätt](#publishing-pages), en eller flera sidor kan avpubliceras från det önskade målet:

* [Från sidredigeraren](#unpublishing-from-the-editor)
* [Från webbplatskonsolen](#unpublishing-from-the-console)

### Avpublicera från redigeraren {#unpublishing-from-the-editor}

Om du vill avpublicera en sida när du redigerar den väljer du **Avpublicera sida** i **Sidinformation** meny, som du skulle [publicera sidan](#publishing-from-the-editor).

>[!NOTE]
>
>Sidor som används av [alias](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced) i redigeraren kan inte avpubliceras. Publiceringsalternativen i redigeraren är bara tillgängliga för sidor som du kommer åt via de faktiska sökvägarna.

### Avpublicera från konsolen {#unpublishing-from-the-console}

Precis som du [publicera med alternativet Hantera publikation](#manage-publication)kan du också använda den för att avpublicera.

1. Markera sidan eller sidorna i webbplatskonsolen och klicka på **Hantera publikation** -knappen.
1. Guiden **Hantera publikation** startar. I det första steget **Alternativ** väljer du **Avpublicera** i stället för standardalternativet **Publicera**.

   ![Avpublicering - alternativ](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   På samma sätt som publiceringen senare startar ett arbetsflöde för att publicera den här versionen av sidan vid den angivna tidpunkten, startar inaktiveringen senare ett arbetsflöde för att avpublicera den valda sidan eller de valda sidorna vid en viss tidpunkt.

   >[!NOTE]
   >
   >Om du vill avbryta en publicering/avpublicering senare går du till [Arbetsflödeskonsol](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) för att avsluta motsvarande arbetsflöde.

   >[!NOTE]
   >Om du har en [Förhandsgranska](/help/sites-cloud/authoring/fundamentals/previewing-content.md) -miljö kan du välja **Mål** under Hantera publicering.

1. Slutför borttagningen genom att fortsätta med guiden på samma sätt som du gör [publicera sidan](#manage-publication).

   ![Avpublicering - omfång](/help/sites-cloud/authoring/assets/publishing-unpublish-scope.png)

## Publicera och avpublicera ett träd {#publishing-and-unpublishing-a-tree}

När du har angett eller uppdaterat ett stort antal innehållssidor, som alla finns på samma rotsida, kan det vara enklare att publicera hela trädet i en enda åtgärd.

Du kan använda [Hantera publikation](#manage-publication) på webbplatskonsolen för att göra detta.

1. I webbplatskonsolen väljer du rotsidan för trädet som du vill publicera eller avpublicera och väljer **Hantera publikation**.
1. Guiden **Hantera publikation** startar. Välj om du vill publicera eller avpublicera och när det ska ske och välj **Nästa** för att fortsätta.
1. I **Omfång** markerar du rotsidan och väljer **Inkludera underordnade**.

   ![Hantera publikationsmarkering av sidor](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. I **Inkludera underordnade** dialog:

   * välj **Inkludera underordnade**
   * avmarkera **Inkludera endast omedelbart underordnade**
   * avmarkera **Inkludera endast redan publicerade sidor**
   * konfigurera **Inkludera endast ändrade sidor** efter behov

   Dessa alternativ är markerade som standard, så du måste komma ihåg att konfigurera dem. Bekräfta markeringen med **OK** om du vill lägga till innehållet i publikationen/avpublikationen.

   ![Inkludera underordnade för trädpublicering](/help/sites-cloud/authoring/assets/publishing-include-children-tree.png)

1. I **Hantera publikation** kan du anpassa markeringen ytterligare genom att lägga till ytterligare sidor eller ta bort de markerade sidorna.

   Kom ihåg att du även kan granska referenser som ska publiceras via **Publicerade referenser** alternativ.

1. [Fortsätt med guiden Hantera publikation som vanligt](#manage-publication) för att slutföra publikationen eller avpubliceringen av trädet.

## Bestämmer publiceringsstatus {#determining-publication-status}

Du kan ange en sidas publiceringsstatus:

* I [resursöversiktsinformation på webbplatskonsolen](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

  ![Publikationsstatus i kortvyn](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

  Publikationsstatusen visas i [kort](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view)-, [kolumn](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)- och [list](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)vyerna i Sites-konsolen.

* I [tidslinje](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)

  ![Publiceringsstatus i tidslinjevyn](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* I [Sidinformation-menyn](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) när du redigerar en sida

  ![Publiceringsstatus på menyn Sidinformation](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
