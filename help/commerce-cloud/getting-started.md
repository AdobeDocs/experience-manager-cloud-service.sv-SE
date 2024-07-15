---
title: Komma igång med AEM Commerce as a Cloud Service
description: Lär dig hur du distribuerar ett e-handelsprojekt från Adobe Experience Manager (AEM) med Adobe Cloud Manager, en CI/CD-pipeline och Venias referensbutik.
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: Cloud Service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 0%

---

# Komma igång med AEM Commerce as a Cloud Service {#start}

För att komma igång med Adobe Experience Manager (AEM) Commerce as a Cloud Service måste Experience Manager Cloud Servicen etableras med tillägget Commerce integration framework (CIF). Tillägget CIF är en extra modul ovanpå [AEM Sites as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/home.html).

## Onboarding {#onboarding}

Introduktionen AEM Commerce as a Cloud Service är en tvåstegsprocess:

1. Aktivera AEM Commerce as a Cloud Service och CIF tillägg
2. Koppla AEM Commerce as a Cloud Service till er e-handelslösning

Det första startsteget görs av Adobe. Mer information om priser och provisionering får du av din säljare.

När du har etablerat tillägget CIF tillämpas det på alla befintliga Cloud Manager-program. Om du inte har något Cloud Manager-program måste du skapa ett. Mer information finns i [Konfigurera ditt program](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/getting-started/program-setup.html).

Det andra steget är självbetjäning för varje AEM as a Cloud Service-miljö. Det finns ytterligare konfigurationer som du måste göra efter den första etableringen av CIF.

## Ansluta AEM till en Commerce-lösning {#solution}

