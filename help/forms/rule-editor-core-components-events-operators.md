---
title: Vilka operatortyper och händelser finns tillgängliga i regelredigeraren för ett adaptivt formulär baserat på kärnkomponenterna?
description: Anpassad regelredigerare för Forms stöder olika operatortyper och händelser.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
source-git-commit: 780c68f0c21ef94ff6a73ce991370100b1a88db9
workflow-type: tm+mt
source-wordcount: '1860'
ht-degree: 0%

---


# Operatortyper och händelser i regelredigeraren för ett adaptivt formulär baserat på kärnkomponenter

I AEM Forms som moln innehåller regelredigeraren olika typer av operatorer och händelser som gör att du enkelt kan definiera och utföra komplexa villkor och åtgärder.

Operatortyperna som är tillgängliga i regelredigeraren för ett adaptivt formulär ger ett robust ramverk för att skapa exakta villkor. De gör det möjligt för er att hantera data, utföra beräkningar och kombinera olika villkor på ett logiskt och sammanhängande sätt. Oavsett om du jämför värden, utför aritmetiska operationer eller manipulerar strängar ser de här operatorerna till att reglerna är både flexibla och kraftfulla.

Händelser i regelredigeraren fungerar som utlösare som aktiverar reglerna. De definierar de specifika åtgärder som inträffar när vissa villkor uppfylls. Genom att utnyttja olika typer av händelser kan du automatisera svar på en mängd olika scenarier, till exempel användarinteraktioner, schemalagda tider, dataändringar och systemtillstånd. Med möjlighet att ange dessa utlösare kan du skapa dynamiska och responsiva regler som uppfyller dina specifika krav.

Genom att förstå och använda tillgängliga operatortyper och händelser kan du utnyttja regelredigerarens fulla potential, som gör att du kan skapa effektiva regler som uppfyller dina unika behov och förbättra den övergripande systemfunktionaliteten.

## Tillgängliga operatortyper och händelser i regelredigeraren {#available-operator-types-and-events-in-rule-editor}

Regelredigeraren innehåller följande logiska operatorer och händelser som du kan använda för att skapa regler.

* **är lika med**
* **är inte lika med**
* **Börjar med**
* **Slutar med**
* **Innehåller**
* **Innehåller inte**
* **är tom**
* **är inte tom**
* **Har markerat:** Returnerar true när användaren väljer ett visst alternativ för en kryssruta, nedrullningsbar alternativknapp.
* **Är initierad (händelse):** Returnerar true när ett formulärobjekt återges i webbläsaren.
* **Har ändrats (händelse):** Returnerar true när användaren ändrar det angivna värdet eller det valda alternativet för ett formulärobjekt.

<!--
* **Navigation(event):** Returns true when the user clicks a navigation object. Navigation objects are used to move between panels. 
* **Step Completion(event):** Returns true when a step of a rule completes.
* **Successful Submission(event):** Returns true on successful submission of data to a form data model.
* **Error in Submission(event):**  Returns true on unsuccessful submission of data to a form data model. -->

### Tillgängliga regeltyper i regelredigeraren {#available-rule-types-in-rule-editor}

