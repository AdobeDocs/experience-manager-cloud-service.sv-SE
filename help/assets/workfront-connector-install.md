---
title: Installera [!DNL Workfront for Experience Manager enhanced connector]
description: Installera [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
source-git-commit: 8ca25f86a8d0d61b40deaff0af85e56e438efbdc
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---


# Installera [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

En användare med administratörsåtkomst i [!DNL Adobe Experience Manager] som [!DNL Cloud Service] installerar den utökade anslutningen. Innan du installerar bör du granska plattformsstödet och andra [krav för kopplingen](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>Adobe kräver installation och konfiguration av [!DNL Adobe Workfront for Experience Manager enhanced connector] endast via certifierade partners eller [!DNL Adobe Professional Services]. Om den distribueras och konfigureras utan en certifierad partner eller [!DNL Adobe Professional Services], stöds den inte av Adobe.
>
>Adobe kan släppa uppdateringar av [!DNL Adobe Workfront] och [!DNL Adobe Experience Manager] som gör denna koppling redundant, Om detta inträffar kan kunderna behöva gå över från att använda denna koppling.

Innan du installerar anslutningsprogrammet följer du de här förinstallationsstegen:

1. [Konfigurera brandväggen](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html). Så här känner du IP-klustret i [!DNL Workfront], navigera till [!UICONTROL Setup] > [!UICONTROL System] > [!UICONTROL Customer Info].

1. Tillåt HTTP-huvuden med namnet i dispatchern `authorization`, `username`och `apikey`. Tillåt `GET`, `POST`och `PUT` förfrågningar till `/bin/workfront-tools`.

1. Kontrollera att följande sökvägar inte finns i [!DNL Experience Manager] databas:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. Den här installationen kräver kunskaper för att skapa ett Maven-projekt i [!DNL Experience Manager] som [!DNL Cloud Service]. Använd följande resurser för att lära dig hur du inkluderar ett tredjepartspaket i ditt Maven-projekt:

   * [Inkludera tredjepartspaket i ditt Maven-projekt](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#including-third-party).
   * [Distribuera med [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html).

Installera tillägget i [!DNL Experience Manager] som [!DNL Cloud Service]gör du så här:

1. Lägg till `pom.xml` beroenden:

   1. Lägg till ett beroende i överordnat objekt `pom.xml`.

      ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version>1.7.4</version>
      </dependency>
      ```

   1. Lägg till ett beroende i alla moduler [!DNL pom.xml].

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
         </dependency>
      ```

1. Lägg till `pom.xml` autentisering.

   1. Inkludera nedanstående databaskonfiguration i pom.xml i profilen adobe-public, så att anslutningsberoendena (ovan) kan lösas vid byggtillfället (både lokalt och med Cloud Manager). Autentiseringsuppgifter för databasåtkomst tillhandahålls när en licens köpts. Autentiseringsuppgifterna måste läggas till filen settings.xml i serveravsnittet.

      ```XML
      <repository>
         <id>hoodoo-maven</id>
         <name>Hoodoo Repository</name>
         <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
      </repository>
      ```

   1. Skapa en fil med namnet `./cloudmanager/maven/settings.xml` i projektets rot. Information om hur du hanterar lösenordsskyddade Maven-databaser finns i [konfigurera projektet](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md). Dessutom, ett exempel `settings.xml` fil för referens. Till sist kan du uppdatera din lokala `settings.xml` för att kompilera lokalt.

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

1. Om du vill skapa en systemanvändarkonfiguration skapar du `wf-workfront-users` in [!DNL Experience Manager] Användargrupp och tilldela behörighet `jcr:all` till `/content/dam`. En systemanvändare `workfront-tools` skapas automatiskt och de behörigheter som krävs hanteras automatiskt. Alla användare från [!DNL Workfront] som använder den utökade kopplingen läggs automatiskt till som en del av den här gruppen.

## Konfigurera anslutningen mellan [!DNL Experience Manager] som [!DNL Cloud Service] och [!DNL Workfront] {#configure-connection}

Skapa en anslutning med [!DNL Workfront]gör du så här:

1. I [!DNL Experience Manager] väljer du **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront Tools Configuration]**.

1. Välj `workfront-tools` i den vänstra panelen och väljer **[!UICONTROL Create]** i det övre högra hörnet på sidan.

1. I **[!UICONTROL Workfront Connection]** kan du ange den information du behöver [!DNL Workfront] driftsättning och välj **[!UICONTROL Connect to Workfront]** alternativ. När anslutningen är klar [!DNL Workfront] anpassad integration av dokument skapas automatiskt i [!DNL Workfront] miljö.

   ![Anslut [!DNL Experience Manager] och [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Navigera till **[!UICONTROL Advanced]** och välj alternativet **[!UICONTROL Is the Server AEM as a Cloud Service]**.
