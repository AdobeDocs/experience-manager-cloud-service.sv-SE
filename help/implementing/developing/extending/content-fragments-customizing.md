---
title: Anpassa och utöka innehållsfragment
description: Ett innehållsfragment utökar en standardresurs. Lär dig hur du kan anpassa dem.
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
feature: Developing, Content Fragments
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 0%

---

# Anpassa och utöka innehållsfragment{#customizing-and-extending-content-fragments}

I Adobe Experience Manager as a Cloud Service utökar ett innehållsfragment en standardresurs; se:

* [Skapa och hantera innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md) och [Skapa sidor med innehållsfragment](/help/sites-cloud/authoring/fragments/content-fragments.md) om du vill ha mer information om innehållsfragment.

* [Hantera Assets](/help/assets/manage-digital-assets.md) om du vill ha mer information om standardresurser.

## Arkitektur {#architecture}

De grundläggande [beståndsdelarna](/help/sites-cloud/administering/content-fragments/overview.md#constituent-parts-of-a-content-fragment) i ett innehållsfragment är följande:

* Ett *innehållsfragment* självt
* Den består av ett eller flera *innehållselement*
* Den kan ha en eller flera *innehållsvariationer*

De enskilda innehållsfragmenten baseras på modeller för innehållsfragment:

* Modeller för innehållsfragment definierar strukturen för ett innehållsfragment när det skapas.
* Ett fragment refererar till modellen, så ändringar i modellen kan påverka eller påverka beroende fragment.
* Modeller är inbyggda i datatyper.
* Funktioner för att lägga till nya varianter, och så vidare, måste uppdatera fragmentet därefter.

  >[!NOTE]
  >
  >För att du ska kunna visa/återge ett innehållsfragment måste ditt konto ha `read` behörigheter för modellen.

  >[!CAUTION]
  >
  >Alla ändringar i en befintlig innehållsfragmentmodell kan påverka beroende fragment, vilket kan leda till överblivna egenskaper i dessa fragment.

### Integration av webbplatser med Assets {#integration-of-sites-with-assets}

Content Fragment Management (CFM) ingår i Adobe Experience Manager (AEM) Assets som:

* Innehållsfragment är resurser.
* De använder befintliga Assets-funktioner.
* De är helt integrerade med Assets (administrationskonsoler och så vidare).

Innehållsfragment anses vara en AEM Sites-funktion som:

* De används när du redigerar sidorna.

#### Mappa innehållsfragment till Assets {#mapping-content-fragments-to-assets}

![innehållsfragment till resurser](assets/content-fragment-to-assets.png)

Innehållsfragment, som baseras på en innehållsfragmentmodell, mappas till en enda resurs:

* Allt innehåll lagras under resursens `jcr:content/data`-nod:

   * Elementdata lagras under huvudundernoden:
     `jcr:content/data/master`

   * Variationer lagras under en undernod som har variantens namn:
till exempel `jcr:content/data/myvariation`

   * Data för varje element lagras i respektive undernod som en egenskap med elementnamnet:
Innehållet i elementet `text` lagras till exempel som egenskapen `text` på `jcr:content/data/master`

* Metadata och associerat innehåll lagras under `jcr:content/metadata`
Förutom rubriken och beskrivningen, som inte betraktas som traditionella metadata och lagras på `jcr:content`

#### Resursplats {#asset-location}

Precis som med standardresurser finns ett innehållsavdrag under:

`/content/dam`

#### Tillgångsbehörigheter {#asset-permissions}

Se [Innehållsfragment - Ta bort överväganden](/help/sites-cloud/administering/content-fragments/delete-considerations.md).

#### Funktionsintegrering {#feature-integration}

Integrera med Assets Core:

* Funktionen Content Fragment Management (CFM) bygger på Assets Core.

* CFM har sina egna implementeringar för objekt i vyerna kort, kolumn och lista; dessa plugins finns i de befintliga versionerna av Assets Content Rendering.

* Flera Assets-komponenter har utökats för att passa innehållsfragment.

### Använda innehållsfragment på sidor {#using-content-fragments-in-pages}

>[!CAUTION]
>
>Komponenten [Innehållsfragment är en del av kärnkomponenterna](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=sv-SE). Mer information finns i [Utveckla kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=sv-SE).

Innehållsfragment kan refereras från AEM-sidor, precis som andra resurstyper. AEM tillhandahåller kärnkomponenten **[Content Fragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=sv-SE)** - en [komponent som gör att du kan ta med innehållsfragment på dina sidor](/help/sites-cloud/authoring/fragments/content-fragments.md#adding-a-content-fragment-to-your-page). Du kan också utöka den här kärnkomponenten för **[innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=sv-SE)**.

* Komponenten använder egenskapen `fragmentPath` för att referera till det faktiska innehållsfragmentet. Egenskapen `fragmentPath` hanteras på samma sätt som liknande egenskaper för andra resurstyper, till exempel när innehållsfragmentet flyttas till en annan plats.

* Med komponenten kan du välja den variant som ska visas.

* Du kan också markera ett styckeintervall om du vill begränsa utdata. Det kan till exempel användas för utdata med flera kolumner.

* Komponenten tillåter mellanliggande innehåll:

   * Här kan du placera andra resurser (bilder och så vidare) mellan styckena i det refererade fragmentet.

   * För mellanliggande innehåll:

      * Tänk på risken för instabila referenser. Mellanliggande innehåll (som läggs till när en sida redigeras) har ingen fast relation till stycket som är placerat bredvid det. Om du infogar ett nytt stycke (i innehållsfragmentredigeraren) före placeringen av det mellanliggande innehållet kan den relativa positionen gå förlorad.

      * Tänk på de extra parametrarna (till exempel variant- och styckefilter) för att konfigurera vad som ska återges på sidan.

>[!NOTE]
>
>**Modell för innehållsfragment:**
>
>När ett innehållsfragment används på en sida refereras den innehållsfragmentmodell som det baseras på.
>
>Det innebär att om modellen inte har publicerats när du publicerar sidan, flaggas den och modellen läggs till i resurserna som ska publiceras med sidan.

### Integrering med andra ramar {#integration-with-other-frameworks}

Innehållsfragment kan integreras med:

* **Översättningar**

  Innehållsfragment är helt integrerade med [AEM översättningsarbetsflöde](/help/sites-cloud/administering/translation/overview.md). Arkitekturnivå innebär följande:

   * De enskilda översättningarna av ett innehållsfragment är separata fragment, till exempel:

      * De finns under olika språkrötter, men delar den relativa sökvägen under den relevanta språkroten:

        `/content/dam/<path>/en/<to>/<fragment>`

        jämfört med

        `/content/dam/<path>/de/<to>/<fragment>`

   * Förutom de regelbaserade sökvägarna finns det ingen annan koppling mellan de olika språkversionerna av ett innehållsfragment. De hanteras som två separata fragment, men användargränssnittet ger möjlighet att navigera mellan språkvarianterna.

  >[!NOTE]
  >
  >AEM översättningsarbetsflöde fungerar med `/content`:
  >
  >* Eftersom innehållsfragmentmodellerna finns i `/conf` inkluderas de inte i sådana översättningar. Du kan internationalisera gränssnittssträngarna.

* **Metadata-scheman**

   * Innehållsfragment använder och återanvänder [metadatamodeller](/help/assets/metadata-schemas.md) som kan definieras med standardresurser.

   * CFM har ett eget specifikt schema:

     `/libs/dam/content/schemaeditors/forms/contentfragment`

     Detta kan vid behov förlängas.

   * respektive schemaformulär är integrerat med fragmentredigeraren.

## API för hantering av innehållsfragment - serversidan {#the-content-fragment-management-api-server-side}

Du kan använda serversidans API för att komma åt dina innehållsfragment. Se:

[com.adobe.cq.dam.cfm](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>Adobe rekommenderar att du använder serversidans API i stället för att komma åt innehållsstrukturen direkt.

### Nyckelgränssnitt {#key-interfaces}

Följande tre gränssnitt kan fungera som startpunkter:

* **Innehållsfragment** ([ContentFragment](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

  Med det här gränssnittet kan du arbeta med ett innehållsfragment på ett abstrakt sätt.

  Gränssnittet ger dig möjlighet att

   * Hantera grundläggande data (till exempel get name; get/set title/description)
   * Åtkomst till metadata
   * Åtkomstelement:

      * Listelement
      * Hämta element efter namn
      * Skapa element (se [Caveats](#caveats))

      * Åtkomst till elementdata (se `ContentElement`)

   * Listvarianter definierade för fragmentet
   * Skapa variationer globalt
   * Hantera associerat innehåll:

      * Listsamlingar
      * Lägg till samlingar
      * Ta bort samlingar

   * Åtkomst till fragmentets modell

  Gränssnitt som representerar de primära elementen i ett fragment är:

   * **Innehållselement** ([ContentElement](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Hämta grundläggande data (namn, titel, beskrivning)
      * Hämta/ange innehåll
      * Få åtkomst till varianter av ett element:

         * Listvarianter
         * Hämta varianter efter namn
         * Skapa variationer (se [Caveats](#caveats))
         * Ta bort variationer (se [Caveats](#caveats))
         * Åtkomst till variantdata (se `ContentVariation`)

      * Kortkommando för att matcha variationer (tillämpa ytterligare, implementeringsspecifik reservlogik om den angivna varianten inte är tillgänglig för ett element)

   * **Innehållsvariation** ([ContentVariation](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Hämta grundläggande data (namn, titel, beskrivning)
      * Hämta/ange innehåll
      * Enkel synkronisering, baserat på den senast ändrade informationen

  Alla tre gränssnitten ( `ContentFragment`, `ContentElement`, `ContentVariation`) utökar gränssnittet `Versionable`, som lägger till versionshantering som krävs för innehållsfragment:

   * Skapa en version av elementet
   * Lista versioner av elementet
   * Hämta innehållet i en specifik version av det versionshanterade elementet

### Adapting - Using customito() {#adapting-using-adaptto}

Följande kan anpassas:

* `ContentFragment` kan anpassas till:

   * `Resource` - den underliggande Sling-resursen. Om du uppdaterar den underliggande `Resource` direkt måste du återskapa `ContentFragment`-objektet.

   * `Asset` - DAM `Asset`-förkortningen som representerar innehållsfragmentet. Om du uppdaterar `Asset` direkt måste du återskapa `ContentFragment`-objektet.

* `ContentElement` kan anpassas till:

   * [`ElementTemplate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html) - för åtkomst till elementets strukturinformation.

* [`FragmentTemplate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource` kan anpassas till:

   * `ContentFragment`

### Caveats {#caveats}

Det bör noteras att

* Hela API:t är utformat för att **inte** ska behålla ändringar automatiskt (om inget annat anges i API JavaDoc). Verkställ alltid resurslösaren för respektive begäran (eller den lösare som du använder).

* Uppgifter som kan kräva ytterligare arbete:

   * Adobe rekommenderar att du skapar varianter från `ContentFragment`. Detta garanterar att alla element delar den här variationen och att lämpliga globala datastrukturer uppdateras efter behov för att återspegla den nya variationen i innehållsstrukturen.

   * Om du tar bort befintliga variationer via ett element, med `ContentElement.removeVariation()`, uppdateras inte de globala datastrukturer som är tilldelade variationen. Om du vill vara säker på att de här datastrukturerna är synkroniserade använder du `ContentFragment.removeVariation()` i stället, vilket tar bort en global variant.

## API:t för hantering av innehållsfragment - klientsidan {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>Klientsidans API är internt.

### Ytterligare information {#additional-information}

Se följande:

* `filter.xml`

  `filter.xml` för hantering av innehållsfragment har konfigurerats så att den inte överlappar Assets kärninnehållspaket.

## Redigera sessioner {#edit-sessions}

>[!CAUTION]
>
>Tänk på den här bakgrundsinformationen. Du ska inte ändra någonting här (eftersom det är markerat som ett *privat område* i databasen), men det kan ibland hjälpa att förstå hur saker och ting fungerar under huven.

Att redigera ett innehållsfragment, som kan sträcka sig över flera vyer (= HTML-sidor), är av avgörande betydelse. Eftersom sådana atomiska redigeringsfunktioner för flera vyer inte är ett typiskt AEM-koncept använder innehållsfragment det som kallas *redigeringssession*.

En redigeringssession startas när användaren öppnar ett innehållsfragment i redigeraren. Redigeringssessionen avslutas när användaren lämnar redigeraren genom att välja **Spara** eller **Avbryt**.

Tekniskt sett utförs alla redigeringar på *live*-innehåll, precis som all annan redigering i AEM. När redigeringssessionen startas skapas en version av den aktuella, oredigerade statusen. Om en användare avbryter en redigering återställs den versionen. Om användaren klickar på **Spara** utförs ingenting specifikt eftersom redigeringen kördes på *live* -innehåll, och därför behålls alla ändringar redan. Om du klickar på **Spara** utlöses även en del bakgrundsbearbetning, till exempel att du skapar fullständig textsökningsinformation eller hanterar blandade medieresurser, eller båda.

Det finns vissa säkerhetsåtgärder för kantärenden, till exempel om användaren försöker lämna redigeraren utan att spara eller avbryta redigeringssessionen. Det går även att spara data med jämna mellanrum.
Två användare kan redigera samma innehållsfragment samtidigt och därför skriva över varandras ändringar. För att förhindra detta måste innehållsfragmentet låsas genom att DAM-administrationens *utcheckningsåtgärd* tillämpas på fragmentet.

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

### Exempel: Skapa ett innehållsfragment {#example-creating-a-new-content-fragment}

Om du vill skapa ett innehållsfragment programmatiskt använder du en `FragmentTemplate` som är anpassad från en modellresurs.

Till exempel:

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Exempel: Ange intervall för autosparande {#example-specifying-the-auto-save-interval}

Intervallet [för automatiskt sparande](/help/sites-cloud/administering/content-fragments/managing.md#save-close-and-versions) (mätt i sekunder) kan definieras med konfigurationshanteraren (ConfMgr):

* Nod: `<conf-root>/settings/dam/cfm/jcr:content`
* Egenskapsnamn: `autoSaveInterval`
* Typ: `Long`

* Standard: `600` (10 minuter); detta definieras på `/libs/settings/dam/cfm/jcr:content`

Om du vill ange ett intervall för automatiskt sparande på 5 minuter definierar du egenskapen på noden.

Till exempel:

* Nod: `/conf/global/settings/dam/cfm/jcr:content`
* Egenskapsnamn: `autoSaveInterval`

* Typ: `Long`

* Värde: `300` (5 minuter motsvarar 300 sekunder)

## Komponenter för sidredigering {#components-for-page-authoring}

Mer information finns i

* [Kärnkomponenter - Innehållsfragmentkomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=sv-SE) (rekommenderas)
