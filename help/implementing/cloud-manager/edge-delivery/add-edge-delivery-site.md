---
title: Lägg till en Edge Delivery-webbplats i Cloud Manager
description: Lär dig hur du lägger till en Edge Delivery-webbplats i ditt produktionsprogram eller sandlådeprogram och vilka fördelar det ger.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 68f05c49ebc3d46aa44b3998e6142ab8547e5455
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---


# Lägg till en Edge Delivery-webbplats i Cloud Manager {#eds-add-site}

Lär dig hur du lägger till en Edge Delivery-webbplats i ditt produktionsprogram eller sandlådeprogram och vilka fördelar det ger.

## Introduktion {#introduction}

Som en del av ditt projekt för Edge Delivery Services med AEM as a Cloud Service bör du lägga till din Edge Delivery-webbplats i Cloud Manager. Om du lägger till en Edge Delivery-webbplats till Cloud Manager får du följande fördelar.

* [Tillgång till CDN som hanteras av Adobe](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)
* [Åtkomst till SLA-rapporter](/help/implementing/cloud-manager/sla-reporting.md)
* [Tillgång till användningsrapporter för licenser](/help/implementing/cloud-manager/license-dashboard.md)

Observera att du måste lägga till din Edge Delivery-webbplats i Cloud Manager för att [registrera en supportanmälan för ditt Edge Delivery-projekt.](/help/edge/overview.md##support-ticket)

## Lägga till och Edge Delivery webbplats i Cloud Manager {#adding}

1. Logga in på Cloud Manager på [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) och välj lämpligt program.
1. Gör något av följande:
   * Klicka på fliken **Edge Delivery** på sidan **Programöversikt**. Klicka sedan på **Lägg till Edge Delivery-webbplats** nära sidans nedre högra hörn.

     ![Lägg till Edge Delivery-webbplats från fliken Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * I det övre vänstra hörnet av sidan klickar du på hamburgikonen för att visa den vänstra navigeringsmenyn. Klicka på **Edge Delivery Sites** under rubriken **Tjänster**. Klicka på **Lägg till plats** i sidans övre högra hörn.

     ![Lägg till Edge Delivery-webbplats från knappen Edge Delivery-platser](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

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

När du har lagt till Edge Delivery Services i ett produktionsprogram läggs din Edge Delivery Services till i det.

Varje Edge Delivery-webbplats har en **Edge Delivery att göra-lista** som hjälper dig att skapa din Edge Delivery-webbplats.

![Edge Delivery att göra-app](/help/implementing/cloud-manager/assets/edge-delivery-to-do-ist.png)

I dokumentet [Introduktion till Edge Delivery Services i Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#ed-todo-list) finns mer information om de här stegen.
