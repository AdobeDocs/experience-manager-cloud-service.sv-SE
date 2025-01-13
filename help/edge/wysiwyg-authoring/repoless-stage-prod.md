---
title: Repoless Stage- och Prod-miljöer
description: Lär dig hur du skapar separata sajter för staging- och produktionsmiljöer som utnyttjar en enda kodbas på ett smidigt sätt.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 701bd9bc-30e8-4654-8248-a06d441d1504
source-git-commit: 42218450ab03201c69c59053f720954183f4b652
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Repoless Stage- och Prod-miljöer {#repoless-stage-prod}

Lär dig hur du skapar separata sajter för staging- och produktionsmiljöer som utnyttjar en enda kodbas på ett smidigt sätt.

## Ökning {#overview}

Du kanske vill konfigurera en plats för din produktionsmiljö som är separat från din staging-miljö. Att konfigurera en andra plats för en separat staging- och produktionsinställning liknar konfigurationen för [som krävs för hantering av flera platser.](/help/edge/wysiwyg-authoring/repoless-msm.md) Den kan faktiskt kombineras med MSM-webbplatsstrukturer om det behövs.

Det här dokumentet använder det typiska exemplet med separata miljöer för staging och produktion. Du kan skapa separata miljöer för de miljöer du vill.

## Konfiguration {#configuration}

I det här dokumentet beskrivs hur du konfigurerar en separat produktionsplats för ditt projekt med samma kodbas. Följande antaganden görs.

* Mellanlagringsplatsen har redan konfigurerats och du vill nu skapa en konfiguration för produktionsplatsen.
* Innehållsstrukturen i AEM är likartad.
* Samma sökvägsmappningar används för mellanlagring och produktion.

I det här exemplet antar vi att en produktionsplats redan har skapats för projektet wknd vars GitHub-repo också kallas wknd.

Det finns två steg för att konfigurera en separat produktionsplats.

1. [Skapa nya Edge Delivery Services för produktionsmiljön.](#create-edge-site)
1. [Uppdatera molnkonfigurationen i AEM för produktionsplatsen.](#update-cloud-configuration)

### Skapa nya Edge Delivery Services för produktionsmiljön {#create-edge-site}

1. Hämta din auth-token och programmets tekniska konto.
   * I dokumentet **Återanvända kod mellan platser** finns mer information om hur du [hämtar din åtkomsttoken](/help/edge/wysiwyg-authoring/repoless.md#access-token) och det [tekniska kontot](/help/edge/wysiwyg-authoring/repoless.md#access-control) för ditt program.
1. Skapa en ny plats genom att göra följande anrop till konfigurationstjänsten. Tänk på följande:
   * Projektnamnet i POST-URL:en måste vara det nya platsnamnet som du skapar. I det här exemplet är det `wknd-prod`.
   * Konfigurationen `code` ska vara densamma som du använde när du skapade det första projektet.
   * `content` > `source` > `url` måste anpassas till namnet på den nya platsen som du skapar. I det här exemplet är det `wknd-prod`.
   * Webbplatsnamnet i POST-URL och `content` > `source` > `url` måste vara samma.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-prod.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "code": {
           "owner": "<your-github-org>",
           "repo": "wknd",
           "source": {
               "type": "github",
               "url": "https://github.com/<your-github-org>/wknd"
           }
       },
       "content": {
           "source": {
               "url": "https://author-p<programID>-e<environmentID>.adobeaemcloud.com/bin/franklin.delivery/<your-github-org>/wknd-prod/main",
               "type": "markup",
               "suffix": ".html"
           }
       },
       "access": {
           "admin": {
               "role": {
                   "admin": [
                       "*@adobe.com"
                   ],
                   "config_admin": [
                       "<tech-account-id>@techacct.adobe.com"
                   ]
               },
               "requireAuth": "auto"
           }
       }
   }'
   ```

1. Lägg till sökvägsmappningen för den nya platsen genom att göra följande anrop till konfigurationstjänsten.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-prod/public.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "paths": {
           "mappings": [
               "/content/wknd/:/"
           ],
           "includes": [
               "/content/wknd/"
           ]
       }
   }'
   ```

Verifiera att den offentliga konfigurationen för den nya platsen fungerar genom att anropa `https://main--wknd-prod--<your-github-org>.aem.page/config.json` och verifiera innehållet i den returnerade JSON.

### Uppdatera molnkonfigurationer i AEM för din produktionsplats {#update-cloud-configuration}

Din AEM måste vara konfigurerad att använda de nya Edge Delivery Sites som du skapade i föregående avsnitt för en dedikerad produktionsplats. I det här exemplet måste innehåll under `/content/wknd` i din produktionsmiljö känna till för att kunna använda den `wknd-prod`-plats du skapade.

1. Logga in i AEM produktionsinstans och gå till **Verktyg** -> **Cloud Service** -> **Konfiguration av Edge Delivery Services**.
1. Välj den konfiguration som skapades automatiskt för ditt projekt.
1. Tryck eller klicka på **Egenskaper** i verktygsfältet.
1. I fönstret **Konfiguration av Edge Delivery Services**:
   * Ange din GitHub-organisation i fältet **Organisation**.
   * Ändra platsnamnet till namnet på platsen som du skapade i föregående avsnitt. I det här fallet är det `wknd-prod`.
   * Ändra projekttypen till **aem.live med konfigurationen för den omvända konfigurationen**.
1. Tryck eller klicka på **Spara och stäng**.

## Verifiera installationen {#verify}

Nu när du har gjort alla nödvändiga konfigurationsändringar kontrollerar du att allt fungerar som det ska.

1. Logga in i din AEM produktionsredigeringsinstans.
1. Navigera till **webbplatskonsolen** genom att gå till **Navigering** -> **Platser**.
1. Välj en sida på webbplatsen.
1. Tryck eller klicka på **Redigera** i verktygsfältet.
1. Kontrollera att sidan återges korrekt i Universellt redigeringsprogram och använder samma kod som platsroten.
1. Gör ändringar på sidan och publicera på nytt.
1. Besök webbplatsen för nya Edge Delivery Services för den sidan på `https://main--wknd-prod--<your-github-org>.aem.page`.

Om du ser ändringarna som du har gjort fungerar inställningarna för den separata produktionsplatsen som de ska.
