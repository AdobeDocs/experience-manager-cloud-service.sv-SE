---
title: Hantera miljöer - Cloud Service
description: Hantera miljöer - Cloud Service
exl-id: 93fb216c-c4a7-481a-bad6-057ab3ef09d3
source-git-commit: c4e788527ab0be8b54f9a0baed2e4e2677129898
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 3%

---

# Hantera miljöer {#manage-environments}

I följande avsnitt beskrivs de typer av miljö som en användare kan skapa och hur användaren kan skapa en miljö.

## Miljötyper {#environment-types}

En användare med nödvändig behörighet kan skapa följande miljötyper (inom gränserna för vad som är tillgängligt för den specifika klientorganisationen).

* **Produktions- och scenmiljö**: Produktionen och scenen finns som duo och används för testning och produktion.

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

1. Klicka på **Lägg till miljö** för att lägga till en miljö. Den här knappen kommer att vara tillgänglig från skärmen **Environment**.
   ![](assets/environments-tab.png)

   Alternativet **Lägg till miljö** finns också på **miljökortet** när det inte finns några miljöer i programmet.

   ![](assets/no-environments.png)

   >[!NOTE]
   >Alternativet **Lägg till miljö** inaktiveras beroende på brist på behörigheter eller vad som kan komma att skrivas under.

1. Dialogrutan **Lägg till miljö** visas. Användaren måste skicka in information som **miljötyp**, **miljönamn** och **miljöbeskrivning** (beroende på vad användaren har för mål med att skapa miljön inom gränserna för vad som är tillgängligt för den specifika klientorganisationen).

   ![](assets/add-environment2.png)

   >[!NOTE]
   >När du skapar en miljö skapas en eller flera *integreringar* i Adobe I/O. De är synliga för kundanvändare som har åtkomst till Adobe I/O Console och får inte tas bort. Detta tas inte med i beskrivningen i Adobe I/O Console.

   ![](assets/add-environment-image1.png)

1. Klicka på **Spara** om du vill lägga till en miljö med de ifyllda villkoren.  Nu visar skärmen *Översikt* kortet från vilket du kan konfigurera din pipeline.

   >[!NOTE]
   >Om du ännu inte har konfigurerat produktionsflödet för icke-produktion visas kortet där du kan skapa produktionsflödet på skärmen *Översikt*.

## Miljöinformation {#viewing-environment}

Kortet **Environment** på sidan Översikt visar upp till tre miljöer.

1. Välj knappen **Visa alla** för att navigera till sammanfattningssidan för **Miljö** för att visa en tabell med en fullständig lista över miljöer.

   ![](assets/environment-view-1.png)

1. Sidan **Miljöer** visar en lista över alla befintliga miljöer.

   ![](assets/environment-view-2.png)

