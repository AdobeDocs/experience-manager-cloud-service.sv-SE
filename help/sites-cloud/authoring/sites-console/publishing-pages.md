---
title: Publicera sidor
description: Lär dig hur du publicerar och avpublicerar sidor med olika mekanismer i AEM.
exl-id: 89f2363c-7922-4ca5-92cb-cbee6a393ee3
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1936'
ht-degree: 4%

---

# Publicera sidor {#publishing-pages}

När du har skapat och granskat ditt innehåll i författarmiljön är målet att [göra det tillgängligt på din offentliga webbplats](/help/sites-cloud/authoring/author-publish.md) (din publiceringsmiljö).

Detta kallas att publicera en sida. När du vill ta bort en sida från publiceringsmiljön kallas det för att avpublicera. När sidan publiceras och avpubliceras är den fortfarande tillgänglig i redigeringsmiljön för ytterligare ändringar tills du tar bort den.

Du kan publicera/avpublicera en sida direkt eller vid ett fördefinierat datum/tid i framtiden.

>[!NOTE]
>
>När du publicerar ett Experience Fragment följer du i princip samma procedur som när du publicerar en sida, även om du väljer Experience Fragments-konsolen eller redigeraren.

## Terminologi {#terminology}

Du kan stöta på olika termer om publicering när du arbetar med Adobe Experience Manager (AEM) as a Cloud Service.

* **Publish/Avpublicera**
   * Detta är de primära villkoren för de åtgärder som gör innehållet tillgängligt för allmänheten i publiceringsmiljön (eller inte).
   * Detta är de termer som används i AEM.
* **Aktivera/inaktivera**
   * Dessa termer är synonyma med publicera/avpublicera.
   * Dessa termer användes i tidigare versioner av AEM.
* **Replikera/replikera**
   * Detta är de tekniska termer som beskriver hur data flyttas (till exempel sidinnehåll, filer, kod, användarkommentarer) från en miljö till en annan när du publicerar en sida.
   * Dessa termer används främst av utvecklare.

## Publicera sidor {#publishing-pages-1}

Beroende på din plats kan du publicera:

