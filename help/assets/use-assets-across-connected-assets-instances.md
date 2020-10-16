---
title: Använd Connected Assets när du vill dela DAM-resurser i [!DNL Sites]
description: Använd resurser som är tillgängliga på en [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] fjärrdistribution.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26294ad57544aa822dc6341fbbd85f396730ee8b
workflow-type: tm+mt
source-wordcount: '2137'
ht-degree: 39%

---


# Använd Connected Assets när du vill dela DAM-resurser i [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

I stora företag kan den infrastruktur som krävs för att skapa webbplatser vara distribuerad. Ibland kan funktionerna för att skapa webbplatser och de digitala resurser som används för att skapa webbplatserna finnas i olika distributioner. En orsak kan vara att befintliga distributioner som behövs för att fungera tillsammans distribueras geografiskt. En annan orsak kan vara förvärv som leder till heterogen infrastruktur som moderbolaget vill använda tillsammans.

Användare kan skapa webbsidor i [!DNL Experience Manager Sites]. [!DNL Experience Manager Assets] är det DAM-system (Digital Asset Management) som tillhandahåller de resurser som krävs för webbplatser. [!DNL Experience Manager] har nu stöd för ovanstående användningsexempel genom integrering [!DNL Sites] och [!DNL Assets].

## Översikt över Connected Assets {#overview-of-connected-assets}

When editing pages in [!UICONTROL Page Editor], the authors can seamlessly search, browse, and embed assets from a different [!DNL Assets] deployment. Administratörerna skapar en engångs integrering av en distribution av [!DNL Sites] med en annan (fjärransluten) distribution av [!DNL Assets].

For the [!DNL Sites] authors, the remote assets are available as read-only local assets. Funktionen stöder enkel sökning och användning av ett fåtal fjärresurser i taget. To make many remote assets available on a [!DNL Sites] deployment in one-go, consider migrating the assets in bulk.

### Förutsättningar och distributioner som stöds {#prerequisites}

Innan du använder eller konfigurerar den här funktionen bör du kontrollera följande:

* Användarna ingår i rätt användargrupper för varje distribution.
* Ett av villkoren som stöds är uppfyllt för [!DNL Adobe Experience Manager] distributionstyper. Mer information om [!DNL Experience Manager] 6.5 finns i [Funktionen för anslutna resurser i Experience Manager 6.5-resurser](https://docs.adobe.com/content/help/en/experience-manager-65/assets/using/use-assets-across-connected-assets-instances.html).

   |  | [!DNL Sites] som en Cloud Service | [!DNL Experience Manager] 6.5 [!DNL Sites] på AMS | [!DNL Experience Manager] 6.5 [!DNL Sites] på plats |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]som en Cloud Service** | Stöds | Stöds | Stöds |
   | **[!DNL Experience Manager]6.5 [!DNL Assets] på AMS** | Stöds | Stöds | Stöds |
   | **[!DNL Experience Manager]6.5 [!DNL Assets] på plats** | Stöds ej | Stöds ej | Stöds ej |

### Filformat som stöds {#mimetypes}

Författare söker efter bilder och följande typer av dokument i Content Finder och använder de sökbara resurserna i Page Editor. Dokument läggs till i `Download` komponenten och bilder i `Image` komponenten. Authors also add the remote assets in any custom [!DNL Experience Manager] component that extends the default `Download` or `Image` components. De format som stöds är:

