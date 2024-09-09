---
title: Kontrollerar DNS-poststatus
description: Lär dig hur du avgör om dina DNS-inställningar kan matchas med Cloud Manager.
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---


# Kontrollerar DNS-poststatus {#check-dns-record-status}

Lär dig hur du avgör om dina DNS-inställningar kan matchas med Cloud Manager.

## Status för DNS-poster {#status}

Ett anpassat domännamn kan inte hantera livatrafik förrän DNS-matchningen är korrekt. I Cloud Manager kan du avgöra om ditt domännamn matchar din AEM as a Cloud Service webbplats.

## Krav {#requirements}

Du måste uppfylla dessa krav innan du kontrollerar DNS-poststatus med Cloud Manager.

* Du måste redan ha konfigurerat DNS-inställningarna för ditt anpassade domännamn enligt beskrivningen i dokumentet [Konfigurera DNS-inställningar](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md).

## Kontrollera DNS-poststatus {#how-to}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Gå till skärmen **Miljö** från sidan **Översikt**.

1. Klicka på **Domäninställningar** i den vänstra navigeringspanelen.

1. Klicka på ikonen **Status** för domännamnet.

Cloud Manager utför en DNS-sökning efter ditt domännamn och visar den [aktuella statusen](#statuses).

Cloud Manager utlöser automatiskt en DNS-sökning när ditt anpassade domännamn verifieras och distribueras. För efterföljande försök måste du aktivt välja ikonen **Lös igen** bredvid statusen.

## DNS-status i Cloud Manager {#statuses}

En anpassad domän kan ha någon av följande statusar i Cloud Manager.

* **DNS-status hittades inte** - DNS-status kommer inte att identifieras förrän det anpassade domännamnet har verifierats och distribuerats.

   * Den här statusen observeras även när ditt anpassade domännamn håller på att tas bort.

* **DNS-matchningen är felaktig** - Detta indikerar att DNS-postkonfigurationen inte har matchats eller är felaktig.

   * Mer information finns i [Konfigurera DNS-inställningar](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md).
   * När du är klar måste du markera ikonen **Lös igen** bredvid statusen.

* **DNS-matchning pågår** - Upplösningen pågår.

   * Den här statusen visas vanligtvis när du har valt ikonen **Lös igen** bredvid statusen.

* **DNS-matchningen är korrekt** - DNS-inställningarna är korrekt konfigurerade.

   * Din webbplats betjänar besökare.

## Nästa steg {#next-steps}

Grattis! Du har konfigurerat din anpassade domän för användning med Cloud Manager. Mer information om hur du hanterar anpassade domännamn med Cloud Manager finns i dokumentet [Hantera anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md).
