---
title: Bildfältsobjekt i interaktiv kommunikationsredigerare
description: Image Field Object in Interactive Communication Editor in AEM Forms to allows authors to insert images into a communication layout.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Bildfältsobjekt i interaktiv kommunikationsredigerare

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

## &#x200B;1. Inledning

Med bildfältskomponenten i redigeraren för interaktiv kommunikation kan författare infoga bilder i en kommunikationslayout. Det är idealiskt för användning vid till exempel foto-ID, dokumentverifiering eller visuell validering där det är viktigt att visa en bild för slutanvändaren.

Komponenten har stöd för vanliga format som **JPEG** och **PNG** och erbjuder flexibla konfigurationsalternativ för att definiera hur bilden ska visas, lagras och formateras. Författare kan också **tilldela ett namn eller en etikett** till bildfältet, vilket förbättrar tydligheten i och organisationen av layouten.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/imagefield.png)

## &#x200B;2. Egenskaper

Bildfältsobjektet innehåller flera konfigurerbara egenskaper:

2.1. Grundläggande fält

- **Namn:** Definiera en unik identifierare för fältet som används för att referera till datamodeller och regler.

- **Bildtext:** Visa etiketten som visas för användarna i gränssnittet.

- **Välj bild:** Låt författaren överföra en bild med den här egenskapen, som ofta används för logotyper, ID:n eller andra visuella element.

- **Reservbild:** Definiera bildens justering, vänster, höger, upptill eller nedtill eller ange en **anpassad position** med enheter som millimeter (t.ex. 20 mm).

2.2. Position

Styr bildens rumsliga placering i layouten.

- X- och Y-koordinater

- Höjd och bredd (i mm)

2.3. Marginal

Definiera avstånd runt textrutan:

- Överkant (uppåt)

- Nederkant (nedåt)

- Vänster

- Höger

2.4 Utseende

Utseende: Definierar bildfältets visuella stil, väljer förinställningar som kantlinje, platt eller upphöjd och anpassar med fyllningsfärg, linjebredd och hörnformat (rundad eller skarp).

2.5 Närvaro

Bestämmer bildobjektets synlighet vid körning.

- Synlig

- Dold (behåller utrymme)

2.6. Databindning

Länka bildfältet till en datakälla för att hämta och visa dynamiskt bildinnehåll i kommunikationen.

**Databindningstyp:** Definierar hur bildfältet ansluts till den underliggande datastrukturen eller schemat.

**Använd namn:** Binder bildfältet med fältnamnet som anges i datamodellen eller schemat, vilket gör att bilden kan fyllas i dynamiskt vid körning.

**Använd globala data:** Ansluter bildfältet till globala data som delas i hela kommunikationen, vilket ger ett konsekvent visuellt innehåll.

**Ingen databindning:** Behåller fältet frånkopplat från backend-data, idealiskt för fall där en statisk bild visas eller när bilden styrs enbart via gränssnittsinställningar.

## &#x200B;3. Användning

Bildfältet är användbart i sammanhang där visuellt innehåll måste skickas. Exempel på vanliga användningsområden:

- Överför ID-bevis (pass, licens)

- Skicka profil eller personliga foton

- Bifoga stöddokument visuellt

Författare kan placera fältet i delformulär eller layoutbehållare för justering och använda anpassade valideringsregler för att styra godkända filtyper och storlekar.

## &#x200B;4. Bästa praxis

- Använd tydliga etiketter eller instruktioner när du tillfrågas om bildöverföringar.

- Begränsa filstorlek och format genom validering för prestanda.

- Se till att bilderna blir tillgängliga med reserv.

- Bind fältet till en meningsfull schemasökväg om det integreras med backend-objektet

Bildfältsobjektet i den interaktiva kommunikationsredigeraren är en mångsidig komponent som förbättrar formulärinteraktiviteten genom att aktivera visuella innehållsöverföringar. När den har utformats med format, validering och databindning har den stöd för en smidig användarupplevelse och effektiv datainhämtning för bildbaserade överföringar.




