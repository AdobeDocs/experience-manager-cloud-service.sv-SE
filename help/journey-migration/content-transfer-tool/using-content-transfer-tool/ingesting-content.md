---
title: Infoga innehåll i Cloud Service
description: Lär dig hur du använder Cloud Acceleration Manager för att importera innehåll från din migreringsuppsättning till en instans av en Cloud Service.
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: 4c8565d60ddcd9d0675822f37e77e70dd42c0c36
workflow-type: tm+mt
source-wordcount: '2407'
ht-degree: 1%

---

# Infoga innehåll i Cloud Service {#ingesting-content}

## Inmatningsprocess i Cloud Acceleration Manager {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Innehållsintag"
>abstract="Inmatning avser att hämta innehåll från migreringsuppsättningen till målinstansen för Cloud Service. Content Transfer Tool har en funktion för differentiell innehållsuppdatering som gör att du kan överföra enbart de ändringar som gjorts sedan den föregående innehållsöverföringen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html#top-up-extraction-process" text="Extrahering uppifrån"

Följ stegen nedan för att importera din migreringsuppsättning med Cloud Acceleration Manager:

1. Gå till Cloud Acceleration Manager. Klicka på projektkortet och klicka på kortet för innehållsöverföring. Navigera till **Inmatningsjobb** och klicka **Nytt intag**

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Granska checklistan för konsumtion och se till att alla steg är slutförda. Dessa steg är nödvändiga för att tillförseln ska lyckas. Gå till **Nästa** endast om checklistan är slutförd.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. Ange nödvändig information för att skapa ett intag.

   * **Migreringsuppsättning:** Välj den migreringsuppsättning som innehåller extraherade data som källa.
      * Migreringsuppsättningar kommer att upphöra efter en längre inaktivitetsperiod, så det förväntas att intaget sker relativt snart efter att extraktionen har utförts. Granska [Förfallotid för migreringsuppsättning](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) för mer information.

   >[!TIP]
   > Om extraheringen körs visas en dialogruta. När extraheringen har slutförts startas intaget automatiskt. Om extraheringen misslyckas eller stoppas kommer intagningsjobbet att avbrytas.

   * **Mål:** Välj målmiljö. I den här miljön importeras migreringsuppsättningens innehåll.
      * Inställningarna har inte stöd för en Rapid Development Environment-destination (RDE) och de visas inte som ett möjligt målval, även om användaren har åtkomst till den.
      * En migreringsuppsättning kan importeras till flera destinationer samtidigt, men målet kan vara att bara ha ett som kör eller väntar på inmatning åt gången.

   * **Nivå:** Välj nivån. (Författare/Publicera).
      * Om källan var `Author`rekommenderar vi att du importerar det till `Author` på målet. Om källan var `Publish`, ska målet vara `Publish` också.

   >[!NOTE]
   > Om målnivån är `Author`, stängs författarinstansen av under den tid som inmatningen pågår och blir otillgänglig för användare (till exempel författare eller alla som utför underhåll). Orsaken är att skydda systemet och förhindra alla ändringar som antingen kan gå förlorade eller orsaka en konflikt i ett intag. Se till att ditt team är medvetna om detta. Observera också att miljön visas i viloläge under författarintaget.

   * **Svep:** Välj `Wipe` value
      * The **Svep** anger målets startpunkt för inmatningen. If **Svep** är aktiverat återställs målet, inklusive allt innehåll, till den version av AEM som anges i Cloud Manager. Om det inte är aktiverat behåller målet sitt aktuella innehåll som startpunkt.
      * Det här alternativet gör det **NOT** påverka hur innehållsintaget kommer att ske. Inmatningen använder alltid en innehållsersättningsstrategi och _not_ en strategi för sammanfogning av innehåll så att, i båda **Svep** och **Ej svep** om en migreringsuppsättning matas in skrivs innehållet i samma sökväg över på destinationen. Om till exempel migreringsuppsättningen innehåller `/content/page1` och målet innehåller redan `/content/page1/product1`, tar det bort hela `page1` bana och dess undersidor, inklusive `product1`och ersätt den med innehållet i migreringsuppsättningen. Detta innebär att noggrann planering måste göras när du utför en **Ej svep** Inmatning till ett mål som innehåller innehåll som bör behållas.

   >[!IMPORTANT]
   > Om inställningen **Svep** är aktiverat för inmatningen, återställs hela den befintliga databasen inklusive användarbehörigheter för målinstansen av Cloud Servicen. Återställningen gäller även för en admin-användare som lagts till i **administratörer** gruppen och den användaren måste läggas till i administratörsgruppen igen för att påbörja ett intag.

   * **Förkopia:** Välj `Pre-copy` value
      * Du kan köra det valfria förkopieringssteget för att avsevärt snabba upp intaget. Se [Ingesting with AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) för mer information.
      * Om du använder inmatning med förkopia (för S3 eller Azure Data Store) bör du köra `Author` enbart intag. Det snabbar upp `Publish` intag när det körs senare.

   >[!IMPORTANT]
   > Du kan bara initiera ett intag till målmiljön om du tillhör den lokala **AEM administratörer** på Cloud Servicens författartjänst. Om du inte kan påbörja ett intag, se [Det går inte att starta matning](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) för mer information.

