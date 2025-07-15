---
title: Skapa en plats
description: Lär dig hur du använder AEM för att skapa en webbplats med hjälp av webbplatsmallar för att definiera webbplatsens format och struktur.
feature: Administering
role: Admin
exl-id: 9c71c167-2934-4210-abd9-ab085b36593b
solution: Experience Manager Sites
source-git-commit: 4d45e7ef626ad0b46f5323263cca791b14f9732f
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---


# Skapa en plats {#creating-site}

Lär dig hur du använder AEM för att skapa en webbplats med hjälp av webbplatsmallar för att definiera webbplatsens format och struktur.

## Ökning {#overview}

Innan innehållsförfattare kan skapa sidor med innehåll måste webbplatsen först skapas. Detta utförs vanligtvis av en AEM-administratör som definierar platsens ursprungliga struktur. Med hjälp av webbplatsmallar kan du snabbt och flexibelt skapa webbplatser för icke-utvecklare.

## Struktur för planeringsplats {#structure}

Ta tid till att fundera över webbplatsens syfte och planerade innehåll långt i förväg. Detta styr hur du utformar webbplatsens struktur. En bra webbplatsstruktur har stöd för enkel navigering och innehållsidentifiering för webbplatsens besökare och har stöd för olika AEM-funktioner som [hantering av flera webbplatser och översättning.](/help/sites-cloud/administering/msm-and-translation.md)

## Webbplatsmallar {#site-templates}

Eftersom webbplatsstrukturen är så viktig för att en webbplats ska lyckas är det bekvämt att ha fördefinierade strukturer tillgängliga för att snabbt kunna driftsätta en ny webbplats baserat på en uppsättning befintliga standarder. Webbplatsmallar är ett sätt att kombinera grundläggande webbplatsinnehåll i ett bekvämt och återanvändbart paket.

Webbplatsmallar innehåller i allmänhet information om baswebbplatsinnehåll och struktur- och webbplatsformatering så att du snabbt kommer igång med den nya webbplatsen. Mallarna är kraftfulla eftersom de kan återanvändas och anpassas. Och eftersom du kan ha flera mallar tillgängliga i din AEM-installation kan du skapa olika webbplatser som passar olika affärsbehov.

>[!TIP]
>
>Mer information om webbplatsmallar finns i dokumentet [Webbplatsmallar.](site-templates.md)

>[!NOTE]
>
>Webbplatsmallen ska inte blandas ihop med [sidmallar.](/help/sites-cloud/authoring/page-editor/templates.md) Platsmallar definierar den övergripande strukturen för en plats. En sidmall definierar strukturen och det ursprungliga innehållet för en enskild sida.

### Webbplatsmallar från Adobe {#adobe-templates}

{{adobe-templates}}

## Skapa en plats {#create-site}

Det är enkelt att använda en mall för att skapa en plats.

1. Logga in i din AEM-redigeringsmiljö och navigera till webbplatskonsolen

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. Välj **Skapa** längst upp till höger på skärmen och välj **Plats från mall** på den nedrullningsbara menyn.

   ![Skapa en plats från en mall](../assets/create-site-from-template.png)

1. I guiden Skapa plats väljer du en befintlig mall på den vänstra panelen eller på **Importera** högst upp i den vänstra kolumnen om du vill importera en ny mall.

   ![Guiden Skapa webbplats](../assets/site-creation-wizard.png)

   1. Om du väljer att importera letar du i filläsaren reda på mallen som du vill använda och väljer **Överför**.

   1. När den har överförts visas den i listan med tillgängliga mallar.

1. När du väljer en mall visas information om mallen i den högra kolumnen. Välj önskad mall och välj **Nästa**.

   ![Välj en mall](../assets/select-site-template.png)

1. Ange en titel för din webbplats. Om det utelämnas kan du ange eller generera ett platsnamn från titeln.

   * Platsens titel visas i webbläsarens namnlist.
   * Webbplatsnamnet blir en del av webbadressen.
   * Webbplatsnamnet måste uppfylla [AEM regler för sidnamngivning](/help/sites-cloud/authoring/sites-console/organizing-pages.md#page-name-restrictions-and-best-practices).

1. Ange ytterligare webbplatsinformation enligt webbplatsmallen.

   * Olika mallar kan kräva ytterligare information.
   * Mallar för [Edge Delivery Services-projekt](https://www.aem.live/developer/ue-tutorial) kräver till exempel GitHub-databasen för ditt projekt.

1. Välj **Skapa** så skapas webbplatsen från webbplatsmallen.

   ![Information om den nya platsen](../assets/create-site-details.png)

1. Välj **Klar** i bekräftelsedialogrutan som visas.

   ![Dialogrutan Slutfört](../assets/success.png)

1. I webbplatskonsolen är den nya platsen synlig och kan navigeras för att utforska dess grundläggande struktur enligt mallen.

   ![Ny webbplatsstruktur](../assets/new-site.png)

Innehållsförfattare kan nu börja skriva!

## Webbplatsanpassning {#site-customization}

Mallar är användbara när du snabbt vill ställa in grundläggande struktur och stil för en plats. De flesta projekt kräver dock viss ytterligare formatering och anpassning. Webbplatsmallar gör att webbplatsens format inte behöver vara densamma så att utvecklare inte behöver någon kunskap om AEM för att skapa webbplatsen, utan kan
arbeta separat och parallellt med de som skapar innehållet. Beroende på vilken typ av projekt det är kan det ta två former.

* För projekt med AEM sidredigering med Universal Editor och leverans via [edge-leverans,](/help/edge/overview.md) görs all formatering i GitHub-projektet.
   * Mer information finns i dokumentet [Komma igång - Självstudiekurs för utvecklare av universell redigerare](https://www.aem.live/developer/ue-tutorial).
* För projekt med traditionell AEM sidredigering och leverans via [publiceringsleverans](/help/sites-cloud/authoring/author-publish.md) hämtar AEM-administratören bara webbplatstemat och skickar det till den frontutvecklare som anpassar det med sina favoritverktyg och sedan implementerar ändringarna i AEM koddatabas, som sedan distribueras.
   * Mer information finns i dokumentet [AEM Quick Site Creation Journey](/help/journey-sites/quick-site/overview.md).
