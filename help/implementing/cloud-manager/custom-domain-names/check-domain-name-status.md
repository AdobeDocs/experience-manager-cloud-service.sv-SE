---
title: Kontrollerar domännamnsstatus
description: Kontrollerar domännamnsstatus
translation-type: tm+mt
source-git-commit: 5cd22d8af20bb947e4cdab448cf8f20c6596bb2e
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 0%

---


# Kontrollerar domännamnsstatus {#check-status}

Du kan ta reda på om ditt domännamn har verifierats genom att klicka på statusikonen för domännamnet i tabellen i Miljöer på sidan Domäninställningar.

>[!NOTE]
>Cloud Manager utlöser automatiskt en TXT-verifiering när du väljer Spara i verifieringssteget i guiden Lägg till anpassad domän. För efterföljande verifieringar måste du aktivt välja ikonen&quot;verifiera igen&quot; bredvid statusen. INFOGA BILD

Cloud Manager verifierar domänägarskap via TXT-värdet och visar ett av följande statusmeddelanden:

* **Domänverifieringen**
FailedTXT-värdet saknas eller har identifierats med fel. Följ instruktionerna och försök igen. När du är klar måste du markera ikonen&quot;verifiera igen&quot; bredvid statusen.

* **Domänverifiering**
pågårVerifiering pågår. Den här statusen visas vanligtvis när du har valt ikonen&quot;verifiera igen&quot; bredvid statusen.

* **Verifierad, Distributionen**
FailedTXT-verifieringen lyckades. CDN-distributionen misslyckades dock. En Adobe-representant meddelas automatiskt.

* **Domän verifierad och**
distribueradDen här statusen anger att ditt anpassade domännamn är klart att användas. Obs! Nu är ditt anpassade domännamn klart för testning och kan hänvisas till molnhanterarens domännamn. Gå till Konfigurera INSERT LINK för DNS-inställningar om du vill veta hur du gör det.

* **Borttagning**
av anpassat domännamn pågår.

* **Borttagningen**
misslyckades. Det gick inte att ta bort det anpassade domännamnet. Du måste försöka igen. Gå till Ta bort anpassat domännamn om du vill veta mer om ämnet.


## Konfigurera DNS-inställningar {#configure-dns}

När det anpassade domännamnet har verifierats och distribuerats kan du uppdatera DNS-posterna för det anpassade domännamnet med din DNS-leverantör. På så sätt kan er webbplats betjäna besökare. Den här aktiviteten utförs därför vanligtvis före GoLive.

>[!NOTE]
>Du eller en lämplig person i organisationen måste kunna logga in eller kontakta din DNS-leverantör (företaget som du köpte domänen från) och göra uppdateringar i dina DNS-inställningar.

För att göra detta måste du avgöra om du måste konfigurera dina DNS-inställningar till en `CNAME`- eller Apex-post som pekar ditt anpassade domännamn mot Cloud Manager-domännamnet. En `CNAME`- eller A-post dirigerar all Internettrafik för domänen till den plats där den pekar när den har etablerats. Om den platsen inte tillhandahålls för att betjäna trafiken uppstår ett driftstopp. Om innehållet inte har testats kan det finnas fel i det. Det är därför det här steget alltid görs när testningen är klar och kunden är redo för Go-live.

### CNAME-post {#cname-record}

Följande avsnitt hjälper dig att avgöra vilken typ av post som passar din DNS-konfiguration.

Ett kanoniskt namn eller en `CNAME`-post är en typ av DNS-post som mappar ett aliasnamn till ett sant eller kanoniskt domännamn. CNAME-poster används vanligtvis för att mappa en underdomän som `www.example.com` till den domän som är värd för underdomänens innehåll.

Logga in på din domänregistrator och skapa en CNAME-post för att peka ditt anpassade domännamn mot målet så som visas nedan:

| CNAME | Anpassad domännamnspunkt till mål |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

### APEX-post {#apex-record}

En domän är en anpassad domän som inte innehåller någon underdomän, till exempel example.com. En apex-domän har konfigurerats med en `A`-, `ALIAS`- eller `ANAME`-post via din DNS-leverantör. Apex-domänerna måste peka på specifika IP-adresser.

Lägg till alla följande A-poster i domänens DNS-inställningar via din domänleverantör:

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`

## Kontrollerar DNS-poststatus {#check-status-dns-record}

Du kan ta reda på om ditt domännamn tolkas som en Cloud Service-webbplats på rätt sätt till AEM genom att klicka på statusikonen för DNS-posten i tabellen på sidan Domäninställningar. Cloud Manager utför en DNS-sökning efter ditt domännamn och visar ett av följande statusmeddelanden:

>[!NOTE]
>Cloud Manager utlöser automatiskt en DNS-sökning när ditt anpassade domännamn verifieras och distribueras. För efterföljande försök måste du aktivt välja ikonen **resolve igen** bredvid statusen. INFOGA BILD

* **DNS-status**
upptäcktes inte DNS-status kommer inte att identifieras förrän det anpassade domännamnet har verifierats och distribuerats. Den här statusen visas även när ditt anpassade domännamn håller på att tas bort.

* **DNS-matchningen**
är felaktig Detta indikerar att konfigurationen av DNS-poster inte har matchats/pekats över än eller är felaktig. En Adobe-representant meddelas automatiskt.

   >[!NOTE]
   >Du måste konfigurera antingen en `CNAME` eller `A-record` genom att följa motsvarande instruktioner. Gå till Konfigurera INSERT LINK för DNS-inställningar om du vill veta mer om ämnet. När du är klar måste du välja ikonen för att lösa igen bredvid statusen.

* **DNS-matchning**
pågår. Den här statusen visas vanligtvis när du har valt ikonen&quot;lös igen&quot; bredvid statusen.

* **DNS-matchningen**
är korrektDNS-inställningarna är korrekt konfigurerade. Din webbplats betjänar besökare.
