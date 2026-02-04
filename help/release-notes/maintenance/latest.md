---
title: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell information om underhållsversionen av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: f01a98604e045c48ab7167122aee3b2468db6d52
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 0%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsversionen av Experience Manager as a Cloud Service.

## Version 24288 {#24288}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåva 24288, som offentliggjordes den 4 februari 2026. Den tidigare underhållsversionen var version 23963.

Funktionsaktiveringen i 2026.2.0 kommer att innehålla alla funktioner som finns i den här underhållsversionen. Mer information finns i [Experience Manager Releases Roadmap](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap).

>[!NOTE]
>
>Utgåva 2422 har gjorts privat.

### Förbättringar {#enhancements-24288}

* CNTBF-604: Skapa en ny paketversion för innehållbackflow.
* CQ-4361592: Stöd för att lägga till TypeHint för att skapa och uppdatera projekt.
* CQ-4362198: Senaste översättningar av AEM- och Granite-paket.
* GRANITE-36205: Uppdatera den interna versionen av Oak till den senaste versionen.
* GRANITE-59211: OPTEL: Engångssupport och självbetjäningskonfiguration har lagts till.
* GRANITE-62166: Uppdatera migreringspaketet för att återanvända migreringstillstånd från migreringsverktyget.
* GRANITE-62598: Ta bort överflödig egenskap som exkluderar från innehållspaketfilter.
* GRANITE-62684: Gör klientsocketens timeout konfigurerbar via skyltfönster.
* GRANITE-62702: Ersätt sling discovery med fristående implementering för onlinemigrering.
* GRANITE-62763: Uppdatera undantagslista över borttagning av Guava baserat på ASSETS-rotation.
* GRANITE-62771: Quickstart-byggen misslyckas när nya inaktuella Commons-Lang-beroenden införs.
* GRANITE-62987: Uppdatera Felix webconsole till version 5.0.18.
* GRANITE-63339: Förbättra leasingmekanismen för Azure-migreringsstatens blob.
* GRANITE-63343: Lägg till stöd för den senaste versionen av Sling API-paketet i workflow.core.
* GRANITE-63799: OIDC Authentication Bundle-version - Oump.
* GRANITE-63821: Uppdatera Quickstart till filevaults release som korrigerar JCRVLT-831/JCRVLT-839.
* GRANITE-63827: Uppdatera Quickstart till den senaste offentliga utgåvan av Oak (1.90.0).
* GRANITE-63888: Uppdatera Quickstart till Jackrabbit 2.22.3.
* GRANITE-64030: Lägg till nyckelord och mönster i tillåtelselista för språkvalideraren för uttryck.
* GRANITE-64050: Tillåt att dolda konf-mappar döljer externa produktfunktioner.
* SITES-30452: Content API with ASO - Title and Description Suggquestions.
* SITES-38099: Uppdatera `testing-model.txt` om du vill använda en senare version av säkerhetskontroller.
* SKYOPS-43616: Migrera Jenkins-autentiseringsuppgifter till Vault i dispatcherdatabaser.
* SKYOPS-108584: Ojämnhetsverktyget från 0.6.0 till 0.6.10.
* SKYOPS-115691: Uppgradera CORS-filterpaket för att lägga till Vary Origin-huvud vid preflight-begäranden.
* SKYOPS-123094: Uppdatera Apache HTTP-komponenter i QuickStart.
* SKYOPS-123236: Ta med `rep:cugPolicy` i replikeringspaketet.
* SKYOPS-123240: Uppdatera CRXDE-beroenden i QuickStart.
* SKYOPS-123247: Uppdatera Sling XSS-paketet i QuickStart.
* SKYOPS-123250: Uppdatera säkerhetspaket för Sling i QuickStart.
* SKYOPS-123327: Kräv Java 21 för AEM-CS SDK.
* SKYOPS-125574: Uppdatera nätcentrerade AC-verktygspaket i QuickStart.
* SKYOPS-126150: Förbättra det övre kommandot för generatorskript för tråddumpar.

### Åtgärdade problem {#fixed-issues-24288}

