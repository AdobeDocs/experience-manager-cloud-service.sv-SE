---
title: Validerar innehållsöverföringar (äldre)
description: Använd verktyget Innehållsöverföring för att validera innehållsöverföringar
hide: true
hidefromtoc: true
exl-id: 304b7aee-1d84-4d90-a89b-0c532d5d9c92
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 1%

---

# Validerar innehållsöverföringar (äldre) {#validating-content-transfers}

## Komma igång {#getting-started}

Användarna kan på ett tillförlitligt sätt avgöra om allt innehåll som extraherats av verktyget Innehållsöverföring har importerats till målinstansen. Den här valideringsfunktionen fungerar genom att jämföra en sammanfattning av de noder som berördes under extraheringen med en sammanfattning av noder som berördes vid förtäringen. Om det finns några nodsökvägar i extraheringssammanfattningen som saknas i importen, anses valideringen ha misslyckats och ytterligare manuell validering kan vara nödvändig.

>[!INFO]
>
>Den här funktionen är tillgänglig från och med version 1.8.x av verktyget för innehållsöverföring (CTT). AEM Cloud Service målmiljö måste köra minst version 6158 eller senare. Källmiljön måste också vara konfigurerad för att kunna köras [förkopia](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#setting-up-pre-copy-step). Valideringsfunktionen söker efter filen azcopy.config i källan. Om filen inte hittas körs inte valideringen. Mer information om hur du konfigurerar en azcopy.config-fil finns i [den här sidan](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#configure-azcopy-config-file).

Det är valfritt att validera en innehållsöverföring. Om du aktiverar den här funktionen ökar både tiden det tar att utföra en extrahering och ett intag. Om du vill använda funktionen aktiverar du den i systemkonsolen för AEM genom att följa dessa steg:

1. Navigera till Adobe Experience Manager Web Console i källinstansen genom att gå till **Verktyg - Åtgärder - Webbkonsol** eller direkt till URL:en på *https://serveraddress:serverport/system/console/configMgr*
1. Sök efter **Konfiguration av extraheringstjänst för innehållsöverföringsverktyg**
1. Använd pennikonknappen för att redigera dess konfigurationsvärden
1. Aktivera **Aktivera migreringsvalidering vid extrahering** ställa in och sedan trycka **Spara**:

   ![bild](/help/journey-migration/content-transfer-tool/assets/CTTvalidation1.png)

När den här inställningen är aktiverad och målmiljön i AEM Cloud Service kör en kompatibel version, kommer migreringsvalideringen att utföras under all extrahering och de efterföljande förslagen.

Mer information om hur du installerar verktyget Innehållsöverföring finns i [Komma igång med verktyget Innehållsöverföring](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).

## Validera en innehållsöverföring {#how-to-validate-a-content-transfer}

När migreringsvalidering är aktiverat i AEM källmiljö påbörjar du en extrahering.

If **Skriv över mellanlagringsbehållaren under extraheringen** är aktiverat loggas alla noder som är inblandade i extraheringen till extraheringssökvägssammanfattningen. När den här inställningen används är det viktigt att aktivera **Rensa befintligt innehåll i molninstansen före intag** Inställningen under intaget, annars kan det verka som att det saknas noder i matsmältningen. Detta är de noder som redan finns på målet från tidigare inmatningar.

En illustration av detta finns i exemplen nedan:

### Exempel 1 {#example-1}

* **Extrahering (skriv över)**

   ![bild](/help/journey-migration/content-transfer-tool/assets/CTTextractionoverwrite.png)

* **Inmatning (svep)**

   ![bild](/help/journey-migration/content-transfer-tool/assets/CTTingestionwipe.png)

* **Anteckningar**

   Den här kombinationen av Skriv över och Svep ger enhetliga valideringsresultat, även för upprepade inmatningar.

### Exempel 2 {#example-2}

* **Extrahering**

   ![bild](/help/journey-migration/content-transfer-tool/assets/CTTextraction.png)

* **Inmatning**

   ![bild](/help/journey-migration/content-transfer-tool/assets/CTTingestion.png)

* **Anteckningar**

   Kombinationen av Skriv över och Svep ger enhetliga valideringsresultat för det initiala intaget.

   Om intaget upprepas kommer ätningssammanfattningen att vara tom och valideringen verkar ha misslyckats. Inledningssammanfattningen är tom eftersom alla noder från den här extraheringen redan finns på målet.

När extraktionen är klar, börja intaget.

Inmatningsloggens överkant innehåller en post som påminner om `aem-ethos/tools:1.2.438`. Kontrollera att versionsnumret är **1.2.438** eller senare, annars stöds inte valideringen av AEM as a Cloud Service som du använder.

När intaget är klart och valideringen börjar, kommer följande loggpost att registreras i matningsloggen:

```
Gathering artifacts for migration validation...  
```

Utförlig information om valideringen följer efter den här posten. Hitta ett exempel från en stor migrering nedan:

```
Beginning publish migration validation. Migration job id=[3aba1f96-84b6-4bd0-8642-c61c0d528387]
Extraction path digest is being processed...
Extraction path digest processing took 982 seconds
Ingestion path digest is being processed...
Ingestion path digest processing took 999 seconds
Comparing the Extraction and Ingestion path digests...
----------------------------------------------------------
EXTRACTION: Number of nodes extracted: 51674784
INGESTION: Number of nodes ingested: 51674784
----------------------------------------------------------
Validation succeeded! No entries were detected to be missing from the ingestion digest.
----------------------------------------------------------
Comparing the path digests took 29 seconds
Migration validation took 33 minutes
```

Det här är ett exempel på en validering som har slutförts eftersom det inte fanns några poster som saknades i den digest som fanns i extraheringssammanfattningen.

Här kan du jämföra: Så här skulle en valideringsrapport se ut om valideringen hade misslyckats:

```
Beginning publish migration validation. Migration job id=[ac217e5a-a08d-4e81-cbd6-f39f88b174ce]
Extraction path digest is being processed...
Extraction path digest processing took 0 seconds
Ingestion path digest is being processed...
Ingestion path digest processing took 0 seconds
Comparing the Extraction and Ingestion path digests...
----------------------------------------------------------
EXTRACTION: Number of nodes extracted: 4635
INGESTION: Number of nodes ingested: 0
----------------------------------------------------------
Validation failed. However, the following nodes may already be present in the target environment.
Please refer to our Migration Validation FAQ (https://www.adobe.com/go/aem_cloud_ctt_validation_en) or open a ticket with Customer Care.
There are 4635 entries present in the extraction digest that are missing from the ingestion digest.
/content/dam/bruce
/content/dam/bruce-assets
... more paths listed (up to 10k) ...
----------------------------------------------------------
Comparing the path digests took 0 seconds
Migration validation took 0 minutes
```

Ovanstående felexempel uppnåddes genom att ett intag kördes och därefter kördes samma intag igen med rensning inaktiverat, så att inga noder berördes under intaget - allt fanns redan på målet.

Förutom att den ingår i inmatningsloggen kan även valideringsrapporten nås via användargränssnittet i verktyget Innehållsöverföring. Välj en migreringsuppsättning och klicka på **Validera** från åtgärdsfältet:


![bild](/help/journey-migration/content-transfer-tool/assets/CTTvalidatebutton.png)

Dialogrutan Valideringsloggar öppnas:

![bild](/help/journey-migration/content-transfer-tool/assets/CTTvalidationlogs.png)

Använd **Rapport om publicering/författare för validering** för att visa valideringsrapporten för det senaste intaget till den angivna nivån i målmiljön. Nedan finns ett exempel från ett litet publiceringsförslag:

![bild](/help/journey-migration/content-transfer-tool/assets/CTTvalidationreport.png)

>[!NOTE]
>
>The **Rapport om publicering/författare för validering** -länken visas när det är klart. Valideringsrapporterna är dessutom beständiga, så de upphör inte att gälla när intaget är slutfört, som i matningsloggarna.

## Felsökning {#troubleshooting}

### Valideringen misslyckades. Vad händer nu? {#validation-fail}

Det första steget är att avgöra om intag verkligen misslyckades eller om det extraherade innehållet redan finns i målmiljön. Detta kan inträffa om ett intag upprepas med **Rensa befintligt innehåll i molninstansen före intag** Alternativet är inaktiverat.

Verifiera genom att välja en sökväg i valideringsrapporten och kontrollera om den finns i målmiljön. Om det här är en publiceringsmiljö kan du vara begränsad till att kontrollera sidor och resurser direkt. Öppna en biljett hos Kundtjänst om du behöver hjälp med det här steget.

### Nodantalet är lägre än jag förväntade mig. Varför det? {#node-count-lower-than-expected}

Vissa vägar från extraherings- och intagssammanfattningarna exkluderas för att hålla storleken på dessa filer hanterbar, med målet att kunna beräkna migreringens valideringsresultat inom två timmar efter att intaget har slutförts.

De sökvägar vi för närvarande utesluter från sammanfattningarna är: `cqdam.text.txt` återgivningar, noder i `/home`och noder i `/jcr:system`.
