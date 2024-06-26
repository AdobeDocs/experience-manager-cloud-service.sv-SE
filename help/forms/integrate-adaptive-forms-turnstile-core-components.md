---
title: Hur använder man Turnstile i en AEM adaptiv Form Core Components?
description: Förbättra säkerheten i blanketterna med problemfri hantering. Stegvisa anvisningar inifrån!
topic-tags: Adaptive Forms, author
feature: Adaptive Forms, Core Components
hide: true
hidefromtoc: true
exl-id: e9c13228-0857-4936-9c39-12ed2bddf429
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# Koppla samman din AEM Forms-miljö med Turnstile {#connect-your-forms-environment-with-turnstile-service}

<span class="preview"> Den här funktionen är under Tidigt Adobe-program. Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) är ett program som ofta används vid onlinetransaktioner för att skilja mellan människor och automatiserade program eller organ. Det utgör en utmaning och utvärderar användarens svar för att avgöra om det är en människa eller en robot som interagerar med webbplatsen. Det förhindrar användaren att fortsätta om testet misslyckas och gör onlinetransaktionerna säkra genom att förhindra att skräppost eller skadliga syften publiceras.

AEM Forms as a Cloud Service stöder följande CAPTCHA-lösningar:


* [Molnformad vändning](#integrate-aem-forms-environment-with-turnstile-captcha)
* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms-core-components.md)
* [hCaptcha](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)



<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

## Integrera AEM Forms med Turnstile Captcha

Cloudflare&#39;s Turnstile Captcha är en säkerhetsåtgärd som syftar till att skydda formulär och webbplatser från automatiserade robotar, skadliga attacker, spam och oönskad automatiserad trafik. Den visar en kryssruta när formuläret skickas in för att verifiera att det är humant, innan det går att skicka in formuläret. AEM Forms as a Cloud Service stöder Turnstile Captcha i adaptiva Forms Core-komponenter.

### Förutsättningar för att integrera AEM Forms-miljön med Turnstile Captcha {#prerequisite}

