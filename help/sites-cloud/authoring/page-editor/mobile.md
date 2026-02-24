---
title: Skapa en sida för mobila enheter
description: När du skapar för mobilen kan du växla mellan flera emulatorer för att se vad slutanvändaren ser
badgeSaas: label="AEM Sites" type="Positive" tooltip="Gäller AEM Sites)."
exl-id: fabd4468-3304-402f-9522-342da3bbae94
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 98c0c9b6adbc3d7997bc68311575b1bb766872a6
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---

# Skapa en sida för mobila enheter {#authoring-a-page-for-mobile-devices}

Adobe Experience Manager sidor baseras på en responsiv layout. [Responsiv layout](/help/sites-cloud/authoring/page-editor/responsive-layout.md) anpassar innehållet automatiskt så att det passar målenheten, vilket eliminerar behovet av att skapa innehåll för specifika enheter.

När du skapar en mobilsida visas sidan på ett sätt som emulerar den mobila enheten. När du redigerar sidan kan du växla mellan flera emulatorer för att se vad slutanvändaren ser när han/hon öppnar sidan.

Enheterna grupperas i kategorierna, funktion, smart och touchfunktion enligt enhetens funktioner för att återge en sida. När slutanvändaren kommer åt en mobilsida identifierar AEM enheten och skickar den representation som motsvarar enhetsgruppen.

>[!NOTE]
>
>Om du vill skapa en mobilwebbplats baserad på en befintlig standardwebbplats skapar du en live-kopia av standardwebbplatsen. Se [Skapa live-kopior](/help/sites-cloud/administering/msm/creating-live-copies.md).
>
>AEM-utvecklare kan skapa nya enhetsgrupper. Se Skapa enhetsgruppsfilter.

<!--
>AEM developers can create new device groups. (See [Creating Device Group Filters](/help/sites-developing/groupfilters.md).)
-->

Använd följande procedur för att skapa en mobilsida:

1. Öppna konsolen **Platser** från global navigering.
1. Redigera en innehållssida.
1. Växla till önskad emulator genom att klicka på ikonen **Emulator** längst upp på sidan.

   ![Emulatorikon](/help/sites-cloud/authoring/assets/emulator.png)

1. Dra och släpp komponenter från komponentwebbläsaren eller resursläsaren till sidan.
1. [Ändra den responsiva layouten](/help/sites-cloud/authoring/page-editor/responsive-layout.md) för sidan och dess komponenter baserat på den valda enheten.

Sidan ser ut ungefär så här:

![Mobilexempel](/help/sites-cloud/authoring/assets/mobile.png)

>[!NOTE]
>
>Emulatorerna inaktiveras när en sida på författarinstansen begärs från en mobilenhet.
