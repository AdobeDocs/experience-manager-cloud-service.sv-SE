---
title: Körningsfas
description: Körningsfas
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 4%

---


# Körning {#execution-phase}

Innan du startar körningsfasen bör du vara registrerad på molntjänsten. Du måste också bekanta dig med Cloud Manager eftersom det är den enda mekanismen för att distribuera kod till AEM Cloud-tjänsten.

Med Cloud Manager kan organisationer själva hantera AEM i molnet. Det innehåller en kontinuerlig integrering och ett kontinuerligt leveransramverk (CI/CD) som gör att IT-team och implementeringspartners kan snabba upp leveransen av anpassningar eller uppdateringar utan att kompromissa med prestanda eller säkerhet.

Mer information finns i följande resurser nedan:

* [Integrering med Experience Manager som en molntjänst](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/home.html) för att förstå självhjälpsresurser om introduktion av Experience Manager som en molntjänst.

* [Integrera Git med Adobe Cloud Manager](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) för att lära dig mer om hur du använder en enda Git-databas för att distribuera kod.

* [Adobe Experience som en molntjänstkonfiguration](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/security/ims-support.html#aem-configuration) för att lära dig mer om hur du hanterar produkter och användaråtkomst i Admin Console.


## Introduktion {#introduction}

De exakta stegen i övergången till molntjänsten beror på vilka system du har köpt och vilka metoder du följer för programvaruutveckling.

I följande bild visas de huvudsakliga stegen som ingår i körningsfasen:

![image](/help/move-to-cloud-service/assets/exec-image1.png)

## Innehållsöverföring {#content-transfer}

Om du vill överföra innehåll från din aktuella AEM-instans till din molntjänst kan du använda Adobes verktyg för innehållsöverföring.

Med det här verktyget kan du ange önskad delmängd av innehållet som du vill överföra från din AEM-källinstans till din AEM Cloud Service-instans.

>[!NOTE]
>Vi rekommenderar att du gör regelbundna tillägg av differentiellt innehåll för att förkorta innehållets frysningsperiod för den slutliga differentiella innehållsöverföringen innan du börjar använda molntjänsten.

Mer information finns i [verktyget](/help/move-to-cloud-service/content-transfer-tool/overview-content-transfer-tool.md) Innehållsöverföring.

>[!IMPORTANT]
>Lägsta systemkrav för verktyget Innehållsöverföring är AEM 6.3 + och JAVA 8. Om du har en lägre AEM-version måste du uppgradera din innehållsdatabas till AEM 6.5 för att kunna använda verktyget för innehållsöverföring.

## Kodomfaktorisering {#code-refactor}

Att utveckla och köra kod i AEM som en molntjänst kräver en förändring. Observera att koden måste vara flexibel, särskilt eftersom en instans kan stoppas när som helst. Kod som körs i molntjänsten måste vara medveten om att den alltid körs i ett kluster. Det innebär att fler än en instans alltid körs.

Vissa ändringar krävs i AEM Maven-projekt för att de ska vara kompatibla med AEM som molntjänst. AEM som en molntjänst kräver att *innehåll* och *kod* delas upp i separata paket för distribution till AEM.

* `/apps` och `/libs` betraktas som oföränderliga områden i AEM, eftersom de inte kan ändras (skapa, uppdatera, ta bort) efter att AEM startats (dvs. vid körning). Alla försök att ändra ett oföränderligt område vid körning misslyckas.

* Allt annat i databasen, `/content` , `/conf` , `/var` , `/home` , `/etc` , `/oak:index` , `/system` , `/tmp` osv. är alla ändringsbara områden, vilket innebär att de kan ändras under körning.

Mer information finns i [Rekommenderad paketstruktur](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#recommended-package-structure) .

Det finns ytterligare riktlinjer för utveckling som du behöver vara medveten om när du utvecklar på AEM som en molntjänst. Läs mer i [AEM som riktlinjer](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html) för molntjänstutveckling.

Från din planeringsfas bör du ha en lista över områden som behöver omarbetas för att vara kompatibla med molntjänsten. Du bör även läsa [Utvecklingsriktlinjer](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html) för mer information om hur du omfaktoriserar och optimerar koden för att gå över till molntjänsten.

Du kan använda följande verktyg för att snabba upp vissa av dina åtgärder inom kodomfaktorisering:

* [Migrering av arbetsflöde för tillgångar](/help/move-to-cloud-service/moving-to-aem-assets/asset-workflow-migration-tool.md)
* [Dispatcher Converter](/help/move-to-cloud-service/refactoring-tools/dispatcher-transformation-utility-tools.md)
* [Moderniseringsverktyg](/help/move-to-cloud-service/refactoring-tools/aem-modernization-tools.md)

Vi rekommenderar att du omfaktoriserar och testar koden lokalt innan du skickar den till en molntjänstmiljö via Cloud Manager Git.

Läs [dokumentationen för AEM SDK](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#aem-as-a-cloud-service-sdk) om du vill veta mer.

Nedan finns ytterligare resurser:

* Titta på Install Dispatcher SDK om du vill veta hur du installerar Dispatcher SDK:

   > [!VIDEO](https://video.tv.adobe.com/v/30601)

* Titta på Konfigurera Dispatcher SDK om du vill veta mer om hur du konfigurerar Dispatcher SDK:

   > [!VIDEO](https://video.tv.adobe.com/v/30602)

* Granska dokumentationen för [lokal](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html) utvecklingskonfiguration för att konfigurera en lokal utvecklingsmiljö


Om du vill hantera den pågående kodutvecklingen på din aktiva AEM-fil tillsammans med kodomfaktoriseringsuppgifterna som en del av din övergångsresa bör du schemalägga en frysperiod tills du har slutfört omstruktureringen av ditt Maven-projekt så att det blir kompatibelt med AEM som en molntjänst.

När projektomstruktureringen är klar kan du återuppta utvecklingen av ny kod baserat på den nya strukturen. Detta minskar antalet fel i pipeline för Cloud Manager under koddistribution och testning.

>[!NOTE]
>Aktiviteterna Innehållsöverföring och Kodreaktorn behöver inte utföras sekventiellt. Dessa åtgärder kan utföras oberoende av varandra. Korrekt projektstruktur krävs dock för att se till att innehållet återges korrekt i molntjänstmiljön.

## Bästa metoder för koddriftsättning och testning {#best-practices}

Körningar av pipeline för Cloud Manager för molntjänster stöder körning av tester som körs mot scenmiljön.

Läs [Kodkvalitetstestning](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#code-quality-testing) om du vill veta mer om hur du skriver testskript och om rekommenderad täckning på minst 50 %.

Läs även [Förstå regler](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/custom-code-quality-rules.html) för anpassad kodkvalitet om du vill veta mer om regler för anpassad kodkvalitet som körs av Cloud Manager och som skapats utifrån bästa praxis från AEM Engineering.

Användning av Cloud Manager är den enda mekanismen för att distribuera kod till molntjänstmiljöer.

Följ resurserna nedan för att lära dig hur du använder Cloud Manager för att hantera och distribuera din kod.

* [Hantera miljöer](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html)

* [Konfigurera CI-CD-pipeline](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html)

* [Distribuera kod](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html)

## Best Practices for Go-Live Preparation {#go-live}

För att säkerställa en smidig och framgångsrik publicering på AEM som molntjänst bör du överväga att utföra följande steg:

* Schemalägg kod och frysperiod för innehåll
* Utför den slutliga innehållsuppdateringen
* Slutför testiterationer
* Kör prestanda- och säkerhetstester
* Klipp ut
