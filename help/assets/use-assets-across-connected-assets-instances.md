---
title: Använd anslutna resurser för att dela DAM-resurser i redigeringsarbetsflödet för [!DNL Adobe Experience Manager Sites].
description: Använd resurser som är tillgängliga på en [!DNL Adobe Experience Manager Assets]-fjärrdistribution när du skapar webbsidor på en annan [!DNL Adobe Experience Manager Sites]-distribution.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5e89a44cb727547af9db783662e035c4e2102a4e

---


# Använd Connected Assets när du vill dela DAM-resurser i [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

I stora företag kan den infrastruktur som krävs för att skapa webbplatser vara distribuerad. Ibland kan funktionerna för att skapa webbplatser och de digitala resurser som används för att skapa webbplatserna finnas i olika distributioner. En orsak kan vara att befintliga distributioner som behövs för att fungera tillsammans distribueras geografiskt. En annan orsak kan vara förvärv som leder till heterogen infrastruktur som moderbolaget vill använda tillsammans.

Användare kan skapa webbsidor i [!DNL Experience Manager Sites]. [!DNL Experience Manager Assets] är det DAM-system (Digital Asset Management) som tillhandahåller de resurser som krävs för webbplatser. [!DNL Experience Manager] har nu stöd för ovanstående användningsexempel genom integrering [!DNL Sites] och [!DNL Assets].

## Översikt över Connected Assets {#overview-of-connected-assets}

When editing pages in [!UICONTROL Page Editor], the authors can seamlessly search, browse, and embed assets from a different [!DNL Assets] deployment. Administratörerna skapar en engångs integrering av en distribution av [!DNL Sites] med en annan (fjärransluten) distribution av [!DNL Assets].

For the [!DNL Sites] authors, the remote assets are available as read-only local assets. Funktionen stöder enkel sökning och användning av ett fåtal fjärresurser i taget. To make many remote assets available on a [!DNL Sites] deployment in one-go, consider migrating the assets in bulk.

### Förutsättningar och distributioner som stöds {#prerequisites}

Innan du använder eller konfigurerar den här funktionen bör du kontrollera följande:

* Användarna ingår i lämpliga användargrupper för varje distribution.
* Ett av villkoren som stöds är uppfyllt för [!DNL Adobe Experience Manager] distributionstyper. Mer information om [!DNL Experience Manager] 6.5 finns i [Funktionen för anslutna resurser i Experience Manager 6.5 Assets](https://docs.adobe.com/content/help/en/experience-manager-65/assets/using/use-assets-across-connected-assets-instances.html).

   |  | [!DNL Sites] som molntjänst | [!DNL Experience Manager] 6.5 [!DNL Sites] på AMS | [!DNL Experience Manager] 6.5 [!DNL Sites] på plats |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]som molntjänst ** | Stöds | Stöds | Stöds |
   | **[!DNL Experience Manager]6.5[!DNL Assets]på AMS ** | Stöds | Stöds | Stöds |
   | **[!DNL Experience Manager]6.5[!DNL Assets]på plats ** | Stöds ej | Stöds ej | Stöds ej |

### Filformat som stöds {#mimetypes}

Författare kan söka efter bilder och följande typer av dokument i Content Finder och använda resurserna i Page Editor. Dokument kan läggas till i `Download`-komponenten och bilder kan läggas till i `Image`-komponenten. Authors can also add the remote assets in any custom [!DNL Experience Manager] component that extends the default `Download` or `Image` components. De format som stöds är:

* **Bildformat**: De format som stöds av [bildkomponenten](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/image.html) . [!DNL Dynamic Media] bilder stöds inte.
* **Dokumentformat**: Se [Dokumentformat som stöds i Connected Assets](file-format-support.md#document-formats).

### Användare och grupper som krävs {#users-and-groups-involved}

De olika roller som krävs för att konfigurera och använda funktionen och motsvarande användargrupper beskrivs nedan. Lokalt omfång används för de fall där en författare skapar en webbsida. Fjärromfång används för DAM-distributionen som är värd för de nödvändiga resurserna. The [!DNL Sites] author fetches these remote assets.

| Roll | Omfång | Användargrupp | Användarnamn i genomgång | Krav |
|----------------------------------|--------|------------------------------------------------------------------------------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Sites] administratör | Lokalt | [!DNL Experience Manager] `administrators` | `admin` | Set up [!DNL Experience Manager] and configure integration with the remote [!DNL Assets] deployment. |
| DAM-användare | Lokalt | `Authors` | `ksaner` | Används för att visa och duplicera de hämtade resurserna i `/content/DAM/connectedassets/`. |
| [!DNL Sites] author | Lokalt | `Authors` (med läsåtkomst på fjärr-DAM och författaråtkomst lokalt [!DNL Sites]) | `ksaner` | End user are [!DNL Sites] authors who use this integration to improve their content velocity. The authors search and browse assets in remote DAM using [!UICONTROL Content Finder] and using the required images in local web pages. Autentiseringsuppgifterna för `ksaner` DAM-användaren används. |
| [!DNL Assets] administratör | Fjärr | [!DNL Experience Manager] `administrators` | `admin` på fjärrkontrollen [!DNL Experience Manager] | Konfigurerar CORS (Cross-Origin Resource Sharing). |
| DAM-användare | Fjärr | `Authors` | `ksaner` på fjärrkontrollen [!DNL Experience Manager] | Author role on the remote [!DNL Experience Manager] deployment. Search and browse assets in Connected Assets using the [!UICONTROL Content Finder]. |
| DAM-distributör (teknisk användare) | Fjärr | [!DNL Sites] `Authors` | `ksaner` på fjärrkontrollen [!DNL Experience Manager] | This user present on the remote deployment is used by [!DNL Experience Manager] local server (not the [!DNL Sites] author role) to fetch the remote assets, on behalf of [!DNL Sites] author. Den här rollen är inte densamma som de två `ksaner`-rollerna ovan och den tillhör en annan användargrupp. |

## Configure a connection between [!DNL Sites] and [!DNL Assets] deployments {#configure-a-connection-between-sites-and-assets-deployments}

An [!DNL Experience Manager] administrator can create this integration. Once created, the permissions required to use it are established via user groups that are defined on the [!DNL Sites] deployment and on the DAM deployment.

To configure Connected Assets and local [!DNL Sites] connectivity, follow these steps.

1. Access an existing [!DNL Sites] deployment or create a deployment using the following command:

   1. In the folder of the JAR file, execute the following command on a terminal to create each [!DNL Experience Manager] server.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. After a few minutes, the [!DNL Experience Manager] server starts successfully. Consider this [!DNL Sites] deployment as the local machine for web page authoring, say at `https://[local_sites]:4502`.

