---
title: Konfigurera Dynamic Media Cloud Service
description: Lär dig konfigurera Dynamic Media i Adobe Experience Manager as a Cloud Service.
contentOwner: Rick Brough
feature: Configuration,Dynamic Media
role: Admin,User
exl-id: 8e07bc85-ef26-4df4-8e64-3c69eae91e11
source-git-commit: 2ca425f9a142432a5d3bcce8ce522c97e4c2cf2d
workflow-type: tm+mt
source-wordcount: '3500'
ht-degree: 1%

---

# Konfigurera Dynamic Media Cloud Service {#configuring-dynamic-media}

{{work-with-dynamic-media}}

Om du använder Adobe Experience Manager as a Cloud Service för olika miljöer, som utveckling, testning och liveproduktion, konfigurerar du Dynamic Media Cloud Services för var och en av dessa miljöer.

Se även [Konfigurera ett Dynamic Media Company-alias](/help/assets/dynamic-media/dm-alias-account.md)

>[!IMPORTANT]
>
>**Dynamiska media (Scene7) stöds inte i Förbättrade säkerhetsmiljöer**
>
>Dynamic Media (Scene7) på AEM as a Cloud Service är inte HIPAA-klart och kan inte användas i AEM-miljöer där Förbättrat skydd är aktiverat.
>
>Från och med AEM as a Cloud Service-versionen från april 2025 förhindrar en teknisk begränsning att Dynamic Media (Scene7) konfigureras i miljöer med förbättrat skydd. Därför är kortet **Dynamisk mediekonfiguration** under **Verktyg** > **Molntjänster** inte längre synligt i dessa miljöer.
>
>Dessutom bör kunder som använder AEM 6.5 vara medvetna om att stacken Dynamic Media (Scene7) inte är HIPAA-klar.

## Arkitektur för Dynamic Media {#architecture-diagram-of-dynamic-media}

I följande arkitekturdiagram beskrivs hur Dynamic Media fungerar.

Med den nya arkitekturen ansvarar Experience Manager för primära källmaterial och synkronisering med Dynamic Media för bearbetning och publicering av material:

1. När den primära källresursen överförs till Adobe Experience Manager as a Cloud Service replikeras den till Dynamic Media. I det läget hanterar Dynamic Media all materialbearbetning och återgivningsgenerering, till exempel videokodning och dynamiska varianter av en bild.
1. När renderingarna har skapats kan Experience Manager as a Cloud Service på ett säkert sätt komma åt och förhandsgranska de dynamiska fjärrrenderingarna (inga binärfiler skickas tillbaka till Experience Manager as a Cloud Service-instansen).
1. När innehållet är klart för publicering och godkännande aktiveras Dynamic Media-tjänsten för att skicka innehåll till leveransservrar och cachelagra innehåll på CDN (Content Delivery Network).

![chlimage_1-550](assets/chlimage_1-550.png)

