---
title: Bästa tillvägagångssätt för installation och användning av AEM GraphQL med innehållsfragment
description: Lär dig de rekommenderade bästa metoderna för konfiguration och användning av AEM GraphQL med innehållsfragment.
source-git-commit: 9a544fb9d2494862efdb2263f3b9b61214c4b8b9
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 5%

---


# Bästa tillvägagångssätt för installation och användning av AEM GraphQL med innehållsfragment{#best-practices-setup-use-aem-graphql-content-fragments}

I dessa riktlinjer sammanfattas de rekommenderade bästa sätten att konfigurera, konfigurera och använda AEM med GraphQL- och Content Fragments.

## Komma igång {#getting-started}

Så här kommer du igång:

* [Vad är Headless?](/help/headless/what-is-headless.md)
* En översikt över de olika miljöerna i AEM [Arkitektur](/help/headless/deployment/architecture.md)

## Inställningar {#setup}

Om du vill konfigurera AEM GraphQL för användning med innehållsfragment och dina appar måste du konfigurera olika komponenter.

### Skapa GraphQL-slutpunkter (inklusive säkerhet) {#graphql-endpoint-creation}

Slutpunkten är den sökväg som används för att komma åt GraphQL för AEM. Dessa slutpunkter måste skapas och publiceras så att de kan nås på ett säkert sätt.

#### Information {#details-graphql-endpoint-creation}

[Hantera GraphQL-slutpunkter i AEM](/help/headless/graphql-api/graphql-endpoint.md)

#### Miljöer {#environments-graphql-endpoint-creation}

Slutpunkter måste konfigureras i:

* Författare
* Förhandsgranska
* Publicera

För:

* Utveckling
* Testning
* Produktion

### AEM Dispatcher-cachning {#dispatcher-caching}

>[!NOTE]
>Om cachelagring i Dispatcher är aktiverad är [CORS-inställningar](#cors-setup) behövs inte och kan därför ignoreras.

Cachelagring av beständiga frågor är inte aktiverat som standard i Dispatcher. Standardaktivering är inte möjlig eftersom kunder som använder CORS (Cross-Origin Resource Sharing) med flera ursprung måste granska och eventuellt uppdatera sin Dispatcher-konfiguration.

#### Information {#details-dispatcher-caching}

[GraphQL Persistent Queries - aktivera cachelagring i Dispatcher](/help/headless/deployment/dispatcher-caching.md)

#### Miljöer {#environments-dispatcher-caching}

Dispatcher är vanligtvis konfigurerad för:

* Publicera: produktion

### CORS-inställningar {#cors-setup}

>[!NOTE]
>Om du cachelagrar i [AEM](#dispatcher-caching) är aktiverat behövs inte CORS-inställningen och därför kan det här avsnittet ignoreras.

För att få åtkomst till GraphQL-slutpunkten måste en CORS-princip konfigureras och läggas till i ett AEM som distribueras till AEM via Cloud Manager. Detta görs genom att en lämplig OSGi CORS-konfigurationsfil läggs till för de önskade slutpunkterna.

#### Information {#details-cors-setup}

[CORS-konfiguration (Cross-Origin Resource Sharing)](/help/headless/deployment/cross-origin-resource-sharing.md)

#### Miljöer {#environments-cors-setup}

CORS är vanligtvis konfigurerad för:

* Publicera: produktion

### Autentisering {#authentication}

Ett primärt användningsexempel för Adobe Experience Manager as a Cloud Service (AEM) GraphQL API for Content Fragment Delivery är att ta emot fjärrfrågor från tredjepartsprogram eller -tjänster. Dessa fjärrfrågor kan kräva autentiserad API-åtkomst för säker leverans av headless-innehåll.

#### Information {#details-authentication}

[Autentisering för fjärrfrågor AEM GraphQL-frågor om innehållsfragment](/help/headless/security/authentication.md)

#### Miljöer {#environments-authentication}

Autentisering är vanligtvis konfigurerad för:

* Förhandsgranska
* Publicera

För:

* Utveckling
* Testning
* Produktion

### Behörigheter {#permissions}

Med en headless-implementering finns det flera säkerhets- och behörighetsområden som bör hanteras. Tillstånd och personer kan i stort sett övervägas baserat på den AEM miljön **Upphovsman** eller **Publicera**. Varje miljö innehåller olika personligheter och med olika behov.

#### Information {#details-permissions}

[Behörighetsaspekter för headless-innehåll](/help/headless/security/permissions.md)

#### Miljöer {#environments-permissions}

Behörigheter är vanligtvis konfigurerade för:

* Författare
* Förhandsgranska
* Publicera

För:

* Utveckling
* Testning
* Produktion

### Använd ett CDN (Content Delivery Network) {#cdn}

GraphQL-frågor och deras JSON-svar kan cachelagras om de är riktade som `GET` -begäranden när ett CDN används. Icke cachelagrade begäranden kan däremot vara mycket (resurskrävande) och långsamma att behandla, vilket kan få ytterligare negativa effekter på ursprungsmaterialets resurser.

#### Information {#details-cdn}

[CDN i AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md)

#### Miljöer {#environments-cdn}

Ett CDN är vanligtvis konfigurerat för:

* Publicera: produktion

### Konfigurera och skapa innehållsfragment {#cconfigure-create-content-fragments}

AEM GraphQL används för att hämta information från dina innehållsfragment. Dessa måste konfigureras, sedan en struktur och en plats definierad, innan du kan skapa innehållet.

#### Information {#details-content-fragments}

* [Skapa en konfiguration](/help/headless/setup/create-configuration.md)
* [Skapa en innehållsfragmentmodell](/help/headless/setup/create-content-model.md)
* [Skapa en resursmapp](/help/headless/setup/create-assets-folder.md)
* [Skapa och redigera dina innehållsfragment](/help/headless/setup/create-content-fragment.md)

#### Miljöer {#eenvironments-content-fragments}

Innehållsfragment definieras, skapas, testas, publiceras och öppnas på:

* Författare
* Förhandsgranska
* Publicera

För:

* Utveckling
* Testning
* Produktion

## Använda AEM GraphQL {#use-aem-graphql}

### Optimera dina GraphQL-frågor {#optimize-graphql-queries}

Riktlinjerna är till för att förhindra prestandaproblem i dina GraphQL-frågor.

#### Information {#details-optimize-graphql-queries}

[Optimera GraphQL-frågor](/help/headless/graphql-api/graphql-optimization.md)

>[!NOTE]
>
>Optimeringsriktlinjerna täcker cachekonfigurationen, som redan ingår i [Inställningar](#setup).

### Få tillgång till GraphQL från dina appar {#access-graphql-from-your-apps}

AEM headless CMS ger utvecklare frihet att skapa och leverera exceptionella upplevelser med de språk, ramverk och verktyg de redan är bekanta med.

#### Information {#details-your-apps}

* [Installera och använda AEM SDK för utveckling](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/aem-headless-sdk.html)
* [AEM resurser för utvecklare utan rubriker](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)
* Exempel, inklusive [Reagera](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/react-app.html), [Next.js](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/next-js.html), [Node.js](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/server-to-server-app.html), bland andra

#### Miljöer {#environments-your-apps}

Appar utvecklas, testas och används vanligtvis på:

* Förhandsgranska
* Publicera

För:

* Utveckling
* Testning
* Produktion

### Ytterligare resurser

Mer information om AEM GraphQL och Content Fragments finns i:

* [AEM GraphQL API för användning med innehållsfragment](/help/headless/graphql-api/content-fragments.md)
* [Använda GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md)
* [AEM resurser för utvecklare utan rubriker](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)
