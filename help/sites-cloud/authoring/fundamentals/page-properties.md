---
title: Redigera sidegenskaper
description: Definiera de egenskaper som krävs för en sida
exl-id: 27521a6d-c6e9-4f43-9ddf-9165b0316084
source-git-commit: 628a95d7b7d0e84bfc8edecaaf127dd83ce1e578
workflow-type: tm+mt
source-wordcount: '2428'
ht-degree: 4%

---

# Redigera sidegenskaper {#editing-page-properties}

Du kan definiera de egenskaper som krävs för en sida. Dessa kan variera beroende på sidans beskaffenhet. Vissa sidor kan till exempel vara kopplade till en live-kopia medan andra inte är det och live-kopieringsinformationen är tillgänglig efter behov.

## Sidegenskaper {#page-properties}

Egenskaperna fördelas på flera flikar.

### Grundläggande {#basic}

* **Titel och taggar**

   * **Titel** - Sidans rubrik visas på olika platser. Till exempel **Webbplatser** tabblista och **Webbplatser** kort-/listvyer.
      * Detta är ett obligatoriskt fält.
   * **Taggar** - Här kan du lägga till eller ta bort taggar från sidan genom att uppdatera listan i valrutan.
      * När du har valt en tagg visas den under markeringsrutan. Du kan ta bort en tagg från den här listan med hjälp av x.
      * Du kan ange en helt ny tagg genom att skriva namnet i en tom markeringsruta.
         * Den nya taggen skapas när du trycker på Retur.
         * Den nya taggen visas sedan med en liten stjärna till höger som anger att det är en ny tagg.
      * Med den nedrullningsbara menyn kan du välja bland befintliga taggar.
      * Ett x-tecken visas när du för musen över en taggpost i markeringsrutan, som kan användas för att ta bort taggen för den här sidan.
      * Mer information om taggar finns i [Använda taggar](/help/sites-cloud/authoring/features/tags.md).
   * **Dölj i navigering** - Anger om sidan visas eller döljs i sidnavigeringen på den slutliga platsen.

* **Varumärke**

   Använd en enhetlig varumärkesidentitet på alla sidor genom att lägga till en instruktionsmarginal till varje sidrubrik. Den här funktionen kräver att du använder Page Component från version 2.14.0 eller senare av [Kärnkomponenter.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)

   * **Varumärkesinstruktionsmarginal**

      * **Åsidosätt** - Markera för att definiera instruktionsmarginalen för varumärket på den här sidan.
         * Värdet ärvs av alla underordnade sidor såvida de inte också har sina **Åsidosätt** värden anges.
      * **Åsidosätt värde** - Texten i instruktionsmarginalen som ska läggas till i sidrubriken.
         * Värdet läggs till i sidrubriken efter ett lodstreck som &quot;Cycling Tuscany&quot; | Alltid redo för WKND&quot;

* **HTML ID**

   * **ID** - HTML-ID som ska användas för komponenten.

* **Fler rubriker och beskrivning**

   * **Sidrubrik** - En rubrik som ska användas på sidan. Används vanligtvis av titelkomponenter. Om den är tom **Titel** kommer att användas.
   * **Navigeringsrubrik** - Du kan ange en separat rubrik som ska användas i navigeringen (t.ex. om du vill ha något mer koncist). Om den är tom visas **Titel** kommer att användas.
   * **Underrubrik** - En underrubrik som ska användas på sidan.
   * **Beskrivning** - Din beskrivning av sidan, dess syfte eller annan information som du vill lägga till.

