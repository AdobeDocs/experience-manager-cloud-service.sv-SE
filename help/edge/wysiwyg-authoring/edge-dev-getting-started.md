---
title: Utvecklarhandbok för att komma igång med WYSIWYG-redigering med Edge Delivery Services
description: Den här guiden hjälper dig att komma igång med en ny Adobe Experience Manager-webbplats med hjälp av Edge Delivery Services och den universella redigeraren för WYSIWYG-innehåll.
feature: Edge Delivery Services
exl-id: a71184a7-c954-442e-b276-99edc6d2acd8
role: Admin, Architect, Developer
source-git-commit: 7ad9a959592f1e8cebbcad9a67d280d5b2119866
workflow-type: tm+mt
source-wordcount: '1298'
ht-degree: 0%

---


# Utvecklarhandbok för att komma igång med WYSIWYG-redigering med Edge Delivery Services {#edge-dev-getting-started}

Den här guiden hjälper dig att komma igång med en ny Adobe Experience Manager-webbplats med hjälp av Edge Delivery Services och den universella redigeraren för WYSIWYG-innehåll.

## Förutsättningar {#prerequisites}

Innan du börjar den här guiden bör du känna till grunderna i och ha tillgång till Edge Delivery Services som:

* Du har slutfört självstudiekursen [Edge Delivery Service.](/help/edge/developer/tutorial.md)
* Du har åtkomst till en [AEM Cloud Service-sandlåda.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)
* Du har [aktiverat den universella redigeraren i samma sandlådemiljö.](/help/implementing/universal-editor/getting-started.md)

## Välj rätt redigerare {#editor-choice}

AEM erbjuder två olika innehållsredigerare och vilka alternativ du kan välja mellan beror på din situation.

* **Universell redigerare** - Det här bör vara standardalternativet för nya webbplatser.
* **AEM sidredigeraren** - Detta bör väljas för en befintlig AEM Sites-migrering till Edge Delivery Services.

Den här guiden fokuserar AEM projekt på Edge Delivery Services med hjälp av den universella redigeraren. Se dokumentet [Använda Edge Delivery Services med AEM](/help/edge/using.md) för mer information om hur du väljer rätt redigerare och migreringen av befintliga AEM till Edge Delivery Services.

## Grundbegrepp vid utveckling för Edge Delivery Services {#core-concepts}

Edge Delivery Services bygger på konceptet med block. AEM innehåller ett omfattande bibliotek med fördefinierade block, som kan byggas ut efter dina projektbehov. Kod för Edge Delivery Services-projekt hanteras i GitHub.

### Block {#blocks}

Block är den mest grundläggande delen av en sida som levereras av Edge Delivery Services. Ett -block kapslar in format och kod som driver en logisk komponent på en innehållssida.

AEM tillhandahåller standardblock som en del av produkten i projektmallen. Exempel på sådana block är rubrik, text, bilder, länkar, listor osv.

>[!TIP]
>
>Mer information om hur du blockerar och utvecklar för Edge Delivery-Edge Delivery Services finns i avsnittet [Build](/help/edge/developer/block-collection.md) i dokumentationen för .

### Edge Delivery Services och GitHub {#github-edge}

Edge Delivery utnyttjar GitHub så att du kan hantera och driftsätta kod direkt från din GitHub-databas.

Dina författare kan skapa innehåll med antingen dokumentbaserad redigering eller innehåll i AEM med den universella redigeraren. Utvecklare kan anpassa webbplatsens funktionalitet med hjälp av CSS och JavaScript i GitHub oavsett hur författarna skapar sitt innehåll.

Webbplatser skapas automatiskt för var och en av dina grenar, från förhandsgranskning av innehåll till produktion. Alla resurser du lägger in i GitHub-databasen är tillgängliga på din webbplats utan någon byggprocess.

>[!TIP]
>
>Mer information om hur du blockerar och utvecklar för Edge Delivery-Edge Delivery Services finns i avsnittet [Build](/help/edge/developer/block-collection.md) i dokumentationen för .

## Komma igång med WYSIWYG-redigering och Edge Delivery Services {#getting-started}

