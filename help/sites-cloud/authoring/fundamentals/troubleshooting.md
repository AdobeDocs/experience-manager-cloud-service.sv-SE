---
title: Felsöka AEM vid redigering
description: Vissa problem som kan uppstå när du använder AEM
exl-id: b9c0584d-255e-486d-b829-09e07499ecd2
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Felsöka AEM vid redigering {#troubleshooting-aem-when-authoring}

I följande avsnitt beskrivs några problem som du kan stöta på när du använder AEM, tillsammans med förslag på hur du felsöker dem.

## Gammal sidversion på publicerad webbplats {#old-page-version-still-on-published-site}

* **Utgåva**:
   * Du har ändrat en sida och publicerat sidan på den publicerade webbplatsen, men den *gamla* versionen av sidan visas fortfarande på den publicerade webbplatsen.
* **Orsak**:
   * Detta kan ha flera orsaker, oftast cacheminnet (antingen din lokala webbläsare eller Dispatcher), men ibland kan det vara ett problem med replikeringskön.
* **Lösningar**:
   * Här finns olika möjligheter:
   * Bekräfta att sidan har replikerats korrekt. Kontrollera sidstatus och, om det behövs, status för replikeringskön.
   * Rensa cacheminnet i den lokala webbläsaren och få åtkomst till sidan igen.
   * Lägg till `?` i slutet av sidans URL. Till exempel:
      * `http://<host>:<port>/sites.html/content?`
      * Detta begär sidan direkt från AEM och kringgår Dispatcher. Om du får den uppdaterade sidan är det en indikation på att du bör rensa Dispatcher-cachen.
   * Kontakta systemadministratören om det finns problem med replikeringsköerna.

## Komponentåtgärder visas inte i verktygsfältet {#component-actions-not-visible-on-toolbar}

* **Utgåva**:
   * Hela omfånget av tillämpliga komponentåtgärder visas inte när du redigerar en innehållssida i redigeringsmiljön.
* **Orsak**:
   * I sällsynta fall kan en tidigare åtgärd påverka verktygsfältet.
* **Lösning**:
   * Uppdatera sidan.
