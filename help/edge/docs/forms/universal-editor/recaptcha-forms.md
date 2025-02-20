---
title: Använd reCAPTCHA med Edge Delivery Services för AEM Forms as a Cloud Service
description: Använd Google reCAPTCHA i ett formulär för Edge Delivery Services för AEM Forms
feature: Edge Delivery Services
keywords: reCAPTCHA in forms, Using reCAPTCHA in Universal Editor, Add reCAPTCHA in forms
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: ba42a99e6138616ab6a7564c4bf58400844bdcc4
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 0%

---


# Använd reCAPTCHA i WYSIWYG Authoring

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) är ett populärt verktyg som används för att skydda webbplatser från bedrägliga aktiviteter, skräppost och missbruk.

Ta till exempel ett formulär som beräknar momsen baserat på ytterligare avdrag och skattesatsen. I sådana fall finns det en risk för att obehöriga använder formuläret för att skicka nätfiske eller översvämma det med irrelevant eller skadligt innehåll med hjälp av skräppost. Integreringen av CAPTCHA ger ökad säkerhet genom att verifiera att inskickade data kommer från äkta användare, vilket minimerar inmatningen av skräppost.

![Google recaptcha](/help/edge/docs/forms/universal-editor/assets/google-recaptcha.png)

I Edge Delivery Services Forms kan du med formulärblocket [ansluta Google reCAPTCHA med formulär](#connect-forms-with-recaptcha-service-by-google) med komponenten **Captcha(osynlig)** för att skilja mellan människor och botar. Den här funktionen hjälper författare att skydda sina formulär mot skräppost och missbruk.

## Anslut Forms med reCAPTCHA-tjänsten från Google

Du kan skapa Edge Delivery Services Forms för att implementera tjänsten reCAPTCHA som tillhandahålls av Google. Beroende på dina behov kan du konfigurera någon av följande reCAPTCHA-tjänster för din Edge Delivery Services Forms:

* [reCAPTCHA Enterprise](#configure-recaptcha-enterprise)
* [reCAPTCHA](#configure-recaptcha)

>[!NOTE]
>
> Mer information om hur reCAPTCHA fungerar finns i [Google reCAPTCHA](https://developers.google.com/recaptcha/).

### Konfigurera reCAPTCHA Enterprise

reCAPTCHA Enterprise är en premiumtjänst för upptäckt och förebyggande av bedrägeri i företagsklass som Google erbjuder. Den bygger på reCAPTCHA (score-based) men har ytterligare funktioner, skalbarhet och anpassning för att uppfylla verksamhetens komplexa behov.

#### Innan du börjar

Innan du konfigurerar Google reCAPTCHA Enterprise för Edge Delivery Services Forms måste du utföra följande steg:

1. Skapa eller välj ett [Google Cloud-projekt](https://cloud.google.com/recaptcha/docs/prepare-environment#before-you-begin) och hämta [projekt-ID](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed).

1. [Aktivera företags-API:t reCAPTCHA](https://cloud.google.com/recaptcha/docs/prepare-environment#enable-api) för ditt Google Cloud-projekt och [skapa en API-nyckel](https://console.cloud.google.com/apis/credentials).

1. Skapa en [webbplatsnyckel för ditt Google Cloud-projekt](https://console.cloud.google.com/security/recaptcha) och kopiera webbplatsnyckeln.

När du har dessa uppgifter kan du fortsätta att konfigurera reCAPTCHA Enterprise för dina formulär:

1. [Skapa molnkonfigurationsbehållare](#1-create-cloud-configuration-container)
1. [Skapa molntjänstkonfigurationen för reCAPTCHA Enterprise](#2-create-the-cloud-service-configuration-for-recaptcha-enterprise)

#### 1. Skapa molnkonfigurationsbehållare

Så här skapar du molnkonfigurationsbehållaren:

1. Logga in på din författarinstans.
1. Gå till **[!UICONTROL Tools]** ![tools-1](/help/forms/assets/tools-1.png) > **[!UICONTROL General]** > **[!UICONTROL Configuration Browser]**.

   ![Molnkonfigurationsbehållare](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. I **[!UICONTROL Configuration Browser]** navigerar du till ditt formulär och väljer **[!UICONTROL Properties]**.

   ![Egenskaper för molnkonfiguration](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. Aktivera **[!UICONTROL Cloud Configurations]** i dialogrutan **[!UICONTROL Configuration Properties]**.

1. Välj **[!UICONTROL Save & Close]** om du vill spara konfigurationen och stänga dialogrutan.

   ![Aktivera konfigurationsegenskaper för molnet](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)
`
Publicera molnkonfigurationsbehållaren när du har skapat den.

   ![Publicera molnkonfiguration](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. Skapa molntjänstkonfigurationen för reCAPTCHA Enterprise

Så här skapar du molntjänstkonfigurationen för reCAPTCHA Enterprise:

1. Logga in på din författarinstans.
1. Navigera till **[!UICONTROL Tools]** ![tools-1](/help/forms/assets/tools-1.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL reCAPTCHA]**.

   ![Spela in molnkonfiguration](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   Dialogrutan **Konfigurationer** öppnas.

1. Navigera till formuläret och välj **[!UICONTROL Create]**.

   ![Captcha-konfiguration](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   Dialogrutan **[!UICONTROL Create reCAPTCHA Configuration]** öppnas.

   ![reCaptcha Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)

1. Välj version som [!DNL ReCAPTCHA Enterprise] och ange namn, namn, projekt-ID, webbplatsnyckel och API-nyckel.

   >[!NOTE]
   >
   > Du kan hämta projekt-ID, webbplatsnyckel och API-nyckel från avsnittet [Innan du börjar](#before-you-start) för reCAPTCHA Enterprise.

1. Välj **[!UICONTROL Key type]** som **Sökvägsbaserad webbplatsnyckel**.
1. Ange ett [tröskelvärde i intervallet 0 till 1](https://cloud.google.com/recaptcha/docs/interpret-assessment-website#interpret_scores). Poängvärden som är större än eller lika med tröskelvärdena identifierar mänsklig interaktion, som annars betraktas som båda interaktioner.
1. Välj **[!UICONTROL Create]** om du vill skapa molntjänstkonfigurationen.

   Publicera molnkonfigurationen för reCAPTCHA när du har skapat den.

   ![Publicera Recaptcha-konfiguration](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

Nu kan du skapa eller redigera ett formulär och lägga till komponenten reCAPTCHA med hjälp av den WYSIWYG-baserade utvecklingsmiljön. Detaljerade anvisningar om hur du integrerar Google reCAPTCHA i ditt formulär finns i [Använd reCAPTCHA i ditt formulär](#use-recaptcha-in-your-form).

## Konfigurera reCAPTCHA

reCAPTCHA är en kostnadsfri tjänst från Google som hjälper webbplatser att upptäcka och förhindra trafikmissbruk, inklusive stötar och spam. Den har stöd för en poängbaserad version som fungerar i bakgrunden och tilldelar riskpoäng (från 0,0 till 1,0) till varje användarinteraktion. Poängvärden som är större än eller lika med tröskelvärdena identifierar mänsklig interaktion, som annars betraktas som båda interaktioner.

#### Innan du börjar

Innan du konfigurerar Google reCAPTCHA för Edge Delivery Services Forms hämtar du nyckelparet [reCAPTCHA API från Google Console](https://www.google.com/recaptcha/admin). Paret innehåller en platsnyckel och en hemlig nyckel.

>[!NOTE]
>
> * Edge Delivery Services Forms stöder endast **reCAPTCHA Score-baserad** version.

När du har API-nyckelparet kan du fortsätta att konfigurera reCAPTCHA för dina formulär:

1. [Skapa molnkonfigurationsbehållare](#1-create-cloud-configuration-container-1)
1. [Skapa molntjänstkonfigurationen för reCAPTCHA](#2-create-the-cloud-service-configuration-for-recaptcha)

#### 1. Skapa molnkonfigurationsbehållare

Så här skapar du molnkonfigurationsbehållaren:

1. Logga in på din författarinstans.
1. Gå till **[!UICONTROL Tools]** ![tools-1](/help/forms/assets/tools-1.png) > **[!UICONTROL General]** > **[!UICONTROL Configuration Browser]**.

   ![Molnkonfigurationsbehållare](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. I **[!UICONTROL Configuration Browser]** navigerar du till ditt formulär och väljer **[!UICONTROL Properties]**.

   ![Egenskaper för molnkonfiguration](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. Aktivera **[!UICONTROL Cloud Configurations]** i dialogrutan **[!UICONTROL Configuration Properties]**.

1. Välj **[!UICONTROL Save & Close]** om du vill spara konfigurationen och stänga dialogrutan.

   ![Aktivera konfigurationsegenskaper för molnet](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)

   Publicera molnkonfigurationsbehållaren när du har skapat den.

   ![Publicera molnkonfiguration](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. Skapa molntjänstkonfigurationen för reCAPTCHA

Så här skapar du molntjänstkonfigurationen för reCAPTCHA:

1. Logga in på din författarinstans.
1. Navigera till **[!UICONTROL Tools]** ![tools-1](/help/forms/assets/tools-1.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL reCAPTCHA]**.

   ![Spela in molnkonfiguration](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   Dialogrutan **Konfigurationer** öppnas.

1. Navigera till formuläret och välj **[!UICONTROL Create]**.

   ![Captcha-konfiguration](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   Dialogrutan **[!UICONTROL Create reCAPTCHA Configuration]** öppnas.

   ![reCaptcha Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)

1. Välj version som [!DNL ReCAPTCHA v2] och ange Titel och Namn.
1. Ange webbplatsnyckeln och hemlig nyckel.

   >[!NOTE]
   >
   > Du kan hämta nyckeln Site Key och Secret i avsnittet [Before You Begin](#before-you-begin) för reCAPTCHA.

1. Välj **[!UICONTROL Create]** om du vill skapa molntjänstkonfigurationen.

   Publicera molnkonfigurationen för reCAPTCHA när du har skapat den.

   ![Publicera Recaptcha-konfiguration](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

Nu kan du skapa och redigera ett formulär och lägga till komponenten reCAPTCHA med hjälp av den WYSIWYG-baserade utvecklingsmiljön. Detaljerade anvisningar om hur du integrerar Google reCAPTCHA i ditt formulär finns i [Använd reCAPTCHA i ditt formulär](#use-recaptcha-in-your-form).

### Använd reCAPTCHA i ditt formulär

Så här skapar du ett formulär och lägger till komponenten reCAPTCHA (osynlig):

1. Öppna ett formulär i Universal Editor för redigering.
1. Navigera till det tillagda adaptiva formuläravsnittet i innehållsträdet.
1. Klicka på ikonen **[!UICONTROL Add]** och lägg till komponenten **[!UICONTROL Captcha (Invisble)]** från listan **Adaptiva formulärkomponenter**.

   ![Lägg till reCaptcha-komponent](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)

   Du kan också dra och släppa den adaptiva Forms-komponenten, eftersom den universella redigeraren har en intuitiv dra och släpp-funktion.

1. Klicka på **Publicera** om du vill publicera formuläret igen när du har lagt till komponenten **[!UICONTROL Captcha (Invisble)]**.

   ![publicera om formulär](/help/edge/docs/forms/universal-editor/assets/publish-form.png)

Du kan nu visa formuläret med tjänsten reCAPTCHA på följande URL:
`https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form-name`.

![Formulär med reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/form-with-recaptcha.png)

## Vanliga frågor

* **Vad händer om en användare inte skapar en reCAPTCHA-molnkonfiguration?**

  **A**: Om en användare inte skapar en reCAPTCHA-molnkonfiguration söker AEM-servern efter reCAPTCHA-molnkonfigurationen i den globala konfigurationsbehållaren. Om det inte finns någon konfiguration i den globala konfigurationsbehållaren genereras ett fel på AEM-servern.

* **Vad händer om en användare skapar flera reCAPTCHA-molnkonfigurationer?**
  **A**: Om en användare skapar fler än en reCAPTCHA-molnkonfiguration väljer systemet automatiskt den första reCAPTCHA-konfigurationen som skapats.

* **Varför syns inte ändringar på den publicerade URL:en?**
Om ändringarna inte visas på den publicerade URL:en kontrollerar du att formuläret publiceras på nytt för att uppdatera.

* **Vilken reCAPTCHA-tjänst stöder Edge Delivery Services Forms?**
  **A**: Edge Delivery Services Forms stöder endast poängbaserade reCAPTCHA-tjänster från Google.


## Se även

{{universal-editor-see-also}}

