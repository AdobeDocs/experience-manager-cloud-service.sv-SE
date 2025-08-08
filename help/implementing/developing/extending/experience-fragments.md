---
title: Översikt över Experience Fragments
description: Utöka upplevelsefragment för Adobe Experience Manager as a Cloud Service
exl-id: bd4ea763-d17c-40a6-9a86-a24d7600229e
feature: Developing, Experience Fragments
role: Admin, Architect, Developer
source-git-commit: bc422429d4a57bbbf89b7af2283b537a1f516ab5
workflow-type: tm+mt
source-wordcount: '1657'
ht-degree: 0%

---

# Upplevelsefragment{#experience-fragments}

## Grunderna {#the-basics}

Ett [Experience Fragment](/help/sites-cloud/authoring/fragments/content-fragments.md) är en grupp med en eller flera komponenter, inklusive innehåll och layout, som kan refereras till på sidor.

En Experience Fragment Master, eller Variant, eller båda, använder:

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

Eftersom det inte finns någon `/libs/cq/experience-fragments/components/xfpage/xfpage.html` återgår den till

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## The Plain HTML Rendition {#the-plain-html-rendition}

Du kan använda väljaren `.plain.` i URL:en för att få åtkomst till den vanliga HTML-återgivningen.

Den här återgivningen är tillgänglig från webbläsaren. Dess främsta syfte är dock att tillåta andra program (till exempel webbprogram från tredje part, anpassade mobilimplementeringar) att komma åt innehållet i Experience Fragment direkt, med enbart URL:en.

Den rena HTML-renderingen lägger till protokoll, värd och kontextsökväg till sökvägar som är:

* av typen: `src`, `href` eller `action`

* eller avslutas med: `-src`, eller `-href`

Till exempel:

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>Länkar refererar alltid till publiceringsinstansen. De är avsedda att användas av tredje part, så länken anropas alltid från publiceringsinstansen, inte författarinstansen.
>
>Mer information finns i [Externalisera URL:er](/help/implementing/developing/tools/externalizer.md).

![Oformaterad HTML-återgivning](assets/xf-14.png)

Väljaren för ren återgivning använder en transformator i stället för ytterligare skript. [Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) används som transformator. Den här transformatorn är konfigurerad på följande sätt:

* `/libs/experience-fragments/config/rewriter/experiencefragments`

### Konfigurera generering av HTML-återgivning {#configuring-html-rendition-generation}

HTML-renderingen genereras med Sling Rewriter-pipelines. Pipelinen definieras på `/libs/experience-fragments/config/rewriter/experiencefragments`. HTML Transformer stöder följande alternativ:

* `allowedCssClasses`
   * Ett RegEx-uttryck som matchar CSS-klasserna som ska lämnas i den slutliga återgivningen.
   * Det här alternativet är användbart om kunden vill ta bort vissa specifika CSS-klasser
* `allowedTags`
   * En lista över HTML-taggar som ska tillåtas i den slutliga återgivningen.
   * Som standard är följande taggar tillåtna (ingen konfiguration behövs): html, head, title, body, img, p, span, ul, li, a, b, i, em, strong, h1, h2, h3, h4, h5, h6, br, noscript, div, link och script

Adobe rekommenderar att omskrivaren konfigureras med en övertäckning. Se [Övertäckningar i AEM as a Cloud Service](/help/implementing/developing/introduction/overlays.md).

## Mallar för Experience Fragments {#templates-for-experience-fragments}

>[!CAUTION]
>
>***Endast*** redigerbara mallar stöds för Experience Fragments.
>
>Upplevelsefragment kan bara användas på sidor som är baserade på redigerbara mallar.

<!-- 
***Only*** [editable templates](/help/sites-developing/page-templates-editable.md) are supported for Experience Fragments.
-->

När du utvecklar en ny mall för Experience Fragments kan du följa standardmetoderna för en redigerbar mall.

<!-- 
When developing a new template for Experience Fragments you can follow the standard practices for an [editable template](/help/sites-developing/page-templates-editable.md).
-->

Om du vill skapa en Experience Fragment-mall som identifieras av guiden **Skapa Experience Fragment** måste du följa någon av dessa regeluppsättningar:

1. Båda:

   1. Mallens resurstyp (den inledande noden) måste ärva från:
      `cq/experience-fragments/components/xfpage`

   1. Och mallens namn måste börja med:
      `experience-fragments`
