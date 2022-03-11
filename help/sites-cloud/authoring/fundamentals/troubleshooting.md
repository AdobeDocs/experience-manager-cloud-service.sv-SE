---
title: Felsöka AEM vid redigering
description: Vissa problem som kan uppstå när du använder AEM
exl-id: b9c0584d-255e-486d-b829-09e07499ecd2
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 13%

---

# Felsöka AEM vid redigering {#troubleshooting-aem-when-authoring}

I följande avsnitt beskrivs några problem som du kan stöta på när du använder AEM, tillsammans med förslag på hur du felsöker dem.

## Gammal sidversion finns fortfarande på publicerad webbplats {#old-page-version-still-on-published-site}

* **Problem**:
   * Du har gjort ändringar på en sida och publicerat sidan på den publicerade webbplatsen, men *gammal* versionen av sidan visas fortfarande på publiceringswebbplatsen.
* **Orsak**:
   * Detta kan ha flera orsaker, oftast cachen (antingen din lokala webbläsare eller Dispatcher), men ibland kan det vara ett problem med replikeringskön.
* **Lösningar**:
   * Här finns olika möjligheter:
   * Bekräfta att sidan har replikerats korrekt. Kontrollera sidstatus och, om det behövs, status för replikeringskön.
   * Rensa cacheminnet i den lokala webbläsaren och öppna sidan igen.
   * Lägg till `?` till slutet av sid-URL:en. Till exempel:
      * `http://<host>:<port>/sites.html/content?`
      * Detta begär sidan direkt från AEM och kringgår Dispatcher. Om du får den uppdaterade sidan är det en indikation på att du bör rensa Dispatcher-cachen.
   * Kontakta systemadministratören om det finns problem med replikeringsköerna.

## Komponentåtgärder visas inte i verktygsfältet {#component-actions-not-visible-on-toolbar}

* **Problem**:
   * Hela omfånget av tillämpliga komponentåtgärder visas inte när du redigerar en innehållssida i redigeringsmiljön.
* **Orsak**:
   * I sällsynta fall kan en tidigare åtgärd påverka verktygsfältet.
* **Lösning**:
   * Uppdatera sidan.
