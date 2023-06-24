---
title: Hantera stora innehållsdatabaser
description: I det här avsnittet beskrivs hantering av stora innehållsdatabaser
exl-id: 21bada73-07f3-4743-aae6-2e37565ebe08
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '1816'
ht-degree: 0%

---

# Hantera stora innehållsdatabaser {#handling-large-content-repositories}

## Översikt {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="Hantera stora innehållsdatabaser"
>abstract="För att påskynda extraherings- och inmatningsfaserna i innehållsöverföringsaktiviteten avsevärt så att innehållet flyttas till AEM as a Cloud Service kan verktyget för innehållsöverföring (CTT) använda AzCopy som ett valfritt förkopieringssteg. När det här försteget är konfigurerat kopierar AzCopy i extraheringsfasen blober från Amazon S3 eller Azure Blob Storage till migreringsuppsättningens blobbutik. Under själva intaget kopierar AzCopy blober från migreringsuppsättningens blobbutik till AEM as a Cloud Service blobbutik."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html#setting-up-pre-copy-step" text="Komma igång med AzCopy som ett steg före kopiering"

Det kan ta flera dagar att kopiera många bloggar med innehållsöverföringsverktyget (CTT).
För att snabba upp extraherings- och inmatningsfaserna i innehållsöverföringsaktiviteten så att innehåll flyttas till AEM as a Cloud Service kan CTT använda [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) som ett valfritt förkopieringssteg. Detta förkopieringssteg kan användas när AEM är konfigurerad att använda ett Amazon S3-, Azure Blob Storage-datalager eller ett File Data Store. Steg före kopiering är mest effektivt för första fullständiga extrahering och förtäring. Vi rekommenderar dock inte att du använder pre-copy för efterföljande översta filer (om den översta storleken är mindre än 200 GB) eftersom det kan ge mer tid till hela processen. När det här försteget är konfigurerat kopierar AzCopy i extraheringsfasen blober från Amazon S3, Azure Blob Storage eller File data store till migreringsuppsättningens blobbutik. Under själva intaget kopierar AzCopy blober från migreringsuppsättningens blobbutik till AEM as a Cloud Service blobbutik.

## Viktiga överväganden innan du börjar {#important-considerations}

Följ avsnittet nedan för att förstå viktiga aspekter innan du börjar:

* Från och med version 2.0.16 av CTT görs precopy-inställningen automatiskt när paketet installeras. Om storleken på migreringsuppsättningen är större än 200 GB används dessutom funktionen för förhandsgranskning automatiskt i extraheringsprocessen. Filen azcopy.config skapas i katalogen crx-quickstart/cloud-migration/. Du behöver inte konfigurera prekopian manuellt om du använder CTT version 2.0.16 eller senare.

* AEM måste vara 6.3-6.5.

* AEM är konfigurerat att använda Amazon S3 eller Azure Blob Storage. Mer information finns i [Konfigurera nodarkiv och datalager i AEM 6](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html).

* Varje migreringsuppsättning kopierar hela datalagret, så bara en migreringsuppsättning ska användas.

* Du måste ha tillgång till installationen [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) på den instans (eller VM) som kör AEM.