* [Från sidredigeraren](#publishing-from-the-page-editor)
* [Från ](#publishing-from-the-sites-console)
* [Från den universella redigeraren](/help/sites-cloud/authoring/universal-editor/publishing.md)

>[!NOTE]
>
>Om du inte har behörighet att publicera en viss sida:
>
>* Ett arbetsflöde aktiveras för att meddela lämplig person om din begäran om publicering.
>* Det här arbetsflödet kan ha anpassats av ditt utvecklingsteam.
>* Ett meddelande visas kort för att meddela dig att arbetsflödet har utlösts.

>[!NOTE]
>
>Om du vill bevara sidordningen måste du använda [Hantera publikation](#manage-publication) för att publicera den överordnade sidan tillsammans med eventuella underordnade sidor i en enda åtgärd.
>
>Sidordningen garanteras inte:
>* om endast underordnade sidor har valts för publicering (som orderinformationen finns på den överordnade sidan)
>* om de överordnade och underordnade sidorna publiceras i separata åtgärder

>[!NOTE]
>
> Mer information finns i **På tid** och **Från tid** på fliken [Grundläggande i Sidegenskaper](/help/sites-cloud/authoring/sites-console/page-properties.md#basic)

### Publicera från sidredigeraren {#publishing-from-the-page-editor}

Om du redigerar en sida i [sidredigeraren](/help/sites-cloud/authoring/page-editor/introduction.md) kan den publiceras direkt från redigeraren.

1. Välj ikonen **Sidinformation** för att öppna menyn och sedan alternativet **Publish Page** .

   ![Publicera en sida via sidalternativ](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. Beroende på om sidan har referenser som behöver publiceras:

   * Sidan publiceras direkt om det inte finns några referenser att publicera.
   * Om sidan innehåller referenser som behöver publiceras visas dessa i guiden **Publish** där du kan antingen:
      * Ange vilka resurser, eller taggar och så vidare, som du vill publicera tillsammans med sidan och använd sedan **Publish** för att slutföra processen.
      * Använd **Avbryt** om du vill avbryta åtgärden.

   ![Publicerar referenser med sidan](/help/sites-cloud/authoring/assets/publishing-references.png)

1. Om du väljer **Publish** replikeras sidan till publiceringsmiljön. I sidredigeraren visas en informationsbanderoll som bekräftar publiceringsåtgärden.

   ![Banderoll för Publish-statusinformation](/help/sites-cloud/authoring/assets/publishing-info.png)

   När du visar samma sida i konsolen visas den uppdaterade publiceringsstatusen.

   ![Sidpubliceringsstatus i kolumnvy i webbplatskonsolen](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>Publicering från sidredigeraren är en ytlig publicering, d.v.s. endast den valda sidan/de markerade sidorna publiceras och eventuella underordnade sidor publiceras/inte.

>[!NOTE]
>
>Sidor som används av [alias](/help/sites-cloud/authoring/sites-console/page-properties.md#advanced) i redigeraren kan inte publiceras. Publish-alternativen i redigeraren är bara tillgängliga för sidor som du kommer åt via de faktiska sökvägarna.

### Publicera från Site Console {#publishing-from-the-sites-console}

I konsolen **Platser** finns det två alternativ för publicering:

* [Snabb Publish](#quick-publish)
* [Hantera publikation](#manage-publication)

#### Snabb Publish {#quick-publish}

**Snabba Publish** är till för enkla ärenden och publicerar de markerade sidorna direkt utan ytterligare interaktion. Därför kommer alla icke-publicerade referenser också att publiceras automatiskt.

Så här publicerar du en sida med Quick Publish:

1. Markera sidan eller sidorna i webbplatskonsolen och klicka på knappen **Snabba Publish** .

   ![Välja sidor för publicering](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. Bekräfta publikationen genom att klicka på **Publish** i dialogrutan Snabb Publish eller klicka på **Avbryt**. Kom ihåg att alla opublicerade referenser också publiceras automatiskt.

   ![Snabbpubliceringsbekräftelse](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. När sidan publiceras visas en varning som bekräftar publiceringen.

>[!NOTE]
>
>Quick Publish är en ytlig publicering, d.v.s. endast den markerade sidan/de markerade sidorna publiceras och inga underordnade sidor publiceras.

#### Hantera publikation {#manage-publication}

**Hantera publikation** har fler alternativ än **Snabb-publicering**, vilket gör det möjligt att inkludera underordnade sidor, anpassa referenserna och starta eventuella arbetsflöden och erbjuda möjlighet att publicera vid ett senare datum.

>[!NOTE]
>
>Om du vill bevara sidordningen måste du använda **Hantera publikation** för att publicera den överordnade sidan tillsammans med eventuella underordnade sidor i en enda åtgärd.
>
>Sidordningen garanteras inte:
>* om endast underordnade sidor har valts för publicering (som orderinformationen finns på den överordnade sidan)
>* om de överordnade och underordnade sidorna publiceras i separata åtgärder

Så här publicerar eller avpublicerar du en sida med Hantera publikation:

1. Markera sidan eller sidorna i webbplatskonsolen och klicka på knappen **Hantera publikation** .

   ![Välja sidor för publicering](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. Guiden **Hantera publikation** startar. I det första steget, **Alternativ**, kan du:

   * **Åtgärd**

     Välj om du vill publicera eller avpublicera de markerade sidorna.

   * **Schemaläggning**

     Välj om du vill utföra åtgärden nu eller vid ett senare datum.

     När du publicerar senare startas ett arbetsflöde för publicering av den eller de valda sidorna vid den angivna tidpunkten. Om du inte publicerar senare startas ett arbetsflöde för att avpublicera den eller de valda sidorna vid en viss tidpunkt.

     >[!NOTE]
     >
     >Om du vill avbryta en publicering/avpublicering senare går du till [arbetsflödeskonsolen](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) och avslutar motsvarande arbetsflöde.

   ![Hantera publikationsalternativ](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

1. Klicka på **Nästa** för att fortsätta.

1. I nästa steg i guiden Hantera publikation, **Omfång**, kan du definiera omfattningen för publikationen/avpublikationen, till exempel att inkludera underordnade sidor och/eller inkludera referenser.

   ![Hantera publikationsomfång](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   **Lägg till innehåll**

   Du kan använda knappen **Lägg till innehåll** för att lägga till ytterligare sidor i listan över sidor som ska publiceras, om du inte valde någon innan du startade guiden Hantera publikation.

   Om du väljer knappen **Lägg till innehåll** startas [sökvägsläsaren](/help/sites-cloud/authoring/path-selection.md) så att innehåll kan väljas.

   Markera önskade sidor och klicka sedan på **Välj** för att lägga till innehållet i guiden eller **Avbryt** för att avbryta valet och återgå till guiden.

   **Ta bort markering**

   I guiden kan du markera ett objekt i listan för att ta bort det från markeringen.

   ![Hantera publikation, välja sidor](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **Publicerade referenser**

   Du kan visa och ändra referenserna som ska publiceras eller avpubliceras för en sida genom att markera den och sedan klicka på knappen **Publicerade referenser** .

   ![Hantera publikationsalternativ](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   I dialogrutan **Publicerade referenser** visas referenser för det markerade innehållet. Som standard är alla markerade och publicerade/opublicerade, men du kan avmarkera dem genom att avmarkera dem så att de inte tas med i funktionsmakrot.

   Klicka på **Klar** om du vill spara ändringarna eller på **Avbryt** om du vill avbryta markeringen och återgå till guiden.

   I guiden uppdateras kolumnen **Referenser** så att den återspeglar ditt val av referenser som ska publiceras eller avpubliceras.

   ![Hantera publikation, välja sidor](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **Inkludera underordnade**

   >[!NOTE]
   >
   >Se [Publicera och avpublicera ett träd](#publishing-and-unpublishing-a-tree)

   Om du klickar på **Inkludera underordnade** öppnas en dialogruta där du kan:

   * **Inkludera underordnade**
   * **Inkludera endast omedelbart underordnade**
   * **Inkludera endast ändrade sidor**
   * **Ta endast med redan publicerade sidor**

   Aktivera de nödvändiga alternativen och bekräfta med **OK** för att lägga till de underordnade sidorna i listan över sidor som ska publiceras eller avpubliceras baserat på de valda alternativen. Klicka på **Avbryt** om du vill avbryta markeringen och återgå till guiden.

   ![Hantera publikation inklusive underordnade](/help/sites-cloud/authoring/assets/publishing-include-children.png)

1. Klicka på **Publish** för att slutföra.

   I webbplatskonsolen bekräftar ett meddelande publikationen.

1. Om de publicerade sidorna är kopplade till arbetsflöden kan de visas i ett slutligt **arbetsflödessteg** i publikationsguiden.

   ![Hantera publikation, välja sidor](/help/sites-cloud/authoring/assets/publishing-manage-publication-workflow.png)

   >[!NOTE]
   >
   >Steget **Arbetsflöden** visas baserat på vilka rättigheter din användare har eller inte har. Mer information finns i föregående kommentar på den här sidan om publiceringsbehörigheter och hanterad åtkomst till arbetsflöden och [Tillämpa arbetsflöden på sidor](/help/sites-cloud/authoring/workflows/applying.md).

   Resurserna grupperas efter de arbetsflöden som utlöses och de olika alternativen:

   * Definiera arbetsflödets rubrik.
   * Behåll arbetsflödespaketet, förutsatt att arbetsflödet har stöd för flera resurser.
   * Definiera en titel på arbetsflödespaketet om alternativet att behålla arbetsflödespaketet har valts.

1. Klicka på **Publicera** eller **Publicera senare** för att slutföra publiceringen.

## Avpublicerar sidor {#unpublishing-pages}

Om du avpublicerar en sida tas den bort från publiceringsmiljön eller [förhandsvisningen](/help/sites-cloud/authoring/sites-console/previewing-content.md) så att den inte längre är tillgänglig för läsarna.

På ett [sätt som liknar publicering](#publishing-pages) kan en eller flera sidor avpubliceras från det önskade målet:

* [Från sidredigeraren](#unpublishing-from-the-editor)
* [Från webbplatskonsolen](#unpublishing-from-the-console)

### Avpublicera från redigeraren {#unpublishing-from-the-editor}

Om du vill avpublicera en sida när du redigerar den väljer du **Avpublicera sida** på menyn **Sidinformation**, på samma sätt som du [publicerar sidan](#publishing-from-the-editor).

>[!NOTE]
>
>Sidor som används av [alias](/help/sites-cloud/authoring/sites-console/page-properties.md#advanced) i redigeraren kan inte avpubliceras. Publish-alternativen i redigeraren är bara tillgängliga för sidor som du kommer åt via de faktiska sökvägarna.

### Avpublicera från konsolen {#unpublishing-from-the-console}

Precis som du [använder alternativet Hantera publikation för att publicera](#manage-publication) kan du även använda det för att avpublicera.

1. Markera sidan eller sidorna i webbplatskonsolen och klicka på knappen **Hantera publikation** .
1. Guiden **Hantera publikation** startar. I det första steget **Alternativ** väljer du **Avpublicera** i stället för standardalternativet **Publicera**.

   ![Avpublicering - alternativ](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   På samma sätt som publiceringen senare startar ett arbetsflöde för att publicera den här versionen av sidan vid den angivna tidpunkten, startar inaktiveringen senare ett arbetsflöde för att avpublicera den valda sidan eller de valda sidorna vid en viss tidpunkt.

   >[!NOTE]
   >
   >Om du vill avbryta en publicering/avpublicering senare går du till [arbetsflödeskonsolen](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) och avslutar motsvarande arbetsflöde.

   >[!NOTE]
   >Om du har en [förhandsvisningsmiljö](/help/sites-cloud/authoring/sites-console/previewing-content.md) kan du välja **Mål** under Hantera publikation.

1. Om du vill slutföra den borttagna publikationen fortsätter du med guiden på samma sätt som du [publicerar sidan](#manage-publication).

   ![Avpublicerar - scope](/help/sites-cloud/authoring/assets/publishing-unpublish-scope.png)

## Publicera och avpublicera ett träd {#publishing-and-unpublishing-a-tree}

När du har angett eller uppdaterat ett stort antal innehållssidor, som alla finns på samma rotsida, kan det vara enklare att publicera hela trädet i en enda åtgärd.

Du kan använda alternativet [Hantera publikation](#manage-publication) på webbplatskonsolen för att göra detta.

1. På webbplatskonsolen markerar du rotsidan för trädet som du vill publicera eller avpublicera och väljer **Hantera publikation**.
1. Guiden **Hantera publikation** startar. Välj om du vill publicera eller avpublicera och när det ska ske och välj **Nästa** för att fortsätta.
1. I steget **Omfång** markerar du rotsidan och väljer **Inkludera underordnade**.

   ![Hantera publikation, välja sidor](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. I dialogrutan **Inkludera underordnade**:

   * välj **Inkludera underordnade**
   * avmarkera **Ta endast med direkt underordnade**
   * avmarkera **Ta endast med redan publicerade sidor**
   * konfigurera **Inkludera endast ändrade sidor** efter behov

   Dessa alternativ är markerade som standard, så du måste komma ihåg att konfigurera dem. Bekräfta markeringen med **OK** om du vill lägga till innehållet i publikationen/avpublikationen.

   ![Inkluderar underordnade för trädpublikation](/help/sites-cloud/authoring/assets/publishing-include-children-tree.png)

1. I guiden **Hantera publikation** kan du anpassa markeringen ytterligare genom att lägga till ytterligare sidor eller ta bort de markerade sidorna.

   Kom ihåg att du även kan granska referenser som ska publiceras via alternativet **Publicerade referenser**.

1. [Fortsätt med guiden Hantera publikation som vanligt](#manage-publication) för att slutföra publikationen eller ta bort publikationen för trädet.

## Bestämmer publiceringsstatus {#determining-publication-status}

Du kan ange en sidas publiceringsstatus:

* I [resursöversiktsinformationen på webbplatskonsolen](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)

  ![Publikationsstatus i kortvyn](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

  Publikationsstatusen visas i [kort](/help/sites-cloud/authoring/basic-handling.md#card-view)-, [kolumn](/help/sites-cloud/authoring/basic-handling.md#column-view)- och [list](/help/sites-cloud/authoring/basic-handling.md#list-view)vyerna i Sites-konsolen.

* På tidslinjen [](/help/sites-cloud/authoring/basic-handling.md#timeline)

  ![Publiceringsstatus i tidslinjevyn](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* På menyn [Sidinformation](/help/sites-cloud/authoring/page-editor/introduction.md#page-information) när du redigerar en sida

  ![Publiceringsstatus på menyn Sidinformation](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
