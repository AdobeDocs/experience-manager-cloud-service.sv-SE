---
title: Hur använder man regelredigeraren för att lägga till regler i formulärfält för att lägga till dynamiskt beteende och skapa komplex logik i ett anpassat formulär?
description: Med den anpassningsbara regelredigeraren i Forms kan du lägga till dynamiskt beteende och bygga in komplex logik i formulär utan kodning eller skript.
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 6fd38e9e-435e-415f-83f6-3be177738c00
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '6526'
ht-degree: 0%

---

# Lägga till regler i ett adaptivt formulär {#adaptive-forms-rule-editor}

>[!NOTE]
>
> Adobe rekommenderar att du använder den moderna och utbyggbara datainhämtningen [Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) för [att skapa nya adaptiva Forms](/help/forms/creating-adaptive-form-core-components.md) eller [lägga till adaptiva Forms på AEM Sites-sidor](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter.

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service (Foundation Components) | Den här artikeln |
| AEM as a Cloud Service (kärnkomponenter) | [Klicka här](/help/forms/rule-editor-core-components.md) |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html) |

## Ökning {#overview}

Regelredigerarfunktionen ger formuläranvändare och utvecklare möjlighet att skriva regler på adaptiva formulärobjekt. Dessa regler definierar åtgärder som ska utlösas av formulärobjekt baserat på förinställda villkor, användarindata och användaråtgärder i formuläret. Det effektiviserar formulärifyllningen ytterligare och ger större precision och snabbhet.

Regelredigeraren har ett intuitivt och förenklat användargränssnitt för att skriva regler. Regelredigeraren erbjuder en visuell redigerare för alla användare.<!-- In addition, only for forms power users, rule editor provides a code editor to write rules and scripts. --> Några av de nyckelåtgärder du kan utföra på adaptiva formulärobjekt med regler är:

* Visa eller dölja ett objekt
* Aktivera eller inaktivera ett objekt
* Ange ett värde för ett objekt
* Validera ett objekts värde
* Utför funktioner för att beräkna värdet för ett objekt
* Anropa en tjänst för formulärdatamodell och utföra en åtgärd
* Ange ett objekts egenskap

