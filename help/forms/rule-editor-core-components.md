---
title: Hur använder man regelredigeraren för att lägga till regler i formulärfält för att lägga till dynamiskt beteende och bygga komplex logik i ett adaptivt formulär baserat på kärnkomponenterna?
description: Med den anpassningsbara regelredigeraren i Forms kan du lägga till dynamiskt beteende och bygga in komplex logik i formulär utan kodning eller skript.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 1292f729-c6eb-4e1b-b84c-c66c89dc53ae
source-git-commit: 8585ec309b04e04b9a8dcaa43063369d1c9d5d24
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 0%

---


# Introduktion till regelredigeraren för adaptiva formulär baserade på kärnkomponenter

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service (kärnkomponenter) | Den här artikeln |
| AEM as a Cloud Service (Foundation Components) | [Klicka här](/help/forms/rule-editor.md) |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=sv-SE) |

I ett adaptivt formulär baserat på kärnkomponenter ger regelredigeringsfunktionen både företagsanvändare och utvecklare möjlighet att skriva regler för adaptiva formulärobjekt. Dessa regler definierar åtgärder som ska utlösas av formulärobjekt baserat på förinställda villkor, användarindata och användaråtgärder i formuläret. Detta gör att man kan effektivisera ifyllandet ytterligare och säkerställa både precision och hastighet.

Regelredigeraren har ett intuitivt och förenklat användargränssnitt för att skriva regler. Det erbjuder en visuell redigerare som fångar upp alla användare och gör det möjligt för dem att skapa och hantera regler utan att behöva omfattande teknisk kunskap. Detta visuella tillvägagångssätt gör det enklare för användarna att förstå och implementera den önskade logiken i sina formulär.

Några av de nyckelåtgärder du kan utföra på adaptiva formulärobjekt med hjälp av regler är:

* Visa eller dölja ett objekt
* Aktivera eller inaktivera ett objekt
* Ange ett värde för ett objekt
* Validera ett objekts värde
* Utför funktioner för att beräkna värdet för ett objekt
* Anropa en FDM-tjänst (Form Data Model) och utföra en åtgärd
* Ange ett objekts egenskap

<!-- Rule editor replaces the scripting capabilities in [!DNL Experience Manager 6.1 Forms] and earlier releases. However, your existing scripts are preserved in the new rule editor. For more information about working with existing scripts in the rule editor, see [Impact of rule editor on existing scripts](rule-editor.md#p-impact-of-rule-editor-on-existing-scripts-p). -->

Användare som läggs till i gruppen `forms-power-users` kan skapa skript och redigera befintliga. Användare i gruppen [!DNL forms-users] kan använda skript men inte skapa eller redigera skript.

Se artikeln [Skillnad mellan redigeraren för grundregler och redigeraren för kärnkomponentregel](/help/forms/rule-editor-core-components-difference-tables.md) för en detaljerad jämförelse.

<!--
## Difference between Rule editor in Core Components and Rule Editor in Foundation Components

{{rule-editor-diff}}

>[!NOTE]
>
> To see how to create and use custom functions in detail, refer to [Custom functions in Adaptive Forms (Core Components)](/help/forms/create-and-use-custom-functions.md) article.

-->

## Förstå en regel {#understanding-a-rule}

En regel är en kombination av åtgärder och villkor. I regelredigeraren omfattar åtgärderna aktiviteter som att dölja, visa, aktivera, inaktivera eller beräkna värdet för ett objekt i ett formulär. Villkor är booleska uttryck som utvärderas genom att kontroller och åtgärder utförs på ett formulärobjekts status, värde eller egenskap. Åtgärder utförs baserat på det värde ( `True` eller `False`) som returneras när ett villkor utvärderas.

Regelredigeraren innehåller en uppsättning fördefinierade regeltyper, till exempel När, Visa, Dölj, Aktivera, Inaktivera, Ange värde för och Validera, som hjälper dig att skriva regler. Med varje regeltyp kan du definiera villkor och åtgärder i en regel. I dokumentet förklaras dessutom varje regeltyp i detalj.

En regel följer vanligtvis någon av följande konstruktioner:

**Condition-Action** I den här konstruktionen definierar en regel först ett villkor följt av en åtgärd som ska utlösas. Konstruktionen är jämförbar med if-then-satsen i programmeringsspråk.

Regeltypen **När** används i regelredigeraren för att framtvinga konstruktorn för villkorsåtgärd.

**Åtgärdsvillkor** I den här konstruktionen definierar en regel först en åtgärd som ska utlösas följt av villkor för utvärdering. En annan variant av den här konstruktionen är action-condition-alternate action, som också definierar en alternativ åtgärd som ska utlösas om villkoret returnerar False.

Regeltyperna Visa, Dölj, Aktivera, Inaktivera, Ange värde för och Validera i regelredigeraren framtvingar regelkonstruktionen för åtgärdsvillkor. Som standard är den alternativa åtgärden för Visa Dölj och Aktivera Inaktivera, och tvärtom. Du kan inte ändra den alternativa standardåtgärden.

>[!NOTE]
>
>De tillgängliga regeltyperna, inklusive villkor och åtgärder som du definierar i regelredigeraren, beror också på vilken typ av formulärobjekt du skapar en regel på. Regelredigeraren visar endast giltiga regeltyper och alternativ för att skriva villkor och åtgärdssatser för en viss formulärobjekttyp. Du kan till exempel inte se Validera och Ange typvärde för ett panelobjekt.

Mer information om tillgängliga regeltyper i regelredigeraren finns i [Tillgängliga regeltyper i regelredigeraren](rule-editor.md#p-available-rule-types-in-rule-editor-p).

### Riktlinjer för val av regelkonstruktion {#guidelines-for-choosing-a-rule-construct}

Även om du kan uppnå de flesta användningsexemplen genom att använda valfri regelkonstruktion finns det några riktlinjer för att välja en konstruktion framför en annan. Mer information om tillgängliga regler i regelredigeraren finns i [Tillgängliga regeltyper i regelredigeraren](rule-editor.md#p-available-rule-types-in-rule-editor-p).

* En typisk tumregel när du skapar en regel är att tänka på den i kontexten för det objekt som du skriver en regel för. Tänk på att du vill dölja eller visa fältet B baserat på det värde som användaren anger i fältet A. I det här fallet utvärderar du ett villkor i fält A och baserat på det värde som returneras utlöser du en åtgärd i fält B.

  Om du skriver en regel i fält B (det objekt som du utvärderar ett villkor för) ska du därför använda konstruktorn condition-action eller regeltypen When. Använd på samma sätt konstruktionen action-condition eller Visa eller Dölj regel i fält A.

* Ibland måste du utföra flera åtgärder baserat på ett villkor. I sådana fall bör du använda konstruktorn condition-action. I den här konstruktionen kan du utvärdera ett villkor en gång och ange flera åtgärdssatser.

  Om du till exempel vill dölja fält B, C och D baserat på villkoret som kontrollerar värdet som användaren anger i fält A, skriver du en regel med villkorsstyrd konstruktion eller Regeltyp för När i fält A och anger åtgärder som styr synligheten för fält B, C och D. I annat fall behöver du tre separata regler för fälten B, C och D, där varje regel kontrollerar villkoret och visar eller döljer respektive fält. I det här exemplet är det effektivare att skriva Regeltypen När för ett objekt i stället för regeltypen Visa eller Dölj för tre objekt.

* Om du vill aktivera en åtgärd baserat på flera villkor bör du använda en konstruktor för åtgärdsvillkor. Om du till exempel vill visa och dölja fält A genom att utvärdera villkor i fält B, C och D, använder du regeltypen Visa eller Dölj i fält A.
* Använd villkorskonstruktion för villkorsåtgärd eller åtgärd om regeln innehåller en åtgärd för ett villkor.
* Om en regel söker efter ett villkor och utför en åtgärd omedelbart när ett värde anges i ett fält eller när ett fält avslutas, rekommenderar vi att du skriver en regel med en villkorsstyrd konstruktion eller med regeltypen När i fältet som villkoret utvärderas i.
* Villkoret i regeln När utvärderas när en användare ändrar värdet på objektet som regeln När används på. Men om du vill att åtgärden ska utlösas när värdet ändras på serversidan, till exempel för förifyllning av värdet, rekommenderar vi att du skriver en When-regel som utlöser åtgärden när fältet initieras.
* När du skriver regler för nedrullningsbara listor, alternativknappar eller kryssruteobjekt fylls alternativen eller värdena för dessa formulärobjekt i förväg i regelredigeraren.

Mer information om hur du använder användargränssnittet för att skriva och hantera regler i en regelredigerare finns i artikeln [Användargränssnitt för regelredigeraren för Adaptiv Forms baserat på kärnkomponenter](/help/forms/rule-editor-core-components-user-interface.md).

## Se även

{{see-also-rule-editor}}