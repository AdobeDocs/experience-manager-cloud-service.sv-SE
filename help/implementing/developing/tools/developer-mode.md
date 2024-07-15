---
title: Utvecklarläge
seo-title: Developer Mode
description: I utvecklarläget öppnas en sidopanel med flera flikar som ger utvecklaren information om den aktuella sidan
seo-description: Developer mode opens a side panel with several tabs that provide a developer with information about the current page
exl-id: fbf11c0f-dc6e-43f3-bcf2-080eacc6ba99
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Utvecklarläge {#developer-mode}

När du redigerar sidor i AEM finns flera [lägen](/help/sites-cloud/authoring/sites-console/introduction.md#page-modes) tillgängliga, bland annat i utvecklarläget. I utvecklarläget öppnas en sidopanel med flera flikar som ger utvecklaren teknisk information om den aktuella sidan.

Det finns två flikar:

* **[Komponenter](#components)** för att visa struktur- och prestandainformation.
* **[Fel](#errors)** om du vill se eventuella problem.

Detta hjälper en utvecklare att:

* **Upptäck** hur sidorna är sammansatta.
* **Felsök:** vad som händer var och när, vilket i sin tur hjälper till att lösa problem.

>[!NOTE]
>
>Utvecklarläge:
>
>* Är inte tillgängligt på mobila enheter eller små fönster på skrivbordet (på grund av utrymmesbegränsningar).
>  * Detta inträffar när bredden är mindre än 1024px.
>* Är bara tillgänglig för användare som är medlemmar i gruppen `administrators`.

## Öppnar utvecklarläge {#opening-developer-mode}

Utvecklarläget implementeras som en sidopanel i sidredigeraren. Om du vill öppna panelen väljer du **Utvecklare** i lägesväljaren i verktygsfältet i sidredigeraren:

![Öppnar utvecklarläge](assets/developer-mode.png)

Panelen är uppdelad i två flikar:

* **[Komponenter](#components)** - Detta visar ett komponentträd, som liknar [innehållsträdet](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#content-tree) för författare
* **[Fel](#errors)** - När problem uppstår visas information för varje komponent.

### Fliken Komponenter {#components}

![Fliken Komponenter](assets/developer-mode-components-tab.png)

Detta visar ett komponentträd som:

* Skapar konturer för kedjan med komponenter och mallar som återges på sidan. Trädet kan expanderas för att visa kontext i hierarkin.
* Visar den datortid på serversidan som krävs för att återge komponenten.
* Gör att du kan expandera trädet och välja specifika komponenter i trädet. Markeringen ger åtkomst till komponentinformation, till exempel:
   * Databassökväg
   * Länkar till skript (används i CRXDE Lite)
   * Komponentdetaljer som de visas i [komponentkonsolen](/help/sites-cloud/authoring/components-console.md)
* Komponenter som är markerade i trädet markeras med en blå kant i redigeraren.

På fliken Komponenter kan du

* Fastställ och jämför återgivningstiden per komponent.
* Se och förstå hierarkin.
* Förstå och förbättra sidinläsningstiden genom att hitta långsamma komponenter.

Varje komponentpost kan ha följande alternativ:

![Exempel på komponent i utvecklarläge](assets/developer-mode-component-example.png)

* **Visa detaljer:** En länk till en lista som visar:
   * Alla komponentskript som används för att återge komponenten.
   * Databasens innehållssökväg för den här specifika komponenten.

     ![Visa detaljer](assets/developer-mode-view-details.png)

* **Redigera skript:** En länk som öppnar komponentskriptet i CRXDE Lite.

* **Visa komponentinformation:** Öppnar information om komponenten i [komponentkonsolen](/help/sites-cloud/authoring/components-console.md).

Om du expanderar en komponentpost genom att trycka eller klicka på gruppen kan du även visa:

    * Hierarkin i den markerade komponenten.
    * Återgivningstider för den markerade komponenten separat, alla enskilda inkapslade komponenter och den kombinerade summan.

### Fliken Fel {#errors}

![Fliken Fel](assets/developer-mode-errors-tab.png)

Förhoppningsvis kommer fliken **Fel** alltid att vara tom (som ovan), men när problem uppstår kan följande information visas för varje komponent:

* En varning om komponenten skriver en post i felloggen, tillsammans med information om felet och direktlänkar till rätt kod i CRXDE Lite.
* En varning om komponenten öppnar en administratörssession.

Om till exempel en odefinierad metod anropas visas det resulterande felet på fliken **Fel** och komponentposten i trädet på fliken **Komponenter** markeras också med en indikator när ett fel inträffar.
