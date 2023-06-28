---
title: Så här migrerar du från en AEM 6.5 Forms till [!DNL AEM Forms] as a Cloud Service miljö?
description: Migrera från en [!DNL AEM Forms] (On-Premise- och AMS-miljöer) till [!DNL AEM Forms] as a Cloud Service miljö.
keywords: 6.5-formulär till molntjänster, 6.5-formulär till cs, migrera 6.5-formulär till CS, migrera 6.5-formulär till molntjänsten, uppgradera 6.5-formulär till CS, flytta 6.5-formulär till CS, uppgradera AEM 6.5 till CS
contentOwner: khsingh
feature: Adaptive Forms
role: User, Developer
level: Intermediate
topic: Migration
exl-id: 090e77ff-62ec-40cb-8263-58720f3b7558
source-git-commit: f6b8ef52ad551be70e665a14ce00c197d1470e84
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 1%

---

# Migrera från en [!DNL AEM Forms] (On-Premise- och AMS-miljöer) till [!DNL AEM Forms] as a Cloud Service  {#Harden-your-AEM-Forms-as-a-Cloud-Service-environment}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/upgrade-aem-forms/upgrade.html) |
| AEM as a Cloud Service | Den här artikeln |

Du kan migrera eller uppgradera dina adaptiva Forms-konfigurationer, teman, mallar och molnkonfigurationer från <!-- AEM 6.3 Forms AEM 6.4 Forms on OSGi and --> AEM 6.5 Forms on OSGi to [!DNL AEM] as a Cloud Service. Innan du migrerar dessa resurser använder du migreringsverktyget för att konvertera det format som användes i de tidigare versionerna till det format som används i [!DNL AEM] as a Cloud Service. När du kör migreringsverktyget uppdateras följande resurser:

* Anpassade komponenter för Adaptive Forms
* Anpassningsbara Forms-mallar och teman
* Molnkonfigurationer
* Skript för kodredigeraren konverteras till återanvändbara funktioner och tillämpas på visuella regler.

## Överväganden att migrera till Forms as a Cloud Service {#consideration}

Om du vill migrera från AEM 6.5 Forms till AEM Cloud Service är det viktigt att ta hänsyn till följande punkter:

* Tjänsten hjälper dig att migrera innehåll endast från [!DNL AEM Forms] i OSGi-miljöer. Migrera innehåll från [!DNL AEM Forms] JEE till en Cloud Service-miljö stöds inte.

* (Endast för tidigare versioner än AEM 6.5 Forms) Adaptiv Forms baserad på färdiga mallar och teman i AEM 6.3 Forms eller tidigare versioner stöds inte i [!DNL AEM Forms] as a Cloud Service.

