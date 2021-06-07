---
title: Anpassa och utöka Content Fragments
description: Ett innehållsfragment utökar en standardresurs.
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
source-git-commit: a446efacb91f1a620d227b9413761dd857089c96
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 1%

---

# Anpassa och utöka Content Fragments{#customizing-and-extending-content-fragments}

Inom Adobe Experience Manager som Cloud Service utökar ett innehållsfragment en standardresurs. se:

* [Skapa och hantera ](/help/assets/content-fragments/content-fragments.md) innehållsfragment och  [sidredigering med ](/help/sites-cloud/authoring/fundamentals/content-fragments.md) innehållsfragment för mer information om innehållsfragment.

* [Hantera ](/help/assets/manage-digital-assets.md) resurser för mer information om standardresurser.

<!-- Removing the extend-asset-editor article for now as I'm unsure of its accuracy. Hence commenting this link.
* [Managing Assets](/help/assets/manage-digital-assets.md) and [Customizing and Extending the Asset Editor](/help/assets/extend-asset-editor.md) for further information about standard assets.
-->

## Arkitektur {#architecture}

De grundläggande [beståndsdelarna](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) i ett innehållsfragment är:

* A *Content Fragment*,
* bestående av ett eller flera *innehållselement*,
* och som kan ha en eller flera *innehållsvariationer*.

De enskilda innehållsfragmenten baseras på modeller för innehållsfragment:

* Modeller för innehållsfragment definierar strukturen för ett innehållsfragment när det skapas.
* Ett fragment refererar till modellen. så ändringar i modellen kan/kommer att påverka beroende fragment.
* Modeller är inbyggda i datatyper.
* Funktioner för att lägga till nya varianter, osv., måste uppdatera fragmentet därefter.

   >[!NOTE]
   >
   >För att du ska kunna visa/återge ett innehållsfragment måste ditt konto ha `read` behörighet för modellen.

   >[!CAUTION]
   >
   >Alla ändringar i en befintlig innehållsfragmentmodell kan påverka beroende fragment. detta kan leda till egenskaper som är överblivna i dessa fragment.

### Integrering av platser med resurser {#integration-of-sites-with-assets}

Content Fragment Management (CFM) ingår i AEM Assets som:

* Innehållsfragment är resurser.
* De använder befintliga Assets-funktioner.
* De är helt integrerade med Assets (Admin Consoles, etc.).

Innehållsfragment betraktas som en webbplatsfunktion som:

* De används när du redigerar sidorna.

#### Mappa innehållsfragment till resurser {#mapping-content-fragments-to-assets}

![innehållsfragment till resurser](assets/content-fragment-to-assets.png)

Innehållsfragment, som baseras på en innehållsfragmentmodell, mappas till en enda resurs:

* Allt innehåll lagras under noden `jcr:content/data` för resursen:

   * Elementdata lagras under den överordnad undernoden:
      `jcr:content/data/master`

   * Variationer lagras under en undernod som har variantens namn:
t.ex. `jcr:content/data/myvariation`

   * Data för varje element lagras i respektive undernod som en egenskap med elementnamnet:
Innehållet i elementet `text` lagras t.ex. som egenskapen `text` på `jcr:content/data/master`

* Metadata och tillhörande innehåll lagras under `jcr:content/metadata`
Förutom rubriken och beskrivningen, som inte betraktas som traditionella metadata och lagras på 
`jcr:content`

#### Resursplats {#asset-location}

Precis som med standardresurser finns ett innehållsavdrag under:

`/content/dam`

#### Resursbehörigheter {#asset-permissions}

Mer information finns i [Innehållsfragment - Ta bort överväganden](/help/assets/content-fragments/content-fragments-delete.md).

#### Funktionsintegrering {#feature-integration}

Integrera med Assets Core:

* Funktionen Content Fragment Management (CFM) bygger på Assets core.

* CFM tillhandahåller egna implementeringar för objekt i vyerna kort/kolumn/lista. dessa plugin-program i befintliga resursåtergivningsimplementationer.

* Flera Assets-komponenter har utökats för att passa innehållsfragment.

### Använda innehållsfragment på sidor {#using-content-fragments-in-pages}

>[!CAUTION]
>
>Komponenten [Innehållsfragment är en del av kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html). Mer information finns i [Developing Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html).

Innehållsfragment kan refereras från AEM sidor, precis som andra resurstyper. AEM innehåller **[kärnkomponenten för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)** - en [komponent som gör att du kan ta med innehållsfragment på dina sidor](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-a-content-fragment-to-your-page). Du kan också utöka den här **[innehållskomponenten](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html)**.

* Komponenten använder egenskapen `fragmentPath` för att referera till det faktiska innehållsfragmentet. Egenskapen `fragmentPath` hanteras på samma sätt som liknande egenskaper för andra tillgångstyper. till exempel när innehållsfragmentet flyttas till en annan plats.

