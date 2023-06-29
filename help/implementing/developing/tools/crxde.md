---
title: Använda CRXDE Lite
description: CRXDE Lite är en del av AEM snabbstart och är tillgängligt för dig att komma åt och ändra databasen i dina lokala utvecklingsmiljöer i webbläsaren.
exl-id: 1581a7e5-6f84-4a45-8e8f-c83692ea077a
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1688'
ht-degree: 0%

---

# Använda CRXDE Lite {#using-crxde-lite}

CRXDE Lite är en del av AEM snabbstart och är tillgängligt för dig att komma åt och ändra databasen i dina lokala utvecklingsmiljöer i webbläsaren. Med CRXDE Lite kan du redigera filer, mappar, noder och egenskaper. Hela databasen är tillgänglig i det här lättanvända gränssnittet.

>[!NOTE]
>
>CRXDE Lite är endast tillgängligt i dina lokala utvecklingsmiljöer. Det finns inte på AEM as a Cloud Service.

## Komma igång med CRXDE Lite {#getting-started-with-crxde-lite}

Så här kommer du igång med CRXDE Lite:

1. Kom igång snabbt med utvecklingen av AEM.
1. Öppna URL-adressen i webbläsaren `https://<host>:<port>/crx/de`.
1. Ange **användarnamn** och **lösenord**.
1. Klicka **OK**.

Gränssnittet CRXDE Lite visas så här i webbläsaren:

![Gränssnittet CRXDE Lite](assets/crxde-lite.png)

>[!TIP]
>
>Du kan också öppna CRXDE Lite från AEM-menyn. På huvudmenyn väljer du **verktyg** -> **Allmänt** -> **CRXDE Lite**.

## Översikt över användargränssnittet {#overview-of-the-user-interface}

CRXDE Lite användargränssnitt har många delar och många funktioner.

### Övre växlingsfält {#top-switcher-bar}

Med hjälp av det övre växlingsfältet kan du snabbt växla mellan CRXDE Lite och [Pakethanteraren.](package-manager.md)

### Nodsökväg, widget {#node-path-widget}

Widgeten Nodsökväg visar sökvägen till den markerade noden.

Du kan också använda den för att hoppa till en nod genom att ange sökvägen manuellt eller klistra in den någon annanstans och trycka på Retur.

Det finns även stöd för att söka efter noder med ett specifikt nodnamn. Ange namnet på noden som du vill söka efter och vänta (eller välj sökikonen till höger). Om en viss nod eller noder läses in i utforskarrutan visas listan och du kan välja sökvägen och trycka på Retur för att navigera till den. Observera att det bara fungerar för de noder som för närvarande är inlästa i CRXDE-klientprogrammet i webbläsaren. Om du vill söka i hela databasen använder du **verktyg** ->: **Fråga**.

### Utforskarfönster {#explorer-pane}

The **Utforskarfönster** visar ett träd med alla noder i databasen.

Klicka på en nod för att visa dess egenskaper i **Egenskaper** -fliken. När du har klickat på en nod kan du välja en åtgärd i verktygsfältet. Klicka på noden igen för att byta namn på den.

Med Trädnavigeringsfilter (ikonen för kikaren) kan du filtrera noderna i databasen som namnet innehåller indatatexten för. Det gäller endast noder som har lästs in lokalt.

### Redigeringsruta {#edit-pane}

The **Redigeringsruta** I kan du visa innehållet i den markerade filen i databasen. Varje fil som öppnas representeras som en egen flik i rutan.

The **Startsida** Med -fliken kan du söka efter innehåll och/eller dokumentation och få tillgång till utvecklardokumentation och stöd för Adobe.

Dubbelklicka på en fil i **Utforskarfönster** för att visa innehållet i **Redigeringsruta**. Du kan sedan ändra den och spara ändringarna.

När en fil har redigerats i **Redigeringsruta** finns följande verktyg i verktygsfältet:

* **Visa i träd** - Visar filen i databasträdet.
* **Sök/ersätt** - Utför en sökning eller ersättning.

Dubbelklicka på statusraden i **Redigeringsruta** öppnar **Gå till rad** så att du kan ange ett visst radnummer.

### Fliken Egenskaper {#properties-tab}

The **Fliken Egenskaper** visar egenskaperna för den nod som du har valt. Du kan lägga till nya eller ta bort befintliga egenskaper.

### Fliken Åtkomstkontroll {#access-control-tab}

The **Fliken Åtkomstkontroll** visar behörigheter baserat på aktuell sökväg, databas eller huvudnamn.

Behörigheterna är indelade i följande kategorier.

* **Tillämplig åtkomstkontrollprincip** - De profiler som kan tillämpas på den aktuella markeringen
* **Principer för lokal åtkomstkontroll** - De aktuella principer som används lokalt för den aktuella markeringen
* **Effektiva åtkomstkontrollprinciper** - De aktuella principer som används för den aktuella markeringen, som kan anges lokalt eller ärvs från överordnade noder

>[!NOTE]
>
För att kunna se åtkomstkontrollsinformation måste användaren som är inloggad på CRXDE Lite ha behörighet att läsa ACL-poster.

### Fliken Replikering {#replication-tab}

The **Fliken Replikering** visar den aktuella nodens replikeringsstatus. Du kan replikera och replikera borttagningen av den aktuella noden.

### Fliken Konsol {#console-tab}

The **Fliken Konsol** visar loggmeddelanden. Du kan konfigurera loggnivån, rensa konsolen, fästa vid den valda rullningspositionen och aktivera/inaktivera visning av meddelanden.

### Fliken Build Info {#build-info-tab}

The **Fliken Build Info** visar information när ett paket byggs.

### Knappen Uppdatera {#refresh-button}

The **Knappen Uppdatera** uppdaterar den aktuella markeringen. Ändringar från andra användare uppdateras i din vy av databasen. De ändringar du har gjort påverkas inte.

### Spara alla, knapp {#save-all-button}

The **Spara alla, knapp** sparar alla ändringar du har gjort. Ändringarna är tillfälliga tills du väljer att spara och försvinner när du avslutar konsolen.

* **Återställ** - Ignorerar alla ändringar som du har gjort på den valda noden sedan den senaste Spara-åtgärden och läser sedan in databasens aktuella status för den valda noden igen
* **Återställ alla** - Ignorerar alla ändringar som du har gjort i hela databasen sedan den senaste sparåtgärden och läser sedan in databasens aktuella läge igen

### Skapa-knapp {#create-button}

The **Skapa-knapp** är en nedrullningsbar meny som skapar följande under den markerade noden:

* Nod - en nod med en godtycklig nodtyp
* Fil - en `nt:file` nod och nod:resursundernod
* Mapp - en `nt:folder` nod

### Ta bort-knapp {#delete-button}

The **Ta bort-knapp** tar bort den markerade noden.

### Knappen Kopiera {#copy-button}

The **Knappen Kopiera** kopierar den markerade noden.

## Knappen Klistra in {#paste-button}

The **Knappen Klistra in** klistrar in den kopierade noden under den markerade noden.

### Flytta-knapp {#move-button}

The **Flytta-knapp** flyttar den markerade noden till den nod som anges i dialogrutan.

### Byt namn {#rename-button}

The **Byt namn på knapp** byter namn på den markerade noden.

### Blandningar {#mixins-button}

The **Knappen Blandningar** gör att du kan lägga till blandningstyper i nodtypen. Blandningstyperna används oftast för att lägga till avancerade funktioner.

### verktyg {#tools-button}

The **Verktygsknapp** är en rullgardinsmeny med följande verktyg tillgängliga:

* **Serverkonfiguration** - för åtkomst till Felix Console (finns även på `https://<host>:<port>/system/console/configMgr`)
* **Fråga** - för att fråga databasen
* **Behörighet** - för att visa och lägga till behörigheter
* **Testa åtkomstkontroll** - för att testa tillstånd för viss sökväg och/eller huvudman
* **Exportera nodtyp** - för att exportera nodtyper i systemet som CND-notation
* **Importera nodtyp** - om du vill importera nodtyper med CND-notation.

### Inloggningswidget {#login-widget}

The **Inloggningswidget** visar den inloggade användaren.

Klicka på den för att logga in eller logga in igen som en annan användare. The `@crx.default` används för att visa att du befinner dig i standardarbetsytan (och endast) i databasen.

The **Inställningar** kan användas för att ställa in användargränssnittets språk och för att visa och anpassa snabbtangenterna för olika åtgärder som att spara, söka, skapa anteckningar osv.

## Skapa en mapp {#creating-a-folder}