* **På/av-tid**

   >[!NOTE]
   >
   > Se [På- och avaktiveringstider - utlösarkonfiguration](/help/operations/replication.md#on-and-off-times-trigger-configuration) om du vill ha mer information om hur du konfigurerar den relaterade automatiska replikeringen.

   >[!NOTE]
   >Om någon av **I tid** eller **Fråntid** är tidigare och automatisk replikering har konfigurerats, kommer den relevanta åtgärden att utlösas omedelbart.

   * **I tid** - Det datum och den tidpunkt då den publicerade sidan ska synas (återges) i publiceringsmiljön. Sidan måste publiceras, antingen manuellt eller med förkonfigurerad automatisk replikering.

      * Om redan [publicerad (manuellt)](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) den här sidan behålls vilande (dold) tills den återges vid den angivna tidpunkten.
      * Om sidan inte publiceras och konfigureras för automatisk replikering kommer den att publiceras automatiskt och sedan återges vid den angivna tidpunkten.
      * Om sidan inte publiceras och inte är konfigurerad för automatisk replikering kommer den inte att publiceras automatiskt. Därför visas 404 när du försöker komma åt sidan.
   * **Fråntid** - Liknar och används ofta i kombination med **I tid** definierar detta den tidpunkt då den publicerade sidan döljs i publiceringsmiljön.

   * Lämna dessa fält (**I tid** och **Fråntid**) är tom för sidor som du vill publicera omedelbart och som finns tillgängliga i publiceringsmiljön tills de har inaktiverats (standardscenariot).


* **Vanity URL**

   * Gör att du kan ange en egen URL för den här sidan, vilket kan göra att du kan ha en kortare och/eller mer uttrycksfull URL.
   * Om Vanity-URL:en till exempel är inställd på `welcome` till sidan som identifieras av sökvägen `/v1.0/startpage` för webbplatsen `http://example.com`sedan `http://example.com/welcome` skulle vara den vanligaste URL:en för `http://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >Alternativa URL:er:
   >
   >* Måste vara unikt så du bör vara försiktig med att värdet inte redan används av en annan sida.
   >* Använd inte regex-mönster.
   >* Ska inte anges till en befintlig sida.


   * **Lägg till** - Tryck eller klicka för att visa ett fält för att definiera en fågel-URL för sidan.
      * Tryck eller klicka igen för att lägga till flera.
      * Tryck eller klicka på **Ta bort** -ikonen för att ta bort fågel-URL:en.
   * **URL för omdirigering** - Anger om du vill att sidan ska använda fågel-URL:en.


### Avancerat {#advanced}

* **Inställningar**

   * **Språk** - Sidspråket
   * **Språkrot** - Måste kontrolleras om sidan är roten i en språkkopia
   * **Omdirigering** - Anger den sida som den här sidan automatiskt ska omdirigeras till med HTML `302 Found` status.
      * **Permanent omdirigering** - När det här alternativet är markerat dirigeras sidan om till målsökvägen som medföljer HTML `301 Moved Permanently` status.
   * **Design** - Anger om sidan visas eller döljs i sidnavigeringen på den slutliga webbplatsen
   * **Alias** - Anger ett alias som ska användas med den här sidan
      * Om du till exempel definierar ett alias för `private` för sidan `/content/wknd/us/en/magazine/members-only`kan den här sidan också öppnas via `/content/wknd/us/en/magazine/private`
      * När du skapar ett alias anges `sling:alias` på sidnoden, vilket bara påverkar resursen, inte databassökvägen.
      * Sidor som används av alias i redigeraren kan inte publiceras. [Publiceringsalternativ](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) i redigeraren är bara tillgängliga för sidor som du kommer åt via de faktiska sökvägarna.
      * Mer information finns i [Lokaliserade sidnamn under SEO och URL Management Best Practices](/help/overview/seo-and-url-management.md#localized-page-names).

* **Konfiguration**

   * **Ärvs från &lt;path>** - aktivera/inaktivera arv, växlar tillgänglighet för **Molnkonfiguration** för markering

   * **Molnkonfiguration** - Sökvägen till den valda konfigurationen

* **Mallinställningar**

   * **Tillåtna mallar** - [Definierar listan med mallar som ska vara tillgängliga](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author) inom denna underavdelning

* **Autentiseringskrav**

   * **Aktivera** - Aktivera användning av autentisering för att komma åt sidan

      >[!NOTE]
      >
      >Stängda användargrupper för sidan definieras på **[Behörigheter](#permissions)** -fliken.

   * **Inloggningssida** - Den sida som ska användas för inloggning

* **Exportera**

   * **Exportera konfiguration** - Anger en exportkonfiguration

* **SEO**

   * **Kanonisk URL** - kan användas för att skriva över sidans kanoniska URL, om den lämnas tom blir sidans URL dess kanoniska URL

   * **Robots-taggar** - välj robottaggarna för att styra beteendet för sökmotorcrawler.

      >[!NOTE]
      >
      >Vissa av alternativen står i konflikt med varandra. Om en konflikt uppstår har det mer tillåtna alternativet företräde.

   * **Generera platskarta** - När du väljer det här alternativet genereras en sitemap.xml för den här sidan och dess underordnade

### Bilder {#images}

* **Aktuell bild**

   Markera och konfigurera den bild som ska visas. Detta används i komponenter som refererar till sidan; till exempel teasers, page lists, etc.

   * **Bild**

      Du kan **Välj** en resurs, eller bläddra efter en fil som ska överföras, och sedan **Redigera**, eller **Rensa**.

   * **Alternativ text** - en text som används för att representera bildens betydelse och/eller funktion, till exempel för skärmläsare.

   * **Ärv - värde som tagits från DAM-resursen** - om det här alternativet är markerat fylls den alternativa texten i med värdet för `dc:description`metadata i DAM

* **Miniatyrbild**

   Konfigurera sidminiatyrbilden

   * **Generera förhandsgranskning** - Generera en förhandsgranskning av sidan som ska användas som miniatyrbild
   * **Överför bild** - Överför en bild som ska användas som miniatyrbild
   * **Välj bild** - Välj en befintlig resurs som ska användas som miniatyrbild
   * **Återställ** - Det här alternativet blir tillgängligt när du har ändrat miniatyrbilden. Om du inte vill behålla ändringen kan du återställa den innan du sparar.

### Sociala medier {#social-media}

* **Delning i sociala medier**

   Definierar de delningsalternativ som är tillgängliga på sidan. Visar de alternativ som är tillgängliga för [Dela kärnkomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/sharing.html).

   * **Aktivera användardelning för Facebook**
   * **Aktivera användardelning för Pinterest**
   * **Önskad XF-variation**
      * Definiera variant av upplevelsefragment som används för att generera metadata för sidan

### Cloud Services {#cloud-services}

* **Cloud Service Configurations** - Definiera egenskaper för molntjänster

### Personanpassning {#personalization}

* **ContextHub-konfigurationer**

   * **Ärvs från &lt;path>** - aktivera/inaktivera arv, växlar tillgänglighet för **ContextHub-bana** och **Segmentsökväg** för markering

   * **ContextHub-sökväg** - Definiera [ContextHub-konfiguration](/help/sites-cloud/authoring/personalization/contexthub.md)
   * **Segmentsökväg** - Definiera [Segmentbana](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)

* **Målkonfiguration**

   * **Varumärke** - Definierar en [Varumärke som anger ett omfång för målanpassning](/help/sites-cloud/authoring/personalization/targeted-content.md).
   >[!NOTE]
   >Det här alternativet kräver att användarkontot finns i `Target Administrators`grupp.

### Behörigheter {#permissions}

* **Behörigheter**

   * **Lägg till behörigheter**
   * **Redigera stängd användargrupp**
   * Visa **Effektiva behörigheter**

### Blueprint {#blueprint}

Den här fliken visas bara för sidor som fungerar som utkast. Kort text utgör grunden för Live-kopior som ingår i [Hantering av flera webbplatser.](/help/sites-cloud/administering/msm/overview.md)

* **Aktuella Live-kopior** - Visar en lista över sidor som är baserade (d.v.s. live-kopior av) på den här översiktssidan

* **Utrullningskonfigurationer** - Styr under vilka omständigheter ändringar ska spridas till Live Copy

### Live Copy {#live-copy}

Den här fliken visas bara för sidor som har konfigurerats som live-kopior.

* **Synkronisera** - Synkronisera Live Copy med utkast, med lokala ändringar
* **Återställ** - Återställ live-kopia till blå text och ta bort lokala ändringar
* **Gör uppehåll** - Skjut upp Live Copy från ytterligare ändringar
* **Koppla loss** - Frigör Live Copy från utkast

* **Källa**

   * Visar sökvägen till ritningen för den här Live-kopian

* **Status**

   * Visar sidans aktuella Live Copy-status

* **Konfiguration**

   * **Live Copy-arv** - Om det här alternativet är markerat gäller konfigurationen för Live Copy för alla underordnade
   * **Ärv utrullningskonfigurationer från överordnad** - Om det här alternativet är markerat ärvs utrullningskonfigurationen från sidans överordnade objekt
   * **Välj utrullningskonfiguration** - Definierar under vilka omständigheter ändringar ska spridas från utkast och endast vara tillgängliga när **Ärv utrullningskonfigurationer från överordnad** är inte markerad

### Förhandsgranska {#preview}

När en förhandsvisningsmiljö är aktiverad ser du:

* URL för förhandsgranskning - den URL som används för att komma åt innehållet i förhandsvisningsmiljön

### Progressiv webbapp {#progressive-web-app}

Genom en enkel konfiguration kan en innehållsförfattare nu aktivera progressiva webbprogramfunktioner (PWA) för upplevelser som skapats i AEM Sites.

>[!NOTE]
>
>Mer information finns i [Aktivera progressiva webbprogramfunktioner](/help/sites-cloud/authoring/features/enable-pwa.md).

* **Konfigurera installerbar upplevelse**

   * **Aktivera PWA** - aktivera/inaktivera funktionen, tillåter användare att installera webbplatsen som PWA
   * **StartURL** - önskad start-URL
   * **Visningsläge** - hur webbläsaren ska döljas eller på annat sätt visas för användaren på den lokala enheten
   * **Skärmorientering** - hur PWA ska hantera enhetsorienteringar
   * **Temafärg** - färgen på appen som påverkar hur den lokala användarens operativsystem visar det inbyggda verktygsfältet och navigeringskontrollerna
   * **Bakgrundsfärg** - appens bakgrundsfärg, som visas när appen läses in
   * **Ikon** - ikonen som representerar appen på användarens enhet

* **Cachehantering (avancerat)**

   * **Cachelagringsstrategi och uppdateringsfrekvens för innehåll** - definierar cachningsmodellen för PWA
   * **Filer som ska cachas för offlineanvändning**
      * **Filförcachelagring (teknisk förhandsgranskning)** - filer som lagras på AEM sparas i den lokala webbläsarcachen när servicearbetaren installeras och innan den används
      * **Bibliotek på klientsidan** - bibliotek på klientsidan för att cachelagra offlineupplevelsen
      * **Inkluderingar av banor** - nätverksbegäranden för de definierade sökvägarna fångas upp och cachelagrat innehåll returneras i enlighet med den konfigurerade cachelagringsstrategin och frekvensen för innehållsuppdatering
      * **Undantag för sökväg** - dessa filer kommer aldrig att cachelagras oavsett inställningarna under Filförcachelagring och Sökvägsinkluderingar

## Redigera sidegenskaper {#editing-page-properties-1}

* Från **Webbplatser** konsol:
   * [Skapa en ny sida](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) (en delmängd av egenskaperna)
   * Klicka eller peka **Egenskaper**
      * För en enstaka sida
      * För flera sidor (endast en deluppsättning av egenskaperna är tillgängliga för redigering av en masse)
* Från sidredigeraren:
   * Med **Sidinformation** (och sedan **Öppna egenskaper**)

### Från webbplatskonsolen - en sida {#from-the-sites-console-single-page}

Klicka eller peka **Egenskaper** för att definiera sidegenskaperna:

1. Använda **Webbplatser** navigera till platsen för sidan som du vill visa och redigera egenskaper för.
1. Välj **Egenskaper** för den önskade sidan med något av följande alternativ:
   * [Snabbåtgärder](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Markeringsläge](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)
   * Sidegenskaperna visas med rätt flikar.
1. Visa eller redigera egenskaperna efter behov.
1. Använd sedan **Spara** för att spara uppdateringar följt av **Stäng** för att återgå till konsolen.

### När en sida redigeras {#when-editing-a-page}

När du redigerar en sida kan du använda **Sidinformation** för att definiera sidegenskaperna:

1. Öppna sidan som du vill redigera egenskaper för.
1. Välj **Sidinformation** -ikon för att öppna markeringsmenyn:
1. Välj **Öppna egenskaper** så öppnas en dialogruta där du kan redigera egenskaperna. Följande knappar finns också till höger om verktygsfältet:
   * **Avbryt**
   * **Spara och stäng**
1. Använd **Spara och stäng** för att spara ändringarna.

### Från webbplatskonsolen - flera sidor {#from-the-sites-console-multiple-pages}

På **Sites**-konsolen kan du markera flera sidor och sedan använda **Visa egenskaper** för att visa och/eller redigera sidegenskaperna. Detta kallas massredigering av sidegenskaper.

>[!NOTE]
>
>Det finns även massredigering av egenskaper för Assets. Den är mycket lik, men skiljer sig på några punkter. Mer information finns i Redigera egenskaper för flera resurser.
>
>Här finns också en gruppredigerare där du kan söka efter innehåll från flera sidor med GQL (Google Query Language) och sedan redigera innehållet direkt i gruppredigeraren innan du sparar ändringarna på originalsidorna.

<!--
>Bulk editing of properties is also available for Assets. It is very similar, but differs in a few points. See [Editing Properties of Multiple Assets](/help/assets/managing-multiple-assets.md) for details.
>
>There is also the [Bulk Editor](/help/sites-administering/bulk-editor.md), which allows you to search for content from multiple pages using GQL (Google Query Language) and then edit the content directly in the bulk editor before saving your changes to the originating pages.
-->

Du kan välja flera sidor för massredigering på olika sätt, bland annat:

* När du bläddrar **Webbplatser** konsol
* Efter användning **Sök** för att hitta en uppsättning sidor

När du har markerat sidorna och tryckt eller klickat på alternativet **Egenskaper**, visas massegenskaperna:

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
      * När fältet har flera värden (till exempel Taggar) visas värden endast när *alla* är vanliga. Om bara vissa är vanliga visas de bara när du redigerar.
      * När det inte finns några egenskaper med ett gemensamt värde visas ett meddelande.

* **Redigera**

   * Du kan uppdatera värdena i de tillgängliga fälten.
      * De nya värdena tillämpas på alla markerade sidor när du markerar **Klar**.
      * När fältet har flera värden (till exempel Taggar) kan du antingen lägga till ett nytt värde eller ta bort ett gemensamt värde.
   * Fält som är gemensamma, men har olika värden på de olika sidorna, markeras med ett särskilt värde, t.ex. texten `<Mixed Entries>`.

>[!NOTE]
>
>Sidkomponenten kan konfigureras för att ange de fält som är tillgängliga för massredigering. Se Konfigurera sidan för massredigering av sidegenskaper.

<!--
>The page component can be configured to specify the fields available for bulk editing. See [Configuring your page for bulk editing of page properties](/help/sites-developing/bulk-editing.md).
-->
