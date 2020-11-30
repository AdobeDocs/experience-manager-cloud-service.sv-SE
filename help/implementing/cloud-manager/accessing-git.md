---
title: Åtkomst till Git
seo-title: Åtkomst till Git
description: På den här sidan beskrivs hur du kan komma åt och hantera Git-databasen.
seo-description: Följ den här sidan för att lära dig hur du får åtkomst till och hanterar din Git-databas.
translation-type: tm+mt
source-git-commit: 114bc678fc1c6e3570d6d2a29bc034feb68aa56d
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 7%

---


# Åtkomst till Git {#accessing-git}

Du kan komma åt och hantera din Git-databas med hjälp av Git-kontohantering för självbetjäning från användargränssnittet i Cloud Manager.

## Använda självbetjäning för Git-kontohantering {#self-service-git}

Använd knappen **Hantera Git** som finns i användargränssnittet i molnhanteraren, som finns längst upp på pipeline-kortet.

1. Gå till sidan Översikt *över ditt* program och till Pipelines-kortet.

1. Du kan visa alternativet **Hantera Git** för att få åtkomst till och hantera din Git-databas.

   ![](assets/manage-git1.png)

   Om du dessutom väljer fliken **Ej produktion** visas alternativet **Hantera Git** även där.

   ![](assets/manage-git-new2.png)

>[!NOTE]
>Alternativet **Hantera Git** är synligt för användare med rollen Utvecklare eller Distributionshanterare. Om du klickar på den här knappen öppnas en dialogruta där användaren kan hitta URL:en till sin Git-databas för Cloud Manager tillsammans med användarnamn och lösenord.

![](assets/manage-git3.png)

Viktigt att tänka på när du hanterar ditt Git i Cloud Manager är:

* **URL**: Databas-URL
* **Användarnamn**: Användarnamnet
* **Lösenord**: Värdet som visas när användaren klickar på knappen **Generera lösenord**.


>[!NOTE]
>
>En användare kan checka ut en kopia av sin kod och göra ändringar i den lokala koddatabasen. När det är klart kan användaren spara sina kodändringar i fjärrkoddatabasen i Cloud Manager.

