---
title: Versionsinformation för version 2020.4.0
description: Versionsinformation för version 2020.4.0
translation-type: tm+mt
source-git-commit: 77163877bea36f854ac8ea6fbc78cbcf4d58ccc0

---


# Versionsinformation för AEM som molntjänst 2020.4.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för Experience Manager som en molntjänst 2020.4.0.

## Assets {#assets}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Experience Manager Assets och Dynamic Media i AEM som en molntjänst 2020.4.0.

### Nyheter {#assets-what-is-new}

* [Varumärkesportalen](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) är tillgänglig för AEM som molntjänster och stöder användningsexempel för resursdistribution. Varumärkesportalen hjälper organisationer att tillgodose sina marknadsföringsbehov genom att på ett säkert sätt distribuera godkänt varumärkes- och produktmaterial till externa byråer, partners, interna team och återförsäljare för nedladdning.
   * Varumärkesportalen konfigureras via Adobe I/O-konsolen
   * Resurshantering i varumärkesportalen stöds ännu inte med AEM som molntjänst
* Den nya versionen av [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) 2.0 stöds med AEM som en molntjänst. Adobe Asset Link effektiviserar samarbetet mellan kreatörer och marknadsförare när det gäller att skapa innehåll genom att koppla samman AEM Assets med Creative Cloud-datorprogrammen Photoshop, Illustrator och InDesign via länkpanelen i appen.
   * AEM som en molntjänst är förkonfigurerad för Adobe Asset Link, vilket ger en [förenklad konfiguration](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html).
   * Asset Link har nu stöd för en [AEM-miljöväljare](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink), vilket gör det enklare för kreativa användare att ansluta till olika AEM-miljöer (t.ex. för byrådesigners som arbetar med flera klienter med AEM Assets)
* Automatisk start för [efterbearbetning av arbetsflöden](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) kan konfigureras i användargränssnittet för mappegenskaper för specifika mapphierarkier.
   * Mappegenskapsgränssnittet har förenklats, med den nya fliken Resursbearbetning som innehåller metadataprofil, Bearbetningsprofil och den nya konfigurationen för automatisk start av arbetsflöde
* Dialogrutan Återbearbetning av resurser gör att du kan välja en viss bearbetningsprofil och bestämma dig för att bearbeta om i undermappar
* Dynamiska medier: Konfiguration för selektiv publicering har lagts till, vilket innebär att resurser automatiskt publiceras enbart för säker förhandsgranskning och kan publiceras explicit till AEM utan publicering till DMS7 för att distribueras offentligt.

### Felkorrigeringar {#assets-bug-fixes}

* Anläggningar i tillgångsbearbetning
* Korrigeringar i Dynamic Media-konfiguration och publicering av resurser till Dynamic Media-leveranstjänsten
