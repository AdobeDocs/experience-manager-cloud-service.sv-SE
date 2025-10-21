---
title: Anpassa webbplatstemat
description: Lär dig hur webbplatstemat byggs, hur du anpassar och hur du testar med AEM-innehåll.
exl-id: b561bee0-3a64-4dd3-acb8-996f0ca5bfab
solution: Experience Manager Sites
feature: Developing
role: Admin, Developer
recommendations: display, noCatalog
source-git-commit: 0a458616afad836efae27e67dbe145fc44bee968
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 0%

---


# Anpassa webbplatstemat {#customize-the-site-theme}

{{traditional-aem}}

Lär dig hur webbplatstemat byggs, hur du anpassar och hur du testar med AEM-innehåll.

## Story hittills {#story-so-far}

I det föregående dokumentet på AEM-snabbwebbplatsprocessen [Hämta information om Git-databasåtkomst](retrieve-access.md) lärde du dig hur gränssnittsutvecklarna använder Cloud Manager för att få åtkomst till Git-databasinformation. Nu bör du:

* Lär dig mer om vad Cloud Manager är.
* Har hämtat dina inloggningsuppgifter för att få tillgång till AEM Git så att du kan implementera dina anpassningar.

Den här delen av resan tar nästa steg och går in i webbplatstemat och visar hur du anpassar det och sedan implementerar anpassningarna med de åtkomstautentiseringsuppgifter som du hämtade.

## Syfte {#objective}

I det här dokumentet förklaras hur AEM webbplatstema är uppbyggt, hur man anpassar det och hur man testar det med AEM direktinnehåll. När du har läst bör du:

* Förstå webbplatsens grundläggande struktur och hur du redigerar den.
* Se hur du testar dina temaanpassningar med verkligt AEM-innehåll via en lokal proxy.
* Lär dig implementera ändringarna i AEM Git-databasen.

## Ansvarig roll {#responsible-role}

Den här delen av resan gäller för den som utvecklar gränssnittet.

## Förstå temastrukturen {#understand-theme}

Extrahera temat från AEM-administratören till den plats där du vill redigera temat och öppna det i den redigerare du vill.

![Redigera temat](assets/edit-theme.png)

Du ser att temat är ett typiskt frontprojekt. De viktigaste delarna i strukturen är:

* `src/main.ts`: Huvudstartpunkten för JS- och CSS-temat
* `src/site`: JS- och CSS-filer som gäller för hela platsen
* `src/components`: JS- och CSS-filer specifika för AEM-komponenter
* `src/resources`: Statiska filer som ikoner, logotyper och teckensnitt

