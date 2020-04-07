---
title: Använd Connected Assets när du vill dela DAM-resurser i redigeringsarbetsflödet för Adobe Experience Manager Sites
description: Använd resurser som är tillgängliga på en fjärrdistribution av Adobe Experience Manager Assets när du skapar webbsidor på en annan Experience Manager Site-distribution.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# Använd Connected Assets när du vill dela DAM-resurser i AEM Sites {#use-connected-assets-to-share-dam-assets-in-aem-sites}

I stora företag kan den infrastruktur som krävs för att skapa webbplatser vara distribuerad. Ibland kan funktionerna för att skapa webbplatser och de digitala resurser som används för att skapa webbplatserna finnas i olika distributioner. Vissa skäl kan vara geografiskt spridda befintliga driftsättningar som måste fungera tillsammans eller förvärv som leder till heterogen infrastruktur som moderbolaget vill använda tillsammans.

AEM Sites erbjuder funktioner för att skapa webbsidor och AEM Assets är det DAM-system (Digital Asset Management) som tillhandahåller de resurser som krävs för webbplatserna. AEM stöder nu ovanstående exempel genom att integrera AEM Sites och AEM Assets.

## Översikt över Connected Assets {#overview-of-connected-assets}

När sidor redigeras i Page Editor kan författare enkelt söka efter, bläddra bland och bädda in resurser från en annan AEM Assets-distribution. En AEM-administratör kan göra en engångsintegrering av en lokal AEM Sites-distribution tillsammans med en annan (fjärransluten) AEM Assets-distribution.

Fjärresurserna är tillgängliga som skrivskyddade lokala resurser för Sites-författarna. Funktionen stöder enkel sökning och användning av ett fåtal fjärresurser i taget. Om du vill göra många fjärresurser tillgängliga för lokal distribution på en gång bör du överväga att migrera resurserna samtidigt.

### Förutsättningar och distributioner som stöds {#prerequisites}

Innan du använder eller konfigurerar den här funktionen bör du kontrollera följande:

* Användarna ingår i lämpliga användargrupper för varje distribution.
* Ett av de kriterier som stöds för Adobe Experience Manager-distributionstyper är uppfyllt.

   |  | AEM Sites as a Cloud Service | AEM 6.5 Sites i AMS | AEM 6.5 Sites på plats |
   |---|---|---|---|
   | **AEM Assets as a Cloud Service** | Stöds | Stöds | Stöds |
   | **AEM 6.5 Assets i AMS** | Stöds | Stöds | Stöds |
   | **AEM 6.5 Assets på plats** | Stöds ej | Stöds ej | Stöds ej |

### Filformat som stöds {#mimetypes}

Författare kan söka efter bilder och följande typer av dokument i Content Finder och använda resurserna i Page Editor. Dokument kan läggas till i `Download`-komponenten och bilder kan läggas till i `Image`-komponenten. Författare kan också lägga till fjärresurserna i en anpassad AEM-komponent som utökar standardversionen av `Download` eller `Image`-komponenterna. Listorna med format som stöds är:

* **Bildformat**: De bildformat som stöds av [bildkomponenten](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/image.html) stöds. Dynamic Media-bilder stöds inte.
* **Dokumentformat**: Se [Dokumentformat som stöds i Connected Assets](file-format-support.md#doc-formats).

### Användare och grupper som krävs {#users-and-groups-involved}

De olika roller som krävs för att konfigurera och använda funktionen och motsvarande användargrupper beskrivs nedan. Lokalt omfång används för de fall då en webbsida skapas av en författare. Fjärromfång används för DAM-distributionen som är värd för de nödvändiga resurserna. Sites-författaren hämtar dessa fjärresurser.

| Roll | Omfång | Användargrupp | Användarnamn i genomgång | Krav |
|----------------------------------|--------|------------------------------------------------------------------------------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AEM Sites-administratör | Lokalt | AEM-administratör | `admin` | Konfigurerar AEM, konfigurerar integrering med fjärrdistributionen av Assets. |
| DAM-användare | Lokalt | Författare | `ksaner` | Används för att visa och duplicera de hämtade resurserna i `/content/DAM/connectedassets/`. |
| AEM Sites-författare | Lokalt | Författare (med läsbehörighet på det fjärranslutna DAM-systemet och författarbehörighet på den lokala Sites-distributionen) | `ksaner` | Slutanvändare är Sites-författare som använder den här integreringen för att förbättra innehållshastigheten. Författarna söker efter och bläddrar bland resurser i fjärrversionen av DAM med hjälp av Content Finder och använder de bilder som behövs på lokala webbsidor. Autentiseringsuppgifterna för `ksaner` DAM-användaren används. |
| AEM Assets-administratör | Fjärr | AEM-administratör | `admin` på fjärr-AEM | Konfigurerar CORS (Cross-Origin Resource Sharing). |
| DAM-användare | Fjärr | Författare | `ksaner` på fjärr-AEM | Författarroll för AEM-fjärrdistributionen. Söker efter och bläddrar bland resurser i Connected Assets med hjälp av Content Finder. |
| DAM-distributör (teknisk användare) | Fjärr | paketbyggare och webbplatsförfattare | `ksaner` på fjärr-AEM | Den här användaren finns i fjärrdistributionen och används av den lokala AEM-servern (inte Sites-författarrollen) för att hämta fjärresurser på uppdrag av Sites-författaren. Den här rollen är inte densamma som de två `ksaner`-rollerna ovan och den tillhör en annan användargrupp. |

## Konfigurera en anslutning mellan Sites- och Assets-distributioner {#configure-a-connection-between-sites-and-assets-deployments}

En AEM-administratör kan skapa den här integreringen. När den har skapats anges de behörigheter som krävs för att använda den via användargrupper som definieras i Sites-distributionen och i DAM-distributionen.

Följ dessa steg när du vill konfigurera anslutningar för Connected Assets och lokala Sites-distributioner.

1. Få åtkomst till en befintlig AEM Sites-distribution eller skapa en distribution med följande kommando:

   1. Kör följande kommando på en terminal i JAR-filens mapp för att skapa varje AEM-server.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. Efter några minuter startas AEM-servern. Se den här AEM Sites-distributionen som den lokala datorn för webbsidesredigering, till exempel `https://[local_sites]:4502`.

1. Kontrollera att användare och roller med lokalt omfång finns i AEM Sites-distributionen och i AEM Assets-distributionen på AMS. Skapa en teknisk användare i Assets-distributionen och lägg till i användargruppen som nämns i [Användare och grupper som krävs](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Gå till den lokala AEM Sites-distributionen på `https://[local_sites]:4502`. Klicka på **[!UICONTROL Verktyg]** > **[!UICONTROL Resurser]** > Konfiguration **[!UICONTROL av]** anslutna resurser och ange följande värden:

   1. AEM Assets-platsen är `https://[assets_servername_ams]:[port]`.
   1. Autentiseringsuppgifter för en DAM-distributör (teknisk användare).
   1. In **[!UICONTROL Mount Point]** field, enter the local AEM path where AEM fetches the assets. Till exempel, mappen `remoteassets`.

   1. Justera värdena för det **[!UICONTROL ursprungliga tröskelvärdet för optimering av binär överföring]** beroende på nätverket. En resursåtergivning med en storlek som är större än detta tröskelvärde överförs asynkront.
   1. Select **[!UICONTROL Datastore Shared with Connected Assets]**, if you use a datastore to store your assets and the Datastore is the common storage between both AEM deployments. I det här fallet spelar tröskelvärdet ingen roll eftersom resursernas binärfiler finns i datalagret och de inte överförs.
   ![En typisk konfiguration för Connected Assets](assets/connected-assets-typical-config.png)

   *Bild: En typisk konfiguration för Connected Assets*

1. Inaktivera arbetsflödets startprogram eftersom resurserna redan har bearbetats och återgivningarna hämtas. Justera startkonfigurationerna för den lokala distributionen (AEM Sites) för att exkludera den `connectedassets`-mapp där fjärresurserna hämtas.

   1. I AEM Sites-distributionen klickar du på **[!UICONTROL Verktyg]** > **[!UICONTROL Arbetsflöde]** > **[!UICONTROL Startprogram]**.

   1. Sök efter startare med arbetsflöden som **[!UICONTROL DAM Update Asset]** och **[!UICONTROL DAM Metadata Writeback]**.

   1. Select the workflow launcher and click **[!UICONTROL Properties]** on the action bar.

   1. In the Properties wizard, change the **[!UICONTROL Path]** fields as the following mappings to update their regular expressions to exclude the mount point **[!UICONTROL connectedassets]**.
   | Före | Efter |
   |---|---|
   | /content/dam(/((?!/subassets).)*/)renditions/original | /content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original |
   | /content/dam(/.*/)renditions/original | /content/dam(/((?!connectedassets).)*/)renditions/original |
   | /content/dam(/.*)/jcr:content/metadata | /content/dam(/((?!connectedassets).)*/)jcr:content/metadata |

   >[!NOTE]
   >
   >Alla återgivningar som är tillgängliga på den fjärranslutna AEM-distributionen hämtas när författare hämtar en resurs. Om du vill skapa fler återgivningar av en hämtad resurs hoppar du över det här konfigurationssteget. DAM Update Asset-arbetsflödet aktiveras och skapar fler återgivningar. Dessa återgivningar är bara tillgängliga i den lokala Sites-distributionen, inte i DAM-fjärrdistributionen.

1. Add the AEM Sites instance as one of the **[!UICONTROL Allowed Origins]** on the remote AEM Assets&#39; CORS configuration.

   1. Logga in med administratörsuppgifterna. Sök efter Cross-Origin. Öppna **[!UICONTROL Verktyg]** > **[!UICONTROL Åtgärder]** > **[!UICONTROL Webbkonsol]**.

   1. Om du vill skapa en CORS-konfiguration för en AEM Sites-instans klickar du på ![ikonen aem_assets_add_icon](assets/do-not-localize/aem_assets_add_icon.png) bredvid **[!UICONTROL Adobe Granite-resursdelningspolicy]** för korsursprung.

   1. In the field **[!UICONTROL Allowed Origins]**, input the URL of the local Sites, that is, `https://[local_sites]:[port]`. Spara konfigurationen.

## Använda fjärresurser {#use-remote-assets}

Webbplatsförfattare använder Content Finder för att ansluta till DAM-instansen. Författarna kan bläddra bland, söka efter och dra fjärresurserna till en komponent. Om du vill autentisera med DAM-fjärrdistributionen bör du ha DAM-användarens autentiseringsuppgifter som du fått av administratören till hands.

Författare kan använda resurserna som finns på både den lokala DAM-instansen och fjärrinstansen av DAM på samma webbsida. Använd Content Finder för att växla mellan att söka i det lokala DAM-systemet eller söka i det fjärranslutna DAM-systemet.

Endast taggar för fjärresurser som har en exakt motsvarande tagg, med samma taxonomiska hierarki, hämtas på den lokala Sites-instansen. Alla andra taggar tas bort. Författare kan söka efter fjärresurser med hjälp av alla taggar som finns i den fjärranslutna AEM-distributionen eftersom AEM erbjuder fulltextsökning.

### Genomgång av användningen {#walk-through-of-usage}

Använd konfigurationen ovan när du vill prova redigeringsfunktionen och se hur den fungerar. Använd de dokument eller bilder du vill ha på den fjärranslutna DAM-distributionen.

1. Navigate to the Assets UI on the remote deployment by accessing **[!UICONTROL Assets]** > **[!UICONTROL Files]** from AEM workspace. Du kan även få åtkomst till `https://[assets_servername_ams]:[port]/assets.html/content/dam` i en webbläsare. Ladda upp de resurser du vill ha.
1. On the Sites instance, in the profile activator in the upper-right corner, click **[!UICONTROL Impersonate as]**. Provide `ksaner` as user name, select the option provided, and click **[!UICONTROL OK]**.
1. Öppna en webbsida för Vi.Butiker på **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Redigera sidan. Du kan även öppna `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` i en webbläsare när du vill redigera en sida.

   Klicka på **[!UICONTROL Växla sidopanel]** i det övre vänstra hörnet på sidan.

1. Öppna fliken Resurser och klicka på **[!UICONTROL Logga in på Anslutna resurser]**.
1. Ange inloggningsuppgifterna, `ksaner` som användarnamn och `password` som lösenord. Den här användaren har redigeringsbehörighet för båda AEM-distributionerna.
1. Sök efter resursen som du har lagt till i DAM. Fjärresurserna visas i den vänstra panelen. Filtrera efter bilder eller dokument och filtrera efter olika typer av dokument som stöds. Dra bilderna till en `Image`-komponent och dokument till en `Download`-komponent.

   De hämtade resurserna är skrivskyddade i den lokala AEM Sites-distributionen. Du kan fortfarande använda alternativen som finns i AEM Sites-komponenterna för att redigera den hämtade resursen. Redigering med komponenter är icke-destruktiv.

   ![Alternativ för att filtrera dokumenttyper och bilder vid sökning efter resurser på DAM-fjärrdistribution](assets/filetypes_filter_connected_assets.png)

   *Bild: Alternativ för att filtrera dokumenttyper och bilder vid sökning efter resurser på DAM-fjärrdistribution*

1. En Sites-författare meddelas om en resurs hämtas asynkront och om en hämtningsåtgärd misslyckas. Under eller efter redigeringen kan författare se detaljerad information om hämtningsåtgärder och fel i användargränssnittet för [asynkrona jobb](/help/assets/asynchronous-jobs.md).

   ![Meddelande om asynkron hämtning av resurser som sker i bakgrunden.](assets/assets_async_transfer_fails.png)

   *Bild: Meddelande om asynkron hämtning av resurser som sker i bakgrunden.*

1. När du publicerar en sida visar AEM en fullständig lista över resurser som används på sidan. Kontrollera att fjärresurserna har hämtats vid publiceringen. Se [användargränssnittet för asynkrona jobb](/help/assets/asynchronous-jobs.md) om du vill kontrollera status för varje hämtad resurs.

   >[!NOTE]
   >
   >Sidan publiceras även om en eller flera fjärresurser inte hämtats. Komponenten som använder fjärresursen publiceras tom. AEM-meddelandeområdet visar meddelanden om fel som visas på sidan för asynkrona jobb.

>[!CAUTION]
>
>När de hämtade fjärresurserna har använts på en webbsida är de sökbara och användbara för alla som har behörighet att komma åt den lokala mappen där de hämtade resurserna lagras (`connectedassets` i ovanstående genomgång). The assets are also searchable and visible in the local repository via [!UICONTROL Content Finder].

De hämtade resurserna kan användas som andra lokala resurser, förutom att associerade metadata inte kan redigeras.

## Begränsningar {#limitations}

**Behörigheter och hantering av resurser**

* Lokala resurser synkroniseras inte med de ursprungliga resurserna i fjärrdistributionen. Ändringar, borttagningar eller återkallande av behörigheter i DAM-distributionen sprids inte längre ned i kedjan.
* Lokala resurser är skrivskyddade kopior. Med AEM-komponenterna är redigeringen av resurser icke-destruktiv. Inga andra redigeringar tillåts.
* Lokalt hämtade resurser är endast tillgängliga för redigeringsändamål. Det går inte att använda arbetsflöden för resursuppdatering och metadata kan inte redigeras.
* Endast bilder och dokumentformaten i listan stöds. Dynamic Media-resurser, innehållsfragment och Experience-fragment stöds inte.
* Metadatascheman hämtas inte.
* Alla Sites-författare har läsbehörighet för de hämtade kopiorna, även om de inte har åtkomst till den fjärranslutna DAM-distributionen.
* Det finns inte API-stöd för att anpassa integreringen.
* Funktionen stöder smidig sökning och användning av fjärresurser. Om du vill göra många fjärresurser tillgängliga i den lokala distributionen på en gång bör du överväga att migrera resurserna.
* It is not possible to use a remote asset as a thumbnail for a web page in the [!UICONTROL Thumbnail] tab in [!UICONTROL Page Properties] by clicking [!UICONTROL Select Image].

**Konfigurera och licensiera**

* AEM Assets-distribution på AMS stöds.
* AEM Sites kan ansluta till ett enda AEM Assets-datalager åt gången.
* En licens för AEM Assets som fungerar som fjärrdatalager.
* En eller flera licenser för AEM Sites som fungerar som lokal redigeringsdistribution.

**Användning**

* De enda funktioner som stöds är sökning efter fjärresurser och att dra fjärresurserna till den lokala sidan för att skapa innehåll.
* Tidsgränsen för hämtning är 5 sekunder. Författare kan ha problem med att hämta resurser, till exempel om det råder nätverksproblem. Författare kan försöka igen genom att dra fjärrresursen från [!UICONTROL Innehållssökning] till [!UICONTROL sidredigeraren].
* Enkla redigeringar som är icke-destruktiva och redigering som stöds via AEM `Image`-komponenten kan tillämpas på hämtade resurser. Resurserna är skrivskyddade.

## Felsöka problem {#troubleshoot}

Följ dessa steg för att felsöka vanliga fel:

* Om du inte kan söka efter fjärresurser via Content Finder kontrollerar du att de roller och behörigheter som krävs finns på plats.
* En resurs som hämtats från en DAM-fjärrdistribution kanske inte publiceras på en webbsida av följande skäl: Den finns inte i fjärrdistributionen, lämplig behörighet saknas för att hämta den eller nätverksfel. Kontrollera att resursen inte tagits bort från DAM-fjärrdistributionen eller att behörigheterna inte har ändrats, kontrollera att lämpliga villkor är uppfyllda, försök lägga till resursen på sidan igen och publicera den på nytt. Kontrollera i [listan över asynkrona jobb](/help/assets/asynchronous-jobs.md) om fel uppstod vid hämtning av resurser.
