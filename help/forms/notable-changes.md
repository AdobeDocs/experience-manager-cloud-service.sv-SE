---
title: Skillnader mellan AEM 6.5 Forms och AEM Cloud Services
description: Använder du Experience Manager Forms och vill uppgradera till Adobe Experience Manager Forms as a Cloud Service? Jämför AEM 6.5 Forms och AEM Cloud Services och lär dig de viktigaste ändringarna innan du uppgraderar eller migrerar till Cloud Service.
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: dea6c266e5c10135a320f923dc77d0fd2050988e
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 0%

---

# Betydande förändringar för befintliga användare av Adobe Experience Manager 6.5 Forms  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Service förändrar de befintliga funktionerna avsevärt jämfört med Adobe Experience Manager Forms On-Premise och [!DNL Adobe-Managed Service] miljöer. De viktigaste skillnaderna anges nedan:

<!-- 
<table>
    <thead>
        <tr>
            <th>AEM Forms Components</th>
            <th>Feature/Capability</th>
            <th>[!DNL AEM Forms] as a Cloud Service</th>
            <th>AEM 6.5 Forms on-premise </th>
            <th>AEM 6.5 Forms Adobe Managed Services </th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="6">Cloud native features</td>
            <td>Cloud-native architecture</td>
            <td>&#x2705;</td>
            <td>---</td>
            <td>---</td>
        </tr>
        <tr>
            <td>Auto-scaling based on load</td>
            <td>&#x2705;</td>
            <td>---</td>
            <td>---</td>
        </tr>
        <tr>
            <td>Zero downtime for upgrades</td>
            <td>&#x2705;</td>
            <td>---</td>
            <td>---</td>
        </tr>
        <tr>
            <td>Feature roll-out frequency</td>
            <td>Monthly</td>
            <td>Quarterly</td>
            <td>Quarterly</td>
        </tr>
        <tr>
            <td>CDN (content delivery network) included</td>
            <td>&#x2705;</td>
            <td>---</td>
            <td>---</td>
        </tr>
        <tr>
            <td>Topologies optimized for maximum resilience and efficiency</td>
            <td>&#x2705;</td>
            <td>---</td>
            <td>---</td>
        </tr>
        <tr>
            <td rowspan="3">Developer environment <sup>6</sup></td>
            <td>Self-Service via Cloud Manager</td>
            <td>&#x2705;</td>
            <td>---</td>
            <td>---</td>
        </tr>
        <tr>
            <td>Cloud-native development environment</td>
            <td>&#x2705;</td>
            <td>---</td>
            <td>---</td>
        <tr>
            <td>Automated upgrades with Continuous Integration and Continuous Delivery (CI/CD)</td>
            <td>&#x2705;</td>
            <td>---</td>
            <td>---</td>
        </tr>
        <tr>
            <td rowspan="8">Third-party and Adobe integrations</td>
            <td>[!DNL Micosoft Power Automate] for business process automation</td>
            <td>&#x2705;</td>
            <td>---</td>
            <td>---</td>
        </tr>
        <tr>
            <td>[!DNL Microsoft Dynamics] and [!DNL Salesforce] for Customer Relationship Management (CRM)</td>
            <td>&#x2705;</td>
            <td>---</td>
            <td>---</td>
        </tr>
        <tr>
            <td>Integration with [!DNL Microsoft Azure] for data storage</td>
            <td>&#x2705;</td>
            <td>---</td>
            <td>---</td>
        </tr>
        <tr>
            <td>[!DNL DocuSign] for e-signatures</td>
            <td>&#x2705;</td>
            <td>---</td>
            <td>---</td>
        </tr>
        <tr>
            <td>[!DNL Adobe Sign] for e-signatures</td>
            <td>&#x2705;</td>
            <td>---</td>
            <td>---</td>
        </tr>
        <tr>
            <td>[Adobe Launch] to track usage and performance</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>[!DNL Adobe Analytics] to track usage and performance</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Google reCaptcha for adaptive challenges</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td rowspan="11">Adaptive Forms</td>
            <td>Automated Forms Conversion Service<sup>1</sup></td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Core Components</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Foundation Components</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Form creation wizard</td>
            <td>&#x2705;</td>
            <td>---</td>
            <td>---</td>
        </tr>
        <tr>
            <td>Rule Editor<sup>1</sup></td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Prefill Service <sup>1</sup></td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Auto-save an adaptive form</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>XSD-Based adaptive forms <sup>1</sup></td>
            <td>---</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>In-form signing experience for adaptive forms</td>
            <td>---</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Submit an adaptive form to AEM Forms on JEE Workflows (Process Management)</td>
            <td>---</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Summary, Verify, and Scribble Signature components for adaptive forms</td>
            <td>---</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td rowspan="4">Forms Portal</td>
            <td>Drafts and Submission component <sup>2<sup></td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Search & Lister component</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Link component</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>List forms for non-logged in users <sup>2</sup></td>
            <td>---</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td rowspan="13">Data integration (Form Data Model) </td>
            <td>OData services</td>
            <td>&#x2705;</td>
            <td>---</td>
            <td>---</td>
        </tr>
        <tr>
            <td>Microsoft Dynamics</td>
            <td>&#x2705;</td>
            <td>---</td>
            <td>---</td>
        </tr>
        <tr>
            <td>SalesForce</td>
            <td>&#x2705;</td>
            <td>---</td>
            <td>---</td>
        </tr>
        <tr>
            <td>Microsoft Azure Blob Storage</td>
            <td>&#x2705;</td>
            <td>---</td>
            <td>---</td>
        </tr>
        <tr>
            <td>RESTful web services - Open API version 3.0 <sup>4</sup></td>
            <td>&#x2705;</td>
            <td>---</td>
            <td>---</td>
        </tr>
        <tr>
            <td>RESTful web services - Open API version 2.0 <sup>4</sup></td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>SOAP-based web services <sup>4</sup></td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Microsoft SQL Server</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>MySQL</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>IBM DB2</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
                <tr>
            <td>Oracle RDBMS</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>AEM user profile</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Sybase</td>
            <td>---</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td rowspan="8">Communication APIs (Document Services)</td>
            <td>Document Generation (Output Service) <sup>3</sup></td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Document Manipulation (Assembler Service) <sup>3</sup></td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Signature Service</td>
            <td>---</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Encryption service</td>
            <td>---</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Reader Extension service</td>
            <td>---</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Send to printer service</td>
            <td>---</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Convert PDF service</td>
            <td>---</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Barcoded Forms service </td>
            <td>---</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Document Security</td>
            <td>Document Security Extension for Microsoft Office (Digital Rights Management)</td>
            <td>---</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td rowspan="2">HTML5 Forms <sup>5</sup></td>
            <td>HTML5 Forms</td>
            <td>---</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Forms Workspace</td>
            <td>---</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
        <tr>
            <td>Interactive Communications</td>
            <td>Interactive Communications</td>
            <td>---</td>
            <td>&#x2705;</td>
            <td>&#x2705;</td>
        </tr>
    </tbody>
</table>


<!-- 

## Cloud native features 

| Feature/Capability | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms  | 
|---|---|---|
| Cloud-native architecture | &#x2705;  | --- |
| Auto-scaling based on load | &#x2705;  | --- |
| Zero downtime for upgrades | &#x2705;  | --- |
| Feature roll-out frequency | Agile*  | Quarterly |
| CDN (content delivery network) included | &#x2705;  | --- | 
| Topologies optimized for maximum resilience and efficiency| &#x2705;  | --- | 

## Integrations 

| Feature/Capability | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms  | 
|---|---|---|
| Integration with [!DNL Micosoft Power Automate] | &#x2705; | --- | 
| Integration with [!DNL DocuSign] | &#x2705; | --- | 
| Integration with [!DNL Microsoft Dynamics] and [!DNL Salesforce] | &#x2705; | --- |  
| Integration with Microsoft Azure data stores | &#x2705; | --- | 
| Integration with [!DNL Adobe Sign] | &#x2705; | &#x2705; | 
| Integration with [!DNL AEM Sites] | &#x2705;| &#x2705; | 
| Integration with [!DNL Adobe Launch] | &#x2705; | &#x2705; | 
| Integration with [!DNL Adobe Analytics] | &#x2705; | &#x2705; |
| Data integration (Form Data Model) | &#x2705; | &#x2705; |
 
## Adaptive forms <sup> 1 </sup>

