---
title: 'Tilldela teammedlemmar till Cloud Manager-produktprofiler '
description: Följ den här sidan för att lära dig hur du tilldelar teammedlemmar till produktprofiler för Cloud Manager
hide: true
hidefromtoc: true
index: false
source-git-commit: 8b30fc9494e152aa742cf17c02f982f5c9479473
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 0%

---


# Tilldela teammedlemmar till Cloud Manager-produktprofiler {#assign-team-members}

När du har lärt dig att logga in på Admin Console och visat dina behörigheter som systemadministratör kan du nu tilldela teammedlemmar till produktprofiler för Cloud Manager.

## Syfte {#objective}

I det här dokumentet sammanfattas hur du tilldelar teammedlemmar till Cloud Manager-produktprofiler från Admin Console.

När du har läst det här avsnittet ska du kunna:

* Förstå varför och hur ni måste lägga till teammedlemmar.
* Lär dig mer om tre olika Cloud Manager-produktprofiler, som Business Owner, Deployment Manager och Developer.
* Tilldela teammedlemmar till Cloud Manager-produktprofiler (Business Owner, Deployment Manager och Developer).

## Granska produktprofiler för Cloud Manager {#review-product-profiles}

Från Admin Console kan du se en lista med Cloud Manager-profiler.

>[!NOTE]
>Innan du granskar Cloud Manager-produktprofilerna från Admin Console rekommenderar vi att du granskar de tillgängliga produktprofilerna för Cloud Manager.

Följ stegen nedan om du vill visa en lista med Cloud Manager-profiler:

1. Logga in på Adobe Admin Console. På sidan **Översikt** väljer du Adobe Experience Manager som en molntjänst från kortet Produkter och tjänster.

   >[!NOTE]
   >Mer information om hur du använder Admin Console finns i Logga in i Admin Console.


1. Navigera till molnhanterarinstansen från tabellen med listan över alla instanser. Du ser en lista över förkonfigurerade Cloud Manager-produktprofiler.


## Tilldela användare till företagsägarens produktprofil {#assign-users-business-owner}

Nu kan du lägga till användare och tilldela dem till produktprofilen för Cloud Manager Business Owner.

För att detta ska lyckas måste du från Adobe Admin Console lägga till en användare både i produkten (AEM som en Cloud Service i det här fallet) och i Cloud Manager Business Owner-produktprofilen.

Följ de här stegen:

1. Identifiera de användare som ska hantera Cloud Manager-program och lägga till dem i produktprofilen för Business Owner. Systemadministratören måste vara den första personen som får åtkomst till och loggar in på Cloud Manager. Du måste lägga till dig själv (systemadministratör) till produktprofilen för Business Owner först.

1. På sidan Översikt över Admin Console väljer du Adobe Experience Manager som en Cloud Service av produkter och tjänstekort enligt nedan:

1. Välj fliken Användare i den övre navigeringen och välj sedan Lägg till användare.

1. I dialogrutan Lägg till användare skriver du e-post-ID:t för den användare som du vill lägga till. För ID-typ väljer du Adobe ID om Federated ID för dina teammedlemmar inte har konfigurerats ännu.

1. I produktvalet väljer du&quot;Adobe Experience Manager som Cloud Service&quot; och tilldelar produktprofilen&quot;Business Owner&quot; till användaren enligt nedan. Se produktprofilerna för Cloud Manager för att se till att rätt användare tilldelas rätt roll(er) i Admin Console enligt nedan.

1. Tilldela användaren till minst en produktprofil så att användaren kan komma åt Cloud Manager. Kom ihåg att tilldela dig själv (systemadministratör) till&quot;Affärsägare&quot;.

1. Klicka på Spara. Ett välkomstmeddelande skickas till användaren som du har lagt till. Den inbjudna användaren kan komma åt Cloud Manager genom att klicka på länken i välkomstmeddelandet och logga in med sin Adobe ID.

