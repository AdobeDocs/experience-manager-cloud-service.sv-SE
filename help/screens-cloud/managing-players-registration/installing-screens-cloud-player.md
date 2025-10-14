---
title: Installera och konfigurera spelare i Screens as a Cloud Service
description: På den här sidan beskrivs hur du installerar och konfigurerar spelare i Screens as a Cloud Service.
exl-id: a022738a-c543-4629-a244-f70fa294fe7f
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: 53086e2ec6d9d962a8f1cb1cc40f0601da74ac63
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---

# Installera och konfigurera spelare i Screens as a Cloud Service {#installing-players-screens-cloud}

I det här avsnittet beskrivs hur du installerar AEM Screens-spelare som är registrerade för lokala AEM. Du måste också göra en fabriksåterställning av den befintliga spelaren och sedan registrera den nya spelaren mot AEM Screens as a Cloud Service.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du konfigurerar spelaren innan du registrerar spelarna. När du har läst bör du förstå följande:

* var spelarna ska installeras från
* hur du uppdaterar spelaren till molnläge

## Steg för att ställa in spelaren till molnläge {#cloud-mode-setup}

När du har hämtat den senaste spelaren från [AEM Screens Player-hämtningar](https://download.macromedia.com/screens/) kan du nu uppdatera spelaren till molnläge.

Uppdatera spelaren genom att följa stegen nedan:

1. Öppna AEM Screens Player.

   >[!NOTE]
   >Du kan välja att testa med dedikerade maskinvaruenheter eller med ett webbtillägg på din egen spelare.

1. Klicka på fliken **Konfiguration** och klicka på knappen **Till fabrik** under alternativet **Återställ**.

   ![Till fabrik, knapp under alternativet Återställ](/help/screens-cloud/assets/player/installplayer-2.png)

1. Klicka på **Bekräfta** för att återställa spelaren.

1. Återigen från fliken **Konfiguration** och klicka på knappen **Ändra till molnläge** under alternativet **Växla körläge**.

   ![Ändra till molnläge under alternativet Växla körläge &#x200B;](/help/screens-cloud/assets/player/installplayer-1.png)

1. Klicka på **Bekräfta** som visas när du växlar till molnläge för att avregistrera spelaren.

## Grundläggande uppspelningsövervakning {#playback-monitoring}

Spelaren rapporterar olika uppspelningsmått med varje `ping` som har standardvärdet 30 sekunder. Baserat på dessa mått kan Adobe identifiera olika kantfall, t.ex. problem med fastsittning, tomma skärmar och schemaläggning. Den här identifieringen gör att vi kan förstå och felsöka problem på enheten och därför kan vi genomföra en utredning och vidta åtgärder tillsammans med dig.

Med grundläggande uppspelningsövervakning i en AEM Screens-spelare kan vi:

* Fjärrövervaka om en spelare spelar upp innehållet korrekt.

* Förbättra reaktiviteten till tomma skärmar eller trasiga upplevelser på fältet.

* Minskar risken för att användaren får en trasig upplevelse.

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
>
>Du kan även aktivera en mer avancerad egenskap i spelarens inställningar (Aktivera övervakning av uppspelning):
>
>| Egenskap | Beskrivning |
>|---|---|
>| isContentRendering {boolean} | true om grafikprocessorn kan bekräfta att det spelar upp faktiskt innehåll (baserat på pixelanalys) |

### Begränsningar {#limitations}

Några begränsningar för grundläggande uppspelningsövervakning visas nedan:

* Spelaren rapporterar ett eget uppspelningsläge till servern, vilket kräver en aktiv anslutning.

* Egenskapen `isContentRendering` som kontrollerar grafikprocessorn är för resurskrävande att aktiveras som standard och kräver explicit deltagande från spelarens inställningar. Vi rekommenderar att du inte använder den med videofilmer i produktion.

* Den här funktionen stöds bara för sekvenskanaler och täcker ännu inte de interaktiva kanalernas (SPA) användningsfall.

* Måtten är ännu inte helt exponerade för kunderna. Adobe arbetar på att aktivera kontrollpanelsliknande rapporterings- och varningsfunktioner inom kort.

## What&#39;s Next {#whats-next}

Nu när du har installerat och konfigurerat spelaren till molnläge kan du fortsätta din as a Cloud Service Screens-resa. Se [Registrera spelare i Screens as a Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) från Screens Services Provider.
