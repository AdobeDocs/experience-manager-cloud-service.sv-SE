---
title: Infoga innehåll i mål
description: Infoga innehåll i mål
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: 79f5133e681261fa8f7604f1fc9c3fbf5c6a5f59
workflow-type: tm+mt
source-wordcount: '1722'
ht-degree: 6%

---

# Infoga innehåll i mål {#ingesting-content}

## Inmatningsprocess i verktyget Innehållsöverföring {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Innehållsintag"
>abstract="Inmatning avser att hämta innehåll från migreringsuppsättningen till målinstansen för Cloud Service. Content Transfer Tool har en funktion för differentiell innehållsuppdatering som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#top-up-ingestion-process" text="Uppdatera inmatning"

Följ stegen nedan för att importera migreringsuppsättningen från Content Transfer Tool:

>[!NOTE]
>Kom du ihåg att logga en supportbiljett för det här intaget? Se [Viktigt att tänka på innan du använder verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) och andra överväganden för att underlätta intag.

1. Gå till Cloud Acceleration Manager. Klicka på ditt projektkort och klicka på kortet för innehållsöverföring. Navigera till **Inmatningsjobb** och klicka på **Nytt intag**

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Granska checklistan för konsumtion och se till att alla steg har slutförts. Detta är nödvändiga steg för att säkerställa ett lyckat intag. Du kan fortsätta till **Nästa** endast om checklistan har slutförts.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. Ange nödvändig information för att skapa ett nytt intag.

   * Välj den migreringsuppsättning som innehåller extraherade data som källa.
      * Migreringsuppsättningar kommer att upphöra efter en längre inaktivitetsperiod, så det förväntas att intaget sker relativt snart efter att extraktionen har utförts. Granska [Förfallotid för migreringsuppsättning](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) för mer information.
   * Välj målmiljö. Det är här som migreringsuppsättningens innehåll importeras. Välj nivån. (Författare/Publicera). Snabba utvecklingsmiljöer stöds inte.

   >[!NOTE]
   >Följande anmärkningar gäller inhämtning av innehåll:
   > Om källan var författare rekommenderar vi att du importerar den till nivån Författare på målet. Om källan var Publish ska även målet vara Publish.
   > Om målnivån är `Author`, kommer författarinstansen att stängas under den tid som inmatningen pågår och kommer inte att vara tillgänglig för användare (till exempel författare eller alla som utför underhåll). Detta är för att skydda systemet och förhindra ändringar som antingen kan gå förlorade eller orsaka en ingiftskonflikt. Se till att ditt team är medvetna om detta. Observera också att miljön kommer att visas i viloläge under författarintaget.
   > Du kan köra det valfria förkopieringssteget för att avsevärt snabba upp intagningsfasen. Se [Ingesting with AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) för mer information.
   > Om du använder inmatning med förkopia (för S3 eller Azure Data Store) bör du endast köra Author-intagning. Detta snabbar upp inläsningen av publiceringen när den körs senare.
   > Inställningarna stöder inte en Rapid Development Environment-destination (RDE). De visas inte som ett möjligt målalternativ, även om användaren har åtkomst till det.

   >[!IMPORTANT]
   > Följande viktiga meddelanden gäller inhämtning av innehåll:
   > Du kan bara initiera ett intag till målmiljön om du tillhör den lokala **AEM administratörer** på Cloud Servicens författartjänst. Om du inte kan påbörja ett intag, se [Det går inte att starta matning](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) för mer information.
   > Om inställningen **Svep** är aktiverat före inmatning, tar bort hela den befintliga databasen och skapar en ny databas där innehållet kan importeras till. Det innebär att alla inställningar återställs, inklusive behörigheter för målinstansen av Cloud Servicen. Detta gäller även för en admin-användare som har lagts till i **administratörer** grupp. Du måste läggas till igen i administratörsgruppen för att kunna påbörja ett intag.

1. Klicka på **Ingest**

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. Du kan sedan övervaka matningsfasen från listvyn Ingessionsjobb och använda matningsens åtgärdsmeny för att visa loggen allt eftersom matningen fortskrider.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. När du har slutfört intag klickar du på (i) knappen i det övre högra hörnet av skärmen för att få mer information om intagsjobbet.

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
   
   Also, refer to [Important Considerations for Using Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) to learn more.

1. Once the ingestion is complete, the status under **Author ingestion** updates to **FINISHED**.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png) -->

## Uppdatera inmatning {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="Uppdatera inmatning"
>abstract="Använd den övre funktionen för att flytta ändrat innehåll sedan föregående innehållsöverföringsaktivitet. Kontrollera loggarna efter eventuella fel/varningar när du har slutfört Ingestition. Felen bör åtgärdas omedelbart, antingen genom att man hanterar de rapporterade problemen eller genom att kontakta Adobe kundtjänst."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html" text="Visa loggar"

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

