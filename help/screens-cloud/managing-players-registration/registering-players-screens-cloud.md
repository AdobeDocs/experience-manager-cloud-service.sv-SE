---
title: Registrera spelare i skärmar som en Cloud Service
description: På den här sidan beskrivs hur du registrerar spelare i skärmar som en Cloud Service.
source-git-commit: b9b27c09b1f4a1799a8c974dfb846295664be998
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---


# Registrera spelare i skärmar som en Cloud Service {#registering-players-screens-cloud}

När du har installerat och konfigurerat spelare för skärmar som Cloud Service måste du registrera spelarna.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du registrerar spelare i Screens Services Provider. Efter läsningen ska du kunna:

* förstå hur man registrerar spelare
* hur man slutför registreringsprocessen från Screens Services Provider

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

## What&#39;s Next {#whats-next}

Nu när du har installerat och konfigurerat spelaren i molnläge bör du fortsätta att använda skärmar som en Cloud Service genom att nästa gång du granskar dokumentet [Tilldela spelaren till en skärm i skärmar som en Cloud Service](/help/screens-cloud/managing-players-registration/assigning-player-display.md) från leverantören av skärmar.