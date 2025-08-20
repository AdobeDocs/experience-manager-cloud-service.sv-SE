---
title: Betydande förändringar av tillägget Commerce integration framework (CIF)
description: Betydande förändringar av Commerce integration framework (CIF) jämfört med tidigare CIF-versioner.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
feature: Commerce Integration Framework
role: Admin
source-git-commit: 856442039fcd25ec675a6258d182f7a35f590c3c
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---


# Observerbara ändringar av Commerce integration framework-tillägget (CIF) {#notable-changes}

Adobe Experience Manager as a Cloud Service har många nya funktioner och möjligheter att hantera dina AEM-projekt. Om du vill veta mer om de här funktionerna kan du följa länken för [ändringar av Experience Manager as a Cloud Service.](/help/release-notes/aem-cloud-changes.md)

Det här dokumentet belyser de viktiga skillnaderna mellan Commerce integration framework (CIF) och gamla CIF-versioner, så kallade CIF Classic (Quickstart) och CIF Open-source.

## Installation och uppdateringar

AEM CIF-tillägget installeras via Cloud Manager. Installationen kräver en CIF-kredit förutom för sandlådor där CIF kan installeras utan krediter. Krediter tas emot automatiskt via etablering av CIF-tillägget i ditt AEM-kontrakt.

Tillägget uppdateras automatiskt som en del av den vanliga AEM as a Cloud Service-uppdateringen.

### Tidigare versioner av CIF {#previous-versions-installation}

* CIF Classic: CIF var en del av QuickStart och behövde inte installeras. CIF-uppdateringar ingick i AEM- eller Service Pack-uppdateringar
* CIF Open-source för AEM lokal: Installation via GitHub. Uppdateringarna var en del av det manuella uppdaterings-/underhållsarbetet.
* CIF Open-source för AEM Adobe Managed Services: Installation via Adobe Account Team. Uppdateringarna var en del av det manuella uppdaterings-/underhållsarbetet.

## Konfiguration av slutpunkt {#endpoint-configuration}

Slutpunkten konfigureras och uppdateras antingen via Cloud Manager UI eller dess CLI.

### Tidigare versioner av CIF {#previous-versions-endpoint}

* CIF Classic: Via OSGi-konfiguration i AEM
* CIF Open-source: Via CIF Configuration Browser

## Driftsättning av CIF Venia Project {#venia-project}

Projektet är tillgängligt i [Cloud Manager Git-databas](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) och distributionen görs via [Cloud Manager.](/help/implementing/deploying/overview.md)

### Tidigare versioner av CIF {#previous-versions-venia}

* CIF Classic: Installera med AEM-paket
* CIF Open-source: Via [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=sv-SE)

## Produktkatalogdata {#product-catalog-data}

Produktkatalogdata efterfrågas vid behov via realtidsanrop till en extern slutpunkt som stöder de GraphQL API:er som krävs. Dessa API:er har stöd för åtkomst till livedata eller mellanlagrade data vid ett visst datum. Ingen replikering behövs.

### Tidigare versioner av CIF {#previous-versions-catalog}

* CIF Classic: Live-produktdata och mellanlagrade produktdata importeras och lagras i JCR på AEM Author via import av komplett- eller deltaprodukt. Live-produktdata replikeras till AEM Publish.

## Produktkatalogupplevelser med AEM Rendering {#catalog-experiences}

AEM återger produktkatalogupplevelser direkt med AEM katalogmallar som har tilldelats produkter och kategorier. Ingen replikering behövs.

### Tidigare versioner av CIF {#previous-cif-versions}

* CIF Classic: AEM Author skapar en AEM-sida för varje kategori/produkt med hjälp av katalogritningsverktyget. Dessa sidor replikeras till AEM Publish.

>[!NOTE]
>
>Mer information om hur du använder CIF med AEM Managed Service eller AEM On-Local finns i [Commerce integration framework.](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
