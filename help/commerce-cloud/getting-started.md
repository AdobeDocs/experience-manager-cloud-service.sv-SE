---
title: Komma igång med AEM Commerce as a Cloud Service
description: Lär dig hur du distribuerar ett e-handelsaktiverat AEM till ett AEM som körs som en molntjänstmiljö. Använd funktionerna i Adobe Cloud Manager och en CI/CD-pipeline för att bygga Venia-referensbutiken till en körbar miljö.
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: Cloud Service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
source-git-commit: 118945f407dab8ccad1ec018b588b64972fb5f12
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 0%

---

# Komma igång med AEM Commerce as a Cloud Service {#start}

För att komma igång med AEM Commerce as a Cloud Service måste din Experience Manager Cloud Service etableras med tillägget Commerce Integration Framework (CIF). CIF-tillägget är ytterligare en modul ovanpå [AEM Sites as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/home.html).

## Onboarding {#onboarding}

Introduktionen av AEM Commerce as a Cloud Service är en tvåstegsprocess:

1. Aktivera AEM Commerce as a Cloud Service och CIF-tillägget har etablerats
2. Anslut AEM Commerce as a Cloud Service till din e-handelslösning

Det första startsteget görs av Adobe. Mer information om priser och provisionering får du av din säljare.

När du har etablerats med CIF-tillägget kommer det att tillämpas på alla befintliga Cloud Manager-program. Om du inte har något Cloud Manager-program måste du skapa ett nytt. Mer information finns i [Konfigurera ditt program](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

Det andra steget är självbetjäning för varje AEM as a Cloud Service miljö. Det finns ytterligare konfigurationer du behöver göra efter den första etableringen av CIF-tillägget.

## Ansluta AEM till en Commerce Solution {#solution}

Ansluta CIF-tillägget och [AEM CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components) med en e-handelslösning måste du ange URL:en för GraphQL-slutpunkten via en Cloud Manager-miljövariabel. Variabelnamnet är `COMMERCE_ENDPOINT`. En säker anslutning via HTTPS måste konfigureras.

Miljövariabeln används på två ställen:

- GraphQL-anrop från AEM till e-handelsbackend via en gemensam delbar GraphQl-klient som används av AEM CIF Core Components och kundprojektskomponenter.
- Konfigurera en GraphQL-proxy-URL för varje AEM som variabeln är inställd på `/api/graphql`. Detta används av AEM utvecklingsverktyg (CIF-tillägg) och CIF-komponenter på klientsidan.

En annan URL för GraphQL-slutpunkt kan användas för varje AEM as a Cloud Service miljö. På så sätt kan projekt koppla AEM staging-miljöer till e-handelssystem och AEM produktionsmiljö till ett handelsproduktionssystem. GraphQL-slutpunkten måste vara offentligt tillgänglig, privata VPN-anslutningar eller lokala anslutningar stöds inte. Ett autentiseringshuvud kan anges om du vill använda ytterligare CIF-funktioner som kräver autentisering.

Tillägget CIF kan användas endast för Adobe Commerce Enterprise/Cloud med stöd för användning av testade katalogdata för AEM. Detta kräver att du konfigurerar en auktoriseringshuvud. Den här rubriken är bara tillgänglig och används AEM författarinstanser av säkerhetsskäl. AEM publiceringsinstanser kan inte visa mellanlagrade data.

Det finns två alternativ för att konfigurera slutpunkten:

### Via användargränssnittet i Cloud Manager (standard) {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

Detta kan du göra med en dialogruta på sidan Miljöinformation. När den här sidan visas för ett program som har stöd för Commerce visas en knapp om slutpunkten inte är konfigurerad:

![CM-miljöinformation](/help/commerce-cloud/assets/commerce-cmui.png)

Om du klickar på den här knappen öppnas en dialogruta:

![CM Commerce Endpoint](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

När slutpunkten och eventuellt en auktoriseringshuvud för stöd för mellanlagrad katalog har angetts, visas slutpunkten på detaljsidan. Om du klickar på ikonen Redigera öppnas samma dialogruta där slutpunkten kan ändras om det behövs.

![CM-miljöinformation](/help/commerce-cloud/assets/commerce-cmui-done.png)

### Via Adobe I/O CLI  {#adobe-cli}

Följ de här stegen för att ansluta AEM till en e-handelslösning via Adobe I/O CLI:

1. Skaffa Adobe I/O CLI med plugin-programmet Cloud Manager

   Kontrollera [Dokumentation för Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) om hur du hämtar, konfigurerar och använder [Adobe I/O CLI](https://github.com/adobe/aio-cli) med [CLI-plugin för Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Autentisera Adobe I/O CLI med det AEM as a Cloud Service programmet

3. Ange `COMMERCE_ENDPOINT` variabel i Cloud Manager

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Se [CLI-dokument](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) för mer information.

   Slutpunktens URL för Commerce GraphQL måste peka på e-handelns GraphQl-tjänst och använda en säker HTTPS-anslutning. Till exempel: `https://<yourcommercesystem>/graphql`.

4. Aktivera mellanlagrade katalogfunktioner som kräver autentisering (valfritt)

   >[!NOTE]
   >
   >Den här funktionen är endast tillgänglig med Adobe Commerce Enterprise eller Cloud Edition. Se [Tokenbaserad autentisering](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens) för mer information.

   Ange `COMMERCE_AUTH_HEADER` hemlig variabel i Cloud Manager:

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>Du kan visa alla Cloud Manager-variabler med följande kommando för att dubbelkontrollera: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

Detta gör att du kan använda AEM Commerce as a Cloud Service och driftsätta ditt projekt via Cloud Manager.

## Konfigurera butiker och kataloger {#catalog}

CIF-tillägget och [CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components) kan användas på flera AEM webbplatsstrukturer som är anslutna till olika e-handelsbutiker (eller butiksvyer osv.). Som standard distribueras CIF-tillägget med en standardkonfiguration som ansluter till Adobe Commerce standardbutik och -katalog.

Den här konfigurationen kan justeras för projektet via CIF-Cloud Servicens konfiguration enligt följande steg:

1. I AEM går du till Verktyg -> Cloud Services -> CIF-konfiguration

2. Välj den e-postkonfiguration som du vill ändra

3. Öppna konfigurationsegenskaperna via åtgärdsfältet

![Konfiguration av CIF-Cloud Services](/help/commerce-cloud/assets/cif-cloud-service-config.png)

Följande egenskaper kan konfigureras:

- GraphQL-klient - Välj den konfigurerade GraphQL-klienten för e-handel med serverdelskommunikation. Detta bör normalt vara kvar som standard.
- Butiksvy - butiksvyns identifierare. Om den är tom används standardbutiksvyn.
- Proxysökväg för GraphQL - URL-sökvägen för GraphQL-proxy som används AEM proxybegäranden till GraphQL-slutpunkten för handel.
   >[!NOTE]
   >
   > I de flesta inställningar är standardvärdet `/api/graphql` får inte ändras. Endast avancerade inställningar som inte använder den angivna GraphQL-proxyn bör ändra den här inställningen.
- Aktivera stöd för katalog-UID - aktivera stöd för UID i stället för ID i e-handelsbackend-GraphQL-anropen.
   >[!NOTE]
   >
   > Stöd för UID introducerades i Adobe Commerce 2.4.2. Aktivera bara detta om e-handelsbackend har stöd för ett GraphQL-schema av version 2.4.2 eller senare.
- Katalogrotkategoriidentifierare - identifieraren (UID eller ID) för arkivkatalogroten
   >[!CAUTION]
   >
   > Från och med CIF Core Components version 2.0.0 finns stöd för `id` togs bort och ersattes med `uid`. Om ditt projekt använder CIF Core Components version 2.0.0 måste du aktivera stöd för katalog-UID och använda ett giltigt kategori-UID som &quot;Katalogens rotkategoriidentifierare&quot;.

Konfigurationen som visas ovan är för referens. Projekten ska innehålla egna konfigurationer.

Mer komplexa inställningar som använder flera AEM webbplatsstrukturer i kombination med olika e-handelskataloger finns i [Inställningar för Commerce Multi-Store](configuring/multi-store-setup.md) självstudiekurs.

## Ytterligare resurser {#additional-resources}

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Inställningar för Commerce Multi-Store](configuring/multi-store-setup.md)
- [Installation av flera Commerce Systems](configuring/multiple-commerce-systems-setup.md)

