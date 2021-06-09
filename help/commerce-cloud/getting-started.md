---
title: Komma igång med AEM Commerce som Cloud Service
description: Lär dig hur du distribuerar ett e-handelsaktiverat AEM till ett AEM som körs som en molntjänstmiljö. Använd funktionerna i Adobe Cloud Manager och en CI/CD-pipeline för att bygga Venia-referensbutiken till en körbar miljö.
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: cloud-service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
source-git-commit: de756a469f2be7b4f93d647b500cd4e8dc046342
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 0%

---

# Komma igång med AEM Commerce som Cloud Service {#start}

För att komma igång med AEM Commerce som Cloud Service måste Experience Manager Cloud Servicen etableras med tillägget Commerce Integration Framework (CIF). CIF-tillägget är en extra modul ovanpå [AEM Sites som en Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/home.html).

## Onboarding {#onboarding}

Introduktionen av AEM Commerce som Cloud Service är en tvåstegsprocess:

1. Få AEM Commerce som en Cloud Service aktiverad och CIF-tillägget etablerat
2. Anslut AEM Commerce som en Cloud Service med er e-handelslösning

Det första startsteget görs av Adobe. Mer information om priser och provisionering får du av din säljare.

När du har etablerats med CIF-tillägget kommer det att tillämpas på alla befintliga Cloud Manager-program. Om du inte har något Cloud Manager-program måste du skapa ett nytt. Mer information finns i [Konfigurera ditt program](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

Det andra steget är självbetjäning för varje AEM som en Cloud Service-miljö. Det finns ytterligare konfigurationer du behöver göra efter den första etableringen av CIF-tillägget.

## Ansluta AEM till en Commerce Solution {#magento}

Om du vill ansluta CIF-tillägget och [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) med en e-handelslösning måste du ange URL:en för GraphQL-slutpunkten via en Cloud Manager-miljövariabel. Variabelnamnet är `COMMERCE_ENDPOINT`. En säker anslutning via HTTPS måste konfigureras.

Miljövariabeln används på två ställen:

- GraphQL-anrop från AEM till e-handelsbackend via en gemensam delbar GraphQl-klient som används av AEM CIF Core Components och kundprojektskomponenter.
- Konfigurera en GraphQL-proxy-URL för varje AEM som variabeln är inställd på `/api/graphql`. Detta används av AEM utvecklingsverktyg (CIF-tillägg) och CIF-komponenter på klientsidan.

En annan GraphQL-slutpunkts-URL kan användas som Cloud Service för varje AEM. På så sätt kan projekt koppla AEM staging-miljöer till e-handelssystem och AEM produktionsmiljö till ett handelsproduktionssystem. GraphQL-slutpunkten måste vara offentligt tillgänglig, privata VPN-anslutningar eller lokala anslutningar stöds inte. Ett autentiseringshuvud kan anges om du vill använda ytterligare CIF-funktioner som kräver autentisering.

Tillägget CIF är valfritt och endast för Adobe Commerce Enterprise/Cloud. Det har stöd för användning av mellanlagrade katalogdata för AEM. Detta kräver att du konfigurerar en auktoriseringstoken. Den konfigurerade auktoriseringstoken är bara tillgänglig och används AEM författarinstanser av säkerhetsskäl. AEM publiceringsinstanser kan inte visa mellanlagrade data.

Det finns två alternativ för att konfigurera slutpunkten:

### Via användargränssnittet i Cloud Manager (standard) {#cm-ui}

Detta kan du göra med en dialogruta på sidan Miljöinformation. När den här sidan visas för ett program som har stöd för Commerce visas en knapp om slutpunkten inte är konfigurerad:

![CM-miljöinformation](/help/commerce-cloud/assets/commerce-cmui.png)

Om du klickar på den här knappen öppnas en dialogruta:

![CM Commerce Endpoint](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

När slutpunkten (eventuellt en autentiseringstoken för stöd för mellanlagrad katalog) har angetts visas slutpunkten på detaljsidan. Om du klickar på ikonen Redigera öppnas samma dialogruta där slutpunkten kan ändras om det behövs.

![CM-miljöinformation](/help/commerce-cloud/assets/commerce-cmui-done.png)

### Via Adobe I/O CLI {#adobe-cli}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

Följ de här stegen för att ansluta AEM till en e-handelslösning via Adobe I/O CLI:

1. Skaffa Adobe I/O CLI med plugin-programmet Cloud Manager

   Läs [dokumentationen för Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) om hur du hämtar, konfigurerar och använder [Adobe I/O CLI](https://github.com/adobe/aio-cli) med [CLI-plugin-programmet för Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Autentisera Adobe I/O CLI med AEM som ett Cloud Service-program

3. Ange variabeln `COMMERCE_ENDPOINT` i Cloud Manager

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Mer information finns i [CLI-dokument](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid).

   Slutpunktens URL för Commerce GraphQL måste peka på e-handelns GraphQl-tjänst och använda en säker HTTPS-anslutning. Till exempel: `https://<yourmagentosystem>/graphql`.

4. Aktivera mellanlagrade katalogfunktioner som kräver autentisering (valfritt)

   >[!NOTE]
   >
   >Den här funktionen är endast tillgänglig i Adobe Commerce Enterprise eller Cloud Edition. Mer information finns i [Tokenbaserad autentisering](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens).

   Ange den hemliga variabeln `COMMERCE_AUTH_HEADER` i Cloud Manager:

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>Du kan visa alla Cloud Manager-variabler med följande kommando för att dubbelkontrollera: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

Detta gör att du kan använda AEM Commerce som Cloud Service och driftsätta ditt projekt via Cloud Manager.

## Konfigurera butiker och kataloger {#catalog}

CIF-tillägget och [CIF Core-komponenterna](https://github.com/adobe/aem-core-cif-components) kan användas på flera AEM webbplatsstrukturer som är anslutna till olika e-handelsbutiker (eller butiksvyer osv.). Som standard distribueras CIF-tillägget med en standardkonfiguration som ansluter till Adobe Commerce standardbutik och -katalog (Magento).

Den här konfigurationen kan justeras för projektet via CIF-Cloud Servicens konfiguration enligt följande steg:

1. I AEM går du till Verktyg -> Cloud Services -> CIF-konfiguration

2. Välj den e-postkonfiguration som du vill ändra

3. Öppna konfigurationsegenskaperna via åtgärdsfältet

![Konfiguration av CIF-Cloud Services](/help/commerce-cloud/assets/cif-cloud-service-config.png)

Följande egenskaper kan konfigureras:

- GraphQL-klient - Välj den konfigurerade GraphQL-klienten för e-handel med serverdelskommunikation. Detta bör normalt vara kvar som standard.
- Butiksvy - (Magento) butiksvyns identifierare. Om den är tom används standardbutiksvyn.
- Proxysökväg för GraphQL - URL-sökvägen för GraphQL-proxy som används AEM proxybegäranden till GraphQL-slutpunkten för handel.
   >[!NOTE]
   >
   > I de flesta inställningar får standardvärdet `/api/graphql` inte ändras. Endast avancerade inställningar som inte använder den angivna GraphQL-proxyn bör ändra den här inställningen.
- Aktivera stöd för katalog-UID - aktivera stöd för UID i stället för ID i e-handelsbackend-GraphQL-anropen.
   >[!NOTE]
   >
   > Stöd för UID introducerades i Adobe Commerce (Magento) 2.4.2. Aktivera bara detta om e-handelsbackend har stöd för ett GraphQL-schema av version 2.4.2 eller senare.
- Katalogrotkategoriidentifierare - identifieraren (UID eller ID) för arkivkatalogroten

Konfigurationen som visas ovan är för referens. Projekten ska innehålla egna konfigurationer.

Mer komplexa inställningar som använder flera AEM webbplatsstrukturer i kombination med olika e-handelskataloger finns i [Commerce Multi-Store Setup](configuring/multi-store-setup.md) självstudiekursen.

## Ytterligare resurser {#additional-resources}

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Inställningar för Commerce Multi-Store](configuring/multi-store-setup.md)
