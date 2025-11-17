---
title: Inmatning av innehåll i Cloud Service
description: Lär dig hur du använder Cloud Acceleration Manager för att importera innehåll från din migreringsuppsättning till en Cloud Service-målinstans.
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
feature: Migration
role: Admin
source-git-commit: 7c0703d746601742a28c3c98f35e69de70f25e05
workflow-type: tm+mt
source-wordcount: '3647'
ht-degree: 1%

---

# Inmatning av innehåll i Cloud Service {#ingesting-content}

## Inmatningsprocess i Cloud Acceleration Manager {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Innehållsintag"
>abstract="Inmatning avser att hämta innehåll från migreringsuppsättningen till Cloud Service-målinstansen. Content Transfer Tool har en funktion för differentiell innehållsuppdatering som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content#top-up-extraction-process" text="Extrahering uppifrån"

Följ stegen nedan för att importera din migreringsuppsättning med Cloud Acceleration Manager:

1. Gå till Cloud Acceleration Manager. Klicka på projektkortet och klicka på kortet för innehållsöverföring. Navigera till **Inmatningsjobb** och klicka på **Nytt inlägg**

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Granska checklistan för konsumtion och se till att alla steg är slutförda. Dessa steg är nödvändiga för att tillförseln ska lyckas. Gå bara till steget **Nästa** om checklistan är slutförd.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. Ange nödvändig information för att skapa ett intag.

   * **Migreringsuppsättning:** Välj den migreringsuppsättning som innehåller extraherade data som Source.
      * Migreringsuppsättningar kommer att upphöra efter en längre inaktivitetsperiod, så det förväntas att intaget sker relativt snart efter att extraktionen har utförts. Granska [migreringsuppsättningen upphör](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) om du vill ha mer information.

   >[!TIP]
   > Om extraheringen körs visas en dialogruta. När extraheringen har slutförts startas intaget automatiskt. Om extraheringen misslyckas eller stoppas kommer intagningsjobbet att avbrytas.

   * **Mål:** Välj målmiljö. I den här miljön importeras migreringsuppsättningens innehåll.
      * Inställningarna stöder inte mål av typen Rapid Development Environment (RDE) eller Preview, och de visas inte som ett möjligt målval, även om användaren har tillgång till det.
      * En migreringsuppsättning kan importeras till flera destinationer samtidigt, men målet kan vara att bara ha ett som kör eller väntar på inmatning åt gången.

   * **Nivå:** Välj nivån. (Författare/Publicera).
      * Om källan var `Author` rekommenderar vi att du importerar den till `Author`-nivån på målet. Om källan var `Publish` bör målet också vara `Publish`.

   >[!NOTE]
   > Om målnivån är `Author` stängs författarinstansen av under den tid som inmatningen pågår och blir otillgänglig för användare (till exempel författare eller alla som utför underhåll). Orsaken är att skydda systemet och förhindra alla ändringar som antingen kan gå förlorade eller orsaka en konflikt i ett intag. Se till att ditt team är medvetna om detta. Observera också att miljön visas i viloläge under författarintaget.

   >[!NOTE]
   > Om målnivån är `Publish` fortsätter publiceringsinstansen att köras under inmatning.  Men om komprimeringsprocessen körs medan intag sker är det troligt att en konflikt uppstår mellan de två processerna.  Av den anledningen inaktiverar inmatningsprocessen (1) det tidsbestämda skriptet för komprimeringen så komprimeringen inte startar under intaget, och 2) kontrollerar om komprimeringen körs och i så fall väntar på att den ska slutföras innan intaget fortsätter.  Om publiceringsintaget tar längre tid än förväntat bör du kontrollera om det finns relaterade loggsatser i användningsloggarna.

   * **Rensa:** Välj värdet `Wipe`
      * Alternativet **Rensa** anger målets startpunkt för importen. Om **Rensa** är aktiverat återställs målet inklusive allt innehåll till den version av AEM som är angiven i Cloud Manager. Om det inte är aktiverat behåller målet sitt aktuella innehåll som startpunkt.
      * Det här alternativet påverkar **INTE** hur innehållsintaget kommer att utföras. Inmatningen använder alltid en strategi för innehållsersättning och _inte_ en strategi för innehållssammanfogning, så i både **Rensa** och **Ej rensad** kommer inmatningen av en migreringsuppsättning att skriva över innehåll i samma sökväg på målet. Om migreringsuppsättningen till exempel innehåller `/content/page1` och målet redan innehåller `/content/page1/product1`, tar det bort hela `page1`-sökvägen och dess underordnade sidor, inklusive `product1`, och ersätter den med innehållet i migreringsuppsättningen. Detta innebär att noggrann planering måste utföras när du utför ett **icke-rensat**-inlägg till ett mål som innehåller innehåll som ska behållas.
      * Icke-rensningsfrågor är särskilt utformade för att användas i det övre intaget. Dessa förslag är avsedda att innehålla en stegvis mängd nytt innehåll som har ändrats sedan det senaste intaget i en befintlig migreringsuppsättning. Genomgående av icke-rensningsfrågor utanför detta användningsfall kan leda till mycket lång intag.

   >[!IMPORTANT]
   > Om inställningen **Rensa** är aktiverad för den aktuella importen återställs hela den befintliga databasen, inklusive användarbehörigheterna för Cloud Service-målinstansen. Den här återställningen gäller även för en admin-användare som har lagts till i gruppen **administratörer** och den användaren måste läggas till i gruppen Administratörer igen för att kunna starta ett inlägg.

   * **Förkopia:** Välj värdet `Pre-copy`
      * Du kan köra det valfria förkopieringssteget för att avsevärt snabba upp intaget. Mer information finns i [Ingesting with AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy).
      * Om konsumtion med förkopia används (för S3 eller Azure Data Store) bör du endast köra `Author`-intagning. Om du gör det går det snabbare att få tillgång till `Publish` när det körs senare.

   >[!IMPORTANT]
   > Du kan bara initiera en inmatning till målmiljön om du tillhör den lokala gruppen **AEM-administratörer** i Cloud Service-målförfattartjänsten. Om du inte kan påbörja ett inlägg kan du läsa [Det går inte att påbörja inmatningen](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) för mer information.

