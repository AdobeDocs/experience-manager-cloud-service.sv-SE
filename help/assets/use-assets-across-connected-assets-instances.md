---
title: Använd anslutna resurser för att dela DAM-resurser i redigeringsarbetsflödet för Adobe Experience Manager Sites
description: Använd resurser som är tillgängliga på en fjärrdistribution av Adobe Experience Manager Assets när du skapar webbsidor på en annan Experience Manager-webbplatsdistribution.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 45371da5617a0d87105dbf2f574de15bf0698d98

---


# Använd anslutna resurser för att dela DAM-resurser på AEM-platser {#use-connected-assets-to-share-dam-assets-in-aem-sites}

I stora företag kan den infrastruktur som krävs för att skapa webbplatser distribueras. Ibland kan funktioner för att skapa webbplatser och digitala resurser som används för att skapa dessa webbplatser finnas i olika distributioner. Det finns vissa skäl till att det krävs en geografisk fördelning av driftsättningarna för att kunna arbeta tillsammans. Förvärv som leder till en heterogen infrastruktur som moderbolaget vill konsolidera. tillväxt som leder till en sådan skala att en dedikerad instans krävs för tillgångshantering.

AEM Sites erbjuder funktioner för att skapa webbsidor och AEM Assets är det DAM-system (Digital Asset Management) som tillhandahåller de resurser som krävs för webbplatser. AEM stöder nu ovanstående användningsexempel genom att integrera AEM Sites och AEM Assets.

## Översikt över anslutna resurser {#overview-of-connected-assets}

När du redigerar sidor i sidredigeraren kan författarna enkelt söka efter, bläddra bland och bädda in resurser från en annan AEM Resurser-distribution. Att göra en AEM-administratör gör en engångsintegrering av en lokal driftsättning av AEM Sites med en annan (fjärransluten) driftsättning av AEM Assets.

För webbplatsförfattarna är fjärrresurserna tillgängliga som skrivskyddade lokala resurser. Funktionen stöder smidig sökning och användning av ett fåtal fjärrresurser i taget. Om du vill göra många fjärrresurser tillgängliga för lokal distribution på en gång bör du överväga att migrera resurserna samtidigt. Se Handbok för [resursmigrering](/help/assets/assets-migration-guide.md).

### Förutsättningar och driftsättningar som stöds {#prerequisites}

Innan du använder eller konfigurerar den här funktionen bör du kontrollera följande:

* Användarna ingår i lämpliga användargrupper för varje distribution.
* Ett av de kriterier som stöds för Adobe Experience Manager-distributionstyper är uppfyllt.

   |  | AEM Sites as a Cloud Service | AEM 6.5 Sites på AMS | AEM 6.5 Sites på plats |
   |---|---|---|---|
   | **AEM Resurser som en molntjänst** | Stöds | Stöds | Stöds |
   | **AEM 6.5 Assets on AMS** | Stöds inte | Stöds | Stöds |
   | **AEM 6.5 Assets på plats** | Stöds inte | Stöds inte | Stöds inte |

### Filformat som stöds {#mimetypes}

Författare kan söka efter bilder och följande typer av dokument i Content Finder och använda de sökbara resurserna i Page Editor. Dokument kan läggas till i `Download` komponenten och bilder kan läggas till i `Image` komponenten. Författare kan också lägga till fjärrresurserna i en anpassad AEM-komponent som utökar standard- `Download` eller `Image` komponenterna.

* Microsoft Word (DOC och DOCX)
* Microsoft Excel (XLS och XLSX)
* Microsoft PowerPoint (PPT och PPTX)
* Adobe PDF (PDF)
* OpenDocument-text (ODT)
* RTF (Rich Text Format)
* Oformaterad text (TXT)
* Webbsidor (HTML)

### Användare och grupper {#users-and-groups-involved}

De olika roller som används för att konfigurera och använda funktionen och deras motsvarande användargrupper beskrivs nedan. Lokalt omfång används för de fall där en webbsida skapas av en författare. Fjärrscope används för DAM-distributionen som är värd för de nödvändiga resurserna. Webbplatsförfattaren hämtar dessa fjärrresurser.

