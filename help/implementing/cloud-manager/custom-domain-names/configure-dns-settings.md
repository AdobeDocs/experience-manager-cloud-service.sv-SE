---
title: Konfigurera DNS-inställningar
description: Lär dig hur du konfigurerar DNS-inställningar för dina anpassade domännamn så att din webbplats kan betjäna besökare.
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 06e961febd7cb2ea1d8fca00cb3dee7f7ca893c9
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---


# Konfigurera DNS-inställningar {#configure-dns}

När ditt anpassade domännamn har [verifierats och distribuerats ](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) kan du uppdatera DNS-posterna för ditt anpassade domännamn med din DNS-leverantör. På så sätt kan er webbplats betjäna besökare. Denna aktivitet utförs därför vanligtvis innan den publiceras.

## Vad är DNS-inställningar? {#dns-settings}

En `CNAME`- eller A-post dirigerar all Internettrafik för domänen till var den än pekar när den har etablerats. Om den platsen inte har etablerats för att betjäna trafiken uppstår ett driftstopp. Om innehållet inte har testats kan det finnas fel i det. Det är därför det här steget alltid utförs när testningen är klar och du är redo att publicera.

Om du vill konfigurera de här inställningarna måste du avgöra om en `CNAME`- eller en apex-post måste konfigureras för att peka ditt anpassade domännamn mot Cloud Manager domännamn. Följande avsnitt i det här dokumentet hjälper dig att avgöra vilken typ av post som passar din DNS-konfiguration.

## Krav {#requirements}

Du måste uppfylla dessa krav innan du konfigurerar dina DNS-poster.

* Du måste identifiera din domänvärd eller registrator om du inte redan känner till den.
* Du måste kunna redigera DNS-posterna för din organisations domän eller kontakta rätt person som kan göra det.
* Du måste redan ha verifierat ditt konfigurerade anpassade domännamn enligt beskrivningen i dokumentet [Kontrollerar domännamnsstatus.](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)

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

## Nästa steg {#next-steps}

När du har konfigurerat dina DNS-poster för ditt anpassade domännamn måste du verifiera de inställningarna i Cloud Manager. Fortsätt till dokumentet [Kontrollerar DNS-poststatus](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) för att slutföra ditt anpassade domännamn.
