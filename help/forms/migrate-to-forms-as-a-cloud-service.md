---
title: Hur kan vi migrera från AEM 6.5 Forms till AEM Forms as a Cloud Service?
description: Komma igång med migreringsresan till AEM as a Cloud Service | Adobe Experience Manager. Migrera från en  [!DNL AEM Forms] (On-Premise- och AMS-miljö) till en  [!DNL AEM Forms] as a Cloud Service miljö.
Keywords: 6.5 forms to cloud service, 6.5 forms to cs, migrate 6.5 forms to CS, migrate 6.5 forms to cloud service, upgrade 6.5 forms to CS, move 6.5 forms to CS, upgrade AEM 6.5 to CS, AEM Forms 6.5 to Cloud Service, AEM form migration to cloud service, Migration Journey to AEM as a Cloud Service | Adobe Experience Manager.
contentOwner: khsingh
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
topic: Migration
exl-id: 090e77ff-62ec-40cb-8263-58720f3b7558
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 0%

---

# Migrera från en [!DNL AEM Forms] (lokal miljö och AMS-miljö) till [!DNL AEM Forms] as a Cloud Service  {#Harden-your-AEM-Forms-as-a-Cloud-Service-environment}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/upgrade-aem-forms/upgrade.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |

Du kan migrera eller uppgradera dina adaptiva Forms, teman, mallar och molnkonfigurationer från <!-- AEM 6.3 Forms AEM 6.4 Forms on OSGi and --> AEM 6.5 Forms i OSGi till [!DNL AEM] as a Cloud Service. Innan du migrerar dessa resurser använder du migreringsverktyget för att konvertera det format som används i tidigare versioner till det format som används i [!DNL AEM] as a Cloud Service.
Låt oss komma igång med migreringsresan till AEM as a Cloud Service | Adobe Experience Manager. När du kör migreringsverktyget uppdateras följande resurser:

* Anpassade komponenter för Adaptive Forms
* Anpassningsbara Forms-mallar och teman
* Molnkonfigurationer
* Skript för kodredigeraren konverteras till återanvändbara funktioner och tillämpas på visuella regler.

## Överväganden att migrera till Forms as a Cloud Service {#consideration}

Om du vill migrera från AEM 6.5 Forms till AEM Cloud Service är det viktigt att tänka på följande:

* Tjänsten hjälper dig att migrera innehåll från endast [!DNL AEM Forms] i OSGi-miljöer. Migrering av innehåll från [!DNL AEM Forms] på JEE till en Cloud Service-miljö stöds inte.

* (Endast för tidigare versioner än AEM 6.5 Forms) Adaptiv Forms som baseras på färdiga mallar och teman i AEM 6.3 Forms eller tidigare versioner stöds inte på [!DNL AEM Forms] as a Cloud Service.

