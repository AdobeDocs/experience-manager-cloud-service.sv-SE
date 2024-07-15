---
title: AEM Forms as a Cloud Service versionsinformation
description: Läs om nya funktioner, betaversioner, information om förhandsversioner med mera för AEM Forms as a Cloud Service.
exl-id: 35950b81-6e45-4a75-bd27-8c28fd68e42e
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '2003'
ht-degree: 1%

---


# [!DNL Experience Manager Forms] as a Cloud Service versionsinformation {#overview}

Adobe Experience Manager [!DNL AEM Forms] as a Cloud Service får kontinuerliga förbättringar. Besök sidan regelbundet för att hålla dig uppdaterad om den senaste utvecklingen. Sidan innehåller information om:

- Nya funktioner
- Förbättringar
- Funktioner i förhandsversionen
- Beta-funktioner
- Felkorrigeringar
- Inaktuell funktionalitet
- Specialinstruktioner
- Framtida planer för ändringar

>[!NOTE]
>
>Versionsinformation om alla andra AEM as a Cloud Service-komponenter finns i [Aktuell versionsinformation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

## 2021.10.0 {#sep-2021-10-0}

### Nyheter i [!DNL Forms] {#what-is-new-forms-oct-2021}

- **Analytics for Adaptive Forms**: Nu kan du samla in och spåra beteenden hos både inloggad och ej inloggad (anonym) via Adobe Analytics for Adaptive Forms för att samla in användarinsikter. Det hjälper er att fatta välgrundade beslut baserat på data för att förbättra användarupplevelsen.

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Forms] {#prerelease-features-forms-oct-2021}

- **Gör AEM arbetsflödesdata externt för säker bearbetning**: Du kan lagra processdata AEM arbetsflödesdata (AEM arbetsflödesvariabeldata) som innehåller känsliga SPD-element (Personal Data) i en kundhanterad databas för säker bearbetning. Dataelementen och arbetsflödesvariablerna lagras inte i AEM och hämtas på begäran från en kundhanterad databas när arbetsflödet bearbetas.

### Beta-funktioner i [!DNL Forms] {#sep-what-is-new-forms-oct-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [Kommunikations-API:er](aem-forms-cloud-service-communications.md) hjälper dig att kombinera en mall och XML-data för att generera utskriftsdokument i olika format. Med tjänsten kan du generera dokument i synkront läge och gruppläge. Med API:erna kan du skapa program som gör att du kan:

   - Generera dokument genom att fylla i mallfiler (PDF och XDP) med XML-data.
   - Generera utdataformulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.

Du kan skriva till [!DNL formscsbeta@adobe.com] för att registrera dig för betaprogrammet.

## 2021.9.0 {#sep-2021-09-0}

### Nyheter i [!DNL Forms] {#what-is-new-forms-sep-2021}

- **Använd Adobe Sign-roller i ett adaptivt formulär**: Adobe Sign för företags- och företagsnivåer har möjlighet att expandera rollerna för avtalsmottagare, utöver bara signeraren, så att de bättre motsvarar deras arbetsflödesbehov. Du kan nu [aktivera alla mottagare av avtal att konfigurera sin roll i ett anpassat formulär](working-with-adobe-sign.md#addsignerstoanadaptiveform) med signerare som standardroll.

- **Analytics for Adaptive Forms**: Nu kan du hämta in och [spåra användarbeteende med Adobe Analytics](integrate-aem-forms-with-adobe-analytics.md) for Adaptive Forms för att samla in användarinsikter. Det hjälper er att fatta välgrundade beslut baserat på data för att förbättra användarupplevelsen.

- **Anslut enkelt AEM Forms till Microsoft Dynamics och Salesforce**: Tjänsten tillhandahåller out of the box-datakällkonfiguration och datamodeller för Microsoft Dynamics och Salesforce, vilket gör det [snabbare och enklare för utvecklare att konfigurera Microsoft Dynamics och Salesforce som datakällor för ett anpassat formulär](configure-msdynamics-salesforce.md).

- **E-signera ett anpassat formulär med DocuSign:** [Du kan använda DocuSign för att e-signera ett anpassat formulär](integrate-docusign-adaptive-forms.md). Tjänsten tillhandahåller en anpassad skickaåtgärd för att använda DocuSign med ett adaptivt formulär.

### Beta-funktioner i [!DNL Forms] {#sep-what-is-new-forms-prerelease}

- **Enhetlig lagringskontakt:** Använd Enhetlig lagringskontakt för att externalisera processdata i kundhanterade databaser. Du kan t.ex. lagra AEM arbetsflödesdata (AEM arbetsflödesvariabeldata) som innehåller känsliga personuppgifter (SPD) i en kundhanterad databas.
  <!--* Enable Forms Portal's save and resume functionality and store adaptive forms drafts in a customer-managed data repository.-->

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [Kommunikations-API:er](aem-forms-cloud-service-communications.md) hjälper dig att kombinera XDP-mallar och XML-data för att generera utskriftsdokument i olika format. Med tjänsten kan du generera dokument i synkront läge. Med API:erna kan du skapa program som gör att du kan:
   - Generera dokument genom att fylla i mallfiler med XML-data.
   - Generera utdataformulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.
   - Generera PDF-filer från ett XFA-formulär i PDF och Adobe Acrobat-formulär.

Du kan skriva till [!DNL formscsbeta@adobe.com] för att registrera dig för betaprogrammet.

### Begränsningar {#limitations}

- Adobe Analytics kan bara spåra formulärdata för autentiserade användare.

<!--

### New features available in [!DNL Forms] prerelease channel {#prerelease-features-forms-sep-2021}

* **Forms Portal:**  In a typical forms-centric portal deployment scenario, forms development and portal development are two disjoint activities. While Form Designers design and store forms in a repository, Web Developers create a web application to list forms and handle submission of forms. Forms are copied over to the web tier as there is no communication between the forms repository and the web application.

  Such scenarios often result in management issues and production delays. For example, if there is a newer version of a form available in the repository, you need to replace the form on the web tier, modify the web application, and redeploy the form on the public site. Redeploying the web application might cause some server downtime. Typically, the server downtime is a planned activity and therefore the changes cannot be pushed to the public site instantaneously.

  AEM Forms provides portal components that reduce management overheads and production delays. The components equip Web Developers to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM). The form portal components allow you to add the following functionality:

  * List forms in customized layouts. Out of the box, List view and Card view are provided.

  * List published adaptive forms on an AEM Sites page.

  * Enable searching of forms based on a various criteria, such as form properties, metadata, and tags.

  * Lists drafts and submissions related to Adaptive Form created by user.

  -->

## 2021.8.0 {#aug-2021-08-0}

### Nyheter i [!DNL Forms] {#what-is-new-forms-aug-2021}

<!-- * Automated Forms Conversion service can [convert PDF Forms in Italian and Portuguese language](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) to Adaptive Forms. -->

- AEM Archetype-projekt för Forms as a Cloud Service innehåller nu [formulärdatamodeller för Microsoft Dynamics och Salesforce](setup-local-development-environment.md).

- **Acroform-based Document of Record**: AEM Forms as a Cloud Service stöder användning av [Adobe Acrobat Form PDF (Acroform PDF)](generate-document-of-record-for-non-xfa-based-adaptive-forms.md) som mall för arkivhandlingar förutom XFA-baserad formulärmall.

- **Microsoft Azure-datalageranslutning**: Nu kan du [ansluta formulärdatamodellen till Microsoft Azure Storage](configure-azure-storage.md). Med den kan du hämta och lagra adaptiva formulärdata till Microsoft Azure Storage som en BLOB.

### Beta-funktion i [!DNL Forms] {#aug-what-is-new-forms-prerelease}

- **Enhetlig lagringskontakt:** Använd Enhetlig lagringskontakt för att externalisera processdata i kundhanterade databaser. Du kan till exempel

   - Möjliggör Forms Portals funktioner för att spara och återuppta samt lagra adaptiva blankettutkast i ett kundhanterat datalager.
   - Lagra AEM arbetsflödesdata (AEM arbetsflödesvariabeldata) som innehåller känsliga personuppgifter (SPD) i en kundhanterad databas.

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [Kommunikations-API:er](aem-forms-cloud-service-communications.md) hjälper dig att kombinera XDP-mallar och XML-data för att generera utskriftsdokument i olika format. Med tjänsten kan du generera dokument i synkront läge. Med API:erna kan du skapa program som gör att du kan:
   - Generera dokument genom att fylla i mallfiler med XML-data.
   - Generera utdataformulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.
   - Generera PDF-filer från ett XFA-formulär i PDF och Adobe Acrobat-formulär.

Du kan skriva till [!DNL formscsbeta@adobe.com] för att registrera dig för betaprogrammet.

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Forms] {#prerelease-features-forms-aug-2021}

- **Använd Adobe Sign-roller i ett adaptivt formulär**: Adobe Sign för företags- och företagsnivåer har möjlighet att expandera rollerna för avtalsmottagare, utöver bara signeraren, så att de bättre motsvarar deras arbetsflödesbehov. Du kan nu [aktivera alla mottagare av avtal att konfigurera sin roll i ett anpassat formulär](working-with-adobe-sign.md#addsignerstoanadaptiveform) med signerare som standardroll.

- **Analytics for Adaptive Forms**: Nu kan du hämta in och spåra användarbeteende med Adobe Analytics for Adaptive Forms för att samla in användarinsikter. Det hjälper er att fatta välgrundade beslut baserat på data för att förbättra användarupplevelsen.

- **Anslut enkelt AEM Forms till Microsoft Dynamics och Salesforce**: Tjänsten tillhandahåller out of the box-datakällkonfiguration och datamodeller för Microsoft Dynamics och Salesforce, vilket gör det [snabbare och enklare för utvecklare att konfigurera Microsoft Dynamics och Salesforce som datakällor för ett anpassat formulär](configure-msdynamics-salesforce.md).

## 2021.7.0 {#july-2021-07-0}

### Nyheter i [!DNL Forms] {#july-what-is-new-forms}

- Du kan nu använda tjänsten Automated forms conversion för att [konvertera PDF forms på franska, tyska och spanska ](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) till anpassningsbara formulär.
- En separat panel har lagts till i mallredigeraren för att visa fel som rör adaptiva formulärkomponenter. Det bidrar till att konsolidera alla adaptiva formulärfel på en plats och minskar upplösningstiden.

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Forms] {#july-prerelease-features-forms}

- **Acrobat-baserat postdokument**: Du kan även [använda Adobe Acrobat Form PDF (Acrobat PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) som en mall för postdokument förutom XFA-baserad formulärmall.

- **Microsoft Azure-datalageranslutning**: Nu kan du [ansluta formulärdatamodellen till Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). Med den kan du hämta och lagra adaptiva formulärdata till Microsoft Azure Storage som en BLOB.

- **Variable Data Externalizer**: Du kan spara data AEM arbetsflödesvariabler i ett externt lagringssystem som hanteras av din organisation.

### Beta-funktion i [!DNL Forms] {#july-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [Kommunikations-API:er](aem-forms-cloud-service-communications.md) hjälper dig att kombinera XDP-mallar och XML-data för att generera utskriftsdokument i olika format. Med tjänsten kan du generera dokument i synkront läge. Med API:erna kan du skapa program som gör att du kan:
   - Generera dokument genom att fylla i mallfiler med XML-data.
   - Generera utdataformulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.
   - Generera PDF-filer från ett XFA-formulär i PDF och Adobe Acrobat-formulär.

## 2021.6.0 {#july-2021-06-0}

### Nyheter i [!DNL Forms] {#june-what-is-new-forms}

- Lagt till möjlighet att filtrera anpassade kolumner AEM Inkorgen.
- Lagt till möjlighet att använda temaredigeraren och stillagret i en adaptiv formulärredigerare för att formatera captcha-komponenten.
- Snabbare och exaktare för automatisk detektering av logiska avsnitt i PDF forms och konvertering av dessa till motsvarande adaptiva formulärpaneler.
- Flyttningsåtgärd har lagts till för att flytta en PDF- eller XDP-fil från en mapp till en annan.

### Beta-funktion i [!DNL Forms] {#june-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**: Kommunikations-API:er hjälper dig att kombinera XDP-mallar och XML-data för att generera utskriftsdokument i olika format. Med tjänsten kan du generera dokument i synkront läge. Med API:erna kan du skapa program som gör att du kan:

   - Generera slutliga formulärdokument genom att fylla i mallfiler med XML-data.
   - Generera utdataformulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.
   - Generera PDF från ett XFA-formulär i PDF och Adobe Acrobat-formulär (AcroForm).

- **Variable Data Externalizer**: Du kan spara data AEM arbetsflödesvariabler i ett externt lagringssystem som hanteras av din organisation.

Du kan skriva till [!DNL formscsbeta@adobe.com] för att registrera dig för betaprogrammet.

### Fel som har åtgärdats i [!DNL Forms] {#june-forms-bugs-fixed}

- När ett fält valideras innan data skickas till backend-tjänsten via FDM (Form Data Model), lyckas valideringen men tjänsten Form Data Model kan inte anropa eftervalideringen.
- När du skickar ett formulär som innehåller ett standardfält för överföring av HTML från en Apple iOS-enhet skickas ibland inte filens innehåll och en 0-byte-fil tas emot i den andra änden. Apple iOS 15.1 åtgärdar problemet.

## 2021.5.0 {#may-2021-05-0}

## [!DNL Adobe Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#may-what-is-new-forms}

- **Sammanhangsberoende hjälp**: En sammanhangsberoende hjälp har lagts till för adaptiv formulärredigerare, mallredigerare och temaredigerare för att hjälpa författare att förstå olika funktioner i redigerare.
- **Felmeddelanden i egenskapsläsaren**: Felmeddelanden har lagts till för varje egenskap i webbläsaren Adaptiva Forms-egenskaper. Dessa meddelanden hjälper till att förstå tillåtna värden för ett fält.

### Kommande betafunktion för [!DNL Forms] {#may-what-is-new-forms-prerelease}

Utdata som en molntjänst: Med Output Service kan du kombinera XDP-mallar och XML-data för att generera utskriftsdokument i olika format. Med tjänsten kan du generera dokument i synkront och asynkront gruppläge. Med Output Service kan du skapa program som gör att du kan:

- Generera slutliga formulärdokument genom att fylla i mallfiler med XML-data.
- Generera utdataformulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.
- Generera PDF från XFA-PDF.

Du kan skriva till formscsbeta@adobe.com och registrera dig för betaprogrammet.

### Fel som har åtgärdats i [!DNL Forms] {#may-forms-bugs-fixed}

- När du ersätter standardikonen för åtgärdsknapparna med en korallikon i ett steg Tilldela uppgift i AEM Forms Workflows slutar arbetsflödet att fungera och ett undantag loggas. Arbetsflödet fungerar som förväntat när standardikoner används.
- När du ändrar antalet kolumner i layoutlagret öppnar du redigeringslagret och drar några komponenter i en panel visas fyrkantiga blåa rutor i innehållsområdet i den adaptiva formulärredigeraren och redigeraren slutar svara.
- Felmeddelande om ett alternativ för regelredigering som är relaterat till att ange en URL för en adaptiv resurs eller en extern resurs är för lång och inte användarvänlig.

## 2021.4.0 {#april-2021-04-0}

### Nyheter i [!DNL Forms] {#april-what-is-new-forms}

- **Använd autentiseringsmetoden för myndighets-ID i Adobe Sign-aktiverade adaptiva Forms**

  Adobe Sign Government ID-process drivs av avancerade maskininlärningsalgoritmer och ger företag över hela världen möjlighet att säkra en högkvalitativ autentisering av mottagarens identitet. Nu kan du använda autentiseringsmetoden för myndighets-ID i Adobe Sign-aktiverade Adaptive Forms.

  Myndighets-ID är en autentiseringsmetod för premiumidentitet som instruerar mottagaren att [överföra bilden av ett myndighetsutfärdat identitetsdokument (körkort, nationellt ID, pass)](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html) och sedan utvärdera dokumentet för att säkerställa att det är autentiskt.

- **Stöd för signering i formulär för asynkrona, adaptiva formulärinskickade formulär**

  Nu kan du använda signeringsfunktionen i formulär för asynkrona, anpassningsbara formulärinskickade formulär. Du kan även bädda in ett anpassat formulär på en [!DNL Experience Manager Sites]-sida och använda signeringsfunktionen i formulär för att skicka formulär med adaptiv form.

- **Stöd för att använda en variabel för att ange en bifogad fil när ett adaptivt formulär fylls i i förväg för steget Tilldela uppgift**

  När du fyller i ett adaptivt formulär i förväg för steget Tilldela uppgift kan du nu använda en dokumenttypsvariabel för att välja en bifogad inmatning för det adaptiva formuläret.

- **Stöd för att använda det literala alternativet för att ange ett värde för en JSON-typvariabel**

  Du kan använda det literala alternativet för att ange ett värde för en JSON-typvariabel i det angivna variabelsteget i ett AEM arbetsflöde. Med alternativet literal kan du ange en JSON i form av en sträng.

- **Använd lokal utvecklingsmiljö för att skapa en DoR-fil (Document of Record)**

  Du kan använda en XDP-fil som en dokumentmall på Cloud Service och AEM Forms as a Cloud Service SDK (lokal utvecklingsmiljö). Tidigare var stödet begränsat till endast Cloud Service.

### Felkorrigeringar i [!DNL Forms] {#april-bug-fixes-forms}

- När ett anpassat formulär som inte har konfigurerats för att generera ett postdokument skickas till ett AEM arbetsflöde som har konfigurerats för att generera ett postdokument, visas inget felmeddelande och uppgiften kan inte skickas.