1. Klicka **Ingest**.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. Du kan sedan övervaka intaget från listvyn för förbrukningsjobb och använda matningsens åtgärdsmeny för att visa varaktighet och logg allt eftersom intaget fortskrider.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. Klicka på **(i)** om du vill ha mer information om intagsjobbet. Du kan se hur länge varje steg i Inledningen varar när den körs eller slutförs genom att klicka **...** och sedan klicka **Visa varaktighet**. Informationen från extraheringen visar också på vad som förtärs.

   ![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

## Övre inmatning {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="Övre inmatning"
>abstract="Använd den övre funktionen för att flytta innehåll som ändrats sedan föregående innehållsöverföringsaktivitet. Kontrollera loggarna efter eventuella fel eller varningar när Ingeset är klart. Felen bör åtgärdas omedelbart, antingen genom att man hanterar de rapporterade problemen eller genom att kontakta Adobe kundtjänst."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html" text="Visa loggar"

Verktyget Innehållsöverföring har en funktion som gör att du kan extrahera differentiellt innehåll genom att utföra en *uppifrån* av migreringsuppsättningen. Detta gör att migreringsuppsättningen kan ändras så att endast innehåll som har ändrats sedan den föregående extraheringen tas med, utan att allt innehåll behöver extraheras igen.

>[!NOTE]
>Efter den initiala innehållsöverföringen bör du göra regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du publicerar på Cloud Servicen. Om du har använt steget före kopiering för det första intaget kan du hoppa över förkopiering för efterföljande toppkopieringsförslag (om den övre migreringsuppsättningsstorleken är mindre än 200 GB). Orsaken är att det kan lägga till tid i hela processen.

Om du vill importera differentierat innehåll efter att en del inmatningar är slutförda måste du köra en [Extrahering uppifrån och ned](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)och sedan använda metoden för att få ett intag med **Svep** option **inaktiverad**. Läs mer i **Svep** ovan för att undvika att innehåll som redan finns på målet går förlorat.

Börja med att skapa ett matningsjobb och se till att **Svep** är inaktiverat under intaget, vilket visas nedan:

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## Felsökning {#troubleshooting}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_troubleshooting"
>title="Felsökning av innehållsmatning"
>abstract="Läs i förbrukningsloggarna och dokumentationen för att hitta lösningar på vanliga orsaker till varför ett intag kan misslyckas och hitta ett sätt att åtgärda problemet. När det är klart kan intaget köras igen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html" text="Verifierar innehållsöverföringar"

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
* Det är möjligt att en annan process körs på instansen. Om [Uppdateringar av AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html) installerar en uppdatering, systemet kanske är upptaget och migreringstjänsten är inte tillgänglig regelbundet. När den processen är klar kan ett nytt försök att starta intaget göras.
* Om en [IP-Tillåtelselista har tillämpats](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) via Cloud Manager blockerar det Cloud Acceleration Manager från att nå migreringstjänsten. Det går inte att lägga till en IP-adress för frågor eftersom adressen är dynamisk. För närvarande är den enda lösningen att inaktivera IP-tillåtelselista under importen och indexeringen.
* Det kan finnas andra skäl till att en utredning behöver göras. Om det fortfarande inte går att få tillgång till produkten eller indexeringen kontaktar du Adobe kundtjänst.

### AEM och förslag {#aem-version-updates-and-ingestions}

[Uppdateringar av AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html) används automatiskt i miljöer för att hålla dem uppdaterade med den senaste AEM as a Cloud Service versionen. Om uppdateringen utlöses när ett intag utförs, kan det orsaka oförutsägbara resultat, bland annat skador på miljön.

Om&quot;AEM versionsuppdateringar&quot; introduceras i målprogrammet försöker den att inaktivera kön innan den startar. När inmatningen är klar återställs versionsuppdaterarens tillstånd till det som var innan inmatningen startade.

>[!NOTE]
>
> Du behöver inte längre logga en supportanmälan för att inaktivera AEM versionsuppdateringar.

Om&quot;AEM versionsuppdateringar&quot; är aktiv (d.v.s. uppdateringar körs eller köas för att köras), kommer importen inte att börja och följande meddelande visas i användargränssnittet. När uppdateringarna är klara kan intaget startas. Molnhanteraren kan användas för att se det aktuella läget för programmets pipelines.

>[!NOTE]
>
> &quot;AEM versionsuppdateringar&quot; körs i miljöns pipeline och väntar tills pipeline är klar. Om uppdateringar köas längre än förväntat kontrollerar du att ett anpassat arbetsflöde inte har pipeline oavsiktligt låst.

![bild](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_active.png)

### Inmatningsfel i toppklass på grund av Unikhetsbegränsningsöverträdelse {#top-up-ingestion-failure-due-to-uniqueness-constraint-violation}

En vanlig orsak till [Inmatning uppifrån](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) fel är en konflikt i nod-ID:n. Identifiera felet genom att hämta matningsloggen med användargränssnittet i Cloud Acceleration Manager och leta efter en post som följande:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakConstraint0030: Unikhetsvillkoret bröt egenskap [jcr:uuid] med värdet a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5e5: /some/path/jcr:content, /some/other/path/jcr:content

Varje nod i AEM måste ha ett unikt uuid. Detta fel anger att en nod som importeras har samma UID som en som finns på en annan sökväg i målinstansen. Detta kan bero på två orsaker:

* En nod flyttas på källan mellan en extrahering och en efterföljande [Extrahering uppifrån och ned](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)
   * _KOM IHÅG_: För top-up-extraheringar finns noden fortfarande i migreringsuppsättningen, även om den inte längre finns i källan.
* En nod på destinationen flyttas mellan ett intag och ett efterföljande uppåtgående intag.

Den här konflikten måste lösas manuellt. Någon som är bekant med innehållet måste bestämma vilken av de två noderna som ska tas bort, med hänsyn tagen till annat innehåll som refererar till det. Lösningen kan kräva att extraheringen av den övre delen görs igen utan den felande noden.

### Inmatningsfel högst upp på grund av att det inte går att ta bort referensnod {#top-up-ingestion-failure-due-to-unable-to-delete-referenced-node}

En annan vanlig orsak till [Inmatning uppifrån](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) fel är en versionskonflikt för en viss nod i målinstansen. Identifiera felet genom att hämta matningsloggen med användargränssnittet i Cloud Acceleration Manager och leta efter en post som följande:

>java.lang.RuntimeException: org.apache.jackrabbit.oak.api.CommitFailedException: OakIntegrity001: Det går inte att ta bort refererad nod: 8a2289f4-b904-4bd0-8410-15e41e 0976a8

Detta kan inträffa om en nod på målet ändras mellan ett intag och en efterföljande **Ej svep** så att en ny version har skapats. Om migreringsuppsättningen har extraherats med inkluderingsversioner aktiverat kan en konflikt uppstå eftersom målet nu har en senare version som versionshistorik och annat innehåll refererar till. Det går inte att ta bort den felaktiga versionsnoden eftersom den refereras.

Lösningen kan kräva att extraheringen av den övre delen görs igen utan den felande noden. Eller skapa en liten migreringsuppsättning av den felande noden, men med inkluderingsversioner inaktiverade.

Bästa tillvägagångssätt visar att om en **Ej svep** Tillförsel måste utföras med en migreringsuppsättning som innehåller versioner, det är viktigt att innehållet på destinationen ändras så lite som möjligt, tills migreringsresan är klar. I annat fall kan dessa konflikter uppstå.

### Inmatningsfel på grund av stora nodegenskapsvärden {#ingestion-failure-due-to-large-node-property-values}

Nodegenskapsvärden som lagras i MongoDB får inte överskrida 16 MB. Om ett nodvärde överskrider den storlek som stöds misslyckas importen och loggen innehåller en `BSONObjectTooLarge` fel och ange vilken nod som överskrider maxgränsen. Detta är en MongoDB-begränsning.

Se `Node property value in MongoDB` anteckning i [Krav för verktyget Innehållsöverföring](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md) om du vill ha mer information och en länk till ett ekverktyg som kan hjälpa dig att hitta alla stora noder. När alla noder med stora storlekar har åtgärdats kör du extraheringen och intaget igen.

### Inmatningen har avbrutits {#ingestion-rescinded}

Ett intag som skapades med en pågående extrahering när dess källmigreringsuppsättning väntar tålt tills extraheringen lyckas och börjar då normalt. Om extraheringen misslyckas eller stoppas börjar inte intaget och indexeringsjobbet utan avbryts. I det här fallet kontrollerar du extraheringen för att fastställa varför den misslyckades, åtgärdar problemet och börjar extrahera igen. När den fasta extraheringen körs kan ett nytt intag schemaläggas.

## What&#39;s Next {#whats-next}

När importen är klar AEM indexeringen startas automatiskt. Se [Indexering efter migrering av innehåll](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/indexing-content.md) för mer information.

När du har slutfört Inkludering av innehåll i Cloud Servicen kan du visa loggar för varje steg (extrahering och förtäring) och leta efter fel. Se [Visa loggar för en migreringsuppsättning](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/viewing-logs.md) om du vill veta mer.
