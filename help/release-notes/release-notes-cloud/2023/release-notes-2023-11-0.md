---
title: Versionsinformation om 2023.11.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2023.11.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: c33874869bccae1e9837b30827a655e70636dd56
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 0%

---


# Versionsinformation 2023.11.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

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

Utgivningsdatumet [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2023.11.0) är 30 november 2023. Nästa funktionsrelease (2023.12.0) planeras att släppas den 14 december 2023.

## Versionsinformation om underhåll {#maintenance}

Du kan hitta den senaste underhållsreleasenumerationen [här](/help/release-notes/maintenance/latest.md).

## Släpp video {#release-video}

Titta på videon med versionsöversikten för november 2023 om du vill se en sammanfattning av funktioner som lagts till i version 2023.11.0:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Tidiga Adobe-program {#sites-early-adopter}

**[Sök och ersätt strängar i innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#find-and-replace-find-and-replace)**: Med Content Fragment Console kan användarna enkelt och intuitivt ersätta en sträng som finns i flera innehållsfragment samtidigt för att snabba upp innehållets hastighet.

![Sök och ersätt](/help/sites-cloud/administering/content-fragments/assets/cf-managing-find-replace.png)

Är du intresserad av att testa funktionen och ge feedback? Skicka e-post till **aemcs-headless-adopter@adobe.com** från ditt officiella e-post-ID om du vill veta mer om programmet för tidig användning.

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i resursvyn {#assets-view-features}

* **Redigerare för inbäddad Adobe Express i AEM Assets**: Användare med tillgång till Express har nu integrerade bildredigerings- och redigeringsverktyg från Adobe Express och Adobe Firefly som är tillgängliga direkt inifrån AEM Assets för att förbättra återanvändningen av innehåll och snabba upp innehållets hastighet.

  ![tilldela metadataformulär till en mapp](/help/assets/assets/adobe-express-aem-assets.png)

<!--

* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)

-->


* **Rapporter om lagringsanvändning i insikter**: Administratörer kan nu visa användningsrapporter för lagring som ingår i Insights.

  ![information om lagringsanvändning](/help/assets/assets/storage-usage-insights.png)

* **Sök i den första startsidans konfiguration**: Med Experience Manager Assets kan du nu konfigurera startsidan för din organisation. Om du väljer att söka först som startsida kan du konfigurera sökfältets justering, bakgrundsbild och logotyp för din organisation.

  ![söka efter första konfigurationen](/help/assets/assets/search-first-configuration.png)

### Nya funktioner i förhandsversionen för administratörsvyn {#admin-view-features-prerelease}

**Videoförhandsgranskning**: AEM Assets genererar nu förhandsvisningsåtergivningar av alla videoformat som stöds som standard, utan att du behöver konfigurera en bearbetningsprofil.

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Experience Manager Forms] {#forms-features}

* **[Kryssrutekomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**: Adaptiv Forms baserad på kärnkomponenter kan nu innehålla en kryssrutekomponent. Det gör att användare kan göra binära val, markera eller avmarkera ett visst alternativ. Det visas vanligtvis som en liten ruta som du kan klicka på eller peka på för att växla mellan två lägen: markerad och avmarkerad. Kryssrutan är ett vanligt formulärelement som används för att ange ett ja/nej- eller sant/falskt-val.

* **[Villkorskomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**: Adaptiv Forms baserad på kärnkomponenter kan nu innehålla en villkorskomponent. Det gör det möjligt för formulärförfattare att infoga ett specifikt avsnitt i formuläret där användarna presenteras med de villkor eller juridiska avtal som är kopplade till användningen av en tjänst, produkt eller plattform. Den här komponenten är utformad för att informera användare om de regler, bestämmelser och skyldigheter som de godkänner genom att skicka in formuläret.

  ![Komponenter på fliken Kryssruta, Villkor och Lodrätt](/help/forms/assets/forms-components.png)

* **[Lodräta flikar, komponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**: Adaptiv Forms baserad på kärnkomponenter kan nu ordna formulärinnehåll i en lodrät lista med flikar, vilket ger en strukturerad och navigeringsbar layout. Om du använder vertikala flikar i ett formulär kan det förbättra användarupplevelsen genom att förenkla navigeringen och förbättra organisationen av formulärinnehållet, särskilt i situationer där ett formulär innehåller flera avsnitt eller komplex information.



### Nya funktioner i [!DNL Forms] Förhandsversion {#prerelease-features-forms}

* **[Ansluta en adaptiv Forms med Microsoft® SharePoint List](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**: AEM Forms erbjuder en OOTB-integrering för att skicka in formulärdata direkt till SharePoint List, vilket gör att du kan utnyttja SharePoint Lists funktioner. Du kan konfigurera Microsoft SharePoint List som en datakälla för en formulärdatamodell och använda **Skicka med formulärdatamodell** skicka-åtgärd för att ansluta ett adaptivt formulär till SharePoint List.

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Tidiga Adobe-program {#forms-early-adopter}

* **Skicka ett anpassat formulär till Adobe Workfront Fusion Scenario**: Forms as a Cloud Service har ett körklart alternativ för smidig anslutning av adaptiva formulär till Adobe Workfront. Detta förenklar processen att skicka in ett adaptivt formulär till ett Adobe Workfront-scenario, vilket gör att du kan utlösa ett Workfront Fusion-scenario när ett adaptivt formulär skickas in.

* **Stöd för språk från höger till vänster**: Adaptiv Forms som bygger på kärnkomponenter kan nu presenteras på höger-till-vänster-språk (RTL) som arabiska, persiska och urdu. RTL-språken talas av över 2 miljarder människor globalt. Med hjälp av ett formulär på RTL-språk kan ni utöka räckvidden för era adaptiva formulär så att de kan passa olika målgrupper och utnyttja RTL-marknader. I vissa regioner är det också ett juridiskt mandat att tillhandahålla formulär på det lokala språket. Genom att ta hand om lokala språk kan ni inte bara öppna dörrar för en bredare publik utan också säkerställa att relevanta lagar och bestämmelser följs.

  ![Stöd för höger-till-vänster-språk](/help/forms/assets/right-to-left-language-support.png)

* **[Protect dina dokument med DocAssurance API:er (del av kommunikations-API:er)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: Med API:erna för DocAssurance kan du skydda känslig information genom att signera och kryptera dokumenten. Genom kryptering omvandlas innehållet i ett dokument till ett oläsligt format så att bara behöriga användare kan få åtkomst till det. Detta förstärkta skydd skyddar inte bara värdefulla data från obehöriga ögon, utan ger även sinnesro. Med signatur-API:erna kan din organisation skydda säkerheten och sekretessen för Adobe PDF-dokument som den distribuerar och tar emot. Den här tjänsten använder digitala signaturer och certifiering för att säkerställa att endast avsedda mottagare kan ändra dokument.

  Du kan skriva till `aem-forms-early-adopter-program@adobe.com` från ditt officiella e-post-id för att gå med i programmet för tidiga användare och begära åtkomst till funktionen.

## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation {#foundation}

### WAF-trafikfilterregler kan nu licensieras {#cdn-waf-license}

Traffic Filter Rules släpptes i oktober och innehöll en kommentar om att den speciella kategorin för reglerna för Web Application Firewall (WAF) skulle vara tillgänglig senare i år för att komplettera de regler som redan finns för Sites och Forms-kunder. Som uppdatering kan WAF-DDoS Protection-erbjudandet nu licensieras.

När dessa avancerade WAF-regler har licensierats kan de distribueras till CDN med Cloud Manager Configuration Pipeline för att lägga till ett extra skydd mot webbattacker.

Läs om [Trafikfilterregler](/help/security/traffic-filter-rules-including-waf.md), inklusive WAF. Tala med ditt AEM om licenser för WAF-DDoS Protection eller Enhanced Security.

### CDN-konfiguration Tidigt program {#cdn-config-early-adopter}

Förutom den nyligen släppta [Trafikfilterregler (inklusive WAF)](/help/security/traffic-filter-rules-including-waf.md)kan du använda Configuration Pipeline för att deklarera och distribuera andra typer av CDN-konfigurationer. Vi vill gärna veta mer om dina användningsexempel, bland annat:
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

## Kända fel {#known-issues}

* Det går inte att skicka Adaptiv Forms baserat på kärnkomponenter. Problemet inträffar för Adaptive Forms som byggts med Core Components version 2.0.38 - 2.0.60.

  För att lösa problemet. du kan gå över till Adaptive Form Core Components version 2.0.62 eller senare. Om du vill ange en version av adaptiva Forms Core-komponenter för din miljö, [ange versioner av komponenterna core.forms.components.version, core.forms.components.af.version och core.wcm.components.version](/help/forms/enable-adaptive-forms-core-components.md#2-add-adaptive-forms-core-components-dependencies-to-your-git-repository) beroenden i ditt Forms as a Cloud Service arkiv eller AEM Archetype-baserade projekt och [driftsätta ändringarna i Forms as a Cloud Service miljö](/help/forms/enable-adaptive-forms-core-components.md#build-and-deploy-updated-code-on-an-aem-forms-as-a-cloud-service-environment). Du hittar den senaste versionen av adaptiva Forms Core Components-beroenden på [Adaptiv Forms Core Components Git-databas](https://github.com/adobe/aem-core-forms-components#system-requirements).
