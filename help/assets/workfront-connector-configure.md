---
title: Konfigurera [!DNL Workfront for Experience Manager enhanced connector]
description: Konfigurera [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: d4e1247a-342c-4bc4-83bf-4e4902468fb3
source-git-commit: e49d536dc918861604f3e5d19608eb69d038c49a
workflow-type: tm+mt
source-wordcount: '1644'
ht-degree: 0%

---

# Konfigurera [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-configure.html) |
| AEM as a Cloud Service | Den här artikeln |

En användare med administratörsåtkomst i [!DNL Adobe Experience Manager] som [!DNL Cloud Service] konfigurerar den utökade anslutningen efter installation. Anvisningar om hur du installerar finns i [Installera anslutningsprogrammet](/help/assets/workfront-integrations.md).

>[!IMPORTANT]
>
> Från juni 2022 släppte Adobe en ny inbyggd integrering för att ansluta Workfront till Adobe Experience Manager Assets as a Cloud Service. Den här integreringen har blivit den metod som krävs för att ansluta dessa två lösningar. Eventuella framtida nya implementeringar av den utökade anslutningen (1.9.8 och senare) för att ansluta Workfront till AEM Assets as a Cloud Service blockeras.

>[!IMPORTANT]
>
>* Adobe kräver installation och konfiguration av [!DNL Adobe Workfront for Experience Manager enhanced connector] endast via certifierade partners eller [!DNL Adobe Professional Services]. Om den distribueras och konfigureras utan en certifierad partner eller [!DNL Adobe Professional Services], stöds den inte av Adobe.
>
>* Adobe kan släppa uppdateringar av [!DNL Adobe Workfront] och [!DNL Adobe Experience Manager] som gör den här kopplingen överflödig. Om detta inträffar kan kunderna behöva gå över från att använda den här anslutningen.
>
>* Adobe har stöd för utökade anslutningsversioner 1.7.4 och senare. Tidigare förhandsversioner och anpassade versioner stöds inte. Information om hur du kontrollerar den förbättrade anslutningsversionen finns i steg 5 a i [installationsanvisningar för förbättrad anslutning](workfront-connector-install.md).
>
>* Se [Partnercertifieringsprov för Workfront för Experience Manager Assets förbättrad anslutning](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Mer information om provet finns i [Provguide](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## Konfigurera händelseprenumerationer {#event-subscriptions}

Evenemangsprenumerationer används för att meddela AEM om händelser som inträffar i [!DNL Adobe Workfront]. Det finns tre [!DNL Workfront for Experience Manager enhanced connector] funktioner som kräver att en händelseprenumeration fungerar:

* Automatiskt skapande av projektlänkade mappar.
* Synkronisering av ändringar i anpassade formulärvärden för Workfront-dokument till AEM metadata för resurser.
* Automatisk publicering av material till Brand Portal när projektet är klart.

Aktivera händelseprenumerationer om du vill använda dessa funktioner.

* Redigera [!UICONTROL Workfront Tools] Cloud Service som du skapade i steg 5 och väljer [!UICONTROL Event Subscriptions] -fliken.
* Välj [!UICONTROL Workfront Custom Integration] som du skapade i avsnitt 6.
* Klicka på [!UICONTROL Enable Workfront Event Subscriptions].

  ![Evenemangsprenumeration](/help/assets/assets/event-subs.png)

## Konfigurera länkade mappar {#linked-folders}

Så här prenumererar du på händelserna:

1. Navigera till **[!UICONTROL Event Subscriptions]** i molntjänsterna.
1. Välj den anpassade integrering som skapas i [!DNL Workfront].
1. Klicka på **[!UICONTROL Enable Workfront Event Subscriptions]**.

### Konfiguration av länkad mappstruktur {#linked-folder-structure}

1. Gå till fliken Projektlänkade mappar i molntjänsterna.
1. Länkad mappens överordnade sökväg: Välj en mapp i DAM där du vill skapa de länkade mapparna. Om det lämnas tomt används /content/dam som standard. Se till att metadatamatchemat för Workfront Tools och Workfront-mappen för länkade mappar har tillämpats på den markerade mappen.
1. Länkad mappstruktur: Ange kommaavgränsade värden. Varje värde ska `DE:<some-project-custom-form-field>`, Portfolio, Program, Year, Name eller lite Literal String Value (det här sista med citattecken). Den är för närvarande inställd på Portfolio, Program, År, DE:Projekttyp, Namn.
1. Konfigurera behörigheter: Lägg till `jcr:all permissions` behörigheter till `/conf/workfront-tools/settings/cloudconfigs` for `wf-workfront-users` grupp.
1. Skapa länkad mapptitel i Workfront med hjälp av kryssrutan Mappstrukturnamn bör vara markerad om mappens titel i Workfront ska innehålla alla mappar i strukturen. I annat fall är det den sista mappens namn.
1. Med undermappsmappar kan du ange en lista med mappar som ska skapas som en underordnad mapp till den länkade mappen.
1. Projektstatus: Välj den status som projektet måste ställas in för för att skapa den länkade mappen.
1. Skapa en länkad mapp i projekt med portfölj: Lista med Portfolio som projektet måste tillhöra så att du kan skapa den länkade mappen. Lämna listan tom om du vill skapa den länkade mappen för alla projektportföljer.
1. Skapa en länkad mapp i projekt med anpassat formulärfält: Anpassat formulärfält och motsvarande värde som projektet måste ha för att du ska kunna skapa den länkade mappen. Den här konfigurationen ignoreras om den lämnas tom. Välj `CUSTOM FORMS: Create DAM Linked Folder` för fält och indata `Yes` för värdet.
1. Klicka på Aktivera automatiskt skapande av länkade mappar. Om du går tillbaka till fliken Händelseabonnemang ser du att det nu finns en händelse för att skapa.

![länkad mappkonfiguration](/help/assets/assets/wf-linked-folder-config.png)

## Mappning av metadataram {#metadata-schema-mapping}

### Konfigurera mappning av metadata {#folder-metadata-mapping}

Metadatamappning mellan Workfront-projekt och AEM-mappar definieras AEM mappmetadatamappningar. Mappens metadatascheman ska skapas och konfigureras som vanligt i AEM. Workfront Tools lägger till en automatiskt ifylld listruta på konfigurationsfliken Inställningar i varje formulärfält för mappmetadataram. I den här listrutan kan du ange till vilket Workfront-fält varje AEM ska mappas.

Så här konfigurerar du mappningarna:

1. Lägg till `jcr:read` behörigheter till `/conf/global/settings/dam/adminui-extension/foldermetadataschema` for `wf-workfront-users` grupp.
1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Folder Metadata Schemas]**.
1. Markera det mappmetadatamatchschema som du vill redigera och klicka på Redigera.
1. Markera det formulärfält för mappmetadataram som du vill redigera och välj fliken Inställningar på den högra panelen.
1. I [!UICONTROL Mapped from Workfront Field] markerar du namnet på det Workfront-fält som du vill mappa till den markerade AEM mappegenskapen. Tillgängliga alternativ är:

   * Anpassade formulärfält för projekt
   * Fält för projektöversikt (ID, namn, beskrivning, referensnummer, planerat slutförandedatum, projektägare, projektsponsor, Portfolio eller program)

![konfiguration för metadatamappning](/help/assets/assets/wf-metadata-mapping-config2.png)

### Konfigurera metadatamappning för resurser {#asset-metadata-mapping}

Metadatamappning mellan Adobe Workfront-dokument och -resurser definieras AEM metadatamappningar. Metadata Schemas ska skapas och konfigureras som vanligt i AEM. Workfront Tools lägger till konfigurationsalternativ på fliken Settings (Inställningar) i varje formulärfält för metadatdataschema. Med dessa alternativ kan du ange till vilket fält varje AEM ska mappas.

Så här konfigurerar du mappningarna:

1. Navigera till **verktyg** > **Resurser** > **Metadata-scheman**.
1. Välj det metadatamatchformulär som du vill redigera och klicka på **Redigera** eller skapa ett metadatamatchema från grunden.
1. Markera det formulärfält för metadataschemat som du vill redigera och välj **Inställningar** på den högra panelen.
1. I [!DNL Workfront] Anpassat formulärfält markerar namnet på [!DNL Workfront] fält som du vill mappa till den markerade AEM. Tillgängliga alternativ är:

   * Anpassade formulärfält för dokument
   * Anpassade formulärfält för projekt
   * Skapa anpassade formulärfält
   * Anpassade formulärfält för uppgift
   * Projektöversiktsfält (ID, namn, beskrivning eller referensnummer)

1. I det fall [!DNL Workfront] fält markerat i [!UICONTROL Workfront Custom Form Field] är ett fält av typen Workfront-användare måste du ange vilket Workfront-användarfält du vill mappa. Om du vill göra det markerar du Hämta värde från objektfältet som Workfront refererar till och anger sedan namnet på [!UICONTROL Workfront User Custom Form Field] som värdet ska mappas från.

   ![konfiguration för metadatamappning](/help/assets/assets/wf-metadata-mapping-config1.png)

## Egenskapen Karta {#map-property}

I det här arbetsflödessteget kan en användare mappa en egenskap till en [!DNL Workfront] anpassade formulär för ett projekt, en uppgift, en utgåva eller ett dokument. The [!DNL Workfront] artefakt det här steget påverkar slås upp med en relativ sökväg från nyttolasten. De egenskaper som ska mappas styrs från inställningarna i dialogrutan för steg.

**Typ**: I det här fältet kan du välja den Workfront-objekttyp som egenskaperna ska mappas till.

**ID-egenskap**: I det här fältet kan du ange sökvägen till ID:t för det Workfront-objekt som egenskaperna ska mappas till. Sökvägen som anges i det här fältet ska vara relativ till arbetsflödets nyttolast.

**Egenskapstilldelningar**: Med detta multifält kan du ange mappningar mellan AEM och Workfront-fält. Varje objekt i flerfältet anger en mappning. Varje mappning ska ha formatet `<workfront-field>=<aem-mapped-property>`.

* The `workfront-field` kan

   * Ett anpassat formulärfält som identifieras av prefixet `DE:`.
   * Ett redigerbart fält som identifieras av dess namn. Fältnamnen finns i [[!DNL Workfront] API Explorer](https://experience.workfront.com/s/api-explorer).

* The `aem-mapped-property` kan vara:

   * Ett literalt värde. De ska omges av citattecken.
   * En AEM. Den här referensen ska vara relativ till arbetsflödets nyttolast.
   * Ett namngivet värde. Dessa bör omges av hakparenteser.
   * En sammanfogning av de tre ovanstående objekten. Ange det med `{+}`.
   * En ändring av ovanstående 3 objekt genom att omge värdet med `{replace(<value>,"old-char","new-char")}`.

* Exempel:

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL="https://my-aem-author/assets.html"{+}{path}`

![Konfiguration för mappningsegenskap](/help/assets/assets/wf-map-property-config.png)

## Ange status {#set-status}

Redigera egenskaperna för **[!UICONTROL Workfront - Set Status]** i **[!UICONTROL Arguments]** -fliken.

![Redigera arbetsflöde för att ange status](/help/assets/assets/wf-set-status.png)

## Synkronisering av kommentarer {#comments-sync}

1. I [!DNL Experience Manager], åtkomst **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront Tools Configuration]**, välj konfigurationen och välj **[!UICONTROL Properties]**.

   ![synka kommentarer](/help/assets/assets/comments-sync1.png)

1. Välj **[!UICONTROL Event Subscriptions]** flik, klicka **[!UICONTROL Enable Comment Sync]** på **[!UICONTROL Send Comments made in Workfront to AEM]** alternativ.

   ![Synkronisering är aktiverat](/help/assets/assets/wf-comment-sync-enabled.png)

Så här testar du synkroniseringen av kommentarer från Workfront till AEM:

1. Navigera till ett länkat dokument i Workfront och lägg till en kommentar på fliken Uppdateringar.

   ![lämna kommentarer i Workfront](/help/assets/assets/comments-sync2.png)

1. Navigera till samma länkade dokument i AEM, markera dokumentet och öppna [!UICONTROL Timeline] i den vänstra navigeringen och välj [!UICONTROL Comments]. I den vänstra sidlisten visas de kommentarer som synkroniserats från [!DNL Workfront].

## Resursversioner {#asset-versions}

Om du vill behålla versionshistorik för resurser i AEM konfigurerar du resursversionshantering i AEM.

1. I Experience Manager, åtkomst **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront Tools Configuration]** och öppna **[!UICONTROL Advanced]** -fliken.

1. Välj alternativ **[!UICONTROL Store assets with the same name as versions of the existing asset]**. När du markerar det här alternativet aktiveras lagring av resurser som överförts med samma namn och till samma plats som versionen av den befintliga resursen. Om alternativet inte är markerat skapas en ny resurs med ett annat namn (till exempel `asset-name.pdf` och `asset-name-1.pdf`).

1. Välj alternativ **[!UICONTROL Update asset metadata when creating a new version]**. När det här alternativet är markerat uppdateras resursens metadata varje gång en ny version av resursen skapas. Om alternativet inte är markerat behåller resursen de metadata som den hade innan den nya versionen skapades.

![konfigurera resursversionshantering](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>Versionshantering stöds inte i länkade mappar. När en [!DNL Workfront] korrektur med ett dokument i en länkad mapp tas kommentarerna och anteckningarna i den tidigare versionen av resursen bort.

## Bifoga anpassade formulär {#attach-custom-forms}

Med det här arbetsflödessteget kan användare bifoga ett anpassat formulär till ett [!DNL Workfront] artefakt. Det här arbetsflödessteget kan läggas till i alla arbetsflödesmodeller. The [!DNL Workfront] artefakt det här steget påverkar slås upp med en relativ sökväg från nyttolasten.

Redigera egenskaperna för arbetsflödesredigeraren i Experience Manager [!UICONTROL Workfront - Attach custom form] arbetsflödessteg.

![anpassade formulär](/help/assets/assets/wf-custom-forms.png).

## Publicera resurser automatiskt {#auto-publish-assets}

1. I Experience Manager, åtkomst **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront Tools Configuration]** och öppna **[!UICONTROL Advanced]** -fliken.

1. Välj **[!UICONTROL Automatically publish assets when sent from Workfront]**. Med det här alternativet aktiveras automatisk publicering av resurser när de skickas från Workfront till AEM. Den här funktionen kan aktiveras villkorligt genom att du anger ett anpassat Workfront-formulärfält och vilket värde det ska anges till. När ett dokument skickas till AEM, om det uppfyller villkoret, publiceras resursen automatiskt.

1. Välj **[!UICONTROL Publish all project assets to Brand Portal upon project completion]**. Med det här alternativet aktiveras automatisk publicering av resurser till [!DNL Brand Portal] när statusen för det Workfront-projekt de tillhör ändras till `Complete`.

![konfigurera automatisk publicering](/help/assets/assets/wf-auto-publish-config.png)

## Anpassade formuläruppdateringar för Workfront {#subscribe-workfront-doc-custom-form-updates}

Prenumerera på ändringarna i [!DNL Workfront] anpassade formulär väljer du relevant alternativ i dialogrutan **[!UICONTROL Advanced]** -fliken. När du prenumererar på dessa uppdateringar uppdateras dina mappade [!DNL Experience Manager] metadatafält när motsvarande fält i [!DNL Workfront] anpassat formulär för dokument ändras.

![Konfigurera anpassade formuläruppdateringar i Workfront [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
