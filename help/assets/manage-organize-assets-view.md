---
title: Hantera era digitala resurser
description: Flytta, ta bort, kopiera, byta namn på, uppdatera och version av dina resurser i  [!DNL Assets view].
role: User, Leader
contentOwner: AG
exl-id: 2459d482-828b-4410-810c-ac55ef0a2119
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: fb7ce7dbb58be9fef5ab087441457770828d73c8
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 0%

---

# Hantera resurser {#manage-assets}

Du kan enkelt utföra olika DAM-åtgärder (Digital Asset Management) med det användarvänliga gränssnittet i [!DNL Assets view]. När du har lagt till resurserna kan du söka efter, hämta, flytta, kopiera, byta namn på, ta bort, uppdatera och redigera dina resurser.

Använd [!DNL Assets view] för att utföra följande resurshanteringsåtgärder. När du markerar en resurs visas följande alternativ i verktygsfältet högst upp.

![Verktygsfältsalternativ när du väljer en resurs](assets/toolbar-image-selected.png)

*Bild: Alternativ i verktygsfältet för en markerad bild.*

* ![avmarkera ikon](assets/do-not-localize/close-icon.png) Avmarkera markeringen.

* ![hitta liknande ikon](assets/do-not-localize/find-similar.svg) Hitta liknande bildresurs i Assets-gränssnittet baserat på metadata och smarta taggar.

* ![informationsikon](assets/do-not-localize/edit-in-icon.png) Klicka för att förhandsgranska en resurs och visa detaljerade metadata. När du förhandsgranskar kan du visa versionerna och redigera en bild.

* ![hämtningsikon](assets/do-not-localize/download-icon.png) Hämta den valda resursen till det lokala filsystemet.

* ![Lägg till samlingsikon](assets/do-not-localize/add-collection.svg) Lägg till den valda resursen i en samling.

* ![Fäst resursikonen](assets/do-not-localize/pin-quick-access.svg) Fäst en resurs för snabbare åtkomst när du behöver den senare. Alla fästa objekt visas i avsnittet **Snabbåtkomst** i Min Workspace.

* ![redigera i Express-ikon](assets/do-not-localize/edit-e.svg) Redigera en bild i den integrerade Adobe Express-filen i Adobe Experience Manager Assets.

* ![redigera resursikon](assets/do-not-localize/edit-e.svg) Redigera bilden med Adobe Express.

* ![dela resurslänksikon](assets/do-not-localize/share-link.svg) för en resurs med andra användare så att de kan komma åt och hämta den.

* ![Ta bort ikon](assets/do-not-localize/delete-icon.png) Ta bort den markerade resursen eller mappen.

* ![kopiera ikon](assets/do-not-localize/copy-icon.png) Kopiera den markerade filen eller mappen.

* ![flytta ikon](assets/do-not-localize/move-icon.png) Flytta den markerade resursen eller mappen till en annan plats i databashierarkin.

* ![Byt namn på ikonen](assets/do-not-localize/rename-icon.png) Byt namn på den markerade resursen eller mappen. Använd ett unikt namn, annars misslyckas namnbytet med en varning. Försök igen med ett nytt namn.
Du kan också klicka på titeln för en resurs eller en mapp för att byta namn på den. Ange den nya texten i textrutan **Byt namn på resurs** och klicka på **Spara**. Den här funktionen är tillgänglig i stödraster-, galleri-, vattenfalls- och listvyerna.

* ![ikon för vattenfallsvy](assets/do-not-localize/waterfall-view.png) [!UICONTROL Waterfall View].

* ![kopiera biblioteksikonen](assets/do-not-localize/copy-icon.png) Lägg till en resurs i biblioteket.

* ![tilldela en aktivitetsikon](assets/do-not-localize/review-delegate-icon.png) Tilldela uppgifter till andra användare för samarbete i en resurs.

* ![tilldelningsikonen](assets/do-not-localize/watch-asset.svg) Övervaka åtgärder som utförs på en resurs.

