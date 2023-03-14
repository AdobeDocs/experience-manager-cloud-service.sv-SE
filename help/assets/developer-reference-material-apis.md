---
title: Utvecklarreferenser för [!DNL Assets]
description: "[!DNL Assets] Med API:er och referensinnehåll för utvecklare kan du hantera resurser, inklusive binära filer, metadata, återgivningar, kommentarer och [!DNL Content Fragments]."
contentOwner: AG
feature: APIs,Assets HTTP API
role: Developer,Architect,Admin
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: 627befb2fb1463ed2e3aad02f5e37b43f869b17c
workflow-type: tm+mt
source-wordcount: '1864'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager Assets] användningsfall för utvecklare, API:er och referensmaterial {#assets-cloud-service-apis}

Artikeln innehåller rekommendationer, referensmaterial och resurser för utvecklare av [!DNL Assets] som [!DNL Cloud Service]. Den innehåller en ny modul för överföring av resurser, API-referens och information om stödet som ges i arbetsflöden efter bearbetning.

## [!DNL Experience Manager Assets] API:er och åtgärder {#use-cases-and-apis}

[!DNL Assets] som [!DNL Cloud Service] innehåller flera API:er för programmässig interaktion med digitala resurser. Varje API har stöd för särskilda användningsfall, vilket framgår av tabellen nedan. The [!DNL Assets] användargränssnitt, [!DNL Experience Manager] datorprogram och [!DNL Adobe Asset Link] har stöd för alla eller vissa av åtgärderna.

>[!CAUTION]
>
>Vissa API:er finns fortfarande men stöds inte aktivt (anges med en ×). Använd inte dessa API:er i största möjliga utsträckning.

| Supportnivå | Beskrivning |
| ------------- | --------------------------- |
| ✓ | Stöds |
| × | Stöds inte. Skall ej användas. |
| - | Inte tillgängligt |

| Använd skiftläge | [aem-upload](https://github.com/adobe/aem-upload) | [Experience Manager / Sling / JCR](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) Java API:er | [Tjänsten asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) | [[!DNL Assets] HTTP-API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) servlets | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **Ursprunglig binär** |  |  |  |  |  |  |
| Skapa original | ✓ | × | - | × | × | - |
| Läs original | - | × | ✓ | ✓ | ✓ | - |
| Uppdatera original | ✓ | × | ✓ | × | × | - |
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

## Överföring av tillgångar {#asset-upload}

I [!DNL Experience Manager] som [!DNL Cloud Service]kan du överföra resurserna direkt till molnlagringen med hjälp av HTTP API. Stegen för att överföra en binär fil visas nedan. Utför dessa steg i ett externt program och inte i [!DNL Experience Manager] JVM.

1. [Skicka en HTTP-begäran](#initiate-upload). Den informerar [!DNL Experience Manage]r driftsättning av din avsikt att överföra en ny binär fil.
1. [PUT innehållet i binärfilen](#upload-binary) till en eller flera URI:er som tillhandahålls av initieringsbegäran.
1. [Skicka en HTTP-begäran](#complete-upload) för att informera servern om att innehållet i binärfilen har överförts.

![Översikt över protokollet för direkt binär överföring](assets/add-assets-technical.png)

>[!IMPORTANT]
Utför ovanstående steg i ett externt program och inte i [!DNL Experience Manager] JVM.

Metoden ger en skalbar och mer effektiv hantering av överföringar av resurser. Skillnaderna jämfört med [!DNL Experience Manager] 6.5 är:

* Binärfiler går inte igenom [!DNL Experience Manager], som nu helt enkelt koordinerar överföringsprocessen med det binära molnlagringsutrymmet som är konfigurerat för distributionen.
* Binär molnlagring fungerar med ett CDN-nätverk (Content Delivery Network) eller Edge-nätverk. Ett CDN väljer en slutpunkt för överföring som är närmare för en klient. När data flyttas kortare tid till en närliggande slutpunkt förbättras överföringsprestanda och användarupplevelsen, särskilt för geografiskt utspridda team.

>[!NOTE]
Se klientkoden för att implementera den här metoden i öppen källkod [aem-upload library](https://github.com/adobe/aem-upload).
[!IMPORTANT]
Under vissa omständigheter är det inte säkert att ändringarna till fullo kan spridas mellan begäranden till Experience Manager på grund av att lagringsutrymmet i Cloud Service så småningom är konsekvent. Detta leder till 404 svar på initiering eller slutförande av överföringsanrop på grund av att de nödvändiga mappprojekten inte sprids. Kunderna bör förvänta sig 404 svar och hantera dem genom att implementera ett nytt försök med en strategi för backoff.

### Initiera överföring {#initiate-upload}

Skicka en begäran om HTTP-POST till den önskade mappen. Resurser skapas eller uppdateras i den här mappen. Inkludera väljaren `.initiateUpload.json` för att ange att begäran är att initiera överföring av en binär fil. Sökvägen till mappen där resursen ska skapas är `/assets/folder`. Begäran om POST är `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

Innehållstypen för begärandetexten ska vara `application/x-www-form-urlencoded` formulärdata, som innehåller följande fält:

* `(string) fileName`: Krävs. Namnet på resursen så som den visas i [!DNL Experience Manager].
* `(number) fileSize`: Krävs. Filstorleken, i byte, för resursen som överförs.

En enda begäran kan användas för att initiera överföringar för flera binärfiler, förutsatt att varje binärfil innehåller de obligatoriska fälten. Om det lyckas svarar begäran med en `201` statuskod och brödtext som innehåller JSON-data i följande format:

```json
{
    "completeURI": "(string)",
    "folderPath": "(string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ],
            "minPartSize": (number),
            "maxPartSize": (number)
        }
    ]
}
```

* `completeURI` (sträng): Anropa den här URI:n när den binära filen har överförts. URI:n kan vara en absolut eller relativ URI och klienterna bör kunna hantera båda. Värdet kan alltså vara `"https://[aem_server]:[port]/content/dam.completeUpload.json"` eller `"/content/dam.completeUpload.json"` Se [fullständig överföring](#complete-upload).
* `folderPath` (sträng): Fullständig sökväg till mappen som binärfilen överförs till.
* `(files)` (array): En lista med element vars längd och ordning matchar längden och ordningen för listan med binär information som tillhandahålls i initieringsbegäran.
* `fileName` (sträng): Namnet på motsvarande binärfil, som anges i initieringsbegäran. Detta värde bör inkluderas i den fullständiga begäran.
* `mimeType` (sträng): Mime-typen för motsvarande binärfil, som anges i initieringsbegäran. Detta värde bör inkluderas i den fullständiga begäran.
* `uploadToken` (sträng): En överföringstoken för motsvarande binär fil. Detta värde bör inkluderas i den fullständiga begäran.
* `uploadURIs` (array): En lista över strängar vars värden är fullständiga URI:er som binärens innehåll ska överföras till (se [Ladda upp binärt](#upload-binary)).
* `minPartSize` (tal): Minsta tillåtna längd, i byte, för data som kan skickas till någon av `uploadURIs`, om det finns mer än en URI.
* `maxPartSize` (tal): Den maximala längden, i byte, på data som kan skickas till någon av `uploadURIs`, om det finns mer än en URI.

### Ladda upp binärt {#upload-binary}

Utdata från initiering av en överföring innehåller ett eller flera överförda URI-värden. Om mer än en URI anges kan klienten dela upp binärfilen i delar och göra PUT-förfrågningar för varje del till de angivna överförings-URI:erna, i ordning. Om du väljer att dela upp binärfilen i delar ska du följa följande riktlinjer:

* Varje del, med undantag för den sista, måste ha en storlek som är större än eller lika med `minPartSize`.
* Varje del måste ha en storlek som är mindre än eller lika med `maxPartSize`.
* Om binärfilens storlek överskrider `maxPartSize`, delar upp binärfilen i delar för att ladda upp den.
* Du behöver inte använda alla URI:er.

Om binärfilens storlek är mindre än eller lika med `maxPartSize`kan du istället överföra hela binärfilen till en enda överförings-URI. Om mer än en överförings-URI anges, ska du använda den första och ignorera resten. Du behöver inte använda alla URI:er.

CDN-kantnoder snabbar upp begärd överföring av binärfiler.

Det enklaste sättet att uppnå detta är att använda värdet för `maxPartSize` som delstorlek. API-kontraktet garanterar att det finns tillräckligt med överförda URI:er för att överföra din binära fil om du använder det här värdet som delstorlek. Det gör du genom att dela binärfilen i delar av storleken `maxPartSize`, med en URI för varje del, i ordning. Den sista delen kan ha en storlek som är mindre än eller lika med `maxPartSize`. Anta till exempel att binärfilens totala storlek är 20 000 byte, `minPartSize` är 5 000 byte, `maxPartSize` är 8 000 byte och antalet överförings-URI är 5. Utför följande steg:

* Överför de första 8 000 byten i binärfilen med den första överförings-URI:n.
* Överför de andra 8 000 byten i binärfilen med den andra överförings-URI:n.
* Överför de sista 4 000 byten i binärfilen med den tredje överförings-URI:n. Eftersom det här är den sista delen behöver den inte vara större än `minPartSize`.
* Du behöver inte använda de två sista överförings-URI:erna. Du kan ignorera dem.

Ett vanligt fel är att beräkna delstorleken baserat på antalet överförings-URI:er som tillhandahålls av API:t. API-avtalet garanterar inte att den här metoden fungerar och kan i själva verket resultera i delstorlekar som ligger utanför intervallet mellan `minPartSize` och `maxPartSize`. Detta kan leda till binära överföringsfel.

Det enklaste och säkraste sättet är att helt enkelt använda delar som är lika stora `maxPartSize`.

Om överföringen lyckas svarar servern på varje begäran med en `201` statuskod.

>[!NOTE]
Mer information om överföringsalgoritmen finns i [officiell funktionsdokumentation](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload) och [API-dokumentation](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/api/binary/BinaryUpload.html) i projektet Apache Jackrabbit Oak.

### fullständig överföring {#complete-upload}

När alla delar av en binär fil har överförts skickar du en begäran om HTTP-POST till den fullständiga URI som anges av initieringsdata. Innehållstypen för begärandetexten ska vara `application/x-www-form-urlencoded` formulärdata, som innehåller följande fält.

| fält | Typ | Obligatoriskt eller inte | Beskrivning |
|---|---|---|---|
| `fileName` | Sträng | Krävs | Namnet på resursen, enligt initieringsdata. |
| `mimeType` | Sträng | Krävs | HTTP-innehållstypen för binärfilen, som angavs i initieringsdata. |
| `uploadToken` | Sträng | Krävs | Överför token för binärfilen enligt initieringsdata. |
| `createVersion` | Boolesk | Valfritt | If `True` och det finns en resurs med det angivna namnet [!DNL Experience Manager] skapar en ny version av resursen. |
| `versionLabel` | Sträng | Valfritt | Om en ny version skapas är den etikett som är associerad med den nya versionen av en resurs . |
| `versionComment` | Sträng | Valfritt | Om en ny version skapas, de kommentarer som är kopplade till versionen. |
| `replace` | Boolesk | Valfritt | If `True` och det finns en resurs med det angivna namnet, [!DNL Experience Manager] tar bort resursen och återskapar den. |
| `uploadDuration` | Siffra | Valfritt | Den totala tiden, i millisekunder, för att filen ska kunna överföras i sin helhet. Om det anges inkluderas överföringens varaktighet i systemets loggfiler för analys av överföringshastigheten. |
| `fileSize` | Siffra | Valfritt | Filens storlek i byte. Om det anges inkluderas filstorleken i systemets loggfiler för analys av överföringshastighet. |

>[!NOTE]
Om tillgången finns och ingendera `createVersion` eller `replace` anges, sedan [!DNL Experience Manager] uppdaterar resursens aktuella version med den nya binärfilen.

Precis som initieringsprocessen kan fullständiga data för begäran innehålla information för mer än en fil.

Överföringen av en binär fil utförs inte förrän den fullständiga URL:en anropas för filen. En resurs bearbetas när överföringen är klar. Bearbetningen startar inte även om resursens binära fil överförs helt, men överföringen inte slutförs. Om överföringen lyckas svarar servern med en `200` statuskod.

### Överföringsbibliotek med öppen källkod {#open-source-upload-library}

Om du vill veta mer om överföringsalgoritmerna eller skapa egna överföringsskript och verktyg kan du använda Adobe för att skapa bibliotek och verktyg med öppen källkod:

* [Open-source aem-upload library](https://github.com/adobe/aem-upload).
* [Kommandoradsverktyg med öppen källkod](https://github.com/adobe/aio-cli-plugin-aem).

>[!NOTE]
Både aem-upload-biblioteket och kommandoradsverktyget använder [node-httptransfer library](https://github.com/adobe/node-httptransfer/)

### Inaktuella API:er för överföring av resurser {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

Den nya överföringsmetoden stöds endast för [!DNL Adobe Experience Manager] som [!DNL Cloud Service]. API:erna från [!DNL Adobe Experience Manager] 6.5 är föråldrat. Metoderna för att överföra eller uppdatera resurser eller återgivningar (all binär överföring) är ersatta i följande API:er:

* [Experience Manager Assets HTTP API](mac-api-assets.md)
* `AssetManager` Java API, som `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [Open-source aem-upload library](https://github.com/adobe/aem-upload).
* [Kommandoradsverktyg med öppen källkod](https://github.com/adobe/aio-cli-plugin-aem).
* [Apache Jackrabbit Oak-dokumentation för direkt överföring](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload).


## Resurshantering och efterbearbetning {#post-processing-workflows}

I [!DNL Experience Manager], är tillgångsbehandlingen baserad på **[!UICONTROL Processing Profiles]** konfiguration som använder [tillgångsmikrotjänster](asset-microservices-configure-and-use.md#get-started-using-asset-microservices). Bearbetningen kräver inga utvecklartillägg.

Använd standardarbetsflödena med tillägg med anpassade steg för konfiguration av efterbearbetning av arbetsflöde.

## Stöd för arbetsflödessteg i efterbearbetningsarbetsflödet {#post-processing-workflows-steps}

Om du uppgraderar från en tidigare version av [!DNL Experience Manager]kan du använda mikrotjänster för att bearbeta resurser. De molnbaserade mikrotjänsterna är enklare att konfigurera och använda. Ett fåtal arbetsflödessteg som används i [!UICONTROL DAM Update Asset] arbetsflödet i den tidigare versionen stöds inte. Mer information om klasser som stöds finns i [Java API-referens eller Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

Följande tekniska arbetsflödesmodeller ersätts av resursmikrotjänster eller så är support inte tillgänglig:

* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.switchengine.process.SwitchEngineHandlingProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`

<!-- Commenting the previous list documented at the time of GA. Replacing it with the updated list via cqdoc-18231.

* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
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
-->

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

>[!MORELIKETHIS]
* [[!DNL Experience Cloud] as a [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

