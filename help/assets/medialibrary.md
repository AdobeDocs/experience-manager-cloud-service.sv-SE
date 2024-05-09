---
title: Använd Media Library för grundläggande hantering av digitala resurser
description: "[!DNL Experience Manager Assets] och Media Library för filhantering."
contentOwner: AG
feature: Asset Management,Publishing
role: User,Architect,Leader
exl-id: 4737d5ee-9a93-49f3-9f20-d4368e60e9fb
source-git-commit: f7f60036088a2332644ce87f4a1be9bae3af1c5e
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

# Använd Media Library för grundläggande resurshantering {#manage-assets-using-media-library}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/medialibrary.html?lang=en) |
| AEM as a Cloud Service | Den här artikeln |

[!DNL Adobe Experience Manager] -plattformen har olika funktioner för att hantera resurser. Med Media Library kan användarna överföra ett litet antal resurser till databasen, söka efter och använda dem på webbsidorna och utföra enkla resurshanteringsåtgärder på resurserna.

Media Library är en lättviktig DAM-lösning som medföljer [!DNL Adobe Experience Manager Sites] licens. [!DNL Sites] är ett web content management-erbjudande. Media Library fungerar med alla funktioner i Experience Manager.

[!DNL Adobe Experience Manager Assets] kan köpas separat. [!DNL Experience Manager Assets] möjliggör robust hantering av resurser via företagsbruk, anpassningar av metadata, scheman, sökning och användargränssnitt samt många andra funktioner utöver vad Media Library erbjuder.

## Licenskrav {#avail-media-library-license}

Kunder som har [!DNL Sites] licens har rätt att använda Media Library. Fungerar med alla komponenter i [!DNL Experience Manager].

Media Library installeras som en del av Sites. Ingen ytterligare licens eller paket krävs utöver Sites-licens och -installation.

## [!DNL Assets] jämfört med Media Library {#assets-and-media-library}

Experience Manager Assets tillhandahåller DAM-funktionalitet i enterpriseklass. Funktionen för resurser levereras med [!DNL Experience Manager] i ett och samma paket. Användare som inte har köpt en Assets-licens har dock inte rätt att använda de avancerade DAM-funktionerna. Utan Assets-licens, endast [Media Library-funktioner](#use-media-library) är tillgängliga.

Om du vill förhindra oavsiktlig användning av [!DNL Assets] funktioner som du inte har licens för, ta sedan bort alla [!DNL Assets]-specifika arbetsflöden, komponenter, taxonomier, alternativ och [!DNL Assets] admin från [!DNL Experience Manager]. På så sätt förhindras användarna från att oavsiktligt använda [!DNL Assets] funktioner som du inte licensierat.

## Använd Media Library {#use-media-library}

Media Library omfattar i stort sett följande användningsområden:

* Tillhandahåll grundläggande DAM-funktioner för webbsidor som skapats med [!DNL Adobe Experience Manager Sites].
* Anpassningsbara formulär och kommunikation som skapats med [!DNL Adobe Experience Manager Forms].
* Upplevelser på digital skärm skapade med [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] HTTP REST API:er för headless-åtgärder.

<!-- TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.

* Static renditions

-->

Om du vill använda Media Library-funktionen kan du använda standardfunktionen [!DNL Experience Manager] användargränssnitt. Media Library ingår i [!DNL Experience Manager Sites] installation och inget separat gränssnitt eller tillägg krävs. Med det befintliga gränssnittet har Media Library-användare rätt att utföra följande uppgifter:

* Skapa mappar för att ordna resurser.
* Överför resurser.
* Publicera resurser.
* Redigera, flytta och kopiera resurser.
* Bläddra bland, filtrera och söka (inklusive likhetssökning) resurser.
* Lägg till värden i och redigera värdena i metadatafälten, förutom i fältet Smarta taggar, som finns i [!UICONTROL Basic] fliken för en resurs [!UICONTROL Properties] sida som standard.
* Lägg till och ta bort statiska återgivningar.
* Hämta mappar, resurser och resursrenderingar.
* Skapa resursversioner.
* Skapa och utför granskningsåtgärder på resurser.
* Anteckna resurser.
* Lägg till resurser i [!DNL Sites] sidor via Content Finder.
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
>Många avancerade DAM-användningsfall uppfylls av [!DNL Experience Manager Assets]. Media Library-licens berättigar dig att endast fylla i de angivna användningsområdena med Media Library. Om ett användningsexempel inte finns med i listan ska du inte använda det med Media Library-licens. Kontakta kundsupport om du har frågor.

Du kan inte använda smarta taggar, [!DNL Asset] länk, [!DNL Asset] väljare, bulktaggning, arbetsflöden för att ändra resurser eller standard [!DNL Adobe Experience Manager] användargränssnitt som ger åtkomst till Media Library utan [!DNL Assets] licens.

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

**Se även**

* [Översätt resurser](translate-assets.md)
* [Resurser för HTTP API](mac-api-assets.md)
* [Resurser som stöds i filformat](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publicera resurser till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [DAM-funktioner i [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/home.html)
>* [[!DNL Experience Manager] som [!DNL Cloud Service] produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-cloud-service.html)
