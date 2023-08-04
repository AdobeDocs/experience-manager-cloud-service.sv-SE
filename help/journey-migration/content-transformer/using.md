---
title: Använda innehållstransformeraren
description: Lär dig hur du omvandlar innehållsstrukturen som förberedelse för migrering till AEM as a Cloud Service.
source-git-commit: 8c73805b6ed1b7a03c65b4d21a4252c1412a5742
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 1%

---

# Använda innehållstransformeraren {#using-ct}

## Viktigt att tänka på när du använder innehållstransformeraren {#imp-considerations-ct}

Följ avsnittet nedan om du vill veta mer om viktiga aspekter av att använda innehållstransformeraren:

* Om du vill använda Content Transformer måste du först köra Best Practices Analyzer i din Adobe Experience Manager-miljö (AEM).
* Även om du kan köra Content Transformer i produktionsmiljön rekommenderar vi att du kör Content Transformer på en klon av produktionsmiljön. Dessutom måste du se till att BPA och CT körs i samma miljö.
* Du måste vara administratör i miljön där du vill köra innehållstransformeraren.
* Alla åtgärder som kan ändra källinnehållet ( move/remove/rename ) skapar som standard ett säkerhetskopieringspaket med källsökvägarna under `/etc/packages/content-transformation` före omformningen. Även om varje åtgärdsdialogruta har ett alternativ för att inaktivera/aktivera skapande av säkerhetskopieringspaket, rekommenderar vi att du alltid har aktiverat generering av paket.
* Varje sida i innehållstransformeraren är konfigurerad att innehålla högst 50 upptäckter, vilket innebär att maximalt 50 upptäckter kan omformas. Detta görs för att ge ett svar i rätt tid på användargränssnittet.

## Tillgänglighet {#availability-ct}

Innehållstransformeraren paketeras med [Verktyget Innehållsöverföring](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) som kan laddas ned som en zip-fil från Software Distribution Portal. Du kan installera paketet via Package Manager på AEM.

>[!NOTE]
>Innehållsomvandlaren är tillgänglig med verktyget Innehållsöverföring v2.0.20 eller senare.

## Öppna innehållstransformeraren {#opening-ct}

1. Logga in på AEM som administratör och gå till startsidan: https://host:port/aem/start.html.
1. Navigera till Verktyg > Åtgärder > Innehållsmigrering

   ![bild](/help/journey-migration/content-transformer/assets/ct-1.png)

   >[!NOTE]
   > Kontrollera att du har kört BPA-rapporten tidigare och verifiera den med URL:en http://host:port/apps/best-practices-analyzer/content/BestPracticesReport.html

1. Klicka på kortet med en titel **Content Transformer for BPA report**

   ![bild](/help/journey-migration/content-transformer/assets/ct-2.png)

   Nedan visas ett exempel på hur sidan Översikt över innehållstransformering ser ut om BPA-rapporten skapades och om innehållsrelaterade problem påträffades.

   Den återstående förfallotiden för BPA-rapporten visas på sidospåret. Vi rekommenderar att du kör innehållstransformeraren med den senaste BPA-rapporten för att undvika att innehållsrelaterade brister saknas.

   ![bild](/help/journey-migration/content-transformer/assets/ct-3.png)

1. Du kan filtrera problemen baserat på `Pattern Code`, `Subtype`, `Importance`och `Source`.

   ![bild](/help/journey-migration/content-transformer/assets/ct-4.png)

1. Du kan markera alla eller specifika problem och vidta åtgärder som att flytta, ta bort och byta namn på dem för att lösa dem. Anpassade banor kan också läggas till med **Lägg till banor** längst upp till höger.

   >[!NOTE]
   > När du använder flyttåtgärden bör du flytta alla sökvägar till endast en mapp (till exempel under `/etc/packages/content-transformation/paths`), så när säkerhetskopieringspaketen installeras för att återföra instansen till det ursprungliga läget, är mappen (`/etc/packages/content-transformation/paths`) kan tas bort med åtgärden remove för att minska databasstorleken.

   ![bild](/help/journey-migration/content-transformer/assets/ct-5.png)
   ![bild](/help/journey-migration/content-transformer/assets/ct-6.png)

   >[!NOTE]
   > Alla åtgärder som kan ändra källinnehållet (`move`/`remove`/`rename`) skapas som standard ett säkerhetskopiepaket med källsökvägarna under `/etc/packages/content-transformation` före omformningen. Även om varje åtgärdsdialogruta har ett alternativ för att inaktivera/aktivera skapande av säkerhetskopieringspaket, rekommenderar vi att du alltid har aktiverat generering av paket.

1. Ett exempel på ett säkerhetskopieringspaket som skapats för flyttningsåtgärden för sökvägarna visas nedan. Klicka på Installera för att återställa källsökvägarna. Observera att installationen endast tar tillbaka källsökvägarna till deras ursprungliga plats och inte tar bort sökvägarna som de flyttades till under omformningen. Om du vill ta bort banorna på den flyttade platsen klickar du på **Lägg till banor** knapp för att lägga till platsen (till exempel `/etc/packages/content-transformation/paths`) väljer du platsen och klickar på **Ta bort**.

   >[!CAUTION]
   > Ta inte bort `/etc/packages/content-transformation` eftersom det är platsen där säkerhetskopieringspaketen finns. Du kan bara ta bort den här platsen om du är säker på att du inte behöver dessa paket längre för att minska databasstorleken.

   ![bild](/help/journey-migration/content-transformer/assets/ct-7.png)
   ![bild](/help/journey-migration/content-transformer/assets/ct-8.png)
