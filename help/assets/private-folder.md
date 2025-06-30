---
title: Privata mappar för att dela resurser
description: Lär dig hur du skapar en privat mapp i  [!DNL Adobe Experience Manager Assets]  och delar den med andra användare och tilldelar olika behörigheter till dem.
contentOwner: Vishabh Gupta
role: User
feature: Collaboration
exl-id: d48f6daf-af81-4024-bff2-e8bf6d683b0c
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 1%

---

# Privat mapp i [!DNL Adobe Experience Manager Assets] {#private-folder}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/private-folder.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |

Du kan skapa en privat mapp i användargränssnittet [!DNL Adobe Experience Manager Assets] som är exklusivt tillgänglig för dig. Du kan dela den här privata mappen med andra användare och tilldela andra användare olika behörigheter. Beroende på vilken behörighetsnivå du tilldelar kan användare utföra olika åtgärder i mappen, till exempel visa resurser i mappen eller redigera resurserna.

>[!NOTE]
>
>Den privata mappen har minst en medlem med ägarrollen.
>
>Om du vill skapa en privat mapp måste du ha `Read`- och `Modify`-behörighet för den överordnade mappen som du skapar en privat mapp i. Om du inte är administratör är dessa behörigheter inte aktiverade som standard på `/content/dam`. I så fall måste du först skaffa dessa behörigheter för ditt användar-ID/din grupp innan du försöker skapa privata mappar.

## Skapa och dela privat mapp  {#create-share-private-folder}

Så här skapar och delar du en privat mapp:

1. Klicka på knappen **[!UICONTROL Create]** i verktygsfältet i [!DNL Assets]-konsolen och välj sedan **[!UICONTROL Folder]** på menyn.

   ![Skapa resursmapp](assets/create-folder.png)

1. Ange en `Title` och `Name` (valfritt) för mappen i dialogrutan **[!UICONTROL Create Folder]**.

   Markera kryssrutan **[!UICONTROL Private]** och klicka på **[!UICONTROL Create]**.

   ![chlimage_1-413](assets/create-private-folder.png)

   En privat mapp skapas. Du kan nu [lägga till resurser](add-assets.md#upload-assets) i mappen och dela mappen med andra användare eller grupper. Mappen visas inte för andra användare förrän du delar den och tilldelar behörigheter till dem.

1. Om du vill dela mappen markerar du mappen och klickar på **[!UICONTROL Properties]** i verktygsfältet.

1. På sidan **[!UICONTROL Folder Properties]** väljer du en användare eller grupp i listan **[!UICONTROL Add User]**, tilldelar en roll (`Viewer`, `Editor` eller `Owner`) i din privata mapp och klickar på **[!UICONTROL Add]**.

   ![assign-user-group](assets/assign-permissions-private-folder.png)

   Du kan tilldela olika roller, till exempel `Editor`, `Owner` eller `Viewer`, till användaren som du delar mappen med. Om du tilldelar användaren en `Owner`-roll har användaren `Editor`-behörighet för mappen. Dessutom kan användaren dela mappen med andra. Om du tilldelar en `Editor`-roll kan användaren redigera resurserna i din privata mapp. Om du tilldelar en visningsprogramroll kan användaren bara visa resurserna i din privata mapp.

   >[!NOTE]
   >
   >Den privata mappen har minst en medlem med rollen `Owner`. Administratören kan därför inte ta bort alla ägarmedlemmar från en privat mapp. Om du vill ta bort befintliga ägare (och själva administratören) från den privata mappen måste administratören lägga till en annan användare som ägare.

1. Klicka på **[!UICONTROL Save & Close]**. Beroende på vilken roll du tilldelar tilldelas användaren en uppsättning behörigheter i din privata mapp när användaren loggar in på [!DNL Assets].
1. Klicka på **[!UICONTROL Ok]** för att stänga bekräftelsemeddelandet.
1. Användaren som du delar mappen med får ett delningsmeddelande i användargränssnittet.

1. Klicka på [!UICONTROL Notifications] för att öppna en lista med meddelanden.

   ![meddelande](assets/notification-icon.png)

1. Klicka på posten för den privata mappen som delas av administratören för att öppna mappen.

## Borttagning av privata mappar {#delete-private-folder}

Du kan ta bort en mapp genom att markera mappen och välja alternativet [!UICONTROL Delete] på den översta menyn, eller genom att använda backstegstangenten på tangentbordet.

![borttagningsalternativ på den översta menyn](assets/delete-option.png)

>[!CAUTION]
>
>Om du tar bort en privat mapp från CRXDE Lite lämnas överflödiga användargrupper kvar i databasen.

>[!NOTE]
>
>Om du tar bort en mapp med metoden ovan från användargränssnittet tas även de associerade användargrupperna bort.
>
>Befintliga överflödiga, oanvända och automatiskt genererade användargrupper kan dock tas bort från databasen med metoden `clean` i JMX i författarinstansen (`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`).

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publicera Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
