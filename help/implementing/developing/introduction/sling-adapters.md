---
title: Använda Sling-adaptrar
description: Sling erbjuder ett adaptermönster för att enkelt översätta objekt som implementerar gränssnittet Adaptable
exl-id: 8ffe3bbd-01fe-44c2-bf60-7a4d25a6ba2b
source-git-commit: 5311ba7f001201fc94c73fa52bc7033716c1ba78
workflow-type: tm+mt
source-wordcount: '2214'
ht-degree: 0%

---

# Använda Sling-adaptrar {#using-sling-adapters}

[Sling](https://sling.apache.org) erbjuder [Adaptermönster](https://sling.apache.org/documentation/the-sling-engine/adapters.html) att enkelt översätta objekt som implementerar [Adaptiv](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) gränssnitt. Det här gränssnittet innehåller en allmän [customiTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) metod som översätter objektet till den klasstyp som skickas som argument.

Om du till exempel vill översätta ett Resource-objekt till motsvarande Node-objekt kan du bara göra följande:

```java
Node node = resource.adaptTo(Node.class);
```

## Användningsexempel {#use-cases}

Det finns följande användningsområden:

* Få implementeringsspecifika objekt.

  En JCR-baserad implementering av den generiska [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) -gränssnittet ger åtkomst till underliggande JCR [`Node`](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html).

* Skapa genvägar för objekt som kräver att interna kontextobjekt skickas.

  Till exempel den JCR-baserade [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) innehåller en referens till begäran [`JCR Session`](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html), som i sin tur behövs för många objekt som arbetar baserat på den begärda sessionen, som [`PageManager`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html) eller [`UserManager`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/security/UserManager.html).

* Genväg till tjänster.

  Ett sällsynt fall - `sling.getService()` är också enkelt.

### Null-returvärde {#null-return-value}

`adaptTo()` Kan returnera null.

Det finns olika orsaker till null-returen, bland annat följande:

* implementeringen saknar stöd för måltypen
* en adapterfabrik som hanterar det här ärendet är inte aktivt (till exempel på grund av att det saknas tjänstreferenser)
* internt villkor misslyckades
* tjänsten är inte tillgänglig

Det är viktigt att du hanterar skiftläget null på ett smidigt sätt. Vid jsp-återgivning kan det vara acceptabelt att jsp misslyckas om det resulterar i en tom del av innehållet.

### Cachelagring {#caching}

För att förbättra prestanda kan implementeringar cachelagra objektet som returneras från en `obj.adaptTo()` ring. Om `obj` är samma, returnerade objekt är samma.

Denna cachelagring utförs för alla `AdapterFactory` baserade fall.

Det finns dock ingen allmän regel - objektet kan vara antingen en ny eller en befintlig instans. Det betyder att du inte kan lita på något av beteendena. Därför är det viktigt, särskilt inom `AdapterFactory`att objekt kan återanvändas i det här scenariot.

### Så här fungerar det {#how-it-works}

Det finns olika sätt att `Adaptable.adaptTo()` kan implementeras:

* själva objektet, implementera själva metoden och mappa till vissa objekt.
* Av en [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html), som kan mappa godtyckliga objekt.

  Objekten måste fortfarande implementera `Adaptable` gränssnitt och måste utöka [`SlingAdaptable`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/adapter/SlingAdaptable.html) (som klarar `adaptTo` till en central adapterhanterare).

  Den här metoden tillåter att kopplingar till `adaptTo` mekanism för befintliga klasser, som `Resource`.

* En kombination av båda.

I det första fallet kan Java™-dokumenten ange vad `adaptTo-targets` är möjliga. För vissa underklasser, t.ex. JCR-baserade resurser, går det ofta inte att använda den här programsatsen. I det senare fallet ska `AdapterFactory` är vanligtvis en del av de privata klasserna i ett paket och därför inte exponeras i ett klient-API, och inte heller listas i Java™-dokument. Teoretiskt sett är det möjligt att komma åt alla `AdapterFactory` implementeringar från [OSGi](/help/implementing/deploying/configuring-osgi.md) runtime-modulen för tjänster och se hur deras&quot;adaptable&quot;-konfigurationer (källor och mål) ser ut, men inte för att mappa dem till varandra. I slutändan beror det på den interna logiken, som måste dokumenteras. Denna referens.

## Referens {#reference}

### Sling {#sling}

[**Resurs**](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) anpassar sig till:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nod</a></td>
   <td>Om det är en JCR-nodbaserad resurs eller en JCR-egenskap refererar en nod</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">Egenskap</a></td>
   <td>Om det är en JCR-egenskapsbaserad resurs</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">Objekt</a></td>
   <td>Om det är en JCR-baserad resurs (nod eller egenskap)</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Map.html">Karta</a></td>
   <td>Returnerar en karta över egenskaperna, om det är en JCR-nodbaserad resurs (eller annan resurs som stöder värdekartor)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>Returnerar en användbar karta över egenskaperna, om det är en JCR-nodbaserad resurs (eller annan resurs som stöder värdekartor). Kan också uppnås (enklare) genom att använda<br /> <code><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ResourceUtil.html">ResourceUtil.getValueMap(Resource)</a></code> (hanterar gemener och så vidare)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">ArvValueMap</a></td>
   <td>Utökning av <a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> som gör det möjligt att ta hänsyn till resurshierarkin när du söker efter egenskaper</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModiitableValueMap</a></td>
   <td>En förlängning av <a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>som gör att du kan ändra egenskaper på den noden</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>Returnerar det binära innehållet för en filresurs (om det är en JCR-nodbaserad resurs och nodtypen är <code>nt:file</code> eller <code>nt:resource</code>; om det är en paketresurs, filinnehåll, om det är en filsystemresurs). Eller returnerar data för en binär JCR-egenskapsresurs.</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>Returnerar en URL till resursen (databas-URL för den här noden om det är en JCR-nodbaserad resurs; jar bundle URL om det är en paketresurs, fil-URL om det är en filsystemresurs)</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/File.html">Fil</a></td>
   <td>Om det är en filsystemresurs</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>Om resursen är ett skript (till exempel jsp-fil) som en skriptmotor är registrerad med sling</td>
  </tr>
  <tr>
   <td><a href="https://www.oracle.com/java/technologies/servlet-technology.html">Servlet</a></td>
   <td>Om resursen är ett skript (t.ex. jsp-fil) som en skriptmotor har registrerats med sling, eller om det är en serverresurs</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">Sträng</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Boolean</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Lång</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Double.html">Dubbel</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">Kalender</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Värde</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">Sträng[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Boolean[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Long[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">Kalender[]</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Värde[]</a></td>
   <td>Returnerar värdena om det är en JCR-egenskapsbaserad resurs (och värdet passar)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/LabeledResource.html">EtiketteradResurs</a></td>
   <td>Om det är en JCR-nodbaserad resurs</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/Page.html">Sida</a></td>
   <td>Om det är en JCR-nodbaserad resurs och noden är en <code>cq:Page</code> (eller <code>cq:PseudoPage</code>)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/components/Component.html">Komponent</a></td>
   <td>Om det är en <code>cq:Component</code> nodresurs</td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/designer/Design.html">Design</a></td>
   <td>Om det är en designnod (<code>cq:Page</code>)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/Template.html">Mall</a></td>
   <td>Om det är en <code>cq:Template</code> nodresurs</td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">Blueprint</a></td>
   <td>Om det är en <code>cq:Template</code> nodresurs</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/dam/api/Asset.html">Tillgång</a></td>
   <td>Om det är en dam:Asset-nodresurs</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/dam/api/Rendition.html">Återgivning</a></td>
   <td>Om det är en dam:Asset-rendering (not:file under renderingsmappen för en dam:Assert)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/Tag.html">Tagg</a></td>
   <td>Om det är en <code>cq:Tag</code> nodresurs</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>Baserat på JCR-sessionen om det är en JCR-baserad resurs och användaren har behörighet att komma åt UserManager</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Auktoriserbar</a></td>
   <td>Authorizable är det gemensamma basgränssnittet för användare och grupper</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/User.html">Användare</a></td>
   <td>Användaren är en särskild auktoriseringsfunktion som kan autentiseras och personifieras</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/SimpleSearch.html">SimpleSearch</a></td>
   <td>Söker nedanför resursen (eller använder setSearchIn()) om det är en JCR-baserad resurs</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>Arbetsflödesstatus för den angivna sidans/arbetsflödets nyttolastnod</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/ReplicationStatus.html">ReplicationStatus</a></td>
   <td>Replikeringsstatus för den angivna resursen eller dess jcr:innehållsundernod (markerad först)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/connector/ConnectorResource.html">KopplingResurs</a></td>
   <td>Returnerar en anpassad anslutningsresurs för vissa typer, om det är en JCR-nodbaserad resurs</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/contentsync/config/package-summary.html">Konfig</a></td>
   <td>Om det är en <code>cq:ContentSyncConfig</code> nodresurs</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>Om den är under en <code>cq:ContentSyncConfig</code> nodresurs</td>
  </tr>
 </tbody>
</table>

[**ResursResolver**](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ResourceResolver.html) anpassar sig till:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">Session</a></td>
   <td>JCR-sessionen för begäran, om det är en JCR-baserad resurslösare (standard)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>Baserat på JCR-sessionen, om det är en JCR-baserad resurslösare</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>Baserat på JCR-sessionen, om det är en JCR-baserad resurslösare</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>UserManager ger åtkomst till och möjlighet att underhålla auktoriserbara objekt, det vill säga användare och grupper. UserManager är bundet till en viss session
   </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Auktoriserbar</a> </td>
   <td>Aktuell användare</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/User.html">Användare</a><br /> </td>
   <td>Aktuell användare</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html">Externalizer</a></td>
   <td>För att externalisera absoluta URL:er, även utan objektet request<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest**](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) anpassar sig till:

Inga mål ännu, men implementerar Adaptable och kan användas som källa i en anpassad AdapterFactory.

[**SlingHttpServletResponse**](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) anpassar sig till:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>Om det är ett svarsalternativ</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[Sida](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/Page.html)** anpassar sig till:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html">Resurs</a><br /> </td>
   <td>Sidans resurs.</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/LabeledResource.html">EtiketteradResurs</a></td>
   <td>Etiketterad resurs (== this).</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nod</a></td>
   <td>Sidans nod.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Allt som sidans resurs kan anpassas till.</td>
  </tr>
 </tbody>
</table>

**[Komponent](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/components/Component.html)** anpassar sig till:

| [Resurs](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) | Komponentens resurs. |
|---|---|
| [EtiketteradResurs](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/LabeledResource.html) | Etiketterad resurs (== this). |
| [Nod](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Komponentens nod. |
| ... | Allt som komponentens resurs kan anpassas till. |

**[Mall](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/Template.html)** anpassar sig till:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html">Resurs</a><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>Mallens resurs.</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/LabeledResource.html">EtiketteradResurs</a></td>
   <td>Etiketterad resurs (== this).</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nod</a></td>
   <td>Nod för den här mallen.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Allt som mallens resurs kan anpassas till.</td>
  </tr>
 </tbody>
</table>

#### Dokumentskydd {#security}

**Auktoriserbar**, **Användare** och **Grupp** anpassa till:

| [Nod](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Returnerar hemnoden för användaren/gruppen. |
|---|---|
| [ReplicationStatus](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/ReplicationStatus.html) | Returnerar replikeringsstatusen för användarens/gruppens hemnod. |

#### DAM {#dam}

**Tillgång** anpassar sig till:

| [Resurs](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) | Resurs för tillgången. |
|---|---|
| [Nod](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nod för resursen. |
| ... | Allt som resursen kan anpassas till. |

#### Taggar {#tagging}

**Tagg** anpassar sig till:

| [Resurs](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) | Resurs för taggen. |
|---|---|
| [Nod](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Taggens nod. |
| ... | Allt som taggens resurs kan anpassas till. |

#### Övriga {#other}

Dessutom ger Sling/JCR/OCM [`AdapterFactory`](https://sling.apache.org/documentation/the-sling-engine/adapters.html) för anpassad OCM ([Mappning av objektinnehåll](https://jackrabbit.apache.org/jcr/object-content-mapping.html)).
