---
title: Använd Connected Assets när du vill dela DAM-resurser i [!DNL Sites]
description: Använd resurser som är tillgängliga på en fjärrdistribution av [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] data.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 29c3ca56281c482f195d84590ceb4ef07c556e64
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 39%

---


# Använd Connected Assets när du vill dela DAM-resurser i [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

I stora företag kan den infrastruktur som krävs för att skapa webbplatser vara distribuerad. Ibland kan funktionerna för att skapa webbplatser och de digitala resurser som används för att skapa webbplatserna finnas i olika distributioner. En orsak kan vara att befintliga distributioner som behövs för att fungera tillsammans distribueras geografiskt. En annan orsak kan vara förvärv som leder till heterogen infrastruktur som moderbolaget vill använda tillsammans.

Användare kan skapa webbsidor i [!DNL Experience Manager Sites]. [!DNL Experience Manager Assets] är det DAM-system (Digital Asset Management) som tillhandahåller de resurser som krävs för webbplatser. [!DNL Experience Manager] har nu stöd för ovanstående användningsexempel genom integrering  [!DNL Sites] och  [!DNL Assets].

## Översikt över Connected Assets {#overview-of-connected-assets}

När du redigerar sidor i [!UICONTROL Page Editor] som målmål kan författarna sömlöst söka efter, bläddra bland och bädda in resurser från en annan [!DNL Assets]-distribution som fungerar som en källa för resurser. Administratörerna skapar en engångsintegrering av en distribution av [!DNL Experience Manager] med [!DNL Sites]-funktioner med en annan distribution av [!DNL Experience Manager] med [!DNL Assets]-funktioner.

För [!DNL Sites]-författare är fjärrresurserna tillgängliga som skrivskyddade lokala resurser. Funktionen stöder enkel sökning och användning av ett fåtal fjärresurser i taget. Om du vill göra många fjärrresurser tillgängliga för en [!DNL Sites]-distribution på en gång bör du överväga att migrera resurserna samtidigt.

### Förutsättningar och distributioner som stöds {#prerequisites}

Innan du använder eller konfigurerar den här funktionen bör du kontrollera följande:

* Användarna ingår i rätt användargrupper för varje distribution.
* För [!DNL Adobe Experience Manager]-distributionstyper uppfylls ett av villkoren. Mer information om hur den här funktionen fungerar i [!DNL Experience Manager] 6.5 finns i [Anslutna resurser i Experience Manager 6.5-resurser](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/use-assets-across-connected-assets-instances.html).

   |  | [!DNL Sites] som  [!DNL Cloud Service] | [!DNL Experience Manager] 6.5  [!DNL Sites] på AMS | [!DNL Experience Manager] 6.5  [!DNL Sites] på plats |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]som[!DNL Cloud Service]** | Stöds | Stöds | Stöds |
   | **[!DNL Experience Manager]6.5  [!DNL Assets] på AMS** | Stöds | Stöds | Stöds |
   | **[!DNL Experience Manager]6.5  [!DNL Assets] på plats** | Stöds ej | Stöds ej | Stöds ej |

### Filformat som stöds {#mimetypes}

Författare söker efter bilder och följande typer av dokument i Content Finder och använder de sökbara resurserna i Page Editor. Dokument läggs till i `Download`-komponenten och bilder till `Image`-komponenten. Författare lägger också till fjärrresurserna i valfri anpassad [!DNL Experience Manager]-komponent som utökar standardkomponenterna för `Download` eller `Image`. De format som stöds är:

