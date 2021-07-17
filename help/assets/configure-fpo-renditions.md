---
title: Generera renderingar endast för placering för Adobe InDesign
description: Generera FPO-återgivningar av nya och befintliga resurser med hjälp av arbetsflödet Experience Manager Assets och ImageMagick.
contentOwner: Vishabh Gupta
role: Admin
feature: Återgivningar
exl-id: null
source-git-commit: 568c25d77eb42f7d5fd3c84d71333e083759712d
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# Generera renderingar endast för placering för Adobe InDesign {#fpo-renditions}

När du monterar stora resurser från Experience Manager i Adobe InDesign-dokument måste en kreatör vänta en lång tid efter att de [har monterat en resurs](https://helpx.adobe.com/indesign/using/placing-graphics.html). Användaren kan inte använda InDesign. Detta stör det kreativa flödet och påverkar användarupplevelsen negativt. Med Adobe kan du tillfälligt placera små renderingar i InDesign-dokument till att börja med. När det slutliga resultatet behövs, till exempel för tryck- och publiceringsarbetsflöden, ersätter det ursprungliga, högupplösta materialet den tillfälliga återgivningen i bakgrunden. Denna asynkrona uppdatering i bakgrunden snabbar upp designprocessen för att öka produktiviteten och hindrar inte den kreativa processen.

Resurser innehåller återgivningar som endast används för placering (FPO). Dessa FPO-återgivningar har en liten filstorlek men har samma proportioner. Om det inte finns någon FPO-återgivning tillgänglig för en resurs använder Adobe InDesign den ursprungliga resursen i stället. Denna reservfunktion säkerställer att det kreativa arbetsflödet fortsätter utan avbrott.

Experience Manager som Cloud Service har funktioner för resurshantering i molnet för att generera FPO-renderingar. Använd resursmikrotjänster för att generera renderingar. Du kan konfigurera återgivningsgenerering för nyligen överförda resurser och för de resurser som finns i Experience Manager.

Så här genererar du FPO-återgivningar:
1. [Skapa en bearbetningsprofil](#create-processing-profile).
1. Konfigurera Experience Manager att använda den här profilen för att [bearbeta nya resurser](#generate-renditions-of-new-assets).
1. Använd profilerna för att [bearbeta befintliga resurser](#generate-renditions-of-existing-assets).

## Skapa en bearbetningsprofil {#create-processing-profile}

Om du vill generera FPO-återgivningar skapar du en **[!UICONTROL Processing Profile]**. Profilerna använder molnbaserade resurstjänster för bearbetning. Instruktioner finns i [skapa bearbetningsprofiler för resursmikrotjänster](asset-microservices-configure-and-use.md).

Välj **[!UICONTROL Create FPO Rendition]** för att generera FPO-återgivning. Du kan också klicka på **[!UICONTROL Add New]** om du vill lägga till ytterligare återgivningsinställningar i samma profil.

![create-processing-profile-fpo-renditions](assets/create-processing-profile-fpo-renditions.png)

## Generera återgivningar av nya resurser {#generate-renditions-of-new-assets}

Om du vill generera FPO-återgivningar av nya resurser använder du **[!UICONTROL Processing Profile]** på mappen i mappegenskaperna. Klicka på fliken **[!UICONTROL Asset Processing]** på sidan Egenskaper för en mapp, markera **[!UICONTROL FPO profile]** som **[!UICONTROL Processing Profile]** och spara ändringarna. Alla nya resurser som överförs till mappen bearbetas med den här profilen.

![add-fpo-rendering](assets/add-fpo-rendition.png)


## Generera återgivningar av befintliga resurser {#generate-renditions-of-existing-assets}

Om du vill generera återgivningar markerar du resurserna och följer dessa steg.

![fpo-existing-asset-reprocess](assets/fpo-existing-asset-reprocess.gif)


## Visa FPO-återgivningar {#view-fpo-renditions}

Du kan kontrollera de genererade FPO-återgivningarna när arbetsflödet har slutförts. Klicka på resursen i användargränssnittet för Experience Manager Resurser för att öppna en stor förhandsgranskning. Öppna den vänstra listen och välj **[!UICONTROL Renditions]**. Du kan också använda kortkommandot `Alt + 3` när förhandsvisningen är öppen.

Klicka på **[!UICONTROL FPO rendition]** för att läsa in förhandsgranskningen. Du kan även högerklicka på återgivningen och spara den i filsystemet. Kontrollera om det finns tillgängliga återgivningar i den vänstra listen.

![rendition_list](assets/list-renditions.png)
