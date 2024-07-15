---
title: Resursmappning
description: Lär dig hur du definierar omdirigeringar, tillfälliga URL:er och virtuella värdar för AEM genom att använda resursmappning.
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 1a1bb23c-d1d1-4e2b-811b-753e6a90a01b
role: Admin
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Resursmappning{#resource-mapping}

Resursmappning används för att definiera omdirigeringar, tillfälliga URL:er och virtuella värdar för AEM.

Du kan till exempel använda dessa mappningar för:

* Lägg till prefix för alla begäranden med `/content` så att den interna strukturen döljs för besökarna på webbplatsen.
* Definiera en omdirigering så att alla begäranden till sidan `/content/en/gateway` på webbplatsen omdirigeras till `https://gbiv.com/`.

En möjlig HTTP-mappning prefix för alla begäranden till `localhost:4503` med `/content`. En sådan här mappning kan användas för att dölja den interna strukturen för besökarna på webbplatsen så som den tillåter:

`localhost:4503/content/we-retail/en/products.html`

Ska kommas åt med:

`localhost:4503/we-retail/en/products.html`

När mappningen automatiskt lägger till prefixet `/content` i `/we-retail/en/products.html`.

>[!CAUTION]
>
>Vanity-URL:er stöder inte regex-mönster.

>[!NOTE]
>
>Mer information finns i dokumentationen för Sling och [Mappningar för resursmatchning](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) och [Resurser](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html).

## Visa mappningsdefinitioner {#viewing-mapping-definitions}

Mappningarna består av två listor som JCR-resurslösaren utvärderar (högst upp) för att hitta en matchning.

De här listorna kan visas (tillsammans med konfigurationsinformation) under alternativet **JCR ResourceResolver** i Felix-konsolen, till exempel `https://<*host*>:<*port*>/system/console/jcrresolver`:

* Konfiguration
Visar den aktuella konfigurationen (enligt definition för [Resurslösaren för Apache Sling](/help/overview/seo-and-url-management.md#etc-map)).

* Konfigurationstest
Detta gör att du kan ange en URL eller resurssökväg. Klicka på **Lös** eller **Karta** för att bekräfta hur posten omformas.

* **Poster för matchningskarta**
Listan över poster som används av metoderna ResourceResolver.resolve för att mappa URL:er till Resources.

* **Mappa mappningsposter**
Listan över poster som används av metoderna ResourceResolver.map för att mappa resurssökvägar till URL:er.

De två listorna visar olika poster, inklusive de som definierats som standard av programmen. Dessa poster syftar ofta till att förenkla URL:er för användaren.

Listparet är ett **mönster**, ett reguljärt uttryck som matchar begäran, med en **Ersättning** som definierar omdirigeringen som ska skjutas ut.

Till exempel:

**Mönster** `^[^/]+/[^/]+/welcome$`

Startar:

**Ersättning** `/libs/cq/core/content/welcome.html`.

Så här omdirigerar du en begäran:

`https://localhost:4503/welcome` &quot;

Till:

`https://localhost:4503/libs/cq/core/content/welcome.html`

Nya mappningsdefinitioner skapas i databasen.

>[!NOTE]
>
>Det finns många tillgängliga resurser som förklarar hur du definierar reguljära uttryck. Exempel: [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### Skapar mappningsdefinitioner i AEM {#creating-mapping-definitions-in-aem}

I en standardinstallation av AEM finns mappen:

`/etc/map/http`

Mappen är den struktur som används för att definiera mappningar för HTTP-protokollet. Andra mappar ( `sling:Folder`) kan skapas under `/etc/map` för alla andra protokoll som du vill mappa.

#### Konfigurera en intern omdirigering till /content {#configuring-an-internal-redirect-to-content}

Så här skapar du en mappning som prefixar en begäran till https://localhost:4503/ med `/content`:

1. Använd CRXDE och navigera till `/etc/map/http`.

1. Skapa en nod:

   * **Typ** `sling:Mapping`
Den här nodtypen är avsedd för sådana mappningar, men det är inte obligatoriskt att använda den.

   * **Namn** `localhost_any`

1. Klicka på **Spara alla**.
1. **Lägg till** följande egenskaper i den här noden:

   * **Namn** `sling:match`

      * **Typ** `String`

      * **Värde** `localhost.4503/`

   * **Namn** `sling:internalRedirect`

      * **Typ** `String`

      * **Värde** `/content/`

1. Klicka på **Spara alla**.

Den här mappningen hanterar en begäran som:
`localhost:4503/geometrixx/en/products.html`
som if:
`localhost:4503/content/geometrixx/en/products.html`
begärdes.

>[!NOTE]
>
>Mer information om tillgängliga snedsättningsegenskaper och hur de kan konfigureras finns i [Resurser](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) i dokumentationen om Sling.
>[Stränginterpolation](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html#string-interpolation-for-etcmap) är till exempel användbar eftersom den gör att du kan konfigurera en mappning som hämtar värden per miljö via systemvariabler.

>[!NOTE]
>
>Du kan använda `/etc/map.publish` för konfigurationerna för publiceringsmiljön. Dessa konfigurationer måste replikeras och den nya platsen ( `/etc/map.publish`) konfigureras för **mappningsplatsen** för [Apache Sling Resource Resolver](/help/overview/seo-and-url-management.md#etc-map) i publiceringsmiljön.
