---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 17903c6e44afd1742d21b7fc7dbe4d7c63fe8b6b
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2021 eller 2022.
>
>Ta en titt på [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) om de kommande funktionsaktiviteterna för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Se [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) för information om dokumentationsuppdateringar som inte är direkt relaterade till en release.

## Releasedatum {#release-date}

Utgivningsdatumet [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2023.12.0) är 14 december 2023. Nästa funktionsversion (2024.1.0) är planerad till 25 januari 2023.

## Versionsinformation om underhåll {#maintenance}

Du kan hitta den senaste underhållsreleasenumerationen [här](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the December 2023 Release Overview video for a summary of the features added in the 2023.12.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

-->

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Tidiga Adobe-program {#sites-early-adopter}

**Du kan använda [Real User Monitoring (RUM) Data Service](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** för att aktivera klientsidessamling för AEM as a Cloud Service.

Real User Monitoring (RUM) Data Service ger en mer exakt återgivning av användarinteraktioner och säkerställer ett tillförlitligt mått på webbplatsengagemanget. Det är en utmärkt möjlighet att få avancerade insikter om hur sidan fungerar. Detta är fördelaktigt för kunder som använder antingen Adobe-hanterat CDN eller icke-Adobe-hanterat CDN. För kunder som använder ett icke-Adobe-hanterat CDN kan nu dessutom automatiserad trafikrapportering aktiveras för dem, vilket eliminerar behovet av att dela trafikrapporter med Adobe.

Om du vill testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till `aemcs-rum-adopter@adobe.com`, tillsammans med ditt domännamn för produktions-, scen- och utvecklingsmiljön från din e-postadress som är kopplad till din Adobe ID. Adobe produktteam aktiverar sedan datatjänsten Real User Monitoring (RUM) åt dig.


## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i resursvyn {#assets-view-features}

**Skapa GenAI-bilder med Adobe Firefly**

Skapa nya bilder baserat på sökfrågor med en integrerad Adobe Firefly text-till-bild-funktion (kräver licens för Adobe Firefly).

![Integrering av Assets Firefly](/help/assets/assets/assets-firefly-integration.png)

**Sök efter liknande bilder**

Nu kan du enkelt hitta innehåll genom att välja en bild och visa liknande bilder i Experience Manager Assets-databasen.

<!--

* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)


**Video Preview**: AEM Assets now generates preview renditions of all supported video formats by default, without the need to configure a processing profile.

-->

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Experience Manager Forms] {#forms-features}

* **[Ansluta en adaptiv Forms med Microsoft® SharePoint List](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**: AEM Forms erbjuder en OOTB-integrering för att skicka formulärdata direkt till SharePoint List, så att du kan använda funktionerna i SharePoint Lists. Du kan konfigurera Microsoft SharePoint List som en datakälla för en formulärdatamodell och använda **Skicka med formulärdatamodell** skicka-åtgärd för att ansluta ett adaptivt formulär till SharePoint List.

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Tidiga Adobe-program {#forms-early-adopter}

* **[Skicka ett anpassat formulär till Adobe Workfront Fusion Scenario](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**: Forms as a Cloud Service har ett körklart alternativ för smidig anslutning av adaptiva formulär till Adobe Workfront. Detta förenklar processen att skicka in ett adaptivt formulär till ett Adobe Workfront-scenario, vilket gör att du kan utlösa ett Workfront Fusion-scenario när ett adaptivt formulär skickas in.

* **[Stöd för språk från höger till vänster](/help/forms/supporting-new-language-localization-core-components.md)**: Adaptiv Forms som bygger på kärnkomponenter kan nu presenteras på höger-till-vänster-språk (RTL) som arabiska, persiska och urdu. RTL-språken talas av över 2 miljarder människor globalt. Genom att använda ett formulär på RTL-språk kan ni utöka räckvidden för era adaptiva formulär så att de kan anpassas till dessa olika målgrupper och väljas ut på RTL-marknader. I vissa regioner är det också ett juridiskt mandat att tillhandahålla formulär på det lokala språket. Genom att ta hand om lokala språk kan ni inte bara öppna dörrar för en bredare publik utan också säkerställa att relevanta lagar och bestämmelser följs.

  ![Stöd för höger-till-vänster-språk](/help/forms/assets/right-to-left-language-support.png)

* **[Protect dina dokument med DocAssurance API:er (del av kommunikations-API:er)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: Med API:erna för DocAssurance kan du skydda känslig information genom att signera och kryptera dokumenten. Genom kryptering omvandlas innehållet i ett dokument till ett oläsligt format så att bara behöriga användare kan få åtkomst till det. Detta förstärkta skydd skyddar inte bara värdefulla data från obehöriga ögon, utan ger även sinnesro. Med signatur-API:erna kan din organisation skydda säkerheten och sekretessen för Adobe PDF-dokument som den distribuerar och tar emot. Den här tjänsten använder digitala signaturer och certifiering för att säkerställa att endast avsedda mottagare kan ändra dokument.

  Du kan skriva till `aem-forms-early-adopter-program@adobe.com` från ditt officiella e-post-id för att gå med i programmet för tidiga användare och begära åtkomst till funktionen.

## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation {#foundation}

### CDN-konfiguration Tidigt program {#cdn-config-early-adopter}

Förutom den nyligen släppta [Trafikfilterregler](/help/security/traffic-filter-rules-including-waf.md), som innehåller reglerna för valfri brandvägg för webbprogram (WAF), finns en möjlighet att använda Configuration Pipeline för att deklarera och distribuera andra typer av CDN-konfigurationer. Vi vill gärna veta mer om dina användningsexempel, bland annat:
* 301/302 klientomdirigeringar
* förbluffande förfrågningar vid kanten till godtyckliga ursprung
* URL-omformningar
* ange eller ändra begärande- eller svarshuvuden
* anpassade felsidor när CDN inte kan nå AEM
* autentisering med användarnamn/lösenord
* andra användbara CDN-konfigurationer

Skicka e-post till **aemcs-cdn-config-adopter@adobe.com** från ditt officiella e-post-ID med din feedback.

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
