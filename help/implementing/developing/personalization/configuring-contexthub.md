---
title: ContextHub konfigureras
description: Lär dig hur du konfigurerar Context Hub, ett ramverk för lagring, manipulering och presentation av kontextdata.
exl-id: 1fd7d41e-31ad-4838-8749-a5791edcfd63
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1629'
ht-degree: 0%

---

# ContextHub konfigureras {#configuring-contexthub}

ContextHub är ett ramverk för att lagra, ändra och presentera kontextdata. Mer information om ContextHub finns i [ContextHub developer overview](contexthub.md).

Du kan konfigurera ContextHub-verktygsfältet för att kontrollera om det visas i förhandsgranskningsläget, för att skapa ContextHub-butiker och lägga till gränssnittsmoduler.

## Visa och dölja ContextHub-gränssnittet {#showing-and-hiding-the-contexthub-ui}

Konfigurera Adobe Granite ContextHub OSGi-tjänsten för att visa eller dölja [ContextHub-gränssnitt](/help/sites-cloud/authoring/personalization/targeted-content.md) på era sidor. Tjänstens PID är `com.adobe.granite.contexthub.impl.ContextHubImpl.`

Du kan antingen använda [Webbkonsol](/help/implementing/deploying/configuring-osgi.md) eller använda en JCR-nod i databasen:

* **Webbkonsol:** Om du vill visa användargränssnittet väljer du egenskapen Visa användargränssnitt. Om du vill dölja användargränssnittet avmarkerar du egenskapen Dölj användargränssnitt.
* **JCR-nod:** Ange det booleska värdet för att visa användargränssnittet `com.adobe.granite.contexthub.show_ui` egenskap till `true`. Om du vill dölja användargränssnittet anger du egenskapen till `false`.

När du visar ContextHub-gränssnittet visas det bara på sidor AEM författarinstanser. Gränssnittet visas inte på sidor med publiceringsinstanser.

## Lägga till gränssnittslägen och moduler för ContextHub {#adding-contexthub-ui-modes-and-modules}

Konfigurera de gränssnittslägen och moduler som visas i ContextHub-verktygsfältet i förhandsgranskningsläget:

* Gränssnittslägen: Grupper av relaterade moduler
* Moduler: Widgetar som visar kontextdata från en butik och gör att författare kan ändra kontexten

Gränssnittslägen visas som en serie ikoner till vänster i verktygsfältet. När du väljer det här alternativet visas modulerna för ett användargränssnittsläge till höger.

![ContextHub-verktygsfältet](assets/contexthub-toolbar.png)

Ikoner är referenser från [Coral UI icon library](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons).

### Lägga till ett gränssnittsläge {#adding-a-ui-mode}

Lägg till ett gränssnittsläge för att gruppera relaterade ContextHub-moduler. När du skapar gränssnittsläget anger du den titel och ikon som visas i ContextHub-verktygsfältet.

1. I Experience Manager väljer du Verktyg > Webbplatser > Kontextnav.
1. Välj standardkonfigurationsbehållaren.
1. Välj Kontextnavskonfiguration.
1. Markera knappen Skapa och välj sedan gränssnittsläge för kontextnav.

   ![Lägg till gränssnittsläge](assets/contexthub-ui-mode.png)

1. Ange värden för följande egenskaper:

   * Rubrik för användargränssnittsläge: Den titel som identifierar användargränssnittsläget
   * Lägesikon: Väljaren för [Coral UI icon](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) att använda, till exempel `coral-Icon--user`
   * Aktiverad: Välj det här alternativet om du vill visa användargränssnittsläget i verktygsfältet ContextHub

1. Välj Spara.

### Lägga till en gränssnittsmodul {#adding-a-ui-module}

Lägg till en ContextHub-gränssnittsmodul i ett UI-läge så att den visas i ContextHub-verktygsfältet för förhandsgranskning av sidinnehåll. När du lägger till en UI-modul skapar du en instans av en modultyp som är registrerad med ContextHub. Om du vill lägga till en gränssnittsmodul måste du känna till namnet på den associerade modultypen.

