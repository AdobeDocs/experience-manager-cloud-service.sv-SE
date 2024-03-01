---
title: Konfigurera tacksida för EDS Forms
description: Lär dig konfigurera tacksidor och omdirigering för EDS Forms för att optimera användarupplevelsen och effektivisera användarresorna.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e2970c7a141025222c6b119787142e7c39d453af
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Konfigurera Tack-sidor och omdirigering i adaptiva Forms-block

Tack för att du skickar sidor och omdirigering är viktiga aspekter av förbättringar av användarupplevelsen, vilket ger användarna en bekräftelse, tydlig kommunikation och smidig navigering efter att formuläret har skickats in.

## Konfigurera tacksidor

Tack! Sidorna är ett tryggt erkännande till användarna och gör det möjligt för organisationer att förmedla viktig information samtidigt som varumärkesidentiteten förstärks. Följ de här stegen för att konfigurera en tacksida för EDS Forms:

1. Gå till projektmappen AEM Edge Delivery på Microsoft SharePoint eller Google Workspace.
1. Skapa en Microsoft Word- eller Google Docs-fil med namnet&quot;thankyou&quot; i projektkatalogen.
1. Lägg till ditt tackmeddelande i&quot;thankyou&quot;-filen.
   ![Exempel på tacksida](/help/edge/assets/sample-thankyou-page.png)
1. Använd AEM Sidekick för att förhandsgranska och publicera&quot;thankyou&quot;-filen.

## Omdirigera användare efter överföring

Omdirigering underlättar smidiga användarresor genom att vägleda användarna till relevanta destinationer, optimera engagemanget och öka konverteringsgraden.

Som standard dirigerar Adaptive Forms-blocket om användarna till&quot;thankyou&quot;-sidan. Om du vill dirigera om användare till en annan sida än standardsidan&quot;Tack&quot; har du två alternativ:

* ersätta den befintliga&quot;tack&quot;-sidan med en annan sida, eller
* omdirigera&quot;thankyou&quot;-sidan till en annan sida som du väljer.

### Ersätt den befintliga&quot;tack&quot;-sidan

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


### Använd omdirigeringar av webbplatser

Konfigurera en omdirigering av en webbplats som dirigerar&quot;Tack&quot;-sidan till en annan sida. Se [Omdirigerar dokumentation](https://www.aem.live/docs/redirects) för detaljerade anvisningar.


