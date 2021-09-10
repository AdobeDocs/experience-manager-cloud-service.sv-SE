---
title: Åtkomst till databaser
seo-title: Accessing Repositories
description: På den här sidan beskrivs hur du kan komma åt och hantera Git-databasen.
seo-description: Follow this page to learn how to access and manage your Git repository.
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 3cdee254eebcf45762feff8fe081b006a803ef1b
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 5%

---

# Åtkomst till databaser {#accessing-repos}

Du kan komma åt och hantera din Git-databas med hjälp av Git-kontohantering för självbetjäning från användargränssnittet i Cloud Manager.

## Använda kontohantering för självbetjäningsdatabaser {#self-service-repos}

Använd knappen **Åtkomst till repo-information** som är tillgänglig från användargränssnittet i Cloud Manager, som är mest framträdande på pipeline-kortet.

1. Gå till **Pipelines**-kortet från sidan **Programöversikt**.

1. Du kommer att visa alternativet **Åtkomst till repo-information** för att komma åt och hantera din Git-databas.

   ![](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

   Om du dessutom väljer pipelinefliken **Icke-produktion** visas även alternativet **Åtkomst till repo-information**.

   ![](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

   >[!NOTE]
   >Alternativet **Åtkomst till repo-information** är synligt för användare i rollen Utvecklare eller Distributionshanterare. Om du klickar på den här knappen öppnas en dialogruta där användaren kan hitta URL:en till sin Git-databas för Cloud Manager tillsammans med användarnamn och lösenord.

   ![](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

   Viktigt att tänka på när du hanterar ditt Git i Cloud Manager är:

   * **URL**: Databas-URL
   * **Användarnamn**: Användarnamnet
   * **Lösenord**: Värdet som visas när användaren klickar på knappen **Generera lösenord**.


      >[!NOTE]
      >En användare kan checka ut en kopia av sin kod och göra ändringar i den lokala koddatabasen. När det är klart kan användaren spara sina kodändringar i fjärrkoddatabasen i Cloud Manager.