1. När du har valt ett alternativ för intag kan en uppskattning av dess varaktighet visas. Detta är en uppskattning av bästa möjliga insats baserad på historiska data om liknande inmatningar.

   * Den här uppskattningen beräknas inte eller visas inte för **icke-rensning**-frågor eftersom CAM inte vet hur mycket innehåll som finns på målsystemet i det här fallet.
   * Den här uppskattningen beräknas och visas endast om värdena för Kontrollera storlek för extraheringen har samlats in och är tillgängliga.
   * Detta värde är en uppskattning och bör inte betraktas som exakt, även om det beräknas på ett intelligent sätt. Olika faktorer kan ändra den faktiska varaktigheten.
   * Det här värdet är även tillgängligt i dialogrutan för varaktighet som du kommer åt via åtgärden **Visa varaktighet** för det aktuella inmatningen när inmatningen körs.

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_estimate"
>title="Uppskattning av varaktighet för inmatning"
>abstract="En ungefärlig varaktighet för ett visst intag kan visas för att ge en allmän uppfattning om hur lång tid det kommer att ta. Det finns begränsningar för dess exakthet."

![bild](/help/journey-migration/content-transfer-tool/assets/estimate.png)

1. Klicka på **Infoga**.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. Du kan sedan övervaka intaget från listvyn för förbrukningsjobb och använda matningsens åtgärdsmeny för att visa varaktighet och logg allt eftersom intaget fortskrider.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. Klicka på knappen **(i)** på raden om du vill ha mer information om intagsjobbet. Du kan se varaktigheten för varje steg i Inmatningen när den körs eller slutförs genom att klicka på **..** och sedan på **Visa varaktighet**. Informationen från extraheringen visar också på vad som förtärs.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

## Övre inmatning {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="Övre inmatning"
>abstract="Använd den övre funktionen för att flytta innehåll som ändrats sedan föregående innehållsöverföringsaktivitet. Kontrollera loggarna efter eventuella fel eller varningar när Ingeset är klart. Felen ska åtgärdas omedelbart, antingen genom att man hanterar de rapporterade problemen eller genom att kontakta Adobe kundtjänst."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs" text="Visa loggar"

Verktyget Innehållsöverföring har en funktion som tillåter extrahering av differentiellt innehåll genom att utföra en *top-up* av migreringsuppsättningen. Detta gör att migreringsuppsättningen kan ändras så att endast innehåll som har ändrats sedan den föregående extraheringen tas med, utan att allt innehåll behöver extraheras igen.