Om du vill ansluta CIF tillägg och [AEM CIF kärnkomponenter](https://github.com/adobe/aem-core-cif-components) med en e-handelslösning måste du ange GraphQL slutpunkts-URL:en via en Cloud Manager-miljövariabel. Variabelnamnet är `COMMERCE_ENDPOINT`. En säker anslutning via HTTPS måste konfigureras.

Miljövariabeln används på två ställen:

- GraphQL anropar från AEM till e-handelskunderna via en gemensam Sharable GraphQl-klient som används av de AEM CIF Core Components och kundprojektskomponenterna.
- Konfigurera en GraphQL proxy-URL för varje AEM som variabeln är inställd på `/api/graphql`. Den här URL:en används av AEM utvecklingsverktyg (CIF) och CIF komponenter på klientsidan.

En annan GraphQL-slutpunkts-URL kan användas för varje AEM as a Cloud Service-miljö. På så sätt kan projekt koppla AEM staging-miljöer till e-handelssystem och AEM produktionsmiljö till ett handelsproduktionssystem. GraphQL-slutpunkten måste vara allmänt tillgänglig, privata VPN-anslutningar eller lokala anslutningar stöds inte. Om du vill kan du ange ett autentiseringshuvud om du vill använda ytterligare CIF funktioner som kräver autentisering.

Tillägget CIF, och endast för Adobe Commerce Enterprise/Cloud, har stöd för användning av mellanlagrade katalogdata för AEM. Dessa data kräver att du konfigurerar en auktoriseringshuvud. Den här rubriken är bara tillgänglig och används AEM författarinstanser av säkerhetsskäl. AEM Publish-instanser kan inte visa mellanlagrade data.

Det finns två alternativ för att konfigurera slutpunkten:

### Via Cloud Manager användargränssnitt (standard) {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

Den här konfigurationen kan göras med hjälp av en dialogruta på sidan Miljöinformation. När den här sidan visas för ett program som har Commerce aktiverat visas en knapp om slutpunkten inte är konfigurerad:

![CM-miljöinformation](/help/commerce-cloud/assets/commerce-cmui.png)

Om du klickar på den här knappen öppnas en dialogruta:

![CM Commerce Endpoint](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

När slutpunkten och eventuellt en auktoriseringshuvud för stöd för mellanlagrad katalog har angetts visas slutpunkten på detaljsidan. Klicka på ikonen Redigera för att öppna samma dialogruta där du kan redigera slutpunkten, om det behövs.

![CM-miljöinformation](/help/commerce-cloud/assets/commerce-cmui-done.png)

### Genom Adobe I/O CLI  {#adobe-cli}

Följ de här stegen för att ansluta AEM till en e-handelslösning via Adobe I/O CLI:

1. Skaffa Adobe I/O CLI med Cloud Manager plugin

   Läs [Adobe Cloud Manager-dokumentationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html) om hur du hämtar, konfigurerar och använder [Adobe I/O CLI](https://github.com/adobe/aio-cli) med [Cloud Manager CLI-plugin](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Autentisera Adobe I/O CLI med AEM as a Cloud Service-programmet

3. Ange variabeln `COMMERCE_ENDPOINT` i Cloud Manager

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Mer information finns i [CLI-dokument](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid).

   GraphQL slutpunkts-URL för handel måste peka på e-handelns GraphQl-tjänst och använda en säker HTTPS-anslutning. Till exempel: `https://<yourcommercesystem>/graphql`.

4. Aktivera mellanlagrade katalogfunktioner som kräver autentisering (valfritt)

   >[!NOTE]
   >
   >Den här funktionen är endast tillgänglig med Adobe Commerce Enterprise eller Cloud Edition. Mer information finns i [Tokenbaserad autentisering](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens).

   Ange den hemliga variabeln `COMMERCE_AUTH_HEADER` i Cloud Manager:

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>Du kan visa alla Cloud Manager-variabler med följande kommando för att dubbelkontrollera: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

Du är redo att använda AEM Commerce as a Cloud Service och kan driftsätta ditt projekt via Cloud Manager.

## Konfigurera butiker och kataloger {#catalog}

Tillägget CIF och [CIF Core Components](https://github.com/adobe/aem-core-cif-components) kan användas på flera AEM webbplatsstrukturer som är anslutna till olika e-handelsbutiker (eller butiksvyer osv.). Som standard distribueras CIF-tillägget med en standardkonfiguration som ansluter till Adobe Commerce standardbutik och -katalog.

Den här konfigurationen kan justeras för projektet med hjälp av CIF Cloud Service-konfigurationen enligt följande steg:

1. Gå AEM till Verktyg > Cloud Service > CIF Konfiguration.

2. Välj den e-postkonfiguration som du vill ändra.

3. Öppna konfigurationsegenskaperna via åtgärdsfältet.

![Konfiguration CIF Cloud Service](/help/commerce-cloud/assets/cif-cloud-service-config.png)

Följande egenskaper kan konfigureras:

- GraphQL Client - Välj den konfigurerade GraphQL-klienten för e-handelskommunikation. Den här klienten ska normalt vara kvar som standard.
- Butiksvy - butiksvyns identifierare. Om den är tom används standardbutiksvyn.
- GraphQL Proxy Path - den URL-sökväg som GraphQL Proxy AEM använder för proxybegäranden till GraphQL-slutpunkt för e-handel.
  >[!NOTE]
  >
  > I de flesta inställningar får standardvärdet `/api/graphql` inte ändras. Endast avancerade inställningar som inte använder den angivna GraphQL-proxyn bör ändra den här inställningen.
- Aktivera stöd för katalog-UID - aktivera stöd för UID i stället för ID i e-handelsserverdelens GraphQL-anrop.
  >[!NOTE]
  >
  > Stöd för UID introducerades i Adobe Commerce 2.4.2. Aktivera bara UID:n om e-handelsbackend har stöd för ett GraphQL-schema av version 2.4.2 eller senare.
- Katalogrotkategoriidentifierare - identifieraren (UID eller ID) för arkivkatalogroten
  >[!CAUTION]
  >
  > Från och med CIF Core Components version 2.0.0 har stödet för `id` tagits bort och ersatts med `uid`. Om ditt projekt använder CIF Core Components version 2.0.0 måste du aktivera stöd för katalog-UID och använda ett giltigt kategori-UID som&quot;Katalogens rotkategoriidentifierare&quot;.

Konfigurationen som visas ovan är för referens. Projekten ska ha egna konfigurationer.

Mer komplexa inställningar finns i självstudiekursen [Commerce Multi-Store Setup](configuring/multi-store-setup.md) om du använder flera AEM webbplatsstrukturer i kombination med olika e-handelskataloger.

## Ytterligare resurser {#additional-resources}

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venias referensarkiv](https://github.com/adobe/aem-cif-guides-venia)
- [Installation av Commerce Multi-Store](configuring/multi-store-setup.md)
- [Flera Commerce-systeminställningar](configuring/multiple-commerce-systems-setup.md)

