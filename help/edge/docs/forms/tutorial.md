---
title: Komma igång med AEM Forms-Edge Delivery Services - självstudiekurs för utvecklare
description: Den här självstudiekursen hjälper dig att komma igång med ett nytt Adobe Experience Manager Forms-projekt (AEM). Om tio till tjugo minuter har du skapat egna formulär.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 2aa70e78764616f41fe64e324c017873cfba1d5b
workflow-type: tm+mt
source-wordcount: '1770'
ht-degree: 0%

---


# Komma igång - självstudiekurs för utvecklare

I dagens digitala samhälle är det viktigt för alla företag att skapa användarvänliga formulär. Med AEM Forms Edge Delivery Services (EDS) kan du skapa formulär med välbekanta verktyg som Google Docs och Microsoft Office.

Dessa formulär skickar data direkt till en Microsoft Excel- eller Google Sheets-fil, vilket gör att du kan använda aktiva ekosystem och stabila API:er för Google Sheets, Microsoft Excel och Microsoft Sharepoint för att enkelt bearbeta inskickade data eller starta ett befintligt arbetsflöde.

AEM Forms har ett block, Adaptive Forms Block, som gör det enkelt att skapa formulär för att hämta in och lagra inhämtade data. Du kan skapa ett nytt AEM projekt förutrustat med Adaptiv Forms Block eller lägga till Adaptiv Forms Block i ett befintligt AEM.

Den här AEM Forms-självstudiekursen guidar dig genom att skapa, förhandsgranska och publicera egna anpassade formulär med ett nytt Adobe Experience Manager (AEM) Forms-projekt. Du får också lära dig att lägga till adaptiva Forms-block i ett befintligt AEM.