>[!TIP]
>
>Om du vill veta mer om AEM standardtema för webbplatser kan du läsa GitHub-länken i avsnittet [Ytterligare resurser](#additional-resources) i slutet av det här dokumentet.

När du känner dig trygg med temaprojektets struktur kan du starta den lokala proxyn så att du kan se alla temaanpassningar i realtid baserat på det faktiska AEM-innehållet.

## Starta den lokala proxyn {#starting-proxy}

1. Navigera från kommandoraden till temats rot på din lokala dator.
1. Kör `npm install` och npm hämtar beroenden och installerar projektet.

   ![npm-installation](assets/npm-install.png)

1. Kör `npm run live` och proxyservern startar.

   ![npm run live](assets/npm-run-live.png)

1. När proxyservern startas öppnas automatiskt en webbläsare till `http://localhost:7001/`. Välj **LOGGA IN LOKALT (ENDAST ADMIN TASKS)** och logga in med de proxyanvändarautentiseringsuppgifter som tillhandahålls av AEM-administratören.

   ![Logga in lokalt](assets/sign-in-locally.png)

   >[!TIP]
   >
   >Om du inte har dessa autentiseringsuppgifter kan du kontakta administratören och hänvisa till avsnittet [Konfigurera proxyanvändare i artikeln Skapa webbplats från mall](/help/journey-sites/quick-site/create-site.md#proxy-user) under den här resan.

1. När du är inloggad ändrar du URL:en i webbläsaren så att den pekar på sökvägen till exempelinnehållet som AEM-administratören har gett dig.

   * Om den angivna sökvägen till exempel var `/content/<your-site>/en/home.html?wcmmode=disabled`
   * Du ändrar URL:en till `http://localhost:7001/content/<your-site>/en/home.html?wcmmode=disabled`

   ![Proxiderat exempelinnehåll](assets/proxied-sample-content.png)

Du kan navigera på webbplatsen för att utforska innehållet. Webbplatsen hämtas direkt från AEM-instansen så att du kan anpassa temat efter det verkliga innehållet.

## Anpassa temat {#customize-theme}

Nu kan du börja anpassa temat. Följande är ett enkelt exempel som illustrerar hur du kan se ändringarna direkt via utkastet.

1. Öppna filen `<your-theme-sources>/src/site/_variables.scss` i redigeraren

   ![Redigera tema](assets/edit-theme.png)

1. Redigera variabeln `$color-background` och ange ett annat värde än vitt. I detta exempel används `orange`.

   ![Redigerat tema](assets/edited-theme.png)

1. När du sparar filen ser du att proxyservern känner igen ändringen via raden `[Browsersync] File event [change]`.

   ![Webbläsarsynkronisering för proxy](assets/proxy-browsersync.png)

1. När du växlar tillbaka till webbläsaren på proxyservern visas ändringen omedelbart.

   ![Orange tema](assets/orange-theme.png)

Du kan fortsätta att anpassa temat baserat på de krav som du har fått från AEM-administratören.

## Genomför ändringarna {#committing-changes}

När anpassningarna är klara kan du implementera dem i AEM Git-databasen. Först måste du klona databasen till din lokala dator.

1. Navigera från kommandoraden till den plats där du vill klona svaret.
1. Kör kommandot som du [tidigare har hämtat från Cloud Manager](retrieve-access.md). Det ska likna `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`. Använd Git-användarnamnet och lösenordet som [du hämtade i den tidigare delen av den här resan](retrieve-access.md).

   ![Klona repo](assets/clone-repo.png)

1. Flytta temaprojektet som du redigerade till det klonade svaret med ett kommando som liknar `mv <site-theme-sources> <cloned-repo>`
1. I katalogen för den klonade kopian implementerar du de temafiler som du just har flyttat till med följande kommandon.

   ```text
   git add .
   git commit -m "Adding theme sources"
   git push
   ```

1. Anpassningarna skickas till AEM Git-databasen.

   ![Ändringar har implementerats](assets/changes-committed.png)

Dina anpassningar lagras nu säkert i AEM Git-databasen.

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av AEM snabbwebbplats bör du:

* Förstå webbplatsens grundläggande struktur och hur du redigerar den.
* Se hur du testar dina temaanpassningar med verkligt AEM-innehåll via en lokal proxy.
* Lär dig implementera ändringarna i AEM Git-databasen.

Bygg vidare på den här kunskapen och fortsätt din resa till AEM Quick Site Creation genom att gå igenom dokumentet [Distribuera ditt anpassade tema](deploy-theme.md), där du får lära dig hur du distribuerar temat med hjälp av pipeline i gränssnittet.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av processen för att skapa snabbwebbplats genom att granska dokumentet [Distribuera ditt anpassade tema](deploy-theme.md), men följande är ytterligare, valfria resurser som gör en djupdykning i vissa koncept som nämns i det här dokumentet, men de behöver inte fortsätta på resan.

* [AEM Site Theme](https://github.com/adobe/aem-site-template-standard-theme-e2e) - Detta är GitHub-databasen för AEM Site Theme.
* [npm](https://www.npmjs.com) - AEM-teman som används för att snabbt skapa webbplatser baseras på npm.
* [webpack](https://webpack.js.org) - AEM-teman som används för att snabbt skapa webbplatser är beroende av webbpaket.
