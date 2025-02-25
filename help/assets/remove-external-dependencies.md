---
title: Ta bort externa beroenden för befintliga installationer
description: Ta bort externa beroenden för befintliga installationer
feature: Workfront Integrations and Apps
exl-id: 5b28ce97-2719-47b8-a386-77d4aaddbe81
role: Admin
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Ta bort externa beroenden för befintliga installationer {#remove-external-depedencies}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Adobe rekommenderar att du utför konfigurationssteg för befintliga utökade anslutningsinstallationer för Workfront för att ta bort beroenden till Hoodoos distributionsplatser.

>[!NOTE]
>
>Kör bara konfigurationsstegen om du har installerat den utökade anslutningen för Workfront före mars 2022. Det finns inga beroenden till Hoodoos distributionsplatser för nya utökade anslutningsinstallationer för Workfront från mars 2022.

Så här tar du bort externa beroenden:

1. Ta bort följande konfiguration för Hoodoo-databas från den överordnade `pom.xml`:

   ```XML
     <repository>
        <id>hoodoo-maven</id>
        <name>Hoodoo Repository</name>
        <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
     </repository>
   ```

1. Ta bort följande serverkonfiguration från filen `settings.xml` som är tillgänglig på `./cloudmanager/maven/settings.xml`:

   ```XML
         <server>
            <id>hoodoo-maven</id>
            <configuration>
               <httpHeaders>
                     <property>
                        <name>Deploy-Token</name>
                        <value>xxxxxxxxxxxxxxxx</value>
                     </property>
               </httpHeaders>
            </configuration>
         </server>
   ```

1. Kör de [nya installationsstegen](workfront-connector-install.md).