>[!NOTE]
>Efter den initiala innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du publicerar på Cloud Service. Om du har använt steget före kopiering för det första intaget kan du hoppa över förkopiering för efterföljande toppkopieringsförslag (om den övre migreringsuppsättningsstorleken är mindre än 200 GB). Orsaken är att det kan lägga till tid i hela processen.

Om du vill importera differentiellt innehåll efter att en del inmatningsfrågor är slutförda måste du köra en [extrahering uppifrån](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) och sedan använda inmatningsmetoden med alternativet **Rensa** **inaktiverat**. Läs förklaringen **Rensa** ovan för att undvika att innehåll som redan finns på målet går förlorat.

Börja med att skapa ett matningsjobb och se till att **Rensa** är inaktiverat under matningen, vilket visas nedan:

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## Felsökning {#troubleshooting}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_troubleshooting"
>title="Felsökning av innehållsmatning"
>abstract="Läs i förbrukningsloggarna och dokumentationen för att hitta lösningar på vanliga orsaker till varför ett intag kan misslyckas och hitta ett sätt att åtgärda problemet. När det är klart kan intaget köras igen."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers" text="Verifierar innehållsöverföringar"

### CAM kan inte hämta migreringstoken {#cam-unable-to-retrieve-the-migration-token}

Den automatiska hämtningen av migreringstoken kan misslyckas av olika orsaker, bland annat [att konfigurera ett IP-tillåtelselista via Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) i Cloud Service-målmiljön. I sådana fall visas följande dialogruta när du försöker starta ett intag:

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

Hämta migreringstoken manuellt genom att klicka på länken Hämta token i dialogrutan. En annan flik öppnas som visar token. Du kan sedan kopiera token och klistra in den i fältet **Indata för migreringstoken**. Nu borde du kunna påbörja intaget.

>[!NOTE]
>
>Token är tillgänglig för användare som tillhör den lokala gruppen **AEM-administratörer** i Cloud Service-målförfattartjänsten.

### Det går inte att starta matning {#unable-to-start-ingestion}

Du kan bara initiera en inmatning till målmiljön om du tillhör den lokala gruppen **AEM-administratörer** i Cloud Service-målförfattartjänsten. Om du inte tillhör AEM administratörsgrupp visas ett fel som visas nedan när du försöker starta ett intag. Du kan antingen be din administratör att lägga till dig i de lokala **AEM-administratörerna** eller be om själva token, som du sedan kan klistra in i fältet **Migreringstokenindata**.

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### Det gick inte att nå migreringstjänsten {#unable-to-reach-migration-service}

Efter att ett matningsförslag har begärts kan ett meddelande som följande visas för användaren: &quot;Migreringstjänsten i målmiljön är inte tillgänglig. Om så är fallet, försök igen senare eller kontakta Adobe support.&quot;

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

Det här meddelandet anger att Cloud Acceleration Manager inte kunde nå målmiljöns migreringstjänst för att starta inmatningen. Denna situation kan uppstå av olika skäl.

>[!NOTE]
> 
> Fältet &quot;Migreringstoken&quot; visas eftersom det i ett fåtal fall inte är tillåtet att hämta denna token. Genom att tillåta manuell inmatning kan användaren snabbt påbörja intagningen utan ytterligare hjälp. Om token anges och meddelandet fortfarande visas, var det inte problemet att hämta token.

* AEM as a Cloud Service underhåller miljötillståndet och måste ibland starta om migreringstjänsten av olika vanliga orsaker. Om tjänsten startas om kan den inte nås, men är tillgänglig så småningom.
* Det är möjligt att en annan process körs på instansen. Om [AEM-versionsuppdateringar](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates) till exempel tillämpar en uppdatering kan systemet vara upptaget och migreringstjänsten är inte tillgänglig regelbundet. När den processen är klar kan ett nytt försök att starta intaget göras.
* Om ett [IP-Tillåtelselista har tillämpats](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) via Cloud Manager blockeras Cloud Acceleration Manager från att nå migreringstjänsten. Det går inte att lägga till en IP-adress för frågor eftersom adressen är dynamisk. För närvarande är den enda lösningen att inaktivera IP-tillåtelselista under importen och indexeringen genom att tillfälligt lägga till 0.0.0.0/0 i tillåtelselista medan importen och indexeringen pågår.
* Det kan finnas andra skäl till att en utredning behöver göras. Om det fortfarande inte går att få tillgång till produkten eller indexeringen kontaktar du Adobe kundtjänst.

