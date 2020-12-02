---
title: Experience Fragments
description: Använd Adobe Experience Manager som Cloud Service Experience Fragments för att göra upplevelserna återanvändbara och flexibla.
translation-type: tm+mt
source-git-commit: b7a2e86de27dbfcdecaf3a2bc1984678b7b69375
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 7%

---


# Experience Fragments {#experience-fragments}

Inom Adobe Experience Manager som Cloud Service, en Experience Fragment:
* är en grupp med en eller flera komponenter
* innehåller både innehåll och layout
* kan refereras inom sidor
* kan innehålla alla komponenter

An Experience Fragment:

* Är en del av en upplevelse (sida).
* Kan användas på flera sidor.
* Är baserad på en mall (endast redigerbar) för att definiera struktur och komponenter.
* Består av en eller flera komponenter, med layout, i ett styckesystem.
* Kan innehålla andra upplevelsefragment.
* Kan kombineras med andra komponenter (inklusive andra Experience Fragments) för att skapa en komplett sida (upplevelse).
* Kan ha olika variationer, som kan dela innehåll och/eller komponenter.
* Kan delas upp i byggstenar som kan användas i flera varianter av fragmentet.

Du kan använda Experience Fragments:

* Om en författare vill återanvända delar (ett fragment av en upplevelse) av en sida.
Utan Experience Fragments måste författaren kopiera och klistra in det fragmentet. Att skapa och underhålla dessa klipp-och-klistra-upplevelser är tidskrävande och leder ofta till användarfel.
Upplevelsefragment eliminerar behovet av att kopiera/klistra in.
* För att stödja headless CMS-fallstudier.
Författare vill bara använda AEM för att skapa, men inte för att leverera till kunden. Ett system/kontaktyta från tredje part skulle förbruka upplevelsen och sedan leverera till slutanvändaren.

>[!NOTE]
>
>Skrivåtkomst för upplevelsefragment kräver att användarkontot är registrerat i gruppen:
>
>* `experience-fragments-editors`
>
>
Kontakta systemadministratören om du har problem.

## När ska ni använda upplevelsefragment? {#when-should-you-use-experience-fragments}

Experience Fragments ska användas:

* När ni vill återanvända upplevelser.
   * Upplevelser som återanvänds med samma eller liknande innehåll.
* När du använder AEM som en innehållsleveransplattform för tredje part.
   * Alla lösningar som vill använda AEM som plattform för innehållsleverans.
   * Bädda in innehåll i kontaktpunkter från tredje part.
* Om du har en upplevelse med olika variationer eller renderingar.
   * Kanal- eller kontextspecifika varianter.
   * upplevelser som är begripliga att gruppera, till exempel en kampanj med olika upplevelser i olika kanaler.
* När ni använder Omnichannel Commerce.
   * Dela e-handelsrelaterat innehåll i [sociala medier](/help/implementing/developing/extending/experience-fragments.md#social-variations)-kanaler i stor skala.
   * Göra kontaktytor transaktionella.

## Organisera dina upplevelsefragment {#organizing-your-experience-fragments}

Det rekommenderas att
* använda mappar för att ordna dina upplevelsefragment,

* [konfigurera tillåtna mallar för dessa mappar](#configure-allowed-templates-folder).

Om du skapar mappar kan du:

* skapa en meningsfull struktur för era Experience Fragments, t.ex. efter klassificering

   >[!NOTE]
   >
   >Det är inte nödvändigt att anpassa strukturen för dina Experience Fragments till sidstrukturen på din plats.

* [allokera tillåtna mallar på mappnivå](#configure-allowed-templates-folder)

   >[!NOTE]
   >
   >Du kan använda [mallredigeraren](/help/sites-cloud/authoring/features/templates.md) för att skapa en egen mall.

WKND-projektet strukturerar vissa Experience Fragments enligt `Contributors`. Den struktur som används visar också hur andra funktioner, som Multi Site Management (inklusive språkkopior), kan användas.

Se:

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

![Mappar för Experience Fragments](/help/sites-cloud/authoring/assets/xf-folders.png)

## Skapa och konfigurera en mapp för dina Experience Fragments {#creating-and-configuring-a-folder-for-your-experience-fragments}

Om du vill skapa och konfigurera en mapp för dina Experience Fragments bör du:

1. [Skapa en mapp](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-folder).

1. [Konfigurera tillåtna Experience Fragment-mallar för den mappen](#configure-allowed-templates-folder).

>[!NOTE]
>
>Det går också att konfigurera [tillåtna mallar för din instans](#configure-allowed-templates-instance), men den här metoden **rekommenderas inte** eftersom värdena kan skrivas över vid uppgradering.

### Konfigurera tillåtna mallar för mappen {#configure-allowed-templates-folder}

>[!NOTE]
>
>Det här är den rekommenderade metoden för att ange **tillåtna mallar**, eftersom värdena inte skrivs över vid uppgradering.

1. Navigera till mappen **Experience Fragments**.

1. Markera mappen och **Egenskaper**.

1. Ange det reguljära uttrycket för att hämta de nödvändiga mallarna i fältet **Tillåtna mallar**.

   Till exempel:
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   Se:
   `http://localhost:4502/mnt/overlay/cq/experience-fragments/content/experience-fragments/folderproperties.html/content/experience-fragments/wknd`

   ![Upplevelsefragmentegenskaper - tillåtna mallar](/help/sites-cloud/authoring/assets/xf-folders-templates.png)

   >[!NOTE]
   >
   >Mer information finns i [Mallar för Experience Fragments](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments).

1. Välj **Spara och stäng**.

### Konfigurera tillåtna mallar för din instans {#configure-allowed-templates-instance}

>[!CAUTION]
>
>Du bör inte ändra **Tillåtna mallar** med den här metoden eftersom de angivna mallarna kan skrivas över vid uppgradering.
>
>Använd den här dialogrutan endast i informationssyfte.

1. Navigera till den obligatoriska **Experience Fragments**-konsolen.

1. Välj **Konfigurationsalternativ**:

   ![Knappen Konfiguration](/help/sites-cloud/authoring/assets/xf-18.png)

1. Ange de mallar som krävs i dialogrutan **Konfigurera Experience Fragments**:

   ![Konfigurera Experience Fragments](/help/sites-cloud/authoring/assets/xf-19.png)

   >[!NOTE]
   >
   >Mer information finns i [Mallar för Experience Fragments](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments).

1. Välj **Spara**.


## Skapa ett Experience Fragment {#creating-an-experience-fragment}

Så här skapar du ett Experience Fragment:

1. Välj **Experience Fragments** i Global Navigation.

   ![Upplev fragment på navigeringspanelen](/help/sites-cloud/authoring/assets/xf-01.png)

1. Navigera till önskad mapp och välj **Skapa**:

   ![Skapa en mapp för Experience Fragments](/help/sites-cloud/authoring/assets/xf-02.png)

1. Välj **Experience Fragment** för att öppna guiden **Skapa Experience Fragment**.

   Välj önskad **mall** och sedan **Nästa**:

   ![Välja en upplevelsefragmentmall](/help/sites-cloud/authoring/assets/xf-03.png)


1. Ange **egenskaperna** för **upplevelsefragmentet**.

   En **titel** är obligatorisk. Om **namnet** lämnas tomt hämtas det från **titeln**.

   ![Experience Fragment-egenskaper](/help/sites-cloud/authoring/assets/xf-04.png)

1. Klicka på **Skapa**.

   Ett meddelande visas. Välj:

   * **Återgå** inte till konsolen
   * **Öppna** fragmentredigeraren

## Redigera din upplevelsefragment {#editing-your-experience-fragment}

Experience Fragment Editor har funktioner som liknar den vanliga sidredigeraren.

>[!NOTE]
>
>Mer information om hur du använder sidredigeraren finns i [Redigera sidinnehåll](/help/sites-cloud/authoring/fundamentals/editing-content.md).

Följande exempelprocedur visar hur du skapar ett teaser för en produkt:

1. Dra och släpp den önskade komponenten från [komponentwebbläsaren](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).

1. Beroende på komponenten:
   * Lägg till innehåll och/eller resurser efter behov.
   * Konfigurera egenskaperna efter behov.

1. Lägg till fler komponenter efter behov.

Till exempel: `http://<host>:<port>/editor.html/content/experience-fragments/wknd/language-masters/en/contributors/stacey-roswells/master.html`

![Experience Fragment on page](/help/sites-cloud/authoring/assets/xf-05.png)

## Skapa en upplevelsefragmentvariant {#creating-an-experience-fragment-variation}

Ni kan skapa variationer av ert Experience Fragment, beroende på era behov:

1. Öppna fragmentet för [redigering](#editing-your-experience-fragment).
1. Öppna fliken **Variationer**.

   ![Skapa en Experience Fragment-variation](/help/sites-cloud/authoring/assets/xf-06.png)

1. **Med** CreateCreatekan du skapa:

   * **Variant**
   * **Variation som live-copy**.

1. Definiera de nödvändiga egenskaperna:

   * **Mall**
   * **Titel**
   * **Namn**  - Om det lämnas tomt hämtas det från titeln
   * **Beskrivning**
   * **Variationstaggar**

   Till exempel:

   ![Variantegenskaper](/help/sites-cloud/authoring/assets/xf-07.png)

1. Bekräfta med **Klar** visas den nya varianten på panelen.

## Använda ditt Experience Fragment {#using-your-experience-fragment}

Nu kan du använda din Experience Fragment när du redigerar dina sidor:

1. Öppna en sida för redigering.

1. Skapa en instans av Experience Fragment-komponenten i sidstyckesystemet:

1. Lägg till den faktiska Experience Fragment-funktionen i komponentinstansen. antingen:

   * Dra det önskade fragmentet från Resursläsaren och släpp det på komponenten.
   * Välj **Konfigurera** i komponentverktygsfältet och ange vilket fragment som ska användas, bekräfta med **Klar**.

   >[!NOTE]
   >
   >Redigera i komponentverktygsfältet fungerar som ett kortkommando för att öppna fragmentet i fragmentredigeraren.

Till exempel: `http://<host>:<port>/editor.html/content/wknd/language-masters/en/about-us.html`

![Upplevelsefragment i sidredigeraren](/help/sites-cloud/authoring/assets/xf-08.png)

## Byggblock {#building-blocks}

Du kan välja en eller flera komponenter för att skapa en byggsten för återvinning i fragmentet:

### Skapar ett byggblock {#creating-a-building-block}

Så här skapar du ett nytt byggblock:

1. Välj de komponenter som du vill återanvända i Experience Fragment-redigeraren:

   ![Välj komponent för byggblock](/help/sites-cloud/authoring/assets/xf-09.png)

1. Välj **Konvertera till byggblock** i komponentverktygsfältet:

   ![Knappen Byggblock](/help/sites-cloud/authoring/assets/xf-10.png)

1. Ange namnet på **byggblocket** och bekräfta med **Konvertera**:

   ![Namnbyggblock](/help/sites-cloud/authoring/assets/xf-11.png)

1. **Byggblocket** visas på den vänstra fliken (**Lokal**) och kan väljas för ytterligare åtgärder:

   ![Byggblock i rälen](/help/sites-cloud/authoring/assets/xf-12.png)

#### Hantera ett byggblock {#managing-a-building-block}

Byggblocket visas på fliken **Byggblock**. Följande åtgärder är tillgängliga för varje block:

* **Gå till master**: öppna mastervarianten på en ny flik
* **Byt namn på**
* **Ta bort**

![Hantera byggblock](/help/sites-cloud/authoring/assets/xf-13.png)

#### Använda ett byggblock {#using-a-building-block}

Du kan dra byggblocket till styckesystemet för vilket fragment som helst, precis som med vilken komponent som helst.

När du redigerar ett Experience Fragment visas tillgängliga byggblock på fliken till vänster. Du kan filtrera enligt:

* **Lokalt**  - Byggblock från det aktuella Experience Fragment
* **Alla**  - Byggblock från alla fragment

![Markera byggblock](/help/sites-cloud/authoring/assets/xf-14.png)

## Information om ditt Experience Fragment {#details-of-your-experience-fragment}

Information om ditt fragment kan ses:

1. Navigera till platsen för dina Experience Fragments (navigera inte längre till variationerna i fragmentet).
Detaljer visas i alla vyer av konsolen **Upplevelsefragment** och **listvyn** visar även information om export till Target: <!--Details are shown in all views of the **Experience Fragments** console, with the **List View** including details of an [export to Target](/help/sites-administering/experience-fragments-target.md):-->

   ![Information om Experience Fragment](/help/sites-cloud/authoring/assets/xf-15.png)

1. När du öppnar **Egenskaper** för Experience Fragment:

   ![Egenskapsknapp](/help/sites-cloud/authoring/assets/xf-16.png)

   Egenskaperna är tillgängliga på olika flikar:

   >[!CAUTION]
   >
   >Dessa flikar visas när du öppnar **Egenskaper** från konsolen Experience Fragments.
   >
   >Om du **öppnar egenskaperna** när du redigerar ett upplevelsefragment visas rätt [Sidegenskaper](/help/sites-cloud/authoring/fundamentals/page-properties.md).

   ![Experience Fragment-egenskaper](/help/sites-cloud/authoring/assets/xf-17.png)

   * **Grundläggande**
      * **Titel**  - obligatoriskt
      * **Beskrivning**
      * **Taggar**
      * **Totalt antal varianter**  - endast information
      * **Antal webbvarianter**  - endast information
      * **Antal icke-webbvarianter**  - endast information
      * **Antal sidor som använder detta fragment**  - endast information
   * **Cloud Services**
      * **Molnkonfiguration**
      * **Cloud Service Configurations**
      * **ID för Facebook-sida**
      * **Pinterest board**
   * **Referenser**
      * En lista med referenser
   * **Status för sociala medier**
      * Information om variationer i sociala medier

## Den vanliga HTML-återgivningen {#the-plain-html-rendition}

Om du använder `.plain.`-väljaren i URL:en kan du komma åt den vanliga HTML-återgivningen från webbläsaren.

>[!NOTE]
>
>Även om detta är direkt tillgängligt från webbläsaren är [det primära syftet att tillåta andra program (till exempel webbprogram från tredje part, anpassade mobilimplementeringar) att komma åt innehållet i Experience Fragment direkt, med enbart URL:en](/help/implementing/developing/extending/experience-fragments.md#the-plain-html-rendition).

## Exporterar Experience Fragments {#exporting-experience-fragments}

Som standard levereras Experience Fragments i HTML-format. Detta kan användas av både AEM och tredjepartskanaler.

JSON kan även användas för export till Adobe Target. Mer information finns i Målintegrering med Experience Fragments. <!--For export to Adobe Target, JSON can also be used. See [Target Integration with Experience Fragments](/help/sites-administering/experience-fragments-target.md) for full information.-->
