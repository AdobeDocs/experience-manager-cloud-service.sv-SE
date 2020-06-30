---
title: Övertäckningar för Adobe Experience Manager som Cloud Service
description: AEM som Cloud Service använder övertäckningsprincipen för att utöka och anpassa konsoler och andra funktioner
translation-type: tm+mt
source-git-commit: e9fa89753289563edd59e3d75413c90efe3ff0b2
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---


# Overlays in AEM as a Cloud Service {#overlays-in-aem}

Adobe Experience Manager som Cloud Service använder principen om övertäckningar för att du ska kunna utöka och anpassa konsoler och andra funktioner (till exempel för att skapa sidor).

<!--
Adobe Experience Manager as a Cloud Service uses the principle of overlays to allow you to extend and customize the [consoles](/help/sites-developing/customizing-consoles-touch.md) and other functionality (for example, [page authoring](/help/sites-developing/customizing-page-authoring-touch.md)).
-->

Övertäckning är en term som kan användas i många sammanhang. I det här sammanhanget (utökning av AEM som Cloud Service) innebär en övertäckning att du tar de fördefinierade funktionerna och lägger in egna definitioner över dem (för att anpassa standardfunktionerna).

I en standardinstans lagras den fördefinierade funktionen under `/libs` och du rekommenderas att definiera övertäckningen (anpassningar) under `/apps` grenen. AEM använder en söksökväg för att hitta en resurs, söker först i `/apps` grenen och sedan i `/libs` grenen ( [söksökvägen kan konfigureras](#configuring-the-search-paths)). Den här mekanismen innebär att övertäckningen (och de anpassningar som definieras där) kommer att ha prioritet.

* Det beröringskänsliga användargränssnittet använder [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)-relaterade övertäckningar:

   * Metod

      * Rekonstruera lämplig `/libs` struktur under `/apps`.

         Detta kräver ingen 1:1-kopia, [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) används för att korsreferera till de ursprungliga definitioner som krävs. Med Sling Resource Merger får du tillgång till och kan sammanfoga resurser på olika sätt (differentiering).

      * Gör eventuella ändringar under `/apps`.
   * Fördelar

      * Kraftfullare med förändringar under `/libs`.
      * Definiera bara om vad som faktiskt behövs.


<!-- Still links to reference material in 6.5 -->

>[!CAUTION]
>
>Samlingsresursen för [Sling](/help/implementing/developing/introduction/sling-resource-merger.md) och de relaterade metoderna kan bara användas med [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Det innebär att det bara är lämpligt att skapa en övertäckning med en skelettstruktur för det pekaktiverade standardgränssnittet.

Övertäckningar är den rekommenderade metoden för många ändringar, som att konfigurera konsoler eller skapa en markeringskategori för resursläsaren på sidopanelen (används vid utveckling av sidor). De krävs enligt följande:

<!--
Overlays are the recommended method for many changes, such as [configuring your consoles](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) or [creating your selection category to the asset browser in the side panel](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (used when authoring pages). They are required as:
-->

* Du ***får inte *göra ändringar i`/libs`grenen **. Alla ändringar du gör kan gå förlorade eftersom den här grenen kan ändras när du:

   * uppgradera till din instans
   * tillämpa en snabbkorrigering
   * installera ett funktionspaket

* De koncentrerar dina ändringar på ett ställe; gör det enklare för dig att spåra, migrera, säkerhetskopiera och/eller felsöka ändringar efter behov.

## Konfigurera sökvägar {#configuring-the-search-paths}

För övertäckningar är den levererade resursen en sammanställning av resurser och egenskaper som har hämtats, beroende på sökvägar som kan definieras:

* Resurslösarens **söksökväg** enligt definitionen i [OSGi-konfigurationen](/help/implementing/deploying/configuring-osgi.md) för **Apache Sling Resource Resolver Factory**.

   * Sökvägarnas övre och nedre ordning anger deras respektive prioriteringar.
   * I en standardinstallation är de primära standardvärdena `/apps`, `/libs` vilket innebär att innehållet i `/apps` har högre prioritet än `/libs` (d.v.s. att det *övertäcker* det).

* Två tjänstanvändare behöver JCR:READ-åtkomst till den plats där skripten lagras. Dessa användare är: components-search-service (används av komponenterna com.day.cq.wcm.coreto access/cache) och sling-scripting (används av org.apache.sling.servlets.resolver för att hitta servrar).
* Följande konfiguration måste även konfigureras efter var du placerade dina skript (i det här exemplet under /etc, /libs eller /apps).

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* Slutligen måste även Serverlösaren konfigureras (i det här exemplet lägger du till /etc)

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

<!--
## Example of Usage {#example-of-usage}

Some examples are covered when:

* [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md)
* [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md)
-->