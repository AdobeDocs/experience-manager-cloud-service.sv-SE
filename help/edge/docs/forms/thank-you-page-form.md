---
title: Visa ett anpassat tackmeddelande efter att formuläret har skickats
description: Lär dig konfigurera tacksidor och omdirigering för Forms Block för att optimera användarupplevelsen och effektivisera användarresorna.
feature: Edge Delivery Services
exl-id: e6c66b22-dc52-49e3-a920-059adb5be22f
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# Visa ett anpassat tackmeddelande efter att formuläret har skickats

När en användare har skickat in ett formulär är det viktigt att kunna erbjuda en smidig upplevelse genom ett tackmeddelande. Det bekräftar inte bara att ansökan har lämnats in, det ger också nöjdare användare och leder dem vidare på kundresan.

- **Tack**! Ett tackmeddelande är en hörnsten i användarupplevelsen och ger trygghet och förmedlar viktig information samtidigt som varumärkesidentiteten förstärks. Det fungerar som ett direkt erkännande av användarens åtgärder och ger en känsla av komplettering och tillfredsställelse.

- **Omdirigering**: En omdirigering spelar en avgörande roll för att styra användare mot relevanta destinationer, optimera engagemanget och i slutändan öka konverteringsgraden. En omdirigering ger en smidig navigeringsupplevelse genom att användaren smidigt vägleds till nästa steg i kundresan. Du kan till exempel dirigera om användaren till betalningssidan efter att du har samlat in initiala uppgifter.

Standardbeteendet för Adaptive Forms Block är att visa följande tackmeddelande när det skickas. Meddelandet visas högst upp i formuläret när formuläret har skickats.

![standardtackmeddelande](/help/edge/assets/thank-you-message.png)

Du kan dock anpassa den här upplevelsen efter dina specifika behov. Alternativen är:

- Visa ett anpassat tackmeddelande efter att formuläret har skickats
- Dirigera om användare till en annan sida efter inskickandet för ytterligare åtgärder

>[!NOTE]
>
> Du kan använda följande [frågekalkylblad](/help/edge/docs/forms/assets/enquiry.xlsx) för att anpassa tackmeddelandet efter dina önskemål.

## Konfigurera ett anpassat tackmeddelande

Om du vill visa ett personligt tackmeddelande när formuläret har skickats kan du konfigurera kalkylbladet så att det visas.

Följ stegen nedan för att konfigurera ett anpassat tackmeddelande för ditt adaptiva Forms-block:

1. Gå till projektmappen Edge Deliver på Microsoft SharePoint eller Google Workspace och öppna kalkylbladet.
1. Lägg till ett anpassat tackmeddelande i kolumnen `value` för fälttypen `submit` i kalkylbladet.

   ![Anpassat tackmeddelande](/help/edge/docs/forms/assets/thankyou-custommessage.png)

   Lägg till exempel till meddelandet `Submission Successful!` i kolumnen `value` för fälttypen `submit`.

1. Förhandsgranska och publicera bladet med [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   ![Anpassat tackmeddelande](/help/edge/docs/forms/assets/customized-thank-you-message.png)

## Dirigera om användare till en annan sida efter att de skickats in

Att dirigera om en användare till en annan sida efter att formuläret har skickats in kan förbättra användarupplevelsen genom att tillhandahålla relevant information, bekräfta åtgärder och vägleda användarna mot önskat resultat. Exempel:

- när en användare har slutfört ett inköpsformulär omdirigeras de till en betalningssida för att slutföra transaktionen på ett säkert sätt.
- När man skickar in ett registreringsformulär för en händelse eller webbinarium dirigeras man om till en bekräftelsesida med händelseinformation som datum, tid och plats.

Följ stegen nedan för att omdirigera användare till en annan sida:

1. Gå till projektmappen Edge Deliver på Microsoft SharePoint eller Google Workspace och öppna kalkylbladet.
1. Klistra in URL:en i kolumnen `value` för fälttypen `submit` i kalkylbladet för att omdirigera användaren när formuläret har skickats.
Om du vill dirigera om sidan till en annan sida använder du URL:en för sidan [Edge Delivery Documentation](https://www.aem.live/docs/) .

   ![Tack! Omdirigerings-URL](/help/edge/docs/forms/assets/thankyou-redirecturl.png)

1. Förhandsgranska och publicera bladet med [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   ![Omdirigera tackmeddelande](/help/edge/docs/forms/assets/thankyou-redirectpage.gif)

Du kan också skapa en ny dokumentfil och lägga till dess förhandsgransknings-URL i kolumnen `value` för fälttypen `submit`.

När en användare har skickat in ett formulär är det viktigt att du skickar ett tydligt tackmeddelande. Det bekräftar att inlämningen är klar och att användaren blir nöjdare.

