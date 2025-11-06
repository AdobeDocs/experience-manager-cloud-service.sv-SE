---
title: Versionshantering för Maven Project
description: Cloud Manager genererar en unik och stegvis version för testnings- och produktionsdistributioner av AEM as a Cloud Service.
exl-id: 658bcbed-0733-45da-a3e3-9a5f817099c5
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Versionshantering för Maven Project {#maven-project-version-handling}

Cloud Manager genererar en unik och stegvis version för driftsättning av AEM as a Cloud Service.

Den här versionen visas på [informationssidan för pipeline-körning](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) och aktivitetssidan. När ett bygge körs uppdateras Maven-projektet till att använda den här versionen och en tagg skapas i Git-databasen med den versionen som namn.

Om den ursprungliga projektversionen uppfyller vissa kriterier kommer den uppdaterade projektversionen från Maven att sammanfoga både den ursprungliga projektversionen och den version av Cloud Manager som genererats. Men taggen använder alltid den genererade versionen. För att den här sammanfogningen ska ske måste den ursprungliga projektversionen ha exakt tre versionssegment, till exempel `1.0.0` eller `1.2.3`, men inte `1.0` eller `1`, och den ursprungliga versionen får inte sluta med `-SNAPSHOT`.

>[!IMPORTANT]
>
>Det här ursprungliga projektversionsvärdet måste anges statiskt i elementet `<version>` i den översta `pom.xml`-filen i Git-databasgrenen.

Om den ursprungliga versionen uppfyller dessa villkor läggs den genererade versionen till i den ursprungliga versionen som ett nytt versionssegment. Den genererade versionen kommer också att ändras något för att inkludera korrekt sortering och versionshantering. Anta att en genererad version av `2019.926.121356.0000020490` skulle få följande resultat.

| Version | Version i `pom.xml` | Kommentar |
|---|---|---|
| `1.0.0` | `1.0.0.2019_0926_121356_0000020490` | Rätt formaterad originalversion |
| `1.0.0-SNAPSHOT` | `2019.926.121356.0000020490` | ögonblicksbildsversion, överskriven |
| `1` | `2019.926.121356.0000020490` | Ofullständig version, överskriven |

>[!NOTE]
>
>Oavsett om originalversionen införlivades i den Cloud Manager-initierade versionen eller inte är originalversionen tillgänglig som en Maven-egenskap med namnet `cloudManagerOriginalVersion`.
