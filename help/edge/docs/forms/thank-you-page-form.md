---
title: Konfigurera tacksidan eller omdirigeringsformuläret efter att du skickat det
description: Lär dig konfigurera tacksidor och omdirigering för Forms Block för att optimera användarupplevelsen och effektivisera användarresorna.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: fd2e5df72e965ea6f9ad09b37983f815954f915c
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 0%

---


# Visa tacksidan eller omdirigeringsformuläret efter att du skickat in det

När en användare har skickat in ett formulär är det viktigt att kunna erbjuda en smidig upplevelse via en tacksida eller en omdirigering. Dessa element bekräftar inte bara att de har lämnats in utan även att de ger nöjdare användare och leder dem vidare på kundresan.

* **Tack**: En tacksida är hörnstenen i användarupplevelsen och ger trygghet och förmedlar viktig information samtidigt som varumärkesidentiteten förstärks. Det fungerar som ett direkt erkännande av användarens åtgärder och ger en känsla av komplettering och tillfredsställelse.

* **Omdirigering**: En omdirigering spelar en avgörande roll för att styra användarna mot relevanta destinationer, optimera engagemanget och i slutändan öka konverteringsgraden. En omdirigering ger en smidig navigeringsupplevelse genom att användaren smidigt vägleds till nästa steg i kundresan. Du kan till exempel dirigera om användare till betalningssidan efter att du har samlat in initiala uppgifter.

I det adaptiva Forms-blocket är standardbeteendet att visa en tacksida. Du kan dock anpassa den här upplevelsen efter dina specifika behov. Alternativen är:

* [Konfigurera tacksidan och meddelandet för att passa ert varumärke och era kommunikationsmål](#configuring-the-thank-you-page-and-message)
* [Dirigera om användare till en annan sida efter att de skickats in för ytterligare åtgärder](#redirect-users-to-another-page-post-submission)

## Konfigurera tacksidan och meddelandet

Standardbeteendet för Adaptive Forms-block är att visa&quot;thankyou&quot;-sidan när det skickas. Följ de här stegen för att konfigurera&quot;thankyou&quot;-sidan för ditt adaptiva Forms-block:

1. Gå till projektmappen AEM Edge Delivery på Microsoft SharePoint eller Google Workspace.
1. Skapa en Microsoft Word- eller Google Docs-fil med namnet&quot;thankyou&quot; i projektkatalogen.
1. Lägg till ditt tackmeddelande i&quot;thankyou&quot;-filen. </br>

   ![Exempel på tacksida](/help/edge/assets/sample-thankyou-page.png)

1. Använd AEM Sidekick för att förhandsgranska och publicera&quot;Tack&quot;-filen.

Ditt adaptiva Forms-block visar&quot;thankyou&quot;-sidan när du skickar in formulär.

## Dirigera om användare till en annan sida efter att de skickats in

Som standard dirigerar Adaptive Forms-blocket om användarna till&quot;thankyou&quot;-sidan. Om du vill dirigera om användare till en annan sida än standardsidan&quot;Tack&quot; har du två alternativ:

* [Ersätt&quot;Tack&quot;-sidan med en annan sida](#replace-the-existing-thankyou-page)
* [Använd omdirigeringar av webbplatser för sidomdirigering&quot;tack&quot;](#use-website-redirects-for-thankyou-page-redirection)

### Ersätt&quot;thankyou&quot;-sidan

1. Öppna &quot;[EDS-projekt]/blocks/form/form.js&quot; för redigering.
1. Ändra `thankyou` sida på följande rad till valfri sida:

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'thankyou';
   ```

   Exempel:

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'payment';
   ```

   >[!NOTE]
   >
   > Kontrollera att det finns en sida med samma namn i projektmappen Edge Delivery Service på antingen Microsoft SharePoint eller Google Workspace. Om sidan inte finns fortsätter du med att skapa och publicera den.

1. Fortsätt med att checka in den uppdaterade &#39;form.js&#39;-mappen och dess underliggande filer i Edge Delivery Service-projektet på GitHub. Denna uppdatering säkerställer att formuläret nu dirigeras om till den uppdaterade sidan enligt specifikationen.

1. Kontrollera att sidan finns i EDS-projektmappen och publicera den.


### Använd omdirigeringar av webbplatser för sidomdirigering&quot;tack&quot;

Att dirigera om en användare till en annan sida efter att formuläret har skickats in kan förbättra användarupplevelsen genom att tillhandahålla relevant information, bekräfta åtgärder och vägleda användarna mot önskat resultat. Exempel:

* när en användare har slutfört ett inköpsformulär omdirigeras de till en betalningssida för att slutföra transaktionen på ett säkert sätt.
* När man skickar in ett registreringsformulär för en händelse eller webbinarium dirigeras man om till en bekräftelsesida med händelseinformation som datum, tid och plats.

Om du vill dirigera om&quot;Tack&quot;-sidan till en annan sida använder du [omdirigeringar av webbplatser](https://www.aem.live/docs/redirects) kalkylblad.


## Se mer

* [Formulärkomponenter](/help/edge/docs/forms/form-components.md)
* [Egenskaper för formulärfält](/help/edge/docs/forms/eds-form-field-properties)
* [Skapa och förhandsgranska ett formulär](/help/edge/docs/forms/create-forms.md)
* [Aktivera formulär för att skicka data](/help/edge/docs/forms/submit-forms.md)
* [Publicera ett formulär på webbplatssidan](/help/edge/docs/forms/publish-forms.md)
* [Lägga till valideringar i formulärfält](/help/edge/docs/forms/validate-forms.md)
* [Ändra teman och format för formulär](/help/edge/docs/forms/style-theme-forms.md)
