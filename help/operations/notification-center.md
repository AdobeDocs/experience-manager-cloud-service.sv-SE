---
title: Notiscenter
description: Utnyttja Notiscenter för att enkelt vidta åtgärder i samband med incidenter och annan viktig information
hidefromtoc: true
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
source-git-commit: 283493187142e1aeaaf272818bb9b7921841ed67
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 0%

---

# Notiscenter {#notification-center}

>[!NOTE]
>Den här funktionen har inte släppts.

AEM som Cloud Service skickar meddelanden när allvarliga incidenter inträffar som kräver omedelbara åtgärder, samt proaktiva rekommendationer för optimering. Exempel är en blockerad kö eller en uppsättning uppgifter som förfaller. hela uppsättningen meddelandetyper kan visas i [tabellen nedan](#supported-notification-types), som kommer att byggas ut med tiden.

Dessa meddelanden kan konfigureras att tas emot både via e-post och under meddelandewidgeten, som du kommer åt genom att klicka på klockikonen i det övre högra hörnet i Adobe Experience Cloud.

När ett meddelande tas emot kan du klicka på det för att öppna AEM as a Cloud Service Notiscenter med en popup som visar ytterligare kontext som förklarar vilken åtgärd en kund ska vidta.

Förutom att visa information om det meddelande du just klickade på fungerar Notiscenter som ett nav där du kan visa och hantera den aktuella och äldre meddelandeuppsättningen. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

Det finns två högnivåkategorier med meddelanden som visas i Notiscenter:

1. Driftsincidenter - en händelse har inträffat, som vanligtvis kräver snabb lösning. Du kan till exempel lösa en blockerad kö.
1. Förebyggande rekommendationer - Adobe har en rekommendation om en åtgärd som en kund ska vidta inom den närmaste framtiden. Om du till exempel vill sluta referera till ett föråldrat användargränssnitt.

Se [tabellen nedan](#supported-notification-types) för de meddelanden som stöds.

I Notiscenter kan du välja ett specifikt program och en viss miljö, vilket filtrerar för det omfånget.

## Konfiguration {#configuration}

Följ stegen nedan för att konfigurera mottagningsmeddelanden:

1. Skapa följande produktprofiler enligt beskrivningen [i den här artikeln](/help/journey-onboarding/notification-profiles.md)och du kan även tilldela rätt Adobe-ID från din organisation till dessa profiler. Detta gör att en administratör kan avgöra vilka användare som är kvalificerade att ta emot dessa meddelanden.
1. Varje tilldelad användare som tilldelats i föregående steg kan konfigurera hur de vill få sina meddelanden. På [Experience Cloud inställningssida](https://experience.adobe.com/preferences/notification-section)kontrollerar du att prenumerationen på Experience Manager är aktiverad och att **Driftincidenter** och **Förebyggande rekommendationer** kryssrutor är markerade för både in-app- och e-postkolumner (se bilden nedan). Vi rekommenderar dessutom att avsnittet E-post är inställt på **Snabbmeddelanden** så att meddelanden tas emot omedelbart när en incident inträffar.

![Konfigurera prenumerationer](/help/operations/assets/configure-subscriptions.png)

>[!NOTE]
>Meddelanden fungerar på organisationsnivå så att prenumeranterna får meddelanden om alla program och miljöer i dessa program.

## Detaljerat användarflöde {#detailed-user-flow}

Om du klickar på e-postmeddelandet kommer du till Notiscenter, med en popup-meny som visar sammanhanget för det meddelande du klickade på och i vissa fall länkar till ytterligare information som beskriver hur du ska vidta korrigerande åtgärder.

![Incidentinformation](/help/operations/assets/incident-details.png)

Klicka på **Läs mer** länkar användaren till den här artikeln, där meddelandet kan refereras i tabellen nedan, som ger vägledning om vilka åtgärder som ska vidtas.

I Notiscenter kan du se en lista med andra senaste meddelanden. Vi rekommenderar att du i åtgärdslistan bekräftar ett meddelande för att informera Adobe om att din organisation känner till uppgiften och att senare lösa meddelandet när en korrigeringsåtgärd har vidtagits.

![Meddelandelista](/help/operations/assets/notification-list.png)

I de flesta fall bör anmälan innehålla alla nödvändiga kontexter för att lösa problemet. Om du har frågor om Adobe Support kan du klicka på **Kontakta supporten** i meddelandefönstret. Då öppnas ett formulär där du kan beskriva frågan och skicka in den för att skapa supportanmälan, som även innehåller en hänvisning till den specifika anmälan så att en supporttekniker från Adobe har rätt sammanhang.

![Kontakta support 1](/help/operations/assets/contact-support1.png)

![Kontakta support 2](/help/operations/assets/contact-support2.png)

Precis som alla supportärenden visas de i [Fliken Adobe Admin Console Supportärenden](https://helpx.adobe.com/enterprise/using/support-for-enterprise.html), där du kan spåra det och lägga till ytterligare kommentarer.

![Stöd för Admin Console](/help/operations/assets/admin-console-support.png)

## Vilka meddelanden visas? {#which-notification}

AEM as a Cloud Service har flera typer av meddelanden, men bara en delmängd visas i Notiscenter, enligt tabellen nedan.

| Meddelandetyp | Beskrivning | Konfigurera | Visas i Notiscenter |
|---|---|---|---|
| Driftincidenter | Kritiska incidenter som kräver omedelbara åtgärder | Användare tilldelad produktprofilen&quot;Incidentmeddelande - Cloud Service&quot;, kryssrutan&quot;Driftincidenter&quot; markerad i [Inställningar för Experience Cloud](https://experience.adobe.com/preferences) | X |
| Förebyggande rekommendationer | Optimeringar som ska planeras | Användare tilldelad produktprofilen &quot;Proaktiv avisering - Cloud Service&quot;, kryssrutan &quot;Proaktiva rekommendationer&quot; markerad i [Inställningar för Experience Cloud](https://experience.adobe.com/preferences) | X |
| Molnhanterarens pipeline-status | Information om tillståndet för dina rörledningar | Användare med Business Owner, Program Manager eller Deployment Manager-roller, kryssrutan &quot;Others&quot; (Övriga) markerad i [Inställningar för Experience Cloud](https://experience.adobe.com/preferences) |  |

## Meddelandetyper som stöds {#supported-notification-types}

I följande tabell visas de meddelandetyper som stöds för närvarande.

| Meddelandetyp | Relaterad produktprofil | Korrigeringsåtgärd |
|---|---|---|
| Blockerad replikeringskö | Incident | Avblockera kön genom att följa instruktionerna i [Replikeringsdokumentation](/help/operations/replication.md#troubleshooting) |
| S2S-certifikatet förfaller | Proaktiv | Lär dig hur du uppdaterar en autentiseringsuppgift i dialogrutan [Genererar åtkomsttoken för dokumentation för API:er på serversidan](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |

