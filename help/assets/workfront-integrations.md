---
title: '[!DNL Experience Manager Assets] integration with [!DNL Adobe Workfront]'
description: Introduktion till integrering mellan [!DNL Assets] och [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
source-git-commit: 045387bc02ca5a30e0caa020885d4cf63b4e9aef
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager] som [!DNL Cloud Service] [!DNL Assets] integrering med [!DNL Adobe Workfront] {#assets-integration-overview}

[!DNL Adobe Workfront] är ett program för arbetshantering som hjälper dig att hantera hela arbetscykeln på ett och samma ställe. Integrationen mellan [!DNL Workfront] och [!DNL Adobe Experience Manager Assets] gör att organisationer kan förbättra innehållets hastighet och time-to-market genom att knyta samman arbete och hantering av digitala resurser. När man arbetar i Workfront får man tillgång till dokument och bilder.

The [!DNL Workfront for Experience Manager enhanced connector] möjliggör förbättrade affärsprocesser med kompletta arbetsflöden och ger personaliserade kundupplevelser från början till slut och central lagring. Mer information om funktionerna och funktionerna i [!DNL enhanced connector], se [nyheter i [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

[!DNL Workfront for Experience Manage enhanced connector] gör att din organisation kan:

* Skapa automatiskt länkade Experience Manager-mappar i Workfront och ordna mapparna baserat på Workfront Portfolio, Program och Projekt.
* Synkronisera Workfront-projektmetadata med länkade Experience Manager-mappar.
* Experience Manager metadatauppdateringar med nya versioner.
* Ange objektstatus för Workfront baserat på konfigurerbara villkor med hjälp av arbetsflöden i Experience Manager.
* Publicera material i Experience Manager eller Brand Portal.

Se plattformsstödet och [krav för den förbättrade anslutningen](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>Adobe kräver installation och konfiguration av [!DNL Adobe Workfront for Experience Manager enhanced connector] endast via certifierade partners eller [!DNL Adobe Professional Services]. Om den distribueras och konfigureras utan en certifierad partner eller [!DNL Adobe Professional Services], stöds den inte av Adobe.
>
>Adobe kan släppa uppdateringar av [!DNL Adobe Workfront] och [!DNL Adobe Experience Manager] som gör denna koppling överflödig, Om detta inträffar kan kunderna behöva gå över från att använda denna koppling.

## Jämför olika integreringar mellan [!DNL Assets] och [!DNL Workfront] {#feature-parity-matrix}

Nedan beskrivs de funktioner som är tillgängliga genom olika typer av integreringar mellan [!DNL Assets] och [!DNL Workfront].

| Funktion | Beskrivning | [!DNL Workfront] and [!DNL Assets Essentials] | [!DNL Workfront] for [!DNL Experience Manager] koppling | [!DNL Workfront for Experience Manager enhanced connector] |
|----|----|----|------|-----|
| Distributionsmetoder | Lämpliga för vilka [!DNL Assets] erbjuder. | Assets Essentials | Cloud Service, Adobes hanterade tjänster, lokal | Cloud Service, Adobes hanterade tjänster, lokal |
| Skicka digitala filer från [!DNL Workfront] till [!DNL Assets] | Den senaste versionen av ett WF-dokument kan överföras till AEM Assets som länkas som en ny version av dokumentet. | ✓ | ✓ | ✓ |
| Länka AEM mappar manuellt till Workfront-objekt | Befintliga AEM kan länkas som en Workfront-mapp och dess underordnade resurser länkas som nya Workfront-dokument. | ✓ | ✓ | ✓ |
| Länk [!DNL Assets] till Workfront Objects | Befintliga resurser i AEM kan länkas till ett nytt Workfront-dokument eller som en ny version av ett befintligt dokument. | ✓ | ✓ | ✓ |
| Resurser som läggs till i länkade mappar skickas automatiskt till AEM | Om ett dokument läggs till i en länkad mapp överförs den associerade resursen automatiskt till AEM Assets som en ny resurs. | ✓ | ✓ | ✓ |
| Hämta länkade AEM Assets inifrån Workfront | När en resurs är länkad i Workfront kan användaren hämta resursens byte. | ✓ | ✓ | ✓ |
| Sök efter AEM Assets inifrån Workfront | Med AEM Assets-väljaren i Workfront kan du göra fulltextsökningar efter resurser. | ✓ | ✓ | ✓ |
| Visa och navigera AEM mapphierarki inifrån Workfront | Med AEM Assets-väljaren i Workfront kan du bläddra i AEM Assets-hierarkin som begränsas av användarens tillhörande åtkomstkontroller och behörigheter som anges i AEM. | ✓ | ✓ | ✓ |
| Avlänka resurser från AEM Assets i Workfront | En befintlig länkad resurs från AEM kan tas bort från det associerade Workfront-dokumentet. Originalresursen i AEM tas inte bort. | ✓ | ✓ | ✓ |
| Lägg till ny versionshanterad resurs i AEM Assets från Workfront | När en nytillagd version läggs till i ett dokument i Workfront kan användaren skicka den nya versionen till AEM för att ersätta den befintliga versionen. | ✓ | ✓ | ✓ |
| Resurser länkade i Workfront när användaren klickades på AEM | Användare dirigeras till AEM för att förhandsgranska en länkad resurs i Workfront. | ✓ | ✓ | Anpassat |
| Skapa automatiskt länkade AEM i Workfront | Skapa automatiskt länkade AEM i Workfront med objektstatus. Ordna automatiskt AEM mappar baserat på Workfront Portfolio, Program och Projekt. | Nej | Nej | ✓ |
| Synkronisering av kommentarer | Synkronisera kommentarer automatiskt för resurser från [!DNL Workfront] till [!DNL Assets] | Nej | ✓ | ✓ |
| Mappa metadata för Workfront-resurser till AEM Assets | Workfront-objekt och anpassade formuläregenskaper kan mappas till AEM metadataegenskaper för resurser. Värden överförs vid första överföring/länk. | ✓ | ✓ | ✓ |
| Skapa automatiskt anpassad Forms för dokument i Workfront | Bifoga skräddarsydda blanketter i Workfront dokument, uppgifter och ärenden med hjälp AEM arbetsflöden. | Nej | Lägg till det anpassade formuläret manuellt och automatisk synkronisering fungerar | ✓ |
| Automatisk dubbelriktad uppdatering av metadata mellan AEM Assets och Workfront | Uppdatera automatiskt metadata mellan AEM Assets och Workfront. | Nej | ✓ | ✓ |
| Mappa Workfront-metadata till AEM Assets-mappar | Synkronisera Workfront projektmetadata med länkade AEM. | Nej | Nej | ✓ |
| AEM metadatauppdateringar med nya versioner | En konfiguration i AEM kan göras för att avgöra om en nyversion av en resurs i Workfront också ska pushas med ändringar i dess metadata. | Nej | Nej | ✓ |
| Uppdatera AEM metadata automatiskt vid ändringar i anpassad Forms i Workfront | Workfront är konfigurerat så att angivna egenskaper AEM metadata mappas till ett anpassat dokumentformulär. När en resurs är länkad från början, eller när en resurs uppdateras, kopieras värdena för dessa metadataegenskaper till motsvarande anpassade formulärfält i Workfront-dokumentet. Man måste vara försiktig för att förhindra att AEM skickas tillbaka till AEM som om det var en ändring som hade sitt ursprung i Workfront. | Nej | ✓ | ✓ |
| Skapa ny korrekturversion på länkade resurser | När en resurs länkas i Workfront kan ett korrektur genereras automatiskt. | Nej | ✓ | Anpassat |
| Ange status för Workfront-objekt | Ange Workfront objektstatusbaserade konfigurerbara villkor med hjälp av AEM arbetsflöden | Nej | Nej | ✓ |
| Publicera resurser i AEM Publish Environment eller Brand Portal | Ge Workfront-användare möjlighet att automatiskt publicera länkade resurser i en AEM-publiceringsmiljö eller Brand Portal. | Nej | Nej | ✓ |
