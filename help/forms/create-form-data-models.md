---
title: Hur skapar man en FDM (Form Data Model)?
description: Lär dig skapa en formulärdatamodell (FDM) och skicka eller hämta data till en datakälla med hjälp av ett adaptivt formulär eller ett AEM-arbetsflöde.
feature: Adaptive Forms, Form Data Model
role: User, Developer
level: Beginner, Intermediate
exl-id: b17b7441-912c-44c7-a835-809f014a8c86
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '1467'
ht-degree: 0%

---

# Skapa formulärdatamodell (FDM) {#create-form-data-model}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html) |
| AEM as a Cloud Service | Den här artikeln |


![Dataintegrering](do-not-localize/data-integeration.png)

Dataintegrering för [!DNL Experience Manager Forms] ger ett intuitivt användargränssnitt för att skapa och arbeta med formulärdatamodeller. En formulärdatamodell (FDM) använder datakällor för datautbyte, men du kan skapa en formulärdatamodell (FDM) med eller utan en datakälla. Det finns två sätt att skapa en utifrån datamodell beroende på om du har konfigurerat datakällor:

* **Använda förkonfigurerade datakällor**: Om du har konfigurerat datakällor enligt beskrivningen i [Konfigurera datakällor](configure-data-sources.md) kan du markera dem när du skapar en formulärdatamodell (FDM). Den hämtar alla datamodellsobjekt, egenskaper och tjänster från de valda datakällorna som är tillgängliga för användning i formulärdatamodellen (FDM).

* **Utan datakällor**: Om du inte har konfigurerat datakällor för formulärdatamodellen (FDM) kan du fortfarande skapa den utan datakällor. Du kan använda formulärdatamodellen (FDM) för att skapa adaptiv Forms <!--and interactive communication--> och testa dem med exempeldata. När datakällor är tillgängliga kan du binda formulärdatamodellen (FDM) till datakällor, som automatiskt återspeglas i den associerade adaptiva Forms<!--and interactive communications-->.

>[!NOTE]
>
>Du måste vara medlem i båda grupperna **fdm-author** och **forms-user** för att kunna skapa och arbeta med formulärdatamodell (FDM). Kontakta [!DNL Experience Manager]-administratören om du vill bli medlem i grupperna.

## Skapa formulärdatamodell (FDM) {#data-sources}

Kontrollera att du har konfigurerat de datakällor som du vill använda i formulärdatamodellen (FDM) enligt beskrivningen i [Konfigurera datakällor](configure-data-sources.md). Så här skapar du en FDM (Form Data Model) baserad på konfigurerade datakällor:

1. Navigera till [!DNL Experience Manager] i **[!UICONTROL Forms > Data Integrations]**-författarinstansen.
1. Välj **[!UICONTROL Create > Form Data Model]**.
1. I dialogrutan Skapa formulärdatamodell:

   * Ange ett namn för formulärdatamodellen (FDM).
   * (**Valfritt**) Ange rubrik, beskrivning och taggar för formulärdatamodellen (FDM).
   * (**Valfritt och endast tillämpligt om datakällor har konfigurerats**) Markera kryssruteikonen bredvid fältet **[!UICONTROL Data Source Configuration]** och välj konfigurationsnoden där molntjänster för de datakällor som du vill använda finns. Den begränsar listan med datakällor som är tillgängliga för val på nästa sida till de som är tillgängliga i den valda konfigurationsnoden. Alla datakällor för användarprofilen i [!DNL Experience Manager] listas som standard. Om du inte väljer en konfigurationsnod visas datakällor från alla konfigurationsnoder.

1. Välj **[!UICONTROL Next]**.

1. (**Gäller endast om datakällor har konfigurerats**) Skärmen **[!UICONTROL Select Datasource]** visar eventuella tillgängliga datakällor. Välj de datakällor som du vill använda i formulärdatamodellen.
1. Välj **[!UICONTROL Create]** och välj **[!UICONTROL Open]** i bekräftelsedialogrutan för att öppna redigeraren för formulärdatamodellen.

   Låt oss granska de olika komponenterna i användargränssnittet för formulärdatamodellsredigeraren.

   ![En formulärdatamodell med tre datakällor - en RESTful-tjänst, [!DNL Experience Manager] användarprofil och en RDBMS ](assets/fdm-ui.png)

   S. **[!UICONTROL Data Sources]** Visar datakällor i en formulärdatamodell. Expandera en datakälla om du vill visa dess datamodellsobjekt och -tjänster.

   B. **[!UICONTROL Refresh Data Source Definitions]** Hämtar alla ändringar i datakälldefinitioner från konfigurerade datakällor och uppdaterar dem på fliken Datakällor i formulärdatamodellens redigerare.

   C. **[!UICONTROL Model]** Innehållsområde där tillagda datamodellsobjekt visas.

   D. **[!UICONTROL Services]** Innehållsområde där tillagda datakällåtgärder eller -tjänster visas.

   E. **[!UICONTROL Toolbar]** Verktyg för att arbeta med formulärdatamodell (FDM). I verktygsfältet visas fler alternativ beroende på det valda objektet i formulärdatamodellen (FDM).

   F. **[!UICONTROL Add Selected]** Lägger till markerade datamodellsobjekt och tjänster i formulärdatamodellen.

