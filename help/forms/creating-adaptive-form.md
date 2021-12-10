---
title: Hur skapar man ett adaptivt formulär?
description: 'Lär dig hur du skapar ett adaptivt formulär med [!DNL Experience Manager Forms]. Adaptiva Forms är responsiva HTML5-formulär som effektiviserar informationsinsamling och -bearbetning. Mer information om hur du skapar ett adaptivt formulär baserat på en formulärdatamodell och ett XML- eller JSON-schema. '
feature: Adaptive Forms
role: User, Developer
level: Beginner
exl-id: 38ca5eea-793b-420b-ae60-3a0bd83caf00
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1444'
ht-degree: 0%

---

# Skapa ett adaptivt formulär {#creating-an-adaptive-form}

Med adaptiva Forms kan du skapa engagerande, responsiva, dynamiska och anpassningsbara formulär. [!DNL AEM Forms] har ett intuitivt användargränssnitt och färdiga komponenter för att skapa och arbeta med Adaptive Forms. Du kan välja att skapa ett adaptivt formulär baserat på en formulärmodell eller ett schema eller utan en formulärmodell. Det är viktigt att du noga väljer den formulärmodell som inte bara passar dina behov, utan som utökar dina befintliga infrastrukturinvesteringar och resurser. Du kan välja mellan följande alternativ för att skapa ett adaptivt formulär:

* **Använda en formulärdatamodell**
   [Dataintegrering](data-integration.md) Med kan du integrera enheter och tjänster från olika datakällor i en formulärdatamodell som du kan använda för att skapa adaptiv Forms. Välj Formulärdatamodell om det adaptiva formulär du skapar inbegriper hämtning och skrivning av data från och till flera datakällor.

   <!--  * **Using an XDP Form Template**
   It is an ideal form model if you have investments in XFA-based or XDP forms. It provides a direct way to convert your XFA-based forms into Adaptive Forms. Any existing XFA rules are retained in the associated Adaptive Forms. The resulting Adaptive Forms support XFA constructs, such as validations, events, properties, and patterns. -->

* **Använda en XSD (XML Schema Definition) eller ett JSON-schema**
XML- och JSON-scheman representerar den struktur i vilken data produceras eller förbrukas av organisationens serversystem. Du kan koppla schemat till ett adaptivt formulär och använda dess element för att lägga till dynamiskt innehåll i det adaptiva formuläret. Elementen i schemat kommer att vara tillgängliga för användning på fliken Datamodellobjekt i innehållsläsaren när du redigerar Adaptiv Forms.

* **Använda ingen eller utan en formulärmodell**
Adaptiv Forms som skapats med det här alternativet använder ingen formulärmodell. Data-XML som genereras från sådana formulär har en platt struktur med fält och motsvarande värden.

## Krav

Du behöver följande för att skapa ett adaptivt formulär:

* En adaptiv formulärmall. En mall innehåller en grundläggande struktur och definierar utseendet (layouter och format) för ett adaptivt formulär. Den har förformaterade komponenter som innehåller vissa egenskaper och innehållsstruktur Du kan [skapa en ny mall](template-editor.md), importera en befintlig mall eller hämta och importera [exempelmallar](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:3f89abe1-0ece-492a-b5af-57c73badad52).
* Ett adaptivt formulärtema. Ett tema innehåller formatinformation för komponenterna och panelerna. Format innehåller egenskaper som bakgrundsfärger, lägesfärger, genomskinlighet, justering och storlek. När du använder ett tema återspeglas det angivna formatet i motsvarande komponenter. Du kan [skapa ett nytt tema](themes.md), [importera ett befintligt tema](import-export-forms-templates.md#uploading-a-theme)eller hämta och importera [exempelteman](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:2779f80e-16ba-4cd1-a96f-8e2b53f3be25).
* Lägg till dina användare i [!DNL forms-users] för att ge dem behörighet att skapa ett adaptivt formulär. En detaljerad lista över formulärspecifika användargrupper finns i [Grupper och behörigheter](forms-groups-privileges-tasks.md).

## Skapa ett adaptivt formulär {#strong-create-an-adaptive-form-strong}

Följ de här stegen för att skapa ett adaptivt formulär.

1. Åtkomst [!DNL Experience Manager Forms] Författarinstans. Det kan vara en molninstans eller en lokal utvecklingsinstans.

1. Ange dina uppgifter på inloggningssidan för Experience Manager.

   När du är inloggad trycker du på **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.

1. Tryck **[!UICONTROL Create]** och markera **[!UICONTROL Adaptive Form]**. Välj en mall och tryck på **[!UICONTROL Next]**.
1. Ett alternativ till **[!UICONTROL Add Properties]** visas. Ange värdena för följande egenskapsfält. Fälten Titel och Namn är obligatoriska:

   * **[!UICONTROL Title:]** Anger formulärets visningsnamn. Titeln hjälper dig att identifiera formuläret i [!DNL Experience Manager Forms] användargränssnitt.
   * **[!UICONTROL Name:]** Anger formulärets namn. En nod med det angivna namnet skapas i databasen. När du börjar skriva en titel genereras värdet för namnfältet automatiskt. Du kan ändra det föreslagna värdet. Namnfältet får endast innehålla alfanumeriska tecken, bindestreck och understreck. Alla ogiltiga indata ersätts med ett bindestreck.
   * **[!UICONTROL Description:]** Anger detaljerad information om formuläret.
   * **[!UICONTROL Tags:]** Anger taggar som unikt identifierar den adaptiva formen. Taggar hjälper dig att söka i formuläret. Om du vill skapa taggar skriver du nya taggnamn i **[!UICONTROL Tags]** box.

1. Du kan skapa ett adaptivt formulär baserat på någon av följande formulärmodeller:

   * [Formulärdatamodell](#fdm)

   <!--* [XFA form template](#create-an-adaptive-form-based-on-an-xfa-form-template)-->
   * [XML- eller JSON-schema](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * Ingen eller utan någon formulärmodell

   Du kan konfigurera dessa från **[!UICONTROL Form Model]** på **[!UICONTROL Add Properties]** sida. Som standard är den valda formulärmodellen **[!UICONTROL None]**.

1. Tryck på **[!UICONTROL Create]**. Ett anpassat formulär skapas och en dialogruta öppnas där du kan öppna formuläret för redigering.

1. Tryck **[!UICONTROL Open]** om du vill öppna det nya formuläret på en ny flik. Formuläret öppnas för redigering och visar det innehåll som är tillgängligt i mallen. Här visas också sidlisten där du kan anpassa det nya formuläret efter behov.

   Baserat på typen av adaptiv form finns formulärelementen i den associerade <!--XFA form template, -->XML-schema eller JSON-schema visas i **[!UICONTROL Data Model Objects]** -fliken i **[!UICONTROL Content Browser]** i sidlisten. Du kan också dra och släppa dessa element för att skapa ett anpassat formulär.

## Skapa ett anpassat formulär baserat på en formulärdatamodell {#fdm}

[Dataintegrering](data-integration.md) Med kan du integrera flera datakällor och sammanföra deras enheter och tjänster för att skapa en formulärdatamodell. Det är ett tillägg till JSON-schemat. Du kan använda en formulärdatamodell för att skapa ett adaptivt formulär. Enheterna eller datamodellsobjekten som konfigurerats i en formulärdatamodell är tillgängliga som datamodellsobjekt för formulärutveckling. De är bundna till respektive datakällor och används för att fylla i ett formulär i förväg och skriva inlämnade data tillbaka till respektive datakälla. Du kan också anropa tjänster som konfigurerats i en formulärdatamodell med hjälp av regler för adaptiva formulär.

Så här använder du en formulärdatamodell för att skapa ett adaptivt formulär:

1. På fliken Formulärmodell på skärmen Lägg till egenskaper väljer du **[!UICONTROL Form Data Model]** i **[!UICONTROL Select From]** nedrullningsbar lista.

   ![Skapa ett adaptivt formulär](assets/create-af-1-1.png)

1. Tryck för att expandera **[!UICONTROL Select Form Data Model]**. Alla tillgängliga formulärdatamodeller visas.Välj en från datamodell.

>[!NOTE]
>
>Du kan också ändra formulärdatamodellen för ett adaptivt formulär. Detaljerade anvisningar finns i [Redigera formulärmodellegenskaper för ett adaptivt formulär](#edit-form-model).

## Skapa ett adaptivt formulär baserat på XML- eller JSON-schema {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML- och JSON-scheman representerar den struktur i vilken data produceras eller förbrukas av organisationens serversystem. Du kan koppla ett schema till ett adaptivt formulär och använda dess element för att lägga till dynamiskt innehåll i det adaptiva formuläret. Elementen i schemat är tillgängliga på fliken Datamodellsobjekt i innehållsläsaren för att skapa Adaptiv Forms. Du kan dra och släppa schemaelementen för att skapa formuläret.

Se följande dokument för att förstå hur du utformar XML- eller JSON-schema för att skapa Adaptive Forms.

* [Skapa adaptiv Forms med XML-schema](adaptive-form-xml-schema-form-model.md)
* [Skapa adaptiv Forms med JSON-schema](adaptive-form-json-schema-form-model.md)

Gör följande om du vill använda XML- eller JSON-schema som formulärmodell för ett adaptivt formulär:

1. På **[!UICONTROL Add Properties]** på sidan Skapa adaptiva formulär trycker du på **[!UICONTROL Form Model]** -fliken.
1. På fliken Formulärmodell väljer du **[!UICONTROL Schema]** från **[!UICONTROL Select From]** nedrullningsbart fält.

1. Tryck **[!UICONTROL Select Schema]** och gör något av följande:

   * **[!UICONTROL Upload from disk]** - Välj det här alternativet och tryck på Överför schemadefinition för att bläddra och överföra ett XML-schema eller JSON-schema från filsystemet. Den överförda schemafilen finns i formuläret och är inte tillgänglig för andra adaptiva Forms.
   * **[!UICONTROL Search in repository]** - Välj det här alternativet om du vill välja från listan med schemadefinitionsfiler som är tillgängliga i databasen. Välj XML- eller JSON-schemafilen som formulärmodell. Det valda schemat är kopplat till formuläret via referens och kan användas i andra adaptiva Forms.

      Kontrollera att JSON-schemats filnamn slutar med **.schema.json**. Till exempel: mySchema.schema.json
   ![Välja XML- eller JSON-schema](assets/upload-schema.png)
   **Bild:** *Välja XML- eller JSON-schema*

1. (Endast för XML-schema) När du har valt eller överfört ett XML-schema anger du ett rotelement för den markerade XSD-filen som ska mappas med det adaptiva formuläret.

   ![Välja XSD-rotelement](assets/xsd-root-element.png)
   **Bild:** *Välja XSD-rotelement*

>[!NOTE]
>
>Du kan också ändra schemat för ett anpassat formulär. Detaljerade anvisningar finns i [Redigera formulärmodellegenskaper för ett adaptivt formulär](#edit-form-model).

## Redigera formulärmodellegenskaper för ett adaptivt formulär {#edit-form-model}

Adaptiv Forms skapas utan formulärmodell (med alternativet Ingen för formulärmodellen) eller med en formulärmodell som <!-- form template, --> XML-schema, JSON-schema eller formulärdatamodell. Du kan ändra formulärmodellen för ett anpassat formulär från Ingen till en annan formulärmodell. För adaptiva formulär baserade på en formulärmodell kan du välja ett annat <!-- form template,--> XML-schema, JSON-schema eller formulärdatamodell för samma formulärmodell. Du kan dock inte ändra från en formulärmodell till en annan.

1. Markera det adaptiva formuläret och tryck på **Egenskaper** ikon.
1. Öppna **[!UICONTROL Form Model]** och gör något av följande.

   * Om det adaptiva formuläret inte har någon formulärmodell kan du välja en annan formulärmodell och därefter välja <!-- a form template, --> XML- eller JSON-schema eller formulärdatamodell.
   * Om det adaptiva formuläret är baserat på en formulärmodell kan du välja ett annat <!-- form template, --> XML- eller JSON-schema eller formulärdatamodell för samma formulärmodell.

1. Tryck **[!UICONTROL Save]** för att spara egenskaperna.
