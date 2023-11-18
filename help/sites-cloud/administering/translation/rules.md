---
title: Identifiera innehåll som ska översättas
description: Lär dig hur översättningsregler identifierar innehåll som behöver översättas.
feature: Language Copy
role: Admin
exl-id: 24cc6aa6-5b3c-462b-a10a-8b25277229dc
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1288'
ht-degree: 0%

---

# Identifiera innehåll som ska översättas {#identifying-content-to-translate}

Översättningsregler identifierar innehållet som ska översättas för sidor, komponenter och resurser som ingår i, eller utesluts från, översättningsprojekt. När en sida eller resurs översätts extraherar AEM innehållet så att det kan skickas till översättningstjänsten.

>[!TIP]
>
>Om du inte är van vid att översätta innehåll, se [Sites Translation Journey,](/help/journey-sites/translation/overview.md) som vägleder dig genom att översätta ditt AEM Sites-innehåll med AEM kraftfulla översättningsverktyg, idealiskt för dem som saknar AEM eller översättningsupplevelse.

## Innehållsfragment och översättningsregler {#content-fragments}

Översättningsreglerna som beskrivs i det här dokumentet gäller endast för innehållsfragment om **Aktivera fält för innehållsmodell för översättning** har inte aktiverats på [konfigurationsnivå för översättningsintegreringsramverk.](integration-framework.md#assets-configuration-properties)

Om **Aktivera fält för innehållsmodell för översättning** är aktivt, AEM använder **Översättningsbar** fält på [Modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#properties) för att avgöra om fältet ska översättas och skapar automatiskt översättningsregler i enlighet med detta. Det här alternativet ersätter eventuella översättningsregler som du har skapat och kräver inga åtgärder eller ytterligare steg.

Om du vill använda översättningsregler för översättning av dina innehållsfragment, **Aktivera fält för innehållsmodell för översättning** för konfiguration av översättningsintegreringsramverk måste vara inaktiverat och du måste följa stegen nedan för att skapa reglerna.

## Översikt {#overview}

Sidor och resurser representeras som noder i JCR-databasen. Innehållet som extraheras är ett eller flera egenskapsvärden för noderna. Översättningsregler identifierar de egenskaper som innehåller innehållet som ska extraheras.

Översättningsreglerna uttrycks i XML-format och lagras på följande platser:

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

Filen gäller för alla översättningsprojekt.

Reglerna innehåller följande information:

* Sökvägen till noden som regeln gäller för
   * Regeln gäller även för nodens underordnade noder.
* Namnen på nodegenskaperna som innehåller innehållet som ska översättas
   * Egenskapen kan vara specifik för en viss resurstyp eller för alla resurstyper.

Du kan till exempel skapa en regel som översätter innehållet som författare lägger till i alla textkomponenter på sidorna. Regeln kan identifiera `/content` noden och `text` -egenskapen för `core/wcm/components/text/v2/text` -komponenten.

Det finns en [konsol](#translation-rules-ui) som har lagts till för att konfigurera översättningsregler. Definitionerna i användargränssnittet fyller i filen åt dig.

En översikt över funktionerna för innehållsöversättning i AEM finns på [Översätta innehåll för flerspråkiga webbplatser](overview.md).

>[!NOTE]
>
>AEM har stöd för 1:1-mappning mellan resurstyper och referensattribut för översättning av refererat innehåll på en sida.

## Regelsyntax för sidor, komponenter och resurser {#rule-syntax-for-pages-components-and-assets}

En regel är en `node` element med ett eller flera underordnade `property` element och noll eller fler underordnade `node` element:

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

Alla dessa `node` elementen har följande egenskaper:

* The `path` -attributet innehåller sökvägen till rotnoden för grenen som reglerna gäller för.
* Underordnad `property` element identifierar de nodegenskaper som ska översättas för alla resurstyper:
   * The `name` -attributet innehåller egenskapsnamnet.
   * Valfritt `translate` attribute equals `false` om egenskapen inte är översatt. Som standard är värdet `true`. Det här attributet är användbart när du åsidosätter tidigare regler.
* Underordnad `node` element identifierar de nodegenskaper som ska översättas för specifika resurstyper:
   * The `resourceType` -attributet innehåller sökvägen som matchar komponenten som implementerar resurstypen.
   * Underordnad `property` element identifierar den nodegenskap som ska översättas. Använd den här noden på samma sätt som den underordnade noden `property` -element för nodregler.

Följande exempelregel orsakar innehållet i alla `text` egenskaper som ska översättas för alla sidor under `/content` nod. Regeln gäller för alla komponenter som lagrar innehåll i en `text` -egenskap, till exempel textkomponenten.

```xml
<node path="/content">
          <property name="text"/>
</node>
```

I följande exempel översätts innehållet i alla `text` och översätter även andra egenskaper i bildkomponenten. Om andra komponenter har egenskaper med samma namn gäller regeln inte för dem.

```xml
<node path="/content">
      <property name="text"/>
      <node resourceType="core/wcm/components/image/v2/image">
         <property name="image/alt"/>
         <property name="image/jcr:description"/>
         <property name="image/jcr:title"/>
      </node>
</node>
```

## Regelsyntax för att extrahera resurser från sidor  {#rule-syntax-for-extracting-assets-from-pages}

Använd följande regelsyntax för att inkludera resurser som är inbäddade i eller refererade från komponenter:

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

Varje `assetNode` -elementet har följande egenskaper:

* Ett `resourceType` attribut som är lika med sökvägen som matchar komponenten
* Ett `assetReferenceAttribute` attribut som är lika med namnet på egenskapen som lagrar resursens binära (för inbäddade resurser) eller sökvägen till den refererade resursen

I följande exempel extraheras bilder från bildkomponenten:

```xml
<assetNode resourceType="core/wcm/components/image/v2/image" assetReferenceAttribute="fileReference"/>
```

## Åsidosätta regler {#overriding-rules}

The `translation_rules.xml` filen består av en `nodelist` element med flera underordnade `node` -element. AEM läser nodlistan uppifrån och ned. När flera regler har samma nod som mål används den regel som är lägre i filen. Följande regler skapar till exempel allt innehåll i `text` egenskaper som ska översättas förutom för `/content/mysite/en` sidförgrening:

```xml
<nodelist>
     <node path="/content">
           <property name="text" />
     </node>
     <node path="/content/mysite/en">
          <property name="text" translate="false" />
     </node>
<nodelist>
```

## Filteregenskaper {#filtering-properties}

Du kan filtrera noder som har en viss egenskap med en `filter` -element.

Följande regler skapar till exempel allt innehåll i `text` egenskaper som ska översättas, förutom de noder som har egenskapen `draft` ange till `true`.

```xml
<nodelist>
    <node path="/content">
     <filter>
   <node containsProperty="draft" propertyValue="true" />
     </filter>
        <property name="text" />
    </node>
<nodelist>
```

## Gränssnitt för översättningsregler {#translation-rules-ui}

Det finns även en konsol för att konfigurera översättningsregler.

Så här kommer du åt den:

1. Navigera till **verktyg** och sedan **Allmänt**.

1. Välj **Översättningskonfiguration**.

I översättningsregelgränssnittet kan du:

1. **Lägg till kontext** så att du kan lägga till en bana.

   ![Lägg till översättningskontext](../assets/add-translation-context.png)

1. Använd sökvägsläsaren för att välja önskad kontext och markera **Bekräfta** knappen som ska sparas.

   ![Välj kontext](../assets/select-context.png)

1. Sedan måste du markera kontexten och sedan klicka **Redigera**. Då öppnas redigeraren för översättningsregler.

   ![Redigerare för översättningsregler](../assets/translation-rules-editor.png)

Det finns fyra attribut som du kan ändra via gränssnittet:

* `isDeep`
* `inherit`
* `translate`
* `updateDestinationLanguage`

### isDeep {#isdeep}

**`isDeep`**  används på nodfilter och är true som standard. Den kontrollerar om noden (eller dess överordnade noder) innehåller den egenskapen med det angivna egenskapsvärdet i filtret. Om värdet är false kontrolleras endast den aktuella noden.

Underordnade noder läggs till i ett översättningsjobb även om den överordnade noden har egenskapen `draftOnly` inställd på true för att flagga utkastinnehåll. Här `isDeep` spelas upp och kontrollerar om de överordnade noderna har en egenskap `draftOnly` som true och exkluderar dessa underordnade noder.

I redigeraren kan du markera/avmarkera **Är djup** i **Filter** -fliken.

![Filterregler](../assets/translation-rules-editor-filters.png)

Här är ett exempel på den resulterande XML-koden när **Är djup** är avmarkerad i användargränssnittet:

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

### ärva {#inherit}

**`inherit`** används för egenskaper. Som standard ärvs alla egenskaper, men om du vill att vissa egenskaper inte ska ärvas av den underordnade kan du markera den här egenskapen som false så att den bara tillämpas på den specifika noden.

I användargränssnittet kan du checka in/avmarkera **Inherit** i **Egenskaper** -fliken.

### translate {#translate}

**`translate`** används bara för att ange om en egenskap ska översättas eller inte.

I användargränssnittet kan du checka in/avmarkera **Översätt** i **Egenskaper** -fliken.

### updateDestinationLanguage {#updatedestinationlanguage}

**`updateDestinationLanguage`** används för egenskaper som inte har text men språkkoder, till exempel `jcr:language`. Användaren översätter inte text utan språkinställningen från källan till målet. Sådana egenskaper skickas inte för översättning.

I användargränssnittet kan du checka in/avmarkera **Översätt** i **Egenskaper** om du vill ändra det här värdet, men för de specifika egenskaper som har språkkoder som värde.

Förtydliga skillnaden mellan `updateDestinationLanguage` och `translate`Här följer ett enkelt exempel på ett sammanhang med bara två regler:

![updateDestinationLanguage-exempel](../assets/translation-rules-updatedestinationlanguage.png)

Resultatet i xml kommer att se ut så här:

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## Redigera regelfilen manuellt {#editing-the-rules-file-manually}

The `translation_rules.xml` filen som installeras med AEM innehåller en standarduppsättning med översättningsregler. Du kan redigera filen så att den uppfyller översättningsprojektens krav. Du kan till exempel lägga till regler så att innehållet i dina anpassade komponenter översätts.

Om du redigerar `translation_rules.xml` sparar du en säkerhetskopia i ett innehållspaket. Om du installerar om vissa AEM-paket kan det ersätta den aktuella `translation_rules.xml` med originalfilen. Om du vill återställa reglerna i den här situationen kan du installera det paket som innehåller säkerhetskopian.

>[!NOTE]
>
>När du har skapat innehållspaketet återskapar du paketet varje gång du redigerar filen.

## Exempel på översättningsregelfil {#example-translation-rules-file}

```xml
<?xml version="1.0" encoding="UTF-8"?><nodelist>
  <node path="/content">
    <property name="addLabel"/>
    <property name="allowedResponses"/>
    <property name="alt"/>
    <property name="attachFileLabel"/>
    <property name="benefits"/>
    <property name="buttonLabel"/>
    <property name="chartAlt"/>
    <property name="confirmationMessageToggle"/>
    <property name="confirmationMessageUntoggle"/>
    <property name="constraintMessage"/>
    <property name="contentLabel"/>
    <property name="denyText"/>
    <property name="detailDescription"/>
    <property name="emptyText"/>
    <property name="helpMessage"/>
    <property name="image/alt"/>
    <property name="image/jcr:description"/>
    <property name="image/jcr:title"/>
    <property name="jcr:description"/>
    <property name="jcr:title"/>
    <property name="heading"/>
    <property name="label"/>
    <property name="main"/>
    <property name="listLabel"/>
    <property name="moreText"/>
    <property name="pageTitle"/>
    <property name="placeholder"/>
    <property name="requiredMessage"/>
    <property name="resetTitle"/>
    <property name="subjectLabel"/>
    <property name="subtitle"/>
    <property name="tableData"/>
    <property name="text"/>
    <property name="title"/>
    <property name="navTitle"/>
    <property name="titleDivContent"/>
    <property name="toggleLabel"/>
    <property name="transitionLabel"/>
    <property name="untoggleLabel"/>
    <property name="name"/>
    <property name="occupations"/>
    <property name="greetingLabel"/>
    <property name="signInLabel"/>
    <property name="signOutLabel"/>
    <property name="pretitle"/>
    <property name="cq:panelTitle"/>
    <property name="actionText"/>
    <property name="cq:language" updateDestinationLanguage="true"/>
    <node pathContains="/cq:annotations">
      <property name="text" translate="false"/>
    </node>
    <node path="/content/wknd"/>
  </node>
  <node path="/content/forms">
    <property name="text" translate="false"/>
  </node>
  <node path="/content/dam">
    <property name="dc:description"/>
    <property name="dc:rights"/>
    <property name="dc:subject"/>
    <property name="dc:title"/>
    <property name="defaultContent"/>
    <property name="jcr:description"/>
    <property name="jcr:title"/>
    <property name="pdf:Title"/>
    <property name="xmpRights:UsageTerms"/>
    <property name="main"/>
    <property name="adventureActivity"/>
    <property name="adventureDescription"/>
    <property name="adventureDifficulty"/>
    <property name="adventureGearList"/>
    <property name="adventureGroupSize"/>
    <property name="adventureItinerary"/>
    <property name="adventurePrice"/>
    <property name="adventureTitle"/>
    <property name="adventureTripLength"/>
    <property name="adventureType"/>
    <node pathContains="/jcr:content/metadata/predictedTags">
      <property name="name"/>
    </node>
  </node>
  <assetNode assetReferenceAttribute="fragmentPath" resourceType="cq/experience-fragments/editor/components/experiencefragment"/>
  <assetNode assetReferenceAttribute="fragmentVariationPath" resourceType="core/wcm/components/experiencefragment/v1/experiencefragment"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="dam/cfm/components/contentfragment"/>
  <assetNode resourceType="docs/components/download"/>
  <assetNode resourceType="docs/components/image"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="foundation/components/image"/>
  <assetNode assetReferenceAttribute="asset" resourceType="foundation/components/video"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="foundation/components/download"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="core/wcm/components/download/v1/download"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="wcm/foundation/components/image"/>
  <assetNode assetReferenceAttribute="fragmentPath" resourceType="core/wcm/components/contentfragment/v1/contentfragment"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="core/wcm/components/image/v2/image"/>
</nodelist>
```
