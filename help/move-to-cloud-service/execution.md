---
title: Körningsfas
description: Körningsfas
translation-type: tm+mt
source-git-commit: 0dd05c1f6dc197daf154d4df6e6661e00455b233
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 100%

---


# Körning {#execution-phase}

Innan du startar körningsfasen bör du genomgå en introduktion till Cloud Service. Du måste också bekanta dig med Cloud Manager eftersom det är den enda mekanismen för att driftsätta kod till AEM Cloud Service.

Med Cloud Manager kan organisationer själva hantera AEM i molnet. Det innehåller ett ramverk för kontinuerlig integrering och kontinuerligt leverans (CI/CD) som gör att IT-team och implementeringspartners kan snabba upp leveransen av anpassningar eller uppdateringar utan att kompromissa med prestanda eller säkerhet.

Mer information finns i följande resurser nedan: 

* [Onboarding för Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/home.html) för att förstå självhjälpsresurser om onboarding för Experience Manager as a Cloud Service.

* [Integrera Git med Adobe Cloud Manager](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) för att lära dig mer om hur du använder en enstaka Git-databas för att driftsätta kod.

* [Adobe Experience as a Cloud Service-konfiguration](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/security/ims-support.html#aem-configuration) för att lära dig mer om hur du hanterar produkter och användaråtkomst i Admin Console.


## Introduktion {#introduction}

De exakta stegen i övergången till Cloud Service beror på vilka system du har köpt och vilka metoder du följer för programvaruutveckling.

I följande bild visas de huvudsakliga steg som ingår i körningsfasen:

![bild](/help/move-to-cloud-service/assets/exec-image1.png)

## Innehållsöverföring {#content-transfer}

Om du vill överföra innehåll från din aktuella AEM-instans till din Cloud Service-instans kan du använda Adobes verktyg för innehållsöverföring.

Med det här verktyget kan du ange önskad delmängd av innehållet som du vill överföra från din AEM-källinstans till din AEM Cloud Service-instans.

>[!NOTE]
>Vi rekommenderar att du gör regelbundna uppdateringar av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda Cloud Service.

Mer information finns i [Verktyget för innehållsöverföring](/help/move-to-cloud-service/content-transfer-tool/overview-content-transfer-tool.md).

>[!IMPORTANT]
>Lägsta systemkrav för verktyget för innehållsöverföring är AEM 6.3 + och JAVA 8. Om du har en tidigare AEM-version måste du uppgradera din innehållsdatabas till AEM 6.5 för att kunna använda verktyget för innehållsöverföring.

## Omstrukturering av kod {#code-refactor}

Att utveckla och köra kod i AEM as a Cloud Service kräver en förändring i tänkesättet. Observera att koden måste vara flexibel, särskilt eftersom en instans kan avbrytas när som helst. Kod som körs i Cloud Service måste vara medveten om att den alltid körs i ett kluster. Det innebär att fler än en instans alltid körs.

Vissa ändringar krävs i AEM Maven-projekt för att de ska vara kompatibla med AEM as a Cloud Service. AEM as a Cloud Service kräver att *innehåll* och *kod* delas upp i separata paket för driftsättning till AEM.

* `/apps` och `/libs` betraktas som oföränderliga områden i AEM, eftersom de inte kan ändras (skapa, uppdatera, ta bort) efter att AEM startats (dvs. vid körning). Alla försök att ändra ett oföränderligt område vid körning misslyckas.

* Allt annat i databasen, `/content` , `/conf` , `/var` , `/home` , `/etc` , `/oak:index` , `/system` , `/tmp` osv. är ändringsbara områden, vilket innebär att de kan ändras under körning.

Mer information finns i [Rekommenderad paketstruktur](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#recommended-package-structure).

Det finns ytterligare riktlinjer för utveckling som du behöver vara medveten om när du utvecklar på AEM as a Cloud Service. Läs mer i [Utvecklingsriktlinjer för AEM as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html).

I din planeringsfas bör du ha en lista över områden som behöver omarbetas för att vara kompatibla med Cloud Service. Du bör även läsa [Utvecklingsriktlinjer](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html) för mer information om hur du strukturerar om och optimerar koden för att gå över till Cloud Service.

Du kan använda följande verktyg för att snabba upp vissa av dina åtgärder inom omstrukturering av kod:

* [Resursarbetsflödesmigrering](/help/move-to-cloud-service/moving-to-aem-assets/asset-workflow-migration-tool.md)
* [Dispatcher Converter](/help/move-to-cloud-service/refactoring-tools/dispatcher-transformation-utility-tools.md)
* [Moderniseringsverktyg](/help/move-to-cloud-service/refactoring-tools/aem-modernization-tools.md) 

Vi rekommenderar att du strukturerar om och testar koden lokalt innan du skickar den till en Cloud Service-miljö via Cloud Manager Git.

Läs dokumentationen för [AEM SDK](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#aem-as-a-cloud-service-sdk) om du vill veta mer.

Nedan anges ytterligare resurser:

* Titta på Installera Dispatcher SDK om du vill veta hur du installerar Dispatcher SDK:

   >[!VIDEO](https://video.tv.adobe.com/v/30601)

* Titta på Konfigurera Dispatcher SDK om du vill veta hur du konfigurerar Dispatcher SDK:

   >[!VIDEO](https://video.tv.adobe.com/v/30602)

* Granska dokumentationen för [lokal utvecklingskonfiguration](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html) om du vill konfigurera en lokal utvecklingsmiljö


Om du vill hantera den pågående kodutvecklingen på din aktiva AEM-fil tillsammans med omstruktureringen av kod som en del av din övergång bör du schemalägga en frysperiod tills du har slutfört omstruktureringen av ditt Maven-projekt så att det blir kompatibelt med AEM as a Cloud Service.

När projektomstruktureringen är klar kan du återuppta utvecklingen av ny kod baserat på den nya strukturen. Detta minskar antalet fel i pipeline för Cloud Manager under koddriftsättning och testning.

>[!NOTE]
>Aktiviteterna för innehållsöverföring och omstrukturering av kod behöver inte utföras sekventiellt. Dessa åtgärder kan utföras oberoende av varandra. Korrekt projektstruktur krävs dock för att innehållet ska återges korrekt i Cloud Service-miljön.

## Bästa metoder för koddriftsättning och testning {#best-practices}

Körningar av pipeline för Cloud Manager för Cloud Services stöder körning av tester som körs mot mellanlagringsmiljön.

Läs [Kodkvalitetstestning](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#code-quality-testing) om du vill veta hur du skriver testskript och om rekommenderad täckning på minst 50 %.

Läs även [Förstå regler för anpassad kodkvalitet](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/custom-code-quality-rules.html) om du vill veta mer om regler för anpassad kodkvalitet som körs av Cloud Manager och som skapats utifrån bästa praxis från AEM Engineering.

Användning av Cloud Manager är den enda mekanismen för att driftsätta kod till Cloud Service-miljöer.

Följ resurserna nedan för att lära dig hur du använder Cloud Manager för att hantera och driftsätta kod.

* [Hantera miljöer](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html)

* [Konfigurera CI-CD-pipeline](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html)

* [Driftsätta kod](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html)

## Bästa praxis för publiceringsförberedelse {#go-live}

För att säkerställa en smidig och framgångsrik publicering av AEM as a Cloud Service bör du överväga att utföra följande steg:

* Schemalägga kod och frysperiod för innehåll
* Utföra den slutliga innehållsuppdateringen
* Slutföra testiterationer
* Köra prestanda- och säkerhetstester
* Kom igång
