---
title: Använda CRXDE Lite
description: CRXDE Lite är en del av AEM snabbstart och är tillgängligt för dig att komma åt och ändra databasen i dina lokala utvecklingsmiljöer i webbläsaren.
exl-id: 1581a7e5-6f84-4a45-8e8f-c83692ea077a
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 0%

---

# Använda CRXDE Lite {#using-crxde-lite}

CRXDE Lite är en del av AEM snabbstart och är tillgängligt för dig att komma åt och ändra databasen i dina lokala utvecklingsmiljöer i webbläsaren. Med CRXDE Lite kan du redigera filer, mappar, noder och egenskaper. Hela databasen är tillgänglig i det här lättanvända gränssnittet.

>[!NOTE]
>
>CRXDE Lite är endast tillgängligt i dina lokala utvecklingsmiljöer. Det finns inte i AEM as a Cloud Service.

## Komma igång med CRXDE Lite {#getting-started-with-crxde-lite}

Så här kommer du igång med CRXDE Lite:

1. Kom igång snabbt med utvecklingen av AEM.
1. Öppna URL:en `https://<host>:<port>/crx/de` i webbläsaren.
1. Ange ditt **användarnamn** och **lösenord**.
1. Klicka på **OK**.

Gränssnittet CRXDE Lite visas så här i webbläsaren:

![Gränssnittet i CRXDE Lite](assets/crxde-lite.png)

>[!TIP]
>
>Du kan också öppna CRXDE Lite från AEM-menyn. På huvudmenyn väljer du **Verktyg** > **Allmänt** > **CRXDE Lite**.

## Översikt över användargränssnittet {#overview-of-the-user-interface}

CRXDE Lite användargränssnitt har många delar och många funktioner.

### Övre växlingsfält {#top-switcher-bar}

Med det övre växlingsfältet kan du snabbt växla mellan CRXDE Lite och [pakethanteraren.](package-manager.md)

### Nodsökväg, widget {#node-path-widget}

Widgeten Nodsökväg visar sökvägen till den markerade noden.

Du kan också använda den för att hoppa till en nod genom att ange sökvägen manuellt eller klistra in den någon annanstans och trycka på Retur.

Det finns även stöd för att söka efter noder med ett specifikt nodnamn. Ange namnet på noden som du vill söka efter och vänta (eller välj sökikonen till höger). Om en viss nod eller noder läses in i utforskarrutan visas listan och du kan välja sökvägen och trycka på Retur för att navigera till den. Det fungerar bara för de noder som för närvarande är inlästa i CRXDE-klientprogrammet i webbläsaren. Om du vill söka i hela databasen använder du **Verktyg** -&amp;gt: **Fråga**.

### Utforskarfönster {#explorer-pane}

I **Utforskarfönstret** visas ett träd med alla noder i databasen.

Klicka på en nod för att visa dess egenskaper på fliken **Egenskaper**. När du har klickat på en nod kan du välja en åtgärd i verktygsfältet. Klicka på noden igen för att byta namn på den.

Med Trädnavigeringsfilter (ikonen för kikaren) kan du filtrera noderna i databasen som namnet innehåller indatatexten för. Det gäller endast noder som har lästs in lokalt.

### Redigeringsruta {#edit-pane}

I **redigeringsfönstret** kan du visa innehållet i den markerade filen i databasen. Varje fil som öppnas representeras som en egen flik i rutan.

På fliken **Hem** kan du söka efter innehåll och/eller dokumentation och komma åt utvecklardokumentation och stöd för Adobe.

Dubbelklicka på en fil i **Utforskarrutan** för att visa dess innehåll i **redigeringsrutan**. Du kan sedan ändra den och spara ändringarna.

När en fil har redigerats i **redigeringsrutan** är följande verktyg tillgängliga i verktygsfältet:

* **Visa i trädet** - Visar filen i databasträdet.
* **Sök/ersätt** - Utför en sökning eller ersättning.

Dubbelklicka på statusraden i **redigeringsfönstret** så öppnas dialogrutan **Gå till rad** där du kan ange ett visst radnummer.

### Fliken Egenskaper {#properties-tab}

Fliken **Egenskaper** visar egenskaperna för den nod som du har valt. Du kan lägga till nya eller ta bort befintliga egenskaper.

### Fliken Åtkomstkontroll {#access-control-tab}

