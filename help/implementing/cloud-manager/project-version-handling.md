---
title: Versionshantering för Maven Project
description: Versionshantering för Maven Project - Cloud Services
exl-id: 658bcbed-0733-45da-a3e3-9a5f817099c5
source-git-commit: 4761d93fe4fc186dd92ba897f62b8de967d8b890
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 5%

---

# Versionshantering för Maven Project {#maven-project-version-handling}


## Om versionshantering för Maven-projekt {#understanding-project-version}

För driftsättningar på scen- och produktionsstadier genererar Cloud Manager en unik, stegvis version.

Den här versionen visas både på sidan med information om pipeline-körning och på aktivitetssidan. När ett bygge körs uppdateras Maven-projektet till att använda den här versionen och en tagg skapas i Git-databasen med den versionen som namn.

Om den ursprungliga projektversionen uppfyller vissa kriterier kommer den uppdaterade projektversionen från Maven att sammanfoga både den ursprungliga projektversionen och den version av Cloud Manager som genererats. Men taggen använder alltid den genererade versionen. För att sammanfogningen ska ske måste den ursprungliga projektversionen ha exakt tre versionssegment, till exempel 1.0.0 eller 1.2.3, men inte 1.0 eller 1, och den ursprungliga versionen får inte sluta med -SNAPSHOT.

>[!NOTE]
>Detta ursprungliga projektversionsvärde måste anges statiskt i elementet `<version>` för filen `pom.xml` på den översta nivån i Git-databasgrenen.

Om originalversionen uppfyller det här villkoret läggs den genererade versionen till i originalversionen som ett nytt versionssegment. Den genererade versionen kommer också att ändras något för att inkludera korrekt sortering och versionshantering. Om du till exempel antar en genererad version av 2019.926.121356.000020490:

| **Version** | **version i pom.xml** | **Kommentar** |
|---|---|---|
| 1.0.0 | 1.0.0.2019_0926_121356_000020490 | Rätt formaterad originalversion |
| 1.0.0-ÖGONBLICKSBILD | 2019.926.121356.000020490 | ögonblicksbildsversion, överskriven |
| 1 | 2019.926.121356.000020490 | Ofullständig version, överskriven |

>[!NOTE]
>
>Oavsett om den ursprungliga versionen har integrerats i den Cloud Manager-initierade versionen eller inte är den ursprungliga versionen tillgänglig som en Maven-egenskap med namnet *cloudManagerOriginalVersion.*
