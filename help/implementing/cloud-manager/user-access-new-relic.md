---
title: New Relic One
description: Läs om New Relic One APM-tjänst (application performance monitoring) för AEM as a Cloud Service och hur du får tillgång till den.
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 2c863e0cfad3211e811665a5169def7705e8b907
workflow-type: tm+mt
source-wordcount: '1814'
ht-degree: 0%

---


# New Relic One {#user-access}

Läs om New Relic One APM-tjänst (application performance monitoring) för AEM as a Cloud Service och hur du får tillgång till den.

## Om New Relic One {#introduction}

Adobe lägger stor vikt vid övervakning, tillgänglighet och prestanda för dina program. AEM as a Cloud Service ger tillgång till New Relic One övervakning, vilket ger team en heltäckande insikt i prestanda för system och miljö som en del av standarderbjudandet.

I det här dokumentet beskrivs hur du hanterar åtkomst till New Relic One APM-funktioner (Application Performance Monitoring) i AEM as a Cloud Service-miljöer. Effektiv hantering av dessa funktioner ger optimala prestanda och maximerar fördelarna med AEM as a Cloud Service.

När ett nytt produktionsprogram skapas skapas automatiskt det New Relic One-underkonto som är kopplat till ditt AEM as a Cloud Service-program. [Det här underkontot måste aktiveras](#activate-sub-account) för att du ska kunna börja inhämta data.

## Funktioner {#transaction-monitoring}

New Relic One APM för AEM as a Cloud Service har många funktioner.

* Direktåtkomst till ett dedikerat New Relic One-konto

* Instrumenterad New Relic One APM-agent som visar exakta metodanrop med radnummer, inklusive externa beroenden och databaser

* Holistisk prestandaoptimering genom att kombinera nyckelvärden från övervakning på infrastrukturnivå och programövervakning (Adobe Experience Manager)

* AEM as a Cloud Service visar Java Management Extensions (JMX) MBeans och hälsokontroller direkt inifrån New Relic Insights, vilket möjliggör en djupgående undersökning av programmets prestanda och hälsomått.

## Aktivera ditt New Relic One-underkonto {#activate-sub-account}

För ett nytt program skapas ett New Relic One-underkonto åt dig. Du måste dock aktivera den för att den ska kunna importera data. Aktiveringen är inte automatisk. Följ de här stegen för att aktivera ditt underkonto.

>[!NOTE]
>
>En användare i rollen **Affärsägare** måste vara inloggad för att hantera New Relic One-underkontot.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** klickar du på det program som du vill hantera dina New Relic One-användare för.

1. Klicka på ikonen **Mer** och välj ![Aktivera New Relic](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) längst ned på **miljökortet** på programöversiktssidan.

   ![Hantera användare](assets/newrelic-activate-sub-account.png)

   * Du kan även komma åt alternativet **Hantera användare**. Klicka på **Utjämna fler ikoner** längst upp på skärmen ![Miljö](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i ditt program.

1. [Kör en pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines) för samma miljö för att slutföra aktiveringen av underkontot.

När underkontot inaktiveras finns det inget databehov.

## Hantera New Relic One-användare {#manage-users}

Följ de här stegen för att definiera användare för ditt New Relic One-underkonto som är kopplat till ditt AEM as a Cloud Service-program.

>[!NOTE]
>
>En användare i rollen **Business Owner** eller **Deployment Manager** måste vara inloggad för att kunna hantera New Relic One-användare.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Klicka på det program som du vill hantera dina New Relic One-användare för.

1. Klicka på ikonen **Mer** och välj ![Hantera användare](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) längst ned på **miljökortet** på programöversiktssidan.

   ![Hantera användare](assets/newrelic-manage-users.png)

   * Du kan även komma åt alternativet **Hantera användare**. Klicka på **Utjämna fler ikoner** längst upp på skärmen ![Miljö](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i ditt program.

1. I dialogrutan **Hantera New Relic-användare** anger du för- och efternamnet för den användare som du vill lägga till och klickar på knappen **Lägg till** . Upprepa det här steget för alla användare som du vill lägga till.

   ![Lägg till användare](assets/newrelic-add-users.png)

1. Om du vill ta bort en New Relic One-användare klickar du på borttagningsknappen i den högra änden av raden som representerar användaren.

1. Klicka på **Spara** för att skapa användarna.

När användarna har definierats skickar New Relic ett bekräftelsemeddelande via e-post till varje användare som du har beviljat åtkomst, så att användaren kan slutföra installationsprocessen och logga in.

>[!NOTE]
>
>Om du hanterar New Relic One-användare måste du också lägga till dig själv som användare för att få tillgång till dig själv. Det räcker inte att vara **Business Owner** eller **Deployment Manager** för att ha tillgång till New Relic One. Du måste också skapa dig själv som användare.

## Aktivera ditt New Relic One-användarkonto {#activate-user-account}

När ett New Relic One-användarkonto har skapats, enligt beskrivningen i förhandsvisningsavsnittet [Hantera New Relic One-användare](#manage-users), skickar New Relic ett bekräftelsemeddelande via e-post till den angivna adressen. För att kunna använda dessa konton måste användarna först aktivera sina konton hos New Relic genom att återställa sina lösenord.

**Så här aktiverar du ditt New Relic One-användarkonto:**

1. Klicka på länken i mejlet från New Relic.

1. Klicka på **Har du glömt ditt lösenord på inloggningssidan för New Relic?**

   ![New Relic-inloggning](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Ange den e-postadress där du fick bekräftelsemeddelandet och välj **Skicka min återställningslänk**.

   ![Ange e-postadress](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic skickar ett e-postmeddelande till dig med en länk för att bekräfta kontot.

Om du inte får något bekräftelsemeddelande från New Relic kan du läsa [felsökningsavsnittet](#troubshooting).

## Använd New Relic One {#accessing-new-relic}

När du har [aktiverat ditt New Relic-konto](#activate-account) kan du komma åt New Relic One via Cloud Manager eller direkt.

**För åtkomst till New Relic One via Cloud Manager:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Klicka på det program som du vill använda New Relic One för.

1. Klicka på ikonen **Mer** längst ned på ![miljökortet](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) på programöversiktssidan och välj **Öppna New Relic**.

   ![Hantera användare](assets/newrelic-access.png)

   * Du har även tillgång till New Relic. Klicka på **Utjämna fler ikoner** längst upp på skärmen ![Miljö](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i ditt program.

1. Logga in på New Relic One på den nya webbläsarfliken som öppnas.

**Så här kommer du åt New Relic One direkt:**

1. Gå till New Relic inloggningssida på [`https://login.newrelic.com/login`](https://login.newrelic.com/login)

1. Logga in på New Relic One.

### Verifiera din e-postadress {#verify-email}

Om du uppmanas att verifiera din e-postadress under inloggningen på New Relic One innebär det att din e-postadress är kopplad till flera konton. Du kan välja vilket konto du vill få åtkomst till.

Om du inte verifierar din e-postadress försöker New Relic logga in dig med den senast skapade användarposten som är kopplad till din e-postadress. Du kan undvika att verifiera din e-post under varje inloggning genom att klicka i kryssrutan **Kom ihåg mig** på inloggningsskärmen.

Om du vill ha mer hjälp kan du öppna ett supportärende via [AEM supportportal](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## Felsöka New Relic One användaråtkomst {#troubleshooting}

Om du har lagts till som en New Relic One-användare, enligt beskrivningen i [Hantera New Relic One-användare](#manage-users), och inte kan hitta det ursprungliga e-postmeddelandet med kontobekräftelsen, kan du utföra följande felsökningssteg.

**Så här felsöker du New Relic One-användaråtkomst:**

1. Gå till New Relic inloggningssida på [`login.newrelic.com/login`](https://login.newrelic.com/login).

1. Klicka på **[!UICONTROL Forgot your password?]**.

   ![New Relic-inloggning](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Ange den e-postadress som användes för att skapa ditt konto och välj **Skicka min återställningslänk**.

   ![Ange e-postadress](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic skickar ett e-postmeddelande till dig med en länk för att bekräfta kontot.

Om du har slutfört registreringsprocessen och inte kan logga in på ditt konto på grund av felmeddelanden i e-post eller lösenord loggar du en supportanmälan via [Admin Console](https://adminconsole.adobe.com/).

Om du inte får något e-postmeddelande från New Relic gör du följande:

* Kontrollera [skräppostfiltren](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/).
* [Lägg till New Relic i e-postmeddelandet tillåtelselista](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist) om det är tillämpligt.
* Om inget av förslagen hjälper, ge feedback på supportanmälan.

## Användningsinformation {#usage-notes}

* Högst 30 användare kan läggas till. Om det maximala antalet användare har uppnåtts tar du bort användare för att kunna lägga till nya användare.
* Användare som läggs till i New Relic är av typen **Basic**. Mer information finns i [New Relic-dokumentationen](https://docs.newrelic.com/docs/accounts/accounts-billing/new-relic-one-user-management/user-type/).
* AEM as a Cloud Service har bara New Relic One APM-lösning och har inte stöd för varningar, loggning eller API-integreringar.

>[!NOTE]
>
>Om ingen **användarinloggningsaktivitet** identifieras i ditt New Relic One-underkonto i 30 dagar eller mer, stoppas APM-agenten. Data skickas inte från AEM Cloud-tjänsten till New Relic. *Data skickas inte igen förrän ditt underkonto har återaktiverats.*
>
>Följ samma steg i avsnittet [Aktivera ditt New Relic One-underkonto](#activate-sub-account) i det här dokumentet om du vill återaktivera ditt New Relic One-underkonto.

Om du vill ha mer hjälp eller mer information om New Relic One-erbjudanden för ditt AEM as a Cloud Service-program kan du öppna ett supportärende via [AEM supportportal](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## Frågor och svar {#faqs}

+++**Vad övervakar Adobe med New Relic One?**

Adobe övervakar AEM as a Cloud Service författare, publicerar och förhandsgranskar (där de är tillgängliga) tjänster via New Relic One Java-plugin. Adobe möjliggör anpassad New Relic One APM-telemetri och övervakning i AEM as a Cloud Service-miljöer som inte är i produktion och produktion.

Ditt New Relic One-konto är kopplat till ett primärt Adobe-underhållet konto och har flera program som rapporterar till det; tre per AEM as a Cloud Service-miljö.

* Ett program för författartjänsten per miljö
* Ett program för tjänsten `Publish` per miljö (inklusive Golden Publish)
* Ett program för förhandsgranskningstjänsten per miljö

Obs!

* Varje program använder en licensnyckel.
* AEM as a Cloud Service-miljöer rapporterar till endast ett New Relic One-konto.
* Full övervakning av mätvärden och händelser för båda New Relic One bevaras i tre månader.

+++

+++**Skickar Adobe varningsmeddelanden från New Relic One?**

Adobe ger åtkomst till New Relic One endast i observationssyfte och använder det inte för kundvarningar eller interna varningar. Meddelanden om eventuella incidenter skickas med [användarmeddelandeprofiler](/help/journey-onboarding/notification-profiles.md).
+++

+++**Vem har åtkomst till New Relic One molntjänstdata?**

Upp till 30 medlemmar i ditt team har full läsbehörighet. Läsåtkomst innefattar alla APM-värden som samlats in av New Relic One Agent.
+++

+++**Stöds anpassad enkel inloggning?**

Anpassad SSO-konfiguration stöds inte för det New Relic One-konto som tillhandahålls av Adobe.
+++

+++**Vad händer om jag redan har en lokal New Relic-prenumeration?**

New Relic One är den nya plattformen för observerbarhet från New Relic och gör det möjligt för Adobe support och era team att observera, övervaka och se mätvärden och händelser, allt på ett och samma ställe.

New Relic One ger användarna möjlighet att söka på alla konton där de har tillgång till och kan visualisera data från alla tjänster och värdar i en och samma vy.

Adobe support övervakar AEM as a Cloud Service med New Relic One och andra verktyg, medan era team fortfarande kan använda New Relic för lokala tjänster och infrastruktur. De kan visualisera data både från Adobe New Relic One-konton och kundhanterade New Relic-konton.

>[!NOTE]
>
>Om du vill visa båda datauppsättningarna inom New Relic One måste användaren ha rätt behörigheter och använda samma inloggningsmetod för båda kontona (Adobe New Relic One och kundhanterade New Relic-konton).

+++

+++**APM-agenten för mitt New Relic One-konto har stoppats. Vad hände?**

[APM-agenter stoppas](#limitations) om ingen aktivitet identifieras på 30 dagar eller mer. Följ samma steg i avsnittet [Aktivera ditt New Relic One-underkonto](#activate-sub-account) i det här dokumentet om du vill återaktivera ditt New Relic One-underkonto.
+++
