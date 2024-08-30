---
title: Vad är adaptiva formuläruttryck?
description: Använd adaptiva Forms-uttryck för att lägga till automatisk validering, beräkning och aktivera eller inaktivera synlighet för ett avsnitt.
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: 937bd4653e454beea3111cfc7ef7b4bbc1ace193
workflow-type: tm+mt
source-wordcount: '2686'
ht-degree: 0%

---


# Adaptiva formuläruttryck {#adaptive-form-expressions}

Adaptiv Forms ger optimerad och förenklad ifyllning av blanketter för användare med dynamiska skriptfunktioner. Det gör att du kan skriva uttryck för att lägga till olika beteenden, till exempel dynamiska fält och paneler för att visa/dölja. Du kan också lägga till beräknade fält, skrivskydda fält, lägga till valideringslogik och mycket annat. Det dynamiska beteendet baseras på användarens indata eller förifyllda data.

JavaScript™ är uttrycksspråket i Adaptive Forms. Alla uttryck är giltiga JavaScript™-uttryck och använder API:er för adaptiv Forms-skriptmodell. Dessa uttryck returnerar värden av vissa typer. En fullständig lista över adaptiva Forms-klasser, händelser, objekt och offentliga API:er finns i [API-referens för JavaScript™-bibliotek för adaptiv Forms](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

## Bästa tillvägagångssätt för att skriva uttryck {#best-practices-for-writing-expressions}

* När du skriver uttryck kan du använda namnet på fältet eller panelen för att komma åt fält och paneler. Använd egenskapen value om du vill komma åt ett fälts värde. Exempel: `field1.value`
* Använd unika namn för fält och paneler i hela formuläret. Det hjälper till att undvika eventuella konflikter med fältnamn som används när uttryck skrivs.
* När du skriver flerradsuttryck kan du använda ett semikolon för att avsluta en -programsats.

## Metodtips för uttryck som innehåller en upprepande panel {#best-practices-for-expressions-involving-repeating-panel}

Upprepade paneler är instanser av en panel som läggs till eller tas bort dynamiskt med skript-API eller förifyllda data. <!--  For detailed information about using repeating panel, see [creating forms with repeatable sections](creating-forms-repeatable-sections.md). -->

* Om du vill skapa en upprepande panel öppnar du inställningarna i paneldialogrutan och anger värdet för fältet för högsta antal till mer än 1.
* Minsta antal för upprepade panelinställningar kan vara en eller flera, men det får inte vara fler än högsta antal.
* När ett uttryck refererar till ett fält med upprepande panel tolkas fältnamnen i uttrycket som det närmaste upprepade elementet.
* Adaptiv Forms har några specialfunktioner som förenklar beräkning av repeterbara paneler som summa, antal, min, max, filter och många andra. En fullständig lista över funktioner finns i [JavaScript™ Library API reference for Adaptive Forms](https://helpx.adobe.com/aem-forms/6/javascript-api/af.html)
* API:er för manipulering av instanser av upprepande panel är:

   * Så här lägger du till en panelinstans: `panel1.instanceManager.addInstance()`
   * Så här hämtar du en panel: `panel1.instanceIndex`
   * Så här hämtar du instanceManager för en panel: `_panel1 or panel1.instanceManager`
   * Så här tar du bort en instans av en panel: `_panel1.removeInstance(panel1.instanceIndex)`

## Uttryckstyper {#expression-types}

I Adaptiv Forms kan du skriva uttryck för att lägga till beteenden som dynamiska visa/dölj-fält och paneler. Du kan också skriva uttryck för att lägga till beräknade fält, skrivskydda fält, valideringslogik och mycket annat. Stöd för adaptiva Forms-uttryck:

* **[Åtkomstuttryck](#access-expression-enablement-expression)**: om du vill aktivera/inaktivera ett fält.
* **[Beräkna uttryck](#calculate-expression)**: för att beräkna ett fälts värde automatiskt.
* **[Klicka på uttryck](#click-expression)**: om du vill hantera åtgärder vid klickningshändelse för en knapp.
* **[Initieringsskript](#initialization-script):** utför en åtgärd vid initiering av ett fält.
* **[Alternativuttryck](#options-expression)**: om du vill fylla i en nedrullningsbar lista dynamiskt.
* **[Sammanfattningsuttryck](#summary)**: om du vill beräkna titeln för ett dragspelsuttryck dynamiskt.
* **[Validera uttryck](#validate-expression)**: för att validera ett fält.
* **[Värdet implementerar skript](#value-commit-script):** om du vill ändra komponenterna i ett formulär efter att värdet för ett fält har ändrats.
* **[Synlighetsuttryck](#visibility-expression)**: om du vill styra synligheten för ett fält och en panel.
* **[Uttryck för stegslutförande](#step-completion-expression)**: för att förhindra att en användare går vidare till nästa steg i en guide.

### Åtkomstuttryck (aktiveringsuttryck) {#access-expression-enablement-expression}

Du kan använda åtkomstuttrycket för att aktivera eller inaktivera ett fält. Om uttrycket använder ett fältvärde hämtas uttrycket när fältets värde ändras.

**Gäller för**: fält

**Returtyp**: Uttrycket returnerar ett booleskt värde som representerar om fältet är aktiverat eller inaktiverat. **true** representerar att fältet är aktiverat och **false** representerar att fältet är inaktiverat.

**Exempel**: Om du bara vill aktivera ett fält när värdet för **field1** är **X** är åtkomstuttrycket: `field1.value == "X"`

### Beräkna uttryck {#calculate-expression}

Beräkningsuttrycket används för att automatiskt beräkna värdet för ett fält med hjälp av ett uttryck. Vanligtvis används egenskapen value för andra fält i ett sådant uttryck. Exempel: `field2.value + field3.value`. När värdet för `field2` eller `field3` ändras, hämtas uttrycket och värdet beräknas om.

**Gäller för**: fält

**Returtyp**: Uttrycket returnerar ett värde som är kompatibelt med fältet där uttrycksresultatet visas (till exempel decimal).

**Exempel**: Det beräkningsuttryck som ska visa summan av två fält i **fält1** är:
`field2.value + field3.value`

### Klicka på uttryck {#click-expression}

Klickuttrycket hanterar de åtgärder som utförs på en knapps klickningshändelse. I GuideBridge finns API:er för att utföra olika funktioner som skicka, validera som används tillsammans med klickuttrycket. En fullständig lista över API:erna finns i [GuideBridge API:er](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

**Gäller för**: Knappfält

**Returtyp**: Klickuttrycket returnerar inget värde. Om något uttryck returnerar ett värde ignoreras värdet.

**Exempel**: Om du vill fylla i en textruta **textruta1** på klickåtgärden för en knapp med värdet **AEM Forms** är knappens klickuttryck `textbox1.value="AEM Forms"`

### Initieringsskript {#initialization-script}

Initieringsskriptet aktiveras när ett adaptivt formulär initieras. Beroende på scenarier fungerar initieringsskriptet på följande sätt:

* När ett adaptivt formulär återges utan förifyllning av data körs initieringsskriptet efter att formuläret har initierats.
* När ett adaptivt formulär återges med en dataförifyllning, körs skriptet när förifyllningen har slutförts.
* När serverbaserad omvalidering av ett adaptivt formulär utlöses körs initieringsskriptet.

**Gäller för:** fält och panel

**Returtyp:** Initieringsskriptuttrycket returnerar inget värde. Om något uttryck returnerar ett värde ignoreras värdet.

**Exempel:** I ett scenario där data förifylls och fält fylls med standardvärdet `'Adaptive Forms'` när deras värde sparas som null, är initieringsskriptuttrycket:
`if(this.value==null) this.value='Adaptive Forms';`

### Alternativuttryck {#options-expression}

Alternativuttrycket används för att dynamiskt fylla i alternativ för ett nedrullningsbart listfält.

**Gäller för**: nedrullningsbara listfält

**Returtyp**: Alternativuttrycket returnerar en array med strängvärden. Varje värde kan vara en enkel sträng, till exempel **Man**, eller i ett nyckel=värde-parsformat, till exempel **1=Man**

**Exempel**: Ange ett enkelt alternativuttryck om du vill fylla i ett fältvärde baserat på värdet i ett annat fält. Om du till exempel vill fylla i ett fält, **Antal barn**, baserat på den **civilstånd** som uttrycks i ett annat fält, är uttrycket:

**`marital_status.value == "married" ? ["1=One", "2=two"] : ["0=Zero"]`.**

När värdet för fältet **marital_status** ändras, hämtas uttrycket. Du kan också fylla i listrutan från en REST-tjänst. <!-- For detailed information, see [Dynamically populating dropdowns](dynamically-populate-dropdowns.md). -->

### Sammanfattningsuttryck {#summary}

Uttrycket Sammanfattning beräknar dynamiskt titeln på en underordnad panel i en dragspelslayoutpanel. Du kan ange uttrycket Sammanfattning i en regel som använder ett formulärfält eller en anpassad logik för att utvärdera titeln. Uttrycket körs när formuläret initieras. Om du förifyller ett formulär körs uttrycket efter att data har fyllts i i förväg eller när värdet för beroende fält som används i uttrycket ändras.

Sammanfattningsuttrycket används vanligtvis för att upprepa underordnade objekt i en dragspelslayoutpanel för att ge varje underordnad panel en meningsfull rubrik.

**Gäller för:** paneler som är direkt underordnade paneler för en panel vars layout är konfigurerad som dragspelspanel.

**Returtyp:** Uttrycket returnerar en sträng som blir dragspelets titel.

**Exempel:** &quot;Kontonummer: &quot; + texbox1.value

### Validera uttryck {#validate-expression}

Validate-uttrycket används för att validera fälten med det angivna uttrycket. Vanligtvis använder sådana uttryck reguljära uttryck tillsammans med fältvärdet för att validera ett fält. Uttrycket återställs och fältets valideringsstatus beräknas om vid en ändring av ett fälts värde.

**Gäller för**: fält

**Returtyp**: Uttrycket returnerar ett booleskt värde som representerar fältets valideringsstatus. Värdet **false** anger att fältet är ogiltigt och **true** anger att fältet är giltigt.
**Exempel**: För ett fält som representerar postnummer för Storbritannien är valideringsuttrycket:

(**this.value** &amp;&amp; `this.value.match(/^(GIR 0AA|[A-Z]{1,2}\d[A-Z0-9]? ?[0-9][A-Z]{2}\s*)$/i) == null) ? false : true`

I ovanstående exempel returnerar uttrycket **false** för att ange att fältet inte är giltigt om det icke-tomma värdet inte matchar mönstret.

>[!NOTE]
>
>Om du skriver ett valideringsuttryck för ett icke-obligatoriskt eller obligatoriskt fält utvärderas uttrycket oavsett fältets synlighetsstatus. Om du vill stoppa valideringen för de dolda fälten anger du egenskapen validationsDisabled i Initialization eller Value Commit Script till true. Exempel: `this.validationsDisabled=true`

### Värde för implementeringsskript {#value-commit-script}

Skriptet Värde implementeras aktiveras när:

* En användare ändrar värdet för ett fält från användargränssnittet.
* Värdet för ett fält ändras programmatiskt på grund av ändringar i ett annat fält.

**Gäller för:** fält

**Returtyp:** Värdeimplementeringsskriptuttrycket returnerar inget värde. Om något uttryck returnerar ett värde ignoreras värdet.

**Exempel:** Om du vill konvertera skiftläget för alfabet som anges i fältet till versaler vid implementering är värdet för implementeringsuttrycket:
`this.value=this.value.toUpperCase()`

>[!NOTE]
>
>Du kan inaktivera körningen av Value Commit Script när värdet för ett fält ändras programmatiskt. Gå till https://&#39;[server]:[port]/system/console/configMgr och ändra **Adaptiv Forms-version för kompatibilitet** till **AEM Forms 6.1** om du vill göra det. Därefter körs Value Commit Script bara när användaren ändrar fältets värde från användargränssnittet.

### Synlighetsuttryck {#visibility-expression}

Synlighetsuttrycket används för att styra synligheten för fält/panel. Synlighetsuttrycket använder vanligtvis värdeegenskapen för ett fält och hämtas när värdet ändras.

**Gäller för**: fält och panel

**Returtyp**: Uttrycket returnerar ett booleskt värde som representerar att fältet/panelen är synlig eller inte. **false** anger att fältet eller panelen inte är synlig och true anger att fältet eller panelen är synlig.

**Exempel**: För en panel som bara visas om värdet för **field1** är **Male** är synlighetsuttrycket: `field1.value == "Male"`

### Uttryck för slutförande av steg {#step-completion-expression}

Uttrycket för att slutföra steget används för att hindra en användare från att gå till nästa steg i en guidelayout. Dessa uttryck används när paneler har en guidelayout (ett flerstegsformulär som visar ett steg i taget). Användaren kan bara gå till nästa steg, panel eller underavsnitt om alla obligatoriska värden i det aktuella avsnittet är ifyllda och giltiga.

**Gäller för**: Paneler med objektets layout inställd på guide.

**Returtyp**: Uttrycket returnerar ett booleskt värde, som representerar den aktuella panelen, som är giltigt eller inte. **True** representerar att den aktuella panelen är giltig och att användaren kan navigera till nästa panel.

**Exempel**: I ett formulär som är organiserat på olika paneler valideras den aktuella panelen innan du går till nästa panel. I sådana fall används stegslutsuttryck. I allmänhet används validerings-API:t för GuideBridge. Ett exempel på uttryck för stegkomplettering är:
`window.guideBridge.validate([],this.panel.navigationContext.currentItem.somExpression)`

## Valideringar i adaptiv form {#validations-in-adaptive-form}

Det finns flera metoder för att lägga till fältvalidering i ett adaptivt formulär. Om en valideringskontroll läggs till i ett fält representerar **True** att det värde som anges i fältet är giltigt. **Falskt** representerar att värdet är ogiltigt. Om du tabbar in och ut ur ett fält genereras inget felmeddelande.

Du kan lägga till valideringar i ett fält på följande sätt:

### Obligatoriskt {#required}

Om du vill göra en komponent obligatorisk går du till dialogrutan **Redigera** för komponenten och väljer alternativet **Titel och text > Obligatorisk**. Du kan också lägga till ett meddelande (valfritt).

### Valideringsmönster {#validation-patterns}

Det finns flera valideringsmönster tillgängliga för ett fält. Om du vill välja ett valideringsmönster går du till avsnittet **Mönster** i dialogrutan **Redigera** för komponenten och väljer **Mönster**. Du kan skapa ett eget valideringsmönster i textrutan **Mönster**. Valideringsstatusen returneras **True** endast om de data som fylls i är kompatibla med valideringsmönstret, annars returneras **Falskt**. <!-- To write your own custom validation pattern, see [Picture clause support for HTML5 forms](picture-clause-support.md). -->

### Valideringsuttryck {#validation-expressions}

Valideringen av ett fält kan också beräknas med uttryck i olika fält. Uttrycken skrivs inuti fältet **Valideringsskript** på fliken **Skript** i dialogrutan **Redigera** för komponenten. Valideringsstatusen för ett fält beror på värdet som uttrycket returnerar. Mer information om hur du skriver sådana uttryck finns i [Validera uttryck](adaptive-form-expressions.md#p-validate-expression-p).

## Ytterligare information {#additional-information}

### Använda fältvisningsformat {#using-field-display-format}

Visningsformat kan användas för att visa data i olika format. Du kan till exempel använda visningsformatet för att visa ett telefonnummer med bindestreck, formatera postnummer eller datumväljare. Dessa visningsmönster kan väljas under **Mönster** i dialogrutan Redigera för en komponent. Du kan skriva anpassade visningsmönster som liknar de valideringsmönster som nämns ovan.

### GuideBridge - API:er och händelser {#guidebridge-apis-and-events}

GuideBridge är en samling API:er som kan användas för att interagera med Adaptiv Forms i en webbläsares minnesmodell. Detaljerad introduktion till Guide Bridge API, klassmetoder och exponerade händelser finns i [JavaScript™ Library API reference for Adaptive Forms](https://helpx.adobe.com/aem-forms/6/javascript-api/).

>[!NOTE]
>
>Du bör inte använda händelseavlyssnarna i GuideBridge i uttryck.

#### GuideBridge-användning i olika uttryck {#guidebridge-usage-in-various-expressions}

* Om du vill återställa formulärfält kan du aktivera `guideBridge.reset()`-API:t i klickuttrycket för en knapp. På samma sätt finns det ett API för att skicka som kan anropas som ett klickuttryck `guideBridge.submit()`**.**

* Du kan använda API:t `setFocus()` för att ange fokus i olika fält eller paneler (för panelfokus ställs det första fältet automatiskt in). `setFocus()`innehåller en mängd alternativ för navigering, till exempel navigering över paneler, föregående/nästa genomgång, inställning av fokus till ett visst fält och många andra alternativ. Om du till exempel vill gå till nästa panel kan du använda:`guideBridge.setFocus(this.panel.somExpression, &#39;nextItem&#39;).

* Använd `guideBridge.validate(errorList, somExpression).` om du vill validera ett adaptivt formulär eller dess specifika paneler

#### Använda GuideBridge utanför uttryck  {#using-guidebridge-outside-expressions-nbsp}

Du kan också använda API:erna för GuideBridge utanför uttrycken. Du kan till exempel använda API:t för GuideBridge för att ange kommunikation mellan HTML som är värd för det adaptiva formuläret och formulärmodellen. Dessutom kan du ange det värde som kommer från den överordnade delen av Iframe som är värd för formuläret.

Om du vill använda API:t för GuideBridge för ovanstående exempel hämtar du en instans av GuideBridge. Om du vill hämta instansen lyssnar du på `bridgeInitializeStart`händelsen för ett `window`objekt:

```javascript
window.addEventListener("bridgeInitializeStart", function(evnt) {

     // get hold of the guideBridge object

     var gb = evnt.detail.guideBridge;

     //wait for the completion of AF

     gb.connect(function (){

        //this function is called after Adaptive Form is initialized

     })

})
```

>[!NOTE]
>
>I AEM är det en god vana att skriva kod i en clientLib och inkludera den på din sida (header.jsp eller footer.jsp på sidan)

Om du vill använda GuideBridge när formuläret har initierats (händelsen `bridgeInitializeComplete` skickas) hämtar du GuideBridge-instansen med `window.guideBridge`. Du kan kontrollera initieringsstatusen för GuideBridge med API:t `guideBride.isConnected`.

#### GuideBridge Events {#guidebridge-events}

GuideBridge innehåller även vissa händelser för externa skript på värdsidan. Externa skript kan lyssna på dessa händelser och utföra olika åtgärder. När användarnamnet i ett formulär ändras, till exempel, ändras även namnet som visas i sidhuvudet på sidan. Mer information om sådana händelser finns i [JavaScript™ Library API reference for Adaptive Forms](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

Använd följande kod för att registrera hanterare:

```javascript
guideBridge.on("elementValueChanged", function (event, data)  {

      // execute some logic when value of a field is changed

});
```

### Skapa anpassade mönster för ett fält {#creating-custom-patterns-for-a-field}

Som nämnts ovan kan man med Adaptive Forms skapa mönster för validering och visning. Förutom att använda utanför rutmönstren kan du definiera återanvändbara anpassade mönster för en adaptiv formulärkomponent. Du kan till exempel definiera ett textfält eller ett numeriskt fält. När du har definierat det kan du använda de här mönstren i alla formulär för den angivna typen av komponent. Du kan till exempel skapa ett anpassat mönster för ett textfält och använda det i textfälten i deras adaptiva Forms. Du kan välja det anpassade mönstret genom att gå till mönsteravsnittet i redigeringsdialogrutan för en komponent. <!-- For details about Pattern definition or format, see [Picture clause support for HTML5 forms](picture-clause-support.md).-->

Utför följande steg för att skapa ett anpassat mönster för en viss fälttyp och återanvänd det för andra fält av samma typ:

1. Navigera till CRXDE Lite i redigeringsinstansen.
1. Skapa en mapp för att behålla dina anpassade mönster. Skapa en nod av typen sling:folder i katalogen /apps. Skapa till exempel en nod med namnet `customPatterns`. Skapa en annan nod av typen `nt:unstructed` under den här noden och ge den namnet `textboxpatterns`. Den här noden innehåller de olika anpassade mönster som du vill lägga till.
1. Öppna fliken Egenskaper för noden som skapades. Öppna till exempel fliken Egenskaper för `textboxpatterns`. Lägg till egenskapen `guideComponentType` i den här noden och ange dess värde till *fd/af/components/formter/guideTextBox*.

1. Värdet för den här egenskapen varierar beroende på vilket fält du vill definiera mönstren för. För numeriska fält är värdet för egenskapen `guideComponentType` *fd/af/components/formter/guideNumericBox*. Värdet för Datepicker-fältet är *fd/af/components/formter/guideDatepicker*.
&quot;
1. Du kan lägga till ett anpassat mönster genom att tilldela en egenskap till noden `textboxpatterns`. Lägg till en egenskap med ett namn (till exempel `pattern1`) och ställ in värdet på mönstret som du vill lägga till. Lägg till exempel till egenskapen `pattern1` med värdet Fax=text{99-999-9999999}. Mönstret är tillgängligt för alla textrutor som du använder i Adaptiv Forms.

   ![Skapa anpassade mönster för fält i CrxDe](assets/creating-custom-patterns.png)

   Skapa egna mönster

