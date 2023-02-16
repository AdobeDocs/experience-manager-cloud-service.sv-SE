---
title: Versionsinformation för 2022.7.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för 2022.7.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: b339ab48-e836-4589-a573-9c50917b9280
source-git-commit: 7b21a8af886c8e1f209e3b7cc5d94de5c58be1ac
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner; till exempel för 2020, 2021 och så vidare.

>[!NOTE]
>
>Se [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) för information om dokumentationsuppdateringar som inte är direkt relaterade till en release.

## Releasedatum {#release-date}

Releasedatum [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2022.7.0) är 8 augusti 2022.

Nästa version (2022.8.0) är planerad till 1 september 2022.

## Släpp video {#release-video}

Titta på videon med versionsöversikten för juli 2022 om du vill se en sammanfattning av funktioner som lagts till i version 202.7.0:

>[!VIDEO](https://video.tv.adobe.com/v/345409/?quality=12)

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Sites] {#sites-features}

* The [Konsol för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) nu har stöd för [kortkommandon](/help/sites-cloud/administering/content-fragments/content-fragments-console-keyboard-shortcuts.md).

* AEM som Cloud Service [webboptimerad bildleverans](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html) ger möjlighet att avsevärt förbättra sidhastigheten genom att leverera format som WebP. Den här nya tjänsten erbjuder också flexiblare alternativ för storleksändring och omformning av bilder. Alla versioner av [Core Image Component](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html) kan du använda den här tjänsten och leverera bilder som WebP genom att klicka på ett alternativ i bildkomponentens profil.

* AEM kan nu utnyttja upplevelsefragment i stället för våra gamla erbjudanden. Den här funktionen:
   * möjliggör en migreringsväg där AEM innehåll skulle främja upplevelsefragmenterbjudanden i stället för äldre bibliotekserbjudanden för att tillhandahålla lämpligt formaterat innehåll som passar personaliseringen i stor skala framåt.
   * förhindrar att innehållsförfattare av misstag skickar oformaterat innehåll till sin webbplats.
   * gör att målinriktningsläge för alla komponenter kan konverteras till ett upplevelsefragment (både JSON- och HTML-typer) som använder redigerbara mallar.

>[!NOTE]
>
>Befintliga personaliseringsaktiviteter som redan använder äldre erbjudanden kan fortsätta att göra det, men nya personaliseringsaktiviteter bör skapas som upplevelsefragment eftersom det är det rekommenderade tillvägagångssättet.

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i [!DNL Assets] prerelease channel {#prerelease-features-assets}

Nu kan du konfigurera Adobe Experience Manager Assets till [begränsa vilken typ av resurser som användare kan överföra baserat på MIME-typen](/help/assets/configure-asset-upload-restrictions.md).

![Begränsningar för överföring av tillgångar](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Forms] {#forms-features}

* **[Stöd för tangentbordsinmatning med Scribble-signaturer](/help/forms/signing-forms-using-scribble.md)**: Adaptiv Forms används i allt större utsträckning på pekenheter, och ett vanligt krav är att stödja signaturer. Att signera dokument på pekenheter har blivit ett accepterat sätt att signera formulär. Adaptiv Forms har inbyggt stöd för Scribble Signatures och Adobe Sign för sådana användningsområden. Nu kan du, tillsammans med andra alternativ som redan stöds, även använda tangentbordet för att göra signaturer smarta i ett adaptivt formulär. Det förbättrar också tillgängligheten.

![Stöd för tangentbordsinmatning för klottersignaturer på iphone](/help/release-notes/assets/scribble-keyboard-mobile.png)

* **Använd guiden Adaptiv Forms på det lokala språket**: Du kan använda guiden på valfritt språk. Det har nu stöd för alla språk som stöds av Adobe Experience Manager.

### Nya funktioner i [!DNL Forms] prerelease channel {#prerelease-features-forms}

<!-- 

* **[Launch Adaptive Form creation wizard from embed form component](/help/forms/using/embed-adaptive-form-aem-sites.md)**: You can now launch Adaptive Form creation wizard from embed form component. It helps improve content and forms authoring workflows for Sites and Forms practitioners trying to add enrollment experiences to a web page. 

![Keyboard input support for Scribble signatures on iphone](/help/release-notes/assets/froms-container.png) 

-->

* **[Anropa DDX - ett AEM arbetsflödessteg](/help/forms/aem-forms-workflow-step-reference.md#invokeddx)**: Document Description XML (DDX) är ett deklarativt kodspråk vars element representerar byggstenar av dokument. Dessa byggstenar innehåller PDF- och XDP-dokument och andra element som kommentarer, bokmärken och formaterad text. DDX-dokument är mallar för dokumenten och beskriver önskade egenskaper för källdokument som ska visas i resulterande dokument. Ett enda DX kan användas med ett antal olika källdokument. Du kan använda steget Anropa och AEM arbetsflöde för att utföra olika åtgärder, t.ex. att samla ihop dokument, skapa och ändra Acrobat och XFA Forms samt andra åtgärder som beskrivs i [DDX-referens](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf) dokumentation.

* **[Konvertera till PDF/A - ett AEM arbetsflödessteg](/help/forms/aem-forms-workflow-step-reference.md##convert-pdfa)**: PDF/A är ett arkiveringsformat som gör att dokumentets innehåll bevaras på lång sikt. Alla teckensnitt bäddas in och filen är okomprimerad. Nu kan du använda steget Konvertera till PDF/A och AEM arbetsflöde för att konvertera dina dokument eller filer i valfritt format till PDF/A-format.


## CIF-tillägg {#cloud-services-cif}

### Vad är nytt? {#what-is-new-cif}

* Produktkatalogsberikning har nu stöd för AEM sidor. Detta gör att författare kan hantera sida - produktassociation.

* Olika förbättringar av CIF-kärnkomponenten

### Felkorrigeringar {#bug-fixes-cif}

* Lägg till inloggningstoken till prishämtning på klientsidan

* Fel sidkomponent i datalagret

## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation {#foundation}

### Vad är nytt? {#what-is-new-foundation}

* The [Databasläsare](/help/implementing/developing/tools/repository-browser.md) har nu ett sökvägsinmatningsfält, vilket gör det möjligt att hoppa direkt till en viss mapp i databashierarkin
* Sling Content Distribution (SCD) har nu stöd för en explicit&quot;invalidation&quot;-åtgärd för att göra innehåll ogiltigt utan att innehållet publiceras. Se [Cachelagring i AEM as a Cloud Service](/help/implementing/dispatcher/caching.md#explicit-invalidation) sida för mer information.
* mod_macro finns nu i AEM as a Cloud Service. Se [det här registret](/help/implementing/dispatcher/disp-overview.md) för en lista över Apache-moduler som stöds.

### Förbättringar i AEM as a Cloud Service SDK Dispatcher Tools {#dispatcher-tools-enhancements}

* Apache kan startas med `docker_run_hot_reload.sh` som automatiskt läser in och validerar alla efterföljande ändringar i cache- och dispatcherkonfigurationen, vilket förbättrar utvecklarhastigheten. Stöds endast för flyttarverktygens flexibla läge. Se även [Felsöka konfigurationen av Apache och Dispatcher](/help/implementing/dispatcher/validation-debug.md#automatic-reloading) om du vill ha mer information om automatisk omladdning och validering.
* Lokal konfiguration av cache/dispatcher spårar förändringar i molnmiljöer närmare, vilket ökar pariteten mellan de två miljöerna.

### Nya funktioner i [!DNL Experience Manager] prerelease channel {#prerelease-features-foundation}

* AEM as a Cloud Service är nu integrerat med Unified Shell för att förbättra användarupplevelsen och göra den enhetlig med alla andra Experience Cloud-program. Se [AEM as a Cloud Service on Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md) för mer information.

## Adobe Learning Manager Connectors {#learn-manage}

* Nya Adobe Learning Manager har kopplingar till Adobe Experience Manager Sites, Marketo Engage och Adobe Commerce. Mer information finns i: [Användarhandbok för Adobe Learning Manager](https://helpx.adobe.com/learning-manager/user-guide.html).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här.](/help/implementing/cloud-manager/release-notes/current.md)

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