| Roll | Omfång | Användargrupp | Användarnamn i genomgång | Krav |
|----------------------------------|--------|------------------------------------------------------------------------------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AEM Sites Administrator | Lokal | AEM-administratör | `admin` | Konfigurera AEM, konfigurera integrering med distributionen av fjärrresurser. |
| DAM-användare | Lokal | Författare | `ksaner` | Används för att visa och duplicera de hämtade resurserna `/content/DAM/connectedassets/`. |
| Författare av AEM Sites | Lokal | Författare (med läsåtkomst på det fjärranslutna DAM-systemet och författaråtkomst på lokala platser) | `ksaner` | Slutanvändare är webbplatsförfattare som använder den här integreringen för att förbättra innehållets hastighet. Författarna söker efter och bläddrar bland resurser i fjärr-DAM med hjälp av Content Finder och de bilder som behövs på lokala webbsidor. Autentiseringsuppgifterna för `ksaner` DAM-användaren används. |
| Administratör för AEM Resurser | Fjärr | AEM Administrator | `admin` på fjärr-AEM | Konfigurera Cross-Origin Resource Sharing (CORS). |
| DAM-användare | Fjärr | Författare | `ksaner` på fjärr-AEM | Författarroll för fjärr-AEM-distributionen. Sök efter och bläddra bland resurser i anslutna resurser med hjälp av Content Finder. |
| DAM-distributör (teknisk användare) | Fjärr | paketbyggare och författare till webbplatser | `ksaner` på fjärr-AEM | Den här användaren som är närvarande på fjärrdistributionen används av den lokala AEM-servern (inte författarrollen för webbplatsen) för att hämta fjärrresurserna, för författaren till webbplatserna. Den här rollen är inte densamma som ovan två `ksaner` roller och tillhör en annan användargrupp. |

## Konfigurera en anslutning mellan platser och Assets-distributioner {#configure-a-connection-between-sites-and-assets-deployments}

En AEM-administratör kan skapa den här integreringen. När de har skapats skapas de behörigheter som krävs för att använda dem via användargrupper som definieras i Sites-distributionen och i DAM-distributionen.

Följ de här stegen för att konfigurera anslutningsmöjligheter för anslutna resurser och lokala platser.

1. Få åtkomst till en befintlig AEM Sites-distribution eller skapa en distribution med följande kommando:

   1. Kör följande kommando på en terminal i JAR-filens mapp för att skapa varje AEM-server.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. Efter några minuter startas AEM-servern. Se den här AEM Sites-distributionen som den lokala datorn för webbsidesredigering, till exempel `https://[local_sites]:4502`.

1. Kontrollera att användare och roller med lokal omfattning finns i AEM Sites-distributionen och i AEM Assets-distributionen på AMS. Skapa en teknisk användare i Assets-distributionen och lägg till i användargruppen som omnämns i [användare och grupper som deltar](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Gå till den lokala AEM Sites-distributionen på `https://[local_sites]:4502`. Klicka på **[!UICONTROL Verktyg]** > **[!UICONTROL Resurser]** > Konfiguration **[!UICONTROL av]** anslutna resurser och ange följande värden:

   1. AEM Assets-platsen är `https://[assets_servername_ams]:[port]`.
   1. Autentiseringsuppgifter för en DAM-distributör (teknisk användare).
   1. I fältet **[!UICONTROL Monteringspunkt]** anger du den lokala AEM-sökvägen där AEM hämtar resurserna. Till exempel, `remoteassets` mapp.

   1. Justera värdena för det **[!UICONTROL ursprungliga tröskelvärdet för optimering av binär överföring]** beroende på nätverket. En resursåtergivning med en storlek som är större än detta tröskelvärde överförs asynkront.
   1. Välj **[!UICONTROL Datastore Shared with Connected Assets]** om du använder ett datalager för att lagra dina resurser och Datastore är den gemensamma lagringen mellan båda AEM-distributionerna. I det här fallet spelar tröskelvärdet ingen roll eftersom faktiska tillgångsbinärfiler finns i datalagret och inte överförs.
   ![En typisk konfiguration för anslutna resurser](assets/connected-assets-typical-config.png)

   *Bild:En typisk konfiguration för anslutna resurser*

1. Inaktivera arbetsflödets startprogram eftersom resurserna redan har bearbetats och återgivningarna hämtas. Justera startkonfigurationerna för den lokala distributionen (AEM Sites) för att exkludera den `connectedassets` mapp där fjärrresurserna hämtas.

   1. I AEM Sites-distributionen klickar du på **[!UICONTROL Verktyg]** > **[!UICONTROL Arbetsflöde]** > **[!UICONTROL Startprogram]**.

   1. Sök efter startare med arbetsflöden som **[!UICONTROL DAM Update Asset]** och **[!UICONTROL DAM Metadata Writeback]**.

   1. Välj startprogrammet för arbetsflödet och klicka på **[!UICONTROL Egenskaper]** i åtgärdsfältet.

   1. I egenskapsguiden ändrar du **[!UICONTROL sökvägsfälten]** som följande mappningar för att uppdatera deras reguljära uttryck så att de utesluter monteringspunktsanslutna **[!UICONTROL resurser]**.
   | Före | Efter |
   |---|---|
   | /content/dam(/(?!/subassets).)*/)renderingar/original | /content/dam(/(?!/subassets)(?!connectedassets).)*/)renderingar/original |
   | /content/dam(/.*/)renderingar/original | /content/dam(/(?!connectedassets).)*/)renderingar/original |
   | /content/dam(/.*)/jcr:content/metadata | /content/dam(/(?!connectedassets).)*/)jcr:content/metadata |

   >[!NOTE]
   >
   >Alla återgivningar som är tillgängliga på den fjärranslutna AEM-distributionen hämtas när författare hämtar en resurs. Om du vill skapa fler återgivningar av en hämtad resurs hoppar du över det här konfigurationssteget. DAM Update Asset-arbetsflödet aktiveras och skapar fler återgivningar. Dessa återgivningar är bara tillgängliga i den lokala distributionen av platser och inte i den fjärrdistribuerade DAM-distributionen.