Så här skapar du en mapp med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. I navigeringsrutan högerklickar du på den mapp under vilken du vill skapa den nya mappen, och väljer **Skapa ...** sedan **Skapa mapp...**.

1. Ange mappen **Namn** och klicka **OK**.

1. Klicka **Spara alla** för att spara ändringarna på servern.

## Skapa en nod {#creating-a-node}

Så här skapar du en nod med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. I [**Utforskarfönster**,](#explorer-pane) högerklicka på noden där du vill skapa den nya noden, välj **Skapa** sedan **Skapa nod**.
1. Ange **Namn** och väljer **Typ**.
1. Klicka **OK**.
1. Klicka på [**Spara alla, knapp**](#save-all-button) för att spara ändringarna på servern.

Nu kan du anpassa noden efter dina behov genom att ändra egenskaper eller skapa nya noder.

>[!NOTE]
>
De flesta redigeringsåtgärderna, inklusive **Skapa nod** sparar alla ändringar i minnet och lagrar dem endast i databasen när de sparas (med [**Spara alla, knapp**](#save-all-button)). Vissa åtgärder, till exempel move, sparas dock automatiskt.
>
Valideringen av om den nyskapade noden tillåts av den överordnade nodens nodtyp utförs även av databasen när ändringar sparas. Om du får ett felmeddelande när du sparar en nod kontrollerar du om innehållsstrukturen är giltig (du kan till exempel inte skapa en `nt:unstructured` nod som underordnad till `nt:folder` nod).

## Skapa en egenskap {#creating-a-property}

Så här skapar du en egenskap med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. I [**Utforskarfönster**,](#explorer-pane) markera noden där du vill lägga till den nya egenskapen.
1. I [**Fliken Egenskaper**](#properties-tab) i den nedre rutan anger du **Namn**, **Typ** och **Värde**.
1. Klicka **Lägg till**.
1. Klicka på [**Spara alla, knapp**](#save-all-button) för att spara ändringarna på servern.

## Skapa en fil {#creating-a-file}

Så här skapar du en ny fil med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. I [**Utforskarfönster**,](#explorer-pane) högerklicka på komponenten där du vill skapa filen, välj **Skapa** sedan **Skapa fil**.
1. Ange filen **Namn** inklusive dess förlängning.
1. Klicka **OK**.
1. Den nya filen öppnas som en flik i [**Redigeringsruta**.](#edit-pane)
1. Redigera filen.
1. Klicka på [**Spara alla, knapp**](#save-all-button) för att spara ändringarna.

## Exportera och importera nodtyper {#exporting-and-importing-node-types}

Med CRXDE Lite kan du importera och/eller exportera nodtypsdefinitioner i [CND-notation (Compact Namespace and Node Type Definition)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Så här exporterar du en nodtypsdefinition i CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. Välj önskad nod.
1. Välj **verktyg** sedan **Exportera nodtyp**.
1. Definitionen visas i CND-notation på en ny flik i webbläsaren.
1. Spara informationen om det behövs.

Så här importerar du en nodtypsdefinition:

1. Öppna CRXDE Lite i webbläsaren.
1. Välj **verktyg** sedan **Importera nodtyp**.
1. En ny flik öppnas i [**Redigeringsruta**](#edit-pane) märkt **Importera nodtyp**.
1. Ange CND-notation för definitionen i textrutan i **Importera nodtyp** -fliken.
1. Kontrollera **Tillåt uppdatering** om du uppdaterar en befintlig definition.
1. Klicka **Importera**.

## Loggning {#logging}

Med CRXDE Lite kan du visa filen `error.log` som finns i filsystemet på `<aem-install-dir>/crx-quickstart/logs` och filtrera den med rätt loggnivå. Gör så här:

1. Öppna CRXDE Lite i webbläsaren.
1. I listrutan till höger om [**Fliken Konsol**](#console-tab) längst ned i fönstret väljer du **Serverloggar**.
1. Klicka på **Stoppa** -ikonen för att visa meddelandena.

Du kan:

* Justera loggparametrarna i Felix Console genom att klicka på **Loggningskonfigurationer** ikon.
* Rensa meddelandena genom att klicka på knappen **Rensa konsol** ikon.
* Fäst meddelandet vid den aktuella markeringen genom att klicka på knappen **Fäst konsol** ikon.
* Aktivera eller inaktivera visning av meddelanden genom att klicka på **Stoppa** ikon.
