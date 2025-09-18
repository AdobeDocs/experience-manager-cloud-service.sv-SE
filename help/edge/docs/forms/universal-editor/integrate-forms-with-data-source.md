---
title: Hur integrerar man FDM (Form Data Model) för ett formulär i den universella redigeraren?
description: Lär dig skapa formulär för kantleveranstjänster baserade på en formulärdatamodell (FDM). Generera och redigera exempeldata för datamodellsobjekt i FDM.
feature: Edge Delivery Services, Form Data Model
role: Admin, User
exl-id: 9ce51223-57d0-47d8-8868-84b37d4e8e3e
source-git-commit: 7d3ea5bdc6545b9610f595660fcfb2ef70c837de
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---


# Integrera Forms med FDM (Form Data Model)

Koppla formulären till backend-datakällor med FDM för att aktivera arbetsflöden för databindning, validering och inlämning.

## Förutsättningar

Utför dessa steg innan du integrerar FDM med formulären:

1. **[Konfigurera Data Source](/help/forms/configure-data-sources.md)**: Konfigurera backend-anslutningar
2. **[Skapa formulärdatamodell](/help/forms/create-form-data-models.md)**: Definiera datastruktur och tjänster
3. **[Konfigurera datamodellsobjekt](/help/forms/work-with-form-data-model.md)**: Mappa datarelationer

## Överväganden

Om ikonen **Datakällor** inte visas i det universella redigeringsgränssnittet eller egenskapen **Bind referens** i den högra egenskapspanelen aktiverar du tillägget **Datakälla** i **Extension Manager** .

![Skärmbild av Extension Manager-gränssnittet i Universal Editor som visar tillgängliga tillägg, inklusive tillägget Datakällor som kan aktiveras för formulärintegrering](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

Läs artikeln [Extension Manager Feature Highlights](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) om du vill veta hur du aktiverar och inaktiverar tillägg i den universella redigeraren.

## Välj formulärtyp

Universal Editor har stöd för två metoder för att skapa formulär:

| Proportioner | Schemabaserat formulär | Icke-schemabaserat formulär |
|--------|-------------------|----------------------|
| **Konfigurera komplexitet** | Enkel (automatisk bindning) | Manuell (fält-för-fält-bindning) |
| **Använd skiftläge** | Nya formulär med definierad datastruktur | Befintliga blanketter eller flexibla krav |
| **Data Source** | Krävs vid skapande | Kan läggas till senare |
| **Bindning** | Automatisk fältbindning | Manuell bindning per fält |

![Typer av formulär i Universal Editor](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

## Schemabaserat formulär

Schemabaserade formulär konfigurerar automatiskt datakällor och binder formulärfält till data. Det här arbetssättet är idealiskt för nya formulär med väldefinierade datastrukturer.

### Skapa schemabaserat formulär

1. **Åtkomst till Forms Console**
   - Logga in på din [!DNL Experience Manager Forms] Author-instans
   - Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**

2. **Börja skapa formulär**
   - Välj **[!UICONTROL Create]** > **[!UICONTROL Adaptive Forms]**
   - Välja en Edge Delivery Services-mall
   - Klicka på **[!UICONTROL Create]** när den är aktiverad

   ![Edge Delivery Services-mall](/help/edge/assets/create-eds-forms.png)

3. **Konfigurera datamodell**
   - Gå till fliken **Data**
   - Välj **formulärdatamodell (FDM)** för flera datakällor eller **JSON-schema** för ett enda serverdelssystem
   - Välj en FDM-fil (t.ex. Pet Form Data Model)

   ![Välj formulärdatamodell](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)

4. **Slutför formulärinställning**
   - Ange **Namn** och **Titel**
   - Ange **GitHub-URL** (t.ex. `https://github.com/wkndforms/edsforms`)
   - Klicka på **[!UICONTROL Create]**

   ![Skapa schemabaserat formulär](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

### Verifiera schemabaserat formulär

Formuläret öppnas i Universal Editor med förkonfigurerad databindning:

![Skärmbild av den universella redigeraren som visar ett schemabaserat formulär med förifyllda formulärfält och Content Browser som visar tillgängliga datakällelement](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

![Automatisk databindning](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## Icke-schemabaserat formulär

Formulär som inte är scheman kräver manuell konfiguration av datakälla och fältbindning. Detta ger flexibilitet för befintliga blanketter eller komplexa krav.

### Skapa icke-schemabaserat formulär

1. **Åtkomst till formuläregenskaper**
   - Logga in på din [!DNL Experience Manager Forms] Author-instans
   - Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**
   - Markera formuläret och klicka på **[!UICONTROL Properties]**

   ![Öppna formuläregenskaper](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

2. **Konfigurera formulärmodell**
   - Öppna fliken **Formulärmodell**
   - Välj **FDM (Form Data Model)** i listrutan **Välj från**
   - Välj din FDM i listan

   ![Välj fliken Formulärmodell](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

   ![Välj FDM](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

3. **Bekräfta konfiguration**
   - Klicka på **OK** i varningsmeddelandet
   - Klicka på **[!UICONTROL Save & Close]**

   ![Formulärmodellguiden](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

### Lägg till dataelement

1. **Öppna formulär för redigering**
   - Formuläret öppnas i Universal Editor

   ![Icke schemabaserad formulärredigering](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

2. **Få åtkomst till data i Source Elements**
   - Gå till fliken **[!UICONTROL Datasource]** i **[!UICONTROL Content Browser]**
   - Visa tillgängliga dataelement från din FDM

   ![Formulärdata, Source](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

3. **Lägg till element i formulär**
   - Markera dataelement och klicka på **[!UICONTROL Add]**
   - Eller bygg formuläret genom att dra och släppa element

   ![Lägg till dataelement](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   ![Skärmbild som visar den universella redigeraren med ett icke-schemaformulär som byggs genom att dataelement dras och släpps från fliken Data Source till formulärstrukturen](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

### Lägg till manuell databindning

För befintliga formulärfält lägger du till databindning via egenskapen **Bindningsreferens** :

1. **Öppna fältegenskaper**
   - Välj formulärfält för bindning
   - Öppna egenskapspanelen

2. **Konfigurera bindningsreferens**
   - Gå till egenskapen **Bindningsreferens**
   - Klicka på ikonen **Bläddra**

   ![Lägg till dataindrag manuellt för ett formulärfält](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

3. **Markera dataelement**
   - Välj från datakällträdet i guiden **Välj en bindningsreferens**
   - Markera det önskade dataelementet och klicka på **Markera**

   ![välj databindningsreferens](/help/edge/docs/forms/universal-editor/assets/select-bind-reference.png)

   ![välj dataelement](/help/edge/docs/forms/universal-editor/assets/select-data-element.png)

4. **Verifiera bindning**
   - Formulärfältet binds nu till dataelementet
   - Bindningen visas i egenskapen **Bind Reference**

   ![Automatisk databindning](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## Verifiera integrering

När integreringen är klar:

1. **Testa databindning**: Verifiera att formulärfälten visar korrekta data
2. **Verifiera inskickade data**: Se till att data sparas i konfigurerade källor
3. **Kontrollera felhantering**: Testa med ogiltiga datscenarier

## Nästa steg

Konfigurera [skicka-åtgärder](/help/edge/docs/forms/universal-editor/submit-action.md) för att slutföra formulärarbetsflödet.