| Feature/Capability | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms  | 
|---|---|---|
| Automated Forms Conversion Service  | &#x2705; | &#x2705; |
| Forms Portal Submissions | &#x2705; | &#x2705; | 
| Google Captcha integrations | &#x2705; | &#x2705; |
| Repeatable sections in an adaptive form | &#x2705;| &#x2705; |
| Form fragments | &#x2705; | --- |
| Hardened rule editor | &#x2705; | --- | 
| Form creation wizard | &#x2705; | --- |
| Auto-save an adaptive form | --- | &#x2705; |
| Scribble Signatures | --- | &#x2705; |
| XSD-Based adaptive forms | --- | &#x2705; |
| Using Adobe Sign to add signatures within an Adaptive Form | --- | &#x2705; |
|Submit to AEM Forms on JEE Workflows (Process Management)| --- | &#x2705; | 

## Communication APIs (Document Services <sup> 2 </sup>) and Document Security 

| Feature/Capability | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms  | 
|---|---|---|
| Document Generation (Output Service)| &#x2705; | &#x2705; |
| Document Manipulation (Assembler Service) | &#x2705; | &#x2705; |
| Signature service | --- | &#x2705; |
| Encryption service | --- | &#x2705; |
| Reader Extension service | --- | &#x2705; |
| Send to printer service | --- | &#x2705; |
| Convert PDF service | --- | &#x2705; |
| Barcoded Forms service | --- | &#x2705; |
| Document Security Extension for Microsoft Office (Digital Rights Management) | --- | &#x2705; | 

## Data integration (Form Data Model) <sup> 3 </sup>

| Data Sources | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms  | 
|---|---|---|
| OData services | &#x2705; (Version 4.0)|  --- | 
| Microsoft Dynamics| &#x2705;  | --- | 
| SalesForce|  &#x2705; | ---| 
| Microsoft Azure Blob Storage| &#x2705;  | --- | 
| RESTful web services Open API version 3.0| &#x2705; | --- |
| RESTful web services Open API version 2.0| &#x2705; | &#x2705; |
| SOAP-based web services| &#x2705;| &#x2705; |   
| MySQL| &#x2705; | &#x2705; | 
| Microsoft SQL Server| &#x2705; | &#x2705; | 
| IBM DB2| &#x2705; | &#x2705; | 
| Oracle RDBMS| &#x2705; | &#x2705; | 
| Sybase|  ---  | &#x2705; | 
| AEM user profile| --- | &#x2705; | 

## Form-centric workflows

| Feature/Capability | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms  | 
|---|---|---|
|Submit to AEM Forms on JEE Workflows (Process Management)| --- | &#x2705; | 

## HTML5 Forms<sup> 4 </sup> and Interactive Communications 

| Feature/Capability | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms  | 
|---|---|---|
| HTML5 Forms | --- | &#x2705; | 
| HTML5 Workspace| --- | &#x2705; | 
| Interactive Communications | --- | &#x2705; | 

## Developer environment <sup> 5 </sup>

| Feature/Capability | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms  | 
|---|---|---|
| Cloud-native development environment | &#x2705;  | --- | 
| Self-Service via Cloud Manager | &#x2705;  | --- | 
| Automated upgrades with Continuous Integration and Continuous Delivery (CI/CD) | &#x2705;  | --- | 


-->

## Inbyggda funktioner i molnet

* Tjänsten har en molnbaserad arkitektur som möjliggör automatisk skalning baserat på belastning, noll driftstopp för uppgraderingar, frekvent och efter lansering av nya funktioner och uppdateringar samt topologier som optimerats för maximal flexibilitet och effektivitet.

* Tjänsten ger funktioner för extern databehandling (inga data lagras på servern för någon typ av bearbetning) och innehåller inga skicka-åtgärder som lagrar data till instanser av Adobe Experience Manager Cloud Service, vilket gör den supersäker. Data som samlas in via formulär skickas direkt till konfigurerade datalager.

* Ett kostnadsfritt CDN (content delivery network) ingår också så att du snabbare kan leverera och återge formulär.


## Uppdateringar av utvecklingsflödet

* Tjänsten tillhandahåller en SDK för att utveckla och testa anpassad kod i en lokal miljö (lokal dator) innan koden distribueras till en Cloud Service. Utvecklare utvecklar och testar anpassade komponenter, teman, arbetsflöden, program, konfigurationer, mallar och mycket mer med SDK på sina lokala datorer. När de har testat den anpassade koden i den lokala utvecklingsmiljön distribuerar de den anpassade koden till en [Forms CS - miljöutveckling eller scenmiljö](/help/implementing/cloud-manager/deploy-code.md) för ytterligare testning innan den marknadsförs till en produktionsmiljö.

