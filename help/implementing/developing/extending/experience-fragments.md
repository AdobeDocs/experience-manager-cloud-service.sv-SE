---
title: Experience Fragments
description: Bygg ut Adobe Experience Manager som Cloud Service Experience Fragments.
translation-type: tm+mt
source-git-commit: 625e56efdab2f41026988fb90b72c31ff876db57
workflow-type: tm+mt
source-wordcount: '1660'
ht-degree: 0%

---


# Experience Fragments{#experience-fragments}

## Grundläggande {#the-basics}

En [Experience Fragment](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) är en grupp med en eller flera komponenter, inklusive innehåll och layout, som kan refereras till på sidor.

En Experience Fragment-Överordnad och/eller Variant använder:

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

Eftersom det inte finns någon `/libs/cq/experience-fragments/components/xfpage/xfpage.html` återgår den till

* `sling:resourceSuperType` :  `wcm/foundation/components/page`

## Den vanliga HTML-återgivningen {#the-plain-html-rendition}

Om du använder `.plain.`-väljaren i URL:en kan du komma åt den vanliga HTML-återgivningen.

Det här är tillgängligt från webbläsaren, men det främsta syftet är att tillåta andra program (till exempel webbprogram från tredje part, anpassade mobilimplementeringar) att komma åt innehållet i Experience Fragment direkt, med enbart URL:en.

Den rena HTML-återgivningen lägger till protokoll, värd och kontextsökväg till sökvägar som är:

* av typen: `src`, `href` eller `action`

* eller avsluta med: `-src` eller `-href`

Till exempel:

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>Länkar refererar alltid till publiceringsinstansen. De är avsedda att användas av tredje part, så länken anropas alltid från publiceringsinstansen, inte författaren.

![Oformaterad HTML-återgivning](assets/xf-14.png)

Väljaren för ren återgivning använder en transformator i stället för ytterligare skript. [Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) används som transformator. Detta är konfigurerat på

* `/libs/experience-fragments/config/rewriter/experiencefragments`

## Sociala variationer {#social-variations}

Sociala varianter kan publiceras på sociala medier (text och bild). AEM kan dessa sociala varianter innehålla komponenter, till exempel textkomponenter, bildkomponenter.

Bilden och texten för det sociala inlägget kan hämtas från alla bildresurstyper eller textresurstyper på alla djupnivåer (antingen i byggblocket eller layoutbehållaren).

Sociala variationer möjliggör också byggstenar och tar hänsyn till dem vid sociala åtgärder (i publiceringsmiljön).

För att kunna publicera rätt text och bild i sociala medier måste vissa konventioner respekteras om du utvecklar egna anpassade komponenter.

För detta måste följande egenskaper användas:

* Extrahera bilden

   * `fileReference`
   * `fileName`

* Extrahera texten

   * `text`

Komponenter som inte använder den här konventionen kommer inte att beaktas.

## Mallar för Experience Fragments {#templates-for-experience-fragments}

>[!CAUTION]
>
>***Endast*** redigerbara mallar stöds för Experience Fragments.

<!-- >***Only*** [editable templates](/help/sites-developing/page-templates-editable.md) are supported for Experience Fragments.
-->

När du utvecklar en ny mall för Experience Fragments kan du följa standardmetoderna för en redigerbar mall.

<!-- When developing a new template for Experience Fragments you can follow follow the standard practices for an [editable template](/help/sites-developing/page-templates-editable.md).
-->

Om du vill skapa en upplevelsefragmentmall som identifieras av guiden **Skapa upplevelsefragment** måste du följa någon av dessa regeluppsättningar:

1. Båda:

   1. Mallens resurstyp (den inledande noden) måste ärva från:
      `cq/experience-fragments/components/xfpage`

   1. Och mallens namn måste börja med:
      `experience-fragments`
Detta gör att användare kan skapa upplevelsefragment i /content/experience-fragments som 
`cq:allowedTemplates` i den här mappen innehåller alla mallar som har namn som börjar med  `experience-fragment`. Kunder kan uppdatera den här egenskapen så att den omfattar sina egna namngivningsscheman eller mallplatser.

