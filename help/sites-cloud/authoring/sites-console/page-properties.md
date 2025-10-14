---
title: Sidegenskaper
description: Lär dig mer om de olika egenskaper en sida kan ha och hur de styr sidans beteende och hur den hanteras.
exl-id: 27521a6d-c6e9-4f43-9ddf-9165b0316084
solution: Experience Manager Sites
feature: Authoring
role: User
mini-toc-levels: 2
source-git-commit: b9328a22ff544f2c663868d33d7b06e02819f1d7
workflow-type: tm+mt
source-wordcount: '2138'
ht-degree: 0%

---


# Sidegenskaper {#page-properties}

Lär dig mer om de olika egenskaper en sida kan ha och hur de styr sidans beteende och hur den hanteras.

>[!TIP]
>
>Mer information om hur du kan redigera och ändra en sidas egenskaper finns i dokumentet [Redigera sidegenskaper.](/help/sites-cloud/authoring/sites-console/edit-page-properties.md)

## Översikt och egenskapstillgänglighet {#overview}

Sidegenskaper kan styra många aspekter av en sida, från sidans titel och varumärke till dess behörigheter. Egenskaperna fördelas på flera flikar, varav vissa kan vara dolda beroende på sidtypen. Precis som de flesta egenskaper i AEM kan [sidegenskaper ärvas.](/help/sites-cloud/authoring/sites-console/edit-page-properties.md#inheritance)

>[!NOTE]
>
>Det här dokumentet beskriver alla möjliga sidegenskaper. Alla egenskaper är inte tillgängliga beroende på sidtypen.

## Fliken Grundläggande {#basic}

### Titel och taggar {#title-tags}

* **Titel** - Definierar sidmetanamnet för SEO-syften samt den rubrik som visas i sidinnehållet (om den inte åsidosätts)
   * Sidans titel visas på olika platser i AEM-gränssnittet, inklusive vyerna **Sites** kort/lista i [Platskonsolen.](/help/sites-cloud/authoring/sites-console/introduction.md)
   * Detta är ett obligatoriskt fält.
* **Taggar** - Definierar sidmetataggar för SEO-syften
   * Du kan lägga till eller ta bort taggar från sidan genom att uppdatera listan i markeringsrutan.
   * Använd listrutan för att välja bland befintliga taggar.
   * När du har valt en tagg visas den under markeringsrutan. Du kan ta bort en tagg från den här listan med hjälp av x.
   * Du kan ange en helt ny tagg genom att skriva namnet i en tom markeringsruta.
      * Den nya taggen skapas när du trycker på Retur.
      * Den nya taggen visas sedan med en liten stjärna till höger som anger att det är en ny tagg.
   * Ett x-tecken visas när du för musen över en taggpost i markeringsrutan, som kan användas för att ta bort taggen för den här sidan.
   * Mer information om taggar finns i [Använda tagg.](/help/sites-cloud/authoring/sites-console/tags.md)
* **Dölj i navigering** - Anger om sidan visas eller döljs i sidnavigeringen för den slutliga platsen

### Varumärke {#branding}

Använd en enhetlig varumärkesidentitet på alla sidor genom att lägga till en instruktionsmarginal till varje sidrubrik. Den här funktionen kräver att du använder Page Component från version 2.14.0 eller senare av [Core Components.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=sv-SE)

* **Varumärkesinstruktion**
   * **Åsidosätt** - Markera för att definiera instruktionsmarginalen för varumärket på den här sidan.
      * Värdet ärvs av alla underordnade sidor såvida inte deras **Åsidosätt**-värden också har angetts.
   * **Åsidosätt värde** - Texten i instruktionsmarginalen som ska läggas till i sidrubriken.
      * Värdet läggs till i sidtiteln efter ett lodstreck som `Cycling Tuscany | Always ready for the WKND`

### HTML ID {#html-id}

* **ID** - HTML-id som ska användas för komponenten.

### Fler rubriker och beskrivning {#more-titles}

* **Sidtitel** - En titel som ska användas på sidan
   * Detta används vanligtvis av titelkomponenter.
   * Om den är tom används **Title**.
* **Navigeringstitel** - Du kan ange en separat rubrik som ska användas i navigeringen (om du till exempel vill ha något mer koncist).
   * Om den är tom används **sidrubriken**.
* **Underrubrik** - Underrubrik för sidan
* **Beskrivning** - Din beskrivning av sidan, dess syfte eller annan information som du vill lägga till

### På/av-tid {#on-off-time}

På-/avaktiveringstiden för en sida är ett praktiskt sätt att tillfälligt dölja innehåll som redan är publicerat. Innehållet finns kvar i publiceringsinstansen när den är inaktiverad. Innehållet avpubliceras inte när du stänger av en sida.

* **I tid** - Det datum och den tidpunkt då den publicerade sidan visas (återges) i publiceringsmiljön. Sidan måste publiceras, antingen manuellt eller med förkonfigurerad automatisk replikering.

   * Om den redan är [publicerad](/help/sites-cloud/authoring/sites-console/publishing-pages.md) är den här sidan tillgänglig på publiceringsinstansen, men den behåller vilande (dold) tills återgivningen sker vid den angivna tidpunkten.
   * Om den inte publiceras och [konfigureras för automatisk replikering &#x200B;](/help/operations/replication.md#on-and-off-times-trigger-configuratio) publiceras sidan automatiskt och återges sedan vid den angivna tidpunkten.
   * Om sidan inte är publicerad och inte konfigurerad för automatisk replikering publiceras den inte automatiskt. Därför visas 404 när ett försök görs att komma åt sidan.

* **Fråntid** - Ungefär som och ofta används i kombination med **På tid**, definierar detta den tidpunkt då den publicerade sidan döljs i publiceringsmiljön.

Lämna dessa fält (**Vid tid** och **Fråntid**) tomma för sidor som du vill publicera och ha tillgängliga direkt och tillgängliga i publiceringsmiljön tills de inaktiveras (standardscenariot).

>[!NOTE]
>Om antingen **På-tid** eller **Av-tid** redan har inträffat och automatisk replikering har konfigurerats, utlöses den relevanta åtgärden omedelbart.

>[!TIP]
>
>På-/avaktiveringstider hanterar innehåll som redan har publicerats (antingen manuellt eller via automatisk replikering) strikt. Därför aktiveras inte publiceringsarbetsflöden, t.ex. sådana för godkännande av innehåll, av på-/av-tider och på-/av-tider påverkar inte sidans publiceringsstatus. Av den anledningen lämpar sig bäst för att tillfälligt visa/dölja innehåll som redan har godkänts och publicerats.
>
>Om du vill publicera nytt innehåll med alla associerade arbetsflöden eller helt ta bort (avpublicera innehåll) från webbplatsen bör du överväga att [hantera publikationen.](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication)

### Vanity URL {#vanity-url}

Med den här egenskapen kan du ange en innehålls-URL för den här sidan, vilket gör att du kan ha en kortare och/eller mer uttrycksfull URL. Om Vanity-URL:en till exempel är inställd på `welcome` för sidan som identifieras av sökvägen `/v1.0/startpage` för webbplatsen `http://example.com`, blir `http://example.com/welcome` vanity-URL:en för `http://example.com/content/v1.0/startpage`

>[!CAUTION]
>
>Vanity URL:er:
>
>* Måste vara unikt.
>* Använd inte regex-mönster.
>* Ska inte anges till en befintlig sida.

* **Lägg till** - Välj det här alternativet om du vill visa ett fält för att definiera en mål-URL för sidan.
   * Välj igen om du vill lägga till flera.
   * Markera ikonen **Ta bort** för att ta bort fågel-URL:en.
* **Omdirigerings-URL** - Anger om du vill att sidan ska använda innehålls-URL:en eller omdirigera till sidans faktiska URL

## Avancerat {#advanced}

### Inställningar {#settings}

* **Språk** - Sidspråket
* **Språkrot** - Måste kontrolleras om sidan är roten för en språkkopia
* **Omdirigering** - Anger den sida som den här sidan automatiskt ska omdirigeras till med HTML `302 Found` -status
   * **Permanent omdirigering** - När det här alternativet är markerat dirigeras sidan om till den angivna målsökvägen tillsammans med HTML `301 Moved Permanently` -statusen.
* **Design**
* **Alias** - Anger ett alias som ska användas för den här sidan
   * Om du till exempel definierar aliaset `private` för sidan `/content/wknd/us/en/magazine/members-only` kan den här sidan också nås via `/content/wknd/us/en/magazine/private`
   * Om du skapar ett alias anges egenskapen `sling:alias` på sidnoden, vilket bara påverkar resursen, inte databassökvägen.
   * Sidor som används av alias i redigeraren kan inte publiceras. [Publiceringsalternativ](/help/sites-cloud/authoring/sites-console/publishing-pages.md) i redigeraren är bara tillgängliga för sidor som du kommer åt via de faktiska sökvägarna.
   * Mer information finns i [Lokaliserade sidnamn under SEO och Bästa metoder för URL-hantering](/help/overview/seo-and-url-management.md#localized-page-names).

### Konfiguration {#configuration}

* **Ärvs från &lt;sökväg>** - Aktivera/inaktivera arv av **molnkonfigurationen** för sidan
   * Växlar tillgänglighet för **molnkonfiguration** för redigering

* **Molnkonfiguration** - Sökvägen till den valda konfigurationen

### Mallinställningar {#template-settings}

* **Tillåtna mallar** - [Definierar listan med mallar som är tillgängliga](/help/sites-cloud/authoring/page-editor/templates.md#enabling-and-allowing-a-template-template-author) i den här undergrenen
   * Varje värde måste vara en absolut sökväg till en mall.
   * Använd `/.*` om du vill tillåta alla mallar under den här sökvägen.
* **Använd sidan som mall** - [Skapa en ny mall baserad på den aktuella sidan.](/help/sites-cloud/authoring/universal-editor/templates.md)
   * Gäller endast för sidor som skapats för användning med den universella redigeraren som använder Edge Delivery Services.

### Autentiseringskrav {#authentication}

* **Aktivera** - Aktiverar användning av autentisering för att komma åt sidan

>[!NOTE]
>
>Stängda användargrupper för sidan definieras på fliken **[Behörigheter](#permissions)**.

* **Inloggningssida** - Den sida som ska användas för inloggning

### Exportera {#export}

* **Exportkonfiguration** - Anger en exportkonfiguration

## SEO {#seo}

* **Kanonisk URL** - Används för att skriva över sidans kanoniska URL
   * Om den lämnas tom är sidans URL dess kanoniska URL.

* **Robots-taggar** - Använd listrutan för att välja robots-taggar för att styra beteendet för sökmotorcrawler
   * Vissa alternativ står i konflikt med varandra, och i så fall har det mer tillåtna alternativet företräde.

* **Generera platskarta** - När du väljer det här alternativet genereras en `sitemap.xml` för den här sidan och dess underordnade sidor.

## Bilder {#images}

### Aktuell bild {#featured-image}

I det här avsnittet kan du välja och konfigurera den bild som ska visas. Detta används i komponenter som refererar till sidan, t.ex. teasers, page lists, etc.

* **Bild** - Du kan **välja** en resurs eller bläddra efter en fil som ska överföras och sedan **redigera** eller **rensa** den markerade bilden.
* **Alternativ text** - En text som används för att representera innebörden och/eller funktionen i bilden, som ofta används av skärmläsare
* **Ärv - värde som tagits från DAM-resursen** - När det här alternativet är markerat fylls den alternativa texten i med värdet för `dc:description`-metadata i DAM.

### Miniatyrbild {#thumbnail}

Det här avsnittet används för att välja och konfigurera sidans miniatyrbild. Detta används i komponenter som refererar till sidan, t.ex. teasers, page lists, etc.

* **Generera förhandsgranskning** - Generera en förhandsvisning av sidan som ska användas som miniatyrbild
* **Överför bild** - Överför en bild som ska användas som miniatyrbild
* **Välj bild** - Välj en befintlig resurs som ska användas som miniatyrbild
* **Återställ** - Det här alternativet blir tillgängligt när du har ändrat miniatyrbilden. Om du inte vill behålla ändringen kan du återställa den innan du sparar.

## Molntjänster {#cloud-services}

* **Cloud Service-konfigurationer** - Definierar vilken konfiguration som används för sidans molntjänster
* **Ärvd från** - För Live-kopior och språkkopior ärvs molnkonfigurationer som standard från utkast.
   * Avmarkera för att åsidosätta arv

## Personalization {#personalization}

### ContextHub-konfigurationer {#contexthub-config}

* **ContextHub-sökväg** - Definiera [ContextHub-konfigurationen](/help/sites-cloud/authoring/personalization/contexthub.md)
* **Segmentsökväg** - Definiera [segmentbanan](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)

### Målkonfiguration {#targeting-config}

* **Varumärke** - Definierar ett [varumärke som anger ett omfång för målgruppsanpassning](/help/sites-cloud/authoring/personalization/targeted-content.md)
   * Det här alternativet kräver att användarkontot finns i gruppen `Target Administrators`.

## Behörigheter {#permissions}

Använd fliken **Behörigheter** för att definiera vilka användare, grupper eller [stängda användargrupper (CUG)](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/closed-user-groups.html?lang=sv-SE) som kan komma åt och/eller ändra sidan.

* **Lägg till behörigheter**
* **Redigera stängd användargrupp**
* Visa **gällande behörigheter**

## Blueprint {#blueprint}

Den här fliken visas bara för sidor som fungerar som utkast. Utkast fungerar som bas för Live-kopior och ingår i [Hantering av flera webbplatser.](/help/sites-cloud/administering/msm/overview.md)

* **Utrullning** - Initiera en utrullning av utkast till Live-kopior
* **Översikt över Live-kopia** - Öppna ett fönster om du vill bläddra i sidstrukturen för Live-kopia
* **Aktuella live-kopior** - En lista med sidor som baseras på (det vill säga på live-kopior av) den valda designsidan

## Live Copy {#live-copy}

Den här fliken visas bara för sidor som har konfigurerats som live-kopior. Precis som med [utkast är &#x200B;](#blueprint) Live-kopior en del av [Multi Site Management (Hantering av flera webbplatser).](/help/sites-cloud/administering/msm/overview.md)

* **Synkronisera** - Synkronisera Live-kopia med utkast, med lokala ändringar
* **Återställ** - Återställ Live Copy till läget för utkast och ta bort lokala ändringar
* **Gör uppehåll** - Gör uppehåll i Live Copy vid ytterligare rolloutändringar
* **Koppla loss** - Frigör Live-kopia från utkast

### Source {#source}

* Visar sökvägen till ritningen för den här Live-kopian

### Status {#status}

* Visar sidans aktuella Live Copy-status

### Konfiguration {#live-copy-config}

* **Live Copy-arv** - Om det här alternativet är markerat gäller Live Copy-konfigurationen alla underordnade.
* **Ärv utrullningskonfigurationer från överordnad** - Om det här alternativet är markerat ärvs rollout-konfigurationen från den överordnade sidan för sidan.
* **Välj utrullningskonfiguration** - Definierar under vilka omständigheter ändringar sprids från utskriften och bara är tillgängliga när **Ärv utrullningskonfigurationer från överordnad** inte har valts
* **Lista över uteslutna sökvägar**

## Förhandsgranska {#preview}

När en [förhandsvisningsmiljö](/help/sites-cloud/authoring/sites-console/previewing-content.md) är aktiverad är följande information tillgänglig:

* **URL för förhandsgranskning** - Den URL som används för att komma åt innehållet i förhandsvisningsmiljön

## Progressiv webbapp {#progressive-web-app}

Genom en enkel konfiguration kan en innehållsförfattare aktivera funktioner för progressiva webbprogram (PWA) för upplevelser som skapats i AEM Sites. Din webbplats kan sedan uppträda som en inbyggd app genom att bli installerbar på hemskärmen på besökarens enhet och vara tillgänglig offline.

{{pwa-deprecation}}

### Konfigurera installerbar upplevelse {#config-pwa}

* **Aktivera PWA** - När det här alternativet är aktiverat kan sidans besökare installera webbplatsen som en PWA.
* **Start-URL** - URL som ska läsas in när användaren startar webbprogrammet
   * Om URL:en är relativ används manifest-URL:en som en bas-URL för att matcha
   * När den är tom används URL-adressen till sidan som programmet installerades från.
   * Vi rekommenderar att du anger ett värde.
* **Visningsläge** - Hur webbläsaren ska döljas eller på annat sätt visas för användaren på den lokala enheten
* **Skärmorientering** - Så här hanterar PWA enhetsorienteringar
* **Temafärg** - Färgen på appen som påverkar hur den lokala användarens operativsystem visar det inbyggda verktygsfältet och navigeringskontrollerna
* **Bakgrundsfärg** - Appens bakgrundsfärg, som visas när appen läses in
* **Ikon** - Den ikon som representerar appen på användarens enhet när PWA installeras

### Cachehantering (avancerat) {#cache-management}

* **Cachelagringsstrategi och frekvens för innehållsuppdatering** - Definierar cachelagringsmodellen för din PWA.
* **Filer att cachelagra för offlineanvändning**
   * **Filförcachelagring (teknisk förhandsgranskning)** - Filer som lagras i AEM sparas i den lokala webbläsarcachen när tjänstarbetaren installeras och innan den används.
   * **Bibliotek på klientsidan** - Bibliotek på klientsidan som ska cachelagras för offlineupplevelse
   * **Sökvägsinkluderingar** - Nätverksförfrågningar för de definierade sökvägarna fångas upp och cachelagrat innehåll returneras i enlighet med den konfigurerade cachelagringsstrategin och frekvensen för innehållsuppdatering
   * **Sökvägsundantag** - De här filerna kommer aldrig att cachelagras oavsett inställningarna under Filförcachelagring och Sökvägsinkluderingar.

>[!NOTE]
>
>Mer information finns i [Aktivera progressiva webbprogramfunktioner](/help/sites-cloud/authoring/sites-console/enable-pwa.md).

