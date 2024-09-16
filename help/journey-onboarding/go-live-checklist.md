---
title: GoLive Checklist
description: Lär dig mer om alla element som behöver vara på plats för att lyckas med Go-Live med AEM as a Cloud Service.
exl-id: b424a9db-0f3b-4a8d-be84-365d68df46ca
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 64344b9b2cce8d7c7f05d3e5ba94049346308a9d
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# GoLive Checklist {#Go-Live-Checklist}

Granska den här listan över aktiviteter för att säkerställa att du kan genomföra en smidig och framgångsrik Go-Live.

* Kör en komplett produktionsprocess med funktions- och gränssnittstestning för att säkerställa en **alltid aktuell** AEM produktupplevelse. Se följande resurser.
   * [Uppdateringar av AEM](/help/implementing/deploying/aem-version-updates.md)
   * [Anpassad funktionstestning](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [UI-testning](/help/implementing/cloud-manager/ui-testing.md)
* Om du migrerar från AEM 6.5 bör du migrera innehåll till produktion och se till att en relevant delmängd är tillgänglig på testningen.
   * DevOps bästa praxis för AEM innebär att koden går från utveckling till produktionsmiljö medan innehållet rör sig från produktionsmiljöer.
* Schemalägg en frysperiod för kod och innehåll.
   * Se även avsnittet [Tidslinjer för Kod- och Innehållsfrysning för migreringen](#code-content-freeze)
* Utför den slutliga innehållsuppsättningen.
* Validera Dispatcher-konfigurationer.
   * Använd en lokal Dispatcher-validerare som gör det lättare att konfigurera, validera och simulera Dispatcher lokalt
      * [Konfigurera lokala Dispatcher-verktyg](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools#prerequisites).
   * Granska konfigurationen av det virtuella värdsystemet noggrant.
      * Den enklaste (och standardlösningen) är att inkludera `ServerAlias *` i din virtuella värdfil i `/dispatcher/src/conf.d/available_vhostsfolder`. På så sätt kan värdalias som används i produktfunktionstester, ogiltigförklaring av Dispatcher cache och kloner fungera.
      * Om `ServerAlias *` inte är godtagbart måste minst följande `ServerAlias`-poster vara tillåtna utöver dina anpassade domäner:
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* Konfigurera CDN, SSL och DNS.
   * Om du använder ditt eget CDN anger du en supportanmälan för att konfigurera lämplig routning.
      * Mer information finns i avsnittet [Customer CDN points to AEM Managed CDN](/help/implementing/dispatcher/cdn.md#point-to-point-cdn) i CDN-dokumentationen.
      * Konfigurera SSL och DNS enligt dokumentationen från CDN-leverantören.
   * Om du inte använder ytterligare ett CDN hanterar du SSL och DNS enligt följande dokumentation:
      * Hantera SSL-certifikat
         * [Introduktion till SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)
         * [Hantera SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * Hantera anpassade domännamn (DNS)
         * Kontrollera att DNS-rensningen inte orsakar några oväntade problem. Skapa en testunderdomän för att ansluta produktionsinstansen till innan du publicerar och göra en runda UAT-tester. Om din domän är example.com kan du skapa en underdomän test.example.com och använda den i produktionen. Vid UAT-testning av domänen ska du leta efter saker som korrekt länkomdirigering, cachelagring och Dispatcher-konfigurationer.
         * [Introduktion till anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [Hantera ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * Kom ihåg att validera TTL-inställningen för din DNS-post.
      * TTL är den tid som en DNS-post finns kvar i ett cacheminne innan servern tillfrågas om en uppdatering.
      * Om du har en mycket hög TTL tar det längre tid att sprida uppdateringar till DNS-posten.
* Kör prestanda- och säkerhetstester som uppfyller dina affärskrav och mål.
   * Utför tester i en scenmiljö.  Den har samma storlek som produktionen.
   * Utvecklingsmiljöer har inte samma storlek som fas och produktion.
* Klipp ut och se till att den faktiska publiceringen utförs utan någon ny driftsättning eller uppdatering av innehållet.
* Skapa meddelandeprofiler för Admin Console-användare. Se [Meddelandeprofiler](/help/journey-onboarding/notification-profiles.md)
* Överväg att konfigurera trafikfilterregler för att styra vilken trafik som inte ska tillåtas på webbplatsen.
   * Trafikfilterregler för hastighetsbegränsning kan vara ett effektivt verktyg mot DDoS-attacker. En särskild kategori med trafikfilterregler, som kallas WAF-regler (Brandvägg för webbaserade program), kräver en separat licens.
   * Se dokumentationen för några [föreslagna startregler](/help/security/traffic-filter-rules-including-waf.md#recommended-starter-rules).

Du kan alltid referera till listan om du behöver kalibrera om dina uppgifter under Go-Live.
