---
title: Konfigurera [!DNL Workfront for Experience Manager enhanced connector]
description: Konfigurera [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: d4e1247a-342c-4bc4-83bf-4e4902468fb3
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1697'
ht-degree: 0%

---

# Konfigurera [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime och Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets-integrering med Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI-utökningsbarhet</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Aktivera Dynamic Media Prime och Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Sök efter bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Metadata - bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamiska media med OpenAPI-funktioner</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets-dokumentation för utvecklare</b></a>
        </td>
    </tr>
</table>

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-configure.html) |
| AEM as a Cloud Service | Den här artikeln |

En användare med administratörsåtkomst i [!DNL Adobe Experience Manager] som [!DNL Cloud Service] konfigurerar den förbättrade anslutningen efter att den har installerats. Instruktioner om hur du installerar finns i [Installera anslutningsprogrammet](/help/assets/workfront-integrations.md).

>[!IMPORTANT]
>
> Från juni 2022 släppte Adobe en ny inbyggd integrering för att ansluta Workfront till Adobe Experience Manager Assets as a Cloud Service. Den här integreringen har blivit den metod som krävs för att ansluta dessa två lösningar. Eventuella framtida nya implementeringar av den förbättrade anslutningen (1.9.8 och senare) för att ansluta Workfront till AEM Assets as a Cloud Service blockeras.

