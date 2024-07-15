---
title: Hur använder man Google reCAPTCHA i AEM Adaptiv form?
description: Förbättra säkerheten med Google reCAPTCHA-tjänsten utan problem. Stegvisa anvisningar inifrån!
topic-tags: Adaptive Forms, author
keywords: Google reCAPTCHA-tjänst, Adaptiv Forms, CAPTCHA-utmaning, startalternativ, kärnkomponenter, säkerhet för inskickande av formulär, skydd mot skräppost
feature: Adaptive Forms, Core Components
exl-id: d116f979-efb6-4fac-8202-89afd1037b2c
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---

# Använd Google reCAPTCHA i ett AEM anpassat formulär baserat på kärnkomponenter {#using-reCAPTCHA-in-adaptive-forms}

| Gäller för | Artikellänk |
| -------- | ---------------------------- |
| Adaptiv form baserad på kärnkomponenter | Den här artikeln |
| Adaptiv form baserad på grundläggande komponenter | [Klicka här](/help/forms/captcha-adaptive-forms.md) |

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) är ett program som ofta används vid onlinetransaktioner för att skilja mellan människor och automatiserade program eller organ. Det utgör en utmaning och utvärderar användarens svar för att avgöra om det är en människa eller en robot som interagerar med webbplatsen. Det förhindrar användaren att fortsätta om testet misslyckas och gör onlinetransaktionerna säkra genom att förhindra att skräppost eller skadliga syften publiceras.

AEM Forms as a Cloud Service stöder följande CAPTCHA-lösningar:

