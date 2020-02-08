---
title: Skapa startprogram
description: Du kan skapa en startsida som gör det möjligt att uppdatera en ny version av befintliga webbsidor för framtida aktivering.
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Skapa startprogram {#creating-launches}

Skapa en startsida för att möjliggöra uppdatering av en ny version av befintliga webbsidor för framtida aktivering. När du skapar en Launch anger du en titel och källsidan:

* Titeln visas på [fliken Referenser](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) , där författare kan komma åt dem för att arbeta med dem.
* Källsidans underordnade sidor inkluderas som standard i starten. Du kan bara använda källsidan om du vill.
* Som standard uppdateras startsidorna automatiskt när källsidorna ändras. Du kan ange att en statisk kopia ska skapas för att förhindra automatiska ändringar. <!--By default, [Live Copy](/help/sites-administering/msm.md) automatically updates the launch pages as the source pages change. You can specify that a static copy is created to prevent automatic changes.-->

Du kan också ange **startdatum** (och starttid) för att definiera när startsidorna ska befordras och aktiveras. Startdatumet **** fungerar dock endast i kombination med flaggan **Production Ready** (se [Redigera en startkonfiguration](/help/sites-cloud/authoring/launches/editing.md#editing-a-launch-configuration)). för att åtgärderna ska inträffa automatiskt måste båda anges.

## Skapa en Launch {#creating-a-launch}

Du kan skapa en start från Sites- eller Launches-konsolen:

1. Öppna konsolen **Platser** eller **Startar** .

   >[!NOTE]
   >
   >När du använder **Sites** Console är det vanligt att navigera till källsidans plats, men det är inte obligatoriskt eftersom du kan navigera när du väljer **Startkälla** i guiden.

1. Beroende på vilken konsol du använder:
   * **Startar**:
      1. Välj **Skapa start** i verktygsfältet för att öppna guiden.
   * **Webbplatser**:
      1. Välj **Skapa** i verktygsfältet för att öppna markeringsrutan.
      1. Välj **Skapa start** för att öppna guiden.
   >[!NOTE]
   >
   >I **webbplatskonsolen** kan du även använda [markeringsläget](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) för att välja en sida innan du väljer **Skapa**.
   >
   >Då används den valda sidan som den ursprungliga källsidan.

1. I steget **Välj källa** måste du **lägga till sidor**. Du kan markera flera sidor och ange sökvägen för varje sida:
   * Navigera till önskad plats.
   * Markera källsidorna och bekräfta (bockmarkering).
   Upprepa efter behov.

   ![Välj startkälla](/help/sites-cloud/authoring/assets/launches-select-source.png)

   >[!NOTE]
   >
   >Om du vill lägga till sidor och/eller grenar i en lansering måste de finnas på en webbplats. dvs. under en gemensam toppnivårot.
   >
   >Om en webbplats innehåller språkrötter under den översta nivån måste sidorna och grenarna för en start ligga under en gemensam språkrot.

1. För varje tävlingsbidrag kan du ange om du vill:

   * **Inkludera undersidor**:

      * Ange om du vill skapa starten med eller utan de underordnade sidorna.  Som standard inkluderas de här undersidorna.
   Fortsätt med **Nästa**.

   ![Välj startkälla](/help/sites-cloud/authoring/assets/launches-select-source-2.png)

1. I **egenskapssteget** i guiden kan du ange:

   * **Starttitel**: Namnet på Launch. Namnet ska vara meningsfullt för författare.
   * **med befintligt innehåll**: det ursprungliga innehållet kommer att användas för att skapa starten.
   * **Använd en ny mall för att ersätta sidan**: Mer information finns i [Skapa start med ny mall](#create-launch-with-new-template) .
   * **Ärv källsidans livedata**: Välj det här alternativet om du automatiskt vill uppdatera innehållet på startsidor när källsidorna ändras. Det här alternativet uppnår du genom att göra lanseringen till en live-kopia. Som standard är det här alternativet markerat. <!--Select this option to automatically update the content of launch pages when the source pages change. This option achieves this by making the launch a [live copy](/help/sites-administering/msm.md). By default, this option is selected.-->
   * **Startdatum**: Datum och tid då startkopian ska aktiveras (beroende på flaggan **Production Ready** ). se [Startar - Händelsens](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events)ordning).
   ![Startegenskaper](/help/sites-cloud/authoring/assets/launches-properties.png)

1. Använd **Skapa** för att slutföra processen och skapa en ny start. I bekräftelsedialogrutan får du frågan om du vill öppna starten direkt.

   Om du returnerar konsolen (med **Klart**) kan du se (och få tillgång till) hur du startar programmet från:

   * The [**Launches **console](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
   * Referenserna [****i** webbplatskonsolen **](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)

### Skapa start med ny mall {#create-launch-with-new-template}

När du skapar en startsida kan du välja om du vill använda en ny mall:

>[!NOTE]
>
>Det här alternativet är endast tillgängligt när du skapar en start från **webbplatskonsolen** . Det är inte tillgängligt när du skapar en start från **startkonsolen** .

![Skapa en startsida med en ny mall](/help/sites-cloud/authoring/assets/launches-create-new-template.png)

Om du väljer det här alternativet kommer det att:

* Uppdatera andra tillgängliga alternativ,
* Inkludera ett nytt steg där du kan välja önskad mall.

![Välja en ny mall](/help/sites-cloud/authoring/assets/launches-select-template.png)

>[!CAUTION]
>
>Om du använder en annan mall kommer den nya sidan att vara tom. På grund av den annorlunda sidstrukturen kommer inget innehåll att kopieras över.
>
>Den här funktionen kan användas för att ändra mallen för en [befintlig sida](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) , även om innehållsförlusten måste beaktas.

### Skapa en kapslad start {#creating-a-nested-launch}

Genom att skapa en kapslad programstart (starta vid en programstart) kan du skapa en programstart från en befintlig programstart så att författarna kan utnyttja redan gjorda ändringar i stället för att behöva göra samma ändringar flera gånger för varje programstart.

>[!NOTE]
>
>Se även [Befordra en kapslad start](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch).

#### Skapa en kapslad start - Startar konsolen {#creating-a-nested-launch-launches-console}

Att skapa en kapslad start från **Launches** -konsolen är i stort sett detsamma som att skapa någon annan typ av start, med undantag för att du måste navigera till startgrenen `/content/launches`:

1. I **startkonsolen** väljer du **Skapa**.
1. Välj **Lägg till sidor** och navigera sedan till startgrenen genom att ange `/content/launches` i filtret. Välj önskad start och bekräfta med **Välj**:

   ![Skapa en kapslad start](/help/sites-cloud/authoring/assets/launches-create-nested.png)

1. Fortsätt med **Nästa** och fyll i **Egenskaper** som vid andra starter.

   ![Välj källa för kapslad start](/help/sites-cloud/authoring/assets/launches-create-nested-select.png)

#### Skapa en kapslad start - platskonsol {#creating-a-nested-launch-sites-console}

Så här skapar du en kapslad start från **Sites** -konsolen, baserat på en befintlig start:

1. Öppna [Starta från referenser (Sites-konsolen)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) för att visa tillgängliga åtgärder.
1. Välj **Skapa start** för att öppna guiden (eftersom källan redan har valts hoppas steget **Välj källa** över).
1. Ange **starttitel** och annan nödvändig information (som vid normal start).
1. Använd **Skapa** för att slutföra processen och skapa en ny start. I bekräftelsedialogrutan får du frågan om du vill öppna starten direkt.

Om du väljer **Klar**&#x200B;återgår du till **Referenser** i **Sites** Console om du väljer rätt sida som visas när du startar programmet.

### Ta bort en start {#deleting-a-launch}

Du kan ta bort en start från [startkonsolen](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):

* Välj start genom att trycka på/klicka på miniatyrbilden.
* Verktygsfältet visas. Välj Ta bort.
* Bekräfta åtgärden.

>[!CAUTION]
>
>Om du tar bort en programstart tas själva programstarten och alla underordnade kapslade programstarter bort.
