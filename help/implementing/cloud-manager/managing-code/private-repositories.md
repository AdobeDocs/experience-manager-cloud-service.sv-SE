---
title: Lägg till en privat GitHub-databas i Cloud Manager
description: Lär dig hur du konfigurerar Cloud Manager så att det fungerar med dina egna privata GitHub-databaser.
exl-id: 5232bbf5-17a5-4567-add7-cffde531abda
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 169de7971fba829b0d43e64d50a356439b6e57ca
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---

# Lägg till en privat GitHub Cloud-databas i Cloud Manager {#private-repositories}

Genom att konfigurera Cloud Manager för integrering med ditt privata GitHub-moln (databaser på `github.com`) kan du validera din kod direkt i GitHub med Cloud Manager. Den här konfigurationen eliminerar behovet av att synkronisera koden regelbundet med Adobe-databasen.

>[!NOTE]
>
>Du kan även lägga till följande typer av databaser med webbhooks:
>
>* GitHub Enterprise Server-databaser (värdbaserad version av GitHub)
>* GitLab-databaser (både `gitlab.com` och självhanterade versioner av GitLab)
>* Bitbucket-databaser (både `bitbucket.org` och Bitbucket Server, den självhanterade versionen av BitBucket)
>
>Se [Lägg till externa databaser i Cloud Manager - privat beta](/help/implementing/cloud-manager/managing-code/external-repositories.md).

<!-- CONSIDER ADDING MORE DETAIL... THE WHY. Some key points about this capability include the following:

* **Direct Integration**: With this setup, you can directly link your private GitHub repositories to Cloud Manager, allowing for seamless code validation, deployment, and CI/CD (Continuous Integration/Continuous Deployment) pipelines without needing to maintain a separate sync process with Adobe's default Git repository.

* **Customization and Autonomy**: Companies often prefer managing their own source code repositories for security, control, and integration purposes. "Build your own GitHub" allows organizations to maintain their internal development processes while leveraging the full functionality of Cloud Manager for building, testing, and deploying AEM (Adobe Experience Manager) applications.

* **Simplified Workflow**: It reduces the overhead of synchronizing code between multiple repositories by allowing Cloud Manager to access the organization's private repository directly, making the development cycle faster and more efficient.

* **CI/CD Pipelines**: Teams can still benefit from Adobe Cloud Manager's automated build, test, and deployment processes, as the integration allows the CI/CD pipelines to pull code from the organization's own GitHub repository.

In essence, a "Build your own GitHub" in Adobe Cloud Manager empowers teams to manage their own GitHub repositories while still using the robust deployment and validation capabilities of Cloud Manager.

>[!NOTE]
>
>This feature is exclusive to public GitHub. Support for self-hosted GitHub is not available. -->

## Konfiguration {#configuration}

Konfigurationen av en privat GitHub Cloud-databas i Cloud Manager består av två steg:

1. [Lägg till en privat GitHub-molndatabas](#add-repo) i ett valt program.
1. [validera sedan ägarskapet för den privata GitHub-molndatabasen](#validate-ownership).



### Lägg till en privat GitHub Cloud-databas i ett program {#add-repo}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** väljer du det program som du vill länka till en privat Git-databas.

1. Välj ![Mappikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **Databaser** på sidomenyn under **Tjänster**.

   ![Sidan Databaser](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. Klicka på **Lägg till databas** i det övre högra hörnet på sidan **Databaser**.

1. I dialogrutan **Lägg till databas** väljer du **Privat databas** som databastyp.

   ![Lägg till egen databas](/help/implementing/cloud-manager/assets/repos/add-own-github.png)

1. Ange följande information om din databas i varje fält:

   | Fält | Beskrivning |
   | --- | --- |
   | Databasnamn | Ett uttrycksfullt namn för din nya databas. |
   | Databas-URL | URL:en för den privata databasen, som måste sluta i `.git`.<br>Till exempel *`https://github.com/org-name/repo-name.git`* (URL-sökvägen är endast avsedd som illustration). |
   | Beskrivning (valfritt) | En detaljerad beskrivning av databasen. |

1. Välj **Spara**.
Nu kan du [verifiera ägarskapet för den privata databasen](#validate-ownership).

>[!TIP]
>
>Mer information om hur du hanterar databaser i Cloud Manager finns i [Cloud Manager-databaser](/help/implementing/cloud-manager/managing-code/managing-repositories.md).


### Validera ägarskap för en privat GitHub-databas {#validate-ownership}

Cloud Manager känner nu till din GitHub-databas, men den behöver fortfarande åtkomst till den. Om du vill bevilja åtkomst måste du installera Adobe GitHub-appen och verifiera att du äger den angivna databasen.

**Så här verifierar du ägarskap för en privat GitHub-databas:**

1. När du har lagt till en egen databas följer du de återstående stegen i dialogrutan **Validering av privat databasägande**.

   ![Verifiering av privat databasägande](/help/implementing/cloud-manager/assets/repos/private-repo-validate.png)

   |  | Beskrivning |
   | --- | --- |
   | **Steg 1: GitHub-app** | Cloud Manager använder en GitHub-app för att interagera med din privata databas på ett säkert sätt.<br> ・ En ägare till din GitHub-organisation måste installera appen som finns på `https://github.com/apps/cloud-manager-for-aem` och ge åtkomst till databasen.<br> ・ Mer information om hur du installerar och beviljar åtkomst finns i dokumentationen för GitHub. |
   | **Steg 2: Hemlig fil** | För att förbättra säkerheten måste du skapa en hemlig fil i databasens standardgren.<br> ・ Klicka på **Generera** och sedan på **Bekräfta**. Cloud Manager genererar innehållet i den privata filen i textfältet **Hemligt filinnehåll**.<br> ・ Klicka på ![Kopiera ikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) för att kopiera innehållet från det fältet. Innehållet i den hemliga filen visas bara en gång. Generera om hemligheten om du inte kopierar innehållet innan du stänger den här dialogrutan. |

1. Skapa en ny fil i standardgrenen för GitHub-repo med namnet:

   `.well-known/adobe/cloud-manager-challenge`

1. Klistra in det hemliga filinnehållet i den nya filen som du just skapade och spara.

   När appen har installerats och den hemliga filen finns i databasen fortsätter du med steget.

1. Klicka på **Validera** i dialogrutan **Validera** för privat databasägande.

Programmet kan installeras och en hemlig fil kan skapas i valfri ordning. Båda stegen måste dock slutföras innan du kan validera.

Till valideringen visas databasen med en röd ikon, som anger att den ännu inte har validerats och inte kan användas.

![Ovaliderat svar](/help/implementing/cloud-manager/assets/repos/unvalidated-repo.png)

Kolumnen **Type** i tabellen på sidan **Databaser** identifierar databaser som tillhandahålls av Adobe (**Adobe**) och egna privata databaser (**GitHub**).

Om du behöver gå tillbaka till databasen senare för att slutföra valideringen klickar du på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) på sidan **Databaser** på raden som representerar GitHub-databasen som du just lade till. Välj **Verifiering av ägarskap** i listrutan.



## Använd privata GitHub Cloud-databaser med Cloud Manager {#using}

När GitHub-databasen har validerats i Cloud Manager är integreringen klar. Du kan använda databasen med Cloud Manager.

**Så här använder du privata GitHub Cloud-databaser med Cloud Manager:**

1. När du skapar en pull-begäran startas en GitHub-kontroll automatiskt.

   ![GitHub-kontroller](/help/implementing/cloud-manager/assets/repos/github-checks.png)

1. För varje pull-begäran skapas automatiskt en [fullständig kvalitetspipeline för stackkod](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md). Detta tillvägagångssätt startas vid varje uppdatering av pull-begäran.

1. GitHub-kontrollen fortsätter att vara i ett körningsläge tills kodkvalitetskontrollen är slutförd. Kodkvalitetsresultaten sprids sedan till GitHub-kontrollen.

   ![Kvalitetskontroller för GitHub-kod](/help/implementing/cloud-manager/assets/repos/github-code-quality.png)

När pull-begäran sammanfogas eller stängs, tas den fullständiga stackkodens kvalitetspipeline som skapas automatiskt bort.

>[!TIP]
>
>Se [GitHub Check Annotations](github-annotations.md) för mer information om information som tillhandahålls via GitHub när pull-begärankontroller körs.

>[!TIP]
>
>Du kan styra de rörledningar som skapas automatiskt för att validera varje pull-begäran till en privat databas. Mer information finns i [GitHub-kontrollkonfigurationen för privata databaser](github-check-config.md).



## Associera privata GitHub Cloud-databaser med rörledningar {#pipelines}

Validerade privata databaser kan associeras med [rörledningar i full hög och i framtend](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).



## Användningsinformation {#usage-notes}

* Rörledningar för webbnivå och konfiguration stöds inte i privata databaser.
* Ingen Git-tagg skapas och skickas när privata databaser används i produktion av rörledningar i en hel hög.
* Om Adobe GitHub-appen tas bort från din GitHub-organisation tas funktionen för pull-begärandevalidering bort för alla databaser.
* Pipeliner som använder privata GitHub Cloud-databaser och utlösaren för att implementera startas inte automatiskt när en ny implementering överförs till den valda grenen.
* [Återanvändning av felaktigheter](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) gäller inte för privata databaser.
* Du kan inte pausa pull-begärandevalideringen med GitHub-kontrollen från Cloud Manager.
Om GitHub-databasen valideras i Cloud Manager försöker Cloud Manager alltid validera pull-begäranden som skapas för den databasen.