Om du vill konfigurera Turnite för AEM Forms Core Components måste du skaffa [Turnstile sitekey och hemlig nyckel](https://developers.cloudflare.com/turnstile/get-started/) från Turnstiles webbplats.

### Konfigurera vändning {#steps-to-configure-hcaptcha}

Så här integrerar du AEM Forms med Turnstle-tjänsten:

1. Skapa en konfigurationsbehållare i din AEM Forms as a Cloud Service-miljö. En konfigurationsbehållare innehåller molnkonfigurationer som används för att ansluta AEM till externa tjänster. Så här skapar och konfigurerar du en konfigurationsbehållare för att ansluta din AEM Forms-miljö till Turnstle:
   1. Öppna din AEM Forms as a Cloud Service-instans.
   1. Gå till **[!UICONTROL Tools > General > Configuration Browser]**.
   1. I Configuration Browser kan du välja en befintlig mapp eller skapa en mapp. Du kan skapa en mapp och aktivera alternativet Cloud Configurations för den eller Aktivera alternativet Cloud Configurations för en befintlig mapp:

      * Så här skapar du en mapp och aktiverar alternativet Cloud Configurations för den:
         1. Klicka på **[!UICONTROL Create]**.
         1. I dialogrutan Skapa konfiguration anger du ett namn, en rubrik och väljer **[!UICONTROL Cloud Configurations]** alternativ.
         1. Klicka på **[!UICONTROL Create]**.
      * Så här aktiverar du alternativet Cloud Configurations för en befintlig mapp:
         1. Markera mappen och välj **[!UICONTROL Properties]**.
         1. Aktivera i dialogrutan Konfigurationsegenskaper **[!UICONTROL Cloud Configurations]**.
         1. Välj **[!UICONTROL Save & Close]** för att spara konfigurationen och stänga dialogrutan.

1. Konfigurera Cloud Servicen:
   1. Gå till AEM ![verktyg-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]** och markera **[!UICONTROL Turnstile]**.
      ![Turnstile in ui](assets/turnstile-in-ui.png)
   1. Välj en konfigurationsbehållare, skapad eller uppdaterad, enligt beskrivningen i föregående avsnitt. Välj **[!UICONTROL Create]**.
      ![Konfigurationsomkopplare](assets/config-hcaptcha.png)
   1. Ange **[!UICONTROL Widget Type]** som hanterad, **[!UICONTROL Title]**, **[!UICONTROL Name]**, **[!UICONTROL Site Key]** och **[!UICONTROL Secret Key]** för Turnstile-tjänst [som hämtats i en förutsättning](#prerequisite).
   1. Klicka på **[!UICONTROL Create]**.

      ![Konfigurera Cloud Servicen för att ansluta din AEM Forms-miljö till Turnstile](assets/config-turntstile.png)

   >[!NOTE]
   > Användare behöver inte ändra validerings-URL:en på klientsidan och validerings-URL:en på serversidan eftersom de redan är förifyllda för aktiveringsvalidering.

   När Turnstile Captcha-tjänsten har konfigurerats kan den användas i en [Adaptiv form baserad på kärnkomponenter](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction).

## Använd Turnstile i anpassad form {#using-turnstile-core-components}

1. Öppna din AEM Forms as a Cloud Service-instans.
1. Gå till **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents]**.
1. Välj ett adaptivt formulär och välj **[!UICONTROL Properties]**. För **[!UICONTROL Configuration Container]** väljer du den konfigurationsbehållare som innehåller molnkonfigurationen som kopplar AEM Forms till Turnstle och väljer **[!UICONTROL Save & Close]**.

   Om du inte har någon sådan konfigurationsbehållare, se avsnittet [Koppla samman din AEM Forms-miljö med Turnstile](#connect-your-forms-environment-with-turnstile-service) om du vill lära dig hur du skapar en konfigurationsbehållare.

   ![Välj konfigurationsbehållare](/help/forms/assets/captcha-properties.png)

1. Välj ett adaptivt formulär och välj **[!UICONTROL Edit]**. Det adaptiva formuläret öppnas i Adaptiv Forms Editor.
1. Dra och släpp eller lägg till komponentwebbläsaren **[!UICONTROL Adaptive Form Turnstile]** på adaptiva formulär.
1. Välj **[!UICONTROL Adaptive Form Turnstile]** -komponent och klickningsegenskaper ![Ikonen Egenskaper](assets/configure-icon.svg) -ikon. Dialogrutan Egenskaper öppnas. Ange följande egenskaper:

   ![Turnstile v2](assets/turnstile-settings-v2.png)

   * **[!UICONTROL Name]:** Ange namnet på Captcha-komponenten. Du kan enkelt identifiera en formulärkomponent med dess unika namn både i formuläret och i regelredigeraren.
   * **[!UICONTROL Title]:** Ange namnet på Captcha-komponenten.
   * **[!UICONTROL Configuration Settings]:** Välj en molnkonfiguration som är konfigurerad för att växla.
   * **[!UICONTROL Validation Message]:** Ange ett valideringsmeddelande för att validera Captcha när formulär skickas.
   * **[!UICONTROL Script Validation Message]**: Med det här alternativet kan du ange ett meddelande som ska visas om skriptvalideringen misslyckas.
     >[!NOTE]
     >Du kan ha flera molnkonfigurationer i din miljö i liknande syfte. Välj tjänsten noggrant. Om ingen tjänst visas kan du läsa [Koppla samman din AEM Forms-miljö med Turnstile](#connect-your-forms-environment-with-turnstile-service) om du vill lära dig hur du skapar en Cloud Service som kopplar samman din AEM Forms-miljö med den färdiga tjänsten.
   * **Felmeddelande:** Ange felmeddelandet som ska visas för användaren när Captcha-överföringen misslyckas.

1. Välj **[!UICONTROL Done]**.


Nu är det bara berättigade formulär, där formuläranvändaren kan ta bort den utmaning som Turnstile-tjänsten utgör, som kan användas för att skicka in formuläret.

![Turnstutmaning](assets/turnstile-challenge.png)


## Vanliga frågor

* **F: Kan jag använda mer än en Captcha-komponent i en adaptiv form?**
* **Ans:** Det går inte att använda mer än en Captcha-komponent i ett adaptivt formulär. Du bör inte heller använda en Captcha-komponent i ett fragment eller en panel som är markerad för lazy loading.

## Se även {#see-also}

{{see-also}}
