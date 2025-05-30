---
title: Uppdatering  [!DNL Workfront for Experience Manager enhanced connector]
description: Uppdatering  [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 09276b4d-a7c8-4927-8c0a-40eda48e55a7
feature: Workfront Integrations and Apps
role: Admin
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Uppdatera [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime och Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets-integrering med Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI-utökningsbarhet</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Aktivera Dynamic Media Prime och Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Sök efter bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Metadata - bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamiska media med OpenAPI-funktioner</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets-dokumentation för utvecklare</b></a>
        </td>
    </tr>
</table>

Med [!UICONTROL Experience Manager Assets as a Cloud Service] kan du uppdatera [!DNL Workfront for Experience Manager enhanced connector] från en tidigare version till den senaste versionen.

>[!TIP]
>
>Söker du efter [!DNL Workfront for Experience Manager enhanced connector] uppdateringsdokumentation för AEM 6.5? Klicka [här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=sv-SE##update-enhanced-connector-for-workfront).


Uppdatera [!DNL Workfront for Experience Manager enhanced connector] till den senaste versionen:

1. Hämta den senaste versionen av den utökade anslutningen från [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip).

1. [Åtkomst](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=sv-SE) och klona din AEM as a Cloud Service-databas från Cloud Manager.

1. Öppna den klonade Experience Manager as a Cloud Service-databasen med valfri integrerad utvecklingsmiljö.

1. Placera den utökade ZIP-filen för anslutningen som laddats ned i steg 1 på följande sökväg:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Skapa mappen om mappen `resources` inte finns.

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
   >Se till att du lägger till `<scope>` och `<systemPath>` i beroendena i steg 5 och steg 6.

1. Uppdatera `pom.xml` inbäddade. Lägg till [!DNL Workfront for Experience Manager enhanced connector]-paketen i avsnittet `embeddeds` i `pom.xml` för alla ditt underprojekt. Inkludera uppdateringarna i alla moduler `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   Målet för det inbäddade avsnittet är `/apps/<path-to-project-install-folder>/install`. Den här JCR-sökvägen `/apps/<path-to-project-install-folder>` måste inkluderas i filterreglerna i filen `all/src/main/content/META-INF/vault/filter.xml`. Filterreglerna för databasen hämtas vanligtvis från programnamnet. Använd namnet på mappen som mål i de befintliga reglerna.

1. [Ta bort eventuella beroenden för Hoodoo-distributionsplatser](remove-external-dependencies.md).

1. Överför ändringarna till databasen.

1. Kör pipelinen för att [distribuera ändringarna till Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=sv-SE).
