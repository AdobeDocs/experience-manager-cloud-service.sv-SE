---
title: Använd Media Library för grundläggande hantering av digitala resurser
description: '[!DNL Experience Manager Assets] och Media Library för filhantering.'
contentOwner: AG
feature: Asset Management,Publishing
role: User,Architect,Leader
exl-id: 4737d5ee-9a93-49f3-9f20-d4368e60e9fb
source-git-commit: 51ebeda46fbacb2479a5bd007cb741486caa218f
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# Använd Media Library för grundläggande resurshantering {#manage-assets-using-media-library}

[!DNL Adobe Experience Manager] -plattformen har olika funktioner för att hantera resurser. Med Media Library kan användarna överföra ett litet antal resurser till databasen, söka efter och använda dem på webbsidorna och utföra enkla resurshanteringsåtgärder på resurserna.

Media Library är en lättviktig DAM-lösning (Digital Asset Management) som medföljer [!DNL Adobe Experience Manager Sites]-licensen. [!DNL Sites] är ett web content management-erbjudande. Media Library fungerar med alla funktioner i Experience Manager.

[!DNL Adobe Experience Manager Assets] kan köpas separat. [!DNL Experience Manager Assets] möjliggör robust hantering av resurser via företagsbruk, anpassningar av metadata, scheman, sökning och användargränssnitt samt många andra funktioner utöver vad Media Library erbjuder.

## Licenskrav {#avail-media-library-license}

Kunder som har [!DNL Sites] licens har rätt att använda Media Library. Det fungerar med alla komponenter i [!DNL Experience Manager].

Media Library installeras som en del av Sites. Ingen ytterligare licens eller paket krävs utöver Sites-licens och -installation.

## [!DNL Assets] jämfört med Media Library {#assets-and-media-library}

Experience Manager Assets tillhandahåller DAM-funktioner i enterpriseklass. Resursfunktionaliteten levereras med [!DNL Experience Manager] i ett enda paket. Användare som inte har köpt en Assets-licens har dock inte rätt att använda de avancerade DAM-funktionerna. Utan Assets-licens är endast [Media Library-funktioner](#use-media-library) tillgängliga.

Om du vill förhindra oavsiktlig användning av [!DNL Assets]-funktioner som du inte har licensierat tar du bort alla [!DNL Assets]-specifika arbetsflöden, komponenter, taxonomier, alternativ och [!DNL Assets]-administratören från [!DNL Experience Manager]. På så sätt förhindras användarna från att oavsiktligt använda [!DNL Assets]-funktioner som du inte har licensierat.

## Använd Media Library {#use-media-library}

Media Library omfattar i stort sett följande användningsområden:

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

Om du vill använda Media Library-funktionen kan du använda standardanvändargränssnittet för [!DNL Experience Manager]. Media Library ingår i [!DNL Experience Manager Sites]-installationen och inget separat gränssnitt eller tillägg krävs. Med det befintliga gränssnittet har Media Library-användare rätt att utföra följande uppgifter:

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
>Många avancerade DAM-användningsfall uppfylls av [!DNL Experience Manager Assets]. Media Library-licens berättigar dig att endast fylla i de angivna användningsområdena med Media Library. Om ett användningsexempel inte finns med i listan ska du inte använda det med Media Library-licens. Kontakta Adobe kundtjänst om du har frågor.

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [DAM-funktioner i [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/home.html)
>* [[!DNL Experience Manager] as a [!DNL Cloud Service] produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-cloud-service.html)