* **Bildformat**: De format som  [Image-](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html) komponenten stöder. [!DNL Dynamic Media] bilder stöds inte.
* **Dokumentformat**: Se vilka  [dokumentformat](file-format-support.md#document-formats) som stöds.

### Användare och grupper som krävs {#users-and-groups-involved}

De olika roller som krävs för att konfigurera och använda funktionen och motsvarande användargrupper beskrivs nedan. Lokalt omfång används för de fall där en författare skapar en webbsida. Fjärromfång används för DAM-distributionen som är värd för de nödvändiga resurserna. [!DNL Sites]-författaren hämtar dessa fjärrresurser.

| Roll | Omfång | Användargrupp | Användarnamn i genomgång | Krav |
|----------------------------------|--------|------------------------------------------------------------------------------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Sites] administratör | Lokalt | [!DNL Experience Manager] `administrators` | `admin` | Konfigurera [!DNL Experience Manager] och konfigurera integrering med fjärrdistributionen [!DNL Assets]. |
| DAM-användare | Lokalt | `Authors` | `ksaner` | Används för att visa och duplicera de hämtade resurserna i `/content/DAM/connectedassets/`. |
| [!DNL Sites] author | Lokalt | `Authors` (med läsåtkomst på fjärr-DAM och författaråtkomst lokalt  [!DNL Sites]) | `ksaner` | Slutanvändaren är [!DNL Sites]-författare som använder den här integreringen för att förbättra innehållets hastighet. Författarna söker efter och bläddrar bland resurser i fjärr-DAM med [!UICONTROL Content Finder] och använder de bilder som krävs på lokala webbsidor. Autentiseringsuppgifterna för `ksaner` DAM-användaren används. |
| [!DNL Assets] administratör | Fjärr | [!DNL Experience Manager] `administrators` | `admin` på fjärrkontrollen  [!DNL Experience Manager] | Konfigurerar CORS (Cross-Origin Resource Sharing). |
| DAM-användare | Fjärr | `Authors` | `ksaner` på fjärrkontrollen  [!DNL Experience Manager] | Författarrollen på fjärrdistributionen [!DNL Experience Manager]. Söker efter och bläddrar bland resurser i Connected Assets med hjälp av [!UICONTROL Content Finder]. |
| DAM-distributör (teknisk användare) | Fjärr | [!DNL Sites] `Authors` | `ksaner` på fjärrkontrollen  [!DNL Experience Manager] | Den här användaren som finns på fjärrdistributionen används av den lokala servern [!DNL Experience Manager] (inte författarrollen [!DNL Sites]) för att hämta fjärrresurserna, för författaren [!DNL Sites]. Den här rollen är inte densamma som de två `ksaner`-rollerna ovan och den tillhör en annan användargrupp. |

## Konfigurera en anslutning mellan [!DNL Sites] och [!DNL Assets] distributioner {#configure-a-connection-between-sites-and-assets-deployments}

En [!DNL Experience Manager]-administratör kan skapa den här integreringen. Behörigheterna som krävs för att använda det skapas via användargrupper när de har skapats. Användargrupperna definieras i [!DNL Sites]-distributionen och i DAM-distributionen.

Så här konfigurerar du anslutna resurser och lokal [!DNL Sites]-anslutning:

1. Få åtkomst till en befintlig [!DNL Sites]-distribution eller skapa en distribution med följande kommando:

   1. Kör följande kommando på en terminal i JAR-filens mapp för att skapa varje [!DNL Experience Manager]-server.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. Efter några minuter startas [!DNL Experience Manager]-servern. Ta denna [!DNL Sites]-distribution som den lokala datorn för webbsidesredigering, till exempel `https://[local_sites]:4502`.

1. Kontrollera att användare och roller med lokalt omfång finns i [!DNL Sites]-distributionen och i [!DNL Assets]-distributionen på AMS. Skapa en teknisk användare av [!DNL Assets]-distributionen och lägg till i användargruppen som nämns i [användare och grupper som är inblandade](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Åtkomst till den lokala [!DNL Sites]-distributionen på `https://[local_sites]:4502`. Klicka på **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Connected Assets Configuration]** och ange följande värden:

   1. [!DNL Assets] platsen är  `https://[assets_servername_ams]:[port]`.
   1. Autentiseringsuppgifter för en DAM-distributör (teknisk användare).
   1. I fältet **[!UICONTROL Mount Point]** anger du den lokala [!DNL Experience Manager]-sökvägen där [!DNL Experience Manager] hämtar resurserna. Till exempel, mappen `remoteassets`.

   1. Justera värdena för **[!UICONTROL Original Binary transfer optimization Threshold]** beroende på ditt nätverk. En resursåtergivning med en storlek som är större än detta tröskelvärde överförs asynkront.
   1. Välj **[!UICONTROL Datastore Shared with Connected Assets]** om du använder ett datalager för att lagra dina resurser och datalagret är den gemensamma lagringsplatsen mellan båda distributionerna. I det här fallet spelar tröskelvärdet ingen roll eftersom resursernas binärfiler finns i datalagret och de inte överförs.

   ![En typisk konfiguration för Connected Assets](assets/connected-assets-typical-config.png)

   *Bild: En typisk konfiguration för Connected Assets.*

