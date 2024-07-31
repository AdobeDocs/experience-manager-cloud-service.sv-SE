---
title: Använd reCAPTCHA med Edge Delivery Services för AEM Forms as a Cloud Service
description: Använda Google reCAPTCHA i ett EDS-formulär
feature: Edge Delivery Services
exl-id: ac104e23-f175-435f-8414-19847efa5825
role: Admin, Architect, Developer
source-git-commit: fe45123b3aefddaf02bc8584283941db168ba174
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---


# Använd reCAPTCHA med Edge Delivery Services för AEM Forms as a Cloud Service

<span>Funktionen **reCAPTCHA** finns under förhandsversionen. Om du vill begära åtkomst till funktionen **reCAPTCHA** för AEM Forms-Edge Delivery Services skickar du ett e-postmeddelande från din arbetsadress till mailto:aem-forms-ea@adobe.com.</span>

reCAPTCHA är ett populärt verktyg som används för att skydda webbplatser mot bedrägliga aktiviteter, skräppost och missbruk. I Edge Delivery Services ger Adaptive Forms Block möjlighet att lägga till Google reCAPTCHA för att skilja mellan människor och botar. Med den här funktionen kan användare skydda sin webbplats från skräppost och missbruk.
Ta till exempel ett formulär som samlar in data som start- och slutdatum, rumsbudget, beräknad resekostnad och resande information. I sådana fall finns det en risk för att obehöriga använder formuläret för att skicka nätfiske eller översvämma det med irrelevant eller skadligt innehåll med hjälp av skräppost. Integreringen av reCAPTCHA ger ökad säkerhet genom att verifiera att inskickade data kommer från verkliga användare, vilket minimerar inmatningen av skräppost.

<!-- ![Recaptcha Image](/help/edge/docs/forms/assets/recaptcha-image.png){width="300" align="center"} -->

Edge Delivery Services har bara stöd för **Score based(v3)-reCAPTCHA** för det adaptiva formulärblocket.

![Recaptcha V2](/help/forms/assets/recaptcha-v2-invisible.png){width="300" align="center"}


