---
title: 'Konfigurera DNS-inställningar '
description: Konfigurera DNS-inställningar
translation-type: tm+mt
source-git-commit: 1c51560886515e092680c23db3e128758dcd7d99
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---


# Konfigurera DNS-inställningar {#configure-dns}

När det anpassade domännamnet har verifierats och distribuerats kan du uppdatera DNS-posterna för det anpassade domännamnet med din DNS-leverantör. På så sätt kan er webbplats betjäna besökare. Den här aktiviteten utförs därför vanligtvis före GoLive.

>[!NOTE]
>Du eller en lämplig person i organisationen måste kunna logga in eller kontakta din DNS-leverantör (företaget som du köpte domänen från) och göra uppdateringar i dina DNS-inställningar.

För att göra detta måste du avgöra om du måste konfigurera dina DNS-inställningar till en `CNAME`- eller Apex-post som pekar ditt anpassade domännamn mot Cloud Manager-domännamnet. En `CNAME`- eller A-post dirigerar all Internettrafik för domänen till den plats där den pekar när den har etablerats. Om den platsen inte tillhandahålls för att betjäna trafiken uppstår ett driftstopp. Om innehållet inte har testats kan det finnas fel i det. Det är därför det här steget alltid görs när testningen är klar och kunden är redo för Go-live.

## CNAME-post {#cname-record}

Följande avsnitt hjälper dig att avgöra vilken typ av post som passar din DNS-konfiguration.

Ett kanoniskt namn eller en `CNAME`-post är en typ av DNS-post som mappar ett aliasnamn till ett sant eller kanoniskt domännamn. CNAME-poster används vanligtvis för att mappa en underdomän som `www.example.com` till den domän som är värd för underdomänens innehåll.

Logga in på din domänregistrator och skapa en CNAME-post för att peka ditt anpassade domännamn mot målet så som visas nedan:

| CNAME | Anpassad domännamnspunkt till mål |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

## APEX-post {#apex-record}

En domän är en anpassad domän som inte innehåller någon underdomän, till exempel example.com. En apex-domän har konfigurerats med en `A`-, `ALIAS`- eller `ANAME`-post via din DNS-leverantör. Apex-domänerna måste peka på specifika IP-adresser.

Lägg till alla följande A-poster i domänens DNS-inställningar via din domänleverantör:

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
