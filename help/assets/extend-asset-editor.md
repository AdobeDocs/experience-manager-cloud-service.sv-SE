---
title: Utöka redigeringsprogram för resurser
description: Lär dig hur du utökar funktionerna i redigeringsverktyget för resurser med hjälp av anpassade komponenter.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c978be66702b7f032f78a1509f2a11315d1ed89f
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 13%

---


# Utöka resursredigeraren {#extending-asset-editor}

Resursredigeraren är den sida som öppnas när användaren klickar på en resurs som hittas via Resursresurs, så att användaren kan redigera sådana aspekter av resursen som metadata, miniatyrbilder, rubrik och taggar.

Konfiguration av redigeraren med de fördefinierade redigeringskomponenterna beskrivs i [Skapa och konfigurera en resursredigeringssida](https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-finder-editor.html).

Förutom att använda befintliga redigeringskomponenter kan utvecklare av Adobe Experience Manager (AEM) även skapa egna komponenter.

## Skapa en resursredigeringsmall {#creating-an-asset-editor-template}

Följande exempelsidor finns i geometrixx:

* Exempelsida för Geometrixx: `/content/geometrixx/en/press/asseteditor.html`
* Exempelmall: `/apps/geometrixx/templates/asseteditor`
* Exempel på sidkomponent: `/apps/geometrixx/components/asseteditor`

### Konfigurerar Clientlib {#configuring-clientlib}

AEM Resurskomponenter använder ett tillägg till klienten för WCM-redigering. Klientlibs läses vanligtvis in i `init.jsp`.

Jämfört med standardinläsningen av klientlib (i kärnan `init.jsp`) måste en AEM Assets-mall ha följande:

* Mallen måste innehålla `cq.dam.edit` clientlib (i stället för `cq.wcm.edit`).

* Clientlib måste också inkluderas i inaktiverat WCM-läge (t.ex. läsas in vid **publicering**) för att kunna återge predikat, åtgärder och linser.

I de flesta fall bör kopieringen av det befintliga exemplet `init.jsp` (`/apps/geometrixx/components/asseteditor/init.jsp`) uppfylla dessa behov.

### Konfigurera JS-åtgärder {#configuring-js-actions}

Vissa av AEM Assets-komponenterna kräver JS-funktioner som definieras i `component.js`. Kopiera den här filen till komponentkatalogen och länka den.

```javascript
<script type="text/javascript" src="<%= component.getPath() %>/component.js"></script>
```

Exemplet läser in den här javascript-källan i `head.jsp`(`/apps/geometrixx/components/asseteditor/head.jsp`).

### Ytterligare formatmallar {#additional-style-sheets}

Vissa av komponenterna i AEM Assets använder AEM-widgetbiblioteket. För att kunna återges korrekt i innehållskontexten måste ytterligare en formatmall läsas in. Kodåtgärdskomponenten kräver en till.

```css
<link href="/etc/designs/geometrixx/ui.widgets.css" rel="stylesheet" type="text/css">
```

### Geometrixx-formatmall {#geometrixx-style-sheet}

Komponenterna för exempelsidan kräver att alla väljare börjar med `.asseteditor` av `static.css` (`/etc/designs/geometrixx/static.css`). Bästa praxis: Kopiera alla `.asseteditor` väljare till formatmallen och justera reglerna efter behov.

### FormChooser: Justeringar för resurser som slutligen läses in {#formchooser-adjustments-for-eventually-loaded-resources}

Resursredigeraren använder formulärväljaren, som gör att du kan redigera resurser - i det här fallet resurser - på samma formulärsida genom att lägga till en formulärväljare och formulärsökvägen till resursens URL.

Till exempel:

* Oformaterad formulärsida: [http://localhost:4502/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/geometrixx/en/press/asseteditor.html)
* Resursen har lästs in på formulärsidan: [http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html)

Exempelhandtagen i `head.jsp` (`/apps/geometrixx/components/asseteditor/head.jsp`) gör följande:

* De identifierar om en resurs har lästs in eller om det rena formuläret måste visas.
* Om en resurs läses in kan de inaktivera WCM-läget som parsys bara redigeras på en vanlig formulärsida.
* Om en resurs läses in använder de dess titel i stället för den på formulärsidan.

```javascript
 List<Resource> resources = FormsHelper.getFormEditResources(slingRequest);
    if (resources != null) {
        if (resources.size() == 1) {
            // single resource
            FormsHelper.setFormLoadResource(slingRequest, resources.get(0));
        } else if (resources.size() > 1) {
            // multiple resources
            // not supported by CQ 5.3
        }
    }
    Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
    String title;
    if (loadResource != null) {
        // an asset is loaded: disable WCM
        WCMMode.DISABLED.toRequest(request);

        String path = loadResource.getPath();
        Asset asset = loadResource.adaptTo(Asset.class);
        try {
            // it might happen that the adobe xmp lib creates an array
            Object titleObj = asset.getMetadata("dc:title");
            if (titleObj instanceof Object[]) {
                Object[] titleArray = (Object[]) titleObj;
                title = (titleArray.length > 0) ? titleArray[0].toString() : "";
            } else {
                title = titleObj.toString();
            }
        }
        catch (NullPointerException e) {
            title = path.substring(path.lastIndexOf("/") + 1);
        }
    }
    else {
        title = currentPage.getTitle() == null ? currentPage.getName() : currentPage.getTitle();
    }
```

Använd den föregående titeluppsättningen (antingen resurs eller sidrubrik) i HTML-delen:

```html
<title><%= title %></title>
```

## Skapa en enkel formulärfältskomponent {#creating-a-simple-form-field-component}

I det här exemplet beskrivs hur du skapar en komponent som visar och visar metadata för en inläst resurs.

1. Skapa till exempel en komponentmapp i projektkatalogen `/apps/geometrixx/components/samplemeta`.
1. Lägg till `content.xml` med följande kodutdrag:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Dimension"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Asset Editor"/>
   ```

1. Lägg till `samplemeta.jsp` med följande kodutdrag:

   ```javascript
   <%--
   
     Sample metadata field comopnent
   
   --%><%@ page import="com.day.cq.dam.api.Asset,
                    java.security.AccessControlException" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       String value = "";
       String name = "dam:sampleMetadata";
       boolean readOnly = false;
   
       // If the form page is requested for an asset loadResource will be the asset.
       Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
   
       if (loadResource != null) {
   
           // Determine if the loaded asset is read only.
           Session session = slingRequest.getResourceResolver().adaptTo(Session.class);
           try {
               session.checkPermission(loadResource.getPath(), "set_property");
               readOnly = false;
           }
           catch (AccessControlException ace) {
               // checkPermission throws exception if asset is read only
               readOnly = true;
           }
           catch (RepositoryException re) {}
   
           // Get the value of the metadata.
           Asset asset = loadResource.adaptTo(Asset.class);
           try {
               value = asset.getMetadata(name).toString();
           }
           catch (NullPointerException npe) {
               // no metadata dc:description available
           }
       }
   %>
   <div class="form_row">
       <div class="form_leftcol">
           <div class="form_leftcollabel">Sample Metadata</div>
       </div>
       <div class="form_rightcol">
           <%
           if (readOnly) {
               %><c:out value="<%= value %>"/><%
           }
           else {
               %><input class="text" type="text" name="./jcr:content/metadata/<%= name %>" value="<c:out value="<%= value %>" />"><%
           }%>
       </div>
   </div>
   ```

1. Om du vill göra komponenten tillgänglig måste du kunna redigera den. To make a component editable, in CRXDE Lite, add a node `cq:editConfig` of primary type `cq:EditConfig`. Du kan ta bort stycken genom att lägga till en egenskap med flera värden `cq:actions` med ett enda värde på `DELETE`.

1. Navigera till webbläsaren och på exempelsidan (till exempel `asseteditor.html`) växla till designläge och aktivera den nya komponenten för styckesystemet.

1. I **redigeringsläget** är den nya komponenten (till exempel **Exempelmetadata**) nu tillgänglig i assistenten (finns i gruppen **Resursredigeraren**). Infoga komponenten. För att metadata ska kunna lagras måste de läggas till i metadataformuläret.

## Ändra metadataalternativ {#modifying-metadata-options}

Du kan ändra de namnutrymmen som finns i [metadataformuläret](https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-finder-editor.html).

Tillgängliga metadata definieras i `/libs/dam/options/metadata`:

* Den första nivån i den här katalogen innehåller namnutrymmena.
* Objekten i varje namnutrymme representerar metadata, till exempel resultat i ett lokalt delsobjekt.
* Metadatainnehållet innehåller information om typen och alternativen för flera värden.

Alternativen kan skrivas över i `/apps/dam/options/metadata`:

1. Kopiera katalogen från `/libs` till `/apps`.

1. Ta bort, ändra eller lägga till objekt.

>[!NOTE]
>
>Om du lägger till nya namnutrymmen måste de registreras i din databas/CRX. Om du inte skickar metadataformuläret uppstår ett fel.