Regelredigeraren innehåller en uppsättning fördefinierade regeltyper som du kan använda för att skriva regler. Vi tittar närmare på varje regeltyp. Mer information om hur du skriver regler i regelredigeraren finns i [Skriv regler](/help/forms/rule-editor-core-components-user-interface.md#write-rules).

#### [!UICONTROL When] {#whenruletype}

Regeltypen **[!UICONTROL When]** följer regelkonstruktionen **condition-action-alternate action** eller ibland bara **condition-action** -konstruktionen. I den här regeltypen anger du först ett villkor för utvärdering följt av en åtgärd som ska utlösas om villkoret är uppfyllt ( `True`). När du använder regeltypen When kan du använda flera AND- och OR-operatorer för att skapa [kapslade uttryck](/help/forms/rule-editor-core-components-usecases.md#nested-expressions).

Med regeltypen När kan du utvärdera ett villkor i ett formulärobjekt och utföra åtgärder på ett eller flera objekt.

Med enkla ord är en vanlig When-regel strukturerad enligt följande:

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

`Action 2 on Object B;`
`AND`
`Åtgärd 3 på objekt C;

`Else, do the following:`

`Action 2 on Object C;`
_

När du har en komponent med flera värden, till exempel alternativknappar eller en lista, hämtas alternativen automatiskt och görs tillgängliga för regelskaparen när du skapar en regel för den komponenten. Du behöver inte skriva in alternativvärdena igen.

En lista har till exempel fyra alternativ: Röd, Blå, Grön och Gul. När du skapar regeln hämtas alternativen (alternativknapparna) automatiskt och görs tillgängliga för regelskaparen enligt följande:

![Visningsalternativ för flera värden](assets/multivaluefcdisplaysoptions.png)

När du skriver en When-regel kan du utlösa åtgärden Clear Value Of. Med åtgärden Clear Value Of rensas det angivna objektets värde. Med alternativet Radera värde för i programsatsen When kan du skapa komplexa villkor med flera fält. Du kan lägga till Else-satsen för att lägga till ytterligare villkor

![Tydligt värde för](assets/clearvalueof.png)

>[!NOTE]
>
> När regeltypen endast stöder then-else-instruktioner på en nivå.

##### Tillåtna Flera fält i [!UICONTROL When] {#allowed-multiple-fields}

I villkoret **När** kan du välja att lägga till andra fält förutom det fält som regeln tillämpas på.

Med regeltypen När kan du till exempel utvärdera ett villkor för olika formulärobjekt och utföra åtgärden:

När:

(Objekt A Villkor 1)

OCH/ELLER

(Objekt B, villkor 2)

Gör sedan följande:

Åtgärd 1 på objekt A

_

![Tillåtna flera fält i När](/help/forms/assets/allowed-multiple-field-when.png)

**Att tänka på när du använder funktionen Tillåtna flera fält i When-villkorsfunktionen**

* Se till att kärnkomponenten är inställd på [version 3.0.14 eller senare](https://github.com/adobe/aem-core-forms-components) för att använda den här funktionen i regelredigeraren.
* Om regler tillämpas på olika fält i villkoret När utlöses regeln även om endast ett av dessa fält ändras.


<!--
* It is not possible to add multiple fields in the When condition while applying rules to a button.

##### To enable Allowed Multiple fields in When condition feature

Allowed Multiple fields in When condition feature is disabled by default. To enable this feature, add a custom property at the template policy:

1. Open the corresponding template associated with an Adaptive Form in the template editor.
1. Select the existing policy as **formcontainer-policy**.
1. Navigate to the **[!UICONTROL Structure]**  view and, from the **[!UICONTROL Allowed Components]** list, open the **[!UICONTROL Adaptive Forms Container]** policy.
1. Go to the **[!UICONTROL Custom Properties]** tab and to add a custom property, click **[!UICONTROL Add]**.
1. Specify the **Group Name** of your choice. For example, in our case, we added the group name as **allowedfeature**.
1. Add the **key** and **value** pair as follows:
   * key: fd:changeEventBehaviour
   * value: deps
1. Click **[!UICONTROL Done]**. -->

Om det uppstår problem i de tillåtna fälten i villkorsfunktionen följer du felsökningsstegen enligt följande:

1. Öppna formuläret i redigeringsläge.
1. Öppna innehållsläsaren och markera komponenten **[!UICONTROL Guide Container]** i det adaptiva formuläret.
1. Klicka på ikonen för egenskaper för stödlinjebehållaren ![Egenskaper för stödlinje](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas.
1. Klicka på Klar och spara dialogrutan igen.

**[!UICONTROL Hide]** Döljer det angivna objektet.

**[!UICONTROL Show]** Visar det angivna objektet.

**[!UICONTROL Enable]** Aktiverar det angivna objektet.

**[!UICONTROL Disable]** Inaktiverar det angivna objektet.

**[!UICONTROL Invoke service]** Anropar en tjänst som konfigurerats i en formulärdatamodell (FDM). När du väljer åtgärden Anropa tjänst visas ett fält. När användaren knackar på fältet visas alla tjänster som konfigurerats i alla formulärdatamodeller (FDM) på [!DNL Experience Manager]-instansen. När du väljer en tjänst för formulärdatamodell visas fler fält där du kan mappa formulärobjekt med in- och utdataparametrar för den angivna tjänsten. Se exempelregeln för anrop av FDM-tjänster (Form Data Model).

Utöver tjänsten Form Data Model kan du ange en direkt WSDL-URL för att anropa en webbtjänst. En Form Data Model-tjänst har dock många fördelar och det rekommenderade sättet att anropa en tjänst.

Mer information om hur du konfigurerar tjänster i formulärdatamodellen (FDM) finns i [[!DNL Experience Manager Forms] Dataintegrering](data-integration.md).

**[!UICONTROL Set value of]** Beräknar och ställer in värdet för det angivna objektet. Du kan ange objektvärdet som en sträng, värdet för ett annat objekt, det beräknade värdet med hjälp av ett matematiskt uttryck eller en matematisk funktion, värdet för en objektegenskap eller utdatavärdet från en konfigurerad Form Data Model-tjänst. När du väljer webbtjänstalternativet visas alla tjänster som konfigurerats i alla formulärdatamodeller (FDM) på [!DNL Experience Manager]-instansen. När du väljer en tjänst för formulärdatamodell visas fler fält där du kan mappa formulärobjekt med in- och utdataparametrar för den angivna tjänsten.

Mer information om hur du konfigurerar tjänster i formulärdatamodellen (FDM) finns i [[!DNL Experience Manager Forms] Dataintegrering](data-integration.md).

Regeltypen **[!UICONTROL Set Property]** gör att du kan ange värdet för en egenskap för det angivna objektet baserat på en villkorsåtgärd. Du kan ställa in egenskapen på något av följande:
* visible (Boolean)
* label.value (String)
* label.visible (Boolean)
* description (String)
* enabled (Boolean)
* readOnly (Boolean)
* required (Boolean)
* screenReaderText (String)
* valid (Boolean)
* errorMessage (String)
* default (Number, String, Date)
* enumNames (String[])
* chartType (String)

Du kan till exempel definiera regler som visar textrutan när någon klickar på en knapp. Du kan använda en anpassad funktion, ett formulärobjekt, en objektegenskap eller en tjänstutdata för att definiera en regel.

![Ange egenskap](assets/set_property_rule_new.png)

Om du vill definiera en regel baserat på en anpassad funktion väljer du **[!UICONTROL Function Output]** i listrutan och drar och släpper en anpassad funktion på fliken **[!UICONTROL Functions]**. Om villkorsåtgärden uppfylls visas textrutan.

Om du vill definiera en regel baserat på ett formulärobjekt väljer du **[!UICONTROL Form Object]** i listrutan och drar och släpper ett formulärobjekt på fliken **[!UICONTROL Form Objects]**. Om villkorsåtgärden uppfylls visas textinmatningsrutan i det adaptiva formuläret.

Med en Set Property-regel som baseras på en objektegenskap kan du göra textinmatningsrutan synlig i ett adaptivt formulär baserat på en annan objektegenskap som ingår i det adaptiva formuläret.

I följande bild visas ett exempel på hur kryssrutan dynamiskt aktiveras baserat på att en textruta döljs eller visas i ett adaptivt formulär:

![Objekt, egenskap](assets/object_property_set_property_new.png)

**[!UICONTROL Clear Value Of]** Rensar värdet för det angivna objektet.

**[!UICONTROL Set Focus]** anger fokus på det angivna objektet.

**[!UICONTROL Submit Form]** skickar formuläret.

**[!UICONTROL Reset]** Återställer formuläret eller det angivna objektet.

**[!UICONTROL Validate]** Validerar formuläret eller det angivna objektet.

**[!UICONTROL Add Instance]** lägger till en instans av den angivna repeterbara panelen eller tabellraden.

**[!UICONTROL Remove Instance]** Tar bort en instans av den angivna repeterbara panelen eller tabellraden.

**[!UICONTROL Function Output]** definierar en regel baserat på fördefinierade funktioner eller anpassade funktioner.

**[!UICONTROL Navigate to]** Navigera till andra adaptiva Forms, andra resurser som bilder eller dokumentfragment eller en extern URL. <!-- For more information, see [Add button to the Interactive Communication](create-interactive-communication.md#addbuttontothewebchannel). -->

**[!UICONTROL Dispatch Event]** utlöser specifika åtgärder eller beteenden baserat på fördefinierade villkor eller händelser.

#### [!UICONTROL Set Value of] {#set-value-of}

Med regeltypen **[!UICONTROL Set Value of]** kan du ange värdet för ett formulärobjekt beroende på om det angivna villkoret är uppfyllt eller inte. Värdet kan anges till ett värde för ett annat objekt, en stränglitteral, ett värde som härleds från ett matematiskt uttryck eller en funktion, ett värde för en egenskap för ett annat objekt eller utdata från en Form Data Model-tjänst. På samma sätt kan du söka efter ett villkor för en komponent, en sträng, en egenskap eller värden som härletts från en funktion eller ett matematiskt uttryck.

Regeltypen **Ange värdet för** är inte tillgänglig för alla formulärobjekt, till exempel paneler och knappar i verktygsfält. En standardregel för uppsättningsvärde för har följande struktur:

Ange värdet för objekt A till:

(sträng ABC) ELLER
(objektegenskap X för objekt C) ELLER
(värde från en funktion) ELLER
(värde från ett matematiskt uttryck) ELLER
(utdatavärde för en datamodelltjänst);

När (valfritt):

(Villkor 1 OCH Villkor 2 OCH Villkor 3) är SANT;

I följande exempel väljs värdet för `Question2` som `True` och värdet för `Result` anges som `correct`.

![Set-value-web-service](assets/set-value-web-service.png)

Exempel på Ange värderegel med tjänsten Formulärdatamodell.

#### [!UICONTROL Show] {#show}

Med regeltypen **[!UICONTROL Show]** kan du skriva en regel som visar eller döljer ett formulärobjekt baserat på om ett villkor är uppfyllt eller inte. Regeltypen Visa utlöser även åtgärden Dölj om villkoret inte uppfylls eller returnerar `False`.

En vanlig Visa-regel är strukturerad på följande sätt:

`Show Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Hide Object A;`

#### [!UICONTROL Hide] {#hide}

På samma sätt som med regeltypen Visa kan du använda regeltypen **[!UICONTROL Hide]** för att visa eller dölja ett formulärobjekt baserat på om ett villkor är uppfyllt eller inte. Dölj regeltyp utlöser även åtgärden Visa om villkoret inte uppfylls eller returnerar `False`.

En vanlig Dölj-regel är strukturerad på följande sätt:

`Hide Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Show Object A;`

#### [!UICONTROL Enable] {#enable}

Regeltypen **[!UICONTROL Enable]** gör att du kan aktivera eller inaktivera ett formulärobjekt baserat på om ett villkor är uppfyllt eller inte. Regeltypen Aktivera utlöser även åtgärden Inaktivera om villkoret inte uppfylls eller returnerar `False`.

En vanlig Aktivera-regel är strukturerad på följande sätt:

`Enable Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Disable Object A;`

#### [!UICONTROL Disable] {#disable}

På liknande sätt som för typen Aktivera regel kan du med regeltypen **[!UICONTROL Disable]** aktivera eller inaktivera ett formulärobjekt baserat på om ett villkor är uppfyllt eller inte. Regeltypen Inaktivera utlöser också åtgärden Aktivera om villkoret inte uppfylls eller returnerar `False`.

En vanlig inaktiveringsregel är strukturerad på följande sätt:

`Disable Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Enable Object A;`

#### [!UICONTROL Validate] {#validate}

Regeltypen **[!UICONTROL Validate]** validerar värdet i ett fält med hjälp av ett uttryck. Du kan till exempel skriva ett uttryck för att kontrollera att textrutan som anger ett namn inte innehåller specialtecken eller siffror.

En vanlig valideringsregel är strukturerad enligt följande:

`Validate Object A;`

`Using:`

`(Expression 1 AND Expression 2 AND Expression 3) is TRUE;`

>[!NOTE]
>
>Om det angivna värdet inte överensstämmer med regeln Validera kan du visa ett valideringsmeddelande för användaren. Du kan ange meddelandet i fältet **[!UICONTROL Script validation message]** i komponentegenskaperna i sidofältet.

![Skriptvalidering](assets/script-validation.png)

<!--
### [!UICONTROL Set Options Of] {#setoptionsof}

The **[!UICONTROL Set Options Of]** rule type enables you to define rules to add check boxes dynamically to the Adaptive Form. You can use a Form Data Model or a custom function to define the rule.

To define a rule based on a custom function, select **[!UICONTROL Function Output]** from the drop-down list, and drag-and-drop a custom function from the **[!UICONTROL Functions]** tab. The number of checkboxes defined in the custom function are added to the Adaptive Form.

![Custom Functions](assets/custom_functions_set_options_new.png)

To create a custom function, see [custom functions in rule editor](#custom-functions).

To define a rule based on a form data model:

1. Select **[!UICONTROL Service Output]** from the drop-down list.
1. Select the data model object.
1. Select a data model object property from the **[!UICONTROL Display Value]** drop-down list. The number of checkboxes in the Adaptive Form is derived from the number of instances defined for that property in the database.
1. Select a data model object property from the **[!UICONTROL Save Value]** drop-down list.

![FDM set options](assets/fdm_set_options_new.png) -->

## Nästa steg

Låt oss nu förstå olika [exempel för en regelredigerare för ett anpassat formulär baserat på kärnkomponenter](/help/forms/rule-editor-core-components-usecases.md).

## Se även

{{see-also-rule-editor}}