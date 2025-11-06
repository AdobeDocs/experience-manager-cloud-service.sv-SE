---
title: Integrering av [!DNL Experience Manager Assets] med  [!DNL Adobe Workfront]
description: Introduktion till integrering mellan  [!DNL Assets] och [!DNL Workfront]
role: Admin, Leader, Developer
feature: Workfront Integrations and Apps
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager] som en [!DNL Cloud Service] [!DNL Assets]-integrering med [!DNL Adobe Workfront] {#assets-integration-overview}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |

[!DNL Adobe Workfront] är ett program för arbetshantering som hjälper dig att hantera hela arbetscykeln på ett och samma ställe. Integrationen mellan [!DNL Workfront] och [!DNL Adobe Experience Manager Assets] gör att organisationer kan förbättra innehållets hastighet och time-to-market genom att knyta samman arbete och hantering av digitala resurser. När man arbetar i Workfront får man tillgång till dokument och bilder.

Adobe erbjuder att [integrera [!DNL Workfront] och [!DNL Adobe Experience Manager Assets] internt (stöd för Assets Essentials och Assets as a Cloud Service)](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html?lang=sv-SE).

Tack vare integreringen med Experience Manager kan du

* Konfigurera snabbt integreringen i Workfront.

* Skapa automatiskt mappar länkade mellan Workfront och Experience Manager.

* Synkronisera enkelt metadata för befintliga länkade resurser.

* Uppdatera automatiskt projektmetadata när de ändras i Workfront.

* Koppla smidigt ihop flera Experience Manager Assets-arkiv med en Workfront-miljö, eller flera Workfront-miljöer, till en Experience Manager Assets-databas över olika företags-ID:n.


## Adobe Workfront for Experience Manager förbättrad anslutning {#enhanced-connector-information}


Från juni 2022 släppte Adobe en ny inbyggd integrering för att ansluta Workfront till Adobe Experience Manager Assets as a Cloud Service. Den här integreringen har blivit den metod som krävs för att ansluta dessa två lösningar. Eventuella framtida nya implementeringar av den förbättrade anslutningen (1.9.8 och senare) för att ansluta Workfront till AEM Assets as a Cloud Service blockeras. Mer information om hur du konfigurerar den här integreringen finns i [Konfigurera Experience Manager Assets as a Cloud Service-integreringen](workfront-connector-configure.md).

>[!NOTE]
>
>Adobe stöder inte användning av Workfront för Experience Manager förbättrade anslutningsprogram och Experience Manager-integrering parallellt.

För installationer före juni 2022 är följande punkter att notera för distributionen och konfigurationen av [!DNL Adobe Workfront for Experience Manager enhanced connector]:

* Adobe kräver att [!DNL Adobe Workfront for Experience Manager enhanced connector] distribueras och konfigureras endast via certifierade partners eller [!DNL Adobe Professional Services]. Om den distribueras och konfigureras utan en certifierad partner eller [!DNL Adobe Professional Services] stöds den inte av Adobe.
* Adobe kan släppa uppdateringar av [!DNL Adobe Workfront] och [!DNL Adobe Experience Manager] som gör den här kopplingen överflödig. Om detta inträffar kan kunderna behöva gå över från att använda den här anslutningen.
* Adobe har stöd för utökade anslutningsversioner 1.7.4 och senare. Tidigare förhandsversioner och anpassade versioner stöds inte. Om du vill kontrollera den utökade anslutningsversionen läser du steg 5(a) i [de förbättrade installationsanvisningarna för anslutningsprogrammet](workfront-connector-install.md).
* Se [Partnercertifieringsprov för Workfront för Experience Manager Assets förbättrade anslutningsprogram](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Mer information om provet finns i [Handbok för prov](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).