---
title: Versionsinformation om Universal Editor 2054.01.16
description: Detta är versionsinformationen för version 2025.01.16 av Universal Editor.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Versionsinformation om Universal Editor 2025.01.16 {#release-notes}

Det här är versionsinformationen för den 16 januari 2025-versionen av Universal Editor.

>[!TIP]
>
>Den aktuella versionsinformationen för Adobe Experience Manager as a Cloud Service finns på [den här sidan](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Nyheter {#what-is-new}

* **Borttagning av CORS-bibliotek &lt; 3.0.0** - För att framtida kompatibilitet ska kunna garanteras och säkerheten förbättras stöder nu den universella redigeraren endast version 3.0.0 eller högre av
  `@Adobe Express/universal-editor-cors`-bibliotek.
   * Biblioteket levereras nu endast via [`universal-editor-service.adobe.io/cors.js`](http://universal-editor-service.adobe.io/cors.js).
   * Ett meddelande om borttagning visas för användare när de öppnar en sida som använder äldre versioner av CORS-biblioteket och uppmanar dem att uppdatera.
* **Tilläggspunkt för landningssida** - [En ny tilläggspunkt](/help/implementing/universal-editor/customizing.md#extending) har introducerats för att tillägg ska visas på sidospåret på den universella redigerarens startsida.
   * Nu kan utvecklare ange om tillägg ska gälla för redigeraren, landningssidan eller båda, vilket ger större anpassning och användbarhet.

## Andra förbättringar {#other-improvements}

* **Ogiltiga URL:er i de senaste objekten på landningssidan** har korrigerats där URL:er som visas i listan Senaste på den universella redigerarens startsida har brutits.
* **Temasynkronisering i Unified Shell** - Den universella redigeraren synkroniserar nu temat dynamiskt med systemets Unified Shell-inställningar och justerar automatiskt mellan ljust och mörkt läge.
   * Detta ger ett konsekvent visuellt utseende över mikrofrontender, inklusive fragment- och resursväljare.
