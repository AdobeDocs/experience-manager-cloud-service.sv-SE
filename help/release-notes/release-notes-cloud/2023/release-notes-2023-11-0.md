---
title: Versionsinformation om 2023.11.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2023.11.0-utgåvan av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 19cff082-80aa-445c-9462-5e319b7fe0e9
feature: Release Information
role: Admin
source-git-commit: 0845447c1c4f47b77debd179f24eac95a0d2c2db
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 0%

---

# Versionsinformation 2023.11.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2023.11.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2021 eller 2022.
>
>Ta en titt på [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=sv-SE) om du vill veta mer om kommande funktionsaktiveringar för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=sv-SE).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell funktionsversion (2023.11.0) är 30 november 2023. Nästa funktionsrelease (2023.12.0) planeras att släppas den 14 december 2023.

## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

## Släpp video {#release-video}

Titta på videon med versionsöversikten för november 2023 om du vill se en sammanfattning av funktioner som lagts till i version 2023.11.0:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Tidiga Adobe-program {#sites-early-adopter}

**[Sök och ersätt strängar i innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#find-and-replace-find-and-replace)**: Med konsolen Innehållsfragment kan användarna enkelt och intuitivt ersätta en sträng som finns i flera innehållsfragment samtidigt, vilket snabbar upp innehållets hastighet.

![Sök och ersätt](/help/sites-cloud/administering/content-fragments/assets/cf-managing-find-replace.png)

Är du intresserad av att testa funktionen och ge feedback? Skicka ett e-postmeddelande till **aemcs-headless-adopter@adobe.com** från ditt officiella e-post-ID om du vill veta mer om det tidiga adopterprogrammet.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i Assets View {#assets-view-features}

* **Inbäddad Adobe Express-redigerare i AEM Assets**: Användare med tillgång till Express har nu integrerade verktyg för bildredigering och bildskapande från Adobe Express och Adobe Firefly tillgängliga direkt i AEM Assets för att förbättra återanvändning av innehåll och snabba upp hastigheten.

  ![tilldela metadataformulär till en mapp](/help/assets/assets/adobe-express-aem-assets.png)

<!--

* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)

-->


* **Rapporter om lagringsanvändning i Insights**: Administratörer kan nu visa användningsrapporter för lagring som är tillgängliga som en del av Insights.

  ![information om lagringsanvändning](/help/assets/assets/storage-usage-insights.png)

* **Sökningskonfiguration för första hemsidan**: Nu kan du konfigurera startsidan för din organisation med Experience Manager Assets. Om du väljer att söka först som startsida kan du konfigurera sökfältets justering, bakgrundsbild och logotyp för din organisation.

  ![sök i den första konfigurationen](/help/assets/assets/search-first-configuration.png)

### Nya funktioner i förhandsversionen för administratörsvyn {#admin-view-features-prerelease}

**Videoförhandsgranskning**: AEM Assets genererar nu förhandsvisningsåtergivningar av alla videoformat som stöds som standard, utan att du behöver konfigurera en bearbetningsprofil.

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Experience Manager Forms] {#forms-features}

* **[Kryssrutekomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html?lang=sv-SE)**: Adaptiv Forms baserad på kärnkomponenter kan nu innehålla en kryssrutekomponent. Det gör att användare kan göra binära val, markera eller avmarkera ett visst alternativ. Det visas vanligtvis som en liten ruta som du kan klicka på eller peka på för att växla mellan två lägen: markerad och avmarkerad. Kryssrutan är ett vanligt formulärelement som används för att ange ett ja/nej- eller sant/falskt-val.

* **[Villkorskomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html?lang=sv-SE)**: Adaptiv Forms baserad på kärnkomponenter kan nu innehålla en villkorskomponent. Det gör det möjligt för formulärförfattare att infoga ett specifikt avsnitt i formuläret där användarna presenteras med de villkor eller juridiska avtal som är kopplade till användningen av en tjänst, produkt eller plattform. Den här komponenten är utformad för att informera användare om de regler, bestämmelser och skyldigheter som de godkänner genom att skicka in formuläret.

  ![Komponenter på fliken Kryssruta, Villkor och Lodrätt](/help/forms/assets/forms-components.png)

* **[Komponent för lodräta flikar](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html?lang=sv-SE)**: Adaptiv Forms baserad på kärnkomponenter kan nu ordna formulärinnehåll i en lodrät lista med flikar, vilket ger en strukturerad och navigeringsbar layout. Om du använder vertikala flikar i ett formulär kan det förbättra användarupplevelsen genom att förenkla navigeringen och förbättra organisationen av formulärinnehållet, särskilt i situationer där ett formulär innehåller flera avsnitt eller komplex information.



### Nya funktioner i förhandsversionen av [!DNL Forms] {#prerelease-features-forms}

* **[Anslut en adaptiv Forms med Microsoft® SharePoint List](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**: AEM Forms erbjuder en OTB-integrering för att skicka formulärdata direkt till SharePoint List, vilket gör att du kan utnyttja SharePoint Lists-funktioner. Du kan konfigurera Microsoft SharePoint List som en datakälla för en formulärdatamodell och använda åtgärden **Skicka med formulärdatamodell** för att ansluta ett anpassat formulär med SharePoint List.

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Tidiga Adobe-program {#forms-early-adopter}

* **Skicka ett anpassat formulär till Adobe Workfront Fusion Scenario**: Forms as a Cloud Service har ett användbart alternativ för att enkelt ansluta ett anpassat formulär till Adobe Workfront. Detta förenklar processen att skicka in ett adaptivt formulär till ett Adobe Workfront-scenario, vilket gör att du kan utlösa ett Workfront Fusion-scenario när ett adaptivt formulär skickas in.

* **Stöd för höger till vänster-språk**: Adaptiv Forms som bygger på kärnkomponenter kan nu presenteras på ett höger till vänster-språk (RTL) som arabiska, persiska och urdu. RTL-språken talas av över 2 miljarder människor globalt. Med hjälp av ett formulär på RTL-språk kan ni utöka räckvidden för era adaptiva formulär så att de kan passa olika målgrupper och utnyttja RTL-marknader. I vissa regioner är det också ett juridiskt mandat att tillhandahålla formulär på det lokala språket. Genom att ta hand om lokala språk kan ni inte bara öppna dörrar för en bredare publik utan också säkerställa att relevanta lagar och bestämmelser följs.

  ![Stöd för höger till vänster-språk](/help/forms/assets/right-to-left-language-support.png)

* **[Skydda dina dokument med DocAssurance-API:er (del av kommunikations-API:er)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: Med DocAssurance-API:erna kan du skydda känslig information genom att signera och kryptera dokumenten. Genom kryptering omvandlas innehållet i ett dokument till ett oläsligt format så att bara behöriga användare kan få åtkomst till det. Detta förstärkta skydd skyddar inte bara värdefulla data från obehöriga ögon, utan ger även sinnesro. Med signatur-API:erna kan din organisation skydda säkerheten och sekretessen för Adobe PDF-dokument som den distribuerar och tar emot. Den här tjänsten använder digitala signaturer och certifiering för att säkerställa att endast avsedda mottagare kan ändra dokument.

  Du kan skriva till `aem-forms-ea@adobe.com` från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen.

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### WAF trafikfilterregler kan nu licensieras {#cdn-waf-license}

Traffic Filter Rules släpptes i oktober och innehöll en kommentar om att specialkategorin WAF-regler (Web Application Firewall) skulle vara tillgänglig senare i år för att komplettera de regler som redan är tillgängliga för Sites och Forms-kunder. Som en uppdatering kan WAF-DDoS Protection-erbjudandet nu licensieras.

När licensen har löpt ut kan dessa avancerade WAF-regler distribueras till CDN med Cloud Manager Configuration Pipeline för att lägga till ett extra skydd mot webbattacker.

Läs om [trafikfilterregler](/help/security/traffic-filter-rules-including-waf.md), inklusive WAF. Tala med ditt AEM-kontoteam om licensiering av WAF-DDoS-skydd eller förbättrad säkerhet.

### Tidiga Adobe-program för domänmappning {#cdn-config-early-adopter}

Förutom de nyligen släppta [trafikfilterreglerna (inklusive WAF)](/help/security/traffic-filter-rules-including-waf.md) finns det en möjlighet att använda konfigurationsförloppet för att deklarera och distribuera andra typer av CDN-konfigurationer. Vi vill gärna veta mer om dina användningsexempel, bland annat:
* 301/302 klientomdirigeringar
* förbluffande förfrågningar vid kanten till godtyckliga ursprung
* URL-omformningar
* ange eller ändra begärande- eller svarshuvuden
* anpassade felsidor när CDN inte kan nå AEM
* autentisering med användarnamn/lösenord
* andra användbara CDN-konfigurationer

Skicka ett e-postmeddelande till **aemcs-cdn-config-adopter@adobe.com** från ditt officiella e-post-ID med din feedback.

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över migreringsverktygen [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Kända fel {#known-issues}

* Det går inte att skicka Adaptiv Forms baserat på kärnkomponenter. Problemet inträffar för Adaptive Forms som byggts med Core Components version 2.0.38 - 2.0.60.

  För att lösa problemet. du kan gå över till Adaptive Form Core Components version 2.0.62 eller senare. Om du vill ange en version av adaptiva Forms Core-komponenter för din miljö anger du versioner av `core.forms.components.version`-, `core.forms.components.af.version`- och `core.wcm.components.version component`beroenden i ditt Forms as a Cloud Service-databas eller AEM Archetype-baserade projekt och distribuerar ändringarna till din Forms as a Cloud Service-miljö. Du hittar den senaste versionen av adaptiva Forms Core Components-beroenden i [Adaptive Forms Core Components Git-databasen](https://github.com/adobe/aem-core-forms-components#system-requirements).
