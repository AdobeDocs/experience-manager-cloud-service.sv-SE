---
title: Versionsinformation om Adobe Experience Manager som molntjänst för 2020.4.0
description: Versionsinformation om Experience Manager för 2020.4.0
translation-type: tm+mt
source-git-commit: 57df03fe198564a6c02e54e19ef059e46064d163

---


# Release Notes for Adobe Experience Manager as a Cloud Service 2020.4.0 {#release-notes}

I följande avsnitt beskrivs de allmänna versionsinformationen för [!DNL Experience Manager] som molntjänst 2020.4.0.

## Releasedatum {#release-date}

Releasedatum för [!DNL Experience Manager] som molntjänst 2020.4.0 är 9 april 2020.

## Nyheter i Assets {#assets}

Lär dig mer om nya funktioner, förbättringar och felkorrigeringar för [!DNL Experience Manager Assets] och [!DNL Dynamic Media] i den aktuella versionen.

* [Varumärkesportalen](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) stöder användningsexemplen för resursdistribution för Experience Manager Assets. [!DNL Brand Portal] hjälper organisationer att tillgodose sina marknadsföringsbehov genom att på ett säkert sätt distribuera godkänt varumärke och produktmaterial till externa byråer, partners, interna team och återförsäljare för nedladdning.
   * [!DNL Brand Portal] konfigurationen slutförs via [!DNL Adobe I/O] konsolen.
   * Resurskällor i [!DNL Brand Portal] stöds ännu inte med Experience Manager [!DNLEsom en] molntjänst.

* [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) v2.0 fungerar med [!DNL Experience Manager] en molntjänst. [!DNL Adobe Asset Link] effektiviserar samarbetet mellan kreatörer och marknadsförare när det gäller att skapa innehåll genom att ansluta [!DNL Experience Manager Assets] till [!DNL Creative Cloud] datorprogram [!DNL Adobe Photoshop][!DNL Adobe Illustrator]och [!DNL Adobe InDesign] via [!DNL Asset Link] apppanelen.
   * [!DNL Experience Manager] är förkonfigurerat för [!DNL Adobe Asset Link], vilket ger [enkel konfiguration](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html) och snabbare utrullning till kreatörer.
   * [!DNL Asset Link] har nu stöd för en [Experience Manager-miljöväljare](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) som gör att kreativa användare enkelt kan ansluta till en annan [!DNL Experience Manager] miljö. Ett exempel där den här funktionen är användbar är för designers som arbetar med flera klienter med olika [!DNL Experience Manager Assets] installationer.

* Användare kan konfigurera [efterbearbetningsarbetsflöden](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) så att de startar automatiskt i användargränssnittet för [!UICONTROL mappegenskaper] för de specifika mapphierarkierna.
   * Mappens [!UICONTROL egenskapsgränssnitt] har förenklats med den nya fliken [!UICONTROL Resursbearbetning] som innehåller metadataprofil, bearbetningsprofil och den nya arbetsflödeskonfigurationen för autostart.
   * I dialogrutan för ombearbetning av resurser kan du välja en viss bearbetningsprofil och bestämma dig för att bearbeta om i undermappar.
   * [!DNL Dynamic Media]: Lagt till selektiv publiceringskonfiguration så att resurser automatiskt publiceras endast för säker förhandsvisning. Dessutom kan resurserna publiceras explicit till Experience Manager utan att publiceras till DMS7 för att distribueras offentligt.

* Följande problem är åtgärdade:
   * Anläggningar för tillgångsbearbetningsproblem.
   * Korrigeringar i [!DNL Dynamic Media] konfiguration och publicering av resurser till [!DNL Dynamic Media] leveranstjänsten.

>[!MORELIKETHIS]
>
>* [Om Adobe Asset Link](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
>* [Konfigurera varumärkesportal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)
>* [Konfigurera Experience Manager för att arbeta med resurslänk](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html)
>* [Skapa arbetsflöde i Experience Manager med hjälp av resurser och mikrotjänster](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html#post-processing-workflows)

