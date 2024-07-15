---
title: Konfigurera DNS-inställningar
description: Lär dig hur du konfigurerar DNS-inställningar för dina anpassade domännamn.
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# Konfigurera DNS-inställningar {#configure-dns}

När det anpassade domännamnet har verifierats och distribuerats kan du uppdatera DNS-posterna för det anpassade domännamnet med din DNS-leverantör. På så sätt kan er webbplats betjäna besökare. Denna aktivitet utförs därför vanligtvis innan den publiceras.

## Vad är DNS-inställningar? {#dns-settings}

En `CNAME`- eller A-post dirigerar all Internettrafik för domänen till den plats där den pekar när den har etablerats. Om den platsen inte har etablerats för att betjäna trafiken uppstår ett driftstopp. Om innehållet inte har testats kan det finnas fel i det. Det är därför det här steget alltid utförs när testningen är klar och du är redo att publicera.

Om du vill konfigurera de här inställningarna måste du avgöra om en `CNAME`- eller Apex-post måste konfigureras så att den pekar ditt anpassade domännamn mot Cloud Manager domännamn. Följande avsnitt hjälper dig att avgöra vilken typ av post som passar din DNS-konfiguration.

>[!NOTE]
>
>Du eller en lämplig person i organisationen måste kunna logga in eller kontakta din DNS-leverantör (företaget som du köpte domänen från) och göra uppdateringar i dina DNS-inställningar.

## CNAME-post {#cname-record}

Ett kanoniskt namn eller en CNAME-post är en typ av DNS-post som mappar ett aliasnamn till ett sant eller kanoniskt domännamn. CNAME-poster används vanligtvis för att mappa en underdomän som `www.example.com` till den domän som är värd för den underdomänens innehåll.

Logga in på din domänregistrator och skapa en `CNAME`-post för att peka ditt anpassade domännamn mot målet, som i följande tabell.

| CNAME | Anpassad domännamnspunkt till mål |
|--- |--- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

## APEX-post {#apex-record}

En domän är en anpassad domän som inte innehåller någon underdomän, till exempel `example.com`. En huvuddomän har konfigurerats med en `A`-, `ALIAS`- eller `ANAME`-post via din DNS-leverantör. Apex-domäner måste peka på specifika IP-adresser.

Lägg till följande `A`-poster i domänens DNS-inställningar via din domänleverantör.

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
