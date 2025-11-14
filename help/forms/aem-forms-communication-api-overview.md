---
title: AEM Forms Communications APIs - Översikt
description: Översikt över AEM Forms Communications API:er, inklusive autentiseringsmetoder och fullständig API-referens
role: Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: cba0a8a0a0b346fc89cca146519cc5843f244d23
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 0%

---


# AEM Forms Communications APIs - Översikt

AEM Forms Communications API:er innehåller en omfattande uppsättning molnbaserade API:er som hjälper företag att automatisera dokumentarbetsflöden.

AEM Forms API:er är strukturerade och åtkomliga via två primära konsoler:

* [Adobe Developer Console (ADC)](https://developer.adobe.com/developer-console/) - Adobe Developer Console är gateway till Adobe API:er, händelser, körningsmiljö och App Builder.

* [AEM Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console) - AEM Developer Console innehåller verktyg för felsökning och inspektion av AEM as a Cloud Service-miljöer.

Varje konsol ger åtkomst till olika API:er och tjänster för dokumentbearbetning, generering, konvertering, kryptering och kommunikationsuppgifter. API:erna stöder olika [autentiseringsmetoder](#authentication-methods).

## Autentiseringsmetoder

API:er har stöd för flera autentiseringsmetoder för säker integrering mellan program och Adobe-tjänster:

| Proportioner | OAuth Server-till-server (rekommenderas) | JWT (JSON Web Token) |
|-------------|------------------------------------------|---------------------------|
| Beskrivning | Modern och säker metod för API-åtkomst utan användarinteraktion. | Äldre metod som använder signerade tokens för åtkomst. |
| Installationsplats | Adobe Developer Console och AEM Developer Console | Endast AEM Developer Console |
| Dokumentskydd | Hög - använder klientens autentiseringsuppgifter och omfång | Måttligt - beror på nyckelhantering |
| Skalbarhet | Mycket skalbar för serverdelsintegreringar | Begränsat, lämpligt för äldre bruk |
| Tokenhantering | Automatisk generering och förnyelse | Manuell tokensignering och rotation |
| Status | Rekommenderas | Föråldrat |


>[!NOTE]
>
> Klicka på länkarna nedan om du vill veta mer om :-
> 
> * [OAuth Server-till-server (rekommenderas)](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)
> * [JWT (JSON-webbtoken)](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/)

<!--### Execution Models

The following table highlights the key differences between Synchronous (On-Demand) and Asynchronous (Batch) execution models supported in AEM Forms Communications APIs:

| Feature | Synchronous (On-Demand) | Batch (Asynchronous) |
|---------|-------------------------|----------------------|
| **Execution Model** | Real-time, immediate | Queued, scheduled |
| **Response Time** | Seconds | Minutes to hours |
| **Volume** | Single or few documents | Hundreds to thousands |
| **Testing Environment** | Author & Publish | Author Only |
| **Use Case** | User-triggered actions | Scheduled bulk operations |
| **Console Access** | ADC & AEM Developer Console | AEM Developer Console Only |-->

## API-klassificeringsöversikt

Alla AEM Forms API:er är uppdelade i två huvuddelar:

* [API:er för leverans och körning av anpassade formulär](https://developer-stage.adobe.com/experience-cloud/experience-manager-apis/api/stable/forms/)

* [AEM Forms Communication APIs](#aem-forms-communications-apis)

| Information | API:er för leverans och körning av adaptiva formulär | Kommunikations-API:er |
|--------------|----------------------------|--------------------------|
| Syfte | Hantera leverans av adaptiva formulär och körningsåtgärder | Generering och hantering av dokument |
| Användningsexempel | - Formuläråtergivning <br>- Dataförifyllning<br>- Formuläröverföringar<br> - Hantering av utkast | - PDF-generering<br>- Dokumentsammanfogning<br> - Gruppbearbetning<br> - Utskriftsåtgärder |
| Auktoriseringsmetod | Stöder autentiseringsmetoderna OAuth Server-to-Server/User. | Stöder endast OAuth Server-till-Server-autentisering. |

### AEM Forms Communications APIs

Kommunikations-API:er är det primära fokus för dokumentcentrerade åtgärder.

I tabellen nedan visas alla [AEM Forms Communications API:er](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/) tillsammans med autentiseringsmetoder och körningsmodeller som stöds:

#### API för dokumentgenerering


| API-slutpunkt | Beskrivning | Körningsmodell | Autentiseringsmetod |
| ----- | ------ |------- | ------ |
| [/adobe/forms/batch/output/config](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig) | Skapar en ny batchkonfiguration för dokumentgenereringsjobb. | Asynkron/batch | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/{configName}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetBatchConfigbyName) | Hämtar information om en specifik batchkonfiguration. | Asynkron/batch | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/configs ](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetAllBatchConfigs) | Returnerar en lista med alla tillgängliga batchkonfigurationer. | Asynkron/batch | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/{configName}/execution](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/StartBatchRun) | Startar en batchutdatagenerering som körs med en konfiguration. | Asynkron/batch | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/{configName}/execution/{executionId}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetBatchRunInstanceState) | Hämtar körningsstatus för ett batchjobb. | Asynkron/batch | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/{configName}/Executions](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | Visar alla instanser som körs för en specifik batchkonfiguration. | Asynkron/batch | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/doc/v1/generatePDFOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generatePDFOutput/post) | Genererar PDF-utdata synkront baserat på mallar och data. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/doc/v1/generatePrintedOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | Genererar utskriftsklara utdataformat (t.ex. PCL, PostScript). | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/doc/v1/generate/afp](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generate~1afp/post) | Genererar AFP-utdata för stora utskriftsvolymer. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/document/generate/pdfform ](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm) | Återger ett PDF-formulär (XFA/XDP) med sammanfogade data. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/generate/pdfform/job/{id}/status ](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobStatus) | Hämtar status för ett PDF-formulärgenereringsjobb. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/generate/pdfform/job/{id}/result](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobResult) | Hämtar utdata/resultat för ett slutfört PDF-formulärjobb. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |


#### API:er för dokumenthantering

| API-slutpunkt | Beskrivning | Körningsmodell | Autentiseringsmetod |
| ------------------ | ---------------- | ----------| ---------- |
| [/adobe/forms/assembler/ddx/invoke](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/DDX-execution/operation/InvokeDDX) | Kör DDX-instruktioner för att kombinera, dela eller ändra PDF-filer. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/assembler/pdfa/convert](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-conversion/operation/ConvertToPDFA) | Konverterar ett PDF-dokument till PDF/A-format. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/assembler/pdfa/validate](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-validation/operation/CheckIsPDFA) | Validerar om en PDF uppfyller PDF/A-standarden | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |

#### API:er för dokumentkonvertering

| API-slutpunkt | Beskrivning | Körningsmodell | Autentiseringsmetod |
|--------- | -------|---------|----------------------|
| [/adobe/document/convert/pdftoxdp](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Conversion/paths/~1convert~1pdftoxdp/post) | Konverterar ett PDF-formulär till XDP-format. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |

#### API för dokumentextrahering

| API-slutpunkt | Beskrivning | Körningsmodell | Autentiseringsmetod |
|---------| -------|---------|----------------------|
| [/adobe/forms/doc/v1/extract/pdfproperties](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1pdfproperties/post) | Extraherar egenskaper och strukturinformation från en PDF. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/forms/doc/v1/extract/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/extractUsageRights) | Extraherar användarrättigheter som är inbäddade i en PDF. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/forms/doc/v1/extract/metadata ](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1metadata/post) | Extraherar metadata som titel, författare och nyckelord. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/forms/doc/v1/extract/data ](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/exportData) | Hämtar formulärdata (XML/JSON) från PDF forms. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/extract/security](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1security/post) | Extraherar skyddsinställningar som behörigheter och kryptering. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |

#### API:er för dokumentomvandling


| API-slutpunkt | Beskrivning | Körningsmodell | Autentiseringsmetod |
|--------|---------|---------|----------------------|
| [/adobe/document/transform/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1transform~1metadata/post) | Uppdaterar eller lägger till metadata i ett PDF-dokument. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/field/signature/add](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1add/post) | Lägger till ett fält för elektronisk underskrift i en PDF. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/field/signature/clear](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1clear/post) | Rensar innehållet i ett signaturfält. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/field/signature/remove](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1remove/post) | Tar bort ett signaturfält från en PDF. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |

#### Dokument-API:er för Assurance

| API-slutpunkt | Beskrivning | Körningsmodell | Autentiseringsmetod |
|---------|-------|---------|----------------------|
| [/adobe/document/ensure/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/applyUsageRights) | Tillämpar användarrättigheter för en PDF (t.ex. kommentar, fyll i, signera). | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/ensure/encrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1encrypt/post) | Krypterar en PDF med lösenord eller certifikatskydd. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/ensure/decrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1decrypt/post) | Dekrypterar ett skyddat PDF-dokument. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/ensure/sign](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1sign/post) | Signera ett PDF-dokument digitalt. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/ensure/certify](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1certify/post) | Certifierar en PDF med ett digitalt certifikat. | Synkron | [OAuth-server till server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |


## Nästa steg

Lär dig hur du ställer in miljön för API:er för synkron (On-Demand) och asynkron (Batch) Forms Communications:

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <!-- Synchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Synchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" title="Synkrona API:er" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/sync-api.png" alt="Synkrona API:er"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" title="AEM Forms Communications API:er - Synkrona">API:er för AEM Forms Communications - Synkron</a>
                    </p>
                    <p class="is-size-6">Lär dig hur du konfigurerar miljö för Synkrona (on-demand) API:er för Forms Communications som genererar eller bearbetar dokument direkt. </p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Läs mer</span>
                </a>
            </div>
        </div>
    </div>
    <!-- Asynchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Asynchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" title="AEM Forms Communications API:er - asynkrona" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/async-api.png" alt="Asynkrona API:er"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" title="Asynkrona API:er">AEM Forms Communications API:er - asynkron (batch)</a>
                    </p>
                    <p class="is-size-6">Lär dig hur du konfigurerar miljö för asynkrona (Batch) Forms Communications API:er som genererar eller bearbetar flera dokument på ett schemalagt sätt.</p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Läs mer</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


>[!MORELIKETHIS]
>
>* [Introduktion till AEM Forms as a Cloud Service Communications](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* [AEM Forms as a Cloud Service Architecture for Adaptive Forms and Communication APIs](/help/forms/aem-forms-cloud-service-architecture.md)
>* [Kommunikationsbearbetning - Synkrona API:er](/help/forms/aem-forms-cloud-service-communications.md)
>* [Kommunikationsbearbetning - Grupp-API:er](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
>* [Kommunikationsbearbetning - API:er på begäran](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)