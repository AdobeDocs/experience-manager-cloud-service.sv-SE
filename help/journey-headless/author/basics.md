---
title: Lär dig grunderna i redigering
description: Lär dig mer om hur du skapar innehåll för Headless CMS med hjälp av Content Fragments.
exl-id: 3eca973f-b210-41bb-98da-ecbd2bae9803
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 0%

---

# Grundläggande om redigering för Headless med AEM {#author-headless-basics}

## Story hittills {#story-so-far}

I början av [AEM Headless Content Author Journey](overview.md) innehöll [Introduction](introduction.md) grundläggande begrepp och terminologi som är relevant för redigering utan rubrik.

Den här artikeln bygger vidare på dessa artiklar så att du förstår hur du skapar ditt eget innehåll för AEM headless-projekt.

## Syfte {#objective}

* **Målgrupp**: Nybörjare
* **Mål**: Introducera grunderna för Headless CMS-redigering:
   * Introduktion till utveckling med AEMaaCS
   * Introduktion till innehållsfragment

## Grundläggande hantering {#basic-handling}

Innan du får grepp om innehållsfragment finns det en (mycket) snabb introduktion till AEM...men ingenting ersätter faktiskt upplevelsen av att logga in och försöka använda systemet.

### Författare, Förhandsgranska och Publish {#author-preview-publish}

En AEM brukar bestå av tre miljöer:

* Författare
* Publish
* Förhandsgranska

Du loggar in på och använder redigeringsmiljön för att generera ditt innehåll. När det är klart publicerar du sedan innehållet så att det blir allmänt tillgängligt. För hemlösa är detta för andra program, för webbsidor är det för läsare på webben.

Mer information finns i Authoring Concepts.

Från konsolen **Innehållsfragment** kan du även publicera till **förhandsgranskningstjänsten**, för testning och förhandsgranskning, före Publish. Se Publicera och förhandsgranska ett fragment.

### Loggar in {#signing-in}

Precis som med de flesta system måste du logga in. Som författare får du:

* Användarnamn (konto)
* Lösenord
* Länk till inloggningsskärmen

Ditt konto har konfigurerats med de privilegier du behöver. Om du har några problem rekommenderar Adobe att du kontaktar ditt interna projektsupportteam.

### Navigering {#navigation}

Första gången du loggar in i en liten onlinekurs kommer några av huvudfunktionerna i användargränssnittet att markeras.

Du kan sedan använda navigeringspanelen för att komma åt AEM nyckelområden. För innehållsfragment använder du konsolen **Innehållsfragment** (för vissa åtgärder använder du även konsolen **Assets**).

Du kan öppna navigeringspanelen genom att markera ikonen Adobe i det övre vänstra hörnet följt av den lilla kompasikonen.

<!--
The Navigation Panel can be opened by selecting Adobe icon at the top left, followed by the small compass icon:

![Navigation panel](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)
-->

>[!NOTE]
>Innehållsfragment är en funktion i AEM **Webbplatser**, men de sparas som **Assets**. Detta är en teknisk detalj som inte bör påverka dig, men som kan vara användbar att känna till.

I konsolen kan du välja mappar i den vänstra panelen för att navigera till ditt innehållsfragment. Du kan också filtrera och/eller söka.

![Konsolen för innehållsfragment](/help/sites-cloud/administering/content-fragments/assets/cf-managing-console-filter.png)

### funktionsmakron, markera, visa {#actions-selecting-viewing}

I konsolen **Innehållsfragment** finns ett antal åtgärder tillgängliga för dina innehållsfragment från verktygsfältet:

<!-- ![Console actions](assets/cfm-managing-cf-console-01.png) -->

* **Öppna i Assets**
* **Skapa**
* Kolumnen **Refererad av** innehåller också en direktlänk som visar alla överordnade referenser till det fragmentet, inklusive referenser till innehållsfragment, Experience Fragments och sidor.
* Vid hovring över mappnamnet visas JCR-sökvägen.

