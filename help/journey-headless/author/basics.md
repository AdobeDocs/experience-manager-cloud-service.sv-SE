---
title: Lär dig grunderna i redigering
description: Lär dig mer om hur du skapar innehåll för Headless CMS med hjälp av Content Fragments.
exl-id: 3eca973f-b210-41bb-98da-ecbd2bae9803
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1708'
ht-degree: 1%

---

# Grundläggande om redigering för Headless med AEM {#author-headless-basics}

## Story hittills {#story-so-far}

I början av [AEM Headless Content Author Journey](overview.md) den [Introduktion](introduction.md) har omfattat de grundläggande begrepp och termer som är relevanta för utvecklingen av headless.

Den här artikeln bygger vidare på dessa artiklar så att du förstår hur du skapar ditt eget innehåll för AEM headless-projekt.

## Syfte {#objective}

* **Målgrupp**: Nybörjare
* **Syfte**: Introducing the basics of Headless CMS Authoring:
   * Introduktion till utveckling med AEMaaCS
   * Introduktion till innehållsfragment

## Grundläggande hantering {#basic-handling}

Innan du får grepp om innehållsfragment finns det en (mycket) snabb introduktion till att använda AEM...men ingenting ersätter faktiskt upplevelsen av att logga in och försöka använda systemet.

### Skapa, förhandsgranska och publicera {#author-preview-publish}

En AEM brukar bestå av tre miljöer:

* Författare
* Publicera
* Förhandsgranska

Du loggar in på och använder redigeringsmiljön för att generera ditt innehåll. När det är klart publicerar du sedan innehållet så att det blir allmänt tillgängligt. För hemlösa är detta för andra program, för webbsidor är det för läsare på webben.

Mer information finns i Authoring Concepts.

Från **Innehållsfragment** konsolen kan du även publicera på **Förhandsgranskningstjänst**, för testning och förhandsgranskning, före publicering. Se Publicera och förhandsgranska ett fragment.

### Loggar in {#signing-in}

Precis som med de flesta system måste du logga in. Som författare får du:

* Användarnamn (konto)
* Lösenord
* Länk till inloggningsskärmen

Ditt konto har konfigurerats med de privilegier du behöver. Om du har problem rekommenderar vi att du kontaktar ditt interna projektsupportteam.

### Navigering {#navigation}

Första gången du loggar in i en liten onlinekurs kommer några av huvudfunktionerna i användargränssnittet att markeras.

Du kan sedan använda navigeringspanelen för att komma åt AEM nyckelområden. För innehållsfragment använder du **Innehållsfragment** konsol (för vissa åtgärder använder du även **Resurser** konsol).

Du kan öppna navigeringspanelen genom att markera ikonen Adobe i det övre vänstra hörnet följt av den lilla kompasikonen.

<!--
The Navigation Panel can be opened by selecting Adobe icon at the top left, followed by the small compass icon:

![Navigation panel](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)
-->

>[!NOTE]
>Innehållsfragment är en funktion i AEM **Webbplatser**, sparas de som **Resurser**. Detta är en teknisk detalj som inte bör påverka dig, men som kan vara användbar att känna till.

I konsolen kan du välja mappar i den vänstra panelen för att navigera till ditt innehållsfragment. Du kan också filtrera och/eller söka.

![Konsol för innehållsfragment](/help/sites-cloud/administering/content-fragments/assets/cfc-console-filter.png)

### funktionsmakron, markera, visa {#actions-selecting-viewing}

I **Innehållsfragment** konsol: en rad åtgärder är tillgängliga för dina innehållsfragment från verktygsfältet:

<!-- ![Console actions](assets/cfm-managing-cf-console-01.png) -->

* **Öppna i resurser**
* **Skapa**
* The **Refererad av** Kolumnen innehåller också en direkt länk för att visa alla överordnade referenser till det fragmentet. inklusive referenser till innehållsfragment, upplevelsefragment och sidor.
* Vid hovring över mappnamnet visas JCR-sökvägen.

När du har valt fragmentet är alla lämpliga åtgärder tillgängliga:

<!-- ![Console actions - fragment selected](assets/cfm-managing-cf-console-selected-01.png) -->

* **Öppna**
* **Publicera** (och **Avpublicera**)
* **Kopiera**
* **Flytta**
* **Byt namn**
* **Ta bort**

>[!NOTE]
>
>Åtgärder som Publicera, Avpublicera, Ta bort, Flytta, Byt namn, Kopiera, utlöser ett asynkront jobb. Jobbets förlopp kan övervakas via gränssnittet AEM asynkrona jobb.

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

Det var en mycket snabb introduktion till AEM användargränssnitt, men du har förhoppningsvis haft en chans att prova det. Nu kommer vi till ditt verkliga intresse - innehållsfragment för Headless.

