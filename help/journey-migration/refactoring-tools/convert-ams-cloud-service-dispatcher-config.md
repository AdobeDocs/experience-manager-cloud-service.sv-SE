---
title: Konvertera en hanterad tjänst till en Adobe Experience Manager as a Cloud Service Dispatcher-konfiguration
description: Konvertera en hanterad tjänst till en Adobe Experience Manager as a Cloud Service Dispatcher-konfiguration
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 39%

---


# Konvertera en hanterad tjänst till en Adobe Experience Manager (AEM) as a Cloud Service Dispatcher-konfiguration

## Introduktion {#introduction}

I det här avsnittet finns stegvisa instruktioner för hur du konverterar en AMS-konfiguration.

>[!NOTE]
>Det förutsätter att du har ett arkiv med en struktur som liknar den som beskrivs i [Hantera dina Dispatcher-konfigurationer](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/getting-started/dispatcher-configurations.html).

## Steg för att konvertera en hanterad tjänst till en AEM as a Cloud Service Dispatcher-konfiguration

1. **Extrahera arkivet och ta bort ett eventuellt prefix**

   Extrahera arkivet till en mapp och se till att de omedelbara undermapparna börjar med conf, conf.d, conf.dispatcher.d och conf.modules.d. Om de inte gör det flyttar du dem uppåt i hierarkin.

