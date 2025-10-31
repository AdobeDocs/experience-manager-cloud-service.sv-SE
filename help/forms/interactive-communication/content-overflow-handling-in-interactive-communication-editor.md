---
title: Hantering av innehållsspill i interaktiv kommunikationsredigerare
description: Hantering av innehållsspill i Interactive Communication Editor förbättrar textens funktion i layouterna Flödat och Placerad.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 371838c77beafa8c67259a865b25325632bea0b0
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# Hantering av innehållsspill i interaktiv kommunikationsredigerare

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

## Introduktion

Funktionen Innehållsflödeshantering i den interaktiva kommunikationsredigeraren förbättrar hur text fungerar i layouter med flödesformat och positionering. Det ger smidig innehållskontinuitet för flödande layouter och ger visuella aviseringar för positionerade layouter, vilket ger författarna bättre kontroll och flexibilitet när de utformar kommunikation.

## Nyckelfunktioner

### Flödande layout

- **Nytt alternativ:**
Lägger till en egenskap, **Tillåt sidbrytningar** i innehållet, för att styra flödeslänkens beteende. Det här alternativet är bara synligt när det överordnade delformuläret är inställt på Flödat och egenskapen **Tillåt sidbrytningar** är aktiverad.

- **Automatisk sidfortsättning:**
När innehållet överskrider det tillgängliga utrymmet skapas en ny sida automatiskt och redigeringen fortsätter utan problem.

- **Stöd för kopiera och klistra in:**
Stor text som klistras in i redigeraren flödar automatiskt över sidorna, vilket ger en konsekvent layout.

### Placerad layout

- **Flödesindikator:**
När innehållet överskrider behållaren (delformulär eller sida) utökas textredigeraren för redigering, men elementets höjd förblir fast.

- **Visuell varning:**
En röd ram visas längst ned i behållaren för att ange spill.

- **Manuell justering:**
Författare ändrar manuellt storlek på behållaren så att den passar ytterligare innehåll.

>[!NOTE]
>
> Den här funktionen kräver att hela den överordnade hierarkin (till exempel delformulär) är inställd på Flödat. Om något överordnat delformulär i hierarkin är Placerat kommer alternativet **Tillåt sidbrytningar** i innehållet inte att fungera som förväntat.

## Fördelar

- Förbättrar effektiviteten och kontrollen vid redigering av innehåll.

- Bibehåller en konsekvent layout och läsbarhet på alla sidor.

- Identifierar spill snabbt med visuella indikatorer.

- Förbättrar flexibiliteten i kommunikationsdesignen för båda layouttyperna.
