---
title: SecurBank-exempelapp för Universal Editor
description: Lär dig mer om den universella redigeraren med praktiska erfarenheter med SecurBank App, som är utformad för att visa kraften, flexibiliteten och användbarheten hos den universella redigeraren för att snabba upp framtagningen av innehåll.
exl-id: 97e1395f-b51e-4cee-b1d0-2466a08f96af
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# SecurBank-exempelapp för Universal Editor {#securbank}

Lär dig mer om den universella redigeraren med praktiska erfarenheter med SecurBank App, som är utformad för att visa kraften, flexibiliteten och användbarheten hos den universella redigeraren för att snabba upp framtagningen av innehåll.

## Förutsättningar {#prerequisites}

* Du måste tilldelas till **AEM** [produktprofil](/help/journey-onboarding/assign-profiles-aem.md) för att installera programmet SecurBank.
* Du måste ha [Node.js](https://nodejs.org) version 20 eller senare installerad för lokal utveckling.

## Installerar SecurBank {#installation}

Installationen av SecurBank-appen är enkel, men eftersom den berör många områden på AEM as a Cloud Service är det ett antal steg som är aktuella. Här följer en översikt över de viktigaste stegen.

1. [Skapa ett sandlådeprogram i Cloud Manager.](#create-sandbox-program)
1. [Klona programmets Git-databas och uppdatera med SecurBank-AEM projektinnehåll.](#clone-and-update)
1. [Kör pipelinen för att distribuera SecurBank-AEM.](#run-pipeline)
1. [Hämta autentiseringsuppgifter för Cloud Manager för lokal webbappsutveckling.](#retrieve-credentials)
1. [Hämta och konfigurera SecurBanks webbapp.](#download-web-app)
1. [Kör webbappen SecurBank.](#run-web-app)

I följande avsnitt beskrivs de enskilda uppgifter som krävs.

### Skapa ett sandlådeprogram i Cloud Manager. {#create-sandbox-program}

Du behöver ett nytt Cloud Manager-program där du kan installera SecurBank.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation

1. Skapa ett nytt sandlådeprogram för programmet SecurBank.

   * Använd standardalternativen när du väljer **Lösningar och tillägg**.
   * Mer information om hur du skapar ett sandlådeprogram finns i dokumentet [Skapar sandlådeprogram.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)

### Klona programmets Git-databas och uppdatera med SecurBank-AEM projektinnehåll. {#clone-and-update}

1. När programmet är klart öppnar du det och på **Databaser** klickar du på **Åtkomst till svarsinformation** för att öppna **Databasinformation** och visa de inloggningsuppgifter som krävs för att få åtkomst till Git-databasen för sandlådemiljön.

   * Mer information om hur du får åtkomst till din databasinformation finns i dokumentet [Åtkomst till databaser.](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

1. Använda inloggningsuppgifterna i dialogrutan **Databasinformation** , klona databasen på din lokala dator.

1. Leta reda på mappen för den lokala klonen, öppna den och ta bort allt innehåll utom dolda/punktfiler.

1. Hämta den senaste SecurBank-AEM-projektkoden från GitHub på [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank) genom att klicka **Code** och sedan **Ladda ned ZIP** i listrutan.

1. Dekomprimera innehållet i zip-filen på det lokala filsystemet och flytta den till den nu tomma mappen för den lokala klonen i sandlådeprogrammet.

1. Använd terminalen för att växla till mappen för det klonade projektet och spara allt innehåll och skicka det till Git.

   1. `git add --all`
   1. `git commit -m "Adding SecurBank app code"`
   1. `git push`

### Kör pipelinen för att distribuera SecurBank-AEM. {#run-pipeline}

Med det AEM projektet för SecurBank för sandlådedatabasen kan det distribueras med en pipeline.

1. Återgå till **Ökning** -fliken i ditt sandlådeprogram i Cloud Manager och kör hela stacken i icke-produktionsflödet.

   * Avmarkera alla alternativ för pipeline-körningen.
   * Mer information om att köra rörledningar finns i dokumentet [Hantera rörledningar.](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)

### Hämta autentiseringsuppgifter för Cloud Manager för lokal webbappsutveckling. {#retrieve-credentials}

Innan du kan köra SecurBank-appen måste du ha autentiseringsuppgifter för Cloud Manager för att ansluta appen till Cloud Manager.

1. Gå tillbaka till **Ökning** i Cloud Manager och tryck eller klicka på ellipsknappen bredvid miljönamnet och välj **Developer Console**.

1. På Developer Console väljer du **Integreringar** tabben **Lokal token** tabba och trycka eller klicka **Hämta lokal utvecklingstoken**.

1. En JSON-fil skapas med åtkomsttoken. Kopiera endast själva token (den återstående JSON-versionen är inte nödvändig) till en säker plats för användning i ett framtida steg innan du stänger Developer Console och återgår till Cloud Manager.

1. Tillbaka i Cloud Manager på **Ökning** högerklickar du på URL:en för miljön för att kopiera den och spara den på en säker plats för användning i ett framtida steg.

### Hämta och konfigurera SecurBanks webbapp. {#download-web-app}

Nu kan du hämta och konfigurera webbappen SecurBank.

1. Hämta den senaste SecurBank-appkoden från GitHub på [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events) genom att klicka **Code** och sedan **Ladda ned ZIP** i listrutan.

1. Dekomprimera innehållet i zip-filen i det lokala filsystemet.

1. Starta den önskade kodredigeraren och öppna den dolda miljöfilen i SecurBank-appprojektet på `summit-2024-l425-ue-z-final-with-events/react-app/.env`.

1. Gör följande ändringar i `.env` och spara ändringarna.

   * För `REACT_APP_HOST_URI` klistra in värdet för den tidigare kopierade URL-adressen för miljön.
   * För `REACT_APP_DEV_TOKEN` klistra in värdet för den tidigare kopierade lokala utvecklingstoken.

### Kör webbappen SecurBank. {#run-web-app}

När allt är konfigurerat både i Cloud Manager och lokalt kan du köra webbappen SecurBank.

1. Navigera till kommandoraden på den lokala datorn `react-app` mappen för SecurBank-appprojektet som du hämtade och expanderade.

1. I `react-app` installera SecurBank-appen med `node -i` -kommando.

1. Starta SecurBank-appen med `npm start` -kommando.

1. Om installationen och starten lyckades ser du:

* Följande utdata i terminalen.

  ```text
  Compiled successfully!
  
  You can now view securbank in the browser.
  
    Local:            https://localhost:3000
    On Your Network:  https://192.168.1.15:3000
  
  Note that the development build is not optimized.
  To create a production build, use npm run build.
  
  webpack compiled successfully
  ```

   * Och ett webbläsarfönster öppnas för webbadressen `https://localhost:3000`.

      * Observera att detta är avsett för utvecklingsändamål och att inget giltigt certifikat tillhandahålls. Du kan därför behöva informera webbläsaren för att den ska kunna komma åt sidan.

Grattis! Nu bör du se när SecurBank-appen körs i webbläsaren.

Om innehållet inte visas än kontrollerar du att **Distribuera till Dev** pipeline som du har kört har slutförts.

![SecurBank-appen i webbläsaren](assets/securbank.png)
