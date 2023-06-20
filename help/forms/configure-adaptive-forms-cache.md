---
title: Konfigurera anpassad Forms-cache
seo-title: Configure Adaptive Forms cache
description: Cacheminnet för Adaptiv Forms är särskilt utformat för adaptiva Forms och dokument. Den cachelagrar adaptiva Forms-dokument och adaptiva dokument i syfte att minska den tid som krävs för att återge ett adaptivt formulär eller dokument på klienten.
seo-description: The Adaptive Forms cache is designed specifically for Adaptive Forms and documents. It caches Adaptive Forms and adaptive documents with the objective of reducing the time required to render an Adaptive Form or document on the client.
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 0%

---


# Konfigurera anpassad Forms-cache {#configure-adaptive-forms-cache}

Ett cacheminne är en mekanism som förkortar dataåtkomsttider, minskar latensen och förbättrar I/O-hastigheter (input/output). I adaptiv Forms-cache lagras endast HTML-innehåll och JSON-struktur i ett adaptivt formulär utan att några förfyllda data sparas. Det minskar tiden som krävs för att återge ett adaptivt formulär på klienten. Det är särskilt utformat för Adaptiv Forms.

## Konfigurera anpassad Forms-cache vid författare och publiceringsinstanser {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Gå till konfigurationshanteraren AEM webbkonsolen på `https://[server]:[port]/system/console/configMgr`.
1. Klicka **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]** om du vill redigera dess konfigurationsvärden.
1. I [!UICONTROL edit configuration values] anger du det maximala antalet formulär eller dokument som en instans av AEM [!DNL Forms] servern kan cachelagra i **[!UICONTROL Number of Adaptive Forms]** fält. Standardvärdet är 100.

   >[!NOTE]
   >
   >Om du vill inaktivera cachen anger du värdet i fältet Antal adaptiva Forms till **0**. Cacheminnet återställs och alla formulär och dokument tas bort från cacheminnet när du inaktiverar eller ändrar cachekonfigurationen.

   ![Konfigurationsdialogruta för adaptiv Forms HTML cache](assets/cache-configuration-edit.png)

1. Klicka **[!UICONTROL Save]** för att spara konfigurationen.

Miljön är konfigurerad att använda cacheanpassad Forms och relaterade resurser.


## (Valfritt) Konfigurera cache för adaptiv form vid dispatcher {#configure-the-cache}

Du kan också konfigurera adaptiv formulärscachning vid dispatcher för ytterligare prestandaförbättringar.

### Krav {#pre-requisites}

