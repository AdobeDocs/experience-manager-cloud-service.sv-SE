---
title: Planeringsfas
description: Planeringsfas
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# Planering {#planning-phase}

Innan du börjar din övergångsresa till molntjänsten bör du bekanta dig med AEM som en molntjänst och granska de ändringar som gjorts i den samt även se vilka funktioner som har ersatts eller tagits bort.

## Betydande ändringar {#notable-changes}

AEM som en molntjänst har många nya funktioner och möjligheter för att hantera dina AEM-projekt.

Det finns dock ett antal skillnader mellan AEM On-Local och Adobe Managed Services jämfört med AEM som en molntjänst.

Se [Observerbara ändringar i AEM Cloud-tjänsten](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/aem-cloud-changes.html) för att få en förståelse för de viktiga skillnaderna.

## Föråldrade funktioner {#deprecated-features}

Adobe utvärderar ständigt produktfunktioner för att så småningom förnya eller ersätta äldre funktioner med modernare alternativ för att förbättra det totala kundvärdet, alltid med noggrant övervägande av bakåtkompatibilitet.

Mer information om [borttagna funktioner](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/deprecated-removed-features.html#deprecated-features) och funktioner som har markerats som borttagna i Experience Manager som en molntjänst finns i Föråldrade funktioner.

## Förstå planeringsfasen {#introduction}

I följande bild visas de viktigaste stegen under planeringsfasen:

![image](/help/move-to-cloud-service/assets/planning-phaseimg1.png)

### Utvärderar beredskap för molntjänst {#access-cloud-readiness}

Det första steget i planeringsfasen är att utvärdera om du är redo att gå över från din befintliga AEM-version till molntjänsten och fastställa områden som kräver omfaktorisering för att vara kompatibel med AEM som molntjänst.

Du måste göra en omfattande utvärdering av din aktuella AEM-källkod mot de märkbara ändringarna och de borttagna funktionerna för att avgöra hur stor insats som förväntas under övergångsresan.

>[!NOTE]
>Om du redan har tillgång till Cloud Manager och en molntjänstmiljö rekommenderar vi att du kör den aktuella koden i en kvalitetspipeline för Cloud Manager-kod för att utvärdera om de kodändringar som krävs är kompatibla med molntjänsten.

### Granska resursplanering {#review-resource-planning}

När du har uppskattat den nivå av arbete som krävs för att gå över till molntjänsten bör du identifiera resurser, skapa ett team och mappa roller och ansvarsområden för övergångsprocessen.

### Fastställa nyckeltal {#establish-kpis}

Om du inte har fastställt nyckeltal (KPI) tidigare rekommenderar vi att du skapar nyckeltal för implementeringen av Adobe Experience Manager (AEM) så att ditt team kan fokusera på det som är viktigast.

Se [Utveckla nyckeltal](https://guided.adobe.com/welcome/aem/part6.html) för att lära dig hur du väljer rätt nyckeltal för dina affärsmål.

