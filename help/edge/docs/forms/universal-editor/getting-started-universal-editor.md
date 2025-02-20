---
title: Komma igång med Edge Delivery Services för AEM Forms i Universal Editor - självstudiekurs för utvecklare
description: Den här självstudien hjälper dig att komma igång med ett nytt Adobe Experience Manager Forms-projekt (AEM). Om tio till tjugo minuter har du skapat en egen Edge Delivery Services Forms i Universal Editor.
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: 24a23d98-1819-4d6b-b823-3f1ccb66dbd8
source-git-commit: ba42a99e6138616ab6a7564c4bf58400844bdcc4
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 0%

---


# Komma igång med Edge Delivery Services för AEM Forms med Universal Editor (WYSIWYG)

I dagens digitala ålder är användarvänliga formulär oumbärliga för alla organisationer. Edge Delivery Services Forms skapas med Universal Editor, som har WYSIWYG-funktioner (what-you-see-is-what-you-get). Det har ett modernt, intuitivt gränssnitt för effektiv formulärutveckling.

AEM Forms har ett block, Adaptive Forms Block, som gör det enkelt att skapa Edge Delivery Services Forms för datainhämtning och lagring. Du kan [skapa ett nytt AEM-projekt förkonfigurerat med det adaptiva Forms-blocket](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) eller [lägga till det adaptiva Forms-blocket i ett befintligt AEM-projekt](#add-adaptive-forms-block-to-your-existing-aem-project).

Den här självstudiekursen vägleder dig genom att skapa, förhandsgranska och publicera ditt eget formulär med ett nytt eller befintligt Adobe Experience Manager Site-projekt med hjälp av Universal Editors WYSIWYG-redigering.


## Förutsättningar

* Du har ett GitHub-konto och förstår Git-grunderna.
* Du förstår grunderna i HTML, CSS och JavaScript.
* Du har installerat Node/npm för lokal utveckling.

## Skapa ett nytt AEM-projekt förkonfigurerat med Adaptive Forms Block

Med AEM Forms-mallen Boilerplate kommer du snabbt igång med ett AEM-projekt som är förkonfigurerat med Adaptive Forms Block. Det är det snabbaste och enklaste sättet att följa AEM bästa praxis och börja skapa formulär.

### Kom igång med AEM Forms mall för standarddatabas

1. Skapa en GitHub-databas för ditt AEM-projekt. Så här skapar du databas:
   1. Gå till [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms).

      ![AEM Forms-mallsida](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   1. Klicka på alternativet **Använd den här mallen** och välj alternativet **Skapa en ny databas**.

      ![Skapa en ny databas med AEM Forms-standardmallen](/help/edge/docs/forms/assets/use-eds-form-template.png)

      Skärmen **Skapa en ny databas** öppnas.

   1. På skärmen **Skapa en ny databas** väljer du **ägare** och anger **databasnamn** . Adobe rekommenderar att databasen ställs in på **Offentlig**. Välj därför alternativet **public** och klicka på **Skapa databas**.

      ![Ställ in databasen på public](/help/edge/docs/forms/assets/name-eds-repo.png)

1. Installera AEM Code Sync GitHub App i din databas. Installera:
   1. Gå till [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new).
   1. På skärmen **Installera AEM Code Sync** markerar du alternativet **Only select Repositories** och väljer din nya databas. Klicka på **Spara**.

   ![Ställ in databasen på public](/help/edge/docs/forms/assets/aem-code-sync-up.png)

1. Länka nu GitHub-databasen som du skapade med AEM Forms Boilerplate till AEM Project-miljön. Ansluta:

   1. Gå till GitHub-databasen som du skapade tidigare med AEM Forms Boilerplate.
   1. Öppna filen **fstab.yaml** för redigering.

      ![öppna filen fstab.yaml](/help/edge/docs/forms/assets/open-fstab.png)

   1. Redigera filen **fstab.yaml** för att uppdatera monteringspunkten för projektet. Ersätt URL:en med URL:en för AEM as a Cloud Service-redigeringsinstansen.
      `https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main`

      ![redigera filen fstab.yaml](/help/edge/docs/forms/assets/edit-fstab-file.png)

   1. Genomför den uppdaterade filen **fstab.yaml** när du har uppdaterat referensen och allt ser bra ut.

      ![verkställ ändringarna](/help/edge/docs/forms/assets/commit-fstab-changes.png)

      Om du stöter på några byggproblem kan du läsa [Felsökning av GitHub-byggproblem](#troubleshooting-github-build-issues).

### Skapa ett nytt AEM-projekt

Nu när du har ett GitHub-projekt kan du fortsätta att skapa och publicera ett nytt AEM-projekt i AEM as a Cloud Service-redigeringsinstansen.
1. Så här skapar du ett nytt AEM-projekt:

   1. Logga in på AEM as a Cloud Service redigeringsinstans och välj **Platser**.

      ![välj platser](/help/edge/assets/select-sites.png)

   1. Klicka på **Skapa** > **Plats från mall**.

      ![create-sites](/help/edge/docs/forms/assets/create-sites.png)

   1. Markera Edge Delivery Services Site-mallen och klicka på **Next**.

      ![select-site-template](/help/edge/docs/forms/assets/select-site-template.png)

      >[!NOTE]
      >
      > * Om Edge Delivery Services Site-mallen inte är tillgänglig i redigeringsinstansen klickar du på Importera för att överföra mallen.
      > * Du kan hämta Edge Delivery Services webbplatsmallar från [GitHub](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases).

   1. Ange följande information för att skapa ett nytt AEM-projekt:
      * **Platstitel** - Lägg till en beskrivande titel för webbplatsen.
      * **Platsrubrik** - Använd `site-name` som du definierade i föregående steg.
      * **GitHub-URL** - Använd URL:en för GitHub-projektet som du skapade i föregående steg.

      ![skapa AEM Site](/help/edge/docs/forms/assets/create-aem-site.png)

   1. Dialogrutan **Skapa plats** visas. Klicka på **OK**.

      ![klicka på OK](/help/edge/docs/forms/assets/click-ok-aem-site.png)

      På bara några minuter skapas ditt nya AEM-projekt.

   1. Navigera till ditt nyskapade AEM-projekt i webbplatskonsolen och klicka på **Redigera**.
I det här fallet används sidan `index.html` för illustration.

      ![redigera AEM-webbplats](/help/edge/docs/forms/assets/edit-site.png)

      AEM Project öppnas i Universal Editor på en ny flik som möjliggör redigering i WYSIWYG. Nu kan du redigera ditt AEM-projekt.

      ![Webbplatsen öppnas i Universal Editor](/help/edge/docs/forms/assets/site-in-universal-editor.png)

1. Publicera ditt skapade AEM Project

   När du är klar med redigeringen av AEM Project publicerar du det. Publicera:

   1. På webbplatskonsolen markerar du alla AEM Project-sidor och klickar på **Snabbpublicering**.

      ![publicera AEM Sites Project](/help/edge/docs/forms/assets/publish-sites.png)

   1. Bekräftelsedialogrutan **Snabbpublicering** visas. Klicka på **Publicera** för att starta publiceringsprocessen.

      ![Bekräftelsedialogruta för snabbpublicering](/help/edge/docs/forms/assets/quick-publish.png)

      Du kan även publicera dina AEM Project-sidor direkt från användargränssnittet i Universalläsaren.

      ![Bekräftelsedialogruta för snabbpublicering](/help/edge/docs/forms/assets/qui.png)

   Grattis! Du har en ny webbplats som körs på `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`.

   * `<branch>` refererar till din GitHub-databas.
   * `<repository>` betecknar din GitHub-databas.
   * `<owner>` refererar till användarnamnet för ditt GitHub-konto som är värd för din GitHub-databas.
   * `<site-name>` refererar till namnet på den plats du har skapat.

   Om filialnamnet till exempel är `main`, databasen är `edsforms`, ägaren är `wkndforms` och `site-name` är `eds-forms`, kommer webbplatsen att vara igång på `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   >[!NOTE]
   >
   > * Om du vill visa sidan `index.html` i AEM Project använder du URL:en: `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
   > * Om du vill visa andra sidor än `index page` i AEM Project använder du URL:en: `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<site-page-name>`

Nu kan du börja [skapa och lägga till formulär i ditt AEM-projekt](#add-edge-delivery-services-forms-to-aem-project).

## Lägg till anpassat Forms-block i ditt befintliga AEM-projekt

Om du har ett befintligt AEM-projekt kan du integrera det adaptiva Forms-blocket i ditt nuvarande projekt för att komma igång med att skapa formulär.

>[!NOTE]
>
>
> Det här steget gäller projekt som skapats med [AEM-standardmallen](https://github.com/adobe-rnd/aem-boilerplate-xwalk). Om du har skapat ditt AEM-projekt med [AEM Forms-standardmallen](https://github.com/adobe-rnd/aem-boilerplate-forms) kan du hoppa över det här steget.

Integrera:
1. **Lägg till nödvändiga filer och mappar**
   1. Kopiera och klistra in följande mappar och filer från [AEM Forms-originalet](https://github.com/adobe-rnd/aem-boilerplate-forms) i ditt AEM-projekt:

      * Mappen [formulärblock](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form)
      * Mappen [form-common](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-common)
      * Mappen [form-components](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-components)
      * filen [form-editor-support.js](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js)
      * [form-editor-support.css](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css) fil

1. **Uppdatera komponentdefinitioner och modellfiler**
   1. Navigera till filen `../models/_component-definition.json` i ditt AEM-projekt och uppdatera den med ändringarna från filen [_component-definition.json i AEM Forms-mallen ](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-definition.json#L39-L48).

   1. Navigera till filen `../models/_component-models.json` i ditt AEM-projekt och uppdatera den med ändringarna från filen [_component-models.json i AEM Forms-mallen ](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-models.json#L24-L26)

1. **Lägg till formulärredigerare i redigeringsskript**
   1. Navigera till filen `../scripts/editor-support.js` i AEM Project och uppdatera den med ändringarna från filen [editor-support.js i AEM Forms-mallen](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js#L105-L106)
1. **Uppdatera ESLint-konfigurationsfilen**
   1. Navigera till filen `../.eslintignore` i ditt AEM-projekt och lägg till följande kodrad för att förhindra fel relaterade till regelmotorn för formulärblockering:

      ```
          blocks/form/rules/formula/*
          blocks/form/rules/model/*
      ```

1. Genomför och skicka dessa ändringar till AEM Project-databasen på GitHub.

Så ja! Det adaptiva Forms-blocket ingår nu i ditt AEM-projekt. Du kan [börja skapa och lägga till formulär i ditt AEM-projekt](#add-edge-delivery-services-forms-to-aem-site-project).

## Skapa AEM Forms med WYSIWYG

Du kan öppna ditt AEM-projekt i den universella redigeraren för WYSIWYG där du kan redigera projektet och lägga till sektionen Adaptiv form för att inkludera Edge Delivery Services-formulär på AEM Project-sidor.

1. Lägg till avsnittet Adaptivt formulär på din AEM Project-sida. Lägga till:
   1. Navigera till ditt AEM-projekt i webbplatskonsolen, markera den webbplatssida som du vill redigera och klicka på **Redigera**. AEM projektsida öppnas i Universal Editor för redigering.
I det här fallet används sidan `index.html` för illustration.
   1. Öppna innehållsträdet och navigera till ett avsnitt där du vill lägga till avsnittet Adaptivt formulär.
   1. Klicka på ikonen **[!UICONTROL Add]** och välj komponenten **[!UICONTROL Adaptive Form]** i komponentlistan.

   ![innehållsträd](/help/edge/docs/forms/assets/add-adaptive-form-block.png)

   Avsnittet Adaptiv form läggs till. Nu kan du börja lägga till formulärkomponenter på AEM Project-sidan.

1. Lägg till formulärkomponenter i det tillagda adaptiva formuläravsnittet. Så här lägger du till formulärkomponenter:
   1. Navigera till det tillagda adaptiva formuläravsnittet i innehållsträdet.

      ![adaptivt formulärblock tillagt](/help/edge/docs/forms/assets/adative-form-block.png)


   1. Klicka på ikonen **[!UICONTROL Add]** och lägg till de önskade komponenterna från listan **Adaptiva formulärkomponenter**.

      ![lägg till komponent](/help/edge/docs/forms/assets/add-component.png)

      Du kan också dra och släppa nödvändiga adaptiva Forms-komponenter, eftersom den universella redigeraren har en intuitiv dra och släpp-funktion.

   1. Markera den tillagda adaptiva formulärkomponenten om du vill uppdatera dess egenskaper med **[!UICONTROL Properties]**.

      ![öppna egenskaper](/help/edge/docs/forms/assets/component-properties.png)

   1. Förhandsgranska formuläret.
På skärmbilden nedan visas det formulär som skapats i AEM Project med WYSIWYG-redigering:

      ![tillagt formulär](/help/edge/docs/forms/assets/added-form-aem-sites.png)

      När du är nöjd med förhandsgranskningen kan användaren fortsätta att publicera sidan.

      >[!NOTE]
      >
      > Det är viktigt att du publicerar din AEM Project-sida igen när du har gjort ändringar, annars visas inte uppdateringarna i webbläsaren.

1. Publicera om AEM Project-sidan.

   1. Klicka på **Publicera** om du vill publicera AEM Project-sidan igen när du har lagt till formuläret.

      ![publicera formulär](/help/edge/docs/forms/assets/publish-form.png)

   1. Bekräftelsedialogrutan **Publicera** visas på skärmen. Klicka på **Publicera** för att starta publiceringen.

      ![publicera formulär1](/help/edge/docs/forms/assets/publish-form1.png)

      När du klickar på knappen **Publicera** visas meddelandet `Publish started successfully`.

      ![publicera formulär2](/help/edge/docs/forms/assets/publish-form2.png)

   Nu kan du visa AEM Project-sidan med det nya Edge Delivery Services-formuläret på följande URL:
   `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`.

   Om filialnamnet till exempel är `main`, databasen är `edsforms`, ägaren är `wkndforms` och platsen-namnet är `eds-forms`, blir URL:en:
   `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   ![indexsida](/help/edge/docs/forms/assets/publish-index-page.png)

Du kan formatera Edge Delivery Services Forms genom att redigera `.css`- och `.js`-filerna i det adaptiva Forms-blocket och [konfigurera en lokal AEM-utvecklingsmiljö](#set-up-local-aem-development-environment) så att du ser ändringarna direkt i webbläsaren.

## Konfigurera lokal AEM-utvecklingsmiljö

Du kan konfigurera en lokal AEM-utvecklingsmiljö för att utveckla anpassade format och komponenter lokalt. Så här kommer du igång med en lokal utvecklingsmiljö i AEM:

1. **Installera AEM CLI**: AEM CLI förenklar utvecklingsuppgifter. Låt oss installera det globalt med npm:

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. **Klona ditt GitHub-projekt**: Klona din AEM Project-databas från GitHub med följande kommando och ersätt <owner> med databasägaren och <repo> med databasnamnet:

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. **Starta den lokala miljön**: Navigera till projektkatalogen och starta den lokala AEM-instansen med ett enda kommando:

   ```
   cd <repo>
   aem up
   ```

Du kan göra lokala ändringar i den adaptiva Forms-blockmappen `blocks/form` för att formatera och koda dina formulär! Redigera `.css`- eller `.js`-filerna i den här katalogen så ser du att ändringarna återspeglas direkt i webbläsaren.

När du är klar med ändringarna använder du Git-kommandon för att implementera och överföra dem. Detta uppdaterar förhandsgransknings- och produktionsmiljöer som du kommer åt på följande URL:er (ersätt platshållare med projektinformation):

Förhandsgranska: `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`

Produktion: `https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`


## Felsökning av byggproblem med GitHub

Se till att GitHub-byggprocessen blir smidig genom att åtgärda potentiella problem:

* **Hantera lintingfel:**
Om du skulle stöta på ett lintingfel kan du kringgå dem. Öppna [EDS-projektfilen]/package.json och ändra lint-skriptet från `"lint": "npm run lint:js && npm run lint:css"` till `"lint": "echo 'skipping linting for now'"`. Spara filen och implementera ändringarna i GitHub-projektet.

* **Resolve Module Path-fel:**
Om du får felmeddelandet&quot;Det går inte att lösa sökvägen till modulen &quot;&#39;../../scripts/lib-franklin.js&#39;&quot; går du till filen [EDS Project]/blocks/forms/form.js. Uppdatera importsatsen genom att ersätta filen lib-franklin.js med filen aem.js.

## Se även

{{universal-editor-see-also}}