* [Google reCAPTCHA](#connect-your-aem-forms-environment-with-recaptcha-service-by-google)
* [Molnformad vändning](/help/forms/integrate-adaptive-forms-turnstile-core-components.md)
* [hCaptcha](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)


## Koppla samman er AEM Forms-miljö med reCAPTCHA-tjänsten från Google {#connect-your-forms-environment-with-recaptcha-service-by-google}

Formulärförfattare kan använda tjänsten reCAPTCHA från Google för att implementera reCAPTCHA i Adaptiv Forms. Den erbjuder avancerade CAPTCHA-funktioner för att skydda er webbplats. Mer information om hur reCAPTCHA fungerar finns i [Google reCAPTCHA](https://developers.google.com/recaptcha/). [!DNL AEM Forms] som [!DNL Cloud Service] stöder Google reCAPTCHA v2 i Adaptiv Forms. Du kan använda den för att presentera en CAPTCHA-utmaning när formulär skickas. Koppla samman AEM Forms-miljön med reCAPTCHA-tjänsten från Google

1. Hämta [reCAPTCHA API-nyckelpar](https://www.google.com/recaptcha/admin) från Google. Den innehåller en **webbplatsnyckel** och en **hemlig nyckel**.

   ![Skapa Google reCAPTCHA-konfiguration av Google webbplats för att hämta reCAPTCHA-nycklar](/help/forms/assets/google-captcha.gif)
1. Skapa en konfigurationsbehållare i din AEM Forms as a Cloud Service-miljö. En konfigurationsbehållare innehåller molnkonfigurationer som används för att ansluta AEM till externa tjänster. Så här skapar och konfigurerar du en Configuration Container för att ansluta AEM Forms-miljön till reCAPTCHA-tjänsten från Google:
   1. Öppna din AEM Forms as a Cloud Service-instans.
   1. Gå till **[!UICONTROL Tools > General > Configuration Browser]**. I Configuration Browser kan du:
   1. Välj en befintlig mapp eller skapa en mapp. Du kan skapa en mapp och aktivera alternativet Cloud Configurations för den eller Aktivera alternativet Cloud Configurations för en befintlig mapp:

      * Så här skapar du en mapp och aktiverar alternativet Cloud Configurations för den:
         1. Klicka på **[!UICONTROL Create]** i konfigurationsläsaren.
         1. I dialogrutan Skapa konfiguration anger du namn, titel och väljer alternativet **[!UICONTROL Cloud Configurations]**.
         1. Klicka på **[!UICONTROL Create]**
      * Så här aktiverar du alternativet Cloud Configurations för en befintlig mapp:
         1. Markera mappen i Configuration Browser och välj **[!UICONTROL Properties]**.
         1. Aktivera **[!UICONTROL Cloud Configurations]** i dialogrutan Konfiguration.
         1. Välj **[!UICONTROL Save & Close]** om du vill spara konfigurationen och stänga dialogrutan.

1. Konfigurera Cloud Servicen:
   1. Gå till ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]** och välj **[!UICONTROL reCAPTCHA]** i AEM författarinstans.
   1. Välj en konfigurationsbehållare som har skapats eller uppdaterats i föregående avsnitt. Välj **[!UICONTROL Create]**.
   1. Ange **[!UICONTROL Title]**, **[!UICONTROL Name]**, **[!UICONTROL Site Key]** och **[!UICONTROL Secret Key]** för reCAPTCHA-tjänsten (hämtas i steg 1). Välj **[!UICONTROL Create]**.

   ![Konfigurera Cloud Servicen för att ansluta din AEM Forms-miljö med reCAPTCHA-tjänsten från Google](/help/forms/assets/captcha-configuration.gif)

   När reCAPTCHA-tjänsten har konfigurerats kan den användas i ett adaptivt format. Mer information finns i [Använda Google reCAPTCHA i ett adaptivt formulär](#using-reCAPTCHA).

## Använd Google reCAPTCHA i anpassad form {#using-reCAPTCHA}

Så här använder du reCAPTCHA i Adaptive Forms:

1. Öppna din AEM Forms as a Cloud Service-instans.
1. Gå till **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents]**.
1. Välj en anpassad Forms och välj **[!UICONTROL Properties]**. För alternativet **[!UICONTROL Configuration Container]** väljer du den konfigurationsbehållare som innehåller molnkonfigurationen som ansluter AEM Forms till reCAPTCHA-tjänsten av Google och väljer **[!UICONTROL Save & Close]**.

   Om du inte har någon sådan konfigurationsbehållare kan du läsa avsnittet [Anslut AEM Forms-miljön med reCAPTCHA-tjänsten från Google](#connect-your-forms-environment-with-recaptcha-service-by-google) för att lära dig hur du skapar en sådan konfigurationsbehållare.

   ![Välj konfigurationsbehållare](/help/forms/assets/captcha-properties.png)

1. Välj en anpassad Forms och välj **[!UICONTROL Edit]**. Det adaptiva formuläret öppnas i Adaptiv Forms Editor.
1. Dra komponenten **[!UICONTROL Adaptive Form reCAPTCHA]** från komponentwebbläsaren till det adaptiva formuläret.

   Google reCAPTCHA-validering är tidskänslig och upphör att gälla om cirka ett par minuter. Därför rekommenderar Adobe att du placerar komponenten **[!UICONTROL Adaptive Form reCAPTCHA]** precis före knappen **[!UICONTROL Submit]**.

1. Markera **[!UICONTROL Adaptive Form reCAPTCHA]**-komponenten och välj egenskapsikonen ![Egenskaper](assets/configure-icon.svg) . Dialogrutan Egenskaper öppnas. Ange följande obligatoriska egenskaper:
   * **[!UICONTROL Name]:** Du kan enkelt identifiera en formulärkomponent med dess unika namn både i formuläret och i regelredigeraren, men namnet får inte innehålla blanksteg eller specialtecken.
   * **[!UICONTROL CAPTCHA Configuration]:** Välj en molnkonfiguration som konfigurerats för att presentera Google reCAPTCHA-dialogrutan för formuläret. Du kan ha flera molnkonfigurationer i din miljö för liknande ändamål. Välj tjänsten noggrant. Om ingen tjänst visas läser du [Anslut AEM Forms-miljön med reCAPTCHA-tjänsten från Google](#connect-your-forms-environment-with-recaptcha-service-by-google) för att lära dig hur du skapar en Cloud Service som ansluter AEM Forms-miljön till reCAPTCHA-tjänsten från Google.
   * **Captcha-storlek:** Du kan välja visningsstorlek för Google reCAPTCHA-utmaningsdialogrutan. Använd alternativet **[!UICONTROL Compact]** om du vill visa en liten storlek och alternativet **[!UICONTROL Normal]** om du vill visa en relativt stor Google reCAPTCHA-utmaningsdialogruta.

1. Välj **[!UICONTROL Done]**.

   Nu visas **protected by reCAPTCHA** i ditt adaptiva formulär. Den visas på alla Adaptive Forms som är konfigurerade att använda tjänsten Google reCAPTCHA.

   Nu är det bara berättigade formulär, i vilka den som fyller i formuläret kan ta bort den utmaning som Google reCAPTCHA-tjänsten utgör, som kan skickas in.
   ![Google skyddat av reCAPTCHA-märke](/help/forms/assets/google-recaptcha-v2.png)

<!--
### Show or hide CAPTCHA component based on rules {#show-hide-captcha}

You can select to show or hide the CAPTCHA component based on rules that you apply on a component in an Adaptive Form. Select the component, select ![edit rules](assets/edit-rules-icon.svg), and select **[!UICONTROL Create]** to create a rule. For more information on creating rules, see [Rule Editor](rule-editor.md).

For example, the CAPTCHA component must display in an Adaptive Form only if the Currency Value field in the form has a value of more than 25000.

Select the **[!UICONTROL Currency Value]** field in the form and create the following rules:

![Show or hide rules](assets/rules-show-hide-captcha.png)

   >[!NOTE]
   >
   > When you select a reCAPTCHA v2 configuration and the size is set to [!UICONTROL Invisible], the show/hide option remains disabled.

   -->

## Vanliga frågor

**F: Kan jag använda mer än en Captcha-komponent i ett adaptivt formulär?**
**Ans:** Det går inte att använda fler än en Captcha-komponent i ett adaptivt formulär. Vi rekommenderar inte att du använder Captcha-komponenten i ett fragment eller i en panel som är markerad för lat inläsande.

## Se även {#see-also}

{{see-also}}