---
title: Textrutekomponent i interaktiv kommunikationsredigerare
description: Med Text Box Component i Interactive Communication Editor i AEM Forms kan man skriva in och visa text i en kommunikation.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: bd8992792afddb2243736578acd24bc47efad842
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---


# Textrutekomponent i interaktiv kommunikationsredigerare

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

## &#x200B;1. Inledning

Komponenten **Textruta** i den interaktiva kommunikationsredigeraren gör att författare kan ange och visa textinnehåll i en kommunikation. Det är en av de mest grundläggande och allmänt använda komponenterna, som ofta används för att samla in namn, kommentarer, feedback eller anpassade data när man utformar interaktiva kommunikations- eller kommunikationsfragment.

Textrutan stöder **databindning**, vilket gör att författare kan kombinera statiskt och dynamiskt innehåll sömlöst, till exempel: ***&quot;Användarens namn: @name&quot;***, där @name är ett bundet datafält som fylls i dynamiskt när dokumentet sparas som en PDF. Dessutom har det stöd för formaterad text och flexibel positionering för exakt layoutkontroll.

![Sök efter IC-dokument](/help/forms/interactive-communication/assets/textbox.png)

## &#x200B;2. Egenskaper

Textrutekomponenten innehåller en mängd egenskaper som hjälper dig att konfigurera dess utseende, känsla och beteende.

2.1 Typografi

**Teckensnittsfamilj:** Tillåter urval av teckensnittsformat som Arial, Helvetica, Times New Roman osv.

**Teckensnittsvalidering:** Ytterligare indatabegränsningar kan användas för att säkerställa att endast text, numeriska format och specialformat accepteras.

**Textjustering:** Det finns alternativ för vänsterjustering, högerjustering, centrering och marginaljustering.

**Textformat:** Aktivera textformatering med fet, kursiv, genomstrykning och understrykning.

**Listor:** Stöder infogning av ordnade (numrerade) och osorterade (punktlistor) listor.

2.2 Position

**Bredd och höjd:** Ange textrutans mått i pixlar eller procent i förhållande till behållaren.

2,3 marginal

Definiera avstånd runt textrutan:

- Överkant (uppåt)

- Nederkant (nedåt)

- Vänster

- Höger

2.4 Utseende

- **Textfyllning:** Anpassa färg och genomskinlighet för text.

- **Fyllning:** Ange bakgrundsfärg för textrutan.

- **Linje:** Lägg till kanter med anpassningsbara:

   - Bredd (tjocklek)

   - Stil (heldragen, streckad, prickad)

   - Edge (rundade eller skarpa hörn)

2.5 Närvaro

**Synlig:** Standardinställning; textrutan visas för användaren.

**Dold:** Textrutan ingår i formuläret men visas inte.



## &#x200B;3. Användning

Textrutan används för:

- Samla in kundinformation som namn, kommentarer eller feedback.

- Ange alfanumeriska värden.

- Integrera personaliserade meddelanden med bundna datamodeller.

- Bädda in i fragment för upprepad användning i flera dokument.

Författare kan dra textrutan från komponentbiblioteket till designvyn eller mallvyn och konfigurera dess beteende med egenskapspanelen.

## &#x200B;4. Bästa praxis

- Associera alltid textrutor med meningsfulla fältetiketter för att förbättra tillgängligheten.

- Använd lämpliga indatavalideringar för att förhindra inmatningsfel.

- Se till att layouten är responsiv genom att ange marginaler och bredder i förhållande till överordnade behållare.

- Undvik överdrivet många teckensnittsformat som kan göra läsbarheten svårare.

Genom att konfigurera textruteegenskaperna noggrant kan man skapa interaktiva, responsiva och användarvänliga kommunikationsfunktioner i AEM Interactive Communication Editor.
