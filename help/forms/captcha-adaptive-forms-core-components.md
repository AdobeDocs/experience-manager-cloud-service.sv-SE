---
title: Hur använder man Google reCAPTCHA i en AEM Adaptiv form?
description: Förbättra säkerheten med Google reCAPTCHA-tjänsten utan problem. Stegvisa anvisningar inifrån!
topic-tags: Adaptive Forms, author
keywords: Google reCAPTCHA-tjänst, Adaptiv Forms, CAPTCHA-utmaning, startalternativ, kärnkomponenter, säkerhet för inskickande av formulär, skydd mot skräppost
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: d116f979-efb6-4fac-8202-89afd1037b2c
source-git-commit: 76301ca614ae2256f5f8b00c41399298c761ee33
workflow-type: tm+mt
source-wordcount: '1348'
ht-degree: 0%

---

# Använd Google reCAPTCHA i ett AEM-anpassat formulär baserat på kärnkomponenter {#using-reCAPTCHA-in-adaptive-forms}

| Gäller för | Artikellänk |
| -------- | ---------------------------- |
| Adaptiv form baserad på kärnkomponenter | Den här artikeln |
| Adaptiv form baserad på grundläggande komponenter | [Klicka här](/help/forms/captcha-adaptive-forms.md) |

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) är ett program som ofta används vid onlinetransaktioner för att skilja mellan människor och automatiserade program eller organ. Det utgör en utmaning och utvärderar användarens svar för att avgöra om det är en människa eller en robot som interagerar med webbplatsen. Det förhindrar användaren att fortsätta om testet misslyckas och gör onlinetransaktionerna säkra genom att förhindra att skräppost eller skadliga syften publiceras.

AEM Forms as a Cloud Service stöder följande CAPTCHA-lösningar:

