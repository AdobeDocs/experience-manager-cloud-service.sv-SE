---
title: Anpassade HTTP-huvuden
description: Lär dig hur du konfigurerar anpassade HTTP-rubriker som ska skickas till e-handelsmotorn, tillsammans med de som redan skickats av CIF.
exl-id: 2cef5d4b-45f6-4d72-a24b-67ca53d9057d
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Anpassade HTTP-huvuden {#custom-http-headers}

## Ökning {#overview}

För att få bättre kontroll över sin serverdel kan författarna konfigurera anpassade HTTP-rubriker som skickas till e-handelsmotorn, tillsammans med de som redan skickats av CIF. Vanliga användningsfall är bland annat multibutiksinställningar där du kan använda HTTP-huvuden för att styra svaret från e-handelsserverdelen.

>[!NOTE]
>
>Utvecklare kan alltid konfigurera anpassade HTTP-huvuden med hjälp av GraphQL klientkonfiguration.
>

## Konfiguration {#configuration}

Om du vill konfigurera anpassade HTTP-huvuden måste du först definiera dem. De anpassade HTTP-rubrikerna måste först definieras genom att de läggs till i `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` tjänstkonfiguration med en OSGi-konfiguration.

Du kan konfigurera värdena för HTTP-rubrikerna på Cloud Servicens konfigurationssida för ditt projekt:

1. Gå till konfigurationssidan för Cloud Servicen under Verktyg > Cloud Services > CIF Konfiguration
1. Öppna en befintlig konfiguration eller skapa en
1. Gå till fliken &quot;Avancerat&quot; och leta upp det anpassade fältet för HTTP-rubriker. Du kan markera rubrikerna som du definierade tidigare och tilldela dem värden.

Komponenterna som använder molntjänstkonfigurationen ovan skickar dessa HTTP-huvuden med alla GraphQL-förfrågningar.

## Begränsningar {#restrictions}

Även om tjänsten tillåter att rubriknamn definieras, inklusive standardnamn, är de inte tillgängliga för konfigurering. Du kan alltså inte åsidosätta de vanliga HTTP-rubrikerna med den här funktionen. En lista med begränsade rubriknamn finns [här](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers). Det finns ytterligare två rubriker som inte kan användas:

* &quot;Store&quot; - används av CIF för att identifiera Adobe Commerce Store
* &quot;Preview-Version&quot; - används av CIF för att hämta mellanprodukter
