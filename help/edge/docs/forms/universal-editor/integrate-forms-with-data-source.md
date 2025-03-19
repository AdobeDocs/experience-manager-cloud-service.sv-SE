---
title: Hur integrerar man FDM (Form Data Model) för ett formulär i den universella redigeraren?
description: Lär dig skapa formulär baserade på en formulärdatamodell (FDM). Generera och redigera exempeldata för datamodellsobjekt i FDM.
feature: Edge Delivery Services, Form Data Model
role: Admin, User
hide: true
hidefromtoc: true
exl-id: 9ce51223-57d0-47d8-8868-84b37d4e8e3e
source-git-commit: 381aad580762fe957e1dc1d5824e4d35098f1ca4
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 0%

---

# Integrera formulär med formulärdatamodellen i den universella redigeraren

Genom att integrera formulär med en formulärdatamodell (FDM) i den universella redigeraren kan du använda olika backend-datakällor för att skapa en formulärdatamodell (FDM). Du kan använda FDM (Form Data Model) som ett schema i olika formulärarbetsflöden. Konfigurera datakällorna och skapa en FDM (Form Data Model) som bygger på datamodellsobjekten och tjänsterna som finns i datakällorna.

## Övervägande

* Förifyllningstjänsten för formulär i Universal Editor stöds för närvarande inte.

## Förutsättningar

Innan du konfigurerar formuläret med formulärdatamodellen i den universella redigeraren måste du utföra följande steg:

* [Konfigurera Data Source](/help/forms/configure-data-sources.md): Konfigurera datakällan för att ansluta formuläret till backend-data.
* [Skapa formulärdatamodell (FDM)](/help/forms/create-form-data-models.md): Skapa en datamodell med dataobjekt och tjänster från den konfigurerade datakällan.
* [Konfigurera datamodellsobjekt och datatjänster](/help/forms/work-with-form-data-model.md): Mappa datamodellsobjekt och datatjänster för att säkerställa ett jämnt dataflöde mellan formuläret och datakällan.

## Skapa Forms med formulärdatamodell i Universal Editor

