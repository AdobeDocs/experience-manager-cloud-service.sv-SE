---
title: Använd mediebiblioteket för grundläggande hantering av digitala resurser
description: '[!DNL Experience Manager Assets] och mediebibliotek för resurshantering.'
contentOwner: AG
feature: Asset Management, Publishing
role: User, Architect, Leader
exl-id: 4737d5ee-9a93-49f3-9f20-d4368e60e9fb
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# Använd mediebibliotek för grundläggande resurshantering {#manage-assets-using-media-library}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/medialibrary.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |

Plattformen [!DNL Adobe Experience Manager] har olika funktioner för att hantera resurser. Med mediebiblioteket kan användarna överföra ett litet antal resurser till databasen, söka efter och använda dem på webbsidorna och utföra enkla resurshanteringsåtgärder på resurserna.

Mediebiblioteket är en enkel DAM-lösning (Digital Asset Management) som medföljer licensen [!DNL Adobe Experience Manager Sites]. [!DNL Sites] är ett WCM-erbjudande (Web Content Management). Media Library fungerar med alla funktioner i Experience Manager.

[!DNL Adobe Experience Manager Assets]-licensen är tillgänglig separat för inköp. I [!DNL Experience Manager Assets] kan du hantera resurser på ett robust sätt via användningsexempel, anpassningar av metadata, scheman, sökning och användargränssnitt samt många andra funktioner utöver vad som finns i Media Library.

## Licenskrav {#avail-media-library-license}

Kunder som har [!DNL Sites] licens har rätt att använda mediebiblioteket. Det fungerar med alla komponenter i [!DNL Experience Manager].

Mediebiblioteket installeras som en del av Sites. Ingen ytterligare licens eller paket krävs utöver Sites-licens och -installation.

## [!DNL Assets] jämfört med mediebibliotek {#assets-and-media-library}

Experience Manager Assets tillhandahåller DAM-funktionalitet i enterpriseklass. Assets-funktionaliteten levereras med [!DNL Experience Manager] i ett enda paket. Användare som inte har köpt någon Assets-licens har dock inte rätt att använda de avancerade DAM-funktionerna. Utan Assets-licens är endast [mediebiblioteksfunktioner](#use-media-library) tillgängliga.

Om du vill förhindra oavsiktlig användning av [!DNL Assets]-funktioner som du inte har licensierat tar du bort alla [!DNL Assets]-specifika arbetsflöden, komponenter, taxonomier, alternativ och [!DNL Assets]-administratören från [!DNL Experience Manager]. På så sätt förhindras användarna från att oavsiktligt använda [!DNL Assets]-funktioner som du inte har licensierat.

## Använd mediebibliotek {#use-media-library}

Mediebiblioteket omfattar i stort sett följande användningsområden:

* Tillhandahåll grundläggande DAM-funktioner för webbsidor som skapats med [!DNL Adobe Experience Manager Sites].
* Anpassningsbara formulär och kommunikation som skapats med [!DNL Adobe Experience Manager Forms].
* Digitala skärmupplevelser som skapats med [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] HTTP REST API:er för headless-åtgärder.

<!-- TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.

* Static renditions

-->

Om du vill använda funktionerna i mediebiblioteket kan du använda standardanvändargränssnittet för [!DNL Experience Manager]. Mediebiblioteket ingår i installationen av [!DNL Experience Manager Sites] och inget separat gränssnitt eller tillägg krävs. Med det befintliga gränssnittet har mediebiblioteksanvändare rätt att utföra följande uppgifter:

* Skapa mappar för att ordna resurser.
* Överför resurser.
* Publicera resurser.
* Redigera, flytta och kopiera resurser.
* Bläddra bland, filtrera och söka (inklusive likhetssökning) resurser.
* Lägg till värden i och redigera värdena i metadatafälten, förutom fältet Smarta taggar, som är tillgängliga på fliken [!UICONTROL Basic] på en resurs [!UICONTROL Properties] -sida som standard.
* Lägg till och ta bort statiska återgivningar.
* Hämta mappar, resurser och resursrenderingar.
* Skapa resursversioner.
* Skapa och utför granskningsåtgärder på resurser.
* Anteckna resurser.
* Lägg till resurser på [!DNL Sites] sidor via Content Finder.
* Använd [!DNL Content Fragments].
* Använd HTTP REST och GraphQL API:er för [!DNL Content Fragments] och refererade medieresurser, under Sites-licens.
* Integrering med Marketing Cloud.
* Anpassa och utöka gränssnittet för resurshantering.
* Gå till Query Builder (API) för att utöka sökfunktionen.
* Skapa statiska taggar.
* Skapa projekt och uppgifter.
* Activity stream (timeline).
* Kommentarer och kommentarer.

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we do not have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>Många avancerade DAM-användningsfall uppfylls av [!DNL Experience Manager Assets]. Licensen för mediebibliotek berättigar dig att endast fylla i de angivna användningsområdena med hjälp av mediebiblioteket. Om ett användningsexempel inte finns med i listan ska du inte använda det med mediebibliotekslicensen. Kontakta kundsupport om du har frågor.

Du kan inte använda smarta taggar, [!DNL Asset]-länk, [!DNL Asset]-väljare, bulktaggning, ändra resursarbetsflöden eller standardanvändargränssnittet för [!DNL Adobe Experience Manager] för att komma åt mediebiblioteket utan [!DNL Assets] licens.

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publicera Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [DAM-funktioner i [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/home.html?lang=sv-SE)
>* [[!DNL Experience Manager] som en [!DNL Cloud Service] produktbeskrivning](https://helpx.adobe.com/se/legal/product-descriptions/adobe-experience-manager-cloud-service.html)
