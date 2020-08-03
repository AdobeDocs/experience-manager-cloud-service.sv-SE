---
title: Komma igång med AEM Commerce som Cloud Service
description: Komma igång med AEM Commerce som Cloud Service
translation-type: tm+mt
source-git-commit: 170a6f4f3aa07b9aa917014b7a682ead9ed595c1
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 3%

---


# Komma igång med AEM Commerce som Cloud Service {#start}

För att komma igång med AEM Commerce som Cloud Service måste Experience Manager Cloud Servicen etableras med tillägget Commerce Integration Framework (CIF). Tillägget CIF är ytterligare en modul ovanpå [AEM Sites som en Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/home.html).

## Introduktion till {#onboarding}

Introduktionen av AEM Commerce som Cloud Service är en tvåstegsprocess:

1. Få AEM Commerce som en Cloud Service aktiverad och CIF-tillägget etablerat
2. Anslut AEM Commerce som en Cloud Service till Magento

Det första steget görs av Adobe. Du måste ange information som IMS-organisationen, GraphQL-slutpunktens URL i Magento-miljön osv. som en del av provisioneringsprocessen. Mer information om priser och provisionering får du av din säljare.

När du har etablerats med CIF-tillägget kommer det att tillämpas på alla befintliga Cloud Manager-program. Om du inte har något Cloud Manager-program måste du skapa ett nytt. Mer information finns i [Konfigurera ditt program](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

Det andra steget är självbetjäning för varje AEM som en Cloud Service-miljö. Det finns ytterligare konfigurationer du behöver göra efter den första etableringen av CIF-tillägget.

## Koppla AEM handel med Magento {#magento}

Om du vill ansluta CIF-tillägget och [AEM CIF Core-komponenter](https://github.com/adobe/aem-core-cif-components) till Magento-miljön måste du ange Magento GraphQL-slutpunkts-URL:en via en Cloud Manager-miljövariabel. Variabelnamnet är `COMMERCE_ENDPOINT`. En säker anslutning via HTTPS måste konfigureras.
En Magento-URL för GraphQL-slutpunkt kan användas som en Cloud Service för varje AEM. På så sätt kan projekt koppla AEM mellanlagringsmiljöer med Magento och AEM produktionsmiljö till ett produktionssystem i Magento. Magento GraphQL-slutpunkten måste vara allmänt tillgänglig, privata VPN-anslutningar eller lokala anslutningar stöds inte.

Så här ansluter du AEM Commerce till Magento:

1. Skaffa Adobe I/O CLI med pluginprogrammet Cloud Manager

   Läs dokumentationen [för](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) Adobe Cloud Manager om hur du hämtar, konfigurerar och använder [Adobe I/O CLI](https://github.com/adobe/aio-cli) med [Cloud Managers CLI-plugin](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Autentisera CLI med AEM som ett Cloud Service-program

3. Ange `COMMERCE_ENDPOINT` variabeln i Cloud Manager

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Mer information finns i [CLI-dokument](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) .

   Magento-URL:en för GraphQL-slutpunkten måste peka på Magento GraphQl-tjänsten och använda en säker HTTPS-anslutning. Till exempel: `https://demo.magentosite.cloud/graphql`.

>[!TIP]
>
>Du kan visa alla Cloud Manager-variabler med följande kommando för att dubbelkontrollera: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

>[!Note]
>
>Du kan även använda API:t [för](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html) Cloud Manager för att konfigurera Cloud Manager-variabler.

Detta gör att du kan använda AEM Commerce som Cloud Service och driftsätta ditt projekt via Cloud Manager.

## E-handelsintegreringar från tredje part {#integrations}

För e-handelsintegreringar från tredje part krävs ett [API-mappningslager](architecture/third-party.md) för att ansluta AEM Commerce som en Cloud Service och CIF Core Components till ert e-handelssystem. API-mappningslagret distribueras vanligtvis på Adobe I/O Runtime. Kontakta din säljare för att få information om tillgängliga integreringar och tillgång till Adobe I/O Runtime.
