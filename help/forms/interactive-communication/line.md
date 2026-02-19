---
title: Line Component in Interactive Communication Editor
description: Med Line Component i Interactive Communication Editor i AEM Forms kan man infoga horisontella eller vertikala linjer i en kommunikationslayout.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 1ff5ac22-d8c8-4109-8334-217dbc239f1f
source-git-commit: cdaceaabb8eeeec931b1897e1161f408606540b9
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# Line Component in Interactive Communication Editor

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

## &#x200B;1. Inledning

Med Line Component i redigeraren Interactive Communication (IC) kan man infoga horisontella eller vertikala linjer i en kommunikationslayout. Dessa linjer hjälper till att segmentera innehåll visuellt, förbättra läsbarheten eller framhäva formulärstrukturen. Med anpassningsbara format som heldragna linjer eller understrykningar och flexibel placering kan Line-komponenten användas för både funktionellt och estetiskt ändamål i formulärdesign.

![Sök efter IC Docu](/help/forms/interactive-communication/assets/line.png)

## &#x200B;2. Egenskaper

Line-komponenten har en rad konfigurerbara egenskaper som definierar dess identitet, utseende, placering och synlighet i dokumentet.

2.1. Grundläggande fält

- **Namn:** En unik identifierare som används internt för att referera till radkomponenten i datamodeller, regler eller skript.

- **Utseendetyp:** Välj hur raden ska visas i formuläret.

   - **Ingen:** Ingen rad visas.

   - **Solid Box:** Återger raden som en fylld ruta, som vanligtvis används som avgränsare.

   - **Understruken:** Ritar en understrykning som vanligtvis används under rubriker eller fält.

2.2. Position

- **Beskrivning:** Definierar den fysiska placeringen av raden i formulärlayouten.

- **Inställningar:**

   - **X- och Y-koordinater:** Anger vågrät och lodrät placering.

   - **Höjd och bredd:** Ange linjens längd och tjocklek (i mm).

2.3. Marginal

- **Beskrivning:** Lägger till utfyllnad eller mellanrum runt linjekomponenten för att styra layoutdensiteten.

- **Alternativ:**

   - Överkant

   - Nederkant

   - Vänster

   - Höger

2.4 Utseende

- **Beskrivning:** Tillåter formatering av raden att matcha dokumentdesignen.

- **Alternativ:**

   - **Linje:** Definierar linjens färg och tjocklek.

   - **Bredd:** Anger hur bred linjen ska vara i hela formuläret.

   - **Stil:** Välj mellan streckade, prickade eller heldragna linjeformat.

2.5 Närvaro

- **Beskrivning:** Styr linjekomponentens synlighet under körning.

- **Alternativ:**

   - **Synlig:** Raden återges i det slutliga resultatet.

   - **Dold:** Raden visas inte, men layoututrymmet bevaras.

## &#x200B;3. Användning

Line-komponenten används ofta för att:

- Dela upp avsnitt visuellt i en lång form

- Understrykningsrubriker eller etiketter för betoning

- Skapa kanter eller rutor runt fältgrupper

- Förbättra den visuella hierarkin i kommunikationslayouten

## &#x200B;4. Bästa praxis

- Använd konsekventa linjeformat i hela formuläret för att få ett professionellt utseende.

- Justera marginalerna för att undvika oskärpa och för att säkerställa justeringen.

- Välj lämpliga linje- och formatinställningar för att matcha varumärket eller dokumentdesignen.

- Dölj onödiga linjer för att undvika störning samtidigt som du behåller mellanrummet i layouten.

Line-komponenten i redigeraren för interaktiv kommunikation är ett enkelt men kraftfullt designelement. När det används strategiskt förbättrar det den visuella strukturen i kommunikationsdokument, vilket hjälper användarna att navigera bättre och säkerställa en renare och mer prydlig layout.
