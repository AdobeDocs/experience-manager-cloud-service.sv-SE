---
title: Funktionstestning
description: Lär dig mer om de tre olika typerna av funktionstestning som är inbyggda i den AEM as a Cloud Service driftsättningsprocessen för att säkerställa att koden är tillförlitlig och av hög kvalitet.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---


# Funktionstestning {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Funktionstestning"
>abstract="Lär dig mer om de tre olika typerna av funktionstestning som är inbyggda i den AEM as a Cloud Service driftsättningsprocessen för att säkerställa att koden är tillförlitlig och av hög kvalitet."

Läs mer om de tre olika typerna av funktionstestning som ingår i [AEM as a Cloud Service distributionsprocess](/help/implementing/cloud-manager/deploy-code.md) för att säkerställa kvaliteten och tillförlitligheten i koden.

## Omfång

Syftet med de funktionella teststegen i molnhanterarens pipeline är att se till att de viktigaste funktionerna i ditt program fungerar som förväntat.

Denna testfas är den sista nivån av automatiserad testning innan koden distribueras till produktionen.

Funktionstestning bör inte ersätta, utan snarare komplettera och utöka andra teststrategier som enhetstestning, integrationstestning eller funktionstestning som utförs utanför pipeline-körningen i Cloud Manager.

## Översikt {#overview}

Det finns tre olika typer av funktionstestning på AEM as a Cloud Service.

* [Funktionstestning av produkten](#product-functional-testing)
* [Anpassad funktionstestning](#custom-functional-testing)
* [Anpassade gränssnittstestningar](#custom-ui-testing)

För alla funktionstester kan de detaljerade resultaten av testerna hämtas som `.zip` genom att använda **Hämta bygglogg** på skärmen för byggöversikt som en del av [distributionsprocess](/help/implementing/cloud-manager/deploy-code.md).

Loggarna innehåller inte loggarna för den faktiska AEM körningsprocessen. Information om hur du kommer åt loggarna finns i [Åtkomst till och hantering av loggar](/help/implementing/cloud-manager/manage-logs.md) för mer information.

Både produktfunktionstesterna och de anpassade funktionstesterna baseras på [AEM testar klienter.](https://github.com/adobe/aem-testing-clients)

### Funktionstestning av produkten {#product-functional-testing}

Funktionstester för produkter är en uppsättning stabila HTTP-integrationstester (IT) av kärnfunktionalitet i AEM som redigerings- och replikeringsuppgifter. Dessa tester underhålls av Adobe och är avsedda att förhindra att ändringar i anpassad programkod driftsätts om kärnfunktionen bryts.

* [Produktionsförlopp](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md): Funktionstester för produkter körs automatiskt när du distribuerar ny kod till Cloud Manager och kan inte hoppas över.
* [Icke-produktionsförlopp](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md): Du kan välja att produktfunktionstester ska köras varje gång du utför icke-produktionsflödet.

Funktionstester för produkter underhålls som ett öppen källkodsprojekt. Se [funktionsprovningar av produkter](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) i GitHub för mer information.

### Anpassad funktionstestning {#custom-functional-testing}

Även om produktfunktionstestning definieras av Adobe kan du skriva egna kvalitetstester för ditt eget program. Detta körs som anpassad funktionstestning som en del av [produktionsflöde](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) eller valfritt [rörledning för icke-produktion](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) för att säkerställa programmets kvalitet.

Anpassad funktionstestning körs både för anpassade koddistributioner och push-uppgraderingar, vilket gör det särskilt viktigt att skriva bra funktionstester som förhindrar att AEM kan knäcka programkoden. Det anpassade funktionsteststeget finns alltid och kan inte hoppas över.

Se [Java Functional Tests](/help/implementing/cloud-manager/java-functional-testing.md) för mer information.


### Anpassade gränssnittstestningar {#custom-ui-testing}

Anpassad gränssnittstestning är en valfri funktion som gör att du kan skapa och automatiskt köra gränssnittstester för dina program. Användargränssnittstester är självstudiebaserade tester som paketeras i en Docker-bild för ett brett urval av språk och ramverk som Java och Maven, Node och WebDriver.io eller andra ramverk och tekniker som bygger på Selenium.

Se [Anpassade gränssnittstestningar](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) för mer information.

