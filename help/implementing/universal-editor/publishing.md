---
title: Publicera innehåll med den universella redigeraren
description: Lär dig hur den universella redigeraren publicerar innehåll och hur dina appar kan hantera det publicerade innehållet.
exl-id: aee34469-37c2-4571-806b-06c439a7524a
source-git-commit: 79fe3133a6b0553209b14c4cf47faa9db28caacc
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---


# Publicera innehåll med den universella redigeraren {#publishing}

Lär dig hur den universella redigeraren publicerar innehåll och hur dina appar kan hantera det publicerade innehållet.

## Likheter med AEM {#similarities}

För användare av AEM fungerar processen att publicera innehåll med den universella redigeraren som du är van vid: vid publicering i AEM replikeras innehållet från författarnivån till publiceringsnivån.

## Skillnader {#differences}

Det som gör publicering med den universella redigeraren lite annorlunda är inte så mycket själva redigeraren, utan snarare den externa värdfunktionen för appen som den universella redigeraren gör möjlig.

När det finns en extern värd är det webappens sak att se till att innehåll läses in från författarnivån när appen öppnas av författare i redigeraren, och att det läses in från publiceringsnivån när besökarna öppnar appen.

## Identifiera nivån i appen {#detecting}

Du kan avgöra om författaren eller publiceringsnivån ska ha åtkomst genom att använda en enkel villkorssats i appen för att välja rätt författare eller publiceringsslutpunkt när du upptäcker att appen öppnas i redigeraren.

Ett annat alternativ är att distribuera appen till två olika miljöer som är konfigurerade på olika sätt, så att innehållet hämtas från författarnivån och en som hämtar det från publiceringsnivån. För att författare ska kunna öppna den publicerade URL:en i Universell redigerare kan ett litet skript skapas för att&quot;konvertera&quot; URL:en för publiceringssidan till motsvarande URL:er i författarmiljön (t.ex. genom att föregå en `author` underdomän) så att författarna omdirigeras automatiskt.

## Sammanfattning {#summary}

Målet för den universella redigeraren är att inte införa något visst mönster, så att implementeringen bäst kan uppnå sina mål på ett helt fristående sätt samtidigt som allt förblir enkelt och rakt framåt för implementeringen.

Det finns heller inga krav på hur ett visst projekt ska gå till för att avgöra från vilken nivå innehållet ska levereras. Det ger snarare ett antal möjligheter och låter projektet avgöra vilken lösning som är bäst för sina egna behov.
