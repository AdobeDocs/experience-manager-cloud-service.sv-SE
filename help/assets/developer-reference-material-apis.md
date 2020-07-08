---
title: 'Assets APIs for digital asset management in Adobe Experience Manager as a Cloud Service '
description: Resurs-API:er gör det möjligt att använda grundläggande CRUD-åtgärder (create-read-update-delete) för att hantera resurser, inklusive binära, metadata, återgivningar, kommentarer och innehållsfragment.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 1%

---


# Assets as a Cloud Service APIs {#assets-cloud-service-apis}

<!-- 
Give a list of and overview of all reference information available.
* New upload method
* Javadocs
* Assets HTTP API documented at [https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html](https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html)

-->

## Överföring av tillgångar {#asset-upload-technical}

Experience Manager som molntjänst är ett nytt sätt att överföra resurser till databasen - direkt binär överföring till binär molnlagring. Det här avsnittet innehåller en teknisk översikt.

### Översikt över direkt binär överföring {#overview-binary-upload}

Den högnivåalgoritm som ska överföra en binär fil är:

1. Skicka en HTTP-begäran som informerar AEM om avsikten att överföra en ny binär fil.
1. POST the contents of the binary to one or more URIs provided by the initial request.
1. Skicka en HTTP-begäran för att informera servern om att innehållet i binärfilen har överförts.

![Översikt över protokollet för direkt binär överföring](assets/add-assets-technical.png)

Viktiga skillnader jämfört med tidigare versioner av AEM är bland annat:

* Binärfilerna går inte igenom AEM, som nu helt enkelt koordinerar överföringsprocessen med det binära molnlagringsutrymmet som är konfigurerat för distributionen
* Binärt molnlagringsutrymme hanteras av ett CDN-nätverk (Content Delivery Network), som tar slutpunkten för överföringen närmare klienten och därmed förbättrar överföringsprestanda och användarupplevelsen, särskilt för distribuerade team som överför resurser

Den här metoden bör ge en mer skalbar och prestandaanpassad hantering av överföringar av resurser.

