---
title: Betydande förändringar av AEM Commerce som en Cloud Service
description: Betydande förändringar av AEM Commerce som Cloud Service jämfört med Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: ed81d08d9775f61c0ab1e305710ac7ecf29d4229
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 5%

---


# Notable changes to AEM Commerce as a Cloud Service {#notable-changes}

Adobe Experience Manager som Cloud Service har många nya funktioner och möjligheter att hantera dina AEM projekt. I det här dokumentet belyses de viktiga skillnaderna i handelsfunktioner mellan Commerce Integration Framework (CIF) för lokal, Adobe-hanterad tjänst och Experience Manager som Cloud Service. Andra ändringar finns i de allmänna [ändringarna av Experience Manager som en Cloud Service](/help/release-notes/aem-cloud-changes.md).

De största skillnaderna jämfört med Experience Manager 6.5 är inom följande områden:
* [Stöd för CIF Classic](#cif-classic)
* [Distribution av CIF-redigeringsverktyg](#cif-tools)
* [Förflyttning från lokal och Adobe hanterad tjänst](#moving-cif-cs)

## Stöd för CIF Classic/Quickstart på Experience Manager som Cloud Service {#cif-classic}

Classic Commerce Integration Framework, som inkluderade en produktimporterare för att importera och lagra produktkataloger i Experience Manager, är inte längre tillgängligt i Experience Manager som Cloud Service. Klassisk CIF stöds inte i Experience Manager som Cloud Service och projekt som använder klassisk CIF måste ersätta den klassiska CIF-implementeringen med den version som stöds enligt vad som beskrivs i [CIF på Experience Manager som en Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/commerce/architecture/magento.html#overview)

## Distribution av CIF {#deployment}

Nedan visas olika distributionsmodeller för Commerce Integration Framework för de olika AEM:

|  | AEM på plats | AEM Managed Services | AEM Cloud Service |
|-------------     |-----------|-----------|-----------|
| Så här distribuerar du CIF-redigeringsverktyg för Magento backend | [Se CIF Connector](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) som stöds i AEM 6.5 | [Se CIF Connector](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) som stöds i AEM 6.5 | AEM som Cloud Service måste etableras med CIF-tillägg. Kontakta din säljare för mer information |
| Distribuera [CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia) | Installera AEM | Distribuering via [Cloud Manager](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) | Projektet har flyttats till [molnhanterarens Git-databas](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) och distributionen har gjorts via [Cloud Manager](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html) |

>[!NOTE]
>
>Mer information om hur du använder CIF med AEM hanterade tjänster eller AEM lokalt finns i [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)

>[!Note]
>
>CIF Classic/Quickstart-versionen av Commerce Integration Framework kan användas AEM lokal-erbjudanden för mycket begränsad användning. Detta är dock inte den rekommenderade lösningen.

## Övergång till AEM Commerce som Cloud Service från On-Premise och Managed Services {#moving-cif-cs}

Kunder som går från en AEM på plats- eller Managed Services-installation till AEM som Cloud Service måste göra några smärre justeringar i AEM.

Den första justeringen, som beskrivs ovan, behövs för CIF Connector. CIF Connector ersätts av det CIF-tillägg som distribueras av Adobe. Installera därför inte CIF Connector på AEM som en Cloud Service. Dessutom stöds inte användningen med det lokala AEM Cloud SDK. Adobe tillhandahåller CIF-tillägget även för [lokal utveckling](develop.md).

För det andra, förstå [AEM projektstruktur](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) och AEM egenskaper som en Cloud Service. Anpassa projektinställningarna till AEM som en Cloud Service layout.
De viktigaste skillnaderna här är:

* OSGI-paketet för GraphQL-klienten **får inte** längre ingå i AEM, det distribueras via CIF-tillägget
* OSGI-konfigurationer för GraphQL-klienten och Graphql Data Service **får inte** längre ingå i AEM

>[!TIP]
>
>Ta en titt på [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) -projekt på GitHub. Detta projekt innehåller Maven-profiler för AEM som Cloud Service och lokal driftsättning som tar hänsyn till de olika ramverksvillkoren.
