---
title: Versionsinformation om 2023.10.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2023.10.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 81a6cbd2-7101-429b-8572-2650c5bea963
source-git-commit: 811a8f4d83a1034737c23b1707a24b52742fef55
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 0%

---

# Versionsinformation 2023.10.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen i version 2023.10.0 av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2021 eller 2022.
>
>Ta en titt på [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) om de kommande funktionsaktiviteterna för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Se [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) för information om dokumentationsuppdateringar som inte är direkt relaterade till en release.

## Releasedatum {#release-date}

Utgivningsdatumet [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2023.10.0) är 26 oktober 2023. Nästa funktionsrelease (2023.11.0) planeras till 30 november 2023.

## Versionsinformation om underhåll {#maintenance}

Du kan hitta den senaste underhållsreleasenumerationen [här](/help/release-notes/maintenance/latest.md).

## Släpp video {#release-video}

Titta på videon med versionsöversikten för oktober 2023 om du vill se en sammanfattning av funktioner som lagts till i version 2023.10.0:

>[!VIDEO](https://video.tv.adobe.com/v/3425186/?quality=12)

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner {#assets-features}

**AEM Assets-tillägg för Adobe Express**: Experience Manager Assets har nu en [tillägg för Adobe Express](/help/assets/addon-adobe-express.md). Tillägget ger dig direktåtkomst till resurser som lagras i Experience Manager Assets inifrån användargränssnittet för Adobe Expressen. Du kan placera innehåll som hanteras i AEM Assets på arbetsytan Express och sedan spara nytt eller redigerat innehåll i en AEM Assets-databas. Tillägget ger följande fördelar:

* Ökat återanvändning av innehåll genom att redigera och spara nya resurser i AEM

* Minskar den totala tiden och arbetet med att skapa nya resurser eller skapa nya versioner av befintliga resurser

  ![Inkludera resurser från resurstillägg](/help/assets/assets/aem-assets-add-on-include-assets.png)

### Nya funktioner i resursvyn {#assets-view-features}

* **Massimportera resurser från OneDrive-datakällan**: Nu kan administratörer [importera ett stort antal resurser från OneDrive till AEM Assets](/help/assets/bulk-import-assets-view.md#onedrive-developer-application). Den uppdaterade listan över de datakällor som stöds för bulkimport är Azure, AWS, Google Cloud, Dropbox och OneDrive.

  ![tilldela metadataformulär till en mapp](/help/assets/assets/bulk-import-source-details-onedrive.png)

* **Stöd för olika sorters tillstånd för bibliotek**: Med Experience Manager Assets kan du nu konfigurera åtkomst till Creative Cloud-bibliotek i en annan IMS-organisation. Det ger enklare åtkomst till de senaste produktövergripande arbetsflödena mellan Creative Cloud och Experience Manager och minskar tiden och arbetet för kreatörerna.

### Förhandsversioner av funktioner som finns i [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [Stöd för flera undertexter och flerljudspår för videor i Dynamic Media](/help/assets/dynamic-media/video.md#about-msma)—Nu kan du enkelt lägga till flera undertexter och flera ljudspår i en primär video. Detta innebär att videoklippen är tillgängliga för alla mottagare världen över. Du kan anpassa en enda publicerad primär video till en global publik på flera språk och följa riktlinjer för tillgänglighet för olika geografiska regioner. Författare kan också hantera undertexter och ljudspår från en enda flik i användargränssnittet.

  ![Fliken Undertexter och Ljudspår på sidan Egenskaper för en vald videoresurs.](/help/release-notes/assets/msma-aem-cs.png)*Fliken Undertexter och Ljudspår på sidan Egenskaper för en vald videoresurs.*

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Experience Manager Forms] {#forms-features}

* **[Anpassade egenskaper för Adaptive Forms](/help/forms/template-editor-core-components.md#add-a-custom-group-name-in-the-policy-of-template-editor)**: Du kan koppla anpassade attribut (nyckelvärdepar) till en formulärmall eller adaptiv formulärkomponent så att formulärutvecklare kan leverera dynamiska formulärbeteenden som anpassar sig utifrån värdena för dessa anpassade attribut. Utvecklare kan till exempel skapa olika renderingar av en Headless Forms-komponent på mobil-, dator- eller webbplattformar baserat på värdena för anpassade attribut, vilket avsevärt förbättrar användarupplevelsen på en mängd olika enheter.

* **Teman och mallar**: Kom igång snabbt med att skapa formulär med våra nya teman och mallar, som är skräddarsydda för både erfarna yrkesverksamma och nya formulärförfattare. Dessa välstrukturerade teman och mallar är sömlöst byggda med adaptiva Forms Core-komponenter och gör att du snabbt kan börja skapa formulär för vanliga användningsområden.

  ![Körklara mallar](/help/forms/assets/form-templates-ootb.png)


### Program för tidig användning {#forms-early-adopter}

* **[Protect dina dokument med DocAssurance API:er (del av kommunikations-API:er)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: Med API:erna för DocAssurance kan du skydda känslig information genom att signera och kryptera dokumenten. Genom kryptering omvandlas innehållet i ett dokument till ett oläsligt format så att bara behöriga användare kan få åtkomst till det. Detta förstärkta skydd skyddar inte bara värdefulla data från obehöriga ögon, utan ger även sinnesro. Med signatur-API:erna kan din organisation skydda säkerheten och sekretessen för Adobe PDF-dokument som den distribuerar och tar emot. Den här tjänsten använder digitala signaturer och certifiering för att säkerställa att endast avsedda mottagare kan ändra dokument.

  Du kan skriva till `aem-forms-early-adopter-program@adobe.com` från ditt officiella e-post-id för att gå med i programmet för tidiga användare och begära åtkomst till funktionen.

## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation {#foundation}

### Trafikfilterregler, inklusive WAF {#traffic-filter-rules-waf}

[Filtrera trafiken vid hanterad CDN i Adobe](/help/security/traffic-filter-rules-including-waf.md) genom att deklarera regler som matchar webbplatstrafiken efter egenskaper som URL, IP-adress och användaragent, eller ange anpassade trafikhastighetsgränser för att skydda mot DoS-attacker. Kunderna kan även licensiera en uppsättning avancerade regler för Web Application Firewall (WAF) för extra skydd mot avancerade hot mot webbplatser.

Vi rekommenderar att du lär dig trafikfilterregler genom att [testa en självstudiekurs](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html)! Här får du hjälp med att konfigurera en ny konfigurationspipeline för Cloud Manager, deklarera regler i en konfigurationsfil och analysera CDN-loggar för skadlig trafik.

Trafikfilterregler finns nu tillgängliga i dev-miljöer, med en gradvis utrullning till scen- och prodmiljöer i november. Du kan begära tidigare åtkomst på scenen och produkten via e-post **aemcs-waf-adopter@adobe.com**.

De avancerade reglerna för WAF-trafikfilter kan licensieras senare i år genom erbjudandena Förbättrat skydd eller WAF-DDoS-skydd.

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
