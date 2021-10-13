---
title: Felsöka verktyget Innehållsöverföring
description: Felsöka verktyget Innehållsöverföring
source-git-commit: 27e68cd282414da4cc23c3ba276b0fb3c330d49c
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 93%

---


# Felsöka verktyget Innehållsöverföring {#troubleshoot-content-transfer-tool}


## Blobb-ID saknas {#missing-blobs}

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


## Gränssnittsbeteende {#ui-behavior}

Som användare kan du se följande beteendeförändringar i användargränssnittet i Content Transfer Tool:

* Ikonerna i gränssnittet för verktyget för innehållsöverföring kan se annorlunda ut än skärmbilderna som visas i den här handboken, eller också visas de inte alls beroende på versionen av AEM-källinstansen.
