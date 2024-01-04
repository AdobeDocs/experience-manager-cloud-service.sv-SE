---
title: Skapa innehåll med den universella redigeraren
description: Se hur enkelt och intuitivt det är för skribenter att skapa innehåll med den universella redigeraren.
exl-id: 15fbf5bc-2e30-4ae7-9e7f-5891442228dd
source-git-commit: 16f2922a3745f9eb72f7070c30134e5149eb78ce
workflow-type: tm+mt
source-wordcount: '2165'
ht-degree: 0%

---


# Skapa innehåll med den universella redigeraren {#authoring}

Se hur enkelt och intuitivt det är för skribenter att skapa innehåll med den universella redigeraren.

{{universal-editor-status}}

## Introduktion {#introduction}

Med den universella redigeraren kan du redigera alla delar av innehållet i alla implementeringar så att du kan leverera enastående upplevelser, öka innehållets hastighet och skapa en toppmodern utvecklarupplevelse.

För att göra detta har den universella redigeraren ett intuitivt användargränssnitt som kräver minimal utbildning för att man ska kunna börja redigera material. I det här dokumentet beskrivs hur du skapar i Universell redigerare.

>[!TIP]
>
>En mer detaljerad introduktion till Universal Editor finns i dokumentet [Introduktion till Universal Editor.](introduction.md)

## Förbered appen {#prepare-app}

Om du vill skapa innehåll för ett program med den universella redigeraren måste appen vara instrumenterad av en utvecklare för att stödja redigeraren.

>[!TIP]
>
>Se [Komma igång med Universal Editor i AEM](getting-started.md) om du vill se ett exempel på hur du konfigurerar ett AEM program så att det fungerar med den universella redigeraren.

## Logga in {#sign-in}

När programmet har instrumenterats för att fungera med den universella redigeraren loggar du in i den universella redigeraren. Du behöver en Adobe ID för att logga in och [har tillgång till den universella redigeraren.](getting-started.md#request-access)

När du har loggat in anger du URL-adressen till sidan som du vill redigera i dialogrutan [platsfält.](#location-bar) så att du kan börja redigera innehåll som [textinnehåll](#text-mode) eller [mediainnehåll.](#media-mode)

## Förstå användargränssnittet {#ui}

Gränssnittet är indelat i dessa huvudområden.

* [Rubriken Experience Cloud](#experience-cloud-header)
* [Verktygsfältet för den universella redigeraren](#universal-editor-toolbar)
* [Redigeraren](#editor)
* [Egenskapsfältet](#properties-rail)

![Universellt redigeringsgränssnitt](assets/ui.png)

### Sidhuvudet Experience Cloud {#experience-cloud-header}

Sidhuvudet Experience Cloud finns alltid längst upp på skärmen. Det är en ankarpunkt som talar om var du befinner dig i Experience Cloud och som hjälper dig att navigera till andra program i Experience Cloud.

![Rubriken Experience Cloud](assets/experience-cloud-header.png)

#### Experience Manager {#experience-manager}

Klicka på länken Adobe Experience Cloud till vänster om rubriken för att navigera till roten för din Experience Manager-lösning för att komma åt verktyg som [Cloud Manager,](/help/onboarding/cloud-manager-introduction.md) [Cloud Acceleration Manager,](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md) och [Programvarudistribution.](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html)

![Knappen Global navigering](assets/global-navigation.png)

#### Organisation {#organization}

Här visas den organisation du är inloggad på. Välj om du vill byta till en annan organisation om din Adobe ID är kopplad till flera.

![Organisationsindikator](assets/organization.png)

#### Lösningar {#solutions}

Om du trycker eller klickar på lösningens väljare kan du snabbt gå över till andra Experience Cloud-lösningar.

![Lösningsväljare](assets/solutions.png)

#### Hjälp {#help}

Hjälpikonen ger snabb åtkomst till utbildningsresurser och supportresurser.

![Hjälp](assets/help.png)

#### Meddelanden {#notifications}

Den här ikonen är märkt med antalet tilldelade ofullständiga [meddelanden.](/help/implementing/cloud-manager/notifications.md)

![Meddelanden](assets/notifications.png)

#### Användaregenskaper {#user-properties}

Välj den ikon som representerar användaren för att få åtkomst till dina användarinställningar. Om du inte har konfigurerat någon användarbild tilldelas ikonen slumpmässigt.

![Användaregenskaper](assets/user-properties.png)

### Verktygsfältet för den universella redigeraren {#universal-editor-toolbar}

Verktygsfältet för den universella redigeraren visas alltid längst upp på skärmen precis nedanför [Experience Cloud.](#experience-cloud-header) Du får snabb åtkomst för att navigera till en annan sida för att redigera och publicera den aktuella sidan.

![Verktygsfältet för den universella redigeraren](assets/universal-editor-toolbar.png)

#### Hemknappen {#home-button}

Hemknappen återgår till startsidan för Universal Editor

![Hamburger-menyn](assets/home-button.png)

På startsidan anger du URL-adressen till den webbplats som du vill redigera med Universal Editor.

![Startsida](assets/start-page.png)

>[!NOTE]
>
>Alla sidor som du vill redigera med Universal Editor måste vara [som har stöd för Universal Editor.](getting-started.md)

#### Platsfält {#location-bar}

Platsfältet visar adressen till sidan som du redigerar. Välj det här alternativet om du vill ange adressen till en annan sida som ska redigeras.

![Platsfält](assets/location-bar.png)

>[!TIP]
>
>Använda snabbtangenten `L` för att öppna adressfältet.

>[!NOTE]
>
>Alla sidor som du vill redigera med Universal Editor måste vara [som har stöd för Universal Editor.](getting-started.md)

#### Inställningar för autentiseringshuvud {#authentication-settings}

Välj ikonen med inställningar för autentiseringshuvudet om du behöver [ange en anpassad autentiseringshuvud för lokal utveckling.](/help/implementing/universal-editor/developer-overview.md#auth-header)

![Inställningsknapp för autentiseringsrubriker](assets/authentication-header-settings.png)

#### Emulatorinställningar {#emulator}

Välj emuleringsikonen för att definiera hur den universella redigeraren ska återge sidan.

![Emulatorikon](assets/emulator.png)

Om du trycker eller klickar på emuleringsikonen visas alternativen.

![Emuleringsalternativ](assets/emulation-options.png)

Som standard öppnas redigeraren i skrivbordslayout där höjd och bredd definieras automatiskt av webbläsaren.

Du kan också välja att emulera en mobil enhet och i Universell redigerare:

* Definiera dess orientering
* Definiera bredd och höjd
* Ändra orientering

#### Förhandsgranskningsläge {#preview-mode}

I förhandsgranskningsläget återges sidan i redigeraren som den skulle se ut i din publicerade tjänst. Det gör att innehållsförfattaren kan navigera i innehållet genom att klicka på länkar och så vidare.

![Förhandsgranskningsläge](assets/preview-mode.png)

>[!TIP]
>
>Använda snabbtangenten `P` för att växla till och från förhandsgranskningsläge.

#### Öppna programförhandsgranskning {#open-app-preview}

Välj ikonen för förhandsgranskning av öppna program om du vill öppna sidan som du redigerar på en egen webbläsarflik, utan redigeraren, för att förhandsgranska innehållet.

![Öppna appförhandsgranskning](assets/open-app-preview.png)

>[!TIP]
>
>Använda snabbtangenten `O` (bokstaven O) för att öppna förhandsgranskningen av programmet.

#### Publicera {#publish}

Välj publiceringsknappen så att du kan publicera ändringarna i innehållet live för att användas av läsarna.

![Knappen Publicera](assets/publish.png)

>[!TIP]
>
>Se dokumentet [Publicera innehåll med den universella redigeraren](publishing.md) för mer information om publicering med Universal Editor.

### Redigeraren {#editor}

Redigeraren tar upp större delen av fönstret och är där sidan som anges i [platsfältet](#location-bar) återges.

![Redigerare](assets/editor.png)

Om redigeraren är i [förhandsgranskningsläge,](#preview-mode) innehållet kommer att kunna navigeras och du kan följa länkar, men du kan inte redigera innehållet.

### Properties Rail {#properties-rail}

Egenskapsfältet visas alltid längs den högra sidan av redigeraren. Beroende på dess läge kan det visa information för en komponent som är markerad i innehållet eller hierarkin för sidinnehållet.

![Egenskapsfältet](assets/component-rail.png)

#### Egenskapsläge {#properties-mode}

I egenskapsläget visar rälen egenskaperna för den komponent som är markerad i redigeraren. Det här är standardläget för egenskapsfältet när en sida läses in.

![Egenskapsläge](assets/properties-mode.png)

Beroende på vilken typ av komponent du väljer kan information visas och ändras i egenskapsfältet.

![Komponentinformation](assets/component-details.png)

Alla komponenter har inte information som kan visas och/eller redigeras.

>[!TIP]
>
>Använda snabbtangenten `D` för att växla till egenskapsläge.

#### Läge för innehållsträd {#content-tree-mode}

I innehållsträdsläge visar rälen sidinnehållets hierarki.

![Läge för innehållsträd](assets/content-tree-mode.png)

När du väljer ett objekt i innehållsträdet rullar redigeraren till det innehållet och markerar det.

![Innehållsträd](assets/content-tree.png)

>[!TIP]
>
>Använda snabbtangenten `F` för att växla till innehållsträdsläge.

##### Redigera {#edit}

När du redigerar visas alternativen för den markerade komponenten i egenskapsfältet, där du kan redigera den markerade komponenten. Om den markerade komponenten är ett innehållsfragment kan du även välja redigeringsknappen.

![Ikonen Redigera](assets/edit.png)

Om du trycker eller klickar på redigeringsknappen öppnas knappen [Innehållsfragmentsredigerare](/help/assets/content-fragments/content-fragments-managing.md#opening-the-fragment-editor) på en ny flik. Detta ger dig tillgång till den fulla kraften i Content Fragment Editor för att redigera det tillhörande innehållsfragmentet.

Beroende på arbetsflödets behov kan du behöva redigera innehållsfragmentet i den universella redigeraren eller direkt i redigeraren för innehållsfragment.

>[!TIP]
>
>Använda snabbtangenten `E` om du vill redigera en markerad komponent.

##### Lägg till {#add}

Om du väljer en behållarkomponent i innehållsträdet eller i redigeraren visas alternativet Lägg till i egenskapsfältet.

![Ikonen Lägg till](assets/ue-add-component-icon.png)

Om du trycker eller klickar på knappen Lägg till öppnas en listruta med komponenter som är tillgängliga för [lägg till i den markerade behållaren.](#adding-components)

![Lägg till snabbmeny](assets/add-context-menu.png)

>[!TIP]
>
>Använda snabbtangenten `A` om du vill lägga till en komponent i en markerad behållarkomponent.

##### Ta bort {#delete}

Om du markerar en komponent i en behållarkomponent antingen i innehållsträdet eller i redigeraren visas borttagningsalternativet på egenskapslisten.

![Ikonen Ta bort](assets/ue-delete-component-icon.png)

Tryck eller klicka på knappen Ta bort [tar bort komponenten.](#deleting-components)

>[!TIP]
>
>Använda snabbtangenten `Shift+Backspace` om du vill ta bort en markerad komponent från en behållare.

## Redigera innehåll {#editing-content}

Det är enkelt och intuitivt att redigera innehåll. När du för musen över innehåll i redigeraren markeras redigerbart innehåll med en blå ruta.

![Redigerbart innehåll markeras med en blå ruta](assets/editable-content.png)

>[!TIP]
>
>Som standard markeras det för redigering när du trycker eller klickar på ett innehåll. Om du vill navigera i innehållet genom att följa länkar växlar du till [förhandsgranskningsläge.](#preview-mode)

Beroende på vilket innehåll du väljer kan du ha olika redigeringsalternativ på plats och du kan få ytterligare information och alternativ för innehållet i [Egenskaper.](#properties-rail)

### Redigera oformaterad text {#edit-plain-text}

Du kan redigera texten på plats genom att dubbelklicka eller dubbeltrycka på komponenten.

![Redigera innehåll](assets/editing-content.png)

Tryck på Enter eller välj utanför textrutan för att spara ändringarna.

När du väljer att markera textkomponenten visas informationen om den i egenskapsfältet. Du kan också redigera texten på rälsen.

![Redigera text i egenskapsfältet](assets/ue-editing-text-component-rail.png)

Dessutom finns information om texten i egenskapsfältet. Ändringarna sparas automatiskt när fokus lämnar det redigerade fältet i egenskapsfältet.

### Redigera RTF {#edit-rich-text}

Du kan redigera texten på plats genom att dubbelklicka eller dubbeltrycka på komponenten.

Tryck på Enter eller välj utanför textrutan för att spara ändringarna.

![Redigera en RTF-komponent](assets/rich-text-editing.png)

Dessutom finns formateringsalternativ och information om texten i egenskapsfältet. Ändringarna sparas automatiskt när fokus lämnar det redigerade fältet i egenskapsfältet.

### Redigera media {#edit-media}

Du kan visa informationen i egenskapsfältet.

![Redigera media](assets/ue-edit-media.png)

1. Tryck eller klicka på förhandsvisningen av den markerade bilden i egenskapsfältet.
1. The [resursväljare](/help/assets/asset-selector.md#using-asset-selector) öppnas så att du kan välja en resurs.
1. Välj för att välja en ny resurs.
1. Välj **Välj** för att gå tillbaka till egenskapsfältet där tillgången ersattes.

Ändringarna sparas automatiskt i innehållet.

### Redigera innehållsfragment {#edit-content-fragment}

Om du väljer en [Innehållsfragment,](/help/sites-cloud/administering/content-fragments/overview.md) Du kan redigera informationen i egenskapsfältet.

![Redigera ett innehållsfragment](assets/ue-edit-cf.png)

De fält som definieras i innehållsmodellen för det valda innehållsfragmentet visas och kan redigeras i egenskapsfältet.

Om du markerar ett fält som är relaterat till ett innehållsfragment läses innehållsfragmentet in i komponentspåret och fältet rullas automatiskt till.

Ändringarna sparas automatiskt när fokus lämnar det redigerade fältet i egenskapsfältet.

Om du vill redigera ditt innehållsfragment i dialogrutan [Innehållsfragmentsredigerare](/help/sites-cloud/administering/content-fragments/authoring.md) i stället klickar du på [redigeringsknapp](#edit) i lägesrälen.

Beroende på arbetsflödets behov kan du behöva redigera innehållsfragmentet i den universella redigeraren eller direkt i redigeraren för innehållsfragment.

### Lägga till komponenter i behållare {#adding-components}

1. Markera en behållarkomponent i innehållsträdet eller i redigeraren.
1. Välj sedan ikonen Lägg till i egenskapsfältet.

   ![Välja en komponent som ska läggas till i en behållare](assets/ue-add-component.png)

Komponenten infogas i behållaren och kan redigeras i redigeraren.

>[!TIP]
>
>Använda snabbtangenten `A` om du vill lägga till en komponent i den markerade behållaren.

### Ta bort komponenter från behållare {#deleting-components}

1. Markera en behållarkomponent i innehållsträdet eller i redigeraren.
1. Markera ikonen för avfasning för behållaren för att expandera dess innehåll i innehållsträdet.
1. Markera sedan en komponent i behållaren i innehållsträdet.
1. Markera borttagningsikonen i egenskapsfältet.

   ![Ta bort en komponent](assets/ue-delete-component.png)

Den markerade komponenten har tagits bort.

>[!TIP]
>
>Använda snabbtangenten `Shift+Backspace` om du vill ta bort den markerade komponenten från dess behållare.

### Ändra ordning på komponenter i behållare {#reordering-components}

1. Markera en behållarkomponent i innehållsträdet eller i redigeraren.
1. Om inte redan [content tree-läge,](#content-tree-mode) växla till den.
1. Markera ikonen för avfasning för behållaren för att expandera dess innehåll i innehållsträdet.
1. Dra handtagsikonerna intill komponenterna i behållaren för att visa att du kan ordna om dem. Dra komponenterna för att ordna om dem i behållaren.

   ![Ändra ordning på komponenter](assets/ue-reordering-components.png)

1. Den dragna komponenten blir grå i komponentträdet, medan insättningspunkten representeras av en blå linje. Släpp komponenten för att placera den på dess nya plats.

Komponenterna ordnas om i både innehållsträdet och i redigeraren

## Förhandsgranska innehåll {#previewing-content}

När du är klar med redigeringen av innehållet vill du ofta navigera i det och se hur det ser ut i innehållet på andra sidor. I [förhandsgranskningsläge](#preview-mode) Du kan klicka på länkar för att navigera i innehållet som en läsare skulle kunna. Innehållet återges i redigeraren på samma sätt som det publiceras.

I förhandsgranskningsläget fungerar knapptryckning eller klickning på innehåll på samma sätt som för en läsare av innehållet. Om du vill markera innehållet för redigering växlar du bort från [förhandsgranskningsläge.](#preview-mode)

## Ytterligare resurser {#additional-resources}

Mer information om Universal Editor finns i de här dokumenten.

* [Introduktion till Universal Editor](introduction.md) - Lär dig hur den universella redigeraren möjliggör redigering av alla aspekter av innehåll i alla implementeringar, så att du kan leverera enastående upplevelser, öka innehållets hastighet och skapa en toppmodern utvecklarupplevelse.
* [Publicera innehåll med den universella redigeraren](publishing.md) - Lär dig hur den universella redigeraren publicerar innehåll och hur dina appar kan hantera det publicerade innehållet.
* [Komma igång med Universal Editor i AEM](getting-started.md) - Lär dig hur du får tillgång till den universella redigeraren och hur du börjar använda den i ditt första AEM.
* [Universal Editor Architecture](architecture.md) - Lär dig mer om arkitekturen i den universella redigeraren och hur data flödar mellan tjänster och lager.
* [Attribut och typer](attributes-types.md) - Läs mer om de dataattribut och datatyper som krävs för den universella redigeraren.
* [Autentisering av universell redigerare](authentication.md) - Lär dig hur den universella redigeraren autentiseras.
