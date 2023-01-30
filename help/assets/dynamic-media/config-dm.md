---
title: Konfigurera Dynamic Media Cloud Service
description: Lär dig hur du konfigurerar Dynamic Media i Adobe Experience Manager as a Cloud Service.
contentOwner: Rick Brough
role: Admin,User
exl-id: 8e07bc85-ef26-4df4-8e64-3c69eae91e11
source-git-commit: 35caac30887f17077d82f3370f1948e33d7f1530
workflow-type: tm+mt
source-wordcount: '3559'
ht-degree: 2%

---

# Konfigurera Dynamic Media Cloud Service {#configuring-dynamic-media}

Om du använder Adobe Experience Manager för olika miljöer, som utveckling, staging och liveproduktion, konfigurerar du Dynamic Media-Cloud Services för var och en av dessa miljöer.

Se även [Konfigurera ett Dynamic Media-företagskonto](/help/assets/dynamic-media/dm-alias-account.md)

## Arkitektur för Dynamic Media {#architecture-diagram-of-dynamic-media}

I följande arkitekturdiagram beskrivs hur Dynamic Media fungerar.

Med den nya arkitekturen ansvarar Experience Manager för de viktigaste källresurserna och synkroniserar med Dynamic Media när det gäller bearbetning och publicering av mediefiler:

1. När den primära källresursen överförs till Adobe Experience Manager as a Cloud Service replikeras den till Dynamic Media. Då hanterar Dynamic Media all bearbetning och generering av resurser, till exempel videokodning och dynamiska varianter av en bild.
1. När återgivningarna har genererats kan Experience Manager as a Cloud Service på ett säkert sätt få åtkomst till och förhandsgranska Dynamic Media fjärråtergivningar (inga binärfiler skickas tillbaka till den as a Cloud Service instansen av Experience Manager).
1. När innehållet är klart att publiceras och godkännas utlöses Dynamic Media-tjänsten av att skicka innehåll till leveransservrar och cachelagra innehåll på CDN (Content Delivery Network).

![chlimage_1-550](assets/chlimage_1-550.png)

