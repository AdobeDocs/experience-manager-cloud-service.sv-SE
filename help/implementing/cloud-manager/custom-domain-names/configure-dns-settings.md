---
title: 'Konfigurera DNS-inställningar '
description: Konfigurera DNS-inställningar
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: 0b24f8c8b88f476a0d1073e873e46441b1b8b821
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# Konfigurera DNS-inställningar {#configure-dns}

När det anpassade domännamnet har verifierats och distribuerats kan du uppdatera DNS-posterna för det anpassade domännamnet med din DNS-leverantör. På så sätt kan er webbplats betjäna besökare. Den här aktiviteten utförs därför vanligtvis före GoLive.

>[!NOTE]
>Du eller en lämplig person i organisationen måste kunna logga in eller kontakta din DNS-leverantör (företaget som du köpte domänen från) och göra uppdateringar i dina DNS-inställningar.

För att göra detta måste du avgöra om du måste konfigurera dina DNS-inställningar till `CNAME` eller en Apex-post som pekar ditt anpassade domännamn mot domännamnet för Cloud Manager. A `CNAME` eller En post dirigerar all Internettrafik för domänen till den plats där den pekar när den har etablerats. Om den platsen inte tillhandahålls för att betjäna trafiken uppstår ett driftstopp. Om innehållet inte har testats kan det finnas fel i det. Det är därför det här steget alltid görs när testningen är klar och kunden är redo för Go-live.

Följande steg skall utföras enligt tabellen nedan:

| Steg |  | Ansvarsområde | Läs mer |
|--- |--- |--- |---|
| Lägg till SLL-certifikat | Lägg till SLL-certifikat | Kund | [Lägga till ett SSL-certifikat](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) |
| Domänverifiering | Lägg till TXT-post | Kund | [Lägga till en TXT-post](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-text-record.html?lang=en) |
| Verifieringsstatus för domän |  | Kund |  |
|  | Status: Domänverifieringsfel | Kund | [Kontrollerar domännamnsstatus](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
|  | Status: Verifierad, distributionen misslyckades | Kontakta Adobe | [Kontrollerar domännamnsstatus](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
| Lägg till DNS-poster som pekar på AEM as a Cloud Service genom att lägga till CNAME- eller APEX-poster | Konfigurera DNS-inställningar | Kund | [Konfigurera DNS-inställningar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/configure-dns-settings.html?lang=en) |
| Kontrollera DNS-poststatus |  | Kund | [Kontrollerar DNS-poststatus](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | Status: DNS-status kunde inte hittas | Kund | [Kontrollerar DNS-poststatus](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | Status: DNS matchas felaktigt | Kund |  |


## CNAME-post {#cname-record}

Följande avsnitt hjälper dig att avgöra vilken typ av post som passar din DNS-konfiguration.

Ett kanoniskt namn eller `CNAME` post är en typ av DNS-post som mappar ett aliasnamn till ett sant eller kanoniskt domännamn. CNAME-poster används vanligtvis för att mappa en underdomän som `www.example.com`  till den domän som är värd för underdomänens innehåll.

Logga in på din domänregistrator och skapa en CNAME-post för att peka ditt anpassade domännamn mot målet så som visas nedan:

| CNAME | Anpassad domännamnspunkt till mål |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

## APEX-post {#apex-record}

En domän är en anpassad domän som inte innehåller någon underdomän, till exempel example.com. En apex-domän har konfigurerats med en `A` , `ALIAS` , eller `ANAME` spela in via din DNS-leverantör. Apex-domänerna måste peka på specifika IP-adresser.

Lägg till alla följande A-poster i domänens DNS-inställningar via din domänleverantör:

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
