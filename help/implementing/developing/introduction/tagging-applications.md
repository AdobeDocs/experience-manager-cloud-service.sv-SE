---
title: Bygga in märkord i AEM
description: Arbeta med taggar eller utöka taggar i ett anpassat AEM
exl-id: a106dce1-5d51-406a-a563-4dea83987343
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 0%

---

# Bygga in märkord i AEM {#building-tagging-into-aem-applications}

I det här dokumentet beskrivs användningen av

* [API för taggning](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)

som interagerar med

* [Ramverk för taggning](tagging-framework.md)

Mer information om taggning:

* Se [Använda taggar](/help/sites-cloud/authoring/features/tags.md) om du vill ha information om hur du taggar innehåll som innehållsförfattare.
* Se Administrera taggar för administratörens perspektiv om hur du skapar och hanterar taggar, och i vilka innehållstaggar har tillämpats.

## Översikt över taggnings-API {#overview-of-the-tagging-api}

Genomförandet av [taggningsramverk](tagging-framework.md) i AEM kan hantera taggar och tagginnehåll med JCR-API:t. `TagManager` ser till att taggar anges som värden på `cq:tags` strängmatrisegenskapen är inte duplicerad, den tar bort `TagID`pekar på taggar och uppdateringar som inte finns `TagID`s för flyttade eller sammanfogade taggar. `TagManager` använder en JCR-observationslyssnare som återställer felaktiga ändringar. Huvudklasserna finns i [com.day.cq.tagging](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html) paket:

* `JcrTagManagerFactory` - returnerar en JCR-baserad implementering av en `TagManager`. Det är referensimplementeringen av taggnings-API:t.
* `TagManager` - gör att du kan lösa och skapa taggar efter sökvägar och namn.
* `Tag` - definierar taggobjektet.

### Hämta en JCR-baserad TagManager {#getting-a-jcr-based-tagmanager}

Så här hämtar du `TagManager` du måste ha en JCR `Session` och ringa `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

I ett typiskt Sling-sammanhang kan du även anpassa dig till en `TagManager` från `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Hämta ett taggobjekt {#retrieving-a-tag-object}

A `Tag` kan hämtas via `TagManager`genom att antingen matcha en befintlig tagg eller skapa en:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

För den JCR-baserade implementeringen, som mappar `Tags` på JCR `Nodes`kan du direkt använda Sling `adaptTo` om du har resursen (till exempel `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Även om en tagg bara kan konverteras *från* en resurs (inte en nod), en tagg kan konverteras *till* både nod och resurs:

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Direkt anpassning från `Node` till `Tag` är inte möjligt eftersom `Node` implementerar inte Sling `Adaptable.adaptTo(Class)` -metod.

### Hämta och ställa in taggar {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### Söker efter taggar {#searching-for-tags}

```java
// Searching for the Resource objects that are tagged with the tag object:
Iterator<Resource> it = tag.find();

// Retrieving the usage count of the tag object:
long count = tag.getCount();

// Searching for the Resource objects that are tagged with the tagID String:
 RangeIterator<Resource> it = tagManager.find(tagID);
```

>[!NOTE]
>
>Giltig `RangeIterator` att använda är:
>
>`com.day.cq.commons.RangeIterator`

### Ta bort taggar {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Replikerar taggar {#replicating-tags}

Det går att använda replikeringstjänsten (`Replicator`) med taggar eftersom taggar är av typen `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## Taggskräpinsamlaren {#the-tag-garbage-collector}

Taggskräpinsamlaren är en bakgrundstjänst som rensar de dolda och oanvända taggarna. Dolda och oanvända taggar anges nedan `/content/cq:tags` som har `cq:movedTo` och används inte på en innehållsnod. De har ett antal nollor. Genom att använda den här lazy delete-processen kan innehållsnoden (dvs. `cq:tags` ) behöver inte uppdateras som en del av flytt- eller sammanfogningsåtgärden. Referenserna i `cq:tags` -egenskapen uppdateras automatiskt när `cq:tags` egenskapen uppdateras till exempel via dialogrutan för sidegenskaper.

Taggskräpinsamlaren körs som standard en gång om dagen. Detta kan konfigureras på:

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## Märkordssökning och tagglista {#tag-search-and-tag-listing}

Sökningen efter taggar och tagglistan fungerar enligt följande:

* Sökningen efter `TagID` söker efter de taggar som har egenskapen `cq:movedTo` ange till `TagID` och följer med `cq:movedTo` `TagID`s.
* Om du söker efter en taggtitel genomsöks bara de taggar som inte har någon `cq:movedTo` -egenskap.

## Taggar på olika språk {#tags-in-different-languages}

En tagg `title` kan definieras på olika språk. Sedan läggs en språkkänslig egenskap till i taggnoden. Den här egenskapen har formatet `jcr:title.<locale>`, till exempel `jcr:title.fr` för den franska översättningen. `<locale>` måste vara en ISO-språksträng med gemener och använda understreck (`_`) i stället för bindestreck/streck (`-`), till exempel: `de_ch`.

När **Djur** -taggen läggs till **Produkter** sida, värdet `stockphotography:animals` läggs till i egenskapen `cq:tags` av noden `/content/wknd/en/products/jcr:content`. Översättningen refereras från taggnoden.

API:t på serversidan har lokaliserats `title`-relaterade metoder:

* [`com.day.cq.tagging.Tag`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/Tag.html)
   * `getLocalizedTitle(Locale locale)`
   * `getLocalizedTitlePaths()`
   * `getLocalizedTitles()`
   * `getTitle(Locale locale)`
   * `getTitlePath(Locale locale)`
* [`com.day.cq.tagging.TagManager`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/TagManager.html)
   * `canCreateTagByTitle(String tagTitlePath, Locale locale)`
   * `createTagByTitle(String tagTitlePath, Locale locale)`
   * `resolveByTitle(String tagTitlePath, Locale locale)`

I AEM kan språket hämtas antingen från sidspråket eller från användarspråket.

För taggning beror lokaliseringen på sammanhanget som tagg `titles` kan visas på sidspråket, på användarspråket eller på något annat språk.

### Lägga till ett nytt språk i dialogrutan Redigera tagg {#adding-a-new-language-to-the-edit-tag-dialog}

I proceduren nedan beskrivs hur du lägger till ett nytt språk (till exempel finska) i **Redigera tagg** dialog:

1. I **CRXDE**, redigera egenskapen för flera värden `languages` av noden `/content/cq:tags`.
1. Lägg till `fi_fi`, som representerar den finska språkinställningen, och spara ändringarna.

Finska är nu tillgängligt i taggdialogrutan för sidegenskaperna och i **Redigera tagg** när du redigerar en tagg i **Taggning** konsol.

>[!NOTE]
>
>Det nya språket måste vara ett av de AEM identifierade språken. Det måste alltså vara tillgängligt som en nod nedan `/libs/wcm/core/resources/languages`.
