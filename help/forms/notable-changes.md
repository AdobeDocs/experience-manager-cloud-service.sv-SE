---
title: Vad har ändrats mellan AEM 6.5 Forms och AEM Cloud Services
description: Använder du Experience Manager Forms och vill uppgradera till Adobe Experience Manager Forms as a Cloud Service? Lär dig de mest framträdande förändringarna innan du uppgraderar eller migrerar till Cloud Servicen.
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: da53f453b0f2def98d92aae0e3e92d13eb748dab
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 0%

---

# Betydande förändringar för befintliga användare av Adobe Experience Manager 6.5 Forms  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Service förändrar de befintliga funktionerna avsevärt jämfört med Adobe Experience Manager Forms On-Premise och [!DNL Adobe-Managed Service] miljöer. De viktigaste skillnaderna anges nedan:

| Funktion/kapacitet | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms |
|---|---|---|
| Molnbaserad arkitektur | ✅ | ⛌ |
| Automatisk skalning baserad på inläsning | ✅ | ⛌ |
| Ingen driftstopp för uppgraderingar | ✅ | ⛌ |
| Frekvens för utrullning av funktioner | Agile* | Kvartalsvis |
| CDN (content delivery network) ingår | ✅ | ⛌ |
| Topologier som optimerats för maximal flexibilitet och effektivitet | ✅ | ⛌ |
| Molnbaserad utvecklingsmiljö | ✅ | ⛌ |
| Självbetjäning via Cloud Manager | ✅ | ⛌ |
| Automatiserade uppgraderingar med Continuous Integration och Continuous Delivery (CI/CD) | ✅ | ⛌ |
| Integration med [!DNL Micosoft Power Automate] | ✅ | ⛌ |
| Integration med [!DNL DocuSign] | ✅ | ⛌ |
| Enkel anslutning till Microsoft Dynamics och Salesforce | ✅ | ⛌ |
| Enkel anslutning till Microsoft Azure-datalager | ✅ | ⛌ |
| Tydligare regelredigerare | ✅ | ⛌ |
| Guiden Skapa formulär | ✅ | ⛌ |
| Anpassat XCI-stöd för arkivhandlingar | ✅ | ⛌ |
| Adaptiv Forms <sup>1</sup> | ✅ | ✅ |
| Dataintegrering med flera datakällor | ✅ | ✅ |
| Kommunikations-API:er (Document Services) <sup>2,3</sup> | ✅ | ✅ |
| Tjänsten Automated forms conversion <sup>4</sup> | ✅ | ✅ |
| Integration med [!DNL Adobe Sign] | ✅ | ✅ |
| Integration med [!DNL AEM Sites] | ✅ | ✅ |
| Integration med [!DNL Adobe Launch] | ✅ | ✅ |
| Integration med [!DNL Adobe Analytics] | ✅ | ✅ |
| Forms Portal <sup>5</sup> | ✅ | ✅ |
| AEM | ✅ | ✅ |
| Dokument | ✅ | ✅ |
| Osynlig Captcha | ✅ | ✅ |
| Återanvändbara konfigurationer av formulärdatamodell | ✅ | ✅ |
| Acroform-based Document of Record | ✅ | ✅ |
| Myndighets-ID-baserad identitetsautentisering för Adobe Sign-aktiverad Adaptive Forms | ✅ | ✅ |
| HTML5 <sup>6</sup> | ⛌ | ✅ |
| Dokumentsäkerhet | ⛌ | ✅ |

Innan du fortsätter med tjänsten bör du ta hänsyn till följande exceptionella fall:

+++ 1. Adaptiv Forms