* **Bildformat**: De format som stöds av [bildkomponenten](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/image.html) . [!DNL Dynamic Media] bilder stöds inte.
* **Dokumentformat**: Se vilka [dokumentformat](file-format-support.md#document-formats)som stöds.

### Användare och grupper som krävs {#users-and-groups-involved}

De olika roller som krävs för att konfigurera och använda funktionen och motsvarande användargrupper beskrivs nedan. Lokalt omfång används för de fall där en författare skapar en webbsida. Fjärromfång används för DAM-distributionen som är värd för de nödvändiga resurserna. The [!DNL Sites] author fetches these remote assets.

| Roll | Omfång | Användargrupp | Användarnamn i genomgång | Krav |
|----------------------------------|--------|------------------------------------------------------------------------------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Sites] administratör | Lokalt | [!DNL Experience Manager] `administrators` | `admin` | Set up [!DNL Experience Manager] and configure integration with the remote [!DNL Assets] deployment. |
| DAM-användare | Lokalt | `Authors` | `ksaner` | Används för att visa och duplicera de hämtade resurserna i `/content/DAM/connectedassets/`. |
| [!DNL Sites] author | Lokalt | `Authors` (med läsåtkomst på fjärr-DAM och författaråtkomst lokalt [!DNL Sites]) | `ksaner` | End user are [!DNL Sites] authors who use this integration to improve their content velocity. The authors search and browse assets in remote DAM using [!UICONTROL Content Finder] and using the required images in local web pages. Autentiseringsuppgifterna för `ksaner` DAM-användaren används. |
| [!DNL Assets] administratör | Fjärr | [!DNL Experience Manager] `administrators` | `admin` på fjärrkontrollen [!DNL Experience Manager] | Konfigurerar CORS (Cross-Origin Resource Sharing). |
| DAM-användare | Fjärr | `Authors` | `ksaner` på fjärrkontrollen [!DNL Experience Manager] | Author role on the remote [!DNL Experience Manager] deployment. Söker efter och bläddrar bland resurser i Connected Assets med hjälp av [!UICONTROL Content Finder]. |
| DAM-distributör (teknisk användare) | Fjärr | [!DNL Sites] `Authors` | `ksaner` på fjärrkontrollen [!DNL Experience Manager] | This user present on the remote deployment is used by [!DNL Experience Manager] local server (not the [!DNL Sites] author role) to fetch the remote assets, on behalf of [!DNL Sites] author. Den här rollen är inte densamma som de två `ksaner`-rollerna ovan och den tillhör en annan användargrupp. |

## Configure a connection between [!DNL Sites] and [!DNL Assets] deployments {#configure-a-connection-between-sites-and-assets-deployments}

An [!DNL Experience Manager] administrator can create this integration. Behörigheterna som krävs för att använda det skapas via användargrupper när de har skapats. Användargrupperna definieras för [!DNL Sites] distributionen och för DAM-distributionen.

To configure Connected Assets and local [!DNL Sites] connectivity, follow these steps:

1. Access an existing [!DNL Sites] deployment or create a deployment using the following command:

   1. In the folder of the JAR file, execute the following command on a terminal to create each [!DNL Experience Manager] server.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. After a few minutes, the [!DNL Experience Manager] server starts successfully. Consider this [!DNL Sites] deployment as the local machine for web page authoring, say at `https://[local_sites]:4502`.

1. Ensure that the users and roles with local scope exist on the [!DNL Sites] deployment and on the [!DNL Assets] deployment on AMS. Create a technical user on [!DNL Assets] deployment and add to the user group mentioned in [users and groups involved](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Åtkomst till den lokala [!DNL Sites] distributionen på `https://[local_sites]:4502`. Klicka på **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Connected Assets Configuration]** och ange följande värden:

   1. [!DNL Assets] platsen är `https://[assets_servername_ams]:[port]`.
   1. Autentiseringsuppgifter för en DAM-distributör (teknisk användare).
   1. In the **[!UICONTROL Mount Point]** field, enter the local [!DNL Experience Manager] path where [!DNL Experience Manager] fetches the assets. Till exempel, mappen `remoteassets`.

   1. Justera värdena för **[!UICONTROL Original Binary transfer optimization Threshold]** beroende på ditt nätverk. En resursåtergivning med en storlek som är större än detta tröskelvärde överförs asynkront.
   1. Select **[!UICONTROL Datastore Shared with Connected Assets]**, if you use a datastore to store your assets and the Datastore is the common storage between both deployments. I det här fallet spelar tröskelvärdet ingen roll eftersom resursernas binärfiler finns i datalagret och de inte överförs.

   ![En typisk konfiguration för Connected Assets](assets/connected-assets-typical-config.png)

   *Bild: En typisk konfiguration för Connected Assets.*

