---
title: Använd mediebiblioteket för grundläggande digital resurshantering
description: '[!DNL Experience Manager Assets] och mediebibliotek för resurshantering.'
contentOwner: AG
feature: Asset Management,Publishing
role: Business Practitioner,Architect,Leader
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# Använd mediebiblioteket för grundläggande resurshantering {#manage-assets-using-media-library}

[!DNL Adobe Experience Manager] -plattformen har olika funktioner för att hantera resurser. Med mediebiblioteket kan användarna överföra ett litet antal resurser till databasen, söka efter och använda dem på webbsidorna och utföra enkla resurshanteringsåtgärder på resurserna.

Mediebiblioteket är en enkel DAM-lösning (Digital Asset Management) som medföljer [!DNL Adobe Experience Manager Sites]-licensen. [!DNL Sites] är ett web content management-erbjudande. Mediebiblioteket fungerar med alla funktioner i Experience Manager.

[!DNL Adobe Experience Manager Assets] kan köpas separat. [!DNL Experience Manager Assets] möjliggör robust hantering av resurser via användningsfall för företag, anpassningar av metadata, scheman, sökning och användargränssnitt samt många andra funktioner utöver vad Media Library erbjuder.

## Licenskrav {#avail-media-library-license}

Kunder som har [!DNL Sites] licens har rätt att använda mediebiblioteket. Det fungerar med alla komponenter i [!DNL Experience Manager].

Mediebiblioteket installeras som en del av Sites. Ingen ytterligare licens eller paket krävs utöver Sites-licens och -installation.

## [!DNL Assets] kontra mediebibliotek  {#assets-and-media-library}

Experience Manager Assets har funktioner för företagsövergripande resurshantering (DAM). Resursfunktionaliteten levereras med [!DNL Experience Manager] i ett enda paket. Användare som inte har köpt en Assets-licens har dock inte rätt att använda de avancerade DAM-funktionerna. Utan resurslicens är endast [funktioner i mediebiblioteket](#use-media-library) tillgängliga.

Om du vill förhindra oavsiktlig användning av [!DNL Assets]-funktioner som du inte har licensierat tar du bort alla [!DNL Assets]-specifika arbetsflöden, komponenter, taxonomier, alternativ och [!DNL Assets]-administratören från [!DNL Experience Manager]. På så sätt förhindras användarna från att oavsiktligt använda [!DNL Assets]-funktioner som du inte har licensierat.

## Använd mediebibliotek {#use-media-library}

Mediebiblioteket omfattar i stort sett följande användningsområden:

* Tillhandahåll grundläggande DAM-funktioner för webbsidor som skapats med [!DNL Adobe Experience Manager Sites].
* Anpassningsbara formulär och kommunikation som skapats med [!DNL Adobe Experience Manager Forms].
* Digitala skärmupplevelser som skapats med [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] HTTP REST API:er för headless-åtgärder.

<!-- TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.

* Basic metadata properties
* Tag management
* Version control
* Static renditions
* Projects, tasks, workflow authoring
* Activity stream (timeline)
* Query Builder (API)
* Marketing Cloud integration
* User interface customization and extension
* Comments and annotation
-->

Om du vill använda funktionerna i mediebiblioteket kan du använda standardanvändargränssnittet för [!DNL Experience Manager]. Mediebiblioteket ingår i [!DNL Experience Manager Sites]-installationen och inget separat gränssnitt eller tillägg krävs. Med det befintliga gränssnittet har mediebiblioteksanvändare rätt att utföra följande uppgifter:

* Skapa mappar för att ordna resurser.
* Överför resurser.
* Publicera resurser.
* Redigera, flytta och kopiera resurser.
* Bläddra bland, filtrera och söka (inklusive likhetssökning) resurser.
* Lägg till värden i och redigera värdena i metadatafälten, förutom fältet Smarta taggar, som är tillgängliga på fliken [!UICONTROL Basic] på en resurs [!UICONTROL Properties]-sida som standard.
* Lägg till och ta bort statiska återgivningar.
* Hämta mappar, resurser och resursrenderingar.
* Skapa resursversioner.
* Skapa och utför granskningsåtgärder på resurser.
* Anteckna resurser.
* Lägg till resurser på [!DNL Sites]-sidor via Content Finder.
* Använd [!DNL Content Fragments].

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?
-->

>[!IMPORTANT]
>
>Många avancerade DAM-användningsfall uppfylls av [!DNL Experience Manager Assets]. Licensen för mediebibliotek berättigar dig att endast fylla i de angivna användningsområdena med hjälp av mediebiblioteket. Om ett användningsexempel inte finns med i listan ska du inte använda det med mediebibliotekslicensen. Kontakta Adobe kundtjänst om du har frågor.

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [DAM-funktioner i [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/home.html)
>* [[!DNL Experience Manager] as a [!DNL Cloud Service] produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-cloud-service.html)

