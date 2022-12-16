---
title: Infoga innehåll i mål
description: Infoga innehåll i mål
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: 20e54ff697c0dc7ab9faa504d9f9e0e6ee585464
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 9%

---

# Infoga innehåll i mål {#ingesting-content}

## Inmatningsprocess i verktyget Innehållsöverföring {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Innehållsintag"
>abstract="Inmatning avser att hämta innehåll från migreringsuppsättningen till målinstansen för Cloud Service. Content Transfer Tool har en funktion för differentiell innehållsuppdatering som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="Uppdatera inmatning"

Följ stegen nedan för att importera migreringsuppsättningen från Content Transfer Tool:
>[!NOTE]
>Du kan köra det valfria förkopieringssteget för att avsevärt snabba upp intagningsfasen. Steg före kopiering är mest effektivt för första fullständiga extrahering och förtäring. Se [Ingesting with AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) för mer information.

>[!NOTE]
>Kom du ihåg att logga en supportbiljett för det här intaget? Se [Viktigt att tänka på innan du använder verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) och andra överväganden för att underlätta intag.

1. Gå till Cloud Acceleration Manager. Klicka på ditt projektkort och klicka på kortet för innehållsöverföring. Navigera till **Inmatningsjobb** och klicka på **Nytt intag**

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)


1. Granska checklistan för konsumtion och se till att alla steg har slutförts. Detta är nödvändiga steg för att säkerställa ett lyckat intag. Du kan fortsätta till **Nästa** endast om checklistan har slutförts.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. Ange nödvändig information för att skapa ett nytt intag.

   * Välj den migreringsuppsättning som du just extraherade som källa
   * Välj målmiljö. Det är här som migreringsuppsättningens innehåll importeras. Välj nivån. (Författare/Publicera).

   >[!NOTE]
   >
   >Om källan var författare rekommenderar vi att du importerar den till nivån Författare på målet. Om källan var Publish ska även målet vara Publish.

   >[!NOTE]
   >
   >Om målnivån är `Author`, kommer författarinstansen att stängas under den tid som inmatningen pågår och kommer inte att vara tillgänglig för användare (till exempel författare eller alla som utför underhåll). Detta är för att skydda systemet och förhindra ändringar som antingen kan gå förlorade eller orsaka en ingiftskonflikt. Se till att ditt team är medvetna om detta. Observera också att miljön kommer att visas i viloläge under författarintaget.

   >[!NOTE]
   >
   >Du kan köra det valfria förkopieringssteget för att avsevärt snabba upp intagningsfasen. Se [Ingesting with AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) för mer information.
   > 
   >Om du använder inmatning med förkopia (för S3 eller Azure Data Store) bör du endast köra Author-intagning. Detta snabbar upp inläsningen av publiceringen när den körs senare.

   >[!IMPORTANT]
   >
   >Du kommer bara att kunna starta upp ett intag till målmiljön om du tillhör den lokala **AEM administratörer** på Cloud Servicens författartjänst. Om du inte kan påbörja ett intag, se [Det går inte att starta matning](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) för mer information.

   >[!IMPORTANT]
   >
   >Om inställningen **Svep** är aktiverat före inmatning, tar bort hela den befintliga databasen och skapar en ny databas där innehållet kan importeras till. Det innebär att alla inställningar återställs, inklusive behörigheter för målinstansen av Cloud Servicen. Detta gäller även för en admin-användare som har lagts till i **administratörer** grupp. Du måste läggas till igen i administratörsgruppen för att kunna påbörja ett intag.

1. Klicka på **Ingest**

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. Du kan sedan övervaka matningsfasen från listvyn Ingessionsjobb och använda matningsens åtgärdsmeny för att visa loggen allt eftersom matningen fortskrider.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. När du har slutfört intag klickar du på (i) knappen längst upp till höger på skärmen för att få mer information om intagsjobbet.

<!-- Alexandru: hiding temporarily, until it's reviewed 