1. Lägg till AEM Sites-instansen som ett av **[!UICONTROL Tillåtna original]** i fjärr-AEM Assets&#39; CORS-konfiguration.

   1. Logga in med administratörsautentiseringsuppgifterna. Sök efter korsursprung. Öppna **[!UICONTROL Verktyg]** > **[!UICONTROL Åtgärder]** > **[!UICONTROL Webbkonsol]**.

   1. Om du vill skapa en CORS-konfiguration för en AEM Sites-instans klickar du på ![ikonen aem_assets_add_icon](assets/do-not-localize/aem_assets_add_icon.png) bredvid **[!UICONTROL Adobe Granite-resursdelningspolicy]** för korsursprung.

   1. I fältet **[!UICONTROL Tillåtna original]** anger du URL:en för de lokala platserna, det vill säga `https://[local_sites]:[port]`. Spara konfigurationen.

## Använd fjärrresurser {#use-remote-assets}

Webbplatsens författare använder Content Finder för att ansluta till DAM-instansen. Författarna kan bläddra bland, söka efter och dra fjärrresurserna i en komponent. Om du vill autentisera till fjärr-DAM-användarens autentiseringsuppgifter, som du fått av administratören, ska du behålla dem.

Upphovsmannen kan använda resurserna som finns på både den lokala DAM- och fjärrinstansen av DAM på en enda webbsida. Använd Innehållssökning för att växla mellan att söka i det lokala DAM-systemet eller söka i det fjärranslutna DAM-systemet.

Endast taggar för fjärrresurser som har en exakt motsvarande tagg, med samma taxonomi-hierarki, hämtas på den lokala Sites-instansen. Alla andra taggar tas bort. Författare kan söka efter fjärrresurser med hjälp av alla taggar som finns i den fjärranslutna AEM-distributionen, eftersom AEM erbjuder fulltextsökning.

### Genomgång av användningen {#walk-through-of-usage}

Använd ovanstående inställning för att testa hur redigeringsfunktionen fungerar. Använd de dokument eller bilder du vill ha på den fjärranslutna DAM-distributionen.

1. Navigera till resursgränssnittet på fjärrdistributionen genom att gå till **[!UICONTROL Resurser]** > **[!UICONTROL Filer]** från AEM-arbetsytan. Du kan även få åtkomst `https://[assets_servername_ams]:[port]/assets.html/content/dam` i en webbläsare. Ladda upp de mediefiler du vill ha.
1. I platsinstansen klickar du på **[!UICONTROL Personifiera som]** i profilaktiveraren i det övre högra hörnet. Ange `ksaner` som användarnamn, markera det angivna alternativet och klicka på **[!UICONTROL OK]**.
1. Öppna en webbsida för Vi.Butiker på **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**. Redigera sidan. Du kan även använda en webbläsare `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` för att redigera en sida.

   Klicka på **[!UICONTROL Växla sidopanel]** i det övre vänstra hörnet på sidan.

1. Öppna fliken Resurser och klicka på **[!UICONTROL Logga in på Anslutna resurser]**.
1. Ange inloggningsuppgifterna `ksaner` som användarnamn och `password` lösenord. Den här användaren har redigeringsbehörighet för båda AEM-distributionerna.
1. Sök efter resursen som du har lagt till i DAM. Fjärrresurserna visas i den vänstra panelen. Filtrera efter bilder eller dokument och filtrera efter olika typer av dokument som stöds. Dra bilderna på en `Image` komponent och i dokument på en `Download` komponent.

   De hämtade resurserna är skrivskyddade i den lokala AEM Sites-distributionen. Du kan fortfarande använda alternativen som finns i AEM Sites-komponenterna för att redigera den hämtade resursen. Komponenternas redigering är icke-förstörande.

   ![Alternativ för att filtrera dokumenttyper och bilder vid sökning av resurser på fjärr-DAM](assets/filetypes_filter_connected_assets.png)

   *Bild: Alternativ för att filtrera dokumenttyper och bilder vid sökning av resurser på fjärr-DAM*

