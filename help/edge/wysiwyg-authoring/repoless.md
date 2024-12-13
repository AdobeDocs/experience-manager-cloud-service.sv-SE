---
title: Återanvända kod över flera platser
description: Om du har många liknande webbplatser som oftast ser ut och beter sig på samma sätt, men har olika innehåll, ska du lära dig hur du kan dela kod mellan flera webbplatser i en responslös modell.
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: e25e21984ebadde7076d95c6051b8bfca5b2ce03
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

---


# Återanvända kod över flera platser {#repoless}

Om du har många liknande webbplatser som oftast ser ut och beter sig på samma sätt, men har olika innehåll, ska du lära dig hur du kan dela kod mellan flera webbplatser i en responslös modell.

## En kodbas för flera platser {#one-codebase}

Som standard är AEM nära knuten till din koddatabas, som uppfyller de flesta användningsfall. Du kan dock ha flera webbplatser som skiljer sig mest åt i innehållet, men som kan utnyttja samma kodbas.

I stället för att skapa flera GitHub-databaser och köra varje plats från en dedikerad GitHub-databas samtidigt som de är synkroniserade stöder AEM att du kör flera webbplatser från samma kodbas.

Den här förenklade konfigurationen, som eliminerar behovet av kodreplikering, kallas även [&quot;repless&quot;,](https://www.aem.live/docs/repoless) eftersom alla utom den första platsen inte behöver en egen GitHub-databas.

Om ditt projekt kräver den flexibilitet som krävs för att återanvända kod mellan olika webbplatser kan du aktivera funktionen.

Oavsett hur många webbplatser du vill skapa på ett oförglömligt sätt måste du skapa din första webbplats, som fungerar som din baswebbplats. I det här dokumentet förklaras hur du skapar den första webbplatsen för smidig användning.

## Förutsättningar {#prerequisites}

Om du vill använda den här funktionen måste du göra följande.

* Din webbplats är redan helt konfigurerad genom att följa dokumentet [Guiden Komma igång för utvecklare för WYSIWYG-redigering med Edge Delivery Services.](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)
* Du kör minst AEM as a Cloud Service 2024.08.

Du måste också be Adobe att konfigurera två objekt åt dig. Nå ut till Adobe via din Slack-kanal eller ta upp ett supportproblem för att göra dessa förfrågningar.

* Konfigurationstjänsten [aem.live](https://www.aem.live/docs/config-service-setup#prerequisites) är aktiv för din miljö och du är konfigurerad som administratör.
* Den defekta funktionen måste aktiveras av Adobe.

## Aktivera funktion för svarslös {#activate}

Det finns flera steg för att aktivera felfria funktioner för ditt projekt.

1. [Hämta åtkomsttoken](#access-token)
1. [Konfigurera konfigurationstjänsten](#config-service)
1. [Ange åtkomstkontroll](#access-control)
1. [Uppdatera AEM](#update-aem)
1. [Autentisera webbplats](#authenticate-site)

I de här stegen används webbplatsen `https://wknd.site` som exempel. Ersätt dina egna på lämpligt sätt.

### Hämta åtkomsttoken {#access-token}

Du måste först ha en åtkomsttoken för att kunna använda konfigurationstjänsten och konfigurera den för ett svarslöst användningsfall.

1. Gå till `https://admin.hlx.page/login` och använd adressen `login_adobe` för att logga in hos identitetsleverantören Adobe.
1. Du vidarebefordras till `https://admin.hlx.page/profile`.
1. Kopiera värdet för `x-auth-token` från JSON-webbtokencookien som `admin.hlx.page`-sidan anger med hjälp av webbläsarens utvecklarverktyg.

När du har en åtkomsttoken kan den skickas i huvudet för cURL-begäranden i följande format.

```text
--header 'x-auth-token: <your-token>'
```

### Konfigurera konfigurationstjänsten {#config-service}

Som anges i [förutsättningarna](#prerequisites) måste konfigurationstjänsten vara aktiverad för din miljö. Du kan kontrollera konfigurationen av konfigurationstjänsten med det här cURL-kommandot.

```text
curl  --location 'https://admin.hlx.page/config/<your-github-org>.json' \
--header 'x-auth-token: <your-token>'
```

Om konfigurationstjänsten är korrekt konfigurerad returneras JSON som liknar följande.

```json
{
  "title": "<your-github-org>",
  "description": "Your GitHub Org",
  "lastModified": "2024-11-14T12:14:04.230Z",
  "created": "2024-11-14T12:13:37.032Z",
  "version": 1,
  "users": [
    {
      "email": "justthisguyyouknow@adobe.com",
      "roles": [
        "admin"
      ],
      "id": "<your-id>"
    }
  ]
}
```

Nå ut till Adobe via din Slack-projektkanal eller utlösa ett supportproblem om konfigurationstjänsten inte är aktiverad. När du har en token och verifierat att konfigurationstjänsten är aktiverad kan du fortsätta med konfigurationen.

1. Kontrollera att innehållskällan är korrekt konfigurerad.

   ```text
   curl --request GET \
   --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>.json \
   --header 'x-auth-token: <your-token>'
   ```

1. Lägg till en sökvägsmappning i den offentliga konfigurationen.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/public.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "paths": {
           "mappings": [
               "/content/<your-site-content>/:/"
      ],
           "includes": [
               "/content/<your-site-content>/"
           ]
       }
   }'
   ```

När den offentliga konfigurationen har skapats kan du komma åt den via en URL som liknar `https://main--<your-aem-project>--<your-github-org>.aem.page/config.json` för att verifiera den.

### Ange åtkomstkontroll {#access-control}

Om du vill konfigurera åtkomstkontroll måste du ange ett tekniskt konto.

1. Skapa en ny sida i platsens rot och välj mallen [**Konfiguration**.](/help/edge/wysiwyg-authoring/tabular-data.md#other)
   * Du kan lämna konfigurationen tom med endast de fördefinierade kolumnerna `key` och `value`. Du behöver bara skapa den.
1. Skapa en mappning i den offentliga konfigurationen till platskonfigurationen med ett cURL-kommando som liknar följande.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/public.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "paths": {
           "mappings": [
               "/content/<your-site-content>/:/",
               "/content/<your-site-content>/configuration:/.helix/config.json"
      ],
           "includes": [
               "/content/<your-site-content>/"
           ]
       }
   }'
   ```
1. Verifiera att den offentliga konfigurationen har ställts in och är tillgänglig med ett cURL-kommando som liknar följande:

   ```text
   curl 'https://main--<your-aem-project>--<your-github-org>.aem.live/config.json'
   ```
1. I webbläsaren kan du nu hämta det tekniska kontot som svar på följande länk.

   ```text
   https://author-p<programID>-e<envionmentID>.adobeaemcloud.com/bin/franklin.delivery/<your-github-org>/<your-aem-project>/main/.helix/config.json
   ```

Svaret liknar följande:

```json
{
  "total": 1,
  "offset": 0,
  "limit": 1,
  "data": [
    {
      "key": "admin.role.publish",
      "value": "<tech-account-id>@techacct.adobe.com"
    }
  ],
  ":type": "sheet"
}
```

1. Ange det tekniska kontot i konfigurationen med ett cURL-kommando som liknar följande.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/access.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
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
   }'
   ```

Eftersom du nu använder konfigurationstjänsten kan du ta bort `fstab.yaml` och `paths.json` från Git-databasen.

>[!NOTE]
>
>Genom att använda konfigurationstjänsten och visa sökvägsmappningen via `config.json`, ignoreras filen `path.json`.

När AEM har konfigurerats för felfri användning måste du använda konfigurationstjänsten och ange en giltig `config.json` med sökvägsmappningen.

### Uppdatera AEM {#update-aem}

Nu är du redo att göra nödvändiga ändringar i dina Edge Delivery Services i AEM.

1. Logga in på AEM författarinstans och gå till **Verktyg** -> **Cloud Service** -> **Konfiguration av Edge Delivery Services** och markera den konfiguration som skapades automatiskt för platsen. Tryck eller klicka på **Egenskaper** i verktygsfältet.
1. I fönstret **Konfiguration av Edge Delivery Services** ändrar du projekttypen till **aem.live med konfigurationskonfiguration utan replik** och trycker eller klickar på **Spara och stäng**.
   ![Konfiguration av Edge Delivery Services](/help/edge/wysiwyg-authoring/assets/repoless/edge-delivery-services-configuration.png)
1. Gå tillbaka till webbplatsen med Universal Editor och kontrollera att den fortfarande återges korrekt.
1. Ändra en del av innehållet och återpublicera det.
1. Besök din publicerade webbplats på `https://main--<your-aem-project>--<your-github-org>.aem.page/` och kontrollera att ändringarna återspeglas korrekt.

Ditt projekt är nu konfigurerat för smidig användning.

## Nästa steg {#next-steps}

Nu när baswebbplatsen är konfigurerad för snabb användning kan du skapa ytterligare webbplatser som utnyttjar samma kodbas. Se följande dokumentation beroende på ditt användningssätt.

* [Tillförlitlig hantering av flera platser](/help/edge/wysiwyg-authoring/repoless-msm.md)
* [Repoless Stage- och Prod-miljöer](/help/edge/wysiwyg-authoring/repoless-stage-prod.md)

## Felsökning {#troubleshooting}

Det vanligaste problemet som uppstår efter att du har konfigurerat det obestridliga användningsexemplet är att sidorna i Universell redigerare inte längre återges eller att du får en vit sida eller ett generiskt AEM as a Cloud Service-felmeddelande. I sådana fall

* Visa den återgivna sidans källa.
   * Är det något som återges (korrigera HTML head med `scripts.js`, `aem.js` och redigeringsrelaterade JSON-filer)?
* Kontrollera AEM `error.log` för författarinstansen för undantag.
   * Det vanligaste problemet är att sidkomponenten misslyckas med 404 fel.
   * `config.json or paths.json` kan inte läsas in
   * `component-definition.json` osv. kan inte läsas in
