---
title: Använda CRXDE Lite
description: CRXDE Lite är en del av AEM snabbstart och är tillgängligt för dig att komma åt och ändra databasen i dina lokala utvecklingsmiljöer i webbläsaren.
translation-type: tm+mt
source-git-commit: c40d668cb6dcf5c3e2d09504b547457306a99c85
workflow-type: tm+mt
source-wordcount: '1705'
ht-degree: 0%

---


# Använda CRXDE Lite {#using-crxde-lite}

CRXDE Lite är en del av AEM snabbstart och är tillgängligt för dig att komma åt och ändra databasen i dina lokala utvecklingsmiljöer i webbläsaren. Med CRXDE Lite kan du redigera filer, mappar, noder och egenskaper. Hela databasen är tillgänglig i det här lättanvända gränssnittet.

>[!NOTE]
>
>CRXDE Lite är endast tillgängligt i dina lokala utvecklingsmiljöer. Den är inte tillgänglig i AEM som Cloud Service.

## Komma igång med CRXDE Lite {#getting-started-with-crxde-lite}

Så här kommer du igång med CRXDE Lite:

1. Kom igång snabbt med utvecklingen av AEM.
1. Öppna URL:en `https://<host>:<port>/crx/de` i webbläsaren.
1. Ange ditt **användarnamn** och **lösenord**.
1. Klicka på **OK**.

Användargränssnittet CRXDE Lite ser ut så här i webbläsaren:

![Gränssnittet CRXDE Lite](assets/crxde-lite.png)

Nu kan du använda CRXDE Lite för att utveckla programmet.

>[!TIP]
>
>Du kan också öppna CRXDE Lite från AEM-menyn. På huvudmenyn väljer du **Verktyg** -> **Allmänt** -> **CRXDE Lite**.

## Översikt över användargränssnittet {#overview-of-the-user-interface}

CRXDE Lite användargränssnitt har många delar och många funktioner.

### Övre växlingsfält {#top-switcher-bar}

Med det övre växlingsfältet kan du snabbt växla mellan CRXDE Lite, Pakethanteraren och Paketdelning.

### Node Path Widget {#node-path-widget}

Widgeten Nodsökväg visar sökvägen till den markerade noden.

Du kan också använda den för att hoppa till en nod genom att ange sökvägen manuellt eller klistra in den någon annanstans och trycka på Retur.

Det finns även stöd för att söka efter noder med ett specifikt nodnamn. Ange namnet på noden som du vill söka efter och vänta (eller välj sökikonen till höger). Om en viss nod eller noder läses in i utforskarrutan visas listan och du kan välja sökvägen och trycka på Retur för att navigera till den. Observera att det bara fungerar för de noder som för närvarande är inlästa i CRXDE-klientprogrammet i webbläsaren. Om du vill söka i hela databasen använder du **Verktyg** -&amp;gt: **Fråga**.

### Utforskarfönstret {#explorer-pane}

Utforskarpanelen **visar ett träd med alla noder i databasen.**

Klicka på en nod för att visa dess egenskaper på fliken **Egenskaper**. När du har klickat på en nod kan du välja en åtgärd i verktygsfältet. Klicka på noden igen för att byta namn på den.

Med Trädnavigeringsfilter (ikonen för kikaren) kan du filtrera noderna i databasen som namnet innehåller indatatexten för. Det gäller endast noder som har lästs in lokalt.

### Redigera ruta {#edit-pane}

Med **redigeringsfönstret** kan du visa innehållet i den markerade filen i databasen. Varje fil som öppnas visas som en egen flik i rutan.

På fliken **Hem** kan du söka efter innehåll och/eller dokumentation och komma åt utvecklardokumentation och stöd för Adobe.

Dubbelklicka på en fil i rutan **Utforskaren** för att visa dess innehåll i rutan **Redigera**. Du kan sedan ändra den och spara ändringarna.

När en fil har redigerats i **redigeringsrutan** är följande verktyg tillgängliga i verktygsfältet:

* **Visa i träd**  - Visar filen i databasträdet.
* **Sök/ersätt**  - Utför en sökning eller ersättning.

Dubbelklicka på statusraden i dialogrutan **Redigera ruta** så öppnas dialogrutan **Gå till rad** där du kan ange ett visst radnummer.

### Fliken Egenskaper {#properties-tab}

På fliken **Egenskaper** visas egenskaperna för den nod som du har valt. Du kan lägga till nya eller ta bort befintliga egenskaper.