1. Inaktivera arbetsflödets startprogram eftersom resurserna redan har bearbetats och återgivningarna hämtas. Adjust the launcher configurations on the local ([!DNL Sites]) deployment to exclude the `connectedassets` folder, in which the remote assets are fetched.

   1. Vid [!DNL Sites] distributionen klickar du på **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Launchers]**.

   1. Sök efter startprogram med arbetsflöden som **[!UICONTROL DAM Update Asset]** och **[!UICONTROL DAM Metadata Writeback]**.

   1. Välj startprogrammet för arbetsflödet och klicka på **[!UICONTROL Properties]** i åtgärdsfältet.

   1. In the [!UICONTROL Properties] wizard, change the **[!UICONTROL Path]** fields as the following mappings to update their regular expressions to exclude the mount point **[!UICONTROL connectedassets]**.

   | Före | Efter |
   | ------------------------------------------------------- | -------------------------------------------------------------------------- |
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Alla återgivningar som är tillgängliga på fjärrdistributionen hämtas när författare hämtar en resurs. Om du vill skapa fler återgivningar av en hämtad resurs hoppar du över det här konfigurationssteget. Arbetsflödet [!UICONTROL DAM Update Asset] aktiveras och skapar fler återgivningar. These renditions are available only on the local [!DNL Sites] deployment and not on the remote DAM deployment.