Du kan bara initiera ett intag till målmiljön om du tillhör den lokala **AEM administratörer** på Cloud Servicens författartjänst. Om du inte tillhör gruppen AEM administratörer visas ett felmeddelande enligt nedan när du försöker starta ett intag. Du kan antingen be administratören att lägga till dig på den lokala **AEM administratörer** eller fråga efter själva variabeln som du sedan kan klistra in i **Indata för migreringstoken** fält.

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### Det gick inte att nå migreringstjänsten {#unable-to-reach-migration-service}

Efter att en fråga om att få ta emot ett inlägg har skickats ett meddelande som följande till användaren: &quot;Migreringstjänsten på målmiljön är för närvarande inte tillgänglig. Försök igen senare eller kontakta Adobe support.&quot;

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

Detta indikerar att Cloud Acceleration Manager inte kunde nå målmiljöns migreringstjänst för att starta intaget. Det här kan hända av flera orsaker.

>[!NOTE]
> 
> Fältet &quot;Migreringstoken&quot; visas eftersom det i ett fåtal fall inte är tillåtet att hämta denna token. Genom att tillåta manuell inmatning kan användaren snabbt påbörja intagningen utan ytterligare hjälp. Om variabeln anges och meddelandet fortfarande visas är det inte problemet att hämta variabeln.

* AEM as a Cloud Service bevarar miljötillståndet och kan ibland behöva starta om migreringstjänsten av ett antal vanliga orsaker. Om tjänsten startas om går den inte att nå, men kommer snart att vara tillgänglig.
* Det är möjligt att en annan process körs på instansen. Om till exempel Release Orchestrator tillämpar en uppdatering kan systemet vara upptaget och migreringstjänsten är inte tillgänglig regelbundet. Därför, och risken för att scenen eller produktionsinstansen skadas, är det mycket viktigt att du pausar uppdateringarna under ett intag.
* Om en [IP-Tillåtelselista har tillämpats](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) via Cloud Manager blockeras Cloud Acceleration Manager från att nå migreringstjänsten. Det går inte att lägga till en IP-adress för frågor eftersom adressen är mycket dynamisk. För närvarande är den enda lösningen att inaktivera IP-tillåtelselista när intaget körs.
* Det kan finnas andra skäl till att en utredning behöver göras. Kontakta Adobe kundtjänst om ditt intag fortfarande misslyckas.

### Automatiska uppdateringar via Release Orchestrator är fortfarande aktiverat

Frisläpp Orchestrator håller automatiskt miljön uppdaterad genom att uppdatera automatiskt. Om uppdateringen utlöses när ett intag utförs, kan det orsaka oförutsägbara resultat, bland annat skador på miljön. Detta är en av orsakerna till att en supportanmälan bör loggas innan ett förtäring påbörjas (se &quot;Anteckning&quot; ovan), så att det går att schemalägga tillfällig inaktivering av Release Orchestrator.

Om Frisläpp Orchestrator fortfarande körs när ett intag startas visas det här meddelandet. Du kan välja att fortsätta i alla fall och ta risken genom att markera fältet och trycka på knappen igen.

>[!NOTE]
>
> Utgåva av Orchestrator distribueras nu till utvecklingsmiljöer, så det bör även göras pausande uppdateringar för dessa miljöer.

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_ingestion.png)

### Inmatningsfel upptill

En vanlig orsak till [Inmatning uppifrån](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) fel är en konflikt i nod-ID:n. Identifiera felet genom att hämta matningsloggen med användargränssnittet i Cloud Acceleration Manager och leta efter en post som följande:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: Unikitetsbegränsningen bröt mot egenskap [jcr:uuid] med ett värde på a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

Varje nod i AEM måste ha ett unikt uuid. Detta fel anger att en nod som importeras har samma UID som en som redan finns på en annan sökväg i målinstansen.
Detta kan inträffa om en nod flyttas på källan mellan en extrahering och en efterföljande [Extrahering uppifrån och ned](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process).
Det kan också inträffa om en nod på målet flyttas mellan ett intag och ett efterföljande tilläggsintag.

Den här konflikten måste lösas manuellt. Någon som är bekant med innehållet måste bestämma vilken av de två noderna som måste tas bort, med hänsyn tagen till annat innehåll som refererar till det. Lösningen kan kräva att extraheringen av den övre delen görs igen utan den felande noden.

## What&#39;s Next {#whats-next}

När du har slutfört Inkludering av innehåll i Target kan du visa loggar för varje steg (extrahering och förtäring) och leta efter fel. Se [Visa loggar för en migreringsuppsättning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html) om du vill veta mer.