### Åtkomstkontrollfliken {#access-control-tab}

På fliken **Åtkomstkontroll** visas behörigheter baserat på den aktuella sökvägen, databasen eller säkerhetsobjektet.

Behörigheterna är indelade i följande kategorier.

* **Tillämplig åtkomstkontrollprincip**  - de principer som kan tillämpas på det aktuella urvalet
* **Lokala åtkomstkontrollprinciper**  - De aktuella principer som tillämpas lokalt på den aktuella markeringen
* **Effektiva åtkomstkontrollprinciper**  - De aktuella principer som används för den aktuella markeringen, som kan anges lokalt eller ärvs från överordnade noder

>[!NOTE]
För att kunna se åtkomstkontrollsinformation måste användaren som är inloggad på CRXDE Lite ha behörighet att läsa ACL-poster.

### Replikeringsflik {#replication-tab}

På fliken **Replikering** visas den aktuella nodens replikeringsstatus. Du kan replikera och replikera borttagningen av den aktuella noden.

###  Konsolflik {#console-tab}

På fliken **Konsol** visas loggmeddelanden. Du kan konfigurera loggnivån, rensa konsolen, fästa vid den valda rullningspositionen och aktivera/inaktivera visning av meddelanden.

### Fliken Build Info {#build-info-tab}

På fliken **Bygginformation** visas information när ett paket skapas.

### Uppdatera knapp {#refresh-button}

Knappen **Uppdatera** uppdaterar den aktuella markeringen. Ändringar från andra användare uppdateras i din vy av databasen. De ändringar du har gjort påverkas inte.

### Spara alla, knapp {#save-all-button}

Knappen **Spara alla** sparar alla ändringar du har gjort. Tills du väljer att spara är ändringarna tillfälliga och försvinner när du avslutar konsolen.

* **Återställ**  - Ignorerar alla ändringar som du har gjort på den valda noden sedan den senaste sparandeåtgärden och läser sedan in det aktuella läget för databasen för den valda noden igen
* **Återställ alla** - Ignorerar alla ändringar som du har gjort i hela databasen sedan den senaste sparåtgärden och läser sedan in databasens aktuella status igen

### Skapa knapp {#create-button}

**Skapa-knappen** är en nedrullningsbar meny som skapar följande under den markerade noden:

* Nod - en nod med en godtycklig nodtyp
* Fil - en `nt:file`-nod och dess nt:resource-undernod
* Mapp - en `nt:folder`-nod

### Ta bort knapp {#delete-button}

**Ta bort-knappen** tar bort den markerade noden.

### Kopiera knapp {#copy-button}

Knappen **Kopiera** kopierar den markerade noden.

## Klistra in knapp {#paste-button}

Med knappen **Klistra in** klistras den kopierade noden in under den markerade noden.

### Flytta-knapp {#move-button}

**Flytta-knappen** flyttar den markerade noden till den nod som är angiven i dialogrutan.

### Byt namn på {#rename-button}

**Byt namn på knapp** byter namn på den markerade noden.

### Blandningar {#mixins-button}

Med knappen **Mixins** kan du lägga till blandningstyper i nodtypen. Blandningstyperna används oftast för att lägga till avancerade funktioner.

### Verktyg {#tools-button}

**Verktygsknappen** är en listruta med följande verktyg:

* **Server Config** - för åtkomst till Felix Console (finns också på  `https://<host>:<port>/system/console/configMgr`)
* **Fråga**  - för att fråga databasen
* **Behörigheter**  - för att visa och lägga till behörigheter
* **Testa åtkomstkontroll**  - för att testa behörighet för vissa sökvägar och/eller huvudnamn
* **Exportera nodtyp**  - för att exportera nodtyper i systemet som CND-notation
* **Importera nodtyp**  - för att importera nodtyper med CND-notation.

### Inloggningswidget {#login-widget}

I **inloggningswidgeten** visas den inloggade användaren.

Klicka på den för att logga in eller logga in igen som en annan användare. `@crx.default` representerar att du är i standardarbetsytan (och endast) i databasen.

Alternativet **Inställningar** kan användas för att ställa in användargränssnittets språk och för att visa och anpassa snabbtangenterna för olika åtgärder som att spara, söka, skapa anteckning osv.

## Skapar en mapp {#creating-a-folder}

Så här skapar du en mapp med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. I navigeringsrutan högerklickar du på den mapp under vilken du vill skapa den nya mappen och väljer **Skapa ...** och sedan **Skapa mapp ...**.

