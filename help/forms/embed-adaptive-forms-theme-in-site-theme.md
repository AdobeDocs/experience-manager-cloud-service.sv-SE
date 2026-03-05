---
title: Bädda in ett adaptivt Forms-tema i ett AEM Sites-tema
description: Lär dig hur du integrerar ett adaptivt Forms-tema (till exempel Canvas) i ett AEM Sites-tema så att webbplatssidor och inbäddad adaptiv Forms delar ett enhetligt tema och en enhetlig driftsättning.
keywords: adaptivt formulärtema, webbplatstema, AEM Sites-tema, integration av formulärteman, pipeline för frontend, temainbäddning
feature: Adaptive Forms, Core Components
role: Developer
exl-id: a1f8c4d2-3e5b-4a2f-9b7e-2d4f6a8c1b0e
source-git-commit: 2aa13887949507ab74c45b4b6f3135aebd59c6ea
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 0%

---

# Bädda in ett adaptivt Forms-tema i ett AEM Sites-tema

Du kan bädda in ett adaptivt Forms-tema (till exempel [AEM Forms Canvas-temat](https://github.com/adobe/aem-forms-theme-canvas)) i ditt AEM Sites-tema. På så sätt kör ett enda tema både dina webbplatssidor och alla adaptiva Forms-filer som är inbäddade på dessa sidor, med ett bygge och en distribution via [AEM Front-End Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html?lang=sv-SE).

Den här artikeln är avsedd för utvecklare som vill ha anpassade AEM Sites-standardteman (eller anpassade) utan att behöva hantera en separat Forms-temadistribution.

## Förutsättningar {#prerequisites}

Kontrollera att du har:

* **AEM as a Cloud Service** med [Front-End Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html?lang=sv-SE) konfigurerad för ditt webbplatstema.
* **Källor för webbplatsteman** - till exempel [standardtemat för webbplatsmallen](https://github.com/adobe/aem-site-template-standard) (den repo som innehåller `theme/` med `src/theme.scss`, `src/components/` och så vidare).
* **Forms-temakällor** - [AEM Forms Canvas-temat](https://github.com/adobe/aem-forms-theme-canvas) (eller något annat kompatibelt Adaptivt Forms-tema) klonas eller laddas ned lokalt.
* **Node.js och npm** - för att skapa webbplatstemat (se temat README för de versioner som stöds).
* **Maven** - om du skapar hela webbplatsmallpaketet (valfritt för arbete med endast teman).

## Steg 1: Skapa mappen med adaptiva formulärkomponenter {#step-1-create-folder}

Skapa den mapp där Forms-temat ska finnas i din databas för webbplatsteman:

```text
theme/src/components/adaptiveform/
```

Alla Forms-temaresurser placeras under den här mappen så att de hålls åtskilda från befintliga webbplatskomponenter.

## Steg 2: Kopiera Forms temakomponenter och bilder {#step-2-copy-components-and-images}

Använda sökvägarna för ditt **Forms-tema** (till exempel `aem-forms-theme-canvas`) och ditt **webbplatstema**:

1. **Kopiera komponentmappar**\
   Kopiera allt innehåll i `src/components/` från Forms-temat till webbplatstemat som:

   ```text
   theme/src/components/adaptiveform/
   ```

   Så du får banor som:

   ```text
   theme/src/components/adaptiveform/button/
   theme/src/components/adaptiveform/checkbox/
   theme/src/components/adaptiveform/container/
   … (one folder per component)
   ```

2. **Kopiera bilder**\
   Kopiera Forms temabilder till webbplatstemat:

   ```text
   Forms theme:  src/resources/images/*
   Site theme:   theme/src/components/adaptiveform/resources/images/
   ```

   Skapa `theme/src/components/adaptiveform/resources/images/` om den inte finns och kopiera sedan alla bildresurser (till exempel `question.svg`, `Chevron-Left.svg`, `busy-state.gif` och så vidare).

## Steg 3: Kopiera variabler och blandningar {#step-3-copy-variables-and-mixins}

Forms-temat använder delade variabler och blandningar under `src/site/`. Kopiera endast dessa två filer till **root** i `adaptiveform/` (inte inuti en `site` -undermapp):

| Source (Forms-tema) | Mål (webbplatstema) |
|---------------------------|---------------------------------------------------|
| `src/site/_variables.scss` | `theme/src/components/adaptiveform/_variables.scss` |
| `src/site/_mixin.scss` | `theme/src/components/adaptiveform/_mixin.scss` |

Kopiera **inte** resten av Forms-temats `src/site/`-mapp. Endast dessa två filer krävs för de inbäddade formulärformaten.

## Steg 4: Korrigera bildbanor i SCSS {#step-4-fix-image-paths}

I Forms-temat refererar SCSS-komponentfiler ofta till bilder med sökvägar som `./resources/` eller `url(resources/`. När du har flyttat in i `theme/src/components/adaptiveform/<component>/` måste sökvägarna peka upp en nivå till `adaptiveform/resources/`.

**Sök och ersätt** i var `.scss` under `theme/src/components/adaptiveform/`:

| Sök | Ersätt med |
|------|------------------|
| `./resources/` | `../resources/` |
| `url(resources/` | `url(../resources/` |
| `url('resources/` | `url('../resources/` |

**Exempel** - före (Forms-tema):

```scss
.cmp-adaptiveform-button__questionmark {
  background: url(./resources/images/question.svg) center center / cover no-repeat, #969696;
}
```

**Efter** (webbplatstema):

```scss
.cmp-adaptiveform-button__questionmark {
  background: url(../resources/images/question.svg) center center / cover no-repeat, #969696;
}
```

Efter ersättningen blir dessa `url(../resources/images/...)` respektive `url('../resources/images/...')`. Upprepa för varje SCSS-fil under `adaptiveform/` som refererar till bilder (knapp, dragspelspanel, guide, behållare, klottra med flera).

## Steg 5: Skapa SCSS för adaptiv formulärstart {#step-5-create-adaptiveform-scss}

Skapa **`theme/src/components/adaptiveform/_adaptiveform.scss`** i webbplatstemat. Filen måste:

1. Importera de delade variablerna och blandningarna.
2. Importera varje adaptiv formulärkomponents SCSS-huvudfil.

Använd följande som fullständig startpunkt (matchar standardintegreringen med alla Core Components-baserade formulärkomponenter):

```scss
//== Adaptive Form components (forms theme integration)
// Variables and mixins for adaptive form components
@import 'variables';
@import 'mixin';

//== Core adaptive form components
@import './button/_button.scss';
@import './checkboxgroup/_checkboxgroup.scss';
@import './container/_container.scss';
@import './datepicker/_datepicker.scss';
@import './dropdown/_dropdown.scss';
@import './fileinput/_fileinput.scss';
@import './footer/_footer.scss';
@import './image/_image.scss';
@import './numberinput/_numberinput.scss';
@import './panelcontainer/_panelcontainer.scss';
@import './radiobutton/_radiobutton.scss';
@import './text/_text.scss';
@import './textinput/_textinput.scss';
@import './accordion/_accordion.scss';
@import './tabsontop/_tabsontop.scss';
@import './pageheader/_pageheader.scss';
@import './wizard/_wizard.scss';
@import './title/_title.scss';
@import './telephoneinput/_telephoneinput.scss';
@import './emailinput/_emailinput.scss';
@import './recaptcha/_recaptcha.scss';
@import './verticaltabs/_verticaltabs.scss';
@import './checkbox/_checkbox.scss';
@import './termsandconditions/_termsandconditions.scss';
@import './switch/_switch.scss';
@import './hcaptcha/_hcaptcha.scss';
@import './turnstile/_turnstile.scss';
@import './review/_review.scss';
@import './scribble/_scribble.scss';
@import './datetime/_datetime.scss';
```

Om ditt Forms-tema utelämnar vissa komponenter (till exempel ingen klottra eller captcha) bör du ta bort eller kommentera bort motsvarande `@import`-rader för att undvika byggfel. Listan ovan matchar strukturen för [Canvas-temat](https://github.com/adobe/aem-forms-theme-canvas).

## Steg 6: Importera det adaptiva formulärtemat i webbplatstemat {#step-6-import-in-theme-scss}

I **`theme/src/theme.scss`** lägger du till en enskild import i **slutet** av filen (efter andra komponentimporter):

```scss
//== Adaptive Form components (forms theme)
@import './components/adaptiveform/_adaptiveform.scss';
```

**Exempel** - slutet av `theme.scss`:

```scss
// ... existing site component imports ...
@import './components/embed/_embed.scss';
@import './components/pdfviewer/_pdfviewer.scss';
@import './components/socialmediasharing/_social_media_sharing.scss';

//== Adaptive Form components (forms theme)
@import './components/adaptiveform/_adaptiveform.scss';
```

Det här är den enda ändringen som krävs i den befintliga temastrukturen för webbplatsen. All formulärspecifik kod behålls under `src/components/adaptiveform/`.

## Steg 7: Bygg och driftsätt {#step-7-build-and-deploy}

1. Bygg webbplatstemat från temaroten:

   ```bash
   cd theme
   npm install
   npm run build
   ```

2. Distribuera via din befintliga [frontpipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html?lang=sv-SE). Efter distributionen gäller samma tema för CSS för både webbplatssidor och inbäddade adaptiva Forms.

## Felsökning {#troubleshooting}

| Problem | Vad du ska kontrollera |
|-------|-------------------------------|
| Bygget misslyckades: &quot;filen hittades inte&quot; för en bild | Placera alla formulärbilder i `theme/src/components/adaptiveform/resources/images/`. Använd `.scss` (och `adaptiveform/`) för bildsökvägar i alla `../resources/` under `url(../resources/`, inte `./resources/`. Om ditt paket löser sökvägar från `theme/src/` placerar du bilder i `theme/src/resources/images/` och använder `resources/images/` (no `../`) i SCSS. |
| Det gick inte att skapa: filen hittades inte för `_variables.scss` eller `_mixin.scss` | Kopiera båda filerna från Forms-temat `src/site/` till `theme/src/components/adaptiveform/` (adaptiveform root), inte inuti en `site`-undermapp. |
| Det gick inte att skapa: filen hittades inte för en komponent (t.ex. `_scribble.scss`) | Det är inte säkert att ditt Forms-tema innehåller den komponenten. I `theme/src/components/adaptiveform/_adaptiveform.scss` tar du bort eller kommenterar ut raden `@import` för den komponenten. |
| Formuläret återges men har inga format | Bekräfta att sidan använder klientbiblioteket som innehåller det inbyggda temats CSS, och att `theme.scss` innehåller raden `@import './components/adaptiveform/_adaptiveform.scss';` och att temat har byggts om och distribuerats. |
| Formatkonflikter mellan plats- och formulärkomponenter | Formulärkomponentklasserna har ett namnutrymme (t.ex. `cmp-adaptiveform-button`). Om du ser konflikter kontrollerar du om CSS för anpassad plats åsidosätter dessa klasser och justerar specificitet eller ordning. |

## Se även {#see-also}

* [Använd teman för att utforma Core Components-baserade Adaptive Forms](/help/forms/using-themes-in-core-components.md)
* [Utveckla med frontmatade rörledningar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html?lang=sv-SE)