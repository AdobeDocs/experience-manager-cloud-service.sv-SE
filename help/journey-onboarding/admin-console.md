---
title: Åtkomst till Admin Console
description: När du har förstått de förberedelser som krävs för att komma igång och grunderna i AEMaaCS-strukturen är du redo att logga in på Admin Console för första gången.
exl-id: 0ccce328-a356-4ba9-b7fe-f67abc25b924
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 0%

---

# Åtkomst till Admin Console {#accessing-admin-console}

I den här delen av [introduktionsresan ](overview.md) får du reda på vilka förberedelser som krävs innan du kan logga in i systemet för första gången.

## Syfte {#objective}

Nu när du har läst artikeln [AEM as a Cloud Service Terminology](terminology.md) och förstått grunderna i AEMaaCS-strukturen är du redo att logga in på Admin Console för första gången!

Som systemadministratör ansvarar du för att hantera användare i organisationen. Det gör du med Admin Console. När du har läst det här avsnittet bör du:

* Förstå vad en Adobe ID är.
* Du kan logga in på Admin Console.
* Lär dig hur du granskar dina behörigheter som systemadministratör via Admin Console.
* Ta reda på hur du kontaktar supporten för Adobe om du behöver hjälp.

## Admin Console {#admin-console}

Adobe Admin Console är en central plats för att administrera och hantera licenser och användare för Adobe. Med Admin Console kan du skapa och hantera användare på en och samma plats i stället för i olika individuella lösningar.

## Adobe ID {#adobe-id}

För att kunna logga in på Admin Console behöver du en Adobe ID. Och Adobe ID är ett konto som är knutet till en viss e-postadress som krävs för att logga in och få tillgång till AEM as a Cloud Service eller någon av dina Adobe-lösningar. Genom att använda din Adobe ID behåller du alla dina planer och produkter för Adobe som är kopplade till ett enda konto.

När du som systemadministratör konfigurerar ditt team i Admin Console anger du den e-postadress som ska användas som Adobe ID.

Det finns tre typer av Adobe-ID:

* **Personligt ID**: Detta är standardtypen för Adobe ID och skapas på adobe.com. Det här kontot hanteras av Adobe och alla kan skapa ett konto av den här typen.

* **Enterprise ID**: Organisationer vill vanligtvis få bättre kontroll över användarkonton. Endast systemadministratörer kan skapa Enterprise ID:n och organisationen äger dessa konton med Adobe som endast fungerar som värd.

* **Federated ID**: Med federerade ID:n övertar organisationen ägarskap och kontroll över kontona. För att göra detta måste ni integrera Adobe Experience Cloud med ert SAML2 SSO-system (single sign-on). Detta gör att användare kan autentisera mot sin organisations SSO-system i stället för ett konto som ligger hos Adobe.

Som systemadministratör kan du bestämma dig för att introducera dig själv och ditt team på AEM as a Cloud Service med personliga ID:n innan Enterprise ID eller Federated ID:n konfigureras. När Enterprise ID:n eller Federated ID:n har konfigurerats kan medlemmar övergå till att använda dessa ID:n.

## Logga in på Admin Console {#steps-admin-console}

Innan du kan använda Admin Console för att administrera användare i ditt team måste du se till att du själv har tillgång till den och rätt behörigheter.

1. Som systemadministratör kommer du att få flera e-postmeddelanden från Adobe som en del av introduktionsprocessen. Leta efter det välkomstmeddelande som innehåller information om organisationens namn som du har beviljats åtkomst till.

1. Klicka på länken **Kom igång** i ditt välkomstmeddelande för att navigera till Admin Console. Om du inte kan hitta e-postmeddelandet öppnar du en webbläsare direkt till Admin Console på [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com).

   ![Välkomstmeddelande](/help/journey-onboarding/assets/get-started-email.png)

1. Logga in med din Adobe ID. När inloggningen är klar visas sidan **Översikt** i Adobe Admin Console.

   ![Admin Console](/help/journey-onboarding/assets/get-started1.png)

