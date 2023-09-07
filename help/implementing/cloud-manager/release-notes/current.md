---
title: Versionsinformation om Cloud Manager 2023.8.0 i Adobe Experience Manager as a Cloud Service
description: Detta är versionsinformationen för Cloud Manager 2023.8.0 i AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 3eee8a88b9945bb16be992d7157f9f7f3e816246
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---


# Versionsinformation om Cloud Manager 2023.8.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

Den här sidan dokumenterar versionsinformationen för Cloud Manager version 2023.8.0 i AEM as a Cloud Service.

>[!NOTE]
>
>Se [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md) för den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager version 2023.8.0 i AEM as a Cloud Service är 10 augusti 2023. Nästa version är planerad till den 14 september 2023.

## Nyheter {#what-is-new}

* När en innehållsuppsättning konfigureras till [kopiera innehåll,](/help/implementing/developing/tools/content-copy.md) [kontextmedvetna konfigurationer](/help/implementing/developing/introduction/configurations.md) tillåts nu i innehållsuppsättningar i användargränssnittet.
* Förbättringar har gjorts för att förbättra förståelsen och visningen av felmeddelanden i användargränssnittet i Cloud Manager.

## Tidig användning {#early-adoption}

Bli en del av vårt program för tidig användning och få möjlighet att testa några kommande funktioner.

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

## Felkorrigeringar {#bug-fixes}

* The **Miljö** menyn stängs nu när **[Kopiera innehåll](/help/implementing/developing/tools/content-copy.md)** modal.
* [En omkörning av en pipeline](/help/implementing/cloud-manager/deploy-code.md#reexecute-deployment) tillåts inte längre om föregående körning inte har en `commitId` anges för byggfastillståndet.
* Ett mer begripligt meddelande visas nu för sällsynta fel när en användare klickar på en pipeline i **Aktivitet** eller **Pipeline** skärmar.
* The `contentSetName` värdet saknas inte längre i loggarna och anges nu i indata när en [innehållskopia](/help/implementing/developing/tools/content-copy.md) operation.
* Under vissa sällsynta omständigheter är det inte längre möjligt att påbörja två exekveringar från samma pipeline, vilket leder till ett fastnat tillstånd.
* När ett certifikat upphör att gälla tas inte längre domännamn och IP-listor som är associerade med certifikatet bort från CDN.
   * I sådana fall kan webbplatsen fortfarande nås.
   * [Användargränssnittet i Cloud Manager](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) ger mer synliga, avancerade varningar om att SSL-certifikatet snart upphör att gälla.
* Ett problem med att AEM förlora åtkomst till en publiceringsslutpunkt har korrigerats i situationer när Sites läggs till som en lösning i ett program som bara innehåller resurser.
