---
title: Användaråtkomst till New Relic
description: Följ den här sidan om du vill veta mer om prestandaövervakning för nya Relic-program för AEM as a Cloud Service
source-git-commit: bb9532685c10baf13bc31898c0038fde2c5fd43d
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 0%

---


# Användaråtkomst till New Relic {#user-access}

## Introduktion {#introduction}

Adobe lägger stor vikt vid övervakning, tillgänglighet och prestanda för programmet. För att uppnå detta mål tillhandahåller AEM as a Cloud Service tillgång till en anpassad ny Relic-övervakningssvit som en del av standardprodukterbjudandet för att säkerställa att era team får största möjliga insyn i Adobe Experience Manager Cloud Service-systemet och miljöprestandamätningar. I det här avsnittet beskrivs de nya Relic-övervakningsfunktionerna som är aktiverade i dina AEM as a Cloud Service miljöer för att öka prestandan och få ut så mycket som möjligt av AEM as a Cloud Service.

## AEM as a Cloud Service transaktionsövervakning via New Relic - Value Proposition {#transaction-monitoring}

Här är en sammanfattning av värdeförslag från New Relic Application Performance Monitoring för AEM as a Cloud Service:

* Direktåtkomst till ett dedikerat nytt Relic One-konto (åtkomst hanteras av Adobe Support).

* Instrumented New Relic APM-agent som visar exakta metodanrop med radnummer, inklusive externa beroenden och databaser.

* Holistisk prestandaoptimering genom att kombinera viktiga mätvärden från övervakning på infrastrukturnivå och programövervakning (Adobe Experience Manager).

* Exponering av AEM as a Cloud Service JMX-bönor och hälsokontroller direkt in i nya Relic InsiInsights-mätvärden, vilket möjliggör en djupgående undersökning av programmets prestanda och hälsomått.

## Få åtkomst till ditt AEM as a Cloud Service New Relic-konto {#accessing-new-relic}

Ditt dedikerade New Relic-konto kommer att tillhandahållas och hanteras av Adobe via kundtjänst. Adobe förblir ägare och administratör och tillhandahåller kontot å dina vägnar för att ge åtkomst till ditt dedikerade underkonto.

För att få tillgång till ditt New Relic-underkonto som är kopplat till ditt AEM as a Cloud Service program:

* Öppna en begäran via fliken Support i Admin Console.
* Se till att din biljett innehåller information om ditt program-ID samt en lista över användare som du ber Adobe team att öppna den nya Relic-åtkomsten till.
* Alla användare måste anges med fullständigt namn och giltig e-postadress.

   >[!NOTE]
   >Se [AEM supportportal för Experience Cloud](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) för mer information.

När åtkomsten är tillhandahållen skickar New Relic ett bekräftelsemeddelande via e-post till varje användare, så att användaren kan slutföra installationsprocessen och logga in.

Om användaren inte kan hitta e-postadressen till den ursprungliga kontobekräftelsen:

1. Gå till inloggningssidan för New Relic på [login.newrelic.com/login](https://login.newrelic.com/login).

1. Välj **Har glömt lösenordet**.

   ![](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Skriv e-postadressen till kontot och välj **Skicka min återställningslänk**.

   ![](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. När New Relicks system returnerar ett e-postmeddelande markerar du länken i det för att bekräfta ditt konto igen.

   >[!NOTE]
   >Om du inte får något e-postmeddelande från New Relic:
   >Kontrollera [skräppostfilter](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/). Om tillämpligt, [lägg till New Relic i e-postmeddelandet tillåtelselista](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist).
   >Ge feedback på supportanmälan så hjälper våra team dig vidare

1. Om du har slutfört registreringsprocessen och inte kan logga in på ditt konto på grund av felmeddelanden via e-post eller lösenord loggar du en supportanmälan via [Admin Console](https://adminconsole.adobe.com/).

### Verifiera din e-postadress {#verify-email}

Om du uppmanas att verifiera din e-post under inloggningen innebär det att din e-post är kopplad till flera konton och att du kan verifiera din e-post under inloggningen. På så sätt kan du välja vilket konto du vill få åtkomst till. Om du inte verifierar din e-postadress försöker New Relic logga in dig med den senast skapade användarposten som är kopplad till din e-postadress. Du kan undvika att verifiera din e-postadress vid varje inloggning genom att klicka i kryssrutan Kom ihåg mig på inloggningsskärmen.

Om du behöver mer hjälp kan du öppna ett supportärende via [AEM supportportal](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## Undantag {#exceptions}

AEM as a Cloud Service fokuserar endast erbjudandet kring New Relic APM-lösning och har inte stöd för varningsmeddelanden, loggning eller API-integreringsfunktioner.

Om du vill ha mer hjälp eller mer information om nya Relic-erbjudanden för ditt AEM as a Cloud Service program kan du öppna en supportanmälan via [AEM supportportal](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) om du behöver hjälp.

## Frågor och svar för nytt Relic-konto {#faqs}

### Vad övervakar Adobe med New Relic? {#adobe-monitor}

Adobe övervakar AEM as a Cloud Service tjänster för författare, publicering och förhandsgranskning (där de är tillgängliga) via New Relic APM Java plug-in. Adobe möjliggör anpassad telemetri för ny Relic APM och övervakning över icke-produktion och produktion AEM as a Cloud Service miljöer. Ditt New Relic-konto är kopplat till ett primärt Adobe-konto och har flera program som rapporterar till det.

Tre var AEM as a Cloud Service miljö:

* Ett program för författartjänsten per miljö
* Ett program för publiceringstjänsten per miljö (inklusive Golden Publish)
* Ett program för förhandsgranskningstjänsten per miljö
   >[!IMPORTANT]
   >Alla program använder en licensnyckel, AEM as a Cloud Service miljöer rapporterar till endast ett nytt Relic-konto. Full övervakning av mått och händelser för både New Relic APM bevaras i 7 dagar.

### Vem har åtkomst till New Relic-Cloud Servicens data? {#access-new-relic-cloud}

Fullständig läsbehörighet ges för upp till 10 medlemmar i ditt team. Läsåtkomst inkluderar alla APM-värden som samlats in av New Relic-agenten.

### Stöds anpassad SSO-konfiguration? {#custom-sso}

Anpassad SSO-konfiguration stöds för närvarande inte för det nya Relic-konto som tillhandahålls av Adobe.

### Vad händer om du redan har en lokal New Relic-prenumeration? {#new-relic-subscription}

Den nya observerbarhetsplattformen från New Relic One som heter New Relic One gör det möjligt för Adobe Support Groups och era medarbetare att observera, övervaka och se mätvärden och händelser på ett och samma ställe. Med New Relic One kan användarna söka i alla konton där de har åtkomst till och visualisera data från alla tjänster och värdar i en och samma vy. Medan Adobe Support Teams övervakar den AEM as a Cloud Service applikationen med hjälp av nya Relic och andra interna verktyg som en del av din tjänst kan era team fortsätta att utnyttja New Relic för lokala värdtjänster och infrastruktur. De kommer att kunna visualisera data från både Adobe och kundhanterade New Relic-konton.

>[!NOTE]
>Användaren måste ha rätt behörigheter och använda samma inloggningsmetod för båda kontona (Adobe och kundhanterat New Relic-konto).


