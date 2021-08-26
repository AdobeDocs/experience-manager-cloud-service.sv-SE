---
title: Installera och konfigurera spelare i skärmar som en Cloud Service
description: På den här sidan beskrivs hur du installerar och konfigurerar spelare på skärmar som en Cloud Service.
source-git-commit: 6afb71803ae24bed2d5d5662a7cdd4af5637e329
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---


# Installera och konfigurera spelare i skärmar som en Cloud Service {#installing-players-screens-cloud}

I det här avsnittet beskrivs hur du installerar AEM Screens-spelare som är registrerade för lokala AEM. Dessutom måste du göra en fabriksåterställning av den befintliga spelaren och sedan registrera den nya spelaren mot AEM Screens som en Cloud Service.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du konfigurerar spelaren innan du registrerar spelarna. Efter att ha läst bör du förstå:

* var spelarna ska installeras från
* hur du uppdaterar spelaren till molnläge

## Steg för att ställa in spelaren till molnläge {#cloud-mode-setup}

När du har hämtat den senaste spelaren från [AEM Screens Player Downloads](https://download.macromedia.com/screens/) är du nu redo att uppdatera spelaren till molnläge.

Uppdatera spelaren genom att följa stegen nedan:

1. Öppna AEM Screens Player.

   >[!NOTE]
   >Du kan välja att testa med dedikerade maskinvaruenheter eller med ett webbtillägg på din egen spelare.

1. Klicka på fliken **Konfiguration** och klicka på **Till fabrik** under **Återställ**.

   ![bild](/help/screens-cloud/assets/player/installplayer-2.png)

1. Klicka på **Bekräfta** för att återställa spelaren.

1. Återigen från fliken **Konfiguration** och klicka på **Ändra till molnläge** under **Växla körläge**.

   ![bild](/help/screens-cloud/assets/player/installplayer-1.png)

1. Klicka på **Bekräfta** som visas när du växlar till molnläge för att avregistrera spelaren.

## Grundläggande uppspelningsövervakning {#playback-monitoring}

Spelaren rapporterar olika uppspelningsmått med varje `ping` som har standardvärdet 30 sekunder. Baserat på mätvärden kan du identifiera olika kantfall, t.ex. problem med fastnade bilder, tomma skärmar och schemaläggning. På så sätt kan du förstå och felsöka problem på enheten och därmed snabba upp en utredning och korrigerande åtgärder.

Med grundläggande uppspelningsövervakning i en AEM Screens-spelare kan du:

* Fjärrövervaka om en spelare spelar upp innehåll korrekt

* Förbättra reaktiviteten till tomma skärmar eller trasiga upplevelser på fältet

* Minska risken för att slutanvändaren får en trasig upplevelse

### Förstå egenskaper {#understand-properties}

Följande egenskaper ingår i varje `ping`:

| Egenskap | Beskrivning |
|---|---|
| id {string} | spelarens identifierare |
| activeChannel {string} | spelar upp kanalsökvägen eller null om inget är schemalagt |
| activeElements {string} | kommaavgränsad sträng, för närvarande synliga element i alla uppspelningskanaler (flera vid en flerzonslayout) |
| isDefaultContent {boolean} | true om den spelande kanalen betraktas som en standard- eller reservkanal (d.v.s. har prioritet 1 och inget schema) |
| hasContentChanged {boolean} | true om innehållet har ändrats under de senaste fem minuterna, annars false |
| lastContentChange {string} | tidsstämpel för den senaste innehållsändringen |

>[!NOTE]
>Om du vill kan du aktivera en mer avancerad egenskap från spelarens inställningar (Aktivera övervakning av uppspelning). Det vill säga:
>|Egenskap|Beskrivning|
>|—|—|
>|isContentRendering {boolean}|true om grafikprocessorn kan bekräfta att det faktiska innehållet spelas upp (baserat på pixelanalys)|


## What&#39;s Next {#whats-next}

Nu när du har installerat och konfigurerat spelaren till molnläge bör du fortsätta att använda skärmar som en Cloud Service genom att nästa gång du granskar dokumentet [Registrera spelare i skärmar som en Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) från leverantören av skärmtjänster.