---
title: Kopiera och klistra in i Interactive Communication Editor
description: Med Kopiera och Klistra in i Interactive Communication Editor i AEM Forms kan författare duplicera en befintlig Interactive Communication och återanvända den i en annan mapp eller på en annan plats.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: fe99fc4ddc1e2b3bdd1b2a5b583f2b4cb681dee9
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# Kopiera och klistra in i Interactive Communication Editor

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

Med funktionen Kopiera och klistra in i redigeraren för interaktiv kommunikation kan författare duplicera en befintlig interaktiv kommunikation och återanvända den i en annan mapp eller på en annan plats. Detta gör att teamen kan arbeta effektivt genom att aktivera flera varianter av ett grafikkort utan att ändra den ursprungliga versionen.

Genom att skapa en kopia kan man tryggt göra ändringar för olika användningsområden, kunder eller affärsscenarier samtidigt som man bevarar källkoden i Interactive Communication.

## Vad kopieras?

När du kopierar ett interaktivt meddelande dupliceras följande element till det nya konc:t:

- Layout och struktur

- komponenter och fragment

- Databindningar och regler

- Formaterings- och varumärkeskonfigurationer

- Du kan sedan ändra något av dessa element oberoende av varandra i den kopierade IC:n.

## Kopiera en interaktiv kommunikation

![Sök efter IC-dokument](/help/forms/interactive-communication/assets/copy-in-ic.png)

Så här kopierar du en interaktiv kommunikation:

- Navigera till Forms &amp; Documents i AEM gränssnitt.

- Leta reda på den interaktiva kommunikation som du vill kopiera.

- Välj konc.

- Välj Kopiera i verktygsfältet eller på snabbmenyn.

- Navigera till målmappen eller målplatsen.

- Välj Klistra in om du vill skapa en kopia av den interaktiva kommunikationen.

- Ett nytt konc skapas med samma konfiguration som originalet.

## Redigera och återanvänd den kopierade interaktiva kommunikationen

![Sök efter IC-dokument](/help/forms/interactive-communication/assets/paste-in-ic.png)

Efter inklistring av interaktiv kommunikation:

- Öppna den kopierade IC-koden i Interactive Communication Editor.

- Uppdatera innehåll, regler, datamappningar eller layout efter behov.

- Spara och publicera IC när det passar.

- Ändringar som görs i den kopierade IC-koden påverkar inte den ursprungliga interaktiva kommunikationen.

## Bästa praxis

- Behåll den ursprungliga IC:n som baslinje eller huvudversion.

- Byt namn på kopierade IC-kort tydligt för att återspegla deras syfte eller variation.

- Använd kopiera och klistra in tillsammans med versionshantering och kommentarer för bättre spårbarhet.

- Granska databindningar och utdatakanaler efter kopiering för att säkerställa att de är korrekta.

Funktionen Kopiera och Klistra in i interaktiv kommunikation förenklar återanvändning och anpassning genom att tillåta författare att duplicera befintliga konc:er och ändra dem oberoende av varandra. Det möjliggör snabbare utveckling, säkrare experimenterande och enhetlig kommunikationsleverans - utan att riskera att ändringar görs i den ursprungliga interaktiva kommunikationen.

