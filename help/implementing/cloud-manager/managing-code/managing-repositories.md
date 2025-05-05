---
title: Hantera databaser i Cloud Manager
description: Lär dig hur du lägger till, visar och tar bort Git-databaser i Cloud Manager.
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 9cde6e63ec452161dbeb1e1bfb10c75f89e2692c
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---


# Hantera databaser i Cloud Manager {#managing-repos}

Lär dig hur du visar, lägger till och tar bort Git-databaser i Cloud Manager.

## Om databaser i Cloud Manager {#overview}

Databaser i Cloud Manager används för att lagra och hantera projektkoden med Git. För varje *program* som du lägger till skapas en databas som hanteras av Adobe automatiskt.

Dessutom kan du skapa fler Adobe-hanterade databaser eller lägga till egna privata databaser. Alla databaser som är länkade till ditt program kan visas på sidan **Databaser**.

Databaser som skapas i Cloud Manager kan också väljas när du lägger till eller redigerar pipelines. Mer information om hur du konfigurerar pipelines finns i [CI-CD-pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

Varje pipeline är länkad till en primär databas eller gren. Med stöd för [Git-undermodul](git-submodules.md) kan flera sekundära grenar inkluderas under byggprocessen.

## Visa sidan Databaser {#repositories-window}

På sidan **Databaser** kan du visa information om den valda databasen. Denna information omfattar vilken typ av databas som används. Om databasen är markerad som **Adobe** anger den att den är en Adobe-hanterad databas. Om den är märkt som **GitHub** refererar den till en privat GitHub-databas som du hanterar. Dessutom innehåller sidan information om t.ex. när databasen skapades och om de rörledningar som är kopplade till den.

Om du vill vidta åtgärder för en vald databas kan du klicka på databasen och använda ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) för att öppna en nedrullningsbar meny. För databaser som hanteras med Adobe kan du **[kontrollera grenar/skapa projekt](#check-branches)**.

![Databasåtgärder](assets/repository-actions.png)
*Nedrullningsbar meny på sidan Databaser.*

Andra tillgängliga åtgärder på den nedrullningsbara menyn är bland annat **[Kopiera databas-URL](#copy-url)**, **[Visa och uppdatera](#view-update)** och **[Ta bort](#delete)** databasen.

**Så här visar du sidan Databaser:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. På sidan **Programöversikt** klickar du på ![Mappikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **Databaser** på sidomenyn.

1. På sidan **Databaser** visas alla databaser som är associerade med det valda programmet.

   ![Databassida](assets/repositories.png)
   *Sidan Databaser i Cloud Manager.*

## Lägga till en databas {#adding-repositories}

En användare måste ha rollen **Distributionshanteraren** eller **Affärsägare** för att kunna lägga till en databas.

Klicka på **Lägg till databas** på sidan **Databaser** i det övre högra hörnet.

![Dialogrutan Lägg till databas](assets/repository-add.png)
*Dialogrutan Lägg till databas.*

Cloud Manager har stöd för två typer av databaser: databaser som hanteras med Adobe (**Adobe-databas**) och självhanterade databaser (**Privat databas**). De obligatoriska fälten för konfiguration varierar beroende på vilken typ av databas du väljer att lägga till. Mer information finns i följande:

* [Lägga till Adobe-databaser i Cloud Manager](adobe-repositories.md)
* [Lägga till privata databaser i Cloud Manager](private-repositories.md)

Det finns en gräns på 300 databaser i alla program i ett visst företag eller i en IMS-organisation.

## Åtkomst till databasinformation {#repo-info}

När du visar dina databaser i fönstret **Databaser** kan du visa information om hur du kommer åt databaser som hanteras med Adobe genom att klicka på knappen **Åtkomstrepo-information** i verktygsfältet.

![Databasinformation](assets/repository-access-repo-info2.png)

Fönstret **Databasinformation** öppnas med information. Mer information om hur du får åtkomst till databasinformation finns i [Åtkomst till databasinformation](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

## Kontrollera grenar/skapa projekt {#check-branches}

I **AEM Cloud Manager** har åtgärden **Kontrollera grenar/Skapa projekt** två syften, beroende på databasens aktuella tillstånd.

* Om databasen är nyskapad genererar den här åtgärden ett exempelprojekt med hjälp av [den AEM projekttypen](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/developing/archetype/overview).
* Om exempelprojektet redan har skapats i databasen kontrollerar åtgärden databasens och dess grenars status och ger information om huruvida exempelprojektet redan finns.

  ![Åtgärden Kontrollera grenar](assets/check-branches.png)

## Kopiera databas-URL {#copy-url}

Åtgärden **Kopiera databas-URL** kopierar URL:en för den databas som är markerad på sidan **Databaser** till Urklipp så att den kan användas någon annanstans.

## Visa och uppdatera en databas {#view-update}

Åtgärden **Visa och uppdatera** öppnar dialogrutan **Uppdatera databas**, där du kan visa databasens **namn** och **databas-URL-förhandsgranskning**. Dessutom kan du uppdatera **Beskrivning** för databasen.

![Visa och uppdatera databasinformation](assets/repository-view-update.png)

## Ta bort en databas {#delete}

Åtgärden **Ta bort** tar bort databasen från ditt projekt. Det går inte att ta bort en databas om den är associerad med en pipeline.

![Ta bort](assets/repository-delete.png)

Om du tar bort en databas går det inte att använda dess namn för nya databaser som skapas i framtiden. Om du försöker lägga till en databas med samma namn för en borttagen databas visas följande felmeddelande:

`Repository name should be unique within organization.`

Dessutom är den borttagna databasen inte längre tillgänglig i Cloud Manager och kan inte länkas till någon pipeline.

