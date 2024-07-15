---
title: Betydande ändringar av Commerce integrationa frameworken (CIF)
description: Betydande ändringar av Commerce integrationa frameworken (CIF) jämfört med tidigare CIF.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
feature: Commerce Integration Framework
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# Betydande ändringar i tillägget för Commerce integration framework (CIF){#notable-changes}

Adobe Experience Manager as a Cloud Service har många nya funktioner och möjligheter att hantera dina AEM projekt. Om du vill veta mer om de här funktionerna kan du följa länken för [ändringar i Experience Manager as a Cloud Service](/help/release-notes/aem-cloud-changes.md).

I det här dokumentet beskrivs de viktiga skillnaderna mellan tilläggen för Commerce integration framework (CIF) och äldre CIF, så kallade CIF Classic (Quickstart) och CIF OpenSource.

## Installation och uppdateringar

Tillägget AEM CIF installeras via Cloud Manager. Installationen kräver en CIF, förutom för sandlådor där CIF kan installeras utan krediter. Krediter tas emot automatiskt via etablering av CIF tillägg i ditt AEM.

Tillägget uppdateras automatiskt som en del av den vanliga AEM as a Cloud Service-uppdateringen.

**Tidigare CIF versioner**

* CIF Classic: Ingen installation behövs. CIF ingick i QuickStart. CIF uppdateringar ingick i regelbundna AEM- eller servicepaketuppdateringar
* CIF öppen källkod för AEM lokalt: Installation via GitHub. Uppdateringarna var en del av det manuella uppdaterings-/underhållsarbetet.
* CIF öppen källkod för AEM Adobe Managed Services: Installation via Adobe Account Team. Uppdateringarna var en del av det manuella uppdaterings-/underhållsarbetet.

## Konfiguration av slutpunkt

Slutpunkten konfigureras och uppdateras antingen via Cloud Manager UI eller dess CLI.

**Tidigare CIF versioner**

* CIF Classic: Via OSGi-konfiguration i AEM
* CIF öppen källkod: via CIF Configuration Browser

## Driftsättning CIF Veniaprojektet

Projektet är tillgängligt i [Cloud Manager Git-databas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/integrating-with-git.html) och distributionen görs via [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html)

**Tidigare CIF versioner**

* CIF Classic: Genom att AEM
* CIF öppen källkod: Via [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)

## Produktkatalogdata

Produktkatalogdata efterfrågas vid behov via realtidsanrop till en extern slutpunkt som stöder de GraphQL API:er som krävs. Dessa API:er har stöd för åtkomst till livedata eller mellanlagrade data vid ett visst datum. Ingen replikering behövs.

**Tidigare CIF versioner**

* CIF Classic: Live- och mellanlagrade produktdata importeras och lagras i JCR på AEM Author via import av full- eller deltaprodukter. Live-produktdata replikeras till AEM Publish.

## Produktkatalogupplevelser med AEM rendering

AEM återger produktkatalogupplevelser direkt med hjälp AEM katalogmallar som har tilldelats produkter och kategorier. Ingen replikering behövs.

**Tidigare CIF versioner**

* CIF Classic: AEM skapar en AEM sida för varje kategori/produkt med hjälp av katalogritningsverktyget. Dessa sidor replikeras till AEM Publish.

>[!NOTE]
>
>Mer information om hur du använder CIF med AEM hanterade tjänster eller AEM lokalt finns i [Commerce integration framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
