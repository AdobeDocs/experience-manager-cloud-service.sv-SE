---
title: Översikt över utvecklingsagenten
description: Läs om hur utvecklingsagenten i AEM analyserar misslyckade pipelines i Cloud Manager och skapar loggar som föreslår kodkorrigeringar och snabbar upp felsökningen.
feature: Agentic AI, AI Assistant, AI Tools, User Roles
role: User, Admin, Architect, Developer
source-git-commit: 30b715d4e43bf83016622e3cf13f100062a1c08d
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# Utvecklingsagent - översikt {#development-agent-overview}

Utvecklingsagenten hjälper AEM-utvecklare och -administratörer att skapa, felsöka, driftsätta och optimera kod effektivare.

För närvarande kan agenten hämta pipeline-status och hjälpa dig att felsöka misslyckade konstruktionssteg genom att föreslå korrigeringar, vilket sparar tid vid felsökning av AEM as a Cloud Service-distributioner i utvecklings-, scen- och produktionsmiljöer. Den undersöker byggloggar och relaterad kod för att rekommendera en korrigering som du kan tillämpa manuellt.

>[!VIDEO](https://video.tv.adobe.com/v/3478006?quality=12&learn=on)

>[!IMPORTANT]
>
>AI-genererade svar kan vara felaktiga eller vilseledande. Kontrollera att du dubbelkontrollerar föreslagna korrigeringar och svar.
>
>Se även [Adobe Experience Cloud Generative AI User Guidelines](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

<!-- 
## Cloud Manager Pipeline Troubleshooting  {#cloud-manager-pipeline-troubleshooting}
-->

Om du vill få åtkomst till den här agenten kan du läsa [versionsinformationen](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs) för instruktioner om hur du registrerar dig i betaprogrammet och se till att du är intresserad av utvecklingsagenten. Du kan även skicka feedback specifikt för utvecklingsagenten via e-post till [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com).

## Gå till utvecklingsagenten via Cloud Manager {#how-to-access-the-agent}

Du kommer åt utvecklingsagenten via AI-assistenten i användargränssnitt som Cloud Manager eller Experience Hub.

**Så här kommer du åt utvecklingsagenten via Cloud Manager:**

1. Kom igång genom att klicka på [Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home) för att öppna startsidan.

   ![Adobe Experience Cloud hemsida](/help/implementing/cloud-manager/assets/experience-cloud-experiencemanager.png)

1. Klicka på **Cloud Manager** i den vänstra listen under rubriken **Tjänster**.

   ![Listrutan med förinställningen Innehållsförfattare är markerad](/help/implementing/cloud-manager/assets/experience-hub-role-selection.png)

   >[!IMPORTANT]
   >
   >Vilka widgetar, verktyg och artefakter som visas beror på användarens personlighet, berättiganden och AEM driftsättningstyp (AEM as a Cloud Service eller Managed Services 6.5/6.5 LTS).

1. Klicka på ikonen **Översikt** Översikt **![i den vänstra listen under ](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg)Program**.

1. Klicka på en pipeline på sidan **Programöversikt** på kortet **Pipelines**.

   ![Markerad pipeline](/help/ai-in-aem/agents/development/assets/dev-agent-pipeline-select.png)

1. Observera den misslyckade pipeline på sidan **Build and Code Scanning**.

   ![Pipelinefel som den visas på sidan för kodsökning och bygge](/help/ai-in-aem/agents/development/assets/dev-agent-pipeline-failure.png)

1. Klicka på ikonen **AI-assistenten** i det övre högra hörnet av AEM användargränssnitt (antingen från Cloud Manager-sidor eller från författarinstansen av AEM-miljöerna).

   ![AI Assistant-ikon i verktygsfältet](/help/implementing/cloud-manager/assets/ai-assistant-icon.png)

   Se även [AI-assistenten i AEM](/help/implementing/cloud-manager/ai-assistant-in-aem.md).

1. Skriv din fråga eller fråga i textrutan på panelen **AI Assistant** längst ned och tryck sedan på `Enter` eller klicka på ![ikonen Skicka](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg).

   Till exempel:
   *Analysera felet i pipeline och felsökningen för &quot;no-access&quot; i programmet &quot;eda-org-01-no-access&quot;.*

   Uppmaningen ger följande svar.

   ![AI Assistant-fråga och resulterande svar](/help/ai-in-aem/agents/development/assets/dev-agent-prompt-response.png)


## Behörigheter {#permissions}

Utvecklingsagentens pipeline-felsökningsjobb kräver antingen rollen Cloud Manager - Developer eller rollen Cloud Manager - Program Manager.

## Exempeluppmaningar {#sample-prompts}

| Fråga | Resultat |
| --- | --- |
| *Felsök min felaktiga pipeline* | Utför en analys av varför en pipeline misslyckades. Om det är oklart vilken pipeline som hänvisas till kommer ytterligare frågor att tillfrågas användaren. |
| *Visa mina misslyckade pipelines för huvudprogrammet för programmet.* | Resultatet kan variera, men den här uppmaningen visar en tabell med misslyckade pipelines, med ett uppföljningsförslag som refererar till en viss pipeline som ska analyseras. |
| *Analysera min misslyckade pipeline med namnet&quot;Dev Pipeline&quot;.* | Den här uppmaningen resulterar i en analys av den misslyckade pipeline med förslag på åtgärder. Om flera fel uppstår tillfrågas användaren om ytterligare frågor. |
| *Felsöka pipeline-körning 1234567* | Genom att ange ett exakt ID för pipeline-körning utförs en pipeline-analys. |

## Funktioner som inte är tillgängliga {#out-of-scope-features}

Felsökning av pipeline utförs i stegen för att bygga en hel pipeline. Om du vill se andra typer av pipeline och steg felsöker du genom att hämta och inspektera loggarna.

Se [Åtkomst- och hämtningsloggar](/help/implementing/cloud-manager/manage-logs.md).
