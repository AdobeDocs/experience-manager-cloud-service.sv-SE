---
title: Infoga innehåll i Cloud Service
description: Lär dig hur du använder Cloud Acceleration Manager för att importera innehåll från din migreringsuppsättning till en instans av en Cloud Service.
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: 382d1ed93e9545127ebb54641657db365886503d
workflow-type: tm+mt
source-wordcount: '1954'
ht-degree: 5%

---

# Infoga innehåll i Cloud Service {#ingesting-content}

## Inmatningsprocess i verktyget Innehållsöverföring {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Innehållsintag"
>abstract="Inmatning avser att hämta innehåll från migreringsuppsättningen till målinstansen för Cloud Service. Content Transfer Tool har en funktion för differentiell innehållsuppdatering som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html" text="Uppdatera inmatning"

Följ stegen nedan för att importera din migreringsuppsättning med Cloud Acceleration Manager:

>[!NOTE]
>Kom du ihåg att logga en supportbiljett för det här intaget? Se [Viktigt att tänka på innan du använder verktyget Innehållsöverföring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) och andra överväganden för att underlätta intag.

1. Gå till Cloud Acceleration Manager. Klicka på projektkortet och klicka på kortet för innehållsöverföring. Navigera till **Inmatningsjobb** och klicka **Nytt intag**

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Granska checklistan för konsumtion och se till att alla steg är slutförda. Dessa steg är nödvändiga för att tillförseln ska lyckas. Gå till **Nästa** endast om checklistan är slutförd.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. Ange nödvändig information för att skapa ett intag.

   * Välj den migreringsuppsättning som innehåller extraherade data som källa.
      * Migreringsuppsättningar kommer att upphöra efter en längre inaktivitetsperiod, så det förväntas att intaget sker relativt snart efter att extraktionen har utförts. Granska [Förfallotid för migreringsuppsättning](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) för mer information.
   * Välj målmiljö. I den här miljön importeras migreringsuppsättningens innehåll. Välj nivån. (Författare/Publicera). Snabba utvecklingsmiljöer stöds inte.

   >[!NOTE]
   >Följande anmärkningar gäller inhämtning av innehåll:
   > Om källan var författare rekommenderar vi att du importerar den till nivån Författare på målet. Om källan var Publish ska även målet vara Publish.
   > Om målnivån är `Author`, stängs författarinstansen av under den tid som inmatningen pågår och blir otillgänglig för användare (till exempel författare eller alla som utför underhåll). Orsaken är att skydda systemet och förhindra alla ändringar som antingen kan gå förlorade eller orsaka en konflikt i intaget. Se till att ditt team är medvetna om detta. Observera också att miljön visas i viloläge under författarintaget.
   > Du kan köra det valfria förkopieringssteget för att avsevärt snabba upp intagningsfasen. Se [Ingesting with AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) för mer information.
   > Om du använder inmatning med förkopia (för S3 eller Azure Data Store) bör du endast köra Author-intagning. Det snabbar upp publiceringsintrycket när det körs senare.
   > Inställningarna stöder inte ett mål för Rapid Development Environment (RDE) och visas inte som ett möjligt målalternativ, även om användaren har åtkomst till det.

   >[!IMPORTANT]
   > Följande viktiga meddelanden gäller inhämtning av innehåll:
   > Du kan bara initiera ett intag till målmiljön om du tillhör den lokala **AEM administratörer** på Cloud Servicens författartjänst. Om du inte kan påbörja ett intag, se [Det går inte att starta matning](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) för mer information.
   > Om inställningen **Svep** är aktiverat före inmatning, tas hela den befintliga databasen bort och en databas skapas där du kan importera innehåll. Det här arbetsflödet innebär att alla inställningar återställs, inklusive behörigheter för målinstansen av Cloud Servicen. Återställningen gäller även för en admin-användare som lagts till i **administratörer** grupp. Du måste läsa till administratörsgruppen för att kunna påbörja ett intag.

