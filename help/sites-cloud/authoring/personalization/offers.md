---
title: Skapa och hantera erbjudanden (Erbjudandekonsol)
description: Använd offertkonsolen för att skapa erbjudanden som du kan använda i aktivitetsupplevelser
exl-id: 81d2fda2-06a9-48f6-820a-dd9e11d94fcc
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '1391'
ht-degree: 0%

---

# Skapa och hantera erbjudanden (Erbjudandekonsol) {#creating-and-managing-offers}

The **Erbjudanden** Konsolen kommer att bli inaktuell i framtiden. Så från och med nu är det:

* Endast tillgängligt för kunder som har *äldre* redan definierade erbjudanden (d.v.s. befintliga)
* Vi rekommenderar att alla sådana gamla erbjudanden konverteras till Experience Fragment-erbjudanden
   * Så snart det senaste äldre erbjudandet konverteras/tas bort, **Erbjudanden** Konsolen är inte längre tillgänglig.

![Personaliseringskonsoler](/help/sites-cloud/authoring/assets/offers-consoles.png)

>[!NOTE]
>
>Kunder som har äldre erbjudanden kan fortfarande använda **Erbjudanden** för att se både befintliga och nya erbjudanden.
>
>Kunder som inte har tidigare erbjudanden kommer inte att se **Erbjudanden** konsol.
>
>Alla kunder kan använda **Upplevelsefragment** att skapa och hantera erbjudanden.

## Konvertera ett äldre erbjudande till ett upplevelsefragment {#convert-legacy-offer-to-experience-fragment}

A **Konvertera till upplevelsefragmentvariation** har implementerats för att hjälpa er att konvertera ert gamla erbjudande till en Experience Fragment:

>[!NOTE]
>
>Det här är det rekommenderade arbetsflödet för att konvertera äldre erbjudanden till fragment.

>[!NOTE]
>
>Du kan också skapa en ny Experience Fragment själv, manuellt överföra innehållet från ditt gamla erbjudande till fragmentet och sedan ta bort det gamla erbjudandet.

>[!CAUTION]
>
>The **Konvertera till upplevelsefragmentvariation** finns för alla kärnkomponenter.
>
>Det här alternativet stöds inte för anpassade komponenter. För sådana komponenter måste du manuellt konvertera innehållet till ett upplevelsefragment.

>[!CAUTION]
>
>Så snart det senaste äldre erbjudandet har konverterats/tagits bort:
>
>* The **Erbjudanden** Konsolen är inte längre tillgänglig.
>* Målikonen i verktygsfältet för andra påverkade komponenter visas inte längre.

1. Öppna en sida som innehåller erbjudandet för redigering.

1. Växla till **Målinriktning** läge för den sidan.

1. Välj **Börja målinrikta**.

1. Välj lämplig (riktad) komponent.

1. Komponentverktygsfältet innehåller ett alternativ för att **Konvertera till upplevelsefragmentvariation**:

   ![Konvertera äldre erbjudande till Experience Fragment](/help/sites-cloud/authoring/assets/offers-convert-legacy-icon.png)

1. En dialogruta visas. Här kan du välja önskat **Åtgärd**:

   * Skapa ett nytt Experience Fragment
   * Lägg till innehåll i ett befintligt Experience Fragment

   Välj **Skapa ett nytt Experience Fragment**.

   ![Dialogrutan Konvertera till upplevelsefragmentvariationer](/help/sites-cloud/authoring/assets/offers-convert-dialog.png)

1. Fyll i de obligatoriska fälten i dialogrutan:

   * **Överordnad sökväg**
Ange den överordnade sökvägen för det nya upplevelsefragmentet
   * **Mall**
Välj den mall som ska användas för att skapa upplevelsefragmentet.
   * **Fragmenttitel**
Ange rubriken.
   * **Fragment-taggar**
Lägg till taggar, om det behövs.

1. Bekräfta med **Klar**.

   Om du nu navigerar till **Experience Fragment-erbjudanden** konsolen kan du se ditt nya upplevelsefragment, tillsammans med tillhörande varianter.