### Uppdateringar och förslag för AEM-versioner {#aem-version-updates-and-ingestions}

[AEM-versionsuppdateringar](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates) används automatiskt i miljöer för att de ska vara uppdaterade med den senaste AEM as a Cloud Service-versionen. Om uppdateringen utlöses när ett intag utförs, kan det orsaka oförutsägbara resultat, bland annat skador på miljön.

Om&quot;AEM-versionsuppdateringar&quot; introduceras i målprogrammet försöker den inaktivera kön innan den startas. När inmatningen är klar återställs versionsuppdaterarens tillstånd till det som var innan inmatningen startade.

>[!NOTE]
>
> Du behöver inte längre logga en supportanmälan för att inaktivera&quot;AEM Version Updates&quot;.

Om&quot;AEM Version Updates&quot; är aktiv (d.v.s. uppdateringar körs eller köas för att köras), kommer importen inte att börja och följande meddelande visas i användargränssnittet. När uppdateringarna är klara kan intaget startas. Cloud Manager kan användas för att se aktuell status för programmets rörledningar.

>[!NOTE]
>
> &quot;AEM Version Updates&quot; körs i miljön och väntar tills pipeline är klar. Om uppdateringar köas längre än förväntat kontrollerar du att ett anpassat arbetsflöde inte har pipeline oavsiktligt låst.

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_active.png)

### Inmatningsfel på grund av att molnmiljön inte är i klart läge {#ingestion-failure-due-to-cloud-environment-not-in-ready-state}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_cloud_environment_not_in_ready_state"
>title="Molnmiljön är inte i tillståndet Ready"
>abstract="I sällsynta fall kan det uppstå oväntade problem i målmolnmiljön, vilket kan leda till att importen misslyckas."

I sällsynta fall kan målmiljön i Cloud Service ha oväntade problem. Detta resulterar i att intaget misslyckas eftersom miljön inte är i det förväntade tillståndet klar. Kontrollera matningsloggen för att visa mer information om det feltillstånd som påträffats.

Se till att författarmiljön är tillgänglig och vänta några minuter innan du försöker göra om importen. Om problemet kvarstår kan du kontakta kundsupport och få hjälp med felstatus.

### Inmatningsfel i toppklass på grund av Unikhetsbegränsningsöverträdelse {#top-up-ingestion-failure-due-to-uniqueness-constraint-violation}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_uuid"
>title="Felaktigt begränsningsfel"
>abstract="En vanlig orsak till ett icke-rensningsfel är en konflikt i nod-ID:n. Det får bara finnas en av de noder som står i konflikt."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content#top-up-ingestion-process" text="Inmatning uppifrån"

En vanlig orsak till ett [Top-up Inghit](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)-fel är en konflikt i nod-ID:n. Du kan identifiera felet genom att hämta matningsloggen med hjälp av Cloud Acceleration Manager-gränssnittet och leta efter en post som följande:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: Unikhetsvillkoret bröt egenskapen [jcr:uuid] med värdet a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

Varje nod i AEM måste ha ett unikt uuid. Detta fel anger att en nod som importeras har samma UID som en som finns på en annan sökväg i målinstansen. Detta kan bero på två orsaker:

* En nod flyttas till källan mellan en extrahering och en efterföljande [extrahering uppifrån](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)
   * _KOM IHÅG_: För top-up-extraheringar finns noden fortfarande i migreringsuppsättningen, även om den inte längre finns i källan.
* En nod på destinationen flyttas mellan ett intag och ett efterföljande uppåtgående intag.

Den här konflikten måste lösas manuellt. Någon som är bekant med innehållet måste bestämma vilken av de två noderna som ska tas bort, med hänsyn tagen till annat innehåll som refererar till det. Lösningen kan kräva att extraheringen av den övre delen görs igen utan den felande noden.

### Inmatningsfel högst upp på grund av att det inte går att ta bort referensnod {#top-up-ingestion-failure-due-to-unable-to-delete-referenced-node}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_referenced_node"
>title="Det går inte att ta bort referensnod"
>abstract="En vanlig orsak till ett icke-rensningsfel är en versionskonflikt för en viss nod i målinstansen. Versionerna för noden måste repareras."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content#top-up-ingestion-process" text="Inmatning uppifrån"

En annan vanlig orsak till ett [överst inmatningsfel](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) är en versionskonflikt för en viss nod i målinstansen. Du kan identifiera felet genom att hämta matningsloggen med hjälp av Cloud Acceleration Manager-gränssnittet och leta efter en post som följande:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakIntegrity001: Det går inte att ta bort refererad nod: 8a2289f4-b904-4bd0-8410-15e41e 0976a8

Detta kan inträffa om en nod på målet ändras mellan ett intag och ett efterföljande **icke-rensat**-intag så att en ny version har skapats. Om migreringsuppsättningen har extraherats med inkluderingsversioner aktiverat kan en konflikt uppstå eftersom målet nu har en senare version som versionshistorik och annat innehåll refererar till. Det går inte att ta bort den felaktiga versionsnoden eftersom den refereras.

Lösningen kan kräva att extraheringen av den övre delen görs igen utan den felande noden. Eller skapa en liten migreringsuppsättning av den felande noden, men med inkluderingsversioner inaktiverade.

Bästa tillvägagångssätt visar att om ett **icke-rensat**-inlägg måste köras med en migreringsuppsättning som innehåller versioner är det viktigt att innehållet på målet ändras så lite som möjligt, tills migreringsresan är klar. I annat fall kan dessa konflikter uppstå.

### Inmatningsfel på grund av stora nodegenskapsvärden {#ingestion-failure-due-to-large-node-property-values}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_bson"
>title="Stor nodegenskap"
>abstract="En vanlig orsak till att ett fel uppstår i en förtäring är att den maximala storleken för egenskapsvärden för noden har överskridits. Följ dokumentationen, inklusive de som rör BPA-rapporten, för att åtgärda detta."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool" text="Krav för migrering"

Nodegenskapsvärden som lagras i MongoDB får inte överskrida 16 MB. Om ett nodvärde överskrider den storlek som stöds misslyckas importen och loggen innehåller antingen:

* ett `BSONObjectTooLarge`-fel och ange vilken nod som överskrider maxvärdet, eller
* ett `BsonMaximumSizeExceededException`-fel, som anger att det finns en nod som sannolikt innehåller unicode-tecken som överskrider den maximala storleken **

Detta är en MongoDB-begränsning.

Mer information finns i `Node property value in MongoDB`-anteckningen i [Krav för verktyget Innehållsöverföring](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md). Där finns också en länk till ett Oak-verktyg som kan hjälpa dig att hitta alla stora noder. När alla noder med stora storlekar har åtgärdats kör du extraheringen och intaget igen.

Du kan undvika den här begränsningen genom att köra [Best Practices Analyzer](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md) på AEM-källinstansen och granska resultatet som den visar, särskilt [&quot;Repository Structure som inte stöds&quot; (URS)](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/urs) -mönstret.

>[!NOTE]
>
>[Best Practices Analyzer](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md) version 2.1.50+ rapporterar stora noder som innehåller unicode-tecken som överskrider den maximala storleken. Kontrollera att du kör den senaste versionen. BPA-versioner före 2.1.50 identifierar inte och rapporterar om dessa stora noder och de måste identifieras separat med det nödvändiga Oak-verktyget som nämns ovan.

### Inmatningsfel på grund av oväntade återkommande fel {#ingestion-failure-due-to-unexpected-intermittent-errors}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_intermittent_errors"
>title="Oväntade återkommande fel"
>abstract="Ibland kan det uppstå oväntade fel i tjänsten längre fram i kedjan och tyvärr är det enda sättet att försöka på nytt."

Ibland kan oväntade problem ge upphov till misslyckade frågor där det enda sättet att göra detta är att försöka få igen. Undersök matningsloggen för att ta reda på orsaken till felet och se om den är i linje med något av de fel som anges nedan, där ett nytt försök bör göras.

#### MongoDB-problem {#mongo-db-issues}

