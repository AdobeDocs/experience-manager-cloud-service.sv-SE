---
title: Skapa en sida för mobila enheter
description: När du skapar för mobilen kan du växla mellan flera emulatorer för att se vad slutanvändaren ser
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Skapa en sida för mobila enheter {#authoring-a-page-for-mobile-devices}

Adobe Experience Manager-sidor bygger på en responsiv layout. Med responsiv layout anpassas innehållet automatiskt så att det passar målenheten, vilket eliminerar behovet av att skapa innehåll för specifika enheter.

När du skapar en mobilsida visas sidan på ett sätt som emulerar den mobila enheten. När du skapar sidan kan du växla mellan flera emulatorer för att se vad slutanvändaren ser när han/hon öppnar sidan.

Enheterna grupperas i kategorierna, funktion, smart och touchfunktion enligt enhetens funktioner för att återge en sida. När slutanvändaren öppnar en mobilsida upptäcker AEM enheten och skickar den representation som motsvarar enhetsgruppen.

>[!NOTE]
>
>Om du vill skapa en mobilwebbplats baserad på en befintlig standardwebbplats skapar du en live-kopia av standardwebbplatsen. Se Skapa en Live-kopia för olika kanaler.
>
>AEM-utvecklare kan skapa nya enhetsgrupper. Se Skapa enhetsgruppsfilter.
<!--
>To create a mobile site based on an existing standard site, create a live copy of the standard site. (See [Creating a Live Copy for Different Channels](/help/sites-administering/msm-livecopy.md).)
>
>AEM developers can create new device groups. (See [Creating Device Group Filters](/help/sites-developing/groupfilters.md).)
-->

Använd följande procedur för att skapa en mobilsida:

1. Öppna konsolen **Platser** från global navigering.
1. Redigera en innehållssida.
1. Växla till önskad emulator genom att klicka på ikonen **Emulator** längst upp på sidan.

   ![Emulatorikon](/help/sites-cloud/authoring/assets/emulator.png)

1. Dra och släpp komponenter från komponentwebbläsaren eller resursläsaren till sidan.
1. [Ändra sidans responsiva layout](/help/sites-cloud/authoring/features/responsive-layout.md) och dess komponenter baserat på den valda enheten.

Sidan ser ut ungefär så här:

![Exempel på mobiler](/help/sites-cloud/authoring/assets/mobile.png)

>[!NOTE]
>
>Emulatorerna inaktiveras när en sida på författarinstansen begärs från en mobilenhet.