### Målinriktad med erbjudandemallen {#targeting-offers-template}

>[!CAUTION]
>
>Det här alternativet är endast tillgängligt för kunder som har tidigare erbjudanden.
>
>Som med **Erbjudanden** konsolen är inte längre tillgänglig:
>
>* när det senaste äldre erbjudandet har konverterats till Experience Fragments
>* när äldre erbjudanden är föråldrade (i framtiden)
>
>Därför rekommenderar vi att du använder Experience Fragments, inte det här alternativet.

För kunder med tidigare erbjudanden **Använd erbjudandemall** är synliga när du aktiverar komponenter som **not** Upplevelsefragment:

![Dialogrutan Konvertera till upplevelsefragmentvariationer](/help/sites-cloud/authoring/assets/offers-legacy-target-non-experience-fragment.png)

## Erbjudandekonsolen {#offers-console}

>[!CAUTION]
>
>Konsolen kommer att bli inaktuell i framtiden eftersom den erbjuder ett äldre sätt att personalisera innehåll.
>
>Du har tid att förbereda dig. Se hur man [konvertera era gamla erbjudanden till ett upplevelsefragment](#convert-legacy-offer-to-experience-fragment).

Använd offertkonsolen för att skapa erbjudanden som du kan [använda i aktivitetsupplevelser](/help/sites-cloud/authoring/personalization/targeted-content.md). Genom att skapa erbjudanden i offertkonsolen sparar du tid när flera upplevelser kräver samma erbjudande:

* Skapa erbjudandet en gång i biblioteket och använd det i olika upplevelser av era varumärkesaktiviteter.
* Ändra erbjudandet i biblioteket och ändringen påverkar alla upplevelser som använder det.

Erbjudandekonsolen organiserar erbjudanden efter varumärke. Varje varumärke innehåller ett bibliotek med erbjudanden som kan användas i ett varumärkes upplevelser. Använd mappar för att definiera en hierarkisk struktur för att ordna erbjudanden i varje bibliotek. Med en logisk mappstruktur kan man enkelt hitta erbjudanden genom att bläddra. Med taggnings- och sökverktygen kan författare också hitta erbjudanden.

### Lägg till ett varumärke med hjälp av offertkonsolen {#add-a-brand-using-the-offers-console}

Skapa ett varumärke som era erbjudanden är kopplade till. Öppna ett varumärke i Offers-konsolen för att komma åt dess erbjudandebibliotek där du kan skapa mappar och erbjudanden.

När du skapar ett varumärke med hjälp av Erbjudandekonsolen visas det också i [Aktivitetskonsol](/help/sites-cloud/authoring/personalization/activities.md) där ni kan lägga till och administrera aktiviteter för varumärket.

1. Klicka eller tryck på **Personalisering** > **Erbjudanden** i navigeringskonsolen.

   ![Navigera till erbjudandekonsolen](/help/sites-cloud/authoring/assets/offers-navigation.png)

1. Klicka eller tryck **Skapa** och sedan **Skapa** **Varumärke**.
1. Välj varumärkesmallen och klicka eller peka **Nästa**.
1. Skriv en rubrik för varumärket som du vill att det ska visas i konsolerna för erbjudanden och aktiviteter. Du kan också ange eller markera en eller flera taggar som ska kopplas till varumärket.
1. Klicka eller tryck **Skapa**.

### Lägg till en mapp i ett offertbibliotek {#add-a-folder-to-an-offer-library}

Lägg till en mapp i erbjudandebiblioteket för ett varumärke för att ordna och lagra erbjudanden. Du kan skapa en mapp under varumärket eller under andra mappar.

1. Öppna den plats där du vill skapa mappen i konsolen Erbjudanden. Öppna till exempel varumärket för att skapa en mapp på den översta nivån eller öppna en annan mapp i biblioteket.
1. Klicka eller tryck **Skapa** > **Skapa mapp eller erbjudande**.

   ![Skapar erbjudandemapp](/help/sites-cloud/authoring/assets/offers-create-folder.png)

1. Välj **Mapp** och klicka **Nästa**.
1. Skriv en rubrik för mappen som du vill att den ska visas i erbjudandebiblioteket och skriv eller välj taggar.

   ![Definiera mappegenskaper](/help/sites-cloud/authoring/assets/offers-folder-properties.png)

1. Klicka eller tryck **Skapa**.

### Lägg till ett erbjudande i ett erbjudandebibliotek {#add-an-offer-to-an-offer-library}

Lägg till ett erbjudande i ett varumärkes erbjudandebibliotek så att det kan läggas till i varumärkesupplevelsen. När du lägger till ett erbjudande anger du en titel. Du kan även koppla erbjudandet till en eller flera taggar för att förbättra sökbarheten.

När du har skapat erbjudandet kan du öppna det och redigera innehållet.

1. I konsolen Erbjudanden öppnar du den plats där du vill skapa erbjudandet. Öppna till exempel varumärket för att skapa ett erbjudande på högsta nivå eller öppna en mapp i biblioteket.
1. Klicka eller tryck **Skapa** > **Skapa mapp eller erbjudande**.

   ![Skapar erbjudandemapp](/help/sites-cloud/authoring/assets/offers-create-folder.png)

1. Välj **Erbjudandesida** mall och sedan klicka eller peka **Nästa**.
1. Skriv en titel för erbjudandet och välj eller skriv in en eller flera taggar som ska kopplas till erbjudandet. Klicka eller tryck sedan **Skapa**.
1. Öppna erbjudandet för redigering genom att klicka eller trycka på **Öppna sida**.

### Redigera ett erbjudande {#editing-an-offer}

Öppna ett erbjudande och redigera innehållet som du vill att det ska visas i upplevelserna som använder det. När ni redigerar ett erbjudande som används i alla upplevelser visas era ändringar i upplevelserna.

Du kan öppna ett erbjudande från en mapp i ett erbjudandebibliotek eller från sökresultat. Du kan också öppna ett erbjudande från en upplevelse som använder erbjudandet.

1. Tryck eller klicka på ikonen bredvid erbjudandet i konsolen Erbjudanden och klicka eller tryck på **Redigera**.
1. Lägg till komponenter i erbjudandet och redigera komponentinnehållet som vanligt.

### Ta bort ett erbjudande {#deleting-an-offer}

Ta bort ett erbjudande när det inte längre behövs. När du försöker ta bort ett erbjudande som används i en upplevelse uppmanas du att bekräfta borttagningen. Bekräftelse tar bort erbjudandet och tar bort det från upplevelserna.

Du kan ta bort ett erbjudande när du visar antingen mappinnehåll i ett erbjudandebibliotek eller sökresultat.

1. Tryck eller klicka på ikonen bredvid erbjudandet i konsolen Erbjudanden och klicka eller tryck på **Ta bort**.

   Välj erbjudandet och klicka eller tryck **Ta bort**.

1. Klicka på eller tryck i dialogrutan som visas **Ta bort** för att bekräfta borttagningen.
1. Om erbjudandet används i en eller flera upplevelser visas en dialogruta som anger att det hänvisas till erbjudandet:

   * Om du vill ta bort erbjudandet och ta bort det från upplevelserna klickar eller trycker du på **Tvinga borttagning**.
   * Klicka eller tryck för att behålla erbjudandet **Avbryt**.

### Söker efter erbjudanden {#searching-for-offers}

Sök efter erbjudanden för alla varumärken med hjälp av nyckelord för att matcha titeln.

![Söker efter ett erbjudande](/help/sites-cloud/authoring/assets/offers-search.png)

De aktuella sökvillkoren visas bredvid sökresultaten. Du kan också sortera resultaten efter kolumn i stigande eller fallande ordning. Du kan söka i vilken mapp som helst i ett bibliotek. Sökresultaten är desamma oavsett aktuell mapp.

Så här söker du efter erbjudanden:

1. Klicka på eller tryck på förstoringsglaset längst upp på Offers-konsolen. Som standard är sökningen begränsad till erbjudanden.
1. Ange ditt nyckelord om du vill söka efter erbjudanden. Välj bland resultaten.
