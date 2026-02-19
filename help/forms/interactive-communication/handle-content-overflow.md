---
title: Hantering av innehållsspill i interaktiv kommunikationsredigerare
description: Hantering av innehållsspill i Interactive Communication Editor förbättrar textens funktion i layouterna Flödat och Placerad.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: f19abed5-34a1-4c26-9e92-e219da798dab
source-git-commit: cdaceaabb8eeeec931b1897e1161f408606540b9
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# Hantering av innehållsspill i interaktiv kommunikationsredigerare

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

## Introduktion

Funktionen Innehållsflödeshantering i den interaktiva kommunikationsredigeraren förbättrar hur text fungerar i layouter med flödesformat och positionering. Det ger smidig innehållskontinuitet för flödande layouter och ger visuella aviseringar för positionerade layouter, vilket ger författarna bättre kontroll och flexibilitet när de utformar kommunikation.

![Sök efter IC-dokument](/help/forms/interactive-communication/assets/content-overflow.png)

## Använda hantering av innehållsspill i den interaktiva kommunikationsredigeraren

1. Öppna Interactive Communication Editor
Öppna kommunikationen i IC Editor för att börja redigera layouten och innehållet.

1. Välj layouttyp
Välj önskad layout för delformuläret, Flödat eller Placerat baserat på hur du vill att innehållet ska fungera.

1. För flödeslayouter

   1. Kontrollera att hierarkin för det överordnade delformuläret är inställd på Flödat.

   1. Aktivera alternativet Tillåt sidbrytningar i innehållet (visas bara om det överordnade delformulärets Tillåt sidbrytningar är aktiverat) på panelen Egenskaper.

   1. När innehållet överskrider en sida fortsätter det automatiskt på nästa sida när du lägger till eller klistrar in text.

1. För placerade layouter

   1. Lägg till eller redigera text i en fast behållare.

   1. Om innehållet överskrider behållarhöjden visas en röd ram längst ned för att ange spill.

   1. Ändra behållarens storlek manuellt så att det passar det extra innehållet.

1. Förhandsgranska kommunikationen
Använd alternativet PDF Preview för att kontrollera hur innehållet flödar över sidor för båda layouttyperna.

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
