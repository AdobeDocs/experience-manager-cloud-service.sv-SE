---
title: Ordna sidor
description: Lär dig hur du organiserar din webbplats med AEM.
exl-id: c57096ca-34fe-4b19-98e0-8f3cd43cf24e
source-git-commit: 1a4c5e618adaef99d82a00e1118d1a0f8536fc14
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 2%

---


# Ordna sidor {#creating-and-organizing-pages}

Lär dig hur du organiserar din webbplats med AEM. När du förstår hur du ska ordna sidorna kan du [skapa nya sidor](/help/sites-cloud/authoring/sites-console/creating-pages.md) och [hantera befintliga sidor.](/help/sites-cloud/authoring/sites-console/managing-pages.md)

{{edge-delivery-authoring}}

## Organisera din webbplats {#organizing-your-site}

Som författare måste du ordna webbplatsen inom AEM. Detta innebär att du skapar och namnger innehållssidorna så att:

* Du kan enkelt hitta dem i redigeringsmiljön
* Besökare på webbplatsen kan enkelt hitta dem i publiceringsmiljön

Du kan också använda [mappar](#creating-a-new-folder) för att ordna innehållet.

Strukturen på en webbplats kan ses som ett träd som innehåller dina innehållssidor. Namnen på dessa innehållssidor används för att skapa URL-adresserna, medan rubrikerna visas när sidinnehållet visas.

Följande visar ett exempel från [WKND - självstudiekurs](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) webbplats, där en artikel om skateparker (`la-skateparks`) används:

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

```xml
 /content
 /wknd
  /en
   /music
    /...
   /sports
    /la-skateparks
    /five-gyms-la
    /mountain-bike-routes
   /shopping
    /...
   /art
    /...
   /...
```

Den här strukturen kan visas på [**Webbplatser** konsol,](/help/sites-cloud/authoring/sites-console/introduction.md) där du kan navigera på webbplatsens sidor och utföra åtgärder på sidorna.

## Konventioner för sidnamngivning {#page-naming-conventions}

När du skapar en sida finns det två nyckelfält:

* **[Titel](#title)**:
   * Detta visas för användaren i konsolen och visas överst i sidinnehållet när det redigeras.
   * Detta fält är obligatoriskt.
* **[Namn](#name)**:
   * Detta används för att generera URI.
   * Användarindata för det här fältet är valfria. Om inget anges hämtas namnet från titeln. Se följande avsnitt [Begränsningar för sidnamn och bästa praxis](#page-name-restrictions-and-best-practices) för mer information.

### Begränsningar för sidnamn och bästa praxis {#page-name-restrictions-and-best-practices}

Sidans **titel** och **namn** kan skapas separat men hänger ihop:

* När du skapar en sida är det bara **Titel** fältet är obligatoriskt. Om nej **Namn** anges när sidan skapas, kommer AEM att generera ett namn från de 64 första tecknen i titeln (med den validering som anges nedan). Endast de första 64 tecknen används för att ge stöd åt de bästa sätten med namn på korta sidor.
* Om ett sidnamn anges manuellt av författaren gäller inte gränsen på 64 tecken, men andra tekniska begränsningar på sidnamnets längd kan förekomma.

>[!TIP]
>
>När du definierar ett sidnamn är en bra tumregel att hålla sidnamnet så kort, men så uttrycksfullt och minnesvärt som möjligt så att det blir lätt att förstå för läsaren. Se [Stödlinje för W3C-format](https://www.w3.org/Provider/Style/TITLE.html) för `title` för mer information.
>
>Tänk också på att vissa webbläsare (till exempel äldre versioner av IE) bara kan acceptera URL:er med en viss längd, så det finns också tekniska skäl att hålla sidnamnen korta.

När du skapar en sida AEM [validerar sidnamnet enligt konventionerna](/help/implementing/developing/introduction/naming-conventions.md) som ålagts av AEM och JCR.

Minsta tillåtna tecken är:

* `a` via `z`
* `A` via `Z`
* `0` via `9`
* `_` (understreck)
* `-` (minus/bindestreck)

Fullständig information om alla tillåtna tecken finns i [namnkonventioner](/help/implementing/developing/introduction/naming-conventions.md).

>[!NOTE]
>
>Sidnamnen får innehålla högst 150 tecken.

### Titel {#title}

Om du bara anger en sida **Titel** när du skapar en sida, hämtar AEM sidan **Namn** från denna sträng och [validera namnet enligt konventionerna](/help/implementing/developing/introduction/naming-conventions.md) som ålagts av AEM och JCR.

A **Titel** fält som innehåller ogiltiga tecken accepteras, men det härledda namnet har ogiltiga tecken som ersatts. Till exempel:

| Titel | Härlett namn |
|---|---|
| Schön | `schoen.html` |
| SC%&amp;&#42;ç+ | `sc---c-.html` |

### Namn {#name}

När du anger en sida **Namn** när du skapar en sida, AEM [validerar namnet enligt konventionerna](/help/implementing/developing/introduction/naming-conventions.md) som ålagts av AEM och JCR. Du kan inte skicka ogiltiga tecken i **Namn** fält. När AEM upptäcker ogiltiga tecken markeras fältet med en förklaring.

![Exempel på att ange ett ogiltigt sidnamn](/help/sites-cloud/authoring/assets/organizing-invalid-name.png)

>[!TIP]
>
>Du bör undvika att använda en kod med två bokstäver enligt ISO-639-1 som sidnamn, såvida det inte är en språkrot.
>
>Se [Förbereder innehåll för översättning](/help/sites-cloud/administering/translation/preparation.md) för mer information.

## Mallar {#templates}

I AEM [mall](/help/sites-cloud/authoring/sites-console/templates.md) är en specialiserad typ av sida som används som bas för alla nya sidor som skapas.

Mallen definierar strukturen för en sida, inklusive en miniatyrbild och andra egenskaper. Du kan till exempel ha separata mallar för produktsidor, platskartor och kontaktinformation. Mallar består av [komponenter](#components).

AEM innehåller flera färdiga mallar. Vilka mallar som är tillgängliga beror på den enskilda webbplatsen. Nyckelfälten är:

* **Titel** - Den rubrik som visas på den slutliga webbsidan
* **Namn** - Används vid namn på sidan
* **Mall** - En lista över mallar som kan användas när den nya sidan genereras

## Komponenter {#components}

[Komponenter](/help/implementing/developing/components/overview.md) är de element som AEM tillhandahåller så att du kan lägga till specifika typer av innehåll. AEM innehåller en rad färdiga komponenter som kallas [kärnkomponenterna,](/help/implementing/developing/components/overview.md#core-components) som har omfattande funktionalitet. Några exempel på komponenterna är:

* Text
* Bild
* Titel
* Carousel
* Och många fler

När du har skapat och öppnat en sida kan du [lägga till innehåll med komponenterna](/help/sites-cloud/authoring/page-editor/edit-content.md#inserting-a-component)som är tillgängliga från [komponentwebbläsare](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser).

>[!TIP]
>
>The [Komponentkonsol](/help/sites-cloud/authoring/components-console.md) ge en översikt över komponenterna i instansen.
