---
title: Komma igång med omfaktoriseringsverktyg
description: Lär dig komma igång med Refactoring Tools i AEM as a Cloud Service
exl-id: 84394bdd-2b92-4f5d-b08a-7dc2c681baa4
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 1%

---

# Komma igång med omfaktoriseringsverktyg {#getting-started-refactoring-tools}

## Tillgänglighet {#availability}

<!-- Alexandru: duplicate contextualhelp id, drafting this for now

>[!CONTEXTUALHELP]
>id="aemcloud_rs_upload"
>title="Download"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html" text="Release Notes"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Software Distribution Portal"

-->

## Köra omfaktoriseringsverktygen {#running-refactoring-tools}

Använd omfaktoriseringsverktyget för att migrera din kod för kompatibilitet med AEM as a Cloud Service.

1. Om du inte har skapat något CAM-projekt än läser du [Skapa och hantera ett projekt i CAM](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md#create-project).
1. Klicka på **Code Refactoring**-kortet för att överföra källkoden.

   ![bild](/help/journey-migration/refactoring-tools/assets/rscam1.png)

1. När du först öppnar **Source-kodvyn** visas ett tomt läge där du uppmanas att överföra din källkod.

   ![bild](/help/journey-migration/refactoring-tools/assets/rscam2.png)

## Överför Source Code {#uploading}

När kunderna först använder **omfaktoriseringsverktygen** får de ett tomt läge i **Source-kodvyn**. Följ stegen nedan för att ladda upp ditt projekt och påbörja inspektionen:

1. **Gå till projektöverföringssidan**\
   Klicka på knappen **Projektöverföring** i tomt läge för att starta överföringsprocessen.

   ![bild](/help/journey-migration/refactoring-tools/assets/rscam3.png)

1. **Överför din Source-kod**
   - Välj källkoden i ZIP-filen i dialogrutan för överföring.
   - Klicka på **Överför** för att börja.
   - Överföringsförloppet visas i dialogrutan. Varaktigheten beror på projektets storlek.

   ![bild](/help/journey-migration/refactoring-tools/assets/rscam4.png)

1. **Inspektionsprocess**
   - Efter överföring startar **inspektionsprocessen** automatiskt i bakgrunden.
   - **Source-kodvyn** visar nu ditt överförda projekt och dess inspektionsstatus.

1. **Inspektionsstatus** Inspektionsprocessen är utformad för att förenkla körningen av omfaktoriseringsverktyg genom att minska kostnaderna för manuella konfigurationer.

   Inspektionen kommer att visa någon av följande statusar:
   - **Körs** - Kontrollen pågår.
   - **Klar** - Inspektionen är klar. Nu kan du köra omfaktoriseringsverktyg.
   - **Misslyckades** - ett fel uppstod. Klicka på projektet för att granska inspektionsrapporten och lösa eventuella problem.

   ![bild](/help/journey-migration/refactoring-tools/assets/rscam5.png)

>[!NOTE]
>
>Om du överför ett nytt projekt tas det befintliga projektet bort. Kontrollera att alla nödvändiga data har sparats innan du fortsätter.

>[!NOTE]
>
>Omfaktoriseringsjobb kan bara utföras om källkodsöverföringen lyckas.

## Omfaktoriseringsjobb {#refactoring-jobs}

När du klickar på fliken **Omfaktoriseringsjobb** visas en lista med befintliga jobb. Om inga jobb har skapats ännu visas ett tomt läge där du uppmanas att skapa jobb.

![bild](/help/journey-migration/refactoring-tools/assets/rscam6.png)

### &#x200B;1. Skapa ett nytt omfaktoriseringsjobb

- Klicka på knappen **Skapa nytt jobb** .
- Välj önskade omfaktoriseringsverktyg.
- Klicka på **Start** för att starta omfaktoriseringsprocessen.

![bild](/help/journey-migration/refactoring-tools/assets/rscam7.png)

>[!NOTE]
>
>Du kan aktivera enskilda omfaktoriseringsjobb eller köra alla tillgängliga verktyg på en gång med alternativet **Alla verktyg tillsammans** .

### &#x200B;2. Jobbstatus

- **Körs** - Jobbet pågår. Statusuppdateringarna uppdateras automatiskt vid slutförande eller fel.
- **Slutförd** - Jobbet har slutförts. Du kan nu granska resultaten eller hämta den omarbetade koden.
- **Misslyckades** - Ett fel uppstod i jobbet. Klicka på jobbet för att visa detaljerade loggar och felsöka problemet.

![bild](/help/journey-migration/refactoring-tools/assets/rscam8.png)

När jobbet har slutförts blir knappen **Hämta** tillgänglig så att du kan hämta:

- **Det returnerade projektet**: Det här är den uppdaterade koden när omformningen har tillämpats. Kunder kan hämta den senaste koden för sitt projekt.
- **Aktivitetsloggar**: Under jobbkörningen loggas alla steg som har utförts av verktyget och de ändringar som har gjorts som en del av detta.
- **Sökningsrapport**: Den här rapporten innehåller objekt som inte har körts fullständigt av verktyget men som fortfarande behöver åtgärdas. Alla sådana ändringar loggas här.

![bild](/help/journey-migration/refactoring-tools/assets/rscam9.png)

>[!NOTE]
>
>Varje jobb kan ta upp till 1 timme att slutföra. Kontakta Adobe Support om statusen inte uppdateras.
