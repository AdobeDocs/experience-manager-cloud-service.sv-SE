---
title: Versionsinformation om Adobe Experience Manager as a Cloud Service 2020.4.0
description: "[!DNL Adobe Experience Manager] as a Cloud Service versionsinformation för 2020.4.0."
exl-id: d98a3862-76fa-4b5b-b81a-333f5f532b67
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 0%

---

# Versionsinformation om Adobe Experience Manager as a Cloud Service 2020.4.0 {#release-notes}

På den här sidan finns en beskrivning av den allmänna versionsinformationen för [!DNL Experience Manager] as a Cloud Service 2020.4.0.

## Releasedatum {#release-date}

Lanseringsdatumet för [!DNL Experience Manager] as a Cloud Service 2020.4.0 är 9 april 2020.

## Nyheter i Assets {#assets}

Lär dig mer om nya funktioner, förbättringar och felkorrigeringar för [!DNL Experience Manager Assets] och [!DNL Dynamic Media] i den aktuella versionen.

* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=sv-SE) stöder användningsexemplen för resursdistribution för Experience Manager Assets. [!DNL Brand Portal] hjälper organisationer att tillgodose sina marknadsföringsbehov genom att på ett säkert sätt distribuera godkända varumärkes- och produktresurser till externa byråer, partners, interna team och återförsäljare för nedladdning.
   * Konfigurationen av [!DNL Brand Portal] har slutförts via [!DNL Adobe I/O]-konsolen. Se [konfigurera Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html?lang=sv-SE).
   * Resurskälla i [!DNL Brand Portal] stöds ännu inte med [!DNL Experience Manager] as a Cloud Service.

* [Adobe Asset Link](https://helpx.adobe.com/se/enterprise/using/adobe-asset-link.html) v2.0 fungerar med [!DNL Experience Manager] as a Cloud Service. [!DNL Adobe Asset Link] effektiviserar samarbetet mellan kreatörer och marknadsförare när det gäller att skapa innehåll genom att ansluta [!DNL Experience Manager Assets] med [!DNL Creative Cloud] datorprogram [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] och [!DNL Adobe InDesign] via panelen i appen [!DNL Asset Link].
   * [!DNL Experience Manager] är förkonfigurerad för [!DNL Adobe Asset Link], vilket ger [enkel konfiguration](https://helpx.adobe.com/se/enterprise/using/configure-aem-assets-for-asset-link.html) och snabbare utrullning till kreatörer.
   * [!DNL Asset Link] har nu stöd för en [Experience Manager-miljöväljare](https://helpx.adobe.com/se/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) som gör att kreativa användare enkelt kan ansluta till en annan [!DNL Experience Manager]-miljö. Ett exempel där den här funktionen är användbar är för byrådesigners som arbetar med flera klienter med olika [!DNL Experience Manager Assets]-distributioner.

* Användare kan konfigurera [efterbearbetningsarbetsflöden](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) så att de startar automatiskt i användargränssnittet för mappen [!UICONTROL Properties] för de specifika mapphierarkierna.
   * Mappens användargränssnitt [!UICONTROL Properties] är förenklat, med den nya fliken [!UICONTROL Asset Processing] som innehåller metadataprofil, bearbetningsprofil och den nya arbetsflödeskonfigurationen för autostart.

     ![Bearbetningsprofiler kan enkelt tillämpas på mappar och alla resurser som överförs till mappar bearbetas med hjälp av de här profilerna](/help/assets/assets/asset-processing-folder-properties.png)

   * Med alternativet Återbearbetning av resurser kan du välja en specifik bearbetningsprofil för att bearbeta om användarvalda resurser i undermappar.

     ![Bearbeta om markerade resurser med en specifik bearbetningsprofil](/help/assets/assets/fpo-existing-asset-reprocess.gif)

   * [!DNL Dynamic Media]: En selektiv publiceringskonfiguration har lagts till så att resurser automatiskt publiceras endast för säker förhandsvisning. Dessutom kan resurserna publiceras explicit på Experience Manager utan att publiceras till DMS7 för att levereras offentligt.

### Felkorrigeringar {#assets-bug-fixes}

* Anläggningar för tillgångsbearbetningsproblem.
* Korrigeringar i [!DNL Dynamic Media]-konfiguration och publicering av resurser till [!DNL Dynamic Media]-leveranstjänsten.

>[!MORELIKETHIS]
>
>* [Om Adobe Asset Link](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
>* [Konfigurera Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html?lang=sv-SE)
>* [Konfigurera Experience Manager för att arbeta med resurslänk](https://helpx.adobe.com/se/enterprise/using/configure-aem-assets-for-asset-link.html)
>* [Skapa arbetsflöde i Experience Manager med hjälp av objektmikrotjänster](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html?lang=sv-SE#post-processing-workflows)

## Nyheter i Cloud Manager {#whats-new-cloud-manager}

* Utgivar-URL:er är nu tillgängliga från miljösidan i Cloud Manager användargränssnitt.
* Ändringar i navigeringen så att användaren kan redigera, byta eller lägga till ett program från Cloud Manager översiktssida.
* Ändringar som gör att användaren kan redigera program från programkortet på Cloud Manager startsida.
* Den nya pipelinestatusen **Pipeline som körs** visas mot den miljö som den är associerad med.
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
