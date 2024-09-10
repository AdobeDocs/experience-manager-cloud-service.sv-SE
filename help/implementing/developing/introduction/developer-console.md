---
title: AEM as a Cloud Service Developer Console (Beta)
description: Läs om CRX/DE Lite och AEM as a Cloud Service Developer Console
feature: Developing
role: Admin, Architect, Developer
source-git-commit: ea631743af99879d2a76d3a4a78ecf5883f39c69
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 0%

---


# AEM as a Cloud Service Developer Console (Beta) {#developer-console}

>[!NOTE]
>
>I den här artikeln beskrivs en omgjord upplevelse för AEM Cloud Service Developer Console, som nu är en betaversion, och som är tillgänglig för vissa kunder genom att klicka på en knapp högst upp i det klassiska användargränssnittet. Vi uppskattar all feedback du kan skicka till `aemcs-new-devconsole-ui-beta@adobe.com`. Mer information om den klassiska AEM Developer Console finns i [den här artikeln](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console).

## AEM as a Cloud Service utvecklingsverktyg {#aem-as-a-cloud-service-development-tools}

>[!NOTE]
>AEM as a Cloud Service Developer Console får inte blandas ihop med liknande namn [*Adobe Developer Console*](https://developer.adobe.com/developer-console/).
>

Kunderna har tillgång till CRXDE-klassen i utvecklingsmiljön, men inte i fas eller produktion. Det går inte att skriva till den oföränderliga databasen (`/libs`, `/apps`) vid körning, så om du försöker göra det kommer det att uppstå fel.

I stället kan databasläsaren startas från AEM as a Cloud Service Developer Console, vilket ger en skrivskyddad vy i databasen för alla miljöer på författarnivå, publicerings- och förhandsgranskningsnivå. Mer information finns i [Databasläsaren](/help/implementing/developing/tools/repository-browser.md).

En uppsättning verktyg för felsökning av AEM as a Cloud Service utvecklingsmiljöer finns i AEM as a Cloud Service Developer Console för RDE-, dev-, stage- och produktionsmiljöer. URL:en kan bestämmas genom att ändra författarens eller Publish tjänste-URL:er enligt följande:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

Följande Cloud Manager CLI-kommando kan användas för att starta AEM as a Cloud Service Developer Console baserat på en miljöparameter som beskrivs nedan:

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

Mer information finns i [Versionsinformation](/help/release-notes/home.md).

Utvecklare kan generera statusinformation och lösa olika resurser.

Som framgår nedan omfattar tillgänglig statusinformation status för paket, komponenter, OSGI-konfigurationer, ekindex, OSGI-tjänster och Sling-jobb.

### OSGi Bundles {#osgi-bundles}

![Skärm för nya OSGi Bundles i Dev Console](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* Detta ger en översikt över OSGI-paket som distribueras på den valda miljötypen. Det möjliggör fulltextsökning.
* Det är användbart att få information om paketens aktuella tillstånd i miljön. Du kan hämta information som exporterade paket, importerade paket, använda tjänster och mycket annat.
* Utvecklarna vill kontrollera om paketet fungerar som det ska.
* **Exempel på användningsfall:** Ett versionsintervall för ett beroende har angetts i paketet. Något går fel i beroendet. Du vill kontrollera vilken version av beroendet som är kopplad till ditt paket. Du kontrollerar detta genom att gå till paketinformationen och använda importpaket/-paket för att kontrollera vilken paketversion eller vilken paketversion som används vid körningen. Med den här informationen kan du justera versionsområdet för din maven-beroende eller anpassa koden.

### Java-paket {#java-packages}

![Fliken Java-paket i Dev Console-gränssnittet](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)

* Här visas en sökfråga som du kan använda för att söka efter paket som är aktiva i miljöns OSGI-system. På den här platsen kan du se vilket paket som exporterar (eller tillhandahåller) paketet och du kan se vilket paket som importerar (eller använder) paketet. Du kan också söka efter dubblettpaket (samma paket, olika versioner), vilket kan orsaka problem i vissa fall.
* **Exempel på användningsfall:** En anpassad tjänst som använder den [dynamiska klassinläsaren](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html) läser in en klass utan att ange en version, som exporteras av flera paket med olika versioner, vilket gör att implementeringen skiljer sig och beteendet ändras. Utvecklaren vill se vilka paket som finns i miljön utan att analysera funktionsmodellen, så de söker efter det här paketet och ser alla versioner som exporteras. Detta ger dem den information de behöver för att ange ett bättre versionsområde.

### Servlets {#servlets}

![Fliken Servlets i Dev Console-gränssnittet](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)

* Här visas en sökfråga där du kan ange en sökväg med väljare och ett tillägg med antingen GET eller POST. Sedan får du resultat för servlets i den ordning som begäran hanteras i Sling.
* **Exempel på användningsfall:** Du har en OSGI-server som ska aktiveras på en begäran och skriva ut något till svaret, men du får ett tomt svar i stället. Du måste kontrollera om någon annan server har företräde framför din servlet på grund av mer specifika väljare, `resourceType`, tillägg eller rankning. Du söker efter den förväntade sökvägen och tar reda på att en annan server är aktiv med en högre rankning. Sedan bestämmer du om du kan rangordna din tjänstdator ovan genom att lägga till väljare, till exempel.

### Tjänster {#services}

![Fliken Tjänster i Dev Console-gränssnittet](/help/implementing/developing/introduction/assets/services-dev-console.png)

* Liknar vyn OSGI-komponenter, men baserat på tjänster. Du kan snabbt söka efter vilka tjänster som tillhandahålls med vissa egenskaper.

### OSGi-komponenter {#osgi-components}

![OSGi-komponentfliken i Dev Console-gränssnittet](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)

* Detta ger en översikt över OSGI-komponenter i den valda miljötypen. Det möjliggör fulltextsökning.
* Du kan få tillgång till OSGI-komponenternas aktiva status i miljön. Du kan se vilka tjänster det uppfyller, vilket paket som innehåller det och aktiveringstypen (direkt eller fördröjd).
* **Exempel på användningsfall 1:** Som utvecklare vill du verifiera om en komponent som har aktiverats med en konfiguration är aktiv eller inte i en viss miljö, eftersom du inte får det beteende du förväntar dig. Du söker bara upp komponenten i sökningen och kontrollerar om komponenten är aktiv eller inte.
* **Exempel på användningsfall 2:** Du är intresserad av att se vilka komponenter i paketet som finns i miljön, och vilka tjänster de uppfyller, för att lära dig mer om Adobe Experience Manager as a Cloud Service. Du kan checka ut dem i komponentlistan.

### Integreringar {#integrations}

![Fliken Integrationer i Dev Console-gränssnittet](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)

* Ger administratörer möjlighet att generera, byta namn på och ta bort tjänstinloggningsuppgifter och utvecklartoken.

### Databas {#repository}

* Öppnar [databaswebbläsaren](/help/implementing/developing/tools/repository-browser.md).

### StatusDumpar/frågor {#status-dumps-queries}

![Statustips/frågor på fliken Dev Console-gränssnitt](/help/implementing/developing/introduction/assets/status-dumps-queries.png)

* Ger en fullständig text eller JSON-dump av det aktuella tillståndet för paket, paket, konfigurationer, tjänster, komponenter, försäljningsjobb eller ekdefinitioner.
* Detta kan vara praktiskt om utvecklaren har upptäckt ett oväntat tillstånd och vill kommunicera eller dokumentera detta för andra utvecklare. När du hämtar dumpen får du en ögonblicksbild av läget som du kan använda som referens.

### Konfigurationer {#configurations}

![Fliken Konfigurationer i Dev Console-gränssnittet](/help/implementing/developing/introduction/assets/configurations-dev-console.png)

* Detta ger dig en sökbar lista över konfigurationer som är aktiva i miljön. Du kan se vilka egenskaper som tillhandahålls av konfigurationerna genom att checka ut informationssidan.
* **Exempel på användningsfall:** En utvecklare vill se till att de angivna konfigurationerna finns i miljön. Om konfigurationen saknas kan de kontrollera funktionsmodellen, konfigurationens körningsläge eller mapp.

För produktionsprogram definieras åtkomsten till AEM as a Cloud Service Developer Console av&quot;Cloud Manager - Developer Role&quot; i Adobe Admin Console, medan AEM as a Cloud Service Developer Console för sandlådeprogram är tillgängligt för alla användare med en produktprofil som ger dem tillgång till AEM as a Cloud Service. För alla program krävs&quot;Cloud Manager - utvecklarroll&quot; för statusdumpar och databaswebbläsaren och användare måste också definieras i produktprofilen AEM användare eller AEM administratörer för både författare och publiceringstjänster för att kunna visa data från båda tjänsterna. Mer information om hur du konfigurerar användarbehörigheter finns i [Cloud Manager-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).