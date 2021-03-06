---
title: Åtkomst till databaser
description: Lär dig hur du får åtkomst till och hanterar din Git-databas med hjälp av Git-kontohantering för självbetjäning från Cloud Manager.
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 4729574eb31e01077f0d2a35efcef6d134f6aa5c
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Åtkomst till databaser {#accessing-repos}

Lär dig hur du får åtkomst till och hanterar din Git-databas med hjälp av Git-kontohantering för självbetjäning från Cloud Manager.

## Använda självbetjäningsarkivkontohantering {#self-service-repos}

Med Cloud Manager är det enkelt att hämta databasinformation med **Åtkomst till svarsinformation** finns väl synligt på pipeline-kortet.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Pipelines** från **Programöversikt** sidan och hitta **Åtkomst till svarsinformation** för att komma åt och hantera din Git-databas.

   ![Knappen Åtkomst till upprepningsinformation på miljökortet](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. Klicka på **Visa information om svar** för att öppna en dialogruta:

   * URL:en till Cloud Managers Git-databas.
   * Git-användarnamn.
   * Git-lösenordet, vars värde visas när **Generera lösenord** klickas på knappen.

   ![](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

Med hjälp av dessa inloggningsuppgifter kan användaren klona en lokal kopia av databasen och göra ändringar i den lokala databasen, och när den är klar kan han eller hon spara kodändringar i fjärrkoddatabasen i Cloud Manager.

The **Åtkomst till svarsinformation** finns även på **Icke-produktion** fliken pipeline i **Pipelines** kort.

![Knappen Åtkomst till upprepningsinformation på icke-produktionsfliken](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

>[!NOTE]
>
>The **Åtkomst till svarsinformation** alternativet är synligt för användare med **Utvecklare** eller **Distributionshanteraren** roller.
