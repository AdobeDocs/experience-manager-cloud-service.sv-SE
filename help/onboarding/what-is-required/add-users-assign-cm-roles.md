---
title: 'Systemadministratörsuppgifter '
description: Följ den här sidan för att lära dig hur du lägger till användare och tilldelar dem till roller i Cloud Manager som systemadministratör
translation-type: tm+mt
source-git-commit: f1f5766a41763634e0aaba44e55471ac2ea5dc8f
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---


# Systemadministratörsaktiviteter {#add-users-assign}

Systemadministratörer hanterar alla aspekter av sina användare, från åtkomst till behörigheter. Den här användaren är den första personen som har tillgång till att börja utföra uppgifter i Admin Console och Cloud Manager.
En systemadministratör utför följande organisatoriska åtgärder:

* Lägga till användare
* Tilldela användare roller och behörigheter i Cloud Manager

## Lägga till användare {#add-users}

>[!NOTE]
>Du måste vara systemadministratör för att kunna lägga till en användare.

1. Om du är systemadministratör går du till [Admin Console](https://adminconsole.adobe.com). Du kan också navigera till Cloud Manager där du kan se knappen **Hantera åtkomst** enligt beskrivningen nedan.

1. Klicka på **Hantera åtkomst**-knappen, som finns högst upp till höger på Cloud Managers startsida, för att öppna Admin Console på en ny flik.

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin5.png)

   Från **Admin Console** kan du lägga till användare i Cloud Manager och tilldela dem till roller, som kallas produktprofiler i Admin Console.

1. Välj **Adobe Experience Manager som Cloud Service** på **kort för produkter och tjänster** enligt nedan.

   ![](/help/onboarding/what-is-required/assets/admin-console-1.png)

1. Välj fliken **Användare** i åtgärdsfältet och välj sedan **Lägg till användare**.

   ![](/help/onboarding/what-is-required/assets/admin-console-2.png)

1. Välj användare och tilldela lämplig molnhanterarroll(er) eller produktprofil(er) till användaren enligt nedan.

   ![](/help/onboarding/what-is-required/assets/admin-console-3.png)

   >[!NOTE]
   >Se föregående avsnitt, [Användarroller och behörigheter](#user-roles) och [Behörigheter som är associerade med rolldefinitioner](#permissions), för att säkerställa att rätt användare tilldelas rätt roll(er) i **Admin Console**.

   Nu har du lagt till användare i Adobe Experience Manager som produktkontext för Cloud Service och konfigureras med rätt roller eller produktprofiler.

   Om du till exempel har rollen som

   * ***Business Owner***, du har behörighet att lägga till ett nytt program eller redigera ett program, lägga till eller uppdatera en miljö, lägga till/redigera/ta bort pipelinen och köra valfri pipeline samt distribuera kod AEM miljö eller kodkvalitet.

   * ***Distributionshanteraren*** har behörighet att lägga till eller uppdatera en miljö, köra valfri pipeline och distribuera kod AEM miljön eller kodkvaliteten.

   * ***Utvecklare***: du har behörighet att skapa en personlig åtkomsttoken för åtkomst till Git.

      >[!NOTE]
      > En användare kan tilldelas flera roller. Om du till exempel tilldelar både Business Owner- och Deployment Manager-roller till en användare får användaren en kombination av eller summan av dessa behörigheter.
