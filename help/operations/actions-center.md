---
title: Actions Center
description: Utnyttja åtgärdscentret för att enkelt hantera incidenter och annan viktig information
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
feature: Operations
role: Admin
source-git-commit: 7a05b5f19d9d59ad438c18ce510e0c54acd49a93
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 0%

---

# Actions Center {#actions-center}

AEM skickar e-postmeddelanden till Actions Center när allvarliga incidenter inträffar som kräver omedelbara åtgärder och proaktiva rekommendationer för optimering. Exemplen innehåller en blockerad kö eller en uppsättning med förfallande autentiseringsuppgifter. Den fullständiga uppsättningen med meddelandetyper i Åtgärdscenter kan visas i [tabellen nedan](#supported-notification-types), som kommer att utökas över tid.

När ett e-postmeddelande från Åtgärdscenter tas emot kan du klicka på det för att öppna AEM as a Cloud Service Actions Center med en popup-meny som visar ytterligare kontext som förklarar vad kunden ska göra.

Förutom att visa information om det nyligen klickade e-postmeddelandet fungerar Åtgärdscenter som ett nav där du kan visa och hantera den aktuella och äldre meddelandeuppsättningen. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers do not find it) -->

Det finns två högnivåkategorier med meddelanden som visas i Åtgärdscenter:

1. Driftsincidenter - en händelse har inträffat, som vanligtvis kräver snabb lösning. Du kan till exempel lösa en blockerad kö.
1. Proaktiva rekommendationer - Adobe har en rekommendation om en åtgärd som en kund ska vidta inom den närmaste framtiden. Om du till exempel vill sluta referera till ett föråldrat användargränssnitt.

