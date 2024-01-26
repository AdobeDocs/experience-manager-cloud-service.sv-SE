---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 8c33426c38b087c83b945572374089ad9cb44daf
workflow-type: tm+mt
source-wordcount: '775'
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

Utgivningsdatumet [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2024.1.0) är 25 januari 2024. Nästa funktionsversion (2024.2.0) är planerad till den 29 februari 2024.

## Versionsinformation om underhåll {#maintenance}

Du kan hitta den senaste underhållsreleasenumerationen [här](/help/release-notes/maintenance/latest.md).

## Släpp video {#release-video}

Titta på videon med versionsöversikten från januari 2024 om du vill se en sammanfattning av funktioner som lagts till i version 2024.1.0:

>[!VIDEO](https://video.tv.adobe.com/v/3427041?quality=12)

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### EXTENSION MANAGER i AEM SITES {#sites-extension-manager}

**Utforska nya [EXTENSION MANAGER i AEM SITES](https://developer.adobe.com/uix/docs/extension-manager/)** för att anpassa AEM genom att konfigurera gränssnittstillägg.

![EXTENSION MANAGER i AEM SITES](/help/assets/sites/extension-manager/homepage.png)

Extension Manager i AEM Sites gör det möjligt för utvecklare och yrkesverksamma att få tillgång till, hantera och anpassa gränssnittstillägg som har byggts för att förbättra funktionaliteten i AEM Sites.
Med Extension Manager kan man

* Aktivera eller inaktivera tillägg per instans.
* Konfigurera tilläggsparametrar;
* Förhandsgranska tillägg och generera en delbar förhandsgranskningslänk.
* Upptäck funktioner för användargränssnittets utbyggbarhet via interaktiva demos.
* Få tillgång till Adobe experimentella funktioner via förstahandstillägg.

Vi söker aktivt efter feedback och nya användningsexempel för UI-tillägg. Om du vill ansluta skickar du ett e-postmeddelande till `uix@adobe.com`.

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Förhandsversionsfunktioner i administratörsvyn {#admin-view-prerelease}

**Förhandsgranska återgivningar för alla videotyper som stöds**

Experience Manager Assets genererar nu förhandsgranskningsåtergivningar av alla videotyper som stöds som standard utan att en bearbetningsprofilskonfiguration krävs

### Resursvy {#assets-view-features}

**Smarta taggar blocklist**

Med Assets Essentials kan du nu definiera blockeringslista som innehåller ord som inte ska läggas till som smarta taggar för resurser när de överförs till databasen. Med den här funktionen kan ni upprätthålla varumärkets efterlevnad och minska arbetet med att moderera smarta taggar.

![Smarta taggar blocklist](/help/assets/assets/block-tags.png)


## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

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

### Stöd för Dynatrace {#dynatrace}

Dynatracskunder kan övervaka sin AEM. [Läs om](/help/implementing/cloud-manager/dynatrace.md) för att begära anslutning till din Dynatrace-miljö för övervakning av programprestanda. Observera att New Relic APM, som är tillgängligt för alla kunder, kommer att sluta samla in data om Dynatrace är aktiverat.

### RDE-stöd för Front-End-kod med webbplatsteman och webbplatsmallar: Tidigt Adobe-program {#rde-frontend-early-adopter}

[Rapid Development Environment (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) nu stöder kod som bygger på [webbplatsteman](/help/sites-cloud/administering/site-creation/site-themes.md) och [webbplatsmallar](/help/sites-cloud/administering/site-creation/site-templates.md), för tidiga användare. Med de lokala redigeringssystemen görs detta med hjälp av ett kommandoradsdirektiv i stället för ett [rörledning för frontend](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md). Kontakta **aemcs-rde-support@adobe.com** för att testa och ge feedback.

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
