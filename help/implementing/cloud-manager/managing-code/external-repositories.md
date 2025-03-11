---
title: Lägg till externa databaser i Cloud Manager - begränsad betaversion
description: Lär dig hur du lägger till en extern databas i Cloud Manager. Cloud Manager stöder integrering med GitHub Enterprise Server-, GitLab- och Bitbucket-databaser.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: aebda813-2eb0-4c67-8353-6f8c7c72656c
source-git-commit: bfa059ed4e3f04ae6ee1e07910edc62635b03e5a
workflow-type: tm+mt
source-wordcount: '1597'
ht-degree: 0%

---

# Lägga till externa databaser i Cloud Manager - begränsad betaversion {#external-repositories}

Lär dig hur du lägger till en extern databas i Cloud Manager. Cloud Manager stöder integrering med GitHub Enterprise Server-, GitLab- och Bitbucket-databaser.

>[!NOTE]
>
>Den här funktionen är endast tillgänglig genom det tidiga adoptionsprogrammet. Mer information och information om hur du registrerar dig som tidig användare finns i [Bring Your Own Git - now with support for GitLab and Bitbucket](/help/implementing/cloud-manager/release-notes/2024/2024-10-0.md#gitlab-bitbucket).

## Konfigurera en extern databas

Konfigurationen av en extern lagringsplats i Cloud Manager består av tre steg:

1. [Lägg till en extern databas](#add-external-repo) till ett valt program.
1. Ange en åtkomsttoken för den externa databasen.
1. Validera ägarskap för den privata GitHub-databasen.



## Lägga till en extern databas {#add-ext-repo}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** väljer du det program som du vill länka till en extern databas.

1. Klicka på ![Mappdispositionsikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **Databaser** på sidomenyn under **Tjänster**.

   ![Sidan Databaser](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. Klicka på **Lägg till databas** i det övre högra hörnet på sidan **Databaser**.

1. I dialogrutan **Lägg till databas** väljer du **Privat databas** för att länka en extern Git-databas till ditt program.

   ![Lägg till egen databas](/help/implementing/cloud-manager/managing-code/assets/repositories-private-repo-type.png)

1. Ange följande information om din databas i varje fält:

   | Fält | Beskrivning |
   | --- | --- |
   | **Databasnamn** | Obligatoriskt. Ett uttrycksfullt namn för din nya databas. |
   | **Databas-URL** | Obligatoriskt. Databasens URL.<br><br>Om du använder en GitHub-värdbaserad databas måste sökvägen sluta i `.git`.<br>Till exempel *`https://github.com/org-name/repo-name.git`* (URL-sökvägen är endast avsedd som illustration).<br><br>Om du använder en extern databas måste den använda följande URL-sökvägsformat:<br>`https://git-vendor-name.com/org-name/repo-name.git`<br> eller<br>`https://self-hosted-domain/org-name/repo-name.git`<br>Och matcha Git-leverantören. |
   | **Välj databastyp** | Obligatoriskt. Välj den databastyp som du använder:<ul><li>**GitHub** (GitHub Enterprise Server och den självhanterade versionen av GitHub)</li><li>**GitLab** (både `gitlab.com` och den självhanterade versionen av GitLab) </li><li>**Bitbucket** (både `bitbucket.org` och Bitbucket Server samt den självhanterade versionen av Bitbucket)</li></ul>Om databasens URL-sökväg ovan innehåller Git-leverantörens namn, till exempel GitLab eller Bitbucket, är databastypen redan förvald. |
   | **Beskrivning** | Valfritt. En detaljerad beskrivning av databasen. |

1. Välj **Spara** för att lägga till databasen.

1. I dialogrutan **Validering av privat databasägande** anger du en åtkomsttoken för att validera ägarskapet för den externa databasen så att du kan komma åt den.

   ![Välja en befintlig åtkomsttoken för en databas](/help/implementing/cloud-manager/managing-code/assets/repositories-exisiting-access-token.png)
   *Väljer en befintlig åtkomsttoken för en Bitbucket-databas.*

   | Tokentyp | Beskrivning |
   | --- | --- |
   | **Använd befintlig åtkomsttoken** | Om du redan har angett en åtkomsttoken för databasen för din organisation och har tillgång till flera databaser kan du välja en befintlig token. Använd listrutan **Tokennamn** för att välja den token som du vill använda för databasen. I annat fall lägger du till en ny åtkomsttoken. |
   | **Lägg till ny åtkomsttoken** | **Databastyp: GitHub**<br> ・ Ange ett namn för åtkomsttoken som du skapar i textfältet **Token Name**.<br> ・ Skapa en personlig åtkomsttoken genom att följa instruktionerna i [GitHub-dokumentationen](https://docs.github.com/en/enterprise-server@3.14/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).<br> ・ Mer information om vilka behörigheter som krävs finns i följande information: ![Skapa ny PAT för GitHub](/help/implementing/cloud-manager/managing-code/assets/webhook-github-enterprise-server.png)<br> ・ Klistra in den token som du nyss skapade i fältet **Åtkomsttoken**. |
   |  | **Databastyp: GitLab**<br> ・ Ange ett namn för åtkomsttoken som du skapar i textfältet **Token Name**.<br> ・ Skapa en personlig åtkomsttoken genom att följa instruktionerna i [GitLab-dokumentationen](https://docs.gitlab.com/user/profile/personal_access_tokens/).<br> ・ Mer information om vilka behörigheter som krävs finns i följande information: ![Skapa en ny PAT för GitLab](/help/implementing/cloud-manager/managing-code/assets/webhook-gitlab.png)<br> ・ Klistra in den token som du nyss skapade i fältet **Åtkomsttoken**. |
   |  | **Databastyp: Bitbucket**<br> ・ I textfältet **Token Name** anger du ett namn för åtkomsttoken som du skapar.<br> ・ Skapa en databasåtkomsttoken med hjälp av [Bitbucket-dokumentationen](https://support.atlassian.com/bitbucket-cloud/docs/create-a-repository-access-token/).<br> ・ Mer information finns i följande information ![Skapa en ny PAT för Bitbucket](/help/implementing/cloud-manager/managing-code/assets/webhook-bitbucket.png). |

   >[!NOTE]
   >
   >Funktionen **Lägg till ny åtkomsttoken** är för närvarande i fasen Tidiga Adobe-program. Ytterligare funktioner planeras. Därför kan de behörigheter som krävs för åtkomsttoken ändras. Dessutom kan användargränssnittet för hantering av tokens uppdateras, inklusive funktioner som utgångsdatum för token. Och automatiska kontroller för att säkerställa att tokens som är länkade till databaser förblir giltiga.

1. Klicka på **Validera**.

Efter valideringen är den externa databasen klar att användas och länkas till en pipeline.

## Länka en validerad extern databas till en pipeline {#validate-ext-repo}

1. Lägga till eller redigera en pipeline:
   * [Lägg till en produktionspipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [Lägga till icke-produktionsrörledningar](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
   * [Redigera en pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#editing-pipelines)

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
För alla andra externa databaser som är inbyggda med en åtkomsttoken, som GitHub Enterprise Server, GitLab och Bitbucket, är webkrok-konfigurationen tillgänglig och måste konfigureras manuellt.

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
1. Navigera till din Git-leverantörslösning (GitHub Enterprise, GitLab eller Bitbucket).

   All information om webbkrokkonfigurationen och de händelser som krävs för varje leverantör finns i [Lägg till en extern databas](#add-ext-repo). Se tabellen under steg 8.

1. Leta upp lösningsavsnittet **Webkrok** Settings.
1. Klistra in webkroks-URL:en som du kopierade tidigare i URL-textfältet.
   1. Ersätt frågeparametern `api_key` i webkrok-URL:en med din egen riktiga API-nyckel.

      Om du vill generera en API-nyckel måste du skapa ett integreringsprojekt i Adobe Developer Console. Mer information finns i [Skapa ett API-integreringsprojekt](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/).

1. Klistra in webbkrokhemligheten som du kopierade tidigare i textfältet **Hemlig** (eller **Hemlig nyckel** eller **Hemlig token**).
1. Konfigurera webkroken så att rätt händelser skickas som Cloud Manager förväntar.


### Validering av pull-begäranden med webhooks

När webbhookar har konfigurerats korrekt utlöser Cloud Manager automatiskt pipelinekörningar eller PR-valideringskontroller för din databas.

Följande beteenden gäller:

* **GitHub Enterprise Server**

  När kontrollen skapas ser den ut som följande skärmbild nedan. Den största skillnaden från `GitHub.com` är att `GitHub.com` använder en kontrollkörning, medan GitHub Enterprise Server (med personliga åtkomsttoken) genererar en implementeringsstatus:

  ![Bekräfta status för att ange PR-valideringsprocess på GitHub Enterprise Server](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-github-pr-validation.png)

* **Bitbucket**

  När validering av kodkvalitet körs:

  ![Status när kodkvalitetsvalideringen körs](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket1.png)

  Använder bekräftelsestatus för spårning av PR-valideringsförlopp. I följande fall visar skärmbilden vad som händer när en kodkvalitetsvalidering misslyckas på grund av ett kundproblem. En kommentar läggs till med detaljerad felinformation och en implementeringskontroll skapas som visar felet (visas till höger):

  ![Dra in begärandevalideringsstatus för Bitbucket](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket2.png)

* **GitLab**

  GitLab-interaktioner är bara beroende av kommentarer. När valideringen börjar läggs en kommentar till. När valideringen är klar (vare sig den lyckades eller misslyckades) tas den inledande kommentaren bort och ersätts med en ny kommentar som innehåller valideringsresultat eller felinformation.

  När validering av kodkvalitet körs:

  ![När validering av kodkvalitet körs](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab1.png)

  När kvalitetsvalideringen är klar:

  ![När kvalitetsvalideringen är klar](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab2.png)

  När validering av kodkvalitet misslyckas med ett fel:

  ![När kodkvalitetsvalideringen misslyckas och ett fel inträffar](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab3.png)

  När valideringen av kodkvaliteten misslyckas på grund av kundproblem:

  ![När kodkvalitetsvalideringen misslyckas på grund av kundproblem](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab4.png)


## Felsöka webkrockproblem

* Kontrollera att webboks-URL:en innehåller en giltig API-nyckel.
* Kontrollera att webbhothändelser är korrekt konfigurerade i Git-leverantörsinställningarna.
* Om PR-validering eller utlösare för pipeline inte fungerar kontrollerar du att webkrockhemligheten är uppdaterad både i Cloud Manager och i din Git-leverantör.








## Begränsningar

* Externa databaser kan inte länkas till konfigurationspipelines.
* Pipeliner med externa databaser (som inte finns på GitHub) och utlösaren On Git Changes startar inte automatiskt. De kan bara initieras manuellt.


<!-- THIS BULLET REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2024.12.0+Release. THEY CAN NOW START AUTOMATICALLY>
* Pipelines using external repositories (excluding GitHub-hosted repositories) and the **Deployment Trigger** option [!UICONTROL **On Git Changes**], triggers are not automatically started. They must be manually started. -->


