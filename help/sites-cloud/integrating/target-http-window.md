---
title: Adobe AEM Target HTTP Window
description: Adobe AEM Target HTTP Window
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 1%

---


# Introduktion {#introduction}

Den här sidan beskriver de konfigurerbara parametrarna som finns i HTTP-fönstret i Adobe AEM.

## Parametrar {#parameters}

![Mål-HTTP-fönster](assets/httpwindow.png "Mål-HTTP-fönster")

Fönstret innehåller följande konfigurerbara parametrar:

| Parameter | Beskrivning |
|---|---|
| Adobe Target API-URL | URL:en för Adobe Target API. |
| Aktivera absolut URL | Avgör om värddelen av URL:en eller den fullständiga URL:en används. Markera kryssrutan om du vill använda den fullständiga (ej förkortade) URL:en. Kryssrutan är som standard inaktiverad. |
| Tidsgräns för anslutning | Tidsgränsen (i millisekunder) tills en anslutning upprättas. Standardvärdet är 60000 millisekunder. Värdet 0 tolkas som en oändlig timeout. |
| Tidsgräns för socket | Tidsgränsen (i millisekunder) för att vänta på data eller en maximal inaktivitetsperiod mellan två på varandra följande datapaket. Standardvärdet är 30000 millisekunder. |
| Adobe Target Recommendations URL Replace Regex-token | Kontrollerar den token i Adobe Target-slutpunkts-URL som måste ersättas för att peka på målrekommendations-API:ns URL. |
| Adobe Target Recommendations URL Ersätt med token | Ersättning för regex som beskrivs i ovanstående parameter, så den resulterande URL:en pekar på API:t för målrekommendationer. |
