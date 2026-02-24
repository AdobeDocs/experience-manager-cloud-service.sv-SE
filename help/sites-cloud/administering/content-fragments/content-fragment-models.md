---
title: Definiera modeller för innehållsfragment
description: Läs om hur Content Fragment Models fungerar som grund för dina innehållsfragment i AEM, så att du kan skapa strukturerat innehåll som kan användas för rubrikfri leverans eller framtagning av sidor.
feature: Content Fragments
role: User, Developer
badgeSaas: label="AEM Sites" type="Positive" tooltip="Gäller AEM Sites)."
exl-id: 8ab5b15f-cefc-45bf-a388-928e8cc8c603
solution: Experience Manager Sites
source-git-commit: 98c0c9b6adbc3d7997bc68311575b1bb766872a6
workflow-type: tm+mt
source-wordcount: '2223'
ht-degree: 0%

---

# Definiera modeller för innehållsfragment {#defining-content-fragment-models}

Content Fragment Models i Adobe Experience Manager (AEM) as a Cloud Service definierar strukturen för innehållet i dina [Content Fragments](/help/sites-cloud/administering/content-fragments/overview.md). Dessa fragment kan sedan användas för att skapa sidor eller som grund för ditt headless-innehåll.

På den här sidan beskrivs hur du definierar innehållsfragmentmodellen med den dedikerade redigeraren. Se [Hantera dina modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md) för ytterligare uppgifter och alternativ som är tillgängliga när fragmenten har skapats, inklusive [åtgärder som är tillgängliga från konsolen för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#actions), [som tillåter modellen i din mapp](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#allowing-content-fragment-models-assets-folder) och [publicera modellen](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#publishing-a-content-fragment-model).

>[!NOTE]
>
>Observera [Bästa praxis](/help/sites-cloud/administering/content-fragments/overview.md#best-practices) när du arbetar med modeller för innehållsfragment och innehållsfragment.

>[!CAUTION]
>
>Om du ska fråga mot flera refererade fragment rekommenderar vi inte att de olika fragmentmodellerna har fältnamn med samma namn, utan olika typer.
>
>Mer information finns i [AEM GraphQL API för användning med innehållsfragment - begränsningar](/help/headless/graphql-api/content-fragments.md#limitations)

>[!NOTE]
>
>Om du skapar en modell med den nya redigeraren bör du alltid använda den här redigeraren för den modellen.
>
>Om du sedan öppnar modellen med den [ursprungliga modellredigeraren](/help/assets/content-fragments/content-fragments-models.md) visas meddelandet:
>
>* &quot;Den här modellen har ett anpassat gränssnittsschema konfigurerat. Fältordningen som visas i det här användargränssnittet kanske inte matchar användargränssnittets schema. Om du vill visa de fält som är justerade mot gränssnittets schema måste du växla till den nya redigeraren för innehållsfragment.&quot;

## Definiera innehållsfragmentmodellen {#defining-your-content-fragment-model}

Content Fragment Model definierar effektivt strukturen för de resulterande innehållsfragmenten med hjälp av ett urval av **[datatyper](#data-types)**. Med modellredigeraren kan du lägga till instanser av datatyperna och sedan konfigurera dem för att skapa de obligatoriska fälten:

>[!CAUTION]
>
>Om du redigerar en modell som redan används av befintliga innehållsfragment kan det påverka de beroende fragmenten.

1. Markera panelen för [modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#basic-structure-handling-content-fragment-models-console) i konsolen för innehållsfragment och navigera till mappen där modellen för innehållsfragment finns.

   >[!NOTE]
   >
   >Du kan också öppna en modell direkt efter att du har [skapat den](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#creating-a-content-fragment-model).

1. Öppna den modell som krävs för **Redigera**. Använd någon av snabbredigeringslänkarna eller markera modellen och sedan åtgärden i verktygsfältet.


   ![Egenskaper](assets/cf-cfmodels-empty-model.png)

   När du har öppnat modellredigeraren visas följande:

   * överkant:
      * **Hem** - ikon
      * alternativ för att växla mellan den [ursprungliga](/help/assets/content-fragments/content-fragments-models.md) och den nya redigeraren
      * **Avbryt**
      * **Spara**

   * vänster: **Datatyper** tillgängliga för att skapa fält

   * mitten: fält som redan har definierats tillsammans med alternativet **Lägg till**

   * höger: med ikonerna längst till höger kan du välja mellan:

      * **Egenskaper**: definiera och visa egenskaper för det markerade fältet
      * **Modellinformation**: visa status **Aktiverad**, **Modelltitel**, **Taggar**, **Beskrivning** och **Förhandsgranska URL**

1. **Lägga till ett fält**

   * Antingen:

      * Dra en datatyp från den vänstra panelen till önskad plats för ett fält i den mittersta panelen.
      * Välj ikonen **+** efter en datatyp för att lägga till den längst ned i fältlistan.
      * Välj **Lägg till** i den mellersta panelen och sedan den önskade datatypen i den nedrullningsbara listan för att lägga till ett fält längst ned i listan.

     >[!NOTE]
     >
     >**Flikplatshållarfält** måste alltid visas ovanför befintliga fält.

   * Du kan flytta ett fält med hjälp av punktformaten till vänster i fältrutan:

     ![Flytta fält](assets/cf-cfmodels-move-field-icon.png)

   * När ett fält har lagts till i modellen (och markerats) visar den högra panelen **Egenskaper** som kan definieras för den aktuella datatypen. Här kan du definiera vad som krävs för den specifika
fält.

      * Många egenskaper är självförklarande. Mer information finns i [Egenskaper (datatyper)](#properties).
      * Om du skriver en **fältetikett** slutförs **egenskapsnamnet** automatiskt, om det är tomt, och kan uppdateras manuellt efteråt.

        >[!CAUTION]
        >
        >När egenskapen **Egenskapsnamn** uppdateras manuellt för en datatyp, får namn bara innehålla ** A-Z, a-z, 0-9 och understreck&quot;_&quot; som specialtecken.
        >
        >Om modeller som skapats i tidigare versioner av AEM innehåller ogiltiga tecken tar du bort eller uppdaterar dessa tecken.

     Till exempel:

     ![Fältegenskaper](assets/cf-cfmodels-field-properties.png)

     >[!NOTE]
     >
     >När ett fält definieras som **Obligatoriskt** markeras **Label** i den mittersta rutan med en asterix (**&#42;**).

1. **Ta bort ett fält**

   Välj papperskorgsikonen för det aktuella fältet på den mittersta panelen.

   ![Ta bort](assets/cf-cfmodels-remove-icon.png)

1. Lägg till alla obligatoriska fält och definiera de relaterade egenskaperna efter behov.

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

     <!--
    * Internally the reference is held as a universally unique ID (UUID) that references the resource
    * You do not need to know the UUID; in the fragment editor you can browse to the required fragment.
    -->

  <!--
  >[!NOTE]
  >
  >The UUIDs are repository specific. If you use the [Content Copy Tool](/help/implementing/developing/tools/content-copy.md) to copy Content Fragments, the UUIDs will be recalculated in the target environment.
  -->

* **Innehållsreferens**
   * Refererar till annat innehåll, oavsett typ; kan användas för att [skapa kapslat innehåll](#using-references-to-form-nested-content)
   * Om en bild refereras kan du välja att visa en miniatyrbild
   * Fältet kan konfigureras så att fragmentförfattare kan skapa nya instanser av fältet
   * Referensen anger sökvägen till den refererade resursen, till exempel `/content/dam/path/to/resource`

     <!--
    * Internally the reference is held as a universally unique ID (UUID) that references the resource
    * You do not need to know the UUID; in the fragment editor you can browse to the required asset resource
    -->

  <!--
  >[!NOTE]
  >
  >The UUIDs are repository specific. If you use the [Content Copy Tool](/help/implementing/developing/tools/content-copy.md) to copy Content Fragments, the UUIDs will be recalculated in the target environment.
  -->

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
     >
     >**Flikplatshållarfält** måste alltid visas ovanför befintliga fält.

## Egenskaper (datatyper) {#properties}

Många egenskaper är självförklarande, för vissa egenskaper finns ytterligare information nedan:

* **Egenskapsnamn**

  När den här egenskapen uppdateras manuellt för en datatyp, måste **innehålla** *endast* A-Z, a-z, 0-9 och understreck&quot;_&quot; som specialtecken.

  >[!CAUTION]
  >
  >Om modeller som skapats i tidigare versioner av AEM innehåller ogiltiga tecken tar du bort eller uppdaterar dessa tecken.

* **Återge som**

  De olika alternativen för att realisera/återge fältet i ett fragment. Detta gör ofta att du kan ange om författaren ska se en enda instans av fältet eller om den ska kunna skapa flera instanser. När **Flera fält** används kan du definiera minsta och högsta antal objekt - se [Validering](#validation) för mer information.

* **Fältetikett**
Om du anger en **fältetikett** genereras ett **egenskapsnamn** automatiskt, som sedan kan uppdateras manuellt om det behövs.

* **Validering**
Grundläggande validering är tillgängligt av mekanismer som egenskapen **Required** . Vissa datatyper har ytterligare valideringsfält. Mer information finns i [Validering](#validation).

* För datatypen **Flerradig text** går det att definiera **standardtypen** som endera:

   * **RTF**
   * **Markdown**
   * **Oformaterad text**

  Om inget anges används standardvärdet **RTF** för det här fältet.

  Om du ändrar **standardtypen** i en modell för innehållsfragment börjar det bara gälla för ett befintligt, relaterat innehållsfragment efter att fragmentet har öppnats i redigeraren och sparats.

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
   * Testa om det finns en viss modell för innehållsfragment.
* **Minsta antal objekt** / **Max antal objekt**

  Fält som har definierats som ett **flera fält** (anges med **Återge som**) har följande alternativ:

   * **Minsta antal objekt**
   * **Maximalt antal objekt**

  Dessa valideras i [redigeraren för innehållsfragment](/help/sites-cloud/administering/content-fragments/authoring.md).

## Använda referenser till kapslat innehåll {#using-references-to-form-nested-content}

Innehållsfragment kan skapa kapslat innehåll med någon av följande datatyper:

* [Innehållsreferens](#content-reference)
   * Ger en enkel referens till annat innehåll, av alla typer.
   * Tillhandahålls av datatypen **Content Reference**
   * Kan konfigureras för en eller flera referenser (i det resulterande fragmentet).

* [Fragmentreferens](#fragment-reference-nested-fragments) (kapslade fragment)
   * Refererar till andra fragment, beroende på vilka specifika modeller som anges.
   * Tillhandahålls av datatypen **Fragmentreferens**
   * Gör att du kan ta med/hämta strukturerade data.

     >[!NOTE]
     >
     >Den här metoden är särskilt intressant när du använder [Headless Content Delivery med hjälp av Content Fragments med GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).
   * Kan konfigureras för en eller flera referenser (i det resulterande fragmentet).

<!--
>[!NOTE]
>
>See [Upgrade your Content Fragments for UUID References](/help/headless/graphql-api/uuid-reference-upgrade.md) for further information about Content/Fragment Reference and Content/Fragment Reference (UUID), and upgrading to the UUID-based data types.
-->

>[!NOTE]
>
>AEM har upprepningsskydd för:
>
>* Innehållsreferenser
>  Detta förhindrar att användaren lägger till en referens till det aktuella fragmentet och kan leda till en tom dialogruta för fragmentreferensväljaren.
>
>* Fragmentreferenser i GraphQL
>  Om du skapar en djup fråga som returnerar flera innehållsfragment som refereras av varandra, returneras null vid den första förekomsten.

>[!CAUTION]
>
>Om du ska fråga mot flera refererade fragment rekommenderar vi inte att de olika fragmentmodellerna har fältnamn med samma namn, utan olika typer.
>
>Mer information finns i [AEM GraphQL API för användning med innehållsfragment - begränsningar](/help/headless/graphql-api/content-fragments.md#limitations)

### Innehållsreferens {#content-reference}

Datatypen **Innehållsreferens** gör att du kan återge innehåll från en annan källa, till exempel bild, sida eller Experience Fragment.

Förutom standardegenskaper kan du ange:

* **Rotsökvägen** som anger, eller representerar, var det refererade innehållet ska lagras

  >[!NOTE]
  >
  >Detta är obligatoriskt om du vill överföra och referera till bilder direkt i det här fältet när du använder redigeraren för innehållsfragment.
  >
  >Mer information finns i [Referensbilder](/help/sites-cloud/administering/content-fragments/authoring.md#reference-images).

* De innehållstyper som kan refereras

  >[!NOTE]
  >
  >Dessa måste innehålla **Bild** om du vill överföra och referera till bilder direkt i det här fältet när du använder redigeraren för innehållsfragment.
  >
  >Mer information finns i [Referensbilder](/help/sites-cloud/administering/content-fragments/authoring.md#reference-images).

* Begränsningar för filstorlekar
* Om en bild refereras:

   * Visa miniatyrbild
   * Bildbegränsningar för höjd och bredd

![Innehållsreferens](assets/cf-cfmodels-content-reference.png)

### Fragmentreferens (kapslade fragment) {#fragment-reference-nested-fragments}

Datatypen **Fragmentreferens** kan referera till ett eller flera innehållsfragment. Den här funktionen är av särskilt intresse när du hämtar innehåll som ska användas i din app, eftersom du kan hämta strukturerade data med flera lager.

Till exempel:

* En modell som definierar detaljer för en anställd, inklusive:
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
>Fragmentreferenser är av särskilt intresse för [Headless Content Delivery med hjälp av Content Fragments med GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).

Förutom standardegenskaper kan du definiera:

* **Återge som**:

   * **multifield** - fragmentförfattaren kan skapa flera, enskilda referenser

   * **fragmentreferens** - tillåter fragmentförfattaren att välja en enskild referens till ett fragment

* **Modelltyp**
Du kan välja flera modeller. När du lägger till referenser till ett innehållsfragment måste alla refererade fragment ha skapats med dessa modeller.

* **Rotsökväg**
Detta anger, eller representerar, en rotsökväg för alla fragment som refereras.

* **Tillåt att fragment skapas**

  Detta gör att fragmentförfattaren kan skapa ett fragment baserat på lämplig modell.

   * **fragmentreferenssammansatt** - tillåter fragmentförfattaren att skapa en sammansatt bild genom att markera flera fragment

  ![Fragmentreferens](assets/cf-cfmodels-fragment-reference.png)

>[!NOTE]
>
>Det finns en mekanism för upprepningsskydd. Det förhindrar användaren från att markera det aktuella innehållsfragmentet i fragmentreferensen och kan leda till en tom dialogruta för fragmentreferensväljaren.
>
>Det finns också upprepningsskydd för fragmentreferenser i GraphQL. Om du skapar en djup fråga i två innehållsfragment som refererar till varandra returneras null.