När du har uppfyllt [villkoren](#prerequisites) och gjort [till ett val att använda Universell redigerare](#editor-choice) kan du komma igång med ditt eget projekt.

### Skapa ditt GitHub-projekt {#create-github-project}

Först måste du skapa ett nytt projekt på GitHub, baserat på mallen Adobe.

1. Navigera till [`https://github.com/adobe-rnd/aem-boilerplate-xwalk`](https://github.com/adobe-rnd/aem-boilerplate-xwalk) och klicka på **Använd den här mallen** och välj **Skapa en ny databas**.

   * Du måste vara inloggad på GitHub för att kunna se det här alternativet.

   ![Kopiera databasprojekt](assets/edge-dev-getting-started/use-template-project.png)

1. Som standard tilldelas databasen till dig. Ändra detta om det behövs, ange ett databasnamn och en beskrivning och klicka på **Skapa databas**.

   ![Skapar databasen](assets/edge-dev-getting-started/create-repo.png)

1. Navigera till [`https://github.com/apps/aem-code-sync`](https://github.com/apps/aem-code-sync) och klicka på **Konfigurera** på en ny flik i samma webbläsare.

   ![Kodsynkronisering](assets/edge-dev-getting-started/configure-code-sync.png)

1. Klicka på **Konfigurera** för den organisation där du skapade din nya databas i föregående steg.

   ![Välja organisation för kodsynkronisering](assets/edge-dev-getting-started/code-sync-org.png)

1. På sidan AEM för GitHub-kodsynkronisering under **Databasåtkomst** väljer du **Markera endast databaser**, markera databasen som du skapade i föregående steg och klicka sedan på **Spara**.

   ![Beviljar åtkomst AEM kodsynkronisering](assets/edge-dev-getting-started/grant-code-sync-acces.png)

1. När AEM Code Sync har installerats får du en bekräftelse. Gå tillbaka till webbläsarfliken i din nya databas.

   ![Bekräftelse av installation av kodsynkronisering](assets/edge-dev-getting-started/confirmation.png)

1. Klicka på filen `fstab.yaml` för att öppna den och redigera den sedan genom att klicka på ikonen **Redigera den här filen** .

   ![fstab.yaml](assets/edge-dev-getting-started/fstab.png)

1. Redigera filen `fstab.yaml` för att uppdatera monteringspunkten för projektet. Ersätt standardwebbadressen för Google Docs med webbadressen för AEM as a Cloud Service-redigeringsinstansen och klicka sedan på **Verkställ ändringar..**.

   * `https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main`
   * Om du ändrar monteringspunkten får Edge Delivery Servicens information om var innehållet på platsen finns.

   ![Uppdaterar fstab](assets/edge-dev-getting-started/fstab-update.png)

1. Lägg till ett implementeringsmeddelande efter behov och klicka sedan på **Verkställ ändringar** och implementera dem direkt i `main` -grenen.

   ![Utför ändringar](assets/edge-dev-getting-started/commit-fstab-changes.png)

1. Gå tillbaka till roten för databasen, klicka på `paths.json` och sedan på ikonen **Redigera den här filen** .

   ![paths.json](assets/edge-dev-getting-started/paths.png)

1. Standardmappningen använder databasens namn. Uppdatera den standardmappning som krävs för ditt projekt med `/content/<site-name>/:/` och klicka på **Verkställ ändringar..**.

   * Ange din egen `<site-name>`. Du kommer att behöva det i ett senare steg.
   * Mappningarna anger för Edge Delivery Servicens hur innehållet i din AEM ska mappas till webbplatsens URL.

   ![Uppdaterar paths.json](assets/edge-dev-getting-started/paths-update.png)

1. Lägg till ett implementeringsmeddelande efter behov och klicka sedan på **Verkställ ändringar** och implementera dem direkt i `main` -grenen.

   ![Utför ändringar](assets/edge-dev-getting-started/commit-paths-changes.png)

### Skapa och redigera en ny AEM {#create-aem-site}

Nu när du har ett GitHub-projekt måste du skapa en ny AEM som projektet kan använda.

>[!NOTE]
>
>Om du vill redigera webbplatsen med Universal Editor måste du använda en Chromium-baserad webbläsare.

1. Hämta den senaste WYSIWYG-redigeringen med webbplatsmallen för Edge Delivery Services från GitHub på [`https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases).

1. Logga in på din AEM as a Cloud Service-redigeringsinstans och navigera till webbplatskonsolen och tryck eller klicka på **Skapa** -> **Plats från mall**.

   ![Skapa en ny plats från konsolen](assets/edge-dev-getting-started/create-site-console.png)

1. På fliken **Välj en platsmall** i guiden Skapa plats klickar du på knappen **Importera** för att importera en ny mall.

   ![Importerar mallar](assets/edge-dev-getting-started/site-templates.png)

1. Ladda upp WYSIWYG-redigeringen med webbplatsmallen för Edge Delivery Services som du hämtade från GitHub.

   * Mallen får bara överföras en gång. När den har överförts kan den återanvändas för att skapa ytterligare webbplatser.

1. När mallen har importerats visas den i guiden. Tryck eller klicka för att markera den och tryck eller klicka sedan på **Nästa**.

   ![Välj mall](assets/edge-dev-getting-started/select-template.png)

1. Ange följande fält och tryck eller klicka på **Skapa**.

   * **Platstitel** - Lägg till en beskrivande titel för webbplatsen.
   * **Platstitel** - Använd `<site-name>` som du definierade i [föregående steg.](#create-github-project)
   * **GitHub-URL** - Använd URL:en för GitHub-projektet som du skapade i föregående steg.

   ![Webbplatsinformation](assets/edge-dev-getting-started/create-site-details.png)

1. AEM bekräftar att webbplatsen har skapats med en dialogruta. Tryck eller klicka på **OK** för att stänga.

   ![Bekräftelse av webbplatsskapande](assets/edge-dev-getting-started/site-creation-confirmation.png)

1. På webbplatskonsolen går du till `index.html` för den nyligen skapade webbplatsen och trycker eller klickar på **Redigera** i verktygsfältet.

   ![Redigerar den nya platsen](assets/edge-dev-getting-started/new-site.png)

1. Den universella redigeraren öppnas på en ny flik. Du kan behöva trycka eller klicka på **Logga in med Adobe** för att autentisera för att redigera sidan.

   ![Universell redigerare](assets/edge-dev-getting-started/universal-editor.png)

Nu kan du redigera webbplatsen med Universal Editor. Mer information finns i [dokumentationen för den universella redigeraren](/help/sites-cloud/authoring/universal-editor/authoring.md).

### Publicera din nya webbplats {#publishing}

När du är klar med redigeringen av den nya webbplatsen med Universal Editor kan du publicera innehållet.

1. På webbplatskonsolen markerar du alla sidor som du har skapat för den nya webbplatsen och trycker eller klickar på **Snabbpublicering** i verktygsfältet.

   ![Välja sidor att publicera](assets/edge-dev-getting-started/publishing.png)

1. Tryck eller klicka på **Publish** i bekräftelsedialogrutan för att starta processen.

   ![Dialogrutan Publish](assets/edge-dev-getting-started/publish-confirmation.png)

1. Öppna en ny flik i samma webbläsare och navigera till URL:en för den nya platsen.

   * `https://main--<repository-name>--<owner>.hlx.page`

1. Se innehållet publiceras.

   ![Publicerat innehåll](assets/edge-dev-getting-started/published-site.png)

## Nästa steg {#next-steps}

Nu när du har en fungerande WYSIWYG-redigering med Edge Delivery Services kan du börja skapa och formatera egna block.

Mer information finns i guiden [Skapa block som är instrumenterade för användning med den universella redigeraren](/help/edge/wysiwyg-authoring/create-block.md).

>[!TIP]
>
>En genomgång av hur du skapar ett nytt projekt för Edge Delivery Services som är aktiverat för WYSIWYG-redigering med AEM as a Cloud Service som innehållskälla finns i [det här webbinariet för AEM.](https://experienceleague.adobe.com/en/docs/events/experience-manager-gems-recordings/gems2024/aem-authoring-and-edge-delivery)
