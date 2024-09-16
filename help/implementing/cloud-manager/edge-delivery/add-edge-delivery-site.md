---
title: Lägg till en Edge Delivery-webbplats i Cloud Manager
description: Lär dig hur du lägger till en Edge Delivery-webbplats i ditt produktionsprogram eller sandlådeprogram.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


## Lägg till en Edge Delivery-webbplats i Cloud Manager {#eds-add-site}

När du har lagt till Edge Delivery Services i ett produktionsprogram tillämpas din Edge Delivery Services på det.

En klickbar flik med namnet **Edge Delivery** visas på sidan Översikt. När du klickar på fliken visas en tabell med en lista över alla Edge Delivery-webbplatser som du har lagt till. Lägg märke till menyalternativet **Edge Delivery Sites** i den vänstra navigeringspanelen under grupperingen **Tjänster**.

![Översiktssida med Edge Delivery Sites i den vänstra navigeringspanelen och fliken Edge Delivery till höger om fliken Publish Delivery ](/help/implementing/cloud-manager/assets/cm-overview-eds.png)

**Så här lägger du till en Edge Delivery-webbplats i Cloud Manager:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämpligt program.
1. På konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)** väljer du programmet med konfigurerade Edge Delivery Services där du vill lägga till en Edge Delivery-webbplats.
1. Gör något av följande:
   * Klicka på fliken **Edge Delivery** på sidan **Programöversikt**. Klicka sedan på **Lägg till Edge Delivery-webbplats** nära sidans nedre högra hörn.

     ![Lägg till Edge Delivery-webbplats från fliken Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

     **Edge Delivery att göra-listan**, som visas i bilden ovan, är en valfri guide till att komma igång med Edge Delivery. Se [Om att göra-listan för Edge Delivery](#ed-todo-list).

   * I det övre vänstra hörnet av sidan klickar du på hamburgikonen för att visa den vänstra navigeringsmenyn. Klicka på **Edge Delivery Sites** under rubriken **Tjänster**. Klicka på **Lägg till plats** i sidans övre högra hörn.

     ![Lägg till Edge Delivery-webbplats från knappen Edge Delivery-platser](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. Gör följande i dialogrutan **Lägg till Edge Delivery-webbplats**:

   | Textfält | Vad du ska göra |
   | --- | --- |
   | Platsnamn | Ange namnet på den Edge Delivery-webbplats som du lägger till. Namnet fungerar som en unik identifierare för webbplatsen inom Cloud Manager. |
   | Databas-URL | Det här fältet hänvisar till Git-databasen där webbplatsens kod lagras.<br>Ange URL:en för Git-databasen som innehåller de filer och resurser som krävs (till exempel HTML, CSS, JavaScript och andra webbresurser) för din Edge Delivery-webbplats. På så sätt kan Cloud Manager hämta koden från databasen under distributionsprocessen. |
   | Platsbeskrivning (valfritt) | Ange en kort beskrivning av den Edge Delivery-webbplats som du lägger till.<br>Den här beskrivningen hjälper till att identifiera och skilja ut webbplatsen, vilket gör det enklare att hantera och identifiera andra webbplatser som du har lagt till. Du kanske vill inkludera information om webbplatsens syfte, innehåll eller annan relevant information som kan göra det lättare att klargöra dess funktion eller omfattning. |

1. Klicka på **Lägg till** i dialogrutans nedre högra hörn.

1. Gör något av följande i dialogrutan **Verifiera databasägarskap**:

   | Steg | Beskrivning |
   | --- | --- |
   | 1 | Lägg till en fil med platssökvägen till grenen `main` i Git-databasen som visas i fältet **Databas-URL**. Klicka vid behov på ikonen Kopiera för att kopiera sökvägen till Urklipp.<br> Platssökvägen är:<br>`well-known/adobe/cloudmanager-challenge.txt`.<br><br>Lägg *inte* till en punkt i början av platssökvägen, finns i:<br>`.well-known/adobe/cloudmanager-challenge.txt` |
   | 2 | Lägg till den genererade koden i filen som du skapade i steg 1. Klicka vid behov på ikonen Kopiera för att kopiera koden till Urklipp. |
   | 3 | I Git-databasen skapar du en pull-begäran och sammanfogar den för att implementera koden. |

1. Klicka på **Verifiera**. När databasen har verifierats ändras dess status i tabellen Edge Deliver Sites till en grön cirkel med en vit bock inuti.
