---
title: Hur använder man hCaptcha&reg; i en AEM Adaptiv form?
description: Förbättra formulärsäkerheten med Captcha&reg; service utan problem. Stegvisa anvisningar inifrån!
topic-tags: Adaptive Forms, author
keywords: Captcha&reg; service, Adaptive Forms, CAPTCHA enge, Bot prevent, Form submit security, Form spam prevent
feature: Adaptive Forms, Foundation Components
role: User, Developer
exl-id: dc7ca723-1008-472a-b6eb-8e9ed6332a16
source-git-commit: 914139a6340f15ee77024793bf42fa30c913931e
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Koppla samman din AEM Forms-miljö med Captcha® {#connect-your-forms-environment-with-hcaptcha-service}

<span class="preview"> Den här funktionen är under Tidigt Adobe-program. Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) är ett program som ofta används vid onlinetransaktioner för att skilja mellan människor och automatiserade program eller organ. Det utgör en utmaning och utvärderar användarens svar för att avgöra om det är en människa eller en robot som interagerar med webbplatsen. Det förhindrar användaren att fortsätta om testet misslyckas och gör onlinetransaktionerna säkra genom att förhindra att skräppost eller skadliga syften publiceras.

AEM Forms as a Cloud Service stöder följande CAPTCHA-lösningar:

* [hCaptcha](#integrate-aem-forms-environment-with-hcaptcha-captcha)
* [Molnformad vändning](/help/forms/integrate-adaptive-forms-turnstile.md)
* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms.md)

## Integrera AEM Forms-miljön med Captcha Captcha

Med tjänsten Captcha® kan du skydda dina formulär från stötar, skräppost och automatiskt missbruk. Det utgör en utmaning för kryssrutewidgeten och utvärderar användarens svar för att avgöra om det är en människa eller en robot som interagerar med formuläret. Det förhindrar användaren att fortsätta om testet misslyckas och gör onlinetransaktionerna säkra genom att förhindra att skräppost eller skadliga aktiviteter publiceras.

AEM Forms as a Cloud Service stöder Captcha® i Adaptive Forms. Du kan använda den för att visa en kryssrutewidget när formulär skickas.

<!-- ![hCaptcha&reg;](assets/hCaptcha&reg;-challenge.png)-->

## Förutsättningar för att integrera AEM Forms-miljön med Captcha® {#prerequisite}

