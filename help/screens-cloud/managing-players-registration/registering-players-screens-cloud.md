---
title: Registrerar spelare på skärmar as a Cloud Service
description: Den här sidan beskriver hur du registrerar spelare på skärmar as a Cloud Service.
exl-id: 1a0d6b22-71b1-4f3c-acaa-82d8d9c0f81a
source-git-commit: 489cc9963910ba9f94d30906127beb75f9ad37df
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 1%

---

# Registrerar spelare på skärmar as a Cloud Service {#registering-players-screens-cloud}

När du har installerat och konfigurerat spelare för skärmar as a Cloud Service måste du registrera spelarna.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du registrerar spelare i Screens Services Provider. Efter läsningen ska du kunna:

* förstå hur man registrerar spelare
* hur man slutför registreringsprocessen från Screens Services Provider

## Steg för att registrera en skärmspelare {#register-players}

När du har installerat spelaren på skärmen as a Cloud Service kan du registrera spelaren från Screens Services Provider.

Följ stegen nedan för att registrera spelaren:

1. Logga in på Screens Services Provider.

1. Navigera till **Registreringskoder** under **Hantering av spelare** från den vänstra navigeringspanelen och klicka på **Skapa kod**.

   >[!NOTE]
   >Om det inte finns några giltiga/utgångna koder klickar du på Skapa kod, anger ett namn för koden och väljer förfalloinställningar enligt dina önskemål.

   ![bild](/help/screens-cloud/assets/player/register-player1.png)

1. Fyll i följande fält i **Skapa en registreringskod** dialogruta:

   ![bild](/help/screens-cloud/assets/player/register-player2.png)

   1. **Registreringskodens namn**: Namn på din registreringskod
   1. **Registreringskoden upphör**: Sista giltighetsdatum för din registreringskod
   1. **Begränsa användning**: Växla knappen för att stänga av användningsgränsen för din registreringskod. Som standard är alternativet Begränsa användning inaktiverat.
   1. **Användningsgräns**: Ange antalet för din användningsgräns

1. Klicka på **Skapa** för att skapa registreringskoden. Spelaren visas med registreringskoden i listan.

   ![bild](/help/screens-cloud/assets/player/register-player3.png)

1. Klicka på värdet under kolumnen **REGISTRERINGSKOD**  om du vill kopiera värdet till Urklipp.

1. Klistra in det här värdet i **Ange kod** i **Spelarregistrering** -fliken i administratörsgränssnittet för AEM Screens Player och klicka på **Registrera**.

   ![bild](/help/screens-cloud/assets/player/register-player4.png)


1. När du har lagt till koden ser du att spelaren nu är registrerad i administratörsgränssnittet för spelaren.

   ![bild](/help/screens-cloud/assets/player/register-player5.png)

1. Den här spelaren visas nu i **Spelare** från den vänstra navigeringspanelen. Koden som visas i Screens Services Provider matchar **Systeminformation** från administratörsgränssnittet under Spelarkod.

   ![bild](/help/screens-cloud/assets/player/register-player6.png)

>[!IMPORTANT]
>**Rekommendation om bästa praxis för säkerhet vid användning av registreringskod
>Det bästa sättet är att begränsa användningen av registreringskoden. Om en registreringskod har komprometterats men har en gräns på 100 registreringar kan angriparen bara registrera upp till det numret, men inte mer. Du kan alltid uppdatera användningsgränsen när registreringskoden har skapats och vissa av kundens spelare har redan registrerats. Om kunden observerar ovanlig registreringsaktivitet för en viss registreringskod kan de sänka gränsen i realtid medan de undersöker och kan öka antalet tillbaka om det var ett falskt larm, utan att det påverkar de spelare som redan är registrerade.


## What&#39;s Next {#whats-next}

Nu när du har installerat och konfigurerat spelaren till molnläge bör du fortsätta att arbeta as a Cloud Service med skärmar genom att nästa gång du granskar dokumentet, [Tilldela spelare till en skärm på skärmar as a Cloud Service](/help/screens-cloud/managing-players-registration/assigning-player-display.md) från Screens Services Provider.
