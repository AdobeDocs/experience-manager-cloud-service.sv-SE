---
title: Databasmodernisering
description: Lär dig hur du strukturerar om befintliga projektpaket och gör dem kompatibla med den projektstruktur som har definierats för Adobe Experience Manager as a Cloud Service.
exl-id: cd9d212e-e720-4209-8b5a-659883cc1d95
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Databasmodernisering {#repo-modernizer}

Databasmodernisering är ett verktyg som utvecklats för att strukturera om befintliga projektpaket genom att dela upp innehåll och kod i separata paket som är kompatibla med den projektstruktur som definierats för Adobe Experience Manager as a Cloud Service.

## Introduktion {#introduction}

Adobe Experience Manager as a Cloud Service har många nya funktioner och möjligheter i dina AEM projekt. Det krävs dock vissa förändringar i Adobe Experience Manager Maven-projekten för att de ska vara kompatibla med AEM Cloud Service. På en hög nivå kräver AEM en separation av **content** och **code** till diskreta delpaket för att respektera delningen mellan muterbart och oföränderligt innehåll. Se [AEM Projektstruktur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=sv-SE) för mer information om den nya AEM projektstrukturen för Cloud Service.

Databasmodernisering skapar en kompatibel projektstruktur för AEM Cloud Service genom att skapa följande distributionsstruktur:

* Paketet `ui.apps` distribueras till `/apps` och innehåller all kod

* Paketet `ui.content` distribuerar till områden som kan skrivas under vid körning (till exempel `/content`, `/conf`, `/home` eller något annat som inte är `/apps`) och innehåller allt innehåll och all konfiguration.

* Paketet `all` är ett behållarpaket som innehåller underpaketen `ui.apps` och `ui.content`.

>[!NOTE]
>Projektstrukturen baseras på *Arketyp 24* för paket och deras `pom.xml/filter.xml files`. Mer information finns i [Arketyp 24](https://github.com/adobe/aem-project-archetype).

## Använda Repository Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* Som Adobe I/O CLI: Adobe rekommenderar vi att du använder Repository Modernizer via `aio-cli-plugin-aem-cloud-service-migration` (AEM as a Cloud Service-plugin för kodomfaktorisering för Adobe I/O CLI).

  Se **[Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** så att du kan lära dig hur du installerar och använder plugin-programmet.

* Som ett fristående verktyg: Databasmoderniseringen kan även köras som ett fristående verktyg.

  Se **[Git-resurs: Databasmodernisering](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** så att du kan lära dig hur du använder det här verktyget.

  >[!NOTE]
  >
  >Databasmodernizer utvecklas med NodeJS. NodeJS 10.0+ bör vara installerat.
