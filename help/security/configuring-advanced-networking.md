---
title: Konfigurera avancerat nätverk för AEM as a Cloud Service
description: Lär dig hur du konfigurerar avancerade nätverksfunktioner som VPN eller en flexibel eller dedikerad IP-adress för AEM as a Cloud Service
source-git-commit: fa11beb1dfdd8dd2a1a5d49ece059f5894c835be
workflow-type: tm+mt
source-wordcount: '2836'
ht-degree: 0%

---


# Konfigurera avancerat nätverk för AEM as a Cloud Service {#configuring-advanced-networking}

Den här artikeln beskriver de olika avancerade nätverksfunktionerna i AEM as a Cloud Service, inklusive självbetjäningsprovisionering av VPN, icke-standardportar och dedikerade IP-adresser.

## Översikt {#overview}

AEM as a Cloud Service har flera typer av avancerade nätverksfunktioner som kan konfigureras av kunder med API:er för Cloud Manager. Bland dessa finns:

* [Flexibel portutgång](#flexible-port-egress) - konfigurera AEM as a Cloud Service för att tillåta utgående trafik från icke-standardportar
* [Dedikerad IP-adress för utgångar](#dedicated-egress-IP-address) - konfigurera trafik från AEM as a Cloud Service till att härröra från en unik IP-adress
* [VPN (Virtual Private Network)](#vpn) - säker trafik mellan en kunds infrastruktur och AEM as a Cloud Service, för kunder som har VPN-teknik

I den här artikeln beskrivs dessa alternativ i detalj, inklusive hur de kan konfigureras. Som en allmän konfigurationsstrategi `/networkInfrastructures` API-slutpunkten anropas på programnivå för att deklarera önskad typ av avancerat nätverk, följt av ett anrop till `/advancedNetworking` slutpunkt för varje miljö för att aktivera infrastrukturen och konfigurera miljöspecifika parametrar. Referera till lämpliga slutpunkter i Cloud Managers API-dokumentation för varje formell syntax samt exempelbegäranden och svar.

Ett program kan tillhandahålla en enda avancerad nätverksvariant. När du ska välja mellan flexibel portutgång och dedikerad IP-adress för utgångar bör du välja flexibel portutgång om en viss IP-adress inte krävs, eftersom Adobe kan optimera prestanda för flexibel portbelastningstrafik.

>[!INFO]
>
>Avancerade nätverk är inte tillgängliga för sandlådeprogrammet.
>Miljöer måste också uppgraderas till AEM version 5958 eller senare.

>[!NOTE]
>
>Kunder som redan har etablerat sig med äldre dedikerad utgångsteknik som behöver konfigurera något av dessa alternativ bör inte göra det, annars kan platsanslutningen påverkas. Kontakta Adobe Support för att få hjälp.

## Flexibla portägg {#flexible-port-egress}

Med den här avancerade nätverksfunktionen kan du konfigurera AEM as a Cloud Service att utlösa trafik via andra portar än HTTP (port 80) och HTTPS (port 443), som är öppna som standard.

### Överväganden {#flexible-port-egress-considerations}

Det rekommenderas att du väljer Flexibel portutgång om du inte behöver VPN och inte behöver en dedikerad IP-adress för utgångar eftersom trafik som inte är beroende av en dedikerad utgångs kan uppnå högre genomströmning.

### Konfiguration {#configuring-flexible-port-egress-provision}

En gång per program, POSTEN `/program/<programId>/networkInfrastructures` slutpunkten anropas, bara värdet för `flexiblePortEgress` för `kind` parameter och region. Slutpunkten svarar med `network_id`, samt annan information, inklusive status. Alla parametrar och den exakta syntaxen bör refereras i API-dokumenten.

När nätverksinfrastrukturen väl har anropats tar det oftast ca 15 minuter innan den etableras. Ett anrop till Cloud Managers [slutpunkt för GET av nätverksinfrastruktur](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getNetworkInfrastructure) skulle visa statusen&quot;ready&quot;.

Om konfigurationen för flexibel portutgångar som omfattar programmet är klar kan du `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` Slutpunkten måste anropas per miljö för att nätverk på miljönivå ska kunna aktiveras och för att eventuella regler för portvidarebefordran ska kunna deklareras. Parametrar kan konfigureras per miljö för att erbjuda flexibilitet.

Reglerna för portvidarebefordran bör deklareras för alla portar utom 80/443 genom att ange uppsättningen målvärdar (namn eller IP och med portar). För varje målvärd måste kunderna mappa den avsedda destinationsporten till en port från 30000 till 30999.

API:t bör svara på bara några sekunder, vilket anger uppdateringsstatus och efter cirka 10 minuter, slutpunktens `GET` -metoden ska ange att avancerade nätverk är aktiverade.

### Uppdateringar {#updating-flexible-port-egress-provision}

Programnivåkonfigurationen kan uppdateras genom att anropa `PUT /api/program/<program_id>/network/<network_id>` slutpunkten och börjar gälla inom några minuter.

>[!NOTE]
>
> Parametern &quot;kind&quot; (`flexiblePortEgress`, `dedicatedEgressIP` eller `VPN`) kan inte ändras. Kontakta kundsupporten om du behöver hjälp med att beskriva vad som redan har skapats och orsaken till ändringen.

Portvidarebefordringsreglerna per miljö kan uppdateras genom att anropa `PUT /program/{programId}/environment/{environmentId}/advancedNetworking` slutpunkt, se till att inkludera hela uppsättningen konfigurationsparametrar, i stället för en delmängd.

### Ta bort eller inaktivera flexibla portklasser {#deleting-disabling-flexible-port-egress-provision}

För att **delete** nätverksinfrastrukturen, skicka in en kundsupportanmälan med en beskrivning av vad som har skapats och varför det behöver tas bort.

För att **disable** flexibel portutgång från en viss miljö, anropa `DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()`.

Mer information finns i [API-dokumentation för Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### Trafikroutning {#flexible-port-egress-traffic-routing}

Http- eller https-trafik som går till mål via port 80 eller 443 kommer att gå via en förkonfigurerad proxy, förutsatt att Java-standardbiblioteket används. För http- och https-trafik som går genom andra portar bör en proxy konfigureras med följande egenskaper.

* `AEM_HTTP_PROXY_HOST / AEM_HTTPS_PROXY_HOST`
* `AEM_HTTP_PROXY_PORT / AEM_HTTPS_PROXY_PORT`

Här följer till exempel exempelkoden som du kan skicka en begäran till `www.example.com:8443`:

```java
String url = "www.example.com:8443"
var proxyHost = System.getenv("AEM_HTTPS_PROXY_HOST");
var proxyPort = Integer.parseInt(System.getenv("AEM_HTTPS_PROXY_PORT"));
HttpClient client = HttpClient.newBuilder()
      .proxy(ProxySelector.of(new InetSocketAddress(proxyHost, proxyPort)))
      .build();
 
HttpRequest request = HttpRequest.newBuilder().uri(URI.create(url)).build();
HttpResponse<String> response = client.send(request, BodyHandlers.ofString());
```

Om du använder Java-nätverksbibliotek som inte är standard ska du konfigurera proxies med egenskaperna ovan för all trafik.

Ej http/s-trafik med destinationer via portar som deklarerats i `portForwards` parametern ska referera till en egenskap som kallas `AEM_PROXY_HOST`, tillsammans med den mappade porten. Till exempel:

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

Tabellen nedan beskriver trafikdirigering:

<table>
<thead>
  <tr>
    <th>Trafik</th>
    <th>Målningsvillkor</th>
    <th>Port</th>
    <th>Anslutning</th>
    <th>Exempel</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>HTTP- eller https-protokoll</b></td>
    <td>Standard-http/s-trafik</td>
    <td>80 eller 443</td>
    <td>Tillåtet</td>
    <td></td>
  </tr> 
  <tr>
    <td></td>
    <td>Ej standardiserad trafik (på andra portar utanför 80 eller 443) via http-proxy som konfigurerats med dessa miljövariabler:<br><ul>
     <li>AEM_HTTP_PROXY_HOST / AEM_HTTPS_PROXY_HOST</li>
     <li>AEM_HTTP_PROXY_PORT / AEM_HTTPS_PROXY_PORT</li>
    </ul>
    <td>Portar utanför 80 eller 443</td>
    <td>Tillåtet</td>
  </tr>
  <tr>
    <td></td>
    <td>Ej standardiserad trafik (på andra portar utanför port 80 eller 443) som inte använder http-proxy</td>
    <td>Portar utanför 80 eller 443</td>
    <td>Blockerad</td>
    <td></td>
  </tr>
  <tr>
    <td><b>Non-http or non-https</b></td>
    <td>Klienten ansluter till <code>AEM_PROXY_HOST</code> miljövariabel med <code>portOrig</code> deklareras i <code>portForwards</code> API-parameter.</td>
    <td>Alla</td>
    <td>Tillåtet</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>Allt annat</td>
    <td>Alla</td>
    <td>Blockerad</td>
    <td><code>db.example.com:5555</code></td>
  </tr>
</tbody>
</table>

**Konfiguration av Apache/Dispatcher**

AEM Cloud Service Apache/Dispatcher-skiktets `mod_proxy` -direktivet kan konfigureras med hjälp av de egenskaper som beskrivs ovan.

```
ProxyRemote "http://example.com" "http://${AEM_HTTP_PROXY_HOST}:3128"
ProxyPass "/somepath" "http://example.com"
ProxyPassReverse "/somepath" "http://example.com"
```

```
SSLProxyEngine on //needed for https backends
 
ProxyRemote "https://example.com:8443" "http://${AEM_HTTPS_PROXY_HOST}:3128"
ProxyPass "/somepath" "https://example.com:8443"
ProxyPassReverse "/somepath" "https://example.com:8443"
```

## IP-adress för dedikerad utpressning {#dedicated-egress-IP-address}

>[!NOTE]
>
>Om du har fått en dedikerad utgående IP-adress före versionen från september 2021 (10/6/21), se [Äldre dedikerade gruppadresskunder](#legacy-dedicated-egress-address-customers).

### Fördelar {#benefits}

Den här dedikerade IP-adressen kan förbättra säkerheten vid integrering med SaaS-leverantörer (som en CRM-leverantör) eller andra integreringar utanför AEM as a Cloud Service som erbjuder en tillåtelselista av IP-adresser. Genom att lägga till den dedikerade IP-adressen till tillåtelselista säkerställer det att endast trafik från kundens AEM Cloud Service tillåts att flöda in i den externa tjänsten. Detta är utöver trafik från andra IP-adresser som tillåts.

Utan den dedikerade IP-adressfunktionen aktiverad flödar trafik från AEM as a Cloud Service genom en uppsättning IP-adresser som delas med andra kunder.

### Konfiguration {#configuring-dedicated-egress-provision}

>[!INFO]
>
>Splunk-vidarebefordringsfunktionen är inte möjlig från en dedikerad IP-adress.

IP-adressen för den dedikerade IP-adressen är identisk med [flexibel portutgång](#configuring-flexible-port-egress-provision).

Den största skillnaden är att trafiken alltid kommer att gå från en dedikerad, unik IP-adress. Om du vill hitta IP-adressen använder du en DNS-matchare för att identifiera IP-adressen som är associerad med `p{PROGRAM_ID}.external.adobeaemcloud.com`. IP-adressen förväntas inte ändras, men om den behöver ändras i framtiden kommer ett avancerat meddelande att skickas.

Förutom routningsreglerna som stöds av flexibel portutgång i `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` slutpunkt, dedikerad IP-adress för utgångar har stöd för en `nonProxyHosts` parameter. Detta gör att du kan deklarera en uppsättning värdar som ska dirigeras genom ett delat IP-adressintervall i stället för den dedikerade IP-adressen, vilket kan vara användbart eftersom trafikutjämning via delade IP-adresser kan optimeras ytterligare. The `nonProxyHost` URL:er kan följa mönstren för `example.com` eller `*.example.com`, där jokertecknet bara stöds i början av domänen.

När man ska välja mellan flexibel portutgång och dedikerad IP-adress för utgångar bör man välja flexibel portutgång om en viss IP-adress inte krävs, eftersom Adobe kan optimera prestanda för flexibel portutgångstrafik.

### Trafikroutning {#dedcated-egress-ip-traffic-routing}

<table>
<thead>
  <tr>
    <th>Trafik</th>
    <th>Målvillkor</th>
    <th>Port</th>
    <th>Anslutning</th>
    <th>Exempel</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>HTTP- eller https-protokoll</b></td>
    <td>Trafik till Azure eller Adobe-tjänster</td>
    <td>Alla</td>
    <td>Genom de delade IP-klusteradresserna (inte den dedikerade IP-adressen)</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>Värden som matchar <code>nonProxyHosts</code> parameter</td>
    <td>80 eller 443</td>
    <td>Genom de delade kluster-IP:n</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Värden som matchar <code>nonProxyHosts</code> parameter</td>
    <td>Portar utanför 80 eller 443</td>
    <td>Blockerad</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Via http-proxykonfiguration, konfigurerad som standard för http/s-trafik med Java HTTP-klientbibliotek</td>
    <td>Alla</td>
    <td>Genom den dedikerade IP-adressen för utgångar</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Ignorerar http-proxykonfiguration (t.ex. om den uttryckligen tagits bort från standard-Java HTTP-klientbiblioteket eller om ett Java-bibliotek som ignorerar standardproxykonfigurationen används)</td>
    <td>80 eller 443</td>
    <td>Genom de delade kluster-IP:n</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Ignorerar http-proxykonfiguration (t.ex. om den uttryckligen tagits bort från standard-Java HTTP-klientbiblioteket eller om ett Java-bibliotek som ignorerar standardproxykonfigurationen används)</td>
    <td>Portar utanför 80 eller 443</td>
    <td>Blockerad</td>
    <td></td>
  </tr>
  <tr>
    <td><b>Non-http or non-https</b></td>
    <td>Klienten ansluter till <code>AEM_PROXY_HOST</code> env-variabel med en <code>portOrig</code> deklareras i <code>portForwards</code> API-parameter</td>
    <td>Alla</td>
    <td>Genom den dedikerade IP-adressen för utgångar</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>Allt annat</td>
    <td></td>
    <td>Blockerad</td>
    <td></td>
  </tr>
</tbody>
</table>

## Äldre dedikerade gruppadresskunder {#legacy-dedicated-egress-address-customers}

Om du har fått en dedikerad IP-adress för utgångar före 2021.09.30 kommer din dedikerade IP-funktion för utgångar att fungera enligt beskrivningen nedan.

### Funktionsanvändning {#feature-usage}

Funktionen är kompatibel med Java-kod eller bibliotek som resulterar i utgående trafik, förutsatt att de använder Java-standardegenskaper för proxykonfigurationer. I praktiken bör detta omfatta de vanligaste biblioteken.

Nedan visas ett kodexempel:

```java
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();
  URLConnection connection = finalUrl.openConnection();
  connection.addRequestProperty("Accept", "application/json");
  connection.addRequestProperty("X-API-KEY", apiKey);

  try (InputStream responseStream = connection.getInputStream(); Reader responseReader = new BufferedReader(new InputStreamReader(responseStream, Charsets.UTF_8))) {
    return new JSONObject(new JSONTokener(responseReader));
  }
}
```

Vissa bibliotek kräver explicit konfiguration för att använda Java-standardegenskaper för proxykonfigurationer.

Ett exempel med Apache HttpClient, som kräver explicita anrop till
[`HttpClientBuilder.useSystemProperties()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClientBuilder.html) eller använda
[`HttpClients.createSystem()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClients.html#createSystem()):

```java
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();

  HttpClient httpClient = HttpClientBuilder.create().useSystemProperties().build();
  HttpGet request = new HttpGet(finalUrl.toURI());
  request.setHeader("Accept", "application/json");
  request.setHeader("X-API-KEY", apiKey);
  HttpResponse response = httpClient.execute(request);
  String result = EntityUtils.toString(response.getEntity());
}
```

Samma dedikerade IP-adress används för alla kundprogram i Adobe och för alla miljöer i respektive program. Det gäller både författare och publiceringstjänster.

Endast HTTP- och HTTPS-portar stöds. Detta inkluderar HTTP/1.1 och HTTP/2 vid kryptering.

### Felsökningsöverväganden {#debugging-considerations}

Kontrollera loggarna i destinationstjänsten om de är tillgängliga för att validera att trafiken faktiskt är utgående från den förväntade dedikerade IP-adressen. I annat fall kan det vara praktiskt att ringa ut till en felsökningstjänst som [https://ifconfig.me/IP](https://ifconfig.me/IP), som returnerar den anropande IP-adressen.

## VPN (Virtual Private Network) {#vpn}

Med VPN kan du ansluta till en lokal infrastruktur eller ett datacenter från författare, publicera eller förhandsgranska. Till exempel, för sättet att komma åt en databas.

Det gör det även möjligt att ansluta till SaaS-leverantörer som CRM-leverantörer som stöder VPN eller ansluter från ett företagsnätverk till AEM as a Cloud Service författare, förhandsgranska eller publicera.

De flesta VPN-enheter med IPSec-teknik stöds. Läs listan över enheter på [den här sidan](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-devices#devicetable), baserat på informationen i **RouteBased configuration instructions** kolumn. Konfigurera enheten enligt beskrivningen i tabellen.

### Allmänna överväganden {#general-vpn-considerations}

* Stödet är begränsat till en VPN-anslutning
* Splunk-vidarebefordran är inte möjlig via en VPN-anslutning.

### Skapande {#vpn-creation}

En gång per program, POSTEN `/program/<programId>/networkInfrastructures` slutpunkten anropas och skickar en nyttolast med konfigurationsinformation som: värdet på vpn för `kind` parameter, region, adressutrymme (lista med CIDR - observera att detta inte kan ändras senare), DNS-matchare (för att matcha namn i kundens nätverk) och VPN-anslutningsinformation som gatewaykonfiguration, delad VPN-nyckel och IP-säkerhetsprincipen. Slutpunkten svarar med `network_id`, samt annan information, inklusive status. Hela uppsättningen parametrar och exakt syntax ska refereras i [API-dokumentation](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure).

När det anropas tar det normalt mellan 45 och 60 minuter innan nätverksinfrastrukturen etableras. API:ts GET-metod kan anropas för att returnera den aktuella statusen, som så småningom kommer att vändas från `creating` till `ready`. Läs API-dokumentationen för alla lägen.

Om den programomfattande VPN-konfigurationen är klar kan du `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` slutpunkten måste anropas per miljö för att aktivera nätverk på miljönivå och för att deklarera regler för portvidarebefordran. Parametrar kan konfigureras per miljö för att erbjuda flexibilitet.

Se [API-dokumentation](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/enableEnvironmentAdvancedNetworkingConfiguration) för mer information.

Regler för portvidarebefordran ska deklareras för TCP-trafik som inte är http/s-protokoll och som ska dirigeras via VPN genom att ange uppsättningen målvärdar (namn eller IP och med portar). För varje målvärd måste kunderna mappa den avsedda destinationsporten till en port mellan 30000 och 30999, där värdena måste vara unika för alla miljöer i programmet. Kunderna kan även lista en uppsättning URL i `nonProxyHosts` parameter, som deklarerar URL för vilken trafik ska kringgå VPN-routning, men i stället via ett delat IP-intervall. Den följer mönstren i `example.com` eller `*.example.com`, där jokertecknet bara stöds i början av domänen.

API:t bör svara på bara några sekunder, vilket anger statusen `updating` och efter cirka 10 minuter visar ett anrop till Cloud Managers miljöslutpunkt statusen för GET `ready`, vilket anger att uppdateringen av miljön har tillämpats.

Observera att även om det inte finns några trafikdirigeringsregler för miljön (värdar eller bypass), `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` måste fortfarande anropas, bara med en tom nyttolast.

### Uppdaterar VPN {#updating-the-vpn}

VPN-konfigurationen på programnivå kan uppdateras genom att anropa `PUT /api/program/<program_id>/network/<network_id>` slutpunkt.

Observera att adressutrymmet inte kan ändras efter den första VPN-etableringen. Kontakta kundsupport om det är nödvändigt. Dessutom är `kind` parameter (`flexiblePortEgress`, `dedicatedEgressIP` eller `VPN`) kan inte ändras. Kontakta kundsupporten om du behöver hjälp med att beskriva vad som redan har skapats och orsaken till ändringen.

Cirkulationsregler per miljö kan uppdateras genom att anropa `PUT /program/{programId}/environment/{environmentId}/advancedNetworking` slutpunkt, se till att inkludera hela uppsättningen konfigurationsparameter, i stället för en delmängd. Miljöuppdateringar tar vanligtvis 5-10 minuter att installera.

### Ta bort eller inaktivera VPN {#deleting-or-disabling-the-vpn}

Om du vill ta bort nätverksinfrastrukturen skickar du en kundsupportanmälan med en beskrivning av vad som har skapats och varför det måste tas bort.

Om du vill inaktivera VPN för en viss miljö anropar du `DELETE /program/{programId}/environment/{environmentId}/advancedNetworking`. Mer information finns i [API-dokumentation](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### Trafikroutning {#vpn-traffic-routing}

Tabellen nedan beskriver trafikdirigering.

<table>
<thead>
  <tr>
    <th>Trafik</th>
    <th>Målvillkor</th>
    <th>Port</th>
    <th>Anslutning</th>
    <th>Exempel</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>HTTP- eller https-protokoll</b></td>
    <td>Trafik till Azure eller Adobe-tjänster</td>
    <td>Alla</td>
    <td>Genom de delade IP-klusteradresserna (inte den dedikerade IP-adressen)</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>Värden som matchar <code>nonProxyHosts</code> parameter</td>
    <td>80 eller 443</td>
    <td>Genom de delade kluster-IP:n</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Värden som matchar <code>nonProxyHosts</code> parameter</td>
    <td>Portar utanför 80 eller 443</td>
    <td>Blockerad</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Om IP-värdet faller inom <i>VPN-gateway-adress</i> utrymme och genom http-proxykonfiguration (konfigurerad som standard för http/s-trafik med Java HTTP-klientbibliotek som standard)</td>
    <td>Alla</td>
    <td>Via VPN</td>
    <td><code>10.0.0.1:443</code>Det kan också vara ett värdnamn.</td>
  </tr>
  <tr>
    <td></td>
    <td>Om IP-adressen inte faller inom <i>Adressutrymme för VPN-gateway</i> och via http-proxykonfiguration (konfigurerad som standard för http/s-trafik med Java HTTP-klientbibliotek som standard)</td>
    <td>Alla</td>
    <td>Genom den dedikerade IP-adressen för utgångar</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Ignorerar http-proxykonfiguration (t.ex. om den uttryckligen tagits bort från standard-Java HTTP-klientbiblioteket eller om Java-biblioteket som ignorerar standardproxykonfigurationen används)
</td>
    <td>80 eller 443</td>
    <td>Genom de delade kluster-IP:n</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Ignorerar http-proxykonfiguration (t.ex. om den uttryckligen tagits bort från standard-Java HTTP-klientbiblioteket eller om Java-biblioteket som ignorerar standardproxykonfigurationen används)</td>
    <td>Portar utanför 80 eller 443</td>
    <td>Blockerad</td>
    <td></td>
  </tr>
  <tr>
    <td><b>Non-http or non-https</b></td>
    <td>Om IP-värdet faller inom <i>Adressutrymme för VPN-gateway</i> och klienten ansluter till <code>AEM_PROXY_HOST</code> env-variabel med en <code>portOrig</code> deklareras i <code>portForwards</code> API-parameter</td>
    <td>Alla</td>
    <td>Via VPN</td>
    <td><code>10.0.0.1:3306</code>Det kan också vara ett värdnamn.</td>
  </tr>
  <tr>
    <td></td>
    <td>Om IP-adressen inte faller inom <i>Adressutrymme för VPN-gateway</i> omfång och klienten ansluter till <code>AEM_PROXY_HOST</code> env-variabel med en <code>portOrig</code> deklareras i <code>portForwards</code> API-parameter</td>
    <td>Alla</td>
    <td>Genom den dedikerade IP-adressen för utgångar</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Allt annat</td>
    <td>Alla</td>
    <td>Blockerad</td>
    <td></td>
  </tr>
</tbody>
</table>

### Användbara domäner för konfiguration{#vpn-useful-domains-for-configuration}

Bilden nedan visar en visuell representation av en uppsättning domäner och associerade IP-adresser som är användbara för konfiguration och utveckling. Tabellen nedan beskriver dessa domäner och IP-adresser.

![VPN-domänkonfiguration](/help/security/assets/AdvancedNetworking.jpg)

<table>
<thead>
  <tr>
    <th>Domänmönster</th>
    <th>AEM</th>
    <th>Ingång (till AEM), betydelse</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>p{PROGRAM_ID}.external.adobeaemcloud.com</code></td>
    <td>Dedikerad IP-adress för utgångar för trafik som går till Internet i stället för via privata nätverk </td>
    <td>Anslutningar från VPN visas vid CDN från den här IP-adressen. Om du bara vill tillåta anslutningar från VPN att gå till AEM konfigurerar du Cloud Manager så att endast den här IP-adressen tillåts och så att allt annat blockeras. Mer information finns i avsnittet Begränsa ingång till VPN-anslutningar.</td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}-gateway.external.adobeaemcloud.com</code></td>
    <td>Ej tillämpligt</td>
    <td>VPN-gatewayens IP på AEM. En kunds nätverksteam kan använda detta för att endast tillåta VPN-anslutningar till sin VPN-gateway från en viss IP-adress. </td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.inner.adobeaemcloud.net</code></td>
    <td>IP-adressen för trafik från VPN:s AEM till kundsidan. Detta kan tillåtslista i kundens konfiguration för att säkerställa att anslutningar bara kan göras från AEM.</td>
    <td>Om kunden bara vill tillåta VPN-åtkomst till AEM bör de konfigurera CNAME DNS-poster att mappa <code>author-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code>  och/eller <code>publish-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> till detta.</td>
  </tr>
</tbody>
</table>

### Begränsa VPN till ingångsanslutningar {#restrict-vpn-to-ingress-connections}

Om du bara vill tillåta VPN-åtkomst till AEM kan tillåtelselista konfigureras i Cloud Manager så att endast IP-adressen som definieras av `p{PROGRAM_ID}.external.adobeaemcloud.com` får tala med miljön. Detta kan göras på samma sätt som andra IP-baserade tillåtelselista i Cloud Manager.

Om reglerna måste vara sökvägsbaserade använder du http-standarddirektiv på dispatchernivå för att neka eller tillåta vissa IP-adresser. De bör se till att de önskade sökvägarna inte heller är tillgängliga vid CDN så att begäran alltid kommer till ursprungsläget.

**Exempel på HTTP-konfiguration**

```
Order deny,allow
Deny from all
Allow from 192.168.0.1
Header always set Cache-Control private
```

## Övergång mellan avancerade nätverkstyper {#transitioning-between-advanced-networking-types}

Sedan `kind` parametern kan inte ändras. Kontakta kundsupport om du behöver hjälp med att beskriva vad som redan har skapats och orsaken till ändringen.
