---
title: Assets Prime
description: Läs mer om viktiga aspekter av Assets Prime, t.ex. viktiga fördelar, användartyper och behörigheter.
feature: Asset Management
role: User, Admin
exl-id: 012f94c5-b1c3-4799-8eaf-af68d06c036f
source-git-commit: 92faabc50ce4b83ad1015bbbadeac416d66c3b0b
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 0%

---

# [!DNL Assets] as a Cloud Service Prime  {#assets-prime}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![AEM Assets Prime banner image](/help/assets/assets/aem-assets-prime-package-banner.png)

Assets as a Cloud Service Prime innehåller ett lättviktigt DAM som gör att du kan utföra olika viktiga funktioner, som:

* **Resurshantering och bibliotekstjänster** &#x200B;: Verktyg som gör det möjligt för användare att importera, lagra, katalogisera, styra, hantera och styra ett varumärkes digitala resurser i ett centralt arkiv

* **Sök, identifiera och Collaboration**: Verktyg som gör att användare kan bläddra bland, upptäcka, dela och samarbeta med resurser som de behöver för att skapa avancerade kundupplevelser.

* **Säkerhet och Rights Management**: Verktyg för att hantera åtkomst, behörigheter, rättigheter och säkerhet för att säkerställa regelefterlevnad, konsekvens och varumärkesintegritet.

* **Creative Cloud Connections**: Verktyg som gör att marknadsförings- och kreativa team kan samarbeta med enklare åtkomst, kommentarer, granskningar och anteckningar för att uppdatera eller slutföra digitala resurser.

* **Experience Cloud-anslutningar**: Verktyg som stöder inbyggd åtkomst till digitala resurser från andra program och tjänster från Experience Cloud.

* **Distribution Portal Experience utan utökningsalternativ (Content Hub)**: Verktyg för att utöka åtkomsten till ett varumärkes godkända digitala resurser till utökade intressenter för att säkerställa enhetlig användning och varumärke.

* **Integrationer**: integreringar med andra program från Adobe och andra program än Adobe.

* **Dynamic Media (tillägg)**: Verktyg för att omvandla och leverera bilder, videor och annat framväxande innehåll för interaktiva multimedieupplevelser för alla typer av enheter i stor skala.

  >[!NOTE]
  >
  >Dynamic Media med OpenAPI-funktioner, som ger dig tillgång till grundläggande bildmodifieringar som rotering, beskärning (endast manuellt - ingen smart beskärning), vändning, storlek, preferwebp, höjd, bredd, kvalitet, format och adaptiv videoströmning, finns också i Assets Prime. Kontakta Adobe kontoteam för mer information.

1. [Skapa ett nytt program](/help/journey-onboarding/create-program.md).

I takt med att DAM-behoven växer och du behöver fler funktioner, som UI-utökningsmöjligheter, API-driven automatisering och anpassad koddistribution, måste du överväga att uppgradera till [Assets Ultimate](/help/assets/assets-ultimate-overview.md).

Den här artikeln innehåller ett komplett arbetsflöde för att aktivera Assets as a Cloud Service Prime.

## Aktivera Assets as a Cloud Service Prime{#enable-assets-prime}

Aktivera Assets Prime när du skapar ett nytt program med Cloud Manager. Utför följande steg:

1. Logga in på Cloud Manager som systemadministratör. Se till att du väljer rätt organisation när du loggar in.

   >[!NOTE]
   >
   >Se till att du har lagts till i rätt Cloud Manager-produktprofil för att lägga till ett nytt program. Mer information finns i [Rollbaserade behörigheter i Cloud Manager](/help/onboarding/cloud-manager-introduction.md#role-based-permissions).

1. [Skapa ett nytt program](/help/journey-onboarding/create-program.md).

   Välj **[!UICONTROL Assets Prime]** på fliken **[!UICONTROL Solutions & Add-ons]** när du skapar det nya programmet. Du kan också expandera **[!UICONTROL Assets Prime]** och välja **[!UICONTROL Content Hub]** för att aktivera [Content Hub](/help/assets/product-overview.md) för resursdistribution.

   ![AEM Assets Ultimate](assets/aem-assets-prime.png)


1. Klicka på **[!UICONTROL Create]** för att skapa programmet.

1. Klicka på programkortet och klicka på **[!UICONTROL Add Environment]**.

1. Ange miljönamnet, definiera en region och klicka på **[!UICONTROL Save]** för att skapa miljön.

   ![Lägg till miljö i Assets Prime](assets/aem-assets-prime-add-environment.png)

>[!NOTE]
>
>Med Assets Prime kan du bara skapa en produktionsmiljö. Alternativet Lägg till miljö är inte längre tillgängligt när produktionsmiljön har skapats.

Assets Prime är nu aktiverat för Experience Manager Assets as a Cloud Service.

![AEM Assets Prime är tillgängligt](assets/aem-assets-prime-setup-complete.png)

Systemadministratören får automatiskt AEM som administratör och får ett e-postmeddelande om att gå till Admin Console för att hantera produktprofiler.


Din AEM as a Cloud Service-instans på Admin Console innehåller följande produktprofiler:

* AEM administratörer

* AEM

* [Användare av AEM Assets Collaborator](#onboard-collaborator-users)

* [AEM Assets Power Users](#onboard-power-users)


![AEM Assets produktprofiler](assets/aem-assets-product-profiles.png)

Du kan börja lägga till användare eller användargrupper i produktprofilerna för AEM Assets Collaborator Users och AEM Assets Power Users. Mer information finns i [Anlita användare av AEM Assets Collaborator](#onboard-collaborator-users) och [Anlita AEM Assets Power-användare](#onboard-power-users).

Om du har aktiverat Content Hub för Assets as a Cloud Service skapas en ny instans i AEM Assets as a Cloud Service Admin Console med `delivery` som suffix:

![Ny instans för Content Hub](assets/new-instance-content-hub.png)

>[!NOTE]
>
>Om du har etablerat Content Hub före 14 augusti 2024 skapas den nya instansen med `contenthub` som suffix.

Observera att det inte finns någon `author` eller `publish` i instansnamnet för Content Hub.

Klicka på instansnamnet för att visa Content Hub-produktprofilen för `AEM Assets Limited Users`.

![Content Hub produktprofil](assets/content-hub-product-profile.png)

Du kan börja lägga till användare eller användargrupper i den här produktprofilen för att ge dem tillgång till Content Hub.

>[!NOTE]
>
>Om du har etablerat Content Hub före den 14 augusti 2024 har Content Hub produktprofil `contenthub` omnämns efter `Limited Users` i stället för `delivery`.

## Anlita användare av AEM Assets Collaborator {#onboard-collaborator-users}

AEM Assets Collaborator-användare kan arbeta med resurser från Experience Manager via integreringar av Assets som är tillgängliga för din organisation i andra Adobe-produkter och andra program än Adobe, skapa och redigera resurser med inbyggd Adobe Express och Firefly genom att utnyttja professionellt utformade mallar, märkeskit, Adobe Stock-resurser och så vidare, och få tillgång till och utnyttja godkända resurser från din organisation via AEM Assets Content Hub portal.

Anlita medarbetare:

1. Gå till Experience Manager Assets produktprofiler genom att klicka på AEM as a Cloud Service produktnamn i produktlistan på Admin Console.

1. Klicka på författarinstansen för AEM as a Cloud Service:
   ![Produktprofiler för AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

1. Klicka på produktprofilen för medarbetare och klicka på **[!UICONTROL Add users]** för att lägga till användaren i produktprofilen.
   ![Användarproduktprofil](assets/aem-assets-collaborator-user-permissions.png)

1. Klicka på **[!UICONTROL Save]** om du vill spara ändringarna.

Du kan även komma åt och visa de tjänster som tilldelats till Collaborator-användare, vilket visas i följande bild:

![Tjänster för samarbetspartners](assets/aem-assets-collaborator-users.png)

`Adobe Express` och `AEM Assets Collaborator Users` tjänster är aktiverade som standard. Du kan stänga av och sätta på enligt dina önskemål, men Adobe rekommenderar att du använder standardtjänsterna som är aktiverade för produktprofilerna.

## Införliva AEM Assets Power-användare {#onboard-power-users}

AEM Assets Power-användare har tillgång till alla AEM Assets-funktioner, inklusive hantering av resurser, behörigheter, metadata och övergripande styrning och automatisering av digitala resurser, kan arbeta med resurser från Experience Manager via integreringar av Assets som är tillgängliga för din organisation i andra Adobe- och icke-Adobe-program, skapa och redigera resurser med hjälp av inbyggd Adobe Express och Firefly, och utnyttja professionellt utformade mallar, varumärkeskit, Adobe Stock-resurser och så vidare, samt få tillgång till och utnyttja godkända resurser från din organisation via Content Hub portal.

Så här skaffar du Power-användare:

1. Gå till Experience Manager Assets produktprofiler genom att klicka på AEM as a Cloud Service produktnamn i produktlistan på Admin Console.

1. Klicka på författarinstansen för AEM as a Cloud Service:
   ![Produktprofiler för AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

1. Klicka på Power users produktprofil och klicka på **[!UICONTROL Add users]** för att lägga till användaren i produktprofilen.
   ![Användarproduktprofil](assets/aem-assets-power-user-permissions.png)

1. Klicka på **[!UICONTROL Save]** om du vill spara ändringarna.

Du kan även få åtkomst till och visa de tjänster som tilldelats till Power-användare, enligt bilden nedan:

![Tjänster för avancerade användare](assets/aem-assets-power-users.png)

`Adobe Express` och `AEM Assets Power Users` tjänster är aktiverade som standard. Du kan stänga av och sätta på enligt dina önskemål, men Adobe rekommenderar att du använder standardtjänsterna som är aktiverade för produktprofilerna.
