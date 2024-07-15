---
title: Guiden Kopiera språk
description: Läs om hur du använder guiden för språkkopiering i AEM.
feature: Language Copy
role: Admin
exl-id: bf8bdc53-0248-47de-bb9d-c884a7179ab0
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Guiden Kopiera språk {#language-copy-wizard}

Guiden för språkkopiering är en guidad upplevelse för att skapa och instrumentera en struktur med flerspråkigt innehåll. Guiden gör det enkelt och snabbt att skapa en språkkopia.

>[!TIP]
>
>Om du inte är van vid att översätta innehåll läser du [Platsöversättningsresa](/help/journey-sites/translation/overview.md) som vägleder dig genom att översätta ditt AEM Sites-innehåll med AEM kraftfulla översättningsverktyg, vilket är idealiskt för dem som saknar AEM eller översättningsupplevelse.

>[!NOTE]
>
>Användaren måste vara medlem i gruppen `project-administrators` för att kunna skapa en språkkopia av en plats.

Så här öppnar du guiden:

1. I webbplatskonsolen markerar du en sida, väljer **Skapa** och väljer **Språkkopia**.

   ![Skapa språkkopia från guiden](../assets/language-copy-wizard.png)

1. Guiden öppnas i steget **Välj Source** där du kan lägga till/ta bort sidor. Du kan också välja att ta med eller utesluta undersidor. Markera de sidor som du vill inkludera och välj **Nästa**.

   ![Lägga till sidor med guiden](../assets/language-copy-wizard-add-pages.png)

1. Med steget **Konfigurera** i guiden kan du lägga till/ta bort språk och välja översättningsmetod. Välj **Nästa**.

   ![Konfigurera steg i guiden](../assets/language-copy-wizard-configure.png)

   >[!NOTE]
   >
   >Som standard finns det bara en översättningsinställning. Om du vill kunna välja andra inställningar måste du först konfigurera molnkonfigurationer. Se [Konfigurera översättningsintegreringsramverket](integration-framework.md).

1. I steget **Översätt** i guiden kan du välja mellan att skapa enbart strukturen, skapa ett översättningsprojekt eller lägga till i ett befintligt översättningsprojekt.

   >[!NOTE]
   >
   >Om du valde flera språk i föregående steg skapas flera översättningsprojekt.

   ![Översättningssteg i guiden](../assets/language-copy-wizard-translate.png)

1. Knappen **Skapa** avslutar guiden. Välj **Klar** om du vill stänga guiden eller **Öppna** om du vill visa det resulterande översättningsprojektet.

   ![Avsluta guiden](../assets/language-copy-wizard-done.png)
