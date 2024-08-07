---
title: Vilka är de kända problemen och begränsningarna med AEM Forms as a Cloud Service?
description: Kända fel och begränsningar i den as a Cloud Service miljön  [!DNL AEM Forms] .
contentOwner: khsingh
role: Admin, Developer, User
feature: Adaptive Forms
topic: Administration
exl-id: 871f294d-f251-4966-a021-39df65b613f0
source-git-commit: 527c9944929c28a0ef7f3e617ef6185bfed0d536
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Kända fel och begränsningar {#known-issues-and-limitations}

Innan du börjar använda [!DNL AEM Forms] as a Cloud Service bör du granska följande kända problem och begränsningar:

## Kända fel {#known-issues}

* Lägg inte till och kör ett test som skickar ett adaptivt formulär från en publiceringsinstans till ett AEM arbetsflöde som körs på en Author-instans förrän du får mer information.

* När du importerar ett adaptivt formulär som använder en mall som innehåller knappen **[!UICONTROL Save]** fortsätter knappen **[!UICONTROL Save]** att visas i det adaptiva formuläret även efter att det har tagits bort från motsvarande mall. Ta bort knappen **[!UICONTROL Save]** från din adaptiva Forms innan du publicerar den. Håll ett öga på versionsinformationen om att Forms Portal och Spara som är en utkastfunktion är tillgängliga för att återställa och använda knappen.

* **[!UICONTROL Set variable]**-steget i AEM arbetsflöden stöder inte variabler av typen matrislista. Du kan använda processsteget för att ange variabler för typmatrislistan.

* När du skickar ett adaptivt formulär som innehåller ett standardfält för överföring av HTML från en Apple iOS-enhet skickas inte filens innehåll och en 0 byte-fil tas emot i den andra änden. Problemet inträffar då och då endast när synkron överföring används. Detta är ett [känt fel](https://feedbackassistant.apple.com/feedback/9117687) i Apple iOS.

* När du skickar ett formulär som innehåller ett standardfält för överföring av HTML från en Apple iOS-enhet skickas ibland inte filens innehåll och en 0 byte-fil tas emot i den andra änden. Detta är ett känt problem i Apple iOS. [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

* AEM Forms as a Cloud Service genererar inga miniatyrbilder för XDP- och JSON-schemafiler. I tjänsten visas standardikoner i stället för miniatyrbilder.

  ![Problem med Forms-miniatyrbild](/help/forms/assets/forms-tumbnail-known-issue.png)

* När du använder ett schema med repeterbara element för att skapa en Core Components-baserad Adaptive Form fungerar inte alternativet att dra och släppa repeterbara element från datamodellträdet i den adaptiva Forms Editor.

## Begränsningar {#limitations}

* Stöd för XFA-baserad Adaptive Forms finns inte direkt tillgängligt. Om du tänker använda XFA-baserad Adaptive Forms kontaktar du Adobe Support med information om ditt användningsfall och specifika krav.