Med det här mönstret kan användare skapa upplevelsefragment i /content/experience-fragments eftersom egenskapen `cq:allowedTemplates` i den här mappen innehåller alla mallar som har namn som börjar med `experience-fragment` . Kunder kan uppdatera den här egenskapen så att den omfattar sina egna namngivningsscheman eller mallplatser.

1. [Tillåtna mallar](/help/sites-cloud/authoring/fragments/content-fragments.md#configure-allowed-templates-folder) kan konfigureras i Experience Fragments-konsolen.

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- 
>[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## Komponenter för Experience Fragments {#components-for-experience-fragments}

Utveckla komponenter för användning med/i Experience Fragments följer standardrutiner.

Den enda extra konfigurationen är att säkerställa att komponenterna tillåts i mallen. Detta uppnås med innehållspolicyn.

<!--
[Developing components](/help/sites-developing/components.md) for use with/in Experience Fragments follow standard practices.

The only additional configuration is to ensure that the components are [allowed on the template, this is achieved with the Content Policy](/help/sites-developing/page-templates-editable.md#content-policies).
-->

## Experience Fragment Link Rewriter Provider - HTML {#the-experience-fragment-link-rewriter-provider-html}

I AEM kan du skapa Experience Fragments. An Experience Fragment:

* består av en grupp komponenter tillsammans med en layout,
* kan finnas oberoende av en AEM-sida.

Ett av användningsområdena för sådana grupper är att bädda in innehåll i kontaktpunkter från tredje part, som Adobe Target.

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

Länkutjämnaren används för att fastställa rätt URL:er som behövs när du skapar HTML-versionen av målerbjudandet, som sedan skickas till Adobe Target. Denna process är nödvändig eftersom Adobe Target kräver att alla länkar i Target HTML-erbjudandet är tillgängliga för alla. Det innebär att alla resurser som länkarna refererar till, och själva Experience Fragment, måste publiceras innan de kan användas.

Som standard skickas en begäran till en anpassad Sling-väljare i AEM när du skapar ett HTML-erbjudande för mål. Den här väljaren kallas `.nocloudconfigs.html`. Som namnet antyder skapas en ren HTML-återgivning av ett Experience Fragment, men inte molnkonfigurationer (vilket skulle vara överflödig information).

När du har skapat HTML-sidan ändras Sling Rewriter-flödet till utdata:

1. Elementen `html`, `head` och `body` ersätts med elementen `div`. Elementen `meta`, `noscript` och `title` tas bort (de är underordnade element till det ursprungliga `head` -elementet och beaktas inte när de ersätts av `div` -elementet).

   Detta görs för att se till att HTML Target-erbjudandet kan inkluderas i målaktiviteter.

2. AEM ändrar alla interna länkar i HTML så att de pekar på en publicerad resurs.

   För att fastställa vilka länkar som ska ändras följer AEM det här mönstret för attributen för HTML-element:

   1. `src` attribut
   2. `href` attribut
   3. `*-src` attribut (till exempel `data-src` och `custom-src`)
   4. `*-href`-attribut (till exempel `data-href`, `custom-href` och `img-href`)

   >[!NOTE]
   >
   >De interna länkarna i HTML är relativa länkar, men det kan finnas fall när anpassade komponenter tillhandahåller fullständiga URL:er i HTML. Som standard ignorerar AEM dessa fullständiga URL:er och inga ändringar görs.

   Länkarna i de här attributen körs via AEM Link Externalizer `publishLink()` för att återskapa URL:en som om den fanns på en publicerad instans, och som sådan, offentligt tillgänglig.

När du använder en körklar implementering bör den process som beskrivs ovan vara tillräcklig för att generera målerbjudandet från Experience Fragment och sedan exportera det till Adobe Target. Det finns dock vissa användningsfall som inte har beaktats i den här processen. Några av dessa fall som inte har något konto för är:

* Samlingsmappning är bara tillgängligt på publiceringsinstansen
* Dispatcher omdirigerar

I dessa fall tillhandahåller AEM Länkskrivarens providergränssnitt.

### Länk Rewriter-providergränssnitt {#link-rewriter-provider-interface}

För mer komplicerade fall, som inte täcks av [standard](#default-link-rewriting), erbjuder AEM providergränssnittet Länkskrivare. Det här gränssnittet är ett `ConsumerType`-gränssnitt som du kan implementera i dina paket som en tjänst. Den åsidosätter de ändringar AEM utför på interna länkar i ett HTML-erbjudande som återges från en Experience Fragment. Med det här gränssnittet kan du anpassa processen för att skriva om interna HTML-länkar efter företagets behov.

Exempel på användningsområden för implementering av det här gränssnittet som en tjänst är:

* Samlingsmappningar är aktiverade för publiceringsinstanserna, men inte för författarinstansen
* En Dispatcher eller liknande teknik används för att omdirigera URL:er internt
* `sling:alias mechanisms` finns på plats för resurser

>[!NOTE]
>
>Det här gränssnittet bearbetar bara HTML interna länkar från det genererade Target-erbjudandet.

Länkskrivarens providergränssnitt ( `ExperienceFragmentLinkRewriterProvider`) är följande:

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### Så här använder du providergränssnittet Länkskrivare {#how-to-use-the-link-rewriter-provider-interface}

Om du vill använda gränssnittet måste du först skapa ett paket som innehåller en ny tjänstkomponent som implementerar providergränssnittet för Länkskrivare.

Den här tjänsten används för att ansluta till Experience Fragment Export till Target-omskrivning så att den kan komma åt de olika länkarna.

Exempel: `ComponentService`:

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

Ange för systemet om länkarna måste skrivas om när ett anrop görs för Exportera till mål för en viss Experience Fragment-variant. Du kan implementera följande metod:

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

Till exempel:

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

Den här metoden tar som parameter emot Experience Fragment-variationen som systemet Exportera till mål skriver om.

I exemplet ovan vill du skriva om:

* länkar finns i `src`

* Endast `href`-attribut

* för ett specifikt Experience Fragment:
  `/content/experience-fragment/master`

Alla andra Experience Fragments som skickas via systemet Export to Target ignoreras och påverkas inte av ändringar som implementeras i den här tjänsten.

#### rewriteLink {#rewritelink}

För den Experience Fragment-variation som påverkas av omskrivningsprocessen fortsätter den sedan att låta tjänsten hantera omskrivningen av länken. Varje gång en länk påträffas i den interna HTML anropas följande metod:

`rewriteLink(String link, String tag, String attribute)`

Som indata tar metoden emot parametrarna:

* `link`
`String`-representationen av länken som bearbetas. Den här representationen är vanligtvis en relativ URL som pekar på resursen på författarinstansen.

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

När du skapar tjänsten baseras dina beslut på angivna indata och skriver sedan om länken i enlighet med detta.

Du vill till exempel ta bort delen `/etc.clientlibs` i URL:en och lägga till rätt extern domän. Om du vill hålla det enkelt bör du tänka på att du har tillgång till en resurslösare för tjänsten, som i `rewriteLinkExample2`:

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
>Om metoden ovan returnerar `null` lämnar systemet Exportera till mål länken som den är, som en relativ länk till en resurs.

#### Prioriteringar - getPriority {#priorities-getpriority}

Det är inte ovanligt att flera tjänster behövs för olika typer av upplevelsefragment, eller till och med för att ha en allmän tjänst som hanterar externalisering och mappning för alla Experience Fragments. I dessa fall kan konflikter uppstå om vilken tjänst som ska användas, så AEM ger möjlighet att definiera **prioritet** för olika tjänster. Prioriteringarna anges med hjälp av metoden:

* `getPriority()`

Den här metoden tillåter användning av flera tjänster där metoden `shouldRewrite()` returnerar true för samma Experience Fragment. Tjänsten som returnerar det högsta antalet från sin `getPriority()`-metod är den tjänst som hanterar Experience Fragment-variationen.

Du kan till exempel ha en `GenericLinkRewriterProvider` som hanterar den grundläggande mappningen för alla Experience Fragments och när metoden `shouldRewrite()` returnerar `true` för alla Experience Fragment Variations. För flera specifika Experience Fragments kanske du vill ha specialhantering, så i det här fallet kan du ange en `SpecificLinkRewriterProvider` som metoden `shouldRewrite()` bara returnerar true för vissa Experience Fragment-variationer. Om du vill vara säker på att `SpecificLinkRewriterProvider` har valts för att hantera dessa Experience Fragment-variationer måste det returnera ett högre tal i sin `getPriority()`-metod än `GenericLinkRewriterProvider.`
