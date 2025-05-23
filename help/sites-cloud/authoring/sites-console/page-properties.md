---
title: Redigera sidegenskaper
description: Lär dig definiera de egenskaper som krävs för att hantera en sida i AEM.
exl-id: 27521a6d-c6e9-4f43-9ddf-9165b0316084
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 8d31907392e09bc5b3c669b8f8f23d6a2a26ced4
workflow-type: tm+mt
source-wordcount: '2454'
ht-degree: 2%

---

# Redigera sidegenskaper {#editing-page-properties}

Du kan definiera de egenskaper som krävs för en sida. Dessa kan variera beroende på sidans beskaffenhet. Vissa sidor kan t.ex. vara kopplade till en live-kopia medan andra inte är det och live-kopieringsinformationen är tillgänglig om det är lämpligt.

## Sidegenskaper {#page-properties}

Egenskaperna fördelas på flera flikar.

### Grundläggande {#basic}

* **Titel och taggar**

   * **Rubrik** - Sidans rubrik visas på olika platser. Till exempel fliklistan **Webbplatser** och vyerna **Webbplatser** kort/lista.
      * Detta är ett obligatoriskt fält.
   * **Taggar** - Här kan du lägga till eller ta bort taggar från sidan genom att uppdatera listan i markeringsrutan.
      * När du har valt en tagg visas den under markeringsrutan. Du kan ta bort en tagg från den här listan med hjälp av x.
      * Du kan ange en helt ny tagg genom att skriva namnet i en tom markeringsruta.
         * Den nya taggen skapas när du trycker på Retur.
         * Den nya taggen visas sedan med en liten stjärna till höger som anger att det är en ny tagg.
      * Med den nedrullningsbara menyn kan du välja bland befintliga taggar.
      * Ett x-tecken visas när du för musen över en taggpost i markeringsrutan, som kan användas för att ta bort taggen för den här sidan.
      * Mer information om taggar finns i [Använda taggar](/help/sites-cloud/authoring/sites-console/tags.md).
   * **Dölj i navigering** - Anger om sidan visas eller döljs i sidnavigeringen för den slutliga platsen.

* **Varumärke**

  Använd en enhetlig varumärkesidentitet på alla sidor genom att lägga till en instruktionsmarginal till varje sidrubrik. Den här funktionen kräver att du använder Page Component från version 2.14.0 eller senare av [Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=sv-SE).

   * **Varumärkesinstruktion**

      * **Åsidosätt** - Markera för att definiera instruktionsmarginalen för varumärket på den här sidan.
         * Värdet ärvs av alla underordnade sidor såvida inte deras **Åsidosätt**-värden också har angetts.
      * **Åsidosätt värde** - Texten i instruktionsmarginalen som ska läggas till i sidrubriken.
         * Värdet läggs till i sidrubriken efter ett lodstreck som &quot;Cycling Tuscany&quot; | Alltid redo för WKND&quot;

* **HTML ID**

   * **ID** - HTML-id som ska användas för komponenten.

* **Fler rubriker och beskrivning**

   * **Sidtitel** - En titel som ska användas på sidan. Används vanligtvis av titelkomponenter. Om den är tom används **Title**.
   * **Navigeringstitel** - Du kan ange en separat rubrik som ska användas i navigeringen (om du till exempel vill ha något mer koncist). Om den är tom används **Title**.
   * **Bildtext** - En underrubrik som kan användas på sidan.
   * **Beskrivning** - Din beskrivning av sidan, dess syfte eller annan information som du vill lägga till.