När du har valt fragmentet är alla lämpliga åtgärder tillgängliga:

<!-- ![Console actions - fragment selected](assets/cfm-managing-cf-console-selected-01.png) -->

* **Öppna**
* **Publish** (och **Avpublicera**)
* **Kopiera**
* **Flytta**
* **Byt namn**
* **Ta bort**

>[!NOTE]
>
>Åtgärder som Publish, Unpublish, Delete, Move, Rename, Copy, trigger an asynchronous job. Jobbets förlopp kan övervakas via gränssnittet AEM asynkrona jobb.

<!--
The **Assets** console has dedicated **Action Toolbars**, and **Quick Actions** that you can use after selecting a resource (for example, a folder or content fragment).

The Quick Actions are available for a single resource, see **Basel** in the example below:

![Quick Actions](/help/journey-headless/author/assets/headless-journey-author-navigation-05.png)

The Actions Toolbar provides access to the full range of actions - applicable for the current scenario. The actions available can change; for example, dependent on your location, or whether you have selected multiple resources:

![Action Toolbar](/help/journey-headless/author/assets/headless-journey-author-navigation-06.png)

You can select the format for viewing your resources with the View Selector:

![View Selector](/help/journey-headless/author/assets/headless-journey-author-navigation-03.png)

You can view additional information about items using the Rail Selector. This also gives access to additional actions.

![Left Rail](/help/journey-headless/author/assets/headless-journey-author-navigation-04.png)
-->

## Skapa innehållsfragment {#authoring-content-fragments}

Det var en mycket snabb introduktion till AEM användargränssnitt, men du har förhoppningsvis haft en chans att testa det. Nu kommer vi till ditt verkliga intresse - innehållsfragment för Headless.

Vi måste gå igenom allt från början till slut, men din instans kanske redan har mappar och/eller fragment skapade, och dessa kan finnas på olika platser. Principerna är desamma.

### Ordna och navigera {#organizing-and-navigating}

Om du inte har ett fåtal innehållsfragment vill du ordna dem så att du (och andra) kan hitta dem igen.

#### Skapa en mapp {#creating-folder}

Du kan göra detta genom att skapa en serie mappar i avsnittet **Filer** i **Assets**-konsolen. Välj alternativet **Skapa** (överst till höger) följt av **Mapp**:

![Alternativet Skapa mapp](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

En dialogruta öppnas där du kan ange informationen och sedan bekräfta med **Skapa**:

![Dialogrutan Skapa mapp](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### Använda banor och taggar för att begränsa antalet modeller för innehållsfragment i mappen {#tags-paths-for-models-in-folder}

Det här avsnittet är något mer avancerat. Du behöver det egentligen inte om du just har börjat och försöker saker, men det är *mycket* användbart när du har många fragment. Så det är bra att veta om - även om du inte använder det helt än.

Din innehållsarkitekt har skapat alla innehållsfragmentmodeller som krävs för ditt aktuella projekt, och kanske även några andra projekt. För att göra det enklare för dig själv och andra författare kan du begränsa listan med modeller som är tillgängliga för en viss mapp.

När du har skapat mappen kan du öppna mappen **Egenskaper**. Här finns olika flikar med information och konfigurationsinformation om mappen. Särskilt för innehållsfragment kan du använda fliken **Profiler** för att definiera specifika sökvägar och/eller taggar för den här mappen. Detta begränsar vilka modeller för innehållsfragment som är tillgängliga för användning i mappen, eftersom det innebär att modeller för innehållsfragment måste uppfylla dessa krav innan de kan användas för att generera fragment i den här mappen.

![Skapa mappegenskaper - principer](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>Du kan läsa mer under Modeller för innehållsfragment - Tillåt modeller för innehållsfragment i din Assets-mapp.

Du navigerar sedan genom de här mapparna för att skapa och redigera dina innehållsfragment.

#### Precis in case - Konfiguration av mappkonfiguration {#cloud-services-folder}

Bara om..

Du kommer antagligen att få en inledande mapp där du kan skapa dina mappar. Detta beror på att viss konfigurationsinformation måste tillämpas (vanligtvis av en utvecklare eller systemadministratör) på rotmappen. Detta intresserar dig förmodligen inte, men om det behövs kan du kontrollera **Konfiguration** i **Cloud Service** i mappen **Egenskaper**:

![Skapa mappegenskaper - Konfiguration](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>Du kan läsa mer under Använd konfigurationen i din Assets-mapp.

### Skapa ett innehållsfragment {#creating-fragment}

I konsolen **Innehållsfragment** kan du använda **Skapa** för att öppna dialogrutan **Nytt innehållsfragment**:

![Konsolen för innehållsfragment - Skapar ett nytt fragment](/help/sites-cloud/administering/content-fragments/assets/cfc-console-create.png)

Ange:

* **Plats**
* **Modell för innehållsfragment**
* **Titel**
* **Namn**
* **Beskrivning**

Bekräfta sedan med antingen **Skapa** eller **Skapa och öppna**.

### Redigera ett fragment {#editing-fragment}

Du kan öppna ett fragment omedelbart efter att du har skapat det, eller genom att välja det från konsolen för innehållsfragment (även från Assets-konsolen).

>[!NOTE]
>
>Innehållsfragment är en webbplatsfunktion, men lagras som **Assets**.
>
>Det finns två redigerare för att skapa innehållsfragment.
>
>* Den nya redigeraren, som huvudsakligen nås från konsolen **Innehållsfragment** .
>* Den ursprungliga redigeraren, som främst nås från **Assets**-konsolen.

När redigeraren öppnas ser du:

* övre verktygsfältet: för nyckelinformation och åtgärder
   * en länk till konsolen för innehållsfragment (hemikonen)
   * information om modellen och mappen
   * länkar till förhandsgranskning, om standardmönstret för URL för förhandsgranskning har konfigurerats för modellen
   * Publish och Unpublish actions
   * ett alternativ för att visa alla **överordnade referenser** (länkikon)
   * fragmentet **Status** och den senast sparade informationen
   * växla till den ursprungliga (Assets-baserade) redigeraren
* vänster panel: visar **Variationer** för innehållsfragmentet och dess **fält**:
   * dessa länkar kan användas för att navigera i strukturen för innehållsfragment
* höger panel: visar flikar med egenskaper (metadata) och taggar, information om versionshistorik och information om språkkopior
   * på fliken **Egenskaper** kan du uppdatera **Title** och **Description** för fragmentet, eller **Variation**
* central panel: visar de faktiska fälten och innehållet i den valda varianten
   * gör att du kan redigera innehållet
   * om **platshållarfält** definieras i den modell de visas här och kan användas för navigering

Ett fragment kan till exempel:

* Kräver flera uppgifter, andra med en viss typ. För rubrikfritt innehåll är referenser viktiga (du lär dig mer om dem senare under din resa).

* Gör att du kan skriva ett långt textavsnitt. Här finns ytterligare alternativ för att hantera och formatera texten. Du kan även öppna enskilda textfält i en helskärmsredigerare (med den lilla skärmliknande ikonen till höger)

![Content Fragment Editor - Alaska Spirits](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-overview.png)

>[!NOTE]
>
>Projektspecifik dokumentation kan behövas för att hjälpa författare med detaljer om hur vissa fält kan fyllas i.
>
>Se Modeller för innehållsfragment - Datatyper och egenskaper för allmän information.

Bekräfta uppdateringarna med **Spara** eller **Spara och stäng**.

>[!NOTE]
>
>Mer information finns i Variationer - Skapa innehållsfragment.

#### Det du (antagligen) inte behöver oroa dig för {#what-you-probably-do-not-need-to-worry-about}

OK, det kan verka lite konstigt, men så fort du öppnar Content Fragment Editor och börjar utforska kan du se olika alternativ som (förmodligen) inte gäller för din resa som innehållsförfattare. Så det här är bara en snabbtitt på vad du bör ignorera i det headlesssammanhanget:

* **Modeller för innehållsfragment**

  Du kan se namnet på modellen för innehållsfragment på den högra panelen i redigeraren. Det här är också en länk som tar dig till modellredigeraren.
Modeller för innehållsfragment är faktiskt viktiga för dina innehållsfragment när de definierar den struktur som du använder. Men att skapa och redigera dem är (vanligtvis) en annan persons ansvar, innehållsarkitekten.

  >[!NOTE]
  >
  >Om du vill veta mer kan du läsa den AEM Headless Content Architect Journey.

### Publicering {#publishing}

<!-- needs more details -->

När du har slutfört fragmentet kan du **Publish** så att det blir tillgängligt för de headless-program som använder det.

Publiceringsåtgärderna är tillgängliga i redigeraren:

![Innehållsfragmentredigeraren - Mitt fragment](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

>[!NOTE]
>
>Du kan också publicera ditt fragment från konsolen **Assets** eller **Innehållsfragment** .

## What&#39;s Next {#whats-next}

Nu när du har lärt dig grunderna är nästa steg att [Lär dig mer om referenser](references.md). Här presenteras och diskuteras de olika referenser som finns tillgängliga och hur du skapar strukturnivåer med Fragment References - en viktig del i utvecklingen för headless.

## Ytterligare resurser {#additional-resources}

* [Authoring Concepts](/help/sites-cloud/authoring/author-publish.md)

* [Grundläggande hantering](/help/sites-cloud/authoring/basic-handling.md) - Den här sidan är primärt baserad på konsolen **Platser**, men många/de flesta funktioner är också relevanta för att skapa **innehållsfragment** under konsolen **Assets**.

   * [Navigeringspanel](/help/sites-cloud/authoring/basic-handling.md#navigation-panel)

   * [Sidhuvudet](/help/sites-cloud/authoring/basic-handling.md#the-header)

   * [Åtgärdsverktygsfältet](/help/sites-cloud/authoring/basic-handling.md#actions-toolbar)

   * [Snabbåtgärder](/help/sites-cloud/authoring/basic-handling.md#quick-actions)

   * [Visa och välja resurser](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)

   * [Järnvägsväljare](/help/sites-cloud/authoring/basic-handling.md#rail-selector)

* [Arbeta med innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md)

   * [Hantera innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md)

   * [Använd konfigurationen i din Assets-mapp](/help/sites-cloud/administering/content-fragments/setup.md#apply-the-configuration-to-your-folder)

   * [Skapa ett innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment)

   * [Skapa innehållsfragment](/help/sites-cloud/administering/content-fragments/authoring.md)

   * Publicering

      * Från redigeraren eller **Assets**-konsolen

         * [Snabb Publish](/help/assets/manage-publication.md#quick-publish)

         * [Hantera publikation](/help/assets/manage-publication.md#manage-publication)

      * Från konsolen **Innehållsfragment**

         * [Publicera och förhandsgranska ett innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment)

   * [Modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)

      * [Modeller för innehållsfragment - datatyper](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)

      * [Modeller för innehållsfragment - egenskaper](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#properties)

      * [Modeller för innehållsfragment - Tillåt modeller för innehållsfragment i din Assets-mapp](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#allowing-content-fragment-models-assets-folder)

* [Content Fragments - original editor, from Assets Console](/help/assets/content-fragments/content-fragments-variations.md)

* Komma igång-guider
   * [Skapa en huvudlös Assets-mapp](/help/headless/setup/create-assets-folder.md)

* AEM Headless Content Architect Journey

* AEM översättningsresa utan rubrik
