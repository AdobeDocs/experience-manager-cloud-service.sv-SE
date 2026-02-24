---
title: Ordna sidor
description: Lär dig hur du organiserar din webbplats med AEM.
badgeSaas: label="AEM Sites" type="Positive" tooltip="Gäller AEM Sites)."
exl-id: c57096ca-34fe-4b19-98e0-8f3cd43cf24e
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 98c0c9b6adbc3d7997bc68311575b1bb766872a6
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 2%

---


# Ordna sidor {#creating-and-organizing-pages}

Lär dig hur du organiserar din webbplats med AEM. När du har förstått hur du behöver ordna sidorna kan du [skapa nya sidor](/help/sites-cloud/authoring/sites-console/creating-pages.md) och [hantera befintliga sidor](/help/sites-cloud/authoring/sites-console/managing-pages.md).

## Organisera din webbplats {#organizing-your-site}

Som författare måste du ordna din webbplats inom AEM. Detta innebär att du skapar och namnger innehållssidorna så att:

* Du kan enkelt hitta dem i redigeringsmiljön
* Besökare på webbplatsen kan enkelt hitta dem i publiceringsmiljön

Du kan också använda [mappar](#creating-a-new-folder) för att ordna ditt innehåll.

Strukturen på en webbplats kan ses som ett träd som innehåller dina innehållssidor. Namnen på dessa innehållssidor används för att skapa URL-adresserna, medan rubrikerna visas när sidinnehållet visas.

I följande exempel visas ett exempel från webbplatsen [WKND Tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) där du kan få tillgång till en artikel om skateparker (`la-skateparks`):

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

Den här strukturen kan visas från [**webbplatskonsolen**](/help/sites-cloud/authoring/sites-console/introduction.md), där du kan navigera bland sidorna på webbplatsen och utföra åtgärder på sidorna.

## Konventioner för sidnamngivning {#page-naming-conventions}

När du skapar en sida finns det två nyckelfält:

* **[Titel](#title)**:
   * Detta visas för användaren i konsolen och visas överst i sidinnehållet när det redigeras.
   * Detta fält är obligatoriskt.
* **[Namn](#name)**:
   * Detta används för att generera URI.
   * Användarindata för det här fältet är valfria. Om inget anges hämtas namnet från titeln. Mer information finns i följande avsnitt: [Begränsningar för sidnamn och Bästa metoder](#page-name-restrictions-and-best-practices).

### Begränsningar för sidnamn och bästa praxis {#page-name-restrictions-and-best-practices}

Sidans **titel** och **namn** kan skapas separat men hänger ihop:

* När du skapar en sida krävs bara fältet **Titel**. Om inget **namn** anges när sidan skapas, genererar AEM ett namn från de 64 första tecknen i titeln (med den validering som anges nedan). Endast de första 64 tecknen används för att ge stöd åt de bästa sätten med namn på korta sidor.
* Om ett sidnamn anges manuellt av författaren gäller inte gränsen på 64 tecken, men andra tekniska begränsningar på sidnamnets längd kan förekomma.

>[!TIP]
>
>När du definierar ett sidnamn är en bra tumregel att hålla sidnamnet så kort, men så uttrycksfullt och minnesvärt som möjligt så att det blir lätt att förstå för läsaren. Mer information finns i [W3C-formatguiden](https://www.w3.org/Provider/Style/TITLE.html) för elementet `title` .
>
>Tänk också på att vissa webbläsare (till exempel äldre versioner av IE) bara kan acceptera URL:er med en viss längd, så det finns också tekniska skäl att hålla sidnamnen korta.

När du skapar en sida validerar AEM [sidnamnet enligt konventionerna](/help/implementing/developing/introduction/naming-conventions.md) från AEM och JCR.

Minsta tillåtna tecken är:

* `a` till `z`
* `A` till `Z`
* `0` till `9`
* `_` (understreck)
* `-` (bindestreck/minustecken)

Fullständig information om alla tillåtna tecken finns i [namnkonventionen](/help/implementing/developing/introduction/naming-conventions.md).

>[!NOTE]
>
>Sidnamnen får innehålla högst 150 tecken.

### Titel {#title}

Om du bara anger sidan **Rubrik** när du skapar en sida, hämtar AEM sidan **Namn** från den här strängen och [validerar namnet enligt konventionerna](/help/implementing/developing/introduction/naming-conventions.md) som AEM och JCR har infört.

Ett **Title**-fält som innehåller ogiltiga tecken accepteras, men det härledda namnet har de ogiltiga tecknen ersatta. Till exempel:

| Titel | Härlett namn |
|---|---|
| Schön | `schoen.html` |
| SC%&amp;&#42;ç+ | `sc---c-.html` |

### Namn {#name}

När du anger en sida **Namn** när du skapar en sida, validerar AEM [namnet enligt konventionerna](/help/implementing/developing/introduction/naming-conventions.md) från AEM och JCR. Du kan inte skicka ogiltiga tecken i fältet **Namn**. När AEM identifierar ogiltiga tecken markeras fältet med en förklaring.

![Exempel på att ange ett ogiltigt sidnamn](/help/sites-cloud/authoring/assets/organizing-invalid-name.png)

>[!TIP]
>
>Du bör undvika att använda en kod med två bokstäver enligt ISO-639-1 som sidnamn, såvida det inte är en språkrot.
>
>Mer information finns i [Förbereder innehåll för översättning](/help/sites-cloud/administering/translation/preparation.md).

## Mallar {#templates}

I AEM är en [mall](/help/sites-cloud/authoring/page-editor/templates.md) en specialiserad sidtyp som används som bas för alla nya sidor som skapas.

Mallen definierar strukturen för en sida, inklusive en miniatyrbild och andra egenskaper. Du kan till exempel ha separata mallar för produktsidor, platskartor och kontaktinformation. Mallar består av [komponenter](#components).

AEM levereras med flera färdiga mallar. Vilka mallar som är tillgängliga beror på den enskilda webbplatsen. Nyckelfälten är:

* **Titel** - Titeln som visas på den slutliga webbsidan
* **Namn** - Används vid namn på sidan
* **Mall** - En lista med mallar som är tillgängliga för användning när den nya sidan genereras

## Komponenter {#components}

[Komponenter](/help/implementing/developing/components/overview.md) är de element som tillhandahålls av AEM så att du kan lägga till specifika typer av innehåll. AEM levereras med en rad färdiga komponenter, som kallas [kärnkomponenterna](/help/implementing/developing/components/overview.md#core-components), som innehåller omfattande funktioner. Några exempel på komponenterna är:

* Text
* Bild
* Titel
* Karusell
* Och många fler

När du har skapat och öppnat en sida kan du [lägga till innehåll med komponenterna](/help/sites-cloud/authoring/page-editor/edit-content.md#inserting-a-component), som är tillgängliga från [komponentwebbläsaren](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser).

>[!TIP]
>
>[Komponentkonsolen](/help/sites-cloud/authoring/components-console.md) ger en översikt över komponenterna i din instans.
