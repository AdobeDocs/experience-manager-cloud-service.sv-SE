---
title: Stöd för XDP-redigering i Interactive Communication Editor
description: Stöd för XDP-redigering i Interactive Communication Editor gör att befintliga xdps kan redigeras i Interactive Communication Editor.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 957944da363b506c34c2630aeedbe984442f34b8
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# Stöd för XDP-redigering i Interactive Communication Editor

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

## Introduktion

Redigeraren för interaktiv kommunikation (IC) har nu **sömlöst stöd för redigering av XDP-filer (XML-datapaket)** i redigeringsmiljön. Förbättringen gör det möjligt för skribenter att hantera, ändra och underhålla XDP-mallar utan problem, utan att behöva använda externa verktyg. Med den här funktionen kan användare överföra, visa och redigera XDP-filer direkt i IC Editor, vilket ger ett enhetligt och effektivt arbetsflöde från design till leverans.

## Använda stöd för XDP-redigering i interaktiv kommunikationsredigerare

![Sök efter IC-dokument](/help/forms/interactive-communication/assets/support-xdp.png)

1. Navigera till **Forms > Forms &amp; Documents**.

1. Överför din .xdp-fil med alternativet **Skapa > Filöverföring** .

1. Öppna XDP i **Interaktiv kommunikationsredigerare**.

1. Gör nödvändiga ändringar i **design eller databindning**.

1. Om du sparar ändringarna återspeglas uppdateringarna automatiskt i XDP-källfilen.

## Nyckelfunktioner

- **Överför och hantera XDP-filer:**
Överför XDP-mallar via **Forms Manager**. När de har överförts blir de tillgängliga för direktredigering i den interaktiva kommunikationsredigeraren.

- **Redigera med IC Editor:**
Öppna och redigera XDP:er med IC Editor med fullständig tillgång till befintliga redigeringsfunktioner, inklusive layoutjusteringar, databindning, formatering och komponentkonfiguration.

- **Spara tillbaka till Source:**
Alla ändringar som görs i IC Editor sparas direkt i den ursprungliga XDP-filen, vilket bevarar versionens integritet och förenklar designarbetsflödet.

## Fragmentstöd

- **Fragmentreferenser:**
Om en XDP refererar till ett fragment måste det fragmentet finnas i **AEM med samma relativa sökväg** som definieras i XDP-filen.
Om ett fragment saknas visas ett **varningsmeddelande** som anger att det nödvändiga fragmentet inte finns.

- **Återanvändning av fragment i redigeraren:**
Alla befintliga XDP-fragment visas på **fragmentpanelen** i IC Editor.
Författare kan **dra och släppa** dessa fragment direkt på arbetsytan. Referenserna bevaras så att fragmentuppdateringarna sprids över alla XDP-filer som använder dem.

## Fördelar

- Eliminerar beroendet av externa verktyg för XDP-ändringar.

- Bevarar befintliga databindningar och fragmentrelationer.

- Ger enhetlig design och snabbare itereringscykler.

## Bästa praxis

- Kontrollera att alla refererade fragment finns i rätt relativ sökväg innan du redigerar.

- Använd versionskontroll för att hantera uppdateringar över XDP- och fragmentberoenden.

- Validera databindningar efter redigering för att bekräfta korrekt återgivning.

