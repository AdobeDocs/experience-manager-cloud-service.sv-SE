---
title: Generera renderingar endast för placering för Adobe InDesign
description: Generera FPO-återgivningar av nya och befintliga resurser med hjälp av Experience Manager Assets arbetsflöde och ImageMagick.
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 869c1c34-6287-4d62-bb7a-aa4df580ac0e
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Generera renderingar endast för placering för Adobe InDesign {#fpo-renditions}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/configure-fpo-renditions.html?lang=en) |
| AEM as a Cloud Service | Den här artikeln |

När du monterar stora resurser från Experience Manager i Adobe InDesign-dokument måste en kreatör vänta en lång tid efter att de [har monterat en resurs](https://helpx.adobe.com/indesign/using/placing-graphics.html). Samtidigt blockeras användaren från att använda InDesign. Detta stör det kreativa flödet och påverkar användarupplevelsen negativt. Med Adobe kan du tillfälligt placera små renderingar i InDesigner till att börja med. När det slutliga resultatet behövs, till exempel för tryck- och publiceringsarbetsflöden, ersätter det ursprungliga, högupplösta materialet den tillfälliga återgivningen i bakgrunden. Denna asynkrona uppdatering i bakgrunden snabbar upp designprocessen för att öka produktiviteten och hindrar inte den kreativa processen.

Assets tillhandahåller renderingar som endast används för placering (FPO). Dessa FPO-återgivningar har en liten filstorlek men har samma proportioner. Om det inte finns någon FPO-återgivning tillgänglig för en resurs använder Adobe InDesign den ursprungliga resursen i stället. Denna reservfunktion säkerställer att det kreativa arbetsflödet fortsätter utan avbrott.

Experience Manager as a Cloud Service har funktioner för resurshantering i molnet för att generera FPO-renderingar. Använd resursmikrotjänster för att generera renderingar. Du kan konfigurera återgivningsgenerering för nyligen överförda resurser och för de resurser som finns i Experience Manager.

Så här genererar du FPO-återgivningar:

1. [Skapa en bearbetningsprofil](#create-processing-profile).

1. Konfigurera Experience Manager att använda den här profilen för att [bearbeta nya resurser](#generate-renditions-of-new-assets).
1. Använd profilerna för att [bearbeta befintliga resurser](#generate-renditions-of-existing-assets).

## Skapa en bearbetningsprofil {#create-processing-profile}

Skapa en **[!UICONTROL Processing Profile]** om du vill generera FPO-återgivningar. Profilerna använder molnbaserade resurstjänster för bearbetning. Instruktioner finns i [Skapa bearbetningsprofiler för resursmikrotjänster](asset-microservices-configure-and-use.md).

Välj **[!UICONTROL Create FPO Rendition]** om du vill generera FPO-återgivning. Du kan också klicka på **[!UICONTROL Add New]** om du vill lägga till fler återgivningsinställningar i samma profil.

![create-processing-profile-fpo-renditions](assets/create-processing-profile-fpo-renditions.png)

## Generera återgivningar av nya resurser {#generate-renditions-of-new-assets}

Om du vill generera FPO-återgivningar av nya resurser använder du **[!UICONTROL Processing Profile]** i mappen i mappegenskaperna. Klicka på fliken **[!UICONTROL Asset Processing]** på sidan Egenskaper för en mapp, markera **[!UICONTROL FPO profile]** som en **[!UICONTROL Processing Profile]** och spara ändringarna. Alla nya resurser som överförs till mappen bearbetas med den här profilen.

![add-fpo-rendering](assets/add-fpo-rendition.png)


## Generera återgivningar av befintliga resurser {#generate-renditions-of-existing-assets}

Om du vill generera återgivningar markerar du resurserna och följer dessa steg.

![fpo-existing-asset-reprocess](assets/fpo-existing-asset-reprocess.gif)


## Visa FPO-återgivningar {#view-fpo-renditions}

Du kan kontrollera de genererade återgivningarna av FPO när arbetsflödet har slutförts. Klicka på resursen i Experience Manager Assets användargränssnitt för att öppna en stor förhandsvisning. Öppna den vänstra listen och välj **[!UICONTROL Renditions]**. Du kan också använda kortkommandot `Alt + 3` när förhandsgranskningen är öppen.

Klicka på **[!UICONTROL FPO rendition]** för att läsa in förhandsgranskningen. Du kan även högerklicka på återgivningen och spara den i filsystemet. Kontrollera om det finns tillgängliga återgivningar i den vänstra listen.

![rendition_list](assets/list-renditions.png)

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publish Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)