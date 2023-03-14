---
title: Notiscenter
description: Utnyttja Notiscenter för att enkelt vidta åtgärder i samband med incidenter och annan viktig information
hidefromtoc: true
source-git-commit: a5977c667d831c47d41cd86b68e9196fbe726899
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# Notiscenter {#notification-center}

>[!NOTE]
>Den här funktionen har inte släppts.

När konfigurationen är klar skickar AEM som Cloud Service meddelanden om viktig information som kunderna ska vidta åtgärder för. Exempel på meddelanden är till exempel en blockerad kö eller en uppsättning uppgifter som förfaller. Den fullständiga uppsättningen meddelandetyper kan visas i [tabellen nedan](#current-notification-types)och kommer att byggas ut med tiden. Meddelanden tas emot via både e-post och som en ny post under meddelandewidgeten, som du kommer åt genom att klicka på klockikonen i det övre högra hörnet i hela Adobe Experience Cloud. Meddelandeinställningar kan konfigureras.

När ett meddelande tas emot kan du klicka på det för att öppna AEM as a Cloud Service Notiscenter med en popup som visar ytterligare kontext som förklarar den rekommenderade åtgärden som en kund ska vidta.

Förutom att visa information om det meddelande du just klickade på fungerar Notiscenter som ett nav där du kan visa och hantera den aktuella och äldre meddelandeuppsättningen. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

Det finns två meddelandekategorier på hög nivå:

1. Incidenter - en händelse har inträffat, som vanligtvis kräver snabb lösning. Du kan till exempel lösa en blockerad kö
1. Proaktiv - Adobe har en rekommendation om en åtgärd som en kund ska vidta inom den närmaste framtiden. Om du till exempel vill sluta referera till ett föråldrat användargränssnitt.

Se [tabellen nedan](#current-notification-types) för de meddelanden som stöds.

På skärmen Notiscenter kan du välja ett specifikt program och en viss miljö, vilket filtrerar för det omfånget.

## Konfiguration {#configuration}

Följ stegen nedan för att konfigurera mottagningsmeddelanden:

1. Skapa följande produktprofiler enligt beskrivningen [i den här artikeln](/help/journey-onboarding/user-groups.md), och tilldela rätt Adobe-ID från din organisation till dessa profiler.
1. Kontrollera inställningarna för meddelandekonfigurationen. [På den här sidan](https://experience.adobe.com/preferences/notification-section)kontrollerar du att prenumerationen på Experience Manager är aktiverad och att **Övriga** är markerad. Vi rekommenderar dessutom att avsnittet E-post är inställt på **Snabbmeddelanden** så att du får meddelanden omedelbart efter att en incident har inträffat.

>[!NOTE]
>Prenumerationer fungerar på organisationsnivå så att prenumeranterna får meddelanden om alla program och miljöer i dessa program.

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

## Aktuella meddelandetyper {#current-notification-types}

Tabellen nedan visar de meddelandetyper som stöds

| Meddelandetyp | Relaterad produktprofil | Korrigeringsåtgärd |
|---|---|---|
| Blockerad replikeringskö | Incident | Avblockera kön genom att följa instruktionerna i [Replikeringsdokumentation](/help/operations/replication.md#troubleshooting) |
| S2S-certifikatet förfaller | Proaktiv | Lär dig hur du uppdaterar en autentiseringsuppgift i dialogrutan [Genererar åtkomsttoken för dokumentation för API:er på serversidan](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |
