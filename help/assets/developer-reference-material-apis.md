---
title: Utvecklarreferenser för [!DNL Assets]
description: '[!DNL Assets] APIs and developer reference content lets you manage assets, including binary files, metadata, renditions, comments, and [!DNL Content Fragments].'
contentOwner: AG
feature: API:er,Resurser HTTP API
role: Developer,Architect,Administrator
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: 597098cd94d1e40dc45870fd2c0b986f80eb2038
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager Assets] användningsfall för utvecklare, API:er och referensmaterial  {#assets-cloud-service-apis}

Artikeln innehåller rekommendationer, referensmaterial och resurser för utvecklare av [!DNL Assets] som en [!DNL Cloud Service]. Den innehåller en ny modul för överföring av resurser, API-referens och information om stödet som ges i arbetsflöden efter bearbetning.

## [!DNL Experience Manager Assets] API:er och åtgärder  {#use-cases-and-apis}

[!DNL Assets] som en  [!DNL Cloud Service] innehåller flera API:er för programmässig interaktion med digitala resurser. Varje API har stöd för särskilda användningsfall, vilket framgår av tabellen nedan. [!DNL Assets]-användargränssnittet, [!DNL Experience Manager]-datorprogrammet och [!DNL Adobe Asset Link] stöder alla eller vissa åtgärder.

>[!CAUTION]
>
>Vissa API:er finns fortfarande men stöds inte aktivt (anges med en ×). Använd inte dessa API:er i största möjliga utsträckning.

| Supportnivå | Beskrivning |
| ------------- | --------------------------- |
| ✓ | Stöds |
| x | Stöds inte. Skall ej användas. |
| - | Inte tillgängligt |

| Använd skiftläge | [aem-upload](https://github.com/adobe/aem-upload) | [API:er för AEM/Sling/](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html) JCRJava | [Tjänsten asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) | [[!DNL Assets] HTTP-API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html)-servrar | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) _(förhandstitt)_ |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **Ursprunglig binär** |  |  |  |  |  |  |
| Skapa original | ✓ | x | - | x | x | - |
| Läs original | - | x | ✓ | ✓ | ✓ | - |
| Uppdatera original | ✓ | x | ✓ | x | x | - |
| Ta bort original | - | ✓ | - | ✓ | ✓ | - |
| Kopiera original | - | ✓ | - | ✓ | ✓ | - |
| Flytta original | - | ✓ | - | ✓ | ✓ | - |
| **Metadata** |  |  |  |  |  |  |
| Skapa metadata | - | ✓ | ✓ | ✓ | ✓ | - |
| Läs metadata | - | ✓ | - | ✓ | ✓ | - |
| Uppdatera metadata | - | ✓ | ✓ | ✓ | ✓ | - |
| Ta bort metadata | - | ✓ | ✓ | ✓ | ✓ | - |
| Kopiera metadata | - | ✓ | - | ✓ | ✓ | - |
| Flytta metadata | - | ✓ | - | ✓ | ✓ | - |
| **Innehållsfragment (CF)** |  |  |  |  |  |  |
| Skapa CF | - | ✓ | - | ✓ | - | - |
| Läs CF | - | ✓ | - | ✓ | - | ✓ |
| Uppdatera CF | - | ✓ | - | ✓ | - | - |
| Ta bort CF | - | ✓ | - | ✓ | - | - |
| Kopiera CF | - | ✓ | - | ✓ | - | - |
| Flytta CF | - | ✓ | - | ✓ | - | - |
| **Versioner** |  |  |  |  |  |  |
| Skapa version | ✓ | ✓ | - | - | - | - |
| Läsversion | - | ✓ | - | - | - | - |
| Ta bort version | - | ✓ | - | - | - | - |
| **Mappar** |  |  |  |  |  |  |
| Skapa mapp | ✓ | ✓ | - | ✓ | - | - |
| Läs mapp | - | ✓ | - | ✓ | - | - |
| Ta bort mapp | ✓ | ✓ | - | ✓ | - | - |
| Kopiera mapp | ✓ | ✓ | - | ✓ | - | - |
| Flytta mapp | ✓ | ✓ | - | ✓ | - | - |

## Resursöverföring {#asset-upload}

I [!DNL Experience Manager] som [!DNL Cloud Service] kan du överföra resurserna direkt till molnlagringen med HTTP API. Stegen för att överföra en binär fil är:

1. [Skicka en HTTP-begäran](#initiate-upload). Den informerar [!DNL Experience Manage]r-distribution av din avsikt att överföra en ny binär fil.
1. [POST innehållet i ](#upload-binary) binaryen till en eller flera URI:er som tillhandahålls av initieringsbegäran.
1. [Skicka en HTTP-](#complete-upload) begäran för att informera servern om att innehållet i binärfilen har överförts.

![Översikt över protokollet för direkt binär överföring](assets/add-assets-technical.png)

>[!IMPORTANT]
Utför stegen ovan i ett externt program och inte i JVM-filen [!DNL Experience Manager].

Metoden ger en skalbar och mer effektiv hantering av överföringar av resurser. Skillnaderna jämfört med [!DNL Experience Manager] 6.5 är:

* Binärfiler går inte igenom [!DNL Experience Manager], vilket nu innebär att överföringsprocessen samordnas med den binära molnlagringen som är konfigurerad för distributionen.
* Binär molnlagring fungerar med ett CDN-nätverk (Content Delivery Network) eller Edge-nätverk. Ett CDN väljer en slutpunkt för överföring som är närmare för en klient. När data flyttas kortare tid till en närliggande slutpunkt förbättras överföringsprestanda och användarupplevelsen, särskilt för geografiskt utspridda team.

>[!NOTE]
Se klientkoden för att implementera den här metoden i det öppna källbiblioteket [aem-upload library](https://github.com/adobe/aem-upload).

### Initiera överföring {#initiate-upload}

Skicka en begäran om HTTP-POST till den önskade mappen. Resurser skapas eller uppdateras i den här mappen. Inkludera väljaren `.initiateUpload.json` för att ange att begäran är att initiera överföringen av en binär fil. Sökvägen till mappen där resursen ska skapas är till exempel `/assets/folder`. POSTENS begäran är `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

Innehållstypen för begärandetexten ska vara `application/x-www-form-urlencoded` formulärdata, som innehåller följande fält:

* `(string) fileName`: Krävs. Namnet på resursen så som den visas i [!DNL Experience Manager].
* `(number) fileSize`: Krävs. Filstorleken, i byte, för resursen som överförs.

En enda begäran kan användas för att initiera överföringar för flera binärfiler, förutsatt att varje binärfil innehåller de obligatoriska fälten. Om det lyckas svarar begäran med en `201`-statuskod och en brödtext som innehåller JSON-data i följande format:

```json
{
    "completeURI": "(string)",
    "folderPath": (string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ]
        }
    ]
}
```

* `completeURI` (sträng): Anropa den här URI:n när den binära filen har överförts. URI:n kan vara en absolut eller relativ URI och klienterna bör kunna hantera båda. Värdet kan alltså vara `"https://author.acme.com/content/dam.completeUpload.json"` eller `"/content/dam.completeUpload.json"` Se [fullständig överföring](#complete-upload).
* `folderPath` (sträng): Fullständig sökväg till mappen som binärfilen överförs till.
* `(files)` (array): En lista med element vars längd och ordning matchar längden och ordningen för listan med binär information som tillhandahålls i initieringsbegäran.
* `fileName` (sträng): Namnet på motsvarande binärfil, som anges i initieringsbegäran. Detta värde bör inkluderas i den fullständiga begäran.
* `mimeType` (sträng): Mime-typen för motsvarande binärfil, som anges i initieringsbegäran. Detta värde bör inkluderas i den fullständiga begäran.
* `uploadToken` (sträng): En överföringstoken för motsvarande binär fil. Detta värde bör inkluderas i den fullständiga begäran.
* `uploadURIs` (array): En lista över strängar vars värden är fullständiga URI:er som binärens innehåll ska överföras till (se  [Överför binärt](#upload-binary)).
* `minPartSize` (tal): Den minsta längden, i byte, på data som kan tillhandahållas till någon av dem  `uploadURIs`om det finns mer än en URI.
* `maxPartSize` (tal): Den maximala längden, i byte, på data som kan anges för någon av dem  `uploadURIs`om det finns mer än en URI.

### Överför binär {#upload-binary}

Utdata från initiering av en överföring innehåller ett eller flera överförda URI-värden. Om mer än en URI anges delar klienten upp binärfilen i delar och begär POST av varje del till varje URI, i ordning. Använd alla URI:er. Se till att storleken på varje del ligger inom de minimi- och maximistorlekar som anges i initieringssvaret. CDN-kantnoder snabbar upp begärd överföring av binärfiler.

En möjlig metod för att uppnå detta är att beräkna delstorleken baserat på antalet överförings-URI:er som tillhandahålls av API:t. Anta till exempel att binärfilens totala storlek är 20 000 byte och att antalet överförda URI är 2. Följ sedan dessa steg:

* Beräkna delstorlek genom att dividera den totala storleken med antalet URI:er: 20 000 / 2 = 10 000.
* POSTENS byteintervall är 0-9 999 för binärfilen till den första URI:n i listan över överförda URI:er.
* POSTENS byteintervall 10 000 - 19 999 för binärfilen till den andra URI:n i listan över överförda URI:er.

Om överföringen lyckas svarar servern på varje begäran med en `201`-statuskod.

### Slutför överföring {#complete-upload}

När alla delar av en binär fil har överförts skickar du en begäran om HTTP-POST till den fullständiga URI som anges av initieringsdata. Innehållstypen för begärandetexten ska vara `application/x-www-form-urlencoded` formulärdata, som innehåller följande fält.

| fält | Typ | Obligatoriskt eller inte | Beskrivning |
|---|---|---|---|
| `fileName` | Sträng | Krävs | Namnet på resursen, enligt initieringsdata. |
| `mimeType` | Sträng | Krävs | HTTP-innehållstypen för binärfilen, som angavs i initieringsdata. |
| `uploadToken` | Sträng | Krävs | Överför token för binärfilen enligt initieringsdata. |
| `createVersion` | Boolesk | Valfritt | Om det finns `True` och en resurs med det angivna namnet skapar [!DNL Experience Manager] en ny version av resursen. |
| `versionLabel` | Sträng | Valfritt | Om en ny version skapas är den etikett som är associerad med den nya versionen av en resurs . |
| `versionComment` | Sträng | Valfritt | Om en ny version skapas, de kommentarer som är kopplade till versionen. |
| `replace` | Boolesk | Valfritt | Om det finns `True` och en resurs med det angivna namnet, tar [!DNL Experience Manager] bort resursen och skapar den på nytt. |

>[!NOTE]
Om resursen finns och varken `createVersion` eller `replace` har angetts, uppdaterar [!DNL Experience Manager] resursens aktuella version med den nya binärfilen.

Precis som initieringsprocessen kan fullständiga data för begäran innehålla information för mer än en fil.

Överföringen av en binär fil utförs inte förrän den fullständiga URL:en anropas för filen. En resurs bearbetas när överföringen är klar. Bearbetningen startar inte även om resursens binära fil överförs helt, men överföringen inte slutförs.

Om det lyckas svarar servern med en `200`-statuskod.

### Överföringsbibliotek med öppen källkod {#open-source-upload-library}

Om du vill veta mer om överföringsalgoritmerna eller skapa egna överföringsskript och verktyg kan du använda Adobe för att skapa bibliotek och verktyg med öppen källkod:

* [Uppladdningsbibliotek](https://github.com/adobe/aem-upload) med öppen källkod.
* [Kommandoradsverktyget](https://github.com/adobe/aio-cli-plugin-aem) med öppen källkod.

### Inaktuella API:er för överföring av resurser {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

Den nya överföringsmetoden stöds bara för [!DNL Adobe Experience Manager] som [!DNL Cloud Service]. API:erna från [!DNL Adobe Experience Manager] 6.5 är föråldrade. Metoderna för att överföra eller uppdatera resurser eller återgivningar (all binär överföring) är ersatta i följande API:er:

* [Experience Manager Assets HTTP API](mac-api-assets.md)
* `AssetManager` Java API, som  `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [Uppladdningsbibliotek](https://github.com/adobe/aem-upload) med öppen källkod.
* [Kommandoradsverktyget](https://github.com/adobe/aio-cli-plugin-aem) med öppen källkod.


## Resursbearbetning och efterbearbetning av arbetsflöden {#post-processing-workflows}

I [!DNL Experience Manager] baseras resursbearbetningen på **[!UICONTROL Processing Profiles]**-konfigurationen som använder [mikrotjänster](asset-microservices-configure-and-use.md#get-started-using-asset-microservices). Bearbetningen kräver inga utvecklartillägg.

Använd standardarbetsflödena med tillägg med anpassade steg för konfiguration av efterbearbetning av arbetsflöde.

## Stöd för arbetsflödessteg i efterbearbetningsarbetsflödet {#post-processing-workflows-steps}

Kunder som uppgraderar från tidigare versioner av [!DNL Experience Manager] kan använda tillgångsmikrotjänster för att bearbeta resurser. De molnbaserade mikrotjänsterna för resurser är mycket enklare att konfigurera och använda. Ett fåtal arbetsflödessteg som används i [!UICONTROL DAM Update Asset]-arbetsflödet i den tidigare versionen stöds inte.

[!DNL Experience Manager] som  [!DNL Cloud Service] stöd för följande arbetsflödessteg:

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

Följande tekniska arbetsflödesmodeller ersätts av resursmikrotjänster eller så är support inte tillgänglig:

* `com.day.cq.dam.core.impl.process.DamMetadataWritebackWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.XMPWritebackProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.ScheduledPublishBPProcess`
* `com.day.cq.dam.core.process.ScheduledUnPublishBPProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.core.impl.process.SendTransientWorkflowCompletedEmailProcess`

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of 
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

>[!MORELIKETHIS]
* [[!DNL Experience Cloud] as a [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

