---
title: Kontrollerar domännamnsstatus
description: Kontrollerar domännamnsstatus
translation-type: tm+mt
source-git-commit: 91b06bcd96fe8a37c3fb20ef90e1684f6d19183f
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# Kontrollerar domännamnsstatus {#check-status}

Du kan ta reda på om ditt domännamn har verifierats genom att klicka på statusikonen för domännamnet i tabellen i Miljöer på sidan Domäninställningar.

>[!NOTE]
>Cloud Manager utlöser automatiskt en TXT-verifiering när du väljer Spara i verifieringssteget i guiden Lägg till anpassad domän. För efterföljande verifieringar måste du aktivt välja ikonen&quot;verifiera igen&quot; bredvid statusen. INFOGA BILD

Cloud Manager verifierar domänägarskap via TXT-värdet och visar ett av följande statusmeddelanden:

* **Domänverifieringen misslyckades** TXT-värdet saknas eller har identifierats med fel. Följ instruktionerna och försök igen. När du är klar måste du markera ikonen&quot;verifiera igen&quot; bredvid statusen.

* **Domänverifiering pågår**. Den här statusen visas vanligtvis när du har valt ikonen&quot;verifiera igen&quot; bredvid statusen.

* **Verifierad, distributionen misslyckades** TXT-verifieringen lyckades. CDN-distributionen misslyckades dock. En Adobe-representant meddelas automatiskt.

* **Domän verifierad och distribuerad** Den här statusen anger att ditt anpassade domännamn är klart att användas. Obs! Nu är ditt anpassade domännamn klart för testning och kan hänvisas till molnhanterarens domännamn. Gå till Konfigurera INSERT LINK för DNS-inställningar om du vill veta hur du gör det.

* **Det går inte att ta bort** det anpassade domännamnet.

* **Borttagningen misslyckades**. Det gick inte att ta bort det anpassade domännamnet. Du måste försöka igen. Gå till Ta bort anpassat domännamn om du vill veta mer om ämnet.


## Konfigurera DNS-inställningar {#configure-dns}

När det anpassade domännamnet har verifierats och distribuerats kan du uppdatera DNS-posterna för det anpassade domännamnet med din DNS-leverantör. På så sätt kan er webbplats betjäna besökare. Den här aktiviteten utförs därför vanligtvis före GoLive.

>[!NOTE]
>Du eller en lämplig person i organisationen måste kunna logga in eller kontakta din DNS-leverantör (företaget som du köpte domänen från) och göra uppdateringar i dina DNS-inställningar.

För att göra detta måste du avgöra om du måste konfigurera DNS-inställningarna till en `CNAME` eller Apex-post som pekar ditt anpassade domännamn mot Cloud Manager-domännamnet. En `CNAME` eller A-post dirigerar all internettrafik för domänen till den plats där den pekar. Om den platsen inte tillhandahålls för att betjäna trafiken uppstår ett driftstopp. Om innehållet inte har testats kan det finnas fel i det. Det är därför det här steget alltid görs när testningen är klar och kunden är redo för Go-live.

### CNAME-post {#cname-record}

Följande avsnitt hjälper dig att avgöra vilken typ av post som passar din DNS-konfiguration.

Ett kanoniskt namn eller en kanoniskt `CNAME` post är en typ av DNS-post som mappar ett aliasnamn till ett sant eller kanoniskt domännamn. CNAME-poster används vanligtvis för att mappa en underdomän, t.ex. `www.example.com` till den domän som är värd för underdomänens innehåll.

Logga in på din domänregistrator och skapa en CNAME-post för att peka ditt anpassade domännamn mot målet så som visas nedan:

| CNAME | Anpassad domännamnspunkt till mål |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |
