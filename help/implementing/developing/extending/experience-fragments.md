---
title: Översikt över Experience Fragments
description: Bygg ut Adobe Experience Manager as a Cloud Service Experience Fragments.
exl-id: bd4ea763-d17c-40a6-9a86-a24d7600229e
source-git-commit: 4b76fbbb1b58324065b39d6928027759b0897246
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 0%

---

# Experience Fragments{#experience-fragments}

## Grunderna {#the-basics}

An [Experience Fragment](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) är en grupp med en eller flera komponenter, inklusive innehåll och layout, som kan refereras till på sidor.

En Experience Fragment-Överordnad och/eller Variant använder:

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

Som det inte finns `/libs/cq/experience-fragments/components/xfpage/xfpage.html` återgår till

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## The Plain HTML Rendition {#the-plain-html-rendition}

Använda `.plain.` -väljaren i URL-adressen kan du komma åt den vanliga HTML-återgivningen.

Det här är tillgängligt från webbläsaren, men det främsta syftet är att tillåta andra program (till exempel webbprogram från tredje part, anpassade mobilimplementeringar) att komma åt innehållet i Experience Fragment direkt, med enbart URL:en.

Den rena HTML-renderingen lägger till protokoll, värd och kontextsökväg till sökvägar som är:

* av typen: `src`, `href`, eller `action`

* eller avsluta med: `-src`, eller `-href`

Till exempel:

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>Länkar refererar alltid till publiceringsinstansen. De är avsedda att användas av tredje part, så länken anropas alltid från publiceringsinstansen, inte författaren.

![Rendering HTML](assets/xf-14.png)

Väljaren för ren återgivning använder en transformator i stället för ytterligare skript. den [Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) används som transformator. Detta är konfigurerat på

* `/libs/experience-fragments/config/rewriter/experiencefragments`

## Mallar för Experience Fragments {#templates-for-experience-fragments}

>[!CAUTION]
>
>***Endast*** redigerbara mallar stöds för Experience Fragments.

<!-- >***Only*** [editable templates](/help/sites-developing/page-templates-editable.md) are supported for Experience Fragments.
-->

När du utvecklar en ny mall för Experience Fragments kan du följa standardmetoderna för en redigerbar mall.

<!-- When developing a new template for Experience Fragments you can follow follow the standard practices for an [editable template](/help/sites-developing/page-templates-editable.md).
-->

Skapa en upplevelsefragmentmall som identifieras av **Skapa upplevelsefragment** måste du följa någon av dessa regeluppsättningar:

1. Båda:

   1. Mallens resurstyp (den inledande noden) måste ärva från:
      `cq/experience-fragments/components/xfpage`

   1. Och mallens namn måste börja med:
      `experience-fragments`
Detta gör att användare kan skapa upplevelsefragment i /content/experience-fragments som 
`cq:allowedTemplates` -egenskapen i den här mappen innehåller alla mallar som har namn som börjar med `experience-fragment`. Kunder kan uppdatera den här egenskapen så att den omfattar sina egna namngivningsscheman eller mallplatser.

