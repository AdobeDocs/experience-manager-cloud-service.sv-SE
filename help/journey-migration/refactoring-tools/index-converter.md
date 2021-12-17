---
title: Indexkonverterare
description: Indexkonverterare
source-git-commit: a6d225943c5d23ebd960fda0b0912a81f1f80014
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Indexkonverterare {#index-converter}

Index Converter är ett verktyg som utvecklats för att migrera en kunds indexdefinitioner inför övergången till AEM as a Cloud Service.

## Introduktion {#introduction}

Med indexkonverteraren kan AEM utvecklare migrera befintliga anpassade indexdefinitioner för oak till AEM as a Cloud Service kompatibla indexdefinitioner för oak.

>[!NOTE]
>Indexkonverterare, endast omformningar *lucen* ange definitioner för anpassade ekindexvärden som finns under `/apps` eller `/oak:index`. Den omformas inte *lucen* typindex som skapas för `nt:base`.

Det finns två sätt att skapa anpassade indexdefinitioner för eko:

* `under /apps` (via ett anpassat innehållspaket)
* direkt under `/oak:index` bana

If [Kontrollera läckindex](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) har använts, observera att det inte finns stöd för definitioner på AEM as a Cloud Service, och att de därför måste konverteras till indexdefinitioner på eknoder först och sedan måste migreras till anpassade indexdefinitioner för eknoder som är kompatibla med AEM as a Cloud Service enligt nedanstående riktlinjer:

* Om egenskapen ignore är inställd på `true`, ignorera eller hoppa över definitionen av Säkerställ
* Uppdatera `jcr:primaryType` till `oak:QueryIndexDefinition`
* Ta bort alla egenskaper som ska ignoreras enligt OSGi-konfigurationer
* Ta bort underträd `/facets/jcr:content` från Kontrollera definition

## Använda indexkonverteraren {#using-index-converter}

* Via Adobe I/O CLI: Du bör använda indexkonverteraren via `aio-cli-plugin-aem-cloud-service-migration` (AEM plugin-program för omfaktorisering av as a Cloud Service kod för CLI-programmet för Adobe I/O).

   Se **[Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** för att lära dig hur du installerar och använder plugin-programmet.

* Som fristående verktyg: Indexkonverteraren kan också köras som ett fristående verktyg.

   Se **[Git-resurs: aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** om du vill lära dig hur du använder det här verktyget.
