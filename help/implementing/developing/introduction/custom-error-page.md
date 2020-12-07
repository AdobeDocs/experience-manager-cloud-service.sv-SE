---
title: Anpassade felsidor
description: AEM har en standardfelhanterare för hantering av HTTP-fel, som kan anpassas.
translation-type: tm+mt
source-git-commit: d7e9bdee83f1b85436185ca57420ee178268cb33
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---


# Anpassa felsidor {#customizing-error-pages}

AEM har en standardfelhanterare för hantering av HTTP-fel. genom att till exempel visa:

![Standardfelmeddelande](assets/error-message-standard.png)

För att svara på fel tillhandahåller AEM ett `404.jsp`-skript under `/libs/sling/servlet/errorhandler`.

>[!TIP]
>
>Eftersom AEM baseras på Apache Sling finns ytterligare information tillgänglig [i dokumentationen för felhantering i Apache.](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)

>[!NOTE]
>
>På en författarinstans är [CQ WCM Debug Filter](/help/implementing/deploying/configuring-osgi.md) aktiverat som standard. Detta resulterar alltid i svarskoden 200. Standardfelhanteraren svarar genom att skriva den fullständiga stackspårningen till svaret.
>
>I en publiceringsinstans är CQ WCM-felsökningsfiltret **alltid** inaktiverat (även om det har konfigurerats som aktiverat).

## Anpassa sidor som visas av felhanteraren {#how-to-customize-pages-shown-by-the-error-handler}

Du kan utveckla egna skript för att anpassa sidorna som visas i felhanteraren när ett fel inträffar. För att göra detta använder du [AEM standardövertäckningsmekanism](/help/implementing/developing/introduction/overlays.md) så att dina anpassade sidor skapas under `/apps` och täcker över standardsidorna som är under `/libs`.

1. Kopiera standardskripten i databasen:

   * från `/libs/sling/servlet/errorhandler/`
   * till `/apps/sling/servlet/errorhandler/`

   Målsökvägen finns inte som standard, så du måste skapa den första gången.

1. Navigera till `/apps/sling/servlet/errorhandler`. Här kan du antingen:

   * redigera lämpligt skript för att ge den information som behövs. eller
   * skapa och redigera ett nytt skript för den kod som behövs.

1. Spara ändringarna och testa.

>[!CAUTION]
>
>Skriptet `404.jsp` har utformats särskilt för att hantera AEM autentisering. särskilt för att möjliggöra systeminloggning vid dessa fel.
>
>Därför bör det här manuset ersättas med stor omsorg.

### Anpassa svaret till HTTP 500-fel {#customizing-the-response-to-http-errors}

HTTP [500 Internal Server Error](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) indikerar ett serversidesfel, till exempel att servern påträffade ett oväntat tillstånd som gjorde att den inte kunde utföra begäran.

När bearbetningen av en begäran resulterar i ett undantag, är Apache Sling-ramverket (som AEM bygger på):

* Loggar undantaget
* Och returnerar i svarstexten:
   * HTTP-svarskoden 500
   * Undantagets stackspårning

Genom att [anpassa de sidor som visas av felhanteraren](#how-to-customize-pages-shown-by-the-error-handler) kan ett `500.jsp`-skript skapas. Den används dock bara om `HttpServletResponse.sendError(500)` körs explicit; d.v.s. från en undantagskatalog.

Annars är svarskoden inställd på 500, men `500.jsp`-skriptet körs inte.

Om du vill hantera 500 fel måste filnamnet för felhanterarskriptet vara detsamma som undantagsklassen (eller superklassen). Om du vill hantera alla sådana undantag kan du skapa ett skript `/apps/sling/servlet/errorhandler/Throwable.jsp` eller `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>På en författarinstans är [CQ WCM Debug Filter](/help/implementing/deploying/configuring-osgi.md) aktiverat som standard. Detta resulterar alltid i svarskoden 200. Standardfelhanteraren svarar genom att skriva den fullständiga stackspårningen till svaret.
>
>För en anpassad felhanterare behövs svar med kod 500, så [CQ WCM Debug Filter måste inaktiveras.](/help/implementing/deploying/configuring-osgi.md) Detta garanterar att svarskoden 500 returneras, vilket i sin tur utlöser rätt Sling-felhanterare.
>
>I en publiceringsinstans är CQ WCM-felsökningsfiltret **alltid** inaktiverat (även om det har konfigurerats som aktiverat).
