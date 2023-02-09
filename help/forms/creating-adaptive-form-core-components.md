---
title: Hur skapar man ett adaptivt formulär?
description: Lär dig hur du skapar ett adaptivt formulär med [!DNL Experience Manager Forms]. Adaptiva Forms är responsiva HTML5-formulär som effektiviserar informationsinsamling och -bearbetning. Mer information om hur du skapar ett adaptivt formulär baserat på en formulärdatamodell och ett XML- eller JSON-schema.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
source-git-commit: 6f6cf5657bf745a2e392a8bfd02572aa864cc69c
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 0%

---


# Skapa en adaptiv form (kärnkomponenter) {#creating-an-adaptive-form-core-components}

Med adaptiva Forms kan du skapa engagerande, responsiva, dynamiska och anpassningsbara formulär. AEM Forms har en användarvänlig guide för att snabbt skapa Adaptiv Forms. Guiden har en snabb fliknavigering där du enkelt kan välja förkonfigurerade mallar, format, fält och alternativ för att skicka formulär för att skapa ett adaptivt formulär. Adaptiv Forms har två typer av komponenter:

* Adaptiva Forms Core-komponenter är standardiserade datainhämtningskomponenter. Dessa komponenter har anpassningsmöjligheter, kortare utvecklingstid och lägre underhållskostnader för era digitala registreringsupplevelser. Utvecklare kan enkelt anpassa dessa komponenter. Adobe rekommenderar att man utnyttjar dessa moderna och utbyggbara komponenter för att utveckla Adaptiv Forms.

* Adaptiva Forms Foundation-komponenter är klassiska (gamla) datainhämtningskomponenter.

I den här artikeln beskrivs det senaste sättet att skapa ett adaptivt formulär. Information om hur du skapar adaptiva Forms utifrån äldre metoder finns i [Skapa ett adaptivt formulär (grundkomponenter)](creating-adaptive-form.md)

![Guide för att skapa ett adaptivt formulär](/help/release-notes/assets/wizard.png)


## Krav

Du behöver följande för att skapa ett adaptivt formulär:

* **En anpassad formulärmall**: En mall innehåller en grundläggande struktur och definierar utseendet (layouter och format) för ett adaptivt formulär. Den har förformaterade komponenter som innehåller vissa egenskaper och innehållsstruktur. Här finns också alternativ för att definiera ett tema och en skicka-åtgärd. Temat definierar utseendet, känslan och skickaåtgärden definierar vilken åtgärd som ska vidtas när ett adaptivt formulär skickas in. Du kan till exempel skicka insamlade data till en datakälla. Molntjänsten tillhandahåller en OOTB-mall med namnet blank:

   * The `blank` -mallar ingår i alla nya as a Cloud Service AEM Forms-program.
   * Du kan installera referenspaketet via pakethanteraren för att lägga till `blank` till ditt as a Cloud Service AEM Forms-program.
   * Du kan också [skapa en ny adaptiv Forms-mall (kärnkomponenter)](template-editor.md) från scratch.

* **Ett adaptivt formulärtema**: Ett tema innehåller formatinformation för komponenterna och panelerna. Format innehåller egenskaper som bakgrundsfärger, lägesfärger, genomskinlighet, justering och storlek. När du använder ett tema återspeglas det angivna formatet i motsvarande komponenter.  The `Canvas` -mallar ingår i alla nya as a Cloud Service AEM Forms-program.

   <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create a new Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **Behörigheter**: Lägg till dina användare i [!DNL forms-users] grupp. Medlemmarna i [!DNL forms-users] gruppen har behörighet att skapa ett adaptivt formulär. En detaljerad lista över formulärspecifika användargrupper finns i [Grupper och behörigheter](forms-groups-privileges-tasks.md).


## Skapa en adaptiv form (kärnkomponenter) {#create-an-adaptive-form-core-components}

1. Logga in på [!DNL Experience Manager Forms] Författarinstans. Det kan vara en molninstans eller en lokal utvecklingsinstans.

1. Ange dina uppgifter på inloggningssidan för Experience Manager. När du är inloggad trycker du på **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.

1. Tryck på **[!UICONTROL Create]**  > **[!UICONTROL Adaptive Forms]**. Guiden öppnas. Välj en mall på fliken Källa:

   ![Kärnkomponentmall](/help/forms/assets/core-components-template.png)

   När du väljer en mall väljs automatiskt ett tema och en skicka-åtgärd som anges i mallen, och **[!UICONTROL Create]** knappen är aktiverad. Du kan gå till **[!UICONTROL Style]** eller **[!UICONTROL Submission]** för att välja ett annat tema eller skicka-åtgärd. Om den valda mallen inte anger något tema förblir knappen Skapa inaktiverad. Du kan gå till **[!UICONTROL Styles]** om du vill välja ett tema manuellt.

1. I **[!UICONTROL Style]** väljer du ett tema:

   * När den valda mallen anger ett tema väljs temat automatiskt i guiden. Du kan också välja ett annat tema på fliken Format.

   * Om den valda mallen inte anger något tema kan du använda fliken Format för att välja ett tema. The **[!UICONTROL Create]** knappen aktiveras först när ett tema har valts.

