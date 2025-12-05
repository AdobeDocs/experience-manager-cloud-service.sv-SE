---
title: Databasläsare
seo-title: Repository Browser
description: Databasens webbläsare ger en skrivskyddad vy i databasen för alla miljöer på författar-, publicerings- och förhandsgranskningsnivåer.
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
feature: Developing
role: Admin, Developer
source-git-commit: 414608955bce3feebd1249a91e4f77161144e51e
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 0%

---

# Databasläsare {#repository-browser}

>[!NOTE]
>
>Databasläsaren är tillgänglig i AEM version 6582 och senare.

>[!INFO]
>
>Du kan även titta på [det här klippet](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=sv-SE) för att få en snabb videointroduktion om hur du använder Databasläsaren för att felsöka AEM as a Cloud Service.

## Introduktion {#introduction}

Databasens webbläsare är ett utvecklarverktyg som ger en skrivskyddad vy i databasen för alla miljöer när det gäller författare, publicering och förhandsgranskningsnivåer. Den är utformad för att göra det enklare att se och felsöka innehåll genom att visa innehållsstrukturen.

Den är tillgänglig från [AEM as a Cloud Service Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) och kan användas för att bläddra i databasen för en författare eller publicera en instans för en vald miljö.

### Åtkomstkrav {#access-prerequisites}

Följande villkor måste vara uppfyllda för att du ska få åtkomst till AEM as a Cloud Service Developer Console eller databasläsaren

Mer information om hur du kommer åt AEM as a Cloud Service Developer Console finns i [Developer Console-åtkomst](https://experienceleague.adobe.com/sv/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console#developer-console-access).

För att få åtkomst till Databasläsaren är kraven samma som för AEM as a Cloud Service Developer Console (anges ovan). Så här visar du innehållet i Databasläsaren för en viss instans:

* Författarinstanser: Användare med AEM användarproduktprofil för **författarinstansen** kan visa databaswebbläsaren med minimal läsåtkomst. Användarens behörigheter respekteras när användaren bläddrar i databasen. Användare med AEM administratörsproduktprofil kan visa databaswebbläsaren med fullständig läsåtkomst.

* Publiceringsinstanser: Användare med AEM-användarproduktprofil för **publiceringsinstansen** kan visa databaswebbläsaren med minimal läsåtkomst. Om produktprofilen inte anges kommer användarna att navigera som anonyma användare och vissa sökvägar visas inte på grund av begränsad behörighet.

Mer information om hur du konfigurerar användarbehörigheter finns i [Cloud Manager-dokumentationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/requirements/users-and-roles.html?lang=sv-SE).

### Starta Databasläsaren {#launching-the-repository-browser}

Databaswebbläsaren kan startas genom att följa stegen nedan.

1. I Cloud Manager klickar du på de tre punkterna bredvid den miljö du vill använda och väljer **Developer Console**

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. Klicka sedan på fliken **Databasläsare**
1. Välj en ruta som motsvarar författaren, publiceringen eller förhandsgranskningen genom att klicka på listrutan **Pod** .

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. Starta databaswebbläsaren genom att klicka på länken **Öppna databasläsare** längre ned. Webbläsaren som motsvarar en representativ instans (pod) för den valda nivån startas. Du kan inte styra den specifika pod för den nivån som startas.

## Funktioner {#features}

### Navigera i hierarkin {#navigate-the-hierarchy}

Du kan använda den vänstra navigeringsrutan för att navigera i innehållshierarkin. När du klickar på varje mapp eller nod visas dess underordnade objekt. Mappstrukturen återspeglar Sling Resource-trädet, som är en överordnad uppsättning till JCR-nodträdet.

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

Du kan också navigera direkt till en sökväg genom att ange den i fältet **Sökväg**, vilket visas nedan. Sökvägen utökar också sin plats i innehållshierarkin till vänster.

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

När du klickar på en mapp till vänster fylls fältet Sökväg automatiskt i med sin plats. Den här funktionen är användbar när du vill kopiera och klistra in värdet för senare bruk.

När du klickar på en mapp ändras URL-adressen dynamiskt så att den innehåller sökvägen till mappen. Med den här funktionen kan du skapa bokmärkningsbara URL:er.

Som standard visas endast offentligt innehåll i Databasläsaren för publicering, vilket innebär att vissa mappar som `/conf` eller `/home` inte visas.

Om du vill göra platserna synliga använder du AEM Administrators Publish Product Profile. Mer information finns i [dokumentationen för team och produktprofiler](/help/onboarding/aem-cs-team-product-profiles.md).

<!-- Drafting because of CQDOC-23204

1. Click the three dots next to the environment of your choice and select **Manage Access**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. Find your publish instance, then click it

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. Create a product profile for publish administrators. In the example below, it is called **DEV - AEM Administrators Publish**

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. Add the appropriate users, corresponding to who should be able to navigate the publish repository browser with full access, to the new product profile

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. Wait for a few minutes, then open the **AEM author** console
1. Add the group corresponding to the new product profile as a member of the administrator's group by clicking **Tools - Security - Groups on author**, then clicking the **administrators** group. Then, add the group as shown below

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. Activate the **administrators** and the new **DEV - AEM Administrators Publish** group so that they become available on publish

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. As a good security practice, remove the new **DEV - AEM Administrators Publish** group from the administrator's group on **author** so the new group is isolated to publish 

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. Upon accessing repository browser for a publish instance, all folders are visible, including `/home` and `/conf`.

-->

### Visa JCR-egenskaper {#view-jcr-properties}

När du klickar på en nod visas dess JCR-egenskaper i den högra rutan i navigeringsläsaren. Nedan visas ett exempel för noden `experience-fragments`.

![repobrowser4](/help/implementing/developing/tools/assets/repobrowser41.png)

### Visa innehåll {#view-content}

Du kan använda databaswebbläsaren för att visa innehåll. Klicka på en resurs i navigeringsrutan så att du kan öppna en förhandsvisning till höger i webbläsaren, under en flik som heter efter respektive resurs.

![repobrowser6](/help/implementing/developing/tools/assets/repobrowser61.png)

Förhandsvisning är tillgängligt för följande bildtyper:

* apng
* avif
* gif
* jpeg
* png
* svg+xml
* webp
* bmp
* x-icon
* tiff

Och för följande textbaserade MIME-typer:

* `"text/*"`
* `'application/javascript'`
* `'application/json'`
* `'application/x-sh'`

### Hämta innehåll {#download-content}

Du kan också använda databaswebbläsaren för att hämta innehåll. I exemplet nedan kan du trycka på länken **download** för att hämta `jcr:data` som är associerad med den valda noden. Den här funktionen är tillgänglig för alla binära egenskaper genom att navigera till noden som innehåller egenskapsdefinitionen.

![repobrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
