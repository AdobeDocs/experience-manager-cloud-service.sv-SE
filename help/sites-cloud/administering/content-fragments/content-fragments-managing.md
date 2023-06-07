---
title: Hantera innehållsfragment
description: Lär dig hur du använder konsolen Innehållsfragment för att hantera AEM innehållsfragment. för framtagning av sidor, eller som bas för ditt headless-innehåll.
feature: Content Fragments
role: User
exl-id: fc4497cb-85ac-4d2d-aca4-588541266f0b
source-git-commit: 6063c587c1d65587c44e551f3a5c2f3c34ced011
workflow-type: tm+mt
source-wordcount: '2071'
ht-degree: 1%

---

# Hantera innehållsfragment {#managing-content-fragments}

Lär dig använda **Innehållsfragment** för att hantera AEM. Dessa kan användas för att skapa sidor eller som bas för ditt headless-innehåll.

När du har definierat [Modeller för innehållsfragment](#creating-a-content-model) kan du använda dessa för [skapa dina innehållsfragment](#creating-a-content-fragment).

The [Innehållsfragmentsredigerare](#opening-the-fragment-editor) innehåller olika [lägen](#modes-in-the-content-fragment-editor) för att göra det möjligt att

* [Redigera innehållet](#editing-the-content-of-your-fragment) och [hantera variationer](#creating-and-managing-variations-within-your-fragment)
* [Anteckna ditt fragment](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Associera innehåll med fragment](#associating-content-with-your-fragment)
* [Konfigurera metadata](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Visa strukturträdet](/help/sites-cloud/administering/content-fragments/content-fragments-structure-tree.md)
* [Förhandsgranska JSON-representationen](/help/sites-cloud/administering/content-fragments/content-fragments-json-preview.md)


>[!NOTE]
>
>Innehållsfragment kan användas:
>
>* vid framtagning av sidor, se [Sidredigering med innehållsfragment](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
>* for [Headless Content Delivery using Content Fragments with GraphQL](/help/sites-cloud/administering/content-fragments/content-fragments-graphql.md).


>[!NOTE]
>
>Innehållsfragment lagras som **Resurser**. De hanteras huvudsakligen från **Innehållsfragment** konsolen, men kan även hanteras från [Resurser](/help/assets/content-fragments/content-fragments-managing.md) konsol.

## Konsolen Innehållsfragment {#content-fragments-console}

Konsolen för innehållsfragment ger direktåtkomst till dina fragment och relaterade uppgifter. Mer information finns i:

* [Grundläggande struktur och hantering av konsolen för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#basic-structure-handling-content-fragments-console)

* [Information om dina innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#information-content-fragments)

* [Åtgärder för ett innehållsfragment i konsolen för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#actions-selected-content-fragment)

* [Anpassa de kolumner som är tillgängliga i konsolen för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#select-available-columns)

* [Söka och filtrera i konsolen för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#filtering-fragments)

## Skapa innehållsfragment {#creating-content-fragments}

### Skapa en innehållsmodell {#creating-a-content-model}

[Modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-models.md) kan aktiveras och skapas innan du skapar innehållsfragment med strukturerat innehåll.

### Skapa ett innehållsfragment {#creating-a-content-fragment}

Så här skapar du ett innehållsfragment:

1. Från **Innehållsfragment** konsol, välj **Skapa** (överst till höger).

   >[!NOTE]
   >
   >Om du vill ha platsen för det nya fragmentet fördefinierad kan du navigera till mappen där du vill skapa fragmentet, eller ange platsen när du skapar fragmentet.

1. The **Nytt innehållsfragment** öppnas en dialogruta där du kan ange:

   * **Plats** - den här fylls i automatiskt med den aktuella platsen, men du kan välja en annan plats om det behövs
   * **Content Fragment Model** - välj den modell som ska användas som bas för fragmentet i listrutan.
   * **Titel**
   * **Namn** - detta slutförs automatiskt baserat på **Titel**, men du kan redigera det om det behövs
   * **Beskrivning**

   ![Dialogrutan Nytt innehållsfragment](assets/cfm-managing-new-cf-01.png)

1. Välj **Skapa**, eller **Skapa och öppna** för att behålla din definition.

## Status för innehållsfragment {#statuses-content-fragments}

Under dess existens kan ett innehållsfragment ha flera statusvärden, vilket visas i [Konsol för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-console.md):

* **Nytt**
Ett nytt innehållsfragment har skapats, men varken redigerats eller öppnats i redigeraren för innehållsfragment.
* **Utkast**
Någon har antingen redigerat eller öppnat (nytt) innehållsfragment i Content Fragment Editor - men det har ännu inte publicerats.
* **Publicerad**
Innehållsfragmentet har publicerats.
* **Ändrad**
Innehållsfragmentet har redigerats efter att det publicerades (men innan ändringen publicerades).
* **Opublicerad**
Innehållsfragmentet har avpublicerats.

## Öppna fragmentredigeraren {#opening-the-fragment-editor}

Så här öppnar du fragmentet för redigering:

>[!CAUTION]
>
>Om du vill redigera ett innehållsfragment behöver du [lämpliga behörigheter](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). Kontakta systemadministratören om du har problem.

1. Använd **Innehållsfragment** konsol för att navigera till platsen för ditt innehållsfragment.
1. Öppna fragmentet för redigering genom att markera fragmentet och sedan **Öppna** i verktygsfältet.

1. Fragmentredigeraren öppnas. Gör önskade ändringar:

   ![fragmentredigerare](assets/cfm-managing-03.png)

1. När du har gjort ändringar använder du **Spara**, **Spara och stäng** eller **Stäng** efter behov.

   >[!NOTE]
   >
   >**Spara och stäng** är tillgängligt via **Spara** listruta.

   >[!NOTE]
   >
   >Båda **Spara och stäng** och **Stäng** kommer att avsluta redigeraren - se [Spara, stäng och versioner](#save-close-and-versions) om du vill ha fullständig information om hur de olika alternativen fungerar för innehållsfragment.

## Lägen och åtgärder i Content Fragment Editor {#modes-actions-content-fragment-editor}

Det finns olika lägen och åtgärder tillgängliga från Content Fragment Editor.

### Lägen i Content Fragment Editor {#modes-in-the-content-fragment-editor}

Navigera genom de olika lägena med ikonerna på sidopanelen:

* Variationer: [Redigera innehållet](#editing-the-content-of-your-fragment) och [Hantera variationer](#creating-and-managing-variations-within-your-fragment)

* [Anteckningar](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Associerat innehåll](#associating-content-with-your-fragment)
* [Metadata](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Strukturträd](/help/sites-cloud/administering/content-fragments/content-fragments-structure-tree.md)
* [Förhandsgranska](/help/sites-cloud/administering/content-fragments/content-fragments-json-preview.md)

![lägen](assets/cfm-managing-04.png)

### Verktygsfältsåtgärder i redigeraren för innehållsfragment {#toolbar-actions-in-the-content-fragment-editor}

Vissa funktioner i det övre verktygsfältet finns i flera lägen:

![lägen](assets/cfm-managing-top-toolbar.png)

* Ett meddelande visas när fragmentet redan refereras på en innehållssida. Du kan **Stäng** meddelandet.

* Sidpanelen kan döljas/visas med **Växla sidopanel** ikon.

* Under fragmentnamnet kan du se namnet på [Content Fragment Model](/help/sites-cloud/administering/content-fragments/content-fragments-models.md) används för att skapa det aktuella fragmentet:

   * Namnet är också en länk som öppnar modellredigeraren.

* Se fragmentets status. information om när den skapades, ändrades eller publicerades. Statusen är även färgkodad:

   * **Nytt**: grå
   * **Utkast**: blå
   * **Publicerad**: grön
   * **Ändrad**: orange
   * **Inaktiverad**: röd

* **Spara** ger åtkomst till **Spara och stäng** alternativ.

* De tre punkterna (**...**) ger åtkomst till ytterligare åtgärder:
   * **Uppdatera sidreferenser**
      * Detta uppdaterar eventuella sidreferenser.
   * **[Snabbpublicering](/help/assets/manage-publication.md#quick-publish)**
   * **[Hantera publikation](/help/assets/manage-publication.md#manage-publication)**

<!--
This updates any page references and ensures that the Dispatcher is flushed as required. -->

## Spara, stäng och versioner {#save-close-and-versions}

>[!NOTE]
>
>Versioner kan också [har skapats, jämförts och återställts från tidslinjen](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

Redigeraren har olika alternativ:

* **Spara** och **Spara och stäng**

   * **Spara** sparar de senaste ändringarna och finns kvar i redigeraren.
   * **Spara och stäng** sparar de senaste ändringarna och avslutar redigeraren.

   >[!CAUTION]
   >
   >Om du vill redigera ett innehållsfragment behöver du [lämpliga behörigheter](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). Kontakta systemadministratören om du har problem.

   >[!NOTE]
   >
   >Du kan vara kvar i redigeraren och göra en serie ändringar innan du sparar.

   >[!CAUTION]
   >
   >Förutom att bara spara ändringarna uppdaterar åtgärderna alla referenser och ser till att Dispatcher rensas efter behov. Dessa ändringar kan ta tid att bearbeta. På grund av detta kan prestandan påverkas på ett stort/komplext/tungt belastat system.
   >
   >Tänk på detta när du använder **Spara och stäng** och sedan snabbt ange fragmentredigeraren igen för att göra och spara ytterligare ändringar.

* **Stäng**

   Avslutar redigeraren utan att spara de senaste ändringarna (d.v.s. gjorda sedan den senaste **Spara**).

När du redigerar ditt innehållsfragment skapar AEM automatiskt versioner för att säkerställa att tidigare innehåll kan återställas om du avbryter ändringarna (med **Stäng** utan att spara):

1. När ett innehållsfragment öppnas för redigering AEM söker efter den cookie-baserade token som anger om en *redigeringssession* finns:

   1. Om token hittas betraktas fragmentet som en del av den befintliga redigeringssessionen.
   2. Om token är *not* är tillgängligt och användaren börjar redigera innehåll, en version skapas och en token för den nya redigeringssessionen skickas till klienten, där den sparas i en cookie.

2. Medan det finns en *aktiv* redigeringssession sparas det innehåll som redigeras automatiskt var 600:e sekund (standard).

   >[!NOTE]
   >
   >Intervallet för att spara automatiskt kan konfigureras med `/conf` mekanism.
   >
   >Standardvärde, se:
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. Om användaren avbryter redigeringen återställs den version som skapades i början av redigeringssessionen och token tas bort för att avsluta redigeringssessionen.
4. Om användaren väljer **Spara** redigeringarna, de uppdaterade elementen/varianterna bevaras och token tas bort för att avsluta redigeringssessionen.

## Redigera innehållet i fragmentet {#editing-the-content-of-your-fragment}

När du har öppnat fragmentet kan du använda [Variationer](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md) för att skapa ditt innehåll.

## Skapa och hantera variationer i fragment {#creating-and-managing-variations-within-your-fragment}

När du har skapat det Överordnad innehållet kan du skapa och hantera [Variationer](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md) av det innehållet.

## Koppla innehåll till fragment {#associating-content-with-your-fragment}

Du kan också [associera innehåll](/help/sites-cloud/administering/content-fragments/content-fragments-assoc-content.md) med ett fragment. Detta ger en anslutning så att resurser (t.ex. bilder) kan användas (valfritt) med fragmentet när det läggs till på en innehållssida.

## Visa och redigera metadata (egenskaper) för fragmentet {#viewing-and-editing-the-metadata-properties-of-your-fragment}

Du kan visa och redigera egenskaperna för ett fragment med [Metadata](/help/sites-cloud/administering/content-fragments/content-fragments-metadata.md) -fliken.

## Publicera och förhandsgranska ett fragment {#publishing-and-previewing-a-fragment}

Du kan publicera dina innehållsfragment till:

* den **[Publiceringstjänst](/help/overview/architecture.md#runtime-architecture)** - för fullständig, offentlig åtkomst

* den **[Förhandsgranskningstjänst](/help/overview/architecture.md#runtime-architecture)** - förhandsgranska innehållet innan det är fullständigt tillgängligt

   >[!CAUTION]
   Publicera innehållsfragment till **Förhandsgranskningstjänst** är bara tillgängligt från [Konsol för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-console.md); med **Publicera** åtgärd.

   >[!NOTE]
   Mer information om förhandsvisningsmiljöerna finns i:
   * [Hantera miljöer](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)
   * [Konfigurera OSGi-inställningar för förhandsgranskningsnivån](/help/implementing/preview-tier/preview-tier-configuring-osgi.md#configuring-osgi-settings-for-the-preview-tier)
   * [Förhandsvisa felsökning med Developer Console](/help/implementing/preview-tier/preview-tier-configuring-osgi.md#debugging-preview-using-the-developer-console)


Publicera dina innehållsfragment med **Publicera** i verktygsfältet i [Konsol för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#actions-selected-content-fragment):

>[!CAUTION]
Om fragmentet är baserat på en modell bör du se till att [modellen har publicerats](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
Om du publicerar ett innehållsfragment för vilket modellen ännu inte har publicerats, visas detta i en urvalslista och modellen publiceras med fragmentet.

1. Markera ett eller flera av fragmenten i listan.

1. Välj **Publicera** och sedan något av följande för att öppna rätt dialogruta:

   * **Nu** - välj antingen **Publiceringstjänst** eller **Förhandsgranskningstjänst**; efter bekräftelse publiceras fragmentet omedelbart
   * **Schema** - förutom den obligatoriska tjänsten kan du även välja datum och tid då fragmentet ska publiceras

   Vid behov måste du ange vilka referenser som ska publiceras. Som standard publiceras referenser även till förhandsgranskningstjänsten för att säkerställa att det inte finns någon brytning i innehållet.
För en schemalagd publiceringsbegäran:
   ![Dialogrutan Publicera](assets/cfm-publish-01.png)

1. Bekräfta publiceringsåtgärden.

Du kan även publicera på **Publiceringstjänst** från [Innehållsfragmentsredigerare](#toolbar-actions-in-the-content-fragment-editor) med:
* **Snabbpublicering**
* **Hantera publikation**

>[!NOTE]
Efter [publicera en sida som använder fragmentet](/help/sites-cloud/authoring/fundamentals/content-fragments.md#publishing); fragmentet kommer att listas i sidreferenserna.

>[!CAUTION]
När ett fragment har publicerats och/eller refererats visar AEM en varning när en författare öppnar fragmentet för redigering igen. Detta är för att varna för att ändringar i avsnittet även påverkar de refererade sidorna.

## Avpublicera ett fragment {#unpublishing-a-fragment}

Om du vill avpublicera innehållsfragment markerar du ett eller flera fragment och sedan **Avpublicera** i verktygsfältet i [Konsol för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#actions-selected-content-fragment). Du kan välja **Nu** eller **Schemalagd**.

När dialogrutan öppnas kan du välja rätt tjänst:
![Dialogrutan Avpublicera](assets/cfm-unpublish-01.png)

>[!NOTE]
The **Avpublicera** åtgärden visas bara när publicerade fragment är tillgängliga.

>[!CAUTION]
Om fragmentet redan refereras från ett annat fragment, eller från en sida, visas ett varningsmeddelande och du måste bekräfta att du vill fortsätta.

## Ta bort ett fragment {#deleting-a-fragment}

Så här tar du bort ett fragment:

1. I **Innehållsfragment** konsolen navigerar till platsen för innehållsfragmentet.
2. Markera fragmentet.

   >[!NOTE]
   The **Ta bort** åtgärden är inte tillgänglig som en snabbåtgärd.

3. Välj **Ta bort** i verktygsfältet.
4. Bekräfta **Ta bort** åtgärd.

   >[!CAUTION]
   Om fragmentet redan refereras från ett annat fragment, eller från en sida, visas ett varningsmeddelande och du måste bekräfta att du vill fortsätta med ett **Tvinga borttagning**. Fragmentet, tillsammans med dess innehållskomponentfragment, tas bort från alla innehållssidor.

## Söka efter överordnade referenser för ditt fragment {#parent-references-fragment}

Information om överordnade referenser finns i **Referenser** kolumn i [Konsol för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#information-content-fragments).

## Hitta språkkopior av fragmentet {#language-copies-fragment}

Information om språkkopior finns på **Språk** kolumn i [Konsol för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-console.md#information-content-fragments).

## Tidslinje för innehållsfragment {#timeline-for-content-fragments}

>[!NOTE]
Den här funktionen är bara tillgänglig i **Resurser** konsol

Förutom standardalternativen [Tidslinje](/help/assets/manage-digital-assets.md#timeline) innehåller både information och åtgärder som är specifika för innehållsfragment:

* Visa information om versioner, kommentarer och anteckningar
* Åtgärder för versioner

   * **[Återgå till den här versionen](#reverting-to-a-version)** (välj ett befintligt fragment och sedan en specifik version)

   * **[Jämför med aktuell](#comparing-fragment-versions)** (välj ett befintligt fragment och sedan en specifik version)

   * Lägg till en **Etikett** och/eller **Kommentar** (välj ett befintligt fragment och sedan en specifik version)

   * **Spara som version** (markera ett befintligt fragment och sedan uppilen längst ned på tidslinjen)

* Åtgärder för anteckningar

   * **Ta bort**

>[!NOTE]
Kommentarerna är:
* Standardfunktionalitet för alla resurser
* Skapat i tidslinjen
* Relaterat till fragmentresursen
>
Anteckningar (för innehållsfragment) är:
* Anges i fragmentredigeraren
* Specifik för ett markerat textsegment i fragmentet
>


Till exempel:

![tidslinje](assets/cfm-managing-05.png)

## Jämföra fragmentversioner {#comparing-fragment-versions}

>[!NOTE]
Den här funktionen är bara tillgänglig i **Resurser** konsol

The **Jämför med aktuell** finns tillgänglig från [Tidslinje](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) när du har valt en viss version.

Detta öppnas:

* den **Aktuell** (senaste) version (vänster)

* den valda versionen **v&lt;*x.y*>** (höger)

De visas sida vid sida, där:

* Eventuella skillnader markeras

   * Borttagen text - röd
   * Infogad text - grön
   * Ersatt text - blå

* Med helskärmsikonen kan du öppna båda versionerna separat; växla sedan tillbaka till den parallella vyn
* Du kan **Återställ** till den specifika versionen
* **Klar** kommer du tillbaka till konsolen

>[!NOTE]
Du kan inte redigera fragmentinnehållet när du jämför fragment.

![jämföra](assets/cfm-managing-06.png)

## Återställa till en version  {#reverting-to-a-version}

>[!NOTE]
Den här funktionen är bara tillgänglig i **Resurser** konsol

Du kan återgå till en viss version av fragmentet:

* Direkt från [Tidslinje](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

   Välj önskad version och sedan **Återgå till den här versionen** åtgärd.

* while [jämföra en version med den aktuella versionen](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#comparing-fragment-versions) du kan **Återställ** till den valda versionen.
