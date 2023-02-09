---
title: Skapa och använda teman
description: Du kan använda teman för att stilisera och ge en visuell identitet till ett adaptivt formulär med hjälp av kärnkomponenterna. Du kan dela ett tema med ett valfritt antal adaptiva Forms.
source-git-commit: 6f6cf5657bf745a2e392a8bfd02572aa864cc69c
workflow-type: tm+mt
source-wordcount: '1597'
ht-degree: 0%

---


# Introduktion till teman för adaptiva formulär med hjälp av kärnkomponenter {#introduction-to-themes-for-af-using-core-components}

Du kan skapa och använda teman för att stilisera ett adaptivt formulär med hjälp av kärnkomponenterna. Ett tema innehåller formatinformation för komponenterna och panelerna. Format innehåller egenskaper som bakgrundsfärger, lägesfärger, genomskinlighet, justering och storlek. När du använder ett tema återspeglas det angivna formatet i motsvarande komponenter. Temat hanteras oberoende av varandra utan referens till ett adaptivt formulär.

När du [skapa ett adaptivt formulär](/help/forms/creating-adaptive-form.md) med hjälp av kärnkomponenter visas&quot;Out-of-the-Box&quot;-teman under **Stil** -fliken. Som standard är bara **Arbetsyta** temat är tillgängligt.

>[!NOTE]
>
>Ett anpassat formulärtema får inte blandas ihop med [Adaptiva formulärmallar.](/help/forms/template-editor.md) Adaptiva formulärteman innehåller bara formatinformation för ett adaptivt formulär. Anpassningsbara blankettmallar definierar formulärstrukturen och det ursprungliga innehållet och innehåller ett tema som gör det möjligt att skapa nya [Adaptiv form.](/help/forms/creating-adaptive-form.md)

## Använda Canvas-temat i Adaptive Forms med hjälp av kärnkomponenter {#using-theme-in-adaptive-form}

Steg för att tillämpa temat på ett adaptivt formulär är:

1. Logga in på din AEM Forms-författarinstans.

1. Tryck **Adobe Experience Manager** > **Forms** > **Forms och dokument**.

1. Klicka **Skapa** > **Adaptiv Forms**. Guiden för att skapa adaptiva formulär öppnas.

1. Välj kärnkomponentmallen i **Källa** -fliken.

   >[!NOTE]
   >
   > När du skapar ett adaptivt formulär med kärnkomponenter visas Canvas-temat på fliken Format. Det här är det enda färdiga temat som är tillgängligt just nu. Men du kan ändra temat efter dina önskemål och spara det för framtida bruk genom att skapa en frontpipeline.

1. Välj arbetsytans tema i **Stil** -fliken.
1. Klicka **Skapa**.

Adaptiva formulärteman används som en del av en adaptiv formulärmall för att definiera format när du skapar ett adaptivt formulär.

## Anpassa temat {#customizing-theme}

Om du vill anpassa ett tema

* [konfigurera en pipeline i Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline)
* Konfigurera en användare med [medarbetarroll](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html).
* Du borde ha en [grundläggande kunskaper i Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git) och Cloud Service Git-databaser.

