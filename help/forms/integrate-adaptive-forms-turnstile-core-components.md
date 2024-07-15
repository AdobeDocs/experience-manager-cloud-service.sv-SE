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

Om du vill konfigurera Turnstile för AEM Forms Core Components måste du hämta [Turnstile sitekey och hemlig nyckel](https://developers.cloudflare.com/turnstile/get-started/) från Turnstile-webbplatsen.

### Konfigurera vändning {#steps-to-configure-hcaptcha}

Så här integrerar du AEM Forms med Turnstle-tjänsten:

1. Skapa en konfigurationsbehållare i din AEM Forms as a Cloud Service-miljö. En konfigurationsbehållare innehåller molnkonfigurationer som används för att ansluta AEM till externa tjänster. Så här skapar och konfigurerar du en konfigurationsbehållare för att ansluta din AEM Forms-miljö till Turnstle:
   1. Öppna din AEM Forms as a Cloud Service-instans.
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

1. Konfigurera Cloud Servicen:
   1. Gå till ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]** och välj **[!UICONTROL Turnstile]** i AEM författarinstans.
      ![Turnstile in ui](assets/turnstile-in-ui.png)
   1. Välj en konfigurationsbehållare, skapad eller uppdaterad, enligt beskrivningen i föregående avsnitt. Välj **[!UICONTROL Create]**.
      ![Konfigurationsomvandling](assets/config-hcaptcha.png)
   1. Ange **[!UICONTROL Widget Type]** som hanterad, **[!UICONTROL Title]**, **[!UICONTROL Name]**, **[!UICONTROL Site Key]** och **[!UICONTROL Secret Key]** för den färdiga tjänsten [ som hämtats i förutsättning ](#prerequisite).
   1. Klicka på **[!UICONTROL Create]**.

      ![Konfigurera Cloud Servicen för att ansluta din AEM Forms-miljö till Turnestle](assets/config-turntstile.png)

   >[!NOTE]
   > Användare behöver inte ändra validerings-URL:en på klientsidan och validerings-URL:en på serversidan eftersom de redan är förifyllda för aktiveringsvalidering.

   När Turnstile Captcha-tjänsten har konfigurerats är den tillgänglig för användning i ett [adaptivt formulär baserat på kärnkomponenter](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction).

## Använd Turnstile i anpassad form {#using-turnstile-core-components}

1. Öppna din AEM Forms as a Cloud Service-instans.
1. Gå till **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents]**.
1. Välj ett anpassat formulär och välj **[!UICONTROL Properties]**. För alternativet **[!UICONTROL Configuration Container]** väljer du den konfigurationsbehållare som innehåller den molnkonfiguration som ansluter AEM Forms med Turnstle och väljer **[!UICONTROL Save & Close]**.

   Om du inte har någon sådan konfigurationsbehållare kan du läsa avsnittet [Anslut din AEM Forms-miljö med Turnstle](#connect-your-forms-environment-with-turnstile-service) för att lära dig hur du skapar en konfigurationsbehållare.

   ![Välj konfigurationsbehållare](/help/forms/assets/captcha-properties.png)

1. Välj ett anpassat formulär och välj **[!UICONTROL Edit]**. Det adaptiva formuläret öppnas i Adaptiv Forms Editor.
1. Dra och släpp eller lägg till komponenten **[!UICONTROL Adaptive Form Turnstile]** i det adaptiva formuläret från komponentwebbläsaren.
1. Markera komponenten **[!UICONTROL Adaptive Form Turnstile]** och klicka på egenskapsikonen ![Egenskaper](assets/configure-icon.svg) . Dialogrutan Egenskaper öppnas. Ange följande egenskaper:

   ![Turnstile v2](assets/turnstile-settings-v2.png)

   * **[!UICONTROL Name]:** Ange namnet på Captcha-komponenten. Du kan enkelt identifiera en formulärkomponent med dess unika namn både i formuläret och i regelredigeraren.
   * **[!UICONTROL Title]:** Ange titeln för Captcha-komponenten.
   * **[!UICONTROL Configuration Settings]:** Välj en molnkonfiguration som har konfigurerats för Turnstle.
   * **[!UICONTROL Validation Message]:** Ange ett valideringsmeddelande för att validera Captcha när formulär skickas.
   * **[!UICONTROL Script Validation Message]**: Med det här alternativet kan du ange ett meddelande som ska visas om skriptvalideringen misslyckas.
     >[!NOTE]
     >Du kan ha flera molnkonfigurationer i din miljö i liknande syfte. Välj tjänsten noggrant. Om ingen tjänst visas läser du [Ansluta AEM Forms-miljön med Turnstile](#connect-your-forms-environment-with-turnstile-service) för att lära dig hur du skapar en Cloud Service som ansluter AEM Forms-miljön till den färdiga tjänsten.
   * **Felmeddelande:** Ange felmeddelandet som ska visas för användaren när Captcha-överföringen misslyckas.

1. Välj **[!UICONTROL Done]**.


Nu är det bara berättigade formulär, där formuläranvändaren kan ta bort den utmaning som Turnstile-tjänsten utgör, som kan användas för att skicka in formuläret.

![Turnstile Challenge](assets/turnstile-challenge.png)


## Vanliga frågor

* **F: Kan jag använda mer än en Captcha-komponent i ett adaptivt formulär?**
* **Ans:** Det går inte att använda fler än en Captcha-komponent i ett adaptivt formulär. Du bör inte heller använda en Captcha-komponent i ett fragment eller en panel som är markerad för lazy loading.

## Se även {#see-also}

{{see-also}}
