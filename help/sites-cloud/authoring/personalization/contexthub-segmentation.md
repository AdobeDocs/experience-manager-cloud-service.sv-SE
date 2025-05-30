---
title: Konfigurera segmentering med ContextHub
description: Lär dig konfigurera segmentering med ContextHub.
exl-id: fbc38611-dbee-426e-b823-df64b6730c45
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '1653'
ht-degree: 0%

---

# Konfigurera segmentering med ContextHub{#configuring-segmentation-with-contexthub}

Segmentering är en viktig faktor när man skapar en kampanj. Mer information om hur segmentering fungerar och nyckeltermer finns i [Förstå segmentering](segmentation.md).

Beroende på den information du redan har samlat in om webbplatsbesökarna och de mål du vill uppnå, kan du definiera de segment och strategier som behövs för det riktade innehållet.

Dessa segment används sedan för att förse en besökare med specifikt riktat innehåll. [Aktiviteter](activities.md) som definieras här kan inkluderas på alla sidor och definiera vilket besökarsegment det specialiserade innehållet gäller.

AEM gör att ni enkelt kan personalisera användarnas upplevelser. Du kan också kontrollera resultatet av segmentdefinitionerna.

## Åtkomst till segment {#accessing-segments}

Konsolen [Publiker](audiences.md) används för att hantera segment för ContextHub och målgrupper för ditt Adobe Target-konto. I den här dokumentationen beskrivs hur du hanterar segment för ContextHub.

Om du vill komma åt dina segment väljer du **Navigering > Personalization > Publiker** i den globala navigeringen. Välj din konfiguration (till exempel WKND-plats) för att visa dina segment:

![Hantera målgrupper](../assets/contexthub-segmentation-audiences.png)

## Segmentredigerare {#segment-editor}

<!--The **Segment Editor** lets you easily modify a segment. To edit a segment, select a segment in the [list of segments](/help/sites-administering/segmentation.md#accessing-segments) and click the **Edit** button.-->
Med **segmentredigeraren** kan du enkelt ändra ett segment. Om du vill redigera ett segment markerar du det i segmentlistan och klickar på knappen **Redigera** .

![Segmentredigerare](../assets/contexthub-segment-editor.png)

Med komponentwebbläsaren kan du lägga till behållare för **AND** och **OR** för att definiera segmentlogiken och sedan lägga till ytterligare komponenter för att jämföra egenskaper och värden eller referensskript och andra segment för att definiera urvalskriterierna (se [Skapa ett nytt segment](#creating-a-new-segment)) för att definiera det exakta scenariot för att markera segmentet.

När hela programsatsen utvärderas till true har segmentet lösts. Om flera segment är tillämpliga används även **Förstärkningsfaktorn**. Mer information om förstärkningsfaktorn finns i [Skapa ett nytt segment](#creating-a-new-segment).

>[!CAUTION]
>
>Segmentredigeraren söker inte efter några cirkelreferenser. Segment A refererar till exempel till ett annat segment B, som i sin tur refererar till segment A. Du måste se till att dina segment inte innehåller några cirkelreferenser.

### Behållare {#containers}

Följande behållare är tillgängliga när de är klara och gör att du kan gruppera jämförelser och referenser tillsammans för boolesk utvärdering. De kan dras från komponentwebbläsaren till redigeraren. Mer information finns i följande avsnitt: [Använda OCH ELLER Behållare](#using-and-and-or-containers).

|  |  |
|---|---|
| Behållare OCH | Operatorn boolesk AND |
| Behållare ELLER | Operatorn boolesk OR |

### Jämförelser {#comparisons}

Följande segmentjämförelser är tillgängliga när du vill utvärdera segmentegenskaperna. De kan dras från komponentwebbläsaren till redigeraren.

|  |  |
|---|---|
| Property-Value | Jämför en egenskap i en butik med ett definierat värde |
| property-property | Jämför en egenskap i en butik med en annan egenskap |
| Referens för egenskapssegment | Jämför en egenskap i en butik med ett annat refererat segment |
| Referens för egenskapsskript | Jämför en egenskap i en butik med resultatet av ett skript |
| Referens för segmentreferens-Script | Jämför ett hänvisat segment med resultatet av ett skript |

>[!NOTE]
>
>Om datatypen för jämförelsen inte är inställd (d.v.s. inställd på automatisk identifiering), kommer ContextHubs segmenteringsmotor att jämföra värdena som javascript skulle göra. Den konverterar inte värden till de förväntade typerna, vilket kan leda till missvisande resultat. Till exempel:
>
>`null < 30 // will return true`
>
>När du [skapar ett segment](#creating-a-new-segment) bör du därför välja en **datatyp** när typerna av jämförda värden är kända. Till exempel:
>
>När du jämför egenskapen `profile/age` vet du redan att jämförelsetypen är **number**, så även om `profile/age` inte är inställd returneras en jämförelse `profile/age` som är mindre än 30 **false**, som du skulle kunna förvänta dig.

### Referenser {#references}

Följande referenser är tillgängliga när du vill länka direkt till ett skript eller ett annat segment. De kan dras från komponentwebbläsaren till redigeraren.

|  |  |
|---|---|
| Segmentreferens | Utvärdera det refererade segmentet |
| Skriptreferens | Utvärdera det refererade skriptet. Mer information finns i följande avsnitt: [Använda skriptreferenser](#using-script-references). |

## Skapa ett nytt segment {#creating-a-new-segment}

Så här definierar du det nya segmentet:

1. När [har öppnat segmenten](#accessing-segments) [navigerar ](#organizing-segments) till mappen där du vill skapa segmentet.

1. Markera knappen **Skapa** och välj **Skapa ContextHub-segment**.

   ![Lägg till segment](../assets/contexthub-create-segment.png)

1. I **Nytt ContextHub-segment** anger du en rubrik för segmentet och ett boostvärde om det behövs. Välj sedan **Skapa**.

   ![Nytt segment](../assets/contexthub-new-segment.png)

   Varje segment har en startparameter som används som viktningsfaktor. Ett högre värde anger att segmentet är markerat i stället för ett segment med ett lägre värde i instanser där flera segment är giltiga.

   * Minsta värde: `0`
   * Högsta värde: `1000000`

1. I segmentkonsolen redigerar du det segment du har skapat och öppnar det i segmentredigeraren.
1. Dra en jämförelse eller referens till segmentredigeraren som den visas i standardbehållaren OCH.
1. Dubbelmarkera konfigurationsalternativet för den nya referensen eller segmentet för att redigera de specifika parametrarna. I det här exemplet testar vi för folk i Basel.

   ![Testning för personer i Basel](../assets/contexthub-comparing-property-value.png)

   Ange alltid en **datatyp** om möjligt för att försäkra dig om att dina jämförelser utvärderas korrekt. Mer information finns i [Jämförelser](#comparisons).

1. Klicka på **Klar** för att spara definitionen:
1. Lägg till fler komponenter efter behov. Du kan formulera booleska uttryck med behållarkomponenterna för AND- och OR-jämförelser (se [Använda OCH eller behållare](#using-and-and-or-containers) nedan). Med segmentredigeraren kan du ta bort komponenter som inte längre behövs eller dra dem till nya positioner i programsatsen.

### Använda OCH- och ELLER-behållare {#using-and-and-or-containers}

Med hjälp av komponenterna AND och OR kan du skapa komplexa segment i AEM. När du gör det är det bra att tänka på några grundläggande saker:

* Definitionens översta nivå är alltid den AND-behållare som skapas från början. Detta kan inte ändras, men påverkar inte resten av segmentdefinitionen.
* Se till att det är rimligt att kapsla behållaren. Behållarna kan ses som parenteser i ditt booleska uttryck.

Följande exempel används för att välja besökare som beaktas i vår schweiziska målgrupp:

```text
 People in Basel

 OR

 People in Zürich
```

Du börjar med att placera en OR-behållarkomponent i standardbehållaren AND. I ELLER-behållaren kan du lägga till egenskaps- eller referenskomponenterna.

![Segment med OR-operator](../assets/contexthub-or-operator.png)

Du kan kapsla in flera AND- och OR-operatorer efter behov.

### Använda skriptreferenser {#using-script-references}

Genom att använda komponenten Skriptreferens kan utvärderingen av en segmentegenskap delegeras till ett externt skript. När skriptet har konfigurerats på rätt sätt kan det användas som en annan komponent i ett segmentvillkor.

#### Definiera ett skript som ska refereras {#defining-a-script-to-reference}

1. Lägg till fil i `contexthub.segment-engine.scripts` clientlib.
1. Implementera en funktion som returnerar ett värde. Till exempel:

   ```javascript
   ContextHub.console.log(ContextHub.Shared.timestamp(), '[loading] contexthub.segment-engine.scripts - script.profile-info.js');
   
   (function() {
       'use strict';
   
       /**
        * Sample script returning profile information. Returns user info if data is available, false otherwise.
        *
        * @returns {Boolean}
        */
       var getProfileInfo = function() {
           /* let the SegmentEngine know when script should be re-run */
           this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
           this.dependOn(ContextHub.SegmentEngine.Property('profile/givenName'));
   
           /* variables */
           var name = ContextHub.get('profile/givenName');
           var age = ContextHub.get('profile/age');
   
           return name === 'Joe' && age === 123;
       };
   
       /* register function */
       ContextHub.SegmentEngine.ScriptManager.register('getProfileInfo', getProfileInfo);
   
   })();
   ```

1. Registrera skriptet med `ContextHub.SegmentEngine.ScriptManager.register`.

Om skriptet är beroende av ytterligare egenskaper bör skriptet anropa `this.dependOn()`. Om skriptet till exempel är beroende av `profile/age`:

```javascript
this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
```

#### Referera till ett skript {#referencing-a-script}

1. Skapa ContextHub-segment.
1. Lägg till komponenten **Skriptreferens** på den önskade platsen i segmentet.
1. Öppna redigeringsdialogrutan för komponenten **Skriptreferens**. Om [är korrekt konfigurerat](#defining-a-script-to-reference) bör skriptet vara tillgängligt i listrutan **Skriptnamn**.

## Organisera segment {#organizing-segments}

Om du har många segment kan det bli svårt att hantera dem som en platt lista. I sådana fall kan det vara användbart att skapa mappar för att hantera dina segment.

### Skapa en ny mapp {#create-folder}

1. När [har öppnat segmenten](#accessing-segments) markerar du knappen **Skapa** och väljer **Mapp**.

   ![Lägg till mapp](../assets/contexthub-create-segment.png)

1. Ange en **titel** och ett **namn** för din mapp.
   * **Rubriken** ska vara beskrivande.
   * **Namn** blir nodnamnet i databasen.
      * Den genereras automatiskt baserat på titeln och justeras enligt [AEM namnkonventioner](/help/implementing/developing/introduction/naming-conventions.md).
      * Den kan vid behov justeras.

   ![Skapa mapp](../assets/contexthub-create-folder.png)

1. Välj **Skapa**.

   ![Bekräfta mapp](../assets/contexthub-confirm-folder.png)

1. Mappen visas i segmentlistan.
   * Hur du sorterar kolumnerna påverkar var i listan den nya mappen visas.
   * Du kan välja kolumnrubrikerna för att justera sorteringen.

     ![Den nya mappen](../assets/contexthub-folder.png)

### Ändra befintliga mappar {#modify-folders}

1. När [har öppnat segmenten](#accessing-segments) markerar du mappen som du vill ändra.

   ![Välj mapp](../assets/contexthub-select-folder.png)

1. Välj **Byt namn på** i verktygsfältet om du vill byta namn på mappen.

1. Ange en ny **mapptitel** och välj **Spara**.

   ![Byt namn på mapp](../assets/contexthub-rename-folder.png)

>[!NOTE]
>
>När du byter namn på mappar kan du bara ändra titeln. Namnet kan inte ändras.

### Ta bort en mapp

1. När [har öppnat segmenten](#accessing-segments) markerar du mappen som du vill ändra.

   ![Välj mapp](../assets/contexthub-select-folder.png)

1. Välj **Ta bort** i verktygsfältet för att ta bort mappen.

1. En dialogruta innehåller en lista med mappar som har markerats för borttagning.

   ![Bekräfta borttagning](../assets/contexthub-confirm-segment-delete.png)

   * Bekräfta genom att välja **Ta bort**.
   * Välj **Avbryt** om du vill avbryta.

1. Om någon av de markerade mapparna innehåller undermappar eller segment måste borttagningen bekräftas.

   ![Bekräfta borttagning av underordnade](../assets/contexthub-confirm-segment-child-delete.png)

   * Bekräfta genom att välja **Tvinga borttagning**.
   * Välj **Avbryt** om du vill avbryta.

>[!NOTE]
>
> Det går inte att flytta ett segment från en mapp till en annan.

## Testa tillämpningen av ett segment {#testing-the-application-of-a-segment}

När segmentet har definierats kan potentiella resultat testas med hjälp av **[ContextHub](contexthub.md).**

1. Förhandsgranska en sida
1. Klicka på ikonen ContextHub för att visa kontextHub-verktygsfältet
1. Välj en profil som matchar segmentet du skapade
1. ContextHub löser de segment som är tillämpliga för den valda personen

Vår enkla segmentdefinition för att identifiera användare i Basel baseras till exempel på var användaren befinner sig. När du läser in en specifik profil som matchar dessa villkor visas om segmentet har matchats:

![Segment som löses](../assets/contexthub-segment-resolve.png)

Eller om den inte är löst:

![Segment som inte kan matchas](../assets/contexthub-segment-doesnt-resolve.png)

>[!NOTE]
>
>Alla egenskaper åtgärdas omedelbart, men de flesta ändras bara vid sidinläsning.

Sådana tester kan även utföras på innehållssidor och i kombination med riktat innehåll och relaterade **aktiviteter** och **upplevelser**.

Om du har konfigurerat en aktivitet och upplevelse kan du enkelt testa ditt segment med aktiviteten. Mer information om hur du konfigurerar en aktivitet finns i [dokumentationen om hur du redigerar målinnehåll](targeted-content.md).

1. I redigeringsläget för en sida där du har konfigurerat riktat innehåll kan du se att innehållet har angetts som mål via en pilikon i innehållet.
1. Växla till förhandsgranskningsläget och använd kontextnavet för att växla till en profil som inte matchar den segmentering som har konfigurerats för upplevelsen.
1. Byt till en persona som matchar den segmentering som konfigurerats för upplevelsen och se att upplevelsen ändras i enlighet med detta.

## Använda ditt segment {#using-your-segment}

Segment används för att styra det faktiska innehåll som ses av specifika målgrupper. Mer information om målgrupper och segment finns i [Hantera målgrupper](audiences.md) och [Skapa riktat innehåll](targeted-content.md) om hur du använder målgrupper och segment för att rikta innehåll.