1. **Ta bort oanvända undermappar och filer**

   Ta bort undermapparna conf och conf.modules.d och filer som matchar conf.d/*.conf.

1. **Ta bort alla virtuella värdar som inte är publicerade** 

1. **Ta bort en virtuell värd-fil**

   I conf.d/enabled_vhosts som har författare, felfri, hälsa, lc eller tömt sitt namn. Alla virtuell värd-filer i conf.d/available_vhosts som inte är länkade kan också tas bort.

1. Ta bort eller kommentera virtuell värd-sektioner som inte refererar till port 80

   Om du fortfarande har avsnitt i dina virtuella värdfiler som endast refererar till andra portar än port 80, till exempel

   `<VirtualHost *:443>`
   `...`
   `</VirtualHost>`
ska du ta bort eller kommentera dem. Programsatser i de här avsnitten bearbetas inte, men om du behåller dem kan du ändå redigera dem utan någon effekt, vilket är förvirrande.

1. **Kontrollera återskrivningar**

   * Ange katalogen conf.d/rewrites.

   * Ta bort alla filer med namnen base_rewrite.rules och xforward_forcessl_rewrite.rules och kom ihåg att ta bort Include-satser i de virtuell värd-filerna som refererar till dem.

   * Om conf.d/rewrites nu innehåller en enda fil bör namnet på filen ändras till rewrite.rules och glöm inte att anpassa programsatserna Include som refererar till den filen i de virtuella värdfilerna.

   * Om mappen däremot innehåller flera, virtuella värdspecifika filer, ska deras innehåll kopieras till programsatsen Inkludera som refererar till dem i de virtuella värdfilerna.

1. **Kontrollera variabler**

   1. Ange katalogen conf.d/variables.

   1. Ta bort alla filer med namnet ams_default.vars och kom ihåg att ta bort Include-satser i de virtuell värd-filer som refererar till dem.

   1. Om conf.d/variables nu innehåller en enda fil bör namnet på filen ändras till custom.vars och du får inte glömma att anpassa programsatserna Include som refererar till den filen i de virtuella värdfilerna.

   1. Om mappen däremot innehåller flera, virtuella värdspecifika filer, ska deras innehåll kopieras till programsatsen Inkludera som refererar till dem i de virtuella värdfilerna.

1. **Ta bort vitlistor**

   Ta bort mappen conf.d/whitelists och ta bort Include-satser i de virtuell värd-filer som refererar till en fil i den undermappen.

1. **Ersätt alla variabler som inte längre är tillgängliga**

   I alla virtuell värd-filer:

   Byt namn på PUBLISH_DOCROOT till DOCROOT
Ta bort avsnitt som refererar till variabler med namnen DISP_ID, PUBLISH_FORCE_SSL eller PUBLISH_WHITELIST_ENABLED

1. **Kontrollera status genom att köra valideraren**

   Kör Dispatcher-valideraren i din katalog med underkommandot httpd:

   `$ validator httpd`
Om fel uppstår om inkluderingsfiler saknas kontrollerar du om du har ändrat namn på filerna korrekt.

   Om Apache-direktiv som inte är vitlistade visas tar du bort dem.

1. **Ta bort alla icke-publicerade servergrupper**

   Ta bort alla servergruppsfiler i conf.dispatcher.d/enabled_farm som har författare, felfri, hälsosam, lc eller tömt sitt namn. Alla servergruppsfiler i conf.dispatcher.d/available_farms som inte är länkade kan också tas bort.

1. **Byta namn på servergruppsfiler**

   Alla grupper i conf.dispatcher.d/enabled_farm måste byta namn för att matcha mönstret *.farm. Byt namn `customerX_farm.any` till `customerX.farm`.

1. **Kontrollera cache**

   Ange katalogen conf.dispatcher.d/cache.

   Ta bort alla filer som har prefixet `ams_`.

   Om conf.dispatcher.d/cache nu är tom kopierar du filen `conf.dispatcher.d/cache/rules.any` från standardkonfigurationen för Dispatcher till den här mappen. Standardkonfigurationen för Dispatcher finns i mappen src för denna SDK. Glöm inte att anpassa $include-satserna som refererar till `ams_*_cache.any` regelfiler i servergruppsfilerna också.

   Om i stället conf.dispatcher.d/cache nu innehåller en enda fil med suffix `_cache.any`bör namnet ändras till `rules.any`. Kom ihåg att anpassa $include-satserna som refererar till den filen i servergruppsfilerna också.

   Om mappen emellertid innehåller flera, servergruppsspecifika filer med det mönstret, ska innehållet kopieras till $include-satsen som refererar till dem i servergruppsfilerna.

   Ta bort alla filer som har suffixet `_invalidate_allowed.any`.

   Kopiera filen conf.dispatcher.d/cache/default_invalidate_any från standardkonfigurationen för Dispatcher till den platsen.

   I varje servergruppsfil tar du bort allt innehåll i avsnittet cache/allowedClients och ersätter det med:

   $include &quot;../cache/default_invalidate.any&quot;

1. **Kontrollera klientrubriker**

   Ange katalogen conf.dispatcher.d/clientheaders.

   Ta bort alla filer som har prefixet `ams_`.

   Om conf.dispatcher.d/clientheaders innehåller en enda fil med suffix `_clientheaders.any`, ändra namn på det till `clientheaders.any`. Kom ihåg att anpassa $include-satserna som refererar till den filen i servergruppsfilerna också.

   Om mappen emellertid innehåller flera, servergruppsspecifika filer med det mönstret, ska innehållet kopieras till $include-satsen som refererar till dem i servergruppsfilerna.

   Kopiera filen `conf.dispatcher/clientheaders/default_clientheaders.any` från standardkonfigurationen för Dispatcher till den platsen.

   Ersätt alla `clientheader` include-programsatser som visas som följande:

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"`

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"`

   med programsatsen:

   `$include "../clientheaders/default_clientheaders.any"`

1. **Kontrollera filter**

   * Ange katalogen conf.dispatcher.d/filters.

   * Ta bort alla filer som har prefixet `ams_`.

   * Om conf.dispatcher.d/filters nu innehåller en enda fil byter du namn på den till `filters.any`. Kom ihåg att anpassa $include-satserna som refererar till den filen i servergruppsfilerna också.

   * Om mappen emellertid innehåller flera, servergruppsspecifika filer med det mönstret, ska innehållet kopieras till $include-satsen som refererar till dem i servergruppsfilerna.

   * Kopiera filen `conf.dispatcher/filters/default_filters.any` från standardkonfigurationen för Dispatcher till den platsen.

   * Ersätt eventuella filtersatser som innehåller följande i varje servergruppsfil:

   * $include `"/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"`
med programsatsen:

     `$include "../filters/default_filters.any"`

1. **Kontrollera återgivningar**

   * Ange katalogen conf.dispatcher.d/renders.

   * Ta bort alla filer i den mappen.

   * Kopiera filen `conf.dispatcher.d/renders/default_renders.any` från standardkonfigurationen för Dispatcher till den platsen.

   * I varje servergruppsfil tar du bort allt innehåll i återgivningsavsnittet och ersätter det med:

     `$include "../renders/default_renders.any"`

1. **Kontrollera virtuella värdar**

   * Byt namn på katalogen `conf.dispatcher.d/vhosts to conf.dispatcher.d/virtualhosts` och ange den.

   * Ta bort alla filer som har prefixet `ams_`.

   * Om conf.dispatcher.d/virtualhosts nu innehåller en enda fil byter du namn på den till `virtualhosts.any`. Kom ihåg att anpassa $include-satserna som refererar till den filen i servergruppsfilerna också.

   * Om mappen emellertid innehåller flera, servergruppsspecifika filer med det mönstret, ska innehållet kopieras till $include-satsen som refererar till dem i servergruppsfilerna.

   * Kopiera filen `conf.dispatcher/virtualhosts/default_virtualhosts.any` från standardkonfigurationen för Dispatcher till den platsen.

   * Ersätt eventuella filtersatser som innehåller följande i varje servergruppsfil:

     `$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"`
med programsatsen:

     `$include "../virtualhosts/default_virtualhosts.any"`


1. **Kontrollera status genom att köra valideraren**

   * Kör Dispatcher-valideraren i din katalog med underkommandot Dispatcher:

     `$ validator dispatcher`

   * Om fel uppstår om inkluderingsfiler saknas kontrollerar du om du har ändrat namn på filerna korrekt.

   * Om felmeddelanden som rör en odefinierad variabel `PUBLISH_DOCROOT` visas, ändrar du namnet till `DOCROOT`.

   * Alla andra fel finns i felsökningsavsnittet i dokumentationen för valideringsverktyget. 

## Testa konfigurationen med en lokal driftsättning {#testing-config-local-deployment}

>[!IMPORTANT]
>
>Testningen av konfigurationen med en lokal driftsättning kräver installation av Docker.

Med hjälp av skriptet `docker_run.sh` i Dispatcher SDK kan du testa att konfigurationen inte innehåller några andra fel som bara skulle visas i driftsättningen:

1. Generera driftsättningsinformation med valideraren.

   `validator full -d out`
Validerar den fullständiga konfigurationen och genererar distributionsinformation in out.

1. Starta Dispatcher i en buffertavbildning med den distributionsinformationen.

   När AEM publiceringsserver körs på din macOS-dator och lyssnar på port 4503 kan du köra Dispatcher framför den servern enligt följande:

   `$ docker_run.sh out docker.for.mac.localhost:4503 8080`

   Startar behållaren och visar Apache på den lokala porten 8080.

## Använda din nya Dispatcher-konfiguration {#using-dispatcher-config}

Om valideraren inte längre rapporterar något problem och Docker-behållaren startar utan fel eller varningar kan du flytta konfigurationen till en`ispatcher/src` underkatalog i Git-databasen.