---
title: Hur använder man hCaptcha&reg; i en AEM Adaptive Form Core Components?
description: Förbättra formulärsäkerheten med Captcha&reg; service utan problem. Stegvisa anvisningar inifrån!
topic-tags: Adaptive Forms, author
keywords: Captcha&reg; service, Adaptive Forms, CAPTCHA enge, Bot Prevention, Core Components, formuläröverföringssäkerhet, förhindrande av skräppost
feature: Adaptive Forms, Core Components
exl-id: 6c559df2-7b6a-42fe-b44c-29a782570a0c
role: User, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 0%

---

# Koppla samman din AEM Forms-miljö med Captcha® {#connect-your-forms-environment-with-hcaptcha-service}

<span class="preview"> Den här funktionen är under Tidigt Adobe-program. Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) är ett program som ofta används vid onlinetransaktioner för att skilja mellan människor och automatiserade program eller organ. Det utgör en utmaning och utvärderar användarens svar för att avgöra om det är en människa eller en robot som interagerar med webbplatsen. Det förhindrar användaren att fortsätta om testet misslyckas och gör onlinetransaktionerna säkra genom att förhindra att skräppost eller skadliga syften publiceras.

AEM Forms as a Cloud Service stöder följande CAPTCHA-lösningar:

* [hCaptcha](#integrate-aem-forms-environment-with-hcaptcha-captcha)
* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms-core-components.md)
* [hCaptcha](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)

## Integrera AEM Forms-miljön med Captcha Captcha

Med tjänsten Captcha® kan du skydda dina formulär från stötar, skräppost och automatiskt missbruk. Det utgör en utmaning för kryssrutewidgeten och utvärderar användarens svar för att avgöra om det är en människa eller en robot som interagerar med formuläret. Det förhindrar användaren att fortsätta om testet misslyckas och gör onlinetransaktionerna säkra genom att förhindra att skräppost eller skadliga aktiviteter publiceras.

AEM Forms as a Cloud Service har stöd för Captcha® i adaptiva Forms Core-komponenter. Du kan använda den för att visa en kryssrutewidget när formulär skickas.

<!-- ![hCaptcha&reg;](assets/hCaptcha&reg;-challenge.png)-->


### Förutsättningar för att integrera AEM Forms-miljön med Captcha® {#prerequisite}

Om du vill konfigurera hCaptcha® med AEM Forms måste du hämta sitekey och hemlig nyckel [ för ](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key)hCaptcha® från webbplatsen hCaptcha®.

### Konfigurera hCaptcha® {#steps-to-configure-hcaptcha}

Så här integrerar du AEM Forms med tjänsten Captcha®:

1. Skapa en konfigurationsbehållare i din AEM Forms as a Cloud Service-miljö. En konfigurationsbehållare innehåller molnkonfigurationer som används för att ansluta AEM till externa tjänster. Så här skapar och konfigurerar du en konfigurationsbehållare för att ansluta din AEM Forms-miljö till hCaptcha®:
   1. Öppna AEM Forms as a Cloud Service-instansen.
   1. Gå till **[!UICONTROL Tools > General > Configuration Browser]**.
   1. I Configuration Browser kan du välja en befintlig mapp eller skapa en mapp. Du kan skapa en mapp och aktivera alternativet Cloud Configurations för den eller Aktivera alternativet Cloud Configurations för en befintlig mapp:

      * Så här skapar du en mapp och aktiverar alternativet Cloud Configurations för den:
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
   1. Ange **[!UICONTROL Title]**, **[!UICONTROL Name]**, **[!UICONTROL Site Key]** och **[!UICONTROL Secret Key]** för hCaptcha®-tjänsten [ som hämtas i Krav](#prerequisite). Välj **[!UICONTROL Create]**.

      ![Konfigurera Cloud Service för att ansluta din AEM Forms-miljö till Captcha®](assets/create-hcaptcha-config.png)

   >[!NOTE]
   > Användarna behöver inte ändra [Verifierings-URL:en för klientsidan ](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage) och [Verifierings-URL:en för serversidan](https://docs.hcaptcha.com/#verify-the-user-response-server-side) eftersom de redan är förfyllda för hCaptcha®-validering.

   När hCAPTCHA-tjänsten har konfigurerats är den tillgänglig för användning i ett [adaptivt formulär baserat på kärnkomponenter](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction).

## Använd Captcha® i en adaptiv Forms Core-komponent {#using-hCaptcha&reg;-core-components}

1. Öppna AEM Forms as a Cloud Service-instansen.
1. Gå till **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents]**.
1. Välj ett anpassat formulär och välj **[!UICONTROL Properties]**. För alternativet **[!UICONTROL Configuration Container]** väljer du den konfigurationsbehållare som innehåller den molnkonfiguration som ansluter AEM Forms med hCaptcha® och väljer **[!UICONTROL Save & Close]**.

   Om du inte har någon sådan konfigurationsbehållare kan du läsa avsnittet [Anslut AEM Forms-miljön med hCaptcha®](#connect-your-forms-environment-with-hcaptcha-service) för att lära dig hur du skapar en konfigurationsbehållare.

   ![Välj konfigurationsbehållare](/help/forms/assets/captcha-properties.png)

1. Välj ett anpassat formulär och välj **[!UICONTROL Edit]**. Det adaptiva formuläret öppnas i Adaptiv Forms Editor.
1. Dra och släpp eller lägg till komponenten **[!UICONTROL Adaptive Form hCaptcha®]** i det adaptiva formuläret från komponentwebbläsaren.
1. Markera komponenten **[!UICONTROL Adaptive Form hCaptcha®]** och klicka på egenskapsikonen ![Egenskaper](assets/configure-icon.svg) . Dialogrutan Egenskaper öppnas. Ange följande egenskaper:

   ![hCaptcha® v2](assets/config-hcaptcha-v2.png)

   * **[!UICONTROL Name]:** Ange namnet på Captcha-komponenten. Du kan enkelt identifiera en formulärkomponent med dess unika namn både i formuläret och i regelredigeraren.
   * **[!UICONTROL Title]:** Ange titeln för Captcha-komponenten.
   * **[!UICONTROL Configuration Settings]:** Välj en molnkonfiguration som har konfigurerats för hCaptcha®.
   * **Captcha-storlek:** Du kan välja visningsstorlek för utmaningsdialogrutan hCaptcha®. Använd alternativet **[!UICONTROL Compact]** om du vill visa en liten storlek och alternativet **[!UICONTROL Normal]** om du vill visa en relativt stor hCaptcha®-utmaningsdialogruta.<!-- or **[!UICONTROL Invisible]** to validate hCaptcha&reg; without explicitly rendering the checkbox widget on the user interface. -->
   * **[!UICONTROL Validation Message]:** Ange ett valideringsmeddelande för din Captcha-validering när formulär skickas.
   * **[!UICONTROL Script Validation Message]** - Med det här alternativet kan du ange ett meddelande som ska visas om skriptvalideringen misslyckas.

     >[!NOTE]
     >Du kan ha flera molnkonfigurationer i din miljö i liknande syfte. Välj tjänsten noggrant. Om ingen tjänst finns med i listan kan du läsa [Koppla din AEM Forms-miljö till hCaptcha®](#connect-your-forms-environment-with-hcaptcha-service) för att lära dig hur du skapar en Cloud Service som ansluter din AEM Forms-miljö till hCaptcha®-tjänsten.

   <!--* **Error Message:** Provide the error message to display to the user when the Captcha submission fails.-->

1. Välj **[!UICONTROL Done]**.


Nu är det bara berättigade formulär, där formuläranvändaren kan ta bort utmaningen från tjänsten hCaptcha®, som kan användas för att skicka in formuläret. hCaptcha®

**hCaptcha® är ett registrerat varumärke som tillhör Intuition Machines, Inc.**


## Vanliga frågor

* **F: Kan jag använda mer än en Captcha-komponent i ett adaptivt formulär?**
* **Ans:** Det går inte att använda fler än en Captcha-komponent i ett adaptivt formulär. Du bör inte heller använda en Captcha-komponent i ett fragment eller en panel som är markerad för lazy loading.

## Se även {#see-also}

{{see-also}}