* Skräpinsamlingen för datalagret har körts inom de senaste sju dagarna på källan. Mer information finns i [Skräpinsamling för datalager](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html#data-store-garbage-collection).

### Ytterligare överväganden om AEM är konfigurerad att använda ett Amazon S3- eller Azure Blob Storage Data Store {#additional-considerations-amazons3-azure}

* Det är en kostnad som är kopplad till överföring av data från Amazon S3 och Azure Blob Storage. Överföringskostnaden är relativ till den totala mängden data i din befintliga lagringsbehållare (oavsett om det hänvisas till i AEM eller inte). Se [Amazon S3](https://aws.amazon.com/s3/pricing/) och [Azure Blob Storage](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) för mer information.

* Du behöver antingen en åtkomstnyckel och ett hemligt nyckelpar för den befintliga Amazon S3-källkodsbucket, eller en SAS URI för den befintliga Azure Blob Storage-källbehållaren (skrivskyddad åtkomst är bra).

### Ytterligare överväganden om AEM är konfigurerad att använda fildatalagret {#additional-considerations-aem-instance-filedatastore}

* Det lokala systemet måste ha ett ledigt utrymme som är större än storleken 1/256 för källdatalagret. Om datalagrets storlek till exempel är 3 terabyte måste det finnas ett ledigt utrymme som är större än 11,72 GB i `crx-quickstart/cloud-migration` på källan för att AzCopy ska fungera. Källsystemet bör ha minst 1 GB ledigt utrymme. Du kan frigöra utrymme genom att använda `df -h` i Linux®-instanser och kommandot dir i Windows-instanser.

* Varje gång extraheringen körs med AzCopy aktiverat förenklas hela fildatalagret och kopieras till molnmigreringsbehållaren. Om din migreringsuppsättning är mindre än storleken på datalagret är AzCopy-extraheringen inte den optimala metoden.

* När AzCopy har använts för att kopiera över det befintliga datalagret kan du inaktivera det för delta- eller top-up-extraheringar.

## Konfigurera för att använda AzCopy som ett förkopieringssteg {#setting-up-pre-copy-step}

>[!NOTE]
>Från och med version 2.0.16 av CTT görs precopy-inställningen automatiskt när paketet installeras. Om storleken på migreringsuppsättningen är större än 200 GB används dessutom funktionen för förhandsgranskning automatiskt i extraheringsprocessen. Filen azcopy.config skapas i katalogen crx-quickstart/cloud-migration/. Om du vill uppdatera filens konfiguration manuellt läser du avsnitten nedan.

Följ det här avsnittet för att lära dig hur du konfigurerar att använda AzCopy som ett förkopieringssteg med verktyget Innehållsöverföring för att migrera innehållet till AEM as a Cloud Service:

### 0. Bestämma den totala storleken för allt innehåll i datalagret {#determine-total-size}

Det är viktigt att fastställa den totala storleken på datalagret av två skäl:

* Om AEM är konfigurerad att använda fildatalagret måste det lokala systemet ha ett utrymme som är större än storleken 1/256 för källdatalagret.

#### Azure Blob Storage Data Store {#azure-blob-storage}

På sidan med behållaregenskaper i Azure-portalen använder du **Beräkna storlek** för att bestämma storleken på allt innehåll i behållaren. Till exempel:

![bild](/help/journey-migration/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Amazon S3 - datalager {#amazon-data}

Du kan använda behållarens Metrisk-flik för att bestämma storleken på allt innehåll i behållaren. Till exempel:


![bild](/help/journey-migration/content-transfer-tool/assets/amazon-s3-data-store.png)

#### Fildatalager {#file-data-store-determine-size}

* För Mac, UNIX®, kör du kommandot du i datastore-katalogen för att få dess storlek:
  `du -sh [path to datastore on the instance]`. Om datalagret till exempel finns på `/mnt/author/crx-quickstart/repository/datastore`, får du med följande kommando dess storlek: `du -sh /mnt/author/crx-quickstart/repository/datastore`.

* I Windows använder du kommandot dir i datastore-katalogen för att få fram dess storlek:
  `dir /a/s [location of datastore]`.

### 1. Installera AzCopy {#install-azcopy}

[AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) är ett kommandoradsverktyg från Microsoft® som måste vara tillgängligt i källinstansen för att den här funktionen ska kunna aktiveras.

Kort och gott: du vill ladda ned binärfilen Linux® x86-64 från [AzCopy-dokumentsida](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) och ta bort det från en plats som /usr/bin.

>[!IMPORTANT]
>Observera var du placerade binärfilen, eftersom du behöver den fullständiga sökvägen till den i ett senare steg.

### 2. Installera CTT (Content Transfer Tool) med stöd för AzCopy {#install-ctt-azcopy-support}

>[!IMPORTANT]
>Den senast släppta versionen av CTT bör användas.

Stöd för AzCopy för Amazon S3, Azure Blob Storage och File Data Store ingår i den senaste CTT-versionen.
Du kan hämta den senaste versionen av CTT från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) portal.
Observera att endast version 2.0.0 och senare stöds, och det är lämpligt att använda den senaste versionen.

### 3. Konfigurera en azcopy.config-fil {#configure-azcopy-config-file}

I AEM källinstansen `crx-quickstart/cloud-migration`, skapa en fil med namnet `azcopy.config`.

>[!NOTE]
>Innehållet i den här konfigurationsfilen skiljer sig åt beroende på om AEM använder ett Azure- eller Amazon S3-datalager eller ett File-datalager.

#### Azure Blob Storage Data Store {#azure-blob-storage-data}

Filen azcopy.config bör innehålla följande egenskaper (se till att du använder rätt azCopyPath och azureSas för din instans).

>[!NOTE]
>
> Om du inte vill ge skrivåtkomst till den befintliga lagringsbehållaren för blob kan du generera en ny SAS-URI som bara har läs- och listbehörighet.

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Amazon S3 - datalager {#amazon-sdata-store}

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

#### Fildatalager {#file-data-store-azcopy-config}

Dina `azcopy.config` filen måste innehålla egenskapen azCopyPath och den valfria egenskapen database.home som pekar på platsen för fildatalagret. Använd rätt värden för instansen.
Fildatalager

```
azCopyPath=/usr/bin/azcopy
repository.home=/mnt/crx/author/crx-quickstart/repository/datastore
```

Egenskapen azCopyPath måste innehålla den fullständiga sökvägen till den plats där kommandoradsverktyget azCopy är installerat på AEM. Om egenskapen azCopyPath saknas utförs inte blobbens precopy-steg.

If `repository.home` egenskapen saknas i azcopy.config, och därefter standardplatsen för datalagret `/mnt/crx/author/crx-quickstart/repository/datastore` används för att utföra precopy.

### 4. Extrahera med AzCopy {#extracting-azcopy}

När konfigurationsfilen ovan är på plats körs förkopieringsfasen av AzCopy som en del av varje efterföljande extrahering. Du kan förhindra att den körs genom att byta namn på filen eller ta bort den.

>[!NOTE]
>Om AzCopy inte är korrekt konfigurerad ser du följande meddelande i loggarna:
>`INFO c.a.g.s.m.c.a.AzCopyCloudBlobPreCopy - Blob pre-copy is not supported`.

1. Starta en extrahering från CTT-gränssnittet. Se [Komma igång med verktyget Innehållsöverföring](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) och [Extraheringsprocess](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) för mer information.

1. Bekräfta att följande rad skrivs ut i extraheringsloggen:

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

Grattis! Det här logginlägget innebär att din konfiguration ansågs vara giltig och att AzCopy kopierar alla blober från källbehållaren till flyttningsbehållaren.

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

Eventuella blobbar som kopierades före felet hoppas över automatiskt av AzCopy vid efterföljande körningar och behöver inte kopieras igen.

#### För fildatalager {#file-data-store-extract}

När AzCopy körs för källfilens dataStore bör du se meddelanden som dessa i loggarna som anger att mapparna bearbetas:
`c.a.g.s.m.c.a.AzCopyFileSourceBlobPreCopy - [AzCopy pre-copy] Processing folder (1/24) crx-quickstart/repository/datastore/5d`

### 5. Ingesting with AzCopy {#ingesting-azcopy}

Se [Infoga innehåll i mål](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
om du vill ha allmän information om hur du importerar innehåll till målet från CAM-hanteraren (Cloud Acceleration Manager), inklusive anvisningar om hur du använder AzCopy (pre-copy) eller inte, i dialogrutan Nytt intag.

För att du ska kunna utnyttja AzCopy vid intag måste du ha en AEM as a Cloud Service version som är minst version 2021.6.5561.

Se listan &quot;Inmatningsjobb&quot; i Cloud Accelerationshanteraren och i ingressens loggar så att du kan se förloppet. Loggposterna som hör till de slutförda AzCopy-åtgärderna visas enligt följande (vilket kan medföra vissa skillnader). Om du kontrollerar loggarna vid olika tillfällen kan du få en varning om problem tidigt och hjälpa dig att hitta en snabb lösning på eventuella problem.

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

## What&#39;s Next {#whats-next}

Du har nu lärt dig att hantera stora innehållsdatabaser för att snabba upp extraherings- och inmatningsfaserna i innehållsöverföringsaktiviteten så att innehållet flyttas till AEM as a Cloud Service. Nu kan du lära dig extraheringsprocessen med verktyget Innehållsöverföring. Se [Extrahera innehåll från källan i verktyget Innehållsöverföring](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) så att du kan lära dig hur du extraherar din migreringsuppsättning från verktyget Innehållsöverföring.