Mer information om formulärdatamodellredigeraren och hur du kan arbeta med den för att redigera och konfigurera formulärdatamodellen (FDM) finns i [Arbeta med formulärdatamodell](work-with-form-data-model.md).

## Uppdatera datakällor {#update}

Gör följande för att lägga till eller uppdatera datakällor till en befintlig formulärdatamodell (FDM).

1. Gå till **[!UICONTROL Forms > Data Integrations]**, markera den formulärdatamodell (FDM) i vilken du vill lägga till eller uppdatera datakällor och välj **[!UICONTROL Properties]**.
1. Gå till fliken **[!UICONTROL Update Source]** i egenskaperna för formulärdatamodellen.

   På fliken **[!UICONTROL Update Source]**:

   * Välj bläddringsikonen i fältet **[!UICONTROL Context-Aware Configuration]** och välj en konfigurationsnod där molnkonfigurationen för den datakälla som du vill lägga till finns. Om du inte väljer en nod visas molnkonfigurationer som bara finns i noden `global` när du väljer **[!UICONTROL Add Sources]**.

   * Om du vill lägga till en ny datakälla väljer du **[!UICONTROL Add Sources]** och markerar de datakällor som ska läggas till i formulärdatamodellen (FDM). Alla datakällor som har konfigurerats i `global` och den valda konfigurationsnoden (om det finns någon) visas.

   * Om du vill ersätta en befintlig datakälla med en annan datakälla av samma typ, väljer du ikonen **[!UICONTROL Edit]** för datakällan och väljer i listan över tillgängliga datakällor.
   * Om du vill ta bort en befintlig datakälla väljer du ikonen **[!UICONTROL Delete]** för datakällan. Ikonen Ta bort är inaktiverad om ett datamodellsobjekt i datakällan läggs till i formulärdatamodellen (FDM).

     ![fdm-properties](assets/fdm-properties.png)

1. Välj **[!UICONTROL Save & Close]** om du vill spara uppdateringarna.

>[!NOTE]
>
>När du har lagt till nya datakällor eller uppdaterat befintliga datakällor i en formulärdatamodell (FDM) måste du uppdatera bindningsreferenserna, beroende på vad som är lämpligt, i Adaptive Forms<!--and interactive communications--> som använder den uppdaterade formulärdatamodellen (FDM).

## Kontextmedvetna konfigurationer för specifika körningslägen {#runmode-specific-context-aware-config}

[!UICONTROL Form Data Model (FDM)] använder [Sling-kontextmedvetna konfigurationer](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html) för att stödja olika datakällparametrar för att ansluta till datakällor för olika [!DNL Experience Manager]-körningslägen.

När [!UICONTROL Form Data Model (FDM)] använder molnkonfigurationer för att lagra parametrar, som när de checkas in och distribueras via källkontroll (Cloud-Manager GIT-databas) skapar molnkonfiguration med samma parametrar för alla körningslägen (utveckling, scen och produktion). I de fall där det finns behov av olika datauppsättningar för test- och produktionsmiljöer använder vi datakällparametrar (till exempel datakällans URL) för olika [!DNL Experience Manager]-körningslägen.

För att uppnå detta måste du skapa en OSGi-konfiguration som innehåller parametrar för datakällans värde. Detta åsidosätter samma par från molnkonfigurationen [!UICONTROL Form Data Model (FDM)] vid körning. Eftersom OSGi-konfigurationerna stöder dessa körningslägen som standard kan du åsidosätta en datakällparameter till olika värden baserat på körningsläge.

Så här aktiverar du distributionsspecifika molnkonfigurationer i [!UICONTROL Form Data Model (FDM)]:

1. Skapa molnkonfiguration på den lokala utvecklingsinstansen. Detaljerade steg finns i [Konfigurera datakällor](/help/forms/configure-data-sources.md).

