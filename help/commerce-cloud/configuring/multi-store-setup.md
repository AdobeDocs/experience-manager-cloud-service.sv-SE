---
title: Installation i flera butiker
description: Installation i flera butiker
translation-type: tm+mt
source-git-commit: 69756d6831678151b0e8eb73db81113d49f17447
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---


# Installation i flera butiker {#multi-store}

AEM CIF Core Components kan användas på flera AEM webbplatsstrukturer och den underliggande GraphQL-klientimplementeringen kan ansluta till olika Magento-butiker/lagringsvyer. Detta gör att projekt kan implementera komplexa flerbutiks-/flerplatsinställningar.

En videogenomgång av detaljerade alternativ för integrering av flera visningsprogram i Magento Store med Adobe Experience Manager Sites.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

Funktionerna för hantering av flera webbplatser i Live Copy och Language Copy används tillsammans med Commerce Integration Framework för att globalt hantera webbplatser i olika regioner och på olika språk.

Den rekommenderade konfigurationen är att använda en 1:1-relation mellan AEM och Magento store-vyn.

Följ stegen nedan för att ansluta en AEM plats och AEM CIF Core Components så att även en dedikerad butiksvy kan visas:

## Konfiguration {#configuration}

1. Konfigurera flera butiker och butiksvyer enligt mönstret som beskrivs på [Magento webbplatser, butiker och vyer](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)

2. Kontrollera att anslutningen mellan AEM &amp; Magento fungerar.

3. Skapa en underordnad konfiguration för CIF-Cloud Servicens konfiguration enligt följande:

   * I AEM går du till Verktyg -> Allmänt -> [Konfigurationsläsare](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)
   * Välj den baskonfiguration du skapade
   * Skapa en ny konfiguration med stegen som beskrivs i punkt 2 ovan

   Den nya konfigurationen skapas som en underordnad konfiguration till den ursprungliga konfigurationen. Du kan nu gå till Verktyg -> Allmänt -> Konfigurationsläsaren och skapa konfigurationsinställningarna.

4. Tilldela den underordnade konfigurationen till en AEM plats

   * Gå till AEM Sites Console
   * Navigera till regionen eller språkroten i platsstrukturen, t.ex. /content/venia/us _eller_ /content/venia/us/en för exempelsidan Venia
   * Markera sidan och öppna sidegenskaper
   * Välj fliken Avancerat
   * Välj den konfiguration du skapade i steg i `Configuration` avsnittet

## Ytterligare resurser

* [Magento webbplatser, butiker och vyer](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [AEM CIF Core Components - konfiguration av flera butiker/platser](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [Använda Multi-Site Manager](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [Återanvända innehåll: Multi Site Manager och Live Copy](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/msm.html)
