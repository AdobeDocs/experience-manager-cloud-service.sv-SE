---
title: Installation i flera butiker
description: Lär dig hur du mappar olika butiksvyer från Magento till AEM. Detta gör att projekt kan stödja multi-tenant- och multi-lingual use-fall.
sub-product: Handel
version: cloud-service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
translation-type: tm+mt
source-git-commit: 95ac5e5f6c49d5a2d7aef5dcf30d8298fd459457
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---


# Inställningar för flera butiker {#multi-store}

AEM CIF Core Components kan användas på flera AEM webbplatsstrukturer och den underliggande GraphQL-klientimplementeringen kan ansluta till olika Magento-butiker/lagringsvyer. Detta gör att projekt kan implementera komplexa flerbutiks-/flerplatsinställningar.

En videogenomgång av detaljerade alternativ för integrering av flera visningsprogram i Magento Store med Adobe Experience Manager Sites.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

Funktionerna för hantering av flera webbplatser i Live Copy och Language Copy används tillsammans med Commerce Integration Framework för att globalt hantera webbplatser i olika regioner och på olika språk.

Den rekommenderade konfigurationen är att använda en 1:1-relation mellan AEM och Magento store-vyn.

Följ stegen nedan för att ansluta en AEM plats och AEM CIF Core Components så att även en dedikerad butiksvy kan visas:

## Konfiguration {#configuration}

1. Konfigurera flera butiker och butiksvyer enligt mönstret som beskrivs i [Magento webbplatser, butiker och vyer](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)

2. Kontrollera att anslutningen mellan AEM &amp; Magento fungerar.

3. Skapa en underordnad konfiguration för CIF-Cloud Servicens konfiguration enligt följande:

   * I AEM går du till Verktyg -> Allmänt -> [Konfigurationsläsaren](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)
   * Välj den baskonfiguration du skapade
   * Skapa en ny konfiguration med stegen som beskrivs i punkt 2 ovan

   Den nya konfigurationen skapas som en underordnad konfiguration till den ursprungliga konfigurationen. Du kan nu gå till Verktyg -> Allmänt -> Konfigurationsläsaren och skapa konfigurationsinställningarna.

4. Tilldela den underordnade konfigurationen till en AEM plats

   * Gå till AEM Sites Console
   * Navigera till regionen eller språkroten i platsstrukturen, t.ex. /content/venia/us _eller_ /content/venia/us/en för Venias exempelsida
   * Markera sidan och öppna sidegenskaper
   * Välj fliken Avancerat
   * I avsnittet `Configuration` väljer du konfigurationen som du skapade i steg

## Ytterligare resurser

* [Magento webbplatser, butiker och vyer](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [AEM CIF Core Components - konfiguration av flera butiker/platser](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [Använda Multi-Site Manager](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [Återanvända innehåll: Multi Site Manager och Live Copy](/help/sites-cloud/administering/msm/overview.md)
