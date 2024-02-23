---
title: Skapa en sida för mobila enheter
description: När du skapar för mobilen kan du växla mellan flera emulatorer för att se vad slutanvändaren ser
exl-id: fabd4468-3304-402f-9522-342da3bbae94
source-git-commit: a868bf4d4acf4fbae7ccaf55b03319ba0617f9a4
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Skapa en sida för mobila enheter {#authoring-a-page-for-mobile-devices}

Adobe Experience Manager sidor baseras på en responsiv layout. [Responsiv layout](/help/sites-cloud/authoring/page-editor/responsive-layout.md) anpassar innehållet automatiskt så att det passar målenheten och eliminerar behovet av att skapa innehåll för specifika enheter.

När du skapar en mobilsida visas sidan på ett sätt som emulerar den mobila enheten. När du redigerar sidan kan du växla mellan flera emulatorer för att se vad slutanvändaren ser när han/hon öppnar sidan.

Enheterna grupperas i kategorierna, funktion, smart och touchfunktion enligt enhetens funktioner för att återge en sida. När slutanvändaren öppnar en mobilsida upptäcker AEM enheten och skickar den representation som motsvarar enhetsgruppen.

>[!NOTE]
>
>Om du vill skapa en mobilwebbplats baserad på en befintlig standardwebbplats skapar du en live-kopia av standardwebbplatsen. Se [Skapa Live-kopior](/help/sites-cloud/administering/msm/creating-live-copies.md).
>
>AEM kan skapa nya enhetsgrupper. Se Skapa enhetsgruppsfilter.

<!--
>AEM developers can create new device groups. (See [Creating Device Group Filters](/help/sites-developing/groupfilters.md).)
-->

Använd följande procedur för att skapa en mobilsida:

1. Öppna **Webbplatser** konsol.
1. Redigera en innehållssida.
1. Växla till önskad emulator genom att klicka på **Emulator** ikonen längst upp på sidan.

   ![Emulatorikon](/help/sites-cloud/authoring/assets/emulator.png)

1. Dra och släpp komponenter från komponentwebbläsaren eller resursläsaren till sidan.
1. [Ändra responsiv layout](/help/sites-cloud/authoring/page-editor/responsive-layout.md) av sidan och dess komponenter baserat på den valda enheten.

Sidan ser ut ungefär så här:

![Exempel på mobiler](/help/sites-cloud/authoring/assets/mobile.png)

>[!NOTE]
>
>Emulatorerna inaktiveras när en sida på författarinstansen begärs från en mobilenhet.
