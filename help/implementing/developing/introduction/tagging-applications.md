---
title: Bygga in märkord i AEM
description: Arbeta med taggar eller utöka taggar i ett anpassat AEM
exl-id: a106dce1-5d51-406a-a563-4dea83987343
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---

# Bygga in märkord i AEM {#building-tagging-into-aem-applications}

I det här dokumentet beskrivs användningen av

* [API för taggning](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)

som interagerar med

* [Ramverk för taggning](tagging-framework.md)

Mer information om taggning:

* Mer information om hur du taggar innehåll som innehållsförfattare finns i [Använda taggar](/help/sites-cloud/authoring/sites-console/tags.md).
* Se Administrera taggar för administratörens perspektiv om hur du skapar och hanterar taggar, och i vilka innehållstaggar har tillämpats.

## Översikt över taggnings-API {#overview-of-the-tagging-api}

Implementeringen av [taggningsramverket](tagging-framework.md) i AEM tillåter hantering av taggar och tagginnehåll med JCR-API:t. `TagManager` ser till att taggar som anges som värden i strängmatrisegenskapen `cq:tags` inte dupliceras, den tar bort `TagID` som pekar på taggar som inte finns och uppdaterar `TagID` för taggar som flyttas eller sammanfogas. `TagManager` använder en JCR-observationslyssnare som återställer felaktiga ändringar. Huvudklasserna finns i paketet [com.day.cq.ta](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html):

* `JcrTagManagerFactory` - returnerar en JCR-baserad implementering av `TagManager`. Det är referensimplementeringen av taggnings-API:t.
* `TagManager` - gör att du kan matcha och skapa taggar efter sökvägar och namn.
* `Tag` - definierar taggobjektet.

### Hämta en JCR-baserad TagManager {#getting-a-jcr-based-tagmanager}

Om du vill hämta en `TagManager`-instans måste du ha en JCR `Session` och anropa `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

I det typiska Sling-sammanhanget kan du även anpassa dig till en `TagManager` från `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Hämta ett taggobjekt {#retrieving-a-tag-object}

En `Tag` kan hämtas via `TagManager` genom att antingen matcha en befintlig tagg eller skapa en:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

För den JCR-baserade implementeringen, som mappar `Tags` till JCR `Nodes`, kan du direkt använda Sling `adaptTo`-mekanismen om du har resursen (till exempel `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

En tagg kan bara konverteras *från* en resurs (inte en nod), men en tagg kan konverteras *till* både en nod och en resurs:

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Det går inte att direkt anpassa från `Node` till `Tag` eftersom `Node` inte implementerar metoden Sling `Adaptable.adaptTo(Class)`.

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
>Giltiga `RangeIterator` som ska användas är:
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

Taggskräpinsamlaren är en bakgrundstjänst som rensar de dolda och oanvända taggarna. Dolda och oanvända taggar är taggar under `/content/cq:tags` som har en `cq:movedTo`-egenskap och inte används på en innehållsnod. De har ett antal nollor. Genom att använda den här lat borttagningsprocessen behöver inte innehållsnoden (det vill säga egenskapen `cq:tags`) uppdateras som en del av flyttnings- eller sammanfogningsåtgärden. Referenserna i egenskapen `cq:tags` uppdateras automatiskt när egenskapen `cq:tags` uppdateras, till exempel via dialogrutan för sidegenskaper.

Taggskräpinsamlaren körs som standard en gång om dagen. Detta kan konfigureras på:

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## Märkordssökning och tagglista {#tag-search-and-tag-listing}

Sökningen efter taggar och tagglistan fungerar enligt följande:

* Sökningen efter `TagID` söker efter de taggar som har egenskapen `cq:movedTo` inställd på `TagID` och följer genom `cq:movedTo` `TagID`s.
* Om du söker efter taggtiteln genomsöks bara de taggar som inte har någon `cq:movedTo`-egenskap.

## Taggar på olika språk {#tags-in-different-languages}

En tagg `title` kan definieras på olika språk. Sedan läggs en språkkänslig egenskap till i taggnoden. Den här egenskapen har formatet `jcr:title.<locale>`, till exempel `jcr:title.fr` för den franska översättningen. `<locale>` måste vara en ISO-språksträng med gemener och använda understreck (`_`) i stället för bindestreck/tankstreck (`-`), till exempel: `de_ch`.

När taggen **Djur** läggs till på sidan **Produkter** läggs värdet `stockphotography:animals` till i egenskapen `cq:tags` för noden `/content/wknd/en/products/jcr:content`. Översättningen refereras från taggnoden.

API:t på serversidan har lokaliserade `title`-relaterade metoder:

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

För taggning beror lokaliseringen på sammanhanget eftersom taggen `titles` kan visas på sidspråket, på användarspråket eller på något annat språk.

### Lägga till ett nytt språk i dialogrutan Redigera tagg {#adding-a-new-language-to-the-edit-tag-dialog}

I följande procedur beskrivs hur du lägger till ett nytt språk (till exempel finska) i dialogrutan **Taggredigering**:

1. Redigera flervärdesegenskapen `languages` för noden `/content/cq:tags` i **CRXDE**.
1. Lägg till `fi_fi`, som representerar den finska språkversionen, och spara ändringarna.

Finska är nu tillgängligt i taggdialogrutan för sidegenskaperna och i dialogrutan **Redigera tagg** när du redigerar en tagg i konsolen **Taggning**.

>[!NOTE]
>
>Det nya språket måste vara ett av de AEM identifierade språken. Det måste alltså vara tillgängligt som en nod under `/libs/wcm/core/resources/languages`.
