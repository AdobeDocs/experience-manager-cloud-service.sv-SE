---
title: Anpassade felsidor
description: AEM har en standardfelhanterare för hantering av HTTP-fel som kan anpassas.
exl-id: b74c65d1-8ef5-4ad4-8255-8187f3b1d84c
feature: Developing
role: Admin, Architect, Developer
source-git-commit: de50d20dd4c17204ded1ff216d12520d04eafd04
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# Anpassa felsidor {#customizing-error-pages}

AEM har en standardfelhanterare för hantering av HTTP-fel, till exempel genom att visa:

![Standardfelmeddelande](assets/error-message-standard.png)

För att svara på fel tillhandahåller AEM ett `404.jsp`-skript under `/libs/sling/servlet/errorhandler`.

>[!TIP]
>
>Eftersom AEM baseras på Apache Sling finns mer information [&#x200B; i dokumentationen för hantering av Apache-fel &#x200B;](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html).

>[!NOTE]
>
>På en författarinstans är [CQ WCM Debug Filter](/help/implementing/deploying/configuring-osgi.md) aktiverat som standard. Detta resulterar alltid i svarskoden 200. Standardfelhanteraren svarar genom att skriva den fullständiga stackspårningen till svaret.
>
>I en publiceringsinstans är CQ WCM-felsökningsfiltret **alltid** inaktiverat (även om det är aktiverat).

>[!NOTE]
>
>Mer information om felhantering i Dispatcher finns i [Konfigurera CDN-felsidor](/help/implementing/dispatcher/cdn-error-pages.md).

## Anpassa sidor som visas av felhanteraren {#how-to-customize-pages-shown-by-the-error-handler}

Du kan utveckla egna skript för att anpassa sidorna som visas i felhanteraren när ett fel inträffar. För att göra detta använder du [AEM standardövertäckningsmekanism](/help/implementing/developing/introduction/overlays.md) så att dina anpassade sidor skapas under `/apps` och övertäcker standardsidorna som finns under `/libs`.

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
>Skriptet `404.jsp` har utformats särskilt för att hantera AEM-autentisering, särskilt för att tillåta systeminloggning vid dessa fel.
>
>Därför bör det här manuset ersättas med stor omsorg.

### Anpassa svaret till HTTP 500-fel {#customizing-the-response-to-http-errors}

HTTP [500 Internal Server Error](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) indikerar ett serversidesfel, t.ex. att servern påträffade ett oväntat tillstånd som gjorde att den inte kunde utföra begäran.

När bearbetningen av en begäran resulterar i ett undantag, Apache Sling-ramverket (som AEM bygger på):

* Loggar undantaget
* Och returnerar i svarstexten:
   * HTTP-svarskoden 500
   * Undantagets stackspårning

Genom att [anpassa sidorna som visas av felhanteraren](#how-to-customize-pages-shown-by-the-error-handler) kan ett `500.jsp`-skript skapas. Den används dock bara om `HttpServletResponse.sendError(500)` körs explicit, det vill säga från en undantagskatalog.

Annars är svarskoden inställd på 500, men skriptet `500.jsp` körs inte.

Om du vill hantera 500 fel måste filnamnet för felhanterarskriptet vara detsamma som undantagsklassen (eller superklassen). Om du vill hantera alla sådana undantag kan du skapa ett skript `/apps/sling/servlet/errorhandler/Throwable.jsp` eller `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!NOTE]
>
>I AEM som Cloud Service visar CDN en allmän felsida när ett 5XX-fel tas emot från serverdelen. Om du vill tillåta att det faktiska svaret från backend skickas genom måste du lägga till följande rubrik i svaret: `x-aem-error-pass: true`.
>&#x200B;>Detta fungerar bara för svar från AEM eller lagret Apache/Dispatcher. Andra oväntade fel från mellanliggande infrastrukturlager visar fortfarande den allmänna felsidan.

>[!CAUTION]
>
>På en författarinstans är [CQ WCM Debug Filter](/help/implementing/deploying/configuring-osgi.md) aktiverat som standard. Detta resulterar alltid i svarskoden 200. Standardfelhanteraren svarar genom att skriva den fullständiga stackspårningen till svaret.
>
>För en anpassad felhanterare krävs svar med kod 500, så [CQ WCM Debug Filter måste inaktiveras](/help/implementing/deploying/configuring-osgi.md). Detta garanterar att svarskoden 500 returneras, vilket i sin tur utlöser rätt Sling-felhanterare.
>
>I en publiceringsinstans är CQ WCM-felsökningsfiltret **alltid** inaktiverat (även om det är aktiverat).
