---
title: Felsökning av MSM-problem och vanliga frågor
description: Ta reda på hur du felsöker de vanligaste MSM-relaterade problemen och får svar på de vanligaste MSM-relaterade frågorna.
feature: Multi Site Manager
role: Admin
exl-id: 50f02f4f-a347-4619-ac90-b3136a7b1782
source-git-commit: 7c0be1a7bdc9ccb788ba41eb6ee83b89df94f500
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---

# Felsökning av MSM-problem och vanliga frågor {#troubleshooting-msm}

## Felsökning av första steg {#first-steps}

Om du upplever något du tycker är felaktigt eller ett fel i MSM ska du se till att du före felsökningen och den detaljerade felsökningen gör så här:

* Kontrollera [Vanliga frågor om MSM](#faq) eftersom dina problem eller frågor redan kan åtgärdas där.
* Kontrollera [Artiklar om bästa praxis för MSM](best-practices.md) som ett antal tips ges tillsammans med förtydliganden av ett antal missuppfattningar.

## Hitta avancerad information om din plan- och Live Copy-status {#advanced-info}

MSM registrerar flera servrar som kan begäras med väljare på resurs-URL:erna. Dessa används av användargränssnittet men kan också begäras direkt för att se ytterligare avancerade beräknade MSM-statusvärden för dina sidor:

1. `http://<host>:<port>/content/path/to/bluprint/page.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`
   * Använd detta på en ritningssida för att hämta listan över alla Live-kopior som är länkade till den, med ytterligare statusinformation för Live Copy.
   * till exempel:
      `http://localhost:4502/content/wknd/language-masters/en.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`

1. `http://<host>:<port>/content/path/to/livecopy/page.msm.json`
   * Använd detta på Live Copy-sidor för att hämta avancerad information om deras anslutning till deras ritningssidor. Om sidan inte är en Live-kopia returneras ingenting.
   * till exempel:
      `http://localhost:4502/content/wknd/ca/en.msm.json`

Dessa servrar genererar felsökningsloggmeddelanden via `com.day.cq.wcm.msm` loggare som också kan vara till hjälp.

## Kontrollera MSM-specifik information i databasen {#checking-repo}

De tidigare servletarna returnerade beräknad information baserat på MSM-specifika noder och mixins. Informationen lagras i databasen på följande sätt.

* `cq:LiveSync` blandningstyp
   * Detta är inställt på `jcr:content` noder och definiera Live Copy-rotsidor.
   * Sidorna har en `cq:LiveSyncConfig` underordnad nod av typen `cq:LiveCopy` som kommer att innehålla grundläggande och obligatorisk information om Live Copy via följande egenskaper:
      * `cq:master` pekar på Live Copy-sidan.
      * `cq:rolloutConfigs` visar aktiva utrullningskonfigurationer som tillämpas på Live Copy.
      * `cq:isDeep` true if the child pages of this root Live Copy page are included in the Live Copy.
* `cq:LiveRelationship` blandningstyp
   * En Live Copy-sida har en sådan blandningstyp på sin `jcr:content` nod.
   * Om så inte är fallet har sidan vid något tillfälle kopplats loss eller skapats manuellt via redigeringsgränssnittet utanför en Live Copy-åtgärd (skapa eller utrulla).
* `cq:LiveSyncCancelled` blandningstyp
   * Tillagd i `jcr:content` noder med Live Copy-sidor som har pausats.
   * Om uppehållet även gäller för underordnade sidor, är en `cq:isCancelledForChildren` egenskapen är inställd på true på samma nod.

Informationen i dessa egenskaper bör återspeglas i användargränssnittet, men vid felsökning kan det vara bra att observera MSM-beteenden direkt i databasen när MSM-åtgärder utförs.

Att känna till dessa egenskaper kan också vara användbart för att fråga databasen och ta reda på uppsättningar med sidor som är i vissa lägen. Till exempel:

* `select * from cq:LiveSync` returnerar alla Live Copy-rotsidor.

## Vanliga frågor {#faq}

Här är några vanliga frågor om MSM och Live Copy.

### Varför uppdateras inte vissa egenskaper (till exempel titel, anteckningar) under en MSM-utrullning? {#missing-properties}

MSM-synkroniseringsåtgärder är mycket konfigurerbara. Vilka egenskaper eller komponenter som ändras under utrullningar beror direkt på egenskaperna för dessa konfigurationer.

Se [den här artikeln](best-practices.md) om du vill ha mer information om det här avsnittet.

### Hur tar jag bort utrullningsbehörigheter för en grupp författare? {#remove-rollout-permissions}

Det finns inga **utrullning** privilegium som kan anges eller tas bort för AEM (användare eller grupper).

Du kan också:

* Anpassa produktanvändargränssnittet för att dölja rollout-åtgärder för ett givet huvudkonto.
* Ta bort skrivrättigheter från Live Copy-trädet för författare som inte får rulla ut.

### Varför visas Live Copy-sidor med suffixet&quot;_msm_move&quot;? {#moved-pages}

Om en ritningssida introduceras uppdaterar den antingen sin Live Copy-sida eller skapar en ny Live Copy-sida om den inte finns än (t.ex. när den introduceras för första gången eller när Live Copy-sidan tas bort manuellt).

I det senare fallet om en sida utan `cq:LiveRelationship` -egenskapen finns med samma namn. Sidans namn ändras därefter innan sidan Live Copy skapas.

Som standard förväntas en länkad Live Copy-sida, till vilken uppdateringarna av ritningarna kommer att rullas ut, eller ingen sida på, när en Live Copy-sida skapas.

Om en fristående sida hittas väljer MSM att byta namn på sidan och skapa en separat länkad Live Copy-sida.

En sådan fristående sida i ett underträd i Live Copy är vanligtvis resultatet av en **Koppla loss** eller den tidigare Live Copy-sidan togs bort manuellt av en författare och återskapades med samma namn.

Du undviker detta genom att använda Live Copy **Gör uppehåll** i stället för **Koppla loss**. Mer information om **Koppla loss** åtgärd i [den här artikeln.](creating-live-copies.md)