1. The **Migration Set ingestion** dialog box displays. Content can be ingested to either Author instance or Publish instance at a time. Select the instance to ingest content to. Click on **Ingest** to start the ingestion phase. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >If ingesting with pre-copy is used (for S3 or Azure Data Store), it is recommended to run Author ingestion first alone. This will speed up the Publish ingestion when it is run later. 

   >[!IMPORTANT]
   >When the **Wipe existing content on Cloud instance before ingestion** option is enabled, it deletes the entire existing repository and creates a new repository to ingest content into. This means that it resets all settings including permissions on the target Cloud Service instance. This is also true for an admin user added to the **administrators** group.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   Additionally, click on **Customer Care** to log a ticket, as shown in the figure below. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)
   
   Also, refer to [Important Considerations for Using Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) to learn more.

1. Once the ingestion is complete, the status under **Author ingestion** updates to **FINISHED**.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png) -->

## Uppdatera inmatning {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="Uppdatera inmatning"
>abstract="Använd den övre funktionen för att flytta ändrat innehåll sedan föregående innehållsöverföringsaktivitet. Kontrollera loggarna efter eventuella fel/varningar när du har slutfört Ingestition. Felen bör åtgärdas omedelbart, antingen genom att man hanterar de rapporterade problemen eller genom att kontakta Adobe kundtjänst."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en" text="Visa loggar"

Content Transfer Tool har en funktion för differentiell *innehållsuppdatering* som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen.

>[!NOTE]
>Efter den första innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda Cloud Service. Om du har använt steget före kopiering för det första fullständiga intaget kan du hoppa över förkopiering för efterföljande toppkopieringsförslag (om den översta migreringsuppsättningsstorleken är mindre än 200 GB) eftersom det kan göra hela processen tidsödande.

När inmatningsprocessen är klar måste du köra en [Extrahering uppifrån och ned](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) och använd sedan den översta intagsmetoden.

Du kan göra detta genom att skapa ett nytt intag-jobb och se till att **Svep** är inaktiverat under matningsfasen, vilket visas nedan:

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## Felsökning {#troubleshooting}

### CAM kan inte hämta migreringstoken {#cam-unable-to-retrieve-the-migration-token}

Den automatiska hämtningen av migreringstoken kan misslyckas av olika orsaker, inklusive dig [konfigurera ett IP-tillåtelselista via Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) i målmiljön för Cloud Service. I sådana fall visas följande dialogruta när du försöker starta ett intag:

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

Du måste hämta migreringstoken manuellt genom att klicka på länken Hämta token i dialogrutan. Då öppnas en annan flik som visar variabeln. Du kan sedan kopiera token och klistra in den i **Indata för migreringstoken** fält. Nu borde du kunna påbörja intaget.

>[!NOTE]
>
>Token är tillgänglig för användare som tillhör den lokala **AEM administratörer** på Cloud Servicens författartjänst.

### Det går inte att starta matning {#unable-to-start-ingestion}

Du kommer bara att kunna starta upp ett intag till målmiljön om du tillhör den lokala **AEM administratörer** på Cloud Servicens författartjänst. Om du inte tillhör gruppen AEM administratörer visas ett felmeddelande enligt nedan när du försöker starta ett intag. Du kan antingen be administratören att lägga till dig på den lokala **AEM administratörer** eller fråga efter själva variabeln som du sedan kan klistra in i **Indata för migreringstoken** fält.

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### Automatiska uppdateringar via Release Orchestrator är fortfarande aktiverat

Frisläpp Orchestrator håller automatiskt miljön uppdaterad genom att uppdatera automatiskt. Om uppdateringen utlöses när ett intag utförs, kan det orsaka oförutsägbara resultat, bland annat skador på miljön. Detta är en av orsakerna till att en supportanmälan bör loggas innan ett förtäring påbörjas (se &quot;Anteckning&quot; ovan), så att det går att schemalägga tillfällig inaktivering av Release Orchestrator.

Om Frisläpp Orchestrator fortfarande körs när ett intag startas visas det här felmeddelandet. Du kan välja att fortsätta i alla fall och ta risken genom att markera fältet och trycka på knappen igen.

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_ingestion.png)

## What&#39;s Next {#whats-next}

När du har slutfört Inkludering av innehåll i Target kan du visa loggar för varje steg (extrahering och förtäring) och leta efter fel. Se [Visa loggar för en migreringsuppsättning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en) om du vill veta mer.