>[!NOTE]
>
>Följande funktionslista kräver att du använder det färdiga CDN som medföljer Adobe Experience Manager - Dynamic Media. Andra anpassade CDN stöds inte med dessa funktioner.
>
>* [Smart bildbehandling](/help/assets/dynamic-media/imaging-faq.md)
>* [Cacheogiltigförklaring](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
>* [Hotlänksskydd](/help/assets/dynamic-media/hotlink-protection.md)
>* [HTTP/2-leverans av innehåll](/help/assets/dynamic-media/http2faq.md)
>* URL-omdirigering på CDN-nivå
>* Akamai ChinaCDN (för optimal leverans i Kina)


<!-- OBSOLETE CONTENT

## (Optional) Migrating Dynamic Media presets and configurations from 6.3 to 6.5 Zero Downtime {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

If you are upgrading Experience Manager as a Cloud Service Dynamic Media from 6.3 to 6.4 or 6.5 (which now includes the ability for zero downtime deployments), you are required to run the following curl command to migrate all your presets and configurations from `/etc` to `/conf` in CRXDE Lite.

>[!NOTE]
>
>If you run your Experience Manager as a Cloud Service instance in compatibility mode--that is, you have the compatibility packaged installed--you do not need to run these commands.

For all upgrades, either with or without the compatibility package, you can copy the default, out-of-the-box viewer presets that originally came with Dynamic Media by running the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

To migrate any custom viewer presets and configurations that you have created from `/etc` to `/conf`, run the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

-->

## Skapa en Dynamic Media-konfiguration i Cloud Services {#configuring-dynamic-media-cloud-services}

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. I Experience Manager as a Cloud Service väljer du den as a Cloud Service logotypen för Experience Manager för att komma åt den globala navigeringskonsolen.
1. Till vänster om konsolen väljer du verktygsikonen och går till **[!UICONTROL Cloud Services > Dynamic Media Configuration]**.
1. På sidan Dynamic Media Configuration Browser väljer du **[!UICONTROL global]** (markera inte mappikonen till vänster om **[!UICONTROL global]**). Välj sedan **[!UICONTROL Create]**.
1. På **[!UICONTROL Create Dynamic Media Configuration]** Ange titel, e-postadress för Dynamic Media-konto och lösenord för företagsadministratören för Dynamic Media-kontot och välj sedan region. Den här informationen tillhandahålls av Adobe i e-postmeddelandet om etablering. Kontakta Adobe kundsupport om du inte fått det här mejlet.
1. Välj **[!UICONTROL Connect to Dynamic Media]**.
1. I **[!UICONTROL Change Password]** i **[!UICONTROL New Password]** anger du ett nytt lösenord som består av 8-25 tecken. Lösenordet måste innehålla minst ett av följande:

   * Versaler
   * Gemener
   * Siffra
   * Specialtecken: `# $ & . - _ : { }`

   The **[!UICONTROL Current Password]** fältet är avsiktligt ifyllt och dolt för interaktion.

   Om det behövs kan du kontrollera stavningen av ett lösenord som du har skrivit eller skrivit in igen genom att markera lösenordsikonen för att visa lösenordet. Klicka på ikonen igen om du vill dölja lösenordet.

1. I **[!UICONTROL Repeat Password]** anger du det nya lösenordet igen och väljer **[!UICONTROL Done]**.

   Det nya lösenordet sparas när du väljer **[!UICONTROL Save]** i det övre högra hörnet av **[!UICONTROL Create Dynamic Media Configuration]** sida.

   Om du valde **[!UICONTROL Cancel]** i **[!UICONTROL Change Password]** måste du fortfarande ange ett nytt lösenord när du sparar den nya Dynamic Media-konfigurationen.

   Se även [Ändra lösenordet till Dynamic Media](#change-dm-password).

1. När anslutningen lyckas kan du ange följande:

   | Egenskap | Beskrivning |
   |---|---|
   | Företag | Namnet på Dynamic Media-kontot.<br>**Viktigt**: Endast en Dynamic Media-konfiguration i Cloud Services stöds i en instans av Experience Manager. lägger inte till mer än en konfiguration. Flera Dynamic Media-konfigurationer i en Experience Manager-instans är _not_ som stöds eller rekommenderas av Adobe.<!-- CQDOC-19579 and CQDOC-19612 --><br>Se även [Konfigurera ett Dynamic Media-företagskonto](/help/assets/dynamic-media/dm-alias-account.md). |
   | Företagets rotmappsökväg | Företagets rotmappsökväg. |
   | Publicera resurser | Du kan välja mellan följande tre alternativ:<br>**[!UICONTROL Immediately]**- När resurser överförs importeras resurserna och URL/Embed anges omedelbart. Ingen användaråtgärd krävs för att publicera resurser.<br>**[!UICONTROL On Activation]** - Du måste publicera resursen explicit innan en URL/Embed-länk anges.<br>**[!UICONTROL Selective Publish]**- Resurserna publiceras automatiskt för säker förhandsgranskning. De kan också uttryckligen publiceras på Experience Manager as a Cloud Service utan att publiceras till DMS7 för att levereras offentligt. I framtiden avser detta alternativ att publicera resurser på Experience Manager as a Cloud Service och publicera resurser på Dynamic Media, som inte utesluter varandra. Det innebär att du kan publicera resurser på DMS7 så att du kan använda funktioner som Smart Crop eller dynamiska återgivningar. Eller så kan du publicera resurser exklusivt i Experience Manager as a Cloud Service för förhandsgranskning. samma resurser inte publiceras i DMS7 för att distribueras offentligt. |
   | Secure Preview Server | Här kan du ange URL-sökvägen till förhandsgranskningsservern för säkra återgivningar. Det vill säga, när återgivningarna har skapats kan Experience Manager as a Cloud Service på ett säkert sätt komma åt och förhandsgranska Dynamic Media fjärråtergivningar (inga binärfiler skickas tillbaka till den as a Cloud Service instansen i Experience Manager).<br>Om du inte har en särskild lösning för att använda ditt företags server eller en speciell server rekommenderar Adobe att du låter den här inställningen vara angiven. |
   | Synkronisera allt innehåll | Markerad som standard. Avmarkera det här alternativet om du vill inkludera eller exkludera resurser från synkroniseringen till Dynamic Media. Om du avmarkerar det här alternativet kan du välja mellan följande två synkroniseringslägen för Dynamic Media:<br>**[!UICONTROL Dynamic Media sync mode]**<br>**[!UICONTROL Enable by default]**- Konfigurationen används som standard på alla mappar såvida du inte markerar en mapp som är exkluderad.<!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL Disabled by default]** - Konfigurationen tillämpas inte på någon mapp förrän du uttryckligen markerar en markerad mapp för synkronisering till Dynamic Media.<br>Om du vill markera en markerad mapp för synkronisering till Dynamic Media väljer du en resursmapp och väljer sedan i verktygsfältet **[!UICONTROL Properties]**. På **[!UICONTROL Details]** -fliken, i **[!UICONTROL Dynamic Media sync mode]** i den nedrullningsbara listan väljer du mellan följande tre alternativ. När du är klar väljer du **[!UICONTROL Save]**. _Kom ihåg: dessa tre alternativ är inte tillgängliga om du har valt **Synkronisera allt innehåll**tidigare._ Se även [Arbeta med selektiv publicering på mappnivå i Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).<br>**[!UICONTROL Inherited]**- Det finns inget explicit synkroniseringsvärde i mappen. I stället ärver mappen synkroniseringsvärdet från en av de överordnade mapparna eller standardläget i molnkonfigurationen. Detaljerad status för ärvda program via ett verktygstips.<br>**[!UICONTROL Enable for subfolders]** - Inkludera allt i det här underträdet för synkronisering med Dynamic Media. De mappspecifika inställningarna åsidosätter standardläget i molnkonfigurationen.<br>**[!UICONTROL Disabled for subfolders]**- Uteslut allt i det här underträdet från synkronisering till Dynamic Media. |

   >[!NOTE]
   >
   >Det finns inget stöd för versionshantering i Dynamic Media. Dessutom gäller fördröjd aktivering endast om **[!UICONTROL Publish Assets]** på sidan Redigera Dynamic Media-konfiguration är inställd på **[!UICONTROL Upon Activation]**. Och sedan bara tills första gången tillgången aktiveras.
   >
   >
   >När en mediefil har aktiverats publiceras uppdateringar direkt till S7 Delivery.

   ![dynamicmediaconfiguration2updated](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. Välj **[!UICONTROL Save]**. Det nya lösenordet och den nya konfigurationen för Dynamic Media sparas. Om du valde **[!UICONTROL Cancel]** i stället görs ingen lösenordsuppdatering.
1. I **[!UICONTROL Configuring Dynamic Media]** väljer **[!UICONTROL OK]** för att starta konfigurationen.

   >[!IMPORTANT]
   >
   >När den nya Dynamic Media-konfigurationen är klar får du ett statusmeddelande i Inkorgen för Experience Manager as a Cloud Service.
   >
   >Det här inkorgsmeddelandet informerar dig om konfigurationen lyckades eller inte.
   > Se [Felsöka en ny Dynamic Media-konfiguration](#troubleshoot-dm-config) och [Din inkorg](/help/sites-cloud/authoring/getting-started/inbox.md) för mer information.

1. För att på ett säkert sätt förhandsgranska Dynamic Media-innehåll innan det publiceras använder Experience Manager as a Cloud Service tokenbaserad validering och Experience Manager Author förhandsgranskar därmed Dynamic Media-innehåll som standard. Du kan dock *tillåtelselista* fler IP-adresser för att ge användarna tillgång till säkert förhandsgranskningsmaterial. Information om hur du konfigurerar den här åtgärden på Experience Manager as a Cloud Service finns i [Konfigurera Dynamic Media Publish Setup för Image Server - fliken Säkerhet](/help/assets/dynamic-media/dm-publish-settings.md#security-tab). <!-- To securely preview Dynamic Media content before it gets published, you must "allowlist" the Experience Manager as a Cloud Service author instance to connect to Dynamic Media. To set up this action, do the following: -->

<!--
    * Open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. Your credentials and sign-in details were provided by Adobe at the time of provisioning. If you do not have this information, contact Adobe Customer Support.
    * On the navigation bar near the upper right corner of the page, go to **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**.
    * On the Image Server Publish page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * For the Client Address Filter, select **[!UICONTROL Add]**.
    * To enable (turn on) the address, select the check box, then enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * Select **[!UICONTROL Save]**. -->

Du är nu klar med den grundläggande konfigurationen; är du redo att använda Dynamic Media.

Om du vill anpassa konfigurationen ytterligare, t.ex. aktivera åtkomstkontrollistor (ACL), kan du utföra någon av uppgifterna under [Konfigurera avancerade inställningar i Dynamic Media](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

### Felsöka en ny Dynamic Media-konfiguration {#troubleshoot-dm-config}

När konfigurationen av en ny Dynamic Media-konfiguration är klar får du ett statusmeddelande i Inkorgen för Experience Manager as a Cloud Service. Det här meddelandet informerar dig om konfigurationen lyckades eller inte, vilket visas i följande bilder från Inkorgen.

![Experience Manager Inkorgen har slutförts](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![Inkorgsfel för Experience Manager](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

Se även [Din inkorg](/help/sites-cloud/authoring/getting-started/inbox.md).

**Så här felsöker du en ny Dynamic Media-konfiguration:**

1. I närheten av det övre högra hörnet på den as a Cloud Service Experience Manager-sidan väljer du klockikonen och sedan **[!UICONTROL View All]**.
1. På sidan Inkorg väljer du meddelandet om att åtgärden lyckades. Där kan du läsa en översikt över konfigurationens status och loggar.

   Om konfigurationen misslyckas väljer du felmeddelandet som liknar följande skärmbild.

   ![Dynamic Media-installationen misslyckades](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. På **[!UICONTROL DMSETUP]** Granska konfigurationsinformationen som beskriver felet. Tänk särskilt på eventuella felmeddelanden eller felkoder. Kontakta Adobe kundsupport med den här informationen.

   ![Dynamic Media - konfigurationssida](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### Ändra lösenordet till Dynamic Media {#change-dm-password}

Lösenordets giltighetstid i Dynamic Media är inställd på 100 år från det aktuella systemdatumet.

Lösenordet måste innehålla minst ett av följande:

* Versaler
* Gemener
* Siffra
* Specialtecken: `# $ & . - _ : { }`

Om det behövs kan du kontrollera stavningen av ett lösenord som du har skrivit eller skrivit in igen genom att markera lösenordsikonen för att visa lösenordet. Klicka på ikonen igen om du vill dölja lösenordet.

Det ändrade lösenordet sparas när du väljer **[!UICONTROL Save]** i det övre högra hörnet av **[!UICONTROL Edit Dynamic Media Configuration]** sida.

1. I Experience Manager as a Cloud Service väljer du den as a Cloud Service logotypen för Experience Manager för att komma åt den globala navigeringskonsolen.
1. Till vänster om konsolen väljer du verktygsikonen och går till **[!UICONTROL Cloud Services > Dynamic Media Configuration]**.
1. På sidan Dynamic Media Configuration Browser väljer du **[!UICONTROL global]**. Markera inte mappikonen till vänster om **[!UICONTROL global]**. Välj sedan **[!UICONTROL Edit]**.
1. På **[!UICONTROL Edit Dynamic Media Configuration]** sida, direkt nedanför **[!UICONTROL Password]** fält, markera **[!UICONTROL Change Password]**.
1. I **[!UICONTROL Change Password]** gör du följande:

   * I **[!UICONTROL New Password]** anger du ett nytt lösenord.

      The **[!UICONTROL Current Password]** fältet är avsiktligt ifyllt och dolt för interaktion.

   * I **[!UICONTROL Repeat Password]** anger du det nya lösenordet igen och väljer **[!UICONTROL Done]**.

1. I det övre högra hörnet av **[!UICONTROL Edit Dynamic Media Configuration]** sida, markera **[!UICONTROL Save]** väljer **[!UICONTROL OK]**.

## (Valfritt) Konfigurera avancerade inställningar i Dynamic Media{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Om du vill anpassa konfigurationen och konfigurationen av Dynamic Media ytterligare, eller optimera prestandan, kan du slutföra ett eller flera av följande _valfri_ uppgifter:

* [(Valfritt) Aktivera ACL-behörigheter i Dynamic Media](#optional-enable-acl)
* [(Valfritt) Konfigurera och konfigurera Dynamic Media-inställningar](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [(Valfritt) Justera prestanda för Dynamic Media](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

### (Valfritt) Aktivera behörigheter i åtkomstkontrollistan i Dynamic Media {#optional-enable-acl}

När du kör Dynamic Media på AEM vidarebefordras det för närvarande `/is/image` begäranden om att skydda förhandsvisningsbildservern utan att kontrollera ACL-behörigheter (Access Control List) på PlatformServerServlet. Du kan dock _enable_ ACL-behörigheter. Vidarebefordra de behöriga `/is/image` förfrågningar. Om en användare inte har behörighet att komma åt resursen visas felet&quot;403 - Ej tillåtet&quot;.

**Så här aktiverar du ACL-behörigheter i Dynamic Media:**

1. Navigera från Experience Manager till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. En ny flik i webbläsaren öppnas **[!UICONTROL Adobe Experience Manager Web Console Configuration]** sida.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. Bläddra till namnet på sidan _Adobe CQ Scene7 PlatformServer_.

1. Till höger om namnet väljer du pennikonen (**[!UICONTROL Edit the configuration values]**).

1. På **com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.name** markerar du kryssrutan för följande två inställningar:

   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.cache.enable.name` - När den här inställningen är aktiverad cachelagras behörighetsresultatet i två minuter (standard) för att spara.
   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.validate.userAccess.name` - När den här inställningen är aktiverad valideras användarens åtkomst medan användaren förhandsgranskar resurser via Dynamic Media Image Server.

   ![Aktivera inställningar för åtkomstkontrollistan i Dynamic Media - Scene7-läge](/help/assets/dynamic-media/assets/acl.png)

1. I det nedre högra hörnet av sidan väljer du **[!UICONTROL Save]**.

### (Valfritt) Konfigurera och konfigurera Dynamic Media-inställningar {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

Använd Dynamic Media Classic användargränssnitt för att ändra dina Dynamic Media-inställningar.

<!-- Some of the tasks above require that you open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. -->

Installations- och konfigureringsuppgifter omfattar följande:

* [Konfigurera Dynamic Media Publish Setup för Image Server](#publishing-setup-for-image-server)
* [Konfigurera allmänna inställningar för Dynamic Media](#configuring-application-general-settings)
* [Konfigurera färghantering](#configuring-color-management)
* [Redigera MIME-typer för format som stöds](#editing-mime-types-for-supported-formats)
* [Lägg till MIME-typer för format som inte stöds](#adding-mime-types-for-unsupported-formats)

<!-- OBSOLETE BUT LEAVE FOR POSSIBLE FUTURE* [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### Konfigurera Dynamic Media Publish Setup för Image Server {#publishing-setup-for-image-server}

På sidan Dynamic Media Publish Setup (Publiceringsinställningar) anges standardinställningar som avgör hur resurser levereras från Adobe Dynamic Media-servrar till webbplatser eller program.

Se [Konfigurera Dynamic Media Publish Setup för Image Server](/help/assets/dynamic-media/dm-publish-settings.md).

#### Konfigurera allmänna inställningar för Dynamic Media {#configuring-application-general-settings}

Konfigurera Dynamic Media **[!UICONTROL Publish Server Name]** URL och **[!UICONTROL Origin Server Name]** URL. Du kan också ange **[!UICONTROL Upload to Application]** inställningar och **[!UICONTROL Default Upload Options]** allt baserat på ditt specifika användningsfall.

Se [Konfigurera allmänna inställningar för Dynamic Media](/help/assets/dynamic-media/dm-general-settings.md).

#### Konfigurera färghantering {#configuring-color-management}

Med Dynamic Media färghantering kan du färgkorrigera resurser. Med färgkorrigering behåller inkapslade resurser sin färgmodell (RGB, CMYK, Grå) och inbäddad färgprofil. När du begär en dynamisk återgivning korrigeras bildfärgen till målfärgrymden med hjälp av CMYK-, RGB- eller grå utdata.

Se [Konfigurera bildförinställningar](/help/assets/dynamic-media/managing-image-presets.md).

Så här konfigurerar du standardfärgegenskaperna för aktivering av färgkorrigering när du begär bilder:

1. Öppna [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)loggar sedan in på ditt konto med de autentiseringsuppgifter som anges under etableringen.
1. Gå till **[!UICONTROL Setup > Application Setup]**.
1. Expandera området **[!UICONTROL Publish Setup]** och markera **[!UICONTROL Image Server]**. Ange **[!UICONTROL Publish Context]** som **[!UICONTROL Image Serving]** när du anger standardvärden för publiceringsinstanser.
1. Bläddra till den egenskap som du måste ändra, till exempel en egenskap i **[!UICONTROL Color Management Attributes]** område.
Du kan ange följande egenskaper för färgkorrigering:

   | Egenskap | Beskrivning |
   |---|---|
   | Standardfärgmodell för CMYK | Namn på CMYK-standardfärgprofilen. |
   | Standardfärgrymd för gråskala | Namnet på standardfärgprofilen för grått. |
   | RGB standardfärgmodell | Namn på standardfärgprofilen för RGB. |
   | Återgivningsmetod för färgkonvertering | Anger återgivningsmetod. Godtagbara värden är: **[!UICONTROL perceptual]**, **[!UICONTROL relative colometric]**, **[!UICONTROL saturation]**, **[!UICONTROL absolute colometric]**. Adobe rekommenderar **[!UICONTROL relative]** som standard. |

1. Välj **[!UICONTROL Save]**.

Du kan till exempel ställa in **[!UICONTROL RGB Default Color Space]** på *sRGB* och **[!UICONTROL CMYK Default Color Space]** på *WebCoated*.

Om du gör det gör du så här:

* Aktiverar färgkorrigering för RGB och CMYK-bilder.
* RGB-bilder som inte har någon färgprofil antas finnas i *sRGB* färgrymd.
* CMYK-bilder som inte har någon färgprofil antas finnas i *WebCoated* färgrymd.
* Dynamiska återgivningar som returnerar utdata från RGB, returnerar det i dialogrutan *sRGB* färgrymd.
* Dynamiska återgivningar som returnerar CMYK-utdata och returnerar dem i *WebCoated* färgrymd.

#### Redigera MIME-typer för format som stöds {#editing-mime-types-for-supported-formats}

Du kan definiera vilka resurstyper som bearbetas av Dynamic Media och anpassa avancerade parametrar för resurshantering. Du kan till exempel ange parametrar för tillgångsbearbetning för att göra följande:

* Konvertera en Adobe PDF till en eCatalog-resurs.
* Konvertera ett Adobe Photoshop-dokument (.PSD) till en bannermallsresurs för personalisering.
* Rastrera en Adobe Illustrator-fil (.AI) eller en Adobe Photoshop Encapsulated PostScript®-fil (.EPS).
* [Videoprofiler](/help/assets/dynamic-media/video-profiles.md) och [Bildprofiler](/help/assets/dynamic-media/image-profiles.md) kan användas för att definiera bearbetning av videoklipp och bilder.

Se [Överför resurser](/help/assets/add-assets.md).

**Så här redigerar du MIME-typer för de format som stöds:**

1. Logga in på Experience Manager as a Cloud Service som produktadministratör.
1. I Experience Manager as a Cloud Service väljer du den as a Cloud Service logotypen för Experience Manager för att komma åt den globala navigeringskonsolen och går sedan till **[!UICONTROL General > CRXDE Lite]**.

   Om du inte har tillgång till CRXDE Lite kan du läsa [Använda CRXDE Lite](/help/implementing/developing/tools/crxde.md).

1. Navigera till följande i den vänstra listen:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME-typer](assets/mimetypes.png)

1. Välj en MIME-typ i mappen mimeTypes.
1. Till höger på CRXDE Lite-sidan i den nedre delen:

   * Dubbeltryck på **[!UICONTROL enabled]** fält. Som standard är alla MIME-typer för resurser aktiverade (inställda på **[!UICONTROL true]**), vilket innebär att resurserna synkroniseras till Dynamic Media för bearbetning. Om du vill utesluta den här resursens MIME-typ från bearbetningen ändrar du den här inställningen till **[!UICONTROL false]**.

   * Dubbelknacka **[!UICONTROL jobParam]** för att öppna det tillhörande textfältet. Se [MIME-typer som stöds](/help/assets/file-format-support.md) för en lista över tillåtna värden för bearbetningsparametrar som du kan använda för en viss MIME-typ.

1. Gör något av följande:
   * Upprepa steg 3-4 för att redigera fler MIME-typer.
   * På menyraden på CRXDE Lite-sidan väljer du **[!UICONTROL Save All]**.

1. I det övre vänstra hörnet på sidan väljer du **[!UICONTROL CRXDE Lite]** för att återvända till Experience Manager as a Cloud Service.

#### Lägg till MIME-typer för format som inte stöds {#adding-mime-types-for-unsupported-formats}

Du kan lägga till anpassade MIME-typer för format som inte stöds i Experience Manager Assets. Flytta MIME-typen före för att se till att nya noder som du lägger till i CRXDE Lite inte tas bort av Experience Manager `image_`. Se även till att dess aktiverade värde är inställt på **[!UICONTROL false]**.

**Så här lägger du till MIME-typer för format som inte stöds:**

1. Logga in på Experience Manager as a Cloud Service som produktadministratör.
1. Från Experience Manager as a Cloud Service, gå till **[!UICONTROL Tools > Operations > Web Console]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. En ny flik i webbläsaren öppnas **[!UICONTROL Adobe Experience Manager Web Console Configuration]** sida.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. På sidan bläddrar du nedåt till namnet *Adobe CQ Scene7 Asset MIME type Service* enligt följande skärmbild. Tryck på **[!UICONTROL Edit the configuration values]** (pennikonen) till höger om namnet.

   ![Redigera konfigurationsvärdena](assets/2019-08-02_16-44-56.png)

1. På **Adobe CQ Scene7 Asset MIME Type Service** väljer du en plusteckenikon &lt;+>. Platsen i tabellen där du väljer plustecknet för att lägga till den nya MIME-typen är enkel.

   ![Adobe CQ Scene7 MIME Type Service](assets/2019-08-02_16-27-27.png)

1. Typ `DWG=image/vnd.dwg` i det tomma textfältet som du just lade till.

   The `DWG=image/vnd.dwg` MIME-typen är endast avsedd som exempel. MIME-typen som du lägger till här kan vara ett annat format som inte stöds.

   ![Lägger till MIME-typ för DWG](assets/2019-08-02_16-36-36.png)

1. Välj **[!UICONTROL Save]**.

   Nu kan du stänga webbläsarfliken som har den öppna konfigurationssidan för Adobe Experience Manager Web Console.

1. Gå tillbaka till webbläsarfliken som har din öppna Experience Manager as a Cloud Service konsol.
1. Från Experience Manager as a Cloud Service, gå till **[!UICONTROL Tools > General > CRXDE Lite]**.

   Om du inte har tillgång till CRXDE Lite kan du läsa [Använda CRXDE Lite](/help/implementing/developing/tools/crxde.md).

   ![Verktyg > Allmänt > CRXDE Lite](assets/2019-08-02_16-55-41.png)

1. Navigera till följande i den vänstra listen:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Dra MIME-typen `image_vnd.dwg` och släpp det direkt ovanför `image_` i trädet enligt följande skärmbild.

   ![Redigera en DWG-fil i CRXDE Lite](assets/crxdelite_cqdoc-14627.png)

1. Med MIME-typen `image_vnd.dwg` fortfarande markerad, från **[!UICONTROL Properties]** -fliken, i **[!UICONTROL enabled]** rad, under **[!UICONTROL Value]** kolumnrubrik, dubbeltryck på värdet. The **[!UICONTROL Value]** listrutan öppnas.
1. Typ `false` i fältet (eller markera **[!UICONTROL false]** från listrutan).

   ![Redigera MIME-typer i CRXDE Lite](assets/2019-08-02_16-60-30.png)

1. I närheten av det övre vänstra hörnet på CRXDE Lite-sidan väljer du **[!UICONTROL Save All]**.

### (Valfritt) Justera prestanda för Dynamic Media {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Behåll Dynamic Media <!--(with `dynamicmedia_scene7` run mode)--> Adobe rekommenderar följande finjusteringstips för synkroniseringsprestanda/skalbarhet:

* [Uppdatera de fördefinierade jobbparametrarna för bearbetning av olika filformat](#update-job-para).
* [Uppdatera de fördefinierade arbetsflödeskontakterna för Granite-arbetsflöden (videoresurser)](#update-granite-workflow-queue-worker-threads-video)
* [Uppdatera de fördefinierade arbetsflödeskontraderna för Granska övergångar (bilder och annat material)](#update-granite-transient-workflow-queue-worker-threads-images).
* [Uppdatera de maximala överföringsanslutningarna till Dynamic Media Classic-servern (Scene7)](#update-max-s7-upload-connections).

#### Uppdatera de fördefinierade jobbparametrarna för bearbetning av olika filformat {#update-job-para}

Du kan justera jobbparametrar för snabbare bearbetning när du överför filer. Om du till exempel överför PSD-filer, men inte vill bearbeta dem som mallar, kan du ange att lagerextraheringen ska vara false (av). I så fall visas den justerade jobbparametern enligt följande: `process=None&createTemplate=false`.

Om du vill aktivera mallskapande använder du följande parametrar: `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe rekommenderar att du använder följande &quot;justerade&quot; jobbparametrar för PDF, PostScript® och PSD:

| Filtyp | Rekommenderade jobbparametrar |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

Information om hur du uppdaterar parametrarna finns i [Redigera MIME-typer för format som stöds](#editing-mime-types-for-supported-formats).

Se även [Lägga till MIME-typer för format som inte stöds](#adding-mime-types-for-unsupported-formats).

#### Uppdatera de fördefinierade arbetsflödeskontakterna för Granite-arbetsflöden (videoresurser) {#update-granite-workflow-queue-worker-threads-video}

Beviljad arbetsflödeskö används för icke-tillfälliga arbetsflöden. I Dynamic Media bearbetar man video med **[!UICONTROL Dynamic Media Encode Video]** arbetsflöde.

>[!NOTE]
>
>Du måste vara inloggad på Experience Manager as a Cloud Service som produktadministratör för att kunna slutföra den här uppgiften.

Om du inte har tillgång till OSGi går du till [OSGi-konfiguration](/help/implementing/developing/components/overview.md#osgi-configuration).

**Så här uppdaterar du fördefinierade arbetsflödeskö (videoresurser) för Granite:**

1. Navigera till `https://<server>/system/console/configMgr` och söka efter **Kö: Begränsa arbetsflödeskö**.

   >[!NOTE]
   >
   >En textsökning är nödvändig i stället för en direkt URL eftersom OSGi PID genereras dynamiskt.

1. I **[!UICONTROL Maximum Parallel Jobs]** ändrar du talet till önskat värde.

   Som standard beror det maximala antalet parallella jobb på antalet tillgängliga processorkärnor. På en server med fyra kärnor tilldelas till exempel två arbetstrådar. (Ett värde mellan 0,0 och 1,0 är kvotbaserat, eller ett tal större än ett tilldelar antalet arbetstrådar.)

   I de flesta fall räcker standardinställningen 0,5.

   ![Konfiguration av en jobbbehandlingskö](assets/chlimage_1-1.jpeg)

1. Välj **[!UICONTROL Save]**.

#### Uppdatera fördefinierade Granska tillfälliga arbetsflödesköarbetstrådar {#update-granite-transient-workflow-queue-worker-threads-images}

Kön för Bevilja övergång används för **[!UICONTROL DAM Update Asset]** arbetsflöde. I Dynamic Media används den för att ta in och bearbeta bilder och andra resurser.

>[!NOTE]
>
>Du måste vara inloggad på Experience Manager as a Cloud Service som produktadministratör för att kunna slutföra den här uppgiften.

**Så här uppdaterar du de fördefinierade Granska tillfälliga arbetsflödesköarbetstrådarna:**

1. Navigera till **Konfiguration av Adobe Experience Manager Web Console** på `http://<host>:<port>/system/console/configMgr`
1. Sök efter **Kö: Bevilja tillfällig arbetsflödeskö**.

   >[!NOTE]
   >
   >En textsökning är nödvändig i stället för en direkt URL eftersom OSGi PID genereras dynamiskt.

1. I **[!UICONTROL Maximum Parallel Jobs]** ändrar du talet till önskat värde.

   Du kan öka **[!UICONTROL Maximum Parallel Jobs]** för att ge adekvat stöd för överföring av stora mängder filer till Dynamic Media. Det exakta värdet beror på maskinvarukapaciteten. I vissa scenarier, t.ex. en inledande migrering eller en massöverföring som görs en gång, kan du använda ett stort värde. Tänk dock på att användning av ett stort värde (till exempel två gånger antalet kärnor) kan ha negativa effekter på andra samtidiga aktiviteter. Testa och justera värdet utifrån ditt specifika användningsfall.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. Välj **[!UICONTROL Save]**.

#### Uppdatera de maximala överföringsanslutningarna till Dynamic Media Classic-servern (Scene7) {#update-max-s7-upload-connections}

Inställningen Dynamic Media Classic (Scene7) Upload Connection synkroniserar Experience Manager-resurser till Dynamic Media Classic-servrar.

>[!NOTE]
>
>Du måste vara inloggad på Experience Manager as a Cloud Service som produktadministratör för att kunna slutföra den här uppgiften.

**Så här uppdaterar du de maximala överföringsanslutningarna till Dynamic Media Classic-servern (Scene7):**

1. Navigera till `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. I **[!UICONTROL Number of connections]** eller **[!UICONTROL Active job timeout]** eller båda, ändra talet efter behov.

   The **[!UICONTROL Number of connections]** inställning styr det maximala antalet HTTP-anslutningar som tillåts för överföring från Experience Manager till Dynamic Media. Det fördefinierade värdet för tio anslutningar är vanligtvis tillräckligt.

   The **[!UICONTROL Active job timeout]** inställningen avgör väntetiden för överförda Dynamic Media-resurser som ska publiceras på leveransservern. Det här värdet är som standard 2 100 sekunder eller 35 minuter.

   I de flesta fall räcker det med inställningen 2 100.

   ![Adobe Scene7 Upload Service](assets/chlimage_1-2.jpeg)

1. Välj **[!UICONTROL Save]**.

<!-- NOTE - OBSOLETE that customisations to replication agents to transform content are no longer used; the following content is obsolete now 

### (Optional) Filtering assets for replication {#optional-filtering-assets-for-replication}

In non-Dynamic Media deployments, you replicate *all* assets (both images and video) from your Experience Manager as a Cloud Service author environment to the Experience Manager as a Cloud Service publish node. This workflow is necessary because the Experience Manager as a Cloud Service publish servers also deliver the assets.

However, in Dynamic Media deployments, because assets are delivered by way of the cloud service, there is no need to replicate those same assets to Experience Manager as a Cloud Service publish nodes. Such a "hybrid publishing" workflow avoids extra storage costs and longer processing times to replicate assets. Other content, such as Site pages, continue to be served from the Experience Manager as a Cloud Service publish nodes.

The filters provide a way for you to *exclude* assets from being replicated to the Experience Manager as a Cloud Service publish node.

#### Using default asset filters for replication {#using-default-asset-filters-for-replication}

If you are using Dynamic Media for imaging and/or video, then you can use the default filters that we provide as-is. The following filters are active by default:

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Filter</strong></td>
   <td><strong>Mimetype</strong></td>
   <td><strong>Renditions</strong></td>
  </tr>
  <tr>
   <td>Dynamic Media Image Delivery</td>
   <td><p>filter-images</p> <p>filter-sets</p> <p> </p> </td>
   <td><p>Starts with <strong>image/</strong></p> <p>Contains <strong>application/</strong> and ends with <strong>set</strong>.</p> </td>
   <td>The out-of-the-box "filter-images" (applies to single images assets, including interactive images) and "filter-sets" (applies to Spin Sets, Image Sets, Mixed Media Sets, and Carousel Sets) will:
    <ul>
     <li>Exclude from replication the original image and static image renditions.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media Video Delivery</td>
   <td>filter-video</td>
   <td>Starts with <strong>video/</strong></td>
   <td>The out-of-the-box "filter-video" will:
    <ul>
     <li>Exclude from replication the original video and static thumbnail renditions.<br /> <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Filters apply to mime types and cannot be path specific.

#### Customizing asset filters for replication {#customizing-asset-filters-for-replication}

1. In Experience Manager as a Cloud Service, select the Experience Manager as a Cloud Service logo to access the global navigation console and select the **[!UICONTROL Tools > General > CRXDE Lite]**.
1. In the left folder tree, navigate to `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` to review the filters.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. To define the Mime Type for the filter, you can locate the Mime Type as follows:

   In the left rail, expand `content > dam > <locate_your_asset> > jcr:content > metadata`, and then in the table, locate `dc:format`.

   The following graphic is an example of an asset's path to `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   Notice that the `dc:format` for the asset `Fiji Red.jpg` is `image/jpeg`.

   To have this filter apply to all images, regardless of their format, set the value to `image/*` where `*` is a regular expression that is applied to all images of any format.

   To have the filter apply only to images of the type JPEG, enter a value of `image/jpeg`.

1. Define what renditions you want to include or exclude from replication.

   Characters that you can use to filter for replication include the following:

<table>
 <tbody>
  <tr>
   <td><strong>Character to use</strong></td>
   <td><strong>How it filters assets for replication</strong></td>
  </tr>
  <tr>
   <td>*</td>
   <td>Wildcard character<br /> </td>
  </tr>
  <tr>
   <td>+</td>
   <td>Includes assets for replication.</td>
  </tr>
  <tr>
   <td>-</td>
   <td>Excludes assets from replication.</td>
  </tr>
 </tbody>
</table>

   Navigate to `content/dam/<locate your asset>/jcr:content/renditions`.

   The following graphic is an example of an asset's renditions.

   ![chlimage_1-4](assets/chlimage_1-4.png)

   If you only wanted to replicate the original, then you would enter `+original`.

   -->