>[!NOTE]
>
>Om du vill granska klientkod som implementerar den här metoden, se biblioteket för [aem-upload med öppen källkod](https://github.com/adobe/aem-upload)

### Initiera överföring {#initiate-upload}

Det första steget är att skicka en HTTP POST-begäran till den mapp där resursen ska skapas eller uppdateras. inkludera väljaren `.initiateUpload.json` för att ange att begäran ska påbörja en binär överföring. Sökvägen till mappen där resursen ska skapas är `/assets/folder`:

```
POST https://[aem_server]/content/dam/assets/folder.initiateUpload.json
```

Innehållstypen för begärandetexten ska vara `application/x-www-form-urlencoded` formulärdata, som innehåller följande fält:

* `(string) fileName`: Krävs. Namnet på resursen så som den kommer att visas i instansen.
* `(number) fileSize`: Krävs. Den totala längden, i byte, på den binärfil som ska överföras.

En enda begäran kan användas för att initiera överföringar för flera binärfiler, förutsatt att varje binärfil innehåller de obligatoriska fälten. Om det lyckas svarar begäran med en `201` statuskod och en brödtext som innehåller JSON-data i följande format:

```
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

* `completeURI` (sträng): Anropa den här URI:n när den binära filen har överförts. URI:n kan vara en absolut eller relativ URI och klienterna bör kunna hantera båda. Värdet kan alltså vara `"https://author.acme.com/content/dam.completeUpload.json"` eller `"/content/dam.completeUpload.json"` Se [hela överföringen](#complete-upload).
* `folderPath` (sträng): Fullständig sökväg till mappen där binärfilen överförs.
* `(files)` (array): En lista med element vars längd och ordning matchar längden och ordningen för listan med binär information som tillhandahålls i initieringsbegäran.
* `fileName` (sträng): Namnet på motsvarande binärfil, som anges i initieringsbegäran. Detta värde bör inkluderas i den fullständiga begäran.
* `mimeType` (sträng): Mime-typen för motsvarande binärfil, som anges i initieringsbegäran. Detta värde bör inkluderas i den fullständiga begäran.
* `uploadToken` (sträng): En överföringstoken för motsvarande binär fil. Detta värde bör inkluderas i den fullständiga begäran.
* `uploadURIs` (array): En lista över strängar vars värden är fullständiga URI:er som binärens innehåll ska överföras till (se [Överför binärt](#upload-binary)).
* `minPartSize` (tal): Den minsta längden, i byte, på data som kan anges till någon av uploadURI:erna, om det finns mer än en URI.
* `maxPartSize` (tal): Den maximala längden, i byte, på data som kan tillhandahållas till någon av uploadURI:erna, om det finns mer än en URI.

### Ladda upp binärt {#upload-binary}

Utdata från initiering av en överföring inkluderar ett eller flera överförda URI-värden. Om mer än en URI anges är det klientens ansvar att dela upp binärfilen i delar och POST för varje del, i ordning, till varje URI. Alla URI:er måste användas, och varje del måste vara större än den minsta storleken och mindre än den största storlek som anges i initieringssvaret. Dessa förfrågningar kommer att hanteras av CDN-kantnoder för att påskynda överföringen av binärfiler.

Ett möjligt sätt att uppnå detta är att beräkna delstorleken baserat på antalet överförings-URI:er som tillhandahålls av API:t. Exempel: Om den totala storleken för binärfilen är 20 000 byte och antalet överförda URI:er är 2:

* Beräkna delstorlek genom att dividera den totala storleken med antalet URI:er: 20 000 / 2 = 10 000
* POST-byteintervallet 0-9 999 för binärfilen till den första URI:n i listan över överförda URI:er
* POST-byteintervallet 10 000 - 19 999 för binärfilen till den andra URI:n i listan över överförda URI:er

Om det lyckas svarar servern på varje begäran med en `201` statuskod.

### fullständig överföring {#complete-upload}

När alla delar av en binär fil har överförts skickar du en HTTP POST-begäran till den fullständiga URI som anges av initieringsdata. Innehållstypen för begärandetexten ska vara `application/x-www-form-urlencoded` formulärdata, som innehåller följande fält.

| fält | Typ | Obligatoriskt eller inte | Beskrivning |
|---|---|---|---|
| `fileName` | Sträng | Krävs | Namnet på resursen, enligt initieringsdata. |
| `mimeType` | Sträng | Krävs | HTTP-innehållstypen för binärfilen, som angavs i initieringsdata. |
| `uploadToken` | Sträng | Krävs | Överför token för binärfilen enligt initieringsdata. |
| `createVersion` | Boolesk | Valfritt | Om det redan finns `True` en resurs med det angivna namnet skapar Experience Manager en ny version av resursen. |
| `versionLabel` | Sträng | Valfritt | Om en ny version skapas är den etikett som är associerad med den nya versionen av en resurs . |
| `versionComment` | Sträng | Valfritt | Om en ny version skapas, de kommentarer som är kopplade till versionen. |
| `replace` | Boolesk | Valfritt | Om det redan finns `True` en resurs med det angivna namnet tar Experience Manager bort resursen och återskapar den. |

>!![NOTE]
Om resursen redan finns och varken `createVersion` eller `replace` anges, uppdaterar Experience Manager resursens aktuella version med den nya binärfilen.

Precis som initieringsprocessen kan fullständiga data för begäran innehålla information för mer än en fil.

Överföringen av en binär fil utförs inte förrän den fullständiga URL:en anropas för filen. Även om en fils binära fil överförs i sin helhet, kommer resursen inte att bearbetas av instansen förrän överföringen är klar.

Om det lyckas svarar servern med en `200` statuskod.

### Överföringsbibliotek med öppen källkod {#open-source-upload-library}

Adobe tillhandahåller bibliotek och verktyg med öppen källkod som en startpunkt för att lära dig mer om överföringsalgoritmerna eller för att bygga egna uppladdningsskript och verktyg:

* [Open-source aem-upload library](https://github.com/adobe/aem-upload)
* [Kommandoradsverktyg med öppen källkod](https://github.com/adobe/aio-cli-plugin-aem)

### Inaktuella API:er för överföring av resurser {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

För Adobe Experience Manager som Cloud Service stöds endast de nya överförings-API:erna. API:erna från Adobe Experience Manager 6.5 är föråldrade. Metoderna för att överföra eller uppdatera resurser eller återgivningar (all binär överföring) är ersatta i följande API:er:

* [AEM Assets HTTP API](mac-api-assets.md)
* `AssetManager` Java API, som `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [Uppladdningsbibliotek](https://github.com/adobe/aem-upload)med öppen källkod.
* [Kommandoradsverktyget](https://github.com/adobe/aio-cli-plugin-aem)med öppen källkod.


## Resurshantering och efterbearbetning {#post-processing-workflows}

I Experience Manager baseras resursbearbetningen på **[!UICONTROL Processing Profiles]** konfiguration som använder [tillgångsmikrotjänster](asset-microservices-configure-and-use.md#get-started-using-asset-microservices). Bearbetningen kräver inga utvecklartillägg.

Använd standardarbetsflödena med tillägg med anpassade steg för konfiguration av efterbearbetning av arbetsflöde.

## Stöd för arbetsflödessteg i efterbearbetningsarbetsflödet {#post-processing-workflows-steps}

Kunder som uppgraderar till Experience Manager som en Cloud Service från tidigare versioner av Experience Manager kan använda tillgångsmikrotjänster för bearbetning av resurser. De molnbaserade mikrotjänsterna för resurser är mycket enklare att konfigurera och använda. Ett fåtal arbetsflödessteg som används i arbetsflödet i den tidigare versionen stöds inte [!UICONTROL DAM Update Asset] .

Följande arbetsflödessteg stöds i Experience Manager som Cloud Service.

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

Följande tekniska arbetsflödesmodeller ersätts av resursmikrotjänster eller så är support inte tillgänglig.

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
