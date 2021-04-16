---
title: Betydande ändringar av tillägget Commerce Integration Framework (CIF)
description: Betydande ändringar av Commerce Integration Framework (CIF) jämfört med tidigare CIF-versioner.
exl-id: c136763f-56aa-450e-8796-bc84bf6c205d
translation-type: tm+mt
source-git-commit: 97574c964e757ffa4d108340f6a4d1819050d79a
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 5%

---

# Noterbara ändringar av tillägget CIF (Commerce Integration Framework){#notable-changes}

Adobe Experience Manager som Cloud Service har många nya funktioner och möjligheter att hantera dina AEM projekt. Om du vill veta mer om de här funktionerna kan du följa länken för [ändringar av Experience Manager som Cloud Service](/help/release-notes/aem-cloud-changes.md).

I det här dokumentet belyses de viktiga skillnaderna mellan tillägget i Commerce Integration Framework (CIF) och äldre CIF-versioner, främst kända som CIF Classic (QuickStart) som öppen källkod.

## Installation och uppdateringar

AEM CIF-tillägg installeras via Cloud Manager. Installationen kräver en CIF-kredit förutom för sandlådor där CIF kan installeras utan krediter. Krediter tas emot automatiskt via provisionering av CIF-tillägget i ditt AEM.

Tillägget uppdateras automatiskt som en del av den vanliga AEM när Cloud Servicen uppdateras.

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

Projektet finns i [Cloud Manager Git-databas](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) och distributionen görs via [Cloud Manager](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html)

**Tidigare CIF-versioner**

* CIF Classic: Via AEM
* CIF öppen källkod: Via [Cloud Manager](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)

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
