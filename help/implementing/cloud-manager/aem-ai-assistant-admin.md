---
title: Konfigurera AI-assistenten i Adobe Experience Manager
description: Lär dig hur du konfigurerar och konfigurerar AI-assistenten med Admin Console i Adobe Experience Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: ab8fefe18e43c1fe937d0d16df65b6137fc8a292
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# Konfigurera AEM AI Assistant - Administratörsinstallation {#aem-ai-asst-admin-setup}

En administratör måste konfigurera åtkomst, behörigheter och inställningar innan användare i organisationen kan använda funktionerna i AEM AI Assistant. I den här artikeln beskrivs hur du aktiverar AI-assistenten för din organisation, konfigurerar nödvändiga autentiseringsuppgifter och sparar konfigurationsändringar.

**Översikt över konfigurationsprocessen för AEM AI Assistant**

Konfigurationsprocessen består av följande steg:

1. Skapa en ny produktprofil i Adobe Admin Console.
1. Aktivera behörigheten&quot;AI Assistant Product Knowledge&quot;.
1. Skapa eller använd en befintlig användargrupp.
1. Lägg till användare i användargruppen.
1. Tilldela produktprofilen till användargruppen.

**Förutsättningar**

Innan du börjar bör du kontrollera att du uppfyller följande krav:

* Du måste ha minst produktadministratörsbehörighet i Adobe Admin Console.
* Du har en förståelse för organisationens användarhanteringsstruktur.

## 1 - Skapa en ny produktprofil i Adobe Admin Console{#create-profile}

1. Följ de detaljerade instruktionerna i [Skapa en ny produktprofil i Adobe Admin Console](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/create-profile) när du hittade Experience Platform-dokumentationen.

1. När du skapar den nya produktprofilen använder du följande exempel på de värden du kan använda för AI-assistenten.

   | Textfält | Föreslaget värde |
   | --- | --- |
   | Produktprofilnamn | `AEM AI Assistant` (eller ditt beskrivande namn) |
   | Visningsnamn (valfritt) | `AI Assistant` |
   | Beskrivning (valfritt) | `Product profile for managing AEM AI Assistant access` |
   | Meddelande | Konfigurera baserat på organisationens inställningar |




## 2 - Aktivera behörigheten&quot;AI Assistant Product Knowledge&quot;{#enable-permission}

Processen för att tilldela anpassade behörigheter till produktprofiler följer standardarbetsflödet för anpassade behörigheter i Adobe Cloud Manager.

Referensartikel: [Tilldela anpassade behörigheter till den nya produktprofilen](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. I Admin Console klickar du på namnet på den nya produktprofilen (`AEM AI Assistant`)

   ![Skärmbild](/help/implementing/cloud-manager/assets/ai-assistant-console.png)

1. Klicka på fliken **Behörigheter** om du vill visa listan över redigerbara behörigheter.

1. Leta reda på behörigheten `AI Assistant Product Knowledge` i tabelllistan.

   ![Behörigheter för AI-assistenten på fliken Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-permission.png)

1. Klicka på ikonen ![Penna eller Redigera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) till höger om behörighetens namn.

1. På sidan **Redigera behörigheter för AI Assistant** aktiverar du alternativet **AI Assistant Product Knowledge**.

   ![Sidan Redigera behörigheter för växlingsalternativet AI Assistant Product Knowledge ](/help/implementing/cloud-manager/assets/ai-assistant-prod-knowledge.png)

1. Klicka på **Spara** i sidans nedre högra hörn.

   Din produktprofil har nu AI Assistant-produktkunskapsbehörighet aktiverad.


## 3 - Skapa en användargrupp (eller använd en befintlig användargrupp){#create-user-group}

1. Gör något av följande:

>[!BEGINTABS]

>[!TAB Skapa en ny användargrupp]

1. I Admin Console klickar du på **Användare** > **Användargrupper**.

   ![Användargrupper](/help/implementing/cloud-manager/assets/ai-assistant-user-groups.png)

1. Klicka på **Ny användargrupp** på sidan **Användargrupper**.

   ![Knappen Ny användargrupp på sidan Användargrupper](/help/implementing/cloud-manager/assets/ai-assistant-new-user-group.png)

1. Ange följande information på sidan **Skapa en ny användargrupp**:

   | Alternativ | Föreslaget värde |
   | --- | --- |
   | Användargruppsnamn | `AEM AI Assistant` (eller ditt namn) |
   | Beskrivning (valfritt) | `User group for managing AEM AI Assistant access` |

   ![Skapa en ny användargruppsida](/help/implementing/cloud-manager/assets/ai-assistant-create-new-user-group.png)

1. Klicka på **Spara** i det nedre högra hörnet på sidan.

>[!TAB Använd en befintlig användargrupp]

Du kan använda en befintlig AEM-användargrupp om den uppfyller åtkomstkraven för AI Assistant i stället för att skapa en ny grupp.

>[!ENDTABS]

## 4 - Lägg till användare i användargruppen{#add-users}

1. Gör något av följande:

>[!BEGINTABS]

>[!TAB Lägg till enskilda användare]

1. På sidan **Användargrupper** klickar du i tabellen **Gruppnamn** på det användargruppnamn som du skapade nyligen eller på ett befintligt användargruppnamn.

   ![Sidan Användargrupper med användargruppnamnet AEM AI Assistant i tabellen](/help/implementing/cloud-manager/assets/ai-assistant-user-group-name-in-table.png)

1. Klicka på fliken **Användare** på sidan **Användargrupper** för **AEM AI-assistenten** och sedan på **Lägg till användare**.

   ![Sidan med användargrupper för AEM AI Assistant som visar fliken Användare och knappen Lägg till användare](/help/implementing/cloud-manager/assets/ai-assistant-add-users.png)

1. På sidan **Lägg till användare i den här användargruppen** söker du efter och väljer användare som behöver åtkomst till AEM AI Assistant.

   ![Lägg till användare på den här användargruppsidan](/help/implementing/cloud-manager/assets/ai-assistant-add-users-to-this-group.png)

1. Klicka på **Spara** i sidans nedre högra hörn.

>[!TAB Lägg till användare i grupp]

Du kan använda massöverföring i Admin Console.

1. Förbered en CSV-fil med användarinformation.

1. Använd alternativet **Lägg till användare via CSV** om du vill lägga till flera användare effektivt.

>[!ENDTABS]




## 5 - Tilldela produktprofilen till användargruppen{#assign-product-profile}




