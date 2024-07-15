---
title: Meddelandeprofiler
description: Lär dig hur du skapar användarprofiler i Admin Console för att hantera mottagning av viktiga e-postmeddelanden.
feature: Onboarding
role: Admin, User, Developer
exl-id: 4edecfcd-6301-4a46-98c7-eb5665f48995
source-git-commit: 53a3a4c47becf58f8874083e2878fa3458d6cad7
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 0%

---


# Meddelandeprofiler {#notification-profiles}

Lär dig hur du skapar användarprofiler i Admin Console för att hantera mottagning av viktiga e-postmeddelanden.

## Ökning {#overview}

Adobe kontaktar då och då användare av AEM as a Cloud Service. Förutom meddelanden i produkten använder Adobe ibland även e-post för meddelanden. Det finns två typer av sådana e-postmeddelanden:

* **Incidentmeddelande** - Dessa meddelanden skickas under en incident eller när Adobe har identifierat ett potentiellt tillgänglighetsproblem i din AEM as a Cloud Service-miljö.
* **Proaktiv avisering** - Dessa aviseringar skickas när en medlem i Adobe support vill ge vägledning om en eventuell optimering eller rekommendation som kan vara till nytta för din AEM as a Cloud Service-miljö.

Användarna kan också få dessa meddelanden för specifika program baserat på deras [anpassade gruppbehörigheter.](/help/implementing/cloud-manager/custom-permissions.md)

Dessutom stöds det att tilldela grupper till proaktiva meddelanden, och användare och grupper kan tilldelas produktprofiler direkt.

* Användare i incidentgruppen och den förebyggande meddelandegruppen får som standard meddelanden om alla program.
* Om användare inte vill få alla meddelanden kan de använda anpassade READ-behörigheter för att ange vilka programmeddelanden de vill få.

För att rätt användare ska kunna ta emot dessa meddelanden måste du konfigurera och tilldela användarprofiler enligt beskrivningen i det här dokumentet.

## Förutsättningar {#prerequisites}

Eftersom användarprofiler skapas och underhålls i Admin Console måste du göra följande innan du skapar profiler för meddelanden:

* Har behörighet att lägga till och profilera medlemskap.
* Har en giltig Adobe Admin Console-profil.

## Skapa nya Cloud Manager produktprofiler {#create-profiles}

Skapa två användarprofiler för att konfigurera mottagning av meddelanden på rätt sätt. De här stegen utförs bara en gång.

