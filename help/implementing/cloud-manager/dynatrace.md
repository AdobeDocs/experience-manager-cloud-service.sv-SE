---
title: Dynatrace
description: Lär dig använda Dynatrace med AEM as a Cloud Service
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
source-git-commit: a234f2a00c51bcb23b0c52feac9971259d26b8c3
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# Dynatrace {#dynatrace}

Adobe ger möjlighet att använda Dynatrace för att övervaka AEM as a Cloud Service som en del av företagsdistributionen, identifiera orsaken till eventuella problem och vidta åtgärder för att åtgärda dem efter behov.

Med Dynatrace får du smidig synlighet för alla dina AEM program. Dynatrace ger en heltäckande bild av slutanvändarens upplevelse genom att automatiskt identifiera dina AEM och visualisera deras beroenden från webbplatsen till behållaren till molntjänsten. Kombinerat med kompletta spår i alla nivåer och riktig användarövervakning, lyft era AEM innehållsledda upplevelser till nästa nivå utan mellanrum eller blinda fläckar. Om några avvikelser uppstår diagnostiserar Dynatrace dem i realtid, med Davis AI-motorn, och identifierar orsaken till den trasiga koden innan kunderna påverkas, vilket minimerar den genomsnittliga reparationstiden.

Mer information om Dynatrace finns i [Integrering med Adobe AEM Cloud Service](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/).

![Prestandamätningar för AEM författare och utgivare](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## Integrera Dynatracing med AEM as a Cloud Service {#integrating-dynatrace-with-aem-as-a-cloud-service}

Dynatracekunder kan övervaka sina AEM genom att begära anslutning via en kundsupportbiljett.

Nedan beskrivs mer ingående information om anslutningsbegäranden:

| **Fält** | **Beskrivning** |
|---|---|
| URL för Dynatrace Environment | Din URL för Dynatracemiljö.<br><br>För Dynatrace SaaS-kunder är formatet `https://<your-environment-id>.live.dynatrace.com`.<br><br>För kunder som är hanterade med Dynatrace är formatet `https://<your-managed-url>/e/<environmentId>` |
| Dynatrace Environment ID | Ditt ID för Dynatracemiljö. Se [Hämta information om Dynatrace-miljön](#get-dynatrace-env-info) för hur man får det här. |
| Dynatrace Environment-token | Din miljötoken för Dynatracing. Se [Hämta information om Dynatrace-miljön](#get-dynatrace-env-info) för hur man får det här.<br><br>Detta bör betraktas som en hemlighet, så använd lämpliga säkerhetsrutiner. Lösenordsskydda den till exempel på en webbplats **zerobin.net** som kundsupportbiljetten kan referera till tillsammans med lösenordet. |
| Åtkomsttoken för Dynatrace API | API-åtkomsttoken för din Dynatrace-miljö.  Se [Skapa en åtkomsttoken för Dynatrace API](#create-dynatrace-access-token) för hur du skapar det här.<br><br>Detta bör betraktas som en hemlighet, så använd lämpliga säkerhetsrutiner. Lösenordsskydda den till exempel på en webbplats **zerobin.net** som kundsupportbiljetten kan referera till tillsammans med lösenordet.<br><br>Obs! Detta är endast nödvändigt för Dynatracehantering. |
| Dynatrace ActiveGate-port | Din ActiveGate-port för Dynatrace som den AEM integreringen ska ansluta till.<br><br>Obs! Detta är endast nödvändigt för Dynatracehantering. |
| Dynatrace ActiveGate Network Zone | Dina [ActiveGate-nätverkszonen för Dynatracus](https://docs.dynatrace.com/docs/manage/network-zones) för att AEM övervaka data effektivt över datacenter och nätverksregioner.<br><br>Obs! En ActiveGate-nätverkszon för Dynatrace är valfri. |
| AEM miljö-ID:n | AEM miljö-ID:n för Dynatracs bildskärm. |

>[!NOTE]
>
>När Dynatrace är integrerat flödar data inte längre till andra APM-verktyg som New Relic, om det tidigare var aktiverat.


## Skapa en åtkomsttoken för Dynatrace API {#create-dynatrace-access-token}

1. Logga in i din Dynatracermiljö.
1. Gå till Hantera > Åtkomsttoken på menyn Dynatracetyp.
1. Välj Generera ny token.
1. Definiera ett tokennamn.

1. Valfritt: Ange ett förfallodatum. Generera en ny token innan den upphör att gälla.
1. Ange tokenomfånget till PaaS-integrering - hämtning av installationsprogram
1. Välj Generera token.
1. Kopiera den genererade åtkomsttoken och lagra den på en säker plats.


## Hämta information om Dynatrace-miljön {#get-dynatrace-env-info}

1. Kör följande API-begäran till din Dynattrace-miljö:

`curl -X GET "<environmentUrl>/api/v1/deployment/installer/agent/connectioninfo" -H "accept: application/json" -H "Authorization: Api-Token <accessToken>"`

Ersätt \&lt;environmenturl> med din Dynatracemiljö-URL och \&lt;accesstoken> med din skapade API-åtkomsttoken.

1. Kopiera \&lt;environmentid> och \&lt;environmenttoken> från svarsnyttolasten och lagra dem på en säker plats.

```
{
   "tenantUUID": "<environmentId>",
   "tenantToken": "<environmentToken>",
   "communicationEndpoints": [
   ... 
   ],
   "formattedCommunicationEndpoints": "<endpoints>" 
}
```


