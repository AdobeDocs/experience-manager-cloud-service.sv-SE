---
title: Content Fragment Models (Assets - Content Fragments)
description: Läs om hur Content Fragment Models fungerar som grund för ditt headless-innehåll i AEM, så att du kan skapa Content Fragments med strukturerat innehåll.
exl-id: fd706c74-4cc1-426d-ab56-d1d1b521154b
feature: Content Fragments, GraphQL API
role: User, Admin, Developer
solution: Experience Manager Sites
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '3588'
ht-degree: 1%

---

# Modeller för innehållsfragment {#content-fragment-models}

Content Fragment Models i AEM definierar innehållsstrukturen för dina [innehållsfragment](/help/assets/content-fragments/content-fragments.md), vilket utgör grunden för ditt headless-innehåll.

Så här använder du modeller för innehållsfragment:

1. [Aktivera funktionen Content Fragment Model för instansen](/help/assets/content-fragments/content-fragments-configuration-browser.md)
1. [Skapa](#creating-a-content-fragment-model) och [konfigurera](#defining-your-content-fragment-model), dina modeller för innehållsfragment
1. [Aktivera dina modeller för innehållsfragment](#enabling-disabling-a-content-fragment-model) för användning när du skapar innehållsfragment
1. [Tillåt dina modeller för innehållsfragment i de nödvändiga Assets-mapparna](#allowing-content-fragment-models-assets-folder) genom att konfigurera **Profiler**.

>[!NOTE]
>
>Innehållsfragment är en webbplatsfunktion, men lagras som **Assets**.
>
>Innehållsfragment och modeller för innehållsfragment hanteras nu primärt med konsolen **[Innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console)** , även om innehållsfragment fortfarande kan hanteras från konsolen **Assets** och modeller för innehållsfragment från konsolen **Verktyg** . I det här avsnittet beskrivs hantering från konsolerna **Assets** och **Verktyg** .

>[!NOTE]
>
>Om en modell skapades med den [nya modellredigeraren](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) bör du alltid använda den redigeraren för modellen.
>
>Om du sedan öppnar modellen med den här (ursprungliga) modellredigeraren visas meddelandet:
>
>* &quot;Den här modellen har ett anpassat gränssnittsschema konfigurerat. Fältordningen som visas i det här användargränssnittet kanske inte matchar användargränssnittets schema. Om du vill visa de fält som är justerade mot gränssnittets schema måste du växla till den nya redigeraren för innehållsfragment.&quot;

## Skapa en innehållsfragmentmodell {#creating-a-content-fragment-model}

1. Navigera till **Verktyg**, **Allmänt** och öppna sedan **Modeller för innehållsfragment**.
1. Navigera till den mapp som passar din [konfiguration eller underkonfiguration](/help/assets/content-fragments/content-fragments-configuration-browser.md).
1. Använd **Skapa** för att öppna guiden.

   >[!CAUTION]
   >
   >Om [användningen av innehållsfragmentmodeller inte har aktiverats](/help/assets/content-fragments/content-fragments-configuration-browser.md) är alternativet **Skapa** inte tillgängligt.

1. Ange **modelltitel**.
Du kan också definiera olika egenskaper. Du kan till exempel lägga till **taggar**, en **beskrivning** och välja **Aktivera modell** för att [aktivera modellen](#enabling-disabling-a-content-fragment-model) om det behövs.

   >[!NOTE]
   >
   >Mer information om **URL-mönstret för standardförhandsgranskning** finns i [Modell för innehållsfragment - egenskaper](#content-fragment-model-properties).

   ![titel och beskrivning](assets/cfm-models-02.png)

1. Använd **Skapa** för att spara den tomma modellen. Ett meddelande visar att åtgärden lyckades. Du kan välja **Öppna** om du vill redigera modellen omedelbart eller **Klar** om du vill återgå till konsolen.

## Definiera innehållsfragmentmodellen {#defining-your-content-fragment-model}

Modellen för innehållsfragment definierar effektivt strukturen för de resulterande innehållsfragmenten med en markering av **[datatyper](#data-types)**. Med modellredigeraren kan du lägga till instanser av datatyperna och sedan konfigurera dem för att skapa de obligatoriska fälten:

>[!CAUTION]
>
>Om du redigerar en befintlig innehållsfragmentmodell kan det påverka beroende fragment.

1. Navigera till **Verktyg**, **Allmänt** och öppna sedan **Modeller för innehållsfragment**.

1. Navigera till mappen som innehåller innehållsfragmentmodellen.
1. Öppna den modell som krävs för **Redigera**. Använd snabbåtgärden eller markera modellen och sedan åtgärden från verktygsfältet.

   När du har öppnat modellredigeraren visas följande:

   * vänster: fält har redan definierats
   * höger: **Datatyper** som är tillgängliga för att skapa fält (och **egenskaper** som kan användas när fälten har skapats)
   * top: ett alternativ för att prova den [nya redigeraren](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)

   >[!NOTE]
   >
   >När ett fält är **Obligatoriskt** markeras **Label** som anges i den vänstra rutan med ett asterix (**&#42;**).

![egenskaper](assets/cfm-models-03.png)

1. **Lägga till ett fält**

   * Dra en obligatorisk datatyp till önskad plats för ett fält:

     ![datatyp till fält](assets/cfm-models-04.png)

   * När ett fält har lagts till i modellen visar den högra panelen **Egenskaper** som kan definieras för den aktuella datatypen. Här definierar du vad som krävs för fältet.

      * Många egenskaper är självförklarande. Mer information finns i [Egenskaper](#properties).
      * Om du skriver en **fältetikett** slutförs **egenskapsnamnet** automatiskt, om det är tomt, och den kan uppdateras manuellt senare.

        >[!CAUTION]
        >
        >När du uppdaterar egenskapen **Egenskapsnamn** manuellt för en datatyp måste du tänka på att namn bara får innehålla A-Z, a-z, 0-9 och understreck&quot;_&quot; som specialtecken.
        >
        >Om modeller som skapats i tidigare versioner av AEM innehåller ogiltiga tecken tar du bort eller uppdaterar dessa tecken.

     Till exempel:

     ![fältegenskaper](assets/cfm-models-05.png)

1. **Ta bort ett fält**

   Markera det obligatoriska fältet och välj sedan papperskorgsikonen. Du ombeds bekräfta åtgärden.

   ![ta bort](assets/cfm-models-06.png)

1. Lägg till alla obligatoriska fält och definiera de relaterade egenskaperna efter behov. Till exempel:

   ![spara](assets/cfm-models-07.png)

1. Välj **Spara** om du vill behålla definitionen.

## Datatyper {#data-types}

Det finns ett urval datatyper som du kan använda för att definiera din modell:

* **Enkelradig text**
   * Lägg till ett fält för en enda textrad. Den maximala längden kan definieras
   * Fältet kan konfigureras så att fragmentförfattare kan skapa nya instanser av fältet

* **Flerradstext**
   * Ett textområde som kan vara RTF, Oformaterad text eller Markering
   * Fältet kan konfigureras så att fragmentförfattare kan skapa nya instanser av fältet

  >[!NOTE]
  >
  >Oavsett om textområdet är RTF, Oformaterad text eller Markering definieras i modellen av egenskapen **Standardtyp**.
  >
  >Det här formatet kan inte ändras från [redigeraren för innehållsfragment](/help/sites-cloud/administering/content-fragments/authoring.md), utan bara från modellen.

* **Number**
   * Lägga till ett numeriskt fält
   * Fältet kan konfigureras så att fragmentförfattare kan skapa nya instanser av fältet

* **Boolean**
   * Lägg till en boolesk kryssruta

* **Datum och tid**
   * Lägg till ett datum- och/eller tidsfält

* **Uppräkning**
   * Lägga till en uppsättning kryssrutefält, alternativknappar eller listrutor
      * Du kan ange vilka alternativ som är tillgängliga för fragmentförfattaren

* **Taggar**
   * Tillåter fragmentförfattare att komma åt och markera taggområden

* **Fragmentreferens**
   * Refererar till andra innehållsfragment; kan användas för att [skapa kapslat innehåll](#using-references-to-form-nested-content)
   * Datatypen kan konfigureras så att fragmentförfattare kan:
      * Redigera det refererade fragmentet direkt.
      * Skapa ett nytt innehållsfragment baserat på lämplig modell
      * Skapa nya instanser av fältet
   * Referensen anger sökvägen till den refererade resursen, till exempel `/content/dam/path/to/resource`

* **Fragmentreferens (UUID)**
   * Refererar till andra innehållsfragment; kan användas för att [skapa kapslat innehåll](#using-references-to-form-nested-content)
   * Datatypen kan konfigureras så att fragmentförfattare kan:
      * Redigera det refererade fragmentet direkt.
      * Skapa ett nytt innehållsfragment baserat på lämplig modell
      * Skapa nya instanser av fältet
   * I redigeraren anger referensen sökvägen till den refererade resursen. Referensen behålls internt som ett UUID (Universal Unique ID) som refererar till resursen
      * Du behöver inte känna till UUID. I fragmentredigeraren kan du bläddra till det nödvändiga fragmentet

  >[!NOTE]
  >
  >UUID:n är databasspecifika. Om du använder [innehållskopieringsverktyget](/help/implementing/developing/tools/content-copy.md) för att kopiera innehållsfragment beräknas UUID:n om i målmiljön.

* **Innehållsreferens**
   * Refererar till annat innehåll, oavsett typ; kan användas för att [skapa kapslat innehåll](#using-references-to-form-nested-content)
   * Om en bild refereras kan du välja att visa en miniatyrbild
   * Fältet kan konfigureras så att fragmentförfattare kan skapa nya instanser av fältet
   * Referensen anger sökvägen till den refererade resursen, till exempel `/content/dam/path/to/resource`

* **Innehållsreferens (UUID)**
   * Refererar till annat innehåll, oavsett typ; kan användas för att [skapa kapslat innehåll](#using-references-to-form-nested-content)
   * Om en bild refereras kan du välja att visa en miniatyrbild
   * Fältet kan konfigureras så att fragmentförfattare kan skapa nya instanser av fältet
   * I redigeraren anger referensen sökvägen till den refererade resursen. Referensen behålls internt som ett UUID (Universal Unique ID) som refererar till resursen
      * Du behöver inte känna till UUID. I fragmentredigeraren kan du bläddra till den resurs som krävs

  >[!NOTE]
  >
  >UUID:n är databasspecifika. Om du använder [innehållskopieringsverktyget](/help/implementing/developing/tools/content-copy.md) för att kopiera innehållsfragment beräknas UUID:n om i målmiljön.

* **JSON-objekt**
   * Gör att innehållsfragmentets författare kan ange JSON-syntax i motsvarande element i ett fragment.
      * Om du vill att AEM ska kunna lagra direkt JSON som du har kopierat/klistrat in från en annan tjänst.
      * JSON skickas och skrivs ut som JSON i GraphQL.
      * Innehåller JSON-syntaxmarkering, automatisk komplettering och felmarkering i Content Fragment Editor.

* **Platshållare för flik**
   * Tillåter att flikar kan användas när innehållet i innehållsfragmentet redigeras.
      * Dessa visas som avgränsare i modellredigeraren, och delar upp avsnitt i listan med innehållsdatatyper. Varje instans representerar början på en ny flik.
      * I fragmentredigeraren visas varje instans som en flik.

     >[!NOTE]
     >
     >Den här datatypen används endast för formatering, den ignoreras av AEM GraphQL-schemat.

## Egenskaper {#properties}

Många egenskaper är självförklarande, för vissa egenskaper finns ytterligare information nedan:

* **Egenskapsnamn**

  När du uppdaterar den här egenskapen manuellt för en datatyp bör du tänka på att namn **måste** innehålla *endast* A-Z, a-z, 0-9 och understreck&quot;_&quot; som specialtecken.

  >[!CAUTION]
  >
  >Om modeller som skapats i tidigare versioner av AEM innehåller ogiltiga tecken tar du bort eller uppdaterar dessa tecken.

* **Återge som**
De olika alternativen för att realisera/återge fältet i ett fragment. Med den här egenskapen kan du ofta definiera om författaren ska se en enda instans av fältet eller om han eller hon ska kunna skapa flera instanser. När **Flera fält** används kan du definiera minsta och högsta antal objekt - se [Validering](#validation) för mer information.

* **Fältetikett**
Om du anger en **fältetikett** genereras ett **egenskapsnamn** automatiskt, som sedan kan uppdateras manuellt om det behövs.

* **Validering**
Grundläggande validering är tillgängligt av mekanismer som egenskapen **Required** . Vissa datatyper har ytterligare valideringsfält. Mer information finns i [Validering](#validation).

* För datatypen **Flerradig text** går det att definiera **standardtypen** som endera:

   * **RTF**
   * **Markdown**
   * **Oformaterad text**

  Om inget anges används standardvärdet **RTF** för det här fältet.

  Om du ändrar **standardtypen** i en innehållsfragmentmodell börjar detta bara gälla för ett befintligt, relaterat innehållsfragment efter att fragmentet har öppnats i redigeraren och sparats.

* **Unik**
Innehållet (för det specifika fältet) måste vara unikt för alla innehållsfragment som skapas från den aktuella modellen.

  Detta används för att säkerställa att innehållsförfattare inte kan upprepa innehåll som redan har lagts till i ett annat fragment av samma modell.

  Ett **enkelradigt textfält** med namnet `Country` i innehållsfragmentmodellen kan till exempel inte ha värdet `Japan` i två beroende innehållsfragment. En varning skickas när ett försök görs att utföra den andra instansen.

  >[!NOTE]
  >
  >Unikitet säkerställs per språkrot.

  >[!NOTE]
  >
  >Variationer kan ha samma *unika*-värde som varianter av samma fragment, men inte samma värde som används i andra variationer av fragment.

  >[!CAUTION]
  >
  >Om du vill använda MSM (som skapar kopior av innehållsfragment) ska eventuella **unika**-begränsningar tas bort från alla datatyper som används i respektive modell för innehållsfragment.

* Mer information om den specifika datatypen och dess egenskaper finns i **[Innehållsreferens](#content-reference)**.

* Mer information om den specifika datatypen och dess egenskaper finns i **[Fragmentreferens (kapslade fragment)](#fragment-reference-nested-fragments)**.

* **Översättningsbar**

  Om du markerar kryssrutan **Översättningsbar** för ett fält i redigeraren för innehållsfragmentmodellen kommer följande att göras:

   * Kontrollera att fältets egenskapsnamn har lagts till i översättningskonfigurationen, kontext `/content/dam/<sites-configuration>`, om det inte redan finns.
   * För GraphQL: ställ in egenskapen `<translatable>` i fältet Innehållsfragment på `yes` för att tillåta GraphQL-frågefilter för JSON-utdata med endast översättningsbart innehåll.

## Validering {#validation}

Olika datatyper kan nu definiera valideringskrav för när innehåll anges i det resulterande fragmentet:

* **Enkelradig text**
   * Jämför med ett fördefinierat regex.
* **Number**
   * Sök efter specifika värden.
* **Innehållsreferens**
   * Testa om det finns specifika typer av innehåll.
   * Det går endast att referera till resurser med en angiven filstorlek eller mindre.
   * Det går endast att referera till bilder inom ett fördefinierat intervall med bredd och/eller höjd (i pixlar).
* **Fragmentreferens**
   * Testa om det finns en specifik innehållsfragmentmodell.
* **Minsta antal objekt** / **Max antal objekt**

  Fält som har definierats som ett **flera fält** (anges med **Återge som**) har följande alternativ:

   * **Minsta antal objekt**
   * **Maximalt antal objekt**

  Dessa valideras:

   * Det högsta värdet valideras i den [ursprungliga Content Fragment Editor](/help/assets/content-fragments/content-fragments-variations.md).
   * Båda valideras i [Content Fragment Editor](/help/sites-cloud/administering/content-fragments/authoring.md).

## Använda referenser till kapslat innehåll {#using-references-to-form-nested-content}

Innehållsfragment kan skapa kapslat innehåll med någon av följande datatyper:

* [Innehållsreferens](#content-reference)
   * Ger en enkel referens till annat innehåll, av alla typer.
   * Tillhandahålls av datatyperna:
      * **Innehållsreferens** - sökvägsbaserad
      * **Innehållsreferens (UUID)** - UUID-baserad
   * Kan konfigureras för en eller flera referenser (i det resulterande fragmentet).

* [Fragmentreferens](#fragment-reference-nested-fragments) (kapslade fragment)
   * Refererar till andra fragment, beroende på vilka specifika modeller som anges.
   * Tillhandahålls av datatyperna:
      * **Fragmentreferens** - sökvägsbaserad
      * **Fragmentreferens (UUID)** - UUID-baserad
   * Gör att du kan ta med/hämta strukturerade data.

     >[!NOTE]
     >
     >Den här metoden är särskilt intressant när du använder [Headless Content Delivery med hjälp av Content Fragments med GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).

   * Kan konfigureras för en eller flera referenser (i det resulterande fragmentet).

>[!NOTE]
>
>Se [Uppgradera dina innehållsfragment för UUID-referenser](/help/headless/graphql-api/uuid-reference-upgrade.md) för mer information om Content/Fragment Reference och Content/Fragment Reference (UUID) och uppgradera till UUID-baserade datatyper.

>[!NOTE]
>
>AEM har ett upprepningsskydd för:
>
>* Innehållsreferenser
>  Detta förhindrar att användaren lägger till en referens till det aktuella fragmentet. Detta kan leda till en tom dialogruta för fragmentreferensväljaren.
>
>* Fragmentreferenser i GraphQL
>  Om du skapar en djup fråga som returnerar flera innehållsfragment som refereras av varandra, returneras null vid den första förekomsten.

### Innehållsreferens {#content-reference}

Med datatyperna **Innehållsreferens** och **Innehållsreferens (UUID)** kan du återge innehåll från en annan källa, till exempel bild, sida eller Experience Fragment.

Förutom standardegenskaper kan du ange:

* **Rotsökvägen** för refererat innehåll
* De innehållstyper som kan refereras
* Begränsningar för filstorlekar
* Om en bild refereras:
   * Visa miniatyrbild
   * Bildbegränsningar för höjd och bredd

![Innehållsreferens](assets/cfm-content-reference.png)

### Fragmentreferens (kapslade fragment) {#fragment-reference-nested-fragments}

Datatyperna **Fragmentreferens** och **Fragmentreferens (UUID)** kan referera till ett eller flera innehållsfragment. Den här funktionen är av särskilt intresse när du hämtar innehåll som ska användas i din app, eftersom du kan hämta strukturerade data med flera lager.

Till exempel:

* En modell som definierar detaljer för en medarbetare. Dessa omfattar:
   * En referens till modellen som definierar arbetsgivaren (företaget)

```xml
type EmployeeModel {
    name: String
    firstName: String
    company: CompanyModel
}

type CompanyModel {
    name: String
    street: String
    city: String
}
```

>[!NOTE]
>
>Detta är av särskilt intresse i samband med [leverans av Headless Content Delivery med hjälp av Content Fragments med GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).

Förutom standardegenskaper kan du definiera:

* **Återge som**:

   * **multifield** - fragmentförfattaren kan skapa flera, enskilda referenser

   * **fragmentreferens** - tillåter fragmentförfattaren att välja en enskild referens till ett fragment

* **Modelltyp**
Du kan välja flera modeller. När du redigerar innehållsfragmentet måste alla refererade fragment ha skapats med dessa modeller.

* **Rotsökväg**
Detta anger en rotsökväg för alla fragment som refereras.

* **Tillåt att fragment skapas**

  Detta gör att fragmentförfattaren kan skapa ett fragment baserat på lämplig modell.

   * **fragmentreferenssammansatt** - tillåter fragmentförfattaren att skapa en sammansatt bild genom att markera flera fragment

  ![Fragmentreferens](assets/cfm-fragment-reference.png)

>[!NOTE]
>
>Det finns en mekanism för upprepningsskydd. Användaren kan inte välja det aktuella innehållsfragmentet i fragmentreferensen. Detta kan leda till en tom dialogruta för fragmentreferensväljaren.
>
>Det finns också ett upprepningsskydd för fragmentreferenser i GraphQL. Om du skapar en djup fråga i två innehållsfragment som refererar till varandra returneras null.

## Content Fragment Model - egenskaper {#content-fragment-model-properties}

Du kan redigera **egenskaperna** för en innehållsfragmentmodell:

* **Grundläggande**
   * **Modelltitel**
   * **Taggar**
   * **Beskrivning**
   * **Överför bild**
   * **URL-mönster för standardförhandsvisning**

     >[!NOTE]
     >
     >Detta används bara av den *nya* innehållsfragmentsredigeraren. Mer information finns i [Modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#content-fragment-model-properties).


## Aktivera eller inaktivera en innehållsfragmentmodell {#enabling-disabling-a-content-fragment-model}

För fullständig kontroll över användningen av dina modeller för innehållsfragment har de en status som du kan ange.

### Aktivera en innehållsfragmentmodell {#enabling-a-content-fragment-model}

När en modell skapas måste den aktiveras så att den:

* Kan markeras när du skapar ett innehållsfragment.
* Kan refereras inifrån en innehållsfragmentmodell.
* Är tillgängligt för GraphQL, så schemat genereras.

Så här aktiverar du en modell som har flaggats som antingen:

* **Utkast** : mew (aldrig aktiverat).
* **Inaktiverad** : har inaktiverats specifikt.

Du använder alternativet **Aktivera** från antingen:

* Det övre verktygsfältet när den obligatoriska modellen är markerad.
* Motsvarande snabbåtgärd (mouse-over the required Model).

![Aktivera ett utkast eller en inaktiverad modell](assets/cfm-status-enable.png)

### Inaktivera en innehållsfragmentmodell {#disabling-a-content-fragment-model}

En modell kan också inaktiveras så att:

* Modellen är inte längre tillgänglig som grund för att skapa *nya* innehållsfragment.
* Men:
   * GraphQL-schemat fortsätter att genereras och är fortfarande frågningsbart (för att inte påverka JSON-API:t).
   * Alla innehållsfragment som är baserade på modellen kan fortfarande efterfrågas och returneras från GraphQL slutpunkt.
* Det går inte att referera till modellen längre, men befintliga referenser behålls orörda och kan fortfarande läsas och returneras från GraphQL-slutpunkten.

Om du vill inaktivera en modell som är flaggad som **Aktiverad** använder du alternativet **Inaktivera** från antingen:

* Det övre verktygsfältet när den obligatoriska modellen är markerad.
* Motsvarande snabbåtgärd (mouse-over the required Model).

![Inaktivera en aktiverad modell](assets/cfm-status-disable.png)

## Tillåt modeller för innehållsfragment i din Assets-mapp {#allowing-content-fragment-models-assets-folder}

Om du vill implementera innehållsstyrning kan du konfigurera **profiler** i Assets-mappen för att styra vilka innehållsfragmentmodeller som tillåts för att skapa fragment i den mappen.

>[!NOTE]
>
>Mekanismen liknar [tillåter sidmallar](/help/sites-cloud/authoring/page-editor/templates.md#allowing-a-template-author) för en sida och dess underordnade sidor i avancerade egenskaper för en sida.

Så här konfigurerar du **principer** för **Tillåtna modeller för innehållsfragment**:

1. Navigera och öppna **Egenskaper** för den Assets-mapp som krävs.

1. Öppna fliken **Profiler** där du kan konfigurera:

   * **Ärvd från`<folder>`**

     Profiler ärvs automatiskt när nya underordnade mappar skapas. Profilen kan konfigureras om (och arvet brytas) om undermappar måste tillåta modeller som skiljer sig från den överordnade mappen.

   * **Tillåtna modeller för innehållsfragment via sökväg**

     Flera modeller kan tillåtas.

   * **Tillåtna modeller för innehållsfragment efter tagg**

     Flera modeller kan tillåtas.

   ![Modellprincip för innehållsfragment](assets/cfm-model-policy-assets-folder.png)

1. **Spara** eventuella ändringar.

De Content Fragment-modeller som tillåts för en mapp löses enligt följande:

* **Profiler** för **Tillåtna modeller för innehållsfragment**.
* Om den är tom kan du försöka identifiera principen med arvsreglerna.
* Om arvskedjan inte ger något resultat ska du titta på konfigurationen **Cloud Services** för den mappen (även först direkt och sedan via arv).
* Om inget av ovanstående ger några resultat finns det inga tillåtna modeller för den mappen.

## Ta bort en innehållsfragmentmodell {#deleting-a-content-fragment-model}

>[!CAUTION]
>
>Om du tar bort en innehållsfragmentmodell kan det påverka beroende fragment.

Så här tar du bort en innehållsfragmentmodell:

1. Navigera till **Verktyg**, **Allmänt** och öppna sedan **Modeller för innehållsfragment**.

1. Navigera till mappen som innehåller innehållsfragmentmodellen.
1. Markera din modell, följt av **Ta bort** från verktygsfältet.

   >[!NOTE]
   >
   >Om modellen refereras visas en varning. Vidta åtgärder på lämpligt sätt.

## Publicera en innehållsfragmentmodell {#publishing-a-content-fragment-model}

Modeller för innehållsfragment måste publiceras när/innan beroende innehållsfragment publiceras.

Så här publicerar du en innehållsfragmentmodell:

1. Navigera till **Verktyg**, **Allmänt** och öppna sedan **Modeller för innehållsfragment**.

1. Navigera till mappen som innehåller innehållsfragmentmodellen.
1. Välj en modell, följt av **Publicera** i verktygsfältet.
Publiceringsstatusen anges i konsolen.

   >[!NOTE]
   >
   >Om du publicerar ett innehållsfragment för vilket modellen ännu inte har publicerats, visas detta i en urvalslista och modellen publiceras med fragmentet.

## Avpublicera en innehållsfragmentmodell {#unpublishing-a-content-fragment-model}

Modeller för innehållsfragment kan avpubliceras om de inte refereras av några fragment.

Så här avpublicerar du en innehållsfragmentmodell:

1. Navigera till **Verktyg**, **Allmänt** och öppna sedan **Modeller för innehållsfragment**.

1. Navigera till mappen som innehåller innehållsfragmentmodellen.
1. Välj en modell, följt av **Avpublicera** i verktygsfältet.
Publiceringsstatusen anges i konsolen.

Om du försöker avpublicera en modell som för närvarande används av ett eller flera fragment visas en felvarning om detta:

![Felmeddelande för innehållsfragmentmodell när en modell som används avpubliceras](assets/cfm-model-unpublish-error.png)

Meddelandet föreslår att du kontrollerar panelen [Referenser](/help/sites-cloud/authoring/basic-handling.md#references) för att undersöka mer:

![Modell för innehållsfragment i referenser](assets/cfm-model-references.png)

## Låsta (publicerade) modeller för innehållsfragment {#locked-published-content-fragment-models}

Den här funktionen tillhandahåller styrning för publicerade modeller för innehållsfragment.

### Utmaningen {#the-challenge}

* Content Fragment Models bestämmer schemat för GraphQL-frågor i AEM.

   * AEM GraphQL-scheman skapas så snart en Content Fragment Model skapas, och de kan finnas både i skribent- och publiceringsmiljöer.

   * Publiceringsscheman är de viktigaste eftersom de utgör grunden för leverans av innehåll i innehållsfragment i JSON-format.

* Problem kan uppstå när modeller för innehållsfragment ändras, eller med andra ord redigeras. Det innebär att schemat ändras, vilket i sin tur kan påverka befintliga GraphQL-frågor.

* Att lägga till nya fält i en innehållsfragmentmodell bör (vanligtvis) inte ha några skadliga effekter. Om du ändrar befintliga datafält (t.ex. namn) eller tar bort fältdefinitioner kommer befintliga GraphQL-frågor att brytas när de begär dessa fält.

### Krav {#the-requirements}

* Att göra användarna medvetna om riskerna vid redigering av modeller som redan används för leverans av direktsänt innehåll, med andra ord, modeller som har publicerats.

* För att undvika oönskade ändringar.

Någon av dessa kan göra att frågor bryts om de ändrade modellerna publiceras på nytt.

### Lösningen {#the-solution}

För att åtgärda dessa problem är Content Fragment Models *låst* i READ-ONLY-läge när de har skapats - så snart de har publicerats. Detta indikeras av **Låst**:

![Kort för låst innehållsfragmentmodell](assets/cfm-model-locked.png)

När modellen är **Låst** (i läget SKRIVSKYDDAD) kan du se innehållet och strukturen för modellerna, men du kan inte redigera dem.

Du kan hantera **låsta** modeller från konsolen eller modellredigeraren:

* Konsol

  Från konsolen kan du hantera läget SKRIVSKYDDAD med åtgärderna **Lås upp** och **Lås** i verktygsfältet:

  ![Verktygsfält för låst innehållsfragmentmodell](assets/cfm-model-locked.png)

   * Du kan **Lås upp** en modell om du vill aktivera redigeringar.

     Om du väljer **Lås upp** visas en varning och du måste bekräfta åtgärden **Lås upp**:
     ![Meddelande när innehållsfragmentmodellen låses upp](assets/cfm-model-unlock-message.png)

     Du kan sedan öppna modellen för redigering.

   * Du kan också **låsa** modellen i efterhand.
   * Om du publicerar om modellen återställs den omedelbart till läget **Låst** (SKRIVSKYDDAT).

* Modellredigerare

   * När du öppnar en låst modell får du en varning och tre åtgärder visas: **Avbryt**, **Visa skrivskyddad**, **Redigera**:

     ![Meddelande när en låst innehållsfragmentmodell visas](assets/cfm-model-editor-lock-message.png)

   * Om du väljer **Visa skrivskyddat** kan du se modellens innehåll och struktur:

     ![Visa skrivskyddad - låst innehållsfragmentmodell](assets/cfm-model-editor-locked-view-only.png)

   * Om du väljer **Redigera** kan du redigera och spara dina uppdateringar:

     ![Redigera - låst innehållsfragmentmodell](assets/cfm-model-editor-locked-edit.png)

     >[!NOTE]
     >
     >Det kan fortfarande finnas en varning överst, men det är när modellen redan används av befintliga innehållsfragment.

   * **Avbryt** återgår till konsolen.
