---
title: New Relic One
description: Läs mer om tjänsten New Relic One Application Performance Monitoring (APM) för AEM as a Cloud Service och hur du kan komma åt den.
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
source-git-commit: 6cf164093cc543fe4847859b248e70efd86efbb1
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 0%

---


# New Relic One {#user-access}

Läs mer om tjänsten New Relic One Application Performance Monitoring (APM) för AEM as a Cloud Service och hur du kan komma åt den.

## Introduktion {#introduction}

Adobe lägger stor vikt vid övervakning, tillgänglighet och prestanda för programmet. För att uppnå detta mål tillhandahåller AEM as a Cloud Service tillgång till en anpassad övervakningssvit för New Relic One som en del av standardprodukterbjudandet för att säkerställa att era team har största möjliga insyn i de as a Cloud Service AEM för system- och miljöprestanda.

Det här dokumentet beskriver de nya APM-funktioner (New Relic One application performance surveillance) som är aktiverade i dina AEM as a Cloud Service miljöer för att ge bättre prestanda och få ut så mycket som möjligt av AEM as a Cloud Service.

## Funktioner {#transaction-monitoring}

New Relic One APM för AEM as a Cloud Service har många funktioner.

* Direktåtkomst till ett dedikerat nytt Relic One-konto (åtkomst hanteras av Adobe Support)

* Instrumented New Relic One APM-agent som visar exakta metodanrop med radnummer, inklusive externa beroenden och databaser

* Holistisk prestandaoptimering genom att kombinera nyckelvärden från övervakning på infrastrukturnivå och programövervakning (Adobe Experience Manager)

* Exponering av AEM as a Cloud Service JMX-bönor och hälsokontroller direkt inom nya Relic InsiInsights-mätvärden, vilket gör det möjligt att göra djupgående kontroller av programstackens prestanda och hälsomått.

## Använder New Relic One {#accessing-new-relic}

Följ de här stegen för att få tillgång till ditt New Relic One-underkonto som är kopplat till ditt AEM as a Cloud Service program.

1. Öppna en begäran via fliken Support i Admin Console.
1. Ange i din begäran information om ditt program-ID samt en lista över användare som behöver åtkomst till New Relic.
   * Alla användares fullständiga namn och giltiga e-postadresser måste anges.

Se dokumentet [AEM supportportal för Experience Cloud](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) om du vill ha mer information om att öppna biljetter.

När åtkomsten är tillhandahållen skickar New Relic ett bekräftelsemeddelande via e-post till varje användare, så att användaren kan slutföra installationsprocessen och logga in.

Följ de här stegen om användaren inte kan hitta det ursprungliga e-postmeddelandet med kontobekräftelsen.

1. Gå till inloggningssidan för New Relic på [`login.newrelic.com/login`](https://login.newrelic.com/login).

1. Välj **Har du glömt lösenordet?**.

   ![Ny Relic-inloggning](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Skriv e-postadressen till kontot och välj **Skicka min återställningslänk**.

   ![Ange e-postadress](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic skickar ett e-postmeddelande till användaren med en länk som bekräftar kontot.

Om du har slutfört registreringsprocessen och inte kan logga in på ditt konto på grund av felmeddelanden via e-post eller lösenord loggar du en supportanmälan via [Admin Console](https://adminconsole.adobe.com/).

>[!TIP]
>
>Om du inte får något e-postmeddelande från New Relic:
>
>* Kontrollera [skräppostfilter](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/).
>* Om tillämpligt, [lägg till New Relic i e-postmeddelandet tillåtelselista](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist).
>* Om ingen av dem föreslår hjälp, ge gärna feedback på supportanmälan så kommer Adobe Support att hjälpa dig vidare.


### Verifiera din e-postadress {#verify-email}

Om du uppmanas att verifiera din e-post under inloggningen innebär det att din e-post är kopplad till flera konton. På så sätt kan du välja vilket konto du vill få åtkomst till.

Om du inte verifierar din e-postadress försöker New Relic logga in dig med den senast skapade användarposten som är kopplad till din e-postadress. Klicka på knappen **Kom ihåg mig** i inloggningsfönstret.

Om du behöver mer hjälp kan du öppna ett supportärende via [AEM supportportal](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## Undantag {#exceptions}

AEM as a Cloud Service har bara New Relic One APM-lösning och har inte stöd för varningar, loggning eller API-integreringar.

Om du vill ha mer hjälp eller mer information om nya Relic One-erbjudanden för ditt AEM as a Cloud Service program kan du öppna ett supportärende via [AEM supportportal](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## Frågor och svar för nytt Relic-konto {#faqs}

### Vad övervakar Adobe med New Relic One? {#adobe-monitor}

Adobe övervakar den AEM as a Cloud Service författaren, publicerar och förhandsgranskar (där det är tillgängligt) via Java-pluginen New Relic One. Adobe möjliggör anpassad New Relic One APM-telemetri och övervakning i icke-produktions- och produktionsmiljöer AEM as a Cloud Service miljöer.

Ditt nya Relic One-konto är kopplat till ett primärt konto som underhålls av Adobe och har flera program som rapporterar till det: tre per AEM as a Cloud Service Environment.

* Ett program för författartjänsten per miljö
* Ett program för publiceringstjänsten per miljö (inklusive Golden Publish)
* Ett program för förhandsgranskningstjänsten per miljö

Observera:

* Varje program använder en licensnyckel.
* AEM as a Cloud Service miljöer rapporterar till endast ett New Relic One-konto.
* Fullständiga övervakningsvärden och -händelser för både New Relic One bevaras i 7 dagar.

### Vem har åtkomst till molntjänsten New Relic One? {#access-new-relic-cloud}

Fullständig läsbehörighet ges för upp till 10 medlemmar i ditt team. Läsåtkomst inkluderar alla APM-mått som samlats in av New Relic One-agenten.

### Stöds anpassad SSO-konfiguration? {#custom-sso}

Anpassad SSO-konfiguration stöds inte för det nya Relic One-konto som tillhandahålls av Adobe.

### Vad händer om jag redan har en lokal New Relic-prenumeration? {#new-relic-subscription}

New Relic One är den nya observerbarhetsplattformen från New Relic och gör det möjligt för Adobe support och era team att observera, övervaka och se mätvärden och händelser på ett och samma ställe.

Med New Relic One kan användarna söka i alla konton där de har åtkomst till och visualisera data från alla tjänster och värdar i en och samma vy.

Medan supporten i Adobe övervakar den AEM as a Cloud Service applikationen med nya Relic One och andra interna verktyg som en del av din tjänst kan era team fortsätta att utnyttja New Relic för lokala värdtjänster och infrastrukturer. De kommer att kunna visualisera data från både Adobe New Relic One-kontot och kundhanterade New Relic-konton.

>[!NOTE]
>
>Om du vill visa båda datauppsättningarna i New Relic One måste användaren ha rätt behörigheter och använda samma inloggningsmetod för båda kontona (Adobe New Relic One och kundhanterade New Relic-konton).