1. Välj någon av miljöerna i listan för att visa miljöinformationen.

   >[!NOTE]
   >Förhandsgranskningstjänsten kommer att distribueras rullande till alla program. Kunder meddelas i produkten när deras program är aktiverat för förhandsgranskningstjänsten. Mer information finns i avsnittet [Accessing Preview Service](#access-preview-service).

   ![](assets/environ-preview1.png)


### Åtkomst till förhandsgranskningstjänsten {#access-preview-service}

Förhandsgranskningstjänsten ger varje AEM en extra tjänst för förhandsgranskning (publicering) som en Cloud Service via Cloud Manager.

Förhandsgranska webbplatsens slutliga upplevelse innan den når publiceringsmiljön och är tillgänglig för allmänheten. Några punkter innan du kan se och använda förhandsgranskningstjänsten:

1. **AEM version**: Miljön måste vara i AEM version  `2021.5.5343.20210542T070738Z` eller senare. Kontrollera att en uppdateringsprocess har körts i miljön för att slutföra detta.

1. **Standardlås** för IP-Tillåtelselista: När du skapar programmet för första gången måste du aktivt ta bort det förinställda IP-Tillåtelselista från förhandsgranskningstjänsten i miljön för att kunna aktivera åtkomst.

   En användare med nödvändig behörighet måste göra något av följande för att *låsa upp* åtkomst till förhandsgranskningstjänsten och ge önskad åtkomst:

   * Skapa ett lämpligt IP-Tillåtelselista och använd det på förhandsgranskningstjänsten. Följ detta omedelbart genom att ta bort `Preview Default [Env ID] IP Allow List` från förhandsgranskningstjänsten.

      *ELLER*,

   * Använd arbetsflödet för uppdatering av IP Tillåtelselista för att ta bort standard-IP och lägga till IP:n efter behov. Mer information finns i [Visa och uppdatera en IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/view-update-ip-allow-list.md).

      >[!NOTE]
      >Ovanstående steg måste utföras innan du kan dela URL:en för förhandsgranskningstjänsten med någon av dina team för att säkerställa att rätt medlemmar i ditt team kan komma åt URL:en för förhandsgranskningen.

      När åtkomsten till förhandsgranskningstjänsten har låsts upp visas inte längre låsikonen, vilket visas nedan.

      ![](/help/implementing/cloud-manager/assets/preview-service1.png)

1. **Publicera innehåll för förhandsgranskning**: Du kan publicera innehåll i förhandsgranskningstjänsten med hjälp av gränssnittet Hantera publikation i AEM. Mer information finns i [Förhandsgranska innehåll](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/fundamentals/previewing-content.html?lang=en).

## Uppdaterar miljön {#updating-dev-environment}

Uppdateringar av scen- och produktionsmiljöer hanteras automatiskt av Adobe.

Uppdateringar av utvecklingsmiljöer hanteras av användarna av programmet. När en miljö inte kör den senaste allmänt tillgängliga AEM visar statusen på miljökortet på hemskärmen **UPDATE AVAILABLE**.

![](assets/environ-update.png)


Alternativet **Uppdatera** är tillgängligt på kortet **Environment**.
Det här alternativet är också tillgängligt om du klickar på **Information** från **miljökortet**. Sidan **Environment** öppnas och när du har valt utvecklingsmiljön klickar du på **..** och välj **Uppdatera** enligt bilden nedan:

![](assets/environ-update2.png)

Om du väljer det här alternativet kan en Distributionshanterare uppdatera den pipeline som är associerad med den här miljön till den senaste versionen och sedan köra pipelinen.

Om pipeline redan har uppdaterats uppmanas användaren att köra pipelinen.

## Tar bort miljö {#deleting-environment}

Användare med nödvändig behörighet kan ta bort en utvecklingsmiljö.

Alternativet **Ta bort** finns i listrutan på kortet **Environment**. Klicka på **..** för en utvecklingsmiljö som du vill ta bort.

![](assets/environ-delete.png)

Alternativet Ta bort är också tillgängligt om du klickar på **Information** från **miljökortet**. Sidan **Environment** öppnas och när du har valt utvecklingsmiljön klickar du på **..** och välj **Ta bort** enligt bilden nedan:

![](assets/environ-delete2.png)


>[!NOTE]
>Den här funktionen är inte tillgänglig för produktions-/scenmiljö som angetts i ett produktionsprogram som konfigurerats för produktionsändamål. Funktionen är dock tillgänglig för produktions-/scenmiljöer i ett sandlådeprogram.

## Hantera åtkomst {#managing-access}

Välj **Hantera åtkomst** i listrutan på kortet **Miljö**. Du kan navigera till författarinstansen direkt och hantera åtkomsten för din miljö.

Mer information finns i [Hantera åtkomst till författarinstansen](/help/onboarding/what-is-required/accessing-aem-instance.md).

![](assets/environ-access.png)


## Åtkomst till Developer Console {#accessing-developer-console}

Välj **Developer Console** i listrutan på kortet **Environment**. Då öppnas en ny flik i webbläsaren med inloggningssidan till **Developer Console**.

Endast en användare i utvecklarrollen har åtkomst till **utvecklarkonsolen**. Undantaget är för sandlådeprogram, där alla användare med åtkomst till Cloud Manager Sandbox Program har åtkomst till **Developer Console**.

Mer information finns i [Viloläge och Viloläge i sandlådemiljöer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/sandbox-programs.html#hibernating-introduction).


![](assets/environ-devconsole.png)

Det här alternativet är också tillgängligt om du klickar på **Information** från **miljökortet**. Sidan **Environment** öppnas och när du har valt en miljö klickar du på **..** och välj **Developer Console**.

## Logga in lokalt {#login-locally}

Välj **Lokal inloggning** i listrutan på **miljökortet** om du vill logga in lokalt på Adobe Experience Manager.

![](assets/environ-login-locally.png)

Dessutom kan du logga in lokalt från sammanfattningssidan **Miljöer**.

![](assets/environ-login-locally-2.png)


## Hantera anpassade domännamn {#manage-cdn}

Gå till informationssidan för **Miljöer** från sidan Miljösammanfattning.

>[!NOTE]
>Anpassade domännamn stöds nu i Cloud Manager för webbplatser-program för både publicerings- och förhandsgranskningstjänster. Varje Cloud Manager-miljö har plats för upp till 250 anpassade domäner per miljö.

Följande åtgärder kan utföras på publiceringstjänsten för din miljö enligt beskrivningen nedan:

1. [Lägga till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

1. [Visa och uppdatera ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md)

1. [Ta bort ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)

1. [Kontrollerar status för anpassat ](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) domännamn eller ett  [SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn).

1. [Kontrollerar status för ett IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)


## Hantera IP-Tillåtelselista {#manage-ip-allow-lists}

Gå till sidan Miljöinformation från sidan Miljösammanfattning. Du kan utföra följande åtgärder på tjänsterna Publicera och/eller Författare för din miljö här.

>[!NOTE]
>Funktionen IP Tillåtelselista stöds nu i Cloud Manager för författar-, publicerings- och förhandsgranskningstjänster (finns i webbplatsprogram).

### Använda en IP-Tillåtelselista {#apply-ip-allow-list}

Att använda en IP-Tillåtelselista är den process genom vilken alla IP-intervall som ingår i definitionen av Tillåt-lista kopplas till en författare eller publiceringstjänst i en miljö. En användare i rollen Business Owner eller Deployment Manager måste vara inloggad för att det ska gå att använda IP Tillåtelselista.

>[!NOTE]
>IP-Tillåtelselista måste finnas i Cloud Manager för att det ska kunna användas på en miljötjänst. Om du vill veta mer om IP Tillåtelselista i Cloud Manager går du till [Introduktion till IP Tillåtelselista i Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

Följ stegen nedan för att använda ett IP-Tillåtelselista:

1. Navigera till den specifika miljön från informationssidan **Environment** och navigera till tabellen **IP Tillåtelselista**.
1. Använd inmatningsfälten högst upp i IP Tillåtelselista-tabellen för att välja IP Tillåtelselista och författaren eller publiceringstjänsten som du vill använda den på.
1. Klicka på **Använd** och bekräfta ditt bidrag.

### Tar bort en IP-Tillåtelselista {#unapply-ip-allow-list}

Om du inte använder en IP-Tillåtelselista är det den process där alla IP-intervall som ingår i definitionen av Tillåtelselista inte är kopplade till en författare eller utgivartjänst i en miljö. En användare i rollen Business Owner eller Deployment Manager måste vara inloggad för att du ska kunna Ångra en IP-Tillåtelselista.

Följ stegen nedan för att ta bort en IP-Tillåtelselista:

1. Gå till den specifika **miljöinformationssidan**-informationssidan från skärmen Miljö och navigera till tabellen **IP Tillåtelselista**.
1. Identifiera raden där den IP Tillåtelselista-regel som du vill ta bort är listad.
1. Välj **..**-menyn längst till höger på raden.
1. Välj alternativet **Ta bort tillämpning** och bekräfta överföringen.
