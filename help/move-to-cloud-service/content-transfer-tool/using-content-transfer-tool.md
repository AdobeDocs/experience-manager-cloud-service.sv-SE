---
title: Använda Content Transfer Tool
description: Använda Content Transfer Tool
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: 5b569ab1b1cca7e5ec46b872f8726fddfc8b8d14
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 57%

---

# Använda Content Transfer Tool {#using-content-transfer-tool}

## Köra verktyget Innehållsöverföring på en publiceringsinstans {#running-ctt-on-publish}

Vi rekommenderar att CTT installeras på källpubliceringsinstansen när innehåll flyttas till en publiceringsinstans för att flytta innehållet till målpubliceringsinstansen. Följ de rekommenderade tillvägagångssätten som beskrivs nedan:

* Använd samma version av CTT som användes på Author-instansen.

* Endast en publiceringsnod behöver migreras. Den bör avlägsnas från belastningsutjämnaren innan extraheringen påbörjas.

* När du skapar en migreringsuppsättning använder du URL:en till författarens AEMaaCS-miljö.

* Under publiceringsprocessen kommer publiceringsnivån INTE att förminskas (till skillnad från författaren). Som en försiktighetsåtgärd bör du undvika att användare startar skrivåtgärder som:

   * Innehållsdistribution från AEMaaCS Author till Publish i den miljön
   * Användarsynkronisering mellan publiceringsinstanser


## Felsökning {#troubleshooting}

### Blobb-ID saknas {#missing-blobs}

Om blobb-ID saknas, som nämns nedan, måste en konsekvenskontroll utföras i den befintliga databasen och de saknade blobbarna återställas.
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

Följande kommando körs

>[!NOTE]
>
>`--verbose`-flaggan krävs för att rapportera nodsökvägar som refererar till blobbarna.

**För databaser AEM 6.5 (Oak 1.8 och tidigare)**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**För databaser med Oak > 1.10**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

Mer information finns i [Oak Runable Jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run).

Filerna som skapas i *OUT_DIR* som anges ovan för överensstämmelse, kan sedan kontrolleras för sökvägar som saknar binärfiler och lämpliga åtgärder kan vidtas, till exempel återställning från en säkerhetskopia, borttagning av sökvägar och omindexering.


### Gränssnittsbeteende {#ui-behavior}

Som användare kan du se följande beteendeförändringar i användargränssnittet i Content Transfer Tool:

* Ikonerna i gränssnittet för verktyget för innehållsöverföring kan se annorlunda ut än skärmbilderna som visas i den här handboken, eller också visas de inte alls beroende på versionen av AEM-källinstansen.
