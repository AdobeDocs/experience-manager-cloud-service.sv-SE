---
title: Skapa och ordna sidor
description: Skapa och ordna sidor med AEM
exl-id: c57096ca-34fe-4b19-98e0-8f3cd43cf24e
source-git-commit: 93e0eac6e329c7a0c54cf592b097014d39a8eb17
workflow-type: tm+mt
source-wordcount: '2560'
ht-degree: 5%

---

# Skapa och ordna sidor {#creating-and-organizing-pages}

I det här dokumentet beskrivs hur du skapar och hanterar sidor med Adobe Experience Manager Cloud Service så att du sedan kan [skapa innehåll](/help/sites-cloud/authoring/fundamentals/editing-content.md) på dessa sidor.

>[!NOTE]
>
>Ditt konto behöver rätt behörighet för att kunna utföra åtgärder på sidor som skapa, kopiera, flytta, redigera och ta bort.
>
>Om du råkar ut för problem rekommenderar vi att du kontaktar systemadministratören.

<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to take action on pages such as create, copy, move, edit, and delete.
-->

>[!TIP]
>
>Det finns ett antal [kortkommandon](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) som du kan använda från webbplatskonsolen för att ordna dina sidor mer effektivt.

## Organisera din webbplats {#organizing-your-website}

Som författare måste du ordna din webbplats inom AEM. Detta innebär att du skapar och namnger innehållssidorna så att:

* Du kan enkelt hitta dem i redigeringsmiljön
* Besökare på webbplatsen kan enkelt hitta dem i publiceringsmiljön

Du kan också använda [mappar](#creating-a-new-folder) för att ordna innehållet.

Strukturen på en webbplats kan ses som ett träd som innehåller dina innehållssidor. Namnen på dessa innehållssidor används för att skapa URL-adresserna, medan rubrikerna visas när sidinnehållet visas.

I följande exempel visas ett exempel från [WKND-självstudiekursen](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)-webbplatsen, där du kan komma åt en artikel om skateparker ( `la-skateparks`):

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

Den här strukturen kan visas Från konsolen **Platser**, där du kan [navigera bland sidorna på webbplatsen](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) och utföra åtgärder på sidorna. Du kan också skapa nya webbplatser och [nya sidor](#creating-a-new-page).

Du kan se grenen uppåt från vägbeskrivningar i sidhuvudsfältet:

![Navigera med vägbeskrivningar](/help/sites-cloud/authoring/assets/organizing-breadcrumbs.png)

### Konventioner för sidnamngivning {#page-naming-conventions}

När du skapar en ny sida finns det två nyckelfält:

* **[Titel](#title)**:

   * Detta visas för användaren i konsolen och visas överst i sidinnehållet när det redigeras.
   * Detta fält är obligatoriskt.

* **[Namn](#name)**:

   * Detta används för att generera URI:n.
   * Användarindata för det här fältet är valfria. Om inget anges hämtas namnet från titeln. Mer information finns i följande avsnitt [Begränsningar för sidnamn och bästa praxis](#page-name-restrictions-and-best-practices).

#### Begränsningar för sidnamn och bästa praxis {#page-name-restrictions-and-best-practices}

Sidans **titel** och **namn** kan skapas separat men hänger ihop:

* När du skapar en sida krävs bara fältet **Titel**. Om inget **namn** anges när sidan skapas, kommer AEM att generera ett namn från de första 64 tecknen i titeln (med den validering som anges nedan). Endast de första 64 tecknen används för att ge stöd åt de bästa sätten att använda korta sidnamn.
* Om ett sidnamn anges manuellt av författaren gäller inte gränsen på 64 tecken, men andra tekniska begränsningar på sidnamnets längd kan förekomma.

>[!TIP]
>
>När du definierar ett sidnamn är en bra tumregel att hålla sidnamnet så kort, men så uttrycksfullt och minnesvärt som möjligt så att det blir lätt att förstå för läsaren. Mer information finns i [W3C-formatguiden](https://www.w3.org/Provider/Style/TITLE.html) för `title`-elementet.
>
>Tänk också på att vissa webbläsare (t.ex. äldre versioner av IE) bara kan acceptera URL:er med en viss längd, så det finns också tekniska skäl att hålla sidnamnen korta.

När du skapar en ny sida kommer AEM att [validera sidnamnet enligt konventionerna](/help/implementing/developing/introduction/naming-conventions.md) som AEM och JCR har infört.

Minsta tillåtna tecken är:

* `a` via  `z`
* `A` via  `Z`
* `0` via  `9`
* `_` (understreck)
* `-` (minus/bindestreck)

Fullständig information om alla tillåtna tecken finns i [namnkonventionen](/help/implementing/developing/introduction/naming-conventions.md).

>[!NOTE]
>
>Sidnamnen får innehålla högst 150 tecken.

#### Titel {#title}

Om du bara anger en **sidtitel** när du skapar en ny sida härleds sidans **namn**[ i AEM från den här strängen och namnet valideras enligt konventionerna i AEM och JCR.](/help/implementing/developing/introduction/naming-conventions.md)

Ett **titelfält** som innehåller ogiltiga tecken accepteras, men det härledda namnet kommer att ersätta ogiltiga tecken. Till exempel:

| Titel | Härlett namn |
|---|---|
| Schön | `schoen.html` |
| SC%&amp;*ç+ | `sc---c-.html` |

#### Namn {#name}

När du anger en sida **Namn** när du skapar en ny sida, kommer AEM att [validera namnet enligt konventionerna](/help/implementing/developing/introduction/naming-conventions.md) som AEM och JCR har infört. Du kan inte skicka ogiltiga tecken i fältet **Namn**. När AEM upptäcker ogiltiga tecken markeras fältet med en förklaring.

![Exempel på att ange ett ogiltigt sidnamn](/help/sites-cloud/authoring/assets/organizing-invalid-name.png)

>[!TIP]
>
>Du bör undvika att använda en kod med två bokstäver enligt ISO-639-1 som sidnamn, såvida det inte är en språkrot.
>
>Mer information finns i [Förbereda innehåll för översättning](/help/sites-cloud/administering/translation/preparation.md).

### Mallar {#templates}

I AEM anger en mall en speciell typ av sida. En mall kommer att användas som bas för alla nya sidor som skapas.

Mallen definierar strukturen för en sida, inklusive en miniatyrbild och andra egenskaper. Du kan till exempel ha separata mallar för produktsidor, platskartor och kontaktinformation. Mallar består av [komponenter](#components).

AEM innehåller flera färdiga mallar. Vilka mallar som är tillgängliga beror på den enskilda webbplatsen. Nyckelfälten är:

* **Titel**
Den titel som visas på den slutliga webbsidan.

* **Namn**
Används när sidan namnges.

* ****
MallEn lista med mallar som är tillgängliga för att användas när den nya sidan genereras.

>[!TIP]
>
>Om den är konfigurerad på din instans kan [mallförfattare skapa mallar med mallredigeraren](/help/sites-cloud/authoring/features/templates.md).

### Komponenter {#components}

Komponenterna är de element som AEM tillhandahåller så att du kan lägga till specifika typer av innehåll. AEM innehåller en rad färdiga komponenter som ger omfattande funktionalitet. Bland dessa finns:

* Text
* Bild
* Titel
* Carousel
* Och många fler

När du har skapat och öppnat en sida kan du [lägga till innehåll med komponenterna](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component), som är tillgängliga i [komponentwebbläsaren](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).

>[!TIP]
>
>[Komponentkonsolen](/help/sites-cloud/authoring/features/components-console.md) ger en översikt över komponenterna i din instans.

## Hantera sidor {#managing-pages}

### Skapa en ny sida {#creating-a-new-page}

Om du inte har skapat alla sidor åt dig i förväg måste du skapa en sida innan du kan börja skapa innehåll:

1. Öppna Sites-konsolen (till exempel `https://<host>:<port>/sites.html/content`).
1. Navigera till den plats där du vill skapa den nya sidan.
1. Öppna listrutan med **Skapa** i verktygsfältet och välj sedan **Sida** i listan:

   ![Skapa en sida](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. Från det första steget i guiden kan du antingen:

   * Välj den mall som du vill använda för att skapa den nya sidan och klicka/tryck sedan på **Nästa** för att fortsätta.

   * **Avbryt** om du vill avbryta processen.

   ![Välja en mall för en ny sida](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. Från det sista steget i guiden kan du antingen:

   * Använd de tre flikarna för att ange de [sidegenskaper](/help/sites-cloud/authoring/fundamentals/page-properties.md) som du vill tilldela den nya sidan och klicka/tryck sedan på **Skapa** för att skapa sidan.

   * Använd **Tillbaka** om du vill återgå till mallvalet.

   Nyckelfält är:

   * **Titel**:

      * Detta visas för användaren och är obligatoriskt.
   * **Namn**:

      * Detta används för att generera URI:n. Om inget anges hämtas namnet från titeln.
      * Om du anger en sida **Namn** när du skapar en ny sida, kommer AEM att [validera namnet enligt konventionerna](/help/implementing/developing/introduction/naming-conventions.md) som AEM och JCR har infört.
      * Du **kan inte skicka ogiltiga tecken** i fältet **Namn**. När AEM upptäcker ogiltiga tecken markeras fältet och en förklaring visas som anger vilka tecken som behöver tas bort/ersättas.

   >[!TIP]
   >
   >Se [Konventioner för sidnamngivning](#page-naming-conventions).

   Den information som krävs för att skapa en ny sida är **titeln**.

   ![Ange sidrubrik](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. Använd **Skapa** för att slutföra processen och skapa en ny sida. Bekräftelsedialogrutan frågar om du vill **öppna** sidan direkt eller återgå till konsolen (**Klar**):

   ![Sidskapandet lyckades](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   >[!NOTE]
   >
   >Om du skapar en sida med ett namn som redan finns på den platsen, genereras automatiskt en variant av namnet genom att en siffra läggs till. Om `beach` till exempel redan finns blir en ny sida `beach1`.

1. Om du återgår till konsolen ser du den nya sidan:

   ![Resultat av ny sida](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!CAUTION]
>
>När en sida har skapats kan dess mall inte ändras - såvida du inte [skapar en start med en ny mall](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template), men befintligt innehåll går förlorat.

### Öppna en sida för redigering {#opening-a-page-for-editing}

När du har skapat en sida eller navigerat till en befintlig sida (i konsolen) kan du öppna den för redigering:

1. Öppna konsolen **Platser**.
1. Navigera tills du hittar sidan som du vill redigera.
1. Välj sida genom att använda något av följande:

   * [Snabbåtgärder](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Markeringsläge ](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) och verktygsfältet

   Välj sedan ikonen **Redigera**:

   ![Knappen Redigera](/help/sites-cloud/authoring/assets/edit.png)

1. Sidan öppnas och du kan [redigera sidan](/help/sites-cloud/authoring/fundamentals/editing-content.md) efter behov.

>[!NOTE]
>
>Du kan bara navigera till andra sidor från sidredigeraren i förhandsgranskningsläget eftersom länkarna inte är aktiva i redigeringsläget.

### Kopiera och klistra in en sida {#copying-and-pasting-a-page}

Du kan kopiera en sida och alla dess undersidor till en ny plats:

1. Navigera i konsolen **Platser** tills du hittar sidan som du vill kopiera.
1. Välj sida med någon av följande metoder:

   * [Snabbåtgärder](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Markeringsläge ](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) och verktygsfältet

   Sedan sidikonen **Copy**:

   ![Kopiera](/help/sites-cloud/authoring/assets/copy.png)

1. Navigera till platsen för den nya kopian av sidan.
1. Tryck eller klicka på ikonen **Klistra in** som blev tillgänglig.

   ![Klistra in](/help/sites-cloud/authoring/assets/paste.png)

1. Dialogrutan Klistra in innehåller en sammanfattning av inklistringstransaktionen och möjlighet att:
   * **Nytt platsnamn:** ändra den inklistrade sidans namn
   * **Klistra in utan underordnade:** Uteslut de underordnade sidorna för den markerade sidan när du klistrar in (som standard klistras underordnade sidor in)

   ![Dialogrutan Klistra in](/help/sites-cloud/authoring/assets/paste-dialog.png)

1. Tryck eller klicka på knappen **Klistra in** för att bekräfta inklistringstransaktionen och skapa nya sidor.

>[!NOTE]
>
>Om du kopierar sidan till en plats där det redan finns en sida med samma namn som originalet, kommer systemet automatiskt att generera en variant av namnet genom att lägga till en siffra. Om `beach` redan finns kommer en ny sida med namnet `beach` att bli `beach1`.

>[!NOTE]
>
>Om du startar inklistringsåtgärden i markeringsläget avslutas den automatiskt så fort sidan kopieras.

### Flytta eller byta namn på en sida {#moving-or-renaming-a-page}

Proceduren för att flytta eller byta namn på en sida är i princip densamma och båda åtgärderna hanteras av guiden Flytta sida. Med den här guiden kan du:

* Byta namn på en sida utan att flytta den
* Flytta sidan utan att byta namn på den
* Flytta och byt namn samtidigt

I AEM finns funktioner för att uppdatera interna länkar som refererar till sidan som byter namn/flyttas. Detta kan göras sida för sida för att ge full flexibilitet.

1. Navigera tills du hittar sidan som du vill flytta.
1. Välj sida med någon av följande metoder:

   * [Snabbåtgärder](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Markeringsläge ](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) och verktygsfältet

   Välj sedan sidikonen **Flytta**:

   ![Knappen Flytta](/help/sites-cloud/authoring/assets/move.png)

   Guiden Flytta sida öppnas.

1. Från **Ändra namn**-fasen i guiden kan du antingen:

   * Ange det namn du vill att sidan ska ha efter att den har flyttats och klicka/tryck sedan på **Nästa** för att fortsätta.
   * **Avbryt** om du vill avbryta processen.

   ![Flytta och byta namn på sida](/help/sites-cloud/authoring/assets/move-page-rename.png)

   Sidnamnet kan vara detsamma om du bara flyttar sidan.

   >[!NOTE]
   >
   >Om du flyttar en sida till en plats där det redan finns en sida med samma namn, kommer systemet automatiskt att generera en variant av namnet genom att lägga till en siffra. Om `beach` redan finns kommer en ny sida med namnet `beach` att bli `beach1`.

1. Från **Välj mål**-fasen i guiden kan du antingen:

   * Använd [kolumnvyn](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) för att navigera till sidans nya plats:

      * Markera målet genom att klicka på målets miniatyrbild.
      * Klicka på **Nästa** för att fortsätta.
   * Använd **Tillbaka** för att återgå till sidnamnsspecifikationen.

   >[!NOTE]
   >
   >Som standard väljs den överordnade sidan för sidan som du flyttar/byter namn på som mål.

   ![Välj mål för flyttning av sida](/help/sites-cloud/authoring/assets/move-page-destination.png)

   >[!NOTE]
   >
   >Om du flyttar en sida till en plats där det redan finns en sida med samma namn, kommer systemet automatiskt att generera en variant av namnet genom att lägga till en siffra. Om `winter` till exempel redan finns `winter` blir `winter1`.

1. Om sidan är länkad till eller refererad, eller har publicerats, visas informationen i steget **Justera/Publicera om**.

   Du kan ange vilka som ska justeras och/eller publiceras på nytt efter behov.

   >[!NOTE]
   >
   >Om sidan varken är länkad till eller refererad är det här steget inte tillgängligt.

   ![Publicera om sidan när du flyttar](/help/sites-cloud/authoring/assets/move-page-republish.png)

1. Om du väljer **Flytta** slutförs processen och du flyttar/byter namn på sidan efter behov.

>[!NOTE]
>
>Om sidan redan har publicerats avpubliceras den automatiskt när du flyttar den. Som standard publiceras den om när flytten är klar, men du kan ändra detta genom att avmarkera fältet **Publicera igen** i steget **Justera/publicera igen**.

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

Vanligtvis utförs en åtgärd för att flytta eller byta namn på en sida direkt. Detta betraktas som synkron bearbetning och ytterligare åtgärder i användargränssnittet blockeras tills åtgärden har slutförts.

Om antalet sidor som påverkas ligger över en angiven gräns, kommer åtgärden att bearbetas asynkront, vilket gör att användaren kan fortsätta att redigera i gränssnittet utan att detta hindras av åtgärden för att flytta sidan eller byta namn.

* När du klickar på **Flytta** i det sista steget ovan kontrollerar AEM den konfigurerade gränsen.
* Om antalet sidor som påverkas ligger under gränsen utförs en synkron åtgärd.
* Om antalet sidor som påverkas ligger över gränsen utförs en asynkron åtgärd.
   * Användaren måste definiera när den asynkrona åtgärden ska utföras
      * **Kör** nu det asynkrona jobbet omedelbart.
      * **Med** Laterge kan användaren definiera när det asynkrona jobbet ska starta.

         ![Asynkron flyttning av sida](/help/sites-cloud/authoring/assets/asynchronous-page-move.png)

Status för asynkrona jobb kan kontrolleras i kontrollpanelen [**Async Jobs Status**](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) på **Global navigering** -> **Verktyg** -> **Åtgärder** -> **Jobs**

>[!NOTE]
>
>Mer information om asynkron jobbbearbetning och hur du konfigurerar gränsen för åtgärder för att flytta/byta namn på sidor finns i dokumentet [Asynkrona jobb](/help/operations/asynchronous-jobs.md) i användarhandboken för Operations.

### Ta bort en sida {#deleting-a-page}

1. Navigera tills du ser sidan som du vill ta bort.
1. Använd [markeringsläget](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) för att markera önskad sida och använd sedan **Ta bort** i verktygsfältet:

   ![Knappen Ta bort](/help/sites-cloud/authoring/assets/delete.png)

   >[!NOTE]
   >
   >Som en säkerhetsåtgärd är ikonen **Ta bort** inte tillgänglig som en snabbåtgärd.

1. En dialogruta där du tillfrågas om bekräftelse.

   ![Dialogrutan Ta bort](/help/sites-cloud/authoring/assets/delete-page.png)

   * **Vill du arkivera sidor före borttagning?** - Om det här alternativet är markerat skapas versioner av de sidor som markerats för borttagning när de tas bort.
      * [Versioner kan återställas vid ett senare tillfälle.](/help/sites-cloud/authoring/features/page-versions.md)
      * Det går inte att återställa sidor som tagits bort utan tidigare versioner.
   * **Avbryt** om du vill avbryta åtgärden
   * **Bekräfta åtgärden genom att** ta bort:

      * Om sidan inte har några referenser tas sidan bort.
      * Om sidan innehåller referenser visas ett meddelande om att **en eller flera sidor refereras.** Du kan välja  **Tvinga** borttagning eller  **Avbryt**.

>[!NOTE]
>
>Om en sida redan är publicerad kommer den automatiskt att avpubliceras innan den tas bort.

### Låsa en sida {#locking-a-page}

Du kan [låsa/låsa upp en sida](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page) från en konsol eller när du redigerar en enskild sida. Information om huruvida en sida är låst visas också på båda platserna.

![Lås ](/help/sites-cloud/authoring/assets/lock.png)
![knappLås upp-knapp](/help/sites-cloud/authoring/assets/unlock.png)

### Skapa en ny mapp {#creating-a-new-folder}

Du kan skapa mappar som hjälper dig att ordna dina filer och sidor.

1. Öppna konsolen **Platser** och navigera till önskad plats.
1. Om du vill öppna alternativlistan väljer du **Skapa** i verktygsfältet
1. Välj **Mapp** för att öppna dialogrutan. Här anger du **Namn** och **Titel**:

   ![Skapa mapp](/help/sites-cloud/authoring/assets/organizing-create-folder.png)

1. Välj **Skapa** för att skapa mappen.

>[!NOTE]
>
>Mappar omfattas också av [sidnamngivningskonventionerna](#page-naming-conventions) när du anger det nya mappnamnet.

>[!CAUTION]
>
>* Mappar kan bara skapas direkt under **Platser** eller under andra mappar. De kan inte skapas under en sida.
>* Standardåtgärderna för att flytta, kopiera, klistra in, ta bort, publicera, avpublicera och visa/redigera egenskaper kan utföras på en mapp.
>* Det går inte att välja mappar i en live-kopia.

