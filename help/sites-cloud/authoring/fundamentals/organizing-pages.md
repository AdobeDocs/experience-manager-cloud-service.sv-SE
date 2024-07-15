---
title: Skapa och ordna sidor
description: Lär dig hur du organiserar din webbplats genom att skapa och hantera sidor med AEM.
exl-id: c57096ca-34fe-4b19-98e0-8f3cd43cf24e
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '2424'
ht-degree: 1%

---


# Skapa och ordna sidor {#creating-and-organizing-pages}

I det här dokumentet beskrivs hur du skapar och hanterar sidor med Adobe Experience Manager Cloud Service så att du sedan kan [skapa innehåll](/help/sites-cloud/authoring/fundamentals/editing-content.md) på dessa sidor.

>[!NOTE]
>
>Ditt konto behöver rätt behörighet för att kunna hantera sidor som att skapa, kopiera, flytta, redigera och ta bort.
>
>Om du råkar ut för problem rekommenderar vi att du kontaktar systemadministratören.

<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to act on pages such as create, copy, move, edit, and delete.
-->

>[!TIP]
>
>Det finns flera [kortkommandon](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) som du kan använda från webbplatskonsolen för att ordna dina sidor mer effektivt.

{{edge-delivery-authoring}}

## Organisera din webbplats {#organizing-your-website}

Som författare måste du ordna din webbplats inom AEM. Detta innebär att du skapar och namnger innehållssidorna så att:

* Du kan enkelt hitta dem i redigeringsmiljön
* Besökare på webbplatsen kan enkelt hitta dem i publiceringsmiljön

Du kan också använda [mappar](#creating-a-new-folder) för att ordna ditt innehåll.

Strukturen på en webbplats kan ses som ett träd som innehåller dina innehållssidor. Namnen på dessa innehållssidor används för att skapa URL-adresserna, medan rubrikerna visas när sidinnehållet visas.

I följande exempel visas ett exempel från webbplatsen [WKND Tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) där du kan få tillgång till en artikel om skateparker ( `la-skateparks`):

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

Den här strukturen kan visas i konsolen **Platser**, där du kan [navigera bland sidorna på webbplatsen](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) och utföra åtgärder på sidorna. Du kan också skapa nya webbplatser och [nya sidor](#creating-a-new-page).

Du kan se grenen uppåt från vägbeskrivningar i sidhuvudsfältet:

![Navigera med vägbeskrivningar](/help/sites-cloud/authoring/assets/organizing-breadcrumbs.png)

### Konventioner för sidnamngivning {#page-naming-conventions}

När du skapar en sida finns det två nyckelfält:

* **[Titel](#title)**:

   * Detta visas för användaren i konsolen och visas överst i sidinnehållet när det redigeras.
   * Detta fält är obligatoriskt.

* **[Namn](#name)**:

   * Detta används för att generera URI.
   * Användarindata för det här fältet är valfria. Om inget anges hämtas namnet från titeln. Mer information finns i följande avsnitt: [Begränsningar för sidnamn och Bästa metoder](#page-name-restrictions-and-best-practices).

#### Begränsningar för sidnamn och bästa praxis {#page-name-restrictions-and-best-practices}

Sidans **titel** och **namn** kan skapas separat men hänger ihop:

* När du skapar en sida krävs bara fältet **Titel**. Om inget **namn** anges när sidan skapas, genererar AEM ett namn från de första 64 tecknen i titeln (observerar valideringen som anges nedan). Endast de första 64 tecknen används för att ge stöd åt de bästa sätten med namn på korta sidor.
* Om ett sidnamn anges manuellt av författaren gäller inte gränsen på 64 tecken, men andra tekniska begränsningar på sidnamnets längd kan förekomma.

>[!TIP]
>
>När du definierar ett sidnamn är en bra tumregel att hålla sidnamnet så kort, men så uttrycksfullt och minnesvärt som möjligt så att det blir lätt att förstå för läsaren. Mer information finns i [W3C-formatguiden](https://www.w3.org/Provider/Style/TITLE.html) för elementet `title` .
>
>Tänk också på att vissa webbläsare (till exempel äldre versioner av IE) bara kan acceptera URL:er med en viss längd, så det finns också tekniska skäl att hålla sidnamnen korta.

När du skapar en sida validerar AEM [sidnamnet enligt konventionerna](/help/implementing/developing/introduction/naming-conventions.md) som AEM och JCR har infört.

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

#### Titel {#title}

Om du bara anger sidan **Rubrik** när du skapar en sida, hämtar AEM sidan **Namn** från den här strängen och [validerar namnet enligt konventionerna](/help/implementing/developing/introduction/naming-conventions.md) som AEM och JCR har infört.

Ett **Title**-fält som innehåller ogiltiga tecken accepteras, men det härledda namnet har de ogiltiga tecknen ersatta. Till exempel:

| Titel | Härlett namn |
|---|---|
| Schön | `schoen.html` |
| SC%&amp;&#42;ç+ | `sc---c-.html` |

#### Namn {#name}

När du anger en sida **Namn** när du skapar en sida, validerar AEM [namnet enligt konventionerna](/help/implementing/developing/introduction/naming-conventions.md) som AEM och JCR tillämpar. Du kan inte skicka ogiltiga tecken i fältet **Namn**. När AEM upptäcker ogiltiga tecken markeras fältet med en förklaring.

![Exempel på att ange ett ogiltigt sidnamn](/help/sites-cloud/authoring/assets/organizing-invalid-name.png)

>[!TIP]
>
>Du bör undvika att använda en kod med två bokstäver enligt ISO-639-1 som sidnamn, såvida det inte är en språkrot.
>
>Mer information finns i [Förbereder innehåll för översättning](/help/sites-cloud/administering/translation/preparation.md).

### Mallar {#templates}

I AEM anger en mall en speciell typ av sida. En mall används som bas för alla nya sidor som skapas.

Mallen definierar strukturen för en sida, inklusive en miniatyrbild och andra egenskaper. Du kan till exempel ha separata mallar för produktsidor, platskartor och kontaktinformation. Mallar består av [komponenter](#components).

AEM innehåller flera färdiga mallar. Vilka mallar som är tillgängliga beror på den enskilda webbplatsen. Nyckelfälten är:

* **Titel**
Titeln som visas på den slutliga webbsidan.

* **Namn**
Används när sidan namnges.

* **Mall**
En lista med mallar som är tillgängliga för att användas när den nya sidan genereras.

>[!TIP]
>
>Om den är konfigurerad på din instans kan [mallskapare skapa mallar med mallredigeraren](/help/sites-cloud/authoring/features/templates.md).

### Komponenter {#components}

Komponenterna är de element som AEM tillhandahåller så att du kan lägga till specifika typer av innehåll. AEM innehåller en rad färdiga komponenter som ger omfattande funktionalitet. Bland dessa finns:

* Text
* Bild
* Titel
* Carousel
* Och många fler

När du har skapat och öppnat en sida kan du [lägga till innehåll med komponenterna](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component), som är tillgängliga från [komponentwebbläsaren](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).

>[!TIP]
>
>[Komponentkonsolen](/help/sites-cloud/authoring/features/components-console.md) ger en översikt över komponenterna i din instans.

## Hantera sidor {#managing-pages}

### Skapa en ny sida {#creating-a-new-page}

Om du inte har skapat alla sidor åt dig i förväg måste du skapa en sida innan du kan börja skapa innehåll:

1. Öppna webbplatskonsolen (till exempel `https://<host>:<port>/sites.html/content`.
1. Navigera till den plats där du vill skapa den nya sidan.
1. Öppna den nedrullningsbara väljaren med **Skapa** i verktygsfältet och välj sedan **Sida** i listan:

   ![Skapa en sida](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. Från det första steget i guiden kan du antingen:

   * Välj den mall som du vill använda för att skapa den nya sidan och välj sedan **Nästa** för att fortsätta.

   * **Avbryt** om du vill avbryta processen.

   ![Välja en mall för en ny sida](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. Från det sista steget i guiden kan du antingen:

   * Använd de tre flikarna för att ange de [sidegenskaper](/help/sites-cloud/authoring/fundamentals/page-properties.md) som du vill tilldela den nya sidan och välj sedan **Skapa** för att skapa sidan.

   * Använd **Bakåt** för att återgå till mallval.

   Nyckelfält är:

   * **Titel**:

      * Detta visas för användaren och är obligatoriskt.

   * **Namn**:

      * Detta används för att generera URI. Om inget anges hämtas namnet från titeln.
      * Om du anger en sida **Namn** när du skapar en sida, validerar AEM [namnet enligt konventionerna](/help/implementing/developing/introduction/naming-conventions.md) som AEM och JCR tillämpar.
      * Du **kan inte skicka ogiltiga tecken** i fältet **Namn**. När AEM upptäcker ogiltiga tecken markeras fältet och en förklaring visas som anger vilka tecken som behöver tas bort/ersättas.

   >[!TIP]
   >
   >Se [Konventioner för sidnamngivning](#page-naming-conventions).

   Den information som krävs för att skapa en sida är **Title**.

   ![Tillhandahåller sidtitel](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. Använd **Skapa** för att slutföra processen och skapa en ny sida. Bekräftelsedialogrutan frågar om du vill **öppna** sidan direkt eller återgå till konsolen (**Klar**):

   ![Sidskapandet lyckades](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   >[!NOTE]
   >
   >Om du skapar en sida med ett namn som redan finns på den platsen, genereras automatiskt en variant av namnet genom att en siffra läggs till. Om `beach` till exempel redan finns blir en ny sida `beach1`.

1. Om du återgår till konsolen kan du se din nya sida:

   ![Resulterande ny sida](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!CAUTION]
>
>När en sida har skapats kan dess mall inte ändras - såvida du inte [skapar en start med en ny mall](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template), men befintligt innehåll går förlorat.

### Öppna en sida för redigering {#opening-a-page-for-editing}

När du har skapat en sida eller navigerat till en befintlig sida (i konsolen) kan du öppna den för redigering:

1. Öppna konsolen **Platser**.
1. Navigera tills du hittar sidan som du vill redigera.
1. Välj sida genom att använda något av följande:

   * [Snabbåtgärder](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Markeringsläge](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) och verktygsfältet

   Välj sedan ikonen **Redigera**:

   ![Knappen Redigera](/help/sites-cloud/authoring/assets/edit.png)

1. Sidan öppnas och du kan [redigera sidan](/help/sites-cloud/authoring/fundamentals/editing-content.md) efter behov.

>[!NOTE]
>
>Du kan bara navigera till andra sidor från sidredigeraren i förhandsgranskningsläget eftersom länkarna inte är aktiva i redigeringsläget.

### Kopiera och klistra in en sida {#copying-and-pasting-a-page}

Du kan kopiera en sida och alla dess undersidor till en ny plats:

1. Navigera i konsolen **Platser** tills du hittar sidan som du vill kopiera.
1. Välj sida med hjälp av:

   * [Snabbåtgärder](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Markeringsläge](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) och verktygsfältet

   Sedan sidikonen **Kopiera**:

   ![Kopiera](/help/sites-cloud/authoring/assets/copy.png)

1. Navigera till den nya kopians plats.
1. Välj ikonen **Klistra in** som blev tillgänglig.

   ![Klistra in](/help/sites-cloud/authoring/assets/paste.png)

1. Dialogrutan Klistra in innehåller en sammanfattning av inklistringstransaktionen och möjlighet att:
   * **Nytt platsnamn:** Ändra den inklistrade sidans namn
   * **Klistra in utan underordnade:** Utelämna de underordnade sidorna på den markerade sidan när du klistrar in (som standard klistras underordnade sidor in)

   ![Dialogrutan Klistra in](/help/sites-cloud/authoring/assets/paste-dialog.png)

1. Välj knappen **Klistra in** för att bekräfta inklistringstransaktionen och skapa nya sidor.

>[!NOTE]
>
>Om du kopierar sidan till en plats där det redan finns en sida med samma namn som originalet, kommer systemet automatiskt att generera en variant av namnet genom att lägga till en siffra. Om `beach` till exempel redan finns blir en ny sida med namnet `beach` `beach1`.

>[!NOTE]
>
>Om du startar inklistringsåtgärden i markeringsläget avslutas den automatiskt så fort sidan kopieras.

### Flytta eller byta namn på en sida {#moving-or-renaming-a-page}

Proceduren för att flytta eller byta namn på en sida är i princip densamma och båda åtgärderna hanteras av guiden Flytta sida. Med den här guiden kan du

* Byta namn på en sida utan att flytta den
* Flytta sidan utan att byta namn på den
* Flytta och byt namn samtidigt

I AEM finns funktioner för att uppdatera interna länkar som refererar till sidan som byter namn/flyttas. Detta kan göras sida för sida för att ge full flexibilitet.

1. Navigera tills du hittar sidan som du vill flytta.
1. Välj sida med hjälp av:

   * [Snabbåtgärder](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Markeringsläge](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) och verktygsfältet

   Välj sedan sidikonen **Flytta**:

   ![Flytta-knapp](/help/sites-cloud/authoring/assets/move.png)

   Guiden Flytta sida öppnas.

1. Från steget **Byt namn** i guiden kan du antingen:

   * Ange det namn du vill att sidan ska ha efter att den har flyttats och välj sedan **Nästa** för att fortsätta.
   * **Avbryt** om du vill avbryta processen.

   ![Flytta och byta namn på sidan](/help/sites-cloud/authoring/assets/move-page-rename.png)

   Sidnamnet kan vara detsamma om du bara flyttar sidan.

   >[!NOTE]
   >
   >Om du flyttar en sida till en plats där det redan finns en sida med samma namn, kommer systemet automatiskt att generera en variant av namnet genom att lägga till en siffra. Om `beach` till exempel redan finns blir en ny sida med namnet `beach` `beach1`.

1. Från **Välj mål**-steget i guiden kan du antingen:

   * Använd [kolumnvyn](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) för att navigera till sidans nya plats:

      * Markera målet genom att klicka på målets miniatyrbild.
      * Klicka på **Nästa** för att fortsätta.

   * Använd **Tillbaka** för att återgå till sidnamnsspecifikationen.

   >[!NOTE]
   >
   >Som standard är den överordnade sidan till sidan som du flyttar eller byter namn på markerad som mål.

   ![Välj mål för sidflyttning](/help/sites-cloud/authoring/assets/move-page-destination.png)

   >[!NOTE]
   >
   >Om du flyttar en sida till en plats där det redan finns en sida med samma namn, kommer systemet automatiskt att generera en variant av namnet genom att lägga till en siffra. Om `winter` till exempel redan finns blir `winter` `winter1`.

1. Om sidan är länkad till eller refererad, eller har publicerats, visas informationen i steget **Justera/Publicera igen**.

   Du kan ange vilka som ska justeras och/eller publiceras på nytt efter behov.

   >[!NOTE]
   >
   >Om sidan varken är länkad till eller refererad är det här steget inte tillgängligt.

   ![Publicera om sida vid flytt](/help/sites-cloud/authoring/assets/move-page-republish.png)

1. Om du väljer **Flytta** slutförs processen och du kan flytta/byta namn på sidan efter behov.

>[!NOTE]
>
>Om sidan redan har publicerats, kommer den att återpubliceras automatiskt när du flyttar den. Som standard publiceras den om när flytten är klar, men detta kan ändras genom att du avmarkerar fältet **Publicera igen** i steget **Justera/Publicera igen**.

>[!NOTE]
>
>Om det inte finns någon referens till sidan på något sätt hoppas steget **Justera/Publicera** över.

>[!NOTE]
>
>Om du byter namn på en sida gäller även [Sidnamngivningskonventioner](#page-naming-conventions) när du anger det nya sidnamnet.

>[!NOTE]
>
>En sida kan bara flyttas till en plats där mallen som sidan baseras på tillåts. Mer information finns i [Malltillgänglighet](/help/implementing/developing/components/templates.md#template-availability).

#### Asynkrona åtgärder {#asynchronous-actions}

Åtgärder för att flytta sidor bearbetas alltid asynkront, vilket gör att användaren kan fortsätta att redigera i gränssnittet utan hinder.

* Användaren måste definiera när den asynkrona åtgärden ska utföras
   * **Nu** startar körningen av det asynkrona jobbet omedelbart.
   * **Senare** låter användaren definiera när det asynkrona jobbet ska starta.

<!--
  ![Asynchronous page move](assets/asynchronous-page-move.png)
-->

Status för asynkrona jobb kan kontrolleras på kontrollpanelen [**Async Jobs Status**](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) på **Global Navigation** > **Tools** > **Operations** > **Jobs**

>[!NOTE]
>
>Mer information om asynkron jobbbearbetning och hur du konfigurerar gränsen för åtgärder för att flytta/byta namn på sidor finns i dokumentet [Asynkrona jobb](/help/operations/asynchronous-jobs.md) i användarhandboken för åtgärder.

### Ta bort en sida {#deleting-a-page}

1. Navigera tills du ser sidan som du vill ta bort.
1. Använd [markeringsläget](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) för att markera önskad sida och använd sedan **Ta bort** i verktygsfältet:

   ![Ta bort-knapp](/help/sites-cloud/authoring/assets/delete.png)

   >[!NOTE]
   >
   >Som en säkerhetsåtgärd är ikonen **Ta bort** inte tillgänglig som en snabbåtgärd.

1. En dialogruta där du tillfrågas om bekräftelse.

   ![Ta bort dialogruta](/help/sites-cloud/authoring/assets/delete-page.png)

   * **Vill du arkivera sidor före borttagning?** - Om det här alternativet är markerat skapas versioner av de sidor som har markerats för borttagning vid borttagning.
      * [Versioner kan återställas vid ett senare datum](/help/sites-cloud/authoring/features/page-versions.md).
      * Det går inte att återställa sidor som tagits bort utan tidigare versioner.
   * **Avbryt** om du vill avbryta åtgärden
   * **Ta bort** för att bekräfta åtgärden:

      * Om sidan inte har några referenser tas sidan bort.
      * Om sidan har referenser visas en meddelanderuta om att det finns referenser till **en eller flera sidor.** Du kan välja **Tvinga borttagning** eller **Avbryt**.

>[!NOTE]
>
>Om en sida redan är publicerad kommer den automatiskt att avpubliceras innan den tas bort.

### Låsa en sida {#locking-a-page}

Du kan [låsa/låsa upp en sida](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page) från en konsol eller när du redigerar en enskild sida. Information om huruvida en sida är låst visas också på båda platserna.

![Lås-knapp](/help/sites-cloud/authoring/assets/lock.png)
![ Knappen Lås upp ](/help/sites-cloud/authoring/assets/unlock.png)

### Skapa en ny mapp {#creating-a-new-folder}

Du kan skapa mappar som hjälper dig att ordna dina filer och sidor.

1. Öppna konsolen **Platser** och navigera till önskad plats.
1. Välj **Skapa** i verktygsfältet för att öppna alternativlistan
1. Välj **Mapp** för att öppna dialogrutan. Här kan du ange **Namn** och **Titel**:

   ![Skapa mapp](/help/sites-cloud/authoring/assets/organizing-create-folder.png)

1. Välj **Skapa** för att skapa mappen.

>[!NOTE]
>
>Mappar omfattas också av [Sidnamngivningskonventioner](#page-naming-conventions) när du anger det nya mappnamnet.

>[!CAUTION]
>
>* Mappar kan bara skapas direkt under **Platser** eller under andra mappar. De kan inte skapas under en sida.
>* Standardåtgärderna för att flytta, kopiera, klistra in, ta bort, publicera, avpublicera och visa/redigera egenskaper kan utföras på en mapp.
>* Det går inte att välja mappar i en live-kopia.
