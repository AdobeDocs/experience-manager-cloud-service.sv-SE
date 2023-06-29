---
title: Generera renderingar endast för placering för Adobe InDesign
description: Generera FPO-återgivningar av nya och befintliga resurser med hjälp av Experience Manager Assets arbetsflöde och ImageMagick.
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 869c1c34-6287-4d62-bb7a-aa4df580ac0e
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 3%

---

# Generera renderingar endast för placering för Adobe InDesign {#fpo-renditions}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/configure-fpo-renditions.html?lang=en) |
| AEM as a Cloud Service | Den här artikeln |

När man lägger in stora mängder material från Experience Manager i Adobe InDesign-dokument måste man vänta ett tag efter det [placera en resurs](https://helpx.adobe.com/indesign/using/placing-graphics.html). Användaren kan inte använda InDesign. Detta stör det kreativa flödet och påverkar användarupplevelsen negativt. Med Adobe kan du tillfälligt placera små renderingar i InDesign-dokument till att börja med. När det slutliga resultatet behövs, till exempel för tryck- och publiceringsarbetsflöden, ersätter det ursprungliga, högupplösta materialet den tillfälliga återgivningen i bakgrunden. Denna asynkrona uppdatering i bakgrunden snabbar upp designprocessen för att öka produktiviteten och hindrar inte den kreativa processen.

Resurser innehåller återgivningar som endast används för placering (FPO). Dessa FPO-återgivningar har en liten filstorlek men har samma proportioner. Om det inte finns någon FPO-återgivning tillgänglig för en resurs använder Adobe InDesign den ursprungliga resursen i stället. Denna reservfunktion säkerställer att det kreativa arbetsflödet fortsätter utan avbrott.

Experience Manager as a Cloud Service har funktioner för resurshantering i molnet för att generera FPO-renderingar. Använd resursmikrotjänster för att generera renderingar. Du kan konfigurera återgivningsgenerering för nyligen överförda resurser och för de resurser som finns i Experience Manager.

Så här genererar du FPO-återgivningar:

1. [Skapa en bearbetningsprofil](#create-processing-profile).

1. Konfigurera Experience Manager att använda den här profilen för [bearbeta nya resurser](#generate-renditions-of-new-assets).
1. Använd profilerna för att [bearbeta befintliga resurser](#generate-renditions-of-existing-assets).

## Skapa en bearbetningsprofil {#create-processing-profile}

Skapa en **[!UICONTROL Processing Profile]**. Profilerna använder molnbaserade resurstjänster för bearbetning. Instruktioner finns i [skapa bearbetningsprofiler för tillgångsmikrotjänster](asset-microservices-configure-and-use.md).

Välj **[!UICONTROL Create FPO Rendition]** för att generera FPO-återgivning. Om du vill kan du klicka **[!UICONTROL Add New]** om du vill lägga till ytterligare återgivningsinställningar i samma profil.

![create-processing-profile-fpo-renditions](assets/create-processing-profile-fpo-renditions.png)

## Generera återgivningar av nya resurser {#generate-renditions-of-new-assets}

Om du vill generera FPO-återgivningar av nya resurser använder du **[!UICONTROL Processing Profile]** till mappen i mappegenskaperna. Klicka på **[!UICONTROL Asset Processing]** väljer du **[!UICONTROL FPO profile]** som **[!UICONTROL Processing Profile]** och spara ändringarna. Alla nya resurser som överförs till mappen bearbetas med den här profilen.

![add-fpo-rendering](assets/add-fpo-rendition.png)


## Generera återgivningar av befintliga resurser {#generate-renditions-of-existing-assets}

Om du vill generera återgivningar markerar du resurserna och följer dessa steg.

![fpo-existing-asset-reprocess](assets/fpo-existing-asset-reprocess.gif)


## Visa FPO-återgivningar {#view-fpo-renditions}

Du kan kontrollera de genererade FPO-återgivningarna när arbetsflödet har slutförts. Klicka på resursen i Experience Manager Assets användargränssnitt för att öppna en stor förhandsvisning. Öppna den vänstra listen och välj **[!UICONTROL Renditions]**. Du kan även använda kortkommandot `Alt + 3` när förhandsgranskningen är öppen.

Klicka **[!UICONTROL FPO rendition]** för att läsa in förhandsgranskningen. Du kan även högerklicka på återgivningen och spara den i filsystemet. Kontrollera om det finns tillgängliga återgivningar i den vänstra listen.

![rendition_list](assets/list-renditions.png)

**Se även**

* [Översätt resurser](translate-assets.md)
* [HTTP API för Assets](mac-api-assets.md)
* [Resurser som stöds i filformat](file-format-support.md)
* [Söka efter resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Materialrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Söka efter fasetter](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
