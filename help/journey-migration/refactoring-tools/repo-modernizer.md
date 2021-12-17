---
title: Databasmodernisering
description: Databasmodernisering
source-git-commit: a6d225943c5d23ebd960fda0b0912a81f1f80014
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Databasmodernisering {#repo-modernizer}

Databasmodernisering är ett verktyg som utvecklats för att strukturera om befintliga projektpaket genom att dela upp innehåll och kod i separata paket som är kompatibla med den projektstruktur som definierats för Adobe Experience Manager as a Cloud Service.

## Introduktion {#introduction}

Adobe Experience Manager as a Cloud Service har många nya funktioner och möjligheter i dina AEM projekt. Det krävs dock vissa förändringar i Adobe Experience Manager Maven-projekten för att de ska vara kompatibla med AEM Cloud Service. På en hög nivå kräver AEM att **innehåll** och **kod** till diskreta delpaket för att ta hänsyn till uppdelningen mellan muterbart och oföränderligt innehåll. Se [AEM projektstruktur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) om du vill ha mer information om den nya AEM projektstrukturen för Cloud Service.

Databasmodernisering skapar en kompatibel projektstruktur för AEM Cloud Service genom att skapa följande distributionsstruktur:

* `ui.apps` paket distribuerar till `/apps` och innehåller all kod

* `ui.content` paket distribuerar till områden som kan skrivas under körning (t.ex. `/content`, `/conf`, `/home`eller något som inte `/apps`) och innehåller allt innehåll och all konfiguration.

* `all` paketet är ett behållarpaket som innehåller underpaketen `ui.apps` och `ui.content`.

>[!NOTE]
>Projektstrukturen baseras på *Arketyp 24* för paket och deras `pom.xml/filter.xml files`. Se [Arketyp 24](https://github.com/adobe/aem-project-archetype) för mer information.

## Använda Repository Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* Via Adobe I/O CLI: Vi rekommenderar att du använder Repository Modernizer via `aio-cli-plugin-aem-cloud-service-migration` (AEM plugin-program för omfaktorisering av as a Cloud Service kod för CLI-programmet för Adobe I/O).

   Se **[Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** för att lära dig hur du installerar och använder plugin-programmet.

* Som fristående verktyg: Databasmoderniseraren kan också köras som ett fristående verktyg.

   Se **[Git-resurs: Databasmodernisering](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** om du vill lära dig hur du använder det här verktyget.

   >[!NOTE]
   >
   >Databasmoderniseringen utvecklas med NodeJS. NodeJS 10.0+ bör vara installerat.
