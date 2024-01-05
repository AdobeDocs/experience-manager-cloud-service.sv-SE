---
title: Actions Center
description: Utnyttja åtgärdscentret för att enkelt hantera incidenter och annan viktig information
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 0%

---

# Actions Center {#actions-center}

AEM när Cloud Servicen skickar e-postmeddelanden till Åtgärdscenter när allvarliga incidenter inträffar som kräver omedelbara åtgärder och proaktiva rekommendationer för optimering. Exempel är en blockerad kö eller en uppsättning med förfallna autentiseringsuppgifter. Den fullständiga uppsättningen med meddelandetyper i Åtgärdscenter kan visas i [tabellen nedan](#supported-notification-types), som kommer att byggas ut med tiden.

När ett e-postmeddelande från Åtgärdscenter tas emot kan du klicka på det för att öppna AEM as a Cloud Service åtgärdscenter med en popup som visar ytterligare kontext som förklarar vilken åtgärd en kund ska vidta.

Förutom att visa information om det nyligen klickade e-postmeddelandet fungerar Åtgärdscenter som ett nav där du kan visa och hantera den aktuella och äldre meddelandeuppsättningen. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers do not find it) -->

Det finns två högnivåkategorier med meddelanden som visas i Åtgärdscenter:

1. Driftsincidenter - en händelse har inträffat, som vanligtvis kräver snabb lösning. Du kan till exempel lösa en blockerad kö.
1. Förebyggande rekommendationer - Adobe har en rekommendation om en åtgärd som en kund ska vidta inom den närmaste framtiden. Om du till exempel vill sluta referera till ett föråldrat användargränssnitt.

Se [tabellen nedan](#supported-notification-types) för de meddelanden som för närvarande stöds i Åtgärdscenter.

Från Åtgärdscenter kan du välja ett specifikt program och en viss miljö, vilket filtrerar för det omfånget.

## Konfiguration {#configuration}

Skapa de produktprofiler som beskrivs för att konfigurera mottagning av e-postmeddelanden från Åtgärdscenter [i den här artikeln](/help/journey-onboarding/notification-profiles.md), nämligen Incident Notification - Cloud Service and Proactive Notification - Cloud Service. Tilldela även rätt Adobe-ID från din organisation till dessa profiler. Detta gör att en administratör kan avgöra vilka användare som är kvalificerade att ta emot dessa e-postmeddelanden.

>[!NOTE]
>Actions Center-funktionen för e-postmeddelanden fungerar på organisationsnivå så att prenumeranterna får meddelanden om alla program och miljöer i dessa program.

## Detaljerat användarflöde {#detailed-user-flow}

Om du klickar på e-postmeddelandet kommer du till Åtgärdscenter, där det visas en snabbmeny med information om vilket meddelande du klickade på och i vissa fall länkar till ytterligare information som beskriver hur du ska vidta korrigerande åtgärder. Du kan även komma åt Actions Center direkt på [https://experience.adobe.com/aem/actions-center](https://experience.adobe.com/aem/actions-center/), där du kan välja rätt program och miljö.

![Incidentinformation](/help/operations/assets/incident-details.png)

Klicka på **Läs mer** link navigerar användaren till den här artikeln, där meddelandetypen kan refereras i [tabell med meddelandetyper som stöds](#supported-notification-types) nedan, som ger vägledning om vilka åtgärder som ska vidtas.

I Åtgärdscenter kan du se en lista med andra senaste meddelanden. Vi rekommenderar att du i listan Åtgärder bekräftar ett meddelande som signalerar till Adobe att din organisation känner till uppgiften och senare löser meddelandet när en korrigeringsåtgärd har vidtagits.

![Meddelandelista](/help/operations/assets/notification-list.png)

I de flesta fall bör popup-fönstret innehålla all den kontext som behövs för att lösa problemet. Om du har frågor om Adobe Support kan du klicka på **Kontakta supporten** i popup-fönstret. Då öppnas ett formulär där du kan beskriva frågan och skicka in den för att skapa en supportanmälan, som även innehåller en hänvisning till den specifika anmälan så att en supporttekniker från Adobe har rätt sammanhang.

![Kontakta support 1](/help/operations/assets/contact-support1.png)

![Kontakta support 2](/help/operations/assets/contact-support2.png)

Precis som alla supportärenden visas de i [Fliken Adobe Admin Console Supportärenden](https://helpx.adobe.com/enterprise/using/support-for-enterprise.html), där du kan spåra det och lägga till ytterligare kommentarer.

![Stöd för Admin Console](/help/operations/assets/admin-console-support.png)

## Vilka meddelanden visas? {#which-notification}

AEM as a Cloud Service har flera typer av meddelanden, men bara en delmängd visas i Åtgärdscenter, vilket framgår av tabellen nedan.

| Meddelandetyp | Beskrivning | Konfigurera | Visas i Åtgärdscenter |
|---|---|---|---|
| Driftincidenter | Kritiska incidenter som kräver omedelbara åtgärder | Användare tilldelad produktprofilen&quot;Incident Notification - Cloud Service&quot; | X |
| Förebyggande rekommendationer | Optimeringar som ska planeras | Användare tilldelad produktprofilen &quot;Proaktivt meddelande - Cloud Service&quot; | X |
| Molnhanterarens pipeline-status | Information om tillståndet för dina rörledningar | Användare med Business Owner, Program Manager eller Deployment Manager-roller, kryssrutan Övrigt markerad i [Inställningar för Experience Cloud](https://experience.adobe.com/preferences), som [beskrivs här](/help/implementing/cloud-manager/notifications.md). |   |

## Meddelandetyper som stöds {#supported-notification-types}

I följande tabell visas de meddelandetyper som för närvarande stöds i Åtgärdscenter. Meddelanden är för närvarande begränsade till produktionsmiljöer.

| Meddelandetyp | Relaterad produktprofil | Korrigeringsåtgärd |
|---------------------------------|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Blockerad replikeringskö | Incident | Avblockera kön genom att följa instruktionerna i [Replikeringsdokumentation](/help/operations/replication.md#troubleshooting) |
| Ogiltig beständig GraphQL-fråga | Incident | Åtgärda den ogiltiga GraphQL-frågan genom att referera till [Beständiga GraphQL-frågor felsökningsdokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/headless/graphql-api/persisted-queries-troubleshoot.html) |
| S2S-certifikatet förfaller | Proaktiv | Lär dig hur du uppdaterar en autentiseringsuppgift i dialogrutan [Genererar Access-token för dokumentation för API:er på serversidan](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |
