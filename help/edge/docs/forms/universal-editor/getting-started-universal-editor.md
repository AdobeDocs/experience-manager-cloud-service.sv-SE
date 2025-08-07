---
title: Komma igång med Edge Delivery Services för AEM Forms med Universal Editor
description: Lär dig hur du skapar och publicerar högpresterande formulär med hjälp av den universella redigerarens WYSIWYG-redigering.
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 24a23d98-1819-4d6b-b823-3f1ccb66dbd8
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '2116'
ht-degree: 0%

---


# Komma igång med Edge Delivery Services för AEM Forms med Universal Editor

| Redigeringsmetod | Guide |
|---------------------------------|-----------------------------------------------------------------------|
| **Universell redigerare (WYSIWYG)** | Den här artikeln |
| **Dokumentbaserad redigering** | [Dokumentbaserad självstudiekurs](/help/edge/docs/forms/tutorial.md) |

Edge Delivery Services for AEM Forms kombinerar högpresterande webbpublicering med WYSIWYG i Universal Editor. Den här guiden beskriver hur du skapar, anpassar och publicerar snabbt inlästa formulär.

## Vad du kommer att göra

I slutet av kursen kommer du att:

- Konfigurera en GitHub-databas med det adaptiva Forms-blocket
- Skapa en AEM Site som är integrerad med Edge Delivery Services
- Bygg och publicera blanketter med Universal Editor
- Konfigurera lokal utvecklingsmiljö

## Välj din sökväg

Välj den metod som matchar ditt scenario:

![Välj vägbeslutsguide](/help/edge/docs/forms/universal-editor/assets/choose-your-path.svg)
*Figur: Visuell guide som hjälper dig att välja rätt implementeringsväg*

| **Sökväg A: Nytt projekt** | **Sökväg B: Befintligt projekt** |
|----------------------------------------|-------------------------------------------|
| Börja med en förkonfigurerad mall | Lägg till formulär i ditt aktuella AEM-projekt |
| **Bäst för:** Nya implementeringar | **Bäst för:** Befintlig AEM Sites |
| **Vad du får:** Förkonfigurerat Forms-block | **Vad du får:** Forms har lagts till på en befintlig webbplats |
| **Steg:** Mall → Konfigurera → Forms | **Steg:** Integration → Konfiguration → Forms |
| [Börja med sökväg A](#path-a-create-new-project-with-forms) | [Börja med sökväg B](#path-b-add-forms-to-existing-project) |

## Förutsättningar

Innan du börjar bör du kontrollera att du har följande:

### Nödvändig åtkomst

- **GitHub-konto** med behörighet att skapa databaser
- **Redigeringsåtkomst för AEM as a Cloud Service**

### Tekniska krav

- **Git-grunder**: klona, genomföra, push-åtgärder
- **Webbtekniker**: Grundläggande om HTML, CSS, JavaScript
- **Node.js** (version 16+ rekommenderas) för lokal utveckling
- Pakethanteraren **npm** eller **garn**

### Rekommenderad kunskap

- Grundläggande förståelse för AEM Sites koncept
- Välbekant med principer för formulärdesign
- Upplevelser med WYSIWYG-redigerare

>[!TIP]
>
> Har du inte använt AEM tidigare? Börja med [AEM Sites Starthandbok](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html?lang=sv-SE).

## Sökväg A: Skapa nytt projekt med Forms

**Bäst för:** Nya implementeringar eller konceptkorrektur

AEM Forms Boilerplate är en förkonfigurerad mall med inbyggt Adaptive Forms Block.

### Översikt över steg

1. Konfigurera en GitHub-databas från mallen
2. Installera AEM Code Sync
3. Konfigurera AEM-projektanslutning
4. Skapa och publicera en AEM-webbplats
5. Lägga till formulär med Universal Editor

Vi går igenom varje steg:

+++steg 1: Skapa GitHub-databas från mall

1. **Öppna AEM Forms-mallen för mallar**
   - Gå till [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms)

   ![AEM Forms-mallmall](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   *Bild: AEM Forms-standarddatabas med förkonfigurerat adaptivt Forms-block*

2. **Skapa din databas**
   - Klicka på **Använd mallen** > **Skapa en ny databas**

   ![Skapa databas från mall](/help/edge/docs/forms/assets/use-eds-form-template.png)
   *Figur: Använda mallen för att skapa en ny databas*

3. **Konfigurera databasinställningar**
   - **Ägare**: Välj ditt GitHub-konto eller din organisation
   - **Databasnamn**: Välj ett beskrivande namn (till exempel `my-forms-project`)
   - **Synlighet**: Välj **Offentlig** (rekommenderas för Edge Delivery Services)
   - Klicka på **Skapa databas**

   ![Databaskonfiguration](/help/edge/docs/forms/assets/name-eds-repo.png)
   *Bild: Konfigurera din nya databas med synlighet*

**Validering:** Bekräfta att du har en ny GitHub-databas som är baserad på AEM Forms-mallen Boilerplate.

+++

+++Steg 2: Installera AEM Code Sync

AEM Code Sync synkroniserar automatiskt innehållsändringar mellan din AEM-redigeringsmiljö och din GitHub-databas.

1. **Installera GitHub App**
   - Gå till [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new)

2. **Konfigurera åtkomstbehörigheter**
   - Välj **Välj bara databaser**
   - Välj din nya databas
   - Klicka på **Spara**

   ![Installation av AEM Code Sync](/help/edge/docs/forms/assets/aem-code-sync-up.png)
   *Bild: Installerar AEM Code Sync med databasspecifika behörigheter*

**Kontrollpunkt:** AEM Code Sync är nu installerat och har åtkomst till din databas.

+++

+++steg 3: Konfigurera AEM-integrering

Filen `fstab.yaml` ansluter din GitHub-databas till AEM-redigeringsmiljö för innehållssynkronisering.

1. **Navigera till din databas**
   - Gå till din nya GitHub-databas
   - Du bör se AEM Forms-mallfilerna

2. **Skapa filen fstab.yaml**
   - Klicka på **Lägg till fil** > **Skapa ny fil** i rotkatalogen
   - Namnge filen `fstab.yaml`

   ![Skapar fstab.yaml-fil](/help/edge/docs/forms/assets/open-fstab.png)
   *Figur: Skapar konfigurationsfilen fstab.yaml*

3. **Lägg till din AEM-anslutningsinformation**

   Kopiera och klistra in följande konfiguration och ersätt platshållarna:

   ```yaml
   mountpoints:
     /: https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main
   ```

   **Ersätt:**
   - `<aem-author>`: Din URL för AEM as a Cloud Service-författare (t.ex. `author-p12345-e67890.adobeaemcloud.com`)
   - `<owner>`: ditt GitHub-användarnamn eller din organisation
   - `<repository>`: Ditt databasnamn

   **Exempel:**

   ```yaml
   mountpoints:
     /: https://author-p12345-e67890.adobeaemcloud.com/bin/franklin.delivery/mycompany/my-forms-project/main
   ```

   ![Redigerar filen fstab.yaml](/help/edge/docs/forms/assets/edit-fstab-file.png)
   *Bild: Konfigurerar monteringspunkten för AEM-integrering*

4. **Bekräfta konfigurationen**
   - Lägg till ett implementeringsmeddelande: &quot;Add AEM integration configuration&quot;
   - Klicka på **Genomför ny fil**

   ![Bekräftar FTDB-ändringar](/help/edge/docs/forms/assets/commit-fstab-changes.png)
   *Bild: Bekräftar fstab.yaml-konfigurationen*

**Validering:** Bekräfta din GitHub-databasanslutning till AEM.

>[!NOTE]
>
>Har du byggproblem? Se [Felsökning av GitHub-byggproblem](#troubleshooting-github-build-issues).

+++

+++steg 4: Skapa en AEM-webbplats som är ansluten till din GitHub-databas.

1. **Öppna AEM Sites-konsolen**
   - Logga in i din AEM as a Cloud Service-instans
   - Navigera till **Webbplatser**

   ![AEM Sites Console](/help/edge/assets/select-sites.png)
   *Bild: Åtkomst till AEM Sites-konsolen*

2. **Börja skapa webbplats**
   - Klicka på **Skapa** > **Plats från mall**

   ![Skapa platsalternativ](/help/edge/docs/forms/assets/create-sites.png)
   *Figur: Skapa en ny webbplats från mallen*

3. **Välj Edge Delivery Services-mallen**
   - Välj mallen **Edge Delivery Services Site**
   - Klicka på **Nästa**

   ![Val av platsmall](/help/edge/docs/forms/assets/select-site-template.png)
   *Bild: Välja Edge Delivery Services-webbplatsmall*

   >[!NOTE]
   >
   >**Mallen är inte tillgänglig?** Om du inte ser Edge Delivery Services-mallen:
   >
   >1. Klicka på **Importera** för att överföra mallen
   >2. Hämta mallar från [GitHub-versioner](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases)

4. **Konfigurera din plats**

   Ange följande information:

   | Fält | Värde | Exempel |
   |-----------------|-----------------------------|-----------------------------------------|
   | **Platstitel** | Beskrivande namn för webbplatsen | &quot;Mitt Forms-projekt&quot; |
   | **Platsnamn** | URL-vänligt namn | &quot;my-forms-project&quot; |
   | **GitHub-URL** | Din databas-URL | `https://github.com/mycompany/my-forms-project` |

   ![Platskonfiguration](/help/edge/docs/forms/assets/create-aem-site.png)
   *Bild: Konfigurera din nya AEM-webbplats med GitHub-integrering*

5. **Slutför webbplatsskapandet**
   - Granska dina inställningar
   - Klicka på **Skapa**

   ![Bekräfta skapande av webbplats](/help/edge/docs/forms/assets/click-ok-aem-site.png)
   *Bild: Bekräfta skapande av webbplats*

   **Klart!** Din AEM-webbplats har nu skapats och är ansluten till GitHub.

6. **Öppna i Universal Editor**
   - Leta reda på din nya plats i webbplatskonsolen
   - Välj sidan `index`
   - Klicka på **Redigera**

   ![Redigera plats i universell redigerare](/help/edge/docs/forms/assets/edit-site.png)
   *Bild: Öppnar webbplatsen för redigering*

   Universal Editor öppnas på en ny flik med funktioner för WYSIWYG-redigering.

   ![Universellt redigeringsgränssnitt](/help/edge/docs/forms/assets/site-in-universal-editor.png)
   *Bild: Din webbplats har öppnats i Universal Editor för WYSIWYG-redigering*

**Verifiering:** Bekräfta att din AEM-webbplats är klar för formulärredigering.

+++

+++Steg 5: Publicera din webbplats

Med publicering blir din webbplats tillgänglig på Edge Delivery Services för global åtkomst.

1. **Snabbpublicering från webbplatskonsolen**
   - Återgå till AEM Sites Console
   - Markera dina webbplatssidor (eller markera alla med Ctrl+A)
   - Klicka på **Snabbpublicering**

   ![Publicerar AEM-webbplats](/help/edge/docs/forms/assets/publish-sites.png)
   *Figur: Välja sidor för snabb publicering*

2. **Bekräfta publicering**
   - Klicka på **Publicera** i bekräftelsedialogrutan

   ![Dialogrutan Snabbpublicering](/help/edge/docs/forms/assets/quick-publish.png)
   *Bild: Bekräfta publiceringsåtgärden*

   **Alternativ:** Du kan även publicera direkt från Universal Editor med knappen Publicera.

   ![Publicera från universell redigerare](/help/edge/docs/forms/assets/qui.png)
   *Figur: Publicera direkt från Universal Editor*

3. **Åtkomst till din aktiva webbplats**

   Webbplatsen finns nu på:

   ```
   https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/
   ```

   **URL-strukturen förklaras:**
   - `<branch>`: GitHub-gren (vanligen `main`)
   - `<repo>`: Ditt databasnamn
   - `<owner>`: ditt GitHub-användarnamn eller din organisation
   - `<site-name>`: Ditt AEM-webbplatsnamn

   **Exempel:**

   ```
   https://main--my-forms-project--mycompany.aem.page/content/my-forms-project/
   ```

**Verifiering:** Bekräfta att din webbplats är publicerad på Edge Delivery Services.

>[!TIP]
>
> **URL-mönster:**
>
> - **Startsida:** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
> - **Andra sidor:** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<page-name>`

**Nästa:** [Skapa ditt första formulär](#create-your-first-form)

+++

## Sökväg B: Lägg till Forms i befintligt projekt

**Bäst för:** Befintlig AEM Sites med Edge Delivery Services

Om du redan har ett AEM-projekt med Edge Delivery Services kan du lägga till formulärfunktioner genom att integrera Adaptive Forms Block.

### Krav för sökväg B

- Befintliga AEM-projekt som byggts med [AEM Boilerplate XWalk](https://github.com/adobe-rnd/aem-boilerplate-xwalk)
- Lokal utvecklingsmiljö har konfigurerats
- Git-åtkomst till projektdatabasen

**Använder AEM Forms-mallsida?** Om ditt projekt skapades med [AEM Forms-standardmallen](https://github.com/adobe-rnd/aem-boilerplate-forms) är formulär redan integrerade. Hoppa till [Skapa ditt första formulär](#create-your-first-form).

Vi går igenom varje steg:

### Översikt över steg

1. Kopiera adaptiva Forms Block-filer
2. Uppdatera projektkonfiguration
3. Konfigurera ESLint-regler
4. Bygg och implementera ändringar

+++steg 1: Kopiera Forms-blockfiler

1. **Navigera till ditt lokala projekt**

   ```bash
   cd /path/to/your/aem-project
   ```

2. **Hämta nödvändiga filer från AEM Forms-standardmallen**

   Kopiera de här filerna från [AEM Forms-databasen ](https://github.com/adobe-rnd/aem-boilerplate-forms):

   | Source | Mål | Syfte |
   |------------------------------------------------------------------------|----------------------------|----------------------------|
   | [`blocks/form/`](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form) | `blocks/form/` | Kärnfunktioner |
   | [`scripts/form-editor-support.js`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js) | `scripts/form-editor-support.js` | Integrering med Universal Editor |
   | [`scripts/form-editor-support.css`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css) | `scripts/form-editor-support.css` | Redigerarens format |

3. **Stöd för uppdateringsredigerare**
   - Ersätt din `/scripts/editor-support.js`-fil med [editor-support.js från AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js)

**Verifiering:** Bekräfta att formulärblocksfiler finns i ditt projekt.

+++

+++steg 2: Uppdatera komponentkonfiguration

1. **Uppdatera avsnittsmodell**

   Öppna `/models/_section.json` och lägg till formulärkomponenter i filtren:

   ```json
   {
        "filters": [
        {
      "id": "section",
      "components": [
           "text",
           "image",
           "button",
        "form",
        "embed-adaptive-form"
      ]
       }
     ]
   }
   ```

   **Vad detta gör:** Aktiverar formulärkomponenter i komponentväljaren för Universal Editor.

**Verifiering:** Bekräfta formulärkomponenter visas i Universell redigerare.

+++

+++steg 3: Konfigurera ESLint (valfritt)

**Varför det här steget:** Förhindrar lintingfel från formulärspecifika filer och konfigurerar korrekta valideringsregler.

1. **Uppdatera .eslintignore**

   Lägg till de här raderna i `/.eslintignore`:

   ```bash
   # Form block rule engine files
    blocks/form/rules/formula/*
    blocks/form/rules/model/*
    blocks/form/rules/functions.js
    scripts/editor-support.js
    scripts/editor-support-rte.js
   ```

2. **Uppdatera .eslintrc.js**

   Lägg till de här reglerna i objektet `rules` i `/.eslintrc.js`:

   ```javascript
   {
     "rules": {
       // Existing rules...
   
       // Form component cell limits
    'xwalk/max-cells': ['error', {
         '*': 4, // default limit
      form: 15,
      wizard: 12,
      'form-button': 7,
      'checkbox-group': 20,
      checkbox: 19,
      'date-input': 21,
      'drop-down': 19,
      email: 22,
      'file-input': 20,
      'form-fragment': 15,
      'form-image': 7,
      'multiline-input': 23,
      'number-input': 22,
      panel: 17,
      'radio-group': 20,
      'form-reset-button': 7,
      'form-submit-button': 7,
      'telephone-input': 20,
      'text-input': 23,
      accordion: 14,
      modal: 11,
      rating: 18,
      password: 20,
         tnc: 12
       }],
   
       // Disable this rule for forms
       'xwalk/no-orphan-collapsible-fields': 'off'
     }
   }
   ```

**Validering:** Bekräfta ESLint fungerar med formulärkomponenter.

+++

+++Steg 4: Skapa och distribuera

1. **Installera beroenden och bygg**

   ```bash
   # Install any new dependencies
   npm install
   
   # Build component definitions
   npm run build:json
   ```

   **Vad detta gör:**
   - Uppdaterar `component-definition.json` med formulärkomponenter
   - Skapar `component-models.json` med formulärmodeller
   - Skapar `component-filters.json` med filtreringsregler

2. **Verifiera genererade filer**

   Kontrollera att de här filerna i projektroten innehåller formulärrelaterade objekt:
   - `component-definition.json`
   - `component-models.json`
   - `component-filters.json`

3. **Verkställ och skicka ändringar**

   ```bash
   git add .
   git commit -m "Add Adaptive Forms Block integration"
   git push origin main
   ```

**Validering:** Bekräfta att ditt projekt innehåller formulärfunktioner.

+++

**Nästa:** [Skapa ditt första formulär](#create-your-first-form)

## Skapa ditt första formulär

**Gäller för:** Både användare med sökvägen A och B

Nu när ditt projekt är uppbyggt med formulärfunktioner kan vi skapa ditt första formulär med Universal Editors WYSIWYG-gränssnitt.

### Översikt över processen att skapa formulär

1. **Lägg till anpassat formulärblock** på sidan
2. **Lägg till formulärkomponenter** (textinmatningar, knappar osv.)
3. **Konfigurera komponentegenskaper**
4. **Förhandsgranska och testa** formuläret
5. **Publicera** den uppdaterade sidan

Vi går igenom varje steg:

+++steg 1: Lägg till anpassat formulärblock

1. **Öppna sidan i Universal Editor**
   - Navigera till konsolen **Platser** i AEM
   - Markera sidan där du vill lägga till ett formulär (t.ex. `index`)
   - Klicka på **Redigera**

   Sidan öppnas i Universal Editor för WYSIWYG-redigering.

2. **Lägg till komponenten Adaptivt formulär**
   - Öppna panelen **Innehållsträd** (vänster sidospalt)
   - Navigera till ett avsnitt där du vill lägga till formuläret
   - Klicka på ikonen **Lägg till** (+)
   - Välj **Adaptivt formulär** i komponentlistan

   ![Lägger till adaptivt formulärblock](/help/edge/docs/forms/assets/add-adaptive-form-block.png)
   *Bild: Lägga till ett adaptivt formulärblock på sidan*

**Verifiering:** Bekräfta att du har en tom formulärbehållare.

+++

+++steg 2: Lägg till formulärkomponenter

1. **Navigera till ditt formulärblock**
   - Leta reda på ditt nya adaptiva formuläravsnitt i innehållsträdet

   ![Adaptivt formulärblock tillagt](/help/edge/docs/forms/assets/adative-form-block.png)
   *Figur: Adaptivt formulärblock i innehållsträdet*

2. **Lägg till formulärkomponenter**

   Du kan lägga till komponenter på två sätt:

   **Metod A: Klicka för att lägga till**
   - Klicka på ikonen **Lägg till** (+) i formuläravsnittet
   - Välj komponenter i listan **Adaptiva formulärkomponenter**

   **Metod B: Dra och släpp**
   - Dra komponenter direkt från komponentpanelen till formuläret

   ![Lägger till formulärkomponenter](/help/edge/docs/forms/assets/add-component.png)
   *Figur: Lägga till komponenter i formuläret*

   **Rekommenderade startkomponenter:**
   - Textindata (för namn, e-post)
   - Textområde (för meddelanden)
   - Skicka-knapp

3. **Konfigurera komponentegenskaper**
   - Markera en formulärkomponent
   - Använd panelen **Egenskaper** (höger sidofält) för att konfigurera:
      - Etiketter och platshållare
      - Valideringsregler
      - Obligatoriska fältinställningar

   ![Panelen Komponentegenskaper](/help/edge/docs/forms/assets/component-properties.png)
   *Figur: Konfigurera komponentegenskaper*

4. **Förhandsgranska formuläret**

   Formuläret ser ut ungefär så här:

   ![Förhandsgranskning av slutfört formulär](/help/edge/docs/forms/assets/added-form-aem-sites.png)
   *Figur: Exempelformulär som har skapats med den universella redigeraren*

**Verifiering:** Bekräfta att formuläret är klart för publicering.

>[!IMPORTANT]
>
> Kom ihåg att publicera sidan när du har gjort ändringar för att se uppdateringar i webbläsaren.

+++

+++Steg 3: Publicera formuläret

1. **Publicera från universell redigerare**
   - Klicka på knappen **Publicera** i Universell redigerare

   ![Publicerar formulär](/help/edge/docs/forms/assets/publish-form.png)
   *Figur: Publicera formuläret från den universella redigeraren*

2. **Bekräfta publicering**
   - Klicka på **Publicera** i bekräftelsedialogrutan

   ![Bekräfta publicering](/help/edge/docs/forms/assets/publish-form1.png)
   *Bild: Bekräfta publiceringsåtgärden*

   Ett meddelande som bekräftar publiceringen visas.

   ![Publiceringen lyckades](/help/edge/docs/forms/assets/publish-form2.png)
   *Figur: Publiceringsbekräftelse lyckades*

3. **Visa ditt live-formulär**

   Ditt formulär finns nu på:

   ```
   https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/
   ```

   **Exempel-URL:**

   ```
   https://main--my-forms-project--mycompany.aem.page/content/my-forms-project/
   ```

   ![Live-formulärsida](/help/edge/docs/forms/assets/publish-index-page.png)
   *Figur: Din publicerade formulärsida på Edge Delivery Services*

**Grattis!** Ditt formulär är nu öppet och kan samla in inskickade svar.

+++

### Nästa steg

Nu när du har ett fungerande formulär kan du:

- **Anpassa format** genom att redigera CSS- och JavaScript-filer
- **Lägg till avancerade formulärfunktioner**, som valideringsregler och villkorslogik
- **Konfigurera lokal utveckling** för snabbare iteration
- **Skapa fristående formulär** för särskilda användningsfall

>[!TIP]
>
> **Läs mer:** [Skapa fristående formulär i Universal Editor](/help/edge/docs/forms/universal-editor/create-forms.md)

## Konfigurera lokal utvecklingsmiljö

**Passar bäst för:** Utvecklare som vill anpassa formulärformatering och -beteende

Med en lokal utvecklingsmiljö kan du göra ändringar och se dem direkt utan att behöva gå igenom publiceringscykeln.

+++Konfigurera AEM CLI och lokal utveckling

1. **Installera AEM CLI**

   AEM CLI förenklar lokala utvecklingsuppgifter:

   ```bash
   npm install -g @adobe/aem-cli
   ```

2. **Klona din databas**

   ```bash
   git clone https://github.com/<owner>/<repo>
   cd <repo>
   ```

   Ersätt `<owner>` och `<repo>` med dina faktiska GitHub-uppgifter.

3. **Starta den lokala utvecklingsservern**

   ```bash
   aem up
   ```

   Detta startar en lokal server med funktioner för att ladda upp filer under drift.

4. **Gör anpassningar**

   - Redigera filer i katalogen `blocks/form/` för formulärformat och -beteende
   - Ändra `form.css` för formatering
   - Uppdatera `form.js` för beteende

   **Se ändringarna direkt** i webbläsaren på `http://localhost:3000`

5. **Distribuera dina ändringar**

   ```bash
   git add .
   git commit -m "Custom form styling"
   git push origin main
   ```

   Ändringarna finns på:
   - **Förhandsgranska:** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`
   - **Produktion:** `https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`

+++


## Felsökning

### Vanliga problem och lösningar

+++GitHub Build Issues

**Problem:** Fel vid skapande eller lintingfel

**Lösning 1: Hantera lintingfel**

Om det uppstår lintingfel:

1. Öppna `package.json` i projektets rot
2. Hitta skriptet `lint`:

   ```json
   "scripts": {
     "lint": "npm run lint:js && npm run lint:css"
   }
   ```

3. Inaktivera linting tillfälligt:

   ```json
   "scripts": {
     "lint": "echo 'skipping linting for now'"
   }
   ```

4. Verkställ och skicka ändringarna

**Lösning 2: Sökvägsfel för modul**

Om du ser&quot;Det går inte att matcha sökvägen till modulen &#39;/scripts/lib-franklin.js&#39;&quot;:

1. Navigera till `blocks/form/form.js`
2. Uppdatera importsatsen:

   ```javascript
   // Change this:
   import { ... } from '/scripts/lib-franklin.js';
   
   // To this:
   import { ... } from '/scripts/aem.js';
   ```

+++

+++Universal Editor Issues

**Problem:** Formulärkomponenter visas inte i den universella redigeraren

**Lösningar:**

- Kontrollera att AEM Code Sync är installerat och körs
- Kontrollera att `fstab.yaml` har rätt URL för AEM-författare
- Kontrollera att tidig åtkomst är aktiverat för din AEM-instans
- Bekräfta att `component-definition.json` innehåller formulärkomponenter

**Problem:** Ändringar som inte visas efter publicering

**Lösningar:**

- Vänta på CDN-cacheuppdatering
- Kontrollera webbläsarens cacheminne (prova incognito/private mode)
- Kontrollera att rätt URL-format används

+++

+++Formulärfunktionsproblem

**Problem:** Formuläröverföringar fungerar inte

**Lösningar:**

- Kontrollera att du har en komponent för Skicka-knapp
- Kontrollera URL-konfiguration för formuläråtgärd
- Verifiera formulärverifieringsregler
- Testa i förhandsgranskningsläge först

**Problem:** Formateringsproblem

**Lösningar:**

- Kontrollera CSS-filsökvägar i `blocks/form/`
- Rensa webbläsarcache
- Verifiera CSS-syntax
- Testa i den lokala utvecklingsmiljön

+++

