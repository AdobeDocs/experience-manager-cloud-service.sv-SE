---
title: Kända fel och begränsningar
description: Kända fel och begränsningar i  [!DNL AEM Forms] as a Cloud Service miljö
contentOwner: khsingh
role: User, Developer
level: Intermediate
topic: Administration
exl-id: 871f294d-f251-4966-a021-39df65b613f0
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# Kända fel och begränsningar {#known-issues-and-limitations}

Innan du börjar använda [!DNL AEM Forms] as a Cloud Service kan du läsa om följande kända problem och begränsningar:

## Kända fel {#known-issues}

* Lägg inte till och kör ett test som skickar ett adaptivt formulär från en publiceringsinstans till ett AEM arbetsflöde som körs på en Author-instans förrän du får mer information.

* När du importerar ett adaptivt formulär som använder en mall som innehåller **[!UICONTROL Save]** knappen **[!UICONTROL Save]** knappen fortsätter att visas i det adaptiva formuläret även efter att det har tagits bort från motsvarande mall. Ta bort **[!UICONTROL Save]** från din adaptiva Forms innan den publiceras. Håll ett öga på versionsinformationen om att Forms Portal och Spara som är en utkastfunktion är tillgängliga för att återställa och använda knappen.

* The **[!UICONTROL Set variable]** AEM arbetsflöden stöder inte variabler av typen matrislista. Du kan använda processsteget för att ange variabler för typmatrislistan.

* När du skickar ett adaptivt formulär som innehåller ett standardfält för överföring av HTML från en Apple iOS-enhet skickas inte filens innehåll och en 0 byte-fil tas emot i den andra änden. Problemet inträffar då och då endast när synkron överföring används. Det här är en [känt problem](https://feedbackassistant.apple.com/feedback/9117687) i Apple iOS.

* När du skickar ett formulär som innehåller ett standardfält för överföring av HTML från en Apple iOS-enhet skickas ibland inte filens innehåll och en 0 byte-fil tas emot i den andra änden. Detta är ett känt problem i Apple iOS. [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)


## Begränsningar {#limitations}

* Stöd för XFA-baserad Adaptive Forms finns inte direkt tillgängligt. Om du tänker använda XFA-baserad Adaptive Forms kontaktar du Adobe Support med information om ditt användningsfall och specifika krav.