>[!NOTE]
>
>Följande funktionslista kräver att du använder det färdiga CDN som medföljer Adobe Experience Manager - Dynamic Media. Andra anpassade CDN stöds inte med dessa funktioner.
>
>* [Smart bildbehandling](/help/assets/dynamic-media/imaging-faq.md)
>* [Cacheogiltigförklaring](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
>* [Hotlink-skydd](/help/assets/dynamic-media/hotlink-protection.md)
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

## Skapa en dynamisk mediekonfiguration i molntjänster {#configuring-dynamic-media-cloud-services}

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=sv-SE#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. I Experience Manager as a Cloud Service väljer du Experience Manager as a Cloud Service logotyp för att komma åt den globala navigeringskonsolen.
1. Till vänster om konsolen väljer du verktygsikonen och går till **[!UICONTROL Cloud Services > Dynamic Media Configuration]**.
1. På sidan Dynamic Media Configuration Browser väljer du **[!UICONTROL global]** i den vänstra rutan (markera inte mappikonen till vänster om **[!UICONTROL global]**). Välj sedan **[!UICONTROL Create]**.
1. På sidan **[!UICONTROL Create Dynamic Media Configuration]** anger du rubriken, e-postadressen för Dynamic Media-kontot och lösenordet för företagsadministratören för Dynamic Media-kontot och väljer sedan region. Den här informationen tillhandahålls av Adobe i e-postmeddelandet om etablering. Kontakta Adobe kundsupport om du inte fått det här mejlet.
1. Välj **[!UICONTROL Connect to Dynamic Media]**.
1. I dialogrutan **[!UICONTROL Change Password]** anger du ett nytt lösenord som består av 8-25 tecken i fältet **[!UICONTROL New Password]**. Lösenordet måste innehålla minst ett av följande:

   * Versaler
   * Gemener
   * Nummer
   * Specialtecken: `# $ & . - _ : { }`

   Fältet **[!UICONTROL Current Password]** är avsiktligt ifyllt och dolt för interaktion.

   Om det behövs kan du kontrollera stavningen av ett lösenord som du har skrivit eller skrivit in igen genom att markera lösenordsikonen för att visa lösenordet. Klicka på ikonen igen om du vill dölja lösenordet.

1. Skriv det nya lösenordet igen i fältet **[!UICONTROL Repeat Password]** och välj sedan **[!UICONTROL Done]**.

   Det nya lösenordet sparas när du väljer **[!UICONTROL Save]** i det övre högra hörnet på sidan **[!UICONTROL Create Dynamic Media Configuration]**.

   Om du valde **[!UICONTROL Cancel]** i dialogrutan **[!UICONTROL Change Password]** måste du fortfarande ange ett nytt lösenord när du sparar den skapade Dynamic Media-konfigurationen.

   Se även [Ändra lösenordet till Dynamic Media](#change-dm-password).

1. När anslutningen lyckas kan du ange följande:

   | Egenskap | Beskrivning |
   |---|---|
   | Företag | Namnet på Dynamic Media-kontot.<br>**Viktigt**: Endast en dynamisk mediekonfiguration i molntjänster stöds i en instans av Experience Manager. Lägg inte till mer än en konfiguration. Adobe stöder *inte* eller rekommenderar att du konfigurerar flera dynamiska mediekonfigurationer på en enda Experience Manager-instans.<!-- CQDOC-19579 and CQDOC-19612 --><br>Se även [Konfigurera ett Dynamic Media Company-alias](/help/assets/dynamic-media/dm-alias-account.md). |
   | Företagets rotmappsökväg | Företagets rotmappsökväg. |
   | Publicera Assets | Du kan välja mellan följande tre alternativ:<br>**[!UICONTROL Immediately]**- När resurser överförs importeras resurserna och URL/Embed anges omedelbart. Ingen användaråtgärd krävs för att publicera resurser.<br>**[!UICONTROL On Activation]** - Du måste publicera resursen explicit innan en URL/Embed-länk anges.<br>**[!UICONTROL Selective Publish]**- Assets publiceras automatiskt endast för säker förhandsvisning. De kan också publiceras explicit på Experience Manager as a Cloud Service utan att publiceras på DMS7 för att levereras offentligt. I framtiden har detta alternativ till syfte att publicera material till Experience Manager as a Cloud Service och publicera material till Dynamic Media, som inte utesluter varandra. Det innebär att du kan publicera resurser på DMS7 så att du kan använda funktioner som Smart Crop eller dynamiska återgivningar. Du kan också publicera resurser exklusivt i Experience Manager as a Cloud Service för förhandsgranskning. Samma resurser publiceras inte i DMS7 för att distribueras offentligt. |
   | Secure Preview Server | Här kan du ange URL-sökvägen till förhandsgranskningsservern för säkra återgivningar. Det innebär att när renderingar har skapats kan AEM as a Cloud Service på ett säkert sätt komma åt och förhandsgranska de dynamiska fjärrrenderingarna (inga binärfiler skickas tillbaka till Experience Manager as a Cloud Service-instansen).<br>Om du inte har en särskild överenskommelse om hur du ska använda företagets server eller en speciell server rekommenderar Adobe att du låter den här inställningen vara angiven. |
   | Synkronisera allt innehåll | Markerad som standard. Avmarkera det här alternativet om du vill inkludera eller exkludera vissa resurser från synkroniseringen till dynamiska media. Om du avmarkerar det här alternativet kan du välja mellan följande två synkroniseringslägen för dynamiska media:<br>**[!UICONTROL Dynamic Media sync mode]**<br>**[!UICONTROL Enable by default]**- Konfigurationen tillämpas som standard på alla mappar, såvida du inte markerar en mapp speciellt för undantag.<!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL Disabled by default]** - Konfigurationen tillämpas inte på någon mapp förrän du uttryckligen markerar en markerad mapp för synkronisering till Dynamic Media.<br>Om du vill markera en markerad mapp för synkronisering till dynamiska media markerar du en resursmapp och väljer **[!UICONTROL Properties]** i verktygsfältet. På fliken **[!UICONTROL Details]** i listrutan **[!UICONTROL Dynamic Media sync mode]** väljer du bland följande tre alternativ. Välj **[!UICONTROL Save]** när du är klar. _Kom ihåg: dessa tre alternativ är inte tillgängliga om du valde **Synkronisera allt innehåll**&#x200B;tidigare._ Se även [Arbeta med selektiv publicering på mappnivå i Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).<br>**[!UICONTROL Inherited]**- Det finns inget explicit synkroniseringsvärde för mappen. I stället ärver mappen synkroniseringsvärdet från en av de överordnade mapparna eller standardläget i molnkonfigurationen. Detaljerad status för ärvda program via ett verktygstips.<br>**[!UICONTROL Enable for subfolders]** - Inkludera allt i det här underträdet för synkronisering till dynamiska media. De mappspecifika inställningarna åsidosätter standardläget i molnkonfigurationen.<br>**[!UICONTROL Disabled for subfolders]**- Uteslut allt i det här underträdet från synkronisering till Dynamic Media. |

   >[!NOTE]
   >
   >Det finns inget stöd för versionshantering i Dynamic Media. Försenad aktivering gäller bara om **[!UICONTROL Publish Assets]** på sidan Redigera dynamisk mediekonfiguration är inställd på **[!UICONTROL Upon Activation]**. Och sedan bara tills första gången tillgången aktiveras.
   >
   >
   >När en mediefil har aktiverats publiceras alla uppdateringar direkt till S7 Delivery.

   ![dynamicmediaconfiguration2uppdaterad](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. Välj **[!UICONTROL Save]**. Det nya lösenordet och den nya konfigurationen för Dynamic Media sparas. Om du valde **[!UICONTROL Cancel]** i stället sker ingen lösenordsuppdatering.
1. I dialogrutan **[!UICONTROL Configuring Dynamic Media]** väljer du **[!UICONTROL OK]** för att starta konfigurationen.

   >[!IMPORTANT]
   >
   >När den nya Dynamic Media-konfigurationen är klar får du ett statusmeddelande i Experience Manager as a Cloud Service Inbox.
   >
   >Det här inkorgsmeddelandet informerar dig om konfigurationen lyckades eller inte.
   > Mer information finns i [Felsöka en ny konfiguration för dynamiska media](#troubleshoot-dm-config) och [Inkorgen](/help/sites-cloud/authoring/inbox.md).

1. För att förhandsgranska dynamiskt mediematerial säkert innan det publiceras använder Experience Manager as a Cloud Service tokenbaserad validering och Experience Manager Author förhandsgranskar därför dynamiskt mediematerial som standard. Du kan *tillåtslista* ytterligare IP-adresser om du vill ge användarna åtkomst till förhandsgranskningsinnehållet på ett säkert sätt. Information om hur du konfigurerar den här åtgärden i Experience Manager as a Cloud Service finns i [Konfigurera inställningar för dynamisk mediepublicering för bildserver - säkerhet](/help/assets/dynamic-media/dm-publish-settings.md#security-tab). <!-- To securely preview Dynamic Media content before it gets published, you must "allowlist" the Experience Manager as a Cloud Service author instance to connect to Dynamic Media. To set up this action, do the following: -->

<!--
    * Open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=sv-SE#getting-started), then sign in to your account. Your credentials and sign-in details were provided by Adobe at the time of provisioning. If you do not have this information, contact Adobe Customer Support.
    * On the navigation bar near the upper right corner of the page, go to **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**.
    * On the Image Server Publish page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * For the Client Address Filter, select **[!UICONTROL Add]**.
    * To enable (turn on) the address, select the check box, then enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * Select **[!UICONTROL Save]**. -->

Du är nu klar med den grundläggande konfigurationen. Du är redo att använda Dynamic Media.

Om du vill anpassa konfigurationen ytterligare, t.ex. aktivera åtkomstkontrollistan (ACL), kan du utföra alla åtgärder under [Konfigurera avancerade inställningar i dynamiska media](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

### Felsöka en ny konfiguration för dynamiska media {#troubleshoot-dm-config}

När en ny konfiguration för Dynamic Media är klar får du ett statusmeddelande i Experience Manager as a Cloud Service Inbox. Det här meddelandet informerar dig om konfigurationen lyckades eller inte, vilket visas i följande bilder från Inkorgen.

![Experience Manager Inbox lyckades](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![Experience Manager Inbox-fel](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

Se även [Inkorgen](/help/sites-cloud/authoring/inbox.md).

**Så här felsöker du en ny konfiguration för dynamiska media:**

1. I det övre högra hörnet av Experience Manager as a Cloud Service-sidan väljer du klockikonen och sedan **[!UICONTROL View All]**.
1. På sidan Inkorg väljer du meddelandet om att åtgärden lyckades. Där kan du läsa en översikt över konfigurationens status och loggar.

   Om konfigurationen misslyckas väljer du felmeddelandet som liknar följande skärmbild.

   ![Installationen av dynamiska media misslyckades](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. Granska konfigurationsinformationen som beskriver felet på sidan **[!UICONTROL DMSETUP]**. Tänk särskilt på eventuella felmeddelanden eller felkoder. Kontakta Adobe kundsupport.

   ![Sidan för konfiguration av dynamiska media](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### Ändra lösenordet till Dynamic Media {#change-dm-password}

Lösenordets giltighetstid i Dynamic Media är inställd på 100 år från det aktuella systemdatumet.

Lösenordet måste innehålla minst ett av följande:

* Versaler
* Gemener
* Nummer
* Specialtecken: `# $ & . - _ : { }`

Om det behövs kan du kontrollera stavningen av ett lösenord som du har skrivit eller skrivit in igen genom att markera lösenordsikonen för att visa lösenordet. Klicka på ikonen igen om du vill dölja lösenordet.

Det ändrade lösenordet sparas när du väljer **[!UICONTROL Save]** i det övre högra hörnet på sidan **[!UICONTROL Edit Dynamic Media Configuration]**.

1. I Experience Manager as a Cloud Service väljer du Experience Manager as a Cloud Service logotyp för att komma åt den globala navigeringskonsolen.
1. Till vänster om konsolen väljer du verktygsikonen och går till **[!UICONTROL Cloud Services > Dynamic Media Configuration]**.
1. På sidan Dynamic Media Configuration Browser väljer du **[!UICONTROL global]** i den vänstra rutan. Välj inte mappikonen till vänster om **[!UICONTROL global]**. Välj sedan **[!UICONTROL Edit]**.
1. Välj **[!UICONTROL Change Password]** på sidan **[!UICONTROL Edit Dynamic Media Configuration]**, direkt under fältet **[!UICONTROL Password]**.
1. Gör följande i dialogrutan **[!UICONTROL Change Password]**:

   * Ange ett nytt lösenord i fältet **[!UICONTROL New Password]**.

     Fältet **[!UICONTROL Current Password]** är avsiktligt ifyllt och dolt för interaktion.

   * Skriv det nya lösenordet igen i fältet **[!UICONTROL Repeat Password]** och välj sedan **[!UICONTROL Done]**.

1. I det övre högra hörnet på sidan **[!UICONTROL Edit Dynamic Media Configuration]** väljer du **[!UICONTROL Save]** och sedan **[!UICONTROL OK]**.

## (Valfritt) Konfigurera avancerade inställningar i Dynamic Media{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Om du vill anpassa konfigurationen och konfigurationen av Dynamic Media ytterligare, eller optimera dess prestanda, kan du utföra en eller flera av följande _valfria_ uppgifter:

* [(Valfritt) Aktivera ACL-behörigheter i Dynamic Media](#optional-enable-acl)
* [(Valfritt) Konfigurera inställningar för Dynamic Media](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [(Valfritt) Justera prestanda för Dynamic Media](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

<!-- Removed as per CQDOC-20701 - May need to revisit and update. In Adobe Experience Manager (AEM) as a Cloud Service, enabling Access Control List (ACL) permissions for Dynamic Media requires a different approach compared to on-premise versions (which was described below), as direct editing of OSGi configurations via the UI is not supported. Not sure how this is done now. For example, you can manage ACLs using tools like the Netcentric Access Control Tool (AC Tool), which simplifies the specification and deployment of complex ACLs in AEM but I doubt that's the recommended method.

### (Optional) Enable Access Control List permissions in Dynamic Media {#optional-enable-acl}

When you run Dynamic Media on AEM as a Cloud Service, it currently forwards `/is/image` requests to Secure Preview Image Serving without checking ACL (Access Control List) permissions on the PlatformServerServlet. You can, however, _enable_ ACL permissions. Doing so forwards the authorized `/is/image` requests. If a user is not authorized to access the asset, a "403 - Forbidden" error is displayed.

**To enable Access Control List permissions in Dynamic Media on AEM as a Cloud Service:**

1. From Adobe Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. A new browser tab opens to the **[!UICONTROL Adobe Experience Manager Web Console Configuration]** page.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. On the page, scroll to the name _Adobe CQ Scene7 PlatformServer_.

1. To the right of the name, select the pencil icon (**[!UICONTROL Edit the configuration values]**).

1. On the **com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.name** page, select the check box for the following two settings:

   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.cache.enable.name` &ndash; When enabled, this setting caches permission results for two minutes (default) to save.
   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.validate.userAccess.name` &ndash; When enabled, this setting validates a user's access while they preview assets by way of Dynamic Media Image Server.

   ![Enable Access Control List settings in Dynamic Media - Scene7 mode](/help/assets/dynamic-media/assets/acl.png)

1. Near the lower-right corner of the page, select **[!UICONTROL Save]**.
-->

### (Valfritt) Konfigurera inställningar för Dynamic Media {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

Använd Dynamic Media Classic användargränssnitt för att ändra inställningarna för Dynamic Media.

<!-- Some of the tasks above require that you open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=sv-SE#getting-started), then sign in to your account. -->

Installations- och konfigureringsuppgifter omfattar följande:

* [Konfigurera Dynamic Media Publish Setup för Image Server](#publishing-setup-for-image-server)
* [Konfigurera allmänna inställningar för dynamiska media](#configuring-application-general-settings)
* [Konfigurera färghantering](#configuring-color-management)
* [Redigera MIME-typer för format som stöds](#editing-mime-types-for-supported-formats)
* [Lägg till MIME-typer för format som inte stöds](#adding-mime-types-for-unsupported-formats)
<!-- OBSOLETE BUT LEAVE FOR POSSIBLE FUTURE* [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### Konfigurera Dynamic Media Publish Setup för Image Server {#publishing-setup-for-image-server}

På sidan Dynamic Media Publish Setup anges standardinställningar som avgör hur resurser levereras från Adobe Dynamic Media-servrar till webbplatser eller program.

Se [Konfigurera inställningar för dynamisk mediepublicering för bildserver](/help/assets/dynamic-media/dm-publish-settings.md).

#### Konfigurera allmänna inställningar för dynamiska media {#configuring-application-general-settings}

Konfigurera URL:en för det dynamiska mediet **[!UICONTROL Publish Server Name]** och URL:en för **[!UICONTROL Origin Server Name]**. Du kan också ange **[!UICONTROL Upload to Application]**-inställningar och **[!UICONTROL Default Upload Options]** alla baserat på ditt specifika användningsfall.

Se [Konfigurera allmänna inställningar för dynamiska media](/help/assets/dynamic-media/dm-general-settings.md).

#### Konfigurera färghantering {#configuring-color-management}

Med färghanteringen i Dynamic Media kan du färgkorrigera resurser. Med färgkorrigering behåller inkapslade resurser färgmodellen (RGB, CMYK, Grå) och den inbäddade färgprofilen. När du begär en dynamisk återgivning korrigeras bildfärgen till målfärgrymden med hjälp av CMYK-, RGB- eller gråskaleutdata.

Se [Konfigurera bildförinställningar](/help/assets/dynamic-media/managing-image-presets.md).

Så här konfigurerar du standardfärgegenskaperna för aktivering av färgkorrigering när du begär bilder:

1. Öppna [Dynamic Media Classic-datorprogrammet](https://experienceleague.adobe.com/sv/docs/dynamic-media-classic/using/getting-started/signing-out#getting-started) och logga sedan in på ditt konto med de autentiseringsuppgifter som anges under etableringen.
1. Gå till **[!UICONTROL Setup > Application Setup]**.
1. Expandera området **[!UICONTROL Publish Setup]** och markera **[!UICONTROL Image Server]**. Ange **[!UICONTROL Publish Context]** som **[!UICONTROL Image Serving]** när du anger standardvärden för publiceringsinstanser.
1. Bläddra till egenskapen som du måste ändra, till exempel en egenskap i området **[!UICONTROL Color Management Attributes]**.
Du kan ange följande egenskaper för färgkorrigering:

   | Egenskap | Beskrivning |
   |---|---|
   | Standardfärgmodell för CMYK | Namn på CMYK-standardfärgprofilen. |
   | Standardfärgrymd för gråskala | Namnet på standardfärgprofilen för grått. |
   | RGB standardfärgrymd | Namn på RGB standardfärgprofil. |
   | Återgivningsmetod för färgkonvertering | Anger återgivningsmetod. Godtagbara värden är: **[!UICONTROL perceptual]**, **[!UICONTROL relative colometric]**, **[!UICONTROL saturation]**, **[!UICONTROL absolute colometric]**. Adobe rekommenderar **[!UICONTROL relative]** som standard. |

1. Välj **[!UICONTROL Save]**.

Du kan till exempel ställa in **[!UICONTROL RGB Default Color Space]** på *sRGB* och **[!UICONTROL CMYK Default Color Space]** på *WebCoated*.

Om du gör det gör du så här:

* Aktiverar färgkorrigering för RGB- och CMYK-bilder.
* RGB-bilder som inte har någon färgprofil antas finnas i färgrymden *sRGB*.
* CMYK-bilder som inte har någon färgprofil antas finnas i färgrymden *WebCoated*.
* Dynamiska återgivningar som returnerar RGB-utdata returnerar det i färgrymden *sRGB* .
* Dynamiska återgivningar som returnerar CMYK-utdata returnerar det i färgrymden *WebCoated* .

#### Redigera MIME-typer för format som stöds {#editing-mime-types-for-supported-formats}

Du kan ange de resurstyper som Dynamic Media behandlar och anpassa de avancerade parametrarna för materialbearbetning. Du kan till exempel ange parametrar för tillgångsbearbetning för att göra följande:

* Konvertera en Adobe PDF till en eCatalog-resurs.
* Konvertera ett Adobe Photoshop-dokument (.PSD) till en bannermallsresurs för personalisering.
* Rastrera en Adobe Illustrator-fil (.AI) eller en Adobe Photoshop Encapsulated PostScript®-fil (.EPS).
* [Videoprofiler](/help/assets/dynamic-media/video-profiles.md) och [Bildprofiler](/help/assets/dynamic-media/image-profiles.md) kan användas för att definiera bearbetning av videoklipp och bilder.

Se [Överför resurser](/help/assets/add-assets.md).

**Så här redigerar du MIME-typer för de format som stöds:**

1. Logga in på din Experience Manager as a Cloud Service som produktadministratör.
1. I Experience Manager as a Cloud Service väljer du Experience Manager as a Cloud Service logotyp för att komma åt den globala navigeringskonsolen och går sedan till **[!UICONTROL General > CRXDE Lite]**.

   Om du inte har tillgång till CRXDE Lite, se [Använda CRXDE Lite](/help/implementing/developing/tools/crxde.md).

1. Navigera till följande i den vänstra listen:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME-typer](assets/mimetypes.png)

1. Välj en MIME-typ i mappen mimeTypes.
1. Till höger på CRXDE Lite-sidan i den nedre delen:

   * Dubbelmarkera fältet **[!UICONTROL enabled]**. Som standard är alla MIME-typer för resurser aktiverade (inställda på **[!UICONTROL true]**), vilket innebär att resurserna synkroniseras till Dynamic Media för bearbetning. Om du vill utesluta den här resursens MIME-typ från bearbetningen ändrar du den här inställningen till **[!UICONTROL false]**.

   * Dubbelmarkera **[!UICONTROL jobParam]** om du vill öppna det associerade textfältet. Se [MIME-typer som stöds](/help/assets/file-format-support.md) för en lista över tillåtna värden för bearbetningsparametrar som du kan använda för en viss MIME-typ.

1. Gör något av följande:
   * Upprepa steg 3-4 för att redigera fler MIME-typer.
   * Välj **[!UICONTROL Save All]** på menyraden på CRXDE Lite-sidan.

1. I det övre vänstra hörnet av sidan väljer du **[!UICONTROL CRXDE Lite]** för att återgå till Experience Manager as a Cloud Service.

#### Lägg till MIME-typer för format som inte stöds {#adding-mime-types-for-unsupported-formats}

Du kan lägga till anpassade MIME-typer för format som inte stöds i Experience Manager Assets. Om du inte vill att Experience Manager ska kunna ta bort nya noder som du lägger till i CRXDE Lite flyttar du MIME-typen före `image_`. Kontrollera också att dess aktiverade värde är **[!UICONTROL false]**.

**Så här lägger du till MIME-typer för format som inte stöds:**

1. Logga in på din Experience Manager as a Cloud Service som produktadministratör.
1. Gå till **[!UICONTROL Tools > Operations > Web Console]** från Experience Manager as a Cloud Service.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. En ny flik i webbläsaren öppnas på sidan **[!UICONTROL Adobe Experience Manager Web Console Configuration]**.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. På sidan bläddrar du nedåt till namnet *Adobe CQ Scene7-resursens MIME-typtjänst*, vilket visas på följande skärmbild. Till höger om namnet väljer du pennikonen **[!UICONTROL Edit the configuration values]**.

   ![Redigera konfigurationsvärdena](assets/2019-08-02_16-44-56.png)

1. På sidan **Adobe CQ Scene7 Asset MIME type Service** väljer du en plusteckenikon &lt;+>. Platsen i tabellen där du väljer plustecknet för att lägga till den nya MIME-typen är enkel.

   ![Adobe CQ Scene7 Asset Mime Type Service](assets/2019-08-02_16-27-27.png)

1. Skriv `DWG=image/vnd.dwg` i det tomma textfältet som du just lade till.

   MIME-typen `DWG=image/vnd.dwg` är endast avsedd som exempel. MIME-typen som du lägger till här kan vara ett annat format som inte stöds.

   ![Lägger till MIME-typ för DWG](assets/2019-08-02_16-36-36.png)

1. Välj **[!UICONTROL Save]** i sidans nedre högra hörn.

   Nu kan du stänga webbläsarfliken som har den öppna konfigurationssidan för Adobe Experience Manager Web Console.

1. Gå tillbaka till webbläsarfliken som har din öppna Experience Manager as a Cloud Service-konsol.
1. Gå till **[!UICONTROL Tools > General > CRXDE Lite]** från Experience Manager as a Cloud Service.

   Om du inte har tillgång till CRXDE Lite, se [Använda CRXDE Lite](/help/implementing/developing/tools/crxde.md).

   ![Verktyg > Allmänt > CRXDE Lite](assets/2019-08-02_16-55-41.png)

1. Navigera till följande i den vänstra listen:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Dra MIME-typen `image_vnd.dwg` och släpp den direkt ovanför `image_` i trädet enligt skärmbilden nedan.

   ![Redigera en DWG-fil i CRXDE Lite](assets/crxdelite_cqdoc-14627.png)

1. Med MIME-typen `image_vnd.dwg` markerad dubbelmarkerar du värdet på fliken **[!UICONTROL Properties]** i raden **[!UICONTROL enabled]** under kolumnrubriken **[!UICONTROL Value]**. Listrutan **[!UICONTROL Value]** öppnas.
1. Skriv `false` i fältet (eller välj **[!UICONTROL false]** i listrutan).

   ![Redigera MIME-typer i CRXDE Lite](assets/2019-08-02_16-60-30.png)

1. I det övre vänstra hörnet på CRXDE Lite-sidan väljer du **[!UICONTROL Save All]**.

### (Valfritt) Justera prestanda för Dynamic Media {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Adobe rekommenderar följande finjusteringstips för synkroniseringsprestanda/skalbarhet för att Dynamic Media ska fungera smidigt:

* [Uppdatera de fördefinierade jobbparametrarna för bearbetning av olika filformat](#update-job-para).
* [Uppdatera de fördefinierade arbetsflödeskontakterna för Granite-arbetsflöden (videoresurser)](#update-granite-workflow-queue-worker-threads-video)
* [Uppdatera de fördefinierade Granska tillfälliga arbetsflödesköerna (bilder och icke-videoresurser) för arbetstrådar](#update-granite-transient-workflow-queue-worker-threads-images).
* [Uppdatera de maximala överföringsanslutningarna till Dynamic Media Classic-servern (Scene7)](#update-max-s7-upload-connections).

#### Uppdatera fördefinierade jobbparametrar för bearbetning av olika filformat {#update-job-para}

Du kan justera jobbparametrar för snabbare bearbetning när du överför filer. Om du till exempel överför PSD-filer, men inte vill bearbeta dem som mallar, kan du ange att lagerextraheringen ska vara false (av). I så fall visas den justerade jobbparametern enligt följande: `process=None&createTemplate=false`.

Om du vill aktivera mallskapande använder du följande parametrar: `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe rekommenderar att du använder följande&quot;justerade&quot; jobbparametrar för PDF-, PostScript®- och PSD-filer:

| Filtyp | Rekommenderade jobbparametrar |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

Om du vill uppdatera någon av de här parametrarna läser du [Redigera MIME-typer för de format som stöds](#editing-mime-types-for-supported-formats).

Se även [Lägga till MIME-typer för format som inte stöds](#adding-mime-types-for-unsupported-formats).

#### Uppdatera de fördefinierade arbetsflödeskontakterna för Granite-arbetsflöden (videoresurser) {#update-granite-workflow-queue-worker-threads-video}

Beviljad arbetsflödeskö används för icke-tillfälliga arbetsflöden. I Dynamic Media används den för att bearbeta video med arbetsflödet **[!UICONTROL Dynamic Media Encode Video]**.

>[!NOTE]
>
>Du måste vara inloggad på Experience Manager as a Cloud Service som produktadministratör för att kunna utföra den här uppgiften.

Om du inte har tillgång till OSGi läser du [OSGi Configuration](/help/implementing/developing/components/overview.md#osgi-configuration).

**Så här uppdaterar du de fördefinierade arbetsflödeskö (videoresurser) för arbetstrådar:**

1. Navigera till `https://<server>/system/console/configMgr` och sök efter **Kö: Begränsa arbetsflödeskö**.

   >[!NOTE]
   >
   >En textsökning är nödvändig i stället för en direkt URL eftersom OSGi PID genereras dynamiskt.

1. Ändra talet till det önskade värdet i fältet **[!UICONTROL Maximum Parallel Jobs]**.

   Som standard beror det maximala antalet parallella jobb på antalet tillgängliga CPU-kärnor. På en server med fyra kärnor tilldelas till exempel två arbetsflöden. (Ett värde mellan 0,0 och 1,0 är kvotbaserat, eller ett tal större än ett tilldelar antalet arbetstrådar.)

   I de flesta fall räcker standardinställningen 0,5.

   ![Konfiguration av en jobbbehandlingskö](assets/chlimage_1-1.jpeg)

1. Välj **[!UICONTROL Save]**.

#### Uppdatera fördefinierade Granska tillfälliga arbetsflödesköarbetstrådar {#update-granite-transient-workflow-queue-worker-threads-images}

Bevilja transittjänstens arbetsflödeskö används för arbetsflödet **[!UICONTROL DAM Update Asset]**. I Dynamic Media används den för att hämta och bearbeta bilder och andra resurser.

>[!NOTE]
>
>Du måste vara inloggad på Experience Manager as a Cloud Service som produktadministratör för att kunna utföra den här uppgiften.

**Så här uppdaterar du fördefinierade Granska tillfälliga arbetsflödeskö för arbetstrådar:**

1. Navigera till **Adobe Experience Manager Web Console-konfigurationen** på `http://<host>:<port>/system/console/configMgr`
1. Sök efter **kö: Bevilja tillfällig arbetsflödeskö**.

   >[!NOTE]
   >
   >En textsökning är nödvändig i stället för en direkt URL eftersom OSGi PID genereras dynamiskt.

1. Ändra talet till det önskade värdet i fältet **[!UICONTROL Maximum Parallel Jobs]**.

   Du kan öka **[!UICONTROL Maximum Parallel Jobs]** för att stödja tillräckligt stor överföring av filer till Dynamic Media. Det exakta värdet beror på maskinvarukapaciteten. I vissa scenarier, t.ex. en inledande migrering eller en massöverföring som görs en gång, kan du använda ett stort värde. Tänk dock på att användning av ett stort värde (till exempel två gånger antalet kärnor) kan ha negativa effekter på andra samtidiga aktiviteter. Testa och justera värdet utifrån ditt specifika användningsfall.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. Välj **[!UICONTROL Save]**.

#### Uppdatera de maximala överföringsanslutningarna till Dynamic Media Classic-servern (Scene7) {#update-max-s7-upload-connections}

Inställningen Dynamic Media Classic (Scene7) Upload Connection synkroniserar Experience Manager-resurser till Dynamic Media Classic-servrar.

>[!NOTE]
>
>Du måste vara inloggad på Experience Manager as a Cloud Service som produktadministratör för att kunna utföra den här uppgiften.

**Så här uppdaterar du det maximala antalet överföringsanslutningar till Dynamic Media Classic-servern (Scene7):**

1. Navigera till `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. I fältet **[!UICONTROL Number of connections]**, i fältet **[!UICONTROL Active job timeout]** eller båda, ändrar du talet efter behov.

   Inställningen **[!UICONTROL Number of connections]** styr det maximala antalet HTTP-anslutningar som tillåts för överföring av Experience Manager till dynamiska media. Det fördefinierade värdet för tio anslutningar är vanligtvis tillräckligt.

   Inställningen **[!UICONTROL Active job timeout]** definierar hur länge systemet väntar på att leveransservern ska publicera överförda dynamiska medieresurser. Det här värdet är som standard 2 100 sekunder eller 35 minuter.

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
