---
title: Adobe Experience Manager som Cloud Service Release Notes for 2020.4.0
description: Versionsinformation om Experience Manager för 2020.4.0
translation-type: tm+mt
source-git-commit: 13774cc8684166c98f85bf4096d2c7de8d257746
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 1%

---


# Versionsinformation för Adobe Experience Manager som Cloud Service 2020.4.0 {#release-notes}

På den här sidan beskrivs den allmänna versionsinformationen för [!DNL Experience Manager] som en Cloud Service 2020.4.0.

## Releasedatum {#release-date}

Releasedatum för [!DNL Experience Manager] som Cloud Service 2020.4.0 är 9 april 2020.

## Nyheter i resurser {#assets}

Läs om nya funktioner, förbättringar och felkorrigeringar för [!DNL Experience Manager Assets] och [!DNL Dynamic Media] i den aktuella versionen.

* [Varumärkesportaler ](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) stöder användningsexemplen för resursdistribution för Experience Manager Assets. [!DNL Brand Portal] hjälper organisationer att tillgodose sina marknadsföringsbehov genom att på ett säkert sätt distribuera godkänt varumärke och produktmaterial till externa byråer, partners, interna team och återförsäljare för nedladdning.
   * [!DNL Brand Portal] konfigurationen slutförs via  [!DNL Adobe I/O] konsolen. Se [konfigurera varumärkesportalen](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html).
   * Resurskälla i [!DNL Brand Portal] stöds ännu inte med [!DNL Experience Manager] som Cloud Service.

* [Adobe Asset ](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) Linkv2.0 fungerar med  [!DNL Experience Manager] som Cloud Service. [!DNL Adobe Asset Link] effektiviserar samarbetet mellan kreatörer och marknadsförare när det gäller att skapa innehåll genom att ansluta  [!DNL Experience Manager Assets] till  [!DNL Creative Cloud] datorprogram  [!DNL Adobe Photoshop] [!DNL Adobe Illustrator]och  [!DNL Adobe InDesign] via  [!DNL Asset Link] apppanelen.
   * [!DNL Experience Manager] är förkonfigurerat för  [!DNL Adobe Asset Link], vilket ger  [enkel ](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html) konfiguration och snabbare utrullning till kreatörer.
   * [!DNL Asset Link] har nu stöd för en  [Experience Manager-](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) miljöväljare som gör att kreativa användare enkelt kan ansluta till en annan  [!DNL Experience Manager] miljö. Ett exempel där den här funktionen är användbar är för designers som arbetar med flera klienter med olika [!DNL Experience Manager Assets]-distributioner.

* Användare kan konfigurera [efterbearbetningsarbetsflöden](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) så att de startar automatiskt i mappen [!UICONTROL Properties] användargränssnittet för de specifika mapphierarkierna.
   * Mappens [!UICONTROL Properties] användargränssnitt är förenklat, med den nya fliken [!UICONTROL Asset Processing] som innehåller metadataprofil, bearbetningsprofil och den nya arbetsflödeskonfigurationen för autostart.

      ![Bearbetningsprofiler kan enkelt tillämpas på mappar och allt material som överförs till mappar bearbetas med dessa profiler](/help/assets/assets/asset-processing-folder-properties.png)

   * Med alternativet Återbearbetning av resurser kan du välja en specifik bearbetningsprofil för att bearbeta om användarvalda resurser i undermappar.

      ![Bearbeta markerade resurser med en viss bearbetningsprofil](/help/assets/assets/fpo-existing-asset-reprocess.gif)

   * [!DNL Dynamic Media]: Lagt till selektiv publiceringskonfiguration så att resurser automatiskt publiceras endast för säker förhandsvisning. Dessutom kan resurserna publiceras explicit på Experience Manager utan att publiceras till DMS7 för att levereras offentligt.

### Felkorrigeringar {#assets-bug-fixes}

* Anläggningar för tillgångsbearbetningsproblem.
* Korrigerar i [!DNL Dynamic Media] konfigurations- och publiceringsresurser till [!DNL Dynamic Media]-leveranstjänsten.

>[!MORELIKETHIS]
>
>* [Om Adobe Asset Link](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
>* [Konfigurera varumärkesportal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)
>* [Konfigurera Experience Manager för att arbeta med resurslänk](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html)
>* [Skapa arbetsflöde i Experience Manager med hjälp av resurser och mikrotjänster](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html#post-processing-workflows)


## Nyheter i Cloud Manager {#whats-new-cloud-manager}

* Utgivar-URL:er är nu tillgängliga från miljösidan i användargränssnittet för Cloud Manager.
* Ändringar i navigeringen så att användaren kan redigera, byta eller lägga till ett program från översiktssidan i Cloud Manager.
* Ändringar som gör att användaren kan redigera program från programkortet på Cloud Managers startsida.
* Ny pipeline-status **Pipeline som körs** visas mot den miljö som den är associerad med.
* Förbättringar av förståelsen av sidan för att implementera pipeline. Detta inkluderar visning av Pipeline-namn (endast icke-produktionspipeline) och typ samt ett märke som anger om pipelinestatusen pågår/avbryts/misslyckades.
* Verktygstips som förbättrar användarupplevelsen och gör det lättare att förstå varför knappen Lägg till program/miljö är inaktiverad.
* Misslyckade miljöer kan nu tas bort via gränssnittet och API:t.
* Processen som används för att generera Git-lösenord har gjorts mer flexibel mot problem i det underliggande tjänstskiktet.

### Felkorrigeringar {#bug-fixes-cloud-manager}

* Länkarna till scenmiljön på informationssidan för pipeline-körning navigerade inte konsekvent till rätt plats.
* Enskilda steg i skapandet av miljön skulle timeout inträffa tidigare än nödvändigt och orsaka att processen misslyckas.
* Den Maven-konfiguration som används i byggbehållaren har uppdaterats för att undvika dödlägen när artefaktmetadata hämtas.
* I vissa fall kan steget Skapa bild inte hämta kundpaket.
* Vissa ovanliga förhållanden kan förhindra att miljöer tas bort.
* Meddelanden från Experience Cloud mottogs inte konsekvent.
