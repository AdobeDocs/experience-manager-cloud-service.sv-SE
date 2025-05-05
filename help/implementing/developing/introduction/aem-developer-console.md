---
title: AEM AS A CLOUD SERVICE DEVELOPER CONSOLE - BETA
description: Läs om CRXDE Lite och AEM as a Cloud Service Developer Console.
feature: Developing
role: Admin, Architect, Developer
exl-id: 4b0fc3e9-b7c4-4c95-bd97-8b24e4d5cb3d
source-git-commit: 11c52f6782df3b608bedd4b120c145a7a80a0702
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 0%

---

# AEM as a Cloud Service Developer Console (Beta) {#developer-console}

>[!NOTE]
>
>I den här artikeln beskrivs en omgjord upplevelse av AEM Cloud Service Developer Console, som nu är en betaversion. En del kunder kommer åt den genom att klicka på en knapp i det klassiska användargränssnittet. Adobe tar gärna emot feedback från dig genom att skicka den till `aemcs-new-devconsole-ui-beta@adobe.com`. Mer information om den klassiska AEM Developer Console finns i [den här artikeln](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console).

AEM as a Cloud Service Developer Console innehåller en uppsättning verktyg för felsökning i molnmiljöer. Den kan nås via en länk per miljö i Cloud Manager.

>[!NOTE]
>AEM as a Cloud Service Developer Console får inte blandas ihop med liknande namn [*Adobe Developer Console*](https://developer.adobe.com/developer-console/).
>


<!--
There are multiple ways of accessing it:

1. Launch from Cloud Manager  

1. Type a url that can be determined by adjusting the Author or Publish service urls as follows:
   ```  
   https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com
   ```  

1. As a shortcut, the following Cloud Manager CLI command can be used to launch the AEM as a Cloud Service Developer Console based on an environment parameter described below:    
   ```
   aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>
   ```
-->

Utvecklare kan komma åt funktionerna som beskrivs nedan:

## OSGi Bundles {#osgi-bundles}

![Skärm för nya OSGi Bundles i Dev Console](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* En översikt över OSGI-paket som distribueras i den valda miljötypen. Det möjliggör fulltextsökning.
* Det är användbart att få information om paketens faktiska tillstånd i miljön. Du kan hämta information som exporterade paket, importerade paket, använda tjänster och mycket annat.
* Utvecklarna vill kontrollera om paketet fungerar som det ska.
* **Exempel på användningsfall:** Ett versionsintervall för ett beroende har angetts i paketet. Något går fel i beroendet. Du vill kontrollera vilken version av beroendet som är kopplad till ditt paket. Om du vill kontrollera går du till paketinformationen och använder importpaket/-paket för att kontrollera vilken paketversion eller vilken paketversion som används vid körning. Med den här informationen kan du justera versionsområdet för ditt maven-beroende eller anpassa koden.

## Java-paket {#java-packages}

![Fliken Java-paket i Dev Console-gränssnittet](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)

* En sökfråga som du kan använda för att söka efter paket som är aktiva i miljöns OSGI-system. På den här platsen kan du se vilket paket som exporterar (eller tillhandahåller) paketet och du kan se vilket paket som importerar (eller använder) paketet. Du kan också söka efter dubblettpaket (samma paket, olika versioner), vilket kan orsaka problem i vissa fall.
* **Exempel på användningsfall:** En anpassad tjänst som använder den [dynamiska klassinläsaren](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html) läser in en klass utan att ange någon version. Eftersom flera paket exporterar olika versioner varierar implementeringen, vilket leder till beteendeförändringar. Utvecklaren vill kontrollera vilka paket som finns i miljön utan att analysera funktionsmodellen. De söker efter paketet och visar alla exporterade versioner. Detta ger dem informationen att gå in i ett bättre versionsområde.

## Servlets {#servlets}

![Fliken Servlets i Dev Console-gränssnittet](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)

* En sökfråga där du kan ange en sökväg med väljare och ett tillägg med antingen GET eller POST. Sedan visas resultatet för servlets i den ordning som begäran hanteras i Sling.
* **Exempel på användningsfall:** Du har en OSGI-servlet som ska aktiveras vid en begäran och skrivas ut som svar. I stället för förväntade utdata returneras dock svaret tomt. Du måste kontrollera om någon annan server har företräde framför din servlet på grund av mer specifika väljare, `resourceType`, tillägg eller rankning. Du söker efter den förväntade sökvägen och tar reda på att en annan server är aktiv med en högre rankning. Sedan bestämmer du om du kan rangordna din tjänstdator ovan genom att lägga till väljare, till exempel.

## Tjänster {#services}

![Fliken Tjänster i Dev Console-gränssnittet](/help/implementing/developing/introduction/assets/services-dev-console.png)

* Liknar vyn OSGI-komponenter, men baserat på tjänster. Du kan snabbt söka efter vilka tjänster som tillhandahålls med vissa egenskaper.

## OSGi-komponenter {#osgi-components}

![OSGi-komponentfliken i Dev Console-gränssnittet](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)

* En översikt över OSGI-komponenter i den valda miljötypen. Det möjliggör fulltextsökning.
* Du kan få tillgång till OSGI-komponenternas aktiva status i miljön. Du kan se vilka tjänster det uppfyller, vilket paket som innehåller det och aktiveringstypen (direkt eller fördröjd).
* **Exempel: Använd fall 1:** Som utvecklare måste du kontrollera om en komponent som aktiveras med en konfiguration är aktiv i en viss miljö. Orsaken är att det förväntade beteendet inte inträffar. Du söker bara upp komponenten i sökningen och kontrollerar om komponenten är aktiv eller inte.
* **Exempel på användningsfall 2:** Du vill se vilka färdiga komponenter som är tillgängliga i miljön och identifiera vilka tjänster som stöds. Med den här funktionen kan du lära dig mer om Adobe Experience Manager as a Cloud Service. Du kan checka ut dem i komponentlistan.

## Integreringar {#integrations}

![Fliken Integrationer i Dev Console-gränssnittet](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)

* Administratörer kan generera, byta namn på och ta bort tjänstinloggningsuppgifter och utvecklartoken.

## Databas {#repository}

* Öppnar [databaswebbläsaren](/help/implementing/developing/tools/repository-browser.md).

## StatusDumpar/frågor {#status-dumps-queries}

![Statustips/frågor på fliken Dev Console-gränssnitt](/help/implementing/developing/introduction/assets/status-dumps-queries.png)

* En fulltext eller JSON-dump av det aktuella tillståndet för paket, paket, konfigurationer, tjänster, komponenter, avförsäljningsjobb eller Oak-definitioner.
* Detta är praktiskt om utvecklaren har upptäckt ett oväntat tillstånd och vill kommunicera eller dokumentera det här läget för andra utvecklare. När du hämtar dumpen får du en ögonblicksbild av läget som du kan använda som referens.

## Konfigurationer {#configurations}

![Fliken Konfigurationer i Dev Console-gränssnittet](/help/implementing/developing/introduction/assets/configurations-dev-console.png)

* En sökbar lista med konfigurationer som är aktiva i miljön. Du kan se vilka egenskaper som tillhandahålls av konfigurationerna genom att checka ut informationssidan.
* **Exempel på användningsfall:** En utvecklare vill se till att de angivna konfigurationerna finns i miljön. Om konfigurationen saknas kan de kontrollera funktionsmodellen eller konfigurationens körningsläge eller mapp.

För produktionsprogram styr Cloud Manager - Developer Role i Adobe Admin Console åtkomsten till AEM as a Cloud Service Developer Console. För sandlådeprogram kan alla användare som har en produktprofil som ger AEM åtkomst använda Developer Console. För alla program krävs&quot;Cloud Manager - utvecklarrollen&quot; för statusdumpar och åtkomst till databaswebbläsaren. Om du vill visa data från både författare och publiceringstjänster måste användare även tilldelas produktprofilen AEM Users eller AEM Administrators för båda tjänsterna.

Mer information om hur du konfigurerar användarbehörigheter finns i [Cloud Manager-dokumentation](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-manager/content/requirements/users-and-roles).

