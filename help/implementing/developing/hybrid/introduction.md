---
title: Introduktion och genomgång av SPA
description: I den här artikeln beskrivs begreppen för ett SPA-program och du kan gå igenom hur du använder ett grundläggande SPA-program för att skapa, vilket visar hur det är relaterat till den underliggande AEM SPA-redigeraren.
exl-id: 8dad48d5-fa90-467c-8bec-e4b76e057f80
feature: Developing
role: Admin, Architect, Developer
index: false
source-git-commit: 7a9d947761b0473f5ddac3c4d19dfe5bed5b97fe
workflow-type: tm+mt
source-wordcount: '2045'
ht-degree: 0%

---


# Introduktion och genomgång av SPA {#spa-introduction}

Single page applications (SPAs) can offer compelling experiences for website users. Utvecklare vill kunna skapa webbplatser med SPA-ramverk och författare vill smidigt redigera innehåll i AEM för en webbplats som byggts med sådana ramverk.

SPA Editor är en omfattande lösning för SPA-program i AEM. I den här artikeln går vi igenom hur du använder ett grundläggande SPA-program för att skapa och visar hur det är relaterat till den underliggande AEM SPA-redigeraren.

{{ue-over-spa}}

## Introduktion {#introduction}

### Artikelsyfte {#article-objective}

I den här artikeln beskrivs de grundläggande begreppen för SPA-program innan du leder läsaren genom en genomgång av SPA-redigeraren genom att använda ett enkelt SPA-program för att demonstrera grundläggande innehållsredigering. Sedan går det ned på hur sidan är uppbyggd och hur SPA-programmet relaterar till och interagerar med AEM SPA Editor.

Målet med denna introduktion och genomgång är att visa för en AEM-utvecklare varför SPA är relevanta, hur de i allmänhet fungerar, hur en SPA hanteras av AEM SPA Editor och hur det skiljer sig från en vanlig AEM-applikation.

## Krav {#requirements}

Genomgången baseras på AEM standardfunktioner och exempelprogrammet WKND SPA Project. Om du vill följa med i den här genomgången måste du ha följande till hands.

* [Senaste utveckling av SDK i AEMaaCS](/help/release-notes/release-notes-cloud/release-notes-current.md)
   * Den bör köras som en lokal utvecklingsmiljö.
   * Du måste ha administratörsbehörighet för systemet.
