---
title: Indexkonverterare
description: Indexkonverterare
translation-type: tm+mt
source-git-commit: 1117f03b2eff37f8b25726c3dc60d5a3fe98a5d1
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# Indexkonverterare {#index-converter}

Indexkonverteraren är ett verktyg som utvecklats för att migrera en kunds indexdefinitioner som förberedelse för övergången till AEM som en Cloud Service.

## Introduktion {#introduction}

Med indexkonverteraren kan AEM utvecklare migrera befintliga anpassade indexdefinitioner för ekon till AEM som en Cloud Service-kompatibel indexdefinition för ekon.

>[!NOTE]
>Indexkonverteraren omformar bara *lucene*-typens anpassade indexdefinitioner för eknos som finns under `/apps` eller `/oak:index`. Det omformar inte *lucene*-typindex som skapas för `nt:base`.

Det finns två sätt att skapa anpassade indexdefinitioner för eko:

* `under /apps` (via ett anpassat innehållspaket)
* direkt under `/oak:index`-sökvägen

Om [Kontrollera att ekindexvärdet](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) har använts bör du observera att Definitioner inte stöds i AEM som en Cloud Service och att de därför måste konverteras till ekindexdefinitioner först och sedan måste migreras till anpassade ekindexdefinitioner som är kompatibla med AEM som en Cloud Service enligt riktlinjerna nedan:

* Om egenskapen ignore är inställd på `true`, ignorera eller hoppa över Kontrollera definition
* Uppdatera `jcr:primaryType` till `oak:QueryIndexDefinition`
* Ta bort alla egenskaper som ska ignoreras enligt OSGi-konfigurationer
* Ta bort underträdet `/facets/jcr:content` från definitionen

## Använda indexkonverteraren {#using-index-converter}

* Via Adobe I/O CLI: Du bör använda indexkonverteraren via `aio-cli-plugin-aem-cloud-service-migration` (AEM som ett plugin-program för omfaktorisering av Cloud Service för Adobe I/O CLI).

Se **[Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** för att lära dig hur du installerar och använder plugin-programmet.

* Som fristående verktyg: Indexkonverteraren kan också köras som ett fristående verktyg.

Se **[Git-resurs: aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** om du vill veta hur du använder det här verktyget.



