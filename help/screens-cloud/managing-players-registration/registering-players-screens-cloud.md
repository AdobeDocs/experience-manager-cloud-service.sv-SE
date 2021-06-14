---
title: Registrera spelare i skärmar som en Cloud Service
description: På den här sidan beskrivs hur du registrerar spelare i skärmar som en Cloud Service.
hide: true
hidefromtoc: true
index: false
source-git-commit: c65eeaf74ddfd81d37eb7090b84c8bf6f876dc72
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---


# Registrerar spelare i skärmar som en Cloud Service {#registering-players-screens-cloud}

När du har installerat och konfigurerat spelare för skärmar som Cloud Service måste du registrera spelarna.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du registrerar spelare i Screens Services Provider. När du har läst bör du:

* Lär dig hur du registrerar spelare.
* Hantera era kanaler i ett AEM Screens-projekt utifrån deras omfattning.

## Steg för att registrera en skärmspelare {#register-players}

När du har installerat spelaren på skärmar som Cloud Service kan du registrera spelaren från Screens Services Provider.

Följ stegen nedan för att registrera spelaren:

1. Logga in på Screens Services Provider.

1. Navigera till **Registreringskoder** under **Hantering av spelare** i den vänstra navigeringspanelen och klicka på **Skapa kod**.

   >[!NOTE]
   >Om det inte finns några giltiga/utgångna koder klickar du på Skapa kod, anger ett namn för koden och väljer förfalloinställningar enligt dina önskemål.

   ![bild](/help/screens-cloud/assets/player/register-player1.png)

1. Fyll i följande fält i dialogrutan **Skapa en registreringskod**:

   ![bild](/help/screens-cloud/assets/player/register-player2.png)

   1. **Registreringskodens namn**: Namn på din registreringskod
   1. **Registreringskoden upphör**: Sista giltighetsdatum för din registreringskod
   1. **Begränsa användning**: Växla knappen för att stänga av användningsgränsen för din registreringskod. Som standard är alternativet Begränsa användning inaktiverat.
   1. **Användningsgräns**: Ange antalet för din användningsgräns

1. Klicka på **Skapa** för att skapa registreringskoden. Spelaren visas med registreringskoden i listan.

   ![bild](/help/screens-cloud/assets/player/register-player3.png)

1. Klicka på värdet under kolumnen **REGISTRERINGSKOD** för att kopiera värdet till Urklipp.

1. Klistra in det här värdet i fältet **Ange kod** på fliken **Spelarregistrering** i administratörsgränssnittet för AEM Screens-spelaren och klicka på **Registrera**.

   ![bild](/help/screens-cloud/assets/player/register-player4.png)


1. När du har lagt till koden ser du att spelaren nu är registrerad i administratörsgränssnittet för spelaren.

   ![bild](/help/screens-cloud/assets/player/register-player5.png)

1. Den här spelaren visas nu i **Players** från den vänstra navigeringspanelen. Koden som visas i skärmtjänstprovidern matchar panelen **Systeminformation** i administratörsgränssnittet under Spelarkod.

   ![bild](/help/screens-cloud/assets/player/register-player6.png)

