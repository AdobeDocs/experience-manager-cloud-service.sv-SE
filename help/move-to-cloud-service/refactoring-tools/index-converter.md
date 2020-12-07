---
title: Indexkonverterare
description: Indexkonverterare
translation-type: tm+mt
source-git-commit: fecbd0b4d5cfd8aa970c235c79158bea44403c09
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Indexkonverterare {#index-converter}

Indexkonverteraren är ett verktyg som utvecklats för att migrera en kunds indexdefinition som förberedelse för övergången till AEM som en Cloud Service.

## Introduktion {#introduction}

Med indexkonverteraren kan AEM utvecklare migrera befintliga anpassade indexdefinitioner för ekon till AEM som en Cloud Service-kompatibel indexdefinition för ekon.

>[!NOTE]
>Indexkonverteraren omformar bara *lucene*-typens anpassade indexdefinitioner för eknos som finns under `/apps` eller `/oak:index`. Det omformar inte *lucene*-typindex som skapas för `nt:base`.

Det finns två sätt att skapa anpassade indexdefinitioner för eko:

* `under /apps` (via ett anpassat innehållspaket)
* direkt under `/oak:index`-sökvägen

>[!NOTE]
>Se [Se till att ekindexvärdet](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) är korrekt för att lära dig hur du definierar och skapar ekeldefinitioner

## Använda indexkonverteraren {#using-index-converter}

>[!NOTE]
>Även om du bör använda verktyget Indexkonverterare via [AIO CLI-plugin för källmigrering](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration), kan det också köras fristående.

Se **[Git-resurs: aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** om du vill veta hur du installerar och använder plugin-programmet.

