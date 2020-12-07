---
title: Kontrollerar DNS-poststatus
description: Kontrollerar DNS-poststatus
translation-type: tm+mt
source-git-commit: 1c51560886515e092680c23db3e128758dcd7d99
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Kontrollerar DNS-poststatus {#check-dns-record-status}

Du kan ta reda på om ditt domännamn tolkas som en Cloud Service-webbplats på rätt sätt till AEM genom att klicka på statusikonen för DNS-posten i tabellen på sidan Domäninställningar.

>[!NOTE]
>Cloud Manager utlöser automatiskt en DNS-sökning när ditt anpassade domännamn först verifieras och distribueras. För efterföljande försök måste du aktivt välja ikonen **resolve igen** bredvid statusen.

Cloud Manager utför en DNS-sökning efter ditt domännamn och visar ett av följande statusmeddelanden:

* **DNS-status**
upptäcktes inte DNS-status kommer inte att identifieras förrän det anpassade domännamnet har verifierats och distribuerats. Den här statusen visas även när ditt anpassade domännamn håller på att tas bort.

* **DNS-matchningen**
är felaktig Detta indikerar att konfigurationen av DNS-poster inte har matchats/pekats över än eller är felaktig. En Adobe-representant meddelas automatiskt.

   >[!NOTE]
   >Du måste konfigurera antingen en `CNAME` eller `A-record` genom att följa motsvarande instruktioner. Mer information finns i Konfigurera DNS-inställningar. När du är klar måste du välja ikonen **lös igen** bredvid statusen.

* **DNS-matchning**
pågår. Den här statusen visas vanligtvis när du har valt ikonen&quot;lös igen&quot; bredvid statusen.

* **DNS-matchningen**
är korrektDNS-inställningarna är korrekt konfigurerade. Din webbplats betjänar besökare.
