---
title: Publicera innehåll med den universella visuella redigeraren
description: Lär dig hur den universella Visual Editor publicerar innehåll och hur dina appar kan hantera det publicerade innehållet.
source-git-commit: 7eeebade0255263a240476bc32f9530574495751
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Publicera innehåll med den universella visuella redigeraren {#publishing}

Lär dig hur den universella Visual Editor publicerar innehåll och hur dina appar kan hantera det publicerade innehållet.

## Likheter med AEM {#similarities}

För användare av AEM fungerar processen att publicera innehåll med den universella visuella redigeraren som du är van vid: När innehållet publiceras i AEM replikeras det från författarnivån till publiceringsnivån.

## Skillnader {#differences}

Det som gör publiceringen med den universella Visual Editor lite annorlunda är inte så mycket själva redigeraren, utan snarare den externa värdtjänsten för appen som den universella redigeraren gör möjlig.

När det finns en extern värd är det webappens sak att se till att innehåll läses in från författarnivån när appen öppnas av författare i redigeraren, och att det läses in från publiceringsnivån när besökarna öppnar appen.

## Identifiera nivån i appen {#detecting}

Du kan avgöra om författaren eller publiceringsnivån ska ha åtkomst genom att använda en enkel villkorssats i appen för att välja rätt författare eller publiceringsslutpunkt när du upptäcker att appen öppnas i redigeraren.

Ett annat alternativ är att distribuera appen till två olika miljöer som är konfigurerade på olika sätt, så att innehållet hämtas från författarnivån och en som hämtar det från publiceringsnivån. För att författare ska kunna öppna den publicerade URL:en i Universell redigerare kan ett litet skript skapas för att&quot;konvertera&quot; URL:en för publiceringssidan till motsvarande URL:er i författarmiljön (t.ex. genom att föregå en `author` underdomän) så att författarna omdirigeras automatiskt.

## Sammanfattning {#summary}

Målet för den universella redigeraren är att inte införa något visst mönster, så att implementeringen bäst kan uppnå sina mål på ett helt fristående sätt samtidigt som allt förblir enkelt och rakt framåt för implementeringen.

Det finns heller inga krav på hur ett visst projekt ska gå till för att avgöra från vilken nivå innehållet ska levereras. Det ger snarare ett antal möjligheter och låter projektet avgöra vilken lösning som är bäst för sina egna behov.