1. Inaktivera arbetsflödets startprogram eftersom resurserna redan har bearbetats och återgivningarna hämtas. Justera startkonfigurationerna för den lokala ([!DNL Sites])-distributionen för att exkludera mappen `connectedassets` som fjärrresurserna hämtas till.

   1. Vid [!DNL Sites]-distribution klickar du på **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Launchers]**.

   1. Sök efter startprogram med arbetsflöden som **[!UICONTROL DAM Update Asset]** och **[!UICONTROL DAM Metadata Writeback]**.

   1. Välj startprogrammet för arbetsflödet och klicka på **[!UICONTROL Properties]** i åtgärdsfältet.

   1. I guiden [!UICONTROL Properties] ändrar du fälten **[!UICONTROL Path]** som följande mappningar för att uppdatera deras reguljära uttryck så att den inte omfattar monteringspunkten **[!UICONTROL connectedassets]**.

   | Före | Efter |
   | ------------------------------------------------------- | -------------------------------------------------------------------------- |
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Alla återgivningar som är tillgängliga på fjärrdistributionen hämtas när författare hämtar en resurs. Om du vill skapa fler återgivningar av en hämtad resurs hoppar du över det här konfigurationssteget. Arbetsflödet [!UICONTROL DAM Update Asset] aktiveras och skapar fler återgivningar. Dessa återgivningar är bara tillgängliga på den lokala distributionen av [!DNL Sites] och inte på den fjärranslutna DAM-distributionen.

