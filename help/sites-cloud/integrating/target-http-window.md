---
title: Adobe AEM Target HTTP Window
description: 'Adobe AEM Target HTTP Window '
translation-type: tm+mt
source-git-commit: c193b38718622cd2e960a8e8833c2d295822dc33
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 2%

---


# Introduktion {#introduction}

Den här sidan beskriver de konfigurerbara parametrarna som finns i HTTP-fönstret i Adobe AEM.

## Parametrar {#parameters}

![HTTP-målfönster för ](assets/httpwindow.png "WindowTarget")

Fönstret innehåller följande konfigurerbara parametrar:

| Parameter | Beskrivning |
|---|---|
| Adobe Target API-URL | URL:en för Adobe Target API. |
| Aktivera absolut URL | Avgör om värddelen av URL:en eller den fullständiga URL:en används. Markera kryssrutan om du vill använda den fullständiga (ej förkortade) URL:en. Kryssrutan är som standard inaktiverad. |
| Tidsgräns för anslutning | Tidsgränsen (i millisekunder) tills en anslutning upprättas. Standardvärdet är 60000 millisekunder. Värdet 0 tolkas som en oändlig timeout. |
| Tidsgräns för socket | Tidsgränsen (i millisekunder) för att vänta på data eller en maximal inaktivitetsperiod mellan två på varandra följande datapaket. Standardvärdet är 30000 millisekunder. |
| Adobe Target Recommendations URL Replace Regex-token | Kontrollerar den token i Adobe Target-slutpunkts-URL som måste ersättas för att peka på målrekommendations-API:ns URL. |
| Adobe Target Recommendations URL Ersätt med token | Ersättning för regex som beskrivs i ovanstående parameter, så den resulterande URL:en pekar på API:t för målrekommendationer. |
