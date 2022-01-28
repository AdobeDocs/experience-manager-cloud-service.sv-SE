---
title: Migrera från en AEM 6.5 Forms och AEM 6.4 Forms till [!DNL AEM Forms] as a Cloud Service miljö?
description: Migrera från en [!DNL AEM Forms] Lokal miljö till [!DNL AEM Forms] as a Cloud Service miljö
contentOwner: khsingh
feature: Adaptive Forms
role: User, Developer
level: Intermediate
topic: Migration
exl-id: 090e77ff-62ec-40cb-8263-58720f3b7558
source-git-commit: ea9d8714dca0d30ba2ff33cef220c8b3f8b3c429
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 1%

---

# Migrera till [!DNL AEM Forms] as a Cloud Service  {#Harden-your-AEM-Forms-as-a-Cloud-Service-environment}

Du kan migrera dina adaptiva Forms, teman, mallar och molnkonfigurationer från <!-- AEM 6.3 Forms--> AEM 6.4 Forms on OSGi and AEM 6.5 Forms on OSGi to [!DNL AEM] as a Cloud Service. Innan du migrerar dessa resurser använder du migreringsverktyget för att konvertera det format som användes i de tidigare versionerna till det format som används i [!DNL AEM] as a Cloud Service. När du kör migreringsverktyget uppdateras följande resurser:

* Anpassade komponenter för Adaptive Forms
* Anpassningsbara Forms-mallar och teman
* Molnkonfigurationer
* Skript för kodredigeraren konverteras till återanvändbara funktioner och tillämpas på visuella regler.

## Överväganden {#consideration}

* Tjänsten hjälper dig att migrera innehåll endast från [!DNL AEM Forms] i OSGi-miljöer. Migrera innehåll från [!DNL AEM Forms] JEE till en Cloud Service-miljö stöds inte.

* (Endast för AEM 6.3 Forms eller en tidigare version som uppgraderats till AEM 6.4 Forms eller AEM 6.5 Forms) Adaptiv Forms baserad på färdiga mallar och teman som finns i AEM 6.3 Forms eller tidigare versioner stöds inte i [!DNL [!DNL AEM Forms]] as a Cloud Service.

## Förutsättningar {#prerequisites}

* [Aktivera Forms - digital registrering](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html?#editing-program) för Forms Cloud Service och [köra pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

![Resultat för torr körning](assets/enable-add-on.png)

* I en Cloud Service-miljö fungerar migreringsverktyget tillsammans med verktyget för användarmappning och verktyget för innehållsöverföring. Migreringsverktyget gör [!DNL AEM Forms] resurser som är kompatibla med Cloud Service och innehållsöverföringsverktyget migrerar innehållet från [!DNL AEM Forms] miljö till [!DNL AEM] as a Cloud Service miljö. Läs om processen för migreringsverktyget innan du använder det [flytta till AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/home.html). Processen har två verktyg:
   * [Verktyg för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration): Med verktyget för användarmappning kan du mappa dina användare med motsvarande Adobe IMS-användarkonton.
   * [Verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration): Med verktyget Innehållsöverföring kan du förbereda och överföra innehåll från en befintlig miljö till en Cloud Service-miljö.
* Konton med administratörsbehörighet för [!DNL AEM Forms] as a Cloud Service och lokal [!DNL AEM Forms] miljö.
* Hämta och installera Best Practice Analyzer, Content Transfer Tool och [!DNL AEM Forms] Migreringsverktyg från [Programdistributionsportal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)

* Kör [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration) och åtgärda det rapporterade problemet.

<!-- * Download the latest [compatibility package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases) for your [!DNL AEM Forms] version. -->

## Migrera [!DNL AEM Forms] resurser  {#use-the-migration-utility}

Utför följande steg för att göra [!DNL AEM Forms] resurser som är kompatibla med Cloud Service och överför dem till [!DNL AEM] as a Cloud Service miljö.

1. Skapa en [klona](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/correct-method-to-clone-the-aem-environment/qaq-p/363487) av din befintliga [!DNL AEM Forms] miljö.

   Använd alltid den klonade miljön för att köra innehållsöverföringsverktyget och migreringsverktyget. Verktyget för innehållsöverföring och migreringsverktyget gör några ändringar i innehåll och resurser. Kör alltså inte Content Transfer Tool och Migration Utility i en produktionsmiljö.

1. Logga in i din klonade miljö med administratörsbehörighet.

1. Kör [Verktyg för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration) för att mappa dina användare med motsvarande Adobe IMS-användarkonton. Du måste ha Adobe IMS-användarkonton för att kunna logga in på en [!DNL AEM Forms] as a Cloud Service instans.

1. Hämta och installera [Verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) och [!DNL AEM Forms] as a Cloud Service migreringsverktyg från [Programdistributionsportal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) i den klonade miljön. Du kan använda AEM Package Manager för att installera verktyget och verktyget.

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Content Migration]**.

1. Öppna **[!UICONTROL Prepare Forms for migration]** kort. Webbläsaren visar fem alternativ:
   * **[!UICONTROL AEM Forms Assets Migration]**
   * **[!UICONTROL Adaptive Forms Custom Components Migration]**
   * **[!UICONTROL Adaptive Forms Templates Migration]**
   * **[!UICONTROL AEM Forms Cloud Configurations Migration]**
   * **[!UICONTROL Code Editor Script Migration]**

