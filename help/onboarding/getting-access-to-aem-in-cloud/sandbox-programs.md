---
title: Sandlådeprogram - molntjänst
description: Sandlådeprogram - molntjänst
translation-type: tm+mt
source-git-commit: eb874176c71d7f3d03d953f7bae4cb3db2ffb3b9
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---


# Sandlådeprogram {#sandbox-programs}

## Introduktion {#introduction}

Ett sandlådeprogram är ett av de två typer av program som är tillgängliga i AEM Cloud Service, och det andra är ett vanligt program.

En sandlåda skapas vanligtvis för utbildning, löpande demos, aktivering eller POC. De är inte avsedda att bära livstrafik.

Sandlådeprogram innehåller Sites and Assets och levereras automatiskt ifyllda med en Git-gren som innehåller exempelkod, en utvecklingsmiljö och en icke-produktionsprocess.

Mer information om programtyper finns i [Förstå program och programtyper](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html).

### Attribut för sandlådeprogram {#attributes-sandbox}

Sandlådeprogram har följande attribut:

1. **Skapa program:** När du skapar sandlådeprogram skapas följande automatiska funktioner:
   * konfiguration av projekt med exempelkod och innehåll
   * utvecklingsmiljö
   * Skapande av icke-produktionsförlopp för distribution till utvecklingsmiljö (huvudgren för distribution till utvecklingsmiljö)

1. **Lösningar som ingår:** Sandlådeprogram innehåller Sites and Assets.

1. **AEM-uppdateringar:** AEM-uppdateringar kan användas manuellt i miljöer i ett sandlådeprogram och skickas inte automatiskt.

1. **Viloläge:** Miljöer i ett sandlådeprogram försätts i viloläge automatiskt om ingen aktivitet identifieras under en viss tid. Vilolägen miljöer kan avaktiveras manuellt.

### Skapa ett sandlådeprogram {#creating-sandbox-program}

En guide för att skapa program ber användaren att skicka in information.

Mer information om hur du skapar ett sandlådeprogram finns i [Skapa ett sandlådeprogram](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/creating-a-program.html#create-demo-program).

### Skapa sandlådemiljöer {#creating-sandbox-environments}

Sandlådeprogram levereras i en utvecklingsmiljö när programmet skapas automatiskt. Utvecklingsmiljön levereras med en författare och en publiceringsnivå som standard.

Miljöuppsättningen för produktionsscenen kan läggas till manuellt i sandlådeprogrammet när användaren är redo att ställa in en produktionspipeline.

Mer information om hur du skapar en miljö manuellt finns i [Lägga till miljöer](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments).

### Tar bort sandlådemiljöer  {#deleting-sandbox-environments}

Användare med nödvändig behörighet kan ta bort miljö/uppsättningar för utveckling eller produktion/scen.

Mer information om hur du tar bort en miljö finns i Ta [bort miljöer](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#deleting-environment).


## Viloläge och avvänjningsmiljöer för sandlådor {#hibernating-introduction}

Sandlådeprogrammiljöer försätts i *viloläge* efter en tids inaktivitet.

>[!NOTE]
>Viloläge är unikt för sandlådeprogrammiljöer. Regelbundna programmiljöer kommer inte att döljas.

### Viloläge {#hibernation-introduction}

Viloläge kan antingen inträffa automatiskt eller manuellt. Det kan ta upp till några minuter innan en miljö har viloläge. Data bevaras under viloläge.

Viloläge kategoriseras som:

* **Automatiska** sandlådeprogrammiljöer försätts automatiskt i viloläge efter åtta timmars inaktivitet, vilket innebär att varken författaren eller publiceringstjänsten får en begäran.

* **Manuell**: Kunder kan manuellt förlägga en sandlådeprogrammiljö i viloläge, men det finns inget krav på detta eftersom viloläge inträffar automatiskt efter en inaktivitetsperiod.

#### Använda manuell viloläge {#using-manual-hibernation}


Manuell viloläge kan utföras från någon av två skärmar i utvecklarkonsolen.

Följ stegen nedan för att manuellt gå i viloläge för programmiljöer:

1. Gå till Developer Console.
1. Klicka på Viloläge
1. Bekräfta genom att klicka på Viloläge.
1. När viloläget är klart visas följande skärm.
1. På listskärmen för miljön, som visas nedan och som du kommer åt genom att klicka på länken Miljö från miljöinformationsskärmen, kan du klicka på knappen för viloläge i den avsedda miljön. Därefter visas en bekräftelseskärm.

### Avviloläge {#de-hibernation-introduction}

>[!IMPORTANT]
>Åtkomst till Developer Console definieras av molnhanteraren - utvecklarrollen i Admin Console. Med den behörigheten kan användaren avaktivera en miljö i viloläge.

### Åtkomst till en miljö i viloläge {#accessing-hibernated-environment}

När användaren gör en webbläsarbegäran mot antingen författaren eller publiceringsskiktet i en miljö i viloläge, kommer användaren att få en landningssida som beskriver miljöns viloläge, vilket visas nedan:

En användare som har molnhanteraren - utvecklarrollen kan klicka på knappen för utvecklarkonsolen för att komma åt utvecklarkonsolen och för att avplacera miljön. Information om hur du anger roller finns i dokumentationen för Cloud Manager.

Om en användare i en organisation inte kan klicka på knappen Developer Console för att komma till Developer Console, är det troligt att de måste få rollen&quot;Cloud Manager - Utvecklare&quot;.




## AEM-uppdateringar i sandlådemiljöer {#aem-updates-sandbox}


Se [AEM-versionsuppdateringar](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#version-updates).

Användaren kan manuellt tillämpa AEM-uppdateringar på miljöer i ett sandlådeprogram (se figur nedan). Detta kan göras när statusen som visas är UPPDATERING TILLGÄNGLIG. Uppdateringsalternativet är tillgängligt i listrutan på miljökortet. Den kan också väljas på menyn Hantera på skärmen MILJÖER.

>[!NOTE]
>En icke-produktionspipeline som distribueras till den aktuella utvecklingsmiljön måste konfigureras för att en manuell uppdateringsprocess ska kunna initieras.

>[!NOTE]
>En produktionspipeline måste konfigureras för att en manuell uppdateringspipeline till Production+Stage-miljö ska kunna startas.

>[!NOTE]
>Manuell uppdatering av antingen Production- eller Stage-miljön uppdaterar automatiskt den andra. Miljöuppsättningen Production+Stage måste finnas i samma AEM-version.