* [Exempelprogrammet WKND SPA Project är tillgängligt på GitHub](https://github.com/adobe/aem-guides-wknd-spa)
   * Hämta den [senaste versionen av React-appen](https://github.com/adobe/aem-guides-wknd-spa/releases) med namnet `wknd-spa-react.all-X.Y.Z-SNAPSHOT.zip`.
   * Hämta de [senaste exempelbilderna för appen ](https://github.com/adobe/aem-guides-wknd-spa/releases) med namnet `wknd-spa-sample-images-X.Y.Z.zip`.
   * [Använd pakethanteraren](/help/implementing/developing/tools/package-manager.md) för att installera båda paketen på samma sätt som andra paket i AEM.
   * Appen behöver inte installeras med Maven för den här genomgången.

>[!CAUTION]
>
>Det här dokumentet använder [WKND SPA-projektappen](https://github.com/adobe/aem-guides-wknd-spa) endast i demonstrationssyfte. Använd den inte för något projektarbete.

>[!TIP]
>
>Alla AEM-projekt ska använda [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=sv-SE), som har stöd för SPA-projekt med React eller Angular och som använder SPA SDK.

### Vad är en SPA? {#what-is-a-spa}

Ett SPA-program (single-page application) skiljer sig från en konventionell sida genom att det återges på klientsidan och i första hand är JavaScript-styrt, beroende på att Ajax anropar för att läsa in data och dynamiskt uppdatera sidan. Det mesta eller allt innehåll hämtas en gång på en sida, och ytterligare resurser läses in asynkront efter behov baserat på användarinteraktionen med sidan.

Detta minskar behovet av siduppdatering och ger användaren en upplevelse som är smidig, snabb och som känns mer som en appupplevelse.

Med AEM SPA Editor kan gränssnittsutvecklare skapa SPA som kan integreras i en AEM-webbplats, vilket gör att innehållsförfattarna kan redigera SPA-innehållet lika enkelt som annat AEM-innehåll.

### Varför en SPA? {#why-a-spa}

Genom att vara snabbare, smidigare och mer som ett systemspecifikt program blir en SPA en mycket attraktiv upplevelse inte bara för besökaren på webbsidan, utan även för marknadsförare och utvecklare på grund av hur SPA fungerar.

![SPA-fördelar](assets/spa-benefits.png)

#### Besökare {#visitors}

* Besökarna vill ha upplevelser som påminner om varandra när de interagerar med innehållet.
* Det finns tydliga data om att ju snabbare en sida är, desto troligare blir konverteringen.

#### Marknadsförare {#marketers}

* Marknadsförarna vill erbjuda innehållsrika, verklighetstrogna upplevelser som lockar besökarna att engagera sig fullt ut i innehållet.
* Personalization kan göra dessa upplevelser ännu mer övertygande.

#### Utvecklare {#developers}

* Utvecklarna vill att det ska finnas tydliga skillnader mellan innehåll och presentation.
* Ren separation gör systemet mer utbyggbart och möjliggör oberoende frontendutveckling.

### Hur fungerar en SPA? {#how-does-a-spa-work}

Den främsta idén bakom ett SPA är att anrop till och beroende av en server minskas för att minimera fördröjningar som orsakas av serverfördröjning så att SPA närmar sig svarstiden för ett systemspecifikt program.

På en traditionell, sekventiell webbsida läses bara de data som behövs för den omedelbara sidan in. Det innebär att när besökaren flyttar till en annan sida anropas servern för de extra resurserna. Ytterligare anrop kan behövas eftersom besökaren interagerar med element på sidan. Dessa anrop kan ge en känsla av fördröjning eller fördröjning eftersom sidan måste hinna ifatt besökarens önskemål.

![Sekventiellt jämfört med flytande upplevelser](assets/spa-sequential-vs-fluid.png)

För en smidigare upplevelse, som närmar sig vad en besökare förväntar sig av mobilappar och inbyggda appar, läser en SPA in alla nödvändiga data för besökaren vid den första inläsningen. Detta kan ta lite längre tid i början, men eliminerar sedan behovet av ytterligare serveranrop.

Genom att återge på klientsidan reagerar sidelementen snabbare, och besökarens interaktioner med sidan sker direkt. Eventuella ytterligare data som kan behövas anropas asynkront för att maximera sidans hastighet.

>[!TIP]
>
>Teknisk information om hur SPA fungerar i AEM finns i artiklarna:
>* [Komma igång med SPA i AEM med React](getting-started-react.md)
>* [Komma igång med SPA i AEM med Angular](getting-started-angular.md)
>
>Mer information om design, arkitektur och tekniska arbetsflöden i SPA-redigeraren finns i artikeln:
>* [SPA-redigeraren - översikt](editor-overview.md).

## Innehållsredigering med SPA {#content-editing-experience-with-spa}

När en SPA har byggts för att använda AEM SPA Editor märker innehållsförfattaren ingen skillnad när du redigerar och skapar innehåll. Vanliga AEM-funktioner är tillgängliga och inga ändringar i författarens arbetsflöde krävs.

1. Redigera WKND SPA Project-programmet i AEM.

   `http://localhost:4502/editor.html/content/wknd-spa-react/us/en/home.html`

   ![WKND SPA-projekt, startsida](assets/wknd-home.png)

1. Markera en textkomponent och lägg märke till att ett verktygsfält ser ut som en annan komponent. Välj **Redigera**.

   ![Markera textkomponent](assets/wknd-text.png)

1. Redigera innehållet som vanligt i AEM och lägg märke till att ändringarna bevaras.

   ![Redigera text](assets/wknd-edit-text.png)

1. Använd Assets webbläsare för att dra och släppa en ny bild i en bildkomponent.

   ![Släpp en bildresurs](assets/wkdn-drop-image.png)

1. Ändringen är beständig.

   ![Bilden beständig](assets/wknd-change-persisted.png)

Ytterligare redigeringsverktyg som att dra och släppa ytterligare komponenter på sidan, ordna om komponenter och ändra layouten stöds som i andra AEM-program än SPA.

>[!NOTE]
>
>SPA-redigeraren ändrar inte programmets DOM. Själva SPA är ansvarig för DOM.
>
>Om du vill se hur det fungerar fortsätter du till nästa avsnitt i den här artikeln [SPA-appar och AEM SPA-redigeraren](#spa-apps-and-the-aem-spa-editor).

## SPA-appar och AEM SPA Editor {#spa-apps-and-the-aem-spa-editor}

Genom att uppleva hur en SPA fungerar för användaren och sedan inspektera SPA-sidan blir det lättare att förstå hur en SAP-app fungerar med SPA-redigeraren i AEM.

### Använda ett SPA-program {#using-an-spa-application}

1. Läs in WKND SPA-projektprogrammet på publiceringsservern eller med alternativet **Visa som publicerad** på menyn **Sidinformation** i sidredigeraren.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![Förhandsgranskning av WKND SPA-projektstartsida](assets/wknd-preview.png)

   Lägg märke till sidstrukturen, inklusive navigering till underordnade sidor, menyer och artikelkort.

1. Navigera till en underordnad sida via menyn och se att sidan läses in omedelbart utan att behöva uppdateras.

   ![WKND SPA-projektsida 1](assets/wknd-page1.png)

1. Öppna webbläsarens inbyggda utvecklarverktyg och övervaka nätverksaktiviteten när du navigerar bland de underordnade sidorna.

   ![Nätverksaktivitet](assets/wknd-network-activity.png)

   Trafiken är mycket liten när du går från sida till sida i appen. Sidan läses inte in igen och endast de nya bilderna begärs.

   SPA hanterar innehållet och routningen enbart på klientsidan.

Så om sidan inte läses in igen när du navigerar genom de underordnade sidorna, hur läses den in?

I nästa avsnitt, [Läsa in ett SPA-program](#loading-a-spa-application), läses djupare in i hur SPA läses in och hur innehåll kan läsas in synkront och asynkront.

### Läsa in ett SPA-program {#loading-a-spa-application}

1. Om den inte redan är inläst läser du in WKND SPA-projektappen antingen på publiceringsservern eller med alternativet **Visa som publicerad** på menyn **Sidinformation** i sidredigeraren.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![Förhandsgranskning av WKND SPA-projekt](assets/wknd-preview.png)

1. Använd det inbyggda verktyget i webbläsaren för att visa sidans källa.
1. Källans innehåll är begränsat.
   * Sidan har inget innehåll i sin brödtext. Den består huvudsakligen av formatmallar och ett anrop till olika skript, till exempel `clientlib-react.min.js`.
   * Dessa skript är de primära drivrutinerna för det här programmet och ansvarar för återgivningen av allt innehåll.

1. Använd webbläsarens inbyggda verktyg för att inspektera sidan. Se innehållet i DOM som är fullständigt inläst.

   ![DOM för WKND SPA-projekt](assets/wknd-dom.png)

1. Växla till fliken Nätverk i panelen Granska och läs in sidan igen.

   Observera att de primära resurser som har lästs in för sidan är själva sidan, CSS, React JavaScript, dess beroenden och JSON-data för sidan.

   ![WKND SPA-projektnätverksaktivitet](assets/wknd-network.png)

1. Läs in `home.model.json` på en ny flik.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.model.json`

   ![JSON på WKND SPA-projektets startsida](assets/wknd-json.png)

   AEM SPA Editor använder [AEM Content Services](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-and-content-services) för att leverera hela sidans innehåll som en JSON-modell.

   Genom att implementera specifika gränssnitt tillhandahåller Sling Models den information som krävs för SPA. Leveransen av JSON-data delegeras nedåt till varje komponent (från sida, stycke, komponent osv.).

   Varje komponent väljer vad den visar och hur den återges (på serversidan med HTML eller på klientsidan med React eller Angular). Den här artikeln fokuserar på klientåtergivning med React.

1. Modellen kan också gruppera sidor så att de läses in synkront, vilket minskar antalet sidomladdningar som behövs.

   I exemplet med WKND SPA-projektappen läses sidorna `home`, `page-1`, `page-2` och `page-3` in synkront eftersom besökare vanligtvis besöker alla dessa sidor.

   Detta beteende är inte obligatoriskt och är helt definierbart.

   ![WKND SPA-projektobjektgruppering](assets/wknd-pages.png)

1. Om du vill visa den här skillnaden i beteende läser du in sidan `home` igen och rensar nätverksaktiviteten för inspektören. Navigera till `page-1` på sidmenyn och se att den enda nätverksaktiviteten är en begäran för bilden av `page-1`. `page-1` behöver inte läsas in.

   ![WKND SPA Project page-1 network activity](assets/wknd-page1-network.png)

### Interaktion med SPA-redigeraren {#interaction-with-the-spa-editor}

Med exempelprogrammet WKND SPA Project är det tydligt hur programmet fungerar och läses in när det publiceras, med hjälp av innehållstjänster för JSON-innehållsleverans och asynkron inläsning av resurser.

Innehållsutvecklaren kan också skapa innehåll med en SPA-redigerare utan problem i AEM.

I följande avsnitt ska vi titta närmare på det avtal som gör det möjligt för SPA-redigeraren att koppla komponenter inom SPA till AEM-komponenter för att uppnå denna smidiga redigeringsupplevelse.

1. Läs in WKND SPA-projektprogrammet i redigeraren och växla till läget **Förhandsgranska**.

   `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`

1. Kontrollera sidans innehåll med hjälp av webbläsarens inbyggda utvecklarverktyg. Använd markeringsverktyget och markera en redigerbar komponent på sidan och visa elementinformationen.

   Komponenten har ett nytt dataattribut, `data-cq-data-path`.

   ![Kontrollerar WKND SPA-projektelement](assets/wknd-inspector.png)

   Till exempel

   `data-cq-data-path="/content/wknd-spa-react/us/en/home/jcr:content/root/responsivegrid/text`

   Den här sökvägen tillåter hämtning och associering av konfigurationsobjektet för redigeringssammanhanget för varje komponent.

   Det här är det enda markeringsattribut som krävs för att redigeraren ska kunna identifiera det som en redigerbar komponent i SPA-filen. Utifrån det här attributet avgör SPA-redigeraren vilken redigerbar konfiguration som är kopplad till komponenten, så att rätt bildruta, verktygsfält och så vidare läses in.

   Vissa specifika klassnamn läggs också till för att markera platshållare och för att dra och släppa resurser.

   >[!NOTE]
   >
   >Det här beteendet skiljer sig från serversidans återgivna sidor i AEM, där ett `cq`-element infogas för varje redigerbar komponent.
   >
   >Med den här metoden i SPA-redigeraren tar du bort behovet av att mata in anpassade element, bara genom att förlita dig på ett extra dataattribut, vilket förenklar markeringen för klientutvecklaren.

## Headless and Headless in AEM {#headful-headless}

SPA-program kan aktiveras med flexibla integrationsnivåer inom AEM, inklusive SPA-program som utvecklats och underhålls utanför AEM. SPA kan också användas i AEM och samtidigt använda AEM för att leverera innehåll till ytterligare slutpunkter utan huvudproblem.

>[!TIP]
>
>Mer information finns i dokumentet [Headful and Headless in AEM](/help/implementing/developing/headful-headless.md).

## Nästa steg {#next-steps}

Nu när du förstår redigeringsupplevelsen av SPA i AEM och hur en SPA hör ihop med SPA-redigeraren kan du fördjupa dig i hur en SPA byggs.

* [Komma igång med SPA i AEM med hjälp av React](getting-started-react.md) visar hur en grundläggande SPA har skapats för att fungera med SPA-redigeraren i AEM med hjälp av React
* [Komma igång med SPA-program i AEM med Angular](getting-started-angular.md) visar hur en grundläggande SPA-fil har skapats för att fungera med SPA-redigeraren i AEM med Angular
* [Översikt över SPA-redigeraren](editor-overview.md) går in mer i kommunikationsmodellen mellan AEM och SPA.
* [Utveckla SPA för AEM](developing.md) beskriver hur gränssnittsutvecklare kan engagera sig i utvecklingen av en SPA för AEM och hur SPA interagerar med AEM arkitektur.
