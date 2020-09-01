---
title: Redigera sidegenskaper
description: Definiera de egenskaper som krävs för en sida
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '1687'
ht-degree: 6%

---


# Redigera sidegenskaper {#editing-page-properties}

Du kan definiera de egenskaper som krävs för en sida. Dessa kan variera beroende på sidans beskaffenhet. Vissa sidor kan till exempel vara kopplade till en live-kopia medan andra inte är det och live-kopieringsinformationen är tillgänglig efter behov.

## Sidegenskaper {#page-properties}

Egenskaperna fördelas på flera flikar.

### Grundläggande {#basic}

* **Titel**

   * Sidans rubrik visas på olika platser. Till exempel fliklistan **Webbplatser** och vyerna **Webbplatser** .
   * Detta är ett obligatoriskt fält.

* **Taggar**

   * Här kan du lägga till eller ta bort taggar från sidan genom att uppdatera listan i markeringsrutan.
   * När du har valt en tagg visas den under markeringsrutan. Du kan ta bort en tagg från den här listan med hjälp av x.
   * Du kan ange en helt ny tagg genom att skriva namnet i en tom markeringsruta.
      * Den nya taggen skapas när du trycker på Retur.
      * Den nya taggen visas sedan med en liten stjärna till höger som anger att det är en ny tagg.
   * Med den nedrullningsbara menyn kan du välja bland befintliga taggar.
   * Ett x-tecken visas när du för musen över en taggpost i markeringsrutan, som kan användas för att ta bort taggen för den här sidan.
   * Mer information om taggar finns i [Använda taggar](/help/sites-cloud/authoring/features/tags.md).

* **Dölj i navigering**

   * Anger om sidan visas eller döljs i sidnavigeringen på den slutliga platsen.

* **HTML-ID**

   * HTML-id som ska användas för komponenten.

* **Sidrubrik**

   * En rubrik som ska användas på sidan. Används vanligtvis av titelkomponenter. Om den är tom används **rubriken** .

* **Navigeringsrubrik**

   * Du kan ange en separat rubrik som ska användas i navigeringen (om du till exempel vill ha något mer koncist). Om den är tom används **rubriken** .

* **Underrubrik**

   * En underrubrik som ska användas på sidan.

* **Beskrivning**

   * Din beskrivning av sidan, dess syfte eller annan information som du vill lägga till.