* Utvecklarna har samma kod för Cloud Service och lokal utvecklingsmiljö [git-databas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/cloud-manager-repositories.html). En Git-databas, som baseras på AEM Archetype, skapas automatiskt när ett AEM as a Cloud Service program skapas.

   ![](/help/forms/assets/git-repo-local-and-forms-cs.png)


* En molnbaserad miljö har ingen webbkonsol (konfigurationshanterare). Du kan använda [[!DNL AEM Forms] as a Cloud Service SDK för att generera konfigurationer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) och CI/CD-överföring till [distribuera konfigurationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) till din Cloud Service.

* Adobe Experience Manager Forms as a Cloud Service innehåller många nya funktioner och möjligheter i dina AEM projekt. Det krävs dock vissa förändringar i Adobe Experience Manager Maven-projekten för att de ska vara kompatibla med AEM Cloud Service. På en hög nivå kräver AEM att innehåll och kod skiljs åt i diskreta delpaket för att se skillnaden mellan muterbart och oföränderligt innehåll. Använd [Databasmodernisering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) för att strukturera om befintliga projektpaket genom att separera innehåll och kod i separata paket som är kompatibla med den projektstruktur som har definierats för Adobe Experience Manager as a Cloud Service.

* Innan ni använder era kundpaket med Forms as a Cloud Service måste ni kompilera om den anpassade koden med den senaste versionen av adobe-aemfd-docmanager.

* Använd [AEM Forms as a Cloud Service migreringsverktyg](/help/forms/migrate-to-forms-as-a-cloud-service.md) för att förbereda och migrera dina adaptiva Forms, teman, mallar och molnkonfigurationer från <!-- AEM 6.3 Forms--> AEM 6.4 Forms on OSGi and AEM 6.5 Forms on OSGi to [!DNL AEM] as a Cloud Service. Använd [Git-databasen för ditt program](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) för att importera befintliga adaptiva formulärmallar.

* E-post har som standard bara stöd för HTTP- och HTTP-protokoll. [Kontakta supportteamet](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) för att aktivera portar för att skicka e-post och för att aktivera SMTP-protokoll för din miljö.

## Lokalisering

* URL-konventionen för lokaliserade adaptiva Forms har nu stöd för att ange nationella inställningar i URL:en. Ny URL-konvention möjliggör cachelagring av lokaliserade formulär på en Dispatcher eller CDN. I en Cloud Service-miljö använder du URL-formatet `http://host:port/content/forms/af/<afName>.<locale>.html` begära en lokaliserad version av ett adaptivt formulär i stället för `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`.

* Adobe rekommenderar att du använder Dispatcher eller CDN-cachning. Det förbättrar återgivningshastigheten för förfyllda formulär.


## Adaptiv Forms

