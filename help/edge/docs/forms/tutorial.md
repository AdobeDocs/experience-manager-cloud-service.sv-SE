---
title: Komma igång med AEM Forms-Edge Delivery Services - självstudiekurs för utvecklare
description: Den här självstudiekursen hjälper dig att komma igång med ett nytt Adobe Experience Manager Forms-projekt (AEM). Om tio till tjugo minuter har du skapat egna formulär.
feature: Edge Delivery Services
exl-id: bb7e93ee-0575-44e1-9c5e-023284c19490
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '1848'
ht-degree: 0%

---

# Komma igång - självstudiekurs för utvecklare

I dagens digitala samhälle är det viktigt för alla företag att skapa användarvänliga formulär. Med AEM Forms Edge Delivery Services (EDS) kan du skapa formulär med välbekanta verktyg som Google Docs och Microsoft Office.

Dessa formulär skickar data direkt till en Microsoft Excel- eller Google Sheets-fil, vilket gör att du kan använda aktiva ekosystem och stabila API:er för Google Sheets, Microsoft Excel och Microsoft SharePoint för att enkelt bearbeta inlämnade data eller starta ett befintligt arbetsflöde.

AEM Forms har ett block, Adaptive Forms Block, som gör det enkelt att skapa formulär för att hämta in och lagra inhämtade data. Du kan [skapa ett nytt AEM projekt förkonfigurerat med adaptivt Forms-block](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) eller [lägga till det adaptiva Forms-blocket i ett befintligt AEM](#add-adaptive-forms-block-to-your-existing-aem-project) -projekt.

Den här AEM Forms-självstudiekursen guidar dig genom att skapa, förhandsgranska och publicera egna anpassade formulär med ett nytt Adobe Experience Manager (AEM) Forms-projekt.

## Förutsättningar

* Du har ett GitHub-konto och förstår Git-grunderna.
* Du har ett Google- eller Microsoft SharePoint-konto.
* Du förstår grunderna i HTML, CSS och JavaScript.
* Du har installerat Node/npm för lokal utveckling.

**Upp med huvudet!** I den här självstudien används macOS, Chrome och Visual Studio Code. Stegen kan anpassas för andra inställningar, men skärmbilderna och specifika gränssnittselement kan skilja sig åt beroende på vilket operativsystem, vilken webbläsare och vilken kodredigerare du har valt.


## Skapa ett nytt AEM projekt förkonfigurerat med Adaptive Forms Block

Med AEM Forms-mallen för mallar kommer du snabbt igång med ett AEM projekt som är förkonfigurerat med det adaptiva Forms-blocket. Det är det snabbaste och enklaste sättet att följa AEM bästa praxis och börja skapa formulär.

### Kom igång med AEM Forms mall för standarddatabas

1. Skapa en GitHub-databas för ditt AEM. Så här skapar du databas:
   1. Gå till [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms).

      ![AEM Forms-mallsida](/help/edge/assets/aem-forms-boilerplate.png)
   1. Klicka på alternativet **Använd den här mallen** och välj alternativet **Skapa en ny databas**. Skärmen Skapa en ny databas öppnas.

      ![Skapa en ny databas med AEM Forms-standardmallen](/help/edge/assets/create-new-repository-using-aem-forms-boilerplate.png)

   1. Välj **owner** och ange **Databasnamn** på skärmen Skapa en ny databas. Adobe rekommenderar att databasen är inställd på **Offentlig**. Välj därför alternativet **public** och klicka på **Skapa databas**.

   ![Ställ in databasen på public](/help/edge/assets/create-a-new-repo-keep-it-public.png)


1. Installera AEM Code Sync GitHub App på din databas. Installera:
   1. Gå till [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new).
   1. På skärmen Install AEM Code Sync väljer du alternativet **Only select Repositories** och väljer din nya databas. Klicka på Spara.

   ![Ställ in databasen på public](/help/edge/assets/install-aem-code-sync-app-for-your-repo.png)

   >[!NOTE]
   >
   >
   > Om du använder GitHub Enterprise med IP-filtrering kan du lägga till följande IP-adress i tillåtelselista: 3.227.118.73

   Grattis! Du har en ny webbplats som körs på `https://<branch>--<repo>--<owner>.hlx.page/`.

   * `<branch>` refererar till din GitHub-databas.
   * `<repository>` betecknar din GitHub-databas.
   * `<owner>` refererar till användarnamnet för ditt GitHub-konto som är värd för din GitHub-databas.

   Om filialnamnet till exempel är `main`, databasen är `wefinance` och ägaren är `wkndforms`, kommer webbplatsen att vara igång på [https://main—weFinance—wkndforms.hlx.page/](https://main--wefinance--wkndforms.hlx.page/).



### Länka din egen innehållskälla

Din nyligen skapade GitHub-databas pekar på [exempelinnehåll som lagras i en Google Drive-mapp](https://drive.google.com/drive/folders/1bvjfi6TqpYA7DvbX6kKc-m7FgHuJ4RUQ). Det här skrivskyddade innehållet är en bra utgångspunkt för dina formulär. Du kan kopiera det till din egen Google Drive och anpassa det efter dina behov.

![Exempelinnehåll på Google Drive](/help/edge/assets/folder-with-sample-content.png)

Så här kopierar du exempelinnehållet till din egen innehållsmapp och pekar din GitHub-databas mot din egen innehållsmapp:

1. Skapa en ny mapp specifikt för ditt AEM innehåll i Google Drive eller Microsoft SharePoint. I det här dokumentet används en mapp som har skapats i Microsoft SharePoint.

1. Dela mappen med Adobe Experience Manager-användaren (helix@adobe.com).

   ![Använd alternativet Hantera åtkomst för att dela mappen med AEM användare - SharePoint](/help/edge/assets/share-folder-with-aem-user.png)

   ![Använd alternativet Hantera åtkomst för att dela mappen med AEM användare - Google Drive](/help/edge/assets/share-google-drive-folder.png)


   Se till att du har gett Adobe Experience Manager-användaren redigeringsbehörighet för mappen.

   ![Dela mapp med AEM användare, ange redigeringsbehörighet-SharePoint](/help/edge/assets/share-folder-with-aem-user-provide-editing-access.png)

   ![Dela mapp med AEM användare, ange redigeringsbehörighet - Google Drive](/help/edge/assets/add-aem-user-google-folder.png)

1. Kopiera exempelinnehållet [som lagras i Google Drive-mappen](https://drive.google.com/drive/folders/17LSiMZC77N8tCJRW45TnHHGcG8V3SLG_) till din mapp. Kopiera:

   1. Hämta filerna tillsammans eller hämta enskilda filer.

      ![Hämta exempelinnehåll](/help/edge/assets/download-sample-content.png)

      Filerna `nav` och `footer` definierar den grundläggande layouten för dina sidor och ändras sällan i ett projekt. De har också en särskild struktur som skiljer sig från de flesta andra innehållsfiler. Genom att undersöka dessa filer får du en känsla för hur innehållet är organiserat i AEM projekt.


   1. Överför dessa filer till Microsoft SharePoint eller Google Drive-mappen.

      ![Exempelinnehåll på Google Drive](/help/edge/assets/upload-sample-files-to-your-content-folder.png)

      Kontrollera att du kopierar bladet `enquiry` från exempelinnehållet till din mapp på Google Drive eller Microsoft SharePoint. Den innehåller en struktur för ett exempelformulär.

1. Nu när du har konfigurerat innehållsmappen är det dags att länka den till ditt projekt på GitHub som du skapade med AEM Forms Boilerplate tidigare. Ansluta:

   1. Gå till GitHub-databasen som du skapade tidigare med AEM Forms Boilerplate.
   1. Öppna `fstab.yaml` för redigering.
   1. Ersätt den befintliga referensen med sökvägen till mappen som du delade med AEM användare (helix@adobe.com).

      ![Exempelinnehåll på Google Drive](/help/edge/assets/replace-path-in-fstab-yaml-with-your-content-folder.png)


      Om du använder Microsoft SharePoint har mappsökvägen följande format:

      ```HTML
      https://<tenant>.SharePoint.com/sites/<sp-site>/Shared%20Documents/<folder-name>
      ```

      Exempel:

      ```HTML
      https://adobe.SharePoint.com/sites/wkndforms/Shared%20Documents/wefinance
      ```

      Mer information om hur du hanterar filer med Microsoft SharePoint finns i [Så här använder du Adobe SharePoint](https://www.aem.live/docs/setup-customer-sharepoint).


   1. Genomför den uppdaterade `fsatb.yaml`-filen när du har uppdaterat referensen och allt ser bra ut. Om du stöter på några byggproblem kan du läsa [Felsökning av GitHub-byggproblem](#troubleshooting-github-build-issues).



      ![Bekräfta uppdaterad fsatab.yaml-fil](/help/edge/assets/commit-updated-fstab-yaml.png)

      Detta kopplar innehållsmappen till webbplatsen. När du har uppdaterat referensen kan felet&quot;404 Hittades inte&quot; uppstå från början. Det beror på att ditt innehåll inte har förhandsvisats än. I nästa avsnitt beskrivs hur du börjar redigera och förhandsgranska ditt innehåll.



### Förhandsgranska och publicera ditt innehåll

När du är klar med det sista steget är den nya innehållskällan inte tom, men den syns inte på webbplatsen förrän den befordras till förhandsgranskningen eller live-stadierna. För närvarande kan detta orsaka 404 fel.

Så här förhandsgranskar du opublicerat innehåll:

1. Installera Chrome-tillägget [AEM Sidekick](https://chrome.google.com/webstore/detail/helix-sidekick-beta/ccfggkjabjahcjoljmgmklhpaccedipo).

   ![Installera AEM Sidekick](/help/edge/assets/install-aem-sidekick.png)

   När du har installerat tillägget på Chrome, glöm inte att fästa det, blir det enklare att hitta det.

   ![Fäst AEM Sidekick](/help/edge/assets/pin-aem-sidekick.png)

1. Om du vill konfigurera tillägget Sidekick Chrome går du till den tidigare delade Google Drive- eller Microsoft SharePoint-mappen och högerklickar på tilläggsikonen i webbläsarens verktygsfält och väljer `Add this project`.

   ![AEM Sidekick - Lägg till ett projekt](/help/edge/assets/aem-sidekick-add-a-project.png)

   När tillägget är installerat och ditt projekt har lagts till kan du förhandsgranska och publicera ditt innehåll från Google Drive.

1. Markera alla dokument i Microsoft SharePoint- eller Google Drive-mappen. Du kan välja flera dokument genom att hålla ned Ctrl-tangenten (Windows/Linux) eller Cmd-tangenten (Mac) medan du klickar.

   ![Markera alla filer](/help/edge/assets/select-all-files.png)

1. Klicka på AEM Sidekick-ikonen som är fäst i Chrome tilläggsfält. Ett verktygsfält visas på skärmen. Du kan välja att förhandsgranska eller publicera ditt innehåll.

   Om du kopierade över `index`-, `nav`-, `footer`- och `enquiry`-filer är alla dessa separata dokument med sina egna förhandsgransknings- och publiceringscykler, så se till att du förhandsgranskar (och publicerar) alla dem.

   När du förhandsgranskar filerna visas dokumenten på de nya webbläsarflikarna. Om du vill förhandsgranska exempelformuläret går du till följande URL:


   ```HTML
   https://<branch>--<repository>--<owner>.hlx.live
   ```

   * `<branch>` refererar till din GitHub-databas.
   * `<repository>` betecknar din GitHub-databas.
   * `<owner>` refererar till användarnamnet för ditt GitHub-konto som är värd för din GitHub-databas.


   URL för `https://<branch>--<repo>--<owner>.hlx.page/enquiry`.

   Om projektdatabasen till exempel heter&quot;weFinance&quot; finns den under kontoägaren&quot;wkndforms&quot; (wkndforms)&quot; (wkndforms) och du använder huvudgrenen är URL:en:

   [https://main—weFinance—wkndforms.hlx.page](https://main--wefinance--wkndforms.hlx.page).

### Skapa ett formulär

Exempelinnehållet innehåller ett frågeblad som fungerar som mall för frågeformuläret. Varje rad i kalkylbladet representerar ett [formulärfält](/help/edge/docs/forms/form-components.md#available-components) och kolumnrubrikerna definierar [fältegenskaperna](/help/edge/docs/forms/form-components.md#available-components). Det här exempelformuläret ger dig ett försprång när du skapar formuläret.

![Formulär för förfrågan](/help/edge/docs/forms/assets/enquiry-form-microsoft-sharepoint.png)

Vi börjar med att uppdatera en fältetikett. Öppna förfrågningsbladet för redigering, ändra etiketten för skicka-knappen till `Let's Chat` och använd AEM Sidekick för att förhandsgranska och publicera filen.

![Formulär för förfrågan](/help/edge/assets/enquiry-form-preview-publish.png)

När du förhandsgranskar eller publicerar filen visas en JSON-version av filen på en ny flik. Kopiera förhandsgransknings- (.hlx.page) eller publicerings-URL:en (.hlx.live) för filen.

![JSON för formulärkalkylbladet](/help/edge/assets//preview-and-publish-enquiry-form.png)

Öppna filen `enquiry` och ersätt URL:en i formulärblocket med URL:en för filen som kopierades i föregående steg. Kontrollera att URL:en är en hyperlänk.

![Förfrågningsfil med URL:en .json för kalkylbladets URL](/help/edge/assets/enquiry-doc-to-embed-form.png)

Använd AEM Sidekick för att förhandsgranska och publicera förfrågningsdokumentet.

![Förfrågningsfil med URL:en .json för kalkylbladets URL](/help/edge/assets/preview-and-publish-enquiry-document.png)


Om du vill förhandsgranska det uppdaterade frågeformuläret går du till följande URL:


```HTML
    https://<branch>--<repository>--<owner>.hlx.page/enquiry
       
```

Etiketten för skicka-knappen uppdateras till `Let's Chat`.

![Formulär för förfrågan](/help/edge/assets/updated-form.png)

Mer information om hur du skapar och publicerar ett nytt formulär finns i handboken [Skapa ett formulär](/help/edge/docs/forms/create-forms.md).

### Börja utveckla format och funktionalitet


För att komma igång med en lokal AEM utvecklingsmiljö på nolltid:

1. Installera AEM CLI: AEM CLI förenklar utvecklingsuppgifter. Låt oss installera det globalt med npm:

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. Klona ditt GitHub-projekt: Klona din projektdatabas från GitHub med följande kommando och ersätt <owner> med databasägaren och <repo> med databasnamnet:

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. Starta din lokala miljö: Navigera till din projektkatalog och starta den lokala AEM med ett enda kommando:

   ```
   cd <repo>
   aem up
   ```

Mappen Adaptive Forms Block `blocks/form` är din spelningsmiljö för formatering och kod för dina formulär! Redigera alla `.css`- eller `.js`-filer i den här katalogen så ser du ändringarna direkt i webbläsaren.

Är du redo att visa upp din skapelse? Använd Git för att implementera och föra över ändringarna. Detta uppdaterar förhandsgransknings- och produktionsmiljöer som du kan nå på dessa URL:er (ersätt platshållare med projektinformation):

Förhandsgranska: `https://<branch>--<repo>--<owner>.hlx.page/`
Produktion: `https://<branch>--<repo>--<owner>.hlx.live/`

Grattis! Du har konfigurerat den lokala utvecklingsmiljön och distribuerat ändringarna.



## Lägg till adaptiv Forms Block i ditt befintliga AEM


>[!VIDEO](https://video.tv.adobe.com/v/3427789)

Om du har ett befintligt AEM kan du integrera det adaptiva Forms-blocket i ditt aktuella projekt för att komma igång med att skapa formulär.

>[!NOTE]
>
>
> Det här steget gäller projekt som skapats med [AEM-standardmallen](https://github.com/adobe/aem-boilerplate). Om du har skapat ditt AEM med [AEM Forms-standardmallen](https://github.com/adobe-rnd/aem-boilerplate-forms) kan du hoppa över det här steget.

Integrera:

1. Klona det adaptiva Forms-blockarkivet: [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms) till din dator.

1. I den hämtade mappen hittar du mappen `blocks/form`. Kopiera mappen. Navigera till det lokala `blocks`-mappen för ditt AEM och klistra in den kopierade formulärmappen här.

1. Verkställ och skicka dessa ändringar till ditt AEM på GitHub.


Så ja! Det adaptiva Forms-blocket ingår nu i ditt AEM. Du kan börja skapa och lägga till formulär på dina AEM sidor.


## Felsökning av byggproblem med GitHub

Se till att GitHub-byggprocessen blir smidig genom att åtgärda potentiella problem:

* **Resolve Module Path-fel:**
Om du får felmeddelandet&quot;Det går inte att lösa sökvägen till modulen &quot;&#39;../../scripts/lib-franklin.js&#39;&quot; går du till filen [EDS Project]/blocks/forms/form.js. Uppdatera importsatsen genom att ersätta filen lib-franklin.js med filen aem.js.

* **Hantera lintingfel:**
Om du skulle stöta på ett lintingfel kan du kringgå dem. Öppna [EDS-projektfilen]/package.json och ändra lint-skriptet från `"lint": "npm run lint:js && npm run lint:css"` till `"lint": "echo 'skipping linting for now'"`. Spara filen och implementera ändringarna i GitHub-projektet.


## Se även

{{see-more-forms-eds}}
