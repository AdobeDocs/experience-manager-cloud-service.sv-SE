---
title: Dynatrace OneAgent
description: Lär dig använda Dynatracs OneAgent med AEM as a Cloud Service
source-git-commit: 9379e6a1ec323ff4f05e994e9265da1363b4a3df
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---


# Dynatrace OneAgent {#dynatrace-oneagent}

Adobe har möjlighet att använda Dynatracs OneAgent för att övervaka AEM as a Cloud Service som en del av en företagsdistribution, identifiera orsaken till eventuella problem och vidta åtgärder för att åtgärda dem efter behov. <!-- When GA, add: Read this [Dynatrace article](https://www.dynatrace.com/hub/detail/adobe-experience-manager/) about AEM monitoring to learn more. -->

## Integrera OneAgent med AEM as a Cloud Service {#integrating-oneagent-with-aem-as-a-cloud-service}

Dynatrace OneAgent-kunder kan övervaka AEM genom att begära anslutningsbarhet via en kundsupportbiljett.

Nedan beskrivs mer ingående information om anslutningsbegäranden:

| **Fält** | **Beskrivning** |
|---|---|
| URL för Dynatrace Environment | Din URL för Dynatracemiljö.<br><br>För Dynatrace SaaS-kunder är formatet `https://<you-environment-id>.live.dynatrace.com`.<br><br>För kunder som är hanterade med Dynatrace är formatet `https://<your-managed-url>/e/<environmentId>` |
| Dynatrace Environment ID | Ditt ID för Dynatracemiljö, som finns i URL:en för miljön |
| Dynatrace Environment-token | Din OneAgent-miljötoken. Läs dokumentationen för Dynatrace om hur du skapar detta.<br><br>Detta bör betraktas som en hemlighet, så använd lämpliga säkerhetsrutiner. Lösenordsskydda den till exempel på en webbplats **zerobin.net** som kundsupportbiljetten kan referera till tillsammans med lösenordet. |
| Åtkomsttoken för Dynatrace API | API-åtkomsttoken för din Dynatrace-miljö. Läs dokumentationen för Dynatrace om hur du skapar detta.<br><br>Detta bör betraktas som en hemlighet, så använd lämpliga säkerhetsrutiner. Lösenordsskydda den till exempel på en webbplats **zerobin.net** som kundsupportbiljetten kan referera till tillsammans med lösenordet.<br><br>Obs! Detta är endast nödvändigt för Dynatracehantering. |
| Dynatrace ActiveGate-port | Din ActiveGate-port för Dynatrace som OneAgent ska ansluta till.<br><br>Obs! Detta är endast nödvändigt för Dynatracehantering. |
| AEM miljö-ID:n | Den eller de AEM miljö-ID som Dynatracs ska övervaka. |


