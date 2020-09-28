---
title: AEM versionsuppdateringar
description: 'AEM versionsuppdateringar '
translation-type: tm+mt
source-git-commit: 4e164812cc489959f615dc683f07c362af1555a1
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 5%

---


# AEM versionsuppdateringar {#aem-version-updates}

## Introduktion {#introduction}

AEM som Cloud Service använder nu Continuous Integration och Continuous Delivery (CI/CD) för att säkerställa att dina projekt finns i den senaste AEM versionen. Detta innebär att alla uppgraderingsåtgärder är helt automatiserade, så du behöver inte avbryta tjänsten för användarna.

>[!NOTE]
>Om uppdateringen till produktionsmiljön misslyckas kommer Cloud Manager automatiskt att återställa scenmiljön. Detta görs automatiskt för att säkerställa att både fas- och produktionsmiljöer har samma AEM när uppdateringen är klar.

AEM versionsuppdateringar är av två typer:

* **AEM Push-uppdateringar**

   * Kan släppas dagligen.
   * Mest underhållet, inklusive de senaste felkorrigeringarna och säkerhetsuppdateringarna.

      Eftersom ändringarna utförs regelbundet blir effekten inkrementell vilket minskar påverkan på tjänsten.

* **Nya funktionsuppdateringar**

   * Frisläppt via ett förutsägbart månadsschema.

AEM uppdateringar genomgår en intensiv och helt automatiserad produktvalideringsplan som omfattar flera steg, vilket säkerställer att ingen tjänst avbryts för system i produktionen. Hälsokontroller används för att övervaka programmets hälsa. Om dessa kontroller misslyckas under en AEM som en Cloud Service-uppdatering fortsätter inte releasen och Adobe undersöker varför uppdateringen orsakade detta oväntade beteende.

[Produkttester och kundfunktionstester](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) som förhindrar att produktuppgraderingar och kundkodspush bryter produktionen valideras också under en AEM versionsuppdatering.

>[ANMÄRKNING]
>Om anpassad kod publicerades till mellanlagring och sedan avvisades av dig, kommer nästa AEM att ta bort dessa ändringar för att återspegla Git-taggen för den senaste lyckade kundreleasen till produktionen.

## Sammansatt nodarkiv {#composite-node-store}

Som vi nämnt ovan kommer uppdateringarna i de flesta fall att innebära noll driftavbrott, även för författaren, som är ett kluster med noder. Rullande uppdateringar är möjliga på grund av den *sammansatta nodbutiksfunktionen* i Oak.

Med den här funktionen kan AEM referera till flera databaser samtidigt. I en rullande driftsättning innehåller den nya versionen av den gröna AEM en egen `/libs` (den TjärMK-baserade, oföränderliga databasen), som skiljer sig från den äldre versionen av den blå AEM, även om båda refererar till en delad DocumentMK-baserad ändringsbar databas som innehåller områden som `/content` , `/conf` `/etc` och andra. Eftersom både den blå och den gröna har sina egna versioner av `/libs`kan de båda vara aktiva under den rullande uppdateringen, som båda tar trafik tills den blå har ersatts helt av den gröna.

