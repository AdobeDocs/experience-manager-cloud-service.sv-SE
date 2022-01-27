---
title: Inställningar för Commerce Multi-Store
description: Lär dig hur du mappar olika butiksvyer från Adobe Commerce till AEM. Detta gör att projekt kan stödja multi-tenant- och multi-lingual use-fall.
sub-product: Commerce
version: cloud-service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
exl-id: 4385c9e5-2b25-4f95-952f-72349431cf94,7f6e04a2-89e9-4613-8ea8-9dac1acea30b
source-git-commit: 05a412519a2d2d0cba0a36c658b8fed95e59a0f7
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# Inställningar för Commerce Multi-Store {#multi-store}

AEM CIF Core Components kan användas på flera AEM webbplatsstrukturer och den underliggande GraphQL-klientimplementeringen kan ansluta till olika Adobe Commerce butiker/butiksvyer. Detta gör att projekt kan implementera komplexa flerbutiks-/flerplatsinställningar.

En videogenomgång av olika alternativ för integrering av flera Adobe Commerce Store-vyer med Adobe Experience Manager Sites.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

Funktionerna för hantering av flera webbplatser i Live Copy och Language Copy används tillsammans med Commerce Integration Framework för att globalt hantera webbplatser i olika regioner och på olika språk.

Den rekommenderade konfigurationen är att använda en 1:1-relation mellan AEM och Adobe Commerce Store-vyn.

Följ stegen nedan för att ansluta en AEM plats och AEM CIF Core Components så att även en dedikerad butiksvy kan visas:

## Konfiguration {#configuration}

1. Konfigurera flera butiker och butiksvyer enligt mönstret som beskrivs i [Adobe Commerce webbplatser, butiker och vyer](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)

2. Kontrollera att anslutningen mellan AEM &amp; Adobe Commerce fungerar.

3. Skapa en underordnad konfiguration för CIF-Cloud Servicens konfiguration enligt följande:

   * I AEM går du till Verktyg -> Allmänt -> [Konfigurationsläsaren](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)
   * Välj den baskonfiguration du skapade
   * Skapa en ny konfiguration med stegen som beskrivs i punkt 2 ovan

   Den nya konfigurationen skapas som en underordnad konfiguration till den ursprungliga konfigurationen. Du kan nu gå till Verktyg -> Allmänt -> Konfigurationsläsaren och skapa konfigurationsinställningarna.

   >[!TIP]
   >
   > Commerce-kataloger kan hanteras med ID:n eller UID:n. UID introducerades i Adobe Commerce 2.4.2. Aktivera bara detta om e-handelsbackend har stöd för ett GraphQL-schema av version 2.4.2 eller senare.

4. Tilldela den underordnade konfigurationen till en AEM plats

   * Gå till AEM Sites Console
   * Navigera till regionen eller språkroten i platsstrukturen, t.ex. /content/venia/us _eller_ /content/venia/us/en för exempelsidan Venia
   * Markera sidan och öppna sidegenskaper
   * Välj fliken Avancerat
   * I `Configuration` väljer du konfigurationen som du skapade i steg 3

## Ytterligare resurser

* [Adobe Commerce webbplatser, butiker och vyer](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [AEM CIF Core Components - konfiguration av flera butiker/platser](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [Använda Multi-Site Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [Återanvända innehåll: Multi Site Manager och Live Copy](/help/sites-cloud/administering/msm/overview.md)
