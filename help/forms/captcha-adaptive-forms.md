---
title: Hur använder man CAPTCHA i Adaptive Forms?
description: Lär dig konfigurera eller konfigurera Google reCAPTCHA-tjänsten för ett adaptivt formulär.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
feature: Adaptive Forms, Foundation Components
role: User, Developer
exl-id: 3fdbe5a3-5c3c-474d-b701-e0182da4191a
source-git-commit: b5340c23f0a2496f0528530bdd072871f0d70d62
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 0%

---

# Använd reCAPTCHA i Adaptiv Forms {#using-reCAPTCHA-in-adaptive-forms}

>[!NOTE]
>
> Adobe rekommenderar att du använder den moderna och utbyggbara datainhämtningen [Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=sv-SE) för [att skapa nya adaptiva Forms](/help/forms/creating-adaptive-form-core-components.md) eller [lägga till adaptiva Forms på AEM Sites-sidor](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter.


| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/captcha-adaptive-forms.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |
| Gäller för | Adaptiv form baserad på grundläggande komponenter. <br> [Klicka här](/help/forms/captcha-adaptive-forms-core-components.md) för anpassat formulär baserat på kärnkomponenter. |


CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) är ett program som ofta används vid onlinetransaktioner för att skilja mellan människor och automatiserade program eller organ. Det utgör en utmaning och utvärderar användarens svar för att avgöra om det är en människa eller en robot som interagerar med webbplatsen. Det förhindrar användaren att fortsätta om testet misslyckas och gör onlinetransaktionerna säkra genom att förhindra att skräppost eller skadliga syften publiceras.

AEM Forms as a Cloud Service stöder följande CAPTCHA-lösningar:

* [Google reCAPTCHA](#configure-recaptcha-service-by-google)
* [Molnformad vändning](/help/forms/integrate-adaptive-forms-turnstile.md)
* [hCaptcha](/help/forms/integrate-adaptive-forms-hcaptcha.md)

## Konfigurera tjänsten reCAPTCHA från Google {#google-reCAPTCHA}

Formulärförfattare kan använda tjänsten reCAPTCHA från Google för att implementera reCAPTCHA i Adaptiv Forms. Den erbjuder avancerade CAPTCHA-funktioner för att skydda er webbplats. Mer information om hur reCAPTCHA fungerar finns i [Google reCAPTCHA](https://developers.google.com/recaptcha/). AEM Forms stöder [!DNL reCAPTCHA v2] och [!DNL reCAPTCHA Enterprise]. Andra versioner stöds inte. Observera också att reCAPTCHA i Adaptive Forms inte stöds i offlineläge i appen [!DNL AEM Forms]. Beroende på dina behov kan du konfigurera tjänsten reCAPTCHA för att aktivera:

![reCAPTCHA](/help/forms/assets/recaptcha_new.png)

* [reCAPTCHA Enterprise i AEM Forms](#steps-to-implement-reCAPTCHA-enterprise-in-forms)
* [reCAPTCHA v2 i AEM Forms](#steps-to-implement-reCAPTCHA-v2-in-forms)


### Konfigurera reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms}

1. Skapa eller välj ett [Google Cloud-projekt](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin) och aktivera [reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api).
1. Hämta [projekt-ID](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) och skapa en [API-nyckel](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key) och en [webbplatsnyckel för webbplatser](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key).
1. Skapa konfigurationsbehållare för molntjänster.

   1. Gå till **[!UICONTROL Tools > General > Configuration Browser]**.
   1. Välj en mapp eller skapa en mapp och aktivera mappen för molnkonfigurationer med följande steg:
      1. Markera mappen i Configuration Browser och välj **[!UICONTROL Properties]**.
      1. Aktivera **[!UICONTROL Cloud Configurations]** i dialogrutan Konfiguration.
      1. Välj **[!UICONTROL Save & Close]** om du vill spara konfigurationen och stänga dialogrutan.

1. Konfigurera molntjänsten för [!DNL reCAPTCHA Enterprise].

   1. Gå till ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]** på författarinstansen av Experience Manager.
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
1. Skapa konfigurationsbehållare för molntjänster.
   1. Gå till **[!UICONTROL Tools > General > Configuration Browser]**.
   1. Välj en mapp eller skapa en mapp och aktivera mappen för molnkonfigurationer med följande steg:
      1. Markera mappen i Configuration Browser och välj **[!UICONTROL Properties]**.
      1. Aktivera **[!UICONTROL Cloud Configurations]** i dialogrutan Konfiguration.
      1. Välj **[!UICONTROL Save & Close]** om du vill spara konfigurationen och stänga dialogrutan.

1. Konfigurera molntjänsten för reCAPTCHA v2.

   1. Gå till ![tools-1](assets/tools-1.png) > **Cloud Service** på AEM författarinstans.
   1. Välj **[!UICONTROL reCAPTCHA]**. Sidan Konfigurationer öppnas. Välj den konfigurationsbehållare som du skapade och välj **[!UICONTROL Create]**.
   1. Välj version som [!DNL reCAPTCHA v2], ange namn, platsnyckel och hemlig nyckel för reCAPTCHA-tjänsten (hämtas i steg 1) och välj **[!UICONTROL Create]** för att skapa molntjänstkonfigurationen.
   1. I dialogrutan Redigera komponent anger du platsen och de hemliga nycklarna som fås i steg 1. Välj **[!UICONTROL Save Settings]** och välj sedan **OK** för att slutföra konfigurationen.

   När reCAPTCHA-tjänsten har konfigurerats är den tillgänglig för användning i adaptiva formulär. Mer information finns i [Använda CAPTCHA i adaptiva formulär](#using-reCAPTCHA).

<!--![reCAPTCHA v2](/help/forms/assets/recaptcha-v2.png)-->


## Använd Google reCAPTCHA i anpassningsbara formulär {#using-reCAPTCHA}

Så här använder du Google reCAPTCHA i en adaptiv form:

1. Öppna ett anpassat formulär i redigeringsläge.

   >[!NOTE]
   >
   >Kontrollera att den konfigurationsbehållare som valts när du skapar det adaptiva formuläret innehåller molntjänsten reCAPTCHA. Du kan också redigera adaptiva formuläregenskaper för att ändra konfigurationsbehållaren som är kopplad till formuläret.

1. Dra **Captcha** -komponenten från komponentwebbläsaren till det adaptiva formuläret.

   >[!NOTE]
   >
   >* Det går inte att använda mer än en Captcha-komponent i ett adaptivt formulär. Du bör inte heller använda CAPTCHA i en panel som är markerad för lazy loading eller i ett fragment.
   >* reCaptcha är tidskänsligt och upphör om cirka ett par minuter. Därför rekommenderar vi att du placerar Captcha-komponenten precis före Skicka-knappen i den anpassade formen.

1. Markera den Captcha-komponent som du har lagt till och välj ![cmpr](assets/cmppr.png) för att redigera dess egenskaper.
1. Ange en titel för CAPTCHA-widgeten. Standardvärdet är **Captcha**. Välj **Dölj titel** om du inte vill att titeln ska visas.
1. I listrutan **Captcha-tjänst** väljer du **reCAPTCHA** för att aktivera reCAPTCHA-tjänsten om du har konfigurerat den enligt beskrivningen i [reCAPTCHA-tjänsten av Google](#google-reCAPTCHA).
1. Välj en konfiguration i listrutan Inställningar för **reCAPTCHA Enterprise** eller **reCAPTCHA v2**
   1. Om du väljer versionen **reCAPTCHA Enterprise** kan nyckeltypen vara **kryssruta** eller **poäng baserad**, den baseras på ditt val när du konfigurerar [webbplatsnyckel för webbplatser](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key):

   >[!NOTE]
   >
   >* I molnkonfigurationen med **nyckeltyp** som **kryssruta** visas det anpassade felmeddelandet som ett infogat meddelande om captcha-valideringen misslyckas.
   >* I molnkonfigurationen med **nyckeltyp** som **poäng baserad** visas det anpassade felmeddelandet som ett popup-meddelande om captcha-valideringen misslyckas.

   1. Du kan välja storlek som **[!UICONTROL Normal]** och **[!UICONTROL Compact]**.
   1. Du kan välja en **[!UICONTROL Bind Reference]**. I **[!UICONTROL Bind Reference]** är skickade data bundna, annars är de obundna data. Nedan finns XML-exempel på obundna data och bundna data (med bind referens som SSN) när ett formulär skickas.

   ```xml
           <?xml version="1.0" encoding="UTF-8" standalone="no"?>
           <afData>
           <afUnboundData>
               <data>
                   <captcha16820607953761>
                       <captchaType>reCaptchaEnterprise</captchaType>
                       <captchaScore>0.9</captchaScore>
                   </captcha16820607953761>
               </data>
           </afUnboundData>
           <afBoundData>
               <Root
                   xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                   <PersonalDetails>
                       <SSN>371237912</SSN>
                       <FirstName>Sarah </FirstName>
                       <LastName>Smith</LastName>
                   </PersonalDetails>
                   <OtherInfo>
                       <City>California</City>
                       <Address>54 Residency</Address>
                       <State>USA</State>
                       <Zip>123112</Zip>
                   </OtherInfo>
               </Root>
           </afBoundData>
           <afSubmissionInfo>
               <stateOverrides/>
               <signers/>
               <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
               <afSubmissionTime>20230608034928</afSubmissionTime>
           </afSubmissionInfo>
           </afData>
   ```

   ```xml
           <?xml version="1.0" encoding="UTF-8" standalone="no"?>
           <afData>
           <afUnboundData>
               <data/>
           </afUnboundData>
           <afBoundData>
               <Root
                   xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                   <PersonalDetails>
                       <SSN>
                           <captchaType>reCaptchaEnterprise</captchaType>
                           <captchaScore>0.9</captchaScore>
                       </SSN>
                       <FirstName>Sarah</FirstName>
                       <LastName>Smith</LastName>
                   </PersonalDetails>
                   <OtherInfo>
                       <City>California</City>
                       <Address>54 Residency</Address>
                       <State>USA</State>
                       <Zip>123112</Zip>
                   </OtherInfo>
               </Root>
           </afBoundData>
           <afSubmissionInfo>
               <stateOverrides/>
               <signers/>
               <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
               <afSubmissionTime>20230608035111</afSubmissionTime>
           </afSubmissionInfo>
           </afData>
   ```

   Om du väljer version **reCAPTCHA v2**:
   1. Du kan välja storleken som **[!UICONTROL Normal]** eller **[!UICONTROL Compact]** för widgeten reCAPTCHA.
   1. Du kan välja alternativet **[!UICONTROL Invisible]** om du bara vill visa CAPTCHA-utmaningen om en misstänkt aktivitet inträffar.

   Tjänsten reCAPTCHA är aktiverad i det adaptiva formuläret. Du kan förhandsgranska formuläret och se hur CAPTCHA fungerar. Märket **protected by reCAPTCHA**, som visas nedan, visas i skyddade formulär.
   ![Google skyddat av reCAPTCHA-märke](/help/forms/assets/google-recaptcha-v2.png)

1. Spara egenskaperna.

>[!NOTE]
> 
> Välj inte **[!UICONTROL Default]** i listrutan för Captcha-tjänster eftersom AEM CAPTCHA-tjänsten är föråldrad.

>[!VIDEO](https://video.tv.adobe.com/v/3422641/recaptcha-google-adaptive-forms/?quality=12&learn=on)

### Visa eller dölj CAPTCHA-komponent baserat på regler {#show-hide-captcha}

Du kan välja att visa eller dölja CAPTCHA-komponenten baserat på regler som du tillämpar på en komponent i ett adaptivt formulär. Markera komponenten, välj ![redigera regler](assets/edit-rules-icon.svg) och välj **[!UICONTROL Create]** för att skapa en regel. Mer information om hur du skapar regler finns i [Regelredigeraren](rule-editor.md).

CAPTCHA-komponenten måste till exempel bara visas i ett adaptivt formulär om fältet Valutavärde i formuläret har ett värde över 25000.

Markera fältet **[!UICONTROL Currency Value]** i formuläret och skapa följande regler:

![Visa eller dölj regler](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> När du väljer en reCAPTCHA v2-konfiguration och storleken är inställd på [!UICONTROL Invisible], är alternativet för att visa/dölja fortfarande inaktiverat.

### Validera CAPTCHA {#validate-captcha}

Du kan validera CAPTCHA i ett adaptivt formulär antingen när du skickar formuläret eller baserar CAPTCHA-valideringen på användaråtgärder och villkor.

#### Validera CAPTCHA när formulär skickas {#validation-form-submission}

Så här validerar du en CAPTCHA automatiskt när du skickar in ett adaptivt formulär:

1. Markera CAPTCHA-komponenten och välj ![cmpr](assets/configure-icon.svg) för att visa komponentegenskaperna.
1. Välj **[!UICONTROL Validate CAPTCHA at form submission]** i avsnittet **[!UICONTROL Validate CAPTCHA]**.
1. Välj ![Klar](assets/save_icon.svg) om du vill spara komponentegenskaperna.

#### Validera CAPTCHA på användaråtgärder och villkor {#validate-captcha-user-action}

Så här validerar du en CAPTCHA baserat på villkor och användaråtgärder:

1. Markera CAPTCHA-komponenten och välj ![cmpr](assets/configure-icon.svg) för att visa komponentegenskaperna.
1. Välj **[!UICONTROL Validate CAPTCHA on a user action]** i avsnittet **[!UICONTROL Validate CAPTCHA]**.
1. Välj ![Klar](assets/save_icon.svg) om du vill spara komponentegenskaperna.

[!DNL Experience Manager Forms] tillhandahåller `ValidateCAPTCHA` API för att validera CAPTCHA med fördefinierade villkor. Du kan anropa API:t med en anpassad skickaåtgärd eller genom att definiera regler för komponenter i ett anpassat formulär.

Följande är ett exempel på ett `ValidateCAPTCHA`-API för att validera CAPTCHA med fördefinierade villkor:

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

Exemplet visar att API:t `ValidateCAPTCHA` bara validerar CAPTCHA i formuläret om antalet siffror i den numeriska rutan som användaren anger när formuläret fylls i är större än 5.

**Alternativ 1: Använd [!DNL Experience Manager Forms] ValidateCAPTCHA API för att validera CAPTCHA med en anpassad överföringsåtgärd**

Utför följande steg för att använda API:t `ValidateCAPTCHA` för att validera CAPTCHA med en anpassad skickaåtgärd:

1. Lägg till skriptet som innehåller `ValidateCAPTCHA`-API:t till en anpassad skickaåtgärd. Mer information om anpassade Skicka-åtgärder finns i [Skapa en anpassad Skicka-åtgärd för anpassad Forms](custom-submit-action-form.md).
1. Välj namnet på den anpassade skickaåtgärden i listrutan **[!UICONTROL Submit Action]** i egenskaperna **[!UICONTROL Submission]** för ett anpassat formulär.
1. Välj **[!UICONTROL Submit]**. CAPTCHA valideras baserat på villkoren som definieras i `ValidateCAPTCHA` API för den anpassade åtgärden Skicka.

**Alternativ 2: Använd [!DNL Experience Manager Forms] ValidateCAPTCHA API för att validera CAPTCHA på en användaråtgärd innan formuläret skickas**

Du kan också anropa `ValidateCAPTCHA` API genom att tillämpa regler på en komponent i ett adaptivt formulär.

Du kan till exempel lägga till en **[!UICONTROL Validate CAPTCHA]**-knapp i ett adaptivt formulär och skapa en regel som anropar en tjänst genom att klicka på en knapp.

Följande bild visar hur du kan anropa en tjänst genom att klicka på en **[!UICONTROL Validate CAPTCHA]**-knapp:

![Validera CAPTCHA](assets/captcha-validation1.gif)

Du kan anropa den anpassade servern som innehåller `ValidateCAPTCHA` API med regelredigeraren och aktivera eller inaktivera skicka-knappen för det anpassade formuläret baserat på valideringsresultatet.

På samma sätt kan du använda regelredigeraren för att inkludera en anpassad metod för att validera CAPTCHA i ett adaptivt formulär.

<!--

### Add custom CAPTCHA services {#add-custom-captcha-service}

[!DNL Experience Manager Forms] provides reCAPTCHA as the CAPTCHA service. However, you can add a custom service to display in the **[!UICONTROL CAPTCHA Service]** drop-down list.  

The following is a sample implementation of the interface to add additional CAPTCHA service to your Adaptive Form:

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

`captchaPropertyNodePath` refers to the resource path of the CAPTCHA component in the Sling repository. Use this property to include details specific to the CAPTCHA component. For example, `captchaPropertyNodePath` includes information for the reCAPTCHA cloud configuration configured on the CAPTCHA component. The cloud configuration information provides **[!UICONTROL Site Key]** and **[!UICONTROL Secret Key]** settings for implementing the reCAPTCHA service.

`userResponseToken` refers to the `g_recaptcha_response` that gets generated after solving a CAPTCHA in a form. -->

### Redigera reCAPTCHA-tjänstdomän {#reCAPTCHA-service-domain}

reCAPTCHA-tjänsten använder `https://www.recaptcha.net/` som standarddomän. Du kan ändra inställningarna för att ange `https://www.google.com/` eller ett anpassat domännamn för inläsning, återgivning och validering av tjänsten reCAPTCHA.

Ange egenskapen **[!UICONTROL af.cloudservices.recaptcha.domain]** för konfigurationen **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]** för att ange `https://www.google.com/` eller något annat anpassat domännamn. I följande JSON-fil visas ett exempel:

```json
{
  "af.cloudservices.recaptcha.domain": "https://www.google.com/"
}
```

[Generera OSGi-konfigurationer med AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=sv-SE#generating-osgi-configurations-using-the-aem-sdk-quickstart) och [distribuera konfigurationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=sv-SE#deployment-process) till din Cloud Service om du vill ange värden för en konfiguration.

## Se även {#see-also}

{{see-also}}

<!--

>[!MORELIKETHIS]
>
>* [Reference Themes, Templates, and Form Data models for Adaptive Forms](/help/forms/reference-themes-templates-data-models.md)

-->