Se tabellen [nedan](#supported-notification-types) för de meddelanden som för närvarande stöds i Åtgärdscenter.

Från Åtgärdscenter kan du välja ett specifikt program och en viss miljö, vilket filtrerar för det omfånget.

## Konfiguration {#configuration}

Om du vill konfigurera mottagning av e-postmeddelanden från Åtgärdscenter skapar du produktprofilerna enligt beskrivningen i [Meddelandeprofiler](/help/journey-onboarding/notification-profiles.md), nämligen Incident Notification - Cloud Service och Proactive Notification - Cloud Service. Tilldela även rätt Adobe-ID från din organisation till dessa profiler. Detta gör att en administratör kan avgöra vilka användare som är kvalificerade att ta emot dessa e-postmeddelanden.

>[!NOTE]
>Actions Center-funktionen för e-postmeddelanden fungerar på organisationsnivå så att prenumeranterna får meddelanden om alla program och miljöer i dessa program.

## Detaljerat användarflöde {#detailed-user-flow}

Om du klickar på e-postmeddelandet kommer du till Åtgärdscenter, där det visas en snabbmeny med information om vilket meddelande du klickade på och i vissa fall länkar till ytterligare information som beskriver hur du ska vidta korrigerande åtgärder. Du kan även nå Åtgärdscenter direkt på [https://experience.adobe.com/aem/actions-center](https://experience.adobe.com/aem/actions-center/), där du kan välja relevant program och miljö.

![Incidentinformation](/help/operations/assets/incident-details.png)

Om du klickar på länken **Läs mer** navigerar användaren till den här artikeln, där meddelandetypen kan refereras i tabellen [Meddelandetyper som stöds](#supported-notification-types) nedan, som ger vägledning om vilka åtgärder som ska vidtas.

I Åtgärdscenter kan du se en lista med andra senaste meddelanden. Vi rekommenderar att du i listan Åtgärder bekräftar ett meddelande som signalerar till Adobe att din organisation känner till uppgiften och sedan löser problemet när korrigeringsåtgärder har vidtagits.

![Meddelandelista](/help/operations/assets/notification-list.png)

I de flesta fall bör popup-fönstret innehålla all den kontext som behövs för att lösa problemet. Om du har frågor om Adobe Support kan du klicka på länken **Kontakta support** i popup-fönstret. Här visas ett formulär där du kan beskriva frågan och skicka in den för att skapa en supportanmälan, som även innehåller en hänvisning till den specifika anmälan så att en Adobe supporttekniker har rätt sammanhang.

![Kontakta support ](/help/operations/assets/contact-support1.png)

![Kontakta support 2](/help/operations/assets/contact-support2.png)

Precis som alla supportärenden visas det på fliken [Adobe Admin Console supportärenden](https://helpx.adobe.com/se/enterprise/using/support-for-enterprise.html), där du kan spåra det och lägga till ytterligare kommentarer.

![Admin Console Support](/help/operations/assets/admin-console-support.png)

## Vilka meddelanden visas? {#which-notification}

AEM as a Cloud Service har flera typer av meddelanden, men bara en delmängd visas i Åtgärdscenter, vilket framgår av tabellen nedan.

| Meddelandetyp | Beskrivning | Konfigurera | Visas i Åtgärdscenter |
|---------------------------------|-----------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------|
| Driftincidenter | Kritiska incidenter som kräver omedelbara åtgärder | Användare tilldelad produktprofilen&quot;Incident Notification - Cloud Service&quot; | X |
| Förebyggande rekommendationer | Optimeringar som ska planeras | Användare tilldelad produktprofilen &quot;Proactive Notification - Cloud Service&quot; | X |
| Cloud Manager pipeline-status | Information om tillståndet för dina rörledningar | Användare med Business Owner, Program Manager eller Deployment Manager-roller, kryssrutan &quot;Others&quot; (Övriga) markerad i [Experience Cloud Preferences](https://experience.adobe.com/preferences), se [Notifications](/help/implementing/cloud-manager/notifications.md). |                           |

## Meddelandetyper som stöds {#supported-notification-types}

I följande tabell visas de meddelandetyper som för närvarande stöds i Åtgärdscenter. Meddelanden är för närvarande begränsade till produktionsmiljöer.

| Meddelandetyp | Relaterad produktprofil | Korrigeringsåtgärd |
|---------------------------------|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Blockerad replikeringskö | Incident | Avblockera kön genom att följa instruktionerna i [replikeringsdokumentationen](/help/operations/replication.md#troubleshooting) |
| Ogiltig beständig GraphQL-fråga | Incident | Åtgärda den ogiltiga GraphQL-frågan genom att referera till [Persisted GraphQL queries felsökningsdokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/headless/graphql-api/persisted-queries-troubleshoot.html?lang=sv-SE) |
| Trafikrydda vid ursprung | Incident | Skydda ditt ursprung genom att konfigurera trafikfilterregler för hastighetsbegränsning som utlöser vid lägre tröskelvärden än standardtrafikökningen vid ursprungsvarningen.  Se avsnittet [Blockera DoS- och DDoS-attacker med trafikregler](/help/security/traffic-filter-rules-including-waf.md#blocking-dos-and-ddos-attacks-using-traffic-filter-rules) i dokumentationen för trafikfilterregler, som refererar till en självstudiekurs. |
| Regler för CDN-trafikfilter har utlösts | Incident | Om den matchande trafikfilterregeln reflekterar en attack, och din plats inte blockerar trafiken, skyddar du din plats genom att konfigurera en trafikfilterregel i blockeringsläge. Se avsnittet [Skydda webbplatser med trafikfilterregler (inklusive WAF-regler)](/help/security/traffic-filter-rules-including-waf.md#tutorial-protecting-websites) i dokumentationen om trafikfilterregler, som refererar till en självstudiekurs. |
| Vidarebefordringsfel för skräppostloggen | Incident | Kontrollera att Splunk-slutpunkten fungerar och kan nås från din AEM Cloud-tjänstmiljö. Mer information om vidarebefordran av loggar finns i [vidarebefordringsdokumentationen för skräppost](/help/implementing/developing/introduction/logging.md#splunk-logs). Om du behöver hjälp med felsökning eller behöver göra ändringar i loggningskonfigurationen kontaktar du Adobe. |
| Sidorna innehåller ett stort antal noder | Proaktiv | Minska det totala antalet noder på en sida. Läs [Dokumentation om sidkomplexitet](https://experienceleague.adobe.com/sv/docs/experience-manager-pattern-detection/table-of-contents/pcx) | |
| Stort antal arbetsflödesinstanser som körs | Proaktiv | Avsluta pågående arbetsflöden som inte längre behövs. Lär dig hur du [konfigurerar ett rensningsjobb](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/operations/maintenance) |               |
| S2S-certifikatet förfaller | Proaktiv | Lär dig hur du uppdaterar en autentiseringsuppgift i [Genererar åtkomsttoken för API:er på serversidan](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) | Högt antal anslutningar | Proaktiv | Lär dig mer om anslutningspoolning i [Anslutningspoolning tillsammans med dokumentationen för avancerat nätverk](/help/security/configuring-advanced-networking.md#connection-pooling-advanced-networking) |
| Mappning av tjänstanvändare har tagits bort | Proaktiv | Lär dig hur du använder det nyare användarmappningsformatet för Sling-tjänsten, vilket anges i [Bästa praxis för användarmappning för Sling-tjänsten och Användardefinition för tjänsten](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/security/best-practices-for-sling-service-user-mapping-and-service-user-definition) |
| Högt antal anslutningar | Proaktiv | Läs mer om anslutningspoolning i [dokumentationen för avancerat nätverk](/help/security/configuring-advanced-networking.md#connection-pooling-advanced-networking) |  |
| Användare som läggs till direkt i en anpassad grupp | Proaktiv | Användare måste läggas till i relevanta IMS-grupper och dessa IMS-grupper måste läggas till som medlemmar i AEM-grupper. Justera med [IMS-tips](/help/security/ims-support.md) | |
| JCR-innehåll saknas | Proaktiv | Lägg till noden JCR-innehåll som saknas. Mer information finns i [dokumentationen för Assets Content Validator](https://experienceleague.adobe.com/sv/docs/experience-manager-pattern-detection/table-of-contents/acv) | |
| Slutförda arbetsflöden har inte rensats | Proaktiv | Minimera antalet arbetsflödesinstanser och förbättra resultatet genom att rensa arbetsflödesinstanser som är mer än 90 dagar gamla. Lär dig hur du [konfigurerar underhållsaktiviteter](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/operations/maintenance) | |
| Sling-resurstypen saknas på sidan | Proaktiv | Lägg till saknad nod för Sling-resurstyp. Mer information finns i [dokumentationen för Assets Content Validator](https://experienceleague.adobe.com/sv/docs/experience-manager-pattern-detection/table-of-contents/acv) | |
| Långsam fråga | Proaktiv | Åtgärda långsamma frågor genom att definiera korrekta indexdefinitioner enligt [JCQ-frågeformuläret](https://experienceleague.adobe.com/docs/experience-manager-65/assets/JCR_query_cheatsheet-v1.1.pdf?lang=sv-SE) | |
| Fråga utan index | Proaktiv | Undvik att köra en fråga som inte använder ett index - [länk till indexeringsdokumentation](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/operations/indexing) | |
| Avisering om inaktuellt bibliotek | Proaktiv | Ersätt föråldrade paket med de rekommenderade nyare versionerna, enligt beskrivningen i artikeln [Borttagning](/help/release-notes/deprecated-removed-features.md), för att skydda programmet och få bättre prestanda | |
| Inaktuell konfigurationsvarning | Proaktiv | Ersätt föråldrade konfigurationer med de rekommenderade nyare versionerna, enligt beskrivningen i artikeln [Borttagning](/help/release-notes/deprecated-removed-features.md), för att skydda programmet och behålla dess prestanda |
