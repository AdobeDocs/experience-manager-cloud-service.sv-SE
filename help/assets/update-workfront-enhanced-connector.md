---
title: Uppdatera [!DNL Workfront for Experience Manager enhanced connector]
description: Uppdatera [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 09276b4d-a7c8-4927-8c0a-40eda48e55a7
source-git-commit: 77aceab8db82082185c931202fc6ea8eee79c11e
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# Uppdatera [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

[!UICONTROL Experience Manager Assets as a Cloud Service] gör att du kan uppdatera [!DNL Workfront for Experience Manager enhanced connector] från en tidigare version till den senaste versionen.

>[!TIP]
>
>Söker du efter [!DNL Workfront for Experience Manager enhanced connector] Vill du uppdatera dokumentationen för AEM 6.5? Klicka [här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=en##update-enhanced-connector-for-workfront).


Så här uppdaterar du [!DNL Workfront for Experience Manager enhanced connector] till den senaste versionen:

1. Hämta den senaste versionen av den förbättrade anslutningen från [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip).

1. [Åtkomst](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) och klona din AEM as a Cloud Service databas från Cloud Manager.

1. Öppna den klonade Experience Manager as a Cloud Service databasen med valfri integrerad utvecklingsmiljö.

1. Placera den utökade ZIP-filen för anslutningen som laddats ned i steg 1 på följande sökväg:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Om `resources` mappen finns inte, skapa mappen.

1. Uppdatera den utökade anslutningsversionen i överordnad `pom.xml`.

   ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version> updated enhanced connector version number</version>
         <scope>system</scope>
         <systemPath>${project.basedir}/ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
   ```

1. Uppdatera beroendet i `all module pom.xml`.

   ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <scope>system</scope>
         <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
   ```

   >[!NOTE]
   >
   >Se till att du lägger till `<scope>` och `<systemPath>` till beroendena i steg 5 och steg 6.

1. Uppdatera `pom.xml` bäddar in. Lägg till [!DNL Workfront for Experience Manager enhanced connector] paket till `embeddeds` i `pom.xml` av alla dina underprojekt. Lägg in uppdateringarna i alla moduler `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   Målet för det inbäddade avsnittet är inställt på `/apps/<path-to-project-install-folder>/install`. Denna JCR-sökväg `/apps/<path-to-project-install-folder>` måste inkluderas i filterreglerna i `all/src/main/content/META-INF/vault/filter.xml` -fil. Filterreglerna för databasen hämtas vanligtvis från programnamnet. Använd namnet på mappen som mål i de befintliga reglerna.

1. [Ta bort beroenden till Hoodoos distributionsplatser](remove-external-dependencies.md), om det finns några.

1. Skicka ändringarna till databasen.

1. Kör pipeline till [distribuera ändringarna till Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).
