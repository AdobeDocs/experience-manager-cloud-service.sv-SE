---
title: Verifierar innehållsöverföringar
description: Använd verktyget Innehållsöverföring för att validera innehållsöverföringar
exl-id: a12059c3-c15a-4b6d-b2f4-df128ed0eea5
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---

# Verifierar innehållsöverföringar {#validating-content-transfers}

## Komma igång {#getting-started}

Användarna kan på ett tillförlitligt sätt avgöra om allt innehåll som extraherats av verktyget Innehållsöverföring har importerats till målinstansen. Den här valideringsfunktionen fungerar genom att jämföra en sammanfattning av sökvägarna för alla noder som berördes under extraheringen med en sammanfattning av sökvägarna för alla noder som berördes vid förtäringen. Om det finns några nodsökvägar i extraheringssammanfattningen som saknas i importen, anses valideringen ha misslyckats och ytterligare manuell validering kan vara nödvändig.

>[!INFO]
>
>Den här funktionen är tillgänglig från och med version 1.8.x av verktyget för innehållsöverföring (CTT). AEM Cloud Service målmiljö måste köra minst version 6158 eller senare. Källmiljön måste också vara konfigurerad för att köra [pre-copy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#setting-up-pre-copy-step). Valideringsfunktionen söker efter filen azcopy.config i källan. Om filen inte hittas körs inte valideringen. Mer information om hur du konfigurerar en azcopy.config-fil finns på [den här sidan](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#configure-azcopy-config-file).

Det är valfritt att validera en innehållsöverföring. Om du aktiverar den här funktionen ökar både tiden det tar att utföra en extrahering och ett intag. Om du vill använda funktionen aktiverar du den i systemkonsolen för AEM genom att följa dessa steg:

1. Gå till Adobe Experience Manager Web Console på din källinstans genom att gå till **Verktyg - Åtgärder - Webbkonsol** eller direkt till URL:en på *https://serveraddress:serverport/system/console/configMgr*
1. Sök efter **Konfiguration av extraheringstjänst för innehållsöverföringsverktyg**
1. Använd pennikonknappen för att redigera dess konfigurationsvärden
1. Aktivera inställningen **Aktivera migreringsvalidering under extrahering** och tryck sedan på **Spara**:

   ![bild](/help/journey-migration/content-transfer-tool/assets/CTTvalidation1.png)

När den här inställningen är aktiverad och målmiljön i AEM Cloud Service kör en kompatibel version, kommer migreringsvalideringen att utföras under all extrahering och de efterföljande förslagen.

Mer information om hur du installerar verktyget Innehållsöverföring finns i [Komma igång med verktyget Innehållsöverföring](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).

## Validera en innehållsöverföring {#how-to-validate-a-content-transfer}

När migreringsvalidering är aktiverat i AEM källmiljö påbörjar du en extrahering.

Om **Skriv över mellanlagringsbehållaren under extraheringen** är aktiverat loggas alla noder som är inblandade i extraheringen till extraheringssökvägssammanfattningen. När den här inställningen används är det viktigt att aktivera inställningen **Rensa befintligt innehåll i molninstansen före intag** vid förtäring, annars kan det finnas noder som saknas i uppslutningssammanfattningen. Detta är de noder som redan finns på målet från tidigare inmatningar.

En grafisk illustration av detta finns i följande exempel:

### Exempel 1 {#example-1}

* **Extrahering (skriv över)**

  ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/validation-01.png)

* **Inmatning (svepning)**

  ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/validation-02.png)

* **Anteckningar**

  Den här kombinationen av Skriv över och Svep ger enhetliga valideringsresultat, även för upprepade inmatningar.

### Exempel 2 {#example-2}

* **Extrahering**

  ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/validation-03.png)

* **Inmatning**

  ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/validation-04.png)

* **Anteckningar**

  Kombinationen av Skriv över och Svep ger enhetliga valideringsresultat för det initiala intaget.

  Om intaget upprepas, är ätningssammanfattningen tom och valideringen verkar ha misslyckats. Inledningssammanfattningen är tom eftersom alla noder från den här extraheringen redan finns på målet.

När extraktionen är klar, börja intaget.

Inmatningsloggens överkant kommer att innehålla en post som liknar `aem-ethos/tools:1.2.438`. Kontrollera att versionsnumret är **1.2.438** eller högre, annars stöds inte valideringen i den version av AEM as a Cloud Service som du använder.

När intaget är klart och valideringen börjar, noteras följande loggpost i matningsloggen:

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

Här kan du jämföra: Så här skulle en valideringsrapport se ut om valideringen hade misslyckats (eller om en tilläggsmigrering utfördes):

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
See our Migration Validation FAQ (https://www.adobe.com/go/aem_cloud_ctt_validation_en) or open a ticket with Customer Care.
There are 4635 entries present in the extraction digest that are missing from the ingestion digest.
/content/dam/bruce
/content/dam/bruce-assets
... more paths listed (up to 10k) ...
----------------------------------------------------------
Comparing the path digests took 0 seconds
Migration validation took 0 minutes
```

Ovanstående felexempel uppnåddes genom att ett intag kördes och därefter kördes samma intag igen med rensning inaktiverat, så att inga noder berördes under intaget - allt fanns redan på målet.

Förutom att den ingår i inmatningsloggen kan du även få åtkomst till verifieringsrapporten via användargränssnittet **Inmatningsjobb** i Cloud Acceleration Manager. Om du vill göra det klickar du på de tre punkterna (**..**) och sedan på **Valideringsrapport** i listrutan för att visa valideringsrapporten.


![bild](/help/journey-migration/content-transfer-tool/assets-ctt/CTTvalidationreportnew.png)

## Validera huvudmigreringen {#how-to-validate-principal-migration}

Läs [Användarmappning och huvudmigrering](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md) om du vill läsa information om huvudmigreringar och varför det är nödvändigt.

När extraheringen och intaget har slutförts finns en sammanfattning och rapport om den huvudsakliga migreringen. Den här informationen kan användas för att validera vilka användare och grupper som migrerats och, kanske, för att avgöra varför vissa inte gjorde det.

Om du vill se den här informationen går du till Cloud Acceleration Manager. Klicka på projektkortet och klicka på kortet för innehållsöverföring. Navigera till **Inmatningsjobb** och leta reda på det intag som du vill verifiera. Klicka på de tre punkterna (**..**) för det intagandet och klicka sedan på **Visa huvudsammanfattning** i listrutan.

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-action.png)

En dialogruta med den sammanfattande informationen visas. Använd hjälpikonerna för att läsa en mer fullständig beskrivning. Klicka på knappen **Hämta rapport** om du vill hämta den fullständiga kommaavgränsade (CSV) rapporten.

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-dialog.png)

>[!NOTE]
>
>Om användarmappning är inaktiverad visas en annan variant av den här dialogrutan. Det indikerar att användarmappningen har inaktiverats och inte visar de tre fälten som ger värden för användarmappning.

## Felsökning {#troubleshooting}

### Valideringen misslyckades. Vad händer nu? {#validation-fail}

Det första steget är att avgöra om intag verkligen misslyckades eller om det extraherade innehållet redan finns i målmiljön. Detta kan inträffa om ett intag upprepas med alternativet **Rensa befintligt innehåll i molninstansen innan intag** inaktiveras.

Verifiera genom att välja en sökväg i valideringsrapporten och kontrollera om den finns i målmiljön. Om det här är en publiceringsmiljö kan du vara begränsad till att kontrollera sidor och resurser direkt. Öppna en biljett hos Kundtjänst om du behöver hjälp med det här steget.

### Nodantalet är lägre än jag förväntade mig. Varför är det så? {#node-count-lower-than-expected}

Vissa vägar från extraherings- och intagssammanfattningarna exkluderas för att hålla storleken på dessa filer hanterbar, med målet att kunna beräkna migreringens valideringsresultat inom två timmar efter att intaget har slutförts.

De sökvägar som för närvarande utesluts från sammanfattningarna är: `cqdam.text.txt` återgivningar, noder i `/home` och noder i `/jcr:system`.

### Stängda användargrupper fungerar inte {#validating-cugs}

Mer information om hur du använder en CUG-princip (Closed User Group) finns i [Migrera stängda användargrupper](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md).
