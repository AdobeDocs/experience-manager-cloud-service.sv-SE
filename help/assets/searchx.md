---
title: Utöka sökalternativen och funktionerna i Adobe Experience Manager Assets
description: Utöka sökfunktionerna i Assets.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Utöka resurssökning {#extend-assets-search}

Du kan utöka sökfunktionerna i Adobe Experience Manager (AEM) Assets. När allt är klart söker AEM Resurser efter resurser efter strängar.

Sökningen görs via gränssnittet i QueryBuilder så att sökningen kan anpassas med flera predikat. Du kan täcka över standarduppsättningen med predikat i följande katalog: `/apps/dam/content/search/searchpanel/facets`.

Du kan även lägga till ytterligare flikar på AEM Resurser-administratörspanelen.

## Övertäckning {#overlay}

Om du vill täcka över de förkonfigurerade predikaten kopierar du `facets` noden från `/libs/dam/content/search/searchpanel` till `/apps/dam/content/search/searchpanel/` eller anger en annan `facetURL` egenskap i sökpanelens konfiguration (standardvärdet är `/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`).

>[!NOTE]
>
>Som standard finns inte katalogstrukturen under `/apps` och måste skapas. Kontrollera att nodtyperna matchar dem under `/libs`.

### Lägg till tabbar {#add-tabs}

Du kan lägga till fler sökflikar genom att konfigurera dem i AEM Resurser Admin. Så här skapar du ytterligare flikar:

1. Skapa mappstrukturen `/apps/wcm/core/content/damadmin/tabs,`om den inte redan finns, och kopiera `tabs` noden från `/libs/wcm/core/content/damadmin` och klistra in den.
1. Skapa och konfigurera den andra fliken efter behov.

   >[!NOTE]
   >
   >När du skapar en andra `siteadminsearchpanel`ska du se till att ange en `id` egenskap för att förhindra formulärkonflikter.

### Skapa anpassade predikat {#create-custom-predicates}

AEM Resurser innehåller en uppsättning fördefinierade predikat som kan användas för att anpassa en resursdelssida.
<!-- In addition to using pre-existing predicates, AEM developers can also create their own predicates using the [Query Builder API](/help/sites-developing/querybuilder-api.md). -->

Det krävs grundläggande kunskaper om [widgetramverket](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)för att kunna skapa anpassade predikat.

Det bästa sättet är att kopiera ett befintligt predikat och justera det. Exempelpredikaten finns i **/libs/cq/search/components/predikates**.

#### Exempel: Skapa ett enkelt egenskapspredikat {#example-build-a-simple-property-predicate}

Så här skapar du ett egenskapspredikat:

1. Skapa en komponentmapp i projektkatalogen, till exempel **/apps/geometrixx/components/titlepreate**.
1. Lägg till **content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Title Predicate"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. Lägg till `titlepredicate.jsp`.

   ```xml
   <%--
   
     Sample title predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Title</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:title";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // createId adds a counter to the predicate name - useful in case this predicate
           // is inserted multiple times on the same page.
           var id = qb.createId(predicateName);
   
           // Hidden field that defines the property to search for; in our case this
           // is the "dc:title" metadata. The name "property" (or "1_property", "2_property" etc.)
           // indicates the server to use the property predicate
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id,
               "value": propertyName
           });
   
           // The visible text field. The name has to be like the one of the hidden field above
           // plus the ".value" suffix.
           qb.addField({
               "xtype": "textfield",
               "renderTo": elemId,
               "name": id + ".value"
           });
   
           // Depending on the predicate additional parameters allow to configure the
           // predicate. Here we add an operation parameter to create a "like" query.
           // Again note the name set to the id and a suffix.
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id + ".operation",
               "value": "like"
           });
       });
   </script>
   ```

1. Om du vill göra komponenten tillgänglig måste du kunna redigera den. Om du vill göra en komponent redigerbar lägger du i CRXDE till en nod **cq:editConfig** av den primära typen **cq:EditConfig**. Du kan ta bort stycken genom att lägga till en egenskap med flera värden **cq:actions** med ett enda värde på **DELETE**.
1. Navigera till webbläsaren och på exempelsidan (till exempel **press.html**) växla till designläge och aktivera den nya komponenten för det prediktiva styckesystemet (till exempel **vänster**).

1. I **redigeringsläget** är den nya komponenten nu tillgänglig i sidosparken (finns i **sökgruppen** ). Infoga komponenten i kolumnen **Predikatorer** och skriv ett sökord, till exempel **Diamant** , och klicka på förstoringsglaset för att starta sökningen.

   >[!NOTE]
   >
   >När du söker måste du skriva in ordet exakt, inklusive rätt skiftläge.

#### Exempel: Skapa ett enkelt grupppredikat {#example-build-a-simple-group-predicate}

Så här skapar du ett grupppredikat:

1. Skapa en komponentmapp i projektkatalogen, till exempel **/apps/geometrixx/components/picspredicate.**
1. Lägg till **content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. Lägg till **titlepreate.jsp**:

   ```xml
   <%--
   
     Sample group predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page.
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Image Formats</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:format";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // Create a unique group ID; will return e.g. "1_group".
           var groupId = qb.createGroupId();
   
           // Hidden field that defines the property to search for  - in our case "dc:format" -
           // and declares the group of predicates. "property" in the name ("1_group.property")
           // indicates to the server to use the "property predicate"
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": "<%= elemId %>",
               "name": groupId + "." + predicateName, // 1_group.property
               "value": propertyName
           });
   
           // Declare to combine the multiple values using OR.
           qb.add(new CQ.Ext.form.Hidden({
               "name": groupId + ".p.or",  // 1_group.p.or
               "value": "true"
           }));
   
           // The options
           var options = [
               { "label":"JPEG", "value":"image/jpeg"},
               { "label":"PNG",  "value":"image/png" },
               { "label":"GIF",  "value":"image/gif" }
           ];
   
           // Build a checkbox for each option.
           for (var i = 0; i < options.length; i++) {
               qb.addField({
                   "xtype": "checkbox",
                   "renderTo": "<%= elemId %>",
                   // 1_group.property.0_value, 1_group.property.1_value etc.
                   "name": groupId + "." +  predicateName + "." + i + "_value",
                   "inputValue": options[i].value,
                   "boxLabel": options[i].label,
                   "listeners": {
                       "check": function() {
                           // Submit the search form when checking/unchecking a checkbox.
                           qb.submit();
                       }
                   }
               });
           }
       });
   ```

1. Om du vill göra komponenten tillgänglig måste du kunna redigera den. Om du vill göra en komponent redigerbar lägger du i CRXDE till en nod **cq:editConfig** av den primära typen **cq:EditConfig**. Du kan ta bort stycken genom att lägga till en egenskap med flera värden **cq:actions** med ett enda värde på **DELETE**.
1. Navigera till webbläsaren och på exempelsidan (till exempel **press.html**) växla till designläge och aktivera den nya komponenten för det prediktiva styckesystemet (till exempel **vänster**).
1. I **redigeringsläget** är den nya komponenten nu tillgänglig i sidosparken (finns i **sökgruppen** ). Infoga komponenten i kolumnen **Predicates** .

### Installerade prediktiva widgetar {#installed-predicate-widgets}

Följande predikat är tillgängliga som förkonfigurerade ExtJS-widgetar.

#### FulltextPredicate {#fulltextpredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Egenskap<br /> </strong></td>
   <td><strong>Typ</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>predikateName</td>
   <td>Sträng</td>
   <td>Predikatets namn. Standardvärdet är fulltext</td>
  </tr>
  <tr>
   <td>searchCallback</td>
   <td>Funktion</td>
   <td>Återanrop för att utlösa sökning vid händelse 'keyup'. Standard är CQ.wcm.SiteAdmin.doSearch</td>
  </tr>
 </tbody>
</table>

#### PropertyPredicate {#propertypredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Egenskap<br /> </strong></td>
   <td><strong>Typ</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>predikateName</td>
   <td>Sträng</td>
   <td>Predikatets namn. Standardvärdet är 'property'</td>
  </tr>
  <tr>
   <td>propertyName</td>
   <td>Sträng </td>
   <td>Namn på JCR-egenskapen. Standard är jcr:title</td>
  </tr>
  <tr>
   <td>defaultValue<br /> </td>
   <td>Sträng<br /> </td>
   <td>Förfyllt standardvärde.<br /> </td>
  </tr>
 </tbody>
</table>

#### PathPredicate {#pathpredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Egenskap<br /> </strong></td>
   <td><strong>Typ</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>predikateName</td>
   <td>Sträng</td>
   <td>Predikatets namn. Standardvärdet är 'path'</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>Sträng </td>
   <td>Predikatets rotsökväg. Standard är /content/dam</td>
  </tr>
  <tr>
   <td>pathFieldPredicateName</td>
   <td>Sträng</td>
   <td>Standard till 'mapp'</td>
  </tr>
  <tr>
   <td>showFlatOption</td>
   <td>Boolesk</td>
   <td>Flagga som visar kryssrutan Sök i undermappar. Standardvärdet är true.</td>
  </tr>
 </tbody>
</table>

#### DatePredicate {#datepredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Egenskap<br /> </strong></td>
   <td><strong>Typ</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>predikateName</td>
   <td>Sträng</td>
   <td>Predikatets namn. Standardvärdet är daterange</td>
  </tr>
  <tr>
   <td>egenskapsnamn</td>
   <td>Sträng</td>
   <td>Namn på JCR-egenskapen. Standard är jcr:content/jcr:lastModified</td>
  </tr>
  <tr>
   <td>defaultValue </td>
   <td>Sträng </td>
   <td>Förfyllt standardvärde </td>
  </tr>
 </tbody>
</table>

#### OptionsPredicate {#optionspredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Egenskap<br /> </strong></td>
   <td><strong>Typ</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>title </td>
   <td>Sträng </td>
   <td>Lägger till ytterligare en rubrik </td>
  </tr>
  <tr>
   <td>predikateName</td>
   <td>Sträng</td>
   <td>Predikatets namn. Standardvärdet är daterange</td>
  </tr>
  <tr>
   <td>egenskapsnamn</td>
   <td>Sträng</td>
   <td>Namn på JCR-egenskapen. Som standard 'jcr:content/metadata/cq:tags'</td>
  </tr>
  <tr>
   <td>komprimera</td>
   <td>Sträng</td>
   <td>Komprimera nivå. Standardvärdet är 'level1'</td>
  </tr>
  <tr>
   <td>triggerSearch</td>
   <td>Boolesk </td>
   <td>Flagga för att utlösa sökning vid kontroll. Standardvärdet är false</td>
  </tr>
  <tr>
   <td>searchCallback</td>
   <td>Funktion</td>
   <td>Återanrop för att utlösa sökning. Standardvärdet är CQ.wcm.SiteAdmin.doSearch</td>
  </tr>
  <tr>
   <td>searchTimeoutTime</td>
   <td> Nummer</td>
   <td>Timeout innan searchCallback aktiveras. Standardvärdet är 800 ms</td>
  </tr>
 </tbody>
</table>