1. En webbplatsförfattare meddelas om en resurs hämtas asynkront och om någon hämtningsåtgärd misslyckas. Under utvecklingen eller även efter redigeringen kan författarna se detaljerad information om hämtningsuppgifter och fel i användargränssnittet för [asynkrona jobb](/help/assets/asynchronous-jobs.md) .

   ![Meddelande om asynkron hämtning av resurser som sker i bakgrunden.](assets/assets_async_transfer_fails.png)

   *Bild: Meddelande om asynkron hämtning av resurser som sker i bakgrunden.*

1. När du publicerar en sida visar AEM en fullständig lista över resurser som används på sidan. Kontrollera att fjärrresurserna har hämtats vid publiceringen. Om du vill kontrollera statusen för varje hämtad resurs läser du i [användargränssnittet för asynkrona jobb](/help/assets/asynchronous-jobs.md) .

   >[!NOTE]
   >
   >Sidan publiceras även om en eller flera fjärrresurser inte hämtas. Komponenten som använder fjärrresursen publiceras tom. AEM-meddelandeområdet visar meddelanden om fel som visas på sidan för asynkrona jobb.

>[!CAUTION]
>
>När de hämtade fjärrresurserna har använts på en webbsida är de sökbara och användbara för alla som har behörighet att komma åt den lokala mappen där de hämtade resurserna lagras (`connectedassets` i ovanstående genomgång). Resurserna är också sökbara och synliga i den lokala databasen via [!UICONTROL Content Finder].

De hämtade resurserna kan användas som andra lokala resurser, förutom att associerade metadata inte kan redigeras.

## Begränsningar {#limitations}

**Behörigheter och hantering av resurser**

* Lokala resurser synkroniseras inte med de ursprungliga resurserna på fjärrdistributionen. Ändringar, borttagningar eller återkallande av behörigheter i DAM-distributionen sprids inte längre längre fram i kedjan.
* Lokala resurser är skrivskyddade kopior. AEM-komponenter utför icke-förstörande redigering av resurser. Inga andra redigeringar tillåts.
* Lokalt hämtade resurser är endast tillgängliga för redigeringsändamål. Det går inte att använda arbetsflöden för resursuppdatering och metadata kan inte redigeras.
* Endast bilder och dokumentformaten i listan stöds. Dynamiska medieresurser, innehållsfragment och upplevelsefragment stöds inte.
* Metadata-scheman hämtas inte.
* Alla webbplatsförfattare har läsbehörighet för de hämtade kopiorna, även om de inte har åtkomst till den fjärranslutna DAM-distributionen.
* Inget API-stöd för att anpassa integreringen.
* Funktionen stöder smidig sökning och användning av fjärrresurser. Om du vill göra många fjärrresurser tillgängliga på lokal distribution på en gång bör du överväga att migrera resurserna. Se Handbok för [resursmigrering](assets-migration-guide.md).
* Det går inte att använda en fjärrresurs som miniatyrbild för en webbsida på fliken [!UICONTROL Miniatyrbilder] i [!UICONTROL Sidegenskaper] genom att klicka på [!UICONTROL Välj bild].

**Konfigurera och licensiera**

* AEM Assets-distribution på AMS stöds.
* AEM Sites kan ansluta till en enda AEM Resurser-databas åt gången.
* En licens för AEM Assets som fungerar som fjärrdatabas.
* En eller flera licenser av AEM Sites fungerar som lokal utvecklingsdistribution.

**Användning**

* Det är bara funktioner som stöds som att söka efter fjärrresurser och dra fjärrresurserna på den lokala sidan för att skapa innehåll.
* Hämtningen tar timeout efter 5 sekunder. Författare kan ha problem med att hämta resurser, till exempel om det är nätverksproblem. Författare kan försöka igen genom att dra fjärrresursen från [!UICONTROL Innehållssökning] till [!UICONTROL sidredigeraren].
* Enkla redigeringar som inte är förstörande och redigeringen som stöds via AEM- `Image` komponenten kan göras på hämtade resurser. Resurser är skrivskyddade.

## Felsöka problem {#troubleshoot}

Följ de här stegen för att felsöka vanliga felscenarier:

* Om du inte kan söka efter fjärrresurser från Innehållssökning kontrollerar du att de roller och behörigheter som krävs finns på plats.
* En resurs som hämtats från en fjärrdam kanske inte publiceras på en webbsida av följande skäl: Den finns inte på fjärrbasis. Avsaknad av lämpliga tillstånd för att hämta den. nätverksfel. Se till att resursen inte tas bort från fjärr-DAM eller att behörigheterna inte ändras. se till att lämpliga förutsättningar är uppfyllda, försök lägga till resursen på sidan igen och publicera den på nytt. Kontrollera i [listan över asynkrona jobb](/help/assets/asynchronous-jobs.md) om det finns fel vid hämtning av resurser.