1. Klicka **Ingest**.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. Du kan sedan övervaka matningsfasen från listvyn Ingessionsjobb och använda matningsens åtgärdsmeny för att visa loggen allt eftersom matningen fortskrider.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. Klicka på **(i)** om du vill ha mer information om intagsjobbet. Du kan se hur länge varje steg i Inledningen varar när den körs eller slutförs genom att klicka **...** och sedan klicka **Visa varaktighet**. Informationen från extraheringen visar också på vad som förtärs.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

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

   Also, see [Important Considerations for Using Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) to learn more.

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
>Efter den första innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda Cloud Service. Om du har använt förkopieringssteget för det första fullständiga intaget kan du hoppa över förkopiering för efterföljande toppkopieringsförslag (om den översta migreringsuppsättningsstorleken är mindre än 200 GB). Orsaken är att det kan lägga till tid i hela processen.

När importen är klar måste du köra en [Extrahering uppifrån och ned](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)och använd sedan den översta intagsmetoden.

Börja med att skapa ett matningsjobb och se till att **Svep** är inaktiverat under matningsfasen, vilket visas nedan:

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## Felsökning {#troubleshooting}

### CAM kan inte hämta migreringstoken {#cam-unable-to-retrieve-the-migration-token}

Den automatiska hämtningen av migreringstoken kan misslyckas av olika orsaker, inklusive dig [konfigurera ett IP-tillåtelselista via Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) i målmiljön för Cloud Service. I sådana fall visas följande dialogruta när du försöker starta ett intag:

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

Hämta migreringstoken manuellt genom att klicka på länken Hämta token i dialogrutan. En annan flik öppnas som visar token. Du kan sedan kopiera token och klistra in den i **Indata för migreringstoken** fält. Nu borde du kunna påbörja intaget.

>[!NOTE]
>
>Token är tillgänglig för användare som tillhör den lokala **AEM administratörer** på Cloud Servicens författartjänst.

### Det går inte att starta matning {#unable-to-start-ingestion}

Du kan bara initiera ett intag till målmiljön om du tillhör den lokala **AEM administratörer** på Cloud Servicens författartjänst. Om du inte tillhör gruppen AEM administratörer visas ett fel som visas nedan när du försöker starta ett intag. Du kan antingen be administratören att lägga till dig på den lokala **AEM administratörer** eller fråga efter själva variabeln som du sedan kan klistra in i **Indata för migreringstoken** fält.

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### Det gick inte att nå migreringstjänsten {#unable-to-reach-migration-service}

Efter att ett matningsförslag har begärts kan ett meddelande som följande visas för användaren: &quot;Migreringstjänsten i målmiljön är inte tillgänglig. Om så är fallet, försök igen senare eller kontakta supporten för Adobe.&quot;

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

Det här meddelandet anger att Cloud Acceleration Manager inte kunde nå målmiljöns migreringstjänst för att starta inmatningen. Denna situation kan uppstå av olika skäl.

>[!NOTE]
> 
> Fältet &quot;Migreringstoken&quot; visas eftersom det i ett fåtal fall inte är tillåtet att hämta denna token. Genom att tillåta manuell inmatning kan användaren snabbt påbörja intagningen utan ytterligare hjälp. Om token anges och meddelandet fortfarande visas, var det inte problemet att hämta token.

* AEM as a Cloud Service bevarar miljötillståndet och måste ibland starta om migreringstjänsten av olika vanliga orsaker. Om tjänsten startas om kan den inte nås, men är tillgänglig så småningom.
* Det är möjligt att en annan process körs på instansen. Om till exempel Release Orchestrator tillämpar en uppdatering kan systemet vara upptaget och migreringstjänsten är inte tillgänglig regelbundet. Därför, och risken att scenen eller produktionsinstansen skadas, är det mycket viktigt att du pausar uppdateringar under ett intag.
* Om en [IP-Tillåtelselista har tillämpats](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) via Cloud Manager blockerar det Cloud Acceleration Manager från att nå migreringstjänsten. Det går inte att lägga till en IP-adress för frågor eftersom adressen är dynamisk. För närvarande är den enda lösningen att inaktivera IP-tillåtelselista när intaget körs.
* Det kan finnas andra skäl till att en utredning behöver göras. Kontakta Adobe kundtjänst om ditt intag fortfarande misslyckas.

### Automatiska uppdateringar via Release Orchestrator är fortfarande aktiverat

Frisläpp Orchestrator håller automatiskt miljön uppdaterad genom att uppdatera automatiskt. Om uppdateringen utlöses när ett intag utförs, kan det orsaka oförutsägbara resultat, bland annat skador på miljön. En bra anledning att logga en kundsupportbiljett innan ett förtäring påbörjas (se&quot;Obs&quot; ovan), så att det går att schemalägga en tillfällig inaktivering av Release Orchestrator.

Om Release Orchestrator fortfarande körs när ett intag startas visas det här meddelandet i användargränssnittet. Du kan välja att fortsätta i alla fall och ta risken genom att markera fältet och trycka på knappen igen.

>[!NOTE]
>
> Utgåva av Orchestrator distribueras nu till utvecklingsmiljöer, så det bör även göras pausande uppdateringar för dessa miljöer.

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_ingestion.png)

### Inmatningsfel i toppklass på grund av Unikhetsbegränsningsöverträdelse

En vanlig orsak till [Inmatning uppifrån](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) fel är en konflikt i nod-ID:n. Identifiera felet genom att hämta matningsloggen med användargränssnittet i Cloud Acceleration Manager och leta efter en post som följande:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: Unikhetsvillkoret bröt egenskap [jcr:uuid] med värdet a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

Varje nod i AEM måste ha ett unikt uuid. Detta fel anger att en nod som importeras har samma UID som en som finns någon annanstans på en annan sökväg i målinstansen.
Detta kan inträffa om en nod flyttas på källan mellan en extrahering och en efterföljande [Extrahering uppifrån och ned](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process).
Det kan också inträffa om en nod på målet flyttas mellan ett intag och ett efterföljande tilläggsintag.

Den här konflikten måste lösas manuellt. Någon som är bekant med innehållet måste bestämma vilken av de två noderna som ska tas bort, med hänsyn tagen till annat innehåll som refererar till det. Lösningen kan kräva att extraheringen av den övre delen görs igen utan den felande noden.

### Inmatningsfel högst upp på grund av att det inte går att ta bort referensnod

En annan vanlig orsak till [Inmatning uppifrån](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) fel är en versionskonflikt för en viss nod i målinstansen. Identifiera felet genom att hämta matningsloggen med användargränssnittet i Cloud Acceleration Manager och leta efter en post som följande:
>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakIntegrity001: Det går inte att ta bort refererad nod: 8a2289f4-b904-4bd0-8410-15e41e 0976a8

Detta kan inträffa om en nod på målet ändras mellan ett intag och ett efterföljande toppmängdintag så att en ny version har skapats. Om inmatningen har inkluderingsversioner aktiverat kan en konflikt uppstå eftersom målet nu har en senare version som refereras av versionshistorik och annat innehåll. Det går inte att ta bort den felaktiga versionsnoden eftersom den refereras.

Lösningen kan kräva att extraheringen av den övre delen görs igen utan den felande noden. Eller skapa en liten migreringsuppsättning av den felande noden, men med inkluderingsversioner inaktiverade.

Bästa tillvägagångssätt visar att om ett intag måste köras med wipe=false och&quot;include versions&quot;=true är det viktigt att innehållet på målet ändras så lite som möjligt, tills migreringsresan är klar. I annat fall kan dessa konflikter uppstå.


## What&#39;s Next {#whats-next}

När importen är klar AEM indexeringen startas automatiskt. Se [Indexering efter migrering av innehåll](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/indexing-content.md) för mer information.

När du har slutfört Inkludering av innehåll i Cloud Servicen kan du visa loggar för varje steg (extrahering och förtäring) och leta efter fel. Se [Visa loggar för en migreringsuppsättning](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/viewing-logs.md) om du vill veta mer.

