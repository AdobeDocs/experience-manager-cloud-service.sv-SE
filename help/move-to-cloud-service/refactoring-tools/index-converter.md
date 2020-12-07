---
title: Indexkonverterare
description: Indexkonverterare
translation-type: tm+mt
source-git-commit: adfc453729b88a9cc457783806eb7b4d69150b21
workflow-type: tm+mt
source-wordcount: '170'
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

Se **[Git-resurs: aem-cs-source-migration-index-converter](https://git.corp.adobe.com/vavarshn/aem-cloud-service-source-migration/blob/master/packages/index-converter/README.md)** om du vill veta hur du installerar och använder plugin-programmet.

