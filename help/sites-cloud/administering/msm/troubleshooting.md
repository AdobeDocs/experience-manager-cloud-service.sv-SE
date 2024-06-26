---
title: Felsökning av MSM-problem och vanliga frågor
description: Ta reda på hur du felsöker de vanligaste MSM-relaterade problemen och får svar på de vanligaste MSM-relaterade frågorna.
feature: Multi Site Manager
role: Admin
exl-id: 50f02f4f-a347-4619-ac90-b3136a7b1782
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 0%

---

# Felsökning av MSM-problem och vanliga frågor {#troubleshooting-msm}

## Felsökning av första steg {#first-steps}

Om du upplever något du tycker är felaktigt eller ett fel i MSM ska du se till att du före felsökningen och den detaljerade felsökningen gör så här:

* Kontrollera [Vanliga frågor om MSM](#faq) eftersom dina problem eller frågor redan kan åtgärdas där.
* Kontrollera [Artiklar om bästa praxis för MSM](best-practices.md) eftersom det ges flera tips tillsammans med förtydliganden av vissa missuppfattningar.

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

De tidigare servletarna returnerade beräknad information baserat på de MSM-specifika noderna och mixinerna. Informationen lagras i databasen på följande sätt.

* `cq:LiveSync` blandningstyp
   * Detta är inställt på `jcr:content` noder och definiera Live Copy-rotsidor.
   * Dessa sidor har en `cq:LiveSyncConfig` underordnad nod av typen `cq:LiveCopy` som innehåller grundläggande och obligatorisk information om Live Copy via följande egenskaper:
      * `cq:master` pekar på Live Copy-sidan.
      * `cq:rolloutConfigs` visar aktiva utrullningskonfigurationer som tillämpas på Live-kopian.
      * `cq:isDeep` true if the child pages of this root Live Copy page are included in the Live Copy.
* `cq:LiveRelationship` blandningstyp
   * En Live Copy-sida har en sådan blandningstyp på sin `jcr:content` nod.
   * Om så inte är fallet har sidan vid något tillfälle kopplats loss eller skapats manuellt via redigeringsgränssnittet utanför en Live Copy-åtgärd (skapa eller rulla ut).
* `cq:LiveSyncCancelled` blandningstyp
   * Tillagd i `jcr:content` noder med Live Copy-sidor som har pausats.
   * Om uppehållet även gäller för underordnade sidor, är en `cq:isCancelledForChildren` egenskapen är inställd på true på samma nod.

Informationen i dessa egenskaper bör återspeglas i användargränssnittet, men vid felsökning kan det vara bra att observera MSM-beteenden direkt i databasen när MSM-åtgärder utförs.

Att känna till dessa egenskaper kan också vara användbart så att du kan söka i databasen och ta reda på vilka siduppsättningar som är i olika lägen. Till exempel:

* `select * from cq:LiveSync` returnerar alla Live Copy-rotsidor.

## Vanliga frågor {#faq}

Här är några vanliga frågor om MSM och Live Copy.

### Varför uppdateras inte vissa egenskaper (till exempel titel, anteckningar) under en MSM-utrullning? {#missing-properties}

MSM-synkroniseringsåtgärder är mycket konfigurerbara. Vilka egenskaper eller komponenter som ändras under utrullningar beror direkt på egenskaperna för dessa konfigurationer.

Se [den här artikeln](best-practices.md) om du vill ha mer information om det här avsnittet.

### Hur tar jag bort utrullningsbehörigheter för en grupp författare? {#remove-rollout-permissions}

Det finns inga **utrullning** privilegium som kan anges eller tas bort för Adobe Experience Manager Principal (användare eller grupper).

Du kan också:

* Anpassa produktanvändargränssnittet för att dölja rollout-åtgärder för ett givet huvudkonto.
* Ta bort skrivrättigheter från Live Copy-trädet för författare som inte får rulla ut.

### Varför visas Live Copy-sidor med suffixet&quot;_msm_move&quot;? {#moved-pages}

Om en ritningssida introduceras uppdaterar den antingen sin Live Copy-sida eller skapar en Live Copy-sida om den inte finns ännu. Till exempel när den rullas ut för första gången eller när sidan Live-kopia togs bort manuellt.

I det senare fallet om en sida utan `cq:LiveRelationship` egenskapen finns med samma namn, så namnet på sidan ändras innan sidan Live Copy skapas.

Som standard förväntar sig utrullningen en länkad Live Copy-sida som uppdateringarna av ritningarna rullas ut på. Eller så förväntas ingen sida alls när en Live Copy-sida skapas.

Om en fristående sida hittas väljer MSM att byta namn på sidan och skapar en separat länkad Live Copy-sida.

En sådan fristående sida i ett Live Copy-underträd är vanligtvis resultatet av en **Koppla loss** eller den tidigare Live Copy-sidan togs bort manuellt av en författare och återskapades med samma namn.

Du undviker detta genom att använda Live Copy **Gör uppehåll** i stället för **Koppla loss**. Mer information om **Koppla loss** finns i [den här artikeln.](creating-live-copies.md)
