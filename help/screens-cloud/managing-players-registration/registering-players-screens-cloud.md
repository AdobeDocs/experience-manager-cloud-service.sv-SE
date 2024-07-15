---
title: Registrera spelare i Screens as a Cloud Service
description: På den här sidan beskrivs hur du registrerar spelare i Screens as a Cloud Service.
exl-id: 1a0d6b22-71b1-4f3c-acaa-82d8d9c0f81a
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# Registrera spelare i Screens as a Cloud Service {#registering-players-screens-cloud}

När du har installerat och konfigurerat spelare för Screens as a Cloud Service måste du registrera spelarna.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du registrerar spelare i Screens Services Provider. Efter läsningen ska du kunna:

* förstå hur man registrerar spelare
* Hur man slutför registreringsprocessen från Screens tjänsteleverantör

## Steg för att registrera en Screens Player {#register-players}

När du har installerat spelaren på Screens as a Cloud Service kan du registrera spelaren från Screens tjänsteleverantör.

Registrera spelaren genom att följa stegen nedan:

1. Logga in på Screens Services Provider.

1. Navigera till **Registreringskoder** under **Hantering av spelare** i den vänstra navigeringspanelen och klicka på **Skapa kod**.

   >[!NOTE]
   >Om det inte finns några giltiga/utgångna koder klickar du på Skapa kod, anger ett namn för koden och väljer förfalloinställningar enligt dina önskemål.

   ![bild](/help/screens-cloud/assets/player/register-player1.png)

1. Fyll i följande fält i dialogrutan **Skapa en registreringskod**:

   ![bild](/help/screens-cloud/assets/player/register-player2.png)

   1. **Registreringskodnamn**: Namn på din registreringskod
   1. **Registreringskoden upphör**: Sista giltighetsdatum för din registreringskod
   1. **Begränsa användning**: Växla knappen för att stänga av användningsgränsen för din registreringskod. Som standard är alternativet Begränsa användning inaktiverat.
   1. **Användningsgräns**: Välj antalet för din användningsgräns

1. Klicka på **Skapa** för att skapa registreringskoden. Du kan se din spelare med registreringskoden i listan.

   ![bild](/help/screens-cloud/assets/player/register-player3.png)

1. Klicka på värdet under kolumnen **REGISTRERINGSKOD** för att kopiera värdet till Urklipp.

1. Klistra in det här värdet i fältet **Ange kod** på fliken **Spelarregistrering** i administratörsgränssnittet för AEM Screens-spelaren och klicka på **Registrera**.

   ![bild](/help/screens-cloud/assets/player/register-player4.png)


1. När du har lagt till koden kan du se att spelaren nu är registrerad från spelarens administratörsgränssnitt.

   ![bild](/help/screens-cloud/assets/player/register-player5.png)

1. Den här spelaren visas nu i **Spelare** från den vänstra navigeringspanelen. Koden som visas i Screens Services Provider matchar panelen **Systeminformation** från Admin-gränssnittet under Player-kod.

   ![bild](/help/screens-cloud/assets/player/register-player6.png)

   >[!IMPORTANT]
   >**Rekommendation om bästa praxis för säkerhet vid användning av registreringskod**
   >Det bästa sättet är att begränsa användningen av registreringskoden. Om en registreringskod har komprometterats men har en gräns på 100 registreringar kan angriparen bara registrera upp till det numret, men inte fler. Du kan alltid uppdatera användningsgränsen när registreringskoden har skapats och vissa av kundens spelare har redan registrerats. Om kunden observerar ovanlig registreringsaktivitet för en viss registreringskod kan de sänka gränsen i realtid medan de undersöker och kan öka antalet tillbaka om det var ett falskt larm, utan att det påverkar de spelare som redan är registrerade.


## What&#39;s Next {#whats-next}

Nu när du har installerat och konfigurerat spelaren till molnläge bör du fortsätta din Screens as a Cloud Service resa genom att nästa gång du granskar dokumentet [Tilldela spelaren till en skärm i Screens as a Cloud Service](/help/screens-cloud/managing-players-registration/assigning-player-display.md) från Screens Services Provider.
