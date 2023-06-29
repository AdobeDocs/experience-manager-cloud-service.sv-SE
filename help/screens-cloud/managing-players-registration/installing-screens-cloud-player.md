---
title: Installera och konfigurera spelare på skärmar as a Cloud Service
description: På den här sidan beskrivs hur du installerar och konfigurerar spelare på skärmar as a Cloud Service.
exl-id: a022738a-c543-4629-a244-f70fa294fe7f
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# Installera och konfigurera spelare på skärmar as a Cloud Service {#installing-players-screens-cloud}

I det här avsnittet beskrivs hur du installerar AEM Screens-spelare som är registrerade för lokala AEM. Du måste också göra en fabriksåterställning av den befintliga spelaren och sedan registrera den nya spelaren mot AEM Screens as a Cloud Service.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du konfigurerar spelaren innan du registrerar spelarna. När du har läst bör du förstå följande:

* var spelarna ska installeras från
* hur du uppdaterar spelaren till molnläge

## Steg för att ställa in spelaren till molnläge {#cloud-mode-setup}

När du har hämtat den senaste spelaren från [AEM Screens Player - nedladdningar](https://download.macromedia.com/screens/)är du nu redo att uppdatera spelaren till molnläge.

Uppdatera spelaren genom att följa stegen nedan:

1. Öppna AEM Screens Player.

   >[!NOTE]
   >Du kan välja att testa med dedikerade maskinvaruenheter eller med ett webbtillägg på din egen spelare.

1. Klicka på **Konfiguration** och klicka **Till fabrik** knapp under **Återställ** alternativ.

   ![bild](/help/screens-cloud/assets/player/installplayer-2.png)

1. Klicka **Bekräfta** för att återställa spelaren.

1. Återigen från **Konfiguration** och klicka **Ändra till molnläge** knapp under **Växla körningsläge** alternativ.

   ![bild](/help/screens-cloud/assets/player/installplayer-1.png)

1. Klicka **Bekräfta** som visas när du växlar till molnläge avregistrerar spelaren.

## Grundläggande uppspelningsövervakning {#playback-monitoring}

Spelaren rapporterar olika uppspelningsmått för varje `ping` som standard är 30 sekunder. Baserat på dessa mått kan Adobe identifiera olika kantfall, t.ex. problem med fastsittning, tomma skärmar och schemaläggning. Den här identifieringen gör att vi kan förstå och felsöka problem på enheten och därför kan vi genomföra en utredning och vidta åtgärder tillsammans med dig.

Med grundläggande uppspelningsövervakning i en AEM Screens-spelare kan vi:

* Fjärrövervaka om en spelare spelar upp innehållet på rätt sätt.

* Förbättra reaktiviteten till tomma skärmar eller trasiga upplevelser på fältet.

* Minskar risken för att slutanvändaren får en trasig upplevelse.

### Förstå egenskaper {#understand-properties}

Följande egenskaper ingår i varje `ping`:

| Egenskap | Beskrivning |
|---|---|
| id {string} | spelarens identifierare |
| activeChannel {string} | spelar upp kanalsökvägen eller null om inget är schemalagt |
| activeElements {string} | kommaavgränsad sträng, för närvarande synliga element i alla uppspelningskanaler (flera om det fanns en layout med flera zoner) |
| isDefaultContent {boolean} | true om den spelande kanalen betraktas som en standard- eller reservkanal (d.v.s. har prioritet 1 och inget schema) |
| hasContentChanged {boolean} | true om innehållet har ändrats under de senaste fem minuterna, annars false |
| lastContentChange {string} | tidsstämpel för den senaste innehållsändringen |

>[!NOTE]
>Du kan även aktivera en mer avancerad egenskap i spelarens inställningar (Aktivera övervakning av uppspelning):
>|Egenskap|Beskrivning|
>|—|—|
>|isContentRendering {boolean}|true om grafikprocessorn kan bekräfta att det faktiska innehållet spelas upp (baserat på pixelanalys)|

### Begränsningar {#limitations}

Några begränsningar för grundläggande uppspelningsövervakning visas nedan:

* Spelaren rapporterar ett eget uppspelningsläge till servern, vilket kräver en aktiv anslutning.

* The `isContentRendering` som kontrollerar att grafikprocessorn är alltför resurskrävande att aktiveras som standard och kräver explicit deltagande från spelarens inställningar. Vi rekommenderar att du inte använder den med videofilmer i produktion.

* Den här funktionen stöds bara för sekvenskanaler och täcker ännu inte de interaktiva kanalernas (SPA) användningsfall.

* Måtten är ännu inte helt exponerade för kunderna. Adobe arbetar snart med att aktivera kontrollpanelsliknande rapporterings- och varningsmekanismer.

## What&#39;s Next {#whats-next}

Nu när du har installerat och konfigurerat spelaren till molnläge kan du fortsätta den as a Cloud Service vägen för skärmar. Se [Registrerar spelare på skärmar as a Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) från Screens Services Provider.
