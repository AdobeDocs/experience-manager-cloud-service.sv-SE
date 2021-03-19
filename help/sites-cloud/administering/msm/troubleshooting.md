---
title: Felsökning av MSM-problem och vanliga frågor
description: Ta reda på hur du felsöker de vanligaste MSM-relaterade problemen och får svar på de vanligaste MSM-relaterade frågorna.
feature: Multi Site Manager
role: Administratör
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# Felsökning av MSM-problem och vanliga frågor och svar {#troubleshooting-msm}

## Felsökning av första steg {#first-steps}

Om du upplever något du tycker är felaktigt eller ett fel i MSM ska du se till att du före felsökningen och den detaljerade felsökningen gör så här:

* Kontrollera [Vanliga frågor om MSM](#faq) eftersom dina problem eller frågor redan kan åtgärdas där.
* Läs artikeln [MSM best practices](best-practices.md) när ett antal tips finns där tillsammans med förtydliganden av ett antal missuppfattningar.

## Hitta avancerad information om din plan- och Live Copy-status {#advanced-info}

MSM registrerar flera servrar som kan begäras med väljare på resurs-URL:erna. Dessa används av användargränssnittet men kan också begäras direkt för att se ytterligare avancerade beräknade MSM-statusvärden för dina sidor:

1. `http://<host>:<port>/content/path/to/bluprint/page.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`
   * Använd detta på en ritningssida för att hämta listan över alla Live-kopior som är länkade till den, med ytterligare statusinformation för Live Copy.
1. `http://<host>:<port>/content/path/to/livecopy/page.msm.json`
   * Använd detta på Live Copy-sidor för att hämta avancerad information om deras anslutning till deras ritningssidor. Om sidan inte är en Live-kopia returneras ingenting.

Dessa servrar genererar DEBUG-loggmeddelanden via `com.day.cq.wcm.msm`-loggen som också kan vara till hjälp.

## Kontrollerar MSM-specifik information i databasen {#checking-repo}

De tidigare servletarna returnerade beräknad information baserat på MSM-specifika noder och mixins. Informationen lagras i databasen på följande sätt.

* `cq:LiveSync` blandningstyp
   * Detta anges för `jcr:content`-noder och definierar Live Copy-rotsidor.
   * Dessa sidor kommer att ha en `cq:LiveSyncConfig`-underordnad nod av typen `cq:LiveCopy` som kommer att innehålla grundläggande och obligatorisk information i Live-kopian via följande egenskaper:
      * `cq:master` pekar på Live Copy-sidan.
      * `cq:rolloutConfigs` visar aktiva utrullningskonfigurationer som tillämpas på Live Copy.
      * `cq:isDeep` true if the child pages of this root Live Copy page are included in the Live Copy.
* `cq:LiveRelationship` blandningstyp
   * Alla Live Copy-sidor har en sådan blandningstyp på noden `jcr:content`.
   * Om så inte är fallet har sidan vid något tillfälle kopplats loss eller skapats manuellt via redigeringsgränssnittet utanför en Live Copy-åtgärd (skapa eller utrulla).
* `cq:LiveSyncCancelled` blandningstyp
   * Lades till i `jcr:content` noder med Live Copy-sidor som har pausats.
   * Om uppehållet även gäller för underordnade sidor anges egenskapen `cq:isCancelledForChildren` till true på samma nod.

Informationen i dessa egenskaper bör återspeglas i användargränssnittet, men vid felsökning kan det vara bra att observera MSM-beteenden direkt i databasen när MSM-åtgärder utförs.

Att känna till dessa egenskaper kan också vara användbart för att fråga databasen och ta reda på uppsättningar med sidor som är i vissa lägen. Till exempel:

* `select * from cq:LiveSync` returnerar alla Live Copy-rotsidor.

## Vanliga frågor och svar {#faq}

Här är några vanliga frågor om MSM och Live Copy.

### Varför uppdateras inte vissa egenskaper (t.ex. titel, anteckningar) under en MSM-utrullning? {#missing-properties}

MSM-synkroniseringsåtgärder är mycket konfigurerbara. Vilka egenskaper eller komponenter som ändras under utrullningar beror direkt på egenskaperna för dessa konfigurationer.

Mer information om det här ämnet finns i [den här artikeln](best-practices.md).

### Hur tar jag bort utrullningsbehörigheter för en grupp författare? {#remove-rollout-permissions}

Det finns inget **rollout**-privilegium som kan anges eller tas bort för AEM (användare eller grupper).

Du kan också:

* Anpassa produktanvändargränssnittet för att dölja rollout-åtgärder för ett givet huvudkonto.
* Ta bort skrivrättigheter från Live Copy-trädet för författare som inte får rulla ut.

### Varför visas Live Copy-sidor med suffixet&quot;_msm_move&quot;? {#moved-pages}

Om en ritningssida introduceras uppdaterar den antingen sin Live Copy-sida eller skapar en ny Live Copy-sida om den inte finns ännu (t.ex. när den introduceras för första gången eller när Live Copy-sidan tas bort manuellt).

Om det i det senare fallet däremot finns en sida utan egenskapen `cq:LiveRelationship` med samma namn, kommer sidans namn att ändras i enlighet med detta innan sidan Live Copy skapas.

Som standard förväntas en länkad Live Copy-sida, till vilken uppdateringarna av ritningarna kommer att rullas ut, eller ingen sida på, när en Live Copy-sida skapas.

Om en fristående sida hittas väljer MSM att byta namn på sidan och skapa en separat länkad Live Copy-sida.

En sådan fristående sida i ett underträd i Live Copy är vanligtvis resultatet av en **Koppla loss**-åtgärd, eller så togs den tidigare sidan bort manuellt av en författare och återskapades med samma namn.

Undvik detta genom att använda funktionen **Gör uppehåll** i stället för **Koppla loss**. Mer information om åtgärden **Koppla loss** i [den här artikeln.](creating-live-copies.md)
