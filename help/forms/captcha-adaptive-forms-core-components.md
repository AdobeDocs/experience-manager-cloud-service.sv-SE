---
title: Använd Google reCAPTCHA i ett adaptivt format baserat på kärnkomponenter
description: Förbättra säkerheten med Google reCAPTCHA-tjänsten utan problem. Stegvisa anvisningar inifrån!
topic-tags: Adaptive Forms, author
hide: true
hidefromtoc: true
Keywords: Google reCAPTCHA service, Adaptive Forms, CAPTCHA challenge, Bot prevention, Core Components, Form submission security, Form spam prevention
source-git-commit: a1689c61715f01cb4eb62882dbcd6e202b74ffc9
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# Använd reCAPTCHA i adaptiv Forms baserat på kärnkomponenter {#using-reCAPTCHA-in-adaptive-forms}

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) är ett program som ofta används vid onlinetransaktioner för att skilja mellan människor och automatiserade program eller organ. Det utgör en utmaning och utvärderar användarens svar för att avgöra om det är en människa eller en robot som interagerar med webbplatsen. Det förhindrar användaren att fortsätta om testet misslyckas och gör onlinetransaktionerna säkra genom att förhindra att skräppost eller skadliga syften publiceras.

[!DNL AEM Forms] som [!DNL Cloud Service] har stöd för Google reCAPTCHA v2 i Adaptive Forms. Du kan använda den för att presentera en CAPTCHA-utmaning när formulär skickas. Så här använder du reCAPTCHA i adaptiv form:

