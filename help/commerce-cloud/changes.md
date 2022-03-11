---
title: Betydande ändringar av tillägget Commerce Integration Framework (CIF)
description: Betydande ändringar av Commerce Integration Framework (CIF) jämfört med tidigare CIF-versioner.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# Betydande ändringar av tillägget i Commerce Integration Framework (CIF){#notable-changes}

Adobe Experience Manager as a Cloud Service har många nya funktioner och möjligheter att hantera AEM projekt. Om du vill veta mer om de här funktionerna kan du klicka på länken för [ändringar av Experience Manager as a Cloud Service](/help/release-notes/aem-cloud-changes.md).

I det här dokumentet belyses de viktiga skillnaderna mellan tillägget i Commerce Integration Framework (CIF) och äldre CIF-versioner, främst kända som CIF Classic (Quickstart) och CIF Open source.

## Installation och uppdateringar

AEM CIF-tillägg installeras via Cloud Manager. Installationen kräver en CIF-kredit förutom för sandlådor där CIF kan installeras utan krediter. Krediter tas emot automatiskt via provisionering av CIF-tillägget i ditt AEM.

Tillägget uppdateras automatiskt som en del av de regelbundna AEM as a Cloud Service uppdateringarna.

**Tidigare CIF-versioner**

* CIF Classic: CIF var en del av QuickStart och behövde inte installeras. CIF-uppdateringar var en del av regelbundna AEM- eller Service Pack-uppdateringar
* CIF öppen källkod för AEM lokalt: Installation via GitHub. Uppdateringarna var en del av det manuella uppdaterings-/underhållsarbetet.
* CIF Open Source för AEM Adobe Managed Services: Installation via Customer Success Manager. Uppdateringarna var en del av det manuella uppdaterings-/underhållsarbetet.

## Konfiguration av slutpunkt

Slutpunkten konfigureras och uppdateras antingen via användargränssnittet i Cloud Manager eller via dess CLI.

**Tidigare CIF-versioner**

* CIF Classic: Via OSGi-konfiguration i AEM
* CIF öppen källkod: Via CIF Configuration Browser

## Distribution av CIF Venia-projektet

Projektet är tillgängligt i [Git-databas för Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) och driftsättning via [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html)

**Tidigare CIF-versioner**

* CIF Classic: Via AEM
* CIF öppen källkod: Via [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)

## Produktkatalogdata

Produktkatalogdata hämtas vid behov via realtidsanrop till en extern slutpunkt som stöder de GraphQL API:er som krävs. Dessa API:er har stöd för åtkomst till livedata eller mellanlagrade data vid ett visst datum. Ingen replikering behövs.

**Tidigare CIF-versioner**

* CIF Classic: Live- och mellanlagrade produktdata importeras och lagras i JCR på AEM Author via import av hela eller deltaprodukter. Live-produktdata replikeras till AEM Publish.

## Produktkatalogupplevelser med AEM rendering

AEM återger produktkatalogupplevelser direkt med hjälp AEM katalogmallar som har tilldelats produkter och kategorier. Ingen replikering behövs.

**Tidigare CIF-versioner**

* CIF Classic: AEM Author skapar en AEM sida för varje kategori/produkt med hjälp av katalogdesignverktyget. Dessa sidor replikeras till AEM Publish.

>[!NOTE]
>
>Mer information om hur du använder CIF med AEM hanterade tjänster eller AEM lokalt finns i [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
