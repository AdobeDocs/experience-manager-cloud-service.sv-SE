---
title: Skapa Launches
description: Du kan skapa en startsida som gör det möjligt att uppdatera en ny version av befintliga webbsidor för framtida aktivering.
exl-id: 216ccb7a-1409-4f55-8be2-2b088f91a430
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 12%

---

# Skapa Launches {#creating-launches}

Skapa en startsida för att möjliggöra uppdatering av en ny version av befintliga webbsidor för framtida aktivering. När du skapar en Launch anger du en titel och källsidan:

* Titeln visas i [Referenser](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) på webben, där författarna kan arbeta med dem.
* Källsidans underordnade sidor inkluderas som standard i starten. Du kan bara använda källsidan om du vill.
* Som standard [Live Copy](/help/sites-cloud/administering/msm/overview.md) uppdaterar startsidorna automatiskt när källsidorna ändras. Du kan ange att en statisk kopia ska skapas för att förhindra automatiska ändringar.

Du kan också ange **startdatum** (och starttid) för att definiera när startsidorna ska befordras och aktiveras. **Startdatumet** fungerar dock endast i kombination med flaggan **Produktionsklar** (se [Redigera en startkonfiguration](/help/sites-cloud/authoring/launches/editing.md#editing-a-launch-configuration)). För att åtgärderna ska köras automatiskt måste båda anges.

>[!NOTE]
>
>När du skapar en start är inte sidor högre upp i hierarkin kopior av källsidorna. De är platshållare och skapas med mallen:
>
>* `/libs/launches/templates/outofscope`
>
>Dessa sidor kan inte redigeras. Meddelandet visas:
>
>* **Den här sidan är inte en del av startsidan. Gå till produktionssidan**

## Skapa en Launch {#creating-a-launch}

Du kan skapa en start från Sites- eller Launches-konsolen:

1. Öppna **Webbplatser** eller **Startar** konsol.

   >[!NOTE]
   >
   >När du använder **Webbplatser** konsol är det vanligt att navigera till källsidans plats, men det är inte obligatoriskt eftersom du kan navigera när du väljer **Startkälla** i guiden.

1. Beroende på vilken konsol du använder:
   * **Launches**:
      1. Välj **Skapa start** Öppna guiden i verktygsfältet.
   * **Sites**:
      1. Välj **Skapa** i verktygsfältet för att öppna markeringsrutan.
      1. Välj **Skapa start** för att öppna guiden.

   >[!NOTE]
   >
   >I **Sites**-konsolen kan du även använda [markeringsläget](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) för att välja en sida innan du väljer **Skapa**.
   >
   >Då används den valda sidan som den ursprungliga källsidan.

1. I **Välj källa** steg du behöver **Lägg till sidor**. Du kan markera flera sidor och ange sökvägen för varje sida:
   * Navigera till önskad plats.
   * Markera källsidan/källsidorna och bekräfta (bockmarkering).

   Upprepa efter behov.

   ![Välj startkälla](/help/sites-cloud/authoring/assets/launches-select-source.png)

   >[!NOTE]
   >
   >Om du vill lägga till sidor och/eller grenar i en programstart måste de finnas på en plats, det vill säga under en gemensam toppnivårot.
   >
   >Om en webbplats innehåller språkrötter under den översta nivån måste sidorna och grenarna för en start ligga under en gemensam språkrot.

1. För varje tävlingsbidrag kan du ange om du vill:

   * **Inkludera undersidor**:

      * Ange om du vill skapa starten med eller utan de underordnade sidorna.  Som standard inkluderas de här undersidorna.

   Fortsätt med **Nästa**.

   ![Välj startkälla](/help/sites-cloud/authoring/assets/launches-select-source-2.png)

1. I **Egenskaper** steg i guiden som du kan ange:

   * **Starta titel**: Namnet på Launch. Namnet ska vara meningsfullt för författare.
   * **med befintligt innehåll**: det ursprungliga innehållet används för att skapa starten.
   * **använda en ny mall för att ersätta sidan**: Se [Skapa start med ny mall](#create-launch-with-new-template) för mer information.
   * **Ärv källsidans livedata**: Välj det här alternativet om du automatiskt vill uppdatera innehållet på startsidor när källsidorna ändras. Det här alternativet uppnår du genom att göra starten till [Live Copy](/help/sites-cloud/administering/msm/overview.md). Som standard är det här alternativet markerat.—>
   * **Startdatum**: Det datum och den tidpunkt då startkopian ska aktiveras (beroende på **Produktionsklar** flagga, se [Startar - ordningen för händelser](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events)).

   ![Startegenskaper](/help/sites-cloud/authoring/assets/launches-properties.png)

1. Använd **Skapa** för att slutföra processen och skapa en ny start. I bekräftelsedialogrutan får du frågan om du vill öppna starten direkt.

   Om du returnerar konsolen (med **Klar**) kan du se (och få tillgång till) din programstart från:

   * The [**Startar** konsol](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
   * The [**Referenser** i **Webbplatser** konsol](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)

### Skapa start med ny mall {#create-launch-with-new-template}

När du skapar en startsida kan du välja om du vill använda en ny mall:

>[!NOTE]
>
>Det här alternativet är endast tillgängligt när du skapar en start från **Webbplatser** konsol. Det är inte tillgängligt när du skapar en start från **Startar** konsol.

![Skapa en startsida med en ny mall](/help/sites-cloud/authoring/assets/launches-create-new-template.png)

Om du väljer det här alternativet kommer det att:

* Uppdatera de andra tillgängliga alternativen,
* Inkludera ett nytt steg där du kan välja önskad mall.

![Välja en ny mall](/help/sites-cloud/authoring/assets/launches-select-template.png)

>[!CAUTION]
>
>När en annan mall används är den nya sidan tom. På grund av den annorlunda sidstrukturen kopieras inget innehåll.
>
>Den här funktionen kan användas för att ändra mallen för en [befintlig sida](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) - även om innehållsförlusten måste beaktas.

### Skapa en kapslad start {#creating-a-nested-launch}

Genom att skapa en kapslad programstart (starta vid en programstart) kan du skapa en programstart från en befintlig programstart så att författarna kan utnyttja redan gjorda ändringar i stället för att behöva göra samma ändringar flera gånger för varje programstart.

>[!NOTE]
>
>Se även [Befordra en kapslad start](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch).

#### Skapa en kapslad start - Startar konsolen {#creating-a-nested-launch-launches-console}

Skapa en kapslad start från **Startar** konsolen är i stort sett densamma som att skapa andra former av programstart, med undantag för att du måste navigera till startgrenen `/content/launches`:

1. I **Startar** välj konsol **Skapa**.
1. Välj **Lägg till sidor** navigera sedan till startgrenen genom att ange `/content/launches` i **Filter** järnväg. Välj önskad start och bekräfta med **Välj**:

   ![Skapa en kapslad start](/help/sites-cloud/authoring/assets/launches-create-nested.png)

1. Fortsätt med **Nästa**.

1. Slutför **Egenskaper** som vid andra starter.

1. Fullständigt med **Skapa**.

#### Skapa en kapslad start - platskonsol {#creating-a-nested-launch-sites-console}

Skapa en kapslad programstart från **Webbplatser** konsol - baserat på en befintlig start:

1. Öppna [Starta från referenser (platskonsolen)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) för att visa tillgängliga åtgärder.
1. Välj **Skapa start** för att öppna guiden (eftersom källan redan har valts hoppas steget **Välj källa** över).
1. Ange **Starta titel** och annan nödvändig information (som vid normal start).
1. Använd **Skapa** för att slutföra processen och skapa en ny start. I bekräftelsedialogrutan får du frågan om du vill öppna starten direkt.

Om du väljer **Klar** återgår du till rutan **Referenser** i **Sites**-konsolen och om du väljer rätt sida visas den nya startsidan.

### Ta bort en start {#deleting-a-launch}

Du kan ta bort en programstart från [startar konsolen](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):

* Välj start genom att trycka på/klicka på miniatyrbilden.
* Verktygsfältet visas. Välj Ta bort.
* Bekräfta åtgärden.

>[!CAUTION]
>
>Om du tar bort en programstart tas själva programstarten och alla underordnade kapslade programstarter bort.