>[!IMPORTANT]
>
>* Adobe kräver att [!DNL Adobe Workfront for Experience Manager enhanced connector] distribueras och konfigureras endast via certifierade partners eller [!DNL Adobe Professional Services]. Om den distribueras och konfigureras utan en certifierad partner eller [!DNL Adobe Professional Services] stöds den inte av Adobe.
>
>* Adobe kan släppa uppdateringar av [!DNL Adobe Workfront] och [!DNL Adobe Experience Manager] som gör den här kopplingen överflödig. Om detta inträffar kan kunderna behöva gå över från att använda den här anslutningen.
>
>* Adobe har stöd för utökade anslutningsversioner 1.7.4 och senare. Tidigare förhandsversioner och anpassade versioner stöds inte. Om du vill kontrollera den utökade anslutningsversionen läser du steg 5(a) i [de förbättrade installationsanvisningarna för anslutningsprogrammet](workfront-connector-install.md).
>
>* Se [Partnercertifieringsprov för Workfront för Experience Manager Assets förbättrade anslutningsprogram](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Mer information om provet finns i [Handbok för prov](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## Konfigurera händelseprenumerationer {#event-subscriptions}

Händelseprenumerationer används för att meddela AEM om händelser som inträffar i [!DNL Adobe Workfront]. Det finns tre [!DNL Workfront for Experience Manager enhanced connector]-funktioner som kräver att händelseprenumerationer fungerar:

* Automatiskt skapande av projektlänkade mappar.
* Synkronisering av ändringar i anpassade formulärvärden för Workfront-dokument till metadata för AEM-resurser.
* Automatisk publicering av material till Brand Portal när projektet är klart.

Aktivera händelseprenumerationer om du vill använda dessa funktioner.

* Redigera konfigurationen för [!UICONTROL Workfront Tools] molntjänster som du skapade i steg 5 och välj fliken [!UICONTROL Event Subscriptions].
* Markera [!UICONTROL Workfront Custom Integration] som du skapade i avsnitt 6.
* Klicka på [!UICONTROL Enable Workfront Event Subscriptions].

  ![Evenemangsprenumeration](/help/assets/assets/event-subs.png)

## Konfigurera länkade mappar {#linked-folders}

Så här prenumererar du på händelserna:

1. Navigera till fliken **[!UICONTROL Event Subscriptions]** i molntjänsterna.
1. Välj den anpassade integrering som skapats i [!DNL Workfront].
1. Klicka på **[!UICONTROL Enable Workfront Event Subscriptions]**.

### Konfiguration av länkad mappstruktur {#linked-folder-structure}

1. Gå till fliken Projektlänkade mappar i molntjänsterna.
1. Länkad mappens överordnade sökväg: Välj en mapp i DAM där du vill skapa de länkade mapparna. Om det lämnas tomt används /content/dam som standard. Se till att metadatamatchemat för Workfront Tools och Workfront-mappen för länkade mappar har tillämpats på den markerade mappen.
1. Länkad mappstruktur: Ange kommaavgränsade värden. Varje värde ska vara `DE:<some-project-custom-form-field>`, Portfolio, Program, Year, Name eller något &quot;Literal String Value&quot; (det sista med citattecken). Den är för närvarande inställd på Portfolio, Program, Year, DE:Project Type, Name.
1. Konfigurera behörigheter: Lägg till `jcr:all permissions`-behörigheter i `/conf/workfront-tools/settings/cloudconfigs` för gruppen `wf-workfront-users`.
1. Skapa länkad mapptitel i Workfront med hjälp av kryssrutan Mappstrukturnamn bör vara markerad om mappens titel i Workfront ska innehålla alla mappar i strukturen. I annat fall är det den sista mappens namn.
1. Med undermappsmappar kan du ange en lista med mappar som ska skapas som en underordnad mapp till den länkade mappen.
1. Projektstatus: Välj den status som projektet måste ställas in för för att skapa den länkade mappen.
1. Skapa en länkad mapp i projekt med portfölj: Lista med portföljer som projektet måste tillhöra så att du kan skapa den länkade mappen. Lämna listan tom om du vill skapa den länkade mappen för alla projektportföljer.
1. Skapa en länkad mapp i projekt med anpassat formulärfält: Anpassat formulärfält och motsvarande värde som projektet måste ha för att du ska kunna skapa den länkade mappen. Den här konfigurationen ignoreras om den lämnas tom. Välj `CUSTOM FORMS: Create DAM Linked Folder` för fältet och indata `Yes` för värdet.
1. Konfigurera behörighet: Konfigurera dessa behörigheter, `jcr:all permissions for /conf/workfront-tools/settings/cloudconfigs` för `wf-workfront-users group`.
1. Klicka på Aktivera automatiskt skapande av länkade mappar. Om du går tillbaka till fliken Händelseabonnemang ser du att det nu finns en händelse för att skapa.

![konfiguration av länkad mapp](/help/assets/assets/wf-linked-folder-config.png)

## Mappning av metadataram {#metadata-schema-mapping}

### Konfigurera mappning av metadata {#folder-metadata-mapping}

Metadatamappning mellan Workfront-projekt och AEM-mappar definieras i AEM mappmetadatamatchningar. Mappmetadatascheman ska skapas och konfigureras som vanligt i AEM. Workfront Tools lägger till en automatiskt ifylld listruta på konfigurationsfliken Inställningar i varje formulärfält för mappmetadataram. I den här nedrullningsbara menyn kan du ange till vilket Workfront-fält varje AEM-mappegenskap ska mappas.

Så här konfigurerar du mappningarna:

1. Lägg till `jcr:read`-behörigheter i `/conf/global/settings/dam/adminui-extension/foldermetadataschema` för gruppen `wf-workfront-users`.
1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Folder Metadata Schemas]**.
1. Markera det mappmetadatamatchschema som du vill redigera och klicka på Redigera.
1. Markera det formulärfält för mappmetadataram som du vill redigera och välj fliken Inställningar på den högra panelen.
1. I fältet [!UICONTROL Mapped from Workfront Field] markerar du namnet på det Workfront-fält som du vill mappa till den valda AEM-mappegenskapen. Tillgängliga alternativ är:

   * Anpassade formulärfält för projekt
   * Projektöversiktsfält (ID, namn, beskrivning, referensnummer, planerat slutförandedatum, projektägare, projektsponsor, Portfolio eller program)

![metadatamappningskonfiguration](/help/assets/assets/wf-metadata-mapping-config2.png)

### Konfigurera metadatamappning för resurser {#asset-metadata-mapping}

Metadatamappning mellan Adobe Workfront-dokument och Assets definieras i AEM metadatamatchningar. Metadata Schemas ska skapas och konfigureras som vanligt i AEM. Workfront Tools lägger till konfigurationsalternativ på fliken Settings (Inställningar) i varje formulärfält för metadatdataschema. Med dessa alternativ kan du ange till vilket Workfront-fält varje AEM-egenskap ska mappas.

Så här konfigurerar du mappningarna:

1. Navigera till **Verktyg** > **Assets** > **Metadata Schemas**.
1. Välj det metadatamatchformulär som du vill redigera och klicka på **Redigera** eller skapa ett metadatamatchema från början.
1. Markera det formulärfält för metadataschemat som du vill redigera och välj fliken **Inställningar** på den högra panelen.
1. I det anpassade formulärfältet [!DNL Workfront] markerar du namnet på det [!DNL Workfront]-fält som du vill mappa till den valda AEM-egenskapen. Tillgängliga alternativ är:

   * Anpassade formulärfält för dokument
   * Anpassade formulärfält för projekt
   * Skapa anpassade formulärfält
   * Anpassade formulärfält för uppgift
   * Projektöversiktsfält (ID, namn, beskrivning eller referensnummer)

1. Om fältet [!DNL Workfront] som valts i [!UICONTROL Workfront Custom Form Field] är ett Workfront-fält av typen närmast föregående, måste du ange vilket Workfront-användarfält som du vill mappa. Om du vill göra det markerar du Hämta värde från objektfältet som refereras till av Workfront och anger sedan namnet på [!UICONTROL Workfront User Custom Form Field] som värdet ska mappas från.

   ![konfiguration för metadatamappning](/help/assets/assets/wf-metadata-mapping-config1.png)

## Egenskapen Karta {#map-property}

I det här arbetsflödessteget kan en användare mappa en egenskap till ett [!DNL Workfront] anpassat formulär i ett projekt, en uppgift, ett problem eller ett dokument. [!DNL Workfront]-artefakten som det här steget påverkar har slagits upp med en relativ sökväg från nyttolasten. De egenskaper som ska mappas styrs från inställningarna i dialogrutan för steg.

**Typ**: I det här fältet kan du välja den Workfront-objekttyp som egenskaperna ska mappas till.

**ID-egenskap**: I det här fältet kan du ange sökvägen till ID:t för Workfront-objektet som egenskaperna ska mappas till. Sökvägen som anges i det här fältet ska vara relativ till arbetsflödets nyttolast.

**Egenskapstilldelningar**: Med det här multifältet kan du ange mappningar mellan AEM-egenskaper och Workfront-fält. Varje objekt i flerfältet anger en mappning. Varje mappning ska ha formatet `<workfront-field>=<aem-mapped-property>`.

* `workfront-field` kan vara

   * Ett anpassat formulärfält som identifieras av prefixet `DE:`.
   * Ett redigerbart fält som identifieras av dess namn. Fältnamnen finns i [[!DNL Workfront] API Explorer](https://experience.workfront.com/s/api-explorer).

* `aem-mapped-property` kan vara:

   * Ett literalt värde. De ska omges av citattecken.
   * En AEM-egenskap. Den här referensen ska vara relativ till arbetsflödets nyttolast.
   * Ett namngivet värde. Dessa bör omges av hakparenteser.
   * En sammanfogning av de tre ovanstående objekten. Ange det med `{+}`.
   * En ändring av ovanstående 3 objekt genom att omge värdet med `{replace(<value>,"old-char","new-char")}`.

* Exempel:

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL="https://my-aem-author/assets.html"{+}{path}`

![Konfiguration för att mappa egenskap](/help/assets/assets/wf-map-property-config.png)

## Ange status {#set-status}

Redigera egenskaperna för **[!UICONTROL Workfront - Set Status]** på fliken **[!UICONTROL Arguments]** i arbetsflödesredigeraren.

![Redigera arbetsflöde för att ange status](/help/assets/assets/wf-set-status.png)

## Synkronisering av kommentarer {#comments-sync}

1. Gå till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront Tools Configuration]** i [!DNL Experience Manager], markera konfigurationen och välj **[!UICONTROL Properties]**.

   ![kommentarsynkronisering](/help/assets/assets/comments-sync1.png)

1. Välj fliken **[!UICONTROL Event Subscriptions]** och klicka på alternativet **[!UICONTROL Enable Comment Sync]** på **[!UICONTROL Send Comments made in Workfront to AEM]**.

   ![Synkronisering är aktiverat](/help/assets/assets/wf-comment-sync-enabled.png)

Så här testar du synkroniseringen av kommentarer från Workfront till AEM:

1. Navigera till ett länkat dokument i Workfront och lägg till en kommentar på fliken Uppdateringar.

   ![lämna kommentarer i Workfront](/help/assets/assets/comments-sync2.png)

1. Navigera till samma länkade dokument i AEM, markera dokumentet och öppna alternativet [!UICONTROL Timeline] i den vänstra navigeringen och välj [!UICONTROL Comments]. Den vänstra sidlisten visar de kommentarer som synkroniserats från [!DNL Workfront].

## Resursversioner {#asset-versions}

Om du vill behålla versionshistorik för resurser i AEM konfigurerar du versionshantering för resurser i AEM.

1. I Experience Manager går du till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront Tools Configuration]** och öppnar fliken **[!UICONTROL Advanced]**.

1. Välj alternativet **[!UICONTROL Store assets with the same name as versions of the existing asset]**. När du markerar det här alternativet aktiveras lagring av resurser som överförts med samma namn och till samma plats som versionen av den befintliga resursen. Om alternativet inte är markerat skapas en ny resurs med ett annat namn (till exempel `asset-name.pdf` och `asset-name-1.pdf`).

1. Välj alternativet **[!UICONTROL Update asset metadata when creating a new version]**. När det här alternativet är markerat uppdateras resursens metadata varje gång en ny version av resursen skapas. Om alternativet inte är markerat behåller resursen de metadata som den hade innan den nya versionen skapades.

![konfigurera resursversionshantering](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>Versionshantering stöds inte i länkade mappar. När du skapar ett [!DNL Workfront]-korrektur med ett dokument i en länkad mapp tas kommentarerna och anteckningarna i den tidigare versionen av resursen bort.

## Bifoga anpassade formulär {#attach-custom-forms}

I det här arbetsflödessteget kan användare bifoga ett anpassat formulär till en [!DNL Workfront]-artefakt. Det här arbetsflödessteget kan läggas till i alla arbetsflödesmodeller. [!DNL Workfront]-artefakten som det här steget påverkar har slagits upp med en relativ sökväg från nyttolasten.

Redigera egenskaperna för arbetsflödessteget [!UICONTROL Workfront - Attach custom form] i arbetsflödesredigeraren i Experience Manager.

![anpassade formulär](/help/assets/assets/wf-custom-forms.png).

## Publicera resurser automatiskt {#auto-publish-assets}

1. I Experience Manager går du till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront Tools Configuration]** och öppnar fliken **[!UICONTROL Advanced]**.

1. Välj **[!UICONTROL Automatically publish assets when sent from Workfront]**. Med det här alternativet aktiveras automatisk publicering av mediefiler när de skickas från Workfront till AEM. Den här funktionen kan aktiveras villkorligt genom att du anger ett anpassat Workfront-formulärfält och vilket värde det ska anges till. När ett dokument skickas till AEM publiceras resursen automatiskt om det uppfyller villkoret.

1. Välj **[!UICONTROL Publish all project assets to Brand Portal upon project completion]**. Med det här alternativet aktiveras automatisk publicering av resurser till [!DNL Brand Portal] när statusen för det Workfront-projekt de tillhör ändras till `Complete`.

![konfigurera automatisk publicering](/help/assets/assets/wf-auto-publish-config.png)

## Anpassade formuläruppdateringar för Workfront {#subscribe-workfront-doc-custom-form-updates}

Om du vill prenumerera på ändringarna i [!DNL Workfront] anpassade formulär väljer du det relevanta alternativet på fliken **[!UICONTROL Advanced]**. När du prenumererar på dessa uppdateringar uppdateras dina mappade [!DNL Experience Manager]-metadatafält när motsvarande fält i det anpassade [!DNL Workfront]-dokumentformuläret ändras.

![Konfigurationen för anpassade formulär i Workfront uppdateras i [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
