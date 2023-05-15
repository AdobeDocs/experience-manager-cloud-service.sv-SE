---
title: Snabba utvecklingsmiljöer
description: Lär dig hur du utnyttjar miljöer för snabb utveckling för snabb utveckling i en molnmiljö.
exl-id: 1e9824f2-d28a-46de-b7b3-9fe2789d9c68
source-git-commit: 0095cb1fff99a52f5a048833b3d5a65643c1056d
workflow-type: tm+mt
source-wordcount: '3325'
ht-degree: 0%

---

# Snabba utvecklingsmiljöer {#rapid-development-environments}

För att kunna driftsätta ändringar kräver de aktuella utvecklingsmiljöerna i molnet en process som använder omfattande regler för kodssäkerhet och -kvalitet som kallas CI/CD-pipeline. I situationer där snabba och iterativa förändringar behövs har Adobe infört snabba utvecklingsmiljöer (RDE) för kort tid.

Tack vare de lokala redigeringssystemen kan utvecklare snabbt driftsätta och granska ändringar, vilket minimerar den tid som krävs för att testa funktioner som är beprövade i en lokal utvecklingsmiljö.

När ändringarna har testats i en RDE kan de distribueras till en vanlig molnutvecklingsmiljö via Cloud Managers pipeline.

>[!VIDEO](https://video.tv.adobe.com/v/3415582/?quality=12&learn=on)


Du kan titta på ytterligare videofilmer som visar [konfigurera](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html), [hur man använder den](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html)och [utvecklingslivscykel](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/development-life-cycle.html) med RDE.

## Introduktion {#introduction}

RDE kan användas för konfigurationer av kod, innehåll och Apache eller Dispatcher. Till skillnad från vanliga Cloud Development-miljöer kan utvecklare använda lokala kommandoradsverktyg för att synkronisera kod som skapats lokalt till en RDE.

Alla program tillhandahålls med en RDE. När det gäller sandlådekonton kommer de att försättas i viloläge efter några timmars icke-användning.

När de skapas ställs de virtuella skrivborden in på den senast tillgängliga AEM. En RDE-återställning, som kan utföras med Cloud Manager, går igenom RDE-filen och ställer in den till den senast tillgängliga AEM.

Vanligtvis används en RDE av en enskild utvecklare vid en viss tidpunkt för att testa och felsöka en viss funktion. När utvecklingssessionen är klar kan den återställas till ett standardläge för nästa användning.

Ytterligare RDE kan licensieras för produktionsprogram (ej sandlådeprogram).

## Aktivera RDE i ett program {#enabling-rde-in-a-program}

Följ de här stegen för att använda Cloud Manager för att skapa en RDE för ditt program.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation.

1. Klicka på det program som du vill lägga till en RDE till för att visa information om det.

   * RDE kan läggas till i båda [sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) och [produktionsprogram.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)

1. Från **Programöversikt** sida, klicka på **Lägg till miljö** på **Miljö** för att lägga till en miljö.

   ![Miljökort](/help/implementing/cloud-manager/assets/no-environments.png)

   * The **Lägg till miljö** finns även på **Miljö** -fliken.

      ![Fliken Miljö](/help/implementing/cloud-manager/assets/environments-tab.png)

   * The **Lägg till miljö** kan vara inaktiverat på grund av bristande behörighet eller beroende på vilka licensierade resurser som används.

1. I **Lägg till miljö** som visas:

   * Välj **Snabb utveckling** under **Välj miljötyp** rubrik.
      * Antalet tillgängliga/använda miljöer visas inom parentes bakom miljötypen.
   * Ange en **Namn** för miljön.
   * Ange ett valfritt **Beskrivning** för miljön.
   * Välj en **Molnregion**.

   ![Dialogrutan Lägg till miljö](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. Klicka **Spara** för att lägga till den angivna miljön.

The **Översikt** visas nu din nya miljö i **Miljö** kort.

När de skapas ställs de virtuella skrivborden in på den senast tillgängliga AEM. En RDE-återställning, som även kan utföras med Cloud Manager, går igenom RDE-filen och ställer in den till den senast tillgängliga AEM.

Mer information om hur du använder Cloud Manager för att skapa miljöer, hantera vem som har åtkomst till dem och tilldela anpassade domäner finns i [Cloud Manager-dokumentationen.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## Installera kommandoradsverktygen för RDE {#installing-the-rde-command-line-tools}

När du har lagt till en RDE för ditt program med Cloud Manager kan du interagera med den genom att konfigurera kommandoradsverktygen enligt följande steg:

>[!IMPORTANT]
>
>Kontrollera att du har den senaste versionen av [Nod och NPM har installerats](https://nodejs.org/en/download/) för att Adobe I/O CLI och tillhörande plugin-program ska fungera korrekt.


1. Installera CLI-verktygen för Adobe I/O enligt proceduren [här](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).
1. Installera molnhanterarplugin-programmet för CLI-verktygen i Adobe I/O och konfigurera dem enligt beskrivningen [här](https://github.com/adobe/aio-cli-plugin-cloudmanager).
1. Installera Adobe I/O CLI-verktyg AEM RDE-plugin genom att köra följande kommandon:

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. Konfigurera plugin-programmet för molnhantering för ditt företags-ID:

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   och ersätta den alfanumeriska strängen med ditt eget organisations-ID, som kan slås upp med strategin [här](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

1. Konfigurera sedan ditt program-ID:

   `aio config:set cloudmanager_programid 12345`

1. Konfigurera sedan det miljö-ID som den virtuella miljön ska kopplas till:

   `aio config:set cloudmanager_environmentid 123456`

1. När du är klar med konfigurationen av plugin-programmet loggar du in genom att utföra

   `aio login`

   Svaret på en lyckad inloggning ska likna utdata nedan, men du kan ignorera värdena som visas.

   ```
   ...
   You are currently in:
   1. Org: <no org selected>
   2. Project: <no project selected>
   3. Workspace: <no workspace selected>
   ```

1. Verifiera att inloggningen slutfördes genom att köra

   `aio cloudmanager:list-programs`

   Detta bör visa alla program i din konfigurerade organisation.

   Observera att ovanstående kräver att du är medlem i Cloud Manager **Utvecklare - Cloud Service** Produktprofil. Se [den här sidan](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer) för mer information.

   Du kan också bekräfta att du har den här utvecklarrollen om du kan logga in på utvecklarkonsolen med det här kommandot:

   `aio cloudmanager:environment:open-developer-console`

   >[!TIP]
   >
   >Om du ser `Warning: cloudmanager:list-programs is not a aio command.` måste du installera [aio-cli-plugin-cloud-manager](https://github.com/adobe/aio-cli-plugin-cloudmanager) genom att köra kommandot nedan:
   >
   >
   ```
   >aio plugins:install @adobe/aio-cli-plugin-cloudmanager
   >```

Mer information och demonstrationer finns i [konfigurera en RDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html) videosjälvstudiekurs.

## Använda RDE under utvecklingen av en ny funktion {#using-rde-while-developing-a-new-feature}

Adobe rekommenderar följande arbetsflöde för att utveckla en ny funktion:

* När en mellanliggande milstolpe har nåtts och validerats lokalt med den AEM as a Cloud Service SDK:n, bör koden implementeras på en Git-funktionsgren som ännu inte är en del av huvudraden, även om det är valfritt att binda sig för Git. Vad som utgör en&quot;mellanmilstolpe&quot; varierar beroende på teamets vanor. Exempel är några nya kodrader, en halv arbetsdag eller en underfunktion.

* Återställ RDE om den har använts av en annan funktion och du vill [återställa till standardläge](#reset-rde). <!-- Alexandru: hiding for now, please don't delete This can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). -->Återställningen tar några minuter och allt befintligt innehåll och all befintlig kod tas bort. Du kan använda kommandot för RDE-status för att bekräfta att RDE är klart. Den nya versionen av AEM kommer att användas.

   >[!IMPORTANT]
   >
   > Om din testnings- och produktionsmiljö inte får automatiska AEM och ligger långt efter den senaste versionen av AEM bör du tänka på att koden som körs på den lokala utvecklingsmiljön kanske inte stämmer överens med hur koden fungerar i testversionerna och produktionen. I så fall är det särskilt viktigt att utföra grundliga tester av koden på mellanlagring innan den distribueras till produktion.


* Synkronisera lokal kod med RDE-kommandoradsgränssnittet. Du kan installera ett innehållspaket, ett specifikt paket, en OSGI-konfigurationsfil, en innehållsfil och en zip-fil för en Apache/Dispatcher-konfiguration. Det går också att referera till ett fjärrinnehållspaket. Se [Verktyg för RDE-kommandorad](#rde-cli-commands) för mer information. Du kan använda statuskommandot för att validera att distributionen lyckades. Du kan också använda Package Manager för att installera innehållspaket.

* Testa koden i RDE. URL:er för författare och publicering är tillgängliga i Cloud Manager.

* Om koden inte beter sig som förväntat kan du använda standardfelsökningstekniker för att förstå problemet och göra lämpliga ändringar. Utan att implementera kodändringarna i Git (eftersom de inte har validerats) kan du synkronisera koden med den lokala CLI:n. Fortsätt tills problemet är löst.

* När koden beter sig som förväntat implementerar du koden i Git-funktionsgrenen.

* Kod som synkroniseras till RDE använder inte en molnhanterarpipeline, så nu bör du använda en icke-produktionsprocess i Cloud Manager för att distribuera Git-funktionsgrenen till molnutvecklingsmiljön. Detta validerar att koden klarar Cloud Managers kvalitetsportar och gör att du kan vara säker på att koden senare distribueras med hjälp av Cloud Managers produktionsflöde.

* Upprepa stegen ovan för varje mellanliggande milstolpe tills all kod för funktionen är klar och fungerar bra i både RDE- och Cloud Development-miljön.

* Distribuera koden till produktionen via Cloud Managers produktionsflöde.

## Använda RDE för att felsöka en befintlig funktion {#use-rde-to-debug-an-existing-feature}

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

### Distribuera till RDE {#deploying-to-rde}

I det här avsnittet beskrivs hur du använder RDE CLI för att distribuera, installera eller uppdatera paket, OSGI-konfigurationer, innehållspaket, enskilda innehållsfiler och Apache- eller Dispatcher-konfigurationer.

Det allmänna användningsmönstret är `aio aem:rde:install <artifact>`.

Här följer några exempel:

<u>Distribuera ett innehållspaket</u>

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

Svaret för en lyckad distribution liknar följande:

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

Du kan även referera till en fjärrdatabas:

`aio aem:rde:install -t content-package "https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip"`

Som standard distribueras artefakter till både författar- och publiceringsnivåer, men flaggan&quot;-s&quot; kan användas för att ange ett specifikt skikt som mål.

Alla AEM kan distribueras, till exempel paket med kod, innehåll eller en [behållarpaket](/help/implementing/developing/introduction/aem-project-content-package-structure.md#container-packages) (kallas även&quot;all&quot;-paketet).

>[!IMPORTANT]
>
>Dispatcher-konfigurationen för WKND-projektet distribueras inte via installationen av innehållspaketet ovan. Du måste distribuera den separat enligt stegen&quot;Distribuera en Apache/Dispatcher-konfiguration&quot;.

<u>Distribuera en OSGI-konfiguration</u>

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

där svaret för en lyckad distribution liknar följande:

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

<u>Distribuera ett paket</u>

Använd följande för att distribuera ett paket:

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

där svaret för en lyckad distribution liknar följande:

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

<u>Distribuera en innehållsfil</u>

Använd följande för att distribuera en innehållsfil:

`aio aem:rde:install world.txt -p /apps/hello.txt`

där svaret för en lyckad distribution liknar följande:

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

<u>Distribuera en Apache/Dispatcher-konfiguration</u>

Hela mappstrukturen måste vara i form av en ZIP-fil för den här typen av konfiguration.

Från `dispatcher` i ett AEM projekt kan du zippa upp dispatcherkonfigurationen genom att köra kommandot nedan maven:

`mvn clean package`

eller använda zip-kommandot nedan från `src` katalogen `dispatcher` modul:

`zip -y -r dispatcher.zip .`

distribuera sedan konfigurationen med det här kommandot:

`aio aem:rde:install target/aem-guides-wknd.dispatcher.cloud-X.X.X-SNAPSHOT.zip`

>[!TIP]
>
>Kommandot ovan förutsätter att du distribuerar [WKND](https://github.com/adobe/aem-guides-wknd) projektets dispatcherkonfigurationer. Se till att ersätta `X.X.X` med motsvarande WKND-projektversionsnummer eller projektspecifikt versionsnummer när du distribuerar projektets dispatcherkonfiguration.

>[!NOTE]
>
>RDE har stöd för dispatcherkonfigurationen för&quot;flexibelt läge&quot;, men inte för dispatcherkonfigurationen för&quot;äldre läge&quot;. Se [dokumentation för avsändare](/help/implementing/dispatcher/disp-overview.md#validation-debug) om du vill ha information om de två lägena. Du kan även läsa dokumentationen om [migrera till flexibelt läge](/help/implementing/dispatcher/validation-debug.md#migrating), om du inte redan har gjort det.

En lyckad distribution genererar ett svar som liknar följande:

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

Kod som distribueras till RDE genomgår inte någon Cloud Manager-pipeline och tillhörande kvalitetsgates, men koden går igenom en analys som rapporterar felen, vilket visas i kodexemplet nedan:

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

Kodexemplet ovan visar hur ett paket fungerar om det inte går att lösa. I så fall&quot;staged&quot; och installeras bara om kraven (import saknas, i detta fall) uppfylls genom installation av annan kod.

### Kontrollera statusen för den lokala lagringsplatsen {#checking-rde-status}

Du kan använda RDE CLI för att kontrollera om miljön är klar att distribueras till, som vilka distributioner som har gjorts via RDE-pluginen.

Körs:

`aio aem:rde:status`

kommer att returnera:

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

Om kommandot returnerar en anteckning om instansinstallationer kan du fortsätta och utföra nästa uppdatering, men den senaste uppdateringen kanske inte visas på instansen än.

### Visa distributionshistorik {#show-deployment-history}

Du kan kontrollera historiken för distributioner som gjorts till RDE genom att köra:

`aio aem:rde:history`

som returnerar ett svar i form av

`#1: deploy completed for content-package aem-guides-wknd.all-2.1.0.zip on author,publish - done by 029039A55D4DE16A0A494025@AdobeID at 2022-09-12T14:41:55.393Z`

### Tar bort från RDE {#deleting-from-rde}

Du kan ta bort konfigurationer och paket som tidigare har distribuerats till RDE via CLI-verktygen. Använd `status` om du vill visa en lista över vad som kan tas bort, som innehåller `bsn` för paket och `pid` för konfigurationer att referera till i kommandot delete.

Om `com.adobe.granite.demo.MyServlet.cfg.json` har installerats, `bsn` är bara `com.adobe.granite.demo.MyServlet`, utan **cfg.json** suffix.

Det går inte att ta bort innehållspaket eller innehållsfiler. Om du vill ta bort dem bör du återställa den skrivskyddade miljön så att den återställs till standardläge.

Se exemplet nedan för mer information:

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

Mer information och demonstrationer finns i [använda RDE-kommandon](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html) videosjälvstudiekurs.

## Återställ {#reset-rde}

Om du återställer RDE tas all anpassad kod, konfigurationer och innehåll bort från både författaren och publiceringsinstansen. Detta kan vara användbart om RDE har använts för att testa en viss funktion och du vill återställa den till ett standardläge för att testa en annan funktion.

En återställning anger att den senaste tillgängliga AEM är RDE.

<!-- Alexandru: hiding for now, please don't delete

Resetting can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). Resetting takes a few minutes and all existing content and code will be deleted from the RDE.

>[NOTE!]
>
>You must be assigned the Cloud Manager Developer role in order to be able to use the reset feature. If not, a reset action will result in an error.

### Reset the RDE via Command Line {#reset-the-rde-command-line}

You can reset the RDE and return it to a default state by running:

`aio aem:rde:reset`

This usually takes a few minutes. Use the [status command](#checking-rde-status) to check when the environment is ready again.

### Reset the RDE in Cloud Manager {#reset-the-rde-cloud-manager} -->

Du kan använda Cloud Manager för att återställa din RDE genom att följa stegen nedan:

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation.

1. Klicka på det program för vilket du vill återställa RDE.

1. Från **Översikt** klickar du på **Miljö** överst på skärmen.

   ![Fliken Miljö](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * Du kan även klicka på **Visa alla** på **Miljö** för att gå direkt till **Miljö** -fliken.

      ![Visa alla, alternativ](/help/implementing/cloud-manager/assets/environment-showall.png)

1. The **Miljö** öppnas och alla miljöer för programmet visas.

   ![Fliken Miljöer](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. Klicka på ellipsknappen för den RDE som du vill återställa och välj sedan **Återställ**.

   ![Visa miljöinformation](/help/implementing/cloud-manager/assets/rde-reset.png)

1. Bekräfta att du vill återställa RDE genom att klicka på **Återställ** i dialogrutan.

   ![Bekräfta återställning](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. Cloud Manager bekräftar via ett banderollmeddelande att återställningsprocessen har startats.

   ![Återställ banderollmeddelande](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

När återställningsprocessen för RDE har startats tar det oftast några minuter att slutföra och återställa miljön till standardläget. Återställningsprocessens status kan visas när som helst i **Status** kolumn i **Miljö** eller i **Miljö** -fönstret.

![Återställningsstatus för RDE](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

Du kan också återställa den lokala redigeringsmiljön med hjälp av ellipsknappen direkt från **Miljö** på **Översikt** sida.

![Återställ RDE från miljökort](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

Mer information om hur du använder Cloud Manager för att hantera dina miljöer finns i [Cloud Manager-dokumentationen.](/help/implementing/cloud-manager/manage-environments.md)

## Körningslägen {#runmodes}

RDE-specifik OSGI-konfiguration kan användas med suffix i mappnamnet, som i exemplen nedan:

* `config.rde`
* `config.author.rde`
* `config.publish.rde`

Se [dokumentation för runmode](/help/implementing/deploying/overview.md#runmodes) för allmän information om körningslägen.

>[!NOTE]
>
>RDE OSGI-konfigurationen är unik eftersom den ärver värdena för alla OSGI-egenskaper som deklarerats av paketets `dev` körningsläge.

RDE skiljer sig från andra miljöer där innehåll kan installeras i en install.rde-mapp (eller install.author.rde eller install.publish.rde) under /apps. På så sätt kan du implementera innehåll för att Git och leverera det till RDE med kommandoradsverktygen.

## Fylla med innehåll {#populating-content}

När en RDE återställs tas allt innehåll bort, och om så önskas måste en explicit åtgärd vidtas för att lägga till innehåll. Ett tips är att du bör överväga att sätta ihop en uppsättning innehåll som ska användas som testinnehåll för validering och felsökning i den lokala redigeringsmiljön. Det finns flera möjliga strategier för att fylla i den regionala utvecklingsmiljön med det innehållet:

1. Synkronisera innehållspaketet explicit till RDE med kommandoradsverktygen

1. Placera och implementera exempelinnehållet i Git i en install.rde-mapp under /apps och synka sedan det övergripande innehållspaketet till RDE med kommandoradsverktygen.

1. Använd [innehållskopia, verktyg](/help/implementing/developing/tools/content-copy.md) om du vill kopiera en definierad innehållsuppsättning från produkter, scener eller dev-miljöer, eller från en annan RDE.

1. Använd pakethanteraren

Observera att du är begränsad till 1 GB när du synkroniserar innehållspaket.

## Loggning {#logging}

Loggnivåer kan ställas in genom att ändra OSGi-konfigurationer. Kontrollera [dokumentation](/help/implementing/developing/introduction/logging.md) för mer information.

## Hur skiljer sig de lokala utvecklingsmiljöerna från utvecklingsmiljöer i molnet? {#how-are-rds-different-from-cloud-development-environments}

Även om RDE på många sätt liknar en utvecklingsmiljö i molnet finns det vissa mindre arkitektoniska skillnader som gör det möjligt att snabbt synkronisera kod. Mekanismen för att hämta kod till RDE skiljer sig åt - för RDE synkroniseras en kod från en lokal utvecklingsmiljö, medan en för Cloud Development Environment distribuerar kod via Cloud Manager.

Därför rekommenderar vi att du distribuerar koden till en Cloud Development Environment via icke-produktionsflödet när du har validerat koden i en RDE-miljö. Testa slutligen koden innan du distribuerar med produktionsflödet.

Observera även följande:

* De lokala redigeringssystemen innehåller inte någon förhandsgranskningsnivå
* De lokala lagringsenheterna har för närvarande inte stöd för visning och felsökning av frontkod som distribuerats med molnhanteraren Front-End Pipeline.
* De lokala redigeringssystemen stöder för närvarande inte prerelease-kanalen.


## Hur många skrivbord behöver jag? {#how-many-rds-do-i-need}

Det finns en RDE för varje licensierad lösning och Adobe erbjuder även ytterligare RDE som kan licensieras för Production-program (ej sandlådeprogram).

Hur många skrivbord som behövs beror på en organisations sammansättning och processer. Den mest flexibla modellen är när en organisation köper en dedikerad RDE för var och en av sina AEM Cloud Service-utvecklare. I den här modellen kan varje utvecklare testa sin kod på den lokala utvecklingsmiljön utan att samordna med andra gruppmedlemmar kring om det finns en tillgänglig RDE-miljö.

Å andra sidan kan ett team med en enda RDE använda interna processer för att samordna vilken utvecklare som kan använda miljön vid en viss tidpunkt. Detta kan vara möjligt när en utvecklare har nått en milstolpe för mellanliggande funktioner och är redo att validera i en molnmiljö där de snabbt kan göra de ändringar de behöver.

En mellanliggande modell är en modell där en organisation köper ett antal olika lagringssystem, vilket innebär att det är större sannolikhet att det finns en oanvänd lagringsmodell tillgänglig. En strategi kan vara att tilldela en RDE per team eller större funktion. Interna processer kan användas för att samordna användningen av miljöerna.

## Hur skiljer sig en AEM Forms Cloud Service Rapid Development Environment (RDE) från andra miljöer? {#how-are-forms-rds-different-from-cloud-development-environments}

Forms-utvecklare kan använda AEM Forms Cloud Service Rapid Development Environment för att snabbt utveckla adaptiva Forms, arbetsflöden och anpassningar som att anpassa kärnkomponenter, integreringar med tredjepartssystem med mera. AEM Forms Cloud Service Rapid Development Environment (RDE) saknar stöd för kommunikations-API:er och för funktioner som kräver ett dokument för registrering, som att generera ett dokument för registrering när ett adaptivt formulär skickas. Följande AEM Forms-funktioner är inte tillgängliga i en Rapid Development Environment (RDE):

* Konfigurera ett postdokument för ett adaptivt formulär
* Generera ett registreringsdokument när ett adaptivt formulär skickas eller när ett arbetsflödessteg tas
* Skicka postdokument som en bifogad fil med åtgärden Skicka via e-post eller med steget E-post i ett arbetsflöde
* Använda Adobe Sign i ett adaptivt formulär eller i ett arbetsflödessteg
* Kommunikations-API:er

>[!NOTE]
>
> Det är ingen skillnad på användargränssnittet i Rapid Development Environment (RDE) och andra Cloud Service för Forms. Alla alternativ som är relaterade till Dokumentformat, som att välja ett dokument med en postmall för ett anpassat formulär, fortsätter att visas i användargränssnittet. De här miljöerna har inga kommunikations-API:er och dokumentfunktioner för att testa sådana alternativ. När du väljer ett alternativ som kräver funktioner för kommunikations-API:er eller dokument med post utförs ingen åtgärd och ett felmeddelande visas eller returneras.

## RDE, genomgång

Om du vill veta mer om RDE på AEM as a Cloud Service kan du läsa [videosjälvstudiekurs som visar hur du konfigurerar den, hur du använder den och utvecklingscykeln](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/overview.html)
