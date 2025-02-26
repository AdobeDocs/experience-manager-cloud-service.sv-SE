---
title: Publicera AEM Forms för Edge Delivery Services.
description: Publicera dina Edge Delivery Services-formulär snabbt och smidigt.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: 0c6f024594e1b1fd98174914d2c0714dffecb241
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Publicera ditt adaptiva formulär på Edge Delivery Services

<span class="preview"> Den här funktionen är tillgänglig via programmet för tidig åtkomst. Om du vill begära åtkomst skickar du ett e-postmeddelande från din officiella adress till <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> med ditt GitHub-organisationsnamn och databasnamn. Om databas-URL:en till exempel är https://github.com/adobe/abc är organisationsnamnet adobe och databasnamnet abc.</span>


När formuläret är klart och klart kan du publicera det för att göra det tillgängligt för dina kunder för datainsamling och inlämning. Publiceringen säkerställer att formuläret är tillgängligt i Edge Delivery, så att användarna kan interagera med det smidigt. Detta gör att kunderna kan fylla i och skicka in formuläret i realtid, vilket ger effektiv datainhämtning och smidig behandling.

## Förutsättningar

* Ett formulär som skapats med **Edge Delivery Services-mallen (EDS)**. [Läs mer](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md) om hur du skapar ett EDS-baserat formulär.

## Publicera formuläret

Du kan publicera **EDS-baserade adaptiva formulär** till Edge Delivery genom att följa dessa steg:

<!--1. Select the **Adaptive Form** that you want to publish and click the **Edit** ![edit icon](/help/forms/assets/edit.svg) icon.
   ![Select EDS-Based Form](/help/forms/assets/select-eds-based-form.png)-->

1. Öppna ditt adaptiva formulär i redigeraren och klicka på ikonen **Publicera** i den övre listen.
   ![Klicka på Publicera](/help/forms/assets/publish-icon-eds-form.png)

1. När du klickar på **Publicera** visas en skärm eller ett popup-fönster som visar publiceringsresurserna, inklusive formulärets rubrik. I det här exemplet används mallen **Wknd_Form**.
   ![Vid klickning på Publicera](/help/forms/assets/on-click-publish.png)

1. Klicka på **Publicera** igen så visas ett bekräftelsemeddelande som anger att formuläret nu har publicerats.
   ![Publiceringen lyckades](/help/forms/assets/publish-success.png)

1. Om du vill kontrollera formulärets publiceringsstatus klickar du på **Publicera** igen.
   ![Publiceringsstatus](/help/forms/assets/publish-status.png)

1. Om du vill **avpublicera** ett formulär öppnar du det i redigeraren, klickar på menyn med tre punkter i det övre högra hörnet och klickar på **Avpublicera**.
   ![Avpublicera](/help/forms/assets/unpublish--form.png)

## Aktivera inskickning av formulär på Edge Delivery genom att konfigurera ett referensfilter för AEM Publisher

För att formuläret ska kunna skickas på ett säkert sätt måste du konfigurera ett **referensfilter** i AEM Publisher. Det här filtret säkerställer att endast behöriga förfrågningar från Edge Delivery kan utföra skrivåtgärder (POST, PUT, DELETE, COPY, MOVE) och förhindrar obehöriga ändringar. Så här konfigurerar du ett referensfilter för AEM Publisher:

### Uppdatera AEM Instance URL i Edge Delivery

Ändra `submitBaseUrl` i filen **constant.js** i formulärblocket för att ange AEM-instans-URL:

**För molninstallation:**

```js
export const submitBaseUrl = 'https://publish-p120-e12.adobeaemcloud.com';
```
**För lokal utveckling:**

```js
export const submitBaseUrl = 'http://localhost:4503';
```

### Ändra CORS-konfigurationen

Justera **CORS-inställningarna** för att tillåta formuläröverföringsbegäranden från Edge Delivery-domäner. Mer information finns i [CORS konfigurationsguide](https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors).

**Exempel på CORS-konfiguration:**

```apache
# Developer Localhost
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Franklin Stage
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  

# Franklin Live
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```
Lokal utveckling beskrivs i [dokumentationen](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter) för att aktivera CORS från URL:en för **utvecklingsgränssnittets värd**.

### Konfigurera referensfiltret

Konfigurera **referensfiltret** i AEM Cloud-tjänsten via Cloud Manager. [Mer information](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing) om hur du konfigurerar referensfiltret för en AEM Cloud Service-instans med en molnhanterare.

**JSON-konfiguration för referensfiltret:**

```json
{
  "allow.empty": false,
  "allow.hosts": [],
  "allow.hosts.regexp": [
    "https://.*\\.hlx\\.page:443",
    "https://.*\\.hlx\\.live:443"
  ],
  "filter.methods": [
    "POST",
    "PUT",
    "DELETE",
    "COPY",
    "MOVE"
  ],
  "exclude.agents.regexp": [
    ""
  ]
}
```

Den här konfigurationen anger vilka HTTP-metoder som filtreras, vilka referenser som tillåts och vilka användaragenter som exkluderas från filtret. Genom att implementera dessa konfigurationer skyddas och begränsas **formulärskickningar via Edge Delivery** till endast auktoriserade källor.

### Få tillgång till ditt publicerade adaptiva formulär

Ditt adaptiva formulär är nu tillgängligt via **Edge Delivery** med följande URL-format:

```
https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
```

URL:en för **WKD-Form** är till exempel:

```
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form
```


## Se även

{{universal-editor-see-also}}