* **Regelredigerare:** AEM Forms as a Cloud Service har en härdad [Regelredigerare](rule-editor.md#visual-rule-editor). Kodredigeraren är inte tillgänglig på Forms as a Cloud Service.

   The [migreringsverktyg](/help/forms/migrate-to-forms-as-a-cloud-service.md) hjälper dig att migrera formulär som har anpassade regler (skapade i kodredigeraren). Verktyget konverterar sådana regler till anpassade funktioner som stöds på Forms as a Cloud Service. Du kan använda de återanvändbara funktionerna med Regelredigeraren för att fortsätta att hämta resultat från regelskript. The `onSubmitError` eller `onSubmitSuccess` funktioner är nu tillgängliga som åtgärder i regelredigeraren.

* **Förifyllningstjänst:** Som standard sammanfogar förifyllningstjänsten data med ett adaptivt formulär på klienten i stället för att sammanfoga data på servern i AEM 6.5 Forms. Funktionen hjälper till att ge snabbare förifyllnad av ett adaptivt formulär. Du kan alltid konfigurera så att kopplingsåtgärden körs på Adobe Experience Manager Forms Server.

* **Skicka-åtgärder:** The **E-post** Skicka-åtgärd innehåller alternativ för att skicka bilagor och bifoga DoR-dokument (Document of Record) med e-post. Du kan använda den istället för **Skicka som PDF** i AEM 6.5 Forms.

* **Tjänsten Automated forms conversion**: Tjänsten tillhandahåller inte metamodell för Automated forms conversion Service. Du kan [ladda ned den från Automated forms conversion Service-dokumentationen](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

* **XSD-baserad, adaptiv Forms:** Du kan använda XDP-mall för att utforma en mall för Dokument för post. Tjänsten stöder inte XFA-baserad Adaptive Forms

* **Komponenter**: Tjänsten stöder inte signering i formulär och inkluderar inte komponenterna Summary och Verify för Adaptive Forms.

## Forms Portal

* Du kan använda komponenterna Sök och lista, Utkast och överföring samt Länka i Forms Portal för att lista formulär för inloggade användare. Stöd för anonym användning av Forms Portal finns inte tillgängligt direkt (OOTB). Du kan anpassa Forms Portal för att aktivera visning av formulär för användare som inte är inloggade.

* Tjänsten bevarar inte metadata för utkast och skickade Adaptiv Forms.

## Dokumenttjänster:

Forms as a Cloud Service tillhandahåller RESTful-API:er för dokumentgenerering och dokumentredigering. Du kan använda dessa API:er för att generera eller ändra dokument vid behov eller i grupper, efter behov:

* **Dokumenttjänster: API:er för dokumentgenerering (Output Service)**: I ett enda API-anrop eller en grupp kan du bara använda en mall med flera DATA XML-filer. Det går inte att använda flera mallar med flera datafiler i ett enda API-anrop.

* **API:er för dokumenthantering (Assembler Service)**:

   * De åtgärder som är beroende av dokumenttjänster eller program är inte tillgängliga. Exempel: Microsoft Word till PDF, Microsoft Excel till PDF och HTML till PDF, PostScript (PS) till PDF, XDP till PDF forms stöds inte. De här åtgärderna är beroende av Microsoft Office, Adobe Acrobat, Adobe Distiller och Forms Document Service.

   * Konvertera dokument som inte är i PDF till ett PDF-format innan du använder dem med API:er för kommunikationsdokumentmanipulering. Om dina dokument till exempel är i Microsoft Office-, HTML-, PostScript- (PS) eller XDP-format, konverterar du dessa dokument till PDF innan du använder dem med PDF-dokument. Du kan använda [ConvertPDF](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/using-convertpdf-service.html) för sådana konverteringar.

* Du kan använda en AEM 6.5 Forms-miljö för Digital Signature, Encryption, Reader Extension, Send to printer, Convert PDF och Barcoded Forms.


## Dataintegrering (formulärdatamodell)

* Forms as a Cloud Service tillåter att Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive och tjänster som stöder allmänna CRUD-åtgärder (Skapa, Läs, Uppdatera och Ta bort) används som datalager. Både Open API-specifikation 2.0 och Open API 3.0 stöds.

* Tjänsten ger även stöd för JDBC-anslutning, Microsoft Dynamics, SalesForce, SOAP-baserade webbtjänster och tjänster som stöder OData.

* Du kan även ansluta AEM användarprofil för att hämta och uppdatera användarinformation.

* Forms datamodell stöder endast HTTP- och HTTPS-slutpunkter för att skicka data. Tjänsten stöder inte ömsesidig SSL för REST-anslutning och x509-certifikatbaserad autentisering för SOAP-datakällor.


## E-signera

* Tjänsten ger en OOTB-integrering med Adobe Sign och stöder DocuSign för e-signaturer.


## HTML5 Forms

* Du kan använda en AEM 6.5 Forms-miljö för att:

   * återge dina XDP-baserade formulär som HTML5 Forms. Tjänsten stöder inte HTML5 Forms (Mobile Forms).

   * hämta in data offline och synkronisera dem nästa gång du kommer tillbaka online med [AEM Forms Workspace](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html) app.

## Interaktiv kommunikation

* Du kan använda API:er för kommunikation för att producera personliga dokument on-demand eller gruppvis. Du kan använda en AEM 6.5 Forms-miljö för webbkanaler och agentgränssnitt.

## Document Security Extension for Microsoft Office

* Document Security Extension for Microsoft Office (Digital Rights Management) support AEM 6.5 Forms. Tillägget är inte tillgängligt för Forms as a Cloud Service.








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




