---
title: SPA- och serveråtergivning
description: Om du använder SSR-återgivning (server side rendering) i SPA kan det snabba upp den initiala inläsningen av sidan och sedan skicka vidare återgivningen till klienten.
translation-type: tm+mt
source-git-commit: fc61f13fbf976c43fcdd6921178a9bd4e82fc68d
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 0%

---


# Återgivning på SPA- och serversidan{#spa-and-server-side-rendering}

Single page-applikationer (SPA) kan ge användaren en rik, dynamisk upplevelse som reagerar och beter sig på välbekanta sätt, ofta precis som ett systemspecifikt program. [Detta uppnås genom att kunden förlitar sig på att läsa in innehållet i förväg och sedan gör en reaktiv hantering av ](introduction.md#how-does-a-spa-work) användarinteraktionen, vilket minimerar mängden kommunikation mellan klienten och servern.

Detta kan dock leda till längre inledande inläsningstider, särskilt om SPA är stor och har mycket innehåll. För att optimera inläsningstiden kan en del av innehållet återges på serversidan. Serversidorendering (SSR) kan snabba upp den initiala inläsningen av sidan och sedan överföra ytterligare återgivning till klienten.

## När SSR {#when-to-use-ssr} ska användas

SSR krävs inte för alla projekt. Även om AEM stöder JS SSR fullt ut för SPA rekommenderar Adobe inte att man implementerar det systematiskt för varje projekt.

När du beslutar dig för att implementera SSR måste du först uppskatta vilken ytterligare komplexitet, insats och kostnad som SSR innebär på ett realistiskt sätt för projektet, inklusive det långsiktiga underhållet. En SSR-arkitektur bör endast väljas när mervärdet klart överstiger de uppskattade kostnaderna.

SSR ger vanligtvis ett visst värde när det finns ett tydligt&quot;ja&quot; till någon av följande frågor:

* **SEO:** Krävs det fortfarande SSR för att din webbplats ska kunna indexeras korrekt av sökmotorer som genererar trafik? Kom ihåg att de viktigaste sökmotorcrawlarna nu utvärderar JS.
* **Sidhastighet:** Ger SSR en mätbar hastighetsförbättring i realtidsmiljöer och ökar den övergripande användarupplevelsen?

Endast när minst en av dessa två frågor besvaras med ett tydligt&quot;ja&quot; för ditt projekt rekommenderar Adobe att SSR implementeras. I följande avsnitt beskrivs hur du gör detta med Adobe I/O Runtime.

## Adobe I/O Runtime {#adobe-i-o-runtime}

Om du är [säker på att ditt projekt kräver SSR](#when-to-use-ssr) bör du använda Adobe I/O Runtime som lösning rekommenderas i Adobe.

Mer information om Adobe I/O Runtime finns på

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html)  - för en översikt över tjänsten
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) - för detaljerad dokumentation om plattformen

I följande avsnitt beskrivs hur Adobe I/O Runtime kan användas för att implementera SSR för dina SPA i två olika modeller:

* [AEM kommunikationsflöde](#aem-driven-communication-flow)
* [Adobe I/O Runtime-drivet kommunikationsflöde](#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe rekommenderar en separat Adobe I/O Runtime-instans för varje AEM (författare, publicering, scen osv.).

## Fjärrrenderingskonfiguration {#remote-content-renderer-configuration}

AEM måste veta var det fjärråtergivna innehållet kan hämtas. Oavsett [vilken modell du väljer att implementera för SSR,](#adobe-i-o-runtime) måste du ange hur du ska AEM åtkomst till den här fjärråtergivningstjänsten.

Detta görs via tjänsten **RemoteContentRenderer - Configuration Factory OSGi**. Sök efter strängen RemoteContentRenderer i webbkonsolens konfigurationskonsol på `http://<host>:<port>/system/console/configMgr`.

![Renderingskonfiguration](assets/renderer-configuration.png)

Följande fält är tillgängliga för konfigurationen:

* **Mönster**  för innehållssökväg - Reguljärt uttryck för att matcha en del av innehållet, om det behövs
* **URL**  för fjärrslutpunkt - URL för slutpunkten som ansvarar för att generera innehållet
   * Använd det säkra HTTPS-protokollet om det inte finns i det lokala nätverket.
* **Ytterligare begäranrubriker**  - Ytterligare rubriker som ska läggas till i begäran som skickas till fjärrslutpunkten
   * Mönster: `key=value`
* **Timeout**  för begäran - Timeout för fjärrvärdbegäran i millisekunder

>[!NOTE]
>
>Oavsett om du väljer att implementera [AEM kommunikationsflöde](#aem-driven-communication-flow) eller [Adobe I/O Runtime-drivet flöde, måste du definiera en fjärrkonfiguration för innehållsåtergivning.](#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Den här konfigurationen utnyttjar [Renderer för fjärrinnehåll,](#remote-content-renderer), som har ytterligare tillgängliga alternativ för tillägg och anpassning.

## AEM kommunikationsflöde {#aem-driven-communication-flow}

När du använder SSR innehåller arbetsflödet [för komponentinteraktion](introduction.md#interaction-with-the-spa-editor) för SPA i AEM en fas i vilken det inledande innehållet i appen genereras på Adobe I/O Runtime.

1. Webbläsaren begär SSR-innehåll från AEM.
1. AEM skickar modellen till Adobe I/O Runtime.
1. Adobe I/O Runtime returnerar det genererade innehållet.
1. AEM visar HTML-koden som returneras av Adobe I/O Runtime via HTML-mallen för backend-sidkomponenten.

![SSE CMS-driven AEM Adobe I/O](assets/ssr-cms-drivenaemnode-adobeio.png)

## Adobe I/O Runtime-drivet kommunikationsflöde {#adobe-i-o-runtime-driven-communication-flow}

I föregående avsnitt beskrivs standardimplementeringen och den rekommenderade implementeringen av serversidans återgivning med avseende på SPA i AEM, där AEM utför startsvällning och -visning av innehåll.

Alternativt kan SSR implementeras så att Adobe I/O Runtime ansvarar för startkomponenten, vilket effektivt kan vända kommunikationsflödet.

Båda modellerna är giltiga och stöds av AEM. Man bör dock beakta fördelarna och nackdelarna med var och en av modellerna innan man implementerar en viss modell.

<table>
 <tbody>
  <tr>
   <th><strong>Bootstrap</strong></th>
   <th><strong>Fördelar</strong></th>
   <th><strong>Nackdelar</strong></th>
  </tr>
  <tr>
   <th><strong>via AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM hanterar inmatning av bibliotek där det behövs</li>
     <li>Resurser behöver bara underhållas på AEM<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Okänd för SPA utvecklare<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>via Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>Mer bekant för SPA utvecklare<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Klientlib-resurser som krävs av programmet, t.ex. CSS och JavaScript, måste göras tillgängliga av AEM utvecklare via egenskapen <code><a href="/help/implementing/developing/introduction/clientlibs.md">allowProxy</a></code><br /> </li>
     <li>Resurserna måste synkroniseras mellan AEM och Adobe I/O Runtime<br /> </li>
     <li>Om du vill aktivera redigering av SPA kan det behövas en proxyserver för Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Planering för SSR {#planning-for-ssr}

I allmänhet behöver bara en del av ett program återges på serversidan. Det vanliga exemplet är det innehåll som ska visas ovanför vikningen vid den första inläsningen av sidan återges på serversidan. Detta sparar tid genom att leverera till klienten, som redan har återgett innehåll. När användaren interagerar med SPA återges det extra innehållet av klienten.

När du funderar på att implementera serversidesåtergivning för SPA måste du kontrollera vilka delar av programmet som det är nödvändigt.

## Utveckla en SPA med SSR {#developing-an-spa-using-ssr}

SPA kan återges av klienten (i webbläsaren) eller serversidan. Webbläsaregenskaper som fönsterstorlek och plats finns inte på den återgivna serversidan. SPA bör därför vara isomorfa, utan att man vet var de kommer att återges.

Om du vill använda SSR måste du distribuera koden i AEM och på Adobe I/O Runtime, som ansvarar för återgivningen på serversidan. Den mesta koden blir densamma, men serverspecifika åtgärder skiljer sig åt.

## SSR för SPA i AEM {#ssr-for-spas-in-aem}

SSR för SPA i AEM kräver Adobe I/O Runtime, vilket krävs för återgivning av programinnehållsserversidan. I programmets HTML anropas en resurs på Adobe I/O Runtime för att återge innehållet.

Precis som AEM stöder ramverken Angular och React SPA direkt, stöds även serversidorendering för Angular- och React-appar. Mer information finns i NPM-dokumentationen för båda ramverken.

## Renderare för fjärrinnehåll {#remote-content-renderer}

Konfigurationen [Remote Content Renderer](#remote-content-renderer-configuration) som krävs för att använda SSR med SPA i AEM finns i en mer generaliserad renderingstjänst som kan utökas och anpassas efter dina behov.

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` är en OSGi-tjänst som hämtar innehåll som återges på en fjärrserver, till exempel från Adobe I/O. Innehållet som skickas till fjärrservern baseras på den begärandeparameter som skickas.

`RemoteContentRenderingService` kan injiceras genom beroendeinvertering till antingen en anpassad Sling-modell eller servlet när ytterligare innehållsmanipulering krävs.

Den här tjänsten används internt av [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

`RemoteContentRendererRequestHandlerServlet` kan användas för att ställa in konfigurationen för begäran programmatiskt. `DefaultRemoteContentRendererRequestHandlerImpl`, den medföljande standardimplementeringen av begäranhanteraren, gör att du kan skapa flera OSGi-konfigurationer för att mappa en plats i innehållsstrukturen till en fjärrslutpunkt.

Implementera gränssnittet `RemoteContentRendererRequestHandler` om du vill lägga till en anpassad begärandehanterare. Se till att du anger `Constants.SERVICE_RANKING`-komponentegenskapen till ett heltal som är högre än 100, vilket är rankningen för `DefaultRemoteContentRendererRequestHandlerImpl`.

```javascript
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### Konfigurera OSGi-konfigurationen för standardhanteraren {#configure-default-handler}

Konfigurationen av standardhanteraren måste konfigureras enligt beskrivningen i avsnittet [Konfiguration av fjärrinnehållsåtergivning](#remote-content-renderer-configuration).

### Användning av fjärråtergivning av innehåll {#usage}

Så här hämtar du en servlet och returnerar innehåll som kan injiceras på sidan:

1. Kontrollera att fjärrservern är tillgänglig.
1. Lägg till ett av följande kodfragment i HTML-mallen för en AEM.
1. Du kan också skapa eller ändra OSGi-konfigurationerna.
1. Bläddra i webbplatsens innehåll

Vanligtvis är HTML-mallen för en sidkomponent huvudmottagaren för en sådan funktion.

```html
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### Krav {#requirements}

Servlets använder Sling Model Exporter för att serialisera komponentdata. Som standard stöds både `com.adobe.cq.export.json.ContainerExporter` och `com.adobe.cq.export.json.ComponentExporter` som Sling Model-kort. Om det behövs kan du lägga till klasser som begäran ska anpassas till med `RemoteContentRendererServlet` och implementera `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. Ytterligare klasser måste utöka `ComponentExporter`.
