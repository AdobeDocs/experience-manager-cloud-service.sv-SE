---
title: Versionsinformation för version 2021.2.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: "[!DNL Adobe Experience Manager] as a Cloud Service versionsinformation för 2021.2.0."
exl-id: 88dac54b-cc12-44a0-b429-6e691221f806
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 0%

---


# Versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Experience Manager] as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] as a Cloud Service 2021.2.0 är 25 februari 2021.
Följande version (2021.3.0) kommer att vara den 25 mars 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Headless Content Management {#headless}

* **[GraphQL-API för leverans av innehållsfragment](/help/headless/graphql-api/content-fragments.md)**: Möjlighet att fråga innehållsfragment med GraphQL-syntax och scheman baserade på modeller av innehållsfragment för utdata i JSON-format.

* **[Autentiseringsstöd för GraphQL API-begäranden](/help/headless/security/authentication.md)**: Möjlighet att autentisera GraphQL API-begäranden med åtkomsttoken för API:er på serversidan.

* **[RemotePage-komponenten](/help/implementing/developing/hybrid/remote-page.md)**: Stöd har lagts till för att visa och redigera externa SPA i AEM.

* **[Redigera en extern SPA i AEM](/help/implementing/developing/hybrid/editing-external-spa.md)**: Lagt till möjlighet att överföra ett fristående enkelsidigt program till en AEM, lägga till redigerbara avsnitt med innehåll och aktivera redigering.

* Förbättrade JSON-utdata från GraphQL API, bland annat möjligheten att skapa RTF-text i JSON-format och -språk.

* Stöd för att kapsla modeller för innehållsfragment så att kapslade strukturer för innehållsfragment kan skapas, via särskilda datatyper för Content Fragment Reference eller textbundna referenser för innehållsfragment i flerradiga textfält.

* Ytterligare valideringsregler finns i datatyperna Content Fragment model, inklusive&quot;unique&quot;,&quot;required&quot; och&quot;translatable&quot;.

* Märk upp Content Fragment-modeller och tillåt att Content Fragment kan skapas i en mapp med profiler utifrån taggar eller sökvägar.

* Användbarhetsförbättringar i redigeraren för innehållsfragment, inklusive publiceringsåtgärd och visning av modell som ett fragment baseras på.

* Möjlighet att förhandsgranska JSON-utdata direkt i Content Fragment-redigeraren.

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/sites-console/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

## Nyheter i [!DNL Assets] {#what-is-new-assets}

* Assets kan hämtas med [!DNL Experience Manager Assets Brand Portal]. Det hjälper er att skaffa resurser från byråanvändarna för nya marknadsföringskampanjer, fotografier och projekt.

* [!DNL Experience Manager Assets] som [!DNL Cloud Service] har rätt att ha en förkonfigurerad [!DNL Brand Portal]-instans. [!DNL Cloud Manager]-användaren kan aktivera [!DNL Brand Portal] på [!DNL Experience Manager Assets] som [!DNL Cloud Service]. Se [aktivera Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=sv-SE).

* Företag kan nu hämta resurser med [!DNL Brand Portal]. Funktionen för resurskälla använder [!DNL Brand Portal] för att hjälpa kunder att interagera med byråanvändare för att hämta resurser för nya marknadsföringskampanjer, foton och projekt. Se [Resurshantering i [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=sv-SE).

* Användningsrapporten för [!DNL Brand Portal] visar nu endast de aktiva användarna. De inaktiva användarna visas inte nu. Aktiva användare är de vars konto har tilldelats en produktprofil i [!DNL Admin Console]. Se [[!DNL Brand Portal] rapporter](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html?lang=sv-SE).

* I [!DNL Brand Portal] introduceras en ny hämtningsinställning som gör att du kan skapa separata mappar för varje resurs när du hämtar mappar, samlingar och så vidare. Se [hämtningsinställningar](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html?lang=sv-SE).

## Felkorrigeringar i [!DNL Assets] {#bug-fixes-assets}

* När flera resurser har valts för att uppdatera egenskaperna inträffar ibland ett fel eller så uppdateras egenskaperna för en avmarkerad resurs. (CQ-4316532)
* När du försöker öppna [!UICONTROL Assets Admin Search Rail] är sidan tom och om du klickar på [!UICONTROL Edit] > [!UICONTROL Settings] genereras ett fel. (CQ-4315079)
* När en ny version av en befintlig resurs skapas efter att namnkonflikten har lösts, skrivs metadata för den ursprungliga resursen över. (CQ-4313594)
* När en resurs med lång anteckningstext skrivs ut beskärs anteckningstexten, även om det finns utrymme. (CQ-4314101)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Nyheter {#what-is-new-commerce}

* Product Experience Management: Berika katalogsidorna individuellt med Experience Fragments.

* Utökade egenskaper för produktkonsolen för att visa länkade Assets- och Experience Fragments, inklusive åtgärder för att snabbt navigera till associerat innehåll.

* Lanserade CIF Venia Reference Site - 2021.02.24 som innehåller den senaste CIF Core Components version v1.8.0. Mer information finns i [CIF Venedig-referenswebbplats](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24).

* Frisläppta CIF kärnkomponenter v1.8.0. Mer information finns i [CIF kärnkomponenter](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0).

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.2.0 är 11 februari 2021.

### Nyheter {#what-is-new-cloud-manager}


* Assets-kunder kan nu välja när och var de vill driftsätta Brand Portal-instansen via självbetjäning via Cloud Manager UI. Brand Portal kan nu etableras i produktionsmiljön för ett vanligt (icke-sandlådeprogram) program med Assets-lösning. Etableringen kan bara göras en gång i produktionsmiljön.

* Den AEM Project Archetype som används i Project och Sandbox Creation har uppdaterats till version 25.

* Listan med föråldrade API:er som identifieras vid kodskanning har förfinats så att den innehåller ytterligare klasser och metoder som har tagits bort i den senaste SDK-versionen av Cloud Servicen.

* SonarQube-profilen för Cloud Manager har uppdaterats för att ta bort Sonar rule squid:S2142. Detta kommer inte längre att orsaka en konflikt med kontrollerna för trådavbrott.

* Cloud Manager användargränssnitt informerar användaren som kanske inte kan lägga till/uppdatera domännamn tillfälligt eftersom den associerade miljön antingen har en pågående pipeline kopplad till sig eller som väntar på godkännande.

* Egenskaper som har angetts i kundens `pom.xml` filer som har prefixats med sonar tas nu bort dynamiskt för att undvika fel vid skapande och kvalitetskontroll.

* Cloud Manager användargränssnitt informerar användaren som kanske inte kan välja ett SSL-certifikat tillfälligt om det används av ett domännamn som för närvarande distribueras.

* Ytterligare regler för kodkvalitet har lagts till för att täcka problem med Cloud Servicens kompatibilitet.

### Felkorrigeringar {#bug-fixes-cloud-manager}

* Det är inte längre skiftlägeskänsligt att matcha SSL-certifikat mot ett domännamn.

* Cloud Manager användargränssnitt kommer nu att informera en användare om certifikatets privata nycklar inte uppfyller 2048-bitarsgränsen med ett felmeddelande.

* Cloud Manager användargränssnitt informerar användaren som kanske inte kan välja ett SSL-certifikat tillfälligt om det används av ett domännamn som för närvarande distribueras.

* I vissa fall kan ett internt problem leda till att miljön tas bort.

* En del pipeline-fel rapporterades felaktigt som pipeline-fel.

## Verktyget Innehållsöverföring {#content-transfer-tool}

### Releasedatum {#release-date-ctt}

Releasedatum för innehållsöverföringsverktyget v1.2.4 är 10 februari 2021.

### Felkorrigeringar {#bug-fixes-ctt}

* Vid mappning av flera användare mappades vissa användares IMS-ID felaktigt. Den här har åtgärdats.

### Releasedatum {#release-date-ctt-feb}

Releasedatum för innehållsöverföringsverktyget v1.2.2 är 1 februari 2021.

### Nyheter i verktyget Innehållsöverföring {#what-is-new-ctt}

* Ny funktion och nytt användargränssnitt har lagts till i verktyget Innehållsöverföring - verktyget för användarmappning. Den här funktionen mappar automatiskt befintliga användare och grupper till deras Adobe Identity Management-system-ID som en del av innehållsmigreringsaktiviteten.
Mer information finns i [Använda verktyget för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=sv-SE).
* Verktyget Innehållsöverföring migrerar nu alla grupper och användare som det hänvisas till i migreringsuppsättningen, inklusive underordnade.
* Användare kan välja vissa sökvägar under `/etc` när de skapar migreringsuppsättningar.

## Best Practices Analyzer {#best-practices-analyzer}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.2 är 18 februari 2021.

### Nyheter i Best Practices Analyzer {#what-is-new-bpa}

* Möjlighet att upptäcka användning av AEM Forms och AEM Forms och ange områden som är relevanta för migrering till AEM Forms as a Cloud Service.
* Möjlighet att upptäcka och rapportera om användning och antal anpassade komponenter och mallar.
* Möjlighet att identifiera vilken typ av nodarkiv och datalager som används.
* Möjlighet att upptäcka användningen av Dynamic Media.
* Möjlighet att identifiera den Java-version som används.

## Kodomfaktoriseringsverktyg {#code-refactoring-tools}

### Nyheter i verktygen för kodkorrigering {#what-is-new-crt}

* Ny version av AIO-CLI-plugin släppt. Den senaste versionen av det här plugin-programmet innehåller flera felkorrigeringar för Repository Modernizer.
Mer information om det här plugin-programmet finns i [Enhetlig upplevelse](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=sv-SE#benefits).

### Felkorrigeringar {#bug-fixes-crt}

* Flera felkorrigeringar har gjorts i Repository Modernizer.
Mer information finns i [GitHub-resurs: aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).
