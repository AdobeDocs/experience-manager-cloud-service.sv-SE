---
title: Dynatrace
description: Lär dig använda Dynatrace med AEM as a Cloud Service
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
source-git-commit: 4fe8ed9c3f7b6589878da3317d15fede819bad54
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# Dynatrace {#dynatrace}

Adobe ger möjlighet att använda Dynatrace för att övervaka AEM as a Cloud Service som en del av företagsdistributionen, identifiera orsaken till eventuella problem och vidta åtgärder för att åtgärda dem efter behov.

Med Dynatrace får du smidig synlighet för alla dina AEM program. Dynatrace ger total insyn i slutanvändarnas upplevelse genom att automatiskt identifiera dina AEM och visualisera deras beroenden från webbplatsen till behållaren till molntjänsten. Kombinerat med kompletta spår i alla nivåer och riktig användarövervakning, lyft era AEM innehållsledda upplevelser till nästa nivå utan mellanrum eller blinda fläckar. Om det uppstår avvikelser diagnostiserar Dynatrace dem i realtid, med Davis AI-motorn, och identifierar orsaken till den trasiga koden innan kunderna påverkas, vilket minimerar den genomsnittliga reparationstiden.

Mer information om Dynatrace finns i [Integrering med Adobe AEM Cloud Service](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/).

![Prestandamätningar för AEM författare och utgivare](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## Integrera Dynatrace med AEM as a Cloud Service {#integrating-dynatrace-with-aem-as-a-cloud-service}

Dynatrace-kunder kan övervaka sina AEM genom att begära anslutning via ett kundsupportärende.

Nedan beskrivs mer ingående information om anslutningsbegäranden:

| **Fält** | **Beskrivning** |
|---|---|
| [!DNL Dynatrace Environment URL] | URL till din Dynatrace-miljö.<br><br>För Dynatrace SaaS-kunder är formatet `https://<your-environment-id>.live.dynatrace.com`.<br><br>För Dynatrace Managed-kunder är formatet `https://<your-managed-url>/e/<environmentId>` |
| [!DNL Dynatrace Environment ID] | Ditt Dynatrace-miljö-ID. Se [Hur får jag information om min Dynatrace-anslutning?](#how-do-i-get-my-dynatrace-connection-details) för hur man får det här. |
| [!DNL Dynatrace Environment Token] | Din Dynatrace-miljötoken. Se [Hur får jag information om min Dynatrace-anslutning?](#how-do-i-get-my-dynatrace-connection-details) för hur man får det här.<br><br>Detta bör betraktas som en hemlighet, så använd lämpliga säkerhetsrutiner. Lösenordsskydda den till exempel på en webbplats **zerobin.net** som kundsupportbiljetten kan referera till tillsammans med lösenordet. |
| [!DNL Dynatrace API access token] | API-åtkomsttoken för din Dynatrace-miljö.  Se [Skapa en API-åtkomsttoken för Dynatrace](#create-dynatrace-access-token) för hur du skapar det här.<br><br>Detta bör betraktas som en hemlighet, så använd lämpliga säkerhetsrutiner. Lösenordsskydda den till exempel på en webbplats **zerobin.net** som kundsupportbiljetten kan referera till tillsammans med lösenordet.<br><br>Obs! Detta krävs endast för Dynatrace Managed. |
| [!DNL Dynatrace ActiveGate Port] | Din ActiveGate-port för Dynatrace som den AEM integreringen ska ansluta till.<br><br>Obs! Detta krävs endast för Dynatrace Managed. |
| [!DNL Dynatrace ActiveGate Network Zone] | Dina [Dynatrace ActiveGate-nätverkszon](https://docs.dynatrace.com/docs/manage/network-zones) för att AEM övervaka data effektivt över datacenter och nätverksregioner.<br><br>Obs! En Dynatrace ActiveGate-nätverkszon är valfri. |
| [!DNL AEM Environment ID(s)] | AEM för Dynatrace att övervaka. |

>[!NOTE]
>
>När Dynatrace väl har integrerats kommer data inte längre att flöda till andra APM-verktyg som New Relic, om det tidigare var aktiverat.

## Vanliga frågor {#faq}

### Vilken licens behöver jag för Dynatrace AEM Monitoring? {#which-license-do-i-need-for-AEM-monitoring}

Dynatrace AEM kräver en Dynatrace-licens. Licensen för Dynatrace AEM baseras på [övervakning i full hög för Kubernetes-behållare](https://docs.dynatrace.com/docs/shortlink/dps-hosts#gib-hour-calculation-for-containers-and-application-only-monitoring). Minnesstorleken för övervakade AEM (författare och utgivartjänster) identifieras automatiskt.

Distributionsspecifikationerna för Adobe per AEM är:

* Produktion: I genomsnitt 4 behållare, 16 GB minne var
* Icke-produktion: I genomsnitt 4 behållare, 8 GB minne var

Mer information om Dynatrace-licenser finns i [Dynatrace Platform Subscription](https://docs.dynatrace.com/docs/shortlink/dynatrace-platform-subscription).

### Hur får jag information om min Dynatrace-anslutning? {#how-do-i-get-my-dynatrace-connection-details}

1. Kör följande API-begäran i din Dynatrace-miljö:

   ```
   curl -X GET "<environmentUrl>/api/v1/deployment/installer/agent/connectioninfo" -H "accept: application/json" -H "Authorization: Api-Token <accessToken>"
   ```


   Ersätt `<environmentUrl>` med din Dynatrace-miljö och `<accessToken>` med din skapade API-åtkomsttoken.

1. Kopiera `<environmentId>` och `<environmentToken>` från svarsnyttolasten och lagra dem på en säker plats.

   ```
   {
      "tenantUUID": "<environmentId>",
      "tenantToken": "<environmentToken>",
      "communicationEndpoints": [...]
   }
   ```

### Skapa en API-åtkomsttoken för Dynatrace {#create-dynatrace-access-token}

1. Logga in i din Dynatrace-miljö.
1. Gå till **[!DNL Access tokens]** och markera **[!DNL Generate new token]**.
1. Definiera en [!DNL token name].
1. Ange tokenomfånget till **[!DNL PaaS integration - Installer download]**.
1. Välj **[!DNL Generate token]**.
1. Kopiera den genererade åtkomsttoken och lagra den på en säker plats.