1. [Tillåtna ](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#configure-allowed-templates-folder) mallar kan konfigureras i Experience Fragments-konsolen.

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

## Experience Fragment Link Rewriter-providern - HTML {#the-experience-fragment-link-rewriter-provider-html}

I AEM kan ni skapa Experience Fragments. An Experience Fragment:

* består av en grupp komponenter tillsammans med en layout,
* kan finnas oberoende av en AEM.

Ett av användningsområdena för sådana grupper är att bädda in innehåll i kontaktpunkter från tredje part, till exempel Adobe Target.

### Standardlänkreskrivning {#default-link-rewriting}

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

Länkutjämnaren används för att fastställa rätt URL:er som behövs när du skapar HTML-versionen av målerbjudandet, som sedan skickas till Adobe Target. Detta är nödvändigt eftersom Adobe Target kräver att alla länkar i Target HTML-erbjudandet är tillgängliga för allmänheten. det innebär att alla resurser som länkarna refererar till, och själva Experience Fragment, måste publiceras innan de kan användas.

När du skapar ett mål-HTML-erbjudande skickas som standard en begäran till en anpassad Sling-väljare i AEM. Den här väljaren kallas `.nocloudconfigs.html`. Som namnet antyder skapas en vanlig HTML-återgivning av ett Experience Fragment, men inte molnkonfigurationer (vilket skulle vara överflödig information).

När du har genererat HTML-sidan ändrar Sling Rewriter-flödet utdata:

1. Elementen `html`, `head` och `body` ersätts med `div`-element. Elementen `meta`, `noscript` och `title` tas bort (de är underordnade element till det ursprungliga `head`-elementet och beaktas inte när det ersätts av `div`-elementet).

   Detta görs för att säkerställa att HTML-målerbjudandet kan inkluderas i målaktiviteter.

2. AEM ändrar alla interna länkar i HTML-koden så att de pekar på en publicerad resurs.

   Om du vill ta reda på vilka länkar som ska ändras följer AEM det här mönstret för attribut för HTML-element:

   1. `src` attributes
   2. `href` attributes
   3. `*-src` attribut (t.ex. data-src, custom-src)
   4. `*-href` attribut (som  `data-href`,  `custom-href`,  `img-href`osv.)

   >[!NOTE]
   >
   >I de flesta fall är de interna länkarna i HTML relativa länkar, men det kan finnas fall när anpassade komponenter tillhandahåller fullständiga URL:er i HTML. Som standard ignorerar AEM dessa fullständigt ifyllda URL:er och gör inga ändringar.

   Länkarna i de här attributen körs via AEM Link Externalizer `publishLink()` för att återskapa URL:en som om den fanns på en publicerad instans, och som sådan, offentligt tillgänglig.

När du använder en körklar implementering bör den process som beskrivs ovan vara tillräcklig för att generera målerbjudandet från Experience Fragment och sedan exportera det till Adobe Target. Det finns dock vissa användningsfall som inte har beaktats i denna process. bland annat följande:

* Samlingsmappning är bara tillgängligt på publiceringsinstansen
* Dispatcher-omdirigeringar

I sådana fall AEM tillhandahåller länkskrivarens providergränssnitt.

### Länkomskrivarens providergränssnitt {#link-rewriter-provider-interface}

För mer komplicerade fall, som inte täcks av [standard](#default-link-rewriting), erbjuder AEM Länkskrivarens providergränssnitt. Det här är ett `ConsumerType`-gränssnitt som du kan implementera i dina paket som en tjänst. Den åsidosätter de ändringar AEM utför på interna länkar i ett HTML-erbjudande som återges från ett Experience Fragment. Med det här gränssnittet kan du anpassa processen för att skriva om interna HTML-länkar så att de passar era affärsbehov.

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

### Så här använder du providergränssnittet för Länkskrivare {#how-to-use-the-link-rewriter-provider-interface}

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

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

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

För den Experience Fragment-variation som påverkas av omskrivningsprocessen fortsätter den sedan att låta tjänsten hantera omskrivningen av länken. Varje gång en länk påträffas i den interna HTML-koden anropas följande metod:

`rewriteLink(String link, String tag, String attribute)`

Som indata tar metoden emot parametrarna:

* `link`
The 
`String` återgivning av länken som bearbetas just nu. Detta är vanligtvis en relativ URL som pekar på resursen på författarinstansen.

* `tag`
Namnet på det HTML-element som bearbetas.

* `attribute`
Det exakta attributnamnet.

Om till exempel systemet Exportera till mål bearbetar det här elementet kan du definiera `CSSInclude` som:

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

Anropet till metoden `rewriteLink()` görs med följande parametrar:

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

När du skapar tjänsten kan du fatta beslut baserat på angivna indata och sedan skriva om länken i enlighet med detta.

Vi vill till exempel ta bort delen `/etc.clientlibs` av URL:en och lägga till den externa domänen. För att förenkla allt anser vi att vi har tillgång till en resurslösare för din tjänst, som i `rewriteLinkExample2`:

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
>Om metoden ovan returnerar `null` lämnar systemet Exportera till mål länken som den är, en relativ länk till en resurs.

#### Prioriteter - getPriority {#priorities-getpriority}

Det är inte ovanligt att flera tjänster behövs för olika typer av upplevelsefragment, eller till och med för att ha en allmän tjänst som hanterar externalisering och mappning för alla Experience Fragments. I dessa fall kan konflikter uppstå om vilken tjänst som ska användas, så AEM ger möjlighet att definiera **prioritet** för olika tjänster. Prioriteringarna anges med hjälp av metoden:

* `getPriority()`

Den här metoden tillåter användning av flera tjänster där metoden `shouldRewrite()` returnerar true för samma Experience Fragment. Tjänsten som returnerar det högsta antalet från sin `getPriority()`metod är den tjänst som hanterar Experience Fragment-variationen.

Du kan till exempel ha en `GenericLinkRewriterProvider` som hanterar den grundläggande mappningen för alla Experience Fragments och när metoden `shouldRewrite()` returnerar `true` för alla Experience Fragment Variations. För flera specifika Experience Fragments kanske du vill ha specialhantering, så i det här fallet kan du ange en `SpecificLinkRewriterProvider` som `shouldRewrite()`-metoden bara returnerar true för vissa Experience Fragment-variationer. För att vara säker på att `SpecificLinkRewriterProvider` är valt att hantera dessa Experience Fragment-variationer måste det i sin `getPriority()`-metod returnera ett högre tal än `GenericLinkRewriterProvider.`