Vi måste gå igenom allt från början till slut, men din instans kanske redan har mappar och/eller fragment skapade, och dessa kan finnas på olika platser. Principerna är desamma.

### Ordna och navigera {#organizing-and-navigating}

Om du inte har ett fåtal innehållsfragment vill du ordna dem så att du (och andra) kan hitta dem igen.

#### Skapa en mapp {#creating-folder}

Du kan göra detta genom att skapa en serie mappar i **Filer** i **Resurser** konsol. Välj **Skapa** alternativ (överst till höger), följt av **Mapp**:

![Alternativet Skapa mapp](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

En dialogruta öppnas där du kan ange information och sedan bekräfta med **Skapa**:

![Dialogrutan Skapa mapp](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### Använda banor och taggar för att begränsa vilka modeller för innehållsfragment som finns i mappen {#tags-paths-for-models-in-folder}

Det här avsnittet är något mer avancerat. Du behöver det inte om du bara börjar och provar saker, men det är *mycket* är användbart när du har många fragment. Så det är bra att veta om - även om du inte använder det helt än.

Din innehållsarkitekt har skapat alla innehållsfragmentmodeller som krävs för ditt aktuella projekt, och kanske även några andra projekt. För att göra det enklare för dig själv och andra författare kan du begränsa listan med modeller som är tillgängliga för en viss mapp.

När du har skapat mappen kan du öppna den **Egenskaper**. Här finns olika flikar med information och konfigurationsinformation om mappen. Du kan använda kommandot **Profiler** om du vill definiera specifika sökvägar och/eller taggar för den här mappen. Detta begränsar vilka modeller för innehållsfragment som är tillgängliga för användning i mappen, eftersom det innebär att modeller för innehållsfragment måste uppfylla dessa krav innan de kan användas för att generera fragment i den här mappen.

![Skapa mappegenskaper - principer](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>Du kan läsa mer under Modeller för innehållsfragment - Tillåt modeller för innehållsfragment i resursmappen.

Du navigerar sedan genom de här mapparna för att skapa och redigera dina innehållsfragment.

#### Precis in case - konfiguration av mappkonfiguration {#cloud-services-folder}

Bara om..

Du kommer antagligen att få en inledande mapp där du kan skapa dina mappar. Detta beror på att viss konfigurationsinformation måste tillämpas (vanligtvis av en utvecklare eller systemadministratör) på rotmappen. Det här intresserar dig förmodligen inte, men om det behövs kan du kontrollera **Konfiguration** i **Cloud Services** i mappen **Egenskaper**:

![Skapa mappegenskaper - Konfiguration](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>Du kan läsa mer under Använd konfigurationen i resursmappen.

### Skapa ett innehållsfragment {#creating-fragment}

I **Innehållsfragment** konsol du kan använda **Skapa** för att öppna **Nytt innehållsfragment** dialog:

![Konsol för innehållsfragment - Skapa ett nytt fragment](/help/sites-cloud/administering/content-fragments/assets/cfc-console-create.png)

Ange:

* **Plats**
* **Modell för innehållsfragment**
* **Titel**
* **Namn**
* **Beskrivning**

Bekräfta sedan med antingen **Skapa** eller **Skapa och öppna**.

<!--
Creating a Content Fragment is very similar - you just use the **Content Fragment** option instead:

![Create Content Fragment option](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

This time a wizard opens. The first step is to select the Content Fragment Model that your fragment is based on:

![Create Content Fragment - select Model](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

After continuing with **Next** you can supply the details (**Basic** and **Advanced**) for your fragment:

![Create Content Fragment - provide Name](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

Confirm with **Create** and you can then **Open** your fragment in the editor.
-->

### Redigera ett fragment {#editing-fragment}

Du kan öppna ett fragment omedelbart efter att du har skapat det, eller genom att välja det från konsolen för innehållsfragment (även från konsolen Resurser).

När redigeraren öppnas ser du:

* En lista med ikoner till vänster - det ger dig tillgång till olika funktionsområden. Redigeraren öppnas i **Variationer** är det här den mesta redigeringen görs. Du kan också vara intresserad av **Anteckningar** och **Metadata** -tabbar.

* En rubrik med information om fragmentet och åtkomst till olika åtgärder.

* Huvudområdet för redigering - det beror på vilken modell som används för att skapa fragmentet.

Exempel:

* Ett fragment som bara kräver flera informationsdelar, vissa med en viss typ. För headless-innehåll är referenser viktiga och du kommer att lära dig mer om dem senare under din resa.

  ![Content Fragment Editor - My Fragment](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* Ett fragment som gör att du kan skriva ett långt textavsnitt. Här finns ytterligare alternativ för att hantera och formatera texten. Du kan till och med öppna de enskilda textfälten i en helskärmsredigerare (med den lilla skärmliknande ikonen till höger)

  ![Content Fragment Editor - Alaska Spirits](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>Projektspecifik dokumentation kan behövas för att hjälpa författare med detaljer om hur vissa fält kan fyllas i.
>
>Se Modeller för innehållsfragment - Datatyper och egenskaper för allmän information.

Bekräfta dina uppdateringar med antingen **Spara** eller **Spara och stäng**.

>[!NOTE]
>
>Mer information finns i Variationer - Skapa innehållsfragment.

#### Det du (antagligen) inte behöver oroa dig för {#what-you-probably-do-not-need-to-worry-about}

OK, det här kan verka lite konstigt, men när du väl har öppnat Content Fragment Editor och börjat utforska ser du olika alternativ som (förmodligen) inte gäller för din resa som innehållsförfattare. Så det här är bara en snabbtitt på vad du bör ignorera i det headlesssammanhanget:

* **Modeller för innehållsfragment**

  Namnet på innehållsfragmentmodellen visas längst upp i redigeraren, direkt under fragmentnamnet. Det här är också en länk som tar dig till modellredigeraren.
Modeller för innehållsfragment är faktiskt viktiga för dina innehållsfragment när de definierar den struktur som du använder. Men att skapa och redigera dem är (vanligtvis) en annan persons ansvar, innehållsarkitekten.

  >[!NOTE]
  >
  >Om du vill veta mer kan du läsa den AEM Headless Content Architect Journey.

* **Associerat innehåll**

  Den här är ganska självklar eftersom den är en flik i redigeraren.

  Innehållsfragment har varit tillgängliga i AEM i ganska många versioner. Ursprungligen var de tillgängliga för&quot;traditionell&quot; användning vid redigering av sidor....och de används fortfarande i detta sammanhang. Detta kan innebära att resurser (till exempel bilder) som inte är inbäddade i fragmentet måste vara tillgängliga för författaren när sidan redigeras.

* **Förhandsgranska**

  Det här är en annan flik i redigeraren och ger en teknisk vy som främst är avsedd för utvecklare.

* **Uppdatera sidreferenser**

  Den här åtgärden är tillgänglig från **...** (ellipser) listruta. Det är inte intressant för skribenter utan rubrik när det gäller att skapa sidor.

### Publicering {#publishing}

<!-- needs more details -->

När du är klar med fragmentet kan du **Publicera** så att den blir tillgänglig för headless-applikationer.

Publiceringsåtgärderna är tillgängliga i redigeraren:

![Content Fragment Editor - My Fragment](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

>[!NOTE]
>
>Du kan även publicera ditt fragment från **Resurser** eller **Innehållsfragment** konsol.

## What&#39;s Next {#whats-next}

Nu när du har lärt dig grunderna är nästa steg att [Läs mer om referenser](references.md). Här presenteras och diskuteras de olika referenser som finns tillgängliga och hur du skapar strukturnivåer med Fragment References - en viktig del i utvecklingen för headless.

## Ytterligare resurser {#additional-resources}

* [Redigeringsbegrepp](/help/sites-cloud/authoring/getting-started/concepts.md)

* [Grundläggande hantering](/help/sites-cloud/authoring/getting-started/basic-handling.md) - den här sidan är huvudsakligen baserad på **Webbplatser** konsol, men många/de flesta funktioner är också relevanta för redigering **Innehållsfragment** under **Resurser** konsol.

   * [Navigeringspanel](/help/sites-cloud/authoring/getting-started/basic-handling.md#navigation-panel)

   * [Sidhuvudet](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)

   * [Verktygsfältet Åtgärd](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)

   * [Snabbåtgärder](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)

   * [Visa och välja resurser](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   * [Järnvägsväljare](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

* [Arbeta med innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments.md)

   * [Hantera innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md)

   * [Använd konfigurationen i resursmappen](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

   * [Skapa ett innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#creating-a-content-fragment)

   * [Variationer - Skapa innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md)

   * Publicering

      * från redigeraren, eller **Resurser** konsol

         * [Snabbpublicering](/help/assets/manage-publication.md#quick-publish)

         * [Hantera publikation](/help/assets/manage-publication.md#manage-publication)

      * Från **Innehållsfragment** Konsol

         * [Publicera och förhandsgranska ett innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#publishing-and-previewing-a-fragment)

   * [Modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)

      * [Modeller för innehållsfragment - datatyper](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#data-types)

      * [Modeller för innehållsfragment - egenskaper](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#properties)

      * [Modeller för innehållsfragment - Tillåt modeller för innehållsfragment i resursmappen](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

* Komma igång-guider
   * [Skapa en huvudlös konfiguration för resursmapp](/help/headless/setup/create-assets-folder.md)

* AEM Headless Content Architect Journey

* AEM Headless Translation Journey
