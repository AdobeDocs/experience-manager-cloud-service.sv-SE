---
title: 'Tilldela teammedlemmar till Cloud Manager-produktprofiler '
description: Följ den här sidan för att lära dig hur du tilldelar teammedlemmar till produktprofiler för Cloud Manager
hide: true
hidefromtoc: true
index: false
source-git-commit: 3dbcc5dd09479a84ed13aad0ee3d8c229520e10f
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 0%

---


# Tilldela teammedlemmar till Cloud Manager-produktprofiler {#assign-team-members}

När du har lärt dig att logga in på [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en) och visat dina behörigheter som [systemadministratör](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/system-administrator.html?lang=en) är du nu redo att tilldela teammedlemmar till Cloud Manager-produktprofiler.

## Syfte {#objective}

I det här dokumentet sammanfattas hur du tilldelar teammedlemmar till Cloud Manager-produktprofiler från Admin Console.

När du har läst det här avsnittet ska du kunna:

* Förstå varför och hur ni måste lägga till teammedlemmar.
* Lär dig mer om tre olika Cloud Manager-produktprofiler, som Business Owner, Deployment Manager och Developer.
* Tilldela teammedlemmar till Cloud Manager-produktprofiler som Business Owner, Deployment Manager och Developer.

## Förutsättningar {#prerequisites}

Innan du startar det här avsnittet bör du ta hänsyn till följande förutsättningar. Du måste vara en:

* En systemadministratör och förstår [Cloud Manager-produktprofiler](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).
* Förstå grunderna i [Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en).
* Måste ha information om dina teammedlemmar. En systemadministratör måste ha namn och e-postadresser samt roller och ansvar för de gruppmedlemmar som behöver åtkomst till AEM som Cloud Service.

   >[!NOTE]
   >För att komma igång rekommenderar vi att du först lägger till användare som ska delta i de omedelbara uppgifterna, till exempel administratörer, utvecklare och innehållsförfattare. Du kan fortsätta med resten av introduktionen utan att lägga till alla användare. När du är klar med introduktionen kan du skala till ett större antal användare senare.

## Granska produktprofiler för Cloud Manager {#review-product-profiles}

Från Admin Console kan du se en lista med Cloud Manager-profiler.

>[!NOTE]
>Innan du granskar produktprofilerna för Cloud Manager från Admin Console rekommenderar vi att du granskar de tillgängliga [produktprofilerna för Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).

Följ stegen nedan om du vill visa en lista med Cloud Manager-profiler:

1. Logga in på [Adobe Admin Console](https://adminconsole.adobe.com/). På sidan **Översikt** väljer du **Adobe Experience Manager som Cloud Service** på **kort för produkter och tjänster**.

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

   >[!NOTE]
   >Mer information om hur du använder Admin Console finns i Logga in i Admin Console.


1. Navigera till instansen **Cloud Manager** från tabellen med listan över alla instanser.

   ![](/help/onboarding/onboarding-journey/assets/assign-team2.png)

1. Du ser listan över förkonfigurerade [Cloud Manager-produktprofiler](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).

   ![](/help/onboarding/onboarding-journey/assets/assign-team3.png)


## Tilldela användare till företagsägarens produktprofil {#assign-users-business-owner}

Nu kan du lägga till användare och tilldela dem till produktprofilen för Cloud Manager Business Owner.

>[!NOTE]
>För att detta ska lyckas måste du från Adobe Admin Console lägga till en användare både i produkten (AEM som en Cloud Service i det här fallet) och i [produktprofilen för Cloud Manager Business Owner](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).

Följ de här stegen:

1. Identifiera de användare som ska hantera Cloud Manager-program och lägga till dem i produktprofilen för Business Owner. Systemadministratören måste vara den första personen som får åtkomst till och loggar in på Cloud Manager. Du måste lägga till dig själv (systemadministratör) till produktprofilen för Business Owner först.

1. På [Admin Console](https://adminconsole.adobe.com/enterprise/overview) **Översikt**-sidan väljer du **Adobe Experience Manager som en Cloud Service**-produkt från **Kort för produkter och tjänster** enligt nedan.

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

1. Välj fliken **Användare** i den översta navigeringen och välj sedan **Lägg till användare**.

   ![](/help/onboarding/onboarding-journey/assets/assign-team4.png)

1. I dialogrutan **Lägg till användare i ditt team** skriver du e-post-ID:t för den användare som du vill lägga till. För ID-typ väljer du Adobe ID om Federated ID för dina teammedlemmar inte har konfigurerats ännu.

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png)

1. I produktvalet väljer du **Adobe Experience Manager som Cloud Service** och tilldelar **Business Owner** produktprofil till användaren enligt nedan.

   >[!NOTE]
   >Se [Cloud Manager-produktprofiler](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) för att försäkra dig om att rätt användare tilldelas rätt roll(er) i Admin Console enligt nedan.

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png)

   >[!NOTE]
   >Tilldela användaren till minst en produktprofil så att användaren kan komma åt Cloud Manager. Kom ihåg att tilldela dig själv (systemadministratör) till Business Owner.

