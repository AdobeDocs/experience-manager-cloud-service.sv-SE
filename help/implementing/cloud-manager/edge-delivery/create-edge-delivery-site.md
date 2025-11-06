---
title: Skapa din första Edge Delivery-webbplats med ett klick
description: Lär dig hur du snabbt skapar en Edge Delivery-webbplats i Cloud Manager med en enkel musklickning.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 292bf0b4-990b-4980-b971-91b8aedde3de
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 0%

---

# Skapa din första Edge Delivery-webbplats med ett klick{#about-one-click-edge-delivery-site}

Att skapa din första Edge Delivery-webbplats med ett enda klick har utformats för att hjälpa dig att automatisera introduktionen och driftsättningen av Edge Delivery webbplatser inom Cloud Manager. Det förenklar processen avsevärt genom att du kan klicka på en enda knapp. Den här klickningen ger den infrastruktur som krävs, integreras med GitHub för versionskontroll och konfigurerar dokument- och materiallagring i Google Drive.

Den här automatiseringen minskar den manuella arbetsinsats som krävs för att skapa den första webbplatsen. Det ger smidiga arbetsflöden, skalbarhet och förbättrar teamets prestanda när det gäller att hantera innehåll i framkanten.

<!-- Check out this quick 2-minute video for a step-by-step walkthrough on creating your first Edge Delivery site—no hassle, just one click.