1. Ange mappen **Namn** och klicka på **OK**.

1. Klicka på **Spara alla** för att spara ändringarna på servern.

## Skapa en nod {#creating-a-node}

Så här skapar du en nod med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. I rutan [**Utforskaren**,](#explorer-pane) högerklickar du på den nod där du vill skapa den nya noden, väljer **Skapa** och **Skapa nod**.
1. Ange **Namn** och välj **Typ**.
1. Klicka på **OK**.
1. Klicka på [**Spara alla-knappen**](#save-all-button) för att spara ändringarna på servern.

Nu kan du anpassa noden efter dina behov genom att ändra egenskaper eller skapa nya noder.

>[!NOTE]
De flesta redigeringsåtgärderna, inklusive **Skapa nod**, sparar alla ändringar i minnet och lagrar dem bara i databasen när de sparas (med knappen [**Spara alla**](#save-all-button)). Vissa åtgärder, till exempel move, sparas dock automatiskt.
Valideringen av om den nyskapade noden tillåts av den överordnade nodens nodtyp utförs även av databasen när ändringar sparas. Om du får ett felmeddelande när du sparar en nod kontrollerar du om innehållsstrukturen är giltig (du kan t.ex. inte skapa en `nt:unstructured`-nod som underordnad `nt:folder`-nod).

## Skapar en egenskap {#creating-a-property}

Så här skapar du en egenskap med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. I rutan [**Utforskaren**](#explorer-pane) väljer du den nod där du vill lägga till den nya egenskapen.
1. På fliken [**Egenskaper**](#properties-tab) i den nedre rutan anger du **Namn**, **Typ** och **Värde**.
1. Klicka på **Lägg till**.
1. Klicka på [**Spara alla-knappen**](#save-all-button) för att spara ändringarna på servern.

## Skapar en fil {#creating-a-file}

Så här skapar du en ny fil med CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. I rutan [**Utforskaren**,](#explorer-pane) högerklickar du på komponenten där du vill skapa filen, väljer **Skapa** och **Skapa fil**.
1. Ange filen **Namn** inklusive filnamnstillägget.
1. Klicka på **OK**.
1. Den nya filen öppnas som en flik i [**redigeringsfönstret**.](#edit-pane)
1. Redigera filen.
1. Klicka på [**Spara alla-knappen**](#save-all-button) för att spara ändringarna.

## Exportera och importera nodtyper {#exporting-and-importing-node-types}

Med CRXDE Lite kan du importera och/eller exportera nodtypsdefinitioner i [CND-notationen ](https://jackrabbit.apache.org/jcr/node-type-notation.html) (Compact Namespace and Node Type Definition).

Så här exporterar du en nodtypsdefinition i CRXDE Lite:

1. Öppna CRXDE Lite i webbläsaren.
1. Välj önskad nod.
1. Välj **Verktyg** och sedan **Exportera nodtyp**.
1. Definitionen visas i CND-notation på en ny flik i webbläsaren.
1. Spara informationen om det behövs.

Så här importerar du en nodtypsdefinition:

1. Öppna CRXDE Lite i webbläsaren.
1. Välj **Verktyg** och sedan **Importera nodtyp**.
1. En ny flik öppnas i rutan [**Redigera**](#edit-pane) med etiketten **Importera nodtyp**.
1. Ange CND-notation för definitionen i textrutan på fliken **Importera nodtyp**.
1. Markera **Tillåt uppdatering** om du uppdaterar en befintlig definition.
1. Klicka på **Importera**.

## Loggar {#logging}

Med CRXDE Lite kan du visa filen `error.log` som finns i filsystemet på `<aem-install-dir>/crx-quickstart/logs` och filtrera den med rätt loggnivå. Gör så här:

1. Öppna CRXDE Lite i webbläsaren.
1. Välj **Serverloggar** i listrutan till höger om fliken [**Konsol**](#console-tab) längst ned i fönstret.
1. Klicka på ikonen **Stopp** för att visa meddelandena.

Du kan:

* Justera loggparametrarna i Felix Console genom att klicka på ikonen **Loggningskonfigurationer**.
* Rensa meddelandena genom att klicka på ikonen **Rensa konsol**.
* Fäst meddelandet vid den aktuella markeringen genom att klicka på ikonen **Fäst konsol**.
* Aktivera eller inaktivera visningen av meddelanden genom att klicka på ikonen **Stoppa**.