1. [Koppla samman er AEM Forms-miljö med reCAPTCHA-tjänsten från Google](#connect-your-forms-environment-with-recaptcha-service-by-google)
1. [Konfigurera ditt adaptiva formulär så att CAPTCHA-utmaning visas när formulär skickas](#using-reCAPTCHA)

## Koppla samman er AEM Forms-miljö med reCAPTCHA-tjänsten från Google {#connect-your-forms-environment-with-recaptcha-service-by-google}

Koppla samman AEM Forms-miljön med reCAPTCHA-tjänsten från Google

1. Hämta [API-nyckelpar för reCAPTCHA](https://www.google.com/recaptcha/admin) från Google. Den innehåller **webbplatsnyckel** och **hemlig nyckel**.

   ![Skapa Google reCAPTCHA-konfiguration av Google webbplats för att få reCAPTCHA-nycklar](/help/forms/assets/google-captcha.gif){width="50%"}
1. Skapa en konfigurationsbehållare i din AEM Forms as a Cloud Service miljö. En konfigurationsbehållare innehåller molnkonfigurationer som används för att ansluta AEM till externa tjänster. Så här skapar och konfigurerar du en Configuration Container för att ansluta AEM Forms-miljön till reCAPTCHA-tjänsten från Google:
   1. Öppna din as a Cloud Service AEM Forms-instans.
   1. Gå till **[!UICONTROL Tools > General > Configuration Browser]**. I Configuration Browser kan du:
   1. Välj en befintlig mapp eller skapa en mapp. Du kan skapa en mapp och aktivera alternativet Cloud Configurations för den eller Aktivera alternativet Cloud Configurations för en befintlig mapp:

      * Så här skapar du en mapp och aktiverar alternativet Cloud Configurations för den:
         1. Klicka på **[!UICONTROL Create]**.
         1. I dialogrutan Skapa konfiguration anger du namn, rubrik och väljer **[!UICONTROL Cloud Configurations]** alternativ.
         1. Klicka på **[!UICONTROL Create]**
      * Så här aktiverar du alternativet Cloud Configurations för en befintlig mapp:
         1. Markera mappen i Configuration Browser och tryck på **[!UICONTROL Properties]**.
         1. Aktivera i dialogrutan Konfigurationsegenskaper **[!UICONTROL Cloud Configurations]**.
         1. Tryck **[!UICONTROL Save & Close]** för att spara konfigurationen och stänga dialogrutan.

1. Konfigurera Cloud Servicen:
   1. Gå till AEM ![verktyg-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]** och knacka **[!UICONTROL reCAPTCHA]**.
   1. Välj en konfigurationsbehållare som har skapats eller uppdaterats i föregående avsnitt. Tryck på **[!UICONTROL Create]**.
   1. Ange **[!UICONTROL Title]**, **[!UICONTROL Name]**, **[!UICONTROL Site Key]** och **[!UICONTROL Secret Key]** för reCAPTCHA-tjänsten (finns i steg 1). Tryck på **[!UICONTROL Create]**.


   ![Konfigurera Cloud Servicen för att ansluta din AEM Forms-miljö med reCAPTCHA-tjänsten från Google](/help/forms/assets/captcha-configuration.gif)



   När reCAPTCHA-tjänsten har konfigurerats kan den användas i ett adaptivt format. Mer information finns i [använda Google reCAPTCHA i en adaptiv form](#using-reCAPTCHA).


## Använd Google reCAPTCHA i anpassad form {#using-reCAPTCHA}

Så här använder du reCAPTCHA i Adaptive Forms:

1. Öppna din as a Cloud Service AEM Forms-instans.
1. Gå till **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents]**.
1. Välj en anpassad Forms och tryck **[!UICONTROL Properties]**. För **[!UICONTROL Configuration Container]** markerar du den konfigurationsbehållare som innehåller molnkonfigurationen som ansluter AEM Forms till reCAPTCHA-tjänsten av Google och trycker på **[!UICONTROL Save & Close]**.

   Om du inte har någon sådan konfigurationsbehållare, se avsnittet [Koppla samman er AEM Forms-miljö med reCAPTCHA-tjänsten från Google](#connect-your-forms-environment-with-recaptcha-service-by-google) om du vill lära dig hur du skapar en sådan konfigurationsbehållare.

   ![Välj konfigurationsbehållare](/help/forms/assets/captcha-properties.png)

1. Välj en anpassad Forms och tryck **[!UICONTROL Edit]**. Det adaptiva formuläret öppnas i Adaptiv Forms Editor.
1. Dra från komponentwebbläsaren och släpp **[!UICONTROL Adaptive Form reCAPTCHA]** på adaptiva formulär.

   Google reCAPTCHA-validering är tidskänslig och upphör att gälla om cirka ett par minuter. Adobe rekommenderar därför att du placerar **[!UICONTROL Adaptive Form reCAPTCHA]** -komponenten precis före **[!UICONTROL Submit]** -knappen.

1. Välj **[!UICONTROL Adaptive Form reCAPTCHA]** och trycka på egenskaperna ![Ikonen Egenskaper](assets/configure-icon.svg) -ikon. Dialogrutan Egenskaper öppnas. Ange följande obligatoriska egenskaper:
   * **[!UICONTROL Name]:** Du kan enkelt identifiera en formulärkomponent med dess unika namn både i formuläret och i regelredigeraren, men namnet får inte innehålla blanksteg eller specialtecken.
   * **[!UICONTROL CAPTCHA Configuration]:** Välj en molnkonfiguration som konfigurerats för att visa Google reCAPTCHA-dialogrutan för formuläret. Du kan ha flera molnkonfigurationer i din miljö för liknande ändamål. Välj tjänsten noggrant. Om ingen tjänst visas kan du läsa [Koppla samman er AEM Forms-miljö med reCAPTCHA-tjänsten från Google](#connect-your-forms-environment-with-recaptcha-service-by-google) om du vill lära dig hur du skapar en Cloud Service som kopplar samman din AEM Forms-miljö med reCAPTCHA-tjänsten från Google.
   * **Storlek:** Du kan välja visningsstorlek för Google reCAPTCHA-utmaningsdialogrutan. Använd **[!UICONTROL Compact]** för att visa en liten storlek och **[!UICONTROL Normal]** för att visa en ganska stor dialogruta för Google reCAPTCHA-utmaningar.

1. Tryck på **[!UICONTROL Done]**.

   Nu **skyddat av reCAPTCHA** visas i ditt adaptiva formulär. Den visas på alla Adaptive Forms som är konfigurerade att använda tjänsten Google reCAPTCHA.

   Nu är det bara berättigade formulär, i vilka den som fyller i formuläret kan ta bort den utmaning som Google reCAPTCHA-tjänsten utgör, som kan skickas in.
   ![Google skyddat av reCAPTCHA-märke](/help/forms/assets/google-recaptcha-v2.png)

<!--
### Show or hide CAPTCHA component based on rules {#show-hide-captcha}

You can select to show or hide the CAPTCHA component based on rules that you apply on a component in an Adaptive Form. Tap the component, select ![edit rules](assets/edit-rules-icon.svg), and tap **[!UICONTROL Create]** to create a rule. For more information on creating rules, see [Rule Editor](rule-editor.md).

For example, the CAPTCHA component must display in an Adaptive Form only if the Currency Value field in the form has a value of more than 25000.

Tap the **[!UICONTROL Currency Value]** field in the form and create the following rules:

![Show or hide rules](assets/rules-show-hide-captcha.png)

   >[!NOTE]
   >
   > When you select a reCAPTCHA v2 configuration and the size is set to [!UICONTROL Invisible], the show/hide option remains disabled.

   -->

## Vanliga frågor

**F: Kan jag använda mer än en Captcha-komponent i en adaptiv form?**
**Ans:** Det går inte att använda mer än en Captcha-komponent i ett adaptivt formulär. Vi rekommenderar inte att du använder Captcha-komponenten i ett fragment eller i en panel som är markerad för lat inläsande.

