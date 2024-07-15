---
title: Indexkonverterare
description: Lär dig hur du migrerar indexdefinitioner som förberedelse för övergången till AEM as a Cloud Service.
exl-id: ac02ca41-eb35-4f24-bf17-d00ce318423d
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Indexkonverterare {#index-converter}

Index Converter är ett verktyg som utvecklats för att migrera en kunds indexdefinitioner inför övergången till AEM as a Cloud Service.

## Introduktion {#introduction}

Med indexkonverteraren kan AEM utvecklare migrera befintliga anpassade Oak-indexdefinitioner till AEM as a Cloud Service-kompatibla anpassade Oak-indexdefinitioner.

>[!NOTE]
>Indexkonverteraren omformar bara anpassade Oak-indexdefinitioner av typen *lucene* som finns under `/apps` eller `/oak:index`. Den transformerar inte *lucene*-typindex som skapas för `nt:base`.

Det finns två sätt att skapa anpassade Oak Index-definitioner:

* `under /apps` (via ett anpassat innehållspaket)
* direkt under sökvägen `/oak:index`

Om [Kontrollera att Oak Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) användes kontrollerar du att definitioner inte stöds i AEM as a Cloud Service. Därför måste de först konverteras till Oak Index Definitions och sedan migreras till anpassade Oak Index Definitions som är kompatibla med AEM as a Cloud Service enligt riktlinjerna nedan:

* Om ignorerad egenskap är inställd på `true`, ignorera eller hoppa över Kontrollera definition
* Uppdatera `jcr:primaryType` till `oak:QueryIndexDefinition`
* Ta bort alla egenskaper som ska ignoreras enligt OSGi-konfigurationer
* Ta bort underträdet `/facets/jcr:content` från Kontrollera definition

## Använda indexkonverteraren {#using-index-converter}

* Som Adobe I/O CLI: Adobe rekommenderar vi att du använder indexkonverteraren med `aio-cli-plugin-aem-cloud-service-migration` (AEM as a Cloud Service-plugin för kodomfaktorisering för Adobe I/O CLI).

  Mer information om hur du installerar och använder plugin-programmet finns i **[Git-resurs: aio-cli-plugin-program-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**.

* Som ett fristående verktyg: Indexkonverteraren kan också köras som ett fristående verktyg.

  Se **[Git-resurs: aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** om du vill veta mer om hur du använder det här verktyget.
