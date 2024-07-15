---
title: Skapa och hantera erbjudanden (Erbjudandekonsol)
description: Använd offertkonsolen för att skapa erbjudanden som du kan använda i aktivitetsupplevelser
exl-id: 81d2fda2-06a9-48f6-820a-dd9e11d94fcc
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '1351'
ht-degree: 0%

---

# Skapa och hantera erbjudanden (Erbjudandekonsol) {#creating-and-managing-offers}

Konsolen **Erbjudanden** kommer att bli inaktuell i framtiden. Så från och med nu är det:

* Endast tillgängligt för kunder som redan har *äldre* erbjudanden (d.v.s. redan befintliga)
* Vi rekommenderar att alla sådana gamla erbjudanden konverteras till Experience Fragment-erbjudanden
   * Så snart det senaste äldre erbjudandet har konverterats/tagits bort är konsolen **Erbjudanden** inte längre tillgänglig.

![Personalization-konsoler](/help/sites-cloud/authoring/assets/offers-consoles.png)

>[!NOTE]
>
>Kunder som har tidigare erbjudanden kan fortfarande använda konsolen **Erbjudanden** för att både se befintliga erbjudanden och skapa nya, gamla erbjudanden.
>
>Kunder som saknar tidigare erbjudanden kan inte se konsolen **Erbjudanden**.
>
>Alla kunder kan använda **Experience Fragments Offers** för att skapa och hantera erbjudanden.

## Konvertera ett äldre erbjudande till ett upplevelsefragment {#convert-legacy-offer-to-experience-fragment}

Ett **alternativ och ett arbetsflöde för att konvertera till upplevelsefragmentvariation** har implementerats för att hjälpa dig att konvertera ditt gamla erbjudande till ett Experience Fragment:

>[!NOTE]
>
>Det här är det rekommenderade arbetsflödet för att konvertera äldre erbjudanden till fragment.

>[!NOTE]
>
>Du kan också skapa en Experience Fragment själv, manuellt överföra innehållet från ditt gamla erbjudande till fragmentet och sedan ta bort det gamla erbjudandet.

>[!CAUTION]
>
>Alternativet **Konvertera till upplevelsefragmentvariation** är tillgängligt för alla kärnkomponenter.
>
>Det här alternativet stöds inte för anpassade komponenter. För sådana komponenter måste du manuellt konvertera innehållet till ett upplevelsefragment.

>[!CAUTION]
>
>Så snart det senaste äldre erbjudandet har konverterats/tagits bort:
>
>* Konsolen **Erbjudanden** är inte längre tillgänglig.
>* Målikonen i verktygsfältet för andra påverkade komponenter visas inte längre.

1. Öppna en sida som innehåller erbjudandet för redigering.

1. Växla till **målläge** för den sidan.

1. Välj **Börja målinrikta**.

1. Välj lämplig (riktad) komponent.

1. Komponentverktygsfältet innehåller ett alternativ för **Konvertera till upplevelsefragmentvariation**:

   ![Konverterar gammalt erbjudande till Experience Fragment](/help/sites-cloud/authoring/assets/offers-convert-legacy-icon.png)

1. En dialogruta visas. Här kan du välja önskad **åtgärd**:

   * Skapa ett nytt Experience Fragment
   * Lägg till innehåll i ett befintligt Experience Fragment

   I det här scenariot väljer du **Skapa ett nytt Experience Fragment**.

   ![Dialogrutan Konvertera till upplevelsefragmentvariationer](/help/sites-cloud/authoring/assets/offers-convert-dialog.png)

1. Fyll i de obligatoriska fälten i dialogrutan:

   * **Överordnad sökväg**
Ange den överordnade sökvägen för det nya upplevelsefragmentet
   * **Mall**
Välj den mall som ska användas för att skapa upplevelsefragmentet.
   * **Fragmenttitel**
Ange rubriken.
   * **Fragmenttaggar**
Lägg till taggar, om det behövs.