Om du vill konfigurera hCaptcha® med AEM Forms måste du hämta sitekey och hemlig nyckel ](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key) för [hCaptcha® från webbplatsen hCaptcha®.

## Steg för att konfigurera hCaptcha® {#steps-to-configure-hcaptcha}

1. Skapa en konfigurationsbehållare i din AEM Forms as a Cloud Service-miljö. En konfigurationsbehållare innehåller molnkonfigurationer som används för att ansluta AEM till externa tjänster. Så här skapar och konfigurerar du en konfigurationsbehållare för att ansluta din AEM Forms-miljö till hCaptcha®:
   1. Öppna AEM Forms as a Cloud Service-instansen.
   1. Gå till **[!UICONTROL Tools > General > Configuration Browser]**.
   1. I Configuration Browser kan du välja en befintlig mapp eller skapa en mapp. Du kan skapa en mapp och aktivera alternativet Cloud Configurations för den eller aktivera alternativet Cloud Configurations för en befintlig mapp:

      * **Så här skapar du en mapp och aktiverar alternativet Cloud Configurations för den**:
         1. Klicka på **[!UICONTROL Create]** i konfigurationsläsaren.
         1. Ange ett namn, en titel och välj alternativet **[!UICONTROL Cloud Configurations]** i dialogrutan Skapa konfiguration.
         1. Klicka på **[!UICONTROL Create]**.
      * Så här aktiverar du alternativet Cloud Configurations för en befintlig mapp:
         1. Markera mappen i Configuration Browser och välj **[!UICONTROL Properties]**.
         1. Aktivera **[!UICONTROL Cloud Configurations]** i dialogrutan Konfiguration.
         1. Välj **[!UICONTROL Save & Close]** om du vill spara konfigurationen och stänga dialogrutan.

1. Konfigurera Cloud Service:
   1. Gå till ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]** och välj **[!UICONTROL hCaptcha®]** i AEM-författarinstansen.
      ![hCaptcha® i ui](assets/hcaptcha-in-ui.png)
   1. Välj en konfigurationsbehållare, skapad eller uppdaterad, enligt beskrivningen i föregående avsnitt. Välj **[!UICONTROL Create]**.
      ![Configuration Captcha®](assets/config-hcaptcha.png)
   1. Ange **[!UICONTROL Title]**, **[!UICONTROL Name]**, **[!UICONTROL Site Key]** och **[!UICONTROL Secret Key]** för hCaptcha®-tjänsten [ som hämtats i förutsättning ](#prerequisite). Välj **[!UICONTROL Create]**.

      ![Konfigurera Cloud Service för att ansluta din AEM Forms-miljö till Captcha®](assets/create-hcaptcha-config.png)

>[!NOTE]
> Användarna behöver inte ändra [Verifierings-URL:en för klientsidan ](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage) och [Verifierings-URL:en för serversidan](https://docs.hcaptcha.com/#verify-the-user-response-server-side) eftersom de redan är förfyllda för hCaptcha®-validering. I vissa länder kan slutpunkterna skilja sig åt. Mer information finns på [hCaptcha® FAQ](https://docs.hcaptcha.com/faq#does-hcaptcha-support-access-by-users-in-china).

När hCAPTCHA-tjänsten har konfigurerats kan den användas i en adaptiv form.

## Använd hCaptcha® i en anpassad form {#using-hCaptcha®-foundation-components}

1. Öppna AEM Forms as a Cloud Service-instansen.
1. Gå till **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents]**.
1. Välj ett anpassat formulär och välj **[!UICONTROL Properties]**. För alternativet **[!UICONTROL Configuration Container]** väljer du den konfigurationsbehållare som innehåller den molnkonfiguration som ansluter AEM Forms till Captcha® och väljer **[!UICONTROL Save & Close]**.

   Om du inte har någon sådan konfigurationsbehållare kan du läsa avsnittet [Anslut AEM Forms-miljön med hCaptcha®](#connect-your-forms-environment-with-hcaptcha-service) för att lära dig hur du skapar en konfigurationsbehållare.

   ![Välj konfigurationsbehållare](/help/forms/assets/captcha-properties.png)

1. Välj ett anpassat formulär och välj **[!UICONTROL Edit]**. Det adaptiva formuläret öppnas i Adaptiv Forms Editor.
1. Dra komponenten **[!UICONTROL Captcha]** från komponentwebbläsaren till det adaptiva formuläret.
1. Markera komponenten **[!UICONTROL Captcha]** och klicka på egenskapsikonen ![Egenskaper](assets/configure-icon.svg) . Dialogrutan Egenskaper öppnas.

   ![Alt-text](assets/hcaptcha-properties.png)

   Ange följande egenskaper:

   * **[!UICONTROL Title]:** Ange titeln för Captcha-komponenten. Du kan enkelt identifiera en formulärkomponent med dess unika namn både i formuläret och i regelredigeraren.
   * **[!UICONTROL Validation Message]:** Ange ett valideringsmeddelande för din Captcha-validering när formulär skickas.
   * **[!UICONTROL Validate Captcha]:** Du kan välja ett av alternativen för att validera Captcha:
      * Vid inskickning av formulär
      * Vid en användaråtgärd.
   * **[!UICONTROL Captcha Service]:** Välj din Captcha-tjänst, här väljer du tjänsten hCaptcha®.
   * **[!UICONTROL Captcha Configuration]:** Välj en molnkonfiguration som har konfigurerats för hCaptcha®.

     >[!NOTE]
     >
     > Du kan ha flera molnkonfigurationer i din miljö i liknande syfte. Välj tjänsten noggrant. Om ingen tjänst finns med i listan kan du läsa [Koppla din AEM Forms-miljö till hCaptcha®](#connect-your-forms-environment-with-hcaptcha-service) för att lära dig hur du skapar en Cloud Service som ansluter din AEM Forms-miljö till hCaptcha®-tjänsten.

   * **Felmeddelande:** Ange felmeddelandet som ska visas för användaren när Captcha-överföringen misslyckas.
   * **Captcha-storlek:** Du väljer visningsstorlek för utmaningsdialogrutan hCaptcha®. Använd alternativet **[!UICONTROL Compact]** om du vill visa en liten storlek och alternativet **[!UICONTROL Normal]** om du vill visa en relativt stor hCaptcha®-utmaningsdialogruta eller **[!UICONTROL Invisible]** om du vill validera hCaptcha® utan att explicit återge kryssrutewidgeten i användargränssnittet.

1. Välj **[!UICONTROL Done]**.

Nu är det bara berättigade formulär, där formuläranvändaren kan ta bort utmaningen från tjänsten hCaptcha®, som kan användas för att skicka in formuläret.

**hCaptcha® är ett registrerat varumärke som tillhör Intuition Machines, Inc.**

## Vanliga frågor

* **F: Kan jag använda mer än en Captcha-komponent i ett adaptivt formulär?**
* **Ans:** Det går inte att använda fler än en Captcha-komponent i ett adaptivt formulär. Du bör inte heller använda en Captcha-komponent i ett fragment eller en panel som är markerad för lazy loading.

## Se även {#see-also}

{{see-also}}
