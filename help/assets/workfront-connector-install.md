---
title: Installera [!DNL Workfront for Experience Manager enhanced connector]
description: Installera [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: d0d89c3905b2bf357de8a7599245c9360444e53b
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 0%

---

# Installera [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html) |
| AEM as a Cloud Service | Den här artikeln |

En användare med administratörsåtkomst i [!DNL Adobe Experience Manager] som [!DNL Cloud Service] installerar den utökade anslutningen. Innan du installerar bör du granska plattformsstödet och andra [krav för kopplingen](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe kräver installation och konfiguration av [!DNL Adobe Workfront for Experience Manager enhanced connector] endast via certifierade partners eller [!DNL Adobe Professional Services]. Om den distribueras och konfigureras utan en certifierad partner eller [!DNL Adobe Professional Services], stöds den inte av Adobe.
>
>* Adobe kan släppa uppdateringar av [!DNL Adobe Workfront] och [!DNL Adobe Experience Manager] som gör denna koppling redundant, Om detta inträffar kan kunderna behöva gå över från att använda denna koppling.
>
>* Adobe har stöd för utökade anslutningsversioner 1.7.4 och senare. Tidigare förhandsversioner och anpassade versioner stöds inte. Information om hur du kontrollerar den förbättrade anslutningsversionen finns i steg 5 a i [installationsanvisningar för förbättrad anslutning](workfront-connector-install.md).
>
>* Se [Partnercertifieringsprov för Workfront för Experience Manager Assets förbättrad anslutning](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Mer information om provet finns i [Provguide](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


Innan du installerar anslutningsprogrammet följer du de här förinstallationsstegen:

1. Om ditt AEM as a Cloud Service program har konfigurerat Advanced Networking och aktiverat IP Allow-Listing måste du lägga till Workfront IP-adresser i denna allow-list för att tillåta att händelseprenumerationer och olika API-anrop skickas till AEM.

   * [IP-adresser för Workfront-kluster](https://experienceleague.adobe.com/docs/workfront/using/administration-and-setup/get-started-administration/configure-your-firewall.html?lang=en#ip-addresses-to-allow-for-clusters-1-2-3-5-7-8-and-9). Så här känner du IP-klustret i [!DNL Workfront], navigera till **[!UICONTROL Setup]** > **[!UICONTROL System]** > **[!UICONTROL Customer Info]**.

   * [API:er för Workfront Event Subscription](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-api/event-subscriptions/event-subs-api.html)
   >[!IMPORTANT]
   >
   >* Om du har konfigurerat Advanced Networking för ditt program och använder IP Allow Listing, måste du på grund av en begränsning i den förbättrade Workfront Connector-arkitekturen lägga till programmets IP-adress i listan över tillåtna användare i Cloud Manager.
   >
   >* p{PROGRAM_ID}.external.adobeaemcloud.com
   >
   >* Om du vill hitta programmets IP-adress öppnar du ett terminalfönster och kör ett kommando, till exempel:

      >
      >    ```TXT
      >    dscacheutil -q host -a name p{PROGRAM_ID}.external.adobeaemcloud.com
      >
      >    ```

1. Kontrollera att följande övertäckningar inte finns i [!DNL Experience Manager] databas. Om du har befintliga övertäckningar på de här banorna måste du antingen ta bort övertäckningarna eller sammanfoga ändringarna mellan dem:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`
   * `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

1. Den här installationen kräver kunskaper för att skapa ett Maven-projekt i [!DNL Experience Manager] som [!DNL Cloud Service]. Använd följande resurser för att lära dig hur du inkluderar ett tredjepartspaket i ditt Maven-projekt:

   * [Inkludera tredjepartspaket i ditt Maven-projekt](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#including-third-party).
   * [Distribuera med [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html).

Installera tillägget i [!DNL Experience Manager] som [!DNL Cloud Service]gör du så här:

1. Ladda ned den förbättrade anslutningen från [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. [Åtkomst](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) och klona din AEM as a Cloud Service databas från Cloud Manager.

1. Öppna den klonade AEM as a Cloud Service databasen med valfri integrerad utvecklingsmiljö.

1. Placera den utökade ZIP-filen för anslutningen som laddats ned i steg 1 på följande sökväg:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Om `resources` mappen finns inte, skapa mappen.


1. Lägg till `pom.xml` beroenden:

   1. Lägg till ett beroende i överordnat objekt `pom.xml`.

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
      >Uppdatera det utökade versionsnumret för anslutningen innan du kopierar beroendet till det överordnade `pom.xml`.

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


1. Lägg till `pom.xml` bäddar in. Lägg till [!DNL Workfront for Experience Manager enhanced connector] paket till `embeddeds` i `pom.xml` av alla dina underprojekt. Behöver den vara inbäddad i alla moduler `pom.xml`.

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

1. Skicka ändringarna till databasen.

1. Kör pipeline till [distribuera ändringarna till Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

1. Om du vill skapa en systemanvändarkonfiguration skapar du `wf-workfront-users` in [!DNL Experience Manager] Användargrupp och tilldela behörighet `jcr:all` till `/content/dam`. En systemanvändare `workfront-tools` skapas automatiskt och de behörigheter som krävs hanteras automatiskt. Alla användare från [!DNL Workfront] som använder den utökade kopplingen läggs automatiskt till som en del av den här gruppen.

För information om att uppdatera [!DNL Workfront for Experience Manager enhanced connector] från en tidigare version till den senaste versionen, klicka på [här](update-workfront-enhanced-connector.md).

## Konfigurera anslutningen mellan [!DNL Experience Manager] som [!DNL Cloud Service] och [!DNL Workfront] {#configure-connection}

Skapa en anslutning med [!DNL Workfront]gör du så här:

1. I [!DNL Experience Manager] väljer du **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront Tools Configuration]**.

1. Välj `workfront-tools` i den vänstra panelen och väljer **[!UICONTROL Create]** i det övre högra hörnet på sidan.

1. I **[!UICONTROL Workfront Connection]** kan du ange den information du behöver [!DNL Workfront] driftsättning och välj **[!UICONTROL Connect to Workfront]** alternativ. När anslutningen är klar [!DNL Workfront] anpassad integration av dokument skapas automatiskt i [!DNL Workfront] miljö.

   ![Anslut [!DNL Experience Manager] och [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Navigera till **[!UICONTROL Advanced]** och välj alternativet **[!UICONTROL Is the Server AEM as a Cloud Service]**.
