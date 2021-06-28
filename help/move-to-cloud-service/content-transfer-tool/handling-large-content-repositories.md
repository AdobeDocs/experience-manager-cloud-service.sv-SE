---
title: Hantera stora innehållsdatabaser
description: I det här avsnittet beskrivs hantering av stora innehållsdatabaser
source-git-commit: 1299a4bd4e4139c971680e439a3b366162af0de2
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 1%

---


# Hantera stora innehållsdatabaser {#handling-large-content-repositories}

## Översikt {#overview}

Det kan ta flera dagar att kopiera ett stort antal bloggar med innehållsöverföringsverktyget (CTT).
För att påskynda extraherings- och inmatningsfaserna i innehållsöverföringsaktiviteten avsevärt så att innehåll flyttas till AEM som en Cloud Service, kan CTT utnyttja [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) som ett valfritt förkopieringssteg. Detta förkopieringssteg kan användas när AEM är konfigurerad att använda ett Amazon S3- eller Azure Blob Storage-datalager.  När det här försteget är konfigurerat kopierar AzCopy i extraheringsfasen blober från Amazon S3 eller Azure Blob Storage till migreringsuppsättningens blobbutik. Under själva intaget kopierar AzCopy blober från migreringsuppsättningens blobbutik till AEM som en Cloud Service blobbutik.

>[!NOTE]
> Den här funktionaliteten introducerades i CTT 1.5.4-versionen.

## Viktiga överväganden innan du börjar {#important-considerations}

Följ avsnittet nedan för att förstå viktiga aspekter innan du börjar:

* AEM 6.3-6.5
* AEM är konfigurerat att använda Amazon S3 eller Azure Blob Storage. Mer information finns i [Konfigurera nodarkiv och datalager i AEM 6](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en).
* Hela datalagret kopieras under extraheringen. Eftersom det finns en kostnad som är kopplad till överföring av data från både Amazon S3 och Azure Blob Storage, kommer överföringskostnaden att vara relativ till den totala mängden data i lagringsbehållaren (oavsett om det hänvisas till i AEM eller inte). Mer information finns i [Amazon S3](https://aws.amazon.com/s3/pricing/) och [Azure Blob Storage](https://azure.microsoft.com/en-us/pricing/details/bandwidth/).
* Varje migreringsuppsättning kopierar hela datalagret, så bara en migreringsuppsättning ska användas.
* Du måste ha åtkomst för att kunna installera [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) på den instans (eller VM) som kör AEM.
* Du behöver antingen ett åtkomstnyckel och hemligt nyckelpar för Amazon S3-källkodsbucket eller en SAS URI för Azure Blob Storage-källbehållaren (skrivskyddad åtkomst är bra).
* Skräpinsamlingen för datalagret har körts inom de senaste 7 dagarna på källan. Mer information finns i [Skräpinsamling för datalager](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en#data-store-garbage-collection).
* Huvuddelen av data i källinstansen inkluderas i migreringen.

## Konfigurera för att använda AzCopy som ett förkopieringssteg {#setting-up-pre-copy-step}

Följ det här avsnittet för att lära dig hur du konfigurerar att använda AzCopy som ett förkopieringssteg med verktyget Innehållsöverföring för att migrera innehållet till AEM som en Cloud Service:

### 0. Bestämma den totala storleken för allt innehåll i datalagret {#determine-total-size}

#### Azure Blob Storage Data Store {#azure-blob-storage}

Använd knappen **Beräkna storlek** på sidan för behållaregenskaper i Azure-portalen för att avgöra storleken på allt innehåll i behållaren. Till exempel:

![bild](/help/move-to-cloud-service/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Amazon S3 - datalager {#amazon-data}

Du kan använda behållarens Metrisk-flik för att bestämma storleken på allt innehåll i behållaren. Till exempel:


![bild](/help/move-to-cloud-service/content-transfer-tool/assets/amazon-s3-data-store.png)

### 1. Installera AzCopy {#install-azcopy}

[](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) AzCopy är ett kommandoradsverktyg från Microsoft som måste vara tillgängligt på källinstansen för att den här funktionen ska kunna aktiveras.

Kort och gott är att du troligen vill hämta binärfilen för Linux x86-64 från sidan [AzCopy-dokument](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) och ta bort den från en plats, t.ex. /usr/bin. Observera var du placerade binärfilen, eftersom du behöver den fullständiga sökvägen till den i ett senare steg.

### 2. Installera en version av Content Transfer Tool (CTT) med stöd för AzCopy {#install-ctt-azcopy-support}

Stöd för AzCopy finns i CTT 1.5.4. Du kan hämta den senaste versionen av CTT från [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)-portalen.

### 3. Konfigurera en azcopy.config-fil {#configure-azcopy-config-file}

Skapa en ny fil med namnet azcopy.config i AEM crx-quickstart/cloud-migration .

Innehållet i den här konfigurationsfilen kommer att vara annorlunda beroende på om AEM använder ett Azure- eller Amazon S3-datalager.

#### Azure Blob Storage Data Store {#azure-blob-storage-data}

Filen azcopy.config bör innehålla följande egenskaper (se till att du använder rätt azCopyPath och azureSas för din instans).

>[!NOTE]
>
> Om du inte vill ge skrivåtkomst till blobblagringsbehållaren kan du generera en ny SAS-URI som bara har läs- och listbehörighet.

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Amazon S3 - datalager {#amazon-data-store}

Filen azcopy.config bör innehålla följande egenskaper (se till att använda rätt värden för din instans).

>[!NOTE]
>
> Om din instans använder IAM-roller för att aktivera AEM för åtkomst till S3, måste du skapa en profil och användare med åtgärderna ListBucket och GetObject aktiverade för S3-bucket. Använd användarens åtkomstnyckel och hemliga nyckel när du väl har konfigurerat den.

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

### 4. Extrahera med AzCopy {#extracting-azcopy}

När ovanstående konfigurationsfil är på plats körs AzCopy-förkopieringsfasen som en del av varje efterföljande extrahering. Du kan förhindra att den körs genom att byta namn på filen eller ta bort den.

1. Starta en extrahering från CTT-gränssnittet. Mer information finns i [Köra verktyget Innehållsöverföring](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool) och [Extraheringsprocessen](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process).
1. Bekräfta att följande rad skrivs ut i extraheringsloggen:

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

Grattis! Det här logginlägget innebär att konfigurationen ansågs vara giltig och att AzCopy kopierar alla blober från källbehållaren till flyttningsbehållaren.

Loggposterna från AzCopy visas i extraheringsloggen och har prefixet c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [AzCopy pre-copy]

>[!CAUTION]
>
> Under de första minuterna av en extrahering bör du noggrant se efter om det finns några tecken på ett problem i extraheringsloggarna. Här är till exempel vad som skulle loggas om Azure-källbehållaren inte kunde hittas:


```
[AzCopy pre-copy] failed to perform copy command due to error: cannot start job due to error: cannot list files due to reason -> github.com/Azure/azure-storage-blob-go/azblob.newStorageError, github.com/Azure/azure-storage-blob-go@v0.10.1-0.20210407023846-16cf969ec1c3/azblob/zc_storage_error.go:42
[AzCopy pre-copy] ===== RESPONSE ERROR (ServiceCode=ContainerNotFound) =====
[AzCopy pre-copy] Description=The specified container does not exist.
[AzCopy pre-copy] RequestId:5fb674b9-201e-001b-2a5b-527400000000
[AzCopy pre-copy] Time:2021-05-26T18:18:07.5931967Z, Details: 
[AzCopy pre-copy] Code: ContainerNotFound
```

Om ett problem uppstår med AzCopy misslyckas extraheringen omedelbart och extraheringsloggarna innehåller information om felet.

Alla blobbar som kopierats före felet hoppas över automatiskt av AzCopy vid efterföljande körningar och behöver inte kopieras igen.

### 5. Ingesting with AzCopy {#ingesting-azcopy}

I och med Content Transfer Tool 1.5.4 har vi lagt till AzCopy-stöd för redigering.

>[!NOTE]
> Rekommendationen är att enbart köra Author-intag. Detta snabbar upp inläsningen av publiceringen när den körs senare.

För att kunna dra nytta av AzCopy vid förtäring måste du ha en AEM som en Cloud Service version som är minst version 2021.6.5561.

Börja skriva in författarförslaget från CTT-gränssnittet. Mer information finns i [Instruktionsprocessen](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process).
Loggposterna från AzCopy visas i matningsloggen. De kommer att se ut så här:

```
*************** Beginning AzCopy pre-copy phase ***************
INFO: Scanning...
INFO: Failed to create one or more destination container(s). Your transfers may still succeed if the container already exists.
INFO: Any empty folders will not be processed, because source and/or destination doesn't have full folder support
INFO: azcopy: A newer version 10.11.0 is available to download
 
 
Job 419d98da-fc05-2a45-70cc-797fee632031 has started
Log file is located at: /root/.azcopy/419d98da-fc05-2a45-70cc-797fee632031.log
 
 
0.0 %, 0 Done, 0 Failed, 886 Pending, 0 Skipped, 886 Total,
 
 
Job 419d98da-fc05-2a45-70cc-797fee632031 summary
Elapsed Time (Minutes): 0.0334
Number of File Transfers: 886
Number of Folder Property Transfers: 0
Total Number of Transfers: 886
Number of Transfers Completed: 17
Number of Transfers Failed: 0
Number of Transfers Skipped: 869
TotalBytesTransferred: 248350
Final Job Status: CompletedWithSkipped
 
*************** Completed AzCopy pre-copy phase ***************
```
