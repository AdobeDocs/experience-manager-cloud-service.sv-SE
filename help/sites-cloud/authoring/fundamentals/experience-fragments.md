---
title: Experience Fragments
description: Använd Adobe Experience Manager as a Cloud Service Experience Fragments för att göra upplevelserna återanvändbara och flexibla.
exl-id: 9dc33677-141f-47e5-a01e-6c7488686314
source-git-commit: 6d38886bf3f87be09dd897f615a471c4b8ddd6b7
workflow-type: tm+mt
source-wordcount: '1489'
ht-degree: 7%

---

# Upplevelsefragment {#experience-fragments}

Inom Adobe Experience Manager as a Cloud Service, en Experience Fragment:
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
>Kontakta systemadministratören om du har problem.

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
   * Dela e-handelsrelaterat innehåll på [sociala medier](/help/implementing/developing/extending/experience-fragments.md#social-variations) kanaler i stor skala.
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
   >Du kan använda [mallredigerare](/help/sites-cloud/authoring/features/templates.md) för att skapa en egen mall.

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
>Det går också att konfigurera [Tillåtna mallar för din instans](#configure-allowed-templates-instance), men den här metoden är **not** rekommenderas eftersom värdena kan skrivas över vid uppgradering.

### Konfigurera tillåtna mallar för mappen {#configure-allowed-templates-folder}

>[!NOTE]
>
>Detta är den rekommenderade metoden för att ange **Tillåtna mallar**, eftersom värdena inte skrivs över vid uppgraderingen.

1. Navigera till önskad **Upplevelsefragment** mapp.

1. Markera mappen och sedan **Egenskaper**.

1. Ange det reguljära uttrycket för hämtning av de nödvändiga mallarna i **Tillåtna mallar** fält.

   Till exempel:
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   Se:
   `http://localhost:4502/mnt/overlay/cq/experience-fragments/content/experience-fragments/folderproperties.html/content/experience-fragments/wknd`

   ![Upplevelsefragmentegenskaper - tillåtna mallar](/help/sites-cloud/authoring/assets/xf-folders-templates.png)

   >[!NOTE]
   >
   >Se [Mallar för Experience Fragments](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments) för mer information.

1. Välj **Spara och stäng**.

### Konfigurera tillåtna mallar för din instans {#configure-allowed-templates-instance}

>[!CAUTION]
>
>Vi rekommenderar inte att du ändrar **Tillåtna mallar** den här metoden eftersom de angivna mallarna kan skrivas över vid uppgradering.
>
>Använd den här dialogrutan endast i informationssyfte.

1. Navigera till önskad **Upplevelsefragment** konsol.

1. Välj **Konfigurationsalternativ**:

   ![Knappen Konfiguration](/help/sites-cloud/authoring/assets/xf-18.png)

1. Ange de mallar som krävs i **Konfigurera Experience Fragments** dialog:

   ![Konfigurera Experience Fragments](/help/sites-cloud/authoring/assets/xf-19.png)

   >[!NOTE]
   >
   >Se [Mallar för Experience Fragments](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments) för mer information.

1. Välj **Spara**.


## Skapa ett upplevelsefragment {#creating-an-experience-fragment}

Så här skapar du ett Experience Fragment:

1. Välj **Upplevelsefragment** från Global Navigation.

   ![Upplev fragment på navigeringspanelen](/help/sites-cloud/authoring/assets/xf-01.png)

1. Navigera till önskad mapp och markera **Skapa**:

   ![Skapa en mapp för Experience Fragments](/help/sites-cloud/authoring/assets/xf-02.png)

1. Välj **Experience Fragment** för att öppna **Skapa upplevelsefragment** guide.

   Välj önskad **mall** och sedan **Nästa**:

   ![Välja en upplevelsefragmentmall](/help/sites-cloud/authoring/assets/xf-03.png)


1. Ange **egenskaperna** för **upplevelsefragmentet**.

   A **Titel** är obligatoriskt. Om **Namn** är tom kommer den att härledas från **Titel**.

   ![Experience Fragment-egenskaper](/help/sites-cloud/authoring/assets/xf-04.png)

1. Klicka **Skapa**.

   Ett meddelande visas. Välj:

   * **Klar** för att återgå till konsolen
   * **Öppna** för att öppna fragmentredigeraren

## Redigera din upplevelsefragment {#editing-your-experience-fragment}

Experience Fragment Editor har funktioner som liknar den vanliga sidredigeraren.

>[!NOTE]
>
>Se [Redigera sidinnehåll](/help/sites-cloud/authoring/fundamentals/editing-content.md) om du vill ha mer information om hur du använder sidredigeraren.

Följande exempelprocedur visar hur du skapar ett teaser för en produkt:

1. Dra och släpp önskad komponent från [Komponentbläddraren](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).

1. Beroende på komponenten:
   * Lägg till innehåll och/eller resurser efter behov.
   * Konfigurera egenskaperna efter behov.

1. Lägg till fler komponenter efter behov.

Till exempel: `http://<host>:<port>/editor.html/content/experience-fragments/wknd/language-masters/en/contributors/stacey-roswells/master.html`

![Experience Fragment on page](/help/sites-cloud/authoring/assets/xf-05.png)

## Skapa en upplevelsefragmentvariant {#creating-an-experience-fragment-variation}

Ni kan skapa variationer av ert Experience Fragment, beroende på era behov:

1. Öppna fragmentet för [redigera](#editing-your-experience-fragment).
1. Öppna **Variationer** -fliken.

   ![Skapa en Experience Fragment-variation](/help/sites-cloud/authoring/assets/xf-06.png)

1. **Skapa** kan du skapa:

   * **Variant**
   * **Variation som live-copy**.

1. Definiera de nödvändiga egenskaperna:

   * **Mall**
   * **Titel**
   * **Namn** - Om det lämnas tomt kommer det att härledas från titeln
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
   * Välj **Konfigurera** från komponentverktygsfältet och ange vilket fragment som ska användas, bekräfta med **Klar**.

   >[!NOTE]
   >
   >Redigera i komponentverktygsfältet fungerar som ett kortkommando för att öppna fragmentet i fragmentredigeraren.

Till exempel: `http://<host>:<port>/editor.html/content/wknd/language-masters/en/about-us.html`

![Upplevelsefragment i sidredigeraren](/help/sites-cloud/authoring/assets/xf-08.png)

## Byggblock {#building-blocks}

Du kan välja en eller flera komponenter för att skapa en byggsten för återvinning i fragmentet:

### Skapa ett byggblock {#creating-a-building-block}

Så här skapar du ett nytt byggblock:

1. Välj de komponenter som du vill återanvända i Experience Fragment-redigeraren:

   ![Välj komponent för byggblock](/help/sites-cloud/authoring/assets/xf-09.png)

1. Välj **Konvertera till byggblock**:

   ![Knappen Byggblock](/help/sites-cloud/authoring/assets/xf-10.png)

1. Ange namnet på **byggblocket** och bekräfta med **Konvertera**:

   ![Namnbyggblock](/help/sites-cloud/authoring/assets/xf-11.png)

1. **Byggblocket** visas på den vänstra fliken (**Lokal**) och kan väljas för ytterligare åtgärder:

   ![Byggblock i rälen](/help/sites-cloud/authoring/assets/xf-12.png)

#### Hantera ett byggblock {#managing-a-building-block}

Byggblocket visas i **Byggblock** -fliken. Följande åtgärder är tillgängliga för varje block:

* **Gå till master**: öppna mastervarianten på en ny flik
* **Byt namn på**
* **Ta bort**

![Hantera byggblock](/help/sites-cloud/authoring/assets/xf-13.png)

#### Använda ett byggblock {#using-a-building-block}

Du kan dra byggblocket till styckesystemet för vilket fragment som helst, precis som med vilken komponent som helst.

När du redigerar ett Experience Fragment visas tillgängliga byggblock på fliken till vänster. Du kan filtrera enligt:

* **Lokal** - Byggblock från det aktuella Experience Fragment
* **Alla** - Byggblock från alla fragment

![Markera byggblock](/help/sites-cloud/authoring/assets/xf-14.png)

## Information om ert Experience Fragment {#details-of-your-experience-fragment}

Information om ditt fragment kan ses:

1. Navigera till platsen för dina Experience Fragments (navigera inte längre till variationerna i fragmentet).
Detaljer visas i alla vyer av konsolen **Upplevelsefragment** och **listvyn** visar även information om export till Target: <!--Details are shown in all views of the **Experience Fragments** console, with the **List View** including details of an [export to Target](/help/sites-administering/experience-fragments-target.md):-->

   ![Information om Experience Fragment](/help/sites-cloud/authoring/assets/xf-15.png)

1. När du öppnar **Egenskaper** av Experience Fragment:

   ![Egenskapsknapp](/help/sites-cloud/authoring/assets/xf-16.png)

   Egenskaperna är tillgängliga på olika flikar:

   >[!CAUTION]
   >
   >De här flikarna visas när du öppnar **Egenskaper** från Experience Fragments-konsolen.
   >
   >Om du **öppnar egenskaperna** när du redigerar ett upplevelsefragment visas rätt [Sidegenskaper](/help/sites-cloud/authoring/fundamentals/page-properties.md).

   ![Experience Fragment-egenskaper](/help/sites-cloud/authoring/assets/xf-17.png)

   * **Grundläggande**
      * **Titel** - obligatoriskt
      * **Beskrivning**
      * **Taggar**
      * **Totalt antal varianter** - endast information
      * **Antal webbvarianter** - endast information
      * **Antal icke-webbvarianter** - endast information
      * **Antal sidor som använder det här fragmentet** - endast information
   * **Cloud Services**
      * **Molnkonfiguration**
      * **Cloud Service Configurations**
      * **Facebook page ID**
      * **Pinterest board**
   * **Referenser**
      * En lista med referenser
   * **Status för sociala medier**
      * Information om variationer i sociala medier

## The Plain HTML Rendition {#the-plain-html-rendition}

Använda `.plain.` -väljaren i URL-adressen kan du komma åt den vanliga HTML-återgivningen från webbläsaren.

>[!NOTE]
>
>Även om detta är tillgängligt direkt från webbläsaren, [det främsta syftet är att tillåta andra program (till exempel webbprogram från tredje part, anpassade mobilimplementeringar) att få tillgång till innehållet i Experience Fragment direkt, med endast URL:en](/help/implementing/developing/extending/experience-fragments.md#the-plain-html-rendition).

## Exportera Experience Fragments {#exporting-experience-fragments}

Som standard levereras Experience Fragments i HTML-format. Detta kan användas av både AEM och tredjepartskanaler.

Om du vill exportera till Adobe Target går du till:

* [Integrera med Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [Exportera Experience Fragments till Adobe Target](/help/sites-cloud/integrating/experience-fragments-target.md)

<!-- * JSON can also be used, see [Target Integration with Experience Fragments](/help/sites-cloud/authoring/fundamentals/experience-fragments-target.md)
-->