I den universella redigeraren kan du skapa:
* [Schemabaserat formulär](#schema-based-form): Ett schemabaserat formulär använder en datakälla som konfigurerats när formuläret skapas på fliken **Data** och binder automatiskt data till formulärfält.
* [Icke schemabaserat formulär](#non-schema-based-form): Ett icke schemabaserat formulär kräver att du manuellt lägger till en datakälla och binder varje fält från innehållsträdet.

![Typer av formulär i Universal Editor](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

Dessa metoder ger er flexibilitet att koppla samman datamodeller med formulär baserat på era behov.

### Schemabaserat formulär

När du skapar ett schemabaserat formulär konfigureras det automatiskt med en datakälla, och formulärfälten länkas redan till data via databindningar. Så här skapar du ett schemabaserat formulär med hjälp av guiden Skapa formulär:

1. Logga in på din [!DNL Experience Manager Forms] Author-instans.
2. Ange dina inloggningsuppgifter på Experience Manager inloggningssida. När du är inloggad väljer du **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** i det övre vänstra hörnet.
3. Välj **[!UICONTROL Create]** > **[!UICONTROL Adaptive Forms]**. Guiden öppnas. På fliken **Source** väljer du en mall:

   ![Edge Delivery Services-mall](/help/edge/assets/create-eds-forms.png)

   När du väljer en Edge Delivery Services-baserad mall aktiveras knappen **[!UICONTROL Create]**. Du kan gå till flikarna **[!UICONTROL Data Source]** eller **[!UICONTROL Submission]** för att välja en datakälla eller skicka-åtgärd.

4. På fliken **Data** kan du välja någon av följande datamodeller:

   * **Formulärdatamodell (FDM)**: Integrera datamodellsobjekt och datatjänster från datakällor i formuläret. Välj FDM (Form Data Model) om formuläret kräver att du läser och skriver data från flera källor.

   * **JSON-schema**: Integrera formuläret med ett serverdelssystem genom att associera ett JSON-schema som definierar datastrukturen. Det gör att du kan lägga till dynamiskt innehåll med schemaelementen.

     Välj till exempel den skapade formulärdatamodellen Pet Form Data Model.

     ![Välj formulärdatamodell](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)


     Som standard markeras och konverteras alla fält i det associerade JSON-schemat eller formulärdatamodellen (FDM) automatiskt till motsvarande formulärkomponenter, vilket förenklar redigeringsprocessen. I guiden kan du också välja vilka fält som ska inkluderas i formuläret med hjälp av kryssrutor.

5. Klicka på **[!UICONTROL Create]** så visas guiden **Skapa formulär**.
6. Ange **Namn** och **Titel**.
7. Ange **GitHub-URL**. Om din GitHub-databas till exempel har namnet `edsforms`, finns den under kontot `wkndforms`, är URL:en:
   `https://github.com/wkndforms/edsforms`
8. Klicka på **[!UICONTROL Create]**.

   ![Skapa schemabaserat formulär](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

   När du klickar på **[!UICONTROL Create]** öppnas formuläret i Universell redigerare för redigering.

   ![författare till formuläret](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

   Formuläret skapas med dataelementen från den associerade datakällan, där formulärfälten har förkonfigurerad databindning.

   ![Automatisk databindning](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

   Du kan nu lägga till och [konfigurera åtgärden ](/help/edge/docs/forms/universal-editor/submit-action.md) för att skicka formulär.

### Icke-schemabaserat formulär

När du skapar ett icke schemabaserat formulär konfigureras ingen datakälla. Du kan redigera formuläregenskaperna senare för att lägga till en datakälla och manuellt konfigurera databindningar för formulärfälten. Utför följande steg för att redigera formuläregenskaperna och lägga till en datakälla:

1. Logga in på din [!DNL Experience Manager Forms] Author-instans.
1. Ange dina inloggningsuppgifter på Experience Manager inloggningssida. När du är inloggad väljer du **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** i det övre vänstra hörnet.
1. Markera formuläret som du vill lägga till datakälla för och klicka på **[!UICONTROL Properties]**.
   ![Öppna formuläregenskaper](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

   Formuläregenskaperna öppnas.
1. Klicka för att öppna fliken **Formulärmodell** och från listrutan **Välj från**. Du kan välja något av följande alternativ:

   * **Formulärdatamodell (FDM)**: Skapa formuläret med en formulärdatamodell.
   * **Koppling**: Skapa formuläret med datakällan för Adobe Marketo.
   * **Schema**: Skapa formuläret med ett JSON-schema som har överförts till AEM Forms.
   * **Inget**: Skapa formuläret från grunden utan att använda någon formulärmodell.

     Välj till exempel formulärdatamodellen (FDM)

     ![Välj fliken Formulärmodell](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

1. Välj den skapade formulärdatamodellen (FDM) i listrutan. Välj till exempel den skapade formulärdatamodellen Pet Form Data Model i listrutan.

   ![Välj FDM](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

   När du väljer formulärdatamodellen (FDM) visas varningsmeddelandet. Klicka på **OK** för att stänga dialogrutan.

   ![Formulärmodellguiden](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

1. Klicka på **[!UICONTROL Save & Close]**.
1. Öppna formuläret för redigering. Formuläret öppnas i den universella redigeraren för redigering.

   ![Icke schemabaserad formulärredigering](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

   Formulärelementen i den associerade formulärdatamodellen (FDM) visas på fliken **[!UICONTROL Datasource]** i **[!UICONTROL Content Browser]** på **egenskapspanelen**.

   ![Formulärdata, Source](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

1. Markera dataelementen på fliken **[!UICONTROL Datasource]** och klicka på **[!UICONTROL Add]**.

   ![Lägg till dataelement](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   Du kan också dra och släppa dessa element för att skapa ett anpassat formulär. När du klickar på **[!UICONTROL Add]** läggs de markerade elementen på fliken **[!UICONTROL Datasource]** till i formuläret, och en bock visas framför de tillagda elementen.

   ![Skapa formulär](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

   Du måste lägga till databindning manuellt till ett formulärelement genom att ange den i egenskaperna **Bindningsreferens** för formulärelementet.
Låt oss till exempel lägga till en databindningsreferens i textrutan **Pet Name** som redan finns i formuläret:

   ![Lägg till dataindrag manuellt för ett formulärfält](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

   Du kan nu lägga till och [konfigurera åtgärden ](/help/edge/docs/forms/universal-editor/submit-action.md) för att skicka formulär.

## Se även

{{universal-editor-see-also}}
