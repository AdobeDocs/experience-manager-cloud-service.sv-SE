---
title: Databasläsare
seo-title: Repository Browser
description: Databasens webbläsare ger en skrivskyddad vy i databasen för alla miljöer på författar-, publicerings- och förhandsgranskningsnivåer.
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 9d1b51b465a148551de93f8180b056b8e7752db5
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 0%

---

# Databasläsare {#repository-browser}

>[!NOTE]
>
>Databasläsaren finns AEM version 6582 och senare.

>[!INFO]
>
>Du kan också titta [det här klippet](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html) om du vill få en snabb videointroduktion om hur du använder Databasläsaren för att felsöka AEM as a Cloud Service.

## Introduktion {#introduction}

Databasens webbläsare är ett utvecklarverktyg som ger en skrivskyddad vy i databasen för alla miljöer när det gäller författare, publicering och förhandsgranskningsnivåer. Den är utformad för att göra det enklare att se och felsöka innehåll genom att visa innehållsstrukturen.

Tillgänglig från [AEM as a Cloud Service Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)kan den användas för att bläddra i databasen för en författare eller publicera en instans för en vald miljö.

### Åtkomstkrav {#access-prerequisites}

Följande villkor måste vara uppfyllda för att du ska få tillgång till AEM as a Cloud Service Developer Console eller Databaswebbläsaren

Mer information om AEM as a Cloud Service utvecklarkonsolen finns i [Åtkomst till Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console#developer-console-access).

För att komma åt Databasläsaren är kraven samma som för den AEM as a Cloud Service utvecklarkonsolen (anges ovan). Så här visar du innehållet i Databasläsaren för en viss instans:

* Författarinstanser: Användare med produktprofilen AEM användare för **Författarinstans** kan visa databasens webbläsare med minimal läsåtkomst. Användarens behörigheter respekteras när användaren bläddrar i databasen. Användare med AEM administratörsproduktprofil kan visa databaswebbläsaren med fullständig läsåtkomst.

* Publiceringsinstanser: Användare med produktprofilen AEM användare för **Publicera instans** kan visa databasens webbläsare med minimal läsåtkomst. Om produktprofilen inte anges kommer användarna att navigera som anonyma användare och vissa sökvägar visas inte på grund av begränsad behörighet.

Mer information om hur du ställer in användarbehörigheter finns i [Dokumentation för Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/requirements/users-and-roles.html).

### Starta Databasläsaren {#launching-the-repository-browser}

Databaswebbläsaren kan startas genom att följa stegen nedan.

1. Klicka på de tre punkterna bredvid den miljö du vill använda i Cloud Manager och välj **Developer Console**

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. Klicka sedan på **Databasläsare** tab
1. Välj en ruta som motsvarar författaren, publiceringen eller förhandsgranskningen genom att klicka på **Pod** listruta.

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. Starta databaswebbläsaren genom att klicka på **Öppna databasläsaren** länka längre ned. Webbläsaren som motsvarar en representativ instans (pod) för den valda nivån startas. Du kan inte styra den specifika pod för den nivån som startas.

## Funktioner {#features}

### Navigera i hierarkin {#navigate-the-hierarchy}

Du kan använda den vänstra navigeringsrutan för att navigera i innehållshierarkin. När du klickar på varje mapp eller nod visas dess underordnade objekt. Mappstrukturen återspeglar Sling Resource-trädet, som är en överordnad uppsättning till JCR-nodträdet.

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

Du kan också navigera direkt till en sökväg genom att ange den i dialogrutan **Bana** enligt nedan. Sökvägen utökar också sin plats i innehållshierarkin till vänster.

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

När du klickar på en mapp till vänster fylls fältet Sökväg automatiskt i med sin plats. Den här funktionen är användbar när du vill kopiera och klistra in värdet för senare bruk.

När du klickar på en mapp ändras URL-adressen dynamiskt så att den innehåller sökvägen till mappen. Med den här funktionen kan du skapa bokmärkningsbara URL:er.

Som standard visas endast offentligt innehåll i Databasläsaren för publicering, vilket innebär att vissa mappar `/conf` eller `/home` är inte synliga.

Gör följande om du vill göra platserna synliga:

1. Klicka på de tre punkterna bredvid den miljö du vill använda och välj **Hantera åtkomst**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. Leta reda på publiceringsinstansen och klicka sedan på den

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. Skapa en produktprofil för administratörer. I exemplet nedan anropas den **DEV - AEM administratörer publicerar**

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. Lägg till lämpliga användare, som motsvarar vem som ska kunna navigera i den publicerade databaswebbläsaren med fullständig åtkomst, till den nya produktprofilen

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. Vänta i några minuter och öppna sedan **AEM** konsol
1. Lägg till gruppen som motsvarar den nya produktprofilen som medlem i administratörsgruppen genom att klicka på **Verktyg - Säkerhet - Grupper på författaren** och sedan klicka på **administratörer** grupp. Lägg sedan till gruppen enligt nedan

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. Aktivera **administratörer** och nya **DEV - AEM administratörer publicerar** grupp så att de blir tillgängliga vid publicering

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. Som en bra säkerhetspraxis bör du ta bort den nya **DEV - AEM administratörer publicerar** grupp från administratörens grupp på **författare** så att den nya gruppen isoleras för publicering

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. När du öppnar databaswebbläsaren för en publiceringsinstans visas alla mappar, inklusive `/home` och `/conf`.

### Visa JCR-egenskaper {#view-jcr-properties}

När du klickar på en nod visas dess JCR-egenskaper i den högra rutan i navigeringsläsaren. Nedan visas ett exempel för `experience-fragments` nod.

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

Du kan också använda databaswebbläsaren för att hämta innehåll. I exemplet nedan kan du trycka på **ladda ned** länk för att ladda ned `jcr:data` associeras med den valda noden. Den här funktionen är tillgänglig för alla binära egenskaper genom att navigera till noden som innehåller egenskapsdefinitionen.

![repobrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
