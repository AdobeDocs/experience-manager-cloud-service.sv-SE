---
title: Publicera Forms för Edge Delivery Services
description: Lär dig hur formulärpublicering fungerar med Edge Delivery Services och hur du publicerar AEM formulär med Edge Delivery Services.
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
source-git-commit: bdc0e51a8b16df432f1f1aeabed11135fb8c8e0c
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 0%

---


# Publicera Forms för Edge Delivery Services

I den här artikeln får du hjälp med att publicera formulär till AEM Edge Delivery Services.
Om du vill publicera formulär till Edge Delivery Services måste du först upprätta en anslutning mellan AEM och GitHub-databasen. När du är ansluten kan du skapa formulären med den universella redigeraren, som följer en WYSIWYG-strategi (What You See Is What You Get) för en smidig och konsekvent användarupplevelse med Sites.

## Krav

* Har du inte använt Adaptive Forms tidigare? Konfigurera din GitHub-databas enligt [självstudiekursen](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project) som tillhandahålls.
* Om du redan använder Edge Delivery Services lägger du till den senaste versionen av [Adaptive Forms-blocket](/help/edge/docs/forms/tutorial.md#) i GitHub-databasen.
* Instansen AEM Forms Author innehåller en mall baserad på Edge Delivery Services. Kontrollera att den [senaste versionen av Core Components](https://github.com/adobe/aem-core-forms-components) är installerad i din miljö.
* Ha URL:en till din AEM Forms as a Cloud Service-författarinstans och din GitHub-databas till hands.

## Publish Forms för Edge Delivery Services

Så här publicerar du formulär för Edge Delivery Services:

[1. Länka GitHub-databasen till AEM instans](#link-github-repository-to-aem-instance)

[2. Länka AEM till GitHub-databasen.](#link-aem-instance-to-github-repository)

### Länka GitHub-databas till AEM instans

Så här länkar du [ditt projekt på GitHub-databasen](/help/edge/docs/forms/tutorial.md) till AEM Forms Author-instansen:

1. Gå till din GitHub-databas som du har skapat eller konfigurerat för dina Edge Delivery Services.
1. Öppna filen `fstab.yaml` för redigering.
1. Uppdatera filen `fstab.yaml` i GitHub-databasen med URL:en för din AEM Forms as a Cloud Service-instans.

   ```javascript
    mountpoints:
    /:
        url: [author-instance-url]/bin/franklin.delivery/[Github owner]/[Github Repository]/[Github branch] 
        type: "markup"
        suffix: ".html"
   ```

   Om din GitHub-databas till exempel heter &quot;aemcrosswalk&quot;, finns den under kontot &quot;wkndform&quot; och du använder &quot;main&quot;-grenen, ser författarinstansens URL ut så här:

   ```
        mountpoints:
            /:
            url: https://author-p133911-e1313554.adobeaemcloud.com/bin/franklin.delivery/wkndform/aemcrosswalk/main
            type: "markup"
            suffix: ".html"
   ```

1. Genomför ändringarna av filen `fstab.yaml`.

### Länka AEM till GitHub-databasen

Så här länkar du AEM Forms Author-instansen till [ditt projekt i GitHub-databasen](/help/edge/docs/forms/tutorial.md):

[1. Skapa ett adaptivt formulär baserat på mallen Edge Delivery Services](#1-create-an-adaptive-form-based-on-the-edge-delivery-services-template)

[2. Leta reda på formulärets konfigurationsbehållare i AEM författarinstans](#2-locate-your-forms-configuration-container-in-aem-author-instance)

[3. Skriv formuläret i den universella redigeraren](#3-author-the-form-in-the-universal-editor)

[4. Publish och förhandsgranska formuläret](#4-publish-and-preview-the-form)

#### 1. Skapa ett adaptivt formulär baserat på mallen Edge Delivery Services

1. Få åtkomst till din AEM Forms as a Cloud Service-författarinstans.
1. Välj **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.1. Välj **[!UICONTROL Create]** > **[!UICONTROL Adaptive Forms]**. Guiden öppnas. På fliken Source väljer du en formulärmall baserad på Edge Delivery Services:

   ![Skapa EDS Forms](/help/edge/assets/create-eds-forms.png){width=50%, align-center}

1. Klicka på **[!UICONTROL Create]** så visas guiden **Skapa formulär**.
1. Ange **GitHub-URL**. Om din GitHub-databas till exempel heter&quot;aemcrosswalk&quot;, finns den under kontot&quot;wkndform&quot;, är URL:en:
   `https://github.com/wkndform/aemcrosswalk`
1. Klicka på **[!UICONTROL Create]**.

   ![Guiden Skapa formulär](/help/edge/assets/create-form-wizard.png){width=50%, align-center}

   När du klickar på **[!UICONTROL Create]** öppnas formuläret i Universell redigerare för redigering.

   ![författare till formuläret](/help/edge/assets/author-form.png){width=50%, align-center}

   >[!NOTE]
   >
   > Konfigurationen av Edge Delivery Services för formulär som är baserade på mallen Edge Delivery Services skapas automatiskt i formulärets konfigurationsbehållare.

#### 2. Leta reda på formulärets konfigurationsbehållare i AEM författarinstans

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Edge Delivery Services Configuration]** på din AEM Forms as a Cloud Service författarinstans.
1. Välj den mapp som matchar formulärets namn. Om ditt formulär till exempel heter &#39;contact-us&#39; väljer du mappen `forms/contact-us` och väljer konfigurationen och publicerar konfigurationen:

   ![Konfiguration av Edge Delivery Services](/help/forms/assets/aem-instance-eds-configuration.png){width=50%, align-center}

1. Klicka på **[!UICONTROL Properties]** för att visa konfigurationen.\
   ![Automatiskt skapad konfiguration](/help/edge/assets/aem-forms-create-configuration-github.png){width=50%, align-center}

   Du kan lämna Edge Host-alternativet som det är. Formuläret publiceras både i förhandsgransknings- (.page) och live-miljöer (.live).

1. Klicka på **[!UICONTROL Save and Close]**. Konfigurationen sparas.

#### 3. Skriv formuläret i den universella redigeraren

När du klickar på **[!UICONTROL Create]** öppnas formuläret i den universella redigeraren för redigering.

1. Öppna innehållsläsaren och navigera till komponenten **[!UICONTROL Adaptive Form]** i **innehållsträdet**.

   ![innehållsträd](/help/edge/assets/content-tree.png){width=50%, align-center}

1. Klicka på ikonen **[!UICONTROL Add]** och lägg till de önskade komponenterna från listan **Adaptiva formulärkomponenter**.

   ![lägg till komponent](/help/edge/assets/add-component.png){width=50%, align-center}

1. Markera den tillagda adaptiva formulärkomponenten och uppdatera dess egenskaper med **[!UICONTROL Properties]**.

   ![öppna egenskaper](/help/edge/assets/component-properties.png){width=50%, align-center}

   Skärmbilden nedan visar det enkla&quot;Kontakta oss&quot;-formuläret som har skapats i den universella redigeraren:

   ![kontakta oss ](/help/edge/assets/contact-us.png){width=50%, align-center}

#### 4. Publish och förhandsgranska formuläret

Publicera formuläret till Edge Delivery Services genom att klicka på knappen **[!UICONTROL Publish]** i det övre högra hörnet av Universella redigerare.

![publicera formulär](/help/edge/assets/publish-form.png){width=50%, align-center}


Så här kommer du åt formuläret på Edge Delivery Services:

* **Mellanlagrad version (för testning)**: Den mellanlagrade versionen visar den opublicerade, fungerande versionen av formuläret för testning. Använd följande URL-format för att förhandsgranska formuläret innan det publiceras:

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  Om projektdatabasen till exempel heter&quot;aemcrosswalk&quot;, finns den under kontot&quot;wkndform&quot; och du använder huvudgrenen och formuläret som&quot;kontakta oss&quot;, ser den mellanlagrade versionen ut så här:
https://main—aemcrosswalk—wkndform.aem.page/content/forms/af/contact-us

* **Live-version (publicerat formulär)**:   Den aktiva versionen visar den senast publicerade versionen av formuläret, som är tillgänglig för slutanvändarna. Använd följande URL-format för att komma åt den publicerade, aktiva versionen av formuläret:

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  Om projektdatabasen till exempel heter&quot;aemcrosswalk&quot;, finns den under kontot&quot;wkndform&quot; och du använder huvudgrenen och formuläret som&quot;kontakta oss&quot;, ser den mellanlagrade versionen ut så här:
https://main—aemcrosswalk—wkndform.aem.live/content/forms/af/contact-us

URL-strukturen är densamma för både testversioner och liveversioner. Innehållet som du ser skiljer sig dock åt beroende på sammanhanget:

![Visa publicerat formulär](/help/edge/assets/eds-view-publish-form.png){width=50%, align-center}

## Felsökning

Har du problem med att läsa in formuläret? Här är några vanliga problem och hur du åtgärdar dem:

* **Formulär-URL**: Dubbelkontrollera att formulärets URL inte innehåller tillägget .html i slutet. Edge-tjänsten för leverans kräver inte det här tillägget.

* **AEM Författar-URL** L: Kontrollera att AEM författar-URL som anges i `fstab.yaml`-filen är korrekt formaterad. Den ska innehålla följande uppgifter:

   * Rätt GitHub-ägare
   * Rätt databasnamn
   * Den specifika gren som du använder för Edge Delivery Services

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.
-->

## Se även

{{see-more-forms-eds}}