* `Atlas prescale timeout error` - Inmatningsfasen försöker förskala målmolndatabasen till en lämplig storlek som passar storleken på det migreringsuppsättningsinnehåll som importeras. Oftast slutförs inte den här åtgärden inom den förväntade tidsramen.
* `Exhausted mongo restore retries` - Ett försök att återställa en lokal dump av innehållet i den inkapslade migreringsuppsättningen till molndatabasen har gjorts. Detta tyder på ett övergripande hälso-/nätverksproblem med MongoDB, som ofta läker av sig själv efter några minuter.
* `Mongo network error` - Ibland kan det misslyckas med att upprätta en anslutning till MongoDB, vilket gör att intagsprocessen avslutas tidigt och rapporterar att den misslyckades. Ett enkelt försök att återanvända intaget bör göras.
* `Mongo server selection error` - Detta är ett sällsynt enkelsidigt timeout-fel på klientsidan som kan inträffa av flera underliggande orsaker. Ett efterföljande försök kommer troligen att korrigera problemet.
* `Mongo took too long to start` - I extremt sällsynta fall kan den lokala MongoDB som används i arbetsflödet för förtäring inte startas. Ett efterföljande försök kommer troligen att korrigera problemet.

#### AZCopy-problem {#azcopy-issues}

* `AZCopy critical failure` - I sällsynta fall kan AZCopy-verktyget som används för att utföra pre-copy-steget av intaget misslyckas oväntat. Ett nytt försök att använda detta bör göras i detta fall.

### Inmatningen har avbrutits {#ingestion-rescinded}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_rescinded"
>title="Inmatningen har avbrutits"
>abstract="Extraheringen som intaget väntade på slutfördes inte. Tillträdet avbröts eftersom det inte kunde verkställas."

Ett intag som skapades med en pågående extrahering när dess källmigreringsuppsättning väntar tålt tills extraheringen lyckas och börjar då normalt. Om extraheringen misslyckas eller stoppas börjar inte intaget och indexeringsjobbet utan avbryts. I det här fallet kontrollerar du extraheringen för att fastställa varför den misslyckades, åtgärdar problemet och börjar extrahera igen. När den fasta extraheringen körs kan ett nytt intag schemaläggas.

### Det gick inte att starta väntan på inmatning {#waiting-ingestion-not-started}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_waiting_ingestion_not_started"
>title="Väntar på inmatning har inte startats"
>abstract="Inmatningen kunde inte starta efter att ha väntat på att en extrahering skulle slutföras."

Ett intag som skapades med en pågående extrahering när dess källmigreringsuppsättning väntar tills extraheringen lyckas, och då försöker intaget starta normalt. Om importen inte kan startas markeras den som misslyckad. Möjliga orsaker till att inte starta är: en IP-Tillåtelselista har konfigurerats i målförfattarmiljön. Målmiljön är inte tillgänglig av någon annan anledning.  I det här fallet bör du kontrollera varför det inte gick att starta intaget, åtgärda problemet och sedan påbörja intagandet igen (extraheringen behöver inte göras om).

### Borttagen resurs finns inte efter upprepat förtäring

I allmänhet rekommenderas inte att du ändrar molnmiljödata mellan de olika förslagen.

När en resurs tas bort från Cloud Service-målet med Assets Touch-gränssnittet tas noddata bort, men resursens blob med bilden tas inte bort omedelbart. Den är markerad för borttagning så att den inte längre visas i användargränssnittet. Den finns dock kvar i datalagret tills skräpinsamlingen sker och blobben tas bort.

Om en tidigare migrerad resurs tas bort och nästa inmatning körs innan skräpinsamlaren har slutfört borttagningen av resursen, återställs inte den borttagna resursen om samma migreringsuppsättning används. När intaget kontrolleras i molnmiljön för resursen finns det inga noddata. Inmatningen kopierar därför noddata till molnmiljön. När den kontrollerar blobbutiken ser den dock att blobben finns och hoppar över kopieringen av blobben. Det är därför som metadata förekommer när du tittar på resursen från Touch-gränssnittet, men bilden är inte det. Kom ihåg att migreringsuppsättningar och innehåll inte har utformats för att hantera det här fallet. De vill lägga till nytt innehåll i molnmiljön och inte återställa tidigare migrerat innehåll.

## What&#39;s Next {#whats-next}

När importen är klar startas AEM-indexeringen automatiskt. Mer information finns i [Indexera efter att du har migrerat innehåll](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/indexing-content.md).

När du har slutfört Inkludering av innehåll i Cloud Service kan du visa loggar för varje steg (extrahering och förtäring) och söka efter fel. Mer information finns i [Visa loggar för en migreringsuppsättning](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/viewing-logs.md).