>[!VIDEO](https://video.tv.adobe.com/v/3458975?quality=12&learn=on) -->



<!--
## Practical use cases {#use-cases}

| Use case | Description |
| --- | --- |
| Website and application deployment | <ul><li>Automate the hosting and delivery of static or dynamic sites.</li><li>Ensure fast performance through edge caching. </li></ul> |
| API gateway and content delivery | <ul><li>Optimize API responses by caching data at the edge.</li><li>Reduce backend load and improved response times. </li></ul> |
| Real-time content updates | <ul><li>Instant deployment of new content across edge locations.</li><li>Support integration with automated content pipelines. </li></ul> |
| Edge computing workloads | <ul><li>Support serverless computing to process workloads closer to users.</li><li>Reduce latency and enhance performance. </li></ul> |
| Security and governance | <ul><li>Security is provided with integrated DDoS (Distributed Denial of Service) protection and WAF (Web Application Firewall) integration.</li><li>Ensure that content is delivered securely through TLS (Transport Security Layer) encryption. </li></ul> |
-->





## Skapa en Edge Delivery-webbplats i Cloud Manager med ett klick {#one-click-edge-delivery-site}

Om du vill skapa en Adobe Edge Delivery-webbplats med ett klick måste din organisation ha en tillgänglig Edge Delivery Services-licens. Licensen ingår i Adobe Experience Manager (AEM) och är nödvändig för att skapa Edge Delivery Services i Cloud Manager.

När det gäller behörigheter måste du vara medlem i rollen Affärsägare eller ha fått behörighet att lägga till eller redigera program i Cloud Manager. Med den här åtkomstnivån kan du hantera integreringen av Edge Delivery Services i dina program.

Se även [Introduktion till Edge Delivery Services i Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

<!-- PROPER AEM BOT CONFIGURATIONS MUST BE IN PLACE FIRST FOR AUTOMATIC CONTENT UPDATES? TRUE or FALSE? -->

**Så här skapar du en Edge Delivery-webbplats i Cloud Manager med ett enda klick:**

1. Logga in på Cloud Manager på [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) och välj lämpligt program.
1. Klicka på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i det övre vänstra hörnet på sidan för att visa den vänstra menyn.
1. Klicka på **Översikt** under rubriken **Program** på den vänstra menyn.
1. Klicka på fliken **Edge Delivery** på sidan **Programöversikt**.
1. På Edge Delivery-sidan klickar du i dialogrutan **Edge Delivery att göra-lista** i grupprutan **Lägg till Edge Delivery-webbplats** på **Skapa webbplats nu**.
1. I dialogrutan **Skapa Edge Delivery-webbplats** anger du namnet på din webbplats i textfältet **Projektnamn** och klickar sedan på **Skapa webbplats nu**.

   En popup visas nära skärmens övre mitt och du ser att Edge Delivery platsetablering har startats.

När etableringen och valideringen av webbplatsen har slutförts av Cloud Manager visas **platsnamnet** (projektnamnet du angav tidigare) i listrutan **Edge Delivery-platser** på Edge Delivery-sidan. Dessutom visas en grön bockmarkering till vänster om databasens URL.


### Utforska en Edge Delivery-webbplats som skapats med ett klick {#explore-one-click-ed-site}

1. Logga in på Cloud Manager på [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) och välj lämpligt program.
1. Klicka på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i det övre vänstra hörnet på sidan för att visa den vänstra menyn.
1. Klicka på **Översikt** under rubriken **Program** på den vänstra menyn.
1. Klicka på fliken **Edge Delivery** på sidan **Programöversikt**.
1. Gör något av följande på Edge Delivery-sidan:

   | Vad du ska utforska | Steg |
   | --- | --- |
   | GitHub-databas för en webbplats | <ul><li>I listrutan **Edge Delivery-webbplatser** klickar du på URL-adressen till webbplatsen som du nyss skapade, under kolumnrubriken **Databas**.<br>Du kan behöva logga in på GitHub med ditt användarnamn eller din e-postadress och ditt lösenord.</li> |
   | Publicera en webbplats | <ul><li> Klicka på ikonen **Mer** längst till höger om namnet på din webbplats i listrutan ![Edge Delivery-webbplatser](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) för att öppna listrutan.</li><li>Klicka på ikonen ![Publiceringskontroll](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PublishCheck_18_N.svg) **Publicera webbplats** i listrutan.<br>Ett popup-meddelande visas som talar om att publiceringen av webbplatsen har startats.</li></ul> |
   | Förhandsgranska en publicerad webbplats | <ul><li>I listrutan **Edge Delivery-webbplatser** klickar du, under kolumnrubriken **Platsnamn**, på URL-adressen till webbplatsen som du just skapade och publicerade.<br>Observera att URL-adressen för webbplatsen avslutas med `.page` i URL-adressfältet i webbläsaren, vilket anger att du ser en förhandsgranskning av webbplatsen.</li><li>Om du vill visa webbplatsen live ändrar du `.page` manuellt till `.live` i URL-adressfältet.</li></ul> |
   | Ge användarna tillgång till innehållsarkivet på Google Drive | <ul><li> Klicka på ikonen **Mer** längst till höger om namnet på din webbplats i listrutan ![Edge Delivery-webbplatser](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) för att öppna listrutan.</li><li>Klicka på ikonen ![Lägg till användare](https://spectrum.adobe.com/static/icons/workflow_18/Smock_UsersAdd_18_N.svg) **Få åtkomst till innehållsdatabasen** i listrutan.</li><li>Ange e-postadressen till en medarbetare i dialogrutan **Lägg till medarbetare på webbplatsen** och klicka sedan på ikonen ![Markera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg).</li><li>Fortsätt lägga till e-post från medverkande efter behov.</li><li>När du är klar klickar du på **Lägg till medarbetare**.</li><li>Klicka på **OK** i dialogrutan **Collaboration har lagts till** om du vill dela länken med dina innehållsmedarbetare.</li><li>Klicka på ikonen ![Kopiera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) i dialogrutan som Collaboration har lagt till för att kopiera länken och dela den med dina medarbetare.<br>Innan du delar länken måste du bekräfta att medarbetare är inloggade med den e-postadress som är kopplad till deras IMS-konto. Om deras IMS-e-postkonto inte är tillgängligt måste de använda den e-postadress som lagts till som medarbetare. På så sätt ser du till att medarbetarna kan komma åt länken och se innehållet som ska redigeras eller uppdateras på Google Drive.</li><li>När du är klar med redigeringen klickar du på **Publicera webbplats** i Cloud Manager, enligt beskrivningen ovan.<br>Eller förhandsgranska ändringarna enligt beskrivningen ovan.</li></ul> |
   | Ge användarna åtkomst till basdatabasen på GitHub | <ul><li> Klicka på ikonen **Mer** längst till höger om namnet på din webbplats i listrutan ![Edge Delivery-webbplatser](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) för att öppna listrutan.</li><li>Klicka på ikonen ![Kod](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) **Få åtkomst till basdatabasen** i listrutan.</li><li>Ange GitHub-användarnamnet för en medarbetare i dialogrutan **Åtkomst till basdatabasen för din plats** och klicka sedan på ![bockmarkeringsikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg).</li><li>Fortsätt lägga till GitHub-användarnamn efter behov.</li><li>När du är klar klickar du på **Lägg till medarbetare**.</li>Användarna måste ge åtkomst till sina egna GitHub-användarnamn för att kunna visa databasen. |
