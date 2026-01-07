---
Title: How to Connect AEM Adaptive Forms with Azure SQL Storage
Description: Learn how to configure an Azure SQL Database connection in AEM Forms and integrate it with your Adaptive Forms to store or retrieve data efficiently using JDBC.
Keywords: Azure SQL integration with AEM Forms, Connecting Adaptive Forms to Azure SQL Database, JDBC connection for Azure SQL in AEM Forms, Storing Adaptive Form data in Azure SQL
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: e29f70aa1a8164787c7d310a05c24d7e501803e5
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---

# Ansluta ett adaptivt formulär till Azure SQL Storage

Adaptiv Forms i Adobe Experience Manager (AEM) kan integreras med externa databaser för att lagra eller hämta data.
I den här artikeln beskrivs hur du ansluter ett adaptivt formulär till en Azure SQL-databas med JDBC via AEM as a Cloud Service.

>
> 
> Den här guiden gäller för icke-sandlådemiljöer i AEM as a Cloud Service med avancerade nätverk aktiverade.

## Fördelar

Att integrera Adaptiv Forms med Azure SQL ger flera fördelar:

* **Datakinteraktion i realtid:** Möjliggör läsning och skrivning av data mellan formulär och Azure-databasen.
* **Skalbarhet:** Azure SQL ger skalbara databasprestanda som är lämpliga för företagsprogram.
* **Centraliserad datalagring:** Behåller formuläröverföringar och hämtade data som lagras på en central plats.
* **Säkerhetsöverensstämmelse:** Utnyttjar Azure inbyggda nätverks-, brandväggs- och krypteringsalternativ för att säkerställa säker kommunikation.
* **Integrering med molnet:** Perfekt för moderna, molnbaserade arkitekturer som använder AEM as a Cloud Service.

## Förutsättningar

* Skapa [Azure SQL Database](https://learn.microsoft.com/en-us/azure/azure-sql/database/single-database-create-quickstart?view=azuresql&tabs=azure-portal) och kontrollera att **proxyanslutningen** är aktiverad.

  >[!NOTE]
  >
  > Navigera till: `Azure Portal → SQL Server → Security → Networking → Connectivity` om du vill aktivera **proxyanslutningen**.

  ![Skapa Azure Db](/help/forms/assets/create-azure-db.png)

* Aktivera [Avancerade nätverk som konfigurerats med en dedikerad utgående IP](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/networking/dedicated-egress-ip-address) för den skapade Azure-databasen.

  >[!NOTE]
  >
  >    Efter aktivering av dedikerad IP för utgångar. Gå till `Azure Portal → SQL Server → Security → Networking → Public Access` och lägg till IP-adressen för utgångar i brandväggsreglerna.

  ![Utreses-IP](/help/forms/assets/cretae-azure-db-egress-ip.png)

* Ange portvidarebefordran i molnmiljön med:
   * **portOrigin**: Mellan `30000–30999`
   * **portDest**: `1433` (standardport för Azure SQL)
Till exempel: `portOrigin: 30433 → portDest: 1433`

     >
     > 
     > Du kan kontakta Adobe Cloud Manager support för att konfigurera portvidarebefordran.


## Steg för att ansluta adaptiv Forms till Azure SQL

**Steg 1: Klona AEM as a Cloud Service Git-databasen**

1. Öppna kommandoraden och välj en katalog där AEM as a Cloud Service-databasen ska lagras, t.ex. `/cloud-service-repository/`.

1. Kör följande kommando för att klona databasen:

   ```
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<app-id>/
   ```

   **Var hittar du den här informationen?**

   Stegvisa instruktioner om hur du hittar dessa detaljer finns i Adobe Experience League-artikeln [Accessing Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git).

   När kommandot har slutförts visas en ny mapp som har skapats i din lokala katalog. Mappen får ett namn efter programmet.

1. Öppna databasmappen i en redigerare.

**Steg 2: Lägg till obligatoriska JAR**

Inkludera [SQL-drivrutinsberoendet](https://central.sonatype.com/artifact/com.microsoft.sqlserver/mssql-jdbc/12.8.0.jre11?smo=true) till AEM-projektet via paketet `all`:

>[!NOTE]
>
> Om du vill ta med SQL-beroendet i ditt projekt kan du läsa avsnittet [SQL-drivrutinsberoenden](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool#mysql-driver-dependencies) .

**Steg 3: Lägg till JDBC-konfiguration**

1. Navigera till följande katalog i din `<application folder>` där OSGi-konfigurationen för JDBC-poolen ska placeras:

   ```bash
   cd ui.config/src/jcr_root/apps/<application folder>/osgiconfig/config/
   ```

**Steg 4: Skapa konfigurationsfilen för Azure SQL-anslutningen**

1. Skapa filen:

   ```bash
   com.day.commons.datasource.jdbcpool.JdbcPoolService~<application folder>-sql.cfg.json
   ```

1. Lägg till nedanstående kodrader:

   ```json
   {
   "datasource.name": "azuredbshr",
   "jdbc.driver.class": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
   "jdbc.username": "<azureuser>",
   "jdbc.connection.uri": "jdbc:sqlserver://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30433;database=testdb;user=<azureuser>;password=<azurepassword>;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;",
   "jdbc.password": "******",
   "jdbc.validation.query": "SELECT 1"
       }
   ```

   >
   >
   > Ersätt `jdbc.username` med det faktiska Azure-användarnamnet och `jdbc.password` med det faktiska säkra lösenordet.

**Steg 5: Verkställ och skicka ändringarna**

Öppna terminalen och kör kommandona nedan:

```bash
git add .
git commit -m "<commit message>"
git push 
```

**Steg 6: Distribuera ändringarna via Cloud Manager Pipeline**

1. Logga in på **AEM Cloud Manager**.
1. Navigera till ditt projekt och kör pipeline för att distribuera ändringarna.

**Steg 7: Skapa en formulärdatamodell (FDM)**

När installationen av AEM och Azure är klar och kodändringarna har distribuerats:

1. Gå till AEM Author instance.
1. Navigera till **Verktyg** > **Forms** > **Dataintegreringar**.
1. Skapa ny **formulärdatamodell**.
1. Välj den skapade JDBC-konfigurationen på fliken **Datakällor**.
1. Klicka på **[!UICONTROL Create]** och bekräfta anslutningen.

![Skapa formulärdatamodell](/help/forms/assets/create-azure-sql-fdm.png)

**Steg 8: Använd den skapade FDM-filen i ett anpassat formulär**

1. Öppna ett anpassat formulär i redigeringsläge.
1. Välj den FDM som skapades i föregående steg som datamodell.
1. Använd [databindningar för att ansluta formulärfält till Azure SQL-datakällan](/help/forms/work-with-form-data-model.md#add-data-model-objects-and-services) och konfigurera överföringsåtgärden.

## Bästa praxis

* Använd **hemlighetshantering** för att undvika hårdkodningslösenord i konfigurationsfiler.
* Rotera databasens inloggningsuppgifter regelbundet och uppdatera konfigurationen på ett säkert sätt.
* Övervaka JDBC-anslutningsloggar för fel och fördröjning.
* Följ bästa praxis från Azure för att skydda SQL-databaser och brandväggskonfigurationer.
* Undvik att använda privilegierade databaskonton för formuläråtkomst.

## Relaterade artiklar

{{af-submit-action}}