* **[Skapa ett nytt AEM projekt förutrustat med Adaptive Forms Block](#create-a-new-eds-project-pre-equipped-with-adaptive-forms-block)**
* **[Lägg till adaptivt Forms-block i ett befintligt AEM](#add-adaptive-forms-block-to-an-existing-eds-project)**



## Förutsättningar

* Du har ett GitHub-konto och förstår Git-grunderna.
* Du har ett Google- eller Microsoft SharePoint-konto.
* Du förstår grunderna i HTML, CSS och JavaScript.
* Du har installerat Node/npm för lokal utveckling.

**Skärp dig!** I den här självstudien används macOS, Chrome och Visual Studio Code. Stegen kan anpassas för andra inställningar, men skärmbilderna och specifika gränssnittselement kan skilja sig åt beroende på vilket operativsystem, vilken webbläsare och vilken kodredigerare du har valt.


## Skapa ett nytt AEM projekt förutrustat med Adaptive Forms Block

Med AEM Forms-mallen för mallar kommer du snabbt igång med ett AEM projekt som är förkonfigurerat med det adaptiva Forms-blocket. Det är det snabbaste och enklaste sättet att följa AEM bästa praxis och börja skapa formulär.

### Kom igång med AEM Forms mall för standarddatabas

1. Skapa en Github-databas för ditt AEM projekt. Så här skapar du databas:
   1. Gå till [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms).

      ![AEM Forms Boilerplate](/help/edge/assets/aem-forms-boilerplate.png)
   1. Klicka på **Använd den här mallen** och väljer **Skapa en ny databas** alternativ. Skärmen Skapa en ny databas öppnas.

      ![Skapa en ny databas med AEM Forms Boilerplate](/help/edge/assets/create-new-repository-using-aem-forms-boilerplate.png)

   1. När du skapar en ny databas väljer du **ägare** och ange **Databasnamn** . Adobe rekommenderar att databasen är inställd på **Offentlig**. Välj **public** och klicka på **Skapa databas**.

   ![Ställ in databasen till publik](/help/edge/assets/create-a-new-repo-keep-it-public.png)


1. Installera AEM Code Sync GitHub App på din databas. Installera:
   1. Gå till [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new).
   1. På skärmen Install AEM Code Sync väljer du **Välj bara databaser** och välj din nya databas. Klicka på Spara.

   ![Ställ in databasen till publik](/help/edge/assets/install-aem-code-sync-app-for-your-repo.png)

   >[!NOTE]
   >
   >
   > Om du använder Github Enterprise med IP-filtrering kan du lägga till följande IP-adress i tillåtelselista: 3.227.118.73

   Grattis! Du har en ny webbplats på `https://<branch>--<repo>--<owner>.hlx.page/`.

   * `<branch>` refererar till grenen i din GitHub-databas.
   * `<repository>` anger din GitHub-databas.
   * `<owner>` refererar till användarnamnet för ditt GitHub-konto som är värd för din GitHub-databas.

   Om förgreningsnamnet till exempel är `main`, databasen är `wefinance`och ägaren är `wkndforms`, kommer webbplatsen att vara igång på [https://main—weFinance—wkndforms.hlx.page/](https://main--wefinance--wkndforms.hlx.page/).



### Länka din egen innehållskälla

Din nya Github-databas pekar på [exempelinnehåll som lagras i en Google Drive-mapp](https://drive.google.com/drive/folders/17LSiMZC77N8tCJRW45TnHHGcG8V3SLG_). Det här skrivskyddade innehållet är en bra utgångspunkt för dina formulär. Du kan kopiera det till din egen Google Drive och anpassa det efter dina behov.

![Exempelinnehåll på Google Drive](/help/edge/assets/folder-with-sample-content.png)

Så här kopierar du exempelinnehållet till din egen innehållsmapp och pekar på din Github-databas till din egen innehållsmapp:

1. Skapa en ny mapp specifikt för ditt AEM innehåll i Google Drive eller Microsoft SharePoint. I det här dokumentet används en mapp som har skapats i Microsoft SharePoint.

1. Dela mappen med Adobe Experience Manager-användaren (helix@adobe.com).

   ![Använd alternativet Hantera åtkomst för att dela mappen med AEM användare - SharePoint](/help/edge/assets/share-folder-with-aem-user.png)

   ![Använd alternativet Hantera åtkomst för att dela mappen med AEM användare - Google Drive](/help/edge/assets/share-google-drive-folder.png)


   Se till att du har gett Adobe Experience Manager-användaren redigeringsbehörighet för mappen.

   ![Dela mapp med AEM användare, ange redigeringsbehörighet-SharePoint](/help/edge/assets/share-folder-with-aem-user-provide-editing-access.png)

   ![Dela mapp med AEM användare, ange redigeringsbehörighet - Google Drive](/help/edge/assets/add-aem-user-google-folder.png)

1. Kopiera [exempelinnehåll som lagras i Google Drive-mappen](https://drive.google.com/drive/folders/17LSiMZC77N8tCJRW45TnHHGcG8V3SLG_) till din mapp. Kopiera:

   1. Hämta filerna tillsammans eller hämta enskilda filer.

      ![Hämta exempelinnehåll](/help/edge/assets/download-sample-content.png)

      The `index`, `nav`och `footer` -filer definierar den grundläggande layouten för sidorna och ändras sällan i ett projekt. De har också en särskild struktur som skiljer sig från de flesta andra innehållsfiler. Genom att undersöka dessa filer får du en känsla för hur innehållet är organiserat i AEM projekt.


   1. Överför dessa filer till Microsoft SharePoint eller Google Drive-mappen.

      ![Exempelinnehåll på Google Drive](/help/edge/assets/upload-sample-files-to-your-content-folder.png)

      Se till att du kopierar  `enquiry` från exempelinnehållet till din mapp på Google Drive eller Microsoft SharePoint. Den innehåller en struktur för ett exempelformulär.

1. Nu när du har konfigurerat innehållsmappen är det dags att länka den till ditt projekt på GitHub som du skapade med AEM Forms Boilerplate tidigare. Ansluta:

   1. Gå till GitHub-databasen som du skapade tidigare med AEM Forms Boilerplate.
   1. Öppna `fstab.yaml` för redigering.
   1. Ersätt den befintliga referensen med sökvägen till mappen som du delade med AEM användare (helix@adobe.com).

      ![Exempelinnehåll på Google Drive](/help/edge/assets/replace-path-in-fstab-yaml-with-your-content-folder.png)


      Om du använder Microsoft SharePoint har mappsökvägen följande format:

      ```HTML
      https://<tenant>.sharepoint.com/sites/  <sp-site>/Shared%20Documents/<folder-name>
      ```

      Exempel:

      ```HTML
      https://adobe.sharepoint.com/sites/wkndforms/Shared%20Documents/wefinance
      ```

      Mer information om hur du hanterar filer i Microsoft SharePoint finns i [Så här använder du Adobe Sharepoint](https://www.aem.live/docs/setup-customer-sharepoint).



   1. Genomför den uppdaterade `fsatb.yaml` när du har uppdaterat referensen ser allt bra ut. Om du stöter på några byggproblem kan du läsa [Felsökning av byggproblem med GitHub](#troubleshooting-github-build-issues).



      ![Bekräfta uppdaterad fsatab.yaml-fil](/help/edge/assets/commit-updated-fstab-yaml.png)

      Detta kopplar innehållsmappen till webbplatsen. När du har uppdaterat referensen kan felet&quot;404 Hittades inte&quot; uppstå från början. Det beror på att ditt innehåll inte har förhandsvisats än. I nästa avsnitt beskrivs hur du börjar redigera och förhandsgranska ditt innehåll.

      ![Bekräfta uppdaterad fsatab.yaml-fil](/help/edge/assets/aem-forms-project-folder-error.png)

### Förhandsgranska och publicera ditt innehåll

När du är klar med det sista steget är den nya innehållskällan inte tom, men den syns inte på webbplatsen förrän den befordras till förhandsgranskningen eller live-stadierna. För närvarande kan detta orsaka 404 fel.

Så här förhandsgranskar du opublicerat innehåll:

1. Installera Chrome-tillägget som anropades [AEM Sidekick](https://chrome.google.com/webstore/detail/helix-sidekick-beta/ccfggkjabjahcjoljmgmklhpaccedipo).

   ![Installera AEM Sidekick](/help/edge/assets/install-aem-sidekick.png)

   När du har installerat tillägget i Chrome, glöm inte att fästa det, blir det enklare att hitta det.

   ![Fäst AEM Sidekick](/help/edge/assets/pin-aem-sidekick.png)

1. Om du vill konfigurera tillägget Sidekick Chrome går du till den tidigare delade Google Drive- eller Microsoft SharePoint-mappen och högerklickar på tilläggsikonen i webbläsarens verktygsfält och väljer `Add this project`.

   ![AEM Sidekick - Lägg till ett projekt](/help/edge/assets/aem-sidekick-add-a-project.png)

   När tillägget har installerats och ditt projekt har lagts till kan du förhandsgranska och publicera ditt innehåll från Google Drive.

1. Markera alla dokument i Microsoft SharePoint- eller Google Drive-mappen. Du kan välja flera dokument genom att hålla ned Ctrl-tangenten (Windows/Linux) eller Cmd-tangenten (Mac) medan du klickar.

   ![Markera alla filer](/help/edge/assets/select-all-files.png)

1. Klicka på ikonen AEM Sidekick som är fäst i Chrome-tilläggsfältet. Ett verktygsfält visas på skärmen. Du kan välja att förhandsgranska eller publicera ditt innehåll.

   Om du kopierade över `index`, `nav`, `footer` och `enquiry` -filer är alla separata dokument med sina egna förhandsgransknings- och publiceringscykler, så se till att du förhandsgranskar (och publicerar) alla.

   När du förhandsgranskar filerna visas dokumenten på de nya webbläsarflikarna. Om du vill förhandsgranska exempelformuläret går du till följande URL:


   ```HTML
   https://<branch>--<repository>--<owner>.hlx.live
   ```

   * `<branch>` refererar till grenen i din GitHub-databas.
   * `<repository>` anger din GitHub-databas.
   * `<owner>` refererar till användarnamnet för ditt GitHub-konto som är värd för din GitHub-databas.


   `https://<branch>--<repo>--<owner>.hlx.page/enquiry` URL.

   Om projektdatabasen till exempel heter&quot;weFinance&quot; finns den under kontoägaren&quot;wkndforms&quot; (wkndforms)&quot; (wkndforms) och du använder huvudgrenen är URL:en:



   [https://main—weFinance—wkndforms.hlx.page](https://main--wefinance--wkndforms.hlx.page).

### Uppdatera formuläret

1. Gå till din Microsoft SharePoint- eller Google Drive-mapp.

1. Öppna `enquiry.xlsx` för redigering.

   ![Formulär för förfrågan](/help/edge/assets/enquiry-form-microsoft-sharepoint.png)

1. Ändra Skicka-knappens etikett till `Let's Chat`.

   ![Formulär för förfrågan](/help/edge/assets/enquiry-form-microsoft-sharepoint.png)

1. Använd AEM Sidekick för att förhandsgranska och publicera `enquiry.xlsx` -fil.

   ![Formulär för förfrågan](/help/edge/assets/enquiry-form-preview-publish.png)

1. Om du vill förhandsgranska frågeformuläret går du till följande URL:


   ```HTML
   https://<branch>--<repository>--<owner>.hlx.page/enquiry
   ```

   Etiketten för skicka-knappen uppdateras. Fyll i formuläret och klicka på skicka-knappen. Ett fel inträffar som liknar följande, eftersom kalkylbladet inte är [har angetts för att godkänna data ännu](/help/edge/docs/forms/submit-forms.md).


### Börja utveckla format och funktionalitet


För att komma igång med en lokal AEM utvecklingsmiljö på nolltid:

1. Installera AEM CLI: AEM CLI förenklar utvecklingsuppgifter. Låt oss installera det globalt med npm:

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. Klona ditt Github-projekt: Klona din projektdatabas från GitHub med följande kommando och ersätt <owner> med databasägaren och <repo> med databasnamnet:

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. Starta din lokala miljö: Navigera till din projektkatalog och starta den lokala AEM med ett enda kommando:

   ```
   cd <repo>
   aem up
   ```

The Adaptive Forms Block `blocks/form` är din lekplats för format och kod för dina formulär! Redigera alla `.css` eller `.js` filer i den här katalogen så ser du ändringarna direkt i webbläsaren.

Är du redo att visa upp din skapelse? Använd Git för att implementera och föra över ändringarna. Detta uppdaterar förhandsgransknings- och produktionsmiljöer som du kan nå på dessa URL:er (ersätt platshållare med projektinformation):

Förhandsgranska: `https://<branch>--<repo>--<owner>.hlx.page/`
Produktion: `https://<branch>--<repo>--<owner>.hlx.live/`
Grattis! Du har konfigurerat den lokala utvecklingsmiljön och distribuerat ändringarna.



## Lägg till adaptiv Forms Block i ditt befintliga AEM


>[!VIDEO](https://video.tv.adobe.com/v/3427789)

Om du har ett befintligt AEM kan du integrera det adaptiva Forms-blocket i ditt aktuella projekt för att komma igång med att skapa formulär. Integrera:

1. Klona det adaptiva Forms-blockarkivet: https://github.com/adobe-rnd/aem-boilerplate-forms till din dator.

1. I den hämtade mappen finns `blocks/form` mapp. Kopiera mappen. Gå nu till AEM `blocks` och klistra in den kopierade formulärmappen här.

1. Verkställ och skicka dessa ändringar till ditt AEM på GitHub.


Så ja! Det adaptiva Forms-blocket ingår nu i ditt AEM. Du kan börja skapa och lägga till formulär på dina AEM sidor.


## Felsökning av byggproblem med GitHub

Se till att GitHub-byggprocessen blir smidig genom att åtgärda potentiella problem:

* **Lösning av modulsökvägsfel:**
Om du får felmeddelandet&quot;Det går inte att matcha sökvägen till modulen &quot;&#39;../../scripts/lib-franklin.js&#39;&quot; går du till [EDS-projekt]/blocks/forms/form.js fil. Uppdatera importsatsen genom att ersätta filen lib-franklin.js med filen aem.js.

* **Hantera lintingfel:**
Om du skulle stöta på ett lintingfel kan du kringgå dem. Öppna [EDS-projekt]/package.json och ändra &quot;lint&quot;-skriptet från &quot;lint&quot;: &quot;npm run lint:js &amp;&amp; npm run lint:css&quot; till &quot;lint&quot;: &quot;echo &#39;skipping linting for now&#39;&quot;. Spara filen och implementera ändringarna i GitHub-projektet.


## Se även

* [Skapa ett formulär med Google eller Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Skicka formulär direkt till Microsoft Excel- eller Google-blad](/help/edge/docs/forms/submit-forms.md)
* [Ändra utseende på formulär](/help/edge/docs/forms/style-theme-forms.md)