1. Klicka på **Spara**. Ett välkomstmeddelande skickas till användaren som du har lagt till. Den inbjudna användaren kan komma åt Cloud Manager genom att klicka på länken i välkomstmeddelandet och logga in med sin Adobe ID.

Grattis! Nu har ditt nybildade Cloud Manager-team, inklusive det du själv tilldelat rollen&quot;Business Owner&quot;, konfigurerats. Medlemmar får ett välkomstmejl där de bjuds in att logga in och öppna Cloud Manager. Som Business Owner är du nu bara ett steg från att logga in i Cloud Manager och göra det möjligt att skapa molnresurser.

## Tilldela användare till produktprofil för Distributionshanteraren {#assign-users-deployment-manager}

1. Identifiera de användare som ska hantera Cloud Manager-program och lägga till dem i produktprofilen för Deployment Manager. Systemadministratören måste vara den första personen som får åtkomst till och loggar in på Cloud Manager. Du måste lägga till dig själv (systemadministratör) till produktprofilen för Business Owner först.

1. På [Admin Console](https://adminconsole.adobe.com/enterprise/overview) **Översikt**-sidan väljer du **Adobe Experience Manager som en Cloud Service**-produkt från **Kort för produkter och tjänster** enligt nedan.

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

1. Välj fliken **Användare** i den översta navigeringen och välj sedan **Lägg till användare**.

   ![](/help/onboarding/onboarding-journey/assets/assign-team4.png)

1. I dialogrutan **Lägg till användare i ditt team** skriver du e-post-ID:t för den användare som du vill lägga till. För ID-typ väljer du Adobe ID om Federated ID för dina teammedlemmar inte har konfigurerats ännu.

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png)

1. I produkturvalet väljer du **Adobe Experience Manager som Cloud Service** och tilldelar **Distributionshanteraren** produktprofil till användaren enligt nedan.

   >[!NOTE]
   >Se [Cloud Manager-produktprofiler](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) för att försäkra dig om att rätt användare tilldelas rätt roll(er) i Admin Console enligt nedan.

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png).

   >[!IMPORTANT]
   >Användaren kan läggas till i distributionsledarens produktprofil när Cloud Manager-resurserna har skapats.

## Tilldela användare till produktprofil för utvecklare {#assign-users-developer}

1. Identifiera de användare som ska hantera Cloud Manager-program och lägga till dem i Developer-produktprofilen. Systemadministratören måste vara den första personen som får åtkomst till och loggar in på Cloud Manager. Du måste lägga till dig själv (systemadministratör) till produktprofilen för Business Owner först.

1. På [Admin Console](https://adminconsole.adobe.com/enterprise/overview) **Översikt**-sidan väljer du **Adobe Experience Manager som en Cloud Service**-produkt från **Kort för produkter och tjänster** enligt nedan.

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

1. Välj fliken **Användare** i den översta navigeringen och välj sedan **Lägg till användare**.

   ![](/help/onboarding/onboarding-journey/assets/assign-team4.png)

1. I dialogrutan **Lägg till användare i ditt team** skriver du e-post-ID:t för den användare som du vill lägga till. För ID-typ väljer du Adobe ID om Federated ID för dina teammedlemmar inte har konfigurerats ännu.

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png)

1. I produkturvalet väljer du **Adobe Experience Manager som Cloud Service** och tilldelar **Developer** produktprofil till användaren enligt nedan.

   >[!NOTE]
   >Se [Cloud Manager-produktprofiler](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) för att försäkra dig om att rätt användare tilldelas rätt roll(er) i Admin Console enligt nedan.

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png).


   >[!IMPORTANT]
   >Användare kan läggas till i produktprofilen för utvecklare när Cloud Manager-resurser har skapats.

## What’s Next {#whats-next}

Som systemadministratör tilldelad rollen *Business Owner* måste du komma åt och logga in i Cloud Manager.
>[!NOTE]
>Läs [Navigera till Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/navigate-to-cloud-manager.html?lang=en) om du vill veta mer om hur du loggar in och använder Cloud Manager.

En Cloud Manager-användare i rollen Business Owner kan logga in och konfigurera dina molnresurser, inklusive dina program och miljöer. På så sätt kan ditt expertteam börja använda AEM som Cloud Service så snart som möjligt.
När din Business Owner har konfigurerat dina molnresurser kan utvecklare och distributionsansvariga som har lagts till i Cloud Manager-produktprofilerna få åtkomst till Cloud Manager och inhämta kunskap om hur de kan fortsätta med sin utbildningsväg.

## Ytterligare resurser {#additional-resources}

Följ de andra resurserna för att lära dig mer om:

* [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=en)
* [Produktprofiler för Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)
* [Admin Console Identity Overview](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html)
