---
title: Installation av Commerce Multi-Store
description: Lär dig att mappa olika butiksvyer från Adobe Commerce till Adobe Experience Manager. Detta gör att projekt kan stödja flerspråkiga och flerspråkiga användningsområden.
sub-product: Commerce
version: Experience Manager as a Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
exl-id: 4385c9e5-2b25-4f95-952f-72349431cf94
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Installation av Commerce Multi-Store {#multi-store}

Adobe Experience Manager (AEM) CIF Core Components kan användas på flera av AEM webbplatsstrukturer och den underliggande GraphQL-klientimplementeringen kan ansluta till olika Adobe Commerce-butiker/butiksvyer. Detta gör att projekt kan implementera komplexa flerbutiks-/flerplatsinställningar.

En videogenomgång av olika alternativ för integrering av flera Adobe Commerce Store-vyer med Adobe Experience Manager Sites.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

AEM funktioner för hantering av flera webbplatser i Live Copy och Language Copy används tillsammans med Commerce integration framework för att globalt hantera webbplatser i olika regioner och på olika språk.

Den rekommenderade konfigurationen är att använda en 1:1-relation mellan AEM webbplats och Adobe Commerce Store-vyn.

Så här ansluter du en AEM-webbplats och AEM CIF Core Components till en dedikerad butiksvy:

## Konfiguration {#configuration}

1. Konfigurera flera butiker och butiksvyer enligt mönstret som beskrivs i [Adobe Commerce webbplatser, butiker och vyer](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=sv-SE)

2. Kontrollera att anslutningen mellan AEM och Adobe Commerce fungerar.

3. Skapa en underordnad konfiguration av CIF Cloud Service-konfigurationen enligt följande:

   * I AEM går du till Verktyg > Allmänt > [Konfigurationsläsaren](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)
   * Välj den baskonfiguration som du har skapat
   * Skapa en konfiguration med stegen som beskrivs i punkt 2 ovan

   Den nya konfigurationen skapas som en underordnad konfiguration till den grundläggande konfigurationen. Du kan nu gå till Verktyg > Allmänt > Konfigurationsläsaren och skapa konfigurationsinställningarna.

   >[!TIP]
   >
   > Commerce-kataloger kan hanteras med ID:n eller UID:n. UID introducerades i Adobe Commerce 2.4.2. Aktivera bara detta om e-handelsbackend har stöd för ett GraphQL-schema av version 2.4.2 eller senare.

4. Tilldela den underordnade konfigurationen till en AEM-plats

   * Gå till AEM Sites Console
   * Navigera till regionen eller språkroten i platsstrukturen. Exempel: `/content/venia/us _or_ /content/venia/us/en` för Venias exempelsida
   * Markera sidan och öppna sidegenskaperna
   * Välj fliken Avancerat
   * I avsnittet `Configuration` väljer du konfigurationen som du skapade i steg 3

## Ytterligare resurser

* [Adobe Commerce webbplatser, butiker och vyer](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=sv-SE)
* [AEM CIF Core Components - konfiguration av flera butiker/platser](https://github.com/adobe/aem-core-cif-components#multi-store--site-configuration)
* [Använder Multi-Site Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html?lang=sv-SE)
* [Återanvända innehåll: Multi Site Manager och Live Copy](/help/sites-cloud/administering/msm/overview.md)
