---
title: Lägg till en Edge Delivery-webbplats i Cloud Manager
description: Lär dig hur du lägger till en Edge Delivery-webbplats i ditt produktionsprogram eller sandlådeprogram.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 17e842c9-599a-4877-9834-1e7220f508a8
source-git-commit: db661281831dcb07491dca16e73e835b487814a6
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---

# Lägg till en Edge Delivery-webbplats i Cloud Manager {#adding}

När du har lagt till en Edge Delivery-sajt i ditt produktionsprogram tillämpas din Edge Delivery Services på den.

Du måste lägga till en Edge Delivery-webbplats till Cloud Manager för att [registrera en supportanmälan för ditt Edge Delivery-projekt](/help/edge/overview.md##support-ticket).

Se även [Introduktion till Edge Delivery Services i Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

**Så här lägger du till en Edge Delivery-webbplats i Cloud Manager:**

1. Logga in på Cloud Manager på [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) och välj lämpligt program.
1. Gör något av följande:

   * Klicka på fliken **Edge Delivery** på sidan **Programöversikt**. Klicka sedan på **Lägg till Edge Delivery-webbplats** nära sidans nedre högra hörn.

     ![Lägg till Edge Delivery-webbplats från fliken Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * Klicka på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i det övre vänstra hörnet på sidan för att visa den vänstra menyn.
Klicka på ikonen ![Webbsida](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery Sites** under rubriken **Tjänster**.
Klicka på **Lägg till plats** i sidans övre högra hörn.

     ![Lägg till Edge Delivery-webbplats från knappen Edge Delivery Sites](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. Ange följande information i de obligatoriska fälten i dialogrutan **Lägg till Edge Delivery-plats**:

   | Textfält | Beskrivning |
   | - | --- |
   | Platsnamn | Ange namnet på den Edge Delivery-webbplats som du lägger till.<br>Namnet fungerar som en unik identifierare för webbplatsen i Cloud Manager. |
   | Databas-URL | Ange Git-databasen där webbplatsens kod lagras.<br>I det här fältet kan Cloud Manager hämta koden från den databasen under distributionsprocessen. |
   | Platsbeskrivning (valfritt) | Ange en kort beskrivning av den Edge Delivery-webbplats som du lägger till.<br>En beskrivning hjälper till att identifiera och skilja ut webbplatsen, vilket gör det enklare att hantera och identifiera andra webbplatser som du har lagt till. |

1. Klicka på **Lägg till** i dialogrutans nedre högra hörn.

1. I dialogrutan **Verifiera databasägarskap** verifierar du ägarskapet för din databas genom att utföra följande steg:

   | Stegnummer | Beskrivning |
   | - | - |
   | **1** | Lägg till en fil med sökvägen och namnet `well-known/adobe/cloudmanager-challenge.txt` i Git-databasens `main`-gren som visas i fältet **Databas-URL**. Lägg *inte* till en punkt i början av platssökvägen.<br>Om det behövs klickar du på ![Kopiera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) för att kopiera sökvägen till Urklipp. |
   | **2** | Lägg till koden som visas i textfältet i steg 2 i filen som du just skapade i steg 1.<br>Klicka vid behov på ![Kopiera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) för att kopiera koden till Urklipp. |
   | **3** | Skapa en pull-begäran i Git-databasen för de ändringar som du nyss skapade och sammanfoga den sedan till `main` för att bekräfta koden. |

1. Klicka på **Verifiera**.

När databasen har verifierats uppdateras dess status i Edge Delivery platstabell. En grön cirkel med en vit bock inuti visar statusen.

I samma tabell klickar du på ![Information om Edge Delivery webbplats](https://spectrum.adobe.com/static/icons/workflow_18/Smock_InfoOutline_18_N.svg) för att visa webbplatsinformation. Den här informationen innehåller den verifierade databas-URL:en samt URL:er för förhandsvisnings- och produktionswebbplatsen.
