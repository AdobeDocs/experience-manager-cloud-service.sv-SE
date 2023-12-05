---
title: Hur skapar man en formulärdatamodell?
description: Lär dig skapa en formulärdatamodell (FDM) och skicka eller hämta data till en datakälla med hjälp av ett adaptivt formulär eller ett AEM arbetsflöde.
feature: Form Data Model
role: User, Developer
level: Beginner, Intermediate
exl-id: b17b7441-912c-44c7-a835-809f014a8c86
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 0%

---

# Skapa formulärdatamodell {#create-form-data-model}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html) |
| AEM as a Cloud Service | Den här artikeln |


![Dataintegrering](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] dataintegrering ger ett intuitivt användargränssnitt för att skapa och arbeta med formulärdatamodeller. En formulärdatamodell bygger på datakällor för datautbyte, men du kan skapa en formulärdatamodell med eller utan en datakälla. Det finns två sätt att skapa en utifrån datamodell beroende på om du har konfigurerat datakällor:

* **Använda förkonfigurerade datakällor**: Om du har konfigurerat datakällor enligt beskrivningen i [Konfigurera datakällor](configure-data-sources.md)kan du markera dem när du skapar en formulärdatamodell. Den hämtar alla datamodellsobjekt, egenskaper och tjänster från de valda datakällorna som är tillgängliga för användning i formulärdatamodellen.

* **Utan datakällor**: Om du inte har konfigurerat datakällor för formulärdatamodellen kan du fortfarande skapa den utan datakällor. Du kan använda formulärdatamodellen för att skapa adaptiv Forms <!--and interactive communication--> och testa dem med exempeldata. När datakällor är tillgängliga kan du binda formulärdatamodellen till datakällor, som automatiskt återspeglas i tillhörande adaptiva Forms<!--and interactive communications-->.

>[!NOTE]
>
>Du måste vara medlem i båda **fdm-author** och **formuläranvändare** grupper för att kunna skapa och arbeta med formulärdatamodell. Kontakta [!DNL Experience Manager] administratör för att bli medlem i grupperna.

## Skapa formulärdatamodell {#data-sources}

Kontrollera att du har konfigurerat de datakällor som du vill använda i formulärdatamodellen enligt beskrivningen i [Konfigurera datakällor](configure-data-sources.md). Så här skapar du en formulärdatamodell som baseras på konfigurerade datakällor:

1. I [!DNL Experience Manager] författarinstans, navigera till **[!UICONTROL Forms > Data Integrations]**.
1. Välj **[!UICONTROL Create > Form Data Model]**.
1. I dialogrutan Skapa formulärdatamodell:

   * Ange ett namn för formulärdatamodellen.
   * (**Valfritt**) Ange rubrik, beskrivning och taggar för formulärdatamodellen.
   * (**Valfritt och endast tillämpligt om datakällor har konfigurerats**) Markera kryssruteikonen bredvid **[!UICONTROL Data Source Configuration]** och välj den konfigurationsnod där molntjänster för de datakällor som du vill använda finns. Den begränsar listan med datakällor som är tillgängliga för val på nästa sida till de som är tillgängliga i den valda konfigurationsnoden. Men om [!DNL Experience Manager] datakällor för användarprofiler listas som standard. Om du inte väljer en konfigurationsnod visas datakällor från alla konfigurationsnoder.

1. Välj **[!UICONTROL Next]**.

1. (**Gäller endast om datakällor har konfigurerats**) **[!UICONTROL Select Datasource]** visas tillgängliga datakällor, om det finns några. Välj de datakällor som du vill använda i formulärdatamodellen.
1. Välj **[!UICONTROL Create]** och i bekräftelsedialogrutan väljer **[!UICONTROL Open]** för att öppna formulärdatamodellredigeraren.

   Låt oss granska de olika komponenterna i användargränssnittet för formulärdatamodellsredigeraren.

   ![En formulärdatamodell med tre datakällor - en RESTful-tjänst, [!DNL Experience Manager] användarprofil och RDBMS](assets/fdm-ui.png)

   S. **[!UICONTROL Data Sources]** Visar datakällor i en formulärdatamodell. Expandera en datakälla om du vill visa dess datamodellsobjekt och -tjänster.

   B. **[!UICONTROL Refresh Data Source Definitions]** Hämtar alla ändringar i datakälldefinitioner från konfigurerade datakällor och uppdaterar dem på fliken Datakällor i formulärdatamodellens redigerare.

   C. **[!UICONTROL Model]** Innehållsområde där tillagda datamodellsobjekt visas.

   D. **[!UICONTROL Services]** Innehållsområde där tillagda datakällåtgärder eller -tjänster visas.

   E. **[!UICONTROL Toolbar]** Verktyg för att arbeta med formulärdatamodell. I verktygsfältet visas fler alternativ beroende på vilket objekt som är markerat i formulärdatamodellen.

   F. **[!UICONTROL Add Selected]** Lägger till markerade datamodellsobjekt och tjänster i formulärdatamodellen.

Mer information om redigeraren för formulärdatamodellen och hur du kan arbeta med den för att redigera och konfigurera formulärdatamodellen finns i [Arbeta med formulärdatamodell](work-with-form-data-model.md).

## Uppdatera datakällor {#update}

Gör följande för att lägga till eller uppdatera datakällor till en befintlig formulärdatamodell.

1. Gå till **[!UICONTROL Forms > Data Integrations]** väljer du den formulärdatamodell i vilken du vill lägga till eller uppdatera datakällor och väljer **[!UICONTROL Properties]**.
1. Gå till egenskaperna för formulärdatamodellen **[!UICONTROL Update Source]** -fliken.

   I **[!UICONTROL Update Source]** tab:

   * Välj bläddringsikonen i dialogrutan **[!UICONTROL Context-Aware Configuration]** och välj en konfigurationsnod där molnkonfigurationen för den datakälla som du vill lägga till finns. Om du inte väljer en nod finns molnkonfigurationer endast i `global` noden visas när du väljer **[!UICONTROL Add Sources]**.

   * Välj om du vill lägga till en ny datakälla **[!UICONTROL Add Sources]** och välj datakällor att lägga till i formulärdatamodellen. Alla datakällor konfigurerade i `global` och den valda konfigurationsnoden (om sådan finns) visas.

   * Om du vill ersätta en befintlig datakälla med en annan datakälla av samma typ väljer du **[!UICONTROL Edit]** -ikonen för datakällan och välj i listan över tillgängliga datakällor.
   * Om du vill ta bort en befintlig datakälla väljer du **[!UICONTROL Delete]** -ikon för datakällan. Ikonen Ta bort är inaktiverad om ett datamodellsobjekt i datakällan läggs till i formulärdatamodellen.

     ![fdm-properties](assets/fdm-properties.png)

1. Välj **[!UICONTROL Save & Close]** för att spara uppdateringarna.

>[!NOTE]
>
>När du har lagt till nya datakällor eller uppdaterat befintliga datakällor i en formulärdatamodell måste du uppdatera bindningsreferenserna, efter behov, i Adaptive Forms<!--and interactive communications--> som använder den uppdaterade formulärdatamodellen.

## Kontextmedvetna konfigurationer för specifika körningslägen {#runmode-specific-context-aware-config}

[!UICONTROL Form Data Model] använder [Skicka kontextmedvetna konfigurationer](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html) som stöder olika datakällparametrar för att ansluta till datakällor för olika [!DNL Experience Manager] körningslägen.

När [!UICONTROL Form Data Model] använder molnkonfigurationer för att lagra parametrar, som när de checkas in och distribueras via källkontroll (Cloud-Manager GIT-databas) skapar molnkonfiguration med samma parametrar för alla körningslägen (Utveckling, Scen och Produktion). I de fall där det finns behov av olika datauppsättningar för test- och produktionsmiljöer använder vi datakällparametrar (till exempel datakällans URL) för olika [!DNL Experience Manager] körningslägen.

För att uppnå detta måste du skapa en OSGi-konfiguration som innehåller parametrar för datakällans värde. Detta åsidosätter samma par från [!UICONTROL Form Data Model] molnkonfiguration vid körning. Eftersom OSGi-konfigurationerna stöder dessa körningslägen som standard kan du åsidosätta en datakällparameter till olika värden baserat på körningsläge.

Aktivera distributionsspecifika molnkonfigurationer i [!UICONTROL Form Data Model]:

1. Skapa molnkonfiguration på den lokala utvecklingsinstansen. Detaljerade anvisningar finns i [Konfigurera datakällor](/help/forms/configure-data-sources.md).

1. Lagra molnkonfigurationen i filsystemet.
   1. Skapa paket med filter `/conf/{foldername}/settings/cloudconfigs/fdm`. Använd samma `{foldername}` som i steg 1. Och ersätt `fdm` med `azurestorage` för Azure-lagringskonfiguration.
   1. Skapa och hämta paket. Mer information finns i [paketåtgärder](/help/implementing/developing/tools/package-manager.md).