1. Om du har tillgång till flera organisationer måste du se till att du har loggat in i rätt organisation. Om du vill ändra din organisation klickar du på organisationsnamnet i det övre högra hörnet och väljer den organisation som du behöver åtkomst till.

   ![Ändra organisation](/help/journey-onboarding/assets/admin-console-orgswitch.png)

1. Välj **Administratörer** på **användarkortet** för att verifiera att du är systemadministratör.

   ![Granska administratörer](/help/journey-onboarding/assets/get-started2.png)

1. När du har klickat på **Administratörer** på kortet **Användare** kan du söka genom att ange din Adobe ID-e-postadress, ditt användarnamn, för- eller efternamn.

   ![Sök efter användare](/help/journey-onboarding/assets/get-started3.png)

1. Om allt fungerar som det ska kommer sökningen att returnera din post. Om värdet i kolumnen **ADMIN ROLE** visar **System** vet du att du (eller den användare som visas) är systemadministratör.

   ![Systemstatus](/help/journey-onboarding/assets/get-started4.png)

Grattis, systemadministratör!

## Adobe Identity Management System {#ims}

AEM as a Cloud Service levereras förkonfigurerat med Adobe Identity Management System (kallas även IMS) för autentisering. Det finns inget du behöver göra som systemadministratör för att aktivera detta.

Genom att använda IMS konsoliderar AEM as a Cloud Service inloggningsupplevelsen mellan AEM och resten av Adobe Experience Cloud. Organisationer som har flera Adobe-produkter har särskilt nytta av att skapa rollbaserade grupper i Admin Console och sedan tilldela åtkomst till flera produkter, inklusive AEM as a Cloud Service via IMS.

Du lär dig mer om produktprofiler och hur du tilldelar användare i nästa del av den här introduktionsresan.

## Kontakta supporten för Adobe {#support}

Om du har problem kan du få åtkomst till Adobe support via Admin Console. På fliken **Support** kan du komma åt olika supportfunktioner på Adobe via ett enkelt och lättanvänt gränssnitt.

![Fliken Support](/help/journey-onboarding/assets/support-menu.png)

På fliken kan du skapa och hantera ärenden, chatta direkt med Adobe kundsupportrepresentanter och schemalägga sessioner med experter. Systemadministratörer och supportadministratörer måste logga in för att få tillgång till supportärenden och alternativ för expertsessioner.

## What&#39;s Next {#whats-next}

Nu när du har läst det här dokumentet bör du:

* Förstå vad och vad Adobe ID är.
* Du kan logga in på Admin Console.
* Lär dig hur du granskar dina behörigheter som systemadministratör via Admin Console.
* Ta reda på hur du kontaktar supporten för Adobe om du behöver hjälp.

Du kan fortsätta din introduktionsresa genom att lära dig hur du [tilldelar teammedlemmar till Cloud Manager produktprofiler](assign-profiles-cloud-manager.md) så att dina kollegor även kan komma åt AEMaaCS.

## Ytterligare resurser {#additional-resources}

Här följer ytterligare, valfria resurser om du vill gå längre än vad som ingår i introduktionsresan.

* [Översikt över Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html) - En omfattande översikt över Admin Console
* [Skapa eller uppdatera din Adobe ID](https://helpx.adobe.com/ca/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID) - Lär dig hur du skapar en Adobe ID, ändrar den och hanterar flera Adobe-ID:n.
* [SAML 2.0-autentiseringshanterare](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html) - AEM levereras med en SAML-autentiseringshanterare. Hanteraren har stöd för SAML 2.0 Authentication Request Protocol (Web-SSO-profil) med HTTP-POST-bindning.
* [Administrativa roller](https://helpx.adobe.com/enterprise/using/admin-roles.ug.html) - Med Adobe Admin Console kan organisationer definiera en flexibel administrativ hierarki som möjliggör detaljerad hantering av åtkomst och användning av Adobe-produkter.
* [Support- och expertsessioner](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) - Lär dig hur du kommer åt supportalternativen på Admin Console, hanterar dina supportärenden, schemalägger en expertsession och mycket annat.
