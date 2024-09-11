---
title: Kontrollera DNS-poststatus
description: Lär dig hur du avgör om dina DNS-inställningar kan matchas med Cloud Manager.
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8a10634e413ea5c66845dfffa7396a4554a5b3ca
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---


# Kontrollera DNS-poststatus {#check-dns-record-status}

Lär dig hur du avgör om dina DNS-inställningar kan matchas med Cloud Manager.

## Status för DNS-poster {#status}

Ett anpassat domännamn kan inte hantera livatrafik förrän DNS-matchningen är korrekt. I Cloud Manager kan du avgöra om ditt domännamn matchar din AEM as a Cloud Service webbplats.

## Krav {#requirements}

Uppfyll dessa krav innan du kontrollerar DNS-poststatus med Cloud Manager.

Du måste redan ha konfigurerat DNS-inställningarna för ditt anpassade domännamn enligt beskrivningen i [Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

## Kontrollera DNS-poststatus {#how-to}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Gå till skärmen **Miljö** från sidan **Översikt**.

1. Klicka på **Domäninställningar** i den vänstra navigeringspanelen.

1. Klicka på ikonen **Status** för domännamnet.

Cloud Manager utför en DNS-sökning efter ditt domännamn och visar den [aktuella statusen](#statuses).

Cloud Manager utlöser automatiskt en DNS-sökning när ditt anpassade domännamn först verifieras och distribueras. För efterföljande försök måste du aktivt välja ikonen **Lös igen** bredvid statusen.

## DNS-status i Cloud Manager {#statuses}

En anpassad domän kan ha någon av följande statusar i Cloud Manager.

| Status | Beskrivning |
| --- | --- |
| DNS-status kunde inte identifieras | DNS-status upptäcks inte förrän det anpassade domännamnet har verifierats och distribuerats. Den här statusen observeras även när ditt anpassade domännamn håller på att tas bort. |
| DNS matchas felaktigt | Den här statusen anger att konfigurationen för DNS-posterna inte har lösts eller är felaktig. Mer information finns i [Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).<br>När du är klar måste du markera ikonen **Lös igen** bredvid statusen. |
| DNS-matchning pågår | Upplösningen pågår. Den här statusen visas vanligtvis när du har valt ikonen **Lös igen** bredvid statusen. |
| DNS matchas korrekt | DNS-inställningarna är korrekt konfigurerade. Din webbplats betjänar besökare. |

## Nästa steg {#next-steps}

Du har konfigurerat din anpassade domän för användning med Cloud Manager. Mer information om hur du hanterar anpassade domännamn med Cloud Manager finns i dokumentet [Hantera anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md).
