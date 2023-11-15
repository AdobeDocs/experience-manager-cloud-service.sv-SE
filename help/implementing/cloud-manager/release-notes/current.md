---
title: Versionsinformation för Cloud Manager 2023.11.0 i Adobe Experience Manager as a Cloud Service
description: Detta är versionsinformationen för Cloud Manager 2023.11.0 i AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 3a9eaa162d62cd3e674f14ba39ed7c96ad271f79
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 0%

---


# Versionsinformation för Cloud Manager 2023.11.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

Den här sidan dokumenterar versionsinformationen för Cloud Manager version 2023.11.0 i AEM as a Cloud Service.

>[!NOTE]
>
>Se [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md) för den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för Cloud Manager version 2023.11.0 i AEM as a Cloud Service är 14 november 2023. Nästa version planeras till den 7 december 2023.

## Nyheter {#what-is-new}

* Brandvägg för webbaserade program-DDOS-skydd (WAF-DDOS) finns nu att köpa som en del av dina AEM as a Cloud Service rättigheter och [kan konfigureras på ett självbetjäningssätt.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* Specialiserad [config pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) finns nu för att konfigurera miljöinställningar, underhållsuppgifter, CDN-regler och mycket mer på några minuter.
* [När innehåll kopieras](/help/implementing/developing/tools/content-copy.md) från en högre miljö till en utvecklingsmiljö visas nu ett meddelande som talar om försiktighet vid kopiering av stora innehållsuppsättningar eftersom utvecklingsmiljöer är kapacitetsbegränsade.
* [Informationssidan för pipeline-körning](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) visar nu alla steg i en pipeline-körning med de som ännu inte har börjat nedtonade.
* På båda **[Aktivitet](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity)** och **[Pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines)** på sidor är en sammanfattning av pipeline-körningen nu tillgänglig när du klickar på en pipeline med en körningsstatus.
* En ny **Varaktighet** -avsnittet har lagts till i [informationssida för pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) som omfattar den genomsnittliga tiden för rörledningssteget baserat på den historiska trenden för det programmet.
* På [sidan för pipeline-körning,](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity-window) de färdiga stegen visar nu varaktighet.
* Körningar som [återanvänd build-artefakter](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) kommer nu att visa länken till den körning som ursprungligen skapade dessa artefakter.
* Alternativet som ska väljas **Viktiga måttfel** kan nu konfigureras för [pipelines för kodkvalitet](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) också.


## Tidig användning {#early-adoption}

Bli en del av vårt program för tidig användning och få möjlighet att testa några kommande funktioner.

### Hämta din egen GitHub {#byo-github}

Om du använder GitHub för att hantera dina databaser, [du kan nu validera kod direkt i dina GitHub-databaser via Cloud Manager.](/help/implementing/cloud-manager/managing-code/byo-github.md) Integreringen eliminerar behovet av att konsekvent synkronisera kod med Adobe-databasen och gör att du kan verifiera pull-begäranden innan du sammanfogar dem i huvudgrenarna.

Om du vill testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till `Grp-CloudManager_BYOG@adobe.com` från den e-postadress som är kopplad till din Adobe ID.

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

## Kända fel {#known-issues}

Det finns ett känt fel som förhindrar [config pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md##config-deployment-pipeline) från att knuffas till produktion.

Om **Pausa innan du distribuerar till produktion** är ett alternativ som krävs för en konfigurationspipeline. Följande är den föreslagna lösningen tills felet har åtgärdats.

1. Kör pipelinen.
1. Testa koden i mellanlagringsmiljön.
1. När distributionen och godkännandet blir tillgängligt klickar du på **Avvisa**.
1. Redigera pipeline för att inaktivera **Pausa innan du distribuerar till produktion** alternativ.
1. Kör pipelinen igen. Den kommer att köras igen vid mellanlagring och sedan vid produktion.
