---
title: Konfigurera JetBrains med GitHub Copilot och AEM MCP
description: Lär dig hur du konfigurerar GitHub Copilot i JetBrains IDEs för att ansluta till AEM MCP-servrar
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: c5b46aff5b4ccffa60e8bebf7341935b435079e3
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Konfigurera JetBrains med GitHub Copilot och AEM MCP {#setup-jetbrains-copilot}

Följ de här stegen för att ansluta GitHub Copilot i en JetBrains IDE (till exempel IntelliJ IDEA, WebStorm eller PyCharm) till AEM MCP-servrar.

1. Öppna GitHub Copilot Chat i JetBrains IDE genom att klicka på ikonen **GitHub Copilot Chat** till höger om redigeraren.

   ![JetBrains IDE med GitHub Copilot Chat öppen.](assets/jetbrains-copilot-1.png)

1. Klicka på ikonen **settings** på panelen Kompilera chatt för att öppna MCP-konfigurationen.

   ![Panelen GitHub Copilot Chat med inställningsikonen markerad.](assets/jetbrains-copilot-2.png)

1. I **Inställningar** går du till **Verktyg > GitHub Copilot > Model Context Protocol (MCP)** och klickar på **Configure** för att öppna konfigurationsfilen `mcp.json`.

   ![Dialogrutan JetBrains-inställningar visar MCP-konfigurationen (Model Context Protocol) under GitHub Copilot.](assets/jetbrains-copilot-3.png)

1. Lägg till en eller flera URL-adresser för AEM MCP-servrar i filen `mcp.json`. Till exempel:

   ```json
   {
     "servers": {
       "aem": {
         "url": "https://mcp.adobeaemcloud.com/adobe/mcp/content"
       }
     }
   }
   ```


   ![Konfigurationsfilen mcp.json med URL:en för AEM MCP-servern.](assets/jetbrains-copilot-4.png)


1. Spara filen. GitHub Copilot identifierar den nya serverkonfigurationen automatiskt och visar en **Start** -åtgärd.

   ![Filen mcp.json som visar den konfigurerade AEM-servern med identifierade verktyg.](assets/jetbrains-copilot-5.png)

1. Klicka på åtgärden **Start** och logga in med din Adobe ID för att slutföra autentiseringsflödet när du uppmanas till detta.

1. Du kan granska och hantera identifierade verktyg genom att klicka på indikatorn för **verktyg** som visas på panelen Kopiera chatt. Du kan även aktivera eller inaktivera enskilda verktyg.


   ![Dialogrutan Konfigurera verktyg visar tillgängliga AEM MCP-verktyg.](assets/jetbrains-copilot-6.png)

1. Använd GitHub Copilot Chat för att anropa AEM-verktyg som en del av dina arbetsflöden för utveckling och innehåll.