Du kan visa samma alternativ för miniatyrbilder av resurser.

![Alternativ på miniatyrbild av resurs för att hantera en resurs](assets/options-on-thumbnail.png)

[!DNL Assets view] visar bara de relevanta alternativen i verktygsfältet som är beroende av den valda resursens typ.

![Verktygsfältsalternativ när du väljer en resurs](assets/toolbar-folder-selected.png)

*Bild: Alternativ i verktygsfältet för en markerad mapp.*

![Verktygsfältsalternativ när du väljer en resurs](assets/toolbar-pdf-selected.png)

*Bild: Alternativ i verktygsfältet för en vald PDF-fil.*

## Hämta och distribuera resurser {#download}

Du kan välja en eller flera resurser eller mappar eller en kombination av båda och hämta urvalet till det lokala filsystemet. Du kan redigera resurserna och överföra dem igen eller distribuera resurserna utanför [!DNL Assets view]. Du kan även [hämta återgivningarna](/help/assets/add-delete-assets-view.md#renditions) för en resurs.

## Resursversionshantering {#versions-of-assets}

<!-- 
TBD: query for engineering: How many versions are maintained. What happens when we reach that limit? Are old versions automatically removed? -->

[!DNL Assets view] versioner av resurserna när resurserna överförs igen som uppdateras eller redigeras. Du kan visa versionshistorik, tidigare versioner och återställa en tidigare version av resurser som den senaste versionen, som återställs till en tidigare version om det behövs. Resursversioner skapas i följande scenarier:

* Överför en ny resurs med samma filnamn som en befintlig resurs och i samma mapp som den befintliga resursen. [!DNL Assets view] uppmanar dig att antingen skriva över den tidigare resursen eller spara den nya resursen som en version. Se [Överför duplicerade resurser](/help/assets/add-delete-assets-view.md).

  ![Skapa versioner vid överföring](assets/uploads-manage-duplicates.png)

  *Bild: När du överför en resurs med namnet same as an existing asset, kan du skapa en version av resursen.*

* Redigera en bild och klicka på **[!UICONTROL Save as Version]**. Se [redigera bilder](/help/assets/edit-images-assets-view.md).

  ![Spara redigerad bild som en version](assets/edit-image2.png)

  *Figur: Spara redigerad bild som en version.*

* Öppna versionerna av en befintlig resurs. Klicka på **[!UICONTROL New Version]** och överför en nyare version av resursen i databasen.

  ![Alternativ för att överföra en ny version av en resurs från versionshistoriken](assets/view-asset-versions2.png)

### Visa och jämföra versioner av en resurs {#view-and-compare-versions}

Överför en kopia eller en ändrad kopia av en resurs för att skapa dess versioner. Med versionshantering kan du spåra ändringar i en resurs över tid och återställa en tidigare version om det behövs.

Så här visar och jämför du versioner:

1. Navigera till resursens informationssida.
1. Klicka på ![Versioner](/help/assets/assets/Clock.svg) i den högra rutan för att visa panelen **[!UICONTROL Versions]**. Miniatyrbilderna för den ursprungliga resursen och dess överförda versioner visas på den här panelen.
1. Välj en version på panelen om du vill förhandsgranska den i förhandsvisningsområdet.
1. Välj en annan version än den senaste och klicka på **[!UICONTROL Make Latest]** för att ange den som den senaste versionen.
1. Dra skjutreglaget i förhandsvisningen åt vänster och höger för att snabbt se den valda versionen av en bild och dess senaste version i en enda förhandsvisning. På så sätt kan du snabbt jämföra den valda versionen av bilden med den senaste versionen.

   >[!NOTE]
   >
   > Versionsjämförelse är bara aktiverat för bildresurser.

   ![jämför versioner av resurs](/help/assets/assets/version-compare2.png)

<!-- old content
To view versions, open an asset's preview and click **[!UICONTROL Versions]** ![Versions icon](assets/do-not-localize/versions-clock-icon.png) from the right sidebar. To preview a specific version, select it. To revert to it, click **[!UICONTROL Make Latest]**. 
-->

Välj den senaste versionen och klicka på **[!UICONTROL New Version]** för att överföra en ny kopia av resursen från det lokala filsystemet och skapa en resursversion.

<!-- old content
You can also create versions from the versions timeline. Select the latest version, click **[!UICONTROL New Version]**, and upload a new copy of the asset from your local file system.

![View versions of an asset](assets/view-asset-versions1.png)

*Figure: View versions of an asset, revert to a previous version, or upload another new version.* 
-->

## Hantera resursstatus {#manage-asset-status}

**Behörigheter krävs:** `Can Edit`, `Owner` eller administratörsbehörighet för en resurs.

I Assets-vyn kan du ange status för resurser som är tillgängliga i databasen. Ange en resursstatus som bättre styr och hanterar nedströmsanvändningen av digitala resurser.

Du kan ange följande status för resurser:

* Godkänd

* Avvisad

* Ingen status

### Ange resursstatus {#set-asset-status}

Så här anger du resursstatus:

1. Markera resursen och klicka på **[!UICONTROL Details]** i verktygsfältet.

1. Välj resursstatus i listrutan **[!UICONTROL Status]** på fliken **[!UICONTROL Basic]**. Möjliga värden är Godkänd, Avvisat och Ingen status (standard).
Om du har aktiverat Dynamic Media med OpenAPI-funktioner för din miljö, genererar Experience Manager Assets en offentlig URL så fort du markerar resursen som `Approved`.

   >[!VIDEO](https://video.tv.adobe.com/v/342495)



### Ange godkännandemål {#set-approval-target}

I Assets-vyn kan du publicera godkända mediefiler till Dynamic Media med OpenAPI-funktioner, Content Hub, eller båda, baserat på det värde som du anger i fältet **Godkännandemål** på sidan Resursinformation.

Så här anger du godkännandemål:

1. Markera resursen och klicka på **[!UICONTROL Details]** i verktygsfältet.

1. Välj resursstatus i listrutan **[!UICONTROL Status]** på fliken **[!UICONTROL Basic]**. Möjliga värden är Godkänd, Avvisat och Ingen status (standard).

1. Om du väljer **Godkänd** i steg 2 väljer du ett godkännandemål. Exempel på möjliga värden är Delivery och Content Hub.

   * **Leverans** är det standardalternativ som valts i listrutan och som publicerar resursen till både [Dynamiska media med OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) och [Content Hub](/help/assets/product-overview.md), om båda är aktiverade för Experience Manager Assets.

   * Om du väljer **Content Hub** publiceras resursen bara till Content Hub. Content Hub visas bara som ett alternativ om det är aktiverat för Experience Manager Assets.

   * Om du inte väljer något alternativ i listrutan används standardalternativet som är aktiverat för din AEM as a Cloud Service-miljö automatiskt på resursen.


   Mer information om de tillgängliga alternativen finns i [Standardmål för godkännande och publiceringsmål för godkända resurser](#default-approval-target-options-publish-destinations).

   ![Godkännandestatus](/help/assets/assets/approval-status-delivery.png)

1. Ange andra resursegenskaper och klicka på **[!UICONTROL Save]**.

Några andra punkter att notera är:

* När du inte använder standardformuläret för metadata och inte kan visa fältet **[!UICONTROL Approval Target]**, [redigerar du metadataformuläret](/help/assets/metadata-assets-view.md#metadata-forms) och drar fältet **[!UICONTROL Approval for]** från de tillgängliga komponenterna till metadataformuläret. Klicka sedan på **[!UICONTROL Save]**.

* När du väljer godkännandemålet som `Content Hub` med hjälp av vyn Assets blir resurserna tillgängliga i Content Hub för användare som tillhör samma organisation.

#### Standardgodkännandemål och publicera destinationer för godkända resurser {#default-approval-target-options-publish-destinations}

Följande tabell visar förutsättningarna för att visa listrutan `Approval Target` och standardmålet för godkännande baserat på aktiveringen av DM med OpenAPI och Content Hub i din AEM as a Cloud Service-miljö:

| Dynamiska medier med OpenAPI | Content Hub | Listrutan Godkännandemål visas? | Standardgodkännandemål för godkända tillgångar | Publiceringsmål |
| --- | --- | --- | --- |---|
| Aktiverad | Aktiverad | Ja | Leverans | Dynamic Media med OpenAPI och Content Hub |
| Ej aktiverad | Aktiverad | Ja | Content Hub | Content Hub |
| Aktiverad | Ej aktiverad | Ja | Leverans | Dynamiska medier med OpenAPI |
| Ej aktiverad | Ej aktiverad | Nej | Ej tillämpligt | Ej tillämpligt |

### Ange förfallodatum för tillgång {#set-asset-expiration-date}

I Assets-vyn kan du även ange förfallodatum för resurser som finns i databasen. Du kan sedan [filtrera sökresultaten](search-assets-view.md#refine-search-results) baserat på en `Expired`-resursstatus. Du kan dessutom ange ett förfallodatumintervall för resurser för att ytterligare filtrera sökresultaten.

Så här anger du förfallodatum för tillgång:

1. Markera resursen och klicka på **[!UICONTROL Details]** i verktygsfältet.

1. Ange förfallodatumet för resursen med fältet **[!UICONTROL Expiration date]** på fliken **[!UICONTROL Basic]**.

Indikatorn för `Expired`-resurskortet åsidosätter indikatorn `Approved` eller `Rejected` som angetts för en resurs.

Du kan också filtrera resurser baserat på en resursstatus. Mer information finns i [Söka efter resurser i Assets-vyn](search-assets-view.md).

## Anpassa metadataformulär för att inkludera resursstatusfält {#customize-asset-status-metadata-form}

**Behörigheter krävs:** Administratör

I Assets-vyn finns många standardmetadatafält som standard. Organisationer har ytterligare metadatabehov och behöver fler metadatafält för att kunna lägga till företagsspecifika metadata. Med metadataformulär kan företag lägga till anpassade metadatafält på sidan [!UICONTROL Details] för en resurs. De företagsspecifika metadata förbättrar styrningen och identifieringen av dess resurser.

Mer information om hur du lägger till ytterligare metadatafält i metadataformuläret finns i [Metadata Forms](metadata-assets-view.md#metadata-forms).

**Lägg till metadatafält för resursstatus i formuläret**

Om du vill lägga till metadatafältet för resursstatus i formuläret drar du **[!UICONTROL Asset Status]**-komponenten från den vänstra listen till formuläret. Mappningsegenskapen fylls i automatiskt. Spara formuläret för att bekräfta ändringarna.

**Lägg till metadatafältet Förfallodatum i formuläret**

Om du vill lägga till metadatafältet Förfallodatum i formuläret drar du **[!UICONTROL Date]**-komponenten från den vänstra listen till formuläret. Ange **Förfallodatum** som etikett och `pur:expirationDate` som mappningsegenskap. Spara formuläret för att bekräfta ändringarna.

## Nästa steg {#next-steps}

* [Titta på en video för att hantera resurser i Assets-vyn](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/basics/managing.html)

* Ge produktfeedback med alternativet [!UICONTROL Feedback] som finns i användargränssnittet i Assets-vyn

* Ge feedback om dokumentationen med [!UICONTROL Edit this page] ![redigera sidan](assets/do-not-localize/edit-page.png) eller [!UICONTROL Log an issue] ![skapa ett GitHub-problem](assets/do-not-localize/github-issue.png) som är tillgängligt på den högra sidopanelen

* Kontakta [kundtjänst](https://experienceleague.adobe.com/?support-solution=General#support)

