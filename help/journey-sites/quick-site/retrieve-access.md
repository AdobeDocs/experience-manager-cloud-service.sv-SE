---
title: Hämta Git-databasåtkomstinformation
description: Läs om hur frontendutvecklaren använder Cloud Manager för att få åtkomst till Git-databasinformation.
exl-id: 3ef1cf86-6da4-4c09-9cfc-acafc8f6dd5c
solution: Experience Manager Sites
feature: Developing
role: Admin, Developer
recommendations: display, noCatalog
source-git-commit: 0a458616afad836efae27e67dbe145fc44bee968
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 3%

---


# Hämta Git-databasåtkomstinformation {#retrieve-access}

{{traditional-aem}}

Läs om hur frontendutvecklaren använder Cloud Manager för att få åtkomst till Git-databasinformation.

## Story hittills {#story-so-far}

Om du är en frontendutvecklare som bara ansvarar för anpassning av webbplatstemat behöver du inte veta hur AEM har konfigurerats och kan hoppa till avsnittet [Mål](#objective) i det här dokumentet.

Om du även är Cloud Manager- eller AEM-administratör och gränssnittsutvecklare lärde du dig i det tidigare dokumentet under AEM snabbwebbplats Skapa-resan, [Bevilja åtkomst till frontendutvecklaren](grant-access.md), hur du kan ta med frontutvecklaren så att de har tillgång till Git-databasen, och du bör nu veta:

* Så här lägger du till en frontendutvecklare som användare.
* Så här tilldelar du de roller som krävs till frontendutvecklaren.

I den här artikeln beskrivs hur frontendutvecklaren använder Cloud Manager-åtkomst för att hämta inloggningsuppgifter för åtkomst till AEM Git-databasen.

Nu när det finns en webbplats som är baserad på en mall, där det finns en pipeline-konfiguration, där frontendutvecklaren är inbäddad och har all information de behöver, flyttar den här artikeln perspektiv från administratörer och enbart till frontendutvecklarrollen.

## Syfte {#objective}

I det här dokumentet beskrivs hur du, i rollen som frontendutvecklare, kan få åtkomst till Cloud Manager och hämta inloggningsuppgifter till AEM Git-databasen. När du har läst

* Lär dig mer om vad Cloud Manager är.
* Har hämtat dina inloggningsuppgifter för att få tillgång till AEM Git så att du kan implementera dina anpassningar.

## Ansvarig roll {#responsible-role}

Den här delen av resan gäller för den som utvecklar gränssnittet.

## Krav {#requirements}

Med verktyget för att skapa snabbwebbplatser kan gränssnittsutvecklare arbeta självständigt utan kunskap om AEM eller hur det är konfigurerat. Cloud Manager-administratören måste dock ta in den som utvecklar projektet i projektteamet och AEM-administratören måste ge dig viss nödvändig information. Kontrollera att du har följande information innan du fortsätter.

* Från AEM-administratören:
   * Temakällfiler som ska anpassas
   * Sökväg till en exempelsida som ska användas som referensbas
   * Proxy user credentials to test your customization to live AEM content
   * Krav på utformning av gränssnittet
* Från Cloud Manager-administratören:
   * Ett välkomstmeddelande från Cloud Manager som informerar dig om att du har tillgång till
   * Namnet på programmet eller URL:en till det inom Cloud Manager

Om du saknar något av dessa objekt kontaktar du AEM-administratören eller Cloud Manager-administratören.

Man utgår ifrån att den som utvecklar främst har stor erfarenhet av arbetsflöden för utveckling och gemensamma verktyg som installeras:

* git
* npm
* webbpaket
* En önskad redigerare

## Förstå Cloud Manager {#understanding-cloud-manager}

Med Cloud Manager kan företag hantera AEM själva i molnet. Det innehåller ett ramverk för kontinuerlig integrering och kontinuerligt leverans (CI/CD) som gör att IT-team och implementeringspartners kan snabba upp leveransen av anpassningar eller uppdateringar utan att kompromissa med prestanda eller säkerhet.

För frontutvecklaren är det själva gatewayen att

* Få åtkomst till AEM Git-databasinformation så att du kan implementera dina anpassningar för frontend.
* Starta distributionsflödet för att distribuera dina anpassningar.

Cloud Manager-administratören har utsett dig till Cloud Manager-användare. Du bör ha fått ett välkomstmeddelande som liknar det här.

![Välkomstmeddelande](assets/welcome-email.png)

Kontakta Cloud Manager-administratören om du inte har fått det här e-postmeddelandet.

## Använd Cloud Manager {#access-cloud-manager}

1. Logga in på Adobe Experience Cloud på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) eller klicka på länken i välkomstmeddelandet.

1. Cloud Manager listar de olika program som är tillgängliga. Markera den som du behöver ha tillgång till enligt Cloud Manager-administratörens anvisningar. Om detta är ditt första front end-projekt för AEMaaCS har du troligen bara ett program tillgängligt.

   ![Välja ett program i Cloud Manager](assets/cloud-manager-select-program.png)

Nu visas en översikt över programmet. Sidan ser annorlunda ut men liknar det här exemplet.

![Cloud Manager - översikt](assets/cloud-manager-overview.png)

## Hämta information om databasåtkomst {#repo-access}

1. Markera **Åtkomst till upprepningsinformation** i delen **Förgreningar** på Cloud Manager-sidan.

   ![Rörledningar](assets/pipelines-repo-info.png)

1. Dialogrutan **Databasinformation** öppnas.

   ![Repo info](assets/repo-info.png)

1. Välj knappen **Skapa lösenord** för att skapa ett lösenord för dig själv.

1. Spara lösenordet som genererats i en säker lösenordshanterare. Lösenordet visas aldrig igen.

1. Kopiera även fälten **användarnamn** och **Git-kommandorad**. Du kommer att använda den här informationen senare för att komma åt rapporten.

1. Välj **Stäng**.

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av AEM snabbwebbplats bör du:

* Lär dig mer om vad Cloud Manager är.
* Har hämtat dina inloggningsuppgifter för att få tillgång till AEM Git så att du kan implementera dina anpassningar.

Bygg vidare på den här kunskapen och fortsätt din resa till AEM Quick Site Creation genom att gå igenom dokumentet [Anpassa webbplatstemat](customize-theme.md) där du får lära dig hur webbplatstemat byggs, hur du anpassar och hur du testar med AEM-innehåll.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av snabbwebbplatsskapandeprocessen genom att granska dokumentet [Anpassa webbplatstemat](customize-theme.md), men följande är ytterligare, valfria resurser som gör en djupdykning i vissa koncept som nämns i det här dokumentet, men de behöver inte fortsätta på resan.

* [Adobe Experience Manager Cloud Manager Documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) - Utforska Cloud Manager-dokumentationen och få fullständig information om dess funktioner.
