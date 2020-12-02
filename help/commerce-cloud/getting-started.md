---
title: Komma igång med AEM Commerce som Cloud Service
description: Lär dig hur du distribuerar ett e-handelsaktiverat AEM till ett AEM som körs som en molntjänstmiljö. Använd funktionerna i Adobe Cloud Manager och en CI/CD-pipeline för att bygga Venia-referensbutiken till en körbar miljö.
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: cloud-service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
translation-type: tm+mt
source-git-commit: 7a26596b00f276404934e467490ff79d08b0e1d0
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 2%

---


# Komma igång med AEM Commerce som Cloud Service {#start}

För att komma igång med AEM Commerce som Cloud Service måste Experience Manager Cloud Servicen etableras med tillägget Commerce Integration Framework (CIF). CIF-tillägget är en extra modul ovanpå [AEM Sites som en Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/home.html).

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

## Introduktion till {#onboarding}

Introduktionen av AEM Commerce som Cloud Service är en tvåstegsprocess:

1. Få AEM Commerce som en Cloud Service aktiverad och CIF-tillägget etablerat
2. Anslut AEM Commerce som en Cloud Service till Magento

Det första steget görs av Adobe. Du måste ange information som IMS-organisationen, GraphQL-slutpunktens URL i Magento-miljön osv. som en del av provisioneringsprocessen. Mer information om priser och provisionering får du av din säljare.

När du har etablerats med CIF-tillägget kommer det att tillämpas på alla befintliga Cloud Manager-program. Om du inte har något Cloud Manager-program måste du skapa ett nytt. Mer information finns i [Konfigurera ditt program](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

Det andra steget är självbetjäning för varje AEM som en Cloud Service-miljö. Det finns ytterligare konfigurationer du behöver göra efter den första etableringen av CIF-tillägget.

## Ansluta AEM med Magento {#magento}

Om du vill ansluta CIF-tillägget och [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) till Magento-miljön måste du ange Magento GraphQL-slutpunkts-URL:en via en Cloud Manager-miljövariabel. Variabelnamnet är `COMMERCE_ENDPOINT`. En säker anslutning via HTTPS måste konfigureras.
En Magento-URL för GraphQL-slutpunkt kan användas som en Cloud Service för varje AEM. På så sätt kan projekt koppla AEM mellanlagringsmiljöer med Magento och AEM produktionsmiljö till ett produktionssystem i Magento. Magento GraphQL-slutpunkten måste vara allmänt tillgänglig, privata VPN-anslutningar eller lokala anslutningar stöds inte.

Så här ansluter du AEM Commerce till Magento:

1. Skaffa Adobe I/O CLI med plugin-programmet Cloud Manager

   Läs [Adobe Cloud Manager-dokumentationen](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) om hur du hämtar, konfigurerar och använder [Adobe I/O CLI](https://github.com/adobe/aio-cli) med [Cloud Manager CLI plugin](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Autentisera CLI med AEM som ett Cloud Service-program

3. Ange variabeln `COMMERCE_ENDPOINT` i Cloud Manager

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Mer information finns i [CLI-dokument](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid).

   Magento-URL:en för GraphQL-slutpunkten måste peka på Magento GraphQl-tjänsten och använda en säker HTTPS-anslutning. Till exempel: `https://demo.magentosite.cloud/graphql`.

>[!TIP]
>
>Du kan visa alla Cloud Manager-variabler med följande kommando för att dubbelkontrollera: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

>[!NOTE]
>
>Du kan också använda API:t [Cloud Manager](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html) för att konfigurera Cloud Manager-variabler.

Detta gör att du kan använda AEM Commerce som Cloud Service och driftsätta ditt projekt via Cloud Manager.

## Aktivera mellanlagrade katalogfunktioner (valfritt) {#staging}

>[!NOTE]
>
>Den här funktionen är endast tillgänglig med Magento Enterprise Edition eller Magento Cloud.

1. Logga in på Magento och skapa en integreringstoken. Mer information finns i [Tokenbaserad autentisering](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens). Kontrollera att integreringstoken bara har *åtkomst till*-resurser. `Content -> Staging` Kopiera `Access Token`-värdet.

1. Ange den hemliga variabeln `COMMERCE_AUTH_HEADER` i Cloud Manager:

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization Bearer: <Access Token>"
   ```

   Se [Ansluta AEM med Magento](#magento) om hur du konfigurerar Adobe I/O CLI för Cloud Manager.

## E-handelsintegreringar från tredje part {#integrations}

För e-handelsintegreringar från tredje part krävs ett [API-mappningslager](architecture/third-party.md) för att ansluta AEM Commerce som en Cloud Service och CIF Core Components med ditt handelssystem. API-mappningslagret distribueras vanligtvis på Adobe I/O Runtime. Kontakta din säljare för att få information om tillgängliga integreringar och tillgång till Adobe I/O Runtime.
