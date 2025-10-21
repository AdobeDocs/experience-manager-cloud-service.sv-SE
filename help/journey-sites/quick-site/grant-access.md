---
title: Bevilja åtkomst till klientutvecklaren
description: Anlita gränssnittsutvecklarna till Cloud Manager så att de får tillgång till AEM webbplats via lagringsplats och pipeline.
exl-id: 58e95c92-b859-4bb9-aa62-7766510486fd
solution: Experience Manager Sites
feature: Developing
role: Admin, Developer
recommendations: display, noCatalog
source-git-commit: 0a458616afad836efae27e67dbe145fc44bee968
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---


# Bevilja åtkomst till klientutvecklaren {#grant-fed-access}

{{traditional-aem}}

Anlita gränssnittsutvecklarna till Cloud Manager så att de får tillgång till AEM webbplats via lagringsplats och pipeline.

## Story hittills {#story-so-far}

I det föregående dokumentet för AEM snabbplatsskapanderesa, [Konfigurera din pipeline](pipeline-setup.md), lärde du dig att skapa en frontendpipeline för att hantera anpassningen av webbplatsens tema, och du bör nu:

* Förstå vad en rörledning är.
* Ta reda på hur man lägger upp en rörledning i Cloud Manager.

Nu måste du ge frontendutvecklare åtkomst till Cloud Manager via introduktionsprocessen så att frontendutvecklaren kan komma åt AEM Git-databasen och den pipeline du har skapat.

## Syfte {#objective}

Processen att bevilja åtkomst till Cloud Manager och tilldela användarroller till dina användare kallas för introduktion. Det här dokumentet ger en översikt över de viktigaste stegen för att introducera en frontendutvecklare och när du har läst det kommer du att få veta:

* Så här lägger du till en frontendutvecklare som användare.
* Så här tilldelar du de roller som krävs till frontendutvecklaren.

>[!TIP]
>
>Det finns en hel dokumentationsresa som är dedikerad till att introducera ditt team på AEM som en molntjänst, länkad till i [avsnittet Ytterligare resurser](#additional-resources) i det här dokumentet, om du behöver mer information om processen.

## Ansvarig roll {#responsible-role}

Den här delen av resan gäller Cloud Manager-administratören.

## Krav {#requirements}

* Du måste vara medlem i rollen **Affärsägare** i Cloud Manager.
* Du måste vara **systemadministratör** i Cloud Manager.
* Du måste ha tillgång till Admin Console.

## Lägg till frontendutvecklaren som användare {#add-fed-user}

Först måste du lägga till frontutvecklaren som användare med Admin Console.

1. Logga in på Admin Console på [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/).

1. När du har loggat in visas en översiktssida som liknar följande bild.

   ![Admin Console - översikt](assets/admin-console.png)

1. Kontrollera att du är i rätt organisation genom att kontrollera organisationsnamnet i skärmens övre högra hörn.

   ![Kontrollera organisationsnamn](assets/correct-org.png)

1. Välj **Adobe Experience Manager as a Cloud Service** från kortet **Produkter och tjänster**.

   ![Välj AEMaaCS](assets/select-aemaacs.png)

1. Du ser en lista över förkonfigurerade Cloud Manager-produktprofiler. Om du inte ser de här profilerna kontaktar du Cloud Manager-administratören eftersom du kanske inte har rätt behörighet i din organisation.

   ![Produktprofiler](assets/product-profiles.png)

1. Om du vill tilldela frontend-utvecklaren rätt profiler väljer du fliken **Användare** och sedan knappen **Lägg till användare** .

   ![Lägg till användare](assets/add-user.png)

1. I dialogrutan **Lägg till användare i ditt team** skriver du e-post-ID:t för den användare som du vill lägga till. För ID-typ väljer du Adobe ID om Federated ID för dina teammedlemmar inte har konfigurerats ännu.

   ![Lägg till användare i team](assets/add-to-team.png)

1. Markera plustecknet i **Produkt** och välj sedan **Adobe Experience Manager as a Cloud Service** och tilldela produktprofilerna **Distributionshanteraren** och **Utvecklare** till användaren.

   ![Tilldela teamprofiler](assets/assign-team.png)

1. Välj **Spara** och ett välkomstmeddelande skickas till den frontendutvecklare som du har lagt till som användare.

Den inbjudna frontendutvecklaren kan komma åt Cloud Manager genom att klicka på länken i välkomstmeddelandet och logga in med sin Adobe ID.

## Lämna över till front-end Developer {#handover}

Med en e-postinbjudan till Cloud Manager på vägen till den som utvecklar gränssnittet kan du och AEM-administratören nu ge den som utvecklar gränssnittet den information som behövs för att anpassa produkten.

* En [sökväg till typiskt innehåll](#example-page)
* Temakällan som [du hämtade](#download-theme)
* Autentiseringsuppgifterna för [proxyanvändaren](#proxy-user)
* Namnet på programmet eller URL:en till det [som har kopierats från Cloud Manager](pipeline-setup.md#login)
* Designkrav för framsidan

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av AEM Quick Site Creation bör du känna till:

* Så här lägger du till en frontendutvecklare som användare.
* Så här tilldelar du de roller som krävs till frontendutvecklaren.

Bygg vidare på den här kunskapen och fortsätt din resa till AEM Quick Site Creation genom att nästa gång läsa dokumentet [Hämta information om Git-databasåtkomst](retrieve-access.md) , som endast ändrar perspektiv för den som utvecklar gränssnittet och förklarar hur den som utvecklar gränssnittet Cloud Manager får åtkomst till Git-databasinformation.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av processen för att skapa snabbwebbplats genom att granska dokumentet [Hämta användarautentiseringsuppgifter för frontendutvecklare](retrieve-access.md), men följande är ytterligare, valfria resurser som gör en djupdykning i vissa koncept som nämns i det här dokumentet, men de behöver inte fortsätta på resan.

* [Onboarding Journey](/help/journey-onboarding/overview.md) - Den här guiden fungerar som en startpunkt för att säkerställa att dina team har konfigurerats och tillgång till AEM as a Cloud Service.
