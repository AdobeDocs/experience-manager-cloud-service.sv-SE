---
title: Bygga in märkord i AEM
description: Arbeta programmatiskt med taggar eller utöka taggar i ett anpassat AEM
translation-type: tm+mt
source-git-commit: ce55065c3ae6a2350ed06811af76477df7c11291
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---


# Bygga in märkord i AEM {#building-tagging-into-aem-applications}

I det här dokumentet beskrivs användningen av

* [API för taggning](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

som interagerar med

* [Ramverk för taggning](tagging-framework.md)

Mer information om taggning:

* Mer information om hur du taggar innehåll som innehållsförfattare finns i [Använda taggar](/help/sites-cloud/authoring/features/tags.md) .
* Se Administrera taggar för en administratörs perspektiv om hur du skapar och hanterar taggar, samt vilka innehållstaggar som har tillämpats.

## Översikt över taggnings-API:t {#overview-of-the-tagging-api}

Implementeringen av [taggningsramverket](tagging-framework.md) i AEM gör det möjligt att hantera taggar och tagginnehåll med JCR-API:t. `TagManager` ser till att taggar som anges som värden i strängarrayegenskapen inte dupliceras, tar bort `cq:tags` dem som pekar på taggar som inte finns och uppdaterar `TagID``TagID`dem för flyttade eller sammanfogade taggar. `TagManager` använder en JCR-observationslyssnare som återställer felaktiga ändringar. Huvudklasserna finns i [com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) -paketet:

* `JcrTagManagerFactory` - returnerar en JCR-baserad implementering av en `TagManager`. Det är referensimplementeringen av taggnings-API:t.
* `TagManager` - gör att du kan lösa och skapa taggar efter sökvägar och namn.
* `Tag` - definierar taggobjektet.

### Hämta en JCR-baserad TagManager {#getting-a-jcr-based-tagmanager}

Om du vill hämta en `TagManager` instans måste du ha en JCR `Session` och anropa `getTagManager(Session)`:

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

En `Tag` tagg kan hämtas via `TagManager`, antingen genom att en befintlig tagg matchas eller genom att en ny skapas:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

För den JCR-baserade implementeringen, som mappar `Tags` till JCR `Nodes`, kan du använda Slings `adaptTo` -mekanism direkt om du har resursen (t.ex. `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

En tagg kan endast konverteras *från* en resurs (inte en nod), men en tagg kan konverteras *till* både en nod och en resurs:

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Det går inte `Node` att direkt anpassa från `Tag` till eftersom `Node` inte implementerar Sling- `Adaptable.adaptTo(Class)` metoden.

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
>Giltig `RangeIterator` att använda:
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

Taggskräpinsamlaren är en bakgrundstjänst som rensar de dolda och oanvända taggarna. Dolda och oanvända taggar är taggar under `/content/cq:tags` som har en `cq:movedTo` egenskap och inte används på en innehållsnod. De har ett antal nollor. Genom att använda den här lat borttagningsprocessen behöver inte innehållsnoden (dvs. egenskapen `cq:tags` ) uppdateras som en del av flyttningen eller sammanfogningen. Referenserna i `cq:tags` egenskapen uppdateras automatiskt när `cq:tags` egenskapen uppdateras, t.ex. via dialogrutan för sidegenskaper.

Taggskräpinsamlaren körs som standard en gång om dagen. Detta kan konfigureras på:

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## Märkordssökning och tagglista {#tag-search-and-tag-listing}

Sökningen efter taggar och tagglistan fungerar enligt följande:

* Sökningen efter `TagID` de taggar som har egenskapen `cq:movedTo` inställd på `TagID` och följer genom `cq:movedTo` `TagID`taggarna.
* Om du söker efter en taggtitel genomsöks bara de taggar som inte har någon `cq:movedTo` egenskap.

## Taggar på olika språk {#tags-in-different-languages}

En tagg `title` kan definieras på olika språk. Sedan läggs en språkkänslig egenskap till i taggnoden. Den här egenskapen har formatet `jcr:title.<locale>`, t.ex. `jcr:title.fr` för den franska översättningen. `<locale>` måste vara en ISO-språksträng med gemener och använd understreck (`_`) i stället för bindestreck/bindestreck (`-`), till exempel: `de_ch`.

När taggen **Djur** till exempel läggs till på sidan **Produkter** läggs värdet `stockphotography:animals` till i egenskapen `cq:tags` för noden `/content/wknd/en/products/jcr:content`. Översättningen refereras från taggnoden.

API:t på serversidan har lokaliserade `title`metoder:

* [`com.day.cq.tagging.Tag`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)
   * `getLocalizedTitle(Locale locale)`
   * `getLocalizedTitlePaths()`
   * `getLocalizedTitles()`
   * `getTitle(Locale locale)`
   * `getTitlePath(Locale locale)`
* [`com.day.cq.tagging.TagManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)
   * `canCreateTagByTitle(String tagTitlePath, Locale locale)`
   * `createTagByTitle(String tagTitlePath, Locale locale)`
   * `resolveByTitle(String tagTitlePath, Locale locale)`

I AEM kan språket hämtas antingen från sidspråket eller från användarspråket.

För taggning beror lokaliseringen på sammanhanget eftersom taggen `titles` kan visas på sidspråket, på användarspråket eller på något annat språk.

### Lägga till ett nytt språk i dialogrutan Redigera tagg {#adding-a-new-language-to-the-edit-tag-dialog}

I proceduren nedan beskrivs hur du lägger till ett nytt språk (t.ex. finska) i dialogrutan **Taggredigering** :

1. I **CRXDE** redigerar du egenskapen multi-value `languages` för noden `/content/cq:tags`.
1. Lägg till `fi_fi`, som representerar den finska språkinställningen, och spara ändringarna.

Finska är nu tillgängligt i taggdialogrutan för sidegenskaperna och i dialogrutan **Redigera tagg** när du redigerar en tagg i **taggningskonsolen** .

>[!NOTE]
>
>Det nya språket måste vara ett av de AEM identifierade språken, dvs. det måste vara tillgängligt som en nod nedan `/libs/wcm/core/resources/languages`.