I slutet av den här artikeln lär du dig att:
* [Aktivera Google reCAPTCHA för ett enda formulär](#enable-google-recaptchas-for-a-single-form)
* [Aktivera reCAPTCHA för alla formulär på din webbplats](#enable-recaptcha-for-all-the-forms)

## Krav

* Påbörja utvecklingen av Edge Delivery Services i Forms genom att följa stegen som beskrivs i [Skapa ett formulär med Adaptivt Forms-block](/help/edge/docs/forms/create-forms.md).
* Registrera din domän med [Google reCAPTCHA och få inloggningsuppgifter](https://www.google.com/recaptcha/admin/create).

## Aktivera Google reCAPTCHA för ett enda formulär {#enable-google-recaptchas-for-a-single-form}

Att möjliggöra för Google reCAPTCHA att fylla i ett och samma formulär innebär att Google reCAPTCHA-tjänst integreras i ett specifikt webbformulär för att förhindra automatiskt missbruk eller skräppost.

Så här aktiverar du Google reCAPTCHA för ett enda formulär:
1. [Konfigurera den hemliga reCAPTCHA-nyckeln i projektkonfigurationsfilen](#configure-secret-key)
1. [Lägg till platsnyckeln reCAPTCHA i formuläret](#add-site-key)

Om du vill börja konfigurera reCaptcha i Edge Delivery Servicens Forms, se följande [kalkylblad](/help/edge/docs/forms/assets/recaptcha.xlsx) som innehåller formulärdefinitionen för ett formulär.

### Konfigurera den hemliga reCAPTCHA-nyckeln i projektkonfigurationsfilen {#configure-secret-key}

Webbplatsens hemlighet för en domän som är registrerad hos Google reCAPTCHA läggs till för att projicera konfigurationsfilen (`.helix/config`) i din AEM projektmapp på Microsoft SharePoint eller Google Drive. Så här lägger du till platshemlighet i konfigurationsfilen:

1. Gå till AEM projektmapp på Microsoft® SharePoint eller Google Drive.
1. Skapa filen `.helix/config.xlsx` i din AEM projektmapp på Microsoft SharePoint-platsen eller filen `.helix/config` AEM projektmappen på din Google-enhet.

   >[!NOTE]
   >
   > [projektkonfigurationsfilen](https://www.aem.live/docs/configuration) är ett kalkylblad som finns på `/.helix/config`. Om filen inte finns skapar du den.

1. Öppna filen `config` och lägg till följande nyckel- och värdepar:

   * **captcha.secrets**: Hemligt nyckelvärde för Google reCAPTCHA
   * **captcha.type**: reCAPTCHA v2

   >[!NOTE]
   >
   >  * Du kan hämta reCAPTCHA-nycklarna från [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin).
   >  * Du måste ange värdet **captcha.type** i filen `config` som **reCAPTCHA v2**.

   Se skärmbilden av en projektkonfigurationsfil nedan:

   ![Projektkonfigurationsfil](/help/forms/assets/recaptcha-config-file.png)

1. Spara filen `config`.

1. Förhandsgranska och publicera filen `config` med [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

### Lägg till platsnyckeln reCAPTCHA i formuläret {#add-site-key}

Webbplatsnyckeln för en domän som är registrerad hos Google reCAPTCHA läggs till i kalkylbladet för det formulär som ska skyddas. Så här lägger du till platsnyckeln i ett formulär:

1. Gå till AEM projektmapp på Microsoft® SharePoint eller Google Drive och öppna kalkylbladet. Du kan också skapa nya kalkylblad för ett formulär.
1. Infoga en rad i kalkylbladet och lägg till ett nytt fält som CAPTCHA, inklusive följande information:
   * **typ**: captcha
   * **värde**: Google reCAPTCHA-webbplatsnyckelvärde

   Se skärmbilden nedan som visar kalkylbladet med den nya radtypen CAPTCHA:

   ![Spela in kalkylblad](/help/edge/docs/forms/assets/recaptcha-spreadsheet.png)

   >[!NOTE]
   >
   >  Du kan hämta reCAPTCHA-nycklarna från [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin).

1. Spara kalkylbladet.
1. Använd [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) för att förhandsgranska och publicera kalkylbladet.

När du har lagt till en ny rad i formulärdefinitionen visas ett reCAPTCHA-märke längst ned till höger i formuläret. Detta säkerställer att formuläret nu skyddas mot bedrägliga aktiviteter, skräppost och missbruk.

![recaptcha-form](/help/edge/docs/forms/assets/recaptcha-form.png)

## Aktivera reCAPTCHA för alla formulär på din webbplats{#enable-recaptcha-for-all-the-forms}

Om du vill tillämpa Google reCAPTCHA på alla formulär på din webbplats som använder Adaptive Forms Block, hoppar du över föregående steg och bäddar in värdet `sitekey` direkt i `recaptcha.js`-filen. Så här tar du med värdet för platsnyckeln i filen `recaptcha.js`:

1. [Uppdatera Google reCAPTCHA Site Key i filen recaptcha.js](#1-update-google-recaptcha-site-key-in-recaptchajs-file)
1. [Distribuera filen och bygg projektet](#2-deploy-the-file-and-build-the-project)
1. [Förhandsgranska webbplatsen med AEM](#3-preview-the-site-using-the-aem-sidekick)

### Uppdatera Google reCAPTCHA-webbplatsnyckel i filen recaptcha.js

1. Öppna motsvarande GitHub-databas på den lokala datorn.
1. Navigera till mappen `[../Form Block/integrations]` och öppna filen `recaptcha.js`.
1. Ersätt `siteKey` med nyckelvärdet för Google reCAPTCHA-webbplatsen.

   ![Recaptcha gäller för alla formulär](/help/forms/assets/recaptcha-apply-to-all-forms.png)

   >[!NOTE]
   >
   >  Du kan hämta reCAPTCHA-nycklarna från [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin).

1. Spara filen `recaptcha.js`.

### Distribuera filen och bygg projektet

Distribuera den uppdaterade `recaptcha.js`-filen till ditt GitHub-projekt och verifiera en lyckad version.

### Förhandsgranska webbplatsen med AEM

Använd [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) för att förhandsgranska och publicera webbplatsen.

Emblemet reCAPTCHA visas för alla formulär på din webbplats.

## Se även

{{see-more-forms-eds}}

