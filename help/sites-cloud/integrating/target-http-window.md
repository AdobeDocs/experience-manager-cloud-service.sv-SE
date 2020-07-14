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

På den här sidan beskrivs de konfigurerbara parametrarna i Adobe AEM Target HTTP Window.

## Parametrar {#parameters}

![Target HTTP](assets/httpwindow.png "WindowTarget HTTP Window")

Fönstret innehåller följande konfigurerbara parametrar:

| Parameter | Beskrivning |
|---|---|
| Adobe Target API-URL | URL:en för Adobe Target-API:t. |
| Aktivera absolut URL | Avgör om värddelen av URL:en eller den fullständiga URL:en används. Markera kryssrutan om du vill använda den fullständiga (ej förkortade) URL:en. Kryssrutan är som standard inaktiverad. |
| Tidsgräns för anslutning | Tidsgränsen (i millisekunder) tills en anslutning upprättas. Standardvärdet är 60000 millisekunder. Värdet 0 tolkas som en oändlig timeout. |
| Tidsgräns för socket | Tidsgränsen (i millisekunder) för att vänta på data eller en maximal inaktivitetsperiod mellan två på varandra följande datapaket. Standardvärdet är 30000 millisekunder. |
| Adobe Target Recommendations URL Replace Regex Token | Styr den token i Adobe Target-slutpunkts-URL som måste ersättas för att peka på Target Recommandations API-URL:en. |
| URL-ersättning för Adobe Target Recommendations med token | Ersättning för regex som beskrivs i ovanstående parameter, så den resulterande URL:en pekar på Target Recommandations API. |
