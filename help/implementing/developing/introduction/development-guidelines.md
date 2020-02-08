---
title: AEM som riktlinjer för utveckling av molntjänster
description: 'Fylls i '
translation-type: tm+mt
source-git-commit: cedc14b0d71431988238d6cb4256936a5ceb759b

---


# AEM som riktlinjer för utveckling av molntjänster {#aem-as-a-cloud-service-development-guidelines}

## Bakgrundsuppgifter och tidskrävande jobb {#background-tasks-and-long-running-jobs}

Kod som körs som en bakgrundsuppgift måste anta att instansen som den körs i när som helst kan tas ned. Koden måste därför vara flexibel och de flesta importer kan återupptas. Det innebär att om koden körs igen ska den inte börja om från början, utan i närheten av den plats där den slutade. Detta är inte ett nytt krav för den här typen av kod, men i AEM som en molntjänst är det mer sannolikt att en instans kommer att försvinna.

För att minimera problemet bör långvariga jobb om möjligt undvikas, och de bör kunna återställas till ett minimum. För att utföra sådana jobb använder du Sling Jobs, som har en garanti som är minst en gång och därför, om de avbryts, kommer att köras igen så snart som möjligt. Men de borde förmodligen inte börja från början igen. För schemaläggning av sådana jobb är det bäst att använda schemaläggaren för [delningsjobb](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) så här igen med minst en gång.

Schemaläggaren för Sling Commons ska inte användas för schemaläggning eftersom körning inte kan garanteras. Det är bara mer sannolikt att det kommer att planeras.

På samma sätt kan man inte garantera att allt som sker asynkront, som att agera på observationshändelser (som JCR-händelser eller Sling-resurshändelser), utförs och därför måste användas med försiktighet. Detta gäller redan för AEM-distributioner i nuläget.

## Utgående HTTP-anslutningar {#outgoing-http-connections}

Vi rekommenderar starkt att alla utgående HTTP-anslutningar anger rimliga anslutnings- och lästidsgränser. För kod som inte tillämpar dessa tidsgränser kommer AEM-instanser som körs på AEM som en molntjänst att tillämpa en global tidsgräns. Dessa timeoutvärden är 10 sekunder för anslutningsanrop och 60 sekunder för läsanrop för anslutningar som används av följande populära Java-bibliotek:

Adobe rekommenderar att du använder det medföljande biblioteket [](https://hc.apache.org/httpcomponents-client-ga/) Apache HttpComponents Client 4.x för att skapa HTTP-anslutningar.

Alternativ som är kända för att fungera, men som kan kräva att du själv anger beroendet är:

* [java.net.URL](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) och/eller [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) (tillhandahålls av AEM)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) (rekommenderas inte eftersom den är inaktuell och ersatt av version 4.x)
* [OK Http](OK Http (tillhandahålls inte av AEM)) (tillhandahålls inte av AEM)

## Övervakning och felsökning {#monitoring-and-debugging}

### Loggar {#logs}

* För lokal utveckling skrivs loggposterna till lokala filer
   * `./crx-quickstart/logs`
* I molnmiljöer kan utvecklare hämta loggar via Cloud Manager eller använda ett kommandoradsverktyg för att avsluta loggarna. <!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->
* Om du vill ändra loggnivåerna för molnmiljöer bör du ändra Sling Logging OSGI-konfigurationen, följt av en fullständig omdistribution. Eftersom detta inte sker omedelbart bör du vara försiktig med att aktivera utförliga loggar i produktionsmiljöer som tar emot mycket trafik. I framtiden kan det finnas mekanismer för att snabbare ändra loggnivån.

### Trådbitar {#thread-dumps}

Tråddumpar i molnmiljöer samlas in kontinuerligt, men kan för närvarande inte hämtas på ett självbetjäningssätt. Under tiden kontaktar du AEM-supporten om tråddumpar behövs för att felsöka ett problem och ange exakt tidsfönster.

### CRX/DE Lite och System Console {#crxde-lite-and-system-console}

## Lokal utveckling {#local-development}

För lokal utveckling har utvecklare full tillgång till CRXDE Lite (`/crx/de`) och AEM Web Console (`/system/console`).

Observera att vid lokal utveckling (med molnklar snabbstart) `/apps` och `/libs` kan skrivas direkt till, vilket skiljer sig från molnmiljöer där dessa mappar på den översta nivån inte kan ändras.

## AEM som verktyg för molntjänstutveckling {#aem-as-a-cloud-service-development-tools}

Kunderna har tillgång till CRXDE-stilen i utvecklingsmiljön, men inte i fas eller produktion. Det går inte att skriva till den oföränderliga databasen (`/libs`, `/apps`) vid körning, så om du försöker göra det kommer det att leda till fel.

En uppsättning verktyg för felsökning av AEM som utvecklingsmiljö i molnet finns på Developer Console för dev-, stage- och produktionsmiljöer. URL:en kan bestämmas genom att författaren eller publiceringstjänstens URL:er justeras enligt följande:

`https://dev-console>-<namespace>.<cluster>.dev.adobeaemcloud.com`

Följande CLI-kommando för Cloud Manager kan användas som en genväg för att starta utvecklarkonsolen baserat på en miljöparameter som beskrivs nedan:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Mer information finns [på den här sidan](/help/release-notes/home.md) .

Utvecklare kan generera statusinformation och lösa olika resurser.

Som framgår nedan omfattar tillgänglig statusinformation status för paket, komponenter, OSGI-konfigurationer, ekindex, OSGI-tjänster och Sling-jobb.

![Dev Console 1](/help/implementing/developing/introduction/assets/devconsole1.png)

Som framgår nedan kan utvecklare lösa paketberoenden och -servrar:

![Dev Console 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Dev Console 3](/help/implementing/developing/introduction/assets/devconsole3.png)

Utvecklarkonsolen är också användbar vid felsökning och har en länk till verktyget Förklara fråga:

![Dev Console 4](/help/implementing/developing/introduction/assets/devconsole4.png)

**AEM Staging and Production Service**

Kunderna har inte tillgång till utvecklarverktyg för staging- och produktionsmiljöer.

### Diagnostik {#diagnostics}

Systemkonsolen är tillgänglig för utvecklingsmiljöer. Diagnostikdumpar för testning och produktion är dock inte tillgängliga.