På fliken **Åtkomstkontroll** visas behörigheter baserat på den aktuella sökvägen, databasen eller säkerhetsobjektet.

Behörigheterna är indelade i följande kategorier.

* **Tillämplig åtkomstkontrollprincip** - De principer som kan tillämpas på det aktuella urvalet
* **Lokala åtkomstkontrollprinciper** - De aktuella principer som tillämpas lokalt på den aktuella markeringen
* **Effektiva åtkomstkontrollprinciper** - De aktuella principer som används för den aktuella markeringen, som kan anges lokalt eller ärvs från överordnade noder

>[!NOTE]
>
För att kunna se åtkomstkontrollsinformation måste användaren som är inloggad på CRXDE Lite ha behörighet att läsa ACL-poster.

### Fliken Replikering {#replication-tab}

På fliken **Replikering** visas den aktuella nodens replikeringsstatus. Du kan replikera och replikera borttagningen av den aktuella noden.

### Fliken Konsol {#console-tab}

På fliken **Konsol** visas loggmeddelanden. Du kan konfigurera loggnivån, rensa konsolen, fästa vid den valda rullningspositionen och aktivera/inaktivera visning av meddelanden.

### Fliken Build Info {#build-info-tab}

Fliken **Build Info** visar information när ett paket byggs.

### Knappen Uppdatera {#refresh-button}

Knappen **Uppdatera** uppdaterar den aktuella markeringen. Ändringar från andra användare uppdateras i din vy av databasen. De ändringar du har gjort påverkas inte.

### Spara alla, knapp {#save-all-button}

Knappen **Spara alla** sparar alla ändringar du har gjort. Ändringarna är tillfälliga tills du väljer att spara och försvinner när du avslutar konsolen.

* **Återgå** - Ignorerar alla ändringar som du har gjort på den valda noden sedan den senaste sparandeåtgärden och läser sedan in databasens aktuella status för den valda noden igen
* **Återställ alla** - Ignorerar alla ändringar som du har gjort i hela databasen sedan den senaste sparåtgärden och läser sedan in databasens aktuella status igen

### Skapa-knapp {#create-button}

Knappen **Skapa** är en nedrullningsbar meny som skapar följande under den markerade noden:

* Nod - en nod med en godtycklig nodtyp
* Fil - en `nt:file`-nod och dess nt:resource-undernod
* Mapp - en `nt:folder`-nod

### Ta bort-knapp {#delete-button}

**Ta bort-knappen** tar bort den markerade noden.

### Knappen Kopiera {#copy-button}

Knappen **Kopiera** kopierar den markerade noden.

## Knappen Klistra in {#paste-button}

Knappen **Klistra in** klistrar in den kopierade noden under den markerade noden.

### Flytta-knapp {#move-button}

**Flytta-knappen** flyttar den markerade noden till den nod som anges i dialogrutan.

### Byt namn {#rename-button}

Knappen **Byt namn på** byter namn på den markerade noden.

### Blandningar {#mixins-button}

Med knappen **Blandningar** kan du lägga till blandningstyper i nodtypen. Blandningstyperna används oftast för att lägga till avancerade funktioner.

### verktyg {#tools-button}

**Verktygsknappen** är en nedrullningsbar meny med följande verktyg:

* **Serverkonfiguration** - för åtkomst till Felix Console (finns också på `https://<host>:<port>/system/console/configMgr`)
* **Fråga** - för att fråga databasen
* **Behörigheter** - för att visa och lägga till behörigheter
* **Testa åtkomstkontrollen** - för att testa behörigheten för en viss sökväg och/eller huvudnamn
* **Exportera nodtyp** - för att exportera nodtyper i systemet som CND-notation
* **Importera nodtyp** - för att importera nodtyper med CND-notation.

### Inloggningswidget {#login-widget}

**Inloggningswidgeten** visar den inloggade användaren.

Klicka på den för att logga in eller logga in igen som en annan användare. `@crx.default` representerar att du är i standardarbetsytan (och endast) i databasen.

Alternativet **Inställningar** kan användas för att ange gränssnittsspråk och för att visa och anpassa snabbtangenterna för olika åtgärder som att spara, söka, skapa anteckning och så vidare.

## Skapa en mapp {#creating-a-folder}

Så här skapar du en mapp med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. I navigeringsrutan högerklickar du på den mapp som du vill skapa den nya mappen under, väljer **Skapa ...** och sedan **Skapa mapp ...**.

1. Ange mappen **Namn** och klicka på **OK**.

1. Klicka på **Spara alla** för att spara ändringarna på servern.

## Skapa en nod {#creating-a-node}

Så här skapar du en nod med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. Högerklicka på noden där du vill skapa den nya noden i [**Utforskarrutan**](#explorer-pane), välj **Skapa** och sedan **Skapa nod**.
1. Ange **Namn** och välj **Typ**.
1. Klicka på **OK**.
1. Klicka på knappen [**Spara alla**](#save-all-button) för att spara ändringarna på servern.

Nu kan du anpassa noden efter dina behov genom att ändra egenskaper eller skapa nya noder.

>[!NOTE]
>
De flesta redigeringsåtgärderna, inklusive **Skapa nod**, sparar alla ändringar i minnet och lagrar dem bara i databasen när de sparas (med knappen [**Spara alla**](#save-all-button)). Vissa åtgärder, till exempel move, sparas dock automatiskt.
>
Valideringen av om den skapade noden tillåts av den överordnade nodens nodtyp utförs även av databasen när ändringar sparas. Om du får ett felmeddelande när du sparar en nod kontrollerar du om innehållsstrukturen är giltig (du kan till exempel inte skapa en `nt:unstructured`-nod som underordnad `nt:folder`-nod).

## Skapa en egenskap {#creating-a-property}

Så här skapar du en egenskap med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. I [**Utforskarpanelen** ](#explorer-pane) markerar du den nod där du vill lägga till den nya egenskapen.
1. Ange **Namn**, **Typ** och **Värde** på fliken [**Egenskaper**](#properties-tab) i den nedre rutan.
1. Klicka på **Lägg till**.
1. Klicka på knappen [**Spara alla**](#save-all-button) för att spara ändringarna på servern.

## Skapa en fil {#creating-a-file}

Så här skapar du en fil med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. Högerklicka på komponenten där du vill skapa filen i [**Utforskarrutan**](#explorer-pane), välj **Skapa** och sedan **Skapa fil**.
1. Ange filen **Namn** med filnamnstillägget.
1. Klicka på **OK**.
1. Den nya filen öppnas som en flik i [**redigeringsfönstret**.](#edit-pane)
1. Redigera filen.
1. Klicka på knappen [**Spara alla**](#save-all-button) för att spara ändringarna.

## Exportera och importera nodtyper {#exporting-and-importing-node-types}

Med CRXDE Lite kan du importera och/eller exportera nodtypsdefinitioner i [komprimerat namnutrymme och CND-notation (Node Type Definition)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Så här exporterar du en nodtypsdefinition i CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. Välj önskad nod.
1. Välj **Verktyg** och sedan **Exportera nodtyp**.
1. Definitionen visas i CND-notation på en ny flik i webbläsaren.
1. Spara informationen om det behövs.

Så här importerar du en nodtypsdefinition:

1. Öppna CRXDE Lite i webbläsaren.
1. Välj **Verktyg** och sedan **Importera nodtyp**.
1. En ny flik öppnas i [**redigeringsfönstret**](#edit-pane) med namnet **Importera nodtyp**.
1. Ange CND-notation för definitionen i textrutan på fliken **Importera nodtyp**.
1. Markera **Tillåt uppdatering** om du uppdaterar en befintlig definition.
1. Klicka på **Importera**.

## Loggning {#logging}

Med CRXDE Lite kan du visa filen `error.log` som finns i filsystemet på `<aem-install-dir>/crx-quickstart/logs` och filtrera den med rätt loggnivå. Gör så här:

1. Öppna CRXDE Lite i webbläsaren.
1. Välj **Serverloggar** på den nedrullningsbara menyn till höger om fliken [**Konsol**](#console-tab) längst ned i fönstret.
1. Klicka på ikonen **Stopp** för att visa meddelandena.

Du kan:

* Justera loggparametrarna i Felix Console genom att klicka på ikonen **Loggningskonfigurationer** .
* Rensa meddelandena genom att klicka på ikonen **Rensa konsol** .
* Fäst meddelandet vid den aktuella markeringen genom att klicka på ikonen **Fäst konsol** .
* Aktivera eller inaktivera visningen av meddelanden genom att klicka på ikonen **Stoppa** .