* **På/av-tid**

  >[!NOTE]
  >
  > Information om hur du konfigurerar den relaterade automatiska replikeringen finns i [På- och Av-tider - utlösarkonfiguration](/help/operations/replication.md#on-and-off-times-trigger-configuration).

  >[!NOTE]
  >Om antingen **På-tid** eller **Av-tid** redan har inträffat och automatisk replikering har konfigurerats, utlöses den relevanta åtgärden omedelbart.

   * **I tid** - Det datum och den tidpunkt då den publicerade sidan visas (återges) i publiceringsmiljön. Sidan måste publiceras, antingen manuellt eller med förkonfigurerad automatisk replikering.

      * Om redan [har publicerats (manuellt)](/help/sites-cloud/authoring/sites-console/publishing-pages.md) behålls den här sidan vilande (dold) tills återgivningen sker vid den angivna tidpunkten.
      * Om sidan inte publiceras och konfigureras för automatisk replikering publiceras den automatiskt och återges sedan vid den angivna tidpunkten.
      * Om sidan inte är publicerad och inte konfigurerad för automatisk replikering publiceras den inte automatiskt, så en 404-sida visas när ett försök görs att komma åt sidan.

   * **Fråntid** - Ungefär som och ofta används i kombination med **På tid**, definierar detta den tidpunkt då den publicerade sidan döljs i publiceringsmiljön.

   * Lämna dessa fält (**Vid tid** och **Fråntid**) tomma för sidor som du vill publicera omedelbart och som är tillgängliga i publiceringsmiljön tills de inaktiveras (standardscenariot).

* **Vanity URL**

   * Här kan du ange en fågel-URL för den här sidan, vilket gör att du kan ha en kortare och/eller mer uttrycksfull URL.
   * Om Vanity-URL:en till exempel är inställd på `welcome` för sidan som identifieras av sökvägen `/v1.0/startpage` för webbplatsen `http://example.com`, blir `http://example.com/welcome` vanity-URL:en för `http://example.com/content/v1.0/startpage`

  >[!CAUTION]
  >
  >Vanity URL:er:
  >
  >* Måste vara unikt så du bör vara försiktig med att värdet inte redan används av en annan sida.
  >* Använd inte regex-mönster.
  >* Ska inte anges till en befintlig sida.

   * **Lägg till** - Välj det här alternativet om du vill visa ett fält för att definiera en mål-URL för sidan.
      * Välj igen om du vill lägga till flera.
      * Markera ikonen **Ta bort** för att ta bort fågel-URL:en.
   * **URL för omdirigering av vanity** - Anger om du vill att sidan ska använda den överordnade URL:en.

### Avancerat {#advanced}

* **Inställningar**

   * **Språk** - Sidspråket
   * **Språkrot** - Måste kontrolleras om sidan är roten för en språkkopia
   * **Omdirigering** - Anger sidan som den här sidan automatiskt ska omdirigeras till med statusen HTML `302 Found`.
      * **Permanent omdirigering** - När det här alternativet är markerat dirigeras sidan om till den angivna målsökvägen tillsammans med HTML `301 Moved Permanently` -statusen.
   * **Design** - Anger om sidan visas eller döljs i sidnavigeringen för den slutliga webbplatsen
   * **Alias** - Anger ett alias som ska användas för den här sidan
      * Om du till exempel definierar aliaset `private` för sidan `/content/wknd/us/en/magazine/members-only` kan den här sidan också nås via `/content/wknd/us/en/magazine/private`
      * Om du skapar ett alias anges egenskapen `sling:alias` på sidnoden, vilket bara påverkar resursen, inte databassökvägen.
      * Sidor som används av alias i redigeraren kan inte publiceras. [Publiceringsalternativ](/help/sites-cloud/authoring/sites-console/publishing-pages.md) i redigeraren är bara tillgängliga för sidor som du kommer åt via de faktiska sökvägarna.
      * Se [Lokaliserade sidnamn under SEO och Bästa praxis för URL-hantering](/help/overview/seo-and-url-management.md#localized-page-names).

* **Konfiguration**

   * **Ärvs från &lt;sökväg>** - aktivera/inaktivera arv; växlar tillgänglighet för **molnkonfiguration** för markering

   * **Molnkonfiguration** - Sökvägen till den valda konfigurationen

* **Mallinställningar**

   * **Tillåtna mallar** - [Definierar listan med mallar som är tillgängliga](/help/sites-cloud/authoring/page-editor/templates.md#enabling-and-allowing-a-template-template-author) i den här undergrenen
   * **Använd sidan som mall** - [Skapa en ny mall baserad på den aktuella sidan.](/help/sites-cloud/authoring/universal-editor/templates.md)
      * Gäller endast för sidor som skapats för användning med den universella redigeraren som använder Edge Delivery Services.

* **Autentiseringskrav**

   * **Aktivera** - Aktivera användning av autentisering för att få åtkomst till sidan

     >[!NOTE]
     >
     >Stängda användargrupper för sidan definieras på fliken **[Behörigheter](#permissions)**.

   * **Inloggningssida** - Den sida som ska användas för inloggning

* **Exportera**

   * **Exportkonfiguration** - Anger en exportkonfiguration

* **SEO**

   * **Kanonisk URL** - kan användas för att skriva över sidans kanoniska URL; om den lämnas tom är sidans URL dess kanoniska URL

   * **Robots-taggar** - välj robottaggarna för att styra beteendet för crawler för sökmotorer.

     >[!NOTE]
     >
     >Vissa av alternativen står i konflikt med varandra. Om en konflikt uppstår har det mer tillåtna alternativet företräde.

   * **Generera platskarta** - När du väljer det här alternativet genereras en sitemap.xml för den här sidan och dess underordnade

### Bilder {#images}

* **Aktuell bild**

  Markera och konfigurera den bild som ska visas. Detta används i komponenter som refererar till sidan, t.ex. scenbilder, sidlistor och så vidare.

   * **Bild**

     Du kan **välja** en resurs eller bläddra efter en fil som ska överföras och sedan **redigera** eller **rensa**.

   * **Alternativ text** - en text som används för att representera innebörden och/eller funktionen i bilden, till exempel för skärmläsare.

   * **Ärv - värde som tagits från DAM-resursen** - om det är markerat fylls den alternativa texten i med värdet för `dc:description`metadata i DAM

* **Miniatyrbild**

  Konfigurera sidminiatyrbilden

   * **Generera förhandsgranskning** - Generera en förhandsvisning av sidan som ska användas som miniatyrbild
   * **Överför bild** - Överför en bild som ska användas som miniatyrbild
   * **Välj bild** - Välj en befintlig resurs som du vill använda som miniatyrbild
   * **Återställ** - Det här alternativet blir tillgängligt när du har ändrat miniatyrbilden. Om du inte vill behålla ändringen kan du återställa den innan du sparar.

### Molntjänster {#cloud-services}

* **Cloud Service-konfigurationer** - Definiera egenskaper för molntjänster

### Personalization {#personalization}

* **ContextHub-konfigurationer**

   * **Ärvd från &lt;path>** - aktivera/inaktivera arv; växlar tillgänglighet för **ContextHub-bana** och **Segmentsökväg** för markering

   * **ContextHub-sökväg** - Definiera [ContextHub-konfigurationen](/help/sites-cloud/authoring/personalization/contexthub.md)
   * **Segmentsökväg** - Definiera [segmentbanan](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)

* **Målkonfiguration**

   * **Varumärke** - Definierar ett [varumärke som anger ett omfång för målgruppsanpassning](/help/sites-cloud/authoring/personalization/targeted-content.md).

  >[!NOTE]
  >Det här alternativet kräver att användarkontot finns i gruppen `Target Administrators`.

### Behörigheter {#permissions}

* **Behörigheter**

   * **Lägg till behörigheter**
   * **Redigera stängd användargrupp**
   * Visa **gällande behörigheter**

### Blueprint {#blueprint}

Den här fliken visas bara för sidor som fungerar som utkast. Utkast fungerar som bas för Live-kopior och ingår i [Multi Site Management](/help/sites-cloud/administering/msm/overview.md).

* **Aktuella live-kopior** - Visar en lista över sidor som är baserade på (d.v.s. live-kopior av) den här designsidan

* **Utrullningskonfigurationer** - Styr under vilka omständigheter ändringar ska spridas till Live Copy

### Live Copy {#live-copy}

Den här fliken visas bara för sidor som har konfigurerats som live-kopior. Precis som med utkast är Live-kopior en del av [Multi Site Management](/help/sites-cloud/administering/msm/overview.md).

* **Synkronisera** - Synkronisera Live-kopia med utkast, med lokala ändringar
* **Återställ** - Återställ Live-kopia till läget för utkast och ta bort lokala ändringar
* **Gör uppehåll** - Gör uppehåll i Live Copy vid ytterligare rolloutändringar
* **Koppla loss** - Frigör Live-kopia från utkast

* **Source**

   * Visar sökvägen till ritningen för den här Live-kopian

* **Status**

   * Visar sidans aktuella Live Copy-status

* **Konfiguration**

   * **Live Copy-arv** - Om det här alternativet är markerat gäller Live Copy-konfigurationen alla underordnade objekt
   * **Ärv utrullningskonfigurationer från överordnad** - Om det här alternativet är markerat ärvs utrullningskonfigurationen från sidans överordnade objekt
   * **Välj utrullningskonfiguration** - Definierar under vilka omständigheter ändringar sprids från utskriften och bara är tillgängliga när **Ärv utrullningskonfigurationer från överordnad** inte har valts

### Förhandsgranska {#preview}

När en förhandsvisningsmiljö är aktiverad ser du följande:

* URL för förhandsgranskning - den URL som används för att komma åt innehållet i förhandsvisningsmiljön

### Progressiv webbapp {#progressive-web-app}

Genom en enkel konfiguration kan en innehållsförfattare nu aktivera funktioner för progressiva webbprogram (PWA) för upplevelser som skapats i AEM Sites.

>[!NOTE]
>
>Mer information finns i [Aktivera progressiva webbprogramfunktioner](/help/sites-cloud/authoring/sites-console/enable-pwa.md).

{{pwa-deprecation}}

* **Konfigurera installerbar upplevelse**

   * **Aktivera PWA** - aktivera/inaktivera funktionen; tillåter användare att installera webbplatsen som en PWA
   * **StartupURL** - den rekommenderade startadressen
   * **Visningsläge** - hur webbläsaren ska döljas eller på annat sätt visas för användaren på den lokala enheten
   * **Skärmorientering** - hur PWA hanterar enhetsorienteringar
   * **Temafärg** - färgen på appen som påverkar hur den lokala användarens operativsystem visar det inbyggda verktygsfältet och navigeringskontrollerna
   * **Bakgrundsfärg** - appens bakgrundsfärg, som visas när appen läses in
   * **Ikon** - ikonen som representerar appen på användarens enhet

* **Cachehantering (avancerat)**

   * **Cachningsstrategi och frekvens för innehållsuppdatering** - definierar cachelagringsmodellen för din PWA
   * **Filer att cachelagra för offlineanvändning**
      * **Filförcachelagring (teknisk förhandsgranskning)** - filer som lagras på AEM sparas i den lokala webbläsarcachen när tjänstarbetaren installeras och innan den används
      * **Bibliotek på klientsidan** - bibliotek på klientsidan som ska cachelagras för offlineupplevelse
      * **Sökvägsinkluderingar** - nätverksförfrågningar för de definierade sökvägarna fångas upp och cachelagrat innehåll returneras i enlighet med den konfigurerade cachelagringsstrategin och frekvensen för innehållsuppdatering
      * **Sökvägsundantag** - dessa filer kommer aldrig att cachelagras oavsett inställningarna under Filförcachelagring och Sökvägsinkludering

## Redigera sidegenskaper {#editing-page-properties-1}

* Från konsolen **Platser**:
   * [Skapar en ny sida](/help/sites-cloud/authoring/sites-console/creating-pages.md#creating-a-new-page) (en deluppsättning av egenskaperna)
   * Klicka eller peka på **Egenskaper**
      * För en enstaka sida
      * För flera sidor (endast en deluppsättning av egenskaperna är tillgängliga för redigering av en masse)
* Från sidredigeraren:
   * Med **Sidinformation** (och sedan **Öppna egenskaper**)

### Från webbplatskonsolen - en sida {#from-the-sites-console-single-page}

Klicka eller tryck på **Egenskaper** för att definiera sidegenskaperna:

1. Använd konsolen **Platser** för att navigera till platsen för sidan som du vill visa och redigera egenskaper för.
1. Välj alternativet **Egenskaper** för den begärda sidan med något av följande alternativ:
   * [Snabbåtgärder](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [Markeringsläge](/help/sites-cloud/authoring/basic-handling.md#selecting-resources)
   * Sidegenskaperna visas med rätt flikar.
1. Visa eller redigera egenskaperna efter behov.
1. Använd sedan **Spara** för att spara uppdateringar följt av **Stäng** för att återgå till konsolen.

### När en sida redigeras {#when-editing-a-page}

När du redigerar en sida kan du använda **Sidinformation** för att definiera sidegenskaperna:

1. Öppna sidan som du vill redigera egenskaper för.
1. Välj ikonen **Sidinformation** för att öppna markeringsmenyn:
1. Välj **Öppna egenskaper** så öppnas en dialogruta där du kan redigera egenskaperna, sorterade efter lämplig flik. Följande knappar finns också till höger om verktygsfältet:
   * **Avbryt**
   * **Spara och stäng**
1. Använd knappen **Spara och stäng** för att spara ändringarna.

### Från webbplatskonsolen - flera sidor {#from-the-sites-console-multiple-pages}

På **Sites**-konsolen kan du markera flera sidor och sedan använda **Visa egenskaper** för att visa och/eller redigera sidegenskaperna. Detta kallas massredigering av sidegenskaper.

Du kan välja flera sidor för massredigering på olika sätt, bland annat:

* När du bläddrar i konsolen **Platser**
* När du har använt **Sök** för att hitta en uppsättning sidor

När du har markerat sidorna och sedan klickat eller tryckt på alternativet **Egenskaper** visas bulkegenskaperna:

![Redigera sidegenskaper gruppvis](/help/sites-cloud/authoring/assets/page-properties-bulk-edit.png)

Du kan bara redigera sidor som:

* Dela samma resurstyp
* Är inte en del av en livecopy
   * Om någon av sidorna finns i en live-kopia visas ett meddelande när egenskaperna öppnas.

När du har valt Massredigering kan du:

* **Visa**

   * En lista över de sidor som påverkas
      * Du kan markera/avmarkera vid behov
      * Tabbar
         * På samma sätt som när du visar egenskaper för en enskild sida ordnas egenskaperna under flikar.
   * En deluppsättning med egenskaper
      * Egenskaper som är tillgängliga på alla markerade sidor och som uttryckligen har definierats som tillgängliga för massredigering visas.
      * Om du minskar sidmarkeringen till en sida visas alla egenskaper.
   * Vanliga egenskaper med ett gemensamt värde
      * Endast egenskaper med ett gemensamt värde visas i visningsläget.
      * När fältet har flera värden (till exempel Taggar) visas värden bara när *all* är gemensamma. Om bara vissa är vanliga visas de bara när du redigerar.
      * När det inte finns några egenskaper med ett gemensamt värde visas ett meddelande.

* **Redigera**

   * Du kan uppdatera värdena i de tillgängliga fälten.
      * De nya värdena tillämpas på alla markerade sidor när du väljer **Klar**.
      * När fältet har flera värden (till exempel Taggar) kan du antingen lägga till ett nytt värde eller ta bort ett gemensamt värde.
   * Fält som är vanliga, men har olika värden på de olika sidorna, anges med ett särskilt värde som texten `<Mixed Entries>`.

## Egenskapsarv {#inheritance}

Om sidan baseras på en plan eller på annat sätt ärver innehåll från en annan sida, återspeglas arv i fönstret **Sidegenskaper** för det enskilda fältet.

![Ärvda egenskaper](assets/property-inhertiance.png)

Ärvda egenskaper kan inte redigeras. Tryck eller klicka på ikonen **Avbryt arv** bredvid ett visst fält för att bryta dess arv.

![Avbryt arv](assets/cancel-inheritance.png)

Bekräfta annulleringen i **Avbryt arv** modal.

![Avbryt spärrkontroll av arv](assets/cancel-inheriance-confirmation.png)

När arvet avbryts för ett fält kan det redigeras.

![Avbrutet arv](assets/property-inheritance-broken.png)

Om du vill återställa arvet trycker eller klickar du på ikonen **Återställ arv** bredvid fältet.

![Återgå arv](assets/revert-inheritance.png)

Bekräfta återgivningen i **återställ arv** modal.

![Återgå spärrad arvsbekräftelse modal](assets/revert-inhertiance-confirmation.png)

Välj **Synkronisera sida efter återgång av arv** om du vill uppdatera fältet med de senaste värdena i planen. Om du inte gör det uppdateras värdena nästa gång LiveCopy synkroniseras.

>[!TIP]
>
>Mer information om arv finns i dokumentet [Multi Site Manager och Translation](/help/sites-cloud/administering/msm-and-translation.md)