1. [Tillåtna mallar](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#configure-allowed-templates-folder) kan konfigureras i Experience Fragments-konsolen.

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## Komponenter för Experience Fragments {#components-for-experience-fragments}

Utveckla komponenter för användning med/i Experience Fragments följer standardrutiner.

Den enda ytterligare konfigurationen är att se till att komponenterna tillåts i mallen, vilket uppnås med innehållsprincipen.

<!--
[Developing components](/help/sites-developing/components.md) for use with/in Experience Fragments follow standard practices.

The only additional configuration is to ensure that the components are [allowed on the template, this is achieved with the Content Policy](/help/sites-developing/page-templates-editable.md#content-policies).
-->

## Experience Fragment Link Rewriter Provider - HTML {#the-experience-fragment-link-rewriter-provider-html}

I AEM kan ni skapa Experience Fragments. An Experience Fragment:

* består av en grupp komponenter tillsammans med en layout,
* kan finnas oberoende av en AEM.

Ett av användningsområdena för sådana grupper är att bädda in innehåll i kontaktpunkter från tredje part, till exempel Adobe Target.

### Omskrivning av standardlänk {#default-link-rewriting}

<!--Using the [Export to Target](/help/sites-administering/experience-fragments-target.md) feature, you can:
-->

Med funktionen Exportera till mål kan du:

* skapa en upplevelsefragment,
* lägga till komponenter i den,
* och sedan exportera det som ett Adobe Target-erbjudande, antingen i HTML-format eller JSON-format.

Den här funktionen kan aktiveras för en författarinstans av AEM. Det kräver en giltig Adobe Target-konfiguration och konfigurationer för länkutökningen.

<!--
This feature can be [enabled on an author instance of AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). It requires a valid Adobe Target Configuration, and configurations for the Link Externalizer.
-->

Länkutjämnaren används för att fastställa rätt URL:er som behövs när du skapar målerbjudandets HTML-version, som sedan skickas till Adobe Target. Detta är nödvändigt eftersom Adobe Target kräver att alla länkar i erbjudandet Target HTML ska vara tillgängliga för allmänheten. det innebär att alla resurser som länkarna refererar till, och själva Experience Fragment, måste publiceras innan de kan användas.

När du skapar ett Target-erbjudande skickas som standard en begäran till en anpassad Sling-väljare i AEM. Den här väljaren anropas `.nocloudconfigs.html`. Som namnet antyder skapas en vanlig HTML-återgivning av ett Experience Fragment, men inte molnkonfigurationer (vilket skulle vara överflödig information).

När du har skapat HTML-sidan ändrar Sling Rewriter-flödet utdata:

1. The `html`, `head`och `body` -element ersätts med `div` -element. The `meta`, `noscript` och `title` elementen tas bort (de är underordnade element till originalet) `head` -element och beaktas inte när detta ersätts med `div` element).

   Detta görs för att se till att HTML Target-erbjudandet kan inkluderas i målaktiviteter.

2. AEM ändrar alla interna länkar i HTML så att de pekar på en publicerad resurs.

   AEM här mönstret används för att fastställa vilka länkar som ska ändras:

   1. `src` attributes
   2. `href` attributes
   3. `*-src` attribut (t.ex. data-src, custom-src)
   4. `*-href` attribut (som `data-href`, `custom-href`, `img-href`, etc)

   >[!NOTE]
   >
   >I de flesta fall är de interna länkarna i HTML relativa länkar, men det kan finnas fall när anpassade komponenter tillhandahåller fullständiga URL:er i HTML. Som standard ignorerar AEM dessa fullständigt ifyllda URL:er och gör inga ändringar.

   Länkarna i dessa attribut körs via AEM Link Externalizer `publishLink()` för att återskapa URL:en som om den fanns på en publicerad instans och som sådan offentligt tillgänglig.

När du använder en körklar implementering bör den process som beskrivs ovan vara tillräcklig för att generera målerbjudandet från Experience Fragment och sedan exportera det till Adobe Target. Det finns dock vissa användningsfall som inte har beaktats i denna process. bland annat följande:

* Samlingsmappning är bara tillgängligt på publiceringsinstansen
* Dispatcher-omdirigeringar

I sådana fall AEM tillhandahåller länkskrivarens providergränssnitt.

### Länk Rewriter-providergränssnitt {#link-rewriter-provider-interface}

För mer komplicerade fall omfattas de inte av [standard](#default-link-rewriting), AEM har Link Rewriter Provider Interface. Det här är en `ConsumerType` som ni kan implementera i era paket som en tjänst. Den åsidosätter de ändringar AEM utför på interna länkar för ett HTML-erbjudande som återges från en Experience Fragment. Med det här gränssnittet kan du anpassa processen att skriva om interna HTML-länkar så att de passar era affärsbehov.

Exempel på användningsområden för implementering av det här gränssnittet som en tjänst är:

* Samlingsmappningar är aktiverade för publiceringsinstanserna, men inte för författarinstansen
* En dispatcher eller liknande teknik används för att omdirigera URL:er internt
* Det finns `sling:alias mechanisms` på plats för resurser

>[!NOTE]
>
>Det här gränssnittet bearbetar bara de interna HTML-länkarna från det genererade Target-erbjudandet.

Länkskrivarens providergränssnitt ( `ExperienceFragmentLinkRewriterProvider`) är följande:

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### Så här använder du providergränssnittet Länkskrivare {#how-to-use-the-link-rewriter-provider-interface}

Om du vill använda gränssnittet måste du först skapa ett paket som innehåller en ny tjänstkomponent som implementerar länkskrivarprovidergränssnittet.

Den här tjänsten kommer att användas för att ansluta till Experience Fragment Export till Target för att få tillgång till de olika länkarna.

Till exempel, `ComponentService`:

```java
import com.adobe.cq.xf.ExperienceFragmentLinkRewriterProvider;
import com.adobe.cq.xf.ExperienceFragmentVariation;
import org.osgi.service.component.annotations.Service;
import org.osgi.service.component.annotations.Component;

@Component
@Service
public class GeneralLinkRewriter implements ExperienceFragmentLinkRewriterProvider {

    @Override
    public String rewriteLink(String link, String tag, String attribute) {
        return null;
    }

    @Override
    public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
        return false;
    }

    @Override
    public int getPriority() {
        return 0;
    }

}
```

För att tjänsten ska fungera finns det nu tre metoder som måste implementeras i tjänsten:

* `[shouldRewrite](#shouldrewrite)`
* `[rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* `[getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

Du måste ange för systemet om länkarna behöver skrivas om när du anropar Exportera till mål för en viss Experience Fragment-variation. Detta gör du genom att implementera metoden:

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

Till exempel:

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

Den här metoden tar som parameter emot den Experience Fragment-variation som systemet Exportera till mål för närvarande skriver om.

I exemplet ovan vill vi skriva om:

* länkar finns i `src`

* `href` endast attribut

* för ett specifikt Experience Fragment:
   `/content/experience-fragment/master`

Alla andra Experience Fragments som skickas via systemet Export to Target ignoreras och påverkas inte av ändringar som implementeras i den här tjänsten.

#### rewriteLink {#rewritelink}

För den Experience Fragment-variation som påverkas av omskrivningsprocessen fortsätter den sedan att låta tjänsten hantera omskrivningen av länken. Varje gång en länk påträffas i det interna HTML anropas följande metod:

`rewriteLink(String link, String tag, String attribute)`

Som indata tar metoden emot parametrarna:

* `link`
The 
`String` återgivning av länken som bearbetas just nu. Detta är vanligtvis en relativ URL som pekar på resursen på författarinstansen.

* `tag`
Namnet på det HTML-element som bearbetas.

* `attribute`
Det exakta attributnamnet.

Om till exempel systemet Exportera till mål bearbetar det här elementet kan du definiera `CSSInclude` as:

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

Samtalet till `rewriteLink()` metoden utförs med följande parametrar:

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

När du skapar tjänsten kan du fatta beslut baserat på angivna indata och sedan skriva om länken i enlighet med detta.

Vi vill till exempel ta bort `/etc.clientlibs` del av URL-adressen och lägg till lämplig extern domän. För att förenkla saker och ting anser vi att vi har tillgång till en resurslösare för din tjänst, som i `rewriteLinkExample2`:

>[!NOTE]
>
>Mer information om hur du hämtar en resurslösare via en tjänstanvändare finns i Tjänstanvändare i AEM.

<!--
>For more information on how to get a resource resolver through a service user see [Service Users in AEM](/help/sites-administering/security-service-users.md).
-->

```java
private ResourceResolver resolver;

private Externalizer externalizer;

@Override
public String rewriteLink(String link, String tag, String attribute) {

    // get the externalizer service
    externalizer = resolver.adaptTo(Externalizer.class);
    if(externalizer == null) {
        // if there was an error, then we do not modify the link
        return null;
    }

    // remove leading /etc.clientlibs from resource link before externalizing
    link = link.replaceAll("/etc.clientlibs", "");

    // considering that we configured our publish domain, we directly apply the publishLink() method
    link = externalizer.publishLink(resolver, link);

    return link;
}
```

>[!NOTE]
>
>Om ovanstående metod returnerar `null`lämnar Export till Target-systemet länken som den är, en relativ länk till en resurs.

#### Prioriteringar - getPriority {#priorities-getpriority}

Det är inte ovanligt att flera tjänster behövs för olika typer av upplevelsefragment, eller till och med för att ha en allmän tjänst som hanterar externalisering och mappning för alla Experience Fragments. I dessa fall kan konflikter uppstå om vilken tjänst som ska användas, så AEM ger möjlighet att definiera **Prioriteringar** för olika tjänster. Prioriteringarna anges med hjälp av metoden:

* `getPriority()`

Den här metoden tillåter användning av flera tjänster där `shouldRewrite()` returnerar true för samma Experience Fragment. Tjänsten som returnerar det högsta talet från sin `getPriority()`-metoden är den tjänst som hanterar Experience Fragment-variationen.

Du kan till exempel ha en `GenericLinkRewriterProvider` som hanterar den grundläggande mappningen för alla Experience Fragments och när `shouldRewrite()` metodreturer `true` för alla Experience Fragment Variations. För flera specifika Experience Fragments kanske du vill ha specialhantering, så i det här fallet kan du ange en `SpecificLinkRewriterProvider` som `shouldRewrite()` metoden returnerar bara true för vissa Experience Fragment-variationer. Se till att `SpecificLinkRewriterProvider` väljs för att hantera dessa Experience Fragment-variationer, måste returneras i `getPriority()` metod ett högre tal än `GenericLinkRewriterProvider.`