1. Logga in i Admin Console på [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. Se till att du är i rätt organisation.

1. På sidan **Översikt** väljer du **Adobe Experience Manager as a Cloud Service** från kortet **Produkter och tjänster**.

   ![Lista över produkter och tjänster i Admin Console](assets/products_services.png)

1. Navigera till **Cloud Manager**-instansen från listan med alla instanser.

   ![Lista över instanser i Admin Console](assets/cloud_manager_instance.png)

1. Du kan se en lista över alla konfigurerade Cloud Manager-produktprofiler.

   ![Produktprofiler på Admin Console](assets/cloud_manager_profiles.png)

1. Klicka på **Ny profil** och ange följande information:

   * **Produktprofilnamn**: `Incident Notification - Cloud Service`
   * **Visningsnamn**: `Incident Notification - Cloud Service`
   * **Beskrivning**: Cloud Manager-profil för de användare som ska få meddelanden under en incident eller när Adobe har identifierat ett potentiellt tillgänglighetsproblem i din AEM as a Cloud Service-miljö.
      * Användare med anpassade READ-behörigheter för särskilda program får endast meddelanden för de programmen om de väljer att använda anpassade behörigheter.

1. Klicka på **Spara**.

1. Klicka på **Ny profil** en gång till och ange följande information:

   * **Produktprofilnamn**: `Proactive Notification - Cloud Service`
   * **Visningsnamn**: `Proactive Notification - Cloud Service`
   * **Beskrivning**: Cloud Manager-profil för de användare som får meddelanden när en medlem i supportgruppen på Adobe vill ge vägledning om en eventuell optimering eller rekommendationer som ska utföras med AEM as a Cloud Service-miljökonfigurationen
      * Användare med anpassade READ-behörigheter för särskilda program får endast meddelanden för de programmen om de väljer att använda anpassade behörigheter.

1. Klicka på **Spara**.

De två nya meddelandeprofilerna skapas.

>[!NOTE]
>
>Det är viktigt att Cloud Manager **produktprofilnamn** är exakt samma som angivet. Kopiera och klistra in det angivna produktprofilnamnet för att undvika fel. Eventuella avvikelser eller skrivfel leder till att meddelanden inte skickas som du vill.
>
>Om ett fel uppstår eller om profilerna inte har definierats kommer Adobe som standard att meddela befintliga användare som har tilldelats **Cloud Manager Developer**- eller **Deployment Manager**-profilerna.

## Tilldela användare till meddelandeprofiler {#add-users}

Nu när profilerna har skapats måste du tilldela rätt användare. Du kan göra detta när du skapar nya användare eller genom att uppdatera befintliga användare.

### Lägg till nya användare i profiler {#new-user}

Följ de här stegen för att lägga till användare för vilka Federated ID ännu inte har konfigurerats.

1. Identifiera de användare eller grupper som ska få incidentmeddelanden eller proaktiva meddelanden.

1. Logga in på Admin Console på [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com) om du inte fortfarande är inloggad.

1. Se till att du har valt rätt organisation.

1. På sidan **Översikt** väljer du **Adobe Experience Manager as a Cloud Service** från kortet **Produkter och tjänster**.

   ![Användare](assets/product_services.png)

1. Om det federerade ID:t för dina teammedlemmar ännu inte har konfigurerats väljer du fliken **Användare** i den översta navigeringen och sedan **Lägg till användare**. Hoppa annars till avsnittet [Lägg till befintliga användare i profiler.](#existing-users)

   ![Användare](assets/cloud_manager_add_user.png)

1. I dialogrutan **Lägg till användare i ditt team** anger du e-post-ID för den användare som du vill lägga till och väljer `Adobe ID` som **ID-typ**.

1. Klicka på plusknappen under rubriken **Välj produkter** för att börja produktvalet.

1. Välj **Adobe Experience Manager as a Cloud Service** och tilldela en eller båda de nya profilerna till användaren.

   * **Incidentmeddelande - Cloud Service**
   * **Proaktivt meddelande - Cloud Service**

1. Klicka på **Spara** och ett välkomstmeddelande skickas till användaren som du lade till.

Den inbjudna användaren får nu meddelanden. Användare med anpassade READ-behörigheter för särskilda program får endast meddelanden för de programmen om de väljer att använda anpassade behörigheter.

Upprepa de här stegen för de användare i ditt team som du vill ska få meddelanden om.

### Lägg till befintliga användare i profiler {#existing-user}

Följ de här stegen för att lägga till användare för vilka det redan finns Federated ID.

1. Identifiera de användare eller grupper som ska få incidentmeddelanden eller proaktiva meddelanden.

1. Logga in på Admin Console på [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com) om du inte fortfarande är inloggad.

1. Se till att du har valt rätt organisation.

1. På sidan **Översikt** väljer du **Adobe Experience Manager as a Cloud Service** från kortet **Produkter och tjänster**.

1. Välj fliken **Användare** i den övre navigeringen.

1. Om det federerade ID:t redan finns för den teammedlem som du vill lägga till i en meddelandeprofil letar du reda på användaren i listan och klickar på den. Hoppa annars till avsnittet [Lägg till nya användare i profiler.](#add-user)

1. Klicka på ellipsknappen i avsnittet **Produkter** i fönstret med användarinformation och välj sedan **Redigera**.

1. I fönstret **Redigera produkter** klickar du på pennknappen under rubriken **Välj produkter** för att börja produktvalet.

1. Välj **Adobe Experience Manager as a Cloud Service** och tilldela en eller båda de nya profilerna till användaren.

   * **Incidentmeddelande - Cloud Service**
   * **Proaktivt meddelande - Cloud Service**

1. Klicka på **Spara** och ett välkomstmeddelande skickas till användaren som du lade till.

Den inbjudna användaren får nu meddelanden. Användare med anpassade READ-behörigheter för särskilda program får endast meddelanden för de programmen om de väljer att använda anpassade behörigheter.

Upprepa de här stegen för de användare i ditt team som du vill ska få meddelanden om.

## Ytterligare resurser {#additional-resources}

Här följer ytterligare, valfria resurser om du vill gå längre än vad som ingår i introduktionsresan.

* [Åtgärdscenter](/help/operations/actions-center.md) - Utnyttja åtgärdscentret för att enkelt hantera incidenter och annan viktig information.
