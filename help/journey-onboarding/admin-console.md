---
title: Öppna Admin Console
description: När du har förstått de förberedelser som krävs för att komma igång och grunderna i AEM as a Cloud Service struktur är du redo att logga in på Admin Console för första gången.
exl-id: 0ccce328-a356-4ba9-b7fe-f67abc25b924
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 8ed13eb6f476bab07da07549a83ab9ac16bdea72
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 0%

---

# Öppna Admin Console {#accessing-admin-console}

I den här delen av [introduktionsresan](overview.md) får du lära dig om de förberedelser som krävs innan du kan logga in i systemet för första gången.

## Syfte {#objective}

Nu när du har läst artikeln [AEM as a Cloud Service Terminology](terminology.md) och förstått grunderna i AEMaaCS-strukturen är du redo att logga in på Admin Console för första gången!

Som systemadministratör ansvarar du för att hantera användare i din organisation med Admin Console. När du har läst det här avsnittet bör du kunna göra följande:

* Förstå vad en Adobe ID är.
* Du kan logga in på Admin Console.
* Lär dig hur du granskar dina behörigheter som systemadministratör via Admin Console.
* Se hur du kontaktar Adobe support.

## Om Admin Console {#admin-console}

Adobe Admin Console är en central plats för att administrera och hantera Adobe produktlicenser och användare. Med Admin Console kan du skapa och hantera användare på en och samma plats i stället för i olika individuella lösningar.

### Adobe ID {#adobe-id}

För att kunna logga in på Admin Console behöver du en Adobe ID. Ett Adobe ID är ett konto som är knutet till en viss e-postadress som krävs för att logga in och få tillgång till AEM as a Cloud Service eller någon av dina Adobe-lösningar. Genom att använda din Adobe ID behåller du alla dina Adobe-planer och -produkter som är kopplade till ett enda konto.

När du som systemadministratör konfigurerar ditt team i Admin Console anger du den e-postadress som ska användas som Adobe ID.

Det finns tre typer av Adobe ID:

* **Personligt ID**: Standardtypen för Adobe ID och skapas på adobe.com. Hanteras av Adobe och vem som helst kan skapa ett konto av den här typen.

* **Enterprise ID**: Organisationer vill vanligtvis få bättre kontroll över användarnas konton. Endast systemadministratörer kan skapa Enterprise ID:n och organisationen äger dessa konton med Adobe som endast fungerar som värd.

* **Federated ID**: Med federerade ID:n får organisationen full äganderätt och kontroll över kontona. Din organisation måste integrera Adobe Experience Cloud med ditt SAML2 SSO-system (single sign-on). På så sätt kan användare autentisera mot sin organisations SSO-system i stället för mot ett konto som finns hos Adobe.

Som systemadministratör kan du ta in dig själv och ditt team hos AEM as a Cloud Service med personliga ID:n. Utför den här uppgiften innan Enterprise ID eller Federated ID finns på plats. När Enterprise ID:n eller Federated ID:n har konfigurerats kan medlemmar övergå till att använda dessa ID:n.

### Logga in direkt på Admin Console {#steps-admin-console}

Innan du kan använda Admin Console för att administrera användare i ditt team måste du se till att du själv har tillgång till den och rätt behörigheter.

1. Som systemadministratör får du flera e-postmeddelanden från Adobe som en del av introduktionsprocessen. Leta efter det välkomstmeddelande som innehåller information om organisationens namn som du har beviljats åtkomst till.

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

1. Om allt fungerar som det ska returneras din post. Om värdet i kolumnen **ADMIN ROLE** visar **System** vet du att du (eller den användare som visas) är systemadministratör.

   ![Systemstatus](/help/journey-onboarding/assets/get-started4.png)

Grattis, systemadministratör!

## Få tillgång till Admin Console via Experience Hub  {#access-admin-console-via-experience-hub}

[Experience Hub](/help/experience-hub.md) är AEM enhetliga och personaliserade hus. Här samlas AEM Tools och Admin Console på ett och samma ställe.

![Admin Console-alternativ som det visas på Experience Hub hemsida](/help/journey-onboarding/assets/experiencehub-adminconsole1.png)

**Så här kommer du åt Admin Console via Experience Hub:**

1. Klicka på [Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home) för att öppna Experience Hub hemsida.

1. Klicka på **Admin Console**&#x200B;[**i grupperingen** Snabbåtkomst](https://experience.adobe.com).

## Adobe Identity Management System {#ims}

AEM as a Cloud Service levereras förkonfigurerat med Adobe Identity Management System (kallas även IMS) för autentisering. Det finns inget som du behöver göra som systemadministratör för att aktivera den här funktionen.

Genom att använda IMS konsoliderar AEM as a Cloud Service inloggningsupplevelsen mellan AEM och övriga Adobe Experience Cloud. Organisationer med många Adobe-produkter får det mesta. Skapa rollbaserade grupper i Admin Console och ge produktåtkomst via IMS, till exempel AEM as a Cloud Service.

Du lär dig mer om produktprofiler och hur du tilldelar användare i nästa del av den här introduktionsresan.

## Kontakta Adobe support {#support}

Om du har problem kan du få åtkomst till Adobe support via Admin Console. På fliken **Support** kan du få åtkomst till olika supportfunktioner i Adobe via ett enkelt och lättanvänt gränssnitt.

![Fliken Support](/help/journey-onboarding/assets/support-menu.png)

På fliken kan du skapa och hantera ärenden, chatta direkt med Adobe kundsupportrepresentanter och schemalägga sessioner med experter. Systemadministratörer och supportadministratörer måste logga in för att få tillgång till supportärenden och alternativ för expertsessioner.

## Vad kommer härnäst? {#whats-next}

Nu när du har läst det här dokumentet bör du:

* Förstå vad och vad Adobe ID är.
* Du kan logga in på Admin Console.
* Lär dig hur du granskar dina behörigheter som systemadministratör med Admin Console.
* Se hur du kontaktar Adobe support.

Du är redo att fortsätta din introduktionsresa genom att lära dig hur du [tilldelar teammedlemmar till Cloud Manager produktprofiler](assign-profiles-cloud-manager.md) så att dina kollegor även kan komma åt AEMaaCS.

## Ytterligare resurser {#additional-resources}

Här följer ytterligare, valfria resurser om du vill gå längre än vad som ingår i introduktionsresan.

* [Admin Console Overview](https://helpx.adobe.com/enterprise/using/admin-console.html) - en omfattande översikt över Admin Console
* [Skapa eller uppdatera din Adobe ID](https://helpx.adobe.com/ca/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID) - Lär dig hur du skapar en Adobe ID, ändrar den och hanterar flera Adobe ID:n.
* [SAML 2.0-autentiseringshanterare](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/saml-2-0-authenticationhandler#) - AEM levereras med en SAML-autentiseringshanterare. Hanteraren ger stöd för SAML 2.0 Authentication Request Protocol (Web-SSO-profil) med HTTP POST-bindning.
* [Administrativa roller](https://helpx.adobe.com/enterprise/using/admin-roles.html) - Med Adobe Admin Console kan organisationer definiera en flexibel administrativ hierarki som möjliggör detaljerad hantering av åtkomst och användning av Adobe-produkter.
* [Support- och expertsessioner](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.html) - Lär dig hur du kommer åt supportalternativen på Admin Console, hanterar dina supportärenden, schemalägger en expertsession och mycket annat.
