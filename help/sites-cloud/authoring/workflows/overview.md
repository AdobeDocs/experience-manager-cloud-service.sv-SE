---
title: Arbeta med arbetsflöden
description: Med arbetsflöden i AEM kan du automatisera en serie steg som utförs på en sida eller en resurs.
exl-id: ed157646-abb3-45c6-bafd-7889bd93fdf3
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 7%

---

# Arbeta med arbetsflöden {#working-with-workflows}

AEM arbetsflöden gör att du kan automatisera en serie steg som utförs på (en eller flera) sidor och/eller resurser.

Vid publicering måste till exempel en redigerare granska innehållet innan en webbplatsadministratör aktiverar sidan. Ett arbetsflöde som automatiserar det här exemplet meddelar varje deltagare när det är dags att utföra det arbete de behöver:

1. Författaren tillämpar arbetsflödet på sidan.
1. Redigeraren får ett arbetsobjekt som anger att de måste granska sidinnehållet. När de är klara anger de att deras arbetsuppgifter är slutförda.
1. Webbplatsadministratören får sedan ett arbetsobjekt som begär att sidan aktiveras. När de är klara anger de att deras arbetsuppgifter är slutförda.

Vanligtvis:

* Innehållsförfattare använder arbetsflöden både på sidor och i arbetsflöden.
* De arbetsflöden du använder är specifika för organisationens affärsprocesser.

Följande sidor omfattar:

* [Använda arbetsflöden på sidor](/help/sites-cloud/authoring/workflows/applying.md)
* [Delta i arbetsflöden](/help/sites-cloud/authoring/workflows/participating.md)