1. Lägg till [!DNL Sites]-distributionen som en av **[!UICONTROL Allowed Origins]** på fjärr-CORS-konfigurationen.[!DNL Assets']

   1. Logga in med administratörsautentiseringsuppgifterna. Sök efter `Cross-Origin`. Öppna **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.

   1. Om du vill skapa en CORS-konfiguration för [!DNL Sites]-distribution klickar du på Lägg till alternativ ![Ikon för att lägga till resurser](assets/do-not-localize/aem_assets_add_icon.png) bredvid **[!UICONTROL Adobe Granite Cross-Origin Resource Sharing Policy]**.

   1. I fältet **[!UICONTROL Allowed Origins]** anger du URL:en för den lokala [!DNL Sites], det vill säga `https://[local_sites]:[port]`. Spara konfigurationen.

## Använda fjärresurser {#use-remote-assets}

Webbplatsens författare använder Content Finder för att ansluta till DAM-distributionen. Författarna kan bläddra bland, söka efter och dra fjärresurserna till en komponent. Om du vill autentisera med DAM-fjärrdistributionen bör du ha DAM-användarens autentiseringsuppgifter som du fått av administratören till hands.

Författare kan använda resurserna som finns på den lokala DAM-resursen och den fjärranslutna DAM-distributionen på en enda webbsida. Använd Content Finder för att växla mellan att söka i det lokala DAM-systemet eller söka i det fjärranslutna DAM-systemet.

Endast de taggar för fjärrresurser som har en exakt motsvarande tagg tillsammans med samma taxonomihierarki, som är tillgängliga för den lokala [!DNL Sites]-distributionen, hämtas. Alla andra taggar tas bort. Författare kan söka efter fjärrresurser med hjälp av alla taggar som finns i fjärrdistributionen [!DNL Experience Manager], eftersom det ger en fulltextsökning.

### Genomgång av användningen {#walk-through-of-usage}

Använd konfigurationen ovan när du vill prova redigeringsfunktionen och se hur den fungerar. Använd de dokument eller bilder du vill ha på den fjärranslutna DAM-distributionen.

1. Navigera till gränssnittet [!DNL Assets] i fjärrdistributionen genom att gå till **[!UICONTROL Assets]** > **[!UICONTROL Files]** från arbetsytan [!DNL Experience Manager]. Du kan även få åtkomst till `https://[assets_servername_ams]:[port]/assets.html/content/dam` i en webbläsare. Ladda upp de resurser du vill ha.
1. I [!DNL Sites]-distributionen klickar du på **[!UICONTROL Impersonate as]** i profilaktiveraren i det övre högra hörnet. Ange `ksaner` som användarnamn, markera det angivna alternativet och klicka på **[!UICONTROL OK]**.
1. Öppna en We.Retail-webbsida på **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Redigera sidan. Du kan även öppna `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` i en webbläsare när du vill redigera en sida.

   Klicka på **[!UICONTROL Toggle Side Panel]** överst till vänster på sidan.

1. Öppna fliken [!UICONTROL Assets] och klicka på **[!UICONTROL Log in to Connected Assets]**.
1. Ange inloggningsuppgifterna, `ksaner` som användarnamn och `password` som lösenord. Den här användaren har redigeringsbehörighet för båda [!DNL Experience Manager]-distributionerna.
1. Sök efter resursen som du har lagt till i DAM. Fjärresurserna visas i den vänstra panelen. Filtrera efter bilder eller dokument och filtrera efter olika typer av dokument som stöds. Dra bilderna till en `Image`-komponent och dokument till en `Download`-komponent.

   De hämtade resurserna är skrivskyddade i den lokala [!DNL Sites]-distributionen. Du kan fortfarande använda alternativen i dina [!DNL Sites]-komponenter för att redigera den hämtade resursen. Redigering med komponenter är icke-destruktiv.

   ![Alternativ för att filtrera dokumenttyper och bilder vid sökning efter resurser på DAM-fjärrdistribution](assets/filetypes_filter_connected_assets.png)

   *Bild: Alternativ för att filtrera dokumenttyper och bilder vid sökning efter resurser på DAM-fjärrdistribution.*

1. En Sites-författare meddelas om en resurs hämtas asynkront och om en hämtningsåtgärd misslyckas. Under eller efter redigeringen kan författare se detaljerad information om hämtningsåtgärder och fel i användargränssnittet för [asynkrona jobb](/help/operations/asynchronous-jobs.md).

   ![Meddelande om asynkron hämtning av resurser som sker i bakgrunden.](assets/assets_async_transfer_fails.png)

   *Bild: Meddelande om asynkron hämtning av resurser som sker i bakgrunden.*

1. När du publicerar en sida visar [!DNL Experience Manager] en fullständig lista över resurser som används på sidan. Kontrollera att fjärresurserna har hämtats vid publiceringen. Se [användargränssnittet för asynkrona jobb](/help/operations/asynchronous-jobs.md) om du vill kontrollera status för varje hämtad resurs.

   >[!NOTE]
   >
   >Sidan publiceras även om en eller flera fjärresurser inte hämtats. Komponenten som använder fjärresursen publiceras tom. I meddelandefältet [!DNL Experience Manager] visas ett meddelande om fel som visas på sidan för asynkrona jobb.

>[!CAUTION]
>
>När de hämtade fjärrresurserna har använts på en webbsida är de sökbara och användbara för alla som har behörighet att komma åt den lokala mappen. De hämtade resurserna lagras i den lokala mappen (`connectedassets` i ovanstående genomgång). Resurserna är också sökbara och synliga i det lokala datalagret via [!UICONTROL Content Finder].

De hämtade resurserna kan användas som andra lokala resurser, förutom att associerade metadata inte kan redigeras.

<!-- TBD: Uncomment after verification for Dec release.

### Check use of an asset across other pages {#asset-usage-references}

[!DNL Experience Manager] also lets you check all the incoming references to an asset, that is, the usage of an asset in remote [!DNL Sites] and in compound assets. Authors of webpages on [!DNL Experience Manager Sites] deployment can use an asset on a remote [!DNL Assets] deployment using the Connected Assets functionality. The [!UICONTROL References] tab in an asset's [!UICONTROL Properties] page lists the local and remote references of the asset.

Users can view incoming references of the assets and move or delete the asset.

-->

## Begränsningar och bästa praxis {#tip-and-limitations}

* Konfigurera funktionen [Asset Insight](/help/assets/assets-insights.md) i [!DNL Sites]-instansen för att få information om resursanvändning.

### Behörigheter och resurshantering {#permissions-and-managing-assets}

* Lokala resurser synkroniseras inte med de ursprungliga resurserna i fjärrdistributionen. Ändringar, borttagningar eller återkallande av behörigheter i DAM-distributionen sprids inte längre ned i kedjan.
* Lokala resurser är skrivskyddade kopior. [!DNL Experience Manager] -komponenter gör icke-förstörande redigeringar av resurser. Inga andra redigeringar tillåts.
* Lokalt hämtade resurser är endast tillgängliga för redigeringsändamål. Det går inte att använda arbetsflöden för resursuppdatering och metadata kan inte redigeras.
* Endast bilder och dokumentformaten i listan stöds. [!DNL Dynamic Media] resurser, innehållsfragment och Experience Fragments stöds inte.
* [!DNL Experience Manager] hämtar inte metadatamatcheman. Det innebär att alla hämtade metadata inte visas. Om schemat uppdateras separat visas alla egenskaper.
* Alla [!DNL Sites]-författare har läsbehörighet för de hämtade kopiorna, även om författare inte har åtkomst till fjärr-DAM-distributionen.
* Det finns inte API-stöd för att anpassa integreringen.
* Funktionen stöder smidig sökning och användning av fjärresurser. Om du vill göra många fjärresurser tillgängliga i den lokala distributionen på en gång bör du överväga att migrera resurserna.
* Det går inte att använda en fjärrresurs som sidminiatyr i [!UICONTROL Page Properties]-användargränssnittet. Du kan ange en miniatyrbild för en webbsida i [!UICONTROL Page Properties]-användargränssnittet från [!UICONTROL Thumbnail] genom att klicka på [!UICONTROL Select Image].

### Konfigurera och licensiera {#setup-licensing}

* [!DNL Assets] det  [!DNL Adobe Managed Services] finns stöd för distribution på.
* [!DNL Sites] kan ansluta till en enda  [!DNL Assets] databas åt gången.
* En licens för [!DNL Assets] som fungerar som fjärrdatabas.
* En eller flera licenser av [!DNL Sites] fungerar som lokal redigeringsdistribution.

### Användning {#usage}

* Användare kan söka efter fjärrresurser och dra dem på den lokala sidan när de redigerar. Inga andra funktioner stöds.
* Tidsgränsen för hämtning är 5 sekunder. Författare kan ha problem med att hämta resurser, till exempel om det råder nätverksproblem. Författare kan försöka igen genom att dra fjärrresursen från [!UICONTROL Content Finder] till [!UICONTROL Page Editor].
* Enkla redigeringar som är icke-destruktiva och redigering som stöds via `Image`-komponenten kan tillämpas på hämtade resurser. Resurserna är skrivskyddade.
* Det enda sättet att hämta resursen på nytt är att dra den till en sida. Det finns inget API-stöd eller andra metoder för att hämta om en resurs för att uppdatera den.
* Om resurser tas bort från DAM används de fortfarande på [!DNL Sites]-sidor.

## Felsöka problem {#troubleshoot}

Följ de här stegen för att felsöka det vanliga felscenariot:

* Om du inte kan söka efter fjärrresurser från [!UICONTROL Content Finder] kontrollerar du att de roller och behörigheter som krävs finns på plats.
* En resurs som hämtats från fjärrdammen kanske inte publiceras på en webbsida av en eller flera orsaker. Den finns inte på fjärrservern, saknar behörighet att hämta den eller så kan nätverksfel vara orsaken. Se till att resursen inte tas bort från fjärr-DAM. Se till att rätt behörigheter finns och att kraven är uppfyllda. Försök lägga till resursen på sidan igen och publicera den på nytt. Kontrollera i [listan över asynkrona jobb](/help/operations/asynchronous-jobs.md) om fel uppstod vid hämtning av resurser.
* Om du inte kan komma åt fjärr-DAM-distributionen från den lokala [!DNL Sites]-distributionen kontrollerar du att cookies mellan platser tillåts. Om cookies mellan platser blockeras kanske de två distributionerna av [!DNL Experience Manager] inte autentiseras. [!DNL Google Chrome] i Incognito-läge kan till exempel blockera cookies från tredje part. Om du vill tillåta cookies i [!DNL Chrome]-webbläsaren klickar du på ögonikonen i adressfältet, navigerar till Plats som inte fungerar > Blockerad, markerar fjärr-DAM-URL:en och tillåter inloggningstokencookie. Du kan även läsa mer i hjälpen om [hur du aktiverar cookies](https://support.google.com/chrome/answer/95647) från tredje part.

   ![Cookie-fel i Chrome i Incognito-läge](assets/chrome-cookies-incognito-dialog.png)
