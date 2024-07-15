---
title: Modeller för innehållsfragment
description: Lär dig hur Content Fragment Models fungerar som en grund för dina innehållsfragment i AEM, vilket gör att du kan skapa strukturerat innehåll som kan användas för rubrikfri leverans eller sidredigering.
feature: Content Fragments
role: User, Developer, Architect
exl-id: 8ab5b15f-cefc-45bf-a388-928e8cc8c603
solution: Experience Manager Sites
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '3209'
ht-degree: 1%

---

# Modeller för innehållsfragment {#content-fragment-models}

Content Fragment Models i Adobe Experience Manager (AEM) as a Cloud Service definierar strukturen för innehållet i dina [Content Fragments](/help/sites-cloud/administering/content-fragments/overview.md). Dessa fragment kan sedan användas för att skapa sidor eller som grund för ditt headless-innehåll.

Så här använder du modeller för innehållsfragment:

1. [Aktivera funktionen Content Fragment Model för instansen](/help/sites-cloud/administering/content-fragments/setup.md)
1. [Skapa](#creating-a-content-fragment-model) och [konfigurera](#defining-your-content-fragment-model), dina modeller för innehållsfragment
1. [Aktivera dina modeller för innehållsfragment](#enabling-disabling-a-content-fragment-model) för användning när du skapar innehållsfragment
1. [Tillåt dina modeller för innehållsfragment i de nödvändiga Assets-mapparna](#allowing-content-fragment-models-assets-folder) genom att konfigurera **Profiler**.

## Skapa en innehållsfragmentmodell {#creating-a-content-fragment-model}

1. Navigera till **Verktyg**, **Allmänt** och öppna sedan **Modeller för innehållsfragment**.
1. Navigera till den mapp som passar din [konfiguration eller underkonfiguration](/help/sites-cloud/administering/content-fragments/setup.md).
1. Använd **Skapa** för att öppna guiden.

   >[!CAUTION]
   >
   >Om [användningen av Content Fragment-modeller inte har aktiverats](/help/sites-cloud/administering/content-fragments/setup.md) är alternativet **Skapa** inte tillgängligt.

1. Ange **modelltitel**.
Du kan också definiera olika egenskaper. Du kan till exempel lägga till **taggar**, en **beskrivning**, välja **Aktivera modell** för att [aktivera modellen](#enabling-disabling-a-content-fragment-model) om det behövs och definiera
   **URL-mönster för standardförhandsgranskning**.

   >[!NOTE]
   >
   >Mer information finns i [Modell för innehållsfragment - Egenskaper](#content-fragment-model-properties).

   ![Titel och beskrivning](assets/cf-cfmodels-create.png)

1. Använd **Skapa** för att spara den tomma modellen. Ett meddelande anger att åtgärden lyckades. Du kan välja **Öppna** om du vill redigera modellen omedelbart eller **Klar** om du vill återgå till konsolen.

>[!CAUTION]
>
>Om du ska fråga mot flera refererade fragment rekommenderar vi inte att de olika fragmentmodellerna har fältnamn med samma namn, utan olika typer.
>
>Mer information finns i [AEM GraphQL API för användning med innehållsfragment - begränsningar](/help/headless/graphql-api/content-fragments.md#limitations)

### Content Fragment Model - egenskaper {#content-fragment-model-properties}

De här egenskaperna definieras när du skapar en modell och kan redigeras senare med alternativet **Egenskaper** för innehållsfragmentmodellen:

* **Grundläggande**
   * **Modelltitel**
   * **Taggar**
   * **Beskrivning**
   * **Aktivera modell**
   * **URL-mönster för standardförhandsvisning**
Med redigeraren för innehållsfragment kan författare **förhandsgranska** sitt innehåll i ett externt klientprogram. När **förhandsgranskningstjänsten** har konfigurerats lägger du till URL:en för klientprogrammet.

     URL:en för förhandsgranskning bör följa detta mönster:
    `https://<preview_url>?param=${expression}`

     Tillgängliga uttryck är:

      * `${contentFragment.path}`
      * `${contentFragment.model.path}`
      * `${contentFragment.model.name}`
      * `${contentFragment.variation}`
      * `${contentFragment.id}`

   * **Överför bild**

<!-- CHECK: currently under FT -->
<!--
* **GraphQL**
  Define names relevant for GraphQL.
  Changing the GraphQL API Name, or Query field names will impact client applications.
  * **API Name**
    Represents the GraphQL type and query field names in the GraphQL schema.
  * **Single Query Field Name**
    Represents the GraphQL single query field name in the GraphQL schema.
  * **Multiple Query Field Name**
    Represents the GraphQL multiple query field name in the GraphQL schema.
-->

## Definiera innehållsfragmentmodellen {#defining-your-content-fragment-model}

Content Fragment Model definierar effektivt strukturen för de resulterande innehållsfragmenten med hjälp av ett urval av **[datatyper](#data-types)**. Med modellredigeraren kan du lägga till instanser av datatyperna och sedan konfigurera dem för att skapa de obligatoriska fälten:

>[!CAUTION]
>
>Om du redigerar en modell som redan används av befintliga innehållsfragment kan det påverka de beroende fragmenten.

1. Navigera till **Verktyg**, **Allmänt** och öppna sedan **Modeller för innehållsfragment**.

1. Navigera till den mapp som innehåller innehållsfragmentmodellen.
1. Öppna den modell som krävs för **Redigera**. Använd snabbåtgärden eller markera modellen och sedan åtgärden från verktygsfältet.

   När du har öppnat modellredigeraren visas följande:

   * vänster: fält har redan definierats
   * höger: **Datatyper** som är tillgängliga för att skapa fält (och **egenskaper** som kan användas när fälten har skapats)

   >[!NOTE]
   >
   >När ett fält definieras som **Obligatoriskt** markeras **Label** som anges i den vänstra rutan med ett asterix (**&#42;**).

![Egenskaper](assets/cf-cfmodels-empty-model.png)

1. **Lägga till ett fält**

   * Dra en obligatorisk datatyp till önskad plats för ett fält:

     ![Dra datatypen för att skapa fältet](assets/cf-cfmodels-create-field.png)

   * När ett fält har lagts till i modellen visar den högra panelen de **egenskaper** som kan definieras för den aktuella datatypen. Här definierar du vad som krävs för fältet.

      * Många egenskaper är självförklarande. Mer information finns i [Egenskaper](#properties).
      * Om du skriver en **fältetikett** slutförs **egenskapsnamnet** automatiskt, om det är tomt, och kan uppdateras manuellt efteråt.

        >[!CAUTION]
        >
        När egenskapen **Egenskapsnamn** uppdateras manuellt för en datatyp, får namn bara innehålla ** A-Z, a-z, 0-9 och understreck&quot;_&quot; som specialtecken.
        >
        Om modeller som skapats i tidigare versioner av AEM innehåller ogiltiga tecken tar du bort eller uppdaterar dessa tecken.

     Till exempel:

     ![Fältegenskaper](assets/cf-cfmodels-field-properties.png)

1. **Ta bort ett fält**

   Markera det obligatoriska fältet och välj sedan papperskorgsikonen. Du ombeds bekräfta åtgärden.

   ![Ta bort](assets/cf-cfmodels-remove-icon.png)

1. Lägg till alla obligatoriska fält och definiera de relaterade egenskaperna efter behov. Till exempel:

   ![Spara](assets/cf-cfmodels-save.png)

1. Välj **Spara** om du vill behålla definitionen.

## Datatyper {#data-types}

Det finns ett urval datatyper som du kan använda för att definiera din modell:

* **Enkelradig text**
   * Lägg till ett eller flera fält med en enda textrad. Den maximala längden kan definieras
* **Flerradstext**
   * Ett textområde som kan vara RTF, Oformaterad text eller Markering

  >[!NOTE]
  >
  Oavsett om textområdet är RTF, Oformaterad text eller Markering definieras i modellen av egenskapen **Standardtyp**.
  >
  Det här formatet kan inte ändras från [redigeraren för innehållsfragment](/help/sites-cloud/administering/content-fragments/authoring.md), utan bara från modellen.

* **Number**
   * Lägg till ett eller flera numeriska fält
* **Boolean**
   * Lägg till en boolesk kryssruta
* **Datum och tid**
   * Lägg till ett datum och/eller en tid
* **Uppräkning**
   * Lägga till en uppsättning kryssrutefält, alternativknappar eller nedrullningsbara listrutor
* **Taggar**
   * Tillåter fragmentförfattare att komma åt och markera taggområden
* **Innehållsreferens**
   * Refererar till annat innehåll, oavsett typ; kan användas för att [skapa kapslat innehåll](#using-references-to-form-nested-content)
   * Om en bild refereras kan du välja att visa en miniatyrbild
* **Fragmentreferens**
   * Refererar till andra innehållsfragment; kan användas för att [skapa kapslat innehåll](#using-references-to-form-nested-content)
   * Datatypen kan konfigureras så att fragmentförfattare kan:
      * Redigera det refererade fragmentet direkt.
      * Skapa ett nytt innehållsfragment baserat på lämplig modell
* **JSON-objekt**
   * Gör att innehållsfragmentets författare kan ange JSON-syntax i motsvarande element i ett fragment.
      * För att AEM ska kunna lagra direkt JSON som du har kopierat/klistrat in från en annan tjänst.
      * JSON skickas och skrivs ut som JSON i GraphQL.
      * Innehåller JSON-syntaxmarkering, automatisk komplettering och felmarkering i Content Fragment Editor.
* **Platshållare för flik**
   * Tillåter att flikar kan användas när innehållet i innehållsfragmentet redigeras.
      * Dessa visas som avgränsare i modellredigeraren, och delar upp avsnitt i listan med innehållsdatatyper. Varje instans representerar början på en ny flik.
      * I fragmentredigeraren visas varje instans som en flik.

     >[!NOTE]
     >
     Den här datatypen används endast för formatering, den ignoreras av AEM GraphQL-schema.

## Egenskaper {#properties}

Många egenskaper är självförklarande, för vissa egenskaper finns ytterligare information nedan:

* **Egenskapsnamn**

  När den här egenskapen uppdateras manuellt för en datatyp, måste **innehålla** *endast* A-Z, a-z, 0-9 och understreck&quot;_&quot; som specialtecken.

  >[!CAUTION]
  >
  Om modeller som skapats i tidigare versioner av AEM innehåller ogiltiga tecken tar du bort eller uppdaterar dessa tecken.

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
  Unikitet säkerställs per språkrot.

  >[!NOTE]
  >
  Variationer kan ha samma *unika*-värde som varianter av samma fragment, men inte samma värde som används i andra variationer av fragment.

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

* **[Innehållsreferens](#content-reference)**
   * Ger en enkel referens till annat innehåll, av alla typer.
   * Kan konfigureras för en eller flera referenser (i det resulterande fragmentet).

* **[Fragmentreferens](#fragment-reference-nested-fragments)** (kapslade fragment)
   * Refererar till andra fragment, beroende på vilka specifika modeller som anges.
   * Gör att du kan ta med/hämta strukturerade data.
     >[!NOTE]
     >
     Den här metoden är särskilt intressant när du använder [Headless Content Delivery med hjälp av Content Fragments med GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).
   * Kan konfigureras för en eller flera referenser (i det resulterande fragmentet).

>[!NOTE]
>
AEM har upprepningsskydd för:
>
* Innehållsreferenser
Detta förhindrar att användaren lägger till en referens till det aktuella fragmentet och kan leda till en tom dialogruta för fragmentreferensväljaren.
>
* Fragmentreferenser i GraphQL
Om du skapar en djup fråga som returnerar flera innehållsfragment som refereras av varandra, returneras null vid den första förekomsten.

>[!CAUTION]
>
Om du ska fråga mot flera refererade fragment rekommenderar vi inte att de olika fragmentmodellerna har fältnamn med samma namn, utan olika typer.
>
Mer information finns i [AEM GraphQL API för användning med innehållsfragment - begränsningar](/help/headless/graphql-api/content-fragments.md#limitations)

### Innehållsreferens {#content-reference}

Med Innehållsreferens kan du återge innehåll från en annan källa, till exempel bild, sida eller Experience Fragment.

Förutom standardegenskaper kan du ange:

* **Rotsökvägen**, som anger var det refererade innehållet ska lagras
  >[!NOTE]
  >
  Detta är obligatoriskt om du vill överföra och referera till bilder direkt i det här fältet när du använder redigeraren för innehållsfragment.
  >
  Mer information finns i [Referensbilder](/help/sites-cloud/administering/content-fragments/authoring.md#reference-images).

* De innehållstyper som kan refereras
  >[!NOTE]
  >
  Dessa måste innehålla **Bild** om du vill överföra och referera till bilder direkt i det här fältet när du använder redigeraren för innehållsfragment.
  >
  Mer information finns i [Referensbilder](/help/sites-cloud/administering/content-fragments/authoring.md#reference-images).

* Begränsningar för filstorlekar
* Om en bild refereras:
   * Visa miniatyrbild
   * Bildbegränsningar för höjd och bredd

![Innehållsreferens](assets/cf-cfmodels-content-reference.png)

### Fragmentreferens (kapslade fragment) {#fragment-reference-nested-fragments}

Fragmentreferensen refererar till ett eller flera innehållsfragment. Den här funktionen är av särskilt intresse när du hämtar innehåll som ska användas i din app, eftersom du kan hämta strukturerade data med flera lager.

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
Fragmentreferenser är av särskilt intresse för [Headless Content Delivery med hjälp av Content Fragments med GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).

Förutom standardegenskaper kan du definiera:

* **Återge som**:

   * **multifield** - fragmentförfattaren kan skapa flera, enskilda referenser

   * **fragmentreferens** - tillåter fragmentförfattaren att välja en enskild referens till ett fragment

* **Modelltyp**
Du kan välja flera modeller. När du lägger till referenser till ett innehållsfragment måste alla refererade fragment ha skapats med dessa modeller.

* **Rotsökväg**
Detta anger en rotsökväg för alla fragment som refereras.

* **Tillåt att fragment skapas**

  Detta gör att fragmentförfattaren kan skapa ett fragment baserat på lämplig modell.

   * **fragmentreferenssammansatt** - tillåter fragmentförfattaren att skapa en sammansatt bild genom att markera flera fragment

  ![Fragmentreferens](assets/cf-cfmodels-fragment-reference.png)

>[!NOTE]
>
Det finns en mekanism för upprepningsskydd. Det förhindrar användaren från att markera det aktuella innehållsfragmentet i fragmentreferensen och kan leda till en tom dialogruta för fragmentreferensväljaren.
>
Det finns också upprepningsskydd för fragmentreferenser i GraphQL. Om du skapar en djup fråga i två innehållsfragment som refererar till varandra returneras null.

## Aktivera eller inaktivera en innehållsfragmentmodell {#enabling-disabling-a-content-fragment-model}

Du kan antingen **Aktivera** eller **Inaktivera** dina modeller för innehållsfragment, så att du har fullständig kontroll över hur de används.

### Aktivera en innehållsfragmentmodell {#enabling-a-content-fragment-model}

När en modell har skapats måste den aktiveras så att den:

* Kan markeras när du skapar ett innehållsfragment.
* Kan refereras inifrån en innehållsfragmentmodell.
* Är tillgängligt för GraphQL, så schemat genereras.

Så här aktiverar du en modell som har flaggats som antingen:

* **Utkast** : nytt (aldrig aktiverat).
* **Inaktiverad** : har inaktiverats specifikt.

Du använder alternativet **Aktivera** från antingen:

* Det övre verktygsfältet när den obligatoriska modellen är markerad.
* Motsvarande snabbåtgärd (mouse-over the required Model).

![Aktivera ett utkast eller en inaktiverad modell](assets/cf-cfmodels-status-enable.png)

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

![Inaktivera en aktiverad modell](assets/cf-cfmodels-status-disable.png)

## Tillåt modeller för innehållsfragment i din Assets-mapp {#allowing-content-fragment-models-assets-folder}

Om du vill implementera innehållsstyrning kan du konfigurera **profiler** i Assets-mappen för att styra vilka innehållsfragmentmodeller som tillåts för att skapa fragment i den mappen.

>[!NOTE]
>
Mekanismen liknar [tillåter sidmallar](/help/sites-cloud/authoring/sites-console/templates.md#allowing-a-template-author) för en sida och dess underordnade sidor i avancerade egenskaper för en sida.

Så här konfigurerar du **principer** för **Tillåtna modeller för innehållsfragment**:

1. Navigera och öppna **Egenskaper** för den Assets-mapp som krävs.

1. Öppna fliken **Profiler** där du kan konfigurera:

   * **Ärvd från`<folder>`**

     Principer ärvs automatiskt när nya underordnade mappar skapas. Principen kan konfigureras om (och arvet brytas) om undermappar måste tillåta modeller som skiljer sig från den överordnade mappen.

   * **Tillåtna modeller för innehållsfragment via sökväg**

     Flera modeller kan tillåtas.

   * **Tillåtna modeller för innehållsfragment efter tagg**

     Flera modeller kan tillåtas.

   ![Modellprincip för innehållsfragment](assets/cf-cfmodels-policy-assets-folder.png)

1. **Spara** eventuella ändringar.

De Content Fragment-modeller som tillåts för en mapp löses enligt följande:
* **Profiler** för **Tillåtna modeller för innehållsfragment**.
* Om den är tom kan du försöka identifiera principen med arvsreglerna.
* Om arvskedjan inte ger något resultat ska du titta på konfigurationen **Cloud Services** för den mappen (också först direkt och sedan via arv).
* Om inget av ovanstående ger några resultat finns det inga tillåtna modeller för den mappen.

## Ta bort en innehållsfragmentmodell {#deleting-a-content-fragment-model}

>[!CAUTION]
>
Om du tar bort en modell för innehållsfragment kan det påverka beroende fragment.

Så här tar du bort en innehållsfragmentmodell:

1. Navigera till **Verktyg**, **Allmänt** och öppna sedan **Modeller för innehållsfragment**.

1. Navigera till den mapp som innehåller innehållsfragmentmodellen.
1. Markera din modell, följt av **Ta bort** från verktygsfältet.

   >[!NOTE]
   >
   Om det finns referenser till modellen visas en varning så att du kan vidta lämpliga åtgärder.

## Publicera en innehållsfragmentmodell {#publishing-a-content-fragment-model}

Content Fragment Models måste publiceras när/innan beroende Content Fragments publiceras.

Så här publicerar du en innehållsfragmentmodell:

1. Navigera till **Verktyg**, **Allmänt** och öppna sedan **Modeller för innehållsfragment**.

1. Navigera till den mapp som innehåller innehållsfragmentmodellen.
1. Välj en modell, följt av **Publish** i verktygsfältet.
Publiceringsstatusen visas i konsolen.

   >[!NOTE]
   >
   Om du publicerar ett innehållsfragment för vilket modellen ännu inte har publicerats, visas detta i en urvalslista och modellen publiceras med fragmentet.

## Avpublicera en innehållsfragmentmodell {#unpublishing-a-content-fragment-model}

Modeller för innehållsfragment kan avpubliceras om de inte refereras av några fragment.

Så här avpublicerar du en innehållsfragmentmodell:

1. Navigera till **Verktyg**, **Allmänt** och öppna sedan **Modeller för innehållsfragment**.

1. Navigera till den mapp som innehåller innehållsfragmentmodellen.
1. Välj en modell, följt av **Avpublicera** i verktygsfältet.
Publiceringsstatusen anges i konsolen.

Om du försöker avpublicera en modell som för närvarande används av ett eller flera fragment visas en felvarning. Till exempel:

![Felmeddelande för innehållsfragmentmodell när en modell som används avpubliceras](assets/cf-cfmodels-unpublish-error.png)

Meddelandet tyder på att du bör kontrollera panelen [Referenser](/help/sites-cloud/authoring/basic-handling.md#references) för att undersöka mer:

![Modell för innehållsfragment i referenser](assets/cf-cfmodels-references.png)

## Låsta (publicerade) modeller för innehållsfragment {#locked-published-content-fragment-models}

Den här funktionen tillhandahåller styrning för publicerade modeller för innehållsfragment.

### Utmaningen {#the-challenge}

* Content Fragment Models bestämmer schemat för GraphQL-frågor i AEM.

   * AEM GraphQL-scheman skapas så snart en innehållsfragmentmodell skapas, och de kan finnas både i författar- och publiceringsmiljöer.

   * Publiceringsscheman är de viktigaste eftersom de utgör grunden för leverans av innehåll i innehållsfragment i JSON-format.

* Problem kan uppstå när modeller för innehållsfragment ändras, eller med andra ord redigeras. Det innebär att schemat ändras, vilket i sin tur kan påverka befintliga GraphQL-frågor.

* Att lägga till nya fält i en innehållsfragmentmodell bör (vanligtvis) inte ha några skadliga effekter. Om du ändrar befintliga datafält (t.ex. namn) eller tar bort fältdefinitioner kommer befintliga GraphQL-frågor att brytas när de begär dessa fält.

### Krav {#the-requirements}

* Att göra användarna medvetna om riskerna vid redigering av modeller som redan används för leverans av direktsänt innehåll, med andra ord, modeller som har publicerats).

* För att undvika oönskade ändringar.

Något av dessa villkor kan göra att frågor bryts om de ändrade modellerna publiceras på nytt.

### Lösningen {#the-solution}

För att åtgärda dessa problem är Content Fragment Models *låst* i READ-ONLY-läge när de har skapats - så snart de har publicerats. Den här statusen anges av **Låst**:

![Kort för låst innehållsfragmentmodell](assets/cf-cfmodels-locked.png)

När modellen är **Låst** (i läget SKRIVSKYDDAD) kan du se innehållet och strukturen för modellerna, men du kan inte redigera dem.

Du kan hantera **låsta** modeller från konsolen eller modellredigeraren:

* Konsol

  Från konsolen kan du hantera läget SKRIVSKYDDAD med åtgärderna **Lås upp** och **Lås** i verktygsfältet:

  ![Verktygsfält för låst innehållsfragmentmodell](assets/cf-cfmodels-locked.png)

   * Du kan **Lås upp** en modell om du vill aktivera redigeringar.

     Om du väljer **Lås upp** visas en varning och du måste bekräfta åtgärden **Lås upp**:
     ![Meddelande när innehållsfragmentmodellen låses upp](assets/cf-cfmodels-unlock-message.png)

     Du kan sedan öppna modellen för redigering.

   * Du kan också **låsa** modellen i efterhand.
   * Om du publicerar om modellen återgår den omedelbart till läget **Låst** (SKRIVSKYDDAT).

* Modellredigerare

   * När du öppnar en låst modell får du en varning och tre åtgärder visas: **Avbryt**, **Visa skrivskyddad**, **Redigera**:

     ![Meddelande när en låst innehållsfragmentmodell visas](assets/cf-cfmodels-editor-lock-message.png)

   * Om du väljer **Visa skrivskyddat** kan du se modellens innehåll och struktur:

     ![Visa skrivskyddad - låst innehållsfragmentmodell](assets/cf-cfmodels-editor-locked-view-only.png)

   * Om du väljer **Redigera** kan du redigera och spara dina uppdateringar:

     ![Redigera - låst innehållsfragmentmodell](assets/cf-cfmodels-editor-locked-edit.png)

     >[!NOTE]
     >
     Det kan fortfarande finnas en varning överst, men det är när modellen redan används av befintliga innehållsfragment.

   * **Avbryt** returnerar dig till konsolen.