1. Använd alternativet en efter en för att skapa [!DNL AEM Forms] resurser som är kompatibla med [!DNL AEM] as a Cloud Service:

   1. Tryck **[!UICONTROL AEM Forms Assets Migration]** och på nästa skärm trycker du **[!UICONTROL Start Migration]**. Det gör Adaptiv Forms och teman på dina [!DNL AEM Forms] miljö kompatibel med [!DNL AEM] as a Cloud Service .

   1. Tryck **[!UICONTROL Adaptive Forms Custom Components Migration]** och på sidan för migrering av anpassade komponenter trycker du på **[!UICONTROL Start Migration]**. Den gör alla anpassade komponenter som utvecklats för Adaptive Forms och komponentövertäckningar på din [!DNL AEM Forms] miljö kompatibel med [!DNL AEM] as a Cloud Service .

   1. Tryck **[!UICONTROL Adaptive Forms Template Migration]** och på sidan för migrering av anpassade komponenter trycker du på **[!UICONTROL Start Migration]**. Den gör adaptiva formulärmallar på /apps eller /conf och skapas med AEM mallredigeraren kompatibel med [!DNL AEM] as a Cloud Service .

   1. Tryck **[!UICONTROL AEM Forms Cloud Configurations Migration]** och tryck sedan på **[!UICONTROL Start Migration]**. Den uppdaterar och flyttar följande Cloud Services till en ny plats:

      * Cloud Service för formulärdatamodell
      * Google reCAPTCHA-Cloud Service
      * [!DNL Adobe Sign] Cloud Service
      * Adobe Fonts Cloud Service
   1. Tryck **[!UICONTROL Code Editor Script Migration]**, ange var återanvändbara funktioner ska sparas och tryck på **[!UICONTROL Start Migration].

   Cloud Servicen stöder inte regelredigeringsskript. The **[!UICONTROL Code editor script migration]** används för att konvertera alla regelskript i miljön till återanvändbara funktioner och de återanvändbara funktionerna används i den visuella redigeraren på lämplig plats. Dessa återanvändbara funktioner sparas i form av klientbibliotek och hjälper dig att behålla befintliga funktioner intakta. Verktyget tillämpar automatiskt de genererade återanvändbara funktionerna på motsvarande Adaptive Forms.

   Använd [Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement) om du vill exportera återanvändbara funktioner (klientbibliotek) till ett paket.

1. [Distribuera](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying-content-packages-via-cloud-manager-and-package-manager) paketet med återanvändbara funktioner (Client Libraries), [egen kod, komponenter, konfigurationer](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html#cloud-manager), anpassade språkspecifika bibliotek till [!DNL AEM] as a Cloud Service miljö.

   <!-- 1. Install the latest [Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) to your cloned [!DNL AEM Forms] environment. -->

1. Kör [Verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration). När du anger parametrar på **[!UICONTROL Create Migration Set]** ska du ange sökvägen till Adaptive Forms, teman, mallar, formulärdatamodeller, Cloud Services, anpassade komponenter och andra AEM Forms-specifika resurser till **[!UICONTROL Paths to be included]** alternativ. Den lägger till angivna [!DNL AEM Forms] resurser till migreringsuppsättning.

## Sökvägar för olika AEM Forms-specifika resurser

* **Adaptiv Forms**: Du hittar adaptiva formulär på `/content/dam/formsanddocuments/`och /content/forms/af. För ett adaptivt formulär med namnet WKND Registration kan du till exempel lägga till banor `/content/dam/formsanddocuments/wknd-registration` och `/content/forms/af/wknd-registration`.
* **Formulärdataläge**: Du hittar alla formulärdatamodeller på `/content/dam/formsanddocuments-fdm`. Till exempel, `/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`.

* **Klientbibliotek**: Standardsökvägen för klientbibliotek är `/etc/clientlibs/fd/theme`.

* **Adaptiva formulärmallar**: Standardsökvägen för mallar är `/conf/<template folder>`. Exempel: för en mall med namnet grundläggande sökväg `/conf/ReferenceEditableTemplates/settings/wcm/templates/basic`.

* **Adaptiva formulärteman och klientbibliotek**: Standardsökvägen för teman är ` /content/dam/formsanddocuments-themes/` och standardsökvägen för klientbibliotek är `/etc/clientlibs/fd/theme`. Exempel: för en mall med namnet WKND-tema lägger du till sökväg ` /content/dam/formsanddocuments-themes/wkndtheme` och klientbibliotek för temat på `/etc/clientlibs/reference-themes/wkndtheme-3-0`. Du kan också ha teman och klientbibliotek på andra anpassade sökvägar.

* **Molnkonfigurationer**: Du hittar molnkonfigurationer på `/conf/`. Molnkonfigurationen för formulärdatamodellen finns till exempel på `/conf/global/settings/cloudconfigs/fdm`.

* **Arbetsflödesmodell**: Du hittar AEM arbetsflödesmodeller på `/conf/global/settings/workflow/models/`. Exempel: för en arbetsflödesmodell med namnet WKND Registration, lägg till sökväg `/conf/global/settings/workflow/models/wknd-registration`

Du kan lägga till mappsökvägar på den översta nivån som listas nedan eller särskilda mappsökvägar som beskrivs nedan. Det gör att du kan migrera vissa resurser och alla resurser och formulär på en gång.

* /content/dam/formsanddocuments-fdm
* /content/dam/formSanddocuments/themes
* /content/forms/af
* /etc/clientlibs/fd/theme

Om du vill migrera AEM arbetsflödesmodeller anger du följande sökvägar:

* /conf/global/settings/workflow/models/
* /conf/global/settings/workflow/launcher
* /var/workflow/models