* [Google reCAPTCHA](#connect-your-aem-forms-environment-with-recaptcha-service-by-google)
* [hCaptcha](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)


## Koppla samman dina AEM Forms Core-komponenter med reCAPTCHA-tjänsten från Google {#connect-your-forms-environment-with-recaptcha-service-by-google}

Formulärförfattare kan använda tjänsten reCAPTCHA från Google för att implementera reCAPTCHA i Adaptiv Forms. Den erbjuder avancerade CAPTCHA-funktioner för att skydda er webbplats. Mer information om hur reCAPTCHA fungerar finns i [Google reCAPTCHA](https://developers.google.com/recaptcha/). Du använder den för att presentera en CAPTCHA-utmaning när formulär skickas in.[!DNL AEM Forms] som [!DNL Cloud Service] har stöd för Google reCAPTCHA v2 och reCAPTCHA Enterprise. Andra versioner stöds inte. Observera också att reCAPTCHA i Adaptive Forms inte stöds i offlineläge i AEM Forms-appen.

Beroende på dina behov kan du konfigurera tjänsten reCAPTCHA för att aktivera:

* [reCAPTCHA Enterprise](#steps-to-implement-reCAPTCHA-enterprise-in-forms-core-components)
* [reCAPTCHA v2](#steps-to-implement-reCAPTCHA-v2-in-forms)

### Konfigurera reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms-core-components}

1. Skapa eller välj ett [Google Cloud-projekt](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin) och aktivera [reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api).
1. Hämta [projekt-ID](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) och skapa en [API-nyckel](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key) och en [webbplatsnyckel för webbplatser](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key).
1. Skapa konfigurationsbehållare för molntjänster.

   1. Gå till **[!UICONTROL Tools > General > Configuration Browser]**.
   1. Välj en mapp eller skapa en mapp och aktivera mappen för molnkonfigurationer med följande steg:
      1. Markera mappen i Configuration Browser och välj **[!UICONTROL Properties]**.
      1. Aktivera **[!UICONTROL Cloud Configurations]** i dialogrutan Konfiguration.
      1. Välj **[!UICONTROL Save & Close]** om du vill spara konfigurationen och stänga dialogrutan.

1. Konfigurera molntjänsten för [!DNL reCAPTCHA Enterprise].

   1. Gå till ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]** på din Experience Manager-författarinstans.
   1. Välj **[!UICONTROL reCAPTCHA]**. Sidan Konfigurationer öppnas. Välj den konfigurationsbehållare som du skapade och välj **[!UICONTROL Create]**.
   1. Välj version som [!DNL reCAPTCHA Enterprise] och ange namn, projekt-ID, platsnyckel och API-nyckel (hämtas i steg 2) för reCAPTCHA Enterprise-tjänsten.
   1. Välj nyckeltyp. Nyckeltypen ska vara densamma som den webbplatsnyckel som du konfigurerade i [Google Cloud-projektet](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin), till exempel **Checkbox-webbplatsnyckel** eller **Score-baserad webbplatsnyckel**.
   1. Ange ett [tröskelvärde i intervallet 0 till 1](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment#interpret_scores). Poängvärden som är större än eller lika med tröskelvärdena identifierar mänsklig interaktion, vilket i annat fall omfattar båda interaktioner.
   1. Välj **[!UICONTROL Create]** om du vill skapa molntjänstkonfigurationen.

<!--
    1. In the Edit Component dialog, specify the name, project ID, site key, API key (obtained in steps 2 and 3), select the key type, and enter the threshold score. Select **[!UICONTROL Save Settings]** and then select **[!UICONTROL OK]** to complete the configuration.
-->

När du har aktiverat tjänsten reCAPTCHA Enterprise kan den användas i anpassningsbara formulär. Se [använda CAPTCHA i adaptiva formulär](#using-reCAPTCHA).

<!--
![reCAPTCHA Enterprise](/help/forms/assets/recaptcha1-enterprise.png)
-->


### Konfigurera Google reCAPTCHA v2 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. Hämta [reCAPTCHA API-nyckelpar](https://www.google.com/recaptcha/admin) från Google. Den innehåller en **webbplatsnyckel** och en **hemlig nyckel**.

   ![Skapa Google reCAPTCHA-konfiguration av Google webbplats för att hämta reCAPTCHA-nycklar](/help/forms/assets/google-captcha.gif)
1. Skapa en konfigurationsbehållare i din AEM Forms as a Cloud Service-miljö. En konfigurationsbehållare innehåller molnkonfigurationer som används för att ansluta AEM till externa tjänster. Så här skapar och konfigurerar du en Configuration Container för att ansluta AEM Forms-miljön till reCAPTCHA-tjänsten från Google:
   1. Öppna AEM Forms as a Cloud Service-instansen.
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

1. Konfigurera Cloud Service:
   1. Gå till ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]** och välj **[!UICONTROL reCAPTCHA]** i AEM-författarinstansen.
   1. Välj en konfigurationsbehållare som har skapats eller uppdaterats i föregående avsnitt. Välj **[!UICONTROL Create]**.
   1. Ange **[!UICONTROL Title]**, **[!UICONTROL Name]**, **[!UICONTROL Site Key]** och **[!UICONTROL Secret Key]** för reCAPTCHA-tjänsten (hämtas i steg 1). Välj **[!UICONTROL Create]**.

   ![Konfigurera Cloud Service för att ansluta din AEM Forms-miljö med reCAPTCHA-tjänsten från Google](/help/forms/assets/captcha-configuration.gif)

   När reCAPTCHA-tjänsten har konfigurerats kan den användas i ett adaptivt format. Mer information finns i [Använda Google reCAPTCHA i ett adaptivt formulär](#using-reCAPTCHA).


Använd Google reCAPTCHA i anpassningsbara formulär

## Använd Google reCAPTCHA i anpassad form {#using-reCAPTCHA}

Så här använder du reCAPTCHA i Adaptive Forms:

1. Öppna AEM Forms as a Cloud Service-instansen.
1. Gå till **[!UICONTROL Forms]** > **[!UICONTROL Forms and Documents]**.
1. Välj en anpassad Forms och välj **[!UICONTROL Properties]**. För alternativet **[!UICONTROL Configuration Container]** väljer du den konfigurationsbehållare som innehåller molnkonfigurationen som ansluter AEM Forms till reCAPTCHA-tjänsten av Google och väljer **[!UICONTROL Save & Close]**.

   Om du inte har någon sådan konfigurationsbehållare kan du läsa avsnittet [Anslut AEM Forms-miljön med reCAPTCHA-tjänsten från Google](#connect-your-forms-environment-with-recaptcha-service-by-google) för att lära dig hur du skapar en sådan konfigurationsbehållare.

   ![Välj konfigurationsbehållare](/help/forms/assets/captcha-properties.png)

1. Välj en anpassad Forms och välj **[!UICONTROL Edit]**. Det adaptiva formuläret öppnas i Adaptiv Forms Editor.
1. Dra komponenten **[!UICONTROL Adaptive Form reCAPTCHA]** från komponentwebbläsaren till det adaptiva formuläret.

   >[!NOTE]
   > * Google reCAPTCHA-validering är tidskänslig och upphör att gälla om cirka ett par minuter. Därför rekommenderar Adobe att du placerar komponenten **[!UICONTROL Adaptive Form reCAPTCHA]** precis före knappen **[!UICONTROL Submit]**.

1. Markera **[!UICONTROL Adaptive Form reCAPTCHA]**-komponenten och välj egenskapsikonen ![Egenskaper](assets/configure-icon.svg) . Dialogrutan Egenskaper öppnas. Ange följande obligatoriska egenskaper:
   * **[!UICONTROL Name]:** Du kan enkelt identifiera en formulärkomponent med dess unika namn både i formuläret och i regelredigeraren, men namnet får inte innehålla blanksteg eller specialtecken.
   * **[!UICONTROL Title]:** Ange en titel för CAPTCHA-widgeten. Standardvärdet är **Captcha**. Välj **Dölj titel** om du inte vill att titeln ska visas. Välj **Tillåt RTF för titel** om du vill redigera titeln i RTF-format. Du kan också markera titeln som **Obundet formulärelement**.
   * **[!UICONTROL CAPTCHA Configuration]:** Välj en konfiguration i listrutan Inställningar för **reCAPTCHA Enterprise** eller **reCAPTCHA v2** för att visa Google reCAPTCHA-dialogrutan för formuläret:
      1. Om du väljer versionen **reCAPTCHA Enterprise** kan nyckeltypen vara **kryssruta** eller **poäng baserad**, den baseras på ditt val när du konfigurerar [webbplatsnyckel för webbplatser](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key):

         >[!NOTE]
         >
         >* I molnkonfigurationen med **nyckeltyp** som **kryssruta** visas det anpassade felmeddelandet som ett infogat meddelande om captcha-valideringen misslyckas.
         >* I molnkonfigurationen med **nyckeltyp** som **poäng baserad** visas det anpassade felmeddelandet som ett popup-meddelande om captcha-valideringen misslyckas.

      1. Du kan välja storlek som **[!UICONTROL Normal]** och **[!UICONTROL Compact]**.

     >[!NOTE]
     >* Du kan ha flera molnkonfigurationer i din miljö för liknande ändamål. Välj tjänsten noggrant. Om ingen tjänst visas läser du [Anslut AEM Forms-miljön med reCAPTCHA-tjänsten från Google](#connect-your-forms-environment-with-recaptcha-service-by-google) för att lära dig hur du skapar en Cloud Service som ansluter din AEM Forms-miljö till reCAPTCHA-tjänsten från Google.

   * **Captcha-storlek:** Du kan välja visningsstorlek för Google reCAPTCHA-utmaningsdialogrutan. Använd alternativet **[!UICONTROL Compact]** om du vill visa en liten storlek och alternativet **[!UICONTROL Normal]** om du vill visa en relativt stor Google reCAPTCHA-utmaningsdialogruta.
Om du väljer version **reCAPTCHA v2**:
      1. Du kan välja storleken som **[!UICONTROL Normal]** eller **[!UICONTROL Compact]** för widgeten reCAPTCHA.
      1. Du kan välja alternativet **[!UICONTROL Invisible]** om du bara vill visa CAPTCHA-utmaningen om en misstänkt aktivitet inträffar.

   Tjänsten reCAPTCHA är aktiverad i det adaptiva formuläret. Du kan förhandsgranska formuläret och se hur CAPTCHA fungerar. Märket **protected by reCAPTCHA**, som visas nedan, visas i skyddade formulär.

   ![Google skyddat av reCAPTCHA-märke](/help/forms/assets/google-recaptcha-v2.png)

1. Välj **[!UICONTROL Done]**.

   Nu visas **protected by reCAPTCHA** i ditt adaptiva formulär. Den visas på alla Adaptive Forms som är konfigurerade att använda tjänsten Google reCAPTCHA.

   Nu är det bara berättigade formulär, i vilka den som fyller i formuläret kan ta bort den utmaning som Google reCAPTCHA-tjänsten utgör, som kan skickas in.

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
