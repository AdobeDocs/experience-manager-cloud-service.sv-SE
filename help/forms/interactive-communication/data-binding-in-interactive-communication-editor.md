---
title: Skapa ett interaktivt kommunikationsfragment
description: Skapa interaktiva kommunikationsfragment i AEM Forms för att skapa modulära, återanvändbara innehållsblock som ger enhetlighet, sparar tid och stöder personaliserad, datadriven kommunikation.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: 0c84fa812b74368184d7085fecbb11a1ce4dbfd9
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---


# Databindning i Interactive Communication Editor

>[!NOTE]
>
> Funktionen för interaktiv kommunikation ingår i programmet för tidig anmälan. Skicka ett e-postmeddelande från din arbetsadress till `aem-forms-ea@adobe.com` för att begära åtkomst.

>[!IMPORTANT]
>
> **Dokumentation som kan ändras**: Det här snabbbiblioteket testas för närvarande mot produkten och kan komma att uppdateras och revideras. Frågar, exempel och bästa metoder kan ändras i takt med att Forms Experience Builder fortsätter att utvecklas under det program som antagits tidigt.

## &#x200B;1. Inledning

Databindning i Interactive Communication Editor kopplar ihop fälten på arbetsytan med ett styrt datalager så att kommunikationen återges med faktisk, sammanhangsberoende information. Genom att länka komponenter till en formulärdatamodell (FDM) eller global nyttolast kan författare säkerställa noggrannhet, minska det manuella arbetet och leverera dynamiska, personaliserade upplevelser.

Förutom att bara koppla ihop värden stöder databindning i IC visuell mappning, förifyllning och synkronisering, vilket gör att författare kan designa snabbare samtidigt som de följer datasystem och datamodeller.

## &#x200B;2. Egenskaper

2.1 Hantera dataanslutningar (FDM)

- **Välja FDM:** Välj lämplig formulärdatamodell (t.ex. kunder, konton eller profiler). Detta fastställer det auktoritativa schemat för fält, arrayer och objekt som används i kommunikationen.

- **Skapar databindningar:** När bindningar har aktiverats kan varje fält associeras med FDM-sökvägar, vilket minimerar felen och säkerställer en konsekvent integrering.

- **Bindningsfält till datamodeller:** Punktera fält till specifika noder (t.ex. customer.name, policy.holder.id) för att driva återgivningen med livedata och för att stödja valideringar och villkorslogik.

2.2 Skapa databindningar

- **Visuell mappning:** Dra och släpp-mappning mellan fält och FDM-noder hjälper icke-tekniska användare att undvika misstag.

- **Fältassociation:** Definiera målsökväg, datatyp (text, tal, datum, boolesk, bild) och valfria formaterare (t.ex. datummask, valuta).

- **Förhandsgranska bindning:** Testa bindningar med exempeldatauppsättningar för att validera formatering och korrekthet före publicering.

2.3 Binda fält till datamodeller

- **Fältmappning:** Länka text, bild eller upprepade strukturer (tabeller/listor) med rätt FDM-noder. Samlingar kan använda upprepningskällor och mallrader.

- **Datasynkronisering:** Välj enkelriktad (användargränssnittet har fyllts i från modellen) eller tvåvägs (användarindata har sparats tillbaka i modellen).

- **Förifyll:** Använd standardvärden från modellen eller uttrycken för att förenkla datainmatningen och förbättra precisionen.

## &#x200B;3. Användning

Databindning används ofta när kommunikationen måste visa auktoritativa poster eller hämta användarindata. Exempel:

- **Personalization:** Fyll i kundinformation som namn, adress eller kontosaldo.

- **Villkorligt innehåll:** Visa/dölj avsnitt baserat på modellvärden (t.ex. aktiva kontra inaktiva kunder).

- **Samlingar och tabeller:** Återge historik, transaktioner eller specificerade listor från arrayer.

- **Bilder och media:** Bind profilfoton, företagslogotyper eller produktbilder.

- **Granska och e-signera:** Fyll i formulär i förväg med data och tillåt uppdateringar via tvåvägssynkronisering.

Författare väljer vanligtvis FDM tidigt i projektet, mappar fält visuellt under designen och testar med exempeldata före publicering.

## &#x200B;4. Bästa praxis

- **Definiera schemat tidigt:** Slutför FDM innan bindning för att undvika ommappning senare.

- **Använd visuell mappning:** Förhindra stavfel och felmatchade banor genom att dra och släppa.

- **Verifiera datatyper:** Använd formaterare för valuta, datum och telefonnummer för att säkerställa konsekvens.

- **Behåll explicita bindningar:** Varje fält ska mappas tydligt till en enda datanod.

- **Testa med exempeldata:** Förhandsgranska både vanliga fall och kantfall (t.ex. tomma värden, långa arrayer).

- **Begränsa tvåvägssynkronisering:** Använd bara när redigeringar eller godkännanden krävs.

- **Modularisera samlingar:** Använd mallrader för repeterbara strukturer.

- **Skydda känsliga data:** Tillämpa maskering, kryptering och privilegierad åtkomst för PII eller betalningsinformation.

Genom att konfigurera databindning noggrant kan man skapa en tillförlitlig bro mellan design och data, vilket snabbar upp framtagningen av kommunikationsmaterial, säkerställer exakthet och levererar personaliserade upplevelser i stor skala.