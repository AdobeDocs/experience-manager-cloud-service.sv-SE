---
title: Använda CAPTCHA i Adaptive Forms
seo-title: Using CAPTCHA in Adaptive Forms
description: Lär dig hur du konfigurerar AEM CAPTCHA- eller Google reCAPTCHA-tjänsten i Adaptive Forms.
seo-description: Learn how to configure AEM CAPTCHA or Google reCAPTCHA service in Adaptive Forms.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
exl-id: 3fdbe5a3-5c3c-474d-b701-e0182da4191a
source-git-commit: a16da1b11cfe18910b2e57c0b6b668543dba46e3
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 0%

---

# Använd CAPTCHA i Adaptive Forms{#using-captcha-in-adaptive-forms}

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) är ett program som ofta används vid onlinetransaktioner för att skilja mellan människor och automatiserade program eller organ. Det utgör en utmaning och utvärderar användarens svar för att avgöra om det är en människa eller en robot som interagerar med webbplatsen. Det förhindrar användaren att fortsätta om testet misslyckas och gör onlinetransaktionerna säkra genom att förhindra att skräppost eller skadliga syften publiceras.

[!DNL AEM Forms] har stöd för CAPTCHA i Adaptive Forms. Du kan använda tjänsten reCAPTCHA från Google för att implementera CAPTCHA.

>[!NOTE]
>
>* [!DNL AEM Forms] har endast stöd för reCaptcha v2. Andra versioner stöds inte.
>* CAPTCHA i Adaptive Forms stöds inte i offlineläge i [!DNL AEM Forms] app.
>

## Konfigurera tjänsten reCAPTCHA från Google {#google-reCAPTCHA}

Formulärförfattare kan använda tjänsten reCAPTCHA från Google för att implementera CAPTCHA i Adaptiv Forms. Den har avancerade CAPTCHA-funktioner för att skydda er webbplats. Mer information om hur reCAPTCHA fungerar finns i [Google reCAPTCHA](https://developers.google.com/recaptcha/).

![reCAPTCHA](assets/recaptcha_new.png)

Så här implementerar du tjänsten reCAPTCHA i [!DNL AEM Forms]:

1. Hämta [API-nyckelpar för reCAPTCHA](https://www.google.com/recaptcha/admin) från Google. Den innehåller en webbplatsnyckel och hemlighet.
1. Skapa konfigurationsbehållare för molntjänster.

   1. Gå till **[!UICONTROL Tools > General > Configuration Browser]**.
      * Se [Konfigurationsläsaren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html?lang=en#introduction) mer information.
   1. Gör följande för att aktivera den globala mappen för molnkonfigurationer eller hoppa över det här steget för att skapa och konfigurera en annan mapp för molntjänstkonfigurationer.

      1. I konfigurationsläsaren väljer du **[!UICONTROL global]** mapp och tryck **[!UICONTROL Properties]**.

      1. Aktivera i dialogrutan Konfigurationsegenskaper **[!UICONTROL Cloud Configurations]**.
      1. Tryck **[!UICONTROL Save & Close]** för att spara konfigurationen och stänga dialogrutan.

   1. Tryck på **[!UICONTROL Create]**.
   1. I dialogrutan Skapa konfiguration anger du en rubrik för mappen och aktiverar **[!UICONTROL Cloud Configurations]**.
   1. Tryck **[!UICONTROL Create]** för att skapa en mapp som är aktiverad för molntjänstkonfigurationer.

1. Konfigurera molntjänsten för reCAPTCHA.

   1. Gå till Experience Manager ![verktyg-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]**.
   1. Tryck på **[!UICONTROL reCAPTCHA]**. Sidan Konfigurationer öppnas. Välj den konfigurationsbehållare som skapades i föregående steg och tryck på **[!UICONTROL Create]**.
   1. Ange namn, platsnyckel och hemlig nyckel för reCAPTCHA-tjänsten och tryck på **[!UICONTROL Create]** för att skapa molntjänstkonfigurationen.
   1. I dialogrutan Redigera komponent anger du platsen och de hemliga nycklarna som fås i steg 1. Tryck **[!UICONTROL Save Settings]** och sedan trycka **[!UICONTROL OK]** för att slutföra konfigurationen.

   När reCAPTCHA-tjänsten har konfigurerats kan den användas i Adaptive Forms. Mer information finns i [Använda CAPTCHA i Adaptive Forms](#using-captcha).

## Använd CAPTCHA i Adaptive Forms {#using-captcha}

Så här använder du CAPTCHA i Adaptiv Forms:

1. Öppna ett anpassat formulär i redigeringsläge.

   >[!NOTE]
   >
   > Kontrollera att den konfigurationsbehållare som valts när det adaptiva formuläret skapas innehåller molntjänsten reCAPTCHA. Du kan också redigera egenskaper för adaptiva formulär för att ändra konfigurationsbehållaren som är kopplad till formuläret.

1. Dra från komponentwebbläsaren och släpp **[!UICONTROL Captcha]** på adaptiva formulär.

   >[!NOTE]
   >
   > * Det går inte att använda mer än en Captcha-komponent i ett adaptivt formulär. Du bör inte heller använda CAPTCHA i en panel som är markerad för lazy loading eller i ett fragment.
   > * Captcha är tidskänsligt och upphör om ungefär en minut. Därför rekommenderar vi att du placerar Captcha-komponenten precis före Skicka-knappen i den adaptiva formen.

1. Välj den Captcha-komponent som du har lagt till och tryck på ![cmppr](assets/configure-icon.svg) om du vill redigera dess egenskaper.
1. Ange en titel för CAPTCHA-widgeten. Standardvärdet är **[!UICONTROL Captcha]**. Välj **[!UICONTROL Hide title]** om du inte vill att rubriken ska visas.
1. Från **[!UICONTROL Captcha service]** nedrullningsbar meny, välja **[!UICONTROL reCAPTCHA]** för att aktivera tjänsten reCAPTCHA om du har konfigurerat den enligt beskrivningen i [reCAPTCHA-tjänst från Google](#google-reCAPTCHA). Välj en konfiguration i listrutan Inställningar.
1. Välj typen som **[!UICONTROL Normal]** eller **[!UICONTROL Compact]** för widgeten reCAPTCHA. Du kan också välja **[!UICONTROL Invisible]** möjlighet att visa CAPTCHA-utmaningen endast i händelse av en misstänkt aktivitet. Varumärket protected by reCAPTCHA, som visas nedan, visas på de skyddade formulären.

   ![Google skyddat av reCAPTCHA-märke](assets/google-recaptcha-v2.png)

   >[!NOTE]
   >
   > Markera inte **[!UICONTROL Default]** från listrutan Captcha-tjänst eftersom Experience Manager CAPTCHA-standardtjänsten är inaktuell.

1. Spara egenskaperna.

Tjänsten reCAPTCHA är aktiverad i det adaptiva formuläret. Du kan förhandsgranska formuläret och se hur CAPTCHA fungerar.

### Visa eller dölj CAPTCHA-komponent baserat på regler {#show-hide-captcha}

Du kan välja att visa eller dölja CAPTCHA-komponenten baserat på regler som du tillämpar på en komponent i ett adaptivt formulär. Tryck på komponenten, markera ![redigera regler](assets/edit-rules-icon.svg)och trycka **[!UICONTROL Create]** för att skapa en regel. Mer information om hur du skapar regler finns i [Regelredigeraren](rule-editor.md).

CAPTCHA-komponenten måste till exempel bara visas i ett adaptivt formulär om fältet Valutavärde i formuläret har ett värde över 25000.

Tryck på **[!UICONTROL Currency Value]** i formuläret och skapa följande regler:

![Visa eller dölja regler](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> Om du väljer reCAPTCHA v2-konfiguration med storleken [!UICONTROL Invisible] då alternativet visa/dölj inte är tillgängligt.

### Validera CAPTCHA {#validate-captcha}

Du kan validera CAPTCHA i ett adaptivt formulär antingen när du skickar formuläret eller baserar CAPTCHA-valideringen på användaråtgärder och villkor.

#### Validera CAPTCHA när formulär skickas {#validation-form-submission}

Så här validerar du en CAPTCHA automatiskt när du skickar in ett adaptivt formulär:

1. Tryck på CAPTCHA-komponenten och välj ![cmppr](assets/configure-icon.svg) för att visa komponentegenskaperna.
1. I **[!UICONTROL Validate CAPTCHA]** avsnitt, markera **[!UICONTROL Validate CAPTCHA at form submission]**.
1. Tryck ![Klar](assets/save_icon.svg) för att spara komponentegenskaperna.

#### Validera CAPTCHA på användaråtgärder och villkor {#validate-captcha-user-action}

Så här validerar du en CAPTCHA baserat på villkor och användaråtgärder:

1. Tryck på CAPTCHA-komponenten och välj ![cmppr](assets/configure-icon.svg) för att visa komponentegenskaperna.
1. I **[!UICONTROL Validate CAPTCHA]** avsnitt, markera **[!UICONTROL Validate CAPTCHA on a user action]**.
1. Tryck ![Klar](assets/save_icon.svg) för att spara komponentegenskaperna.

[!DNL Experience Manager Forms] innehåller `ValidateCAPTCHA` API för att validera CAPTCHA med fördefinierade villkor. Du kan anropa API:t med en anpassad skickaåtgärd eller genom att definiera regler för komponenter i ett anpassat formulär.

Följande är ett exempel på en `ValidateCAPTCHA` API för att validera CAPTCHA med fördefinierade villkor:

```javascript
if (slingRequest.getParameter("numericbox1614079614831").length() >= 5) {
     GuideCaptchaValidatorProvider apiProvider = sling.getService(GuideCaptchaValidatorProvider.class);
        String formPath = slingRequest.getResource().getPath();
        String captchaData = slingRequest.getParameter(GuideConstants.GUIDE_CAPTCHA_DATA);
        if (!apiProvider.validateCAPTCHA(formPath, captchaData).isCaptchaValid()){
            response.setStatus(400);
            return;
        }
    }
```

Exemplet anger att `ValidateCAPTCHA` API validerar bara CAPTCHA i formuläret om antalet siffror i den numeriska rutan som användaren anger när formuläret fylls i är större än 5.

**Alternativ 1: Använd [!DNL Experience Manager Forms] ValidateCAPTCHA API to validate CAPTCHA using a custom Submit Action**

Utför följande steg för att använda `ValidateCAPTCHA` API för att validera CAPTCHA med en anpassad överföringsåtgärd:

1. Lägg till skriptet som innehåller `ValidateCAPTCHA` API till anpassad skickaåtgärd. Mer information om anpassade överföringsåtgärder finns i [Skapa en anpassad Skicka-åtgärd för Adaptiv Forms](custom-submit-action-form.md).
1. Välj namnet på den anpassade Skicka-åtgärden på menyn **[!UICONTROL Submit Action]** nedrullningsbar lista i **[!UICONTROL Submission]** egenskaper för ett adaptivt formulär.
1. Tryck på **[!UICONTROL Submit]**. CAPTCHA valideras baserat på de villkor som definieras i `ValidateCAPTCHA` API för den anpassade åtgärden Skicka.

**Alternativ 2: Använd [!DNL Experience Manager Forms] Validera CAPTCHA API för att validera CAPTCHA på en användaråtgärd innan formuläret skickas**

Du kan också anropa `ValidateCAPTCHA` API genom att tillämpa regler på en komponent i ett adaptivt formulär.

Du kan till exempel lägga till en **[!UICONTROL Validate CAPTCHA]** i ett adaptivt formulär och skapa en regel som anropar en tjänst genom att klicka på en knapp.

Följande bild visar hur du kan anropa en tjänst genom att klicka på en **[!UICONTROL Validate CAPTCHA]** knapp:

![Validera CAPTCHA](assets/captcha-validation1.gif)

Du kan anropa den anpassade servern som innehåller `ValidateCAPTCHA` API med regelredigeraren och aktivera eller inaktivera skicka-knappen för det adaptiva formuläret baserat på valideringsresultatet.

På samma sätt kan du använda regelredigeraren för att inkludera en anpassad metod för att validera CAPTCHA i ett adaptivt formulär.

### Lägg till anpassade CAPTCHA-tjänster {#add-custom-captcha-service}

[!DNL Experience Manager Forms] tillhandahåller reCAPTCHA som CAPTCHA-tjänst. Du kan dock lägga till en anpassad tjänst som ska visas i **[!UICONTROL CAPTCHA Service]** nedrullningsbar lista.

Nedan följer ett exempel på en implementering av gränssnittet för att lägga till ytterligare CAPTCHA-tjänst i ditt adaptiva formulär:

```javascript
package com.adobe.aemds.guide.service;

import org.osgi.annotation.versioning.ConsumerType;

/**
 * An interface to provide captcha validation at server side in Adaptive Form
 * This interface can be used to provide custom implementation for different captcha services.
 */
@ConsumerType
public interface GuideCaptchaValidator {
    /**
     * This method should define the actual validation logic of the captcha
     * @param captchaPropertyNodePath path to the node with CAPTCHA configurations inside form container
     * @param userResponseToken  The user response token provided by the CAPTCHA from client-side
     *
     * @return  {@link GuideCaptchaValidationResult} validation result of the captcha
     */
     GuideCaptchaValidationResult validateCaptcha(String captchaPropertyNodePath, String userResponseToken);

    /**
     * Returns the name of the captcha validator. This should be unique among the different implementations
     * @return  name of the captcha validator
     */
     String getCaptchaValidatorName();
}
```

`captchaPropertyNodePath` refererar till resurssökvägen för CAPTCHA-komponenten i Sling-databasen. Använd den här egenskapen om du vill ta med information som är specifik för CAPTCHA-komponenten. Till exempel: `captchaPropertyNodePath` innehåller information om reCAPTCHA-molnkonfigurationen som konfigurerats för CAPTCHA-komponenten. Molnkonfigurationsinformationen innehåller **[!UICONTROL Site Key]** och **[!UICONTROL Secret Key]** inställningar för implementering av tjänsten reCAPTCHA.

`userResponseToken` refererar till `g_recaptcha_response` som genereras när en CAPTCHA har lösts i ett formulär.

### Redigera reCAPTCHA-tjänstdomän {#reCAPTCHA-service-domain}

reCAPTCHA-tjänsten använder `https://www.recaptcha.net/` som standarddomän. Du kan ändra inställningarna för att ange `https://www.google.com/` eller ett anpassat domännamn för inläsning, återgivning och validering av reCAPTCHA-tjänsten.

Ange **[!UICONTROL af.cloudservices.recaptcha.domain]** egenskapen för **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]** konfiguration som ska anges `https://www.google.com/` eller något annat anpassat domännamn. I följande JSON-fil visas ett exempel:

```json
{
  "af.cloudservices.recaptcha.domain": "https://www.google.com/"
}
```

Så här anger du värden för en konfiguration: [Generera OSGi-konfigurationer med AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)och [distribuera konfigurationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) till din Cloud Service.