AEM innehåller en grundläggande gränssnittsmodultyp samt flera exempeltyper av gränssnittsmodul som du kan basera en gränssnittsmodul på. Följande tabell innehåller en kort beskrivning av vart och ett av dem. Mer information om hur du utvecklar en anpassad gränssnittsmodul finns i [Skapa gränssnittsmoduler för ContextHub](extending-contexthub.md#creating-contexthub-ui-module-types).

Egenskaperna för användargränssnittsmodulen innehåller en detaljkonfiguration där du kan ange värden för modulspecifika egenskaper. Du anger detaljkonfigurationen i JSON-format. Kolumnen Modultyp i tabellen innehåller länkar till information om den JSON-kod som krävs för varje gränssnittsmodultyp.

| Modultyp | Beskrivning | Butik |
|---|---|---|
| [contexthub.base](sample-modules.md#contexthub-base-ui-module-type) | En allmän gränssnittsmodultyp | Konfigureras i gränssnittsmodulens egenskaper |
| [contexthub.browserinfo](sample-modules.md#contexthub-browserinfo-ui-module-type) | Visar information om webbläsaren | `surferinfo` |
| [contexthub.datetime](sample-modules.md#contexthub-datetime-ui-module-type) | Visar datum- och tidsinformation | `datetime` |
| [contexthub.location](sample-modules.md#contexthub-location-ui-module-type) | Visar klientens latitud och longitud och platsen på en karta. Gör att du kan ändra platsen. | `geolocation` |
| [contexthub.screen-orientation](sample-modules.md#contexthub-screen-orientation-ui-module-type) | Visar enhetens skärmorientering (liggande eller stående) | `emulators` |
| [contexthub.tagcloud](sample-modules.md#contexthub-tagcloud-ui-module-type) | Visar statistik om sidtaggar | `tagcloud` |
| [granite.profile](sample-modules.md#granite-profile-ui-module-type) | Visar profilinformationen för den aktuella användaren, inklusive `authorizableID`, `displayName` och `familyName`. Du kan ändra värdet för `displayName` och `familyName`. | `profile` |

1. I Experience Manager väljer du Verktyg > Webbplatser > ContextHub.
1. Välj den konfigurationsbehållare som du vill lägga till en gränssnittsmodul i.
1. Klicka på eller skriv den ContextHub-konfiguration som du vill lägga till gränssnittsmodulen i.
1. Välj det användargränssnittsläge som du lägger till användargränssnittsmodulen i.
1. Markera knappen Skapa och välj sedan ContextHub UI Module (generisk).

   ![Användargränssnittsmodulen ContextHub](assets/contexthub-ui-module.png)

1. Ange värden för följande egenskaper:

   * Modultitel för användargränssnitt: En titel som identifierar användargränssnittsmodulen
   * Modultyp: Modultypen
   * Aktiverad: Välj det här alternativet om du vill visa gränssnittsmodulen i ContextHub-verktygsfältet

1. (Valfritt) Om du vill åsidosätta standardkonfigurationen för lagring anger du ett JSON-objekt för att konfigurera UI-modulen.
1. Välj Spara.

## Skapa ett ContextHub Store {#creating-a-contexthub-store}

Skapa ett kontextnavlager för att behålla användardata och komma åt data efter behov. ContextHub-butikerna baseras på registrerade butikskandidater. När du skapar butiken behöver du värdet för den storeType som butikskandidaten registrerats med. (Se [Skapa anpassade butikskandidater](extending-contexthub.md#creating-custom-store-candidates).)

### Detaljerad lagringskonfiguration {#detailed-store-configuration}

När du konfigurerar en butik kan du med egenskapen Detaljkonfiguration ange värden för butiksspecifika egenskaper. Värdet baseras på `config` parameter för butikens `init` funktion. Därför beror det på butiken om du behöver ange det här värdet och värdeformatet.

Värdet för egenskapen Detaljkonfiguration är en `config` -objekt i JSON-format.

### Exempelarkivsökande {#sample-store-candidates}

AEM innehåller följande exempel på butikskandidater som du kan basera en butik på.

| Butikstyp | Beskrivning |
|---|---|
| [aem.segmentation](sample-stores.md#aem-segmentation-sample-store-candidate) | Lagra för lösta och olösta ContextHub-segment. Hämtar automatiskt segment från ContextHub SegmentManager |
| [contexthub.geolocation](sample-stores.md#contexthub-geolocation-sample-store-candidate) | Lagrar latitud- och longitudvärdena för webbläsarplatsen. |
| [granite.emulators](sample-stores.md#granite-emulators-sample-store-candidate) | Definierar egenskaper och funktioner för flera enheter och identifierar den aktuella klientenheten |
| [granite.profile](sample-stores.md#granite-profile-sample-store-candidate) | Lagrar profildata för den aktuella användaren |
| [contexthub.surferinfo](sample-stores.md#contexthub-surferinfo-sample-store-candidate) | Lagrar information om klienten, till exempel enhetsinformation, webbläsartyp och fönsterorientering |

1. I Experience Manager väljer du Verktyg > Webbplatser > ContextHub.
1. Välj standardkonfigurationsbehållaren.
1. Välj kontextubkonfiguration
1. Om du vill lägga till en butik väljer du ikonen Skapa och sedan KontextHub Store Configuration.

   ![Konfiguration av ContextHub-butik](assets/contexthub-store-configuration.png)

1. Ange värden för de grundläggande konfigurationsegenskaperna och välj sedan Nästa:

   * **Konfigurationstitel:** Titeln som identifierar butiken
   * **Lagringstyp:** Värdet på egenskapen storeType för butikskandidaten som butiken ska baseras på
   * **Obligatoriskt:** Välj
   * **Aktiverad:** Markera för att aktivera butiken

1. (Valfritt) Om du vill åsidosätta standardarkivkonfigurationen anger du ett JSON-objekt i rutan Detaljkonfiguration (JSON).
1. Välj Spara.

## Exempel: Använda en JSONP-tjänst  {#example-using-a-jsonp-service}

I det här exemplet visas hur du konfigurerar en lagringsplats och visar data i en gränssnittsmodul. I det här exemplet används MD5-tjänsten på jsontest.com webbplats som datakälla för en butik. Tjänsten returnerar MD5-hash-koden för en sträng i JSON-format.

Ett contextHub.generic-jsonp-arkiv har konfigurerats så att det lagrar data för serviceanropet `https://md5.jsontest.com/?text=%22text%20to%20md5%22`. Tjänsten returnerar följande data som visas i en gränssnittsmodul:

```javascript
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### Skapa ett kontexthub.generic-jsonp-arkiv {#creating-a-contexthub-generic-jsonp-store}

Med exempelarkivkandidaten contexthub.generic-jsonp kan du hämta data från en JSONP-tjänst eller en webbtjänst som returnerar JSON-data. För den här butikskandidaten använder du butikskonfigurationen för att ange information om den JSONP-tjänst som ska användas.

The [init](contexthub-api.md#init-name-config) funktionen i `ContextHub.Store.JSONPStore` JavaScript-klassen definierar en `config` objekt som initierar den här lagringskanalen. The `config` objektet innehåller `service` -objekt som innehåller information om JSONP-tjänsten. Om du vill konfigurera butiken anger du `service` -objekt i JSON-format som värde för egenskapen Detaljkonfiguration.

Om du vill spara data från MD5-tjänsten på jsontest.com här webbplatsen ska du göra så här: [Skapa ett ContextHub Store](#creating-a-contexthub-store) med följande egenskaper:

* **Konfigurationstitel:** md5
* **Lagringstyp:** contexthub.generic-jsonp
* **Obligatoriskt:** Välj
* **Aktiverad:** Välj
* **Detaljkonfiguration (JSON):**

  ```javascript
  {
   "service": {
   "jsonp": false,
   "timeout": 1000,
   "ttl": 1800000,
   "secure": false,
   "host": "md5.jsontest.com",
   "port": 80,
   "params":{
   "text":"text to md5"
       }
     }
   }
  ```

### Lägga till en gränssnittsmodul för md5-data {#adding-a-ui-module-for-the-md-data}

Lägg till en gränssnittsmodul i ContextHub-verktygsfältet för att visa data som lagras i exempelarkivet md5. I det här exemplet används modulen contexthub.base för att skapa följande gränssnittsmodul:

![ContextHub MD5 store](assets/contexthub-md5-store.png)

Använd proceduren i [Lägga till en gränssnittsmodul](#adding-a-ui-module) om du vill lägga till gränssnittsmodulen i ett befintligt användargränssnittsläge, till exempel ett exempel på användargränssnittsläge. Använd följande egenskapsvärden för UI-modulen:

* **Modultitel för användargränssnitt:** MD5
* **Modultyp:** contexthub.base
* **Detaljkonfiguration (JSON):**

  ```javascript
  {
   "icon": "coral-Icon--data",
   "title": "MD5 Conversion",
   "storeMapping": { "md5": "md5" },
   "template": "<p> {{md5.original}}</p>;
                <p>{{md5.md5}}</p>"
  }
  ```

## Debugging ContextHub {#debugging-contexthub}

Ett felsökningsläge för ContextHub kan aktiveras för att tillåta felsökning. Felsökningsläget kan aktiveras antingen via ContextHub-konfigurationen eller via CRXDE.

### Via konfigurationen {#via-the-configuration}

Redigera ContextHub-konfigurationen och markera alternativet **Felsök**

1. Markera **Verktyg > Sites > ContextHub**
1. Välj standard **Konfigurationsbehållare**
1. Välj **KontextHub-konfiguration** och markera **Redigera markerat element**
1. Välj **Felsök** och markera **Spara**

### Via CRXDE {#via-crxde}

Använd CRXDE Lite för att ange egenskapen `debug` till **true** under:

* `/conf/global/settings/cloudsettings` eller
* `/conf/<site>/settings/cloudsettings`

### Felsökningsmeddelanden för loggning för ContextHub {#logging-debug-messages-for-contexthub}

Konfigurera tjänsten Adobe Granite ContextHub OSGi (PID = `com.adobe.granite.contexthub.impl.ContextHubImpl`) för att logga detaljerade felsökningsmeddelanden som är användbara vid utveckling.

Du kan antingen använda [Webbkonsol](/help/implementing/deploying/configuring-osgi.md) eller använda en JCR-nod i databasen:

* Webbkonsol: Om du vill logga felsökningsmeddelanden väljer du egenskapen Felsök.
* JCR-nod: Om du vill logga felsökningsmeddelanden anger du det booleska värdet `com.adobe.granite.contexthub.debug` egenskap till `true`.

### Tyst läge {#silent-mode}

I tyst läge inaktiveras all felsökningsinformation. Till skillnad från det normala felsökningsalternativet, som kan anges separat för varje ContextHub-konfiguration, är tyst läge en global inställning som har företräde framför eventuella felsökningsinställningar på ContextHub-konfigurationsnivån.

Detta är användbart för publiceringsinstansen där du inte vill ha någon felsökningsinformation alls. Eftersom det är en global inställning aktiveras den via OSGi.

1. Öppna **Konfiguration av Adobe Experience Manager Web Console** på `http://<host>:<port>/system/console/configMgr`
1. Sök efter **Adobe Granite ContextHub**
1. Klicka på konfigurationen **Adobe Granite ContextHub** för att redigera dess egenskaper
1. Markera alternativet **Tyst läge** och klicka **Spara**

## Inaktiverar ContextHub {#disabling-contexthub}

ContextHub kan inaktiveras för att förhindra att den läser in js/css och initierar. Det finns två alternativ för att inaktivera ContextHub:

* Redigera ContextHub-konfigurationen och markera alternativet **Inaktivera ContextHub**

   1. Markera **Verktyg > Sites > ContextHub**
   1. Välj standard **Konfigurationsbehållare**
   1. Välj **KontextHub-konfiguration** och markera **Redigera markerat element**
   1. Välj **Inaktivera ContextHub** och markera **Spara**

eller

* Använd CRXDE Lite för att ange egenskapen `disabled` till **true** under `/conf/global/settings/cloudsettings/<configName>/contexthub`
