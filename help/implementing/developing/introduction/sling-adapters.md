---
title: Använda Sling-adaptrar
description: Sling erbjuder ett adaptermönster för att enkelt översätta objekt som implementerar gränssnittet Adaptable
exl-id: 8ffe3bbd-01fe-44c2-bf60-7a4d25a6ba2b
source-git-commit: a446efacb91f1a620d227b9413761dd857089c96
workflow-type: tm+mt
source-wordcount: '2232'
ht-degree: 0%

---

# Använda Sling-adaptrar {#using-sling-adapters}

[](https://sling.apache.org) Slingger erbjuder ett  [adaptermönster ](https://sling.apache.org/site/adapters.html) för att enkelt översätta objekt som implementerar det  [](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) adapterbara gränssnittet. Det här gränssnittet innehåller en allmän [customiTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29)-metod som översätter objektet till den klasstyp som skickas som argument.

Om du till exempel vill översätta ett Resource-objekt till motsvarande Node-objekt kan du bara göra följande:

```java
Node node = resource.adaptTo(Node.class);
```

## Använd fall {#use-cases}

Det finns följande användningsområden:

* Få implementeringsspecifika objekt.

   En JCR-baserad implementering av det generiska [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html)-gränssnittet ger till exempel åtkomst till den underliggande JCR [`Node`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html).

* Skapa genvägar för objekt som kräver att interna kontextobjekt skickas.

   Den JCR-baserade [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) innehåller till exempel en referens till förfrågningens [`JCR Session`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html), som i sin tur behövs för många objekt som ska fungera baserat på den begärandesessionen, till exempel [`PageManager`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/PageManager.html) eller [`UserManager`](https://experienceleague.adobe.com/docs/experience-manager-cloud-service-javadoc/com/day/cq/security/UserManager.html).

* Genväg till tjänster.

   Ett sällsynt fall - `sling.getService()` är också enkelt.

### Null-returvärde {#null-return-value}

`adaptTo()` kan returnera null.

Det finns olika orsaker till detta, bland annat:

* implementeringen saknar stöd för måltypen
* en adapterfabrik som hanterar det här ärendet är inte aktivt (t.ex. på grund av saknad tjänstreferens)
* internt villkor misslyckades
* tjänsten är inte tillgänglig

Det är viktigt att du hanterar skiftläget null på ett smidigt sätt. Vid jsp-återgivning kan det vara acceptabelt att jsp misslyckas om det resulterar i en tom del av innehållet.

### Cachelagring {#caching}

För att förbättra prestanda kan implementeringar cachelagra objektet som returneras från ett `obj.adaptTo()`-anrop. Om `obj` är samma är det returnerade objektet detsamma.

Denna cachelagring utförs för alla `AdapterFactory`-baserade fall.

Det finns dock ingen allmän regel - objektet kan vara antingen en ny eller en befintlig instans. Det innebär att du inte kan förlita dig på något av beteendena. Därför är det viktigt, särskilt i `AdapterFactory`, att objekt kan återanvändas i det här scenariot.

### Så här fungerar det {#how-it-works}

Det finns olika sätt att implementera `Adaptable.adaptTo()`:

* själva objektet, implementera själva metoden och mappa till vissa objekt.
* Med ett [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html), som kan mappa godtyckliga objekt.

   Objekten måste fortfarande implementera gränssnittet `Adaptable` och måste utöka [`SlingAdaptable`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/adapter/SlingAdaptable.html) (som skickar anropet `adaptTo` till en central adapterhanterare).

   Detta tillåter kopplingar till `adaptTo`-mekanismen för befintliga klasser, som `Resource`.

* En kombination av båda.

I det första fallet kan javadocs ange vad `adaptTo-targets` är möjligt. Detta är dock ofta inte möjligt för vissa underklasser, t.ex. JCR-baserade resurser. I det senare fallet är implementeringar av `AdapterFactory` vanligtvis en del av de privata klasserna i ett paket och exponeras därför inte i ett klient-API och inte heller listas i javadocs. Teoretiskt sett skulle det vara möjligt att komma åt alla `AdapterFactory`-implementeringar från [OSGi](/help/implementing/deploying/configuring-osgi.md)-tjänstmiljön och titta på deras&quot;adaptable&quot; (sources and target)-konfigurationer, men inte att mappa dem till varandra. I slutändan beror detta på den interna logiken, som måste dokumenteras. Denna referens.

## Referens {#reference}

### Sling {#sling}

[**Resurserna**](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/Resource.html) anpassas till:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nod</a></td>
   <td>Om detta är en JCR-nodbaserad resurs eller en JCR-egenskap som refererar till en nod.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">Egenskap</a></td>
   <td>Om detta är en JCR-egenskapsbaserad resurs.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">Objekt</a></td>
   <td>Om detta är en JCR-baserad resurs (nod eller egenskap).</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api//java/util/Map.html">Karta</a></td>
   <td>Returnerar en karta över egenskaperna, om detta är en JCR-nodbaserad resurs (eller annan resurs som stöder värdekartor).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>Returnerar en användbar karta över egenskaperna, om detta är en JCR-nodbaserad resurs (eller annan resurs som stöder värdekartor). Kan också uppnås (enklare) med <br /> <code><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code> (hanterar null-skiftläge etc.).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">ArvValueMap</a></td>
   <td>Utökning av <a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> som gör att hierarkin med resurser kan beaktas när egenskaper söks.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModiitableValueMap</a></td>
   <td>Ett tillägg till <a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> som gör att du kan ändra egenskaper på den noden.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>Returnerar det binära innehållet i en filresurs (om detta är en JCR-nodbaserad resurs och nodtypen är <code>nt:file</code> eller <code>nt:resource</code>; om detta är en paketresurs, filinnehåll om det är en filsystemresurs) eller data för en binär JCR-egenskapsresurs.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/net/URL.html">Webbadress</a></td>
   <td>Returnerar en URL till resursen (databas-URL för den här noden om detta är en JCR-nodbaserad resurs; jar bundle URL om detta är en paketresurs, fil-URL om detta är en filsystemresurs).</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/File.html">Arkiv</a></td>
   <td>Om detta är en filsystemresurs.</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>Om den här resursen är ett skript (t.ex. jsp-fil) för vilket en skriptmotor är registrerad med sling.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/products/servlet/2.2/javadoc/javax/servlet/Servlet.html">Servlet</a></td>
   <td>Om den här resursen är ett skript (t.ex. jsp-fil) för vilket en skriptmotor är registrerad med sling eller om det här är en serverresurs.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Double.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html"></a><br /> <a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">StringBooleanLongDoubleCalendarValueString[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">Boolean[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">Long[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">Calendar[]</a><br /> <a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Value[]</a></td>
   <td>Returnerar värdet/värdena om detta är en JCR-egenskapsbaserad resurs (och värdet passar).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/LabeledResource.html">EtiketteradResurs</a></td>
   <td>Om detta är en JCR-nodbaserad resurs.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/Page.html">Sidan</a></td>
   <td>Om detta är en JCR-nodbaserad resurs och noden är en <code>cq:Page</code> (eller <code>cq:PseudoPage</code>).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/components/Component.html">Komponent</a></td>
   <td>Om detta är en <code>cq:Component</code>-nodresurs.</td>
  </tr>  
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/designer/Design.html">Design</a></td>
   <td>Om detta är en designnod (<code>cq:Page</code>).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/Template.html">Mall</a></td>
   <td>Om detta är en <code>cq:Template</code>-nodresurs.</td>
  </tr>  
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/msm/api/Blueprint.html">Blueprint</a></td>
   <td>Om detta är en <code>cq:Template</code>-nodresurs.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/dam/api/Asset.html">Tillgång</a></td>
   <td>Om detta är en resurs för dam:Asset-noden.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/dam/api/Rendition.html">Återgivning</a></td>
   <td>Om det här är en dam:Asset-rendering (not:file under renderingsmappen för en dam:Assert)</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/tagging/Tag.html">Tagg</a></td>
   <td>Om detta är en <code>cq:Tag</code>-nodresurs.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>Baserat på JCR-sessionen om detta är en JCR-baserad resurs och användaren har behörighet att komma åt UserManager.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Auktoriserbar</a></td>
   <td>Authorizable är det gemensamma grundgränssnittet för Användare och Grupp.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/jackrabbit/api/security/user/User.html">Användare</a></td>
   <td>Användaren är en särskild auktoriseringsfunktion som kan autentiseras och personifieras.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/SimpleSearch.html">SimpleSearch</a></td>
   <td>Söker under resursen (eller använder setSearchIn()) om detta är en JCR-baserad resurs.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>Arbetsflödesstatus för den angivna sidans/arbetsflödets nyttolastnod.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/replication/ReplicationStatus.html">ReplicationStatus</a></td>
   <td>Replikeringsstatus för den angivna resursen eller dess jcr:content-undernod (markerad först).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/connector/ConnectorResource.html">KopplingResurs</a></td>
   <td>Returnerar en anpassad anslutningsresurs för vissa typer, om detta är en JCR-nodbaserad resurs.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/contentsync/config/package-summary.html">Konfig</a></td>
   <td>Om detta är en <code>cq:ContentSyncConfig</code>-nodresurs.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>Om detta är under en <code>cq:ContentSyncConfig</code>-nodresurs.</td>
  </tr>
 </tbody>
</table>

[**Resurslösningar**](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/ResourceResolver.html) anpassas till:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">Session</a></td>
   <td>JCR-sessionen för begäran, om det här är en JCR-baserad resurslösare (standard).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>Baserat på JCR-sessionen, om detta är en JCR-baserad resurslösare.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>Baserat på JCR-sessionen, om detta är en JCR-baserad resurslösare.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>UserManager ger åtkomst till och möjlighet att underhålla auktoriserbara objekt, dvs. användare och grupper. UserManager är bundet till en viss session.
   </td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Auktoriserbar</a> </td>
   <td>Den aktuella användaren.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/jackrabbit/api/security/user/User.html">Användare</a><br /> </td>
   <td>Den aktuella användaren.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/Externalizer.html">Externalizer</a></td>
   <td>För extern generering av absoluta URL:er, även med det begärda objektet.<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequestadapts**](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/SlingHttpServletRequest.html) anpassas till:

Inga mål ännu, men implementerar Adaptable och kan användas som källa i en anpassad AdapterFactory.

[**SlingHttpServletResponseanpassas**](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/SlingHttpServletResponse.html) till:

<table>
 <tbody>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>Om det här är ett svarsalternativ.</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[Sidan ](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/Page.html)** anpassas till:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/Resource.html">Resurs</a><br /> </td>
   <td>Sidans resurs.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/LabeledResource.html">EtiketteradResurs</a></td>
   <td>Etiketterad resurs (== this).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nod</a></td>
   <td>Sidans nod.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Allt som sidans resurs kan anpassas till.</td>
  </tr>
 </tbody>
</table>

**[Komponenter ](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/components/Component.html)** anpassas till:

| [Resurs](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/Resource.html) | Komponentens resurs. |
|---|---|
| [EtiketteradResurs](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/LabeledResource.html) | Etiketterad resurs (== this). |
| [Nod](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Komponentens nod. |
| ... | Allt som komponentens resurs kan anpassas till. |

**[Mallar ](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/Template.html)** anpassas till:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/Resource.html">Resurs</a><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>Mallens resurs.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/LabeledResource.html">EtiketteradResurs</a></td>
   <td>Etiketterad resurs (== this).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nod</a></td>
   <td>Nod för den här mallen.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Allt som mallens resurs kan anpassas till.</td>
  </tr>
 </tbody>
</table>

#### Dokumentskydd {#security}

**Authorizable**,  **** Userand  **** Groupes customize to:

| [Nod](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Returnerar hemnoden för användaren/gruppen. |
|---|---|
| [ReplicationStatus](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/replication/ReplicationStatus.html) | Returnerar replikeringsstatusen för användarens/gruppens hemnod. |

#### DAM {#dam}

**Tillgångar** anpassas till:

| [Resurs](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/Resource.html) | Resurs för tillgången. |
|---|---|
| [Nod](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nod för resursen. |
| ... | Allt som resursen kan anpassas till. |

#### Taggar {#tagging}

**Taggar** anpassas till:

| [Resurs](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/Resource.html) | Resurs för taggen. |
|---|---|
| [Nod](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Taggens nod. |
| ... | Allt som taggens resurs kan anpassas till. |

#### Annan {#other}

Dessutom innehåller Sling/JCR/OCM också [`AdapterFactory`](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory) för anpassade OCM-objekt ([Objektinnehållsmappning](https://jackrabbit.apache.org/object-content-mapping.html)).