1. Ensure that the users and roles with local scope exist on the [!DNL Sites] deployment and on the [!DNL Assets] deployment on AMS. Create a technical user on [!DNL Assets] deployment and add to the user group mentioned in [users and groups involved](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Åtkomst till den lokala [!DNL Sites] distributionen på `https://[local_sites]:4502`. Klicka på **[!UICONTROL Verktyg]** > **[!UICONTROL Resurser]** > Konfiguration **[!UICONTROL av]** anslutna resurser och ange följande värden:

   1. [!DNL Assets] platsen är `https://[assets_servername_ams]:[port]`.
   1. Autentiseringsuppgifter för en DAM-distributör (teknisk användare).
   1. I fältet **[!UICONTROL Monteringspunkt]** anger du den lokala [!DNL Experience Manager] sökvägen där [!DNL Experience Manager] resurserna hämtas. Till exempel, mappen `remoteassets`.

   1. Justera värdena för det **[!UICONTROL ursprungliga tröskelvärdet för optimering av binär överföring]** beroende på nätverket. En resursåtergivning med en storlek som är större än detta tröskelvärde överförs asynkront.
   1. Select **[!UICONTROL Datastore Shared with Connected Assets]**, if you use a datastore to store your assets and the Datastore is the common storage between both deployments. I det här fallet spelar tröskelvärdet ingen roll eftersom resursernas binärfiler finns i datalagret och de inte överförs.
      ![En typisk konfiguration för Connected Assets](assets/connected-assets-typical-config.png)

      *Bild: En typisk konfiguration för Connected Assets.*

1. Inaktivera arbetsflödets startprogram eftersom resurserna redan har bearbetats och återgivningarna hämtas. Adjust the launcher configurations on the local ([!DNL Sites]) deployment to exclude the `connectedassets` folder, in which the remote assets are fetched.

   1. Vid [!DNL Sites] distributionen klickar du på **[!UICONTROL Verktyg]** > **[!UICONTROL Arbetsflöde]** > **[!UICONTROL Startprogram]**.

   1. Sök efter startare med arbetsflöden som **[!UICONTROL DAM Update Asset]** och **[!UICONTROL DAM Metadata Writeback]**.

   1. Select the workflow launcher and click **[!UICONTROL Properties]** on the action bar.

   1. In the [!UICONTROL Properties] wizard, change the **[!UICONTROL Path]** fields as the following mappings to update their regular expressions to exclude the mount point **[!UICONTROL connectedassets]**.
   | Före | Efter |
   | ------------------------------------------------------- | -------------------------------------------------------------------------- |
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Alla återgivningar som är tillgängliga på fjärrdistributionen hämtas när författare hämtar en resurs. Om du vill skapa fler återgivningar av en hämtad resurs hoppar du över det här konfigurationssteget. The [!UICONTROL DAM Update Asset] workflow gets triggered and creates more renditions. These renditions are available only on the local [!DNL Sites] deployment and not on the remote DAM deployment.

1. Lägg till [!DNL Sites] instansen som ett av **[!UICONTROL Tillåtna original]** i fjärr- [!DNL Assets'] CORS-konfigurationen.

   1. Logga in med administratörsautentiseringsuppgifterna. Search for `Cross-Origin`. Öppna **[!UICONTROL Verktyg]** > **[!UICONTROL Åtgärder]** > **[!UICONTROL Webbkonsol]**.

   1. Om du till [!DNL Sites] exempel vill skapa en CORS-konfiguration klickar du på ![ikonen aem_assets_add_icon](assets/do-not-localize/aem_assets_add_icon.png) bredvid **[!UICONTROL Adobe Granite-resursdelningspolicy]** för korsursprung.

   1. In the field **[!UICONTROL Allowed Origins]**, input the URL of the local [!DNL Sites], that is, `https://[local_sites]:[port]`. Spara konfigurationen.

## Använda fjärresurser {#use-remote-assets}

Webbplatsförfattare använder Content Finder för att ansluta till DAM-instansen. Författarna kan bläddra bland, söka efter och dra fjärresurserna till en komponent. Om du vill autentisera med DAM-fjärrdistributionen bör du ha DAM-användarens autentiseringsuppgifter som du fått av administratören till hands.

Upphovsmannen kan använda resurserna som finns på den lokala DAM- och fjärrinstansen av DAM på en enda webbsida. Använd Content Finder för att växla mellan att söka i det lokala DAM-systemet eller söka i det fjärranslutna DAM-systemet.

Only those tags of remote assets are fetched that have an exact corresponding tag along with the same taxonomy hierarchy, available on the local [!DNL Sites] instance. Alla andra taggar tas bort. Authors can search for remote assets using all the tags present on the remote [!DNL Experience Manager] deployment, as it offers a full-text search.

### Genomgång av användningen {#walk-through-of-usage}

Använd konfigurationen ovan när du vill prova redigeringsfunktionen och se hur den fungerar. Använd de dokument eller bilder du vill ha på den fjärranslutna DAM-distributionen.

1. Navigera till [!DNL Assets] gränssnittet på fjärrdistributionen genom att gå till **[!UICONTROL Resurser]** > **[!UICONTROL Filer]** från [!DNL Experience Manager] arbetsytan. Du kan även få åtkomst till `https://[assets_servername_ams]:[port]/assets.html/content/dam` i en webbläsare. Ladda upp de resurser du vill ha.
1. On the [!DNL Sites] instance, in the profile activator in the upper-right corner, click **[!UICONTROL Impersonate as]**. Provide `ksaner` as user name, select the option provided, and click **[!UICONTROL OK]**.
1. Öppna en webbsida för Vi.Butiker på **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Redigera sidan. Du kan även öppna `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` i en webbläsare när du vill redigera en sida.

   Klicka på **[!UICONTROL Växla sidopanel]** i det övre vänstra hörnet på sidan.

1. Öppna fliken [!UICONTROL Resurser] och klicka på **[!UICONTROL Logga in på Anslutna resurser]**.
1. Ange inloggningsuppgifterna, `ksaner` som användarnamn och `password` som lösenord. This user has authoring permissions on both the [!DNL Experience Manager] deployments.
1. Sök efter resursen som du har lagt till i DAM. Fjärresurserna visas i den vänstra panelen. Filtrera efter bilder eller dokument och filtrera efter olika typer av dokument som stöds. Dra bilderna till en `Image`-komponent och dokument till en `Download`-komponent.

   The fetched assets are read-only on the local [!DNL Sites] deployment. You can still use the options provided by your [!DNL Sites] components to edit the fetched asset. Redigering med komponenter är icke-destruktiv.

   ![Alternativ för att filtrera dokumenttyper och bilder vid sökning efter resurser på DAM-fjärrdistribution](assets/filetypes_filter_connected_assets.png)

   *Bild: Alternativ för att filtrera dokumenttyper och bilder vid sökning efter resurser på DAM-fjärrdistribution.*

1. En Sites-författare meddelas om en resurs hämtas asynkront och om en hämtningsåtgärd misslyckas. Under eller efter redigeringen kan författare se detaljerad information om hämtningsåtgärder och fel i användargränssnittet för [asynkrona jobb](/help/assets/asynchronous-jobs.md).

   ![Meddelande om asynkron hämtning av resurser som sker i bakgrunden.](assets/assets_async_transfer_fails.png)

   *Bild: Meddelande om asynkron hämtning av resurser som sker i bakgrunden.*

1. When publishing a page, [!DNL Experience Manager] displays a complete list of assets that are used in the page. Kontrollera att fjärresurserna har hämtats vid publiceringen. Se [användargränssnittet för asynkrona jobb](/help/assets/asynchronous-jobs.md) om du vill kontrollera status för varje hämtad resurs.

   >[!NOTE]
   >
   >Sidan publiceras även om en eller flera fjärresurser inte hämtats. Komponenten som använder fjärresursen publiceras tom. The [!DNL Experience Manager] notification area displays a notification for errors that show in async jobs page.

>[!CAUTION]
>
>När de hämtade fjärresurserna har använts på en webbsida är de sökbara och användbara för alla som har behörighet att komma åt den lokala mappen där de hämtade resurserna lagras (`connectedassets` i ovanstående genomgång). The assets are also searchable and visible in the local repository via [!UICONTROL Content Finder].

De hämtade resurserna kan användas som andra lokala resurser, förutom att associerade metadata inte kan redigeras.

## Begränsningar {#limitations}

### Behörigheter och hantering av resurser {#permissions-and-managing-assets}

* Lokala resurser synkroniseras inte med de ursprungliga resurserna i fjärrdistributionen. Ändringar, borttagningar eller återkallande av behörigheter i DAM-distributionen sprids inte längre ned i kedjan.
* Lokala resurser är skrivskyddade kopior. [!DNL Experience Manager] -komponenter gör icke-förstörande redigeringar av resurser. Inga andra redigeringar tillåts.
* Lokalt hämtade resurser är endast tillgängliga för redigeringsändamål. Det går inte att använda arbetsflöden för resursuppdatering och metadata kan inte redigeras.
* Endast bilder och dokumentformaten i listan stöds. [!DNL Dynamic Media] resurser, innehållsfragment och Experience Fragments stöds inte.
* Metadatascheman hämtas inte.
* All [!DNL Sites] authors have read permissions on the fetched copies, even if authors do not have access to the remote DAM deployment.
* Det finns inte API-stöd för att anpassa integreringen.
* Funktionen stöder smidig sökning och användning av fjärresurser. Om du vill göra många fjärresurser tillgängliga i den lokala distributionen på en gång bör du överväga att migrera resurserna.
* Det går inte att använda en fjärrresurs som sidminiatyr i [!UICONTROL användargränssnittet för Sidegenskaper] . Du kan ange en miniatyrbild för en webbsida i [!UICONTROL användargränssnittet för Sidegenskaper] från [!UICONTROL miniatyrbilden] genom att klicka på [!UICONTROL Välj bild].

### Konfigurera och licensiera {#setup-licensing}

* [!DNL Assets] kan användas på [!DNL Adobe Managed Services] .
* [!DNL Sites] kan ansluta till en enda [!DNL Assets] databas åt gången.
* A license of [!DNL Assets] working as remote repository.
* One or more licenses of [!DNL Sites] working as local authoring deployment.

### Användning {#usage}

* De enda funktioner som stöds är sökning efter fjärresurser och att dra fjärresurserna till den lokala sidan för att skapa innehåll.
* Tidsgränsen för hämtning är 5 sekunder. Författare kan ha problem med att hämta resurser, till exempel om det råder nätverksproblem. Författare kan försöka igen genom att dra fjärrresursen från [!UICONTROL Content Finder] till [!UICONTROL Page Editor].
* Enkla redigeringar som är icke-destruktiva och redigering som stöds via `Image`-komponenten kan tillämpas på hämtade resurser. Resurserna är skrivskyddade.

## Felsöka problem {#troubleshoot}

Följ dessa steg för att felsöka vanliga fel:

* If you cannot search for remote assets from the [!UICONTROL Content Finder], recheck and ensure that the required roles and permissions are in place.
* En resurs som hämtats från en DAM-fjärrdistribution kanske inte publiceras på en webbsida av följande skäl: Den finns inte i fjärrdistributionen, lämplig behörighet saknas för att hämta den eller nätverksfel. Se till att resursen inte tas bort från fjärr-DAM eller att behörigheterna inte ändras. Kontrollera att rätt förutsättningar uppfylls. Försök lägga till resursen på sidan igen och publicera den på nytt. Kontrollera i [listan över asynkrona jobb](/help/assets/asynchronous-jobs.md) om fel uppstod vid hämtning av resurser.
