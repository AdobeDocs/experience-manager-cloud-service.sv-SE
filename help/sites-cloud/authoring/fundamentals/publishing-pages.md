---
title: Publicera sidor
description: Publicera och avpublicera sidor med AEM
translation-type: tm+mt
source-git-commit: abb45225e880f3d08b9d26c29e243037564acef0
workflow-type: tm+mt
source-wordcount: '1717'
ht-degree: 5%

---


# Publicera sidor {#publishing-pages}

När du har skapat och granskat ditt innehåll i författarmiljön är målet att [göra det tillgängligt på din offentliga webbplats](/help/sites-cloud/authoring/getting-started/concepts.md) (din publiceringsmiljö).

Detta kallas att publicera en sida. När du vill ta bort en sida från publiceringsmiljön kallas det för att avpublicera. När sidan publiceras och avpubliceras är den fortfarande tillgänglig i redigeringsmiljön för ytterligare ändringar tills du tar bort den.

Du kan publicera/avpublicera en sida direkt eller vid ett fördefinierat datum/tid i framtiden.

## Terminologi {#terminology}

Du kan stöta på olika termer om publicering när du arbetar med Adobe Experience Manager (AEM) som Cloud Service.

* **Publicera/avpublicera**
   * Detta är de primära villkoren för de åtgärder som gör innehållet tillgängligt för allmänheten i publiceringsmiljön (eller inte).
   * Detta är de termer som används i AEM.
* **Aktivera/inaktivera**
   * Dessa termer är synonyma med publicera/avpublicera.
   * Dessa termer användes i tidigare versioner av AEM.
* **Replikering/replikering**
   * Detta är de tekniska termer som beskriver hur data flyttas (t.ex. sidinnehåll, filer, kod, användarkommentarer) från en miljö till en annan när du publicerar en sida.
   * Dessa termer används främst av utvecklare.

## Publicera sidor {#publishing-pages-1}

Beroende på var du befinner dig kan du publicera:

* [Från sidredigeraren](#publishing-from-the-editor)
* [Från webbplatskonsolen](#publishing-from-the-console)

>[!NOTE]
>
>Om du inte har behörighet att publicera en viss sida:
>
>* Ett arbetsflöde kommer att utlösas för att meddela lämplig person om din begäran om publicering.
>* Det här arbetsflödet kan ha anpassats av ditt utvecklingsteam.
>* Ett meddelande visas kort för att meddela dig att arbetsflödet har utlösts.


<!--
>* This [workflow may have been customized](/help/sites-developing/workflows-models.md#main-pars-procedure-6fe6) by your development team.
>* A message will be displayed briefly to notify you that the workflow was triggered.
-->

>[!NOTE]
>
> Ytterligare möjligheter finns under **I tid** och **annan tid** på fliken [Grundläggande i Sidegenskaper](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)

### Publicera från Redigeraren {#publishing-from-the-editor}

Om du redigerar en sida kan den publiceras direkt från redigeraren.

1. Välj ikonen **Sidinformation** för att öppna menyn och sedan alternativet **Publicera sida** .

   ![Publicera en sida via sidalternativ](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. Beroende på om sidan har referenser som behöver publiceras:

   * Sidan publiceras direkt om det inte finns några referenser att publicera.
   * Om sidan innehåller referenser som behöver publiceras visas dessa i **publiceringsguiden** där du kan antingen:
      * Ange vilket av resurserna/taggarna/etc. du vill publicera tillsammans med sidan och sedan använda **Publicera** för att slutföra processen.
      * Använd **Avbryt** om du vill avbryta åtgärden.

   ![Publicera referenser med sidan](/help/sites-cloud/authoring/assets/publishing-references.png)

1. Om du väljer **Publicera** kommer sidan att replikeras till publiceringsmiljön. I sidredigeraren visas en informationsbanderoll som bekräftar publiceringsåtgärden.

   ![Banderoll för publiceringsstatusinformation](/help/sites-cloud/authoring/assets/publishing-info.png)

   När du visar samma sida i konsolen visas den uppdaterade publiceringsstatusen.

   ![Sidpubliceringsstatus i kolumnvy i platskonsolen](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>Publicering från redigeraren är en ytlig publicering, d.v.s. endast den valda sidan/de markerade sidorna publiceras och eventuella underordnade sidor publiceras/inte.

### Publicera från konsolen {#publishing-from-the-console}

I platskonsolen finns det två alternativ för publicering:

* [Snabbpublicering](#quick-publish)
* [Hantera publikation](#manage-publication)

#### Snabbpublicering {#quick-publish}

**Snabbpublicering** är avsett för enkla ärenden och publicerar den eller de markerade sidorna direkt utan ytterligare interaktion. Därför kommer alla icke-publicerade referenser också att publiceras automatiskt.

Så här publicerar du en sida med Snabbpublicering:

1. Markera sidan eller sidorna i webbplatskonsolen och klicka på knappen **Snabbpublicering** .

   ![Välja sidor för publicering](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. I dialogrutan Snabbpublicering bekräftar du publikationen genom att klicka på **Publicera** eller Avbryt genom att klicka på **Avbryt**. Kom ihåg att alla opublicerade referenser också publiceras automatiskt.

   ![Snabbpubliceringsbekräftelse](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. När sidan publiceras visas en varning som bekräftar publiceringen.

>[!NOTE]
>
>Snabbpublicering är en grund publicering, d.v.s. endast den valda sidan/de markerade sidorna publiceras och inga underordnade sidor publiceras.

#### Hantera publikation {#manage-publication}

**Med Hantera publikation** får du fler alternativ än Snabbpublicering, så att du kan inkludera underordnade sidor, anpassa referenserna och starta tillämpliga arbetsflöden samt erbjuda möjlighet att publicera vid ett senare tillfälle.

Så här publicerar eller avpublicerar du en sida med Hantera publikation:

1. Markera sidan eller sidorna i webbplatskonsolen och klicka på knappen **Hantera publikation** .

   ![Välja sidor för publicering](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. Guiden **Hantera publikation** startar. I det första steget, **Alternativ**, kan du:

   * Välj om du vill publicera eller avpublicera de markerade sidorna.
   * Välj om du vill utföra åtgärden nu eller vid ett senare datum.

   När du publicerar senare startas ett arbetsflöde för publicering av den eller de valda sidorna vid den angivna tidpunkten. Om du inte publicerar senare startas ett arbetsflöde för att avpublicera den eller de valda sidorna vid en viss tidpunkt.

   Om du vill avbryta en publicering/avpublicering senare går du till arbetsflödeskonsolen och avslutar motsvarande arbetsflöde. <!--If you want to cancel a publish/unpublish later, go to the [Workflow Console](/help/sites-administering/workflows.md) to terminate the corresponding workflow.-->

   ![Hantera publikationsalternativ](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

   Klicka på **Nästa** för att fortsätta.

1. I nästa steg i guiden Hantera publikation, **Omfång**, kan du definiera omfattningen för publikationen/borttagningen av publikationen, t.ex. inkludera underordnade sidor och/eller inkludera referenser.

   ![Hantera publikationsomfång](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   Du kan använda knappen **Lägg till innehåll** för att lägga till ytterligare sidor i listan över sidor som ska publiceras, om du inte valde någon innan du startade guiden Hantera publikation.

   När du klickar på knappen Lägg till innehåll startas [sökvägsläsaren](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser) så att du kan välja innehåll.

   Markera önskade sidor och klicka sedan på **Välj** för att lägga till innehållet i guiden eller **Avbryt** för att avbryta valet och återgå till guiden.

   I guiden kan du markera ett objekt i listan för att konfigurera ytterligare alternativ, till exempel:

   * Inkludera dess underordnade.
   * Ta bort den från markeringen.
   * Hantera dess publicerade referenser.

   ![Hantera publikationsmarkering av sidor](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   När du klickar på **Inkludera underordnade** öppnas en dialogruta där du kan:

   * Inkludera endast omedelbara barn.
   * Inkludera endast ändrade sidor.
   * Inkludera endast redan publicerade sidor.

   Klicka på **Lägg** till för att lägga till underordnade sidor i listan över sidor som ska publiceras eller avpubliceras baserat på de valda alternativen. Klicka på **Avbryt** om du vill avbryta markeringen och återgå till guiden.

   ![Hantera publikation inklusive underordnade](/help/sites-cloud/authoring/assets/publishing-include-children.png)

   När du återgår till guiden visas de sidor som lagts till baserat på dina val i dialogrutan Inkludera underordnade.

   Du kan visa och ändra referenserna som ska publiceras eller avpubliceras för en sida genom att markera den och sedan klicka på knappen **Publicerade referenser** .

   ![Hantera publikationsalternativ](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   I dialogrutan **Publicerade referenser** visas referenser för det markerade innehållet. Som standard är alla markerade och publiceras/avpubliceras, men du kan avmarkera dem så att de inte tas med i funktionsmakrot.

   Klicka på **Klar** om du vill spara ändringarna eller **Avbryt** om du vill avbryta markeringen och återgå till guiden.

   I guiden uppdateras kolumnen **Referenser** så att den återspeglar ditt val av referenser som ska publiceras eller avpubliceras.

   ![Hantera publikationsmarkering av sidor](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. Klicka på **Publicera** för att slutföra.

   I webbplatskonsolen bekräftar ett meddelande publikationen.

1. Om de publicerade sidorna är kopplade till arbetsflöden kan de visas i ett **arbetsflödessteg** i publikationsguiden.

   >[!NOTE]
   >
   >Steget **Arbetsflöden** visas baserat på vilka rättigheter användaren har eller inte har. Mer information finns i föregående kommentar på den här sidan om publiceringsbehörigheter samt Hantera åtkomst till arbetsflöden och [Använda arbetsflöden på sidor](/help/sites-cloud/authoring/workflows/applying.md) .
   <!--
   >The **Workflows** step will be shown based on what rights your user may or may not have. See the previous note on this page regarding publishing privileges as well as [Managing Access to Workflows](/help/sites-administering/workflows-managing.md) and [Applying Workflows to Pages](/help/sites-cloud/authoring/workflows/applying.md) for details.
   -->

   Resurserna grupperas efter de arbetsflöden som utlöses och de olika alternativen:

   * Definiera arbetsflödets rubrik.
   * Behåll arbetsflödespaketet, förutsatt att arbetsflödet har stöd för flera resurser.

   <!--Keep the workflow package, provided that the workflow has [multi-resource support](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support).
    -->

   * Definiera en titel på arbetsflödespaketet om alternativet att behålla arbetsflödespaketet har valts.

   Klicka på **Publicera** eller **Publicera senare** för att slutföra publiceringen.

## Avpublicerar sidor {#unpublishing-pages}

Om du avpublicerar en sida tas den bort från publiceringsmiljön så att den inte längre är tillgänglig för läsarna.

På ett [sätt som liknar publicering](#publishing-pages)kan en eller flera sidor avpubliceras:

* [Från sidredigeraren](#unpublishing-from-the-editor)
* [Från webbplatskonsolen](#unpublishing-from-the-console)

### Avpublicera från redigeraren {#unpublishing-from-the-editor}

När du redigerar en sida och vill avpublicera den väljer du **Avpublicera sida** på menyn **Sidinformation** , på samma sätt som du skulle [publicera sidan](#publishing-from-the-editor).

### Avpublicera från konsolen {#unpublishing-from-the-console}

På samma sätt som du [använder alternativet Hantera publikation för att publicera](#manage-publication)kan du även använda det för att avpublicera.

1. Markera sidan eller sidorna i webbplatskonsolen och klicka på knappen **Hantera publikation** .
1. Guiden **Hantera publikation** startar. I det första steget **Alternativ** väljer du **Avpublicera** i stället för standardalternativet **Publicera**.

   ![Avpublicerar](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   På samma sätt som publiceringen senare startar ett arbetsflöde för att publicera den här versionen av sidan vid den angivna tidpunkten, startar inaktiveringen senare ett arbetsflöde för att avpublicera den valda sidan eller de valda sidorna vid en viss tidpunkt.

   Om du vill avbryta en publicering/avpublicering senare går du till arbetsflödeskonsolen och avslutar motsvarande arbetsflöde. <!--If you want to cancel a publish/unpublish later, go to the [Workflow Console](/help/sites-administering/workflows.md) to terminate the corresponding workflow.-->

1. Slutför den borttagna publikationen genom att fortsätta med guiden på samma sätt som du [publicerar sidan](#manage-publication).

## Publicera och avpublicera ett träd {#publishing-and-unpublishing-a-tree}

När du har angett eller uppdaterat ett stort antal innehållssidor, som alla finns på samma rotsida, kan det vara enklare att publicera hela trädet i en åtgärd.

Du kan använda alternativet [Hantera publikation](#manage-publication) på webbplatskonsolen för att göra detta.

1. I webbplatskonsolen väljer du rotsidan för det träd som du vill publicera eller avpublicera och väljer **Hantera publikation**.
1. Guiden **Hantera publikation** startar. Välj om du vill publicera eller avpublicera och när det ska ske och välj **Nästa** för att fortsätta.
1. Markera rotsidan i **omfångssteget** och välj **Inkludera underordnade**.

   ![Hantera publikationsmarkering av sidor](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. Avmarkera alternativen i dialogrutan **Inkludera underordnade** :

   * Inkludera endast omedelbart underordnade
   * Inkludera endast redan publicerade sidor

   Dessa alternativ är markerade som standard, så du måste komma ihåg att avmarkera dem. Klicka på **Lägg** till för att bekräfta och lägga till innehållet i publikationen/avpublikationen.

   ![Inkludera barn vid avpublicering](/help/sites-cloud/authoring/assets/publishing-tree-children.png)

1. Guiden **Hantera publikation** visar innehållet i trädet för granskning. Du kan anpassa markeringen ytterligare genom att lägga till ytterligare sidor eller ta bort de markerade sidorna.

   ![Hantera publikationsalternativ](/help/sites-cloud/authoring/assets/publishing-tree-select.png)

   Kom ihåg att du även kan granska referenser som ska publiceras via alternativet **Publicerade referenser** .

1. [Fortsätt med guiden Hantera publikation som vanligt](#manage-publication) för att slutföra publikationen eller ta bort publiceringen av trädet.

## Bestämmer publiceringsstatus {#determining-publication-status}

Du kan ange en sidas publiceringsstatus:

* I [resursöversiktsinformationen på platskonsolen](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   ![Publikationsstatus i kortvyn](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

   Publikationsstatusen visas i [kort](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view)-, [kolumn](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view)- och [list](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view)vyerna i Sites-konsolen.

* På [tidslinjen](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)

   ![Publiceringsstatus i tidslinjevyn](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* På menyn [](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) Sidinformation när du redigerar en sida

   ![Publiceringsstatus på menyn Sidinformation](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
