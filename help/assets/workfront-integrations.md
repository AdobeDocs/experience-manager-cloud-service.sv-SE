---
title: '[!DNL Experience Manager Assets] integrering med [!DNL Adobe Workfront]'
description: Introduktion till integrering mellan [!DNL Assets] och [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: e8607f5dfc9ad5fd5ababec47b4933bee131e566
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] som [!DNL Cloud Service] [!DNL Assets] integrering med [!DNL Adobe Workfront] {#assets-integration-overview}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html) |
| AEM as a Cloud Service | Den här artikeln |

[!DNL Adobe Workfront] är ett program för arbetshantering som hjälper dig att hantera hela arbetscykeln på ett och samma ställe. Integrationen mellan [!DNL Workfront] och [!DNL Adobe Experience Manager Assets] gör att organisationer kan förbättra innehållets hastighet och time-to-market genom att knyta samman arbete och hantering av digitala resurser. När man arbetar i Workfront får man tillgång till dokument och bilder.

Adobe erbjuder [integrera [!DNL Workfront] och [!DNL Adobe Experience Manager Assets] Inbyggt (stöd för Assets Essentials och Assets as a Cloud Service) eller användning av Workfront för Experience Manager-förbättrad anslutning](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html). Vid inbyggd integrering behövs ingen koppling för att integrera de två lösningarna.

>[!NOTE]
>
>Adobe stöder inte samtidig användning av Workfront för Experience Manager utökade kontakter och Experience Manager.

Med inbyggd integrering med Experience Manager och [!DNL Workfront for Experience Manager enhanced connector]kan du:

| Inbyggt [!DNL Adobe Experience Manager Assets] funktioner | [!DNL Workfront for Experience Manager enhanced connector] funktioner |
|---|---|
| <ul><li>Konfigurera snabbt integreringen i Workfront.</li><li>Skapa automatiskt mappar som är länkade mellan Workfront och Experience Manager.</li><li>Synkronisera enkelt metadata för befintliga länkade resurser.</li><li>Uppdatera automatiskt projektmetadata när de ändras i Workfront.</li><li>Koppla smidigt ihop flera Experience Manager Assets-arkiv med en Workfront-miljö, eller flera Workfront-miljöer, till en Experience Manager Assets-databas över olika företags-ID:n.</li> | <ul><li>Skapa automatiskt länkade Experience Manager-mappar i Workfront och ordna mapparna baserat på Workfront Portfolio, Program och Projekt.</li><li>Synkronisera Workfront-projektmetadata med länkade Experience Manager-mappar.</li><li>Experience Manager metadatauppdateringar med nya versioner.</li><li>Ange objektstatus för Workfront baserat på konfigurerbara villkor med hjälp av arbetsflöden i Experience Manager.</li><li>Publicera material i Experience Manager eller Brand Portal.</li> |

Se [funktioner nedan för en jämförelse](#feature-parity-matrix) mellan inbyggd integrering eller integrering med hjälp av anslutningar mellan de två lösningarna.



Se plattformsstödet och [krav för den förbättrade anslutningen](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Från juni 2022 släppte Adobe en ny inbyggd integrering för att ansluta Workfront till Adobe Experience Manager Assets as a Cloud Service. Den här integreringen har blivit den metod som krävs för att ansluta dessa två lösningar. Eventuella framtida nya implementeringar av den utökade anslutningen (1.9.8 och senare) för att ansluta Workfront till AEM Assets as a Cloud Service blockeras. Mer information om hur du konfigurerar den här integreringen finns i [Konfigurera Experience Manager Assets as a Cloud Service-integrering](workfront-connector-configure.md).
>
>* Adobe kräver installation och konfiguration av [!DNL Adobe Workfront for Experience Manager enhanced connector] endast via certifierade partners eller [!DNL Adobe Professional Services]. Om den distribueras och konfigureras utan en certifierad partner eller [!DNL Adobe Professional Services], stöds den inte av Adobe.
>
>* Adobe kan släppa uppdateringar av [!DNL Adobe Workfront] och [!DNL Adobe Experience Manager] som gör denna koppling redundant, Om detta inträffar kan kunderna behöva gå över från att använda denna koppling.
>
>* Adobe har stöd för utökade anslutningsversioner 1.7.4 och senare. Tidigare förhandsversioner och anpassade versioner stöds inte. Information om hur du kontrollerar den förbättrade anslutningsversionen finns i steg 5 a i [installationsanvisningar för förbättrad anslutning](workfront-connector-install.md).
>
>* Se [Partnercertifieringsprov för Workfront för Experience Manager Assets förbättrad anslutning](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Mer information om provet finns i [Provguide](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## Jämför olika integreringar mellan [!DNL Assets] och [!DNL Workfront] {#feature-parity-matrix}

Nedan beskrivs de funktioner som är tillgängliga genom olika typer av integreringar mellan [!DNL Assets] och [!DNL Workfront].

| Funktion | Beskrivning | [!DNL Workfront] och [!DNL Assets Essentials] *Ingen anslutning (OTB)* | [!DNL Workfront for Experience Manager enhanced connector] *Kräver anslutning* | Workfront och [!DNL Experience Manager as a Cloud Service] *Ingen anslutning (OTB)* |
|----|----|----|-----|-----|
| Distributionsmetoder | Lämpliga för vilka [!DNL Assets] erbjuder. | Assets Essentials | Adobes hanterade tjänster, lokala | Cloud Service |
| **Allmänt** |
| Skicka digitala filer från [!DNL Workfront] till [!DNL Assets] | Den senaste versionen av ett WF-dokument kan överföras till AEM Assets som länkas som en ny version av dokumentet. | ✓ | ✓ | ✓ |
| Länka AEM mappar manuellt till Workfront-objekt | Befintliga AEM kan länkas som en Workfront-mapp och dess underordnade resurser länkas som nya Workfront-dokument. | ✓ | ✓ | ✓ |
| Länk [!DNL Assets] till Workfront Objects | Befintliga resurser i AEM kan länkas till ett nytt Workfront-dokument eller som en ny version av ett befintligt dokument. | ✓ | ✓ | ✓ |
| Resurser som läggs till i länkade mappar skickas automatiskt till AEM | Om ett dokument läggs till i en länkad mapp överförs den associerade resursen automatiskt till AEM Assets som en ny resurs. | ✓ | ✓ | ✓ |
| Hämta länkade AEM Assets inifrån Workfront | När en resurs är länkad i Workfront kan användaren hämta resursens byte. | ✓ | ✓ | ✓ |
| Sök efter AEM Assets inifrån Workfront | Med AEM Assets-väljaren i Workfront kan du göra fulltextsökningar efter resurser. | ✓ | ✓ | ✓ |
| Sök efter AEM mappar i Workfront | Med AEM Assets-väljaren i Workfront kan du söka i fulltext efter mappar. | ✓ | ✓ | ✓ |
| Visa och navigera AEM mapphierarki inifrån Workfront | Med AEM Assets-väljaren i Workfront kan du bläddra i AEM Assets-hierarkin som begränsas av användarens tillhörande åtkomstkontroller och behörigheter som anges i AEM. | ✓ | ✓ | ✓ |
| Spåra resursversioner AEM tidslinjer | Bevara dokumentversionshistorik mellan Workfront och AEM. | ✓ | ✓ | ✓ |
| Avlänka resurser från AEM Assets i Workfront | En befintlig länkad resurs från AEM kan tas bort från det associerade Workfront-dokumentet. Originalresursen i AEM tas inte bort. | ✓ | ✓ | ✓ |
| Lägg till ny versionshanterad resurs i AEM Assets från Workfront | När en nytillagd version läggs till i ett dokument i Workfront kan användaren skicka den nya versionen till AEM för att ersätta den befintliga versionen. | ✓ | ✓ | ✓ |
| Resurser länkade i Workfront när användaren klickades på AEM | Användare dirigeras till AEM för att förhandsgranska en länkad resurs i Workfront. | ✓ | ✓ | Kommande |
| Skapa automatiskt länkade AEM i Workfront | Skapa automatiskt länkade AEM i Workfront med projektstatus. Konfigurera AEM automatiskt baserat på Workfront Portfolio, Program och Projekt. | Nej | ✓ | Nej |
| Navigera direkt till AEM från Workfront | Tillåt användare att navigera till tillgängliga AEM som konfigurerats i Workfront. | ✓ | Nej | ✓ |
| Skapa länkade AEM mappar i Workfront | Skapa länkade AEM i Workfront manuellt med hjälp av alternativet på fliken Dokument. | ✓ | Nej | ✓ |
| Synkronisering av kommentarer | Synkronisera kommentarer automatiskt för resurser från [!DNL Workfront] till [!DNL Assets] | Nej | ✓ | Nej |
| Stöd för flera Workfront-miljöer som ansluter till en enda AEM | Användare från flera Workfront-miljöer kan ansluta till en enda AEM. | ✓ | Nej | ✓ |
| Stöd för flera AEM miljöer som ansluter till en enda Workfront-miljö | Användare i en och samma Workfront-miljö kan skicka eller länka resurser mellan flera AEM miljöer. | ✓ | ✓ | ✓ |
| **Metadata** |
| Mappa metadata för Workfront-resurser till AEM Assets | Workfront-objekt och anpassade formuläregenskaper kan mappas till AEM metadataegenskaper för resurser. Värden överförs vid första överföring/länk. | ✓ | ✓ | ✓ |
| Skapa automatiskt anpassad Forms för dokument i Workfront | Bifoga skräddarsydda blanketter i Workfront dokument, uppgifter och ärenden med hjälp AEM arbetsflöden. | Nej | ✓ | Nej |
| Automatisk dubbelriktad uppdatering av metadata mellan AEM Assets och Workfront | Uppdatera automatiskt metadata mellan AEM Assets och Workfront. Resursen måste initialt skickas från Workfront till AEM och Workfront-resursens metadata måste mappas till AEM för att dubbelriktade metadatauppdateringar ska fungera korrekt. | Nej | ✓ | Nej |
| Vy i realtid i Workfront för mappade metadata till AEM | Visa de uppdaterade mappade metadata som AEM i Workfront dokumentinformation och dokumentsammanfattningspaneler. | ✓ | Nej | ✓ |
| Realtidspush av uppdaterade Workfront-metadata för AEM | Uppdatera automatiskt mappade Workfront-metadata till AEM utan att behöva återanvända en resurs eller en ny version av en resurs. | ✓ | Nej | ✓ |
| Mappa Workfront-metadata till AEM Assets-mappar | Synkronisera Workfront projektmetadata med länkade AEM. | Nej | ✓ | ✓ |
| AEM metadatauppdateringar med nya versioner | En konfiguration i AEM kan göras för att avgöra om en nyversion av en resurs i Workfront också ska pushas med ändringar i dess metadata. | Nej | ✓ | Nej |
| Uppdatera AEM metadata automatiskt vid ändringar i anpassad Forms i Workfront | AEM kan du prenumerera på uppdateringar av dokumentformulären i Workfront. Därför ändras värdena för mappade AEM metadatafält om du uppdaterar Workfront-dokumentets anpassade formulärmetadata. | Nej | ✓ | Nej |
| **Arbetsflöden (färdiga)** |
| Skapa ny korrekturversion på länkade resurser | När en resurs länkas i Workfront kan ett korrektur genereras automatiskt. | Nej | Egen | Nej |
| Ange status för Workfront-objekt | Ange Workfront objektstatusbaserade konfigurerbara villkor med hjälp av AEM arbetsflöden | Nej | ✓ | Kommande |
| Publicera resurser i AEM Publish Environment eller Brand Portal | Ge Workfront-användare möjlighet att automatiskt publicera länkade resurser i en AEM-publiceringsmiljö eller Brand Portal. | Nej | ✓ | Kommande |
