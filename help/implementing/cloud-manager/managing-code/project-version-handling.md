---
title: Versionshantering för Maven Project
description: För testnings- och produktionsdistributioner av AEM as a Cloud Service genererar Cloud Manager en unik, stegvis version.
exl-id: 658bcbed-0733-45da-a3e3-9a5f817099c5
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 3%

---


# Versionshantering för Maven Project {#maven-project-version-handling}

För testnings- och produktionsdistributioner av AEM as a Cloud Service genererar Cloud Manager en unik, stegvis version

Den här versionen visas på [informationssida om pipeline-körning](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) samt aktivitetssidan. När ett bygge körs uppdateras Maven-projektet till att använda den här versionen och en tagg skapas i Git-databasen med den versionen som namn.

Om den ursprungliga projektversionen uppfyller vissa kriterier kommer den uppdaterade projektversionen från Maven att sammanfoga både den ursprungliga projektversionen och den version av Cloud Manager som genererats. Men taggen använder alltid den genererade versionen. För att sammanfogningen ska ske måste den ursprungliga projektversionen ha exakt tre versionssegment, till exempel `1.0.0` eller `1.2.3`, men inte `1.0` eller `1`och originalversionen får inte sluta med `-SNAPSHOT`.

>[!IMPORTANT]
>
>Detta ursprungliga projektversionsvärde måste anges statiskt i `<version>` element på den översta nivån `pom.xml` i Git-databasgrenen.

Om den ursprungliga versionen uppfyller dessa villkor läggs den genererade versionen till i den ursprungliga versionen som ett nytt versionssegment. Den genererade versionen kommer också att ändras något för att inkludera korrekt sortering och versionshantering. Anta till exempel att en genererad version av `2019.926.121356.0000020490` skulle få följande resultat.

| Version | Version in `pom.xml` | Kommentar |
|---|---|---|
| `1.0.0` | `1.0.0.2019_0926_121356_0000020490` | Rätt formaterad originalversion |
| `1.0.0-SNAPSHOT` | `2019.926.121356.0000020490` | ögonblicksbildsversion, överskriven |
| `1` | `2019.926.121356.0000020490` | Ofullständig version, överskriven |

>[!NOTE]
>
>Oavsett om originalversionen är inbyggd i den Cloud Manager-initierade versionen eller inte är originalversionen tillgänglig som en Maven-egenskap med namnet `cloudManagerOriginalVersion`.
