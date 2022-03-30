---
title: Kontrollerar domännamnsstatus
description: Lär dig hur du avgör om ditt anpassade domännamn har verifierats av Cloud Manager.
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: cc1b0d653706150c616ceafd002dc7594b6c7072
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---


# Kontrollerar domännamnsstatus {#check-status}

Du kan fastställa statusen för ditt anpassade domännamn i Cloud Manager.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Miljö** från **Översikt** sida.

1. Klicka på **Domäninställningar** i den vänstra navigeringspanelen.

1. Klicka på **Status** -ikon för domännamnet.

Cloud Manager verifierar domänägarskap via TXT-värdet och visar ett av följande statusmeddelanden.

* **Domänverifieringen misslyckades** - TXT-värdet saknas eller har identifierats med fel.

   * Följ instruktionerna för att lösa problemet.
   * När du är klar måste du välja **Verifiera igen** -ikonen bredvid statusen.

* **Domänverifiering pågår** - Verifiering pågår.

   * Den här statusen visas vanligtvis när du har valt **Verifiera igen** -ikonen bredvid statusen.

* **Verifierad, distributionen misslyckades** - TXT-verifieringen lyckades, men CDN-distributionen misslyckades.

   * Kontakta i så fall din Adobe-representant.

* **Domänen har verifierats och distribuerats** - Den här statusen anger att ditt anpassade domännamn är klart att användas.

   * Nu är ditt anpassade domännamn klart för testning och kan hänvisas till molnhanterarens domännamn.
   * Se dokumentet [Konfigurera DNS-inställningar](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) om du vill veta mer.

* **Tar bort** - Borttagningen av ett anpassat domännamn pågår.

* **Borttagningen misslyckades** - Det gick inte att ta bort det anpassade domännamnet. Du måste försöka igen.

   * Se dokumentet [Hantera anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) om du vill veta mer.

Cloud Manager utlöser automatiskt en TXT-verifiering när du väljer **Spara** om kontrollsteg för **Lägg till anpassad domän** guide. För efterföljande verifieringar måste du aktivt markera ikonen för att verifiera igen bredvid statusen.

## Tidigare CDN-konfigurationer för anpassade domännamn {#pre-existing-cdn}

Om du har en befintlig CDN-konfiguration för dina anpassade domännamn visas ett informativt meddelande på **IP Tillåtelselista** och **Miljö** -sidor, som uppmanar dig att lägga till dessa konfigurationer via användargränssnittet så att de visas och kan konfigureras i Cloud Manager.

Meddelandet försvinner när alla befintliga miljökonfigurationer migreras med användargränssnittet. Det kan ta 1-2 arbetsdagar innan meddelandet försvinner.

Se dokumentet [Lägga till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) för mer information.

![Redan befintligt CDN-konfigurationsmeddelande](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)
