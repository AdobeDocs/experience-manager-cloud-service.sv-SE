---
title: Upplevelsefragment
description: Använd Experience Fragments i Adobe Experience Manager as a Cloud Service för att göra upplevelserna återanvändbara och flexibla.
exl-id: 9dc33677-141f-47e5-a01e-6c7488686314
solution: Experience Manager Sites
feature: Authoring, Experience Fragments
role: User
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '2099'
ht-degree: 2%

---

# Upplevelsefragment {#experience-fragments}

Inom Adobe Experience Manager as a Cloud Service, en Experience Fragment:

* är en grupp med en eller flera komponenter
* innehåller både innehåll och layout
* kan refereras inom sidor
* kan innehålla alla komponenter

An Experience Fragment:

* Är en del av en upplevelse (sida).
* Kan användas på flera sidor (som baseras på redigerbara mallar).
* Är baserad på en mall (endast redigerbar) för att definiera struktur och komponenter.
* Den här mallen används för att skapa *rotsidan* i Experience Fragment.
* Består av en eller flera komponenter med layout i ett styckesystem.
* Kan innehålla andra upplevelsefragment.
* Kan kombineras med andra komponenter (inklusive andra Experience Fragments) för att skapa en komplett sida (upplevelse).
* En eller flera varianter kan skapas baserat på rotsidan.
* Dessa variationer kan dela innehåll och/eller komponenter.
* Kan delas upp i byggstenar som kan användas i flera varianter av fragmentet.

Du kan använda Experience Fragments:

* Om en författare vill återanvända delar (ett fragment av en upplevelse) av en sida.
Utan Experience Fragments måste författaren kopiera och klistra in det fragmentet. Att skapa och underhålla dessa klipp-och-klistra-upplevelser är tidskrävande och leder ofta till användarfel.
Upplevelsefragment eliminerar behovet av att kopiera/klistra in.
* För att stödja headless CMS-fall.
Författare vill bara använda AEM för att skapa, men inte för att leverera till kunden. Ett system/kontaktyta från tredje part skulle förbruka upplevelsen och sedan leverera till användaren.
* Med [Multi Site Management (MSM)](/help/sites-cloud/administering/msm/overview.md); som en Experience Fragment är en del av en sida. Detta gäller både de enskilda fragmenten och de mappar de finns i.

>[!NOTE]
>
>**[Innehållsfragment](/help/sites-cloud/authoring/fragments/content-fragments.md)** och **Upplevelsefragment** är olika funktioner i AEM:
>* **Innehållsfragment** är redaktionellt innehåll, med definition och struktur, men utan ytterligare visuell design och/eller layout. De kan användas för att få tillgång till strukturerade data, bland annat texter, siffror och datum.
>* **Upplevelsefragment** är helt utformat för innehåll, ett fragment av en webbsida.
>
>Upplevelsefragment kan innehålla innehåll i form av innehållsfragment, men inte tvärtom.
>
>Mer information finns i [Om innehållsfragment och upplevelsefragment i AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments).

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
   * Upplevelser som är bra att gruppera, till exempel en kampanj med olika upplevelser i olika kanaler.
* När du använder Omnichannel Commerce.
   * Göra kontaktytor transaktionella.

## Organisera dina upplevelsefragment {#organizing-your-experience-fragments}

Det rekommenderas att
* använda mappar för att ordna dina upplevelsefragment,

* [konfigurera tillåtna mallar för dessa mappar](#configure-allowed-templates-folder).

Genom att skapa mappar kan du:

* skapa en meningsfull struktur för era Experience Fragments, till exempel enligt klassificering

  >[!NOTE]
  >
  >Det är inte nödvändigt att anpassa strukturen för dina Experience Fragments till sidstrukturen på din plats.

* [allokera tillåtna mallar på mappnivå](#configure-allowed-templates-folder)

  >[!NOTE]
  >
  >Du kan använda [mallredigeraren](/help/sites-cloud/authoring/sites-console/templates.md) för att skapa en egen mall.

WKND-projektet strukturerar vissa Experience Fragments enligt `Contributors`. Den struktur som används visar också hur andra funktioner, som Multi Site Management (inklusive språkkopior), kan användas.

Se:

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

![Mappar för Experience Fragments](/help/sites-cloud/authoring/assets/xf-folders.png)

## Skapa och konfigurera en mapp för dina Experience Fragments {#creating-and-configuring-a-folder-for-your-experience-fragments}

Om du vill skapa och konfigurera en mapp för dina Experience Fragments bör du:

1. [Skapa en mapp](/help/sites-cloud/authoring/sites-console/managing-pages.md#creating-a-new-folder).

1. [Konfigurera tillåtna Experience Fragment-mallar för den mappen](#configure-allowed-templates-folder).

>[!NOTE]
>
>Det går också att konfigurera [tillåtna mallar för din instans](#configure-allowed-templates-instance), men den här metoden rekommenderas **inte** eftersom värdena kan skrivas över vid uppgradering.

### Konfigurera tillåtna mallar för mappen {#configure-allowed-templates-folder}

>[!NOTE]
>
>Det här är den rekommenderade metoden för att ange **tillåtna mallar** eftersom värdena inte skrivs över vid uppgradering.

1. Navigera till den obligatoriska mappen **Experience Fragments**.

1. Markera mappen och sedan **Egenskaper**.

1. Ange det reguljära uttrycket för hämtning av de nödvändiga mallarna i fältet **Tillåtna mallar**.

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

1. Navigera till den nödvändiga konsolen **Experience Fragments**.

1. Välj **Konfigurationsalternativ**:

   ![Konfigurationsknappen](/help/sites-cloud/authoring/assets/xf-18.png)

1. Ange de mallar som krävs i dialogrutan **Konfigurera Experience Fragments**:

   ![Konfigurera Experience Fragments](/help/sites-cloud/authoring/assets/xf-19.png)

   >[!NOTE]
   >
   >Mer information finns i [Mallar för Experience Fragments](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments).

1. Välj **Spara**.

## Skapa ett upplevelsefragment {#creating-an-experience-fragment}

Så här skapar du ett Experience Fragment:

1. Välj **Upplevelsefragment** i Global Navigation.

   ![Upplev fragment på navigeringspanelen](/help/sites-cloud/authoring/assets/xf-01.png)

1. Navigera till önskad mapp och välj **Skapa**:

   ![Skapa en mapp för Experience Fragments](/help/sites-cloud/authoring/assets/xf-02.png)

1. Välj **Experience Fragment** för att öppna guiden **Skapa Experience Fragment**.

   Välj önskad **mall** och sedan **Nästa**:

   ![Välja en upplevelsefragmentmall](/help/sites-cloud/authoring/assets/xf-03.png)


1. Ange **egenskaperna** för **upplevelsefragmentet**.

   En **titel** är obligatorisk. Om **Name** lämnas tomt hämtas det från **Title**.

   ![Upplev fragmentegenskaper](/help/sites-cloud/authoring/assets/xf-04.png)

   >[!NOTE]
   >
   >Taggar från Experience Fragment-mallen kommer inte att sammanfogas med taggar på den här Experience Fragment-rotsidan.
   >
   >De här är helt separata.

1. Klicka på **Skapa**.

   Ett meddelande visas. Välj:

   * **Klar** för att återgå till konsolen
   * **Öppna** om du vill öppna fragmentredigeraren

## Redigera din upplevelsefragment {#editing-your-experience-fragment}

Experience Fragment Editor har funktioner som liknar den vanliga sidredigeraren.

>[!NOTE]
>
>Mer information om hur du använder sidredigeraren finns i [Redigera sidinnehåll](/help/sites-cloud/authoring/page-editor/edit-content.md).

Följande exempelprocedur visar hur du skapar ett teaser för en produkt:

1. Dra och släpp den nödvändiga komponenten från [komponentwebbläsaren](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser).

1. Beroende på komponenten:
   * Lägg till innehåll och/eller resurser efter behov.
   * Konfigurera egenskaperna efter behov.

1. Lägg till fler komponenter efter behov.

Till exempel: `http://<host>:<port>/editor.html/content/experience-fragments/wknd/language-masters/en/contributors/stacey-roswells/master.html`

![Upplevelsefragment på sida](/help/sites-cloud/authoring/assets/xf-05.png)

## Skapa en upplevelsefragmentvariant {#creating-an-experience-fragment-variation}

Ni kan skapa olika upplevelsefragment beroende på era behov:

1. Öppna ditt fragment för [redigering](#editing-your-experience-fragment).
1. Öppna fliken **Variationer**.

   ![Skapa en Experience Fragment-variation](/help/sites-cloud/authoring/assets/xf-06.png)

1. Med **Skapa** kan du skapa:

   * **Variant**
   * **Variation som live-copy**.

     >[!NOTE]
     >
     >Om du skapar en ursprunglig variant som Live-kopia ärvs titeln med Live Copy Source som huvudvariant.

1. Definiera de nödvändiga egenskaperna:

   * **Mall**
   * **Titel**
   * **Namn** - om det lämnas tomt hämtas det från titeln
   * **Beskrivning**
   * **Variationstaggar**

   Till exempel:

   ![Variationsegenskaper](/help/sites-cloud/authoring/assets/xf-07.png)


1. Bekräfta med **Klar**. Den nya varianten visas på panelen.

## Använda ditt Experience Fragment {#using-your-experience-fragment}

Nu kan du använda din Experience Fragment när du redigerar dina sidor:

1. Öppna en sida för redigering.

   >[!NOTE]
   >
   >Sidan måste baseras på en redigerbar mall.

1. Skapa en instans av Experience Fragment-komponenten i sidstyckesystemet:

1. Lägg till den faktiska Experience Fragment-instansen i komponentinstansen, antingen:

   * Dra det önskade fragmentet från Assets Browser och släpp det på komponenten.
   * Välj **Konfigurera** i komponentverktygsfältet och ange vilket fragment som ska användas. Bekräfta med **Klar**.

   >[!NOTE]
   >
   >Redigera i komponentverktygsfältet fungerar som ett kortkommando för att öppna fragmentet i fragmentredigeraren.

Till exempel: `http://<host>:<port>/editor.html/content/wknd/language-masters/en/about-us.html`

![Upplev fragment i sidredigeraren](/help/sites-cloud/authoring/assets/xf-08.png)

## Byggblock {#building-blocks}

Du kan välja en eller flera komponenter för att skapa en byggsten för återvinning i fragmentet:

### Skapa ett byggblock {#creating-a-building-block}

Så här skapar du ett byggblock:

1. Välj de komponenter som du vill återanvända i Experience Fragment-redigeraren:

   ![Välj komponent för byggblock](/help/sites-cloud/authoring/assets/xf-09.png)

1. Välj **Konvertera till byggblock** i komponentverktygsfältet:

   ![Knappen Byggblock](/help/sites-cloud/authoring/assets/xf-10.png)

1. Ange namnet på **byggblocket** och bekräfta med **Konvertera**:

   ![Namnbyggningsblock](/help/sites-cloud/authoring/assets/xf-11.png)

1. **Byggblocket** visas på den vänstra fliken (**Lokal**) och kan väljas för ytterligare åtgärder:

   ![Byggblock i rälen](/help/sites-cloud/authoring/assets/xf-12.png)

#### Hantera ett byggblock {#managing-a-building-block}

Byggblocket visas på fliken **Byggblock**. Följande åtgärder är tillgängliga för varje block:

* **Gå till mallsida**: öppna varianten av rotsidan på en ny flik
* **Byt namn**
* **Ta bort**

![Hantera byggblock](/help/sites-cloud/authoring/assets/xf-13.png)

#### Använda ett byggblock {#using-a-building-block}

Du kan dra byggblocket till styckesystemet för vilket fragment som helst, precis som med andra komponenter.

När du redigerar ett Experience Fragment visas tillgängliga byggblock på fliken till vänster. Du kan filtrera enligt:

* **Lokal** - Bygger block från det aktuella Experience Fragment
* **Alla** - Bygger block från alla fragment

![Markerar byggblock](/help/sites-cloud/authoring/assets/xf-14.png)

## Personalization på ert Experience Fragment {#personalization-experience-fragment}

Med Personalization på er Experience Fragment kan ni som marknadsförare definiera målgrupper för Experience Fragment en enda gång och sedan återanvända fragmentet på vilken sida som helst. Det:

* eliminerar behovet av att ange önskade variationer för varje målgrupp varje gång fragmentet används
* behåller sin formatering i alla erbjudanden

Du kan skapa ett Experience Fragment med flera komponenter grupperade inuti det här enskilda fragmentet. Ni kan också skapa variationer av fragmentet för varje specifikt målgruppssegment och sedan återanvända dessa Experience Fragments i alla kanaler som behövs.

Personalization uppnås genom att definiera **Personalization** -egenskaperna på Experience Fragment eller variation, eller i den mapp som innehåller fragmenten. Detta innebär att arv kan åsidosätta personaliseringsegenskaper.

När du konfigurerar de här egenskaperna aktiveras även **målläget** i Experience Fragment-redigeraren.

### Definiera Personalization för ert Experience Fragment {#defining-personalization-experience-fragment}

Så här anpassar du fragment:

1. Navigera till önskad plats i konsolen **Experience Fragments**.

1. Välj en mapp eller ditt fragment och **Egenskaper** i verktygsfältet.

   >[!NOTE]
   >
   >Personalization-egenskaper som definieras i en mapp ärvs av alla underordnade mappar nedåt genom underträdet och Experience Fragments (och varianter) i underträdet. De kan åsidosättas genom att arvet bryts.

1. Öppna fliken **Personalization** för att definiera och spara dina inställningar. I en mapp:

   ![Experience Fragment - personaliseringsegenskaper](/help/sites-cloud/authoring/assets/xf-personalization-properties.png)

   >[!CAUTION]
   >
   >När ett fragment är inbäddat på en Sites-sida och **Personalization** har konfigurerats, används endast sidans personaliseringsversion vid sidåtergivning.
   >
   >För att målanpassning som utförs på komponenterna i ett fragment ska fungera vid sidåtergivning måste följande villkor vara uppfyllda:
   >
   >**ContextHub-sökvägen** som har valts på fliken **Personalization** måste vara antingen:
   >
   >* samma sökväg som den som konfigurerats för sidan där fragmentet återges
   >
   >  Eller:
   >
   >* en sökväg som innehåller en delmängd av de butiker som definieras i ContextHub som konfigurerats för sidan
   >
   >**Segmentsökvägen** som har valts på fliken **Personalization** måste vara antingen:
   >
   >* samma sökväg som den som konfigurerats för sidan där fragmentet återges
   >
   >  eller
   >
   >* en sökväg som innehåller en delmängd av segmenten som konfigurerats för sidan

### Definiera målanpassning för ert upplevelsefragment {#defining-targeting-experience-fragment}

När personaliseringsegenskaperna har konfigurerats är målläget tillgängligt när fragmentet öppnas för redigering.

![Experience Fragment Editor - målläge](/help/sites-cloud/authoring/assets/xf-targeting-mode.png)

Det här läget fungerar på samma sätt som för sidredigering. Mer information finns i [Riktningsläge för sidredigeraren](/help/sites-cloud/authoring/personalization/targeted-content.md).

## Information om ert Experience Fragment {#details-of-your-experience-fragment}

Information om ditt fragment kan ses:

1. Navigera till platsen för dina Experience Fragments (navigera inte längre till variationerna i fragmentet).
Information visas i alla vyer av konsolen **Experience Fragments** med **listvyn** inklusive information om en [export till mål](/help/sites-cloud/integrating/integrating-adobe-target.md):

   ![Information om Experience Fragment](/help/sites-cloud/authoring/assets/xf-15.png)

1. När du öppnar **Egenskaper** i Experience Fragment:

   ![Knappen Egenskaper](/help/sites-cloud/authoring/assets/xf-16.png)

   Egenskaperna är tillgängliga på olika flikar:

   >[!CAUTION]
   >
   >De här flikarna visas när du öppnar **Egenskaper** från Experience Fragments-konsolen.
   >
   >Om du **öppnar egenskaperna** när du redigerar ett upplevelsefragment visas rätt [Sidegenskaper](/help/sites-cloud/authoring/sites-console/page-properties.md).

   ![Upplev fragmentegenskaper](/help/sites-cloud/authoring/assets/xf-17.png)

   * **Grundläggande**
      * **Titel** - obligatoriskt
      * **Beskrivning**
      * **Taggar**
      * **Totalt antal varianter** - endast information
      * **Antal webbvarianter** - endast information
      * **Antal icke-webbvarianter** - endast information
      * **Antal sidor som använder det här fragmentet** - endast information
   * **Cloud Service**
      * **Molnkonfiguration**
      * **Konfigurationer av Cloud Service**
      * **Facebook sid-ID**
      * **Pinterest board**
   * **Referenser**
      * En lista med referenser
   * **Personalization**
      * **ContextHub-sökväg**
      * **Segmentsökväg**
      * **Varumärke**

## The Plain HTML Rendition {#the-plain-html-rendition}

Med väljaren `.plain.` i URL:en kan du få åtkomst till den rena HTML-återgivningen via webbläsaren.

>[!NOTE]
>
>Även om detta är direkt tillgängligt från webbläsaren är det främsta syftet med [att tillåta andra program (till exempel webbprogram från tredje part, anpassade mobilimplementeringar) att komma åt innehållet i Experience Fragment direkt, med enbart URL:en ](/help/implementing/developing/extending/experience-fragments.md#the-plain-html-rendition).

## Publicera upplevelsefragment {#publishing-experience-fragments}

Att publicera din Experience Fragment är i princip detsamma som att [publicera en sida](/help/sites-cloud/authoring/sites-console/publishing-pages.md) (även om det kommer från Experience Fragments-konsolen eller redigeraren).

Du kan även [publicera till Preview](/help/sites-cloud/authoring/sites-console/previewing-content.md) (igen från Experience Fragments-konsolen eller redigeraren).

## Exportera Experience Fragments {#exporting-experience-fragments}

Som standard levereras Experience Fragments i HTML-format. Detta kan användas av både AEM och tredjepartskanaler.

JSON kan även användas för export till Adobe Target. Se:

* [Integrera med Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [Exportera Experience Fragments till Adobe Target](/help/sites-cloud/integrating/experience-fragments-target.md)