<!-- Rule editor replaces the scripting capabilities in [!DNL Experience Manager 6.1 Forms] and earlier releases. However, your existing scripts are preserved in the new rule editor. For more information about working with existing scripts in the rule editor, see [Impact of rule editor on existing scripts](rule-editor.md#p-impact-of-rule-editor-on-existing-scripts-p). -->

Användare som läggs till i användargruppen för formulär kan skapa skript och redigera befintliga. Användare i gruppen [!DNL forms-users] kan använda skript men inte skapa eller redigera skript.

## Skillnad mellan regelredigerare i kärnkomponenter och Regelredigerare i Foundation Components

{{rule-editor-diff}}

## Förstå en regel {#understanding-a-rule}

En regel är en kombination av åtgärder och villkor. I regelredigeraren omfattar åtgärderna aktiviteter som att dölja, visa, aktivera, inaktivera eller beräkna värdet för ett objekt i ett formulär. Villkor är booleska uttryck som utvärderas genom att kontroller och åtgärder utförs på ett formulärobjekts status, värde eller egenskap. Åtgärder utförs baserat på det värde ( `True` eller `False`) som returneras när ett villkor utvärderas.

Regelredigeraren innehåller en uppsättning fördefinierade regeltyper, till exempel När, Visa, Dölj, Aktivera, Inaktivera, Ange värde för och Validera, som hjälper dig att skriva regler. Med varje regeltyp kan du definiera villkor och åtgärder i en regel. I dokumentet förklaras dessutom varje regeltyp i detalj.

En regel följer vanligtvis någon av följande konstruktioner:

**Condition-Action** I den här konstruktionen definierar en regel först ett villkor följt av en åtgärd som ska utlösas. Konstruktionen är jämförbar med if-then-programsatsen i programmeringsspråk.

Regeltypen **När** används i regelredigeraren för att framtvinga konstruktorn för villkorsåtgärd.

**Åtgärdsvillkor** I den här konstruktionen definierar en regel först en åtgärd som ska utlösas följt av villkor för utvärdering. En annan variant av den här konstruktionen är action-condition-alternate action, som också definierar en alternativ åtgärd som ska utlösas om villkoret returnerar False.

Regeltyperna Visa, Dölj, Aktivera, Inaktivera, Ange värde för och Validera i regelredigeraren framtvingar regelkonstruktionen för åtgärdsvillkor. Som standard är den alternativa åtgärden för Visa Dölj och Aktivera Inaktivera, och tvärtom. Du kan inte ändra den alternativa standardåtgärden.

>[!NOTE]
>
>De tillgängliga regeltyperna, inklusive villkor och åtgärder som du definierar i regelredigeraren, beror också på vilken typ av formulärobjekt du skapar en regel på. Regelredigeraren visar endast giltiga regeltyper och alternativ för att skriva villkor och åtgärdssatser för en viss formulärobjekttyp. Du kan till exempel inte se regeltyperna Validera, Ange värde för, Aktivera och Inaktivera för ett panelobjekt.

Mer information om tillgängliga regeltyper i regelredigeraren finns i [Tillgängliga regeltyper i regelredigeraren](rule-editor.md#p-available-rule-types-in-rule-editor-p).

### Riktlinjer för val av regelkonstruktion {#guidelines-for-choosing-a-rule-construct}

Även om du kan uppnå de flesta användningsexemplen genom att använda valfri regelkonstruktion finns det några riktlinjer för att välja en konstruktion framför en annan. Mer information om tillgängliga regler i regelredigeraren finns i [Tillgängliga regeltyper i regelredigeraren](rule-editor.md#p-available-rule-types-in-rule-editor-p).

* En typisk tumregel när du skapar en regel är att tänka på den i kontexten för det objekt som du skriver en regel för. Tänk på att du vill dölja eller visa fältet B baserat på det värde som användaren anger i fältet A. I det här fallet utvärderar du ett villkor i fält A och baserat på det värde som returneras utlöser du en åtgärd i fält B.

  Om du skriver en regel i fält B (det objekt som du utvärderar ett villkor för) ska du därför använda konstruktorn condition-action eller regeltypen When. Använd på samma sätt konstruktionen action-condition eller Visa eller Dölj regel i fält A.

* Ibland måste du utföra flera åtgärder baserat på ett villkor. I sådana fall bör du använda konstruktorn condition-action. I den här konstruktionen kan du utvärdera ett villkor en gång och ange flera åtgärdssatser.

  Om du till exempel vill dölja fält B, C och D baserat på villkoret som kontrollerar värdet som användaren anger i fält A, skriver du en regel med villkorsstyrd konstruktion eller Regeltyp för När i fält A och anger åtgärder som styr synligheten för fält B, C och D. I annat fall behöver du tre separata regler för fälten B, C och D, där varje regel kontrollerar villkoret och visar eller döljer respektive fält. I det här exemplet är det effektivare att skriva Regeltypen När för ett objekt i stället för att visa eller dölja regeltypen för tre objekt.

* Om du vill aktivera en åtgärd baserat på flera villkor bör du använda konstruktorn action-condition. Om du till exempel vill visa och dölja fält A genom att utvärdera villkor i fält B, C och D, använder du Visa eller Dölj regeltyp i fält A.
* Använd villkorskonstruktion för villkorsåtgärd eller åtgärd om regeln innehåller en åtgärd för ett villkor.
* Om en regel söker efter ett villkor och utför en åtgärd omedelbart när ett värde anges i ett fält eller när ett fält avslutas, rekommenderar vi att du skriver en regel med villkorsstyrd åtgärd eller med regeltypen När i fältet som villkoret utvärderas i.
* Villkoret i regeln När utvärderas när en användare ändrar värdet på objektet som regeln När används på. Men om du vill att åtgärden ska utlösas när värdet ändras på serversidan, till exempel för förifyllning av värdet, rekommenderar vi att du skriver en When-regel som utlöser åtgärden när fältet initieras.
* När du skriver regler för nedrullningsbara listor, alternativknappar eller kryssruteobjekt fylls alternativen eller värdena för dessa formulärobjekt i förväg i regelredigeraren.

## Tillgängliga operatortyper och händelser i regelredigeraren {#available-operator-types-and-events-in-rule-editor}

Regelredigeraren innehåller följande logiska operatorer och händelser som du kan använda för att skapa regler.

* **är lika med**
* **är inte lika med**
* **Börjar med**
* **Slutar med**
* **Innehåller**
* **är tom**
* **är inte tom**
* **Har markerat:** Returnerar true när användaren väljer ett visst alternativ för en kryssruta, nedrullningsbar alternativknapp.
* **Är initierad (händelse):** Returnerar true när ett formulärobjekt återges i webbläsaren.
* **Har ändrats (händelse):** Returnerar true när användaren ändrar det angivna värdet eller det valda alternativet för ett formulärobjekt.
* **Navigation(event):** Returnerar true när användaren klickar på ett navigeringsobjekt. Navigeringsobjekt används för att flytta mellan paneler.
* **Stegslutförande(händelse):** Returnerar true när ett steg i en regel slutförs.
* **Slutförd sändning(händelse):** Returnerar true när data har skickats till en formulärdatamodell.
* **Fel i överföring(händelse):** Returnerar true om data inte kunde skickas till en formulärdatamodell.

## Tillgängliga regeltyper i regelredigeraren {#available-rule-types-in-rule-editor}

Regelredigeraren innehåller en uppsättning fördefinierade regeltyper som du kan använda för att skriva regler. Vi tittar närmare på varje regeltyp. Mer information om hur du skriver regler i regelredigeraren finns i [Skriv regler](rule-editor.md#p-write-rules-p).

### [!UICONTROL When] {#whenruletype}

Regeltypen **[!UICONTROL When]** följer regelkonstruktionen **condition-action-alternate action** eller ibland bara **condition-action** -konstruktionen. I den här regeltypen anger du först ett villkor för utvärdering följt av en åtgärd som ska utlösas om villkoret är uppfyllt ( `True`). När du använder regeltypen When kan du använda flera AND- och OR-operatorer för att skapa [kapslade uttryck](#nestedexpressions).

Med regeltypen När kan du utvärdera ett villkor i ett formulärobjekt och utföra åtgärder på ett eller flera objekt.

Med enkla ord är en vanlig When-regel strukturerad enligt följande:

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

Åtgärd 2 på objekt B.
OCH
Åtgärd 3 om objekt C.

_

När du har en komponent med flera värden, till exempel alternativknappar eller listor, hämtas alternativen automatiskt och görs tillgängliga för regelskaparen när du skapar en regel för den komponenten. Du behöver inte ange alternativvärdena igen.

En lista har till exempel fyra alternativ: Röd, Blå, Grön och Gul. När regeln skapas hämtas alternativen (alternativknappar) automatiskt och görs tillgängliga för regelskaparen enligt följande:

![Flera värden visar alternativ](assets/multivaluefcdisplaysoptions1.png)

När du skriver en When-regel kan du utlösa åtgärden Clear Value Of. Med åtgärden Clear Value Of rensas det angivna objektets värde. Med alternativet Radera värde för i programsatsen When kan du skapa komplexa villkor med flera fält.

![Rensa värdet för ](assets/clearvalueof1.png)

**[!UICONTROL Hide]** Döljer det angivna objektet.

**[!UICONTROL Show]** Visar det angivna objektet.

**[!UICONTROL Enable]** Aktiverar det angivna objektet.

**[!UICONTROL Disable]** Inaktiverar det angivna objektet.

**[!UICONTROL Invoke service]** Anropar en tjänst som konfigurerats i en formulärdatamodell (FDM). När du väljer åtgärden Anropa tjänst visas ett fält. När användaren knackar på fältet visas alla tjänster som konfigurerats i alla formulärdatamodeller (FDM) på [!DNL Experience Manager]-instansen. När du väljer en FDM-tjänst (Form Data Model) visas fler fält där du kan mappa formulärobjekt med in- och utdataparametrar för den angivna tjänsten. Se exempelregel för anrop av Form Data Model-tjänster.

Utöver Form Data Model-tjänsten kan du ange en direkt WSDL-URL för att anropa en webbtjänst. En Form Data Model-tjänst har dock många fördelar och det rekommenderade sättet att anropa en tjänst.

Mer information om hur du konfigurerar tjänster i formulärdatamodellen (FDM) finns i [[!DNL Experience Manager Forms] Dataintegrering](data-integration.md).

**[!UICONTROL Set value of]** Beräknar och ställer in värdet för det angivna objektet. Du kan ställa in objektvärdet på en sträng, värdet för ett annat objekt, det beräknade värdet med hjälp av matematiska uttryck eller funktioner, värdet för ett objekts egenskap eller utdatavärdet från en konfigurerad Form Data Model-tjänst. När du väljer webbtjänstalternativet visas alla tjänster som konfigurerats i alla formulärdatamodeller (FDM) på [!DNL Experience Manager]-instansen. När du väljer en tjänst för formulärdatamodell visas fler fält där du kan mappa formulärobjekt med in- och utdataparametrar för den angivna tjänsten.

Mer information om hur du konfigurerar tjänster i formulärdatamodellen (FDM) finns i [[!DNL Experience Manager Forms] Dataintegrering](data-integration.md).

Regeltypen **[!UICONTROL Set Property]** gör att du kan ange värdet för en egenskap för det angivna objektet baserat på en villkorsåtgärd. Du kan ställa in egenskapen på något av följande:
* visible (Boolean)
* dorExclusion (Boolean)
* chartType (String)
* title (String)
* enabled (Boolean)
* mandatory (Boolean)
* validationsDisabled (Boolean)
* validateExpMessage (String)
* value (Number, String, Date)
* objekt (lista)
* valid (Boolean)
* errorMessage (String)

Du kan till exempel definiera regler för att lägga till kryssrutor dynamiskt i det adaptiva formuläret. Du kan använda en anpassad funktion, ett formulärobjekt eller en objektegenskap för att definiera en regel.

![Ange egenskap](assets/set_property_rule_new1.png)

Om du vill definiera en regel baserat på en anpassad funktion väljer du **[!UICONTROL Function Output]** i listrutan och drar och släpper en anpassad funktion på fliken **[!UICONTROL Functions]**. Om villkorsåtgärden uppfylls läggs antalet kryssrutor som definierats i den anpassade funktionen till i det adaptiva formuläret.

Om du vill definiera en regel baserat på ett formulärobjekt väljer du **[!UICONTROL Form Object]** i listrutan och drar och släpper ett formulärobjekt på fliken **[!UICONTROL Form Objects]**. Om villkorsåtgärden uppfylls läggs antalet kryssrutor som är definierade i formulärobjektet till i det adaptiva formuläret.

Med en regel för att ange egenskap som baseras på en objektegenskap kan du lägga till antalet kryssrutor i ett adaptivt formulär baserat på en annan objektegenskap som ingår i det adaptiva formuläret.

I följande bild visas ett exempel på hur du dynamiskt lägger till kryssrutor baserat på antalet nedrullningsbara listor i det adaptiva formuläret:

![Objektegenskap](assets/object_property_set_property_new1.png)

**[!UICONTROL Clear Value Of]** Tar bort det angivna objektets värde.

**[!UICONTROL Set Focus]** anger fokus på det angivna objektet.

**[!UICONTROL Save Form]** Sparar formuläret.

**[!UICONTROL Submit Forms]** skickar formuläret.

**[!UICONTROL Reset Form]** Återställer formuläret.

**[!UICONTROL Validate Form]** Validerar formuläret.

**[!UICONTROL Add Instance]** lägger till en instans av den angivna repeterbara panelen eller tabellraden.

**[!UICONTROL Remove Instance]** Tar bort en instans av den angivna repeterbara panelen eller tabellraden.

**[!UICONTROL Navigate to]** Navigerar till annan <!--Interactive Communications,--> Adaptiv Forms, andra resurser som bilder eller dokumentfragment eller en extern URL. <!-- For more information, see [Add button to the Interactive Communication](create-interactive-communication.md#addbuttontothewebchannel). -->

### [!UICONTROL Set Value of] {#set-value-of}

Med regeltypen **[!UICONTROL Set Value of]** kan du ange värdet för ett formulärobjekt beroende på om det angivna villkoret är uppfyllt eller inte. Värdet kan anges till ett värde för ett annat objekt, en stränglitteral, ett värde som härleds från ett matematiskt uttryck eller en funktion, ett värde för en egenskap för ett annat objekt eller utdata från en Form Data Model-tjänst. På samma sätt kan du söka efter ett villkor för en komponent, en sträng, en egenskap eller värden som härletts från en funktion eller ett matematiskt uttryck.

Regeltypen **Ange värdet för** är inte tillgänglig för alla formulärobjekt, till exempel paneler och knappar i verktygsfält. En standarduppsättningsvärde för regel har följande struktur:

Ange värdet för objekt A till:

(sträng ABC) OR
(objektegenskap X för objekt C) OR
(värde från en funktion) OR
(värde från ett matematiskt uttryck) OR
(datavärdet för en datamodelltjänst eller webbtjänst),

När (valfritt):

(Villkor 1 OCH villkor 2 OCH villkor 3) är SANT.

I följande exempel används värdet i fältet `dependentid` som indata och värdet i fältet `Relation` anges som utdata för argumentet `Relation` i tjänsten `getDependent` Form Data Model.

![Set-value-web-service](assets/set-value-web-service1.png)

Exempel på Ange värderegel med tjänsten Formulärdatamodell

>[!NOTE]
>
>Dessutom kan du använda Ange värde för regel för att fylla i alla värden i en nedrullningsbar listkomponent från utdata från en formulärdatamodelltjänst eller en webbtjänst. Se dock till att det utdataargument du väljer är av en arraytyp. Alla värden som returneras i en array blir tillgängliga i den angivna listrutan.

### [!UICONTROL Show] {#show}

Med regeltypen **[!UICONTROL Show]** kan du skriva en regel som visar eller döljer ett formulärobjekt baserat på om ett villkor är uppfyllt eller inte. Regeltypen Visa utlöser även åtgärden Dölj om villkoret inte uppfylls eller returnerar `False`.

En vanlig Visa-regel är strukturerad på följande sätt:

`Show Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Hide Object A;`

### [!UICONTROL Hide] {#hide}

På liknande sätt som med regeltypen Visa kan du använda regeltypen **[!UICONTROL Hide]** för att visa eller dölja ett formulärobjekt baserat på om ett villkor är uppfyllt eller inte. Dölj regeltyp utlöser även åtgärden Visa om villkoret inte uppfylls eller returnerar `False`.

En vanlig Dölj-regel är strukturerad på följande sätt:

`Hide Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Show Object A;`

### [!UICONTROL Enable] {#enable}

Regeltypen **[!UICONTROL Enable]** gör att du kan aktivera eller inaktivera ett formulärobjekt baserat på om ett villkor är uppfyllt eller inte. Regeltypen Aktivera utlöser även åtgärden Inaktivera om villkoret inte uppfylls eller returnerar `False`.

En vanlig Aktivera-regel är strukturerad på följande sätt:

`Enable Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Disable Object A;`

### [!UICONTROL Disable] {#disable}

På liknande sätt som för typen Aktivera regel kan du med regeltypen **[!UICONTROL Disable]** aktivera eller inaktivera ett formulärobjekt baserat på om ett villkor är uppfyllt eller inte. Regeltypen Inaktivera utlöser också åtgärden Aktivera om villkoret inte uppfylls eller returnerar `False`.

En vanlig inaktiveringsregel är strukturerad på följande sätt:

`Disable Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Enable Object A;`

### [!UICONTROL Validate] {#validate}

Regeltypen **[!UICONTROL Validate]** validerar värdet i ett fält med hjälp av ett uttryck. Du kan till exempel skriva ett uttryck för att kontrollera att textrutan för att ange namn inte innehåller specialtecken eller siffror.

En vanlig valideringsregel är strukturerad enligt följande:

`Validate Object A;`

`Using:`

`(Expression 1 AND Expression 2 AND Expression 3) is TRUE;`

>[!NOTE]
>
>Om det angivna värdet inte överensstämmer med regeln Validera kan du visa ett valideringsmeddelande för användaren. Du kan ange meddelandet i fältet **[!UICONTROL Script validation message]** i komponentegenskaperna i sidofältet.

![Skriptvalidering](assets/script-validation.png)

### [!UICONTROL Set Options Of] {#setoptionsof}

Regeltypen **[!UICONTROL Set Options Of]** gör att du kan definiera regler för att lägga till kryssrutor dynamiskt i det anpassade formuläret. Du kan använda en formulärdatamodell (FDM) eller en anpassad funktion för att definiera regeln.

Om du vill definiera en regel baserat på en anpassad funktion väljer du **[!UICONTROL Function Output]** i listrutan och drar och släpper en anpassad funktion på fliken **[!UICONTROL Functions]**. Antalet kryssrutor som definieras i den anpassade funktionen läggs till i det adaptiva formuläret.

![Anpassade funktioner](assets/custom_functions_set_options_new.png)

Mer information om hur du skapar en anpassad funktion finns i [anpassade funktioner i regelredigeraren](#custom-functions).

Så här definierar du en regel baserad på en formulärdatamodell (FDM):

1. Välj **[!UICONTROL Service Output]** i listrutan.
1. Markera datamodellsobjektet.
1. Välj en objektegenskap för datamodell i listrutan **[!UICONTROL Display Value]**. Antalet kryssrutor i det adaptiva formuläret härleds från antalet instanser som definierats för den egenskapen i databasen.
1. Välj en objektegenskap för datamodell i listrutan **[!UICONTROL Save Value]**.

![Alternativ för FDM-uppsättning](assets/fdm_set_options_new.png)

## Förstå användargränssnittet för regelredigeraren {#understanding-the-rule-editor-user-interface}

Regelredigeraren har ett omfattande men ändå enkelt användargränssnitt för att skriva och hantera regler. Du kan starta regelredigerarens användargränssnitt i ett adaptivt formulär i redigeringsläge.

Så här startar du användargränssnittet för regelredigeraren:

1. Öppna ett adaptivt formulär i redigeringsläge.
1. Markera det formulärobjekt som du vill skriva en regel för och välj ![edit-rules](assets/edit-rules-icon.svg) i komponentverktygsfältet. Användargränssnittet för regelredigeraren visas.

   ![create-rules](assets/create-rules1.png)

   Alla befintliga regler för de markerade formulärobjekten visas i den här vyn. Mer information om hur du hanterar befintliga regler finns i [Hantera regler](rule-editor.md#p-manage-rules-p).

1. Välj **[!UICONTROL Create]** om du vill skriva en ny regel. Den visuella redigeraren för regelredigerarens användargränssnitt öppnas som standard när du startar regelredigeraren första gången.

   ![Regelredigerarens gränssnitt](assets/rule-editor-ui1.png)

Vi tittar närmare på varje komponent i regelredigeringsgränssnittet.

### A. Visning av komponentregel {#a-component-rule-display}

Visar titeln på det adaptiva formulärobjektet genom vilket du startade regelredigeraren och den regeltyp som är vald. I ovanstående exempel startas regelredigeraren från ett anpassat formulärobjekt med namnet Lön och den valda regeltypen är När.

### B. Formulärobjekt och -funktioner {#b-form-objects-and-functions-br}

Panelen till vänster i regelredigerarens användargränssnitt innehåller två flikar - **[!UICONTROL Forms Objects]** och **[!UICONTROL Functions]**.

På fliken Formulärobjekt visas en hierarkisk vy över alla objekt som finns i det adaptiva formuläret. Där visas objektens namn och typ. När du skriver en regel kan du dra och släppa formulärobjekt till regelredigeraren. När du skapar eller redigerar en regel när du drar och släpper ett objekt eller en funktion till en platshållare, får platshållaren automatiskt rätt värdetyp.

De formulärobjekt som har en eller flera giltiga regler markerade med en grön punkt. Om någon av reglerna som tillämpas på ett formulärobjekt är ogiltig markeras formulärobjektet med en gul punkt.

Fliken Funktioner innehåller en uppsättning inbyggda funktioner, till exempel summan av, Min av, Max av, Medel av, Antal, och Validera formulär. Du kan använda de här funktionerna för att beräkna värden i repeterbara paneler och tabellrader och använda dem i action- och condition-satser när du skriver regler. Du kan dock även skapa [anpassade funktioner](#custom-functions).

![Fliken Funktioner](assets/functions1.png)

>[!NOTE]
>
>Du kan utföra textsökning på objekt och funktionsnamn och titlar på flikarna Forms Objekt och Funktioner.

I det vänstra trädet för formulärobjekten kan du markera de formulärobjekt som ska visa de regler som tillämpas på vart och ett av objekten. Du kan inte bara navigera bland reglerna för de olika formulärobjekten, du kan även kopiera och klistra in regler mellan formulärobjekten. Mer information finns i [Kopiera och klistra in regler](rule-editor.md#p-copy-paste-rules-p).

### C. Växla mellan formulärobjekt och funktioner {#c-form-objects-and-functions-toggle-br}

När användaren knackar på knappen växlar knappen formulärobjekt och funktionsruta.

### D. Visuell regelredigerare {#visual-rule-editor}

Visuell regelredigerare är det område i det visuella redigeringsläget i regelredigerarens användargränssnitt där du skriver regler. Här kan du välja en regeltyp och definiera villkor och åtgärder. När du definierar villkor och åtgärder i en regel kan du dra och släppa formulärobjekt och funktioner från rutan Formulärobjekt och funktioner.

Mer information om hur du använder den visuella regelredigeraren finns i [Skriva regler](rule-editor.md#p-write-rules-p).
<!-- 
### E. Visual-code editors switcher {#e-visual-code-editors-switcher}

Users in the forms-power-users group can access code editor. For other users, code editor is not available. If you have the rights, you can switch from visual editor mode to code editor mode of the rule editor, and conversely, using the switcher right above the rule editor. When you launch rule editor the first time, it opens in the visual editor mode. You can write rules in the visual editor mode or switch to the code editor mode to write a rule script. However, note that if you modify a rule or write a rule in code editor, you cannot switch back to the visual editor for that rule unless you clear the code editor.

[!DNL Experience Manager Forms] tracks the rule editor mode you used last to write a rule. When you launch the rule editor next time, it opens in that mode. However, you can also configure a default mode to open the rule editor in the specified mode. To do so:

1. Go to [!DNL Experience Manager] web console at `https://[host]:[port]/system/console/configMgr`.
1. Click to edit **[!UICONTROL Adaptive Form Configuration Service]**.
1. choose **[!UICONTROL Visual Editor]** or **[!UICONTROL Code Editor]** from the **[!UICONTROL Default Mode for Rule Editor]** drop-down

1. Click **[!UICONTROL Save]**.
-->

### E. Knapparna Klar och Avbryt {#done-and-cancel-buttons}

Knappen **[!UICONTROL Done]** används för att spara en regel. Du kan spara en ofullständig regel. Ofullständiga är dock ogiltiga och kan inte köras. Sparade regler för ett formulärobjekt visas nästa gång du startar regelredigeraren från samma formulärobjekt. Du kan hantera befintliga regler i den vyn. Mer information finns i [Hantera regler](rule-editor.md#p-manage-rules-p).

Knappen **[!UICONTROL Cancel]** ignorerar alla ändringar du har gjort i en regel och stänger regelredigeraren.

## Skriv regler {#write-rules}

Du kan skriva regler med den visuella regelredigeraren &lt;!— eller kodredigeraren>. När du startar regelredigeraren första gången öppnas den i det visuella redigeringsläget. Du kan växla till kodredigeringsläget och skriva regler. Om du däremot skriver eller ändrar en regel i kodredigeraren kan du inte växla till den visuella redigeraren för den regeln om du inte rensar kodredigeraren. När du startar regelredigeraren nästa gång öppnas den i det läge som du använde när du skapade regeln senast.

Låt oss först titta på hur man skriver regler med visuell redigerare.

### Använda den visuella redigeraren {#using-visual-editor}

Låt oss förstå hur du skapar en regel i den visuella redigeraren med hjälp av följande exempelformulär.

![Create-rule-example](assets/create-rule-example.png)

I avsnittet Krav för lån i exempelformuläret för låneansökan måste de sökande ange sin äktenskapsstatus, lön och, om de är gifta, sin makas lön. Baserat på användarens indata beräknar regeln beloppet för rätt till lån och visas i fältet Låneberättigande. Använd följande regler för att implementera scenariot:

* Fältet för makens lön visas endast när äktenskapsstatus är gift.
* Låneberättigandebeloppet är 50 % av den totala lönen.

Så här skriver du regler:

1. Först skriver du regeln för att styra synligheten för fältet för makslön baserat på det alternativ som användaren väljer för alternativknappen för civilstånd.

   Öppna låneansökningsformuläret i redigeringsläge. Markera komponenten **[!UICONTROL Marital Status]** och välj ![edit-rules](assets/edit-rules-icon.svg). Välj sedan **[!UICONTROL Create]** för att starta regelredigeraren.

   ![write-rules-visual-editor-1](assets/write-rules-visual-editor-1.png)

   När du startar regelredigeraren markeras regeln När som standard. Dessutom anges formulärobjektet (i det här fallet Marital status) från vilket du startade regelredigeraren i programsatsen When.

   Du kan inte ändra eller ändra det markerade objektet, men du kan välja en annan regeltyp med hjälp av den nedrullningsbara menyn. Om du vill skapa en regel för ett annat objekt väljer du Avbryt om du vill avsluta regelredigeraren och starta den igen från det önskade formulärobjektet.

1. Välj listrutan **[!UICONTROL Select State]** och välj **[!UICONTROL is equal to]**. Fältet **[!UICONTROL Enter a String]** visas.

   ![write-rules-visual-editor-2](assets/write-rules-visual-editor-2.png)

   I alternativknappen Marital status tilldelas **[!UICONTROL Married]**- och **[!UICONTROL Single]**-alternativen ****- respektive ****-värden. Du kan verifiera tilldelade värden på fliken Titel i dialogrutan Redigera som visas nedan.

   ![Värden för alternativknappar från regelredigeraren](assets/radio-button-values.png)

1. Ange **[!UICONTROL Enter a String]** 0 **i fältet** i regeln.

   ![write-rules-visual-editor-4](assets/write-rules-visual-editor-4.png)

   Du har definierat villkoret som `When Marital Status is equal to Married`. Definiera sedan åtgärden som ska utföras om villkoret är sant.

1. Välj **[!UICONTROL Show]** i listrutan **[!UICONTROL Select Action]** i programsatsen then.

   ![write-rules-visual-editor-5](assets/write-rules-visual-editor-5.png)

1. Dra och släpp fältet **[!UICONTROL Spouse Salary]** från fliken Formulärobjekt i fältet **[!UICONTROL Drop object or select here]**. Du kan också markera fältet **[!UICONTROL Drop object or select here]** och välja fältet **[!UICONTROL Spouse Salary]** på snabbmenyn, där alla formulärobjekt i formuläret listas.

   ![write-rules-visual-editor-6](assets/write-rules-visual-editor-6.png)

   Regeln visas så här i regelredigeraren.

   ![write-rules-visual-editor-7](assets/write-rules-visual-editor-7.png)

1. Välj **[!UICONTROL Done]** om du vill spara regeln.

1. Upprepa steg 1 till 5 om du vill definiera en annan regel som döljer fältet för makens lön om äktenskapsstatus är Enskild. Regeln visas så här i regelredigeraren.

   ![write-rules-visual-editor-8](assets/write-rules-visual-editor-8.png)

   >[!NOTE]
   >
   >Du kan också skriva en Show-regel i fältet för makarnas lön, i stället för två When-regler i fältet för civilstånd, för att implementera samma beteende.

   ![write-rules-visual-editor-9](assets/write-rules-visual-editor-9.png)

1. Skriv sedan en regel för att beräkna lånebeloppet, som är 50 % av den totala lönen, och visa det i fältet Låneberättigande. För att uppnå det här resultatet skapar du **[!UICONTROL Set value Of]** regler för fältet Lånekvalificering.

   I redigeringsläget markerar du fältet **[!UICONTROL Loan Eligibility]** och väljer ![edit-rules](assets/edit-rules-icon.svg). Välj sedan **[!UICONTROL Create]** för att starta regelredigeraren.

1. Välj **[!UICONTROL Set Value Of]**-regel i listrutan Regel.

   ![write-rules-visual-editor-10](assets/write-rules-visual-editor-10.png)

1. Välj **[!UICONTROL Select Option]** och välj **[!UICONTROL Mathematical Expression]**. Ett fält som skriver matematiskt uttryck öppnas.

   ![write-rules-visual-editor-11](assets/write-rules-visual-editor-11.png)

1. I uttrycksfältet:

   * Markera eller dra och släpp fältet **[!UICONTROL Salary]** i det första **[!UICONTROL Drop object or select here]**-fältet på fliken Forms-objekt.

   * Välj **[!UICONTROL Plus]** i fältet **[!UICONTROL Select Operator]**.

   * Markera eller dra och släpp fältet **[!UICONTROL Spouse Salary]** i det andra **[!UICONTROL Drop object or select here]**-fältet på fliken Forms-objekt.

   ![write-rules-visual-editor-12](assets/write-rules-visual-editor-12.png)

1. Välj sedan **[!UICONTROL Extend Expression]** i det markerade området runt uttrycksfältet.

   ![write-rules-visual-editor-13](assets/write-rules-visual-editor-13.png)

   I fältet för utökat uttryck väljer du **[!UICONTROL divided by]** i fältet **[!UICONTROL Select Operator]** och **[!UICONTROL Number]** i fältet **[!UICONTROL Select Option]**. Ange sedan **[!UICONTROL 2]** i nummerfältet.

   ![write-rules-visual-editor-14](assets/write-rules-visual-editor-14.png)

   >[!NOTE]
   >
   >Du kan skapa komplexa uttryck med hjälp av komponenter, funktioner, matematiska uttryck och egenskapsvärden i fältet Välj alternativ.

   Skapa sedan ett villkor som körs när true returneras.

1. Välj **[!UICONTROL Add Condition]** om du vill lägga till en When-sats.

   ![write-rules-visual-editor-15](assets/write-rules-visual-editor-15.png)

   I programsatsen When:

   * Markera eller dra och släpp fältet **[!UICONTROL Marital Status]** i det första **[!UICONTROL Drop object or select here]**-fältet på fliken Forms-objekt.

   * Välj **[!UICONTROL is equal to]** i fältet **[!UICONTROL Select Operator]**.

   * Välj String i det andra **[!UICONTROL Drop object or select here]**-fältet och ange **[!UICONTROL Married]** i **[!UICONTROL Enter a String]**-fältet.

   Regeln visas slutligen så här i regelredigeraren.  ![write-rules-visual-editor-16](assets/write-rules-visual-editor-16.png)

1. Välj **[!UICONTROL Done]**. Den sparar regeln.

1. Upprepa steg 7 till 14 för att definiera en annan regel som beräknar låneberättigandet om civilstånd är enkel. Regeln visas så här i regelredigeraren.

   ![write-rules-visual-editor-17](assets/write-rules-visual-editor-17.png)

>[!NOTE]
>
>Du kan också använda regeln Ange värde för för för att beräkna låneberättigandet i regeln När som du skapade för att visa och dölja fältet Makslön. Den resulterande kombinerade regeln när Marital status är enkel visas så här i regelredigeraren.
>
>På samma sätt kan du skriva en kombinerad regel för att kontrollera synligheten för fältet för makars lön och beräkna rätten till lån när civilstånd är gifta.

![write-rules-visual-editor-18](assets/write-rules-visual-editor-18.png)

<!-- ### Using code editor {#using-code-editor}

Users added to the forms-power-users group can use code editor. The rule editor auto generates the JavaScript code for any rule you create using visual editor. You can switch from visual editor to the code editor to view the generated code. However, if you modify the rule code in the code editor, you cannot switch back to the visual editor. If you prefer writing rules in code editor rather than visual editor, you can write rules afresh in the code editor. The visual-code editors switcher helps you switch between the two modes.

The code editor JavaScript is the expression language of Adaptive Forms. All the expressions are valid JavaScript expressions and use Adaptive Forms scripting model APIs. These expressions return values of certain types. For the complete list of Adaptive Forms classes, events, objects, and public APIs, see [JavaScript Library API reference for Adaptive Forms](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

For more information about guidelines to write rules in the code editor, see [Adaptive Form Expressions](adaptive-form-expressions.md).

While writing JavaScript code in the rule editor, the following visual cues help you with the structure and syntax:

* Syntax highlights

* Auto Indentation

* Hints and suggestions for Form objects, functions, and their properties

* Auto completion of form component names and common JavaScript functions

![javascriptruleeditor](assets/javascriptruleeditor.png)
-->

#### Anpassade funktioner i regelredigeraren {#custom-functions}

Förutom användningsklara funktioner som *Summan av* som listas under Funktioner Output, kan du skriva anpassade funktioner som du ofta behöver. Kontrollera att den funktion du skriver åtföljs av `jsdoc` ovan.

Ytterligare `jsdoc` krävs:

* Om du vill ha anpassad konfiguration och beskrivning
* Eftersom det finns flera sätt att deklarera en funktion i `JavaScript,` och kommentarer kan du hålla reda på funktionerna.

Regelredigeraren stöder JavaScript ES5-syntax för skript och anpassade funktioner.
Mer information finns i [jsdoc.app](https://jsdoc.app/).

`jsdoc` taggar som stöds:

* **Privat**
Syntax: `@private`
En privat funktion ingår inte som en anpassad funktion.

* **Namn**
Syntax: `@name funcName <Function Name>`
Du kan också `,` använda: `@function funcName <Function Name>` **eller** `@func` `funcName <Function Name>` .
  `funcName` är namnet på funktionen (inga blanksteg tillåts).
  `<Function Name>` är funktionens visningsnamn.

* **Medlem**
Syntax: `@memberof namespace`
Kopplar ett namnutrymme till funktionen.

* **Parameter**
Syntax: `@param {type} name <Parameter Description>`
Du kan också använda: `@argument` `{type} name <Parameter Description>` **eller** `@arg` `{type}` `name <Parameter Description>` .
Visar parametrar som används av funktionen. En funktion kan ha flera parametertaggar, en tagg för varje parameter i ordningen för förekomst.
  `{type}` representerar parametertyp. Tillåtna parametertyper är:

   1. string
   1. tal
   1. boolesk
   1. omfång

  Omfattningen avser fält i ett adaptivt formulär. När ett formulär använder lazy loading kan du använda `scope` för att komma åt dess fält. Du kan komma åt fält antingen när fälten har lästs in eller om fälten har markerats som globala.

  Alla parametertyper kategoriseras under något av ovanstående. Ingen stöds inte. Välj en av typerna ovan. Typer är inte skiftlägeskänsliga. Blanksteg tillåts inte i parametern `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **Returtyp**
Syntax: `@return {type}`
Du kan också använda `@returns {type}` .
Lägger till information om funktionen, till exempel dess mål.
  {type} representerar funktionens returtyp. Följande returtyper tillåts:

   1. string
   1. tal
   1. boolesk

  Alla andra returtyper kategoriseras under en av ovanstående. Ingen stöds inte. Välj en av typerna ovan. Returtyperna är inte skiftlägeskänsliga.

   * **Detta**
Syntax: `@this currentComponent`

  Använd @this för att referera till den adaptiva formulärkomponenten som regeln är skriven för.

  Följande exempel baseras på fältvärdet. I följande exempel döljer regeln ett fält i formuläret. Delen `this` i `this.value` refererar till den underliggande adaptiva formulärkomponenten, som regeln är skriven för.

  ```
     /**
     * @function myTestFunction
     * @this currentComponent
     * @param {scope} scope in which code inside function is run.
     */
     myTestFunction = function (scope) {
        if(this.value == "O"){
              scope.age.visible = true;
        } else {
           scope.age.visible = false;
        }
     }
  ```

  >[!NOTE]
  >
  >Kommentarer före anpassade funktioner används för sammanfattning. Sammanfattningen kan sträcka sig över flera rader tills en tagg påträffas. Begränsa storleken till en enda storlek om du vill ha en kortfattad beskrivning i regelbyggaren.

**Lägger till en anpassad funktion**

Du kan t.ex. lägga till en egen funktion som beräknar en kvadratyta. Sidlängd är användarens indata till den anpassade funktionen, som accepteras med en numerisk ruta i formuläret. Beräknade utdata visas i en annan numerisk ruta i formuläret. Om du vill lägga till en anpassad funktion måste du först skapa ett klientbibliotek och sedan lägga till det i CRX-databasen.

Så här skapar du ett klientbibliotek och lägger till det i CRX-databasen:

1. Skapa ett klientbibliotek. Mer information finns i [Använda klientbibliotek](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).
1. I CRXDE lägger du till egenskapen `categories` med strängtypsvärdet `customfunction` i mappen `clientlib`.

   >[!NOTE]
   >
   >`customfunction` är en exempelkategori. Du kan välja vilket namn som helst för kategorin som du skapar i mappen `clientlib`.

När du har lagt till ditt klientbibliotek i CRX-databasen kan du använda det i ditt adaptiva formulär. Du kan använda den anpassade funktionen som en regel i formuläret. Så här lägger du till klientbiblioteket i ditt adaptiva formulär:

1. Öppna formuläret i redigeringsläge.
Om du vill öppna ett formulär i redigeringsläge markerar du ett formulär och väljer **[!UICONTROL Open]**.
1. I redigeringsläget markerar du en komponent, väljer ![fältnivå](assets/select_parent_icon.svg) > **[!UICONTROL Adaptive Form Container]** och sedan ![cmpr](assets/configure-icon.svg).
1. Lägg till ditt klientbibliotek i sidofältet under Klientbibliotekets namn. ( `customfunction` i exemplet.)

   ![Lägger till klientbiblioteket för anpassade funktioner](assets/clientlib.png)

1. Markera den numeriska rutan och välj ![edit-rules](assets/edit-rules-icon.svg) för att öppna regelredigeraren.
1. Välj **[!UICONTROL Create Rule]**. Använd alternativen som visas nedan för att skapa en regel som sparar indatavärdet i fyrkantiga värden i formulärutdatafältet.

   [![Använda anpassade funktioner för att skapa en regel](assets/add_custom_rule_new.png)](assets/add-custom-rule.png)

1. Välj **[!UICONTROL Done]**. Din anpassade funktion har lagts till.

   >[!NOTE]
   >
   > Om du vill anropa en formulärdatamodell (FDM) från regelredigeraren med anpassade funktioner [går du hit](/help/forms/using-form-data-model.md#invoke-services-in-adaptive-forms-using-rules-invoke-services).

#### Typer som stöds för funktionsdeklaration {#function-declaration-supported-types}

**Funktionssats**

```javascript
function area(len) {
    return len*len;
}
```

Den här funktionen ingår utan `jsdoc` kommentarer.

**Funktionsuttryck**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Funktionsuttryck och programsats**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Funktionsdeklaration som variabel**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Begränsning: den anpassade funktionen väljer bara den första funktionsdeklarationen från variabellistan, om den används tillsammans. Du kan använda funktionsuttryck för varje deklarerad funktion.

**Funktionsdeklaration som objekt**

```javascript
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```

>[!NOTE]
>
>Se till att du använder `jsdoc` för alla anpassade funktioner. Även om `jsdoc` kommentarer uppmuntras bör du inkludera en tom `jsdoc`-kommentar för att markera funktionen som anpassad funktion. Den aktiverar standardhantering av din anpassade funktion.

### Stöd för anpassade funktioner i valideringsuttryck {#supporting-custom-functions-in-validation-expressions-br}

Om det finns **komplexa valideringsregler** finns ibland det exakta valideringsskriptet i anpassade funktioner och författaren anropar dessa anpassade funktioner från fältvalideringsuttryck. Om du vill att det här anpassade funktionsbiblioteket ska vara känt och tillgängligt när du utför validering på serversidan kan formulärförfattaren konfigurera namnet på AEM klientbibliotek på fliken **[!UICONTROL Basic]** i egenskaper för adaptiv formulärbehållare enligt nedan.

![Stöd för anpassade funktioner i valideringsuttryck](assets/clientlib-cat.png)

Stöd för anpassade funktioner i valideringsuttryck

Författaren kan konfigurera customJavaScript-bibliotek per adaptiv form. I biblioteket behåller du bara återanvändbara funktioner som är beroende av jquery- och underscore.js-bibliotek från tredje part.

## Felhantering vid Skicka-åtgärd {#error-handling-on-submit-action}

Konfigurera anpassade felsidor som 400.jsp, 404.jsp och 500.jsp som en del av AEM riktlinjer för säkerhet och skärpning. Dessa hanterare anropas när ett formulär 400-, 404- eller 500-fel skickas. Hanterarna anropas också när dessa felkoder aktiveras på noden Publicera. Du kan också skapa JSP-sidor för andra HTTP-felkoder.

När du förifyller en formulärdatamodell (FDM), eller schemabaserad adaptiv form med XML- eller JSON-dataklagomål till ett schema som inte innehåller `<afData>` -, `<afBoundData>` - och `</afUnboundData>` -taggar, förloras data i obegränsade fält i det adaptiva formuläret. Schemat kan vara ett XML-schema, ett JSON-schema eller en FDM (Form Data Model). Obegränsade fält är adaptiva formulärfält utan egenskapen `bindref`.

## Hantera regler {#manage-rules}

Alla befintliga regler för ett formulärobjekt visas när du markerar objektet och väljer ![edit-rules1](assets/edit-rules-icon.svg). Du kan visa titeln och förhandsgranska regelsammanfattningen. I användargränssnittet kan du dessutom expandera och visa hela regelsammanfattningen, ändra ordningen på regler, redigera regler och ta bort regler.

![Listregler](assets/list-rules.png)

Du kan utföra följande åtgärder på regler:

* **Utöka/komprimera**: Innehållskolumnen i regellistan visar regelinnehållet. Om hela regelinnehållet inte visas i standardvyn kan du expandera innehållet ![expand-rule-content](assets/Smock_ChevronDown.svg) genom att markera det.

* **Ändra ordning**: Alla nya regler som du skapar staplas längst ned i regellistan. Reglerna körs uppifrån och ned. Regeln längst upp körs först följt av andra regler av samma typ. Om du till exempel har reglerna When, Show, Enable och When vid första, andra, tredje respektive fjärde positionen uppifrån, kommer regeln When överst att köras först följt av regeln When vid den fjärde positionen. Sedan körs reglerna Visa och Aktivera.
Du kan ändra ordningen på en regel genom att trycka på ![sorteringsregler](assets/sort-rules.svg) mot den eller dra och släppa den i önskad ordning i listan.

* **Redigera**: Om du vill redigera en regel markerar du kryssrutan bredvid regeltiteln. Alternativ för att redigera och ta bort regeln visas. Välj **[!UICONTROL Edit]** om du vill öppna den valda regeln i regelredigeraren <!-- in visual  or code editor mode depending on the mode used to create the rule -->.

* **Ta bort**: Om du vill ta bort en regel markerar du regeln och väljer **[!UICONTROL Delete]**.

* **Aktivera/inaktivera**: När du tillfälligt måste inaktivera användningen av en regel kan du välja en eller flera regler och välja **[!UICONTROL Disable]** i verktygsfältet Åtgärder för att inaktivera dem. Om en regel är inaktiverad körs den inte vid körningen. Om du vill aktivera en inaktiverad regel kan du markera den och välja Aktivera i verktygsfältet Åtgärder. Statuskolumnen för regeln visar om regeln är aktiverad eller inaktiverad.

![Inaktivera regel](assets/disablerule.png)

## Kopiera och klistra in regler {#copy-paste-rules}

Du kan kopiera och klistra in en regel från ett fält till andra liknande fält för att spara tid.

Så här kopierar och klistrar du in regler:

1. Markera det formulärobjekt som du vill kopiera en regel från och välj ![Redigera regel](assets/edit-rules-icon.svg) i komponentverktygsfältet. Användargränssnittet för regelredigeraren visas med formulärobjektet markerat och de befintliga reglerna visas.

   ![kopieringsregel](assets/copyrule.png)

   Mer information om hur du hanterar befintliga regler finns i [Hantera regler](rule-editor.md#p-manage-rules-p).

1. Markera kryssrutan bredvid regeltiteln. Då visas alternativ för att hantera regeln. Välj **[!UICONTROL Copy]**.

   ![copyright2](assets/copyrule2.png)

1. Markera ett annat formulärobjekt som du vill klistra in regeln i och välj **[!UICONTROL Paste]**. Dessutom kan du redigera regeln för att göra ändringar i den.

   >[!NOTE]
   >
   >Du kan bara klistra in en regel i ett annat formulärobjekt om det formulärobjektet har stöd för den kopierade regelns händelse. En knapp stöder till exempel händelsen click. Du kan klistra in en regel med en klickningshändelse på en knapp, men inte i en kryssruta.

1. Välj **[!UICONTROL Done]** om du vill spara regeln.

## Kapslade uttryck {#nestedexpressions}

Med regelredigeraren kan du använda flera AND- och OR-operatorer för att skapa kapslade regler. Du kan blanda flera AND- och OR-operatorer i regler.

Nedan visas ett exempel på en kapslad regel som visar ett meddelande till användaren om rätt att vårdas av ett barn när de obligatoriska villkoren är uppfyllda.

![Komplext uttryck](assets/complexexpression.png)

Du kan också redigera genom att dra och släppa villkor i en regel. Markera och hovra över handtaget ( ![handle](assets/drag-handle.svg)) före ett villkor. När pekaren ändras till en handsymbol enligt nedan drar och släpper du villkoret någonstans i linjen. Regelstrukturen ändras.

![Dra och släpp](assets/drag-and-drop.png)

## Villkor för datumuttryck {#dateexpression}

Med regelredigeraren kan du använda datumjämförelser för att skapa villkor.

Följande är ett exempelvillkor som visar ett statiskt textobjekt om inteckningen på huset redan har tagits, vilket användaren anger genom att fylla i datumfältet.

När datumet för inteckningen av egendomen som fyllts i av användaren har inträffat visas en anteckning om inkomstberäkningen i det adaptiva formuläret. I följande regel jämförs det datum som användaren fyller i med det aktuella datumet och om det datum som användaren fyller i är tidigare än det aktuella datumet visas textmeddelandet (Inkommande) i formuläret.

![Datumuttrycksvillkor](assets/dateexpressioncondition.png)

När det ifyllda datumet infaller tidigare än det aktuella datumet visas textmeddelandet (intäkt) enligt följande:

![Datumuttrycksvillkoret uppfyllt](assets/dateexpressionconditionmet.png)

## Nummerjämförelsevillkor {#number-comparison-conditions}

Med regelredigeraren kan du skapa villkor som jämför två tal.

Följande är ett exempelvillkor som visar ett statiskt textobjekt om antalet månader en sökande stannar på den aktuella adressen är mindre än 36.

![Villkor för nummerjämförelse](assets/numbercomparisoncondition.png)

När användaren anger att han/hon bor på den aktuella bostadsadressen i mindre än 36 månader visas ett meddelande i formuläret om att det går att begära fler bosättningsbevis.

![Fler bevis har begärts](assets/additionalproofrequested.png)

<!-- ## Impact of rule editor on existing scripts {#impact-of-rule-editor-on-existing-scripts}

In [!DNL Experience Manager Forms] versions prior to [!DNL Experience Manager 6.1 Forms] feature pack 1, form authors and developers used to write expressions in the Scripts tab of the Edit component dialog to add dynamic behavior to Adaptive Forms. The Scripts tab is now replaced by the rule editor.

Any scripts or expressions that you must have written in the Scripts tab are available in the rule editor. While you cannot view or edit them in visual editor, if you are a part of the forms-power-users group you can edit scripts in code editor. -->

## Exempelregler {#example}

### Anropa tjänsten Formulärdatamodell {#invoke}

Överväg en webbtjänst `GetInterestRates` som tar lånebelopp, löptid och sökandens kreditpoäng som indata och returnerar en låneplan som inkluderar EMI-belopp och ränta. Du skapar en formulärdatamodell (FDM) med webbtjänsten som datakälla. Du lägger till datamodellsobjekt och en `get`-tjänst i formulärmodellen. Tjänsten visas på fliken Tjänster i formulärdatamodellen (FDM). Skapa sedan ett adaptivt formulär som innehåller fält från datamodellsobjekt för att samla in användarindata för lånebelopp, löptid och kreditpoäng. Lägg till en knapp som utlöser webbtjänsten för att hämta planinformation. Utdata fylls i i lämpliga fält.

Följande regel visar hur du konfigurerar åtgärden Anropa tjänst för att slutföra exempelscenariot.

![Exempel-invoke-services](assets/example-invoke-services.png)

>[!NOTE]
>
>Om indata är av arraytyp visas fälten som stöder arrayer i den nedrullningsbara utdatafältet.

### Utlösa flera åtgärder med hjälp av regeln När {#triggering-multiple-actions-using-the-when-rule}

I en låneansökan vill du ta reda på om lånesökanden är en befintlig kund eller inte. Baserat på den information som användaren anger, bör fältet för kund-ID visas eller döljas. Du vill också fokusera på fältet för kund-ID om användaren är en befintlig kund. Formuläret för låneansökan innehåller följande komponenter:

* En alternativknapp, **[!UICONTROL Are you an existing Geometrixx customer?]**, som innehåller alternativ för [!UICONTROL Yes] och [!UICONTROL No]. Värdet för Ja är **0** och Nej är **1**.

* Ett textfält, **[!UICONTROL Geometrixx customer ID]**, som anger kund-ID:t.

När du skriver en When-regel på alternativknappen för att implementera det här beteendet, visas regeln på följande sätt i den visuella regelredigeraren.

![When-rule-example](assets/when-rule-example.png)

Regel i den visuella redigeraren

I exempelregeln är programsatsen i avsnittet När villkoret, som när returnerar True, utför de åtgärder som anges i avsnittet Sedan.

<!-- The rule appears as follows in the code editor.

![when-rule-example-code](assets/when-rule-example-code.png) 

Rule in the code editor -->

### Använda ett funktionsutdata i en regel {#using-a-function-output-in-a-rule}

I ett inköpsorderformulär har du följande tabell där användarna fyller i sina order. I denna tabell:

* Den första raden är upprepningsbar, så användarna kan beställa flera produkter och ange olika kvantiteter. Dess elementnamn är `Row1`.
* Titeln på cellen i kolumnen Produktkvantitet på den repeterbara raden är Kvantitet. Elementnamnet för cellen är `productquantity`.
* Den andra raden i tabellen är inte repeterbar och cellens rubrik i kolumnen Produktkvantitet i den här raden är Total Quantity.

![Example-function-table](assets/example-function-table.png)

**A.** Rad1 **B.** Kvantitet **C.** Totalt antal

Nu vill du lägga till angivna kvantiteter i kolumnen Produktkvantitet för alla produkter och visa summan i cellen Total kvantitet. Du kan uppnå den här summan genom att skriva en Set Value Of-regel i cellen Total Quantity enligt nedan.

![Example-function-output](assets/example-function-output.png)

Regel i den visuella redigeraren

<!-- he rule appears as follows in the code editor.

![example-function-output-code](assets/example-function-output-code.png)

Rule in the code editor -->

### Validera ett fältvärde med uttryck {#validating-a-field-value-using-expression}

I inköpsorderformuläret som förklaras i föregående exempel vill du hindra användare från att beställa mer än en kvantitet av en produkt till ett pris som överstiger 10000. Du kan skriva en valideringsregel enligt nedan.

![Exempel-validate](assets/example-validate.png)

Regel i den visuella redigeraren

<!-- The rule appears as follows in the code editor.

![example-validate-code](assets/example-validate-code.png)

Rule in the code editor -->