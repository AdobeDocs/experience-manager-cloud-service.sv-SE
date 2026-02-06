---
title: Cachehantering i dynamiska media med öppna API:er
description: Cachehantering i dynamiska media med öppna API:er
role: User
exl-id: 203a5291-edb5-4900-8b0a-32e1ebae5395
source-git-commit: 8c9e59108d28ee02a4609c58bf7a2543783f47e2
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# Cachehantering i dynamiska media med öppna API:er {#cache-management-dynamic-media-open-apis}

Effektiv cachehantering är avgörande för att kunna leverera högpresterande, skalbara och uppdaterade digitala resurser. I Dynamic Media med öppna API:er definierar cachehantering hur innehåll lagras, uppdateras och levereras över olika lager i leveransflödet. Svar på materialleverans cachelagras på flera lager för att säkerställa optimala prestanda och snabb innehållsleverans.

Långvarig cachelagring i Dynamic Media med Open API:er består av [Cachelagring i CDN-lager](#cdn-layer-caching) och [extern cachekontroll (BYOCDN och webbläsarcache)](#byocdn-browser-caching).

## Cachelagring av CDN-lager {#cdn-layer-caching}

Resursleveranssvar cachelagras på [Adobe Managed CDN](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn#aem-managed-cdn) under en utökad period för att maximera prestanda och minimera inläsningen på ursprungsläget. Denna cachning hanteras helt av Adobe för att säkerställa en konsekvent högklassig upplevelse för slutanvändarna. Cachevaraktigheten är avsiktligt optimerad för prestanda och kan inte anpassas av användare för att bibehålla tillförlitligheten och en effektiv innehållsleverans över alla kunder.

Alla leverans-URL:er cachas vid kanten (snabbt) under en längre tid för att säkerställa optimala prestanda. De cachelagrade leveransobjekten innehåller statiska återgivningar, videoklipp, ursprungliga bildbinärfiler och dynamiskt omformade bilder, t.ex. storleksändrade eller omformade resurser som genererats via URL-parametrar. <!--The CDN is designed to serve these assets directly from the cache without revalidating them, unless an explicit purge is performed.-->

## Extern cachekontroll (BYOCDN och webbläsarcachelagring) {#byocdn-browser-caching}

Resursleveranssvaren innehåller ett `Cache-Control`-huvud med standardvärdet `max-age` på **10 minuter** för cachelagring i efterföljande lager. Detta gäller anpassade *Bring-Your-Own-CDN-konfigurationer (BYOCDN)*, *slutanvändarwebbläsare* och eventuella *mellanliggande cachelagringsproxy*, vilket ger enhetlig cachekontroll över hela leveranssökvägen.

### Anpassa kontrollrubriker för cache {#customizing-cache-control-headers}

Om du ökar cachetiden till livevärden utöver standardkonfigurationen ökar sannolikheten för att gammalt innehåll skickas, vilket kan fördröja synligheten för innehållsuppdateringar i slutanvändarens upplevelse. Om du behöver ändra cachekontrollens beteende för ditt specifika användningsfall kan du konfigurera anpassade CDN-regler för att justera svarshuvuden. På så sätt kan du ange olika varaktigheter för cachen beroende på dina behov. Se [AEM anpassade CDN-regler för svarshuvuden](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic).

```
responseTransformations:
    rules:
      - name: cache-asset-delivery
        when:
          allOf:
            - reqProperty: path
              like: '/adobe/assets/urn:aaid:aem:*'
            - reqProperty: tier
              equals: delivery
        actions:
          - type: set
            respHeader: Cache-Control
            value: max-age=300
```

Om du behöver mer hjälp eller har frågor om cachehantering kan du kontakta [Adobe Support](https://helpx.adobe.com/in/contact.html).

## Invalidering av aktiv cache {#active-cache-invalidation}

När en resurs uppdateras, tas bort eller ändras (alla metadataändringar) blir alla tillhörande leverans-URL:er automatiskt ogiltiga i Dynamic Media med Open API:er i Adobe Managed CDN. Detta gäller för URL:er som använder standard-ID:n eller alias, tillsammans med URL:er som innehåller omformningsparametrar, till exempel bredd, format eller kvalitet. Denna händelsestyrda ogiltigförklaring säkerställer att användarna alltid får den senaste versionen av materialet utan manuell åtgärd.

### Manuell cachetömning {#manual-cache-purging}

Om du behöver rensa cachelagrat innehåll manuellt kan du göra det med AEM cacheminnet. Detaljerade instruktioner om hur du rensar specifika cacheURL:er finns i [AEM CDN Cache Invalidation](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-cache-purge#single-purge).

## Frågor och svar{#faq-cache-management}

+++**Hur påverkar cachehantering befintliga integreringar?**

Resurs-URL:er förblir oförändrade, och det cachekontrollhuvud som skickas till webbläsare (och andra mellanhänder längre fram i kedjan) från Adobe Managed CDN fortsätter att vara 10 minuter med en [`stale-while-revalidate directive`](https://web.dev/articles/stale-while-revalidate#whats_it_mean), vilket säkerställer att senare system fortsätter att utnyttja sina cacheminnen optimalt.

+++

+++**Vad utlöser en cachetömning?**

Cachetömningen aktiveras automatiskt när en resurs uppdateras, ändras, arkiveras eller tas bort.

<!--The cache purge triggers automatically in the following circumstances:
 
 - when an asset is updated, modified, or archived.
 - when an asset reaches `ready_for_delivery` state after approval.-->

+++

<!--
+++ **How long does it take for the cache to refresh after updating an asset?**

Any time the asset changes, the cache refreshes usually in *less than 60 seconds*.

+++

<!--
+++ **What happens if the cache purge system fails?**
The following mechanisms can be followed:
 
 - **Automatic retries:** 3 retry attempts with exponential backoff
 - **Monitoring:** Sev-2 alert fires if staleness exceeds 10 minutes
 - **Natural expiry:** Even without purge, cache expires after 10 hours maximum
 - **Manual override:** Engineers can manually purge via CLI tool

+++
-->

+++ **Vilka resurstyper stöds för cachelagring under lång tid?**

Den förlängda cachningen med händelsestyrd aktiv cachedvalidering kan användas för alla typer av resurser i Dynamic Media med öppna API:er, oavsett resurstyp eller format.

+++

+++ **Kan jag välja bort långvarig cachelagring för min databas?**

Om du vill avanmäla dig från förlängd cachelagring kontaktar du [Adobe Support](https://helpx.adobe.com/in/contact.html) och anger en logisk grund för din begäran.

+++


>[!MORELIKETHIS]
>
>- [Integrera resursväljare med olika program](/help/assets/integrate-asset-selector.md)
>- [Vanity-URL:er](/help/assets/vanity-urls.md)
