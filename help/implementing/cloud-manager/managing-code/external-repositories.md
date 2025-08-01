---
title: Lägg till externa databaser i Cloud Manager
description: Lär dig hur du lägger till en extern databas i Cloud Manager. Cloud Manager stöder integrering med GitHub Enterprise-, GitLab-, Bitbucket- och Azure DevOps-databaser.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="Privat beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
exl-id: aebda813-2eb0-4c67-8353-6f8c7c72656c
source-git-commit: b4bbf73cd49f6d7beb47d2edce0910d957879e39
workflow-type: tm+mt
source-wordcount: '2322'
ht-degree: 0%

---

# Lägga till externa databaser i Cloud Manager {#external-repositories}

Lär dig hur du lägger till en extern databas i Cloud Manager. Cloud Manager stöder integrering med GitHub Enterprise-, GitLab- och Bitbucket-databaser.

Kunderna kan nu även införliva sina Azure DevOps Git-databaser i Cloud Manager, med stöd för både moderna Azure DevOps-databaser och äldre VSTS-databaser (Visual Studio Team Services).

* För Edge Delivery Services-användare kan den inbyggda databasen användas för att synkronisera och distribuera platskod.
* För AEM as a Cloud Service- och Adobe Managed Services-användare (AMS) kan databasen länkas till både fullständiga och frontbaserade pipelines.

>[!NOTE]
>
>De funktioner som beskrivs i den här artikeln är endast tillgängliga via det privata betaprogrammet. Mer information och om du vill registrera dig för den privata betaversionen finns i [Hämta din egen Git](/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket).


## Konfigurera en extern databas

Konfigurationen av en extern databas i Cloud Manager består av följande steg:

1. [Lägg till en extern databas](#add-external-repo) till ett valt program
1. [Länka en validerad extern databas till en pipeline](#validate-ext-repo)
   <!-- 1. Provide an access token to the external repository.
    1. Validate ownership of the private GitHub repository. -->
1. [Konfigurera en webkrok](#configure-webhook) till en extern databas.


## Lägga till en extern databas {#add-ext-repo}

>[!NOTE]
>
>Externa databaser kan inte länkas till konfigurationspipelines.

<!-- THIS BULLET REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2024.12.0+Release. THEY CAN NOW START AUTOMATICALLY>
* Pipelines using external repositories (excluding GitHub-hosted repositories) and the **Deployment Trigger** option [!UICONTROL **On Git Changes**], triggers are not automatically started. They must be manually started. -->


1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** väljer du det program som du vill länka till en extern databas.

1. Klicka på ![Mappdispositionsikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **Databaser** på sidomenyn under **Program**.

   ![Sidan Databaser](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. Klicka på **Lägg till databas** i det övre högra hörnet på sidan **Databaser**.

1. I dialogrutan **Lägg till databas** väljer du **Privat databas** för att länka en extern Git-databas till ditt program.

   ![Lägg till egen databas](/help/implementing/cloud-manager/managing-code/assets/repositories-private-repo-type.png)

1. Ange följande information om din databas i varje fält:

   | Fält | Beskrivning |
   | --- | --- |
   | **Databasnamn** | Obligatoriskt. Ett uttrycksfullt namn för din nya databas. |
   | **Databas-URL** | Obligatoriskt. Databasens URL.<br><br>Om du använder en GitHub-värdbaserad databas måste sökvägen sluta i `.git`.<br>Till exempel *`https://github.com/org-name/repo-name.git`* (URL-sökvägen är endast avsedd som illustration).<br><br>Om du använder en extern databas måste den använda följande URL-sökvägsformat:<br>`https://git-vendor-name.com/org-name/repo-name.git`<br> eller<br>`https://self-hosted-domain/org-name/repo-name.git`<br>Och matcha Git-leverantören. |
   | **Välj databastyp** | Obligatoriskt. Välj den databastyp som du använder. Om databasens URL-sökväg innehåller Git-leverantörens namn, till exempel GitLab eller Bitbucket, är databastypen redan förvald.:<ul><li>**GitHub** (GitHub Enterprise och den självhanterade versionen av GitHub)</li><li>**GitLab** (både `gitlab.com` och den självhanterade versionen av GitLab) </li><li>**Bitbucket** (endast `bitbucket.org` - molnversion) stöds. Den självhanterade versionen av Bitbucket är borttagen från och med den 15 februari 2024.)</li><li>**Azure DevOps** (`dev.azure.com`) </ul> |
   | **Beskrivning** | Valfritt. En detaljerad beskrivning av databasen. |

1. Välj **Spara** för att lägga till databasen.

   Ange nu en åtkomsttoken för att validera ägarskapet för den externa databasen.

1. I dialogrutan **Verifiering av privat databasägande** anger du en åtkomsttoken för att validera ägarskapet för den externa databasen så att du kan komma åt den. Klicka sedan på **Verifiering**.

   ![Välja en befintlig åtkomsttoken för en databas](/help/implementing/cloud-manager/managing-code/assets/repositories-exisiting-access-token.png)
   *Välja en befintlig åtkomsttoken för en Bitbucket-databas (endast illustration).*

>[!BEGINTABS]

>[!TAB GitHub Enterprise]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/github -->

| Alternativ för åtkomsttoken | Beskrivning |
| --- | --- |
| **Använd befintlig åtkomsttoken** | Om du redan har angett en åtkomsttoken för databasen för din organisation och har tillgång till flera databaser kan du välja en befintlig token. Använd listrutan **Tokennamn** för att välja den token som du vill använda för databasen. I annat fall lägger du till en ny åtkomsttoken. |
| **Lägg till ny åtkomsttoken** | <ul><li> Skriv ett namn på åtkomsttoken som du skapar i textfältet **Token Name**.<li>Skapa en personlig åtkomsttoken genom att följa instruktionerna i [GitHub-dokumentationen](https://docs.github.com/en/enterprise-server@3.14/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).<li>Behörigheter som krävs för GitHub Enterprise Personal Access Token (PAT)<br>Dessa behörigheter säkerställer att Cloud Manager kan validera pull-begäranden, hantera implementeringsstatuskontroller och få tillgång till nödvändig repo-information.<br>När du genererar PAT i GitHub Enterprise måste du se till att det innehåller följande databasbehörigheter:<ul><li>Pull-begäran (läs och skriv)<li>Bekräfta status (läs och skriv)<li>Databasmetadata (skrivskyddade)</li></li></ul></li></ul></ul></ul><ul><li>Klistra in den token du just skapade i fältet **Åtkomsttoken**. |

Efter valideringen är den externa databasen klar att användas och länkas till en pipeline.

Se även [Hantera åtkomsttoken](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

>[!TAB GitLab]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/gitlab -->

| Alternativ för åtkomsttoken | Beskrivning |
| --- | --- |
| **Använd befintlig åtkomsttoken** | Om du redan har angett en åtkomsttoken för databasen för din organisation och har tillgång till flera databaser kan du välja en befintlig token. Använd listrutan **Tokennamn** för att välja den token som du vill använda för databasen. I annat fall lägger du till en ny åtkomsttoken. |
| **Lägg till ny åtkomsttoken** | <ul><li>Skriv ett namn på åtkomsttoken som du skapar i textfältet **Token Name**.<li>Skapa en personlig åtkomsttoken genom att följa instruktionerna i [GitLab-dokumentationen](https://docs.gitlab.com/user/profile/personal_access_tokens/).<li>Behörigheter som krävs för GitLab Personal Access Token (PAT)<br>Dessa scope ger Cloud Manager åtkomst till databasdata och användarinformation som behövs för validering och webkrok-integrering.<br>När du genererar PAT i GitLab ska du kontrollera att det innehåller följande tokenomfång:<ul><li>api<li>read_user</li></li></ul></li></li></ul></ul></ul><ul><li>Klistra in den token du just skapade i fältet **Åtkomsttoken**. |

Efter valideringen är den externa databasen klar att användas och länkas till en pipeline.

Se även [Hantera åtkomsttoken](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

>[!TAB Bitbucket]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/bitbucket -->

| Alternativ för åtkomsttoken | Beskrivning |
| --- | --- |
| **Använd befintlig åtkomsttoken** | Om du redan har angett en åtkomsttoken för databasen för din organisation och har tillgång till flera databaser kan du välja en befintlig token. Använd listrutan **Tokennamn** för att välja den token som du vill använda för databasen. I annat fall lägger du till en ny åtkomsttoken. |
| **Lägg till ny åtkomsttoken** | <ul><li>Skriv ett namn på åtkomsttoken som du skapar i textfältet **Token Name**.<li>Skapa en databasåtkomsttoken med hjälp av [Bitbucket-dokumentationen](https://support.atlassian.com/bitbucket-cloud/docs/create-a-repository-access-token/).<li>Behörigheter som krävs för Bitbucket Personal Access Token (PAT)<br>Dessa behörigheter ger Cloud Manager åtkomst till databasinnehåll, hanterar pull-begäranden och konfigurerar eller reagerar på webboks-händelser.<br>När du skapar applösenordet i Bitbucket måste det innehålla följande lösenordsbehörigheter:<ul><li>Databas (skrivskyddad)<li>Hämta begäranden (läsa och skriva)<li>Webhooks (läs och skriv)</li></li></ul></li></li></ul></ul></ul><ul><li>Klistra in den token du just skapade i fältet **Åtkomsttoken**. |

Efter valideringen är den externa databasen klar att användas och länkas till en pipeline.

Se även [Hantera åtkomsttoken](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

>[!TAB Azure DevOps]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/azure_devops -->

| Alternativ för åtkomsttoken | Beskrivning |
| --- | --- |
| **Använd befintlig åtkomsttoken** | Om du redan har angett en åtkomsttoken för databasen för din organisation och har tillgång till flera databaser kan du välja en befintlig token. Använd listrutan **Tokennamn** för att välja den token som du vill använda för databasen. I annat fall lägger du till en ny åtkomsttoken. |
| **Lägg till ny åtkomsttoken** | <ul><li>Skriv ett namn på åtkomsttoken som du skapar i textfältet **Token Name**.<li>Skapa en databasåtkomsttoken med hjälp av [Azure DevOps-dokumentationen](https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops&tabs=Windows).<li>Nödvändig behörighet för Azure DevOps Personal Access Token (PAT).<br>Dessa behörigheter ger Cloud Manager åtkomst till databasinnehåll, hanterar pull-begäranden och konfigurerar eller reagerar på webkrockshändelser.<br>När du skapar applösenordet i Azure DevOps måste det innehålla följande lösenordsbehörigheter för appen:<ul><li>Databas (skrivskyddad)</li></ul></li></li></ul></ul></ul><ul><li>Klistra in den token du just skapade i fältet **Åtkomsttoken**. |

Efter valideringen är den externa databasen klar att användas och länkas till en pipeline.

Se även [Hantera åtkomsttoken](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

>[!ENDTABS]


## Länka en validerad extern databas till en pipeline {#validate-ext-repo}

1. Lägga till eller redigera en pipeline:
   * [Lägg till en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [Lägg till en icke-produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
   * [Redigera en pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#editing-pipelines)

   <!-- Add an Edge Delivery Pipeline -->

   ![Källkodskatalogen för pipeline och Git-grenen](/help/implementing/cloud-manager/managing-code/assets/pipeline-repo-gitbranch.png)
   *Lägg till icke-produktionsförlopp, dialogruta med vald databas och Git-förgrening,*

1. När du lägger till eller redigerar en pipeline och vill ange platsen **Source-kod** för den nya eller befintliga pipelinen, väljer du den externa databas du vill använda i listrutan **Databas** .

1. I listrutan **Git Branch** väljer du grenen som källa för pipelinen.

1. Klicka på **Spara**.


>[!TIP]
>
>Mer information om hur du hanterar databaser i Cloud Manager finns i [Cloud Manager-databaser](/help/implementing/cloud-manager/managing-code/managing-repositories.md).


## Konfigurera en webkrok för en extern databas {#configure-webhook}

Med Cloud Manager kan du konfigurera webbhooks för externa Git-databaser som du har lagt till. Se [Lägg till en extern databas](#add-ext-repo). Dessa webhooks gör det möjligt för Cloud Manager att ta emot händelser som är relaterade till olika åtgärder inom Git-leverantörslösningen.

Med webbhooks kan Cloud Manager till exempel utlösa åtgärder som baseras på händelser som följande:

* Skapa pull-begäran (PR) - initierar PR-valideringsfunktioner.
* Push-händelser - Startar pipelines när utlösaren &quot;Vid Git-implementering&quot; är aktiverad (aktiverad).
* Kommentarsbaserade åtgärder - Möjliggör arbetsflöden, t.ex. direktdistribution från en PR, till en Rapid Development Environment (RDE).

Webkrok-konfiguration krävs inte för databaser på `GitHub.com` eftersom Cloud Manager integreras direkt via GitHub-appen.

Webkrokkonfigurationen är tillgänglig för alla andra externa databaser som är inbyggda med en åtkomsttoken - som GitHub Enterprise, GitLab, Bitbucket och Azure DevOps - och måste konfigureras manuellt.

**Så här konfigurerar du en webkrok för en extern databas:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** väljer du det program som du vill konfigurera en webkrok för en extern Git-databas.

1. Klicka på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i det övre vänstra hörnet på sidan för att visa den vänstra menyn.

1. Klicka på ![Mappdispositionsikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **Databaser** under rubriken **Program** på den vänstra menyn.

1. På sidan **Databaser** använder du kolumnen **Typ** för att vägleda dig i ditt val, letar upp den databas du vill använda och klickar sedan på ikonen ![Ellips - Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) bredvid den.

   ![Alternativet Konfigurera webkrok på nedrullningsbar meny för en vald databas](/help/implementing/cloud-manager/managing-code/assets/repository-config-webhook.png)

1. Klicka på **Konfigurera webkrok** i listrutan.

   ![Konfigurera dialogrutan Webkrok](/help/implementing/cloud-manager/managing-code/assets/config-webhook.png)

1. Gör följande i dialogrutan **Konfigurera webkrok**:

   1. Klicka på ikonen ![Kopiera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) bredvid fältet **Webkroks-URL**.
Klistra in URL:en i en vanlig textfil. Den kopierade URL:en krävs för din Git-leverantörs webkrok-inställningar.
   1. Klicka på **Generera** bredvid fältet **Webkrockhemlighet** och sedan på ![Kopiera-ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg).
Klistra in hemligheten i en vanlig textfil. Den kopierade hemligheten krävs för din Git-leverantörs webkrok-inställningar.
1. Klicka på **Stäng**.
1. Navigera till din Git-leverantörslösning (GitHub Enterprise, GitLab, Bitbucket eller Azure DevOps).

   All information om webbkrokkonfigurationen och de händelser som krävs för varje leverantör finns i [Lägg till en extern databas](#add-ext-repo). Under steg 8, se tabellen med flikar.

1. Leta upp lösningsavsnittet **Webkrok** Settings.
1. Klistra in webkroks-URL:en som du kopierade tidigare i URL-textfältet.
   1. Ersätt frågeparametern `api_key` i webkrok-URL:en med din egen riktiga API-nyckel.

      Om du vill generera en API-nyckel måste du skapa ett integreringsprojekt i Adobe Developer Console. Mer information finns i [Skapa ett API-integreringsprojekt](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/).

1. Klistra in webbkrokhemligheten som du kopierade tidigare i textfältet **Hemlig** (eller **Hemlig nyckel** eller **Hemlig token**).
1. Konfigurera webbokroken för att skicka de händelser som Cloud Manager kräver. Använd följande tabell för att fastställa rätt händelser för Git-leverantören.

>[!BEGINTABS]

>[!TAB GitHub Enterprise]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/github -->

| Nödvändiga webbkrokhändelser |
| --- |
| Dessa händelser gör att Cloud Manager kan svara på GitHub-aktivitet, som pull-begäran-validering, push-baserade utlösare för pipelines eller Edge Delivery Services-kodsynkronisering.<br>Kontrollera att webbkroken är konfigurerad för att aktiveras för följande obligatoriska webkrockshändelser:<ul><li>Dra in begäranden<li>Penslar<li>Skicka kommentarer</li></li></li></ul></ul></ul> |

>[!TAB GitLab]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/gitlab -->

| Nödvändiga webbkrokhändelser |
| --- |
| Dessa webkrofshändelser gör att Cloud Manager kan utlösa rörledningar när kod skickas eller när en sammanfogningsbegäran skickas. De spårar även kommentarer som rör validering av pull-begäran (via anteckningshändelser).<br>Kontrollera att webbkroken är konfigurerad för att aktiveras för följande obligatoriska webkrokrok-händelser<ul><li>Push-händelser<li>Sammanfoga begäranhändelser<li>Anteckningshändelser</li></li></li></ul></ul></ul> |

>[!TAB Bitbucket]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/bitbucket -->

| Nödvändiga webbkrokhändelser |
| --- |
| Dessa händelser säkerställer att Cloud Manager kan validera pull-begäranden, svara på exekveringar och interagera med kommentarer för samordning av pipeline.<br>Kontrollera att webbkroken är konfigurerad för att aktiveras för följande obligatoriska webkrokrok-händelser<ul><li>Dragningsbegäran: Skapad<li>Pull-begäran: Uppdaterad<li>Dragningsbegäranden: Sammanfogade<li>Pull-begäran: Kommentar<li>Databas: Tryck</li></li></li></ul></ul></ul> |

>[!TAB Azure DevOps]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/azure_devops -->

| Nödvändiga webkrockhändelser och autentisering |
| --- |
| Dessa händelser säkerställer att Cloud Manager kan validera pull-begäranden, svara på exekveringar och interagera med kommentarer för samordning av pipeline.<br>Kontrollera att webbkroken är konfigurerad för att aktiveras för följande obligatoriska webkrokrok-händelser<ul><li>Databas: Tryck</li></ul>Ange autentisering:<br>1. Skriv `cloudmanager` i fältet **Användarnamn för grundläggande autentisering**.<br>2. I fältet **Grundläggande autentiseringslösenord** skriver du den Webkrockhemlighet som genererats från Cloud Manager användargränssnitt. |

>[!ENDTABS]


### Validering av pull-begäranden med webhooks

När webbhookar har konfigurerats korrekt utlöser Cloud Manager automatiskt pipelinekörningar eller PR-valideringskontroller för din databas.

Beteendet varierar beroende på vilken Git-leverantör du använder, vilket beskrivs nedan.

>[!BEGINTABS]


>[!TAB GitHub Enterprise]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/github -->

När kontrollen skapas ser den ut som följande skärmbild nedan. Den största skillnaden från `GitHub.com` är att `GitHub.com` använder en kontrollkörning, medan GitHub Enterprise (med personliga åtkomsttoken) genererar en implementeringsstatus:

![Bekräfta status för att ange PR-valideringsprocess för GitHub Enterprise](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-github-pr-validation.png)


>[!TAB GitLab]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/gitlab -->

GitLab-interaktioner är bara beroende av kommentarer. När valideringen börjar läggs en kommentar till. När valideringen är klar (vare sig den lyckades eller misslyckades) tas den inledande kommentaren bort och ersätts med en ny kommentar som innehåller valideringsresultat eller felinformation.

När validering av kodkvalitet körs:

![När validering av kodkvalitet körs](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab1.png)

När kvalitetsvalideringen är klar:

![När kvalitetsvalideringen är klar](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab2.png)

När validering av kodkvalitet misslyckas med ett fel:

![När kodkvalitetsvalideringen misslyckas och ett fel inträffar](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab3.png)

När valideringen av kodkvaliteten misslyckas på grund av kundproblem:

![När kodkvalitetsvalideringen misslyckas på grund av kundproblem](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab4.png)


>[!TAB Bitbucket]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/bitbucket -->

När validering av kodkvalitet körs:

![Status när kodkvalitetsvalideringen körs](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket1.png)

Använder bekräftelsestatus för spårning av PR-valideringsförlopp. I följande fall visar skärmbilden vad som händer när en kodkvalitetsvalidering misslyckas på grund av ett kundproblem. En kommentar läggs till med detaljerad felinformation och en implementeringskontroll skapas som visar felet (visas till höger):

![Dra in begärandevalideringsstatus för Bitbucket](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket2.png)



>[!ENDTABS]


## Felsöka webkrockproblem

* Kontrollera att webboks-URL:en innehåller en giltig API-nyckel.
* Kontrollera att webbhothändelser är korrekt konfigurerade i Git-leverantörsinställningarna.
* Om PR-validering eller utlösare för pipeline inte fungerar kontrollerar du att webkrockhemligheten är uppdaterad både i Cloud Manager och i din Git-leverantör.


