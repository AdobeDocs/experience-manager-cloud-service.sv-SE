---
title: Snabba utvecklingsmiljöer
description: Lär dig hur du använder miljöer för snabb utveckling för snabb utveckling i en molnmiljö.
exl-id: 1e9824f2-d28a-46de-b7b3-9fe2789d9c68
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '4990'
ht-degree: 0%

---

# Snabba utvecklingsmiljöer {#rapid-development-environments}

För att kunna driftsätta ändringar kräver de aktuella utvecklingsmiljöerna i molnet en process som använder omfattande kodsäkerhet och kvalitetsregler som kallas CI/CD-pipeline. I situationer där snabba och iterativa förändringar behövs har Adobe infört snabba utvecklingsmiljöer (RDE) för kort tid.

Tack vare de lokala redigeringssystemen kan utvecklare snabbt driftsätta och granska ändringar, vilket minimerar den tid som krävs för att testa funktioner som är beprövade i en lokal utvecklingsmiljö.

När ändringarna har testats i en RDE kan de distribueras till en vanlig Cloud Development-miljö via Cloud Manager pipeline.

>[!NOTE]
> Kontakta RDE-utvecklarna på vår [Discord-kanal](https://discord.com/channels/1131492224371277874/1245304281184079872). Du kan ställa frågor eller ge feedback om RDE-ämnen.

>[!VIDEO](https://video.tv.adobe.com/v/3415582/?quality=12&learn=on)


Du kan se ytterligare videofilmer som visar [hur du konfigurerar den](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html), [hur du använder den](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html) och [utvecklingscykeln](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/development-life-cycle.html) med hjälp av RDE.

## Introduktion {#introduction}

RDE kan användas för kod, innehåll och Apache- eller Dispatcher-konfigurationer. Till skillnad från vanliga Cloud Development-miljöer kan utvecklare använda lokala kommandoradsverktyg för att synkronisera kod som skapats lokalt till en RDE.

Alla program tillhandahålls med en RDE. Om det finns sandlådekonton är de i viloläge efter några timmars icke-användning.

När de skapas ställs de lokala utvecklingsmiljöerna in på den senast tillgängliga Adobe Experience Manager-versionen (AEM). En RDE-återställning, som kan utföras med Cloud Manager, går igenom RDE-filen och ställer in den till den senast tillgängliga AEM-versionen.

Vanligtvis används en RDE av en enskild utvecklare vid en viss tidpunkt för att testa och felsöka en viss funktion. När utvecklingssessionen är klar kan den återställas till ett standardläge för nästa användning.

Ytterligare RDE kan licensieras för produktionsprogram (ej sandlådeprogram).

## Aktivera RDE i ett program {#enabling-rde-in-a-program}

Följ de här stegen för att använda Cloud Manager för att skapa en RDE för ditt program.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Klicka på det program som du vill lägga till en RDE till för att visa information om det.

   * RDE kan läggas till i både [sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) och [produktionsprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md).

1. Klicka på **Lägg till miljö** på **miljökortet** på sidan **Programöversikt** för att lägga till en miljö.

   ![Miljökort](/help/implementing/cloud-manager/assets/no-environments.png)

   * Alternativet **Lägg till miljö** är också tillgängligt på fliken **Miljö**.

     ![Fliken Miljö](/help/implementing/cloud-manager/assets/environments-tab.png)

   * Alternativet **Lägg till miljö** kan vara inaktiverat på grund av bristande behörighet eller beroende på de licensierade resurserna.

1. I dialogrutan **Lägg till miljö** som visas:

   * Välj **Snabb utveckling** under rubriken **Välj miljötyp**.
      * Antalet tillgängliga/använda miljöer visas inom parentes bakom miljötypen.
   * Ange ett **namn** för miljön.
   * Ange en valfri **beskrivning** för miljön.
   * Välj en **molnregion**.

   ![Dialogrutan Lägg till miljö](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. Klicka på **Spara** för att lägga till den angivna miljön.

Skärmen **Översikt** visar nu din nya miljö på kortet **Miljöer**.

När de skapas ställs de virtuella skrivborden in på den senast tillgängliga AEM. En RDE-återställning, som även kan utföras med Cloud Manager, går igenom RDE-filen och ställer in den till den senast tillgängliga AEM-versionen.

Mer information om hur du använder Cloud Manager för att skapa miljöer, hantera vem som har åtkomst till dem och tilldela anpassade domäner finns i [Cloud Manager-dokumentationen](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

## Installera kommandoradsverktygen för RDE {#installing-the-rde-command-line-tools}

När du har lagt till en RDE för programmet med Cloud Manager kan du interagera med den genom att konfigurera kommandoradsverktygen enligt följande steg:

>[!IMPORTANT]
>
>Kontrollera att version 20 av [Node och NPM är installerade](https://nodejs.org/en/download/) så att Adobe I/O CLI och relaterade plugin-program fungerar som de ska.


1. Installera CLI-verktygen för Adobe I/O enligt den här [proceduren](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).
1. Installera Adobe I/O CLI-verktyg AEM RDE-plugin:

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. Logga in med AIR-klienten.

   ```
   aio login
   ```

   Inloggningsinformationen (token) lagras i den globala AIR-konfigurationen och stöder därför endast en inloggning och organisation. Om du vill använda flera olika referensmiljöer som behöver olika inloggningar eller organisationer följer du exemplet nedan för att presentera kontexter.

   <details><summary>Följ det här exemplet för att konfigurera en lokal kontext för en av dina RDE-inloggningar</summary>
   Följ de här stegen om du vill lagra inloggningsinformationen lokalt i en aio-fil i den aktuella katalogen i en viss kontext. Ett sammanhang är också ett smart sätt att konfigurera en CI/CD-miljö eller skript.  Om du vill använda den här funktionen måste du använda minst aio-cli-version 10.3.1. Uppdatera den med "npm install -g @adobe/aio-cli"

   Låt oss skapa ett sammanhang som kallas &quot;mycontext&quot; som vi sedan anger som standardkontext med plugin-programmet för autentisering innan vi anropar inloggningskommandot.

   ```
   aio config set --json -l "ims.contexts.mycontext" "{ cli.bare-output: false }"
   aio auth ctx -s mycontext
   aio login --no-open
   ```

   >[!NOTE]
   > Inloggningskommandot med alternativet `--no-open` ger en URL i terminalen i stället för att öppna din standardwebbläsare. Du kan kopiera och öppna den med ett **incognito**-fönster i webbläsaren. På så sätt ändras inte den inloggade sessionen i det normala webbläsarfönstret, och du kan se till att du använder den inloggning och organisation som krävs för ditt sammanhang.

   Det första kommandot skapar en ny konfiguration för inloggningskontext, med namnet `mycontext`, i den lokala `.aio`-konfigurationsfilen (filen skapas vid behov). Det andra kommandot anger att kontexten `mycontext` ska vara &quot;aktuell&quot; kontext, dvs. som standard.

   När den här konfigurationen är på plats lagrar inloggningskommandot automatiskt inloggningstoken i kontexten `mycontext` och behåller därmed den lokalt.

   Flera kontexter kan hanteras antingen genom att lokala konfigurationer sparas i flera mappar. Du kan också konfigurera flera kontexter i en enda konfigurationsfil och växla mellan dem genom att ändra den&quot;aktuella&quot; kontexten.
   </details>

1. Konfigurera RDE-pluginen så att den använder din organisation, ditt program och din miljö. Med konfigurationskommandot nedan får användaren en lista över program i sin organisation och visar RDE-miljöer i det programmet att välja mellan.

   ```
   aio aem:rde:setup
   ```

   Installationssteget kan hoppas över om avsikten är att använda en skriptmiljö. I så fall kan värdena för organisation, program och miljö inkluderas i varje kommando. [Mer information finns i följande kommandon.](#rde-cli-commands).

### Den interaktiva installationen {#installing-the-rde-command-line-tools-interactive}

Installationskommandot frågar om den angivna konfigurationen ska lagras lokalt eller globalt.

```
Setup the CLI configuration necessary to use the RDE commands.
? Do you want to store the information you enter in this setup procedure locally? (y/N)
```

Välj `no` att
* lagra organisationen, programmet och miljön globalt i din AIR-konfiguration.
* arbeta med en enda RDE.

Välj `yes` att
* lagra organisationen, programmet och miljön lokalt i den aktuella katalogen i en `.aio`-fil. Detta är praktiskt om du vill implementera filen i versionskontrollen så att andra klonar Git-databasen kan använda den.
* arbeta med många referensdataposter, så att den konfigurationen används i stället när du växlar till en annan katalog.
* använder konfigurationen i en programmatisk kontext som ett skript, som kan referera till den.


När en lokal eller global konfiguration har valts försöker kommandot setup att läsa ditt organisations-ID från din aktuella inloggning och sedan läsa organisationens program. Om det inte går att hitta organisationen kan du ange den manuellt tillsammans med lite vägledning.

```
Selected only organization: XYXYXYXYXYXYXYXXYY
retrieving programs of your organization ...
```

När programmen har hämtats kan användaren välja i listan och även ange vilken typ som ska filtreras.
När programmet har valts listas en lista över RDE-miljöer att välja mellan.
Om det bara finns ett program och/eller en RDE-miljö tillgänglig väljs den automatiskt.

Kör för att se den aktuella miljökontexten:

```aio aem rde setup --show```

Kommandot kommer att ge ett resultat som liknar:

```Current configuration: cm-p1-e1: programName - environmentName (organization: ...@AdobeOrg)```

### Manuell konfigurationsprocedur i en icke-interaktiv miljö {#manual-setup}

I miljöer där ingen användare interaktivt kan köra installationskommandot enligt beskrivningen ovan (till exempel CI/CD eller skript), kan de tre parametrarna för organisation, program och miljö konfigureras manuellt enligt följande steg.


<details>
  <summary>Expandera för att hitta information om hur du konfigurerar manuellt</summary>

1. Konfigurera ditt organisations-ID och ersätt den alfanumeriska strängen med ditt eget organisations-ID.

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   * Ditt eget organisations-ID kan slås upp med den metod som beskrivs under [Visa ditt företags-ID](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

1. Konfigurera sedan ditt program-ID:

   `aio config:set cloudmanager_programid 12345`

1. Konfigurera sedan det miljö-ID som RDE ska kopplas till:

   `aio config:set cloudmanager_environmentid 123456`

1. När du är klar med konfigurationen av plugin-programmet loggar du in genom att utföra

   `aio login`

   Dessa steg kräver att du är medlem i produktprofilen Cloud Manager **Developer - Cloud Service**. Mer information finns i [Tilldela teammedlemmar till Cloud Manager produktprofiler - Tilldela produktprofilen för utvecklare](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer).

Titta på videosjälvstudiekursen [om hur du konfigurerar en RDE (06:24)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html) om du vill ha mer information och demonstration.
</details>

## Använda RDE under utvecklingen av en ny funktion {#using-rde-while-developing-a-new-feature}

Adobe rekommenderar följande arbetsflöde för att utveckla en ny funktion:

* När en mellanliggande milstolpe har nåtts och validerats lokalt med AEM as a Cloud Service SDK implementerar du koden i en Git-funktionsgren. Branschen bör inte vara en del av huvudraden ännu, även om det är valfritt att binda sig för Git. Vad som utgör en&quot;mellanmilstolpe&quot; varierar beroende på teamets vanor. Exempel är några nya kodrader, en halv arbetsdag eller en underfunktion.

* Återställ RDE om den har använts av en annan funktion och du vill [återställa den till standardläge](#reset-rde). <!-- Alexandru: hiding for now, do not delete This can be done by way of [Cloud Manager](#reset-the-rde-cloud-manager) or by way of the [command line](#reset-the-rde-command-line). -->Återställningen tar några minuter och allt befintligt innehåll och all befintlig kod tas bort. Du kan använda kommandot för RDE-status för att bekräfta att RDE är klart. Den senaste versionen av AEM kommer tillbaka till RDE.

  >[!IMPORTANT]
  >
  > Om din testnings- och produktionsmiljö inte får automatiska AEM och ligger bakom den senaste versionen av AEM, kanske koden som körs på den lokala utvecklingsmiljön inte stämmer överens med hur koden fungerar i testversionerna och produktionerna. I så fall är det särskilt viktigt att utföra grundliga tester av koden på mellanlagring innan den distribueras till produktion.


* Synkronisera lokal kod med RDE-kommandoradsgränssnittet. Du kan installera ett innehållspaket, ett specifikt paket, en OSGI-konfigurationsfil, en innehållsfil och en zip-fil för en Apache/Dispatcher-konfiguration. Det går också att referera till ett fjärrinnehållspaket. Mer information finns i [RDE Command-Line Tools](/help/implementing/developing/introduction/rapid-development-environments.md#rde-cli-commands). Du kan använda statuskommandot för att validera att distributionen lyckades. Du kan också använda Package Manager för att installera innehållspaket.

* Testa koden i RDE. URL:er för författare och Publish finns i Cloud Manager.

* Om koden inte beter sig som förväntat kan du använda standardfelsökningstekniker för att förstå problemet och göra lämpliga ändringar. Utan att implementera kodändringarna i Git (eftersom de inte har validerats) kan du synkronisera koden med den lokala CLI:n. Fortsätt tills problemet är löst.

* När koden beter sig som förväntat implementerar du koden i Git-funktionsgrenen.

* Kod som synkroniseras till RDE använder inte en Cloud Manager-pipeline, så nu bör du använda en icke-produktionsprocess från Cloud Manager för att distribuera Git-funktionsgrenen till molnutvecklingsmiljön. Detta validerar att koden klarar Cloud Manager kvalitetsportar och gör att du kan vara säker på att koden senare distribueras med Cloud Manager produktionsflöde.

* Upprepa stegen ovan för varje mellanliggande milstolpe tills all kod för funktionen är klar och fungerar bra i både RDE- och Cloud Development-miljön.

* Distribuera koden till produktionen via Cloud Manager produktionsflöde.

## Felsöka en befintlig funktion med RDE {#use-rde-to-debug-an-existing-feature}

Arbetsflödet liknar utvecklingen av en ny funktion. Skillnaden är att koden som synkroniseras till RDE skulle återspegla Git-etiketten för det som har skickats till miljön där problemet har hittats. Dessutom kan det vara användbart att distribuera innehåll som matchar den överordnade miljön. Detta kan du göra genom att exportera och importera innehållspaket.

## Flera utvecklare som samarbetar i samma utvecklingsmiljö {#multiple-developers-collaborating-on-the-same-rde}

En RDE har stöd för ett enda projekt i taget. Eftersom kod synkroniseras från en lokal utvecklingsmiljö till en RDE-miljö är det mest naturligt för en utvecklare att använda den fristående vid en viss tidpunkt.

Med noggrann samordning kan dock fler än en utvecklare validera en viss funktion eller felsöka ett specifikt problem. Nyckeln är att varje utvecklare håller sina lokala projekt synkroniserade så att kodändringar som gjorts av en viss utvecklare absorberas av andra utvecklare, annars kan en utvecklare oavsiktligt skriva över den andra utvecklarens kod. Den rekommenderade strategin är att varje utvecklare implementerar sina ändringar i en delad Git-gren innan de synkroniserar till den lokala utvecklingsmiljön, så att de andra utvecklarna drar in ändringarna innan de gör sina egna ändringar.

## Verktyg för RDE-kommandorad {#rde-cli-commands}

### Hjälp/Allmän information {#help}

* Om du vill visa en lista med kommandon skriver du:

  `aio aem:rde`

* Om du vill ha mer information om ett kommando skriver du:

  `aio aem rde <command> --help`

### Globala flaggor {#global-flags}

* För mindre utförliga utdata använder du flaggan quiet:

  `aio aem rde <command> --quiet`

  Detta tar bort vissa element, t.ex. nålar och förloppsindikatorer, och begränsar behovet av indata från användaren.

* Använd json-flaggan för JSON i stället för konsolloggutdata:

  `aio aem rde <command> --json`

  Detta returnerar giltig JSON medan konsolutdata inaktiveras. Se JSON-exempel längre fram.

* Om du vill undvika att konfigurera RDE-anslutningsinformationen med kommandot setup eller genom att skapa en AIO-konfiguration använder du de tre flaggorna för organisation, program och miljö:

  `aio aem rde <command> --organizationId=<value> --programId=<value> --environmentId=<value>`

  Detta kräver fortfarande att ```aio login``` utförs.

### Distribuera till RDE {#deploying-to-rde}

I det här avsnittet beskrivs hur du använder RDE CLI för att distribuera, installera eller uppdatera paket, OSGI-konfigurationer, innehållspaket, enskilda innehållsfiler och Apache- eller Dispatcher-konfigurationer.

Det allmänna användningsmönstret är `aio aem:rde:install <artifact>`.

Här följer några exempel:

#### Distribuera ett innehållspaket {#deploy-content-package}

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

Svaret för en lyckad distribution liknar följande:

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

Du kan även referera till en fjärrdatabas:

`aio aem:rde:install -t content-package "https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip"`

Som standard distribueras artefakter till både författar- och publiceringsnivåer, men flaggan&quot;-s&quot; kan användas för att ange ett specifikt skikt som mål.

Alla AEM kan distribueras, till exempel paket med kod, innehåll eller ett [behållarpaket](/help/implementing/developing/introduction/aem-project-content-package-structure.md#container-packages) (kallas även&quot;alla&quot;-paket).

>[!IMPORTANT]
>
>Dispatcher-konfigurationen för WKND-projektet distribueras inte via innehållspaketinstallationen ovan. Distribuera den separat enligt stegen&quot;Distribuera en Apache/Dispatcher-konfiguration&quot;.

#### Distribuera en OSGI-konfiguration {#deploy-OSGI-config}

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

Där svaret för en lyckad distribution liknar följande:

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

#### Distribuera ett paket {#deploy-bundle}

Använd följande för att distribuera ett paket:

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

Där svaret för en lyckad distribution liknar följande:

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

#### Distribuera en innehållsfil {#deploy-content-file}

Använd följande för att distribuera en innehållsfil:

`aio aem:rde:install world.txt -p /apps/hello.txt`

Där svaret för en lyckad distribution liknar följande:

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

#### Distribuera en Apache/Dispatcher-konfiguration {#deploy-apache-config}

Hela mappstrukturen måste vara i form av en ZIP-fil för den här typen av konfiguration.

Från modulen `dispatcher` i ett AEM projekt kan du zippa upp Dispatcher-konfigurationen genom att köra kommandot nedan:

`mvn clean package`

Eller använd zip-kommandot nedan från katalogen `src` i modulen `dispatcher`:

`zip -y -r dispatcher.zip .`

Distribuera sedan konfigurationen med det här kommandot:

`aio aem:rde:install target/aem-guides-wknd.dispatcher.cloud-X.X.X-SNAPSHOT.zip`

>[!TIP]
>
>Ovanstående kommando förutsätter att du distribuerar [WKND](https://github.com/adobe/aem-guides-wknd)-projektets Dispatcher-konfigurationer. Se till att ersätta `X.X.X` med motsvarande WKND-projektversionsnummer eller projektspecifikt versionsnummer när du distribuerar projektets Dispatcher-konfiguration.

>[!NOTE]
>
>RDE har stöd för Dispatcher-konfiguration i flexibelt läge, men inte för Dispatcher-konfiguration i äldre läge. Mer information om de två lägena finns i [Dispatcher-dokumentationen](/help/implementing/dispatcher/disp-overview.md#validation-debug). Du kan även läsa dokumentationen om [migrering till det flexibla läget](/help/implementing/dispatcher/validation-debug.md#migrating), om du inte redan har gjort det.

En lyckad distribution genererar ett svar som liknar följande:

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

Kod som distribueras till RDE genomgår inte någon Cloud Manager-pipeline och tillhörande kvalitetsportar. Koden går dock igenom en del analyser som rapporterar felen, vilket visas i kodexemplet nedan:

```
$ aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar
...
#19: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D74FR1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
Logs:
The analyser found the following errors for author :
[requirements-capabilities] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Artifact com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8 requires [org.apache.felix.gogo.jline/1.1.8] org.apache.felix.gogo; filter:="(&(org.apache.felix.gogo=command.implementation)(version>=1.0.0)(!(version>=2.0.0)))"; effective:=active in start level 20 but no artifact is providing a matching capability in this start level.
[api-regions-exportsimports] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Bundle org.apache.felix.gogo.jline:1.1.8 is importing package(s) [org.jline.builtins, org.jline.utils, org.apache.felix.service.command, org.apache.felix.service.threadio, org.jline.terminal, org.jline.reader, org.apache.felix.gogo.runtime, org.jline.reader.impl] in start level 20 but no bundle is exporting these for that start level.
The analyser found the following errors for publish :
[requirements-capabilities] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Artifact com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8 requires [org.apache.felix.gogo.jline/1.1.8] org.apache.felix.gogo; filter:="(&(org.apache.felix.gogo=command.implementation)(version>=1.0.0)(!(version>=2.0.0)))"; effective:=active in start level 20 but no artifact is providing a matching capability in this start level.
[api-regions-exportsimports] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Bundle org.apache.felix.gogo.jline:1.1.8 is importing package(s) [org.jline.builtins, org.jline.utils, org.apache.felix.service.command, org.apache.felix.service.threadio, org.jline.terminal, org.jline.reader, org.apache.felix.gogo.runtime, org.jline.reader.impl] in start level 20 but no bundle is exporting these for that start level.
```

Kodexemplet ovan visar beteendet om ett paket inte löses. I så fall&quot;mellanlagras&quot; den och installeras endast om dess krav (i detta fall&quot;import som saknas&quot;) uppfylls genom installation av annan kod.

#### Distribuera konfiguration relaterad till konfigurationsförlopp (yaml configs) {#deploy-config-pipeline}

De miljöspecifika konfigurationer (en eller flera dynamiska filer) som beskrivs i artikeln [Använda konfigurationsförlopp](/help/operations/config-pipeline.md) kan distribueras enligt följande:

`aio aem:rde:install -t env-config ./my-config-folder`
där my-config-folder är den överordnade mappen som innehåller dina dynamiska konfigurationer.

Du kan också installera en ZIP-fil som innehåller config-mappträdet:

`aio aem:rde:install -t env-config config.zip`

Observera att yaml-filens envTypes-matris ska innehålla värdet *rde*, som i exemplet nedan:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["rde"]
```

### Distribuera startkod baserat på webbplatsteman och webbplatsmallar {#deploying-themes-to-rde}

De lokala redigeringssystemen har stöd för klientkod som baseras på [webbplatsteman](/help/sites-cloud/administering/site-creation/site-themes.md) och [webbplatsmallar](/help/sites-cloud/administering/site-creation/site-templates.md). Med RDE:er används detta kommandoradsdirektiv för att distribuera frontendpaket, i stället för Cloud Manager [Front-End Pipeline](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md) som används för andra miljötyper.

Som vanligt kan du bygga ditt front end-paket med npm:

`npm run build`

Den ska generera en `dist/`-mapp, så den främre paketmappen ska innehålla en `package.json`-fil och en `dist`-mapp:

```
ls ./path-to-frontend-pkg-folder/
...
dist
package.json
```
Nu kan du distribuera paketet till den lokala utvecklingsmiljön genom att peka på paketmappen i serverdelen:

```
aio aem:rde:install -t frontend ./path-to-frontend-pkg-folder/
...
#1: deploy completed for frontend frontend-pipeline.zip on author,publish - done by ... at 2024-01-18T15:33:22.898Z
Logs:
> Deployed artifact wknd-1.0.0-1705592008-26e7ec1a
> with workspace hash 692021864642a20d6d298044a927d66c0d9cf2adf42d4cca0c800a378ac3f8d3
```

Du kan också komprimera filen `package.json` och mappen `dist` och distribuera zip-filen:

`zip -r frontend-pkg.zip ./path-to-frontend-pkg-folder/dist ./path-to-frontend-pkg-folder/package.json`

```
aio aem:rde:install -t frontend frontend-pkg.zip
...
#1: deploy completed for frontend frontend-pipeline.zip on author,publish - done by ... at 2024-01-18T15:33:22.898Z
Logs:
> Deployed artifact wknd-1.0.0-1705592008-26e7ec1a
> with workspace hash 692021864642a20d6d298044a927d66c0d9cf2adf42d4cca0c800a378ac3f8d3
```

>[!NOTE]
>
>Namngivningen av filerna i paketet längst fram måste följa följande namnkonventioner:
> * &quot;dist&quot;-mapp, för npm-paketets utdatamapp
> * filen &quot;package.json&quot;, för npm-beroendepaketet

>[!TIP]
>
> Om du skapade din RDE före april 2023 och upplever felet&quot;UNEXPECTED_API_ERROR&quot; när du försöker använda klientfunktionen för första gången kan du försöka ta bort miljön och skapa den igen.

### Kontrollera statusen för den lokala lagringsplatsen {#checking-rde-status}

Du kan använda RDE CLI för att kontrollera om miljön är klar att distribueras till, som vilka distributioner som har gjorts via RDE-pluginen.

Körs:

`aio aem:rde:status`

Returnerar följande:

```
Info for cm-p12345-e987654
Environment: Ready
- Bundles Author:
 com.adobe.granite.sample.demo-1.0.0.SNAPSHOT
- Bundles Publish:
 com.adobe.granite.sample.demo-1.0.0.SNAPSHOT
- Configurations Author:
 com.adobe.granite.demo.MyServlet
- Configurations Publish:
 com.adobe.granite.demo.MyServlet
```

Om kommandot returnerar en anteckning om instanser som distribueras kan du fortsätta och utföra nästa uppdatering, men den senaste uppdateringen kanske inte visas på instansen än.

### Visa distributionshistorik {#show-deployment-history}

Du kan kontrollera historiken för distributioner som gjorts till RDE genom att köra:

`aio aem:rde:history`

som returnerar ett svar i form av:

`#1: deploy completed for content-package aem-guides-wknd.all-2.1.0.zip on author,publish - done by 029039A55D4DE16A0A494025@AdobeID at 2022-09-12T14:41:55.393Z`

### Tar bort från RDE {#deleting-from-rde}

Du kan ta bort konfigurationer och paket som tidigare har distribuerats till RDE med CLI-verktyget. Använd kommandot `status` om du vill se en lista över vad som kan tas bort, som innehåller `bsn` för paket och `pid` för konfigurationer att referera till i kommandot delete.

Om till exempel `com.adobe.granite.demo.MyServlet.cfg.json` har installerats är `bsn` bara `com.adobe.granite.demo.MyServlet`, utan suffixet **cfg.json**.

Det går inte att ta bort innehållspaket eller innehållsfiler. Om du vill ta bort dem bör du återställa den skrivskyddade miljön, vilket innebär att den återgår till standardläget.

Se exemplet nedan för mer information:

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

Mer information och demonstration finns i videosjälvstudien [om hur du använder RDE-kommandon (10:01)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html).

## Loggar {#rde-logging}

På samma sätt som för andra miljötyper kan loggnivåer ställas in genom att OSGi-konfigurationer ändras, även om distributionsmodellen för RDE-konfigurationer enligt beskrivningen ovan inbegriper en kommandorad i stället för en Cloud Manager-distribution. Mer information om hur du visar, hämtar och tolkar loggar finns i [loggningsdokumentationen](/help/implementing/developing/introduction/logging.md).

RDE CLI har också ett eget loggkommando som kan användas för att snabbt konfigurera vilka klasser och paket som ska loggas och på vilken loggnivå. Dessa konfigurationer kan betraktas som tillfälliga eftersom de inte ändrar OSGI-egenskaperna i versionskontrollen. Den här funktionen fokuserar på att skräddarsy loggar i realtid, i stället för att leta efter loggar från det avlägsna förflutna.

I följande exempel visas hur du finjusterar författarnivån, med ett paket inställt på en felsökningsloggnivå, och två paket (avgränsade med blanksteg) inställda på en informationsfelsökningsnivå. Utdata som innehåller ett **auth**-paket är markerade.

`aio aem:rde:logs --target=author --debug=org.apache.sling --info=org.apache.sling.commons.threads.impl org.apache.sling.jcr.resource.internal.helper.jcr -H .auth.`

>[!TIP]
>
>Om felet `RDECLI:UNEXPECTED_API_ERROR` visas när du spelar upp med loggkommandona för författartjänsten, återställer du miljön och försöker igen. Det här felet genereras om den senaste återställningsåtgärden utfördes före slutet av maj 2024.
>
>```
>aio aem:rde:reset
>```

Mer information om alla kommandoradsalternativ finns i `aio aem:rde:logs --help`.

Funktioner:

* deklarera loggnivåer per paket eller klassnivå
* anpassa loggutdataformatet
* skräddarsy upp till fyra aktuella loggkonfigurationer, var och en i sin egen terminal
* markera specifika loggar

Observera att loggar lagras i minnet på den lokala lagringsplatsen och att dessa loggar återvinns och därmed tas bort om de inte är skräddarsydda eller om nätverket är för långsamt.


## Återställ {#reset-rde}

Om du återställer RDE tas all anpassad kod, konfigurationer och innehåll bort från både författaren och publiceringsinstansen. Den här återställningen är användbar om den aktuella miljön har använts för att testa en viss funktion och du vill återställa den till ett standardläge så att du kan testa en annan funktion.

En återställning ställer in RDE till den senast tillgängliga AEM.

Du kan återställa med hjälp av [Cloud Manager](#reset-the-rde-cloud-manager) eller med hjälp av [kommandoraden](#reset-the-rde-command-line). Återställningen tar några minuter och allt befintligt innehåll och all befintlig kod tas bort från den lokala utvecklingsmiljön.

>[OBS!]
>
>Du måste tilldelas Cloud Manager Developer-rollen för att kunna använda återställningsfunktionen. Om så inte är fallet uppstår ett fel när en återställningsåtgärd utförs.

### Återställ RDE med kommandoraden {#reset-the-rde-command-line}

Du kan återställa RDE och återställa det till standardläge genom att köra:

`aio aem:rde:reset`

Detta tar vanligtvis några minuter och rapporterar ```Environment reset.``` när det lyckades eller ```Failed to reset the environment.``` om fel. För strukturerade utdata, se kapitlet om ```--json```-utdata nedan.

Använd [statuskommandot](#checking-rde-status) för att kontrollera när miljön är klar igen.

### Återställ RDE i Cloud Manager {#reset-the-rde-cloud-manager}

Du kan använda Cloud Manager för att återställa din RDE genom att följa stegen nedan:

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Klicka på det program för vilket du vill återställa RDE.

1. På sidan **Översikt** klickar du på fliken **Miljö** högst upp på skärmen.

   ![Fliken Miljö](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * Du kan också klicka på knappen **Visa alla** på kortet **Miljöer** om du vill gå direkt till fliken **Miljöer**.

     ![Visa alla alternativ](/help/implementing/cloud-manager/assets/environment-showall.png)

1. Fönstret **Miljö** öppnas och alla miljöer för programmet visas.

   ![Miljöfliken](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. Klicka på ellipsknappen för den RDE som du vill återställa och välj sedan **Återställ**.

   ![Visa miljöinformation](/help/implementing/cloud-manager/assets/rde-reset.png)

1. Bekräfta att du vill återställa RDE genom att klicka på **Återställ** i dialogrutan.

   ![Bekräfta återställning](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. Cloud Manager bekräftar genom ett banderollmeddelande att återställningsprocessen har startat.

   ![Återställ banderollmeddelande](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

När återställningsprocessen för RDE har startats tar det oftast några minuter att slutföra och återställa miljön till standardläget. Återställningsprocessens status kan visas när som helst i kolumnen **Status** på kortet **Environmental** eller i fönstret **Environment** .

![Återställningsstatus för RDE](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

Du kan också återställa den lokala lagringsplatsen med hjälp av ellipsknappen direkt från kortet **Miljöer** på sidan **Översikt**.

![Återställ RDE från miljökortet](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

Mer information om hur du använder Cloud Manager för att hantera miljöer finns i [Cloud Manager-dokumentationen](/help/implementing/cloud-manager/manage-environments.md).

## Kommandon som stöder JSON-utdata {#json-commands}

De flesta kommandon har stöd för den globala flaggan ```--json``` som undertrycker konsolutdata och returnerar giltig json som ska bearbetas i skript. Nedan finns några kommandon som stöds, med exempel på json-utdata.

### Status {#status}

<details>
  <summary>Expandera för att se exempel på status</summary>

#### En ren RDE {#clean-rde}

```$ aio aem rde status --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Modification in progress | Deployment in progress | Upload in progress | Ready (instances are currently deploying) | Ready",
  "author": {
    "osgiBundles": [],
    "osgiConfigs": []
  },
  "publish": {
    "osgiBundles": [],
    "osgiConfigs": []
  }
}
```

#### En RDE med vissa installerade paket {#rde-installed-bundles}

```$ aio aem rde status --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Ready",
  "author": {
    "osgiBundles": [
      {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "updateId": "80",
        "service": "author",
        "type": "osgi-bundle",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        }
      }
    ],
    "osgiConfigs": [
      {
        "id": "publish_osgi-config_com.adobe.granite.demo.MyServlet",
        "updateId": "80",
        "service": "publish",
        "type": "osgi-config",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "configPid": "com.adobe.granite.demo.MyServlet"
        }
      }
    ]
  },
  "publish": {
    "osgiBundles": [
      {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "updateId": "80",
        "service": "author",
        "type": "osgi-bundle",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        }
      }
    ],
    "osgiConfigs": [
      {
        "id": "publish_osgi-config_com.adobe.granite.demo.MyServlet",
        "updateId": "80",
        "service": "publish",
        "type": "osgi-config",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "configPid": "com.adobe.granite.demo.MyServlet"
        }
      }
    ]
  }
}
```

</details>

### Installera {#install}

<details>
  <summary>Expandera för att se Exempel på installation</summary>

```$ aio aem rde install ~/Downloads/hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "items": [
    {
      "updateId": "4",
      "info": "deploy",
      "action": "deploy",
      "metadata": {
        "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip"
      },
      "services": [
        "author",
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:30:44.578Z",
        "processed": "2024-05-21T12:31:07.886468Z"
      },
      "user": "userId",
      "type": "content-package",
      "hash": "2ad73507",
      "logs": [
        "No logs available for this update."
      ]
    }
  ]
}
```

</details>

### Ta bort {#delete}

<details>
  <summary>Expandera för att se Ta bort exempel</summary>

```$ aio aem rde delete com.adobe.granite.hotdev.demo-1.0.0.SNAPSHOT --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "items": [
    {
      "updateId": "84",
      "info": "delete author_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "author"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T11:49:16.889Z",
        "processed": "2024-05-21T11:49:18.188420Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "author",
        "type": "osgi-bundle",
        "updateId": "83"
      },
      "hash": "636f6d2e",
      "logs": [
        "No logs available for this update."
      ]
    },
    {
      "updateId": "85",
      "info": "delete publish_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T11:49:23.857Z",
        "processed": "2024-05-21T11:49:25.237930Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "publish_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "publish",
        "type": "osgi-bundle",
        "updateId": "83"
      },
      "hash": "636f6d2e",
      "logs": [
        "No logs available for this update."
      ]
    }
  ]
}
```

</details>

### Historik {#history}

<details>
  <summary>Expandera för att se historikexempel</summary>

```$ aio aem rde history --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Ready",
  "items": [
    {
      "updateId": "112",
      "info": "delete publish_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:53:07.934Z",
        "processed": "2024-05-21T12:53:09.118766Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "publish_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "publish",
        "type": "osgi-bundle",
        "updateId": "110"
      },
      "hash": "636f6d2e"
    },
    {
      "updateId": "111",
      "info": "delete author_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "author"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:53:00.824Z",
        "processed": "2024-05-21T12:53:02.101560Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "author",
        "type": "osgi-bundle",
        "updateId": "110"
      },
      "hash": "636f6d2e"
    },
    {
      "updateId": "110",
      "info": "deploy",
      "action": "deploy",
      "metadata": {
        "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip"
      },
      "services": [
        "author",
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:52:12.123Z",
        "processed": "2024-05-21T12:52:31.026147Z"
      },
      "user": "userId",
      "type": "content-package",
      "hash": "2ad73507"
    }
  ]
}
```

</details>

### Återställ {#reset}

<details>
  <summary>Expandera för att se Återställa exempel</summary>

#### Eld och Glöm, vänta inte {#fire-no-wait}

```$ aio aem rde reset --no-wait --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "resetting"
}
```

#### Vänta på slutförande, återställningen har slutförts {#wait-success}

```$ aio aem rde reset --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "reset"
}
```

#### Vänta på slutförande, återställningen misslyckades {#wait-failed}

```$ aio aem rde reset --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "reset_failed"
}
```

</details>

### Starta om {#restart}

<details>
  <summary>Expandera för att se Exempel på omstart</summary>

```$ aio aem rde restart --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "restarted"
}
```

</details>

## Körningslägen {#runmodes}

RDE-specifik OSGI-konfiguration kan tillämpas med hjälp av suffix i mappnamnet, som i exemplen nedan:

* `config.rde`
* `config.author.rde`
* `config.publish.rde`

Mer information om körningslägen finns i [dokumentationen för körningsläge](/help/implementing/deploying/overview.md#runmodes).

>[!NOTE]
>
>RDE OSGI-konfigurationen är unik eftersom den ärver värdena för alla OSGI-egenskaper som deklarerats av paketets `dev`-körningsläge.

RDE skiljer sig från andra miljöer där innehåll kan installeras i en install.rde-mapp (eller install.author.rde eller install.publish.rde) under /apps. På så sätt kan du implementera innehåll för att Git och leverera det till RDE med hjälp av kommandoradsverktygen.

## Fylla med innehåll {#populating-content}

När en RDE återställs tas allt innehåll bort, och om så önskas måste en explicit åtgärd vidtas för att lägga till innehåll. Ett tips är att du bör överväga att sätta ihop en uppsättning innehåll som ska användas som testinnehåll för validering och felsökning i den lokala redigeringsmiljön. Det finns flera möjliga strategier för att fylla i den regionala utvecklingsmiljön med det innehållet:

1. Synkronisera innehållspaketet explicit till RDE med kommandoradsverktygen

1. Placera och implementera exempelinnehållet i Git i en install.rde-mapp under /apps och synka sedan det övergripande innehållspaketet till RDE med kommandoradsverktygen.

1. Använd verktyget [innehållskopiering](/help/implementing/developing/tools/content-copy.md) för att kopiera en definierad innehållsuppsättning från produkter-, scen- eller dev-miljöer eller från en annan RDE-miljö.

1. Använd pakethanteraren

Du är begränsad till 1 GB när du synkroniserar innehållspaket.


## Hur skiljer sig de lokala utvecklingsmiljöerna från utvecklingsmiljöer i molnet? {#how-are-rds-different-from-cloud-development-environments}

Även om RDE på många sätt liknar en utvecklingsmiljö i molnet finns det vissa mindre arkitektoniska skillnader som gör det möjligt att snabbt synkronisera kod. Mekanismen för att hämta kod till RDE skiljer sig åt - för RDE synkroniserar en kod från en lokal utvecklingsmiljö, medan en för Cloud Development Environment distribuerar koden via Cloud Manager.

Därför rekommenderar vi att du distribuerar koden till en Cloud Development Environment via icke-produktionsflödet när du har validerat koden i en RDE-miljö. Testa slutligen koden innan du distribuerar med produktionsflödet.

Observera även följande:

* De lokala redigeringssystemen innehåller inte någon förhandsgranskningsnivå
* De lokala redigeringssystemen stöder för närvarande inte prerelease-kanalen.


## Hur många skrivbord behöver jag? {#how-many-rds-do-i-need}

Det finns en RDE för varje licensierad lösning och Adobe erbjuder även ytterligare RDE som kan licensieras för Production-program (ej sandlådeprogram).

Hur många skrivbord som behövs beror på en organisations sammansättning och processer. Den mest flexibla modellen är när en organisation köper en dedikerad RDE för var och en av sina AEM Cloud Service-utvecklare. I den här modellen kan varje utvecklare testa sin kod på den lokala utvecklingsmiljön utan att samordna med andra gruppmedlemmar kring om det finns en tillgänglig RDE-miljö.

Å andra sidan kan ett team med en enda RDE använda interna processer för att samordna vilka utvecklare som kan använda miljön vid en viss tidpunkt. Detta kan vara möjligt när en utvecklare har nått en milstolpe för mellanliggande funktioner och är redo att validera i en molnmiljö där de snabbt kan göra de ändringar de behöver.

En mellanliggande modell är en modell där en organisation köper flera olika lagringssystem, vilket innebär att det är större sannolikhet att det finns en oanvänd lagringsbar dataström tillgänglig. En strategi kan vara att tilldela en RDE per team eller större funktion. Interna processer kan användas för att samordna användningen av miljöerna.

## Hur skiljer sig en AEM Forms Cloud Service Rapid Development Environment (RDE) från andra miljöer? {#how-are-forms-rds-different-from-cloud-development-environments}

Forms-utvecklare kan använda AEM Forms Cloud Service Rapid Development Environment för att snabbt utveckla adaptiva Forms, arbetsflöden och anpassningar som att anpassa kärnkomponenter, integreringar med tredjepartssystem med mera. AEM Forms Cloud Service Rapid Development Environment (RDE) saknar stöd för kommunikations-API:er. Den har inte heller stöd för funktioner som kräver en dokumentfil, som att generera en dokumentfil när en anpassad blankett skickas in. Följande AEM Forms-funktioner är inte tillgängliga i en Rapid Development Environment (RDE):

* Konfigurera ett postdokument för ett adaptivt formulär
* Generera ett registreringsdokument när ett adaptivt formulär skickas eller när ett arbetsflödessteg tas
* Skicka postdokument som en bifogad fil med åtgärden Skicka via e-post eller med steget E-post i ett arbetsflöde
* Använda Adobe Sign i ett adaptivt formulär eller i ett arbetsflödessteg
* Kommunikations-API:er

>[!NOTE]
>
> Det är ingen skillnad på användargränssnittet i Rapid Development Environment (RDE) och andra Cloud Service för Forms. Alla alternativ som är relaterade till Dokumentformat, som att välja ett dokument med en postmall för ett anpassat formulär, fortsätter att visas i användargränssnittet. De här miljöerna har inga kommunikations-API:er och dokumentfunktioner för att testa sådana alternativ. När du väljer ett alternativ som kräver funktioner för kommunikations-API:er eller dokument med post utförs ingen åtgärd och ett felmeddelande visas.

## RDE, genomgång

Om du vill veta mer om RDE i AEM as a Cloud Service kan du titta i videosjälvstudiekursen som demonstrerar [hur du konfigurerar den, hur du använder den och utvecklingscykeln (01:25)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/overview.html).

# Felsökning {#troubleshooting}

## Felsökning av RDE (#rde-troubleshooting)

### Så här skaffar du den senaste AEM för en befintlig RDE {#get-latest-aem-version}

När de skapas ställs de lokala utvecklingsmiljöerna in på den senast tillgängliga Adobe Experience Manager-versionen (AEM). En [RDE-återställning](#reset-rde), som kan utföras med Cloud Manager eller kommandot `aio aem:rde:reset`, går igenom RDE-filen och anger den till den senast tillgängliga AEM.

## felsökning av plugin-program för aio RDE {#aio-rde-plugin-troubleshooting}

### Fel som rör otillräcklig behörighet {#insufficient-permissions}

Om du vill använda RDE-plugin-programmet måste du vara medlem i produktprofilen Cloud Manager **Developer - Cloud Service**. Mer information finns i [Tilldela teammedlemmar till Cloud Manager produktprofiler - Tilldela produktprofilen för utvecklare](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer).

Du kan också bekräfta att du har den här utvecklarrollen om du kan logga in på utvecklarkonsolen med det här kommandot:

`aio cloudmanager:environment:open-developer-console`

>[!TIP]
>
>Om felet `Warning: cloudmanager:* is not a aio command.` visas måste du installera [ aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager) genom att köra kommandot nedan:
>
>```
>aio plugins:install @adobe/aio-cli-plugin-cloudmanager
>```

Verifiera att inloggningen slutfördes genom att köra

`aio cloudmanager:list-programs`

Detta bör visa alla program i den konfigurerade organisationen och bekräfta att du har tilldelats rätt roll.

### Använda det inaktuella sammanhanget&quot;aio-cli-plugin-cloudmanager&quot; {#aio-rde-plugin-troubleshooting-deprecatedcontext}

På grund av historiken för&quot;aio-cli-plugin-aem-rde&quot; användes kontextnamnet&quot;aio-cli-plugin-cloudManager&quot; en tid. Rde-pluginen använder nu IMS-sättet att hantera kontextinformation, vilket innebär att det finns alternativ för att lagra kontextinformation globalt eller lokalt, samt att alla aio-anrop standardkonfigureras om så önskas. Den konfigurerade standardkontexten lagras lokalt och gör att utvecklarna kan spåra och använda enskilda kontexter och deras information i en mapp. Mer information finns i [exemplet för att konfigurera en lokal kontext](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools) ovan.

Utvecklare som använder båda plugin-programmen, aio-cli-plugin-cloudmanager och aio-cli-plugin-aem-rde och vill behålla all information i samma sammanhang måste nu ha följande alternativ:

#### Fortsätt använda kontexten&quot;aio-cli-plugin-cloudmanager&quot;

Kontexten kan fortfarande användas. En varning om borttagning visas i plugin-programmet för RDE. Den här varningen kan utelämnas i läget ```--quiet```. De nyare versionerna av RDE-pluginen ger inte längre möjlighet att läsa kontexten&quot;aio-cli-plugin-cloudmanager&quot;. Om du fortfarande vill använda den konfigurerar du standardkontexten till &quot;aio-cli-plugin-cloudManager&quot;. Mer information finns i [exemplet för att konfigurera en lokal kontext](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools) ovan.

#### Använd valfritt annat kontextnamn även för plugin-programmet för molnhantering

Molnhanterarens plugin-program erbjuder en parameter för att definiera en kontext som ska användas. Den stöder inte IMS-standardkontextkonfigurationen ännu. Om du vill göra det konfigurerar du RDE-plugin-programmet med [exemplet för att konfigurera en lokal kontext](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools) och anger för molnhanterarens plugin att använda myContext som ```--imsContextName=myContext``` i varje anrop till det.
