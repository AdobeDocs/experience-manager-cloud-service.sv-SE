---
title: Hantera databaser i Cloud Manager
description: Lär dig hur du skapar, visar och tar bort Git-databaser i Cloud Manager.
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---


# Hantera databaser i Cloud Manager {#managing-repos}

Lär dig hur du skapar, visar och tar bort Git-databaser i Cloud Manager.

## Ökning {#overview}

Databaser används för att lagra och hantera projektkoden med Git. Alla program du skapar i Cloud Manager har en databas som hanteras av Adobe.

Du kan välja att skapa ytterligare databaser som hanterar Adobe och även lägga till egna privata databaser. Alla databaser som är associerade med ditt program kan visas i fönstret **Databaser**.

Databaser som skapas i Cloud Manager är också tillgängliga när du lägger till eller redigerar pipelines. Mer information finns i [CI-CD Pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

Det finns en enda primär databas eller en gren för en given pipeline. Med stöd för [Git-undermodul kan ](git-submodules.md) många sekundära grenar inkluderas vid byggtiden.

## Fönstret Databaser {#repositories-window}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. På sidan **Programöversikt** väljer du fliken **Databaser** för att växla till sidan **Databaser**.

1. Fönstret **Databaser** visar alla databaser som är associerade med ditt program.

   ![Databasfönstret](assets/repositories.png)

Fönstret **Databaser** innehåller information om databaserna:

* Typ av databas
   * **Adobe** anger databaser som hanteras av Adobe
   * **GitHub** anger privata GitHub-databaser som du hanterar
* När den skapades
* Pipelines som är associerade med databasen

Du kan markera databasen i fönstret och klicka på ellipsknappen för att vidta åtgärder för den valda databasen.

* **[Kontrollera grenar/Skapa projekt](#check-branches)** (endast tillgängligt för Adobe-databaser)
* **[Kopiera databas-URL](#copy-url)**
* **[Visa och uppdatera](#view-update)**
* **[Ta bort](#delete)**

![Databasåtgärder](assets/repository-actions.png)

## Lägga till databaser {#adding-repositories}

Tryck eller klicka på knappen **Lägg till databas** i fönstret **Databaser** för att starta guiden **Lägg till databas**.

![Guiden Lägg till databas](assets/add-repository-wizard.png)

Cloud Manager har stöd för båda databaser som hanteras av Adobe (**Adobe-databas**) och dina egna självhanterade databaser (**Privat databas**). De obligatoriska fälten varierar beroende på vilken typ av databas du väljer att lägga till. Mer information finns i följande dokument.

* [Lägga till Adobe-databaser i Cloud Manager](adobe-repositories.md)
* [Lägga till privata databaser i Cloud Manager](private-repositories.md)

>[!NOTE]
>
>* En användare måste ha rollen **Distributionshanteraren** eller **Affärsägare** för att kunna lägga till en databas.
>* Det finns en gräns på 300 databaser i alla program i ett visst företag eller i en IMS-organisation.

## Åtkomst till svarsinformation {#repo-info}

När du visar dina databaser i fönstret **Databaser** kan du visa information om hur du kommer åt databaser som hanteras med Adobe genom att trycka eller klicka på knappen **Åtkomstrepo-information** i verktygsfältet.

![Databasinformation](assets/repo-info.png)

Fönstret **Databasinformation** öppnas med information. Mer information om åtkomst till databasinformation finns i dokumentet [Åtkomst till databasinformation.](accessing-repos.md)

## Kontrollera grenar/skapa projekt {#check-branches}

Åtgärden **Kontrollera grenar/Skapa projekt** utför två funktioner beroende på databasens tillstånd.

* Om databasen är nyskapad skapar åtgärden ett exempelprojekt baserat på [den AEM projektarkitypen.](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/developing/archetype/overview)
* Om exempelprojektet redan har skapats i databasen kontrolleras statusen för databasen och dess grenar, och sedan rapporteras om exempelprojektet redan finns.

![Åtgärden Kontrollera grenar](assets/check-branches.png)

## Kopiera databas-URL {#copy-url}

Åtgärden **Kopiera databas-URL** kopierar URL:en för den databas som är markerad i fönstret **Databaser** till Urklipp så att den kan användas någon annanstans.

## Visa och uppdatera {#view-update}

Åtgärden **Visa och uppdatera** öppnar dialogrutan **Uppdatera databas**. Med den kan du visa **Namn** och **databas-URL-förhandsgranskning** samt uppdatera **Beskrivning** för databasen.

![Visa och uppdatera databasinformation](assets/view-update.png)

## Ta bort {#delete}

Åtgärden **Ta bort** tar bort databasen från ditt projekt. En databas kan inte tas bort om den är associerad med en pipeline.

![Ta bort](assets/delete.png)

Om du tar bort en databas:

* Gör det borttagna databasnamnet oanvändbart för nya databaser som kan skapas i framtiden.
   * Felmeddelandet `Repository name should be unique within organization.` visas i sådana fall.
* Gör den borttagna databasen otillgänglig i Cloud Manager och inte tillgänglig för länkning till en pipeline.
