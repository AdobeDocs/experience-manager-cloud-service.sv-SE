---
title: SecurBank-exempelapp för Universal Editor
description: Lär dig mer om den universella redigeraren med praktiska erfarenheter med SecurBank App, som är utformad för att visa kraften, flexibiliteten och användbarheten hos den universella redigeraren för att snabba upp framtagningen av innehåll.
exl-id: 97e1395f-b51e-4cee-b1d0-2466a08f96af
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# SecurBank-exempelapp för Universal Editor {#securbank}

Lär dig mer om den universella redigeraren med praktiska erfarenheter med SecurBank App, som är utformad för att visa kraften, flexibiliteten och användbarheten hos den universella redigeraren för att snabba upp framtagningen av innehåll.

## Förutsättningar {#prerequisites}

* Du måste tilldelas **AEM Administrator** [produktprofilen](/help/journey-onboarding/assign-profiles-aem.md) för att kunna installera SecurBank-appen.
* Du måste ha [Node.js](https://nodejs.org) version 20 eller senare installerat för lokal utveckling.

## Installerar SecurBank {#installation}

Installationen av SecurBank-appen är enkel, men eftersom den berör många delar av AEM as a Cloud Service finns det ett antal steg. Här följer en översikt över de viktigaste stegen.

1. [Skapa ett sandlådeprogram i Cloud Manager](#create-sandbox-program).
1. [Klona programmets Git-databas och uppdatera med SecurBank-AEM projektinnehåll](#clone-and-update).
1. [Kör pipelinen för att distribuera SecurBank-AEM](#run-pipeline).
1. [Hämta Cloud Manager-autentiseringsuppgifter för lokal webbprogramsutveckling](#retrieve-credentials).
1. [Hämta och konfigurera SecurBanks webbprogram](#download-web-app).
1. [Kör SecurBank-webbprogrammet](#run-web-app).

I följande avsnitt beskrivs de enskilda uppgifter som krävs.

### Skapa ett sandlådeprogram i Cloud Manager. {#create-sandbox-program}

Du behöver ett nytt Cloud Manager-program där du kan installera SecurBank.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation

1. Skapa ett nytt sandlådeprogram för programmet SecurBank.

   * Använd standardalternativen när du väljer **Lösningar och tillägg**.
   * Mer information om hur du skapar ett sandlådeprogram finns i dokumentet [Skapa sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).

### Klona programmets Git-databas och uppdatera med SecurBank-AEM projektinnehåll. {#clone-and-update}

1. När programmet har skapats öppnar du det och på fliken **Databaser** trycker eller klickar på knappen **Åtkomst till replikinformation** för att öppna dialogrutan **Databasinformation** och visar de inloggningsuppgifter som krävs för åtkomst till Git-databasen för sandlådemiljön.

   * Mer information om hur du får åtkomst till din databasinformation finns i dokumentet [Åtkomst till databaser](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

1. Klona databasen på den lokala datorn med hjälp av inloggningsuppgifterna i dialogrutan **Databasinformation**.

1. Leta reda på mappen för den lokala klonen, öppna den och ta bort allt innehåll utom dolda/punktfiler.

1. Hämta den senaste SecurBank-AEM-projektkoden från GitHub på [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank) genom att klicka på **Code** och sedan på **Download ZIP** i listrutan.

1. Dekomprimera innehållet i zip-filen på det lokala filsystemet och flytta den till den nu tomma mappen för den lokala klonen i sandlådeprogrammet.

1. Använd terminalen för att växla till mappen för det klonade projektet och spara allt innehåll och skicka det till Git.

   1. `git add --all`
   1. `git commit -m "Adding SecurBank app code"`
   1. `git push`

### Kör pipelinen för att distribuera SecurBank-AEM. {#run-pipeline}

Med det AEM projektet för SecurBank för sandlådedatabasen kan det distribueras med en pipeline.

1. Gå tillbaka till fliken **Översikt** i ditt sandlådeprogram i Cloud Manager och kör pipelinen för icke-produktion i helhög.

   * Avmarkera alla alternativ för pipeline-körningen.
   * Mer information om att köra rörledningar finns i dokumentet [Hantera rörledningar](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines).

### Hämta Cloud Manager-autentiseringsuppgifter för lokal webbappsutveckling. {#retrieve-credentials}

Innan du kan köra SecurBank-appen måste du ha Cloud Manager-autentiseringsuppgifter för att ansluta appen till Cloud Manager.

1. När pipeline körs går du tillbaka till fliken **Översikt** i Cloud Manager och trycker eller klickar på ellipsknappen bredvid miljönamnet och väljer **Developer Console**.

1. I Developer Console väljer du fliken **Integrationer**, sedan fliken **Lokal token** och trycker eller klickar på **Hämta lokal utvecklingstoken**.

1. En JSON-fil skapas med åtkomsttoken. Kopiera endast själva token (den återstående JSON är inte nödvändig) till en säker plats för användning i ett framtida steg innan du stänger Developer Console och återgår till Cloud Manager.

1. I Cloud Manager på fliken **Översikt** högerklickar du på miljöns URL-adress för att kopiera den och spara den på en säker plats för användning i ett framtida steg.

### Hämta och konfigurera SecurBanks webbapp. {#download-web-app}

Nu kan du hämta och konfigurera webbappen SecurBank.

1. Hämta den senaste SecurBank-appkoden från GitHub på [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events) genom att klicka på **Code** och sedan på **Download ZIP** i listrutan.

1. Dekomprimera innehållet i zip-filen i det lokala filsystemet.

1. Starta den önskade kodredigeraren och öppna den dolda miljöfilen i SecurBank-appprojektet på `summit-2024-l425-ue-z-final-with-events/react-app/.env`.

1. Gör följande ändringar i filen `.env` och spara ändringarna.

   * Klistra in värdet för den tidigare kopierade URL-adressen för din miljö för `REACT_APP_HOST_URI`.
   * Klistra in värdet för den tidigare kopierade lokala utvecklingstoken för `REACT_APP_DEV_TOKEN`.

### Kör webbappen SecurBank. {#run-web-app}

När allt är konfigurerat både i Cloud Manager och lokalt kan du köra webbappen SecurBank.

1. Gå till mappen `react-app` på kommandoraden på den lokala datorn för det SecurBank-appprojekt som du hämtade och dekomprimerade.

1. Installera SecurBank-appen med kommandot `node -i` i mappen `react-app`.

1. Starta SecurBank-appen med kommandot `npm start` när du har installerat den.

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

   * Och ett webbläsarfönster öppnas för URL:en `https://localhost:3000`.

      * Observera att detta är avsett för utvecklingsändamål och att inget giltigt certifikat tillhandahålls. Du kan därför behöva informera webbläsaren för att den ska kunna komma åt sidan.

Grattis! Nu bör du se när SecurBank-appen körs i webbläsaren.

Om innehållet inte visas än kontrollerar du att pipeline **Distribuera till Dev** som du har kört har slutförts.

![SecurBank-appen i webbläsaren](assets/securbank.png)
