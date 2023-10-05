---
title: Versionsinformation om Cloud Manager 2023.10.0 i Adobe Experience Manager as a Cloud Service
description: Detta är versionsinformationen för Cloud Manager 2023.10.0 i AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: b760b3a65d89b0b4f924379fc460015a58e2ed3e
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---


# Versionsinformation om Cloud Manager 2023.10.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

Den här sidan dokumenterar versionsinformationen för Cloud Manager version 2023.10.0 i AEM as a Cloud Service.

>[!NOTE]
>
>Se [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md) för den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager version 2023.10.0 i AEM as a Cloud Service är 5 oktober 2023. Nästa version planeras till den 2 november 2023.

## Nyheter {#what-is-new}

* Förbättringar av [indexering](/help/operations/indexing.md) har kortare varaktighet för pipeline när nya index distribueras.
   * Förbättringarna varierar beroende på innehållsprofilen.
* Automatisk [uppdateringar för utvecklingsmiljöer](/help/implementing/cloud-manager/manage-environments.md#updating-environments) är aktiverade som standard för nya program, vilket sparar tid när du behöver köra uppdateringar manuellt.
   * Den här uppdateringen kommer att lanseras stegvis.
* I oktober 2023-versionen av Cloud Manager uppdateras Java-versionerna med en stegvis utrullning.
   * De mindre versionerna för Java 8 och 11 samt Maven har uppdaterats och kommer att lanseras stegvis under de kommande två månaderna. Den nya versionen har flera säkerhetskorrigeringar och felkorrigeringar. De nya versionerna är
   * *Maven: 3.8.8*
   * *Java 8 version: /usr/lib/jvm/jdk1.8.0_371*
   * *Java 11 version: /usr/lib/jvm/jdk-11.0.20*
   * [Se OpenJDK-råden](https://openjdk.org/groups/vulnerability/advisories/) om du vill ha information om säkerhet och felkorrigeringar i dessa JDK-uppdateringar.

## Tidig användning {#early-adoption}

Bli en del av vårt program för tidig användning och få möjlighet att testa några kommande funktioner.

### Anpassade behörigheter {#custom-permissions}

[Anpassade behörigheter för Cloud Manager](/help/implementing/cloud-manager/custom-permissions.md) Med kan du skapa nya anpassade behörighetsprofiler med konfigurerbara behörigheter för att begränsa åtkomst till program, pipelines och miljöer för användare av Cloud Manager.

om du är intresserad av att testa den nya funktionen och dela med dig av dina synpunkter, skicka ett e-postmeddelande `Grp-CloudManager-custom-permissions@adobe.com` från den e-postadress som är kopplad till din Adobe ID.

### Självbetjäning för återställning av innehåll {#content-restore}

[En ny självbetjäningsfunktion för innehållsåterställning](/help/operations/restore.md) erbjuder nu säkerhetskopiering för återställning i upp till sju dagar och är tillgänglig för tidiga användare i utvärderingssyfte som omfattar:

* Säkerhetskopiering vid bestämda tidpunkter för de senaste 24 timmarna
* Återställningar i upp till sju dagar

Om du vill testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till `aemcs-restorefrombackup-adopter@adobe.com` via e-post som är kopplad till din Adobe ID. Observera:

* Det tidiga adopterprogrammet är begränsat till utvecklingsmiljöer.
* Tillgången till programmet för tidig användning av den här funktionen är begränsad.
* Den här funktionen används för att återställa innehåll som har tagits bort av misstag och är inte avsedd för katastrofåterställning.

### Kontrollpanelen för Experience Audit {#experience-audit-dashboard}

[Kontrollpanelen för Experience Audit i Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md) innehåller en trendvy över dina sidresultatspoäng tillsammans med insikter och rekommendationer som hjälper dig att förbättra dem. Experience Audit ingår som ett steg i Cloud Managers produktionsflöde.

Kontrollpanelen använder Google Lightroom, ett automatiserat verktyg med öppen källkod som förbättrar kvaliteten på dina webbprogram. Du kan köra det mot alla webbsidor, offentliga eller som kräver autentisering. Den har granskningar av prestanda, tillgänglighet, progressiva webbprogram, SEO med mera.

Är du intresserad av att testa den nya instrumentpanelen? Skicka e-post till `aem-lighthouse-pilot@adobe.com` via ditt e-postmeddelande som är kopplat till din Adobe ID så kommer vi igång.
