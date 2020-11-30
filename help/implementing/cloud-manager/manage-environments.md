---
title: Hantera miljöer - Cloud Service
description: Hantera miljöer - Cloud Service
translation-type: tm+mt
source-git-commit: fb979363fcb8c17fbefd11b9b86498447593f745
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 6%

---


# Hantera miljöer {#manage-environments}

I följande avsnitt beskrivs de typer av miljö som en användare kan skapa och hur användaren kan skapa en miljö.

## Miljötyper {#environment-types}

En användare med nödvändig behörighet kan skapa följande miljötyper (inom gränserna för vad som är tillgängligt för den specifika klientorganisationen).

* **Produktions- och scenmiljö**:
Produktionen och scenen finns som duo och används för testning och produktion.

* **Utveckling**: En utvecklingsmiljö kan skapas för utvecklings- och testningsändamål och kommer endast att kopplas till icke-produktionsrörledningar.

   >[!NOTE]
   >En utvecklingsmiljö som skapas automatiskt i ett sandlådeprogram kommer att konfigureras att innehålla lösningar för platser och resurser.

   I följande tabell sammanfattas miljötyper och deras attribut:

   | Namn | Författarnivå | Publiceringsnivå | Användare kan skapa | Användaren kan ta bort | Rörledning som kan kopplas till miljön |
   |--- |--- |--- |--- |---|---|
   | Produktion | Ja | Ja om webbplatser ingår | Ja | Nej | Produktionspipeline |
   | Scen | Ja | Ja om webbplatser ingår | Ja | Nej | Produktionspipeline |
   | Utveckling | Ja | Ja om webbplatser ingår | Ja | Ja | Icke-produktionsflöde |

   >[!NOTE]
   >Produktionen och scenen finns som duo och används för testning och produktion.  Användaren kan inte skapa enbart scenen eller enbart produktionsmiljön.

## Lägger till miljö {#adding-environments}

1. Klicka på **Lägg till miljö** för att lägga till en miljö. Den här knappen kommer att vara tillgänglig från skärmen **för miljöer** .
   ![](assets/environments-tab.png)

   Alternativet **Lägg till miljö** finns också på **miljökortet** när det inte finns några miljöer i programmet.

   ![](assets/no-environments.png)

   >[!NOTE]
   >Alternativet **Lägg till miljö** inaktiveras beroende på brist på behörigheter eller vad som kommer att ingå i avtalet.

1. Dialogrutan **Lägg till miljö** visas. Användaren måste skicka in information som **miljötyp**, **miljönamn** och **miljöbeskrivning** (beroende på vad användaren har för mål med att skapa miljön inom gränserna för vad som är tillgängligt för den specifika klientorganisationen).

   ![](assets/add-environment2.png)

   >[!NOTE]
   >När du skapar en miljö skapas en eller flera *integreringar* i Adobe I/O. De är synliga för användare som har åtkomst till Adobe I/O Console och får inte tas bort. Detta tas bort i beskrivningen i Adobe I/O Console.

   ![](assets/add-environment-image1.png)

1. Klicka på **Spara** för att lägga till en miljö med de ifyllda villkoren.  På skärmen *Översikt* visas kortet där du kan ställa in din pipeline.

   >[!NOTE]
   >Om du ännu inte har konfigurerat produktionsflödet för icke-produktion visas kortet *Översikt* där du kan skapa produktionsflödet.


## Visningsmiljö {#viewing-environment}

På **miljökortet** på sidan Översikt visas upp till tre miljöer.

1. Klicka på knappen **Visa alla** för att navigera till sammanfattningssidan för **miljön** för att visa en tabell med en fullständig lista över miljöer.

   ![](assets/environment-view-1.png)

1. På sidan **Miljö** visas en lista över alla befintliga miljöer.

   ![](assets/environment-view-2.png)

1. Välj någon av miljöerna i listan för att visa miljöinformationen.

   ![](assets/environment-view-3.png)


## Uppdaterar miljö {#updating-dev-environment}

Uppdateringar av scen- och produktionsmiljöer hanteras automatiskt av Adobe.

Uppdateringar av utvecklingsmiljöer hanteras av användarna av programmet. När en miljö inte kör den senaste allmänt tillgängliga AEM visar statusen för miljökortet på hemskärmen **UPDATE AVAILABLE (TILLGÄNGLIG**).

![](assets/environ-update.png)


Alternativet **Uppdatera** är tillgängligt från **miljökortet** .
Det här alternativet är också tillgängligt om du klickar på **Information** från **miljökortet** . Sidan **Miljö** öppnas och när du har valt utvecklingsmiljön klickar du på **...** och väljer **Uppdatera** enligt bilden nedan:

![](assets/environ-update2.png)

Om du väljer det här alternativet kan en Distributionshanterare uppdatera den pipeline som är associerad med den här miljön till den senaste versionen och sedan köra pipelinen.

Om pipeline redan har uppdaterats uppmanas användaren att köra pipelinen.

## Tar bort miljö {#deleting-environment}

Användare med nödvändig behörighet kan ta bort en utvecklingsmiljö.

Alternativet **Ta bort** finns i listrutan i **miljökortet** . Klicka på **..** för en utvecklingsmiljö som du vill ta bort.

![](assets/environ-delete.png)

Alternativet Ta bort är också tillgängligt om du klickar på **Information** på **miljökortet** . Sidan **Miljö** öppnas och när du har valt utvecklingsmiljön klickar du på **...** och väljer **Ta bort** enligt bilden nedan:

![](assets/environ-delete2.png)


>[!NOTE]
>
>Den här funktionen är inte tillgänglig för produktions-/scenmiljö som angetts i ett reguljärt program som konfigurerats för produktion. Funktionen är dock tillgänglig för produktions-/scenmiljöer i ett sandlådeprogram.

## Hantera åtkomst {#managing-access}

Välj **Hantera åtkomst** i listrutan i **miljökortet** . Du kan navigera till författarinstansen direkt och hantera åtkomsten för din miljö.

Mer information finns i [Hantera åtkomst till författarinstansen](/help/onboarding/getting-access-to-aem-in-cloud/navigation.md#manage-access-aem) .

![](assets/environ-access.png)


## Åtkomst till Developer Console {#accessing-developer-console}

Välj **Developer Console** i listrutan i **miljökortet** . Då öppnas en ny flik i webbläsaren med inloggningssidan på **Developer Console**.

Endast en användare i utvecklarrollen har åtkomst till **utvecklarkonsolen**. Undantaget är för sandlådeprogram, där alla användare med tillgång till Cloud Manager Sandbox Program har tillgång till **Developer Console**.

Mer information finns i [Viloläge och Viloläge i sandlådemiljöer](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/sandbox-programs.html#hibernating-introduction) .


![](assets/environ-devconsole.png)

Det här alternativet är också tillgängligt om du klickar på **Information** från **miljökortet** . Sidan **Miljö** öppnas och när du har valt en miljö klickar du på **...** och väljer **Developer Console**.

## Logga in lokalt {#login-locally}

Välj **Lokal inloggning** i listrutan i **miljökortet** om du vill logga in lokalt på Adobe Experience Manager.

![](assets/environ-login-locally.png)

Dessutom kan du logga in lokalt från sammanfattningssidan för **miljöer** .

![](assets/environ-login-locally-2.png)

