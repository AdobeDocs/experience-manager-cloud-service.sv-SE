---
title: Versionsinformation för 2021.2.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
description: "[!DNL Adobe Experience Manager] as a Cloud Service Release Notes for 2021.2.0."
exl-id: 88dac54b-cc12-44a0-b429-6e691221f806
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 0%

---


# Versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Experience Manager] as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] as a Cloud Service 2021.2.0 är 25 februari 2021.
Följande version (2021.3.0) kommer att vara den 25 mars 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Headless Content Management {#headless}

* **[GraphQL API för leverans av innehållsfragment](/help/headless/graphql-api/content-fragments.md)**: Möjlighet att söka efter innehållsfragment med GraphQL-syntax och scheman baserade på Content Fragment-modeller för JSON-format.

* **[Autentiseringsstöd för GraphQL API-begäranden](/help/headless/security/authentication.md)**: Möjlighet att autentisera GraphQL API-begäranden med åtkomsttoken för API:er på serversidan.

* **[RemotePage-komponenten](/help/implementing/developing/hybrid/remote-page.md)**: Stöd för visning och redigering av externa SPA i AEM.

* **[Redigera en extern SPA i AEM](/help/implementing/developing/hybrid/editing-external-spa.md)**: Lagt till möjlighet att ladda upp ett fristående enkelsidigt program till en AEM, lägga till redigerbara innehållsavsnitt och aktivera redigering.

* Förbättrade JSON-utdata från GraphQL API, bland annat möjligheten att skapa RTF-text i JSON-format och -språk.

* Stöd för att kapsla modeller för innehållsfragment så att kapslade strukturer för innehållsfragment kan skapas, via särskilda datatyper för Content Fragment Reference eller textbundna referenser för innehållsfragment i flerradiga textfält.

* Ytterligare valideringsregler finns i datatyperna Content Fragment model, inklusive&quot;unique&quot;,&quot;required&quot; och&quot;translatable&quot;.

* Märk upp Content Fragment-modeller och tillåt att Content Fragment kan skapas i en mapp med profiler utifrån taggar eller sökvägar.

* Användbarhetsförbättringar i redigeraren för innehållsfragment, inklusive publiceringsåtgärd och visning av modell som ett fragment baseras på.

* Möjlighet att förhandsgranska JSON-utdata direkt i Content Fragment-redigeraren.

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] som [!DNL Cloud Service] {#assets}

## Nyheter i [!DNL Assets] {#what-is-new-assets}

* Resurser kan hämtas med [!DNL Experience Manager Assets Brand Portal]. Det hjälper er att skaffa resurser från byråanvändarna för nya marknadsföringskampanjer, fotografier och projekt.

* [!DNL Experience Manager Assets] som [!DNL Cloud Service] har rätt att ha en förkonfigurerad [!DNL Brand Portal] -instans. The [!DNL Cloud Manager] användare kan aktivera [!DNL Brand Portal] på [!DNL Experience Manager Assets] som [!DNL Cloud Service]. Se [aktivera Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=en).

* Företag kan nu skaffa resurser med [!DNL Brand Portal]. Funktionen för resurskälla använder [!DNL Brand Portal] för att hjälpa kunderna att interagera med byråanvändare för att skaffa resurser för nya marknadsföringskampanjer, fotografier och projekt. Se [resurskälla i [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html).

* The [!DNL Brand Portal] användningsrapporten visar nu endast de aktiva användarna. De inaktiva användarna visas inte nu. Aktiva användare är de vars konto har tilldelats en produktprofil i [!DNL Admin Console]. Se [[!DNL Brand Portal] rapporter](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html).

* I [!DNL Brand Portal], introduceras en ny hämtningsinställning som gör att du kan skapa separata mappar för varje resurs när du hämtar mappar, samlingar och så vidare. Se [hämtningsinställningar](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html).

## Felkorrigeringar i [!DNL Assets] {#bug-fixes-assets}

* När flera resurser har valts för att uppdatera egenskaperna inträffar ibland ett fel eller så uppdateras egenskaperna för en avmarkerad resurs. (CQ-4316532)
* Vid försök att öppna [!UICONTROL Assets Admin Search Rail]förblir sidan tom och klickar på [!UICONTROL Edit] > [!UICONTROL Settings] genererar ett fel. (CQ-4315079)
* När en ny version av en befintlig resurs skapas efter att namnkonflikten har lösts, skrivs metadata för den ursprungliga resursen över. (CQ-4313594)
* När en resurs med lång anteckningstext skrivs ut beskärs anteckningstexten, även om det finns utrymme. (CQ-4314101)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Vad är nytt? {#what-is-new-commerce}

* Product Experience Management: Berika katalogsidorna individuellt med Experience Fragments.

* Utökade egenskaper för produktkonsolen för att visa länkade resurser och upplevelsefragment, inklusive åtgärder för att snabbt navigera till det associerade innehållet.

* Lanserade CIF Venia Reference Site - 2021.02.24 som innehåller den senaste CIF Core Components version v1.8.0. Se [CIF Venias referenswebbplats](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24) för mer information.

* Frisläppta CIF-kärnkomponenter v1.8.0. Se [CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0) för mer information.

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.2.0 är 11 februari 2021.

### Vad är nytt? {#what-is-new-cloud-manager}


* Resurskunder kan nu välja när och var de ska distribuera sin Brand Portal-instans på ett självbetjäningssätt via användargränssnittet i Cloud Manager. För ett vanligt (icke-sandlådeprogram) program med Assets-lösning kan Brand Portal nu etableras i produktionsmiljön. Etableringen kan bara göras en gång i produktionsmiljön.

* Den AEM Project Archetype som används i Project och Sandbox Creation har uppdaterats till version 25.

* Listan med föråldrade API:er som identifieras vid kodskanning har förfinats så att den innehåller ytterligare klasser och metoder som har tagits bort i den senaste SDK-versionen av Cloud Servicen.

* SonarQube-profilen för Cloud Manager har uppdaterats för att ta bort Sonar-regelbläckfisk:S2142. Detta kommer inte längre att orsaka en konflikt med kontrollerna för trådavbrott.

* Molnhanterarens användargränssnitt informerar användaren som kanske inte kan lägga till/uppdatera domännamn för tillfället eftersom den associerade miljön antingen har en pågående pipeline kopplad till sig eller väntar på godkännandesteget.

* Egenskaper angivna i kunden `pom.xml` filer som har prefixats med sonar tas nu bort dynamiskt för att undvika fel i skapande och kvalitet vid skanning.

* Molnhanterarens användargränssnitt informerar användaren som kanske inte kan välja ett SSL-certifikat tillfälligt om det används av ett domännamn som för närvarande distribueras.

* Ytterligare regler för kodkvalitet har lagts till för att täcka problem med Cloud Servicens kompatibilitet.

### Felkorrigeringar {#bug-fixes-cloud-manager}

* Det är inte längre skiftlägeskänsligt att matcha SSL-certifikat mot ett domännamn.

* Molnhanterarens användargränssnitt informerar nu en användare om de privata certifikatnycklarna inte uppfyller 2048-bitarsgränsen med ett felmeddelande.

* Molnhanterarens användargränssnitt informerar användaren som kanske inte kan välja ett SSL-certifikat tillfälligt om det används av ett domännamn som för närvarande distribueras.

* I vissa fall kan ett internt problem leda till att miljön tas bort.

* En del pipeline-fel rapporterades felaktigt som pipeline-fel.

## Content Transfer Tool {#content-transfer-tool}

### Releasedatum {#release-date-ctt}

Releasedatum för innehållsöverföringsverktyget v1.2.4 är 10 februari 2021.

### Felkorrigeringar {#bug-fixes-ctt}

* Vid mappning av flera användare mappades vissa användares IMS-ID felaktigt. Den här har åtgärdats.

### Releasedatum {#release-date-ctt-feb}

Releasedatum för innehållsöverföringsverktyget v1.2.2 är 1 februari 2021.

### Nyheter i verktyget Innehållsöverföring {#what-is-new-ctt}

* Ny funktion och nytt användargränssnitt har lagts till i verktyget Innehållsöverföring - verktyget för användarmappning. Den här funktionen mappar automatiskt befintliga användare och grupper till deras Adobe Identity Management-system-ID som en del av innehållsmigreringsaktiviteten.
Se [Använda verktyget för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) för mer information.
* Verktyget Innehållsöverföring migrerar nu alla grupper och användare som det hänvisas till i migreringsuppsättningen, inklusive underordnade.
* Användare kan välja vissa sökvägar under `/etc` när du skapar migreringsuppsättningar.

## Best Practices Analyzer {#best-practices-analyzer}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.2 är 18 februari 2021.

### Nyheter i Best Practices Analyzer {#what-is-new-bpa}

* Möjlighet att upptäcka användning av AEM Forms och AEM Forms och ange områden som är relevanta för migrering till AEM Forms as a Cloud Service.
* Möjlighet att upptäcka och rapportera användning och antal anpassade komponenter och mallar.
* Möjlighet att identifiera vilken typ av nodarkiv och datalager som används.
* Möjlighet att upptäcka användningen av Dynamic Media.
* Möjlighet att identifiera den Java-version som används.

## Verktyg för omstrukturering av kod {#code-refactoring-tools}

### Nyheter i verktygen för kodkorrigering {#what-is-new-crt}

* Ny version av AIO-CLI-plugin släppt. Den senaste versionen av det här plugin-programmet innehåller flera felkorrigeringar för Repository Modernizer.
Se [Enhetlig upplevelse](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) om du vill veta mer om det här plugin-programmet.

### Felkorrigeringar {#bug-fixes-crt}

* Flera felkorrigeringar har gjorts i Repository Modernizer.
Se [GitHub-resurs: aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) för mer information.