* FORMS-23687: Korrigera SSV-valideringsfel när innehåller regel används utan standardvärde.
* GRANITE-48472: Localize error when changing password in the Edit User Settings tab.
* GRANITE-50286: Åtgärda layoutproblem i statuskolumnen för modal användarhantering.
* GRANITE-52301: Localize Unable to commit changes to session string in Security Groups.
* GRANITE-52920: Fel vid lokalisering när användare skapas i Security Create New User.
* GRANITE-54654: Localize string in Security Adobe IMS Configurations Check dialog.
* GRANITE-56371: Korrigera felaktigt dataformat i Security Trust Store.
* GRANITE-62717: Uppgradera kryptografinyckelbehållare för JSafe-lösenordshantering med icke-ASCII-tecken.
* GRANITE-62789: Uppdatera meddelandeklient för att inte ha stöd för återförsöksläge vid innehållsdistribution.
* GRANITE-62824: Korrigera `NullPointerException` vid åtkomst till fliken Grupper i användarredigeraren.
* GRANITE-63080: Gör importen av `org.slf4j.spi` kompatibel med `slf4j 2.x`.
* GRANITE-63210: Uppdatera distributionskärnan för att korrigera invalidering av dispatcher vid publiceringsstart.
* GRANITE-63293: Korrigera obligatoriskt sökvägsfält och förlora den nödvändiga asterisken efter första redigeringen.
* GRANITE-63360: Korrigera felaktig information som visas när flera sökvägar är markerade.
* SITES-36242: Minska GraphQL execute regex för att korrigera förbikoppling av dispatcherfilter.
* SITES-40122: Korrigera Edge Delivery-integrering med ImsService för innehållsdistribution.
* SKYOPS-84379: Använd det senaste FAKTA-verktyget för att kunna växla upphämtning från RDE-enheter.
* SKYOPS-121216: Återställ uppdatering till bibliotek för Jackson 2.20.0.

#### AEM Guides {#guides-24288}

* GUIDES-38198: När du uppdaterar en infogad MathML-ekvation med alternativet Redigera MathML på snabbmenyn återspeglas inte det uppdaterade värdet förrän sidan uppdateras.
* GUIDES-38276: Det går inte att ta bort versionsetiketter från versionshistorikpanelen i Assets UI.
* GUIDES-36641: När du genererar AEM Sites-utdata inkluderas inte mappningsrubriker som innehåller nyckelord och ämnesrubriker med elementet `<ph>` i publicerade utdata.
* GUIDES-37837: När du försöker spara ett ämne eller en karta kan det hända att åtgärden misslyckas med ett fel av typen Det gick inte att spara, särskilt under intensiva resurshanteringsuppgifter eller översättningsarbetsflöden som körs i bakgrunden.
* GUIDES-27774: Rapporten med den brutna listan innehåller felaktiga externa länkar, giltiga `keyrefs` och nyckelord som är korrekt lösta inom den aktuella kartans omfång.

Mer information om de nya och förbättrade funktionerna och problemen som har åtgärdats i den här versionen finns i [Experience Manager Guides-lanseringens färdplan](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Kända fel {#known-issues-24288}

Ingen.

### Föråldrade funktioner och API:er {#deprecated-24288}

* AEMSRE-2896: Korrigera anpassad konfigurationshantering för logghanterare.
* GRANITE-62802: Ta bort föråldrat `commons-lang`-beroende från `granite.auth.saml`.
* GRANITE-62805: Ta bort föråldrat `commons-lang`-beroende från `granite.httpcache.core`.
* GRANITE-62864: Ta bort föråldrat `commons-lang`-beroende från `granite.jobs.async`.
* GRANITE-62865: Ta bort föråldrat `commons-lang`-beroende från `granite.replication.core`.
* GRANITE-62868: Ta bort föråldrat `commons-lang`-beroende från `granite.rest.api`.
* GRANITE-62895: Ta bort föråldrat `commons-lang`-beroende från `translation.connector.msft.core`.
* GRANITE-63069: `com.adobe.granite.httpcache.core` har tagits bort.
* GRANITE-63179: Ta bort föråldrat `commons-lang`-beroende från `cq-workflow-impl`.
* GRANITE-63180: Ta bort föråldrad `commons.lang`-export från paketet `cq-mailer`.
* SKYOPS-123329: Släpp Java 11-stöd för AEM Ethos-distributioner och uppdatera `commons-lang3`.
* SKYOPS-124983: Ta bort inaktuella `nashorn.args` från AEM startskript.

Inaktuella och borttagna funktioner och API:er i AEM as a Cloud Service beskrivs i dokumentet [Inaktuella och Borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Säkerhetskorrigeringar {#security-24288}

AEM as a Cloud Service strävar efter att optimera säkerheten och prestandan för din plattform. Den här underhållsversionen åtgärdar 10 identifierade sårbarheter, vilket stärker vårt engagemang för robust systemskydd.

### Inbäddade tekniker {#embedded-tech-24288}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.90.0 | [Oak 1.90.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| AEM SLING API | 2.27.6 | [API:t för Apache Sling 2.27.6 &#x200B;](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Språkspecifikation för HTML-mall](https://github.com/adobe/htl-spec) |
| Apache HTTP-server | 2.4.65 | [Apache HTTP 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Grundläggande komponenter i AEM | 2.30.2 | [AEM WCM Core Components](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (standard) | [Node.js-versioner som stöds](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
