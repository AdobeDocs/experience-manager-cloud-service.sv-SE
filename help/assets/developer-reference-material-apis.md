---
title: 'Resurser-API:er för hantering av digitala resurser i Adobe Experience Manager som en molntjänst '
description: Resurs-API:er gör det möjligt att använda grundläggande CRUD-åtgärder (create-read-update-delete) för att hantera resurser, inklusive binära, metadata, återgivningar, kommentarer och innehållsfragment.
contentOwner: AG
translation-type: tm+mt
source-git-commit: ab79c3dabb658e242df08ed065ce99499c9b7357

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

> !![NOTE]
Om du vill granska klientkod som implementerar den här metoden, se biblioteket för [aem-upload med öppen källkod](https://github.com/adobe/aem-upload)

### Initiera överföring {#initiate-upload}

Det första steget är att skicka en HTTP POST-begäran till den mapp där resursen ska skapas eller uppdateras. inkludera väljaren `.initiateUpload.json` för att ange att begäran ska påbörja en binär överföring. Sökvägen till mappen där resursen ska skapas är `/assets/folder`:

```
POST https://[aem_server]/content/dam/assets/folder.initiateUpload.json
````

Innehållstypen för begärandetexten ska vara `application/x-www-form-urlencoded` formulärdata, som innehåller följande fält:

* `(string) fileName`: Krävs. Namnet på resursen så som den kommer att visas i instansen.
* `(number) fileSize`: Krävs. Den totala längden, i byte, på den binärfil som ska överföras.

Observera att en enda begäran kan användas för att initiera överföringar för flera binärfiler, förutsatt att varje binärfil innehåller de obligatoriska fälten.

Om det lyckas kommer begäran att besvaras med en 201-statuskod och en brödtext som innehåller JSON-data i följande format:

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
````

* `(string) completeURI`: Den URI som ska anropas när binärfilen har överförts. Detta kan vara en absolut eller relativ URI, och klienterna bör kunna hantera båda. dvs. värdet kan vara `"https://author.acme.com/content/dam.completeUpload.json"` eller `"/content/dam.completeUpload.json"` (se [Slutför överföring](#complete-upload)).
* `(string) folderPath`: Fullständig sökväg till mappen där binärfilen överförs.
* `(array) (files)`: En lista med element vars längd och ordning matchar längden och ordningen för listan med binär information som tillhandahålls i initieringsbegäran.
* `(string) fileName`: Namnet på motsvarande binärfil, som anges i initieringsbegäran. Detta värde bör inkluderas i den fullständiga begäran.
* `(string) mimeType`: Mime-typen för motsvarande binärfil, som anges i initieringsbegäran. Detta värde bör inkluderas i den fullständiga begäran.
* `(string) uploadToken`: En överföringstoken för motsvarande binär fil. Detta värde bör inkluderas i den fullständiga begäran.
* `(array) uploadURIs`: En lista över strängar vars värden är fullständiga URI:er som binärens innehåll ska överföras till (se [Överför binärt](#upload-binary)).
* `(number) minPartSize`: Den minsta längden, i byte, på data som kan anges till någon av uploadURI:erna, om det finns mer än en URI.
* `(number) maxPartSize`: Den maximala längden, i byte, på data som kan tillhandahållas till någon av uploadURI:erna, om det finns mer än en URI.

### Ladda upp binärt {#upload-binary}

Utdata från initiering av en överföring inkluderar ett eller flera överförda URI-värden. Om mer än en URI anges är det klientens ansvar att dela upp binärfilen i delar och POST för varje del, i ordning, till varje URI. Alla URI:er måste användas, och varje del måste vara större än den minsta storleken och mindre än den största storlek som anges i initieringssvaret. Dessa förfrågningar kommer att hanteras av CDN-kantnoder för att påskynda överföringen av binärfiler.

Ett möjligt sätt att uppnå detta är att beräkna delstorleken baserat på antalet överförings-URI:er som tillhandahålls av API:t. Exempel: Om den totala storleken för binärfilen är 20 000 byte och antalet överförda URI:er är 2:

* Beräkna delstorlek genom att dividera den totala storleken med antalet URI:er: 20 000 / 2 = 10 000
* POST-byteintervallet 0-9 999 för binärfilen till den första URI:n i listan över överförda URI:er
* POST-byteintervallet 10 000-19 999 för binärfilen till den andra URI:n i listan över överförda URI:er

Om det lyckas svarar servern på varje begäran med en `201` statuskod.

### fullständig överföring {#complete-upload}

När alla delar av en binär fil har överförts är det sista steget att skicka en HTTP POST-begäran till den fullständiga URI som tillhandahålls av initieringsdata. Innehållstypen för begärandetexten ska vara program/`x-www-form-urlencoded` formulärdata, som innehåller följande fält:

* `(string) fileName`: Krävs. Namnet på resursen, enligt initieringsdata.
* `(string) mimeType`: Krävs. HTTP-innehållstypen för binärfilen, som angavs i initieringsdata.
* `(string) uploadToken`: Krävs. Överför token för binärfilen enligt initieringsdata.
* `(bool) createVersion`: Valfritt. Om värdet är true och det redan finns en resurs med det angivna namnet skapas en ny version av resursen.
* `(string) versionLabel`: Valfritt. Om en ny version skapas är det den etikett som är kopplad till versionen.
* `(string) versionComment`: Valfritt. Om en ny version skapas, kommer kommentarer som är kopplade till versionen att skapas.
* `(bool) replace`: Valfritt: Om värdet är true och det redan finns en resurs med det angivna namnet, kommer instansen att ta bort resursen och sedan återskapa den.

>!![NOTE]
>
> Om resursen redan finns och varken createVersion eller replace anges, kommer instansen att uppdatera resursens aktuella version med den nya binärfilen.

Precis som initieringsprocessen kan fullständiga data för begäran innehålla information för mer än en fil.

Överföringen av en binär fil utförs inte förrän den fullständiga URL:en anropas för filen. Även om en fils binära fil överförs i sin helhet, kommer resursen inte att bearbetas av instansen förrän överföringen är klar.

Om det lyckas svarar servern med en `200` statuskod.

### Överföringsbibliotek med öppen källkod {#open-source-upload-library}

Adobe tillhandahåller bibliotek och verktyg med öppen källkod som en startpunkt för att lära dig mer om överföringsalgoritmerna eller för att bygga egna överföringsskript och verktyg:

* [Bibliotek för öppen källkodsöverföring](https://github.com/adobe/aem-upload)
* [Kommandoradsverktyget Open source](https://github.com/adobe/aio-cli-plugin-aem)

### Inaktuella API:er för överföring av resurser {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below -->

>[!NOTE]
För Experience Manager som molntjänst stöds endast de nya överförings-API:erna. API:er från Experience Manager 6.5 är föråldrade.

Metoder som relaterar till överföring eller uppdatering av resurser eller återgivningar (all binär överföring) är ersatta i följande API:er:

* [HTTP-API för AEM Assets](mac-api-assets.md)
* `AssetManager` Java API, som `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [Bibliotek för öppen källkodsöverföring](https://github.com/adobe/aem-upload)
* [Kommandoradsverktyget Open source](https://github.com/adobe/aio-cli-plugin-aem)


## Resurshantering och efterbearbetning {#post-processing-workflows}

Den mesta bearbetningen av resurser utförs baserat på konfigurationen av **[!UICONTROL bearbetningsprofiler]** per [objektmikrotjänst](asset-microservices-configure-and-use.md#get-started-using-asset-microservices), och inga utvecklartillägg krävs.

För arbetsflödeskonfigurationen för efterbearbetning kan AEM-standardarbetsflöden med tillägg (t.ex. anpassade steg användas). Granska följande underavsnitt för att förstå vilka arbetsflödessteg som kan användas i arbetsflödena för efterbearbetning av resurser.

### Arbetsflödessteg i efterbearbetningsarbetsflöde {#post-processing-workflows-steps}

>[!NOTE]
Det här avsnittet gäller främst kunder som uppdaterar till AEM som en molntjänst från tidigare versioner av AEM.

På grund av en ny distributionsmodell som introducerats med Experience Manager som en molntjänst kanske vissa arbetsflödessteg som används i arbetsflödet före introduktionen av resursmikrotjänster inte längre stöds för efterbearbetningsarbetsflöden. `DAM Update Asset` Observera att de flesta av dem ersätts med mycket enklare verktyg för att konfigurera och använda resursmikrotjänster.

Här följer en lista över tekniska arbetsflödesmodeller och deras supportnivå i AEM som en molntjänst:

### Arbetsflödessteg som stöds {#supported-workflow-steps}

Följande arbetsflödessteg stöds i molntjänsten.

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

### Modeller som inte stöds eller ersätts {#unsupported-replaced-models}

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
