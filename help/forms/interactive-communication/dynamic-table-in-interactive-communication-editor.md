---
title: Skapa dynamisk tabell i interaktiv kommunikationsredigerare
description: Skapa en dynamisk tabellfunktion som gör att författare kan skapa datadrivna tabeller.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="Gäller AEM Forms)."
source-git-commit: 322183c28719db5b8657d9532ef234e1d18821cd
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---


# Skapa dynamisk tabell i interaktiv kommunikationsredigerare

## Översikt

Interactive Communication Editor innehåller en dynamisk tabell
som gör det möjligt att skapa datadrivna tabeller vars innehåll fylls i automatiskt vid körning från strukturerade datakällor.

Till skillnad från statiska tabeller där rader måste skapas manuellt, utökas eller dras dynamiska tabeller automatiskt samman baserat på de poster som returneras från en bunden datakälla. Detta gör dem användbara för scenarier som faktureringssatser, transaktionshistorik, produktlistor eller policyscheman.

I den här artikeln beskrivs hur du infogar och konfigurerar en dynamisk tabell med databindning, hanterar flersidigt tabellflöde och validerar radantal.

## Infoga en dynamisk tabell

1. Öppna **Interaktiv kommunikationsredigerare**.
1. Dra **tabellkomponenten** från **komponentpanelen** till
arbetsyta.
1. Ange **antalet kolumner** och **inledande rader** i dialogrutan, kontrollera att **rubrikraden** tas med och klicka sedan på OK för att skapa tabellen.

### Binda data till den dynamiska tabellen

Dynamiska tabeller fyller i rader automatiskt genom att binda till en repeterbar datakälla.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/databinding-in-table.png)

Så här binder du data till tabellen:

1. Markera **tabellraden** på hierarkipanelen.

1. Öppna **databindningen** från sidopanelen.

1. Kontrollera att det markerade dataschemat är av matristyp.

1. Dra och släpp arraydatamodellen på den markerade tabellraden för att binda data.

### Aktivera sidflöde

Dynamiska tabeller kan sträcka sig längre än en sida. Om du vill tillåta att tabellen växer och fortsätter över sidor placerar du den inuti en **flödesinnehåll** -behållare.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/table-data-binding.png)

Så här aktiverar du sidflöde:

1. Markera tabellens **överordnade layoutbehållare**.

1. Öppna panelen Egenskaper och ange innehållstypen till **Flödat**.

1. Markera tabellen och kontrollera att den även är konfigurerad för att stödja flödesinnehåll.

1. Förhandsgranska kommunikationen för att kontrollera att tabellen fortsätter på nästa sida när ytterligare rader återges.

### Tillåt sidbrytning i tabell

![Sök efter IC Docu](/help/forms/interactive-communication/assets/table-data-binding.png)

Så här ser du till att tabellen delas upp korrekt på flera sidor:

1. Markera **tabellen** på arbetsytan.
1. Öppna panelen **Egenskaper**.
1. Aktivera **Tillåt sidbrytning i innehållet**.

När det här alternativet är aktiverat bryts tabellen automatiskt i slutet av en sida och fortsätter på nästa sida, där rubrikraden upprepas.

### Konfigurera radvalidering

Du kan styra hur många rader den dynamiska tabellen kan återge.

* **Minimirader:** Ser till att tabellen återger minst det angivna antalet rader.
* **Maximalt antal rader:** Begränsar det totala antalet rader som återges från datakällan.
* **Inledande rader:** Definierar hur många rader som ska visas i redigeraren vid förhandsgranskning i designläge.

>[!NOTE]
>
> Om du ställer in **Inledande rader** på omkring **3-5** får du en mer realistisk förhandsvisning av layouten innan körningsdata används.

## Nyckelfunktioner

* Kolumndatabindning: Bind varje kolumn till ett fält i datamodellen.

* Flödat innehåll: Tabellen kan expanderas och fortsätta över sidor.

* Stöd för sidbrytning: Aktiverar sidbrytningar på radnivå i tabellen.

* Minsta antal rader: Ser till att ett minsta antal rader återges.

* Maximalt antal rader: Begränsar det totala antalet rader som renderas från datakällan.

* Inledande rader: Definierar de standardrader som visas vid förhandsvisning i designläge.

Funktionen Dynamisk tabell i Interactive Communication Editor gör att man kan skapa flexibla, datadrivna tabeller utan att behöva skriva egen kod. Genom att binda tabellen till en datamatris, aktivera flödesinnehåll, tillåta sidbrytningar och konfigurera radvalidering, kan författare skapa strukturerad kommunikation som smidigt anpassas till varierande datavolymer samtidigt som en konsekvent layout upprätthålls.
