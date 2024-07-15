---
title: Versionsinformation för version 2022.7.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för version 2022.7.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: b339ab48-e836-4589-a573-9c50917b9280
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# Versionsinformation 202278.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2022.7.0-versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner, till exempel för versionerna 2020, 2021 och så vidare.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som aktuell [!DNL Cloud Service]-version (2022.7.0) är 8 augusti 2022.

Nästa version (2022.8.0) är planerad till 1 september 2022.

## Släpp video {#release-video}

Titta på videon med versionsöversikten för juli 2022 om du vill se en sammanfattning av funktioner som lagts till i version 202.7.0:

>[!VIDEO](https://video.tv.adobe.com/v/345409/?quality=12)

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Sites] {#sites-features}

* [Konsolen för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) har nu stöd för [kortkommandon](/help/sites-cloud/administering/content-fragments/keyboard-shortcuts.md).

* AEM som Cloud Servicens [webboptimerade bildleverans](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html) kan förbättra sidhastigheten avsevärt genom att leverera format som WebP. Den här nya tjänsten erbjuder också flexiblare alternativ för storleksändring och omformning av bilder. I alla versioner av [kärnbildkomponenten](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html) kan du använda den här tjänsten och leverera bilder som WebP genom att klicka på ett alternativ i bildkomponentens profil.

* AEM personaliseringsaktiviteter kan nu använda upplevelsefragment i stället för våra gamla erbjudanden. Den här funktionen:
   * möjliggör en migreringsväg där AEM innehåll skulle främja upplevelsefragmenterbjudanden i stället för äldre bibliotekserbjudanden för att tillhandahålla lämpligt formaterat innehåll som passar personaliseringen i stor skala framåt.
   * förhindrar att innehållsförfattare av misstag skickar oformaterat innehåll till sin webbplats.
   * gör att målinriktningsläge för alla komponenter kan konverteras till ett upplevelsefragment (både JSON- och HTML-typer) som använder redigerbara mallar.

>[!NOTE]
>
>Befintliga personaliseringsaktiviteter som redan använder äldre erbjudanden kan fortsätta att göra det, men nya personaliseringsaktiviteter bör skapas som upplevelsefragment eftersom det är det rekommenderade tillvägagångssättet.

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Assets] {#prerelease-features-assets}

Du kan nu konfigurera Adobe Experience Manager Assets att [begränsa vilken typ av resurser som användare kan överföra baserat på MIME-typen](/help/assets/configure-asset-upload-restrictions.md).

![Resursöverföringsbegränsningar](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Forms] {#forms-features}

* **[Stöd för tangentbordsinmatning för signaturer](/help/forms/signing-forms-using-scribble.md)**: Adaptiv Forms används i allt större utsträckning på enheter med pekskärm, och ett vanligt krav är att stödja signaturer. Att signera dokument på pekenheter har blivit ett accepterat sätt att signera formulär. Adaptiv Forms har inbyggt stöd för Scribble Signatures och Adobe Sign för sådana användningsområden. Nu kan du, tillsammans med andra alternativ som redan stöds, även använda tangentbordet för att göra signaturer till klottersignaturer i ett adaptivt formulär. Det förbättrar också tillgängligheten.

![Tangentbordsinmatningsstöd för klottersignaturer på iphone](/help/release-notes/assets/scribble-keyboard-mobile.png)

* **Använd guiden Adaptiv Forms på det lokala språket**: Du kan använda guiden på valfritt språk. Det har nu stöd för alla språk som stöds av Adobe Experience Manager.

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Forms] {#prerelease-features-forms}

<!-- 

* **[Launch Adaptive Form creation wizard from embed form component](/help/forms/using/embed-adaptive-form-aem-sites.md)**: You can now launch Adaptive Form creation wizard from embed form component. It helps improve content and forms authoring workflows for Sites and Forms practitioners trying to add enrollment experiences to a web page. 

![Keyboard input support for Scribble signatures on iphone](/help/release-notes/assets/froms-container.png) 

-->

* **[Anropa DDX - Ett AEM arbetsflödessteg](/help/forms/aem-forms-workflow-step-reference.md#invokeddx)**: XML-kod för dokumentbeskrivning (DDX) är ett deklarativt kodspråk vars element representerar byggstenar av dokument. Dessa byggstenar innehåller PDF- och XDP-dokument och andra element som kommentarer, bokmärken och formaterad text. DDX-dokument är mallar för dokumenten och beskriver önskade egenskaper för källdokument som ska visas i resulterande dokument. Ett enda DX kan användas med ett antal olika källdokument. Du kan använda steget Anropa och AEM arbetsflöde för att utföra olika åtgärder, som att sätta ihop isär dokument, skapa och ändra Acrobat och XFA Forms samt andra åtgärder som beskrivs i [DDX Reference](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf) -dokumentationen.

* **[Konvertera till PDF/A - Ett AEM arbetsflödessteg](/help/forms/aem-forms-workflow-step-reference.md##convert-pdfa)**: PDF/A är ett arkiveringsformat för långtidsbevaring av dokumentets innehåll, alla teckensnitt bäddas in och filen är okomprimerad. Nu kan du använda steget Konvertera till PDF/A och AEM arbetsflöde för att konvertera dina dokument eller filer i valfritt format till PDF/A-format.


## CIF {#cloud-services-cif}

### Nyheter {#what-is-new-cif}

* Produktkatalogsberikning har nu stöd för AEM sidor. Detta gör att författare kan hantera sida - produktassociation.

* Förbättringar av CIF kärnkomponent

### Felkorrigeringar {#bug-fixes-cif}

* Lägg till inloggningstoken till prishämtning på klientsidan

* Fel sidkomponent i datalagret

## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### Nyheter {#what-is-new-foundation}

* [Databasläsaren](/help/implementing/developing/tools/repository-browser.md) har nu ett sökvägsinmatningsfält, vilket gör det möjligt att hoppa direkt till en viss mapp i databashierarkin
* Sling Content Distribution (SCD) har nu stöd för en explicit&quot;invalidation&quot;-åtgärd som gör innehållet ogiltigt utan att det publiceras. Mer information finns i [Cachelagring i AEM as a Cloud Service](/help/implementing/dispatcher/caching.md#explicit-invalidation).
* mod_macro finns nu i AEM as a Cloud Service. I [den här tabellen](/help/implementing/dispatcher/disp-overview.md) finns en lista över Apache-moduler som stöds.

### Förbättringar av Dispatcher-verktygen i AEM as a Cloud Service SDK {#dispatcher-tools-enhancements}

* Apache kan startas med skriptet `docker_run_hot_reload.sh`, som automatiskt läser in och validerar alla efterföljande ändringar i cache- och dispatcherkonfigurationen, vilket förbättrar utvecklarhastigheten. Stöds endast för flyttarverktygens flexibla läge. Mer information om automatisk omladdning och validering finns i [Felsöka Apache- och Dispatcher-konfigurationen](/help/implementing/dispatcher/validation-debug.md#automatic-reloading).
* Lokal konfiguration av cache/dispatcher spårar förändringar i molnmiljöer närmare, vilket ökar pariteten mellan de två miljöerna.

### Nya funktioner som är tillgängliga i betaversionskanalen i [!DNL Experience Manager] {#prerelease-features-foundation}

* AEM as a Cloud Service är nu integrerat med Unified Shell för att förbättra användarupplevelsen och göra den enhetlig med alla andra Experience Cloud-program. Mer information finns i [AEM as a Cloud Service i Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md).

## Adobe Learning Manager Connectors {#learn-manage}

* Nya Adobe Learning Manager har kontakter till Adobe Experience Manager Sites, Marketo Engage och Adobe Commerce. Mer information finns i: [Adobe Learning Manager användarhandbok](https://helpx.adobe.com/learning-manager/user-guide.html).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över migreringsverktygen [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
