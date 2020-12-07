---
title: Kontrollerar domännamnsstatus
description: Kontrollerar domännamnsstatus
translation-type: tm+mt
source-git-commit: 1c51560886515e092680c23db3e128758dcd7d99
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# Kontrollerar domännamnsstatus {#check-status}

Du kan ta reda på om ditt domännamn har verifierats genom att klicka på statusikonen för domännamnet i tabellen i Miljöer på sidan Domäninställningar.

>[!NOTE]
>Cloud Manager utlöser automatiskt en TXT-verifiering när du väljer Spara i verifieringssteget i guiden Lägg till anpassad domän. För efterföljande verifieringar måste du aktivt välja ikonen **verifiera igen** bredvid statusen.

Cloud Manager verifierar domänägarskap via TXT-värdet och visar ett av följande statusmeddelanden:

* **Domänverifieringen**
FailedTXT-värdet saknas eller har identifierats med fel. Följ instruktionerna och försök igen. När du är klar måste du markera ikonen&quot;verifiera igen&quot; bredvid statusen.

* **Domänverifiering**
pågårVerifiering pågår. Den här statusen visas vanligtvis när du har valt ikonen&quot;verifiera igen&quot; bredvid statusen.

* **Verifierad, Distributionen**
FailedTXT-verifieringen lyckades. CDN-distributionen misslyckades dock. En Adobe-representant meddelas automatiskt.

* **Domän verifierad och**
distribueradDen här statusen anger att ditt anpassade domännamn är klart att användas. Obs! Nu är ditt anpassade domännamn klart för testning och kan hänvisas till molnhanterarens domännamn. Gå till Konfigurera DNS-inställningar om du vill veta hur du gör det.

* **Borttagning**
av anpassat domännamn pågår.

* **Borttagningen**
misslyckades. Det gick inte att ta bort det anpassade domännamnet. Du måste försöka igen. Gå till Ta bort anpassat domännamn om du vill veta mer om ämnet.