Grattis! Nu har ditt nybildade Cloud Manager-team, inklusive det du själv tilldelat rollen&quot;Business Owner&quot;, konfigurerats. Medlemmar får ett välkomstmejl där de bjuds in att logga in och öppna Cloud Manager. Som Business Owner är du nu bara ett steg från att logga in i Cloud Manager och göra det möjligt att skapa molnresurser.

## Tilldela användare till produktprofilen för Distributionshanteraren {#assign-users-deployment-manager}

1. Identifiera de användare som ska hantera Cloud Manager-program och lägga till dem i produktprofilen för Business Owner. Systemadministratören måste vara den första personen som får åtkomst till och loggar in på Cloud Manager. Du måste lägga till dig själv (systemadministratör) till produktprofilen för Business Owner först.

1. På sidan Översikt över Admin Console väljer du Adobe Experience Manager som en Cloud Service av produkter och tjänstekort enligt nedan:

1. Välj fliken Användare i den övre navigeringen och välj sedan Lägg till användare.

1. I dialogrutan Lägg till användare skriver du e-post-ID:t för den användare som du vill lägga till. För ID-typ väljer du Adobe ID om Federated ID för dina teammedlemmar inte har konfigurerats ännu.

1. I produktvalet väljer du&quot;Adobe Experience Manager som Cloud Service&quot; och tilldelar produktprofilen&quot;Deployment Manager&quot; till användaren enligt nedan. Se produktprofilerna för Cloud Manager för att se till att rätt användare tilldelas rätt roll(er) i Admin Console enligt nedan.

   >[!NOTE]
   >Användaren kan läggas till i distributionsledarens produktprofil när Cloud Manager-resurserna har skapats.

## Tilldela användare till produktprofil för utvecklare {#assign-users-developer}

1. Identifiera de användare som ska hantera Cloud Manager-program och lägga till dem i produktprofilen för Business Owner. Systemadministratören måste vara den första personen som får åtkomst till och loggar in på Cloud Manager. Du måste lägga till dig själv (systemadministratör) till produktprofilen för Business Owner först.

1. På sidan Översikt över Admin Console väljer du Adobe Experience Manager som en Cloud Service av produkter och tjänstekort enligt nedan:

1. Välj fliken Användare i den övre navigeringen och välj sedan Lägg till användare.

1. I dialogrutan Lägg till användare skriver du e-post-ID:t för den användare som du vill lägga till. För ID-typ väljer du Adobe ID om Federated ID för dina teammedlemmar inte har konfigurerats ännu.

1. Välj&quot;Adobe Experience Manager som Cloud Service&quot; och tilldela&quot;Developer&quot; produktprofil till användaren enligt nedan. Se produktprofilerna för Cloud Manager för att se till att rätt användare tilldelas rätt roll(er) i Admin Console enligt nedan.

   >[!NOTE]
   >Användare kan läggas till i produktprofilen för utvecklare när Cloud Manager-resurser har skapats.

## What’s Next {#whats-next}

Som systemadministratör tilldelad rollen *Business Owner* måste du komma åt och logga in i Cloud Manager.
>[!NOTE]
>Mer information om hur du loggar in och använder Cloud Manager finns i Navigera till Cloud Manager.

En Cloud Manager-användare i rollen Business Owner kan logga in och konfigurera dina molnresurser, inklusive dina program och miljöer. På så sätt kan ditt expertteam börja använda AEM som Cloud Service så snart som möjligt.
När din Business Owner har konfigurerat dina molnresurser kan utvecklare och distributionsansvariga som har lagts till i Cloud Manager-produktprofilerna få åtkomst till Cloud Manager och inhämta kunskap om hur de kan fortsätta med sin utbildningsväg.

## Ytterligare resurser {#additional-resources}

Följ de andra resurserna för att lära dig mer om:

* Cloud Manager
* Produktprofiler för Cloud Manager
* Admin Console Identity Overview
