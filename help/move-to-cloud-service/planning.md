---
title: Planeringsfas
description: Planeringsfas
exl-id: 987cb929-7871-4fec-8ef5-4d2f5f2f2186
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 88%

---

# Planering {#planning-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="Planera övergången"
>abstract="Innan du börjar din övergång till Cloud Service bör du bekanta dig med AEM as a Cloud Service och granska de ändringar som gjorts i den samt även se vilka funktioner som har ersatts eller tagits bort."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html" text="Best Practices Analyzer"

Innan du börjar din övergång till Cloud Service bör du bekanta dig med AEM as a Cloud Service och granska de ändringar som gjorts i den samt även se vilka funktioner som har ersatts eller tagits bort.

## Viktiga ändringar {#notable-changes}

AEM as a Cloud Service har många nya funktioner för  att administrera AEM-projekt.

Det finns dock ett antal skillnader mellan AEM On-premise och Adobe Managed Services jämfört med AEM as a Cloud Service.

Se [Viktiga ändringar i AEM Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html) för att få en förståelse för de viktiga skillnaderna.

## Borttagna funktioner {#deprecated-features}

Adobe utvärderar ständigt produktfunktioner för att så småningom förnya eller ersätta äldre funktioner med modernare alternativ för att förbättra det totala kundvärdet, alltid med noggrant övervägande av bakåtkompatibilitet.

Läs [Borttagna funktioner](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html#deprecated-features) om du vill veta mer om funktioner som har markerats som borttagna i Experience Manager as a Cloud Service.

## Förstå planeringsfasen {#introduction}

I följande bild visas de viktigaste stegen under planeringsfasen:

![bild](/help/move-to-cloud-service/assets/planning-phaseimg1.png)

### Utvärderar beredskap för Cloud Service{#access-cloud-readiness}

Det första steget i planeringsfasen är att utvärdera om du är redo att gå över från din befintliga AEM-version till Cloud Service och identifiera områden som kräver omstrukturering för att vara kompatibla med AEM as a Cloud Service.

Du måste göra en omfattande utvärdering av din aktuella AEM-källkod mot de märkbara ändringarna och de borttagna funktionerna för att avgöra hur stor insats som förväntas under övergången.

Du kan snabba upp bedömningssteget genom att köra Best Practices Analyzer på den aktuella AEM. Mer information finns i [Best Practices Analyzer](/help/move-to-cloud-service/best-practices-analyzer/overview-best-practices-analyzer.md).

>[!NOTE]
>Om du redan har tillgång till Cloud Manager och en Cloud Service-miljö rekommenderar vi att du kör den aktuella koden i en kvalitetspipeline för Cloud Manager-kod för att utvärdera om de kodändringar som krävs är kompatibla med Cloud Service.

### Granska resursplanering {#review-resource-planning}

När du har uppskattat den nivå av arbete som krävs för att gå över till Cloud Service bör du identifiera resurser, skapa ett team och mappa roller och ansvarsområden för övergångsprocessen.

### Fastställa nyckeltal {#establish-kpis}

Om du inte har fastställt nyckeltal (KPI) tidigare rekommenderar vi att du skapar nyckeltal för implementeringen av Adobe Experience Manager (AEM) så att ditt team kan fokusera på det som är viktigast.

Läs [Utveckla nyckeltal](https://guided.adobe.com/welcome/aem/part6.html) för att lära dig hur du väljer rätt nyckeltal för dina affärsmål.