1. Lägg till [!DNL Sites] distributionen som en av **[!UICONTROL Allowed Origins]** i fjärrkonfigurationen [!DNL Assets'] av CORS.

   1. Logga in med administratörsautentiseringsuppgifterna. Search for `Cross-Origin`. Öppna **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.

   1. Om du vill skapa en CORS-konfiguration för [!DNL Sites] distribution klickar du på Lägg till ![alternativikon](assets/do-not-localize/aem_assets_add_icon.png) bredvid **[!UICONTROL Adobe Granite Cross-Origin Resource Sharing Policy]**.

   1. In the field **[!UICONTROL Allowed Origins]**, input the URL of the local [!DNL Sites], that is, `https://[local_sites]:[port]`. Spara konfigurationen.

## Använda fjärresurser {#use-remote-assets}

Webbplatsens författare använder Content Finder för att ansluta till DAM-distributionen. Författarna kan bläddra bland, söka efter och dra fjärresurserna till en komponent. Om du vill autentisera med DAM-fjärrdistributionen bör du ha DAM-användarens autentiseringsuppgifter som du fått av administratören till hands.

Författare kan använda resurserna som finns på den lokala DAM-resursen och den fjärranslutna DAM-distributionen på en enda webbsida. Använd Content Finder för att växla mellan att söka i det lokala DAM-systemet eller söka i det fjärranslutna DAM-systemet.

Endast de taggar för fjärrresurser som har en exakt motsvarande tagg tillsammans med samma taxonomihierarki, som är tillgängliga för den lokala [!DNL Sites] distributionen, hämtas. Alla andra taggar tas bort. Authors can search for remote assets using all the tags present on the remote [!DNL Experience Manager] deployment, as it offers a full-text search.

### Genomgång av användningen {#walk-through-of-usage}

Använd konfigurationen ovan när du vill prova redigeringsfunktionen och se hur den fungerar. Använd de dokument eller bilder du vill ha på den fjärranslutna DAM-distributionen.

1. Navigate to the [!DNL Assets] interface on the remote deployment by accessing **[!UICONTROL Assets]** > **[!UICONTROL Files]** from [!DNL Experience Manager] workspace. Du kan även få åtkomst till `https://[assets_servername_ams]:[port]/assets.html/content/dam` i en webbläsare. Ladda upp de resurser du vill ha.
1. On the [!DNL Sites] deployment, in the profile activator in the upper-right corner, click **[!UICONTROL Impersonate as]**. Ange `ksaner` som användarnamn, markera det angivna alternativet och klicka på **[!UICONTROL OK]**.
1. Öppna en We.Retail-webbsida på **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Redigera sidan. Du kan även öppna `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` i en webbläsare när du vill redigera en sida.

   Klicka på **[!UICONTROL Toggle Side Panel]** överst till vänster på sidan.

1. Open the [!UICONTROL Assets] tab and click **[!UICONTROL Log in to Connected Assets]**.
1. Ange inloggningsuppgifterna, `ksaner` som användarnamn och `password` som lösenord. This user has authoring permissions on both the [!DNL Experience Manager] deployments.
1. Sök efter resursen som du har lagt till i DAM. Fjärresurserna visas i den vänstra panelen. Filtrera efter bilder eller dokument och filtrera efter olika typer av dokument som stöds. Dra bilderna till en `Image`-komponent och dokument till en `Download`-komponent.

   The fetched assets are read-only on the local [!DNL Sites] deployment. You can still use the options provided by your [!DNL Sites] components to edit the fetched asset. Redigering med komponenter är icke-destruktiv.

   ![Alternativ för att filtrera dokumenttyper och bilder vid sökning efter resurser på DAM-fjärrdistribution](assets/filetypes_filter_connected_assets.png)

   *Bild: Alternativ för att filtrera dokumenttyper och bilder vid sökning efter resurser på DAM-fjärrdistribution.*

1. En Sites-författare meddelas om en resurs hämtas asynkront och om en hämtningsåtgärd misslyckas. Under eller efter redigeringen kan författare se detaljerad information om hämtningsåtgärder och fel i användargränssnittet för [asynkrona jobb](/help/operations/asynchronous-jobs.md).

   ![Meddelande om asynkron hämtning av resurser som sker i bakgrunden.](assets/assets_async_transfer_fails.png)

   *Bild: Meddelande om asynkron hämtning av resurser som sker i bakgrunden.*

1. When publishing a page, [!DNL Experience Manager] displays a complete list of assets that are used on the page. Kontrollera att fjärresurserna har hämtats vid publiceringen. Se [användargränssnittet för asynkrona jobb](/help/operations/asynchronous-jobs.md) om du vill kontrollera status för varje hämtad resurs.

   >[!NOTE]
   >
   >Sidan publiceras även om en eller flera fjärresurser inte hämtats. Komponenten som använder fjärresursen publiceras tom. The [!DNL Experience Manager] notification area displays a notification for errors that show in async jobs page.

>[!CAUTION]
>
>Once used in a web page, the fetched remote assets are searchable and usable by anyone who has permissions to access the local folder. The fetched assets are stored (`connectedassets` in the above walk-through). Resurserna är också sökbara och synliga i det lokala datalagret via [!UICONTROL Content Finder].

De hämtade resurserna kan användas som andra lokala resurser, förutom att associerade metadata inte kan redigeras.

## Limitations and best practices {#tip-and-limitations}

* Om du vill få insikter om resursanvändning konfigurerar du funktionen [Asset Insight](/help/assets/assets-insights.md) för [!DNL Sites] instansen.

### Tillstånd och resurshantering {#permissions-and-managing-assets}

* Lokala resurser synkroniseras inte med de ursprungliga resurserna i fjärrdistributionen. Ändringar, borttagningar eller återkallande av behörigheter i DAM-distributionen sprids inte längre ned i kedjan.
* Lokala resurser är skrivskyddade kopior. [!DNL Experience Manager] -komponenter gör icke-förstörande redigeringar av resurser. Inga andra redigeringar tillåts.
* Lokalt hämtade resurser är endast tillgängliga för redigeringsändamål. Det går inte att använda arbetsflöden för resursuppdatering och metadata kan inte redigeras.
* Endast bilder och dokumentformaten i listan stöds. [!DNL Dynamic Media] resurser, innehållsfragment och Experience Fragments stöds inte.
* [!DNL Experience Manager] hämtar inte metadatamatcheman. Det innebär att alla hämtade metadata inte visas. Om schemat uppdateras separat visas alla egenskaper.
* Alla [!DNL Sites] författare har läsbehörighet för de hämtade kopiorna, även om författare inte har åtkomst till fjärdistributionen av DAM.
* Det finns inte API-stöd för att anpassa integreringen.
* Funktionen stöder smidig sökning och användning av fjärresurser. Om du vill göra många fjärresurser tillgängliga i den lokala distributionen på en gång bör du överväga att migrera resurserna.
* Det går inte att använda en fjärrresurs som sidminiatyr i [!UICONTROL Page Properties] användargränssnittet. Du kan ange en miniatyrbild för en webbsida i [!UICONTROL Page Properties] användargränssnittet från [!UICONTROL Thumbnail] genom att klicka på [!UICONTROL Select Image].

### Konfigurera och licensiera {#setup-licensing}

* [!DNL Assets] kan användas på [!DNL Adobe Managed Services] .
* [!DNL Sites] kan ansluta till en enda [!DNL Assets] databas åt gången.
* A license of [!DNL Assets] working as remote repository.
* One or more licenses of [!DNL Sites] working as local authoring deployment.

### Användning {#usage}

* Användare kan söka efter fjärrresurser och dra dem på den lokala sidan när de redigerar. Inga andra funktioner stöds.
* Tidsgränsen för hämtning är 5 sekunder. Författare kan ha problem med att hämta resurser, till exempel om det råder nätverksproblem. Authors can reattempt by dragging the remote asset from [!UICONTROL Content Finder] to [!UICONTROL Page Editor].
* Enkla redigeringar som är icke-destruktiva och redigering som stöds via `Image`-komponenten kan tillämpas på hämtade resurser. Resurserna är skrivskyddade.
* Det enda sättet att hämta resursen på nytt är att dra den till en sida. Det finns inget API-stöd eller andra metoder för att hämta om en resurs för att uppdatera den.
* Om resurser tas ur bruk från DAM används de fortfarande på [!DNL Sites] sidor.

## Felsöka problem {#troubleshoot}

Följ de här stegen för att felsöka det vanliga felscenariot:

* If you cannot search for remote assets from the [!UICONTROL Content Finder], then ensure that the required roles and permissions are in place.
* En resurs som hämtats från fjärrdammen kanske inte publiceras på en webbsida av en eller flera orsaker. Den finns inte på fjärrservern, saknar behörighet att hämta den eller så kan nätverksfel vara orsaken. Se till att resursen inte tas bort från fjärr-DAM. Se till att rätt behörigheter finns och att kraven är uppfyllda. Försök lägga till resursen på sidan igen och publicera den på nytt. Kontrollera i [listan över asynkrona jobb](/help/operations/asynchronous-jobs.md) om fel uppstod vid hämtning av resurser.
* Om du inte kan komma åt fjärr-DAM-distributionen från den lokala [!DNL Sites] distributionen kontrollerar du att cookies mellan platser tillåts. Om cookies mellan platser blockeras kanske de två distributionerna av [!DNL Experience Manager] inte autentiseras. I Incognito-läget kan till exempel cookies från tredje part blockeras [!DNL Google Chrome] av cookies. Om du vill tillåta cookies i [!DNL Chrome] webbläsaren klickar du på ögonikonen i adressfältet, navigerar till Plats som inte fungerar > Blockerad, väljer fjärr-DAM-URL och tillåter inloggningstokencookie. Du kan även läsa mer om [hur du aktiverar cookies](https://support.google.com/chrome/answer/95647)från tredje part.

   ![Cookie-fel i Chrome i Incognito-läge](assets/chrome-cookies-incognito-dialog.png)
