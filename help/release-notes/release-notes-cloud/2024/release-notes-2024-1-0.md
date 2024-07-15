---
title: Versionsinformation för version 2024.1.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för version 2024.1.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 9f5d97c6-6536-4593-acbf-cbe8bf9b5eeb
feature: Release Information
role: Admin
source-git-commit: 8d5d8910a906e2adf17fa9c75f17634602c2e0b9
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 0%

---

# Versionsinformation 2024.1.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2024.1.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2021 eller 2022.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) för att lära dig mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2024.1.0) är 25 januari 2024. Nästa funktionsversion (2024.3.0) är planerad till 11 april 2024.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

## Släpp video {#release-video}

Titta på videon med versionsöversikten från januari 2024 om du vill se en sammanfattning av funktioner som lagts till i version 2024.1.0:

>[!VIDEO](https://video.tv.adobe.com/v/3427041?quality=12)

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### EXTENSION MANAGER i AEM SITES {#sites-extension-manager}

**Utforska nya [Extension Manager i AEM Sites](https://developer.adobe.com/uix/docs/extension-manager/)** för att anpassa AEM genom att konfigurera gränssnittstillägg.

![Extension Manager i AEM Sites](/help/assets/sites/extension-manager/homepage.png)

Med Extension Manager i AEM Sites kan utvecklare och tekniker få tillgång till, hantera och anpassa [gränssnittstillägg](https://developer.adobe.com/uix/docs/) som skapats med [Adobe App Builder](https://developer.adobe.com/app-builder/) för att förbättra funktionaliteten i AEM Sites.
Med Extension Manager kan man

* Aktivera eller inaktivera tillägg per instans.
* Konfigurera tilläggsparametrar;
* Förhandsgranska tillägg och generera en delbar förhandsgranskningslänk.
* Upptäck funktioner för användargränssnittets utbyggbarhet via interaktiva demos.
* Få tillgång till Adobe experimentella funktioner via förstahandstillägg.

Vi söker aktivt efter feedback och nya användningsexempel för UI-tillägg. Om du vill ansluta skickar du ett e-postmeddelande till `uix@adobe.com`.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Förhandsversionsfunktioner i administratörsvyn {#admin-view-prerelease}

**Förhandsgranska återgivningar för alla videotyper som stöds**

Experience Manager Assets genererar nu förhandsgranskningsåtergivningar av alla videotyper som stöds som standard utan att en bearbetningsprofilskonfiguration krävs

### Assets view {#assets-view-features}

**Smarta taggar blocklist**

Med Assets Essentials kan du nu definiera blockeringslista som innehåller ord som inte ska läggas till som smarta taggar för resurser när de överförs till databasen. Med den här funktionen kan ni upprätthålla varumärkets efterlevnad och minska arbetet med att moderera smarta taggar.

![Smarta taggar blocklist](/help/assets/assets/block-tags.png)


## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Tidiga Adobe-program {#forms-early-adopter}

* **[Skicka ett anpassat formulär till Adobe Workfront Fusion Scenario](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**: Forms as a Cloud Service har ett användbart alternativ för att enkelt ansluta ett anpassat formulär till Adobe Workfront. Detta förenklar processen att skicka in ett adaptivt formulär till ett Adobe Workfront-scenario, vilket gör att du kan utlösa ett Workfront Fusion-scenario när ett adaptivt formulär skickas in.

* **[Stöd för höger till vänster-språk](/help/forms/supporting-new-language-localization-core-components.md)**: Adaptiv Forms som bygger på kärnkomponenter kan nu presenteras på ett höger till vänster-språk (RTL) som arabiska, persiska och urdu. RTL-språken talas av över 2 miljarder människor globalt. Genom att använda ett formulär på RTL-språk kan ni utöka räckvidden för era adaptiva formulär så att de kan anpassas till dessa olika målgrupper och väljas ut på RTL-marknader. I vissa regioner är det också ett juridiskt mandat att tillhandahålla formulär på det lokala språket. Genom att ta hand om lokala språk kan ni inte bara öppna dörrar för en bredare publik utan också säkerställa att relevanta lagar och bestämmelser följs.

  ![Stöd för höger till vänster-språk](/help/forms/assets/right-to-left-language-support.png)

* **[Protect dina dokument med DocAssurance-API:er (del av kommunikations-API:er)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: Med DocAssurance-API:erna kan du skydda känslig information genom att signera och kryptera dokumenten. Genom kryptering omvandlas innehållet i ett dokument till ett oläsligt format så att bara behöriga användare kan få åtkomst till det. Detta förstärkta skydd skyddar inte bara värdefulla data från obehöriga ögon, utan ger även sinnesro. Med signatur-API:erna kan din organisation skydda säkerheten och sekretessen för Adobe PDF-dokument som den distribuerar och tar emot. Den här tjänsten använder digitala signaturer och certifiering för att säkerställa att endast avsedda mottagare kan ändra dokument.

  Du kan skriva till `aem-forms-early-adopter-program@adobe.com` från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen.

* **[Du kan utnyttja RUM-datatjänsten](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** för att aktivera klientsidessamling för AEM as a Cloud Service.
Real Use Monitoring (RUM) Data Service ger en mer exakt återgivning av användarinteraktioner och säkerställer ett tillförlitligt mått på webbplatsengagemanget. Det är en utmärkt möjlighet att få avancerade insikter om hur sidan fungerar. Detta är fördelaktigt för kunder som använder antingen Adobe-hanterat CDN eller icke-Adobe-hanterat CDN. För kunder som använder ett icke-Adobe-hanterat CDN kan nu dessutom automatiserad trafikrapportering aktiveras för dem, vilket eliminerar behovet av att dela trafikrapporter med Adobe.

  Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till `aemcs-rum-adopter@adobe.com` tillsammans med ditt domännamn för varje miljö som du vill aktivera RUM för från din e-postadress som är kopplad till din Adobe ID. Adobe produktteam kommer sedan att aktivera datatjänsten för övervakning av verkligt bruk (RUM) åt dig.

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### Stöd för Dynatrace {#dynatrace}

Dynatrace-kunder kan övervaka AEM. [Läs hur](/help/implementing/cloud-manager/dynatrace.md) begär anslutning till din Dynatrace-miljö för övervakning av programprestanda. Observera att New Relic APM, som är tillgängligt för alla kunder, kommer att sluta samla in data om Dynatrace är aktiverat.

### RDE-stöd för Front-End-kod med webbplatsteman och webbplatsmallar: Tidigt Adobe-program {#rde-frontend-early-adopter}

[Rapid Development Environment (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) har nu stöd för klientkod baserat på [webbplatsteman](/help/sites-cloud/administering/site-creation/site-themes.md) och [webbplatsmallar](/help/sites-cloud/administering/site-creation/site-templates.md) för tidiga användare. Med RDE:er görs detta med hjälp av ett kommandoradsdirektiv i stället för en [frontendpipeline](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md). Kontakta **aemcs-rde-support@adobe.com** för att prova det och ge feedback.

### CDN-konfiguration Tidigt program {#cdn-config-early-adopter}

Förutom de nyligen släppta [reglerna för trafikfilter](/help/security/traffic-filter-rules-including-waf.md), som innehåller de valfria reglerna för brandväggen för webbprogram (WAF), finns det en möjlighet att använda Configuration Pipeline för att deklarera och distribuera [andra typer av CDN-konfigurationer](/help/implementing/dispatcher/cdn-configuring-traffic.md). Gå med i det tidiga adopter-programmet genom att skicka ett e-postmeddelande till **aemcs-cdn-config-adopter@adobe.com** för att få åtkomst till:
* 301/302 klientomdirigeringar
* förbluffande förfrågningar vid kanten till godtyckliga ursprung
* URL-omformningar
* ange eller ändra begärande- eller svarshuvuden
* anpassade felsidor när CDN inte kan nå AEM

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över migreringsverktygen [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
