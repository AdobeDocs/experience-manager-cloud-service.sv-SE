---
title: Lägg till en Edge Delivery-webbplats i Cloud Manager
description: Lär dig hur du lägger till en Edge Delivery-webbplats i ditt produktionsprogram eller sandlådeprogram.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: c952e69aa637b30abec4deba0e643b4287d84330
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# Lägg till en Edge Delivery-webbplats i Cloud Manager {#adding}

Du kan lägga till en Edge Delivery-plats i produktionsprogrammet eller sandlådeprogrammet.

Du måste lägga till en Edge Delivery-webbplats till Cloud Manager för att [registrera en supportanmälan för ditt Edge Delivery-projekt](/help/edge/overview.md##support-ticket).

Se även [Introduktion till Edge Delivery Services i Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

**Så här lägger du till en Edge Delivery-webbplats i Cloud Manager:**

1. Logga in på Cloud Manager på [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) och välj lämpligt program.
1. Gör något av följande:

   * Klicka på fliken **Edge Delivery** på sidan **Programöversikt**. Klicka sedan på **Lägg till Edge Delivery-webbplats** nära sidans nedre högra hörn.

     ![Lägg till Edge Delivery-webbplats från fliken Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * I det övre vänstra hörnet av sidan klickar du på hamburgikonen för att visa den vänstra navigeringsmenyn. Klicka på **Edge Delivery Sites** under rubriken **Tjänster**. Klicka på **Lägg till plats** i sidans övre högra hörn.

     ![Lägg till Edge Delivery-webbplats från knappen Edge Delivery Sites](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. Ange följande information i de obligatoriska fälten i dialogrutan **Lägg till Edge Delivery-plats**:

   | Textfält | Uppgifter som ska lämnas |
   | --- | --- |
   | Platsnamn | Ange namnet på den Edge Delivery-webbplats som du lägger till. Namnet fungerar som en unik identifierare för webbplatsen inom Cloud Manager. |
   | Databas-URL | Det här fältet hänvisar till Git-databasen där webbplatsens kod lagras. I det här fältet kan Cloud Manager hämta koden från databasen under distributionsprocessen. |
   | Platsbeskrivning (valfritt) | Ange en kort beskrivning av den Edge Delivery-webbplats som du lägger till. Den här beskrivningen hjälper till att identifiera och särskilja webbplatsen, vilket gör det enklare att hantera och identifiera andra webbplatser som du har lagt till. |

1. Klicka på **Lägg till** i dialogrutans nedre högra hörn.

1. Dialogrutan **Verifiera databasägarskap** öppnas. Utför följande steg när den är öppen:

   1. Lägg till en fil med sökvägen och namnet `well-known/adobe/cloudmanager-challenge.txt` i Git-databasens `main`-gren som visas i fältet **Databas-URL**.
      * Klicka vid behov på ikonen **Kopiera** för att kopiera sökvägen till Urklipp.
      * Lägg *inte* till en punkt i början av platssökvägen.
   1. Lägg till koden från fältet **Stega &amp;ut;num; 1** i filen som du skapade i föregående steg.
      * Klicka vid behov på ikonen **Kopiera** för att kopiera koden till Urklipp.
   1. I Git-databasen skapar du en pull-begäran för de ändringar du just har skapat och sammanfogar den sedan till `main`.

1. Klicka på **Verifiera**.

När databasen har verifierats ändras dess status i tabellen Edge Deliver Sites till en grön cirkel med en vit bock inuti.
