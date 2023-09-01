---
title: Anpassa och utöka Content Fragments
description: Ett innehållsfragment utökar en standardresurs. Lär dig hur du kan anpassa dem.
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
source-git-commit: 87630d9530194fd0c6d88e05a17db108b765ccb6
workflow-type: tm+mt
source-wordcount: '1812'
ht-degree: 0%

---

# Anpassa och utöka Content Fragments{#customizing-and-extending-content-fragments}

I Adobe Experience Manager as a Cloud Service utökar ett innehållsfragment en standardresurs; se:

* [Skapa och hantera innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md) och [Sidredigering med innehållsfragment](/help/sites-cloud/authoring/fundamentals/content-fragments.md) för mer information om innehållsfragment.

* [Hantera resurser](/help/assets/manage-digital-assets.md) för mer information om standardtillgångar.

## Arkitektur {#architecture}

Grundläggande [beståndsdelar](/help/sites-cloud/administering/content-fragments/overview.md#constituent-parts-of-a-content-fragment) för ett innehållsfragment är:

* A *Innehållsfragment*,
* bestående av en eller flera *Innehållselement*,
* och som kan ha en eller flera *Innehållsvariationer*.

De enskilda innehållsfragmenten baseras på modeller för innehållsfragment:

* Modeller för innehållsfragment definierar strukturen för ett innehållsfragment när det skapas.
* Ett fragment refererar till modellen, så ändringar i modellen kan påverka alla beroende fragment.
* Modeller är inbyggda i datatyper.
* Funktioner för att lägga till nya varianter, osv., måste uppdatera fragmentet därefter.

  >[!NOTE]
  >
  >För att du ska kunna visa/återge ett innehållsfragment måste ditt konto ha `read` behörigheter för modellen.

  >[!CAUTION]
  >
  >Alla ändringar i en befintlig innehållsfragmentmodell kan påverka beroende fragment, vilket kan leda till överblivna egenskaper i dessa fragment.

### Integrering av webbplatser med resurser {#integration-of-sites-with-assets}

Content Fragment Management (CFM) ingår i AEM Assets som:

* Innehållsfragment är resurser.
* De använder befintliga Assets-funktioner.
* De är helt integrerade med Assets (administrationskonsoler och så vidare).

Innehållsfragment betraktas som en webbplatsfunktion som:

* De används när du redigerar sidorna.

#### Mappa innehållsfragment till resurser {#mapping-content-fragments-to-assets}

![innehållsfragment till resurser](assets/content-fragment-to-assets.png)

Innehållsfragment, som baseras på en innehållsfragmentmodell, mappas till en enda resurs:

* Allt innehåll lagras under `jcr:content/data` resursens nod:

   * Elementdata lagras under huvudundernoden:
     `jcr:content/data/master`

   * Variationer lagras under en undernod som innehåller variantens namn, till exempel: `jcr:content/data/myvariation`

   * Data för varje element lagras i respektive undernod som en egenskap med elementnamnet: till exempel elementets innehåll `text` lagras som egenskap `text` på `jcr:content/data/master`

* Metadata och tillhörande innehåll lagras nedan `jcr:content/metadata`
Förutom rubriken och beskrivningen, som inte betraktas som traditionella metadata och lagras på `jcr:content`

#### Resursplats {#asset-location}

Precis som med standardresurser finns ett innehållsavdrag under:

`/content/dam`

#### Tillgångsbehörigheter {#asset-permissions}

Mer information finns i [Innehållsfragment - Ta bort överväganden](/help/sites-cloud/administering/content-fragments/delete-considerations.md).

#### Funktionsintegrering {#feature-integration}

Integrera med Assets Core:

* Funktionen Content Fragment Management (CFM) bygger på Assets core.

* CFM har sina egna implementeringar för objekt i vyerna kort, kolumn och lista. Dessa plugin finns i befintliga resursåtergivningsimplementationer.

* Flera Assets-komponenter har utökats för att passa innehållsfragment.

### Använda innehållsfragment på sidor {#using-content-fragments-in-pages}

>[!CAUTION]
>
>The [Content Fragment-komponenten är en del av Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html). Se [Utveckla kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html) för mer information.

Innehållsfragment kan refereras från AEM sidor, precis som andra resurstyper. AEM tillhandahåller **[Kärnkomponent för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)** - en [som gör att du kan ta med innehållsfragment på sidorna](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page). Du kan även utöka den här **[Innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html)** kärnkomponent.

* Komponenten använder `fragmentPath` -egenskap som refererar till det faktiska innehållsfragmentet. The `fragmentPath` -egenskapen hanteras på samma sätt som liknande egenskaper för andra resurstyper, till exempel när innehållsfragmentet flyttas till en annan plats.

* Med komponenten kan du välja den variant som ska visas.

* Dessutom kan ett styckeintervall markeras för att begränsa utdata. Det kan till exempel användas för utdata med flera kolumner.

* Komponenten tillåter mellanliggande innehåll:

   * Här kan du placera andra resurser (bilder och så vidare) mellan styckena i det refererade fragmentet.

   * För det mellanliggande innehållet behöver du:

      * vara medveten om risken för instabila referenser. Mellanliggande innehåll (som läggs till när en sida redigeras) har ingen fast relation till det stycke som det placeras bredvid, infogning av ett nytt stycke (i innehållsfragmentredigeraren) innan placeringen av det mellanliggande innehållet kan förlora den relativa positionen

      * överväga ytterligare parametrar (till exempel variant- och styckefilter) för att konfigurera vad som ska återges på sidan

>[!NOTE]
>
>**Content Fragment Model:**
>
>När ett innehållsfragment används på en sida refereras den innehållsfragmentmodell som det baseras på.
>
>Det innebär att om modellen inte har publicerats när du publicerar sidan, flaggas den och modellen läggs till i resurserna som ska publiceras med sidan.

### Integrering med andra ramar {#integration-with-other-frameworks}

Innehållsfragment kan integreras med:

* **Översättningar**

  Innehållsfragment är helt integrerade med [Arbetsflöde för AEM](/help/sites-cloud/administering/translation/overview.md). Arkitekturnivå innebär följande:

   * De enskilda översättningarna av ett innehållsfragment är egentligen separata fragment, till exempel:

      * De finns under olika språkrötter, men har exakt samma relativa sökväg under den relevanta språkroten:

        `/content/dam/<path>/en/<to>/<fragment>`

        jämfört med

        `/content/dam/<path>/de/<to>/<fragment>`

   * Förutom de regelbaserade sökvägarna finns det ingen ytterligare koppling mellan de olika språkversionerna av ett innehållsfragment. De hanteras som två separata fragment, även om gränssnittet ger möjlighet att navigera mellan språkvarianterna.

  >[!NOTE]
  >
  >Det AEM arbetsflödet för översättning fungerar med `/content`:
  >
  >* När innehållsfragmentsmodellerna finns i `/conf`, ingår de inte i sådana översättningar. Du kan internationalisera gränssnittssträngarna.

* **Metadata-scheman**

   * Innehållsfragment (återanvänd) [metadatamodeller](/help/assets/metadata-schemas.md), som kan definieras med standardresurser.

   * CFM har ett eget specifikt schema:

     `/libs/dam/content/schemaeditors/forms/contentfragment`

     detta kan vid behov förlängas.

   * respektive schemaformulär är integrerat med fragmentredigeraren.

## API för hantering av innehållsfragment - serversidan {#the-content-fragment-management-api-server-side}

Du kan använda serversidans API för att komma åt dina innehållsfragment. Se:

[com.adobe.cq.dam.cfm](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>Vi rekommenderar att du använder serversidans API i stället för att komma åt innehållsstrukturen direkt.

### Nyckelgränssnitt {#key-interfaces}

Följande tre gränssnitt kan fungera som startpunkter:

* **Innehållsfragment** ([ContentFragment](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

  Med det här gränssnittet kan du arbeta med ett innehållsfragment på ett abstrakt sätt.

  Gränssnittet ger dig möjlighet att

   * Hantera grundläggande data (till exempel get name; get/set title/description)
   * Åtkomst till metadata
   * Åtkomstelement:

      * Listelement
      * Hämta element efter namn
      * Skapa nya element (se [Caveats](#caveats))

      * Åtkomst till elementdata (se `ContentElement`)

   * Listvarianter definierade för fragmentet
   * Skapa nya varianter globalt
   * Hantera associerat innehåll:

      * Listsamlingar
      * Lägg till samlingar
      * Ta bort samlingar

   * Åtkomst till fragmentets modell

  Gränssnitt som representerar de primära elementen i ett fragment är:

   * **Innehållselement** ([ContentElement](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Hämta grundläggande data (namn, titel, beskrivning)
      * Hämta/ange innehåll
      * Få åtkomst till varianter av ett element:

         * Listvarianter
         * Hämta varianter efter namn
         * Skapa nya varianter (se [Caveats](#caveats))
         * Ta bort variationer (se [Caveats](#caveats))
         * Åtkomst till variantdata (se `ContentVariation`)

      * Kortkommando för att matcha variationer (tillämpa ytterligare, implementeringsspecifik reservlogik om den angivna varianten inte är tillgänglig för ett element)

   * **Innehållsvariation** ([ContentVariation](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Hämta grundläggande data (namn, titel, beskrivning)
      * Hämta/ange innehåll
      * Enkel synkronisering, baserat på den senast ändrade informationen

  Alla tre gränssnitten ( `ContentFragment`, `ContentElement`, `ContentVariation`) utöka `Versionable` gränssnitt, som lägger till versionsfunktioner, som krävs för innehållsfragment:

   * Skapa en ny version av elementet
   * Lista versioner av elementet
   * Hämta innehållet i en specifik version av det versionshanterade elementet

### Adapting - Using customito() {#adapting-using-adaptto}

Följande kan anpassas:

* `ContentFragment` kan anpassas till

   * `Resource` - den underliggande Sling-resursen; uppdatera den underliggande `Resource` kräver att `ContentFragment` -objekt.

   * `Asset` - DAM `Asset` abstraktion som representerar innehållsfragmentet; uppdatera `Asset` kräver att `ContentFragment` -objekt.

* `ContentElement` kan anpassas till

   * [`ElementTemplate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html) - för åtkomst till elementets strukturinformation.

* [`FragmentTemplate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource` kan anpassas till

   * `ContentFragment`

### Caveats {#caveats}

Det bör noteras att

* Hela API:t är utformat för **not** Bevara ändringarna automatiskt (om inget annat anges i API JavaDoc). Därför måste du alltid implementera resurslösaren för respektive begäran (eller den lösare som du använder).

* Uppgifter som kan kräva ytterligare arbete:

   * Vi rekommenderar starkt att du skapar nya varianter av `ContentFragment`. Detta garanterar att alla element delar den här variationen och att lämpliga globala datastrukturer uppdateras efter behov för att återspegla den nyligen skapade variationen i innehållsstrukturen.

   * Ta bort befintliga variationer genom ett element med `ContentElement.removeVariation()`, kommer inte att uppdatera de globala datastrukturer som är tilldelade varianten. Använd `ContentFragment.removeVariation()` som i stället tar bort en variant globalt.

## API:t för hantering av innehållsfragment - klientsidan {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>Klientsidans API är internt.

### Ytterligare information {#additional-information}

Se följande:

* `filter.xml`

  The `filter.xml` för hantering av innehållsfragment konfigureras så att den inte överlappar det centrala resurspaketet.

## Redigera sessioner {#edit-sessions}

>[!CAUTION]
>
>Tänk på den här bakgrundsinformationen. Du ska inte ändra någonting här (eftersom det är markerat som en *privat område* i databasen), men det kan i vissa fall hjälpa dig att förstå hur saker och ting fungerar under huven.

Att redigera ett innehållsfragment, som kan sträcka sig över flera vyer (= HTML-sidor), är atomiskt. Eftersom sådana atomiska redigeringsfunktioner för flera vyer inte är ett vanligt AEM, används det som kallas för ett innehållsfragment *redigeringssession*.

En redigeringssession startas när användaren öppnar ett innehållsfragment i redigeraren. Redigeringssessionen är slut när användaren lämnar redigeraren genom att välja antingen **Spara** eller **Avbryt**.

Tekniskt sett utförs alla redigeringar på *live* innehåll, precis som med all annan AEM redigering. När redigeringssessionen startas skapas en version av den aktuella, oredigerade statusen. Om en användare avbryter en redigering återställs den versionen. Om användaren klickar på **Spara**, inget specifikt görs eftersom all redigering kördes på *live* därför bevaras alla ändringar redan. Klicka även på **Spara** kommer att utlösa viss bakgrundsbearbetning (till exempel att skapa fullständig textsökningsinformation och/eller hantera blandade medieresurser).

Det finns vissa säkerhetsåtgärder för kantärenden, till exempel om användaren försöker lämna redigeraren utan att spara eller avbryta redigeringssessionen. Det går även att spara data med jämna mellanrum.
Observera att två användare kan redigera samma innehållsfragment samtidigt och därför skriva över varandras ändringar. För att förhindra detta måste innehållsfragmentet låsas genom att tillämpa DAM-administrationens *Utcheckning* åtgärd på fragmentet.

## Exempel {#examples}

### Exempel: Åtkomst till ett befintligt innehållsfragment {#example-accessing-an-existing-content-fragment}

För att uppnå detta kan du anpassa resursen som representerar API:t till:

`com.adobe.cq.dam.cfm.ContentFragment`

Till exempel:

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### Exempel: Skapa ett nytt innehållsfragment {#example-creating-a-new-content-fragment}

Om du vill skapa ett nytt innehållsfragment programmatiskt måste du använda en
`FragmentTemplate` anpassas från en modellresurs.

Till exempel:

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Exempel: Ange intervall för autosparande {#example-specifying-the-auto-save-interval}

The [autosparintervall](/help/sites-cloud/administering/content-fragments/managing.md#save-close-and-versions) (mätt i sekunder) kan definieras med konfigurationshanteraren (ConfMgr):

* Nod: `<conf-root>/settings/dam/cfm/jcr:content`
* Egenskapsnamn: `autoSaveInterval`
* Typ: `Long`

* Standard: `600` (10 minuter); detta definieras på `/libs/settings/dam/cfm/jcr:content`

Om du vill ange ett intervall för automatiskt sparande på 5 minuter måste du definiera egenskapen på noden, till exempel:

* Nod: `/conf/global/settings/dam/cfm/jcr:content`
* Egenskapsnamn: `autoSaveInterval`

* Typ: `Long`

* Värde: `300` (5 minuter motsvarar 300 sekunder)

## Komponenter för sidredigering {#components-for-page-authoring}

Mer information finns i

* [Kärnkomponenter - komponent för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html) (rekommenderas)