* Med komponenten kan du välja varianten som ska visas.

* Dessutom kan ett antal stycken väljas för att begränsa utdata. Detta kan till exempel användas för utdata med flera kolumner.

* Komponenten tillåter mellanliggande innehåll:

   * Här kan du placera andra resurser (bilder, etc.) mellan styckena i det refererade fragmentet.

   * För det mellanliggande innehållet behöver du:

      * vara medvetna om risken för instabila referenser, mellanliggande innehåll (som läggs till när en sida redigeras) har ingen fast relation till det stycke som det placeras bredvid, och infogning av ett nytt stycke (i innehållsfragmentredigeraren) innan placeringen av det mellanliggande innehållet kan förlora den relativa positionen

      * överväga ytterligare parametrar (till exempel variant- och styckefilter) för att konfigurera vad som ska återges på sidan

>[!NOTE]
>
>**Content Fragment Model:**
>
>När ett innehållsfragment används på en sida refereras innehållsfragmentmodellen som det baseras på.
>
>Det innebär att om modellen inte har publicerats när du publicerar sidan, kommer den att flaggas och läggas till i resurserna som ska publiceras med sidan.

### Integrering med andra ramverk {#integration-with-other-frameworks}

Innehållsfragment kan integreras med:

* **Översättningar**

   Content Fragments är helt integrerat med arbetsflödet för AEM. Arkitekturnivå innebär följande:

   * De enskilda översättningarna av ett innehållsfragment är i själva verket separata fragment. till exempel:

      * De finns under olika språkrötter. men har exakt samma relativa sökväg under den relevanta språkroten:

         `/content/dam/<path>/en/<to>/<fragment>`

         jämfört med

         `/content/dam/<path>/de/<to>/<fragment>`
   * Förutom de regelbaserade sökvägarna finns det ingen ytterligare koppling mellan de olika språkversionerna av ett innehållsfragment. De hanteras som två separata fragment, även om användargränssnittet ger möjlighet att navigera mellan språkvarianterna.
   >[!NOTE]
   >
   >Det AEM arbetsflödet för översättning fungerar med `/content`:
   >
   >* Eftersom innehållsfragmentmodellerna finns i `/conf` inkluderas de inte i sådana översättningar. Du kan internationalisera gränssnittssträngarna.


* **Metadata-scheman**

   * Innehållsfragment (re) använder [metadatamatcheman](/help/assets/metadata-schemas.md) som kan definieras med standardresurser.

   * CFM har ett eget specifikt schema:

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      detta kan vid behov förlängas.

   * respektive schemaformulär är integrerat med fragmentredigeraren.

## API för hantering av innehållsfragment - serversidan {#the-content-fragment-management-api-server-side}

Du kan använda serversidans API för att komma åt dina innehållsfragment; se:

[com.adobe.cq.dam.cfm](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>Vi rekommenderar att du använder serversidans API i stället för att komma åt innehållsstrukturen direkt.

### Nyckelgränssnitt {#key-interfaces}

Följande tre gränssnitt kan fungera som startpunkter:

* **Innehållsfragment**  ([ContentFragment](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   Med det här gränssnittet kan du arbeta med ett innehållsfragment på ett abstrakt sätt.

   Gränssnittet ger dig möjlighet att

   * Hantera grundläggande data (t.ex. get name;) get/set title/description)
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

   * **Innehållselement**  ([ContentElement](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Hämta grundläggande data (namn, titel, beskrivning)
      * Hämta/ange innehåll
      * Få åtkomst till varianter av ett element:

         * Listvarianter
         * Hämta varianter efter namn
         * Skapa nya varianter (se [Caveats](#caveats))
         * Ta bort variationer (se [Caveats](#caveats))
         * Åtkomst till variantdata (se `ContentVariation`)
      * Kortkommando för att matcha variationer (tillämpa ytterligare, implementeringsspecifik reservlogik om den angivna varianten inte är tillgänglig för ett element)
   * **Innehållsvariation**  ([ContentVariation](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Hämta grundläggande data (namn, titel, beskrivning)
      * Hämta/ange innehåll
      * Enkel synkronisering, baserat på den senast ändrade informationen

   Alla tre gränssnitten ( `ContentFragment`, `ContentElement`, `ContentVariation`) utökar gränssnittet `Versionable`, som lägger till versionshanteringsfunktioner som krävs för innehållsfragment:

   * Skapa en ny version av elementet
   * Lista versioner av elementet
   * Hämta innehållet i en specifik version av det versionshanterade elementet







### Anpassning - Använder customito() {#adapting-using-adaptto}

Följande kan anpassas:

* `ContentFragment` kan anpassas till

   * `Resource` - den underliggande Sling-resursen, Om du vill uppdatera det underliggande  `Resource` direkt måste du återskapa  `ContentFragment` objektet.

   * `Asset` - DAM- `Asset` förkortningen som representerar innehållsfragmentet, för att uppdatera  `Asset` direkt måste  `ContentFragment` objektet återskapas.

* `ContentElement` kan anpassas till

   * [`ElementTemplate`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html) - för åtkomst till elementets strukturinformation.

* [`FragmentTemplate`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource` kan anpassas till

   * `ContentFragment`

### Caveats {#caveats}

Det bör noteras att

* Hela API:t är utformat för att **inte** behålla ändringar automatiskt (om inget annat anges i API JavaDoc). Därför måste du alltid implementera resurslösaren för respektive begäran (eller den lösare som du använder).

* Uppgifter som kan kräva ytterligare arbete:

   * Vi rekommenderar starkt att du skapar nya variationer från `ContentFragment`. Detta garanterar att alla element delar den här variationen och att lämpliga globala datastrukturer uppdateras efter behov för att återspegla den nyligen skapade variationen i innehållsstrukturen.

   * Om du tar bort befintliga variationer genom ett element med `ContentElement.removeVariation()` uppdateras inte de globala datastrukturer som är tilldelade variationen. Om du vill vara säker på att dessa datastrukturer är synkroniserade använder du `ContentFragment.removeVariation()` i stället, vilket tar bort en global variation.

## API för hantering av innehållsfragment - klientsidan {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>Klientsidans API är internt.

### Ytterligare information {#additional-information}

Se följande:

* `filter.xml`

   `filter.xml` för hantering av innehållsfragment har konfigurerats så att den inte överlappar det centrala resurspaketet för resurser.

## Redigera sessioner {#edit-sessions}

>[!CAUTION]
>
>Ta hänsyn till den här bakgrundsinformationen. Du ska inte ändra någonting här (eftersom det är markerat som ett *privat område* i databasen), men det kan i vissa fall hjälpa att förstå hur saker och ting fungerar under huven.

Att redigera ett innehållsfragment, som kan sträcka sig över flera vyer (= HTML-sidor), är av avgörande betydelse. Eftersom sådana atomiska redigeringsfunktioner för flera vyer inte är ett vanligt AEM använder innehållsfragment det som kallas *redigeringssession*.

En redigeringssession startas när användaren öppnar ett innehållsfragment i redigeraren. Redigeringssessionen avslutas när användaren lämnar redigeraren genom att välja antingen **Spara** eller **Avbryt**.

Tekniskt sett utförs alla redigeringar på *live*-innehåll, precis som med all annan AEM redigering. När redigeringssessionen startas skapas en version av den aktuella, oredigerade statusen. Om en användare avbryter en redigering återställs den versionen. Om användaren klickar på **Spara** görs ingenting specifikt, eftersom all redigering utfördes på *live*-innehåll, och därför bevaras alla ändringar redan. Om du klickar på **Spara** utlöses även bakgrundsbearbetning (som att skapa fullständig textsökningsinformation och/eller hantera blandade medieresurser).

Det finns vissa säkerhetsåtgärder för kantfall. Om användaren till exempel försöker lämna redigeraren utan att spara eller avbryta redigeringssessionen. Det går även att spara data med jämna mellanrum för att förhindra dataförlust.
Observera att två användare kan redigera samma innehållsfragment samtidigt och därför skriva över varandras ändringar. För att förhindra detta måste innehållsfragmentet låsas genom att DAM-administrationens *utcheckningsåtgärd* används på fragmentet.

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
`FragmentTemplate` anpassat från en modellresurs.

Till exempel:

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Exempel: Ange intervall för autosparande {#example-specifying-the-auto-save-interval}

Du kan definiera intervallet [för automatiskt sparande](/help/assets/content-fragments/content-fragments-managing.md#save-close-and-versions) (i sekunder) med konfigurationshanteraren (ConfMgr):

* Nod: `<conf-root>/settings/dam/cfm/jcr:content`
* Egenskapsnamn: `autoSaveInterval`
* Typ: `Long`

* Standard: `600` (10 minuter); detta definieras på `/libs/settings/dam/cfm/jcr:content`

Om du vill ange ett intervall för automatiskt sparande på 5 minuter måste du definiera egenskapen på din nod; till exempel:

* Nod: `/conf/global/settings/dam/cfm/jcr:content`
* Egenskapsnamn: `autoSaveInterval`

* Typ: `Long`

* Värde: `300` (5 minuter motsvarar 300 sekunder)

## Komponenter för sidredigering {#components-for-page-authoring}

Mer information finns i

* [Kärnkomponenter - Innehållsfragmentkomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)  (rekommenderas)