1. (Valfritt) Välj en datamodell på fliken Data:

   * **Formulärdatamodell**: A [Formulärdatamodell](data-integration.md) Med kan ni integrera enheter och tjänster från olika datakällor i ett adaptivt formulär. Välj Formulärdatamodell om det adaptiva formulär du skapar inbegriper att hämta och skriva data från och till flera datakällor.

   * **JSON-schema**: [JSON-schema](adaptive-form-json-schema-form-model.md) Vår Core-Components-baserade adaptiva form möjliggör smidig integrering med företagets back-end-system genom att ge möjlighet att associera ett JSON-schema, som representerar strukturen för de data som produceras eller konsumeras. Den här kopplingen gör det möjligt för författare att dynamiskt lägga till innehåll i det adaptiva formuläret med elementen i schemat. Elementen i schemat är enkelt tillgängliga på fliken Datamodellsobjekt i innehållsläsaren under redigeringsprocessen, och alla fält läggs automatiskt till i alla nya adaptiva formulär.

   Som standard markeras alla fält i det associerade JSON-schemat automatiskt och konverteras till motsvarande adaptiva formulärkomponenter, vilket effektiviserar redigeringsprocessen. I guiden kan du välja vilka fält som ska inkluderas i det anpassade formuläret med hjälp av kryssrutor.

1. I **[!UICONTROL Submission]** väljer du en Skicka-åtgärd:

   * När du väljer en mall markeras åtgärden Skicka som anges i mallen automatiskt. Du kan välja en annan skickaåtgärd på fliken Skicka. The **[!UICONTROL  Submission]** på -fliken visas alla tillgängliga skicka-åtgärder.

   * När den valda mallen inte anger någon skicka-åtgärd kan du använda **[!UICONTROL Submission]** flik för att välja en skicka-åtgärd

1. (Valfritt) I dialogrutan **[!UICONTROL Delivery]** kan du ange ett publicerings- eller avpubliceringsdatum för ett adaptivt formulär.

1. Tryck på **[!UICONTROL Create]**. En dialogruta där du kan ange namn, namn och plats för att spara det adaptiva formuläret visas:

   * **[!UICONTROL Title]** Anger formulärets visningsnamn. Titeln hjälper dig att identifiera formuläret i [!DNL Experience Manager Forms] användargränssnitt.
   * **[!UICONTROL Name:]** Anger formulärets namn. En nod med det angivna namnet skapas i databasen. När du börjar skriva en titel genereras värdet för namnfältet automatiskt. Du kan ändra det föreslagna värdet. Namnfältet får endast innehålla alfanumeriska tecken, bindestreck och understreck. Alla ogiltiga indata ersätts med ett bindestreck.
   * **[!UICONTROL Path:]** Anger platsen där det adaptiva formuläret ska sparas. Du kan spara det anpassade formuläret direkt på `/content/dam/formsanddocuments` eller skapa en mapp som `/content/dam/formsanddocuments/adaptiveforms` för att spara ett adaptivt formulär. Se till att du skapar mappen innan du använder den i sökvägen. The **[!UICONTROL Path]** skapas ingen mapp automatiskt.

1. Tryck på **[!UICONTROL Create]**. Ett adaptivt formulär skapas och öppnas i den adaptiva Forms-redigeraren. Redigeraren visar det innehåll som är tillgängligt i mallen.  Baserat på typen av adaptiv form finns formulärelementen i den associerade <!--XFA form template, XML schema or --> JSON-schema eller formulärdatamodell visas i **[!UICONTROL Data Model Objects]** -fliken i **[!UICONTROL Content Browser]** i sidlisten. Du kan också dra och släppa dessa element för att skapa ett anpassat formulär.

Nu kan du dra och släppa de adaptiva Forms Core-komponenterna till den adaptiva Forms-behållaren för att utforma och skapa formuläret.

## Tillgängliga adaptiva Forms Core-komponenter

Adaptiva Forms Core-komponenter är standardiserade datainhämtningskomponenter. Dessa komponenter har anpassningsmöjligheter, kortare utvecklingstid och lägre underhållskostnader för era digitala registreringsupplevelser. Följande kärnkomponenter är tillgängliga direkt:

* Adaptivt Forms-dragspel: Med dragspelsfunktionen kan användaren visa och dölja avsnitt av relaterat innehåll i en adaptiv form.

* Adaptiv Forms-knapp
* Adaptiv Forms-kryssrutegrupp
* Anpassad datumväljare för Forms
* Adaptiv Forms-nedrullningsbar lista
* Anpassad e-postinmatning från Forms
* Adaptiva Forms-filbilagor
* Anpassningsbara vågräta Forms-flikar
* Adaptiv Forms-bild
* Adaptiv inmatning av Forms-nummer
* Adaptiv Forms-panel
* Adaptiv Forms-alternativknapp
* Knapp för återställning av adaptiv Forms
* Adaptiv Forms-sändningsknapp
* Adaptiv telefoninmatning från Forms
* Adaptiv Forms-text
* Adaptiv Forms-textruta
* Adaptiv Forms-titel
* Adaptiv Forms-guidelayout
* Sidhuvud
* Sidfot

## Redigera formulärmodellegenskaper för ett adaptivt formulär {#edit-form-model}

1. Markera det adaptiva formuläret och tryck på ![Sidinformation](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Open Properties]**. Sidan Formuläregenskaper öppnas.

1. Gå till **[!UICONTROL Form Model]** och välj en formulärmodell. Om det adaptiva formuläret inte har någon formulärmodell kan du välja antingen ett JSON-schema eller en formulärdatamodell. Om det adaptiva formuläret däremot redan är baserat på en formulärmodell kan du växla till en annan formulärmodell av samma typ. Om formuläret till exempel använder ett JSON-schema kan du enkelt växla till ett annat JSON-schema, och på samma sätt kan du växla till en annan formulärdatamodell om formuläret använder en formulärdatamodell.

1. Tryck **[!UICONTROL Save]** för att spara egenskaperna.