1. Bekräfta med **Klar**.

   Om du nu navigerar till konsolen **Experience Fragment Offers** kan du se ditt nya upplevelsefragment tillsammans med tillhörande variationer.

### Målinriktad med erbjudandemallen {#targeting-offers-template}

>[!CAUTION]
>
>Det här alternativet är endast tillgängligt för kunder som har tidigare erbjudanden.
>
>Precis som med konsolen **Erbjudanden** är den inte längre tillgänglig:
>
>* när det senaste äldre erbjudandet har konverterats till Experience Fragments
>* när äldre erbjudanden är föråldrade (i framtiden)
>
>Därför rekommenderar vi att du använder Experience Fragments, inte det här alternativet.

För kunder med tidigare erbjudanden är alternativen för **Använd erbjudandemall** synliga när du riktar in komponenter som **inte** är upplevelsefragment:

![Dialogrutan Konvertera till upplevelsefragmentvariationer](/help/sites-cloud/authoring/assets/offers-legacy-target-non-experience-fragment.png)

## Erbjudandekonsolen {#offers-console}

>[!CAUTION]
>
>Konsolen kommer att bli inaktuell i framtiden eftersom den erbjuder ett äldre sätt att personalisera innehåll.
>
>Du har tid att förbereda dig. Se hur du [konverterar dina befintliga erbjudanden till ett upplevelsefragment](#convert-legacy-offer-to-experience-fragment).

Använd offertkonsolen för att skapa erbjudanden som du kan [använda i aktivitetsupplevelser](/help/sites-cloud/authoring/personalization/targeted-content.md). Genom att skapa erbjudanden i offertkonsolen sparar du tid när flera upplevelser kräver samma erbjudande:

* Skapa erbjudandet en gång i biblioteket och använd det i olika upplevelser av era varumärkesaktiviteter.
* Ändra erbjudandet i biblioteket och ändringen påverkar alla upplevelser som använder det.

Erbjudandekonsolen organiserar erbjudanden efter varumärke. Varje varumärke innehåller ett bibliotek med erbjudanden som kan användas i ett varumärkes upplevelser. Använd mappar för att definiera en hierarkisk struktur för att ordna erbjudanden i varje bibliotek. Med en logisk mappstruktur kan man enkelt hitta erbjudanden genom att bläddra. Med taggnings- och sökverktygen kan författare också hitta erbjudanden.

### Lägg till ett varumärke med hjälp av offertkonsolen {#add-a-brand-using-the-offers-console}

Skapa ett varumärke som era erbjudanden är kopplade till. Öppna ett varumärke i Offers-konsolen för att komma åt dess erbjudandebibliotek där du kan skapa mappar och erbjudanden.

När du skapar ett varumärke med hjälp av konsolen Erbjudanden visas det också i [aktivitetskonsolen](/help/sites-cloud/authoring/personalization/activities.md) där du kan lägga till och administrera aktiviteter för varumärket.

1. I navigeringskonsolen väljer du **Personalization** > **Erbjudanden**.

   ![Navigerar till erbjudandekonsolen](/help/sites-cloud/authoring/assets/offers-navigation.png)

1. Välj **Skapa** och sedan **Skapa** **varumärke**.
1. Markera varumärkesmallen och välj **Nästa**.
1. Skriv en rubrik för varumärket som du vill att det ska visas i konsolerna för erbjudanden och aktiviteter. Du kan också ange eller markera en eller flera taggar som ska kopplas till varumärket.
1. Välj **Skapa**.

### Lägg till en mapp i ett offertbibliotek {#add-a-folder-to-an-offer-library}

Lägg till en mapp i erbjudandebiblioteket för ett varumärke för att ordna och lagra erbjudanden. Du kan skapa en mapp under varumärket eller under andra mappar.

1. Öppna den plats där du vill skapa mappen i konsolen Erbjudanden. Öppna till exempel varumärket för att skapa en mapp på den översta nivån eller öppna en annan mapp i biblioteket.
1. Välj **Skapa** > **Skapa mapp eller erbjudande**.

   ![Skapar erbjudandemapp](/help/sites-cloud/authoring/assets/offers-create-folder.png)

1. Välj **Mapp** och klicka på **Nästa**.
1. Skriv en rubrik för mappen som du vill att den ska visas i erbjudandebiblioteket och skriv eller välj taggar.

   ![Definierar mappegenskaper](/help/sites-cloud/authoring/assets/offers-folder-properties.png)

1. Välj **Skapa**.

### Lägg till ett erbjudande i ett erbjudandebibliotek {#add-an-offer-to-an-offer-library}

Lägg till ett erbjudande i ett varumärkes erbjudandebibliotek så att det kan läggas till i varumärkesupplevelsen. När du lägger till ett erbjudande anger du en titel. Du kan även koppla erbjudandet till en eller flera taggar för att förbättra sökbarheten.

När du har skapat erbjudandet kan du öppna det och redigera innehållet.

1. I konsolen Erbjudanden öppnar du den plats där du vill skapa erbjudandet. Öppna till exempel varumärket för att skapa ett erbjudande på högsta nivå eller öppna en mapp i biblioteket.
1. Välj **Skapa** > **Skapa mapp eller erbjudande**.

   ![Skapar erbjudandemapp](/help/sites-cloud/authoring/assets/offers-create-folder.png)

1. Markera mallen **Erbjudandesida** och välj sedan **Nästa**.
1. Ange en titel för erbjudandet och välj eller skriv en eller flera taggar som du vill associera med erbjudandet. Välj sedan **Skapa**.
1. I bekräftelsedialogrutan öppnar du erbjudandet för redigering genom att välja **Öppna sida**.

### Redigera ett erbjudande {#editing-an-offer}

Öppna ett erbjudande och redigera innehållet som du vill att det ska visas i upplevelserna som använder det. När ni redigerar ett erbjudande som används i alla upplevelser visas era ändringar i upplevelserna.

Du kan öppna ett erbjudande från en mapp i ett erbjudandebibliotek eller från sökresultat. Du kan också öppna ett erbjudande från en upplevelse som använder erbjudandet.

1. I konsolen Erbjudanden markerar du ikonen bredvid erbjudandet och väljer **Redigera**.
1. Lägg till komponenter i erbjudandet och redigera komponentinnehållet som vanligt.

### Ta bort ett erbjudande {#deleting-an-offer}

Ta bort ett erbjudande när det inte längre behövs. När du försöker ta bort ett erbjudande som används i en upplevelse uppmanas du att bekräfta borttagningen. Bekräftelse tar bort erbjudandet och tar bort det från upplevelserna.

Du kan ta bort ett erbjudande när du visar antingen mappinnehåll i ett erbjudandebibliotek eller sökresultat.

1. I konsolen Erbjudanden markerar du ikonen bredvid erbjudandet och väljer **Ta bort**.

   Markera erbjudandet och välj **Ta bort**.

1. I dialogrutan som visas väljer du **Ta bort** för att bekräfta borttagningen.
1. Om erbjudandet används i en eller flera upplevelser visas en dialogruta som anger att det hänvisas till erbjudandet:

   * Om du vill ta bort erbjudandet och ta bort det från upplevelserna väljer du **Tvinga borttagning**.
   * Välj **Avbryt** om du vill behålla erbjudandet.

### Söker efter erbjudanden {#searching-for-offers}

Sök efter erbjudanden för alla varumärken med hjälp av nyckelord för att matcha titeln.

![Söker efter ett erbjudande](/help/sites-cloud/authoring/assets/offers-search.png)

De aktuella sökvillkoren visas bredvid sökresultaten. Du kan också sortera resultaten efter kolumn i stigande eller fallande ordning. Du kan söka i vilken mapp som helst i ett bibliotek. Sökresultaten är desamma oavsett aktuell mapp.

Så här söker du efter erbjudanden:

1. Högst upp i konsolen Erbjudanden väljer du förstoringsglaset. Som standard är sökningen begränsad till erbjudanden.
1. Ange ditt nyckelord om du vill söka efter erbjudanden. Välj bland resultaten.
