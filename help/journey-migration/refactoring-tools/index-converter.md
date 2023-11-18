---
title: Indexkonverterare
description: Lär dig hur du migrerar indexdefinitioner som förberedelse för övergången till AEM as a Cloud Service.
exl-id: ac02ca41-eb35-4f24-bf17-d00ce318423d
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Indexkonverterare {#index-converter}

Index Converter är ett verktyg som utvecklats för att migrera en kunds indexdefinitioner inför övergången till AEM as a Cloud Service.

## Introduktion {#introduction}

Med indexkonverteraren kan AEM utvecklare migrera befintliga anpassade indexdefinitioner för oak till AEM as a Cloud Service kompatibla indexdefinitioner för oak.

>[!NOTE]
>Endast indexkonverterare omformningar *lucen* ange definitioner för anpassade ekindexvärden som finns under `/apps` eller `/oak:index`. Den omformas inte *lucen* typindex som skapas för `nt:base`.

Det finns två sätt att skapa anpassade indexdefinitioner för eko:

* `under /apps` (via ett anpassat innehållspaket)
* direkt under `/oak:index` bana

If [Kontrollera läckindex](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) användes, kontrollera att definitioner inte stöds på AEM as a Cloud Service. De måste därför först konverteras till indexdefinitioner för ekolor och sedan migreras till anpassade indexdefinitioner för ekolor som är kompatibla med AEM as a Cloud Service, enligt riktlinjerna nedan:

* Om egenskapen ignore är inställd på `true`, ignorera eller hoppa över Skräddarsy definition
* Uppdatera `jcr:primaryType` till `oak:QueryIndexDefinition`
* Ta bort alla egenskaper som ska ignoreras enligt OSGi-konfigurationer
* Ta bort underträd `/facets/jcr:content` från Kontrollera definition

## Använda indexkonverteraren {#using-index-converter}

* Som Adobe I/O CLI: Adobe rekommenderar vi att du använder indexkonverteraren via `aio-cli-plugin-aem-cloud-service-migration` (AEM plugin-program för omfaktorisering av as a Cloud Service kod för CLI-programmet för Adobe I/O).

  Se **[Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** om du vill lära dig hur du installerar och använder plugin-programmet.

* Som ett fristående verktyg: Indexkonverteraren kan också köras som ett fristående verktyg.

  Se **[Git-resurs: aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** om du vill lära dig hur du använder det här verktyget.