Så här anpassar du ett Canvas-tema:
1. [Klona arbetsytans tema](#1-download-canvas-theme-download-canvas-theme)
1. [Förstå temats struktur](#2-understand-structure-of-the-canvas-theme-structure-of-canvas-theme)
1. [Skapa ](#3-create-the-env-file-in-a-theme-folder-creating-env-file-theme-folder)
1. [Starta den lokala proxyservern](#4-start-a-local-proxy-server-starting-a-local-proxy-server)
1. [Anpassa temat](#customize-the-theme-customizing-theme)
1. [Verkställ ändringarna](#6-committing-the-changes-committing-the-changes)
1. [Distribuera pipeline](#7-deploying-the-customized-theme-deploy-customized-theme)

### 1. Klona arbetsytans tema {#download-canvas-theme}

Öppna kommandotolken och kör följande kommando för att klona arbetsytans tema:

```
git clone https://github.com/adobe/aem-forms-theme-canvas
```

>[!NOTE]
>
> Fliken Format i guiden Skapa formulär visar samma temanamn som package.json .

### 2. Förstå temats struktur {#structure-of-canvas-theme}

Ett Adaptivt formulärtema är ett paket som innehåller CSS-, JavaScript- och statiska resurser som definierar formulärets format och som följer strukturen i ett adaptivt formulärtema. Ett Adaptivt formulärtema har följande struktur som är typisk för ett front end-projekt:

* `src/components`: JavaScript- och CSS-filer som är specifika för AEM kärnkomponenter
* `src/resources`: Statiska filer som ikoner, logotyper och teckensnitt
* `src/site`: JavaScript- och CSS-filer som gäller för hela AEM Sites-sidan
* `src/theme.ts`: Huvudstartpunkten för JavaScript- och CSS-temat
* `src\theme.scss`: JavaScript- och CSS-filer som gäller för hela temat

The `src/components` -mappen har JavaScript- och CSS-filer som är specifika för alla AEM kärnkomponenter som knapp, kryssruta, behållare, sidfot osv. Du kan formatera en knapp eller kryssruta genom att redigera CSS-filen som är specifik för AEM.

![Redigera temat](/help/forms/assets/theme_structure.png)

Om du vill anpassa temat kan du starta den lokala proxyservern och se temaanpassningarna i realtid baserat på det faktiska AEM innehållet.

### 3. Skapa .env-filen i en temamapp {#creating-env-file-theme-folder}

Skapa en `.env` i temamappen och lägg till följande parametrar:

* **AEM url**
AEM_URL=https://[author-instance] eller http://localhost:[port]/

* **AEM webbplatsnamn**
AEM_ADAPTIVE_FORM=Form_name

* **AEM proxyport**
AEM_PROXY_PORT=7000


![Arbetsytans temastruktur](/help/forms/assets/env-file-canvas-theme.png)

### 4. Starta en lokal proxyserver {#starting-a-local-proxy-server}

1. Navigera från kommandoraden till temats rot på din lokala dator.
1. Kör `npm install` och npm hämtar beroenden och installerar projektet.
1. Kör `npm run live` och proxyservern startas.

   ![npm run live](/help/forms/assets/theme_proxy.png)

1. När proxyservern startas öppnas automatiskt en webbläsare för att `http://localhost:[port]/`.
1. Tryck eller klicka **LOGGA IN LOKALT (ENDAST ADMINISTRATÖRSÅTGÄRDER)** och logga in med de autentiseringsuppgifter för proxyanvändare som du har fått från AEM.

   ![Logga in lokalt](/help/forms/assets/local_signin.png)

   >[!NOTE]
   >
   > * Skapa en lokal användare som kan logga in lokalt. Ange deltagarroll för temadesigner.
   > * Om du anger AEM URL som `http://localhost:[port]/` i `.env` -filen med Canvas-temat omdirigeras du direkt till webbläsaren.


1. När du är inloggad ändrar du URL:en i webbläsaren så att den pekar på sökvägen till exempelinnehållet som AEM har gett dig.

   * Om den angivna sökvägen till exempel `/content/formname.html?wcmmode=disabled`, ändra URL:en till `http://localhost:[port]/content/forms/af/formname.html?wcmmode=disabled`

   ![Proxyinnehåll](/help/forms/assets/sample_af.png)

Navigera till ett adaptivt formulär och se arbetsytans tema som används i ett adaptivt formulär.

### 5. Anpassa temat {#customize-theme}

1. Öppna filen i redigeraren `<your-theme-sources>/src/site/_variables.scss`.

   >[!NOTE]
   >
   > Du kan formatera alla adaptiva formulärkomponenter direkt på en plats genom att redigera `site/_variables.scss` -fil.

1. Redigera variabeln för `font colour` till `red`.

   ![Redigera tema](/help/forms/assets/edit_theme.png)

   **Formatera de olika AEM**

   Du kan formatera de olika komponenterna i ett adaptivt formulär genom att ändra dess CSS-fil i redigeraren. Det finns olika CSS-mappar för varje komponent i kärnan Adaptiv form i mappen Tema på arbetsytan.

   ![Kärnkomponent](/help/forms/assets/theme-component.png)

   Om du vill ange format för en viss komponent i temaredigeraren kan du redigera CSS-koden i en temamapp. Om du till exempel vill ändra kantfärgen för ett textrutefält öppnar du CSS-filen i redigeraren och ändrar kantfärgen.

   ![Redigera CSS för textruta](/help/forms/assets/edit_color_textbox.png)

1. När du sparar filen känner proxyservern igen ändringen via raden `[Browsersync] File event [change]`.

   ![Webbläsarsynk för proxy](/help/forms/assets/browser_sync.png)

1. När du växlar tillbaka till webbläsaren på den lokala proxyservern visas ändringen omedelbart.

   ![ändra AF-tema](/help/forms/assets/edit_theme_af.png)

Temadesigner förhandsgranskar ändringarna på den lokala proxyservern och anpassar temat enligt kraven för olika AEM.

Innan du implementerar ändringarna i AEM Git-databasen måste du få åtkomst till [Git-databasinformation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git).

### 6. Verkställ ändringarna {#committing-the-changes}

När du har ändrat temat och testat det med en lokal proxyserver implementerar du ändringarna i Git-databasen för din AEM Forms-Cloud Service. Det gör det anpassade temat tillgängligt i Forms Cloud Service-miljön så att designers av Adaptive Forms kan använda det.

Innan du implementerar ändringar i Git-databasen för din AEM Forms-Cloud Service måste du klona databasen på den lokala datorn. Så här klonar du databasen:

1. Öppna kommandotolken och kör nedanstående kommando när du har ersatt [min-org] och [mitt program] med värden från AEM. Du kan även hitta information i [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git):

   ```
   git clone https://git.cloudmanager.adobe.com/[my-org]/[my-org]/
   ```
1. Flytta temaprojektet som du redigerade till det klonade svaret med ett kommando som liknar `mv <theme-sources> <cloned-repo>`.
1. Gör önskade ändringar i temakomponentmapparna genom att ändra dess CSS-fil.
1. I katalogen för den klonade databasen implementerar du de temafiler som du just har flyttat till med följande kommandon.

   ```text
   git add <theme-file-name>
   git commit -m "Adding theme sources"
   git push
   ```

1. Anpassningarna skickas till Git-databasen.

   ![Utförda ändringar](/help/forms/assets/cmd_git_push.png)

Dina anpassningar lagras nu säkert i Git-databasen.


### 7. Distribuera frontpipeline {#deploy-pipeline}

Driftsätt ditt anpassade tema med hjälp av frontendriet. Lär dig [hur du ställer in en pipeline för första raden för att distribuera anpassat tema](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline).


>[!NOTE]
>
>Om du gör några ändringar i temamappen för arbetsytan i framtiden måste du köra pipelinen ovan igen. Det är därför nödvändigt att komma ihåg rörledningens namn.

## Exempel på hur du anpassar temat {#example-to-customize-a-theme}

1. Logga in på din AEM Forms-författarinstans.
1. Öppna ett adaptivt formulär som skapats med kärnkomponenter.
1. Starta den lokala proxyservern med kommandotolken och klicka på **LOGGA IN LOKALT (ENDAST ADMINISTRATÖRSÅTGÄRDER)**.
1. När du har loggat in omdirigeras du till webbläsaren och ser det aktuella temat.
1. Hämta Canvas-temat och extrahera den hämtade zip-mappen.
1. Öppna den extraherade zip-mappen i det redigeringsprogram du föredrar.
1. Skapa en `.env` i temamappen och lägg till parametrar: **AEM URL**, **AEM_ADAPTIVE_FORM** och **AEM_PROXY_PORT**.
1. Öppna CSS-filen för textrutan i temamappen för arbetsytan och ändra kantfärgen till `red` och spara ändringarna.
1. Öppna webbläsaren igen och du ser ändringarna direkt i ett adaptivt formulär.
1. Flytta temamappen för arbetsytan i din klonade databas.
1. Verkställ ändringarna och distribuera frontendriet.

När du har kört pipeline är temat tillgängligt under fliken Format.

## God praxis {#best-practices}

* **Undvika resurser från ett annat tema**

   När du redigerar ett tema kan du bläddra bland och lägga till resurser (till exempel bilder) från andra teman. Du redigerar till exempel bakgrunden på en sida. Om du till exempel väljer **[!UICONTROL Page]** ![edit-button](assets/edit-button.png)> **[!UICONTROL Background]** > **[!UICONTROL Add]** > **[!UICONTROL Image]** visas en dialogruta där du kan bläddra bland och lägga till bilder i andra teman.

   Du kan stöta på problem med det aktuella temat om en resurs läggs till från ett annat tema och det andra temat flyttas eller tas bort. Du bör undvika att bläddra bland och lägga till resurser från andra teman.

* **Ändra layoutbredd för behållarpanelen**

   Du bör inte ändra bredden på behållarpanelens layout. När du anger bredden på en behållarpanel blir den statisk och anpassas inte till olika skärmar.

* **Använda formulärredigeraren eller temaredigeraren för att arbeta med sidhuvud och sidfot**

   Använd temaredigeraren om du vill formatera sidhuvud och sidfot med formatalternativ som teckensnittsformat, bakgrund och genomskinlighet.
Om du vill ange information som logotypbild, företagsnamn i sidhuvud och copyrightinformation i sidfoten använder du alternativen för formulärredigeraren.
