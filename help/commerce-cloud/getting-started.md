---
title: Komma igång med AEM Commerce as a Cloud Service
description: Learn how to deploy a commerce-enabled AEM project to a running AEM as a Cloud service environment. Använd funktionerna i Adobe Cloud Manager och en CI/CD-pipeline för att bygga Venia-referensbutiken till en körbar miljö.
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: cloud-service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
source-git-commit: d85352b93b9c793a716841523677eb710bb4577c
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 0%

---

# Komma igång med AEM Commerce as a Cloud Service {#start}

To get started with AEM Commerce as a Cloud Service, your Experience Manager Cloud Service needs to be provisioned with the Commerce Integration Framework (CIF) add-on. CIF-tillägget är ytterligare en modul ovanpå [AEM Sites as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/home.html).

## Onboarding {#onboarding}

Introduktionen av AEM Commerce as a Cloud Service är en tvåstegsprocess:

1. Aktivera AEM Commerce as a Cloud Service och CIF-tillägget har etablerats
2. Connect AEM Commerce as a Cloud Service with your commerce solution

The first onboarding step is done by Adobe. Mer information om priser och provisionering får du av din säljare.

Once you have been provisioned with the CIF add-on, it will be applied to any existing Cloud Manager programs. Om du inte har något Cloud Manager-program måste du skapa ett nytt. For more details, refer to [Setup your Program](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

The second step is self-service for each AEM as a Cloud Service environment. Det finns ytterligare konfigurationer du behöver göra efter den första etableringen av CIF-tillägget.

## Connecting AEM with a Commerce Solution {#solution}

Ansluta CIF-tillägget och [AEM CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components) med en e-handelslösning måste du ange URL:en för GraphQL-slutpunkten via en Cloud Manager-miljövariabel. The variable name is `COMMERCE_ENDPOINT`. En säker anslutning via HTTPS måste konfigureras.

Miljövariabeln används på två ställen:

- GraphQL calls from AEM to commerce backend, via some common shareable GraphQl client, used by the AEM CIF Core Components and customer project components.
- Setup a GraphQL proxy URL on each AEM environment the variable is set available at `/api/graphql`. Detta används av AEM utvecklingsverktyg (CIF-tillägg) och CIF-komponenter på klientsidan.

A different  GraphQL endpoint URL can be used for each AEM as a Cloud Service environment. That way projects can connect AEM staging environments with commerce staging systems and AEM production environment to a commerce production system. GraphQL-slutpunkten måste vara offentligt tillgänglig, privata VPN-anslutningar eller lokala anslutningar stöds inte. Ett autentiseringshuvud kan anges om du vill använda ytterligare CIF-funktioner som kräver autentisering.

Tillägget CIF kan användas endast för Adobe Commerce Enterprise/Cloud med stöd för användning av testade katalogdata för AEM. Detta kräver att du konfigurerar en auktoriseringshuvud. This header is only available and used on AEM author instances for security reasons. AEM publiceringsinstanser kan inte visa mellanlagrade data.

Det finns två alternativ för att konfigurera slutpunkten:

### Via användargränssnittet i Cloud Manager (standard) {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

Detta kan du göra med en dialogruta på sidan Miljöinformation. När den här sidan visas för ett program som har stöd för Commerce visas en knapp om slutpunkten inte är konfigurerad:

![CM-miljöinformation](/help/commerce-cloud/assets/commerce-cmui.png)

Om du klickar på den här knappen öppnas en dialogruta:

![CM Commerce Endpoint](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

När slutpunkten och eventuellt en auktoriseringshuvud för stöd för mellanlagrad katalog har angetts, visas slutpunkten på detaljsidan. Om du klickar på ikonen Redigera öppnas samma dialogruta där slutpunkten kan ändras om det behövs.

![CM Enviornment Information](/help/commerce-cloud/assets/commerce-cmui-done.png)

### Via Adobe I/O CLI  {#adobe-cli}

Följ de här stegen för att ansluta AEM till en e-handelslösning via Adobe I/O CLI:

1. Skaffa Adobe I/O CLI med plugin-programmet Cloud Manager

   Kontrollera [Dokumentation för Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) om hur du hämtar, konfigurerar och använder [Adobe I/O CLI](https://github.com/adobe/aio-cli) med [CLI-plugin för Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Autentisera Adobe I/O CLI med det AEM as a Cloud Service programmet

3. Set the `COMMERCE_ENDPOINT` variable in Cloud Manager

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Se [CLI-dokument](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) för mer information.

   Slutpunktens URL för Commerce GraphQL måste peka på e-handelns GraphQl-tjänst och använda en säker HTTPS-anslutning. Till exempel: `https://<yourcommercesystem>/graphql`.

4. Enable Staged catalog features that require authentication (Optional)

   >[!NOTE]
   >
   >This feature is only available with Adobe Commerce Enterprise or Cloud Edition. See [Token-based authentication](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens) for details.

   Ange `COMMERCE_AUTH_HEADER` hemlig variabel i Cloud Manager:

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>Du kan visa alla Cloud Manager-variabler med följande kommando för att dubbelkontrollera: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

With this, you are ready to use AEM Commerce as a Cloud Service and can deploy your project via Cloud Manager.

## Konfigurera butiker och kataloger {#catalog}

CIF-tillägget och [CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components) kan användas på flera AEM webbplatsstrukturer som är anslutna till olika e-handelsbutiker (eller butiksvyer osv.). Som standard distribueras CIF-tillägget med en standardkonfiguration som ansluter till Adobe Commerce standardbutik och -katalog.

Den här konfigurationen kan justeras för projektet via CIF-Cloud Servicens konfiguration enligt följande steg:

1. In AEM go to Tools -> Cloud Services -> CIF Configuration

2. Select the commerce configuration you want to change

3. Öppna konfigurationsegenskaperna via åtgärdsfältet

![CIF Cloud Services Configuration](/help/commerce-cloud/assets/cif-cloud-service-config.png)

The following properties can be configured:

- GraphQL Client - select the configured GraphQL client for commerce backend communication. Detta bör normalt vara kvar som standard.
- Butiksvy - butiksvyns identifierare. Om den är tom används standardbutiksvyn.
- Proxysökväg för GraphQL - URL-sökvägen för GraphQL-proxy som används AEM proxybegäranden till GraphQL-slutpunkten för handel.
   >[!NOTE]
   >
   > In most setups the default value `/api/graphql` must not be changed. Endast avancerade inställningar som inte använder den angivna GraphQL-proxyn bör ändra den här inställningen.
- Enable Catalog UID Support - enable support for UID instead of ID in the commerce backend GraphQL calls.
   >[!NOTE]
   >
   > Stöd för UID introducerades i Adobe Commerce 2.4.2. Aktivera bara detta om e-handelsbackend har stöd för ett GraphQL-schema av version 2.4.2 eller senare.
- Katalogrotkategoriidentifierare - identifieraren (UID eller ID) för arkivkatalogroten
   >[!CAUTION]
   >
   > Från och med CIF Core Components version 2.0.0 finns stöd för `id` togs bort och ersattes med `uid`. If your project uses CIF Core Components version 2.0.0 you must enable Catalog UID Support and use a valid category UID as &quot;Catalog Root Category Identifier&quot;.

Konfigurationen som visas ovan är för referens. Projekten ska innehålla egna konfigurationer.

For more complex setups using multiple AEM site structures combined with different commerce catalogs see the [Commerce Multi-Store Setup](configuring/multi-store-setup.md) tutorial.

## Ytterligare resurser {#additional-resources}

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Commerce Multi-Store Setup](configuring/multi-store-setup.md)
