---
title: Installera [!DNL Workfront for Experience Manager enhanced connector]
description: Installera [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---

# Installera [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |

En användare med administratörsåtkomst i [!DNL Adobe Experience Manager] som [!DNL Cloud Service] installerar den utökade anslutningen. Granska plattformsstödet och andra [krav för anslutningen](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience) innan du installerar.

>[!IMPORTANT]
>
>Från juni 2022 släppte Adobe en ny inbyggd integrering för att ansluta Workfront till Adobe Experience Manager Assets as a Cloud Service. Den här integreringen har blivit den metod som krävs för att ansluta dessa två lösningar. Eventuella framtida nya implementeringar av den förbättrade anslutningen (1.9.8 och senare) för att ansluta Workfront till AEM Assets as a Cloud Service blockeras. Mer information om hur du konfigurerar den här integreringen finns i [Konfigurera Experience Manager Assets as a Cloud Service-integreringen](workfront-connector-configure.md).

>[!IMPORTANT]
>
>* Adobe kräver att [!DNL Adobe Workfront for Experience Manager enhanced connector] distribueras och konfigureras endast via certifierade partners eller [!DNL Adobe Professional Services]. Om den distribueras och konfigureras utan en certifierad partner eller [!DNL Adobe Professional Services] stöds den inte av Adobe.
>
>* Adobe kan släppa uppdateringar av [!DNL Adobe Workfront] och [!DNL Adobe Experience Manager] som gör den här kopplingen överflödig. Om detta inträffar kan kunderna behöva gå över från att använda den här anslutningen.
>
>* Adobe har stöd för utökade anslutningsversioner 1.7.4 och senare. Tidigare förhandsversioner och anpassade versioner stöds inte. Om du vill kontrollera den utökade anslutningsversionen läser du steg 5(a) i [de förbättrade installationsanvisningarna för anslutningsprogrammet](workfront-connector-install.md).
>
>* Se [Partnercertifieringsprov för Workfront för Experience Manager Assets förbättrade anslutningsprogram](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Mer information om provet finns i [Handbok för prov](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

Innan du installerar anslutningsprogrammet följer du de här förinstallationsstegen:

1. Om ditt AEM as a Cloud Service-program har konfigurerat Advanced Networking och aktiverat IP Allow-Listing måste du lägga till Workfront IP-adresser i denna allow-list för att tillåta att händelseprenumerationer och olika API-anrop skickas till AEM.

   * [IP-adresser för Workfront-kluster](https://experienceleague.adobe.com/docs/workfront/using/administration-and-setup/get-started-administration/configure-your-firewall.html?lang=sv-SE#ip-addresses-to-allow-for-clusters-1-2-3-5-7-8-and-9). Om du vill känna till IP-klustret i [!DNL Workfront] går du till **[!UICONTROL Setup]** > **[!UICONTROL System]** > **[!UICONTROL Customer Info]**.

   * [API:er för Workfront Event Subscription ](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-api/event-subscriptions/event-subs-api.html?lang=sv-SE)

   >[!IMPORTANT]
   >
   >* Om du har konfigurerat Advanced Networking för ditt program och använder IP Allow Listing, måste du på grund av en begränsning i den förbättrade Workfront Connector-arkitekturen lägga till programmets IP-adress i listan över tillåtna i Cloud Manager.
   >
   >* p{PROGRAM_ID}.external.adobeaemcloud.com
   >
   >* Om du vill hitta programmets IP-adress öppnar du ett terminalfönster och kör ett kommando, till exempel:
   >
   >    ```
   >    dscacheutil -q host -a name p{PROGRAM_ID}.external.adobeaemcloud.com
   >    
   >    ```

1. Kontrollera att följande övertäckningar inte finns i databasen [!DNL Experience Manager]. Om du har befintliga övertäckningar på de här banorna måste du antingen ta bort övertäckningarna eller sammanfoga ändringarna mellan dem:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`
   * `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

1. Den här installationen kräver kunskap för att ställa in ett Maven-projekt i [!DNL Experience Manager] som [!DNL Cloud Service]. Använd följande resurser för att lära dig hur du inkluderar ett tredjepartspaket i ditt Maven-projekt:

   * [Inkludera paket från tredje part i ditt Maven-projekt](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=sv-SE#including-third-party).
   * [Distribuera med  [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=sv-SE).

Så här installerar du tillägget i [!DNL Experience Manager] som en [!DNL Cloud Service]:

1. Hämta den utökade kopplingen från [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. [Åtkomst](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=sv-SE) och klona din AEM as a Cloud Service-databas från Cloud Manager.

1. Öppna den klonade AEM as a Cloud Service-databasen med valfri integrerad utvecklingsmiljö.

1. Placera den utökade ZIP-filen för anslutningen som laddats ned i steg 1 på följande sökväg:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Skapa mappen om mappen `resources` inte finns.


1. Lägg till `pom.xml` beroenden:

   1. Lägg till ett beroende i överordnad `pom.xml`.

      ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version>enhanced connector version number</version>
         <scope>system</scope>
         <systemPath>${project.basedir}/ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
      ```

      >[!NOTE]
      >
      >Se till att uppdatera det utökade versionsnumret för anslutningen innan du kopierar beroendet till det överordnade `pom.xml`.

   1. Lägg till ett beroende i `all module pom.xml`.

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
            <scope>system</scope>
            <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
         </dependency>
      ```


1. Lägg till `pom.xml` inbäddningar. Lägg till [!DNL Workfront for Experience Manager enhanced connector]-paketen i avsnittet `embeddeds` i `pom.xml` för alla ditt underprojekt. Den måste vara inbäddad i alla moduler `pom.xml`.

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

1. Överför ändringarna till databasen.

1. Kör pipelinen för att [distribuera ändringarna till Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=sv-SE).

1. Om du vill skapa en systemanvändarkonfiguration skapar du `wf-workfront-users` i [!DNL Experience Manager] Användargrupp och tilldelar behörigheten `jcr:all` till `/content/dam`. En systemanvändare `workfront-tools` skapas automatiskt och de behörigheter som krävs hanteras automatiskt. Alla användare från [!DNL Workfront] som använder den utökade kopplingen läggs automatiskt till som en del av den här gruppen.

Om du vill ha information om hur du uppdaterar [!DNL Workfront for Experience Manager enhanced connector] från en tidigare version till den senaste versionen klickar du [här](update-workfront-enhanced-connector.md).

## Konfigurera anslutningen mellan [!DNL Experience Manager] som [!DNL Cloud Service] och [!DNL Workfront] {#configure-connection}

Så här skapar du en anslutning med [!DNL Workfront]:

1. I [!DNL Experience Manager] väljer du **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront Tools Configuration]**.

1. Välj `workfront-tools` i den vänstra panelen och välj alternativet **[!UICONTROL Create]** i sidans övre högra del.

1. I dialogrutan **[!UICONTROL Workfront Connection]** anger du nödvändig information om din [!DNL Workfront]-distribution och väljer alternativet **[!UICONTROL Connect to Workfront]**. När anslutningen är klar skapas den anpassade integrationen av dokumentet [!DNL Workfront] automatiskt i miljön [!DNL Workfront].

   ![Anslut [!DNL Experience Manager] och [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Navigera till fliken **[!UICONTROL Advanced]** och markera alternativet **[!UICONTROL Is the Server AEM as a Cloud Service]**.
