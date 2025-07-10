---
title: Versionsinformation för Cloud Manager 2025.7.0
description: Läs om Cloud Manager 2025.7.0 i Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: cf36a5f22132695be47c3d52292f59f785a0fd52
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 0%

---

# Versionsinformation om Cloud Manager 2025.7.0 i Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Läs om Cloud Manager 2025.7.0 i AEM (Adobe Experience Manager) as a Cloud Service.

Se även [aktuell versionsinformation för Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Releasedatum {#release-date}

Lanseringsdatumet för Cloud Manager 2025.7.0 i AEM as a Cloud Service är torsdagen den 10 juli 2025.

Nästa planerade version är torsdagen den 7 augusti 2025.

## Nyheter {#what-is-new}

* **Cloud Manager lägger till stöd för ECDSA-certifikat (Elliptic Curve Digital Signature Algorithm)**

  Cloud Manager har nu stöd för ECDSA-certifikat. Funktionen ger stark säkerhet med mindre nyckelstorlekar, vilket gör det möjligt för kunderna att använda lätt modern kryptografi i sina CDN-konfigurationer. <!-- https://jira.corp.adobe.com/browse/CMGR-62399 -->

* **Ladda ned licensanvändningsrapport för webbplats**

  På sidan **Webbplatsanvändningsinformation** (i Cloud Manager klickar du på **Licens**). I lösningstabellen klickar du på **Visa användningsinformation** på raden **Platser** och klickar sedan på **Hämta rapport** om du vill exportera data som en CSV-fil. Nedladdningen förenklar analys och delning av användningsmönster. <!-- https://jira.corp.adobe.com/browse/CMGR-42274 -->

  ![Sidan med användningsinformation för webbplatser](/help/implementing/cloud-manager/release-notes/assets/sites-license-usage-page.png)

  Se [Kontrollpanel för licenser](/help/implementing/cloud-manager/license-dashboard.md).

## Tidiga adoptionsprogram {#private-beta-program}

Delta i Cloud Manager alfa- och betaprogram för att få exklusiv tillgång till kommande funktioner innan de släpps.

Följande möjligheter är för närvarande tillgängliga:

### Enklicksåterställning för pipeline-distributioner {#one-click-rollback}

Återgå snabbt till en tidigare distribution om den senaste kundkällkoden inte fungerar som förväntat - du behöver inte köra om hela pipelinen eller återställa implementeringar manuellt.<!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

![Återställ kundens källkod från miljökortet](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed.png) *Miljökortet ovan med alternativet **Återställ**>**Tidigare kod som distribuerats**för en vald miljö.*


![Återställ föregående dialogruta för koddistribution](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed-dialogbox.png)
*I dialogrutan **Återställ tidigare kod som distribuerats**granskar du den version som är distribuerad och den version som du vill återställa. Klicka sedan på&#x200B;**Bekräfta***.


![Återställer aktiveringen](/help/implementing/cloud-manager/release-notes/assets/restoring-previous-code-deployed-restoring.png)
*Cloud Manager återställer miljön till den tidigare versionen, bibehåller innehållet och konfigurationen intakt och markerar miljön **Återställning**tills distributionen är klar.*


![Source-kodversionen används](/help/implementing/cloud-manager/release-notes/assets/environments-view-details-sourcecodeversion.png) *Vyn Miljöinformation, som visas ovan, visar nu även den aktiva källkodsversionen som används.*

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [restorecode@adobe.com](mailto:restorecode@adobe.com) från den e-postadress som är kopplad till din Adobe ID.

Se även [Innehållsåterställning i AEM as a Cloud Service](/help/operations/restore.md).


### Specialiserad testmiljö {#specialized-test-environment}

Cloud Manager stöder nu tillägg av en ny miljötyp som kallas **Specialiserad testmiljö**. Miljön är utformad för att hjälpa team att validera funktioner under förhållanden nära produktionsförhållanden innan de publicerar. Den här miljötypen skiljer sig från *Produktion + Stage*, *Utveckling* eller *Snabb utveckling* och erbjuder ett fokuserat utrymme för att köra avancerade valideringsscenarier.

Senaste förbättringar: Nu kan du konfigurera specialiserade testmiljöer på icke-produktionsflöden via ett enklare och mer intuitivt arbetsflöde. Den strömlinjeformade installationen snabbar upp slutförandet och minskar antalet konfigurationsfel.

Se [Lägg till en anpassad testmiljö](/help/implementing/cloud-manager/specialized-test-environment.md).

![Dialogrutan Lägg till miljö med alternativknappen Specialiserad testmiljö markerad](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) från den e-postadress som är kopplad till din Adobe ID.


### Använd din egen Git (BYOG) - nu med stöd för Azure DevOps {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

Kunderna kan nu lägga in sina Azure DevOps Git-databaser i Cloud Manager, med stöd för både moderna Azure DevOps-databaser och äldre VSTS-databaser (Visual Studio Team Services).

* För Edge Delivery Services-användare kan den inbyggda databasen användas för att synkronisera och distribuera platskod.
* För AEM as a Cloud Service- och Adobe Managed Services-användare (AMS) kan databasen länkas till både fullständiga och frontbaserade pipelines.

Stöd för fler pipelinetyper och pull-begäran-validering via pipelines för kodkvalitet kommer snart.

Se [Lägg till externa databaser i Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Dialogrutan Lägg till databas](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) från den e-postadress som är kopplad till din Adobe ID. Ta med vilken Git-plattform du vill använda och om du har en privat/offentlig eller företagsdatabasstruktur.


**Frågor och svar om BYOG**

| Fråga | Svar |
|---|---|
| *Hur kan ett projekt vid behov växla tillbaka till den Adobe-hanterade Git-databasen?* | Det är enkelt att byta tillbaka. [Uppdatera pipelines](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) så att de pekar på Adobe-databasen och tar bort den externa databasen om den inte längre behövs. |
| *Går det att konfigurera olika databaser för olika miljöer (till exempel icke-produktion kontra produktion) så att testning i icke-produktion först tillåts?* | Ja, olika databaser kan konfigureras för olika miljöer. Utvecklings- eller kodkvalitetsflödet kan till exempel peka på en extern databas medan produktionsflödet är anslutet till Adobe-databasen. Kontrollera att synkroniseringsjobbet mellan de två databaserna förblir aktivt under den här konfigurationen. |
| *Fortsätter befintliga inställningar som IP tillåtelselista att fungera?* | Ja, befintlig IP-tillåtelselista fortsätter att fungera som vanligt. Om den externa Git-databasen skyddas av en brandvägg måste de nödvändiga [Adobe IP-adresserna läggas till i tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/introduction.md). |
| *Fungerar alla URL:er för GitLab-databasen? Databas-URL:en som används har formatet `https://gitlab_dedicated_url.com/path/repo-name.git`, vilket skiljer sig från exemplet i dokumentationen.* | Ja, alla GitLab-databaser som har stöd för API V3 eller V4 stöds, inklusive GitLab-URL:er som de som finns som värd, som den som beskrivs i [Lägg till externa databaser i Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`). |


#### Hantera åtkomsttoken{#manage-access-tokens}

Använd **Hantera åtkomsttoken** i Cloud Manager för att visa, byta namn på och ta bort åtkomsttoken som är kopplade till externa BYOG-databaser, som GitHub Enterprise, GitLab, Bitbucket och Azure DevOps.

Se [Hantera åtkomsttoken](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) från den e-postadress som är kopplad till din Adobe ID.


### Lägg till Edge Delivery Config Pipeline {#add-eds-pipeline}

Config Pipelines stöds nu för sajter som byggts med Edge Delivery Services, vilket ger fler möjligheter än bara Cloud Service-miljöer. Du kan använda **Konfigurera pipelines** för att hantera inställningar som trafikfiltreringsregler och konfigurationer för WAF (Web Application Firewall), där det är tillämpligt. Se [Konfigurationer som stöds](/help/operations/config-pipeline.md#configurations).

![Lägg till Edge Delivery-pipeline i den nedrullningsbara listan Lägg till pipeline](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *Lägger till en Edge Delivery-pipeline från sidan **Programöversikt**,**Pipelines**-kort.*

![Lägg till dialogrutan för Edge Delivery-pipeline](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *Lägg till Edge Delivery-dialogrutan för pipeline.*

Om du är intresserad av att testa den här nya funktionen och dela med dig av dina synpunkter skickar du ett e-postmeddelande till [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) från den e-postadress som är kopplad till din Adobe ID.


## Felkorrigeringar

* Cloud Manager uppdaterar nu releaseversionen för alla pipelines under miljöuppgraderingar, vilket ger en konsekvent versionshantering för alla pipelinetyper. <!-- CMGR-69043 -->
* Gränssnittet visar nu statusmeddelanden och detaljerade felmeddelanden när ett SSL-certifikat för domänvalidering (DV) misslyckas, vilket hjälper till att förstå och lösa certifikatproblem. <!-- CMGR-68872 -->
* När du redigerar en domänmappning förhindrar nu användargränssnittet att SSL-certifikat som inte matchar den valda domänen väljs, vilket minskar antalet felkonfigurationer och förbättrar tillförlitligheten under konfigurationen. <!-- CMGR-64307 -->
* I vissa situationer togs certifikaten inte bort korrekt, och domänen är fortfarande aktiv. <!-- CMGR-69867 -->
* Ett problem som i vissa fall kunde blockera uppgraderingar från *Adobe Assets* till *Adobe Assets Ultimate* har åtgärdats. Övergångarna är nu smidigare och mer tillförlitliga. <!-- CMGR-69506 -->
* Ett problem där nyckelområdesfält ställs in automatiskt när miljöer med flera regioner skapas som stöd för tjänster och distributioner har åtgärdats. <!-- CMGR-69471 -->
* Ett problem där vissa konfigurationspipelines inte stoppades korrekt efter körningen har åtgärdats. Nu är rörledningarna klara och stängda som förväntat, vilket förbättrar tillförlitligheten. <!-- CMGR-69344 -->


<!-- ## Known issues {#known-issues} -->

