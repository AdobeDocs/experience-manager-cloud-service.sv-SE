---
title: Ta bort externa beroenden för befintliga installationer
description: Ta bort externa beroenden för befintliga installationer
feature: Integrations
exl-id: 5b28ce97-2719-47b8-a386-77d4aaddbe81
source-git-commit: b71a78696d4b347c97b077d84b455f53a1747a07
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Ta bort externa beroenden för befintliga installationer {#remove-external-depedencies}

Adobe rekommenderar att du utför konfigurationssteg för befintliga utökade anslutningsinstallationer för Workfront för att ta bort beroenden till Hoodoos distributionsplatser.

>[!NOTE]
>
>Kör bara konfigurationsstegen om du har installerat den utökade anslutningen för Workfront före mars 2022. Det finns inga beroenden till Hoodoos distributionsplatser för nya utökade anslutningsinstallationer för Workfront från och med mars 2022.

Så här tar du bort externa beroenden:

1. Ta bort följande konfiguration för Hoodoo-databasen från den överordnade `pom.xml`:

   ```XML
     <repository>
        <id>hoodoo-maven</id>
        <name>Hoodoo Repository</name>
        <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
     </repository>
   ```

1. Ta bort följande serverkonfiguration från `settings.xml` fil, tillgänglig på `./cloudmanager/maven/settings.xml`:

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

1. Kör [nya installationssteg](workfront-connector-install.md).