* **XSD-baserad, adaptiv Forms:** Tjänsten stöder inte HTML5 Forms (Mobile Forms). Om du återger dina XDP-baserade formulär som HTML5 Forms kan du fortsätta använda funktionen i AEM 6.5 Forms. Du kan använda XDP-mall för att utforma en mall för Dokument för post. Tjänsten stöder inte XFA-baserad Adaptive Forms
* **Importera adaptiva formulärmallar:** Använd byggpipeline och motsvarande Git-databas i programmet för att importera befintliga adaptiva formulärmallar.
* **Regelredigerare:** AEM Forms as a Cloud Service har en härdad [Regelredigerare](rule-editor.md#visual-rule-editor). Kodredigeraren är inte tillgänglig på Forms as a Cloud Service. Migreringsverktyget hjälper dig att migrera formulär som har anpassade regler (skapade i kodredigeraren). Verktyget konverterar sådana regler till anpassade funktioner som stöds på Forms as a Cloud Service. Du kan använda återanvändbara funktioner med Regelredigeraren för att fortsätta att erhålla resultat som erhållits med regelskript. `onSubmitError` eller `onSubmitSuccess` funktioner är nu tillgängliga som åtgärder i regelredigeraren.
* **Utkast och inskickat material:** Tjänsten bevarar inte metadata för utkast och skickade Adaptiv Forms.
* **Förifyllningstjänst:** Som standard sammanfogar förifyllningstjänsten data med ett adaptivt formulär på klienten i stället för att sammanfoga data på servern i AEM 6.5 Forms. Funktionen hjälper till att ge snabbare förifyllnad av ett adaptivt formulär. Du kan alltid konfigurera så att kopplingsåtgärden körs på Adobe Experience Manager Forms Server.
* **Skicka-åtgärder:** The **Skicka som PDF** åtgärden är inte tillgänglig. The **E-post** Skicka-åtgärd innehåller alternativ för att skicka bilagor och bifoga DoR-dokument (Document of Record) med e-post.
* **Komponenter**: Tjänsten stöder inte signering i formulär och inkluderar inte komponenterna Summary och Verify för Adaptive Forms.



+++


+++ 2. Dokumenttjänster: API:er för dokumenthantering (Assembler Service)


Tjänsten stöder inte åtgärder som är beroende av andra tjänster eller program:

* Det går inte att konvertera dokument i andra format än PDF till PDF. Exempel: Microsoft Word till PDF, Microsoft Excel till PDF och HTML till PDF stöds inte. Om dokumenten inte är i PDF-format. Konvertera sådana dokument till PDF-format innan du använder dem med API:er för dokumenthantering i Communications. Om dina dokument till exempel är i Microsoft Office-, HTML-, PostScript- (PS) eller XDP-format, konverterar du dessa dokument till PDF innan du använder dem med PDF-dokument.
* Adobe Distiller-baserade konverteringar stöds inte. PostScript(PS) till PDF
* Forms Service-baserade konverteringar stöds inte. Exempel: XDP till PDF forms.
* Tjänsten stöder inte konvertering av ett signerat PDF eller genomskinligt PDF till ett annat PDF-format.
* Det går inte att använda användningsrättigheter med tjänsten Reader Extensions.
* Tjänsten ger inte möjlighet att konvertera signerade eller genomskinliga PDF-dokument till PDF/A-format.

+++


+++ 3. Dokumenttjänster: API:er för dokumentgenerering (Output Service)

I ett enda API-anrop eller en grupp kan du bara använda en mall med flera DATA XML-filer. Det går inte att använda flera mallar med flera datafiler i ett enda API-anrop.

+++

+++ 4. Tjänsten Automated forms conversion

Tjänsten tillhandahåller inte metamodell för Automated forms conversion Service. Du kan [ladda ned den från Automated forms conversion Service-dokumentationen](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

+++

+++ 5. Forms portal

Stöd för anonym användning av Forms-portalen finns inte tillgängligt direkt (OOTB). Du kan anpassa formulärportalen för att aktivera visning av formulär för användare som inte är inloggade.

+++


+++ 6. HTML5 Forms (Mobile Forms)

Tjänsten stöder inte HTML5 Forms (Mobile Forms). Om du återger dina XDP-baserade formulär som HTML5 Forms kan du fortsätta använda funktionen i AEM 6.5 Forms.

+++


+++ 7. Formulärdatamodell

Forms datamodell stöder endast HTTP- och HTTP-slutpunkter för att skicka data. Tjänsten stöder inte ömsesidig SSL för REST-anslutning och x509-certifikatbaserad autentisering för SOAP-datakällor. * Forms as a Cloud Service tillåter att Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive och tjänster som stöder allmänna CRUD-åtgärder (Skapa, Läs, Uppdatera och Ta bort) används som datalager. Både Open API-specifikation 2.0 och Open API-specifikation stöds. Tjänsten stöder även JDBC-anslutning.

+++


+++ 8. Utvecklarmiljö

* En molnbaserad miljö har ingen webbkonsol (konfigurationshanterare). Du kan använda [[!DNL AEM Forms] as a Cloud Service SDK för att generera konfigurationer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) och CI/CD-överföring till [distribuera konfigurationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) till din Cloud Service.
* E-poststöd är som standard bara för HTTP- och HTTP-protokoll. [Kontakta supportteamet](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) för att aktivera portar för att skicka e-post och för att aktivera SMTP-protokoll för din miljö.
* Tjänsten stöder inte konvertering av ett signerat PDF eller genomskinligt PDF till ett annat PDF-format. Innan ni använder era kundpaket med Forms as a Cloud Service måste ni kompilera om den anpassade koden med den senaste versionen av URL-konventionen adobe-aemfd-docmanager* för lokaliserade adaptiva Forms har nu stöd för att ange nationella inställningar i URL:en. Ny URL-konvention möjliggör cachelagring av lokaliserade formulär på en Dispatcher eller CDN. I Cloud Service-miljön använder du URL-formatet `http://host:port/content/forms/af/<afName>.<locale>.html` begära en lokaliserad version av ett adaptivt formulär i stället för `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe rekommenderar att du använder Dispatcher eller CDN-cachning. Det förbättrar återgivningshastigheten i förfyllda formulär
* Adobe Experience Manager Forms as a Cloud Service innehåller många nya funktioner och möjligheter i dina AEM projekt. Det krävs dock vissa förändringar i Adobe Experience Manager Maven-projekten för att de ska vara kompatibla med AEM Cloud Service. På en hög nivå kräver AEM att innehåll och kod skiljs åt i diskreta delpaket för att se skillnaden mellan muterbart och oföränderligt innehåll. Använd [Databasmodernisering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) för att strukturera om befintliga projektpaket genom att separera innehåll och kod i separata paket som är kompatibla med den projektstruktur som har definierats för Adobe Experience Manager as a Cloud Service.


+++

<!-- 

### HTML5 Forms (Mobile Forms)

The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms.

### Adaptive Forms 

* **XSD-Based Adaptive Forms:** The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. You can use XDP-template to design a template for Document for Record. The service does not support XFA based Adaptive Forms  
* **Importing Adaptive Form templates:** Use build pipeline and corresponding Git repository of your program to import existing Adaptive Form templates. 
*  **Rule editor:** AEM Forms as a Cloud Service provides a hardened [Rule editor](rule-editor.md#visual-rule-editor). The code editor is not available on Forms as a Cloud Service. The migration utility helps you migrate your forms that have custom rules (created in code editor). The utility converts such rules into custom functions supported on Forms as a Cloud Service. You can use the reusable functions with Rule editor to continue obtaining results obtained with rule scripts  The `onSubmitError` or `onSubmitSuccess` functions are now available as actions the Rule Editor.  
* **Drafts and submissions:** The service does not retain metadata for drafts and submitted Adaptive Forms.  
* **Prefill Service:** By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server. 
* **Submit actions:** The **Email as PDF** action is not available. The **Email** submit action provide options to send attachments and attach Document of Record (DoR) with email. 
* **Components**:  The service does not support in-form signing experience and does not include the Summary and Verify components for Adaptive Forms.  
* **Forms portal**: Support for anonymous use of Forms portal is not available out of the box (OOTB). You can customize the forms portal to enable displaying forms for non-logged in users.

### Form Data Model

* Forms data model supports only HTTP and HTTPs endpoints to submit data. The service does not support Mutual SSL for REST connector and x509 certificate-based authentication for SOAP data sources. * Forms as a Cloud Service allows to use Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive, and services supporting general CRUD (Create, Read, Update, and Delete) operations as data stores, both Open API specification 2.0 and Open API specification are supported. The service also provides support for JDBC connector.


### Automated Forms Conversion Service     

The service does not provide meta-model for Automated Forms Conversion Service. You can [download it from Automated Forms Conversion Service documentation](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).


### Configurations

* Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment.  
* If you use custom bundles, recompile your code with latest version of adobe-aemfd-docmanager before using these bundles with Forms as a Cloud Service. 


### Document Services: Document Manipulation APIs (Assembler Service)

The service does not support operations dependent on other services or applications:  

* Conversion of documents in a non-PDF format to a PDF format is not supported. For example, Microsoft Word to PDF, Microsoft Excel to PDF, and HTML to PDF are not supported. If your documents are in a non-PDF format. Convert such documents to PDF format before using those with Communications Document Manipulation APIs. For example, if your documents are in Microsoft Office, HTML, PostScript (PS), XDP format, convert these documents to PDF format before using those with PDF documents. 
* Adobe Distiller-based conversions are not supported. For example, PostScript(PS) to PDF
* Forms Service-based conversions are not supported. For example, XDP to PDF Forms.
* The service does not support converting a Signed PDF or Transparent PDF to another PDF format.
* Applying usage rights using Reader Extensions Service is not available. 
* The service does not provide the ability to convert signed or transparent PDF Documents to PDF/A format. 

### Document Services: Document Generation APIs (Output Service)

* In a single API call or batch, you can use one template with multiple DATA XML files. Using mutiple templates with multiple data files in a single API call is not supported. 

### Other differences

* A cloud-native environment does not have web console (configuration manager). You can use [[!DNL AEM Forms] as a Cloud Service SDK to generate configurations](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) and CI/CD pipeline to [deploy the configuration](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) to your Cloud Service instance.
* Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment.
* The service does not support converting a Signed PDF or Transparent PDF to another PDF format.* Before using your customer bundles with Forms as a Cloud Service, recompile your custom code with the latest version of adobe-aemfd-docmanager* URL convention of localized Adaptive Forms now supports specifying a locale in the URL. New URL convention enables caching localized forms on a Dispatcher or CDN. On Cloud Service environment, use the URL format `http://host:port/content/forms/af/<afName>.<locale>.html` to request a localized version of an Adaptive Form instead of `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe recommends using Dispatcher or CDN caching. It helps improve rendering speed of prefilled forms 
* Adobe Experience Manager Forms as a Cloud Service brings many new features and possibilities into your AEM Projects. However, there are some changes required to Adobe Experience Manager Maven projects to be compatible with AEM Cloud Service. At a high-level, AEM requires a separation of content and code into discrete subpackages to respect the split between mutable and immutable content. Use the [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) tool to restructure existing project packages by separating content and code into discrete packages to be compatible with the project structure defined for Adobe Experience Manager as a Cloud Service.
-->




