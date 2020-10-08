---
title: Databasmodernisering
description: Databasmodernisering
translation-type: tm+mt
source-git-commit: 5da0d4cc8c6d8781dd7cce8bbbde207568a6d10b
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 3%

---


# Databasmodernisering {#repo-modernizer}

Databasmodernisering är ett verktyg som utvecklats för att strukturera om befintliga projektpaket genom att dela upp innehåll och kod i separata paket som är kompatibla med den projektstruktur som definierats för Adobe Experience Manager som en Cloud Service.

## Introduktion {#introduction}

Adobe Experience Manager som Cloud Service innehåller många nya funktioner och möjligheter i dina AEM projekt. Det krävs dock vissa förändringar i Adobe Experience Manager Maven-projekten för att de ska vara kompatibla med AEM Cloud Service. På en hög nivå kräver AEM en separation av **innehåll** och **kod** i diskreta delpaket för att respektera uppdelningen mellan muterbart och oföränderligt innehåll. Se [AEM projektstruktur](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) för mer information om den nya AEM projektstrukturen för Cloud Service.

Databasmodernisering skapar en kompatibel projektstruktur för AEM Cloud Service genom att skapa följande distributionsstruktur:

* `ui.apps` paketet distribuerar till `/apps` och innehåller all kod

* `ui.content` paket distribuerar till områden som kan skrivas under körning (t.ex. `/content`, `/conf`, `/home`eller något annat som inte `/apps`) och innehåller allt innehåll och all konfiguration.

* `all` paketet är ett behållarpaket som innehåller underpaketen `ui.apps` och `ui.content`.

>[!NOTE]
>Projektstrukturen baseras på *Arketyp 24* för paket och deras `pom.xml/filter.xml files`. Mer information finns i [Archetype 24](https://github.com/adobe/aem-project-archetype) .

## Använda Repository Modernizer {#using-repo-modernizer}

* Via Adobe I/O CLI: Vi rekommenderar att du använder Repository Modernizer via `aio-cli-plugin-aem-cloud-service-migration` (AEM som ett plugin-program för omfaktorisering av Cloud Service för Adobe I/O CLI).

   Se **[Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** för att lära dig hur du installerar och använder plugin-programmet.

* Som fristående verktyg: Databasmoderniseraren kan också köras som ett fristående verktyg.

   Se **[Git-resurs: Databasmodernisering](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** om du vill lära dig hur du använder det här verktyget.

   >[!NOTE]
   >
   >Databasmoderniseringen utvecklas med NodeJS. NodeJS 10.0+ bör vara installerat.