1. Integrera molnkonfiguration i [!DNL Experience Manager] Arketype-projekt.
   1. Zippa upp det hämtade paketet.
   1. Kopiera `jcr_root` och skicka den till `ui.content` > `src` > `main` > `content`.
   1. Uppdatera `ui.content` > `src` > `main` > `content` > `META-INF` > `vault` > `filter.xml` innehåller filter `/conf/{foldername}/settings/cloudconfigs/fdm`. Mer information finns i [ui.content-modulen AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uicontent.html). När detta arkivtypsprojekt distribueras via CM-pipeline installeras samma molnkonfiguration i alla miljöer (eller körningslägen). Om du vill ändra värdet för fält (t.ex. URL) för molnkonfigurationer baserat på miljö använder du OSGi-konfigurationen som beskrivs i följande steg.

1. Skapa en kontextmedveten konfiguration för Apache Sling. Så här skapar du OSGi-konfigurationen:
   1. **Konfigurera OSGi-konfigurationsfiler i [!DNL Experience Manager] Arketype-projekt.**
Skapa OSGi Factory Configuration-filer med PID `org.apache.sling.caconfig.impl.override.OsgiConfigurationOverrideProvider`. Skapa en fil med samma namn i varje körningslägesmapp där värdena måste ändras för varje körningsläge. Mer information finns i [Konfigurerar OSGi för [!DNL Adobe Experience Manager]](/help/implementing/deploying/configuring-osgi.md#creating-sogi-configurations).

   1. **Ställ in OSGI-konfigurationsjson.** Så här använder du Åsidosättningsprovider för kontextmedveten konfiguration för Apache Sling:
      1. On local development instance `/system/console/configMgr`väljer du OSGi-fabrikskonfiguration med namnet **[!UICONTROL Apache Sling Context-Aware Configuration Override Provider: OSGi configuration]**.
      1. Ange beskrivning.
      1. Välj **[!UICONTROL enabled]**.
      1. Under overrides anger du fält som behöver ändras baserat på miljön vid sling override syntax. Mer information finns i [Kontextmedveten konfiguration för Apache Sling - Åsidosätt](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration-override.html#override-syntax). Till exempel: `cloudconfigs/fdm/{configName}/url="newURL"`.
Du kan lägga till flera åsidosättningar genom att välja **[!UICONTROL +]**.
      1. Välj **[!UICONTROL Save]**.
      1. Så här hämtar du OSGi Configuration JSON: [Generera OSGi-konfigurationer med AEM SDK QuickStart](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart).
      1. Placera JSON i OSGi Factory Configuration Files som skapades i föregående steg.
      1. Ändra värdet för `newURL` baserat på miljö (eller körläge).
      1. Om du vill ändra ett hemligt värde baserat på körningsläge kan du skapa en hemlig variabel med [API för molnhantering](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) och senare kan refereras i [OSGi-konfiguration](/help/implementing/deploying/configuring-osgi.md#secret-configuration-values).
När det här arketype-projektet distribueras via CM-pipeline, kommer åsidosättning att ge olika värden i olika miljöer (eller körningsläge).
      >[!NOTE]
      >
      >[!DNL Adobe Managed Service] användare kan kryptera de hemliga värdena med krypteringsstöd (mer information finns i [krypteringsstöd för konfigurationsegenskaper](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/encryption-support-for-configuration-properties.html#enabling-encryption-support) och placera krypterad text i värdet efter [Kontextmedvetna konfigurationer finns i Service Pack 6.5.13.0](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html#runmode-specific-context-aware-config).

1. Uppdatera datakällsdefinitionerna med alternativet att uppdatera datakällsdefinitionerna i [Redigerare för formulärdatamodell](#data-sources) för att uppdatera FDM-cachen via FDM-gränssnittet och få den senaste konfigurationen.

## Nästa steg {#next-steps}

Nu har du en formulärdatamodell med datakällor tillagda. Därefter kan du redigera formulärdatamodellen för att lägga till och konfigurera datamodellsobjekt och -tjänster, lägga till associationer mellan datamodellsobjekt, redigera egenskaper, lägga till anpassade datamodellsobjekt och egenskaper, generera exempeldata osv.

Mer information finns i [Arbeta med formulärdatamodell](work-with-form-data-model.md).


>[!MORELIKETHIS]
>
>* [Använd formulärdatamodell](/help/forms/using-form-data-model.md)