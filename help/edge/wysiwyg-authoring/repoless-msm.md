---
title: Tillförlitlig hantering av flera platser
description: Lär dig rekommendationer om hur du skapar ett projekt med flerspråkiga webbplatser och utnyttjar en enda kodbas på ett smidigt sätt.
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 02957fb8671d953a683ebd6e168979b11ad391c4
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Tillförlitlig hantering av flera platser {#repoless-msm}

I det här dokumentet förutsätts att du redan har skapat en basplats för ditt projekt med namnet `my-aem-site` och du vill lokalisera den med AEM MSM-funktion.

Om du redan har konfigurerat ditt projekt för problemfri användning tilldelas molnkonfigurationen på rotsidans nivå, `/content/my-aem-site`. För flerspråkiga platser måste den här konfigurationstilldelningen ändras till språkroten, till exempel `/content/my-aem-site/language-master/de`.