1. Lagra molnkonfigurationen i filsystemet.
   1. Skapa paket med filter `/conf/{foldername}/settings/cloudconfigs/fdm`. Använd samma `{foldername}` som i steg 1. Och ersätt `fdm` med `azurestorage` för Azure-lagringskonfigurationen.
   1. Skapa och hämta paket. Mer information finns i [paketåtgärder](/help/implementing/developing/tools/package-manager.md).

1. Integrera molnkonfigurationen i [!DNL Experience Manager]-arkitekturprojektet.
   1. Zippa upp det hämtade paketet.
   1. Kopiera mappen `jcr_root` och placera den i mappen `ui.content` > `src` > `main` > `content`.
   1. Uppdatera `ui.content` > `src` > `main` > `content` > `META-INF` > `vault` > `filter.xml` för att innehålla filtret `/conf/{foldername}/settings/cloudconfigs/fdm`. Mer information finns i [ui.content-modulen i AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uicontent.html). När detta arkivtypsprojekt distribueras via CM-pipeline installeras samma molnkonfiguration i alla miljöer (eller körningslägen). Om du vill ändra värdet för fält (t.ex. URL) för molnkonfigurationer baserat på miljö använder du OSGi-konfigurationen som beskrivs i följande steg.

1. Skapa en kontextmedveten konfiguration för Apache Sling. Så här skapar du OSGi-konfigurationen:
   1. **Konfigurera OSGi-konfigurationsfiler i [!DNL Experience Manager] Archetype-projekt.**
Skapa OSGi Factory Configuration-filer med PID `org.apache.sling.caconfig.impl.override.OsgiConfigurationOverrideProvider` . Skapa en fil med samma namn i varje körningslägesmapp där värdena måste ändras för varje körningsläge. Mer information finns i [Konfigurera OSGi för [!DNL Adobe Experience Manager]](/help/implementing/deploying/configuring-osgi.md#creating-sogi-configurations).

   1. **Ange konfigurationsjson för OSGI.** Så här använder du Åsidosättningsprovider för kontextmedveten konfiguration för Apache Sling:
      1. På den lokala utvecklingsinstansen `/system/console/configMgr` väljer du OSGi-fabrikskonfiguration med namnet **[!UICONTROL Apache Sling Context-Aware Configuration Override Provider: OSGi configuration]**.
      1. Ange beskrivning.
      1. Välj **[!UICONTROL enabled]**.
      1. Under overrides anger du fält som behöver ändras baserat på miljön vid sling override syntax. Mer information finns i [Kontextmedveten konfiguration för Apache Sling - Åsidosätt](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration-override.html#override-syntax). Exempel: `cloudconfigs/fdm/{configName}/url="newURL"`.
Du kan lägga till flera åsidosättningar genom att välja **[!UICONTROL +]**.
      1. Välj **[!UICONTROL Save]**.
      1. Följ stegen i [Generera OSGi-konfigurationer med AEM SDK Quickstart](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart) för att få OSGi Configuration JSON.
      1. Placera JSON i OSGi Factory Configuration Files som skapades i föregående steg.
      1. Ändra värdet för `newURL` baserat på miljö (eller körläge).
      1. Om du vill ändra ett hemligt värde baserat på körningsläge kan du skapa en hemlig variabel med hjälp av [molnhanterings-API:t](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) och senare kan refereras i [OSGi-konfigurationen](/help/implementing/deploying/configuring-osgi.md#secret-configuration-values).
När det här arketype-projektet distribueras via CM-pipeline, kommer åsidosättning att ge olika värden i olika miljöer (eller körningsläge).

      >[!NOTE]
      >
      >[!DNL Adobe Managed Service]-användare kan kryptera de hemliga värdena med krypteringsstöd för mer information, se [krypteringsstöd för konfigurationsegenskaper](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/encryption-support-for-configuration-properties.html#enabling-encryption-support) och placera krypterad text i värdet efter att [kontextmedvetna konfigurationer är tillgängliga i Service Pack 6.5.13.0](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html#runmode-specific-context-aware-config).

1. Uppdatera datakälldefinitionerna med alternativet att uppdatera datakälldefinitionerna i [redigeraren för formulärdatamodell](#data-sources) för att uppdatera FDM-cachen via FDM-gränssnittet och få den senaste konfigurationen.

## Nästa steg {#next-steps}

Nu har du en formulärdatamodell (FDM) med datakällor tillagda. Därefter kan du redigera FDM (Form Data Model) för att lägga till och konfigurera datamodellsobjekt och -tjänster, lägga till associationer mellan datamodellsobjekt, redigera egenskaper, lägga till anpassade datamodellsobjekt och -egenskaper, generera exempeldata osv.

Mer information finns i [Arbeta med formulärdatamodell](work-with-form-data-model.md).