* Aktivera [sammanfoga eller förifylla data på klienten](prepopulate-adaptive-form-fields.md#prefill-at-client) alternativ. Det hjälper till att sammanfoga unika data för varje instans av ett förfyllt formulär.
* [Aktivera tömningsagent för varje publiceringsinstans](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=en#invalidating-dispatcher-cache-from-a-publishing-instance). Det ger bättre cachningsprestanda för Adaptive Forms. Standardwebbadressen för rensningsagenter är `http://[server]:[port]]/etc/replication/agents.publish/flush.html`.

### Att tänka på vid cachelagring av Adaptiv Forms på en dispatcher {#considerations}

* När du använder cacheminnet för Adaptiv Forms använder du AEM [!DNL Dispatcher] för att cachelagra klientbibliotek (CSS och JavaScript) för ett adaptivt formulär.
* När du utvecklar anpassade komponenter ska du på den server som används för utveckling inaktivera den adaptiva Forms-cachen.
* URL:er utan tillägg cachelagras inte. Exempel: URL med mönstermönster`/content/forms/[folder-structure]/[form-name].html` cachelagras och URL:er med mönster ignoreras `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Använd URL:er med tillägg för att utnyttja fördelarna med cachning.
* Överväganden för lokaliserade adaptiva Forms:
   * Använd URL-format `http://host:port/content/forms/af/<afName>.<locale>.html` begära en lokaliserad version av ett adaptivt formulär i stället för `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * Inaktivera med webbläsarens språkområde <!-- [Disable using browser locale](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) -->för URL:er med format `http://host:port/content/forms/af/<adaptivefName>.html`.
   * När du använder URL-format `http://host:port/content/forms/af/<adaptivefName>.html`och **[!UICONTROL Use Browser Locale]** i konfigurationshanteraren är inaktiverad, används den icke-lokaliserade versionen av det adaptiva formuläret. Det icke-lokaliserade språket är det språk som används vid utvecklingen av det adaptiva formuläret. Språkinställningen som är konfigurerad för webbläsaren (webbläsarens språkområde) tas inte med i beräkningen och en icke-lokaliserad version av den anpassade formen används.
   * När du använder URL-format `http://host:port/content/forms/af/<adaptivefName>.html`och **[!UICONTROL Use Browser Locale]** när konfigurationshanteraren är aktiverad, tillhandahålls en lokaliserad version av det adaptiva formuläret, om en sådan finns. Språket i det lokaliserade adaptiva formuläret baseras på det språk som är konfigurerat för webbläsaren (webbläsarens språkområde). Det kan leda till [cachelagra endast första instansen av ett adaptivt formulär]. Om du vill förhindra att ett problem inträffar på din instans kan du läsa [felsökning](#only-first-insatnce-of-adptive-forms-is-cached).

### Aktivera cachelagring vid dispatcher

Följ stegen nedan för att aktivera och konfigurera cachelagring av Adaptiv Forms för dispatcher:

1. Öppna följande URL för varje publiceringsinstans i miljön och konfigurera replikeringsagenten:
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [Lägg till följande i din dispatcher.alla filer](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#automatically-invalidating-cached-files):

   ```JSON
      /invalidate
      {
      /0000
      {
      /glob "*"
      /type "deny"
      }
      /0001
      {
      # Consider all HTML files stale after an activation.
      /glob "*.html"
      /type "allow"
      }
      /0002
      {
      # Exclude htmls present in AF directories
      /glob "/content/forms/**/*.html"
      /type "deny"
      }
   ```

   När du lägger till ovanstående:

   * Ett anpassat formulär finns kvar i cachen tills en uppdaterad version av formuläret inte publiceras.

   * När en nyare version av en resurs som refereras i ett adaptivt formulär publiceras blir den adaptiva Forms automatiskt ogiltig. Det finns några undantag för automatisk ogiltigförklaring av refererade resurser. Information om hur du använder undantag finns i [felsökning](#troubleshooting) -avsnitt.
1. [Lägg till nedanstående regeldispatcher.vilken eller vilken anpassad regelfil som helst](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#specifying-the-documents-to-cache). URL:er som inte stöder cachelagring utesluts. Exempel: Interaktiv kommunikation.

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Don't cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Don't cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Don't cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [Lägg till följande parametrar i listan över ignorerade URL-parametrar](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#ignoring-url-parameters):

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

Din AEM är konfigurerad att cachelagra Adaptiv Forms. Den cachelagrar alla typer av adaptiva Forms. Om du måste kontrollera användarbehörighet för en sida innan du kan leverera den cachelagrade sidan, se [cachelagra skyddat innehåll](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html).

## Felsökning {#troubleshooting}

### En del anpassningsbara Forms som innehåller bilder eller videor ogiltigförklaras inte automatiskt från dispatcherns cache {#videos-or-images-not-auto-invalidated}

#### Problem {#issue1}

När du markerar och lägger till bilder eller videoklipp via en filläsare i ett adaptivt formulär och dessa bilder och videoklipp redigeras i Assets Editor blir Adaptive Forms som innehåller sådana bilder inte automatiskt ogiltigt från dispatchercachen.

#### Lösning {#Solution1}

När du har publicerat bilder och video avpublicerar och publicerar du den adaptiva Forms som refererar till dessa resurser.

### En del anpassningsbara Forms som innehåller innehållsfragment eller upplevelsefragment ogiltigförklaras inte automatiskt från dispatchercachen {#content-or-experience-fragment-not-auto-invalidated}

#### Problem {#issue2}

När du lägger till ett innehållsfragment eller ett upplevelsefragment i ett adaptivt formulär och dessa resurser redigeras och publiceras oberoende av varandra, blir Adaptiv Forms som innehåller sådana resurser inte automatiskt ogiltiga från dispatchercachen.

#### Lösning {#Solution2}

Efter publicering av uppdaterat innehållsfragment eller upplevelsefragment avpublicerar och publicerar du explicit det adaptiva Forms som använder dessa resurser.

### Endast den första instansen av ett adaptivt formulär cachelagras{#only-first-insatnce-of-adptive-forms-is-cached}

#### Problem {#issue3}

När URL:en för det adaptiva formuläret inte har någon lokaliseringsinformation, och **[!UICONTROL Use Browser Locale]** när konfigurationshanteraren är aktiverad används en lokaliserad version av det adaptiva formuläret och endast den första instansen av det adaptiva formuläret cachelagras och levereras till varje efterföljande användare.

#### Lösning {#Solution3}

Utför följande steg för att lösa problemet:

1. Öppna conf.d/httpd-dispatcher.conf eller någon annan konfigurationsfil som är konfigurerad att läsas in under körning.

1. Lägg till följande kod i filen och spara den. Det är en exempelkod som ändrar den så att den passar din miljö.

```XML
   <VirtualHost *:80>
        # Set log level high during development / debugging and then turn it down to whatever is appropriate
    LogLevel rewrite:trace6
        # Start Rewrite Engine
    RewriteEngine On
        # Handle actual URL convention (just pass through)
        RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
 
        # Handle selector based redirection basded on browser language
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two characters which most likely is the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```
