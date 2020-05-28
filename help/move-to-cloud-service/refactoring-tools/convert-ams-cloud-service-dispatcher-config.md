---
title: Konvertera en AMS till en Adobe Experience Manager som en konfiguration för Cloud Service Dispatcher
description: Konvertera en AMS till en Adobe Experience Manager som en konfiguration för Cloud Service Dispatcher
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 0%

---


# Konvertera en AMS till en Adobe Experience Manager (AEM) som en konfiguration för Cloud Service Dispatcher

## Introduktion {#introduction}

I det här avsnittet finns stegvisa instruktioner för hur du konverterar en AMS-konfiguration.

>[!NOTE]
>Det förutsätter att du har ett arkiv med en struktur som liknar den som beskrivs i [Hantera dina Dispatcher-konfigurationer](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html).

## Steg för konvertering av en AMS till AEM som konfiguration av Cloud Service Dispatcher

1. **Extrahera arkivet och ta bort ett eventuellt prefix**

   Extrahera arkivet till en mapp och se till att de omedelbara undermapparna börjar med conf, conf.d, conf.dispatcher.d och conf.modules.d. Om de inte gör det flyttar du dem uppåt i hierarkin.

1. **Ta bort oanvända undermappar och filer**

   Ta bort undermapparna conf och conf.modules.d samt filer som matchar conf.d/*.conf.

1. **Ta bort alla virtuella värdar som inte är publicerade**

1. **Ta bort en virtuell värdfil**

   I conf.d/enabled_vhosts som har författare, felfri, hälsotillstånd, lc eller tömt sitt namn. Alla virtuella värdfiler i conf.d/available_vhosts som inte är länkade till kan också tas bort.

1. Ta bort eller kommentera virtuella värdsektioner som inte refererar till port 80

   Om du fortfarande har avsnitt i dina virtuella värdfiler som endast refererar till andra portar än port 80, t.ex.

   `<VirtualHost *:443>`
   `...`
   `</VirtualHost>`
ta bort eller kommentera dem. Programsatser i de här avsnitten bearbetas inte, men om du behåller dem kan du ändå redigera dem utan någon effekt, vilket är förvirrande.

1. **Kontrollera återskrivningar**

   * Ange katalogen conf.d/rewrites.

   * Ta bort alla filer med namnen base_rewrite.rules och xforward_forcessl_rewrite.rules och kom ihåg att ta bort Include-satser i de virtuella värdfilerna som refererar till dem.

   * Om conf.d/rewrites nu innehåller en enda fil bör namnet ändras till rewrite.rules och glöm inte att anpassa de Include-satser som refererar till den filen även i de virtuella värdfilerna.

   * Om mappen däremot innehåller flera, virtuella värdspecifika filer, ska deras innehåll kopieras till programsatsen Include som refererar till dem i de virtuella värdfilerna.

1. **Kontrollera variabler**

   1. Ange katalogen conf.d/variables.

   1. Ta bort alla filer med namnet ams_default.vars och kom ihåg att ta bort Include-satser i de virtuella värdfiler som refererar till dem.

   1. Om conf.d/variables now contains a single file, ska namnet på filen ändras till custom.vars och glöm inte att anpassa programsatserna Include som refererar till den filen även i de virtuella värdfilerna.

   1. Om mappen däremot innehåller flera, virtuella värdspecifika filer, ska deras innehåll kopieras till programsatsen Include som refererar till dem i de virtuella värdfilerna.

1. **Ta bort vitlistor**

   Ta bort mappen conf.d/whitelists och ta bort Include-satser i de virtuella värdfilerna som refererar till en fil i den undermappen.

1. **Ersätt alla variabler som inte längre är tillgängliga**

   I alla virtuella värdfiler:

   Byt namn på PUBLISH_DOCROOT till DOCROOTRa bort avsnitt som refererar till variabler med namnen DISP_ID, PUBLISH_FORCE_SSL eller PUBLISH_WHITELIST_ENABLED

1. **Kontrollera ditt tillstånd genom att köra valideraren**

   Kör dispatchervalideraren i din katalog med underkommandot httpd:

   `$ validator httpd`
Om du ser fel om saknade inkluderingsfiler ska du kontrollera om du har bytt namn på filerna korrekt.

   Om Apache-direktiv som inte är vitlistade visas tar du bort dem.

1. **Ta bort alla icke-publicerade servergrupper**

   Ta bort alla servergruppsfiler i conf.dispatcher.d/enabled_farm som har författare, felfri, hälsosam, lc eller tömt sitt namn. Alla servergruppsfiler i conf.dispatcher.d/available_farm som inte är länkade till kan också tas bort.

1. **Byt namn på servergruppsfiler**

   Alla grupper i conf.dispatcher.d/enabled_farm måste byta namn så att de matchar mönstret *.farm, så t.ex. en servergruppsfil med namnet customerX_farm.any bör byta namn till customerX.farm.

1. **Kontrollera cache**

   Ange katalogen conf.dispatcher.d/cache.

   Ta bort eventuella filer med prefix-namn_.

   Om conf.dispatcher.d/cache nu är tom kopierar du filen conf.dispatcher.d/cache/rules.any. Standarddispatcherkonfigurationen finns i mappsrc för denna SDK. Glöm inte att anpassa $include-satserna som refererar till ams_*_cache.alla regelfiler i servergruppsfilerna också.

   Om i stället conf.dispatcher.d/cache nu innehåller en enda fil med suffixet _cache.any bör namnet på filen ändras till rules.any och glöm inte att anpassa $include-satserna som refererar till den filen i servergruppsfilerna.

   Om mappen emellertid innehåller flera, gruppspecifika filer med det mönstret, ska innehållet i dem kopieras till $include-satsen som refererar till dem i servergruppsfilerna.

   Ta bort alla filer som har suffixet _invalidate_allowed.any.

   Kopiera filen conf.dispatcher.d/cache/default_invalidate_any från standardkonfigurationen för dispatcher till den platsen.

   I varje servergruppsfil tar du bort allt innehåll i avsnittet cache/allowedClients och ersätter det med:

   $include &quot;../cache/default_invalidate.any&quot;

1. **Kontrollera klientrubriker**

   Ange katalogen conf.dispatcher.d/clientheaders.

   Ta bort eventuella filer med prefix-namn_.

   Om conf.dispatcher.d/clientheaders nu innehåller en enda fil med suffixet _clientheaders.any, bör namnet ändras till clientheaders.any och glöm inte att anpassa $include-satserna som refererar till den filen i servergruppsfilerna också.

   Om mappen emellertid innehåller flera, gruppspecifika filer med det mönstret, ska innehållet i dem kopieras till $include-satsen som refererar till dem i servergruppsfilerna.

   Kopiera filen conf.dispatcher/clientheaders/default_clientheaders.any från standarddispatcherkonfigurationen till den platsen.

   Ersätt alla klientrubriker med programsatser som ser ut så här i varje servergruppsfil:

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"`

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"`

   med programsatsen:

   `$include "../clientheaders/default_clientheaders.any"`

1. **Kontrollera filter**

   * Ange katalogen conf.dispatcher.d/filters.

   * Ta bort eventuella filer med prefix-namn_.

   * Om conf.dispatcher.d/filters nu innehåller en enda fil bör namnet ändras till filters.any och glöm inte att anpassa $include-satserna som refererar till den filen i servergruppsfilerna också.

   * Om mappen emellertid innehåller flera, gruppspecifika filer med det mönstret, ska innehållet i dem kopieras till $include-satsen som refererar till dem i servergruppsfilerna.

   * Kopiera filen conf.dispatcher/filters/default_filters.any från standarddispatcherkonfigurationen till den platsen.

   * Ersätt alla filter med programsatser som ser ut så här i varje servergruppsfil:

   * $include `"/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"`med programsatsen:

      `$include "../filters/default_filters.any"`

1. **Kontrollera återgivningar**

   * Ange katalogen conf.dispatcher.d/renders.

   * Ta bort alla filer i den mappen.

   * Kopiera filen conf.dispatcher.d/renders/default_renders.any från standarddispatcherkonfigurationen till den platsen.

   * I varje servergruppsfil tar du bort allt innehåll i återgivningsavsnittet och ersätter det med:

      `$include "../renders/default_renders.any"`

1. **Kontrollera virtuella värdar**

   * Byt namn på katalogen `conf.dispatcher.d/vhosts to conf.dispatcher.d/virtualhosts` och ange den.

   * Ta bort alla filer som har prefix `ams_`.

   * Om conf.dispatcher.d/virtualhosts nu innehåller en enda fil bör namnet ändras till virtualhosts.any och glöm inte att anpassa $include-satserna som refererar till den filen i servergruppsfilerna.

   * Om mappen emellertid innehåller flera, gruppspecifika filer med det mönstret, ska innehållet i dem kopieras till $include-satsen som refererar till dem i servergruppsfilerna.

   * Kopiera filen conf.dispatcher/virtualhosts/default_virtualhosts.any från standarddispatcherkonfigurationen till den platsen.

   * Ersätt alla filter med programsatser som ser ut så här i varje servergruppsfil:

      `$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"`
med programsatsen:

      `$include "../virtualhosts/default_virtualhosts.any"`


1. **Kontrollera ditt tillstånd genom att köra valideraren**

   * Kör dispatchervalideraren i din katalog med dispatcherunderkommandot:

      `$ validator dispatcher`

   * Om du ser fel om saknade inkluderingsfiler ska du kontrollera om du har bytt namn på filerna korrekt.

   * Om du ser fel som rör en odefinierad variabel `PUBLISH_DOCROOT`ändrar du namnet till `DOCROOT`.

   * Alla andra fel finns i felsökningsavsnittet i dokumentationen för valideringsverktyget.

## Testa konfigurationen med en lokal distribution {#testing-config-local-deployment}

>[!IMPORTANT]
> Testningen av konfigurationen med en lokal driftsättning kräver installation av Docker.

Med hjälp av skriptet `docker_run.sh` i Dispatcher SDK kan du testa att konfigurationen inte innehåller några andra fel som bara skulle visas i distributionen:

1. Generera distributionsinformation med valideraren

   `validator full -d out`
Detta validerar den fullständiga konfigurationen och genererar distributionsinformation som

1. Starta dispatchern i en buffertavbildning med den distributionsinformationen

   När AEM-publiceringsservern körs på din macOS-dator och lyssnar på port 4503 kan du köra dispatchern framför den servern enligt följande:

   `$ docker_run.sh out docker.for.mac.localhost:4503 8080`

   Detta startar behållaren och visar Apache på den lokala porten 8080.

## Använda din nya dispatcherkonfiguration {#using-dispatcher-config}

Om valideraren inte längre rapporterar något problem och dockningsbehållaren startar utan fel eller varningar kan du flytta konfigurationen till en`ispatcher/src` underkatalog i Git-databasen.