* Adobe Experience Manager Forms as a Cloud Service förändrar de befintliga funktionerna avsevärt jämfört med Adobe Experience Manager 6.5 Forms-miljöer (lokal och Adobe-hanterad tjänst). Innan du fortsätter med migreringen till tjänsten [läs mer om de här ändringarna](notable-changes.md) och [skillnader på funktionsnivå](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#viewing-report) för att bestämma sig för att migrera baserat på funktioner som din organisation behöver.




<!-- 
## Difference with AEM 6.5 Forms 

| Feature         | Difference with AEM 6.5 Forms    |
|--------------|-----------|
| HTML5 Forms (Mobile Forms)     | The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. |
| Adaptive Forms     | <li><b>XSD-Based Adaptive Forms:</b> The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. </li> <li><b> Adaptive Form templates:</b> Use build pipeline and corresponding Git repository of your program to import existing Adaptive Form templates. </li><li><b>Rule editor:</b> AEM Forms as a Cloud Service provides a hardened [Rule editor](rule-editor.md#visual-rule-editor). The code editor is not available on Forms as a Cloud Service. The migration utility helps you migrate your forms that have custom rules (created in code editor). The utility converts such rules into custom functions supported on Forms as a Cloud Service. You can use the reusable functions with Rule editor to continue obtaining results obtained with rule scripts  The `onSubmitError` or `onSubmitSuccess` functions are now available as actions the Rule Editor. </li> <li><b>Drafts and submissions:</b> The service does not retain metadata for drafts and submitted Adaptive Forms. </li> <li><b> Prefill Service:</b> By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server. </li><li><b>Submit actions:</b> The **Email as PDF** action is not available. The **Email** submit action provide options to send attachments and attach Document of Record (DoR) with email. </li>|
| Form Data Model | <li>Forms data model supports only HTTP and HTTPs endpoints to submit data. </li><li>Forms as a Cloud Service allows to use Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive, and services supporting general CRUD (Create, Read, Update, and Delete) operations as data stores. The service does not support JDBC connector, Mutual SSL for Rest connector, and x509 certificate-based authentication for SOAP data sources. </li>|
| Automated Forms Conversion Service     | The service does not provide meta-model for Automated Forms Conversion Service. You can [download it from Automated Forms Conversion Service documentation](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).|
|Configurations|<li>Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment. </li> <li>If you use custom bundles, recompile your code with latest version of adobe-aemfd-docmanager before using these bundles with Forms as a Cloud Service.</li> |
| Document Manipulation APIs (Assembler Service)| The service does not support operations dependent on other services or applications: <li>Conversion of documents in a non-PDF format to a PDF format is not supported. For example, Microsoft Word to PDF, Microsoft Excel to PDF, and HTML to PDF are not supported</li><li>Adobe Distiller-based conversions are not supported. For example, PostScript(PS) to PDF</li><li>Forms Service-based conversions are not supported. For example, XDP to PDF Forms.</li><li>The service does not support converting a Signed PDF or Transparent PDF to another PDF format.</li>| -->

## Förutsättningar {#prerequisites}

För att säkerställa en smidig övergång från AEM Forms 6.5 till AEM as a Cloud Service miljö är det viktigt att tänka på följande:

* Aktivera [Forms - digital registrering](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html?#editing-program) för Forms Cloud Service och [köra pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

  ![Resultat för torr körning](assets/enable-add-on.png)

* I en Cloud Service-miljö fungerar migreringsverktyget tillsammans med verktyget för användarmappning och verktyget för innehållsöverföring. Migreringsverktyget gör [!DNL AEM Forms] resurser som är kompatibla med Cloud Service och innehållsöverföringsverktyget migrerar innehållet från [!DNL AEM Forms] miljö till [!DNL AEM] as a Cloud Service miljö. Läs om processen för migreringsverktyget innan du använder det [flytta till AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/home.html). Processen har två verktyg:
   * [Verktyg för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration): Med verktyget för användarmappning kan du mappa dina användare med motsvarande Adobe IMS-användarkonton.
   * [Verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration): Med verktyget Innehållsöverföring kan du förbereda och överföra innehåll från en befintlig miljö till en Cloud Service-miljö. Det hjälper användarna att enkelt uppgradera från AEM Forms till molnmiljön.
* Konton med administratörsbehörighet för [!DNL AEM Forms] as a Cloud Service och lokal [!DNL AEM Forms] miljö.
* Hämta och installera Best Practice Analyzer, Content Transfer Tool och [!DNL AEM Forms] Migreringsverktyg från [Programdistributionsportal.](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)

* Kör [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration) och åtgärda det rapporterade problemet. Information om möjliga problem med migrering från Adobe Experience Manager Forms till Adobe Experience Manager Forms as a Cloud Service finns i [AEM för Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#viewing-report).


<!-- * Download the latest [compatibility package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases) for your [!DNL AEM Forms] version. -->




## Migrera [!DNL AEM 6.5 Forms] material till AEM Cloud Service {#use-the-migration-utility}

Utför följande steg för att göra [!DNL AEM Forms] resurser som är kompatibla med Cloud Service och överför dem till [!DNL AEM] as a Cloud Service miljö.

1. Skapa en [klona](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/correct-method-to-clone-the-aem-environment/qaq-p/363487) av din befintliga [!DNL AEM Forms] miljö.

   >[!NOTE]
   >
   > När du migrerar från 6.5 till molntjänsten rekommenderar vi att du använder den klonade miljön för att köra innehållsöverföringsverktyget och migreringsverktyget. Verktyget för innehållsöverföring och migreringsverktyget gör några ändringar i innehåll och resurser. Kör alltså inte Content Transfer Tool och Migration Utility i en produktionsmiljö.

1. Logga in i din klonade miljö med administratörsbehörighet.

1. Kör [Verktyg för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration) för att mappa dina användare med motsvarande Adobe IMS-användarkonton. Du måste ha Adobe IMS-användarkonton för att kunna logga in på en [!DNL AEM Forms] as a Cloud Service instans.

1. Hämta och installera [Verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) och [!DNL AEM Forms] as a Cloud Service migreringsverktyg från [Programdistributionsportal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) i den klonade miljön. Du kan använda AEM Package Manager för att installera verktyget och verktyget.

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Content Migration]**.

1. Öppna **[!UICONTROL Prepare Forms for migration]** kort. Webbläsaren visar fem alternativ:
   * **[!UICONTROL AEM Forms Assets Migration]**
   * **[!UICONTROL Adaptive Forms Custom Components Migration]**
   * **[!UICONTROL Adaptive Forms Templates Migration]**
   * **[!UICONTROL AEM Forms Cloud Configurations Migration]**
   * **[!UICONTROL Code Editor Script Migration]**

1. Använd alternativet en efter en för att skapa [!DNL AEM Forms] resurser som är kompatibla med [!DNL AEM] as a Cloud Service:

   1. Tryck **[!UICONTROL AEM Forms Assets Migration]** och på nästa skärm trycker du **[!UICONTROL Start Migration]**. Det gör Adaptiv Forms och teman på dina [!DNL AEM Forms] miljö kompatibel med [!DNL AEM] as a Cloud Service .

   1. Tryck **[!UICONTROL Adaptive Forms Custom Components Migration]** och på sidan för migrering av anpassade komponenter trycker du på **[!UICONTROL Start Migration]**. Den gör alla anpassade komponenter som utvecklats för Adaptive Forms och komponentövertäckningar på din [!DNL AEM Forms] miljö kompatibel med [!DNL AEM] as a Cloud Service .

   1. Tryck **[!UICONTROL Adaptive Forms Template Migration]** och på sidan för migrering av anpassade komponenter trycker du på **[!UICONTROL Start Migration]**. Det gör adaptiva formulärmallar på `/apps` eller `/conf` som skapats med AEM mallredigerare kompatibel med [!DNL AEM] as a Cloud Service .

   1. Tryck **[!UICONTROL AEM Forms Cloud Configurations Migration]** och tryck sedan på **[!UICONTROL Start Migration]**. Den uppdaterar och flyttar följande Cloud Services till en ny plats:

      * Cloud Service för formulärdatamodell
      * Google reCAPTCHA-Cloud Service
      * [!DNL Adobe Sign] Cloud Service
      * Adobe Fonts Cloud Service

   1. Tryck **[!UICONTROL Code Editor Script Migration]**, ange var återanvändbara funktioner ska sparas och tryck på **[!UICONTROL Start Migration].

   Cloud Servicen stöder inte regelredigeringsskript. The **[!UICONTROL Code editor script migration]** används för att konvertera alla regelskript i miljön till återanvändbara funktioner och de återanvändbara funktionerna används i den visuella redigeraren på lämplig plats. Dessa återanvändbara funktioner sparas i form av klientbibliotek och hjälper dig att behålla befintliga funktioner intakta. Verktyget tillämpar automatiskt de genererade återanvändbara funktionerna på motsvarande Adaptive Forms.

   Använd [Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement) om du vill exportera återanvändbara funktioner (klientbibliotek) till ett paket.

1. [Distribuera](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying-content-packages-via-cloud-manager-and-package-manager) paketet med återanvändbara funktioner (Client Libraries), [egen kod, komponenter, konfigurationer](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html#cloud-manager), anpassade språkspecifika bibliotek till [!DNL AEM] as a Cloud Service miljö.

   <!-- 1. Install the latest [Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) to your cloned [!DNL AEM Forms] environment. -->

1. Kör [Verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration). När du anger parametrar på **[!UICONTROL Create Migration Set]** ska du ange sökvägen till Adaptive Forms, teman, mallar, formulärdatamodeller, Cloud Services, anpassade komponenter och andra AEM Forms-specifika resurser till **[!UICONTROL Paths to be included]** alternativ. Den lägger till angivna [!DNL AEM Forms] resurser till migreringsuppsättning.

## Sökvägar för olika AEM Forms-specifika resurser

När du migrerar från AEM Forms 6.5 till molntjänsten kan du hitta de AEM Forms-specifika resurserna på:

* **Adaptiv Forms**: Adaptiva formulär finns på `/content/dam/formsanddocuments/`och `/content/forms/af`. För ett adaptivt formulär med namnet WKND Registration kan du till exempel lägga till banor `/content/dam/formsanddocuments/wknd-registration` och `/content/forms/af/wknd-registration`.
* **Formulärdatamodell**: Du hittar alla formulärdatamodeller på `/content/dam/formsanddocuments-fdm`. Till exempel, `/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`.

* **Klientbibliotek**: Standardsökvägen för klientbibliotek är `/etc/clientlibs/fd/theme`.

* **Adaptiva formulärmallar**: Standardsökvägen för mallar är `/conf/<template folder>`. Exempel: för en mall med namnet grundläggande sökväg `/conf/ReferenceEditableTemplates/settings/wcm/templates/basic`.

* **Adaptiva formulärteman och klientbibliotek**: Standardsökvägen för teman är ` /content/dam/formsanddocuments-themes/` och standardsökvägen för klientbibliotek är `/etc/clientlibs/fd/theme`. Exempel: för en mall med namnet WKND-tema lägger du till sökväg ` /content/dam/formsanddocuments-themes/wkndtheme` och klientbibliotek för temat på `/etc/clientlibs/reference-themes/wkndtheme-3-0`. Du kan också ha teman och klientbibliotek på andra anpassade sökvägar.

* **Molnkonfigurationer**: Du hittar molnkonfigurationer på `/conf/`. Molnkonfigurationen för formulärdatamodellen finns till exempel på `/conf/global/settings/cloudconfigs/fdm`.

* **Arbetsflödesmodell**: Du hittar AEM arbetsflödesmodeller på `/conf/global/settings/workflow/models/`. Exempel: för en arbetsflödesmodell med namnet WKND Registration, lägg till sökväg `/conf/global/settings/workflow/models/wknd-registration`

Du kan lägga till mappsökvägar på den översta nivån som listas nedan eller särskilda mappsökvägar som beskrivs nedan. Det gör att du kan migrera en viss resurs och alla resurser och formulär samtidigt när du uppgraderar till molntjänsten från AEM formulär 6.5.

* `/content/dam/formsanddocuments-fdm`
* `/content/dam/formsanddocuments/themes`
* `/content/forms/af`
* `/etc/clientlibs/fd/theme`

Om du vill migrera AEM arbetsflödesmodeller anger du följande sökvägar:

* `/conf/global/settings/workflow/models/`
* `/conf/global/settings/workflow/launcher`
* `/var/workflow/models`

## Se nästa

* [Betydande förändringar för befintliga användare av Adobe Experience Manager 6.5 Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/notable-changes.html)
* [Anmäl dig till AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-forms-cloud-service.html)
* [Skapa ditt första adaptiva formulär på Cloud Servicen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html)

## Ytterligare information

Med migreringsverktyget kan du migrera adaptiva Forms baserat på grundläggande komponenter. Dessutom har Forms as a Cloud Service stöd för adaptiva Forms Core-komponenter. Så du kan:

* [Skapa grundläggande komponentbaserad fristående adaptiv Forms](/help/forms/creating-adaptive-form-core-components.md)
* [Skapa grundkomponentbaserade adaptiva formulär direkt på en AEM Sites-sida](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

Om du vill veta mer om AEM Forms as a Cloud Service kan du läsa:

* [Introduktion till AEM Forms Cloud Service](/help/forms/home.md)
* [Nyheter i AEM Forms Cloud Service](/help/forms/latest-innovations.md)