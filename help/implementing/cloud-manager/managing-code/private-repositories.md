---
title: Lägga till privata databaser i Cloud Manager
description: Lär dig hur du konfigurerar Cloud Manager så att det fungerar med dina egna privata GitHub-databaser.
exl-id: 5232bbf5-17a5-4567-add7-cffde531abda
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---

# Lägga till privata databaser i Cloud Manager {#private-repositories}

Genom att konfigurera Cloud Manager så att det fungerar med dina egna privata GitHub-databaser kan du validera din kod direkt i GitHub-databasen via Cloud Manager, så att du slipper synkronisera din kod konsekvent med Adobe-databasen.

>[!NOTE]
>
>Den här funktionen är exklusiv för public GitHub. Det finns inget stöd för GitHub som är självvärd.

## Konfiguration {#configuration}

Konfigurationen består av två huvudsteg:

1. [Lägg till databas](#add-repo)
1. [Validering av ägarskap för privat databas](#validate-ownership)

### Lägg till databas {#add-repo}

1. Gå till sidan **Programöversikt** i Cloud Manager och välj fliken **Databaser** för att växla till sidan **Databaser** och klicka på **Lägg till databas**.

1. I dialogrutan **Lägg till databas** väljer du **Privat databas** som databastyp.

1. Ange information om din databas

   * **Databasnamn** - ett uttrycksfullt namn
   * **Databas-URL** - Databasens URL, som måste sluta med `.git`
   * **Beskrivning** (valfritt) - En längre beskrivning av databasen efter behov

   ![Lägg till egen databas](/help/implementing/cloud-manager/assets/repos/add-own-github.png)

1. Välj **Spara**.

>[!TIP]
>
>Mer information om hur du hanterar databaser i Cloud Manager finns i [Cloud Manager-databaser](/help/implementing/cloud-manager/managing-code/managing-repositories.md).

### Validering av privat databasägande {#validate-ownership}

Cloud Manager känner nu till din GitHub-databas, men den behöver fortfarande åtkomst till den. Om du vill bevilja åtkomst måste du installera appen Adobe GitHub och verifiera att du äger den angivna databasen.

1. När du har lagt till en egen databas öppnas dialogrutan **Validering av privat databasägande**.

   ![Verifiering av privat databasägande](/help/implementing/cloud-manager/assets/repos/private-repo-validate.png)

1. Cloud Manager använder en GitHub-app för att interagera säkert med din databas.
   * En ägare till din GitHub-organisation måste installera appen som finns på `https://github.com/apps/cloud-manager-for-aem` och bevilja åtkomst till databasen.
   * Mer information om hur du gör detta finns i dokumentationen för GitHub.

1. För att förbättra säkerheten måste du skapa en hemlig fil i databasens standardgren. Välj **Generera**.

1. Bekräfta genereringen av den hemliga filen genom att trycka eller klicka på **Bekräfta**.

   ![Bekräfta hemlig generering](/help/implementing/cloud-manager/assets/repos/confirm-generation.png)

1. I fönstret **Validering av privat databasägande** har Cloud Manager genererat innehållet i den privata filen i fältet **Secret file content**. Kopiera innehållet från det fältet.

   * Innehållet i den hemliga filen visas bara en gång. Generera om hemligheten om du inte kopierar innehållet innan du stänger det här fönstret.

   ![Kopiera hemligt filinnehåll](/help/implementing/cloud-manager/assets/repos/new-secret.png)

1. Skapa en ny fil i standardgrenen för GitHub-repon med namnet `.well-known/adobe/cloud-manager-challenge` och klistra in det hemliga filinnehållet i den filen och spara.

1. När appen har installerats och den hemliga filen finns i databasen kan du välja **Validera** i dialogrutan **Validering av privat databasägande**.

Programmet kan installeras och en hemlig fil kan skapas i vilken ordning som helst. Båda stegen måste dock slutföras innan du kan validera.

Till valideringen visas databasen med en röd ikon, som anger att den ännu inte har validerats och inte kan användas.

![Ovaliderat svar](/help/implementing/cloud-manager/assets/repos/unvalidated-repo.png)

Kolumnen **Type** identifierar enkelt databaser som tillhandahålls av Adobe (**Adobe**) och dina egna GitHub-databaser (**GitHub**).

Om du behöver gå tillbaka till databasen vid ett senare datum för att slutföra valideringen väljer du ellipsknappen på sidan **Databaser** i den rad som representerar GitHub-databasen som du nyss lade till och väljer **Verifiering av ägarskap** i listrutan.

## Använda privata databaser med Cloud Manager {#using}

När GitHub-databasen har validerats i Cloud Manager slutförs integreringen och du kan använda databasen med Cloud Manager.

1. När du skapar en pull-begäran startas en GitHub-kontroll automatiskt.

   ![GitHub-kontroller](/help/implementing/cloud-manager/assets/repos/github-checks.png)

1. För varje pull-begäran skapas en [fullständig kvalitetspipeline för stackkod](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) automatiskt. Detta tillvägagångssätt startas vid varje uppdatering av pull-begäran.

1. GitHub-kontrollen fortsätter att vara i ett körningsläge tills kodkvalitetskontrollerna har slutförts. Kodkvalitetsresultaten sprids sedan till GitHub-kontrollen.

   ![Kvalitetskontroller för GitHub-kod](/help/implementing/cloud-manager/assets/repos/github-code-quality.png)

När pull-begäran stängs eller sammanfogas, tas hela stackkodens kvalitetsflöde som skapas automatiskt bort.

>[!TIP]
>
>I dokumentet [GitHub Check Annotations](github-annotations.md) finns mer information om den information som ges via GitHub när pull-begärandekontroller körs.

>[!TIP]
>
>Du kan styra de rörledningar som skapas automatiskt för att validera varje pull-begäran till en privat databas. Mer information finns i dokumentet [GitHub Check Configuration for Private Repositories](github-check-config.md).

## Associera privata databaser med pipelines {#pipelines}

Validerade privata databaser kan associeras med [rörledningar i full stack och i klientstruktur.](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)

>[!NOTE]
>
>Rörledningar för webbnivå och konfiguration stöds inte i privata databaser.

## Begränsningar {#limitations}

Vissa begränsningar gäller när du använder privata databaser med Cloud Manager.

* Du kan inte pausa pull-begärandevalideringen med GitHub-kontrollen från Cloud Manager.
   * Om GitHub-databasen valideras i Cloud Manager försöker Cloud Manager alltid validera pull-begäranden som skapas för den databasen.
* Om appen Adobe GitHub tas bort från din GitHb-organisation tas valideringsfunktionen för pull-begäranden bort för alla databaser.
* Rörledningar för webbnivå och konfiguration stöds inte i privata databaser.
* Ingen Git-tagg kommer att skapas och skickas när privata databaser används i produktions-pipelines med fullständig stackanslutning.
* Pipeliner som använder privata databaser och utlösaren för bygge vid implementering startas inte automatiskt när en ny implementering överförs till den valda grenen.
* [Återanvändning av felaktigheter](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) gäller inte för privata databaser.
