---
title: Skapa Vanity-URL:er med Dynamic Media med OpenAPI-funktioner
description: Använd Dynamic Media OpenAPI-funktioner för att omvandla URL:er för leverans av stora tillgångar till korta varumärkesanpassade URL:er. En fågel-URL är en kort, ren, lättåtkomlig och läsbar version av din komplexa leverans-URL. Ni kan inkludera ert varumärke, produktnamn och relevanta nyckelord i er egen webbplats för att öka varumärkets synlighet och användarengagemanget
role: Admin
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: 73574b3358451dfe135b91011abb5cad372a783e
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 0%

---


# Använd vanity-URL:er?{#vanity-urls}

Använd [!DNL Dynamic Media OpenAPI capabilities] för att omvandla dina URL:er för lång resursleverans till korta, varumärkesanpassade URL:er. StandardURL:er för leverans av resurser inkluderar systemgenererade UUID:n som gör leverans-URL:en komplex, svår att komma ihåg och dela. Ersätt dessa tillgångs-UUID med enkla identifierare (Vanity ID) för att generera en vanity-URL. En fågel-URL är en kort, ren och läsbar version av din komplexa leverans-URL.

Se följande URL-format för att förstå skillnaden:
* [Standard delivery URL](#standard-urls)
* [Vanity-URL:er](#vanity-url)

Standardleverans-URL:er använder `aaid` följt av ett UUID, medan standard-URL:er använder `avid` följt av en anpassad identifierare (vanity-identifierare).

Använd korta och enkla vanlighetsidentifierare för att göra din leverans-URL kort, ren, läsbar, lättåtkomlig och dela. Använd ert varumärke, era produktnamn och relevanta nyckelord som sans-ID för att öka varumärkets synlighet och användarengagemanget.

När användaren klickar på din egen URL mappas [!DNL Dynamic Media with OpenAPI] automatiskt till den ursprungliga resursplatsen vid åtkomsten och löser dem korrekt vid leveransen för att servera resursen till användaren.

Lär dig att [skapa Vanity-URL:er](#create-vanity-urls).

## Standard Delivery URLs{#standard-urls}

Den vanliga URL:en för [!DNL Dynamic Media with OpenAPI]-resursleverans innehåller en unik systemgenererad identifierare och har följande format.

***Format:*** `https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:aaid:aem:<asset-uuid>/as/<seoname>.<format>`

Standardleverans-URL:en innehåller `aaid` (*faktisk tillgångsidentifierare*) efter `urn:` och ett UUID mellan `urn:aaid:aem:` och `/as/<seoname>.<format>`.

***Exempel:*** `https://delivery-p30902-e145436.adobeaemcloud.com/adobe/assets/urn:aaid:aem:43341ab1-4086-44d2-b7ce-ee546c35613b/as/check.jpeg`

I exemplet ovan är `43341ab1-4086-44d2-b7ce-ee546c35613b` UUID.

## Vanity-URL:er{#vanity-url}

URL:erna för vanity innehåller en vanity-identifierare i stället för resurs-UUID och följer följande format.

***Format:*** `https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:avid:aem:<vanity-id>/<seoname>.<format>`

Den överordnade URL:en innehåller `avid` (*faktisk vanlighetsidentifierare*) efter `urn:` och ditt fågel-ID mellan `urn:avid:aem:` och `/<seoname>.<format>`.

***Exempel:*** `https://delivery-p30902-e145436.adobeaemcloud.com/adobe/assets/urn:avid:aem:VanityCheck/as/check.jpeg`

I exemplet ovan är `VanityCheck` det fågel-ID som ersatte UUID.

## Utforska nyckelfunktioner och fördelar{#capabilities-and-benefits-of-vanity-urls}

Att använda meningsfulla användar-ID:n för att anpassa URL:er för standardleverans av resurser ger flera fördelar och mätbar effekt. Några av de viktigaste funktionerna och fördelarna med vanliga URL:er är bland annat följande.

### Viktiga funktioner{#key-capabilities}

* **URL-anpassning:** Ersätt långa identifierare (resurs-UUID) i leverans-URL:en med kortare, varumärkesanpassade alternativ för att generera en renare leverans-URL.
* **Omdirigering i realtid:** Vanity-URL:er omdirigerar till ursprungliga resurs-UID:n vid körning utan att arbetsflödena avbryts. Användarna ser rena URL:er i adressfältet medan systemet hanterar den tekniska routningen.
* **Enkel länkhantering:** Anpassa dina egna URL:er när som helst utan att påverka materialets leveransprestanda.

### Viktiga fördelar{#key-benefits}

* **Förbättrar användarupplevelsen:** Rena och kortare URL:er är läsbara, användarvänliga, enkla att komma ihåg och dela.

* **Förbättrar användarengagemanget:** Varumärkesbaserade URL:er skapar användarförtroende och förtroende. Det är troligare att användarna klickar på professionella, varumärkesanpassade länkar, vilket ger högre klickfrekvens.

* **SEO-optimering:** URL:er som innehåller relevanta nyckelord förbättrar sökmotorns rangordning och upptäckbarhet.

* **Ökad synlighet för varumärket:** Webbadresserna som är specifika för varumärket stärker varumärkets närvaro i alla marknadsföringskanaler, inklusive e-post, sociala medier och annonskampanjer.
En konsekvent användning av varumärkesprofilerade URL:er i all kommunikation stärker varumärkets identitet och erkännande.

* **Kampanjspårning och -analys:** Använd unika URL:er för vanity för olika kampanjer och kanaler för att få detaljerade insikter om trafikkällor och konverteringsprestanda.

## Förutsättningar{#prerequisites-for-creating-vanity-id}

Kontrollera att du redan har [godkänt resurserna för offentlig leverans](/help/assets/manage-organize-assets-view.md#manage-asset-status) om du vill skapa en egen URL.

## Skapa Vanity-URL:er{#create-vanity-urls}

Utför följande steg för att skapa mål-URL:er:
1. [Ställ in metadata för resurs](#set-up-asset-metadata)
1. [Skapa och mappa Cloud Manager-miljövariabel](#map-cloud-manager-environment-variable)
1. [Godkänn de resurser som kräver ursprungs-URL för leverans](/help/assets/manage-organize-assets-view.md#manage-asset-status)
1. [Generera URL:er för avvikelse](#generate-vanity-urls)

### Ställ in metadata för resurs{#set-up-asset-metadata}

Gör så här för att ställa in ID:t för sans i resursens metadataformulär:
1. Navigera till informationssidan för den mapp som innehåller dina resurser för [!DNL Dynamic Media with OpenAPI]-leverans.
1. [Redigera metadataformuläret](/help/assets/metadata-assets-view.md#edit-metadata-forms) genom att göra något av följande:
   * Lägg till ett nytt metadatafält och ange det obligatoriska ID:t som värde för det fältet.
   * Uppdatera det befintliga fältet genom att ersätta en befintlig metadataegenskaps värde med det obligatoriska fågel-ID:t. Lär dig [bästa praxis](#best-practices) för att skapa ett fågel-ID.
     ![sans-ID](/help/assets/assets/vanity-id-metadata.png)
Läs mer om [metadatamatcheman](/help/assets/metadata-schemas.md).

     >[!NOTE]
     >
     > * Använd unika användar-ID:n för varje resurs. Kontrollera alltid att resurser som delar samma metadataformulär har unika ID:n för DM med OpenAPI-leverans via egna URL:er. Om två resurser delar samma ID för huvudinnehållet, levererar DM med OpenAPI den resurs som senast tog emot detta ID och åsidosätter det tidigare berättigandet för ID:t till en annan resurs.
     >
     > * En enskild resurs kan ha flera ID:n för huvudinnehållet. [Kontakta Adobe support](https://helpx.adobe.com/in/contact.html) och begär att få generera de ID:n som krävs.

När du har konfigurerat ditt användar-ID i resursens metadataformulär mappar [det här metadatafältet till systemets leveransmekanism](#map-cloud-manager-environment-variable).

### Skapa och mappa Cloud Manager-miljövariabel{#map-cloud-manager-environment-variable}

Utför följande steg för att skapa en miljövariabel och mappa den till metadatafältet med ID:t för vanity:

1. [Navigera till konfigurationssidan för din Cloud Manager-miljö](/help/implementing/cloud-manager/environment-variables.md) och gör följande:
   1. Lägg till variabeln `ASSET_DELIVERY_VANITY_ID`. Det här är nyckeln.
   1. Använd värdefältet för att mappa till metadataegenskapen som innehåller fågel-ID:t. Mappningen följer formatet `dc:<your-metadata-property>`, där metadatamappningsprefixet (t.ex. dc:) varierar beroende på metadatakonfigurationsegenskapen.
      ![variabeln ASSET_DELIVERY_VANITY_ID](/help/assets/assets/environment-config.png)
1. Spara ändringarna för att starta om fönstren i miljön.

### Godkänn tillgångar för leverans{#approve-assets-for-delivery}

När du har mappat variabeln `ASSET_DELIVERY_VANITY_ID` i din Cloud Manager-miljö till resursens metadataegenskap som innehåller det överordnade ID:t, [godkänner du dina resurser som kräver en mål-URL för leverans](/help/assets/manage-organize-assets-view.md#manage-asset-status).

### Generera Vanity-URL:er{#generate-vanity-urls}

Gör följande ersättningar i din standardleverans-URL för att omvandla den till en vanity-URL:

* Ersätt **UID** med ditt **vanity ID**.
* Ersätt `aaid` med `avid`.

Se URL-transformeringen [från standard till mål-URL](#standard-urls) ovan.
Lär dig hur du [kopierar dynamiska media med OpenAPI-leverans-URL:er](/help/assets/approve-assets.md#copy-delivery-url-for-approved-assets) för dina resurser.

När användaren klickar på tilläggs-URL:en mappar [!DNL Dynamic Media with OpenAPI] automatiskt användar-ID:t till det ursprungliga tillgångs-UUID:t vid importen och löser dem korrekt vid leveransen så att resursen kan skickas till användaren utan dröjsmål. Du kan anpassa innehålls-URL:en i realtid utan att påverka materialets leveransresultat.

[Förbättra effekten av era egna URL:er med hjälp av de avancerade anpassningsfunktionerna i AEM Cloud-tjänsten.](#scale-using-vanity-url)

## Skala med hjälp av mål-URL:er{#scale-using-vanity-url}

Med AEM as a Cloud Service kan du [anpassa DNS- och CDN-namnen](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/introduction) i dina webbadresser. Använd dessa AEMCS-funktioner med dina egna URL:er för att omvandla dem till unika webbadresser som är rena, beskrivande, varumärkesanpassade och intuitiva och som ger de [ovannämnda fördelarna](#key-benefits).

Se följande huvud-URL och dess anpassningsbara komponenter:

**Vanity URL-format:**

`https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:avid:aem:<vanity-id>/<seoname>.<format>`

<table style="border-collapse:collapse; table-layout:auto; width:auto;">
<tr valign="top">
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>https://delivery&#8209;&lt;tenant&gt;.adobeaemcloud.com</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#customize-dns">Anpassa denna DNS</a></div>
</td>
<td style="padding:0 6px; white-space:nowrap; text-align:center;">/</td>
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>adobe/assets/urn:avid:aem:</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#rewrite-cdn-rules">Anpassa URL med omskrivningsregler</a></div>
</td>
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>&lt;vanity-id&gt;</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#create-vanity-urls">Skapa sans-ID</a></div>
</td>
<td style="padding:0 4px; white-space:nowrap; text-align:left; width:1%;">
<code>/&lt;seoname&gt;.&lt;format&gt;</code>
</td>
</tr>
</table>

**Vanity URL-format med anpassade DNS- och CDN-namn:**

`https://<custom-dns>` `/` `dam/assets/` `<vanity-id>` `/<seoname>.<format>`

**Anpassningsbara URL-komponenter**

* ***[DNS-namn (värdnamn):](#customize-DNS)*** `https://delivery-<tenant>.adobeaemcloud.com` är serverdomänen som är värd för dina resurser. [Anpassa DNS för att ändra värdnamnet](#customize-DNS).
* ***[CDN-omskrivningsregler:](#rewrite-cdn-rules)*** `adobe/assets/urn:avid:aem:` är sökvägsstrukturen som identifierar resurstyper och leveransmetoder. [Skriv om CDN-regler](#rewrite-cdn-rules) om du vill ändra domänsökvägen.

### Anpassa DNS{#customize-dns}

[Ta upp en begäran till Adobe support](https://helpx.adobe.com/in/contact.html) om att skapa den anpassade DNS som krävs för din leveransnivå. Följ de här [bästa metoderna](#best-practices) för att skapa anpassade DNS-namn.

### Skriv om CDN-regler{#rewrite-cdn-rules}

Utför följande steg för att skriva om CDN-reglerna för leverans:

1. Navigera till din AEM-databas för att skapa en YAML-konfigurationsfil.
2. Utför stegen i avsnittet [setup](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-error-pages#setup) för att konfigurera CDN-regler och distribuera konfigurationen via din Cloud Manager-konfigurationspipeline.
Följ de här [bästa metoderna](#best-practices) för att skapa din domänsökväg.
   [Läs mer om CDN-skrivregler](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#request-transformations).

Nedan följer exempel på skrivregler för att lägga till filnamn med tillägg i tillfälliga URL:er. Anpassa dessa omskrivningsregler efter dina specifika krav. [Kontakta Adobe support](https://helpx.adobe.com/in/contact.html) om du behöver mer hjälp:

```- name: cdn-rewrite-rule
  when:
    allOf:
      - reqProperty: tier
        equals: delivery
```

#### För SVG, GIF och PDF {#svg-gif-pdf}

```
    type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.(?:svg|gif|pdf|docx|xlsx))(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/original/as/\1\2
```

#### För video{#video}

För videor som MP4, MOV, AVI och MKV

```
type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.(?:mp4|mov|avi|mkv))(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/play\2
```

#### För bild{#image}

För alla bildtyper, förutom SVG.

```
type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.[^/]+)(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/as/\1\2
```

## Följ de bästa sätten att skapa rena e-postadresser{#best-practices}

Följ dessa metodtips för att skapa anpassade ID:n, DNS-namn och domännamn:

1. Använd inte specialtecken i användar-ID:n, som blanksteg, snedstreck, bindestreck med mera. Systemet ersätter specialtecken i användar-ID med hjälp av en fördefinierad mappning.
1. Använd ert varumärke, produktnamn och relevanta nyckelord i era egna ID:n, anpassade DNS-namn och domännamn för att öka varumärkets synlighet och användarengagemanget.
1. Använd korta, beskrivande ord eller strängar som förmedlar betydelse.
1. Använd texter som bjuder in användare att klicka.
