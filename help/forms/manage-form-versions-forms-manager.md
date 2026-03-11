---
title: Hantera formulärversioner i Forms Manager
description: Lär dig att skapa och hantera versioner av adaptiva Forms, formulärfragment, teman och andra resurser i användargränssnittet för Forms Manager.
feature: Adaptive Forms, Core Components, Foundation Components
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="Gäller AEM Forms)."
exl-id: cd2c6e15-99a6-4b4e-bfd1-8291a2001ebe
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# Hantera formulär-Assets-versioner i användargränssnittet för Forms Manager

<span class="preview"> Den här funktionen är tillgänglig via programmet Tidig åtkomst. Om du vill begära åtkomst skickar du ett e-postmeddelande från din officiella adress till [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com). </span>

Forms Manager har nu stöd för versionshantering för formulärresurser. Du kan skapa versioner, visa versionshistorik och återställa tidigare versioner av dina resurser från användargränssnittet i Forms Manager.

## Tillgångstyper som stöds {#supported-asset-types}

Du kan skapa och hantera versioner för följande resurstyper:

| Tillgångstyp | Beskrivning |
|---|---|
| Adaptiv Forms (kärnkomponenter) | Adaptiv Forms byggd med kärnkomponenter |
| Adaptiv Forms (Foundation Components) | Adaptiv Forms byggd med Foundation Components |
| Formulärfragment | Återanvändbara formuläravsnitt som delas i flera formulär |
| Teman | Visuella formatdefinitioner som används i Adaptive Forms |
| XDP-mallar | XFA-baserade blankettmallar |
| Binära resurser | Andra filer som lagras i DAM-databasen |

## Skapa en version {#create-version-forms-manager}

Så här skapar du en version av en formulärresurs:

1. Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Markera formuläret eller resursen.
1. Välj **[!UICONTROL Timeline]** i den vänstra panelen.
1. Klicka på **[!UICONTROL Save as Version]** i verktygsfältet för tidslinje.
   ![Spara som version](/help/forms/assets/create-version.png)
1. Ange en **[!UICONTROL Label]** och en valfri **[!UICONTROL Comment]** som beskriver ändringarna.
1. Klicka på **[!UICONTROL Create]**.
   ![Spara som version2](/help/forms/assets/create-version1.png)

Versionen visas på tidslinjepanelen med etikett, kommentar och tidsstämpel.

## Version av en resurs under överföring {#version-on-upload}

När du överför en resurs med samma namn som en befintlig resurs visas dialogrutan **Filöverföring** i Forms Manager med en lista över de resurser som ska uppdateras. I dialogrutan visas resursnamnet, avsnittet och sökvägen.

När det redan finns en resurs med samma namn ersätter överföringen den befintliga resursen och skapar en ny version automatiskt. Du kan visa den skapade versionen på tidslinjen.

![Dialogrutan Filöverföring visar versionsuppladdning](/help/forms/assets/version-upload.png)

## Visa versionshistorik {#view-version-history}

Så här visar du versionshistoriken för en resurs:

1. Markera resursen i Forms Manager.
1. Välj **[!UICONTROL Timeline]** i den vänstra panelen.
   ![Versionshistorik](/help/forms/assets/version-history.png)

På tidslinjen visas alla versionsposter tillsammans med aktivitetshändelser. Varje post visar etikett, kommentar, författare och tidsstämpel.

## Återställa en tidigare version {#restore-version}

Så här återställer du en resurs till en tidigare version:

1. Markera resursen i Forms Manager.
1. Välj **[!UICONTROL Timeline]** i den vänstra panelen.
1. Välj den version som du vill återställa.
1. Klicka på **[!UICONTROL Revert to this Version]**.
   ![Återställ version](/help/forms/assets/revert-version.png)

>[!NOTE]
>
>Det går inte att återställa bilder till en tidigare version. Alla andra resurstyper, inklusive Adaptiv Forms, formulärfragment, teman och XDP-mallar, har stöd för versionsåterställning.

## Se även {#see-also}

* [Versionshantering, granskning och kommentering i ett adaptivt formulär](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)
* [Importera och exportera formulär och relaterade resurser](/help/forms/import-export-forms-templates.md)
* [Publicera och avpublicera formulär](/help/forms/publishing-unpublishing-forms.md)