* **I tid**

   * Det datum och den tidpunkt då den publicerade sidan blir synlig (återgiven) i publiceringsmiljön. Sidan måste publiceras, antingen manuellt eller med förkonfigurerad automatisk replikering.

      >[!NOTE]
      >
      > Information om hur du konfigurerar den relaterade automatiska replikeringen finns i [På- och Av-tider - Utlösarkonfiguration](/help/operations/replication.md#on-and-off-times-trigger-configuration) .

      * Om sidan redan är [publicerad (manuellt)](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) kommer den att vara vilande (dold) tills den återges vid den angivna tidpunkten.
      * Om sidan inte publiceras och konfigureras för automatisk replikering kommer den att publiceras automatiskt och sedan återges vid den angivna tidpunkten.
      * Om sidan inte publiceras och inte är konfigurerad för automatisk replikering, kommer den inte att publiceras automatiskt. Därför visas 404 när du försöker komma åt sidan.
   * Lämna dessa fält (**I tid** och **fråntid**) tomma för sidor som du vill publicera omedelbart och som är tillgängliga i publiceringsmiljön tills de inaktiveras (standardscenario).

* **Fråntid**

   * Parallellt med **På tid** anger detta den tidpunkt då den publicerade sidan döljs i publiceringsmiljön.
   * Lämna dessa fält (**I tid** och **fråntid**) tomma för sidor som du vill publicera omedelbart och som är tillgängliga i publiceringsmiljön tills de inaktiveras (standardscenario).

* **Vanity URL**

   * Gör att du kan ange en fågel-URL för den här sidan, vilket kan ge dig en kortare och/eller mer uttrycksfull URL.
   * Om Vanity-URL:en till exempel är inställd på `welcome` den sida som identifieras av sökvägen `/v1.0/startpage` för webbplatsen `http://example.com`är `http://example.com/welcome` det vanity-URL:en för `http://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >Alternativa URL:er:
   >
   >* Måste vara unikt så du bör vara försiktig med att värdet inte redan används av en annan sida.
   >* Använd inte regex-mönster.
   >* Ska inte anges till en befintlig sida.


* **URL för omdirigering**

   * Anger om du vill att sidan ska använda fågel-URL:en.

### Avancerat {#advanced}

* **Språk:**

   * Sidspråket.

* **Språkrot**

   * Måste kontrolleras om sidan är roten i en språkkopia.

* **Omdirigering**

   * Ange den sida som den här sidan automatiskt ska omdirigeras till.

* **Design**

   * Anger om sidan visas eller döljs i sidnavigeringen på den slutliga platsen.

* **Alias**

   * Ange ett alias som ska användas med den här sidan.
   >[!NOTE]
   >
   >Alias anger egenskapen för att definiera ett aliasnamn för resursen (detta påverkar bara resursen, inte sökvägen). `sling:alias`
   >
   >Till exempel: om du definierar ett alias för `latin-lang` noden `/content/we-retail/spanish` kan du komma åt den här sidan via `/content/we-retail/latin-language`
   >
   >Mer information finns i Lokaliserade sidnamn under SEO och Bästa metoder för URL-hantering.

   <!--
  >For further details see [Localized page names under SEO and URL Management Best Practices](/help/managing/seo-and-url-management.md#localized-page-names).
  -->

* **Ärvs från &lt;path>**

   * Anger om sidan ärvs. och varifrån kommer.

* **Molnkonfiguration**

   * Sökvägen till konfigurationen.

* **Tillåtna mallar**

   * [Definiera listan med mallar som ska vara tillgängliga](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author) i den här undergrenen.

* **Aktivera** (autentiseringskrav)

   * Aktivera (eller inaktivera) autentisering för att få åtkomst till sidan.
   >[!NOTE]
   >
   >Stängda användargrupper för sidan definieras på fliken **[Behörigheter](#permissions)** .

* **Inloggningssida**

   * Den sida som ska användas för inloggning.

* **Exportera konfiguration**

   * Ange en exportkonfiguration.

### Miniatyrbild {#thumbnail}

Visar sidminiatyrbilden. Du kan:

* **Generera förhandsgranskning**

   * Generera en förhandsgranskning av sidan som ska användas som miniatyrbild.

* **Överför bild**

   * Överför en bild som ska användas som miniatyrbild.

* **Välj bild**

   * Välj en befintlig resurs som du vill använda som miniatyrbild.

* **Återställ**

   * Det här alternativet blir tillgängligt när du har ändrat miniatyrbilden. Om du inte vill behålla ändringen kan du återställa den innan du sparar.

### Sociala medier {#social-media}

* **Delning i sociala medier**

   Definierar de delningsalternativ som är tillgängliga på sidan. Visar de alternativ som är tillgängliga för kärnkomponenten [](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/sharing.html)Delning.

   * **Aktivera användardelning för Facebook**
   * **Aktivera användardelning för Pinterest**
   * **Önskad XF-variation**
      * Definiera variant av upplevelsefragment som används för att generera metadata för sidan

### Cloud Services {#cloud-services}

* **Cloud Service Configurations**

   * Definiera egenskaper för molntjänster.

   <!--Define properties for [cloud services](/help/sites-developing/extending-cloud-config.md).
  -->

### Personanpassning {#personalization}

* **ContextHub-konfigurationer**

   * Välj ContextHub Configuration och Segments Path.

   <!--Select the [ContextHub Configuration](/help/sites-administering/contexthub-config.md) and [Segments Path](/help/sites-administering/segmentation.md).
  -->

* **Målkonfiguration**

   * Välj ett [varumärke för att ange ett omfång för målgruppsanpassning](/help/sites-cloud/authoring/personalization/targeted-content.md).
   >[!NOTE]
   >Det här alternativet kräver att användarkontot finns i `Target Adminstrators`gruppen.

### Behörigheter {#permissions}

* **Behörigheter**

   * Lägg till behörigheter
   * Redigera stängd användargrupp
   * Visa gällande behörigheter

   <!--[Add Permissions](/help/sites-administering/user-group-ac-admin.md) -->

   <!-- [Edit Closed User Group](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)-->

   <!-- View the [Effective Permissions](/help/sites-administering/user-group-ac-admin.md)-->

### Blueprint {#blueprint}

* **Blueprint**

   * Definiera egenskaper för en designsida inom hantering av flera webbplatser.

   <!--Define properties for a Blueprint page within [multi-site management](/help/sites-administering/msm.md).-->

   * Styr under vilka omständigheter ändringar ska spridas till Live Copy.


### Live Copy {#live-copy}

* **Livecopy**

   * Definiera egenskaper för en Live Copy-sida inom hantering av flera webbplatser. <!--Define properties for a Live Copy page within [multi-site management](/help/sites-administering/msm.md).-->
   * Styr under vilka omständigheter ändringar ska spridas från utkast.

### Webbplatsstruktur {#site-structure}

* Tillhandahåll länkar till sidor som innehåller funktioner för hela webbplatsen, till exempel **Registreringssida** och **Offlinesida**.

## Redigera sidegenskaper {#editing-page-properties-1}

* Från **webbplatskonsolen** :
   * [Skapa en ny sida](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) (en deluppsättning av egenskaperna)
   * Klicka eller peka på **Egenskaper**
      * För en enstaka sida
      * För flera sidor (endast en deluppsättning av egenskaperna är tillgängliga för redigering av en masse)
* Från sidredigeraren:
   * Med **Sidinformation** (och sedan **Öppna egenskaper**)

### Från webbplatskonsolen - en sida {#from-the-sites-console-single-page}

Klicka eller tryck på **Egenskaper** för att definiera sidegenskaperna:

1. Använd **webbplatskonsolen** för att navigera till platsen för sidan som du vill visa och redigera egenskaper för.
1. Välj alternativet **Egenskaper** för den önskade sidan med något av följande alternativ:
   * [Snabbåtgärder](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Markeringsläge](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)
   * Sidegenskaperna visas med rätt flikar.
1. Visa eller redigera egenskaperna efter behov.
1. Använd sedan **Spara** för att spara uppdateringarna följt av **Stäng** för att återgå till konsolen.

### När en sida redigeras {#when-editing-a-page}

När du redigerar en sida kan du använda **Sidinformation** för att definiera sidegenskaperna:

1. Öppna sidan som du vill redigera egenskaper för.
1. Välj ikonen **Sidinformation** för att öppna markeringsmenyn:
1. Välj **Öppna egenskaper** så öppnas en dialogruta där du kan redigera egenskaperna. Följande knappar finns också till höger om verktygsfältet:
   * **Avbryt**
   * **Spara och stäng**
1. Spara ändringarna med knappen **Spara och stäng** .

### Från webbplatskonsolen - flera sidor {#from-the-sites-console-multiple-pages}

På **Sites**-konsolen kan du markera flera sidor och sedan använda **Visa egenskaper** för att visa och/eller redigera sidegenskaperna. Detta kallas massredigering av sidegenskaper.

>[!NOTE]
>
>Det finns även massredigering av egenskaper för Assets. Den är mycket lik, men skiljer sig på några punkter. Mer information finns i Redigera egenskaper för flera resurser.
>
>Det finns också en gruppredigerare som du kan använda för att söka efter innehåll från flera sidor med GQL (Google Query Language) och sedan redigera innehållet direkt i gruppredigeraren innan du sparar ändringarna på originalsidorna.

<!--
>Bulk editing of properties is also available for Assets. It is very similar, but differs in a few points. See [Editing Properties of Multiple Assets](/help/assets/managing-multiple-assets.md) for details.
>
>There is also the [Bulk Editor](/help/sites-administering/bulk-editor.md), which allows you to search for content from multiple pages using GQL (Google Query Language) and then edit the content directly in the bulk editor before saving your changes to the originating pages.
-->

Du kan välja flera sidor för massredigering på olika sätt, bland annat:

* När du bläddrar i **webbplatskonsolen**
* När du har använt **Sök** för att hitta en uppsättning sidor

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
      * När fältet har flera värden (till exempel Taggar) visas värden bara när *alla* är gemensamma. Om bara vissa är vanliga visas de bara när du redigerar.
      * När det inte finns några egenskaper med ett gemensamt värde visas ett meddelande.

* **Redigera**

   * Du kan uppdatera värdena i de tillgängliga fälten.
      * De nya värdena tillämpas på alla markerade sidor när du väljer **Klar**.
      * När fältet har flera värden (till exempel Taggar) kan du antingen lägga till ett nytt värde eller ta bort ett gemensamt värde.
   * Fält som är gemensamma, men har olika värden på de olika sidorna, markeras med ett särskilt värde, t.ex. texten `<Mixed Entries>`. Du bör vara försiktig när du redigerar sådana fält för att förhindra dataförlust.

>[!NOTE]
>
>Sidkomponenten kan konfigureras för att ange de fält som är tillgängliga för massredigering. Se Konfigurera sidan för massredigering av sidegenskaper.

<!--
>The page component can be configured to specify the fields available for bulk editing. See [Configuring your page for bulk editing of page properties](/help/sites-developing/bulk-editing.md).
-->