* Adobe Experience Manager Forms as a Cloud Service förändrar de befintliga funktionerna avsevärt jämfört med Adobe Experience Manager 6.5 Forms-miljöer (lokal och Adobe-hanterad tjänst). Innan du fortsätter med migreringen till tjänsten kan du [lära dig mer om de här ändringarna](notable-changes.md) och skillnaderna på [funktionsnivå](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=sv-SE#viewing-report) för att bestämma dig för att migrera baserat på funktioner som din organisation kräver.




<!-- 
## Difference with AEM 6.5 Forms 

| Feature         | Difference with AEM 6.5 Forms    |
|--------------|-----------|
| HTML5 Forms (Mobile Forms)     | The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. |
| Adaptive Forms     | <li><b>XSD-Based Adaptive Forms:</b> The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. </li> <li><b> Adaptive Form templates:</b> Use build pipeline and corresponding Git repository of your program to import existing Adaptive Form templates. </li><li><b>Rule editor:</b> AEM Forms as a Cloud Service provides a hardened [Rule editor](rule-editor.md#visual-rule-editor). The code editor is not available on Forms as a Cloud Service. The migration utility helps you migrate your forms that have custom rules (created in code editor). The utility converts such rules into custom functions supported on Forms as a Cloud Service. You can use the reusable functions with Rule editor to continue obtaining results obtained with rule scripts  The `onSubmitError` or `onSubmitSuccess` functions are now available as actions the Rule Editor. </li> <li><b>Drafts and submissions:</b> The service does not retain metadata for drafts and submitted Adaptive Forms. </li> <li><b> Prefill Service:</b> By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server. </li><li><b>Submit actions:</b> The **Email as PDF** action is not available. The **Email** submit action provide options to send attachments and attach Document of Record (DoR) with email. </li>|
| Form Data Model | <li>Forms data model supports only HTTP and HTTPs endpoints to submit data. </li><li>Forms as a Cloud Service allows to use Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive, and services supporting general CRUD (Create, Read, Update, and Delete) operations as data stores. The service does not support JDBC connector, Mutual SSL for Rest connector, and x509 certificate-based authentication for SOAP data sources. </li>|
| Automated Forms Conversion Service     | The service does not provide meta-model for Automated Forms Conversion Service. You can [download it from Automated Forms Conversion Service documentation](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=sv-SE#default-meta-model).|
|Configurations|<li>Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=sv-SE#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment. </li> <li>If you use custom bundles, recompile your code with latest version of adobe-aemfd-docmanager before using these bundles with Forms as a Cloud Service.</li> |
| Document Manipulation APIs (Assembler Service)| The service does not support operations dependent on other services or applications: <li>Conversion of documents in a non-PDF format to a PDF format is not supported. For example, Microsoft Word to PDF, Microsoft Excel to PDF, and HTML to PDF are not supported</li><li>Adobe Distiller-based conversions are not supported. For example, PostScript(PS) to PDF</li><li>Forms Service-based conversions are not supported. For example, XDP to PDF Forms.</li><li>The service does not support converting a Signed PDF or Transparent PDF to another PDF format.</li>| -->

## Förutsättningar {#prerequisites}

För att övergången från AEM Forms 6.5 till AEM as a Cloud Service ska bli så smidig som möjligt är det viktigt att tänka på följande:

* Aktivera alternativet [Forms - digital registrering](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html?lang=sv-SE&#editing-program) för ditt Forms Cloud Service-program och [kör pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=sv-SE).

  ![Resultat för torr körning](assets/enable-add-on.png)

* I en Cloud Service-miljö fungerar migreringsverktyget tillsammans med verktyget Innehållsöverföring. Migreringsverktyget gör [!DNL AEM Forms]-resurser kompatibla med Cloud Service och innehållsöverföringsverktyget migrerar innehållet från din [!DNL AEM Forms]-miljö till en [!DNL AEM] as a Cloud Service miljö. Läs om processen för att [flytta till AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/home.html?lang=sv-SE) innan du använder migreringsverktyget. Processen använder följande verktyg:
   * [Verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=sv-SE&#cloud-migration): Med verktyget Innehållsöverföring kan du förbereda och överföra innehåll från en befintlig miljö till en Cloud Service. Det hjälper användarna att enkelt uppgradera från AEM Forms till molnmiljön.
* Konton med administratörsbehörighet för [!DNL AEM Forms] as a Cloud Service och din lokala [!DNL AEM Forms]-miljö.
* Hämta och installera Best Practice Analyzer, Content Transfer Tool och [!DNL AEM Forms] Migration Utility från [Software Distribution Portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

* Kör verktyget [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=sv-SE#cloud-migration) och åtgärda det rapporterade problemet. Information om möjliga problem med migrering från Adobe Experience Manager Forms till Adobe Experience Manager Forms as a Cloud Service finns i [AEM Mönsteridentifiering för Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=sv-SE#viewing-report).


<!-- * Download the latest [compatibility package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=sv-SE#aem-65-forms-releases) for your [!DNL AEM Forms] version. -->




## Migrera [!DNL AEM 6.5 Forms] resurser till AEM Cloud Service {#use-the-migration-utility}

Utför följande steg för att göra dina [!DNL AEM Forms]-resurser kompatibla med Cloud Service och överför dem till en [!DNL AEM] as a Cloud Service miljö.

1. Skapa en [klon](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/correct-method-to-clone-the-aem-environment/qaq-p/363487) av din befintliga [!DNL AEM Forms]-miljö.

   >[!NOTE]
   >
   > När du migrerar från 6.5 till molntjänsten rekommenderar vi att du använder en klonad miljö för att köra innehållsöverföringsverktyget och migreringsverktyget. Verktyget för innehållsöverföring och migreringsverktyget gör några ändringar i innehåll och resurser. Kör alltså inte Content Transfer Tool eller Migration Utility i en produktionsmiljö.

1. Logga in i din klonade miljö med administratörsbehörighet.

1. Hämta och installera [verktyget för innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=sv-SE&#cloud-migration) och [!DNL AEM Forms] verktyget för as a Cloud Service migrering från [portalen för programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) i den klonade miljön. Du kan använda AEM Package Manager för att installera verktyget och verktyget.

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Content Migration]**.

1. Öppna kortet **[!UICONTROL Prepare Forms for migration]**. Webbläsaren visar fem alternativ:
   * **[!UICONTROL AEM Forms Assets Migration]**
   * **[!UICONTROL Adaptive Forms Custom Components Migration]**
   * **[!UICONTROL Adaptive Forms Templates Migration]**
   * **[!UICONTROL AEM Forms Cloud Configurations Migration]**
   * **[!UICONTROL Code Editor Script Migration]**

1. Använd alternativet efter varandra för att göra dina [!DNL AEM Forms]-resurser kompatibla med [!DNL AEM] as a Cloud Service:

   1. Välj **[!UICONTROL AEM Forms Assets Migration]** och välj **[!UICONTROL Start Migration]** på nästa skärm. Det gör Adaptiv Forms och teman i din [!DNL AEM Forms]-miljö kompatibla med [!DNL AEM] as a Cloud Service.

   1. Välj **[!UICONTROL Adaptive Forms Custom Components Migration]** och välj **[!UICONTROL Start Migration]** på sidan Anpassad komponentmigrering. Den gör alla anpassade komponenter som utvecklats för Adaptiv Forms och komponentövertäckningar i din [!DNL AEM Forms]-miljö kompatibla med [!DNL AEM] as a Cloud Service.

   1. Välj **[!UICONTROL Adaptive Forms Template Migration]** och välj **[!UICONTROL Start Migration]** på sidan Anpassad komponentmigrering. Den gör adaptiva formulärmallar på `/apps` eller `/conf` och som skapats med AEM mallredigerare kompatibla med [!DNL AEM] as a Cloud Service.

   1. Välj **[!UICONTROL AEM Forms Cloud Configurations Migration]** och sedan **[!UICONTROL Start Migration]** på sidan Konfigurationsmigrering. Den uppdaterar och flyttar följande Cloud Service till en ny plats:

      * Cloud Service för formulärdatamodell
      * Google reCAPTCHA-Cloud Service
      * Cloud Servicen [!DNL Adobe Sign]
      * Adobe Fonts Cloud Service

   1. Välj **[!UICONTROL Code Editor Script Migration]**, ange en plats där återanvändbara funktioner ska sparas och välj **[!UICONTROL Start Migration].

   Cloud Servicen stöder inte regelredigeringsskript. Verktyget **[!UICONTROL Code editor script migration]** konverterar alla regelskript i miljön till återanvändbara funktioner och tillämpar återanvändbara funktioner på den visuella redigeraren på lämplig plats. Dessa återanvändbara funktioner sparas i form av klientbibliotek och hjälper dig att behålla befintliga funktioner intakta. Verktyget tillämpar automatiskt de genererade återanvändbara funktionerna på motsvarande Adaptive Forms.

   AEM formulärmigrering till Cloud Servicen använder du [pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=sv-SE#contentmanagement) för att exportera återanvändbara funktioner (klientbibliotek) till ett paket.

1. [Distribuera](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=sv-SE#deploying-content-packages-via-cloud-manager-and-package-manager) det återanvändbara funktionspaketet (klientbibliotek), [anpassad kod, komponenter, konfigurationer](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html?lang=sv-SE#cloud-manager), anpassade språkspecifika bibliotek till din [!DNL AEM]-as a Cloud Service miljö.

   <!-- 1. Install the latest [Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=sv-SE&#cloud-migration) to your cloned [!DNL AEM Forms] environment. -->

1. Kör verktyget [Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=sv-SE&#cloud-migration). När du anger parametrar på skärmen **[!UICONTROL Create Migration Set]** anger du sökvägen till Adaptiv Forms, teman, mallar, formulärdatamodell (FDM), Cloud Service, anpassade komponenter och andra AEM Forms-specifika resurser till alternativet **[!UICONTROL Paths to be included]**. Det lägger till angivna [!DNL AEM Forms] resurser i migreringsuppsättningen.

## Sökvägar för olika AEM Forms-specifika resurser

När du migrerar från AEM Forms 6.5 till molntjänsten kan du hitta de AEM Forms-specifika resurserna på:

* **Adaptiv Forms**: Du kan hitta adaptiva formulär på `/content/dam/formsanddocuments/` och `/content/forms/af`. För ett adaptivt formulär med namnet WKND Registration läggs till sökvägarna `/content/dam/formsanddocuments/wknd-registration` och `/content/forms/af/wknd-registration`.
* **Formulärdatamodell**: Du kan hitta alla formulärdatamodeller (FDM) på `/content/dam/formsanddocuments-fdm`. Exempel: `/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`.

* **Klientbibliotek**: Standardsökvägen för klientbibliotek är `/etc/clientlibs/fd/theme`.

* **Adaptiva formulärmallar**: Standardsökvägen för mallar är `/conf/<template folder>`. Exempel: för en mall med namnet grundläggande tilläggssökväg `/conf/ReferenceEditableTemplates/settings/wcm/templates/basic`.

* **Adaptiva formulärteman och klientbibliotek**: Standardsökvägen för teman är ` /content/dam/formsanddocuments-themes/` och standardsökvägen för klientbibliotek är `/etc/clientlibs/fd/theme`. För en mall med namnet WKND-tema lägger du till sökvägen ` /content/dam/formsanddocuments-themes/wkndtheme` och klientbibliotek för temat på `/etc/clientlibs/reference-themes/wkndtheme-3-0`. Du kan också ha teman och klientbibliotek på andra anpassade sökvägar.

* **Molnkonfigurationer**: Du hittar molnkonfigurationer på `/conf/`. Molnkonfigurationen för formulärdatamodell (FDM) är till exempel `/conf/global/settings/cloudconfigs/fdm`.

* **Arbetsflödesmodell**: Du hittar AEM arbetsflödesmodeller på `/conf/global/settings/workflow/models/`. Exempel: för en arbetsflödesmodell med namnet WKND Registration, lägg till sökvägen `/conf/global/settings/workflow/models/wknd-registration`

Du kan lägga till mappsökvägar på den översta nivån som listas nedan eller särskilda mappsökvägar som beskrivs nedan. Det gör att du kan migrera en viss resurs och alla resurser och formulär samtidigt när du uppgraderar till molntjänsten från AEM formulär 6.5.

* `/content/dam/formsanddocuments-fdm`
* `/content/dam/formsanddocuments/themes`
* `/content/forms/af`
* `/etc/clientlibs/fd/theme`

När du migrerar AEM arbetsflödesmodeller från AEM Forms 6.5 till Cloud Service anger du följande sökvägar:

* `/conf/global/settings/workflow/models/`
* `/conf/global/settings/workflow/launcher`
* `/var/workflow/models`

## Se nästa

* [Observerbara ändringar för befintliga Adobe Experience Manager 6.5 Forms-användare](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/notable-changes.html?lang=sv-SE)
* [Anmäl dig till AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-forms-cloud-service.html?lang=sv-SE)
* [Skapa ditt första adaptiva formulär på Cloud Servicen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html?lang=sv-SE)

## Ytterligare information

Med migreringsverktyget kan du migrera adaptiva Forms baserat på grundläggande komponenter. Dessutom har Forms as a Cloud Service stöd för adaptiva Forms Core-komponenter. Så du kan:

* [Skapa grundläggande komponentbaserad fristående adaptiv Forms](/help/forms/creating-adaptive-form-core-components.md)
* [Skapa grundkomponentbaserade adaptiva formulär direkt på en AEM Sites-sida](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

Läs mer om AEM Forms as a Cloud Service:

* [Introduktion till AEM Forms Cloud Service](/help/forms/home.md)
* [Nyheter i AEM Forms Cloud Service](/help/forms/latest-innovations.md)