---
title: Kontrollerar DNS-poststatus
description: Lär dig hur du avgör om dina DNS-inställningar kan matchas korrekt med hjälp av Cloud Manager.
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
source-git-commit: 2278abcf0c34fd34a7730242ee27814d37b7d4d0
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Kontrollerar DNS-poststatus {#check-dns-record-status}

I Cloud Manager kan du avgöra om ditt domännamn matchar din AEM as a Cloud Service webbplats.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Miljö** från **Översikt** sida.

1. Klicka på **Domäninställningar** i den vänstra navigeringspanelen.

1. Klicka på **Status** -ikon för domännamnet.

Cloud Manager utför en DNS-sökning efter ditt domännamn och visar ett av följande statusmeddelanden.

* **DNS-status kunde inte hittas** - DNS-status kan inte identifieras förrän ditt anpassade domännamn har verifierats och distribuerats.

   * Den här statusen visas även när ditt anpassade domännamn håller på att tas bort.

* **DNS-matchningen är felaktig** - Detta anger att konfigurationen för DNS-posterna inte har matchats eller är felaktig.

   * Se dokumentet [Konfigurera DNS-inställningar](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) om du vill veta mer.
   * När du är klar måste du välja **Lös igen** -ikonen bredvid statusen.

* **DNS-matchning pågår** - Upplösningen pågår.

   * Den här statusen visas vanligtvis när du har valt **Lös igen** -ikonen bredvid statusen.

* **DNS-matchningar korrekt** - DNS-inställningarna är korrekt konfigurerade.

   * Din webbplats betjänar besökare.

Cloud Manager utlöser automatiskt en DNS-sökning när ditt anpassade domännamn först verifieras och distribueras. För efterföljande försök måste du aktivt välja **Lös igen** -ikonen bredvid statusen.
