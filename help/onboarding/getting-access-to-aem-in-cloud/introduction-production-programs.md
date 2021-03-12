---
title: 'Introduktion till produktionsprogram '
description: 'Introduktion till produktionsprogram '
translation-type: tm+mt
source-git-commit: 5773683a75254855687266929a3e1876c8f06e61
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---


# Introduktion till produktionsprogram {#production-programs}

Ett *Production*-program är avsett för en användare som känner till AEM och Cloud Manager och som är redo att börja skriva, bygga och testa kod i syfte att distribuera den till Production.

>[!NOTE]
>Du kan inte ta bort ett produktionsprogram.

En guide hjälper användaren att göra val beroende på vad användaren vill med att skapa programmet. Baserat på de outnyttjade lösningsberättiganden som är tillgängliga för den specifika kunden eller organisationen, har användaren kontroll över hur man mappar tillgängliga (oanvända) lösningsberättiganden till Cloud Manager-program.

## Överväganden om att skapa program {#program-creation-considerations}

I tabellen nedan beskrivs vanliga scenarier som ska beaktas när du skapar program i Cloud Manager:

| Oanvända lösningsberättiganden i organisationen | Skapa programalternativ | Vad ingår? | När du ska använda och andra överväganden |
|--- |--- |--- |--- |
| 1 Platslösning | Skapa 1 Sites only-program | 1 produktion + 1 fas, 1 utveckling | NA |
| 1 Resurslösning | Skapa ett program med endast 1 Assets | 1 produktion + 1 fas, 1 utveckling | NA |
| 1 platser +1 resurser | Skapa ett program: 1 Sites &amp; Assets-program | 1 produktion + 1 fas, 2 utveckling | En majoritet av de digitala resurserna används för att stödja implementeringen av webbplatser. De flesta digitala resurser är färdiga och klara att användas för upplevelser över flera kanaler via Sites. Vanligtvis ansvarar ett team för att hantera innehåll för både Sites och Assets. **Vanliga exempel**: Bilder som främst används för en webbplats. PDF-filer som ska distribueras via en intern portal som byggts in i AEM Sites. |
| 1 platser +1 resurser | Skapa separata program: 1 Endast site-program och 1 Endast Assets-program | 1 produktion + 1 fas, 1 utveckling<br> 1 produktion + 1 fas, 1 utveckling | Många digitala resurser har inte direkt stöd för implementering av webbplatser. Resurser som hanteras är i olika lägen, inklusive råfilstyper och pågående arbeten. Ett dedikerat kreativt team hanterar digitalt material under sin egen livscykel och har separata arbetsflöden och releasecykler än Sites content management-teamet. *Vanliga exempel*: Råbilder från en fotografering lagras i Assets-programmet och endast ett fåtal används i Sites-implementeringen. Ett stort antal filtyper i Creative Cloud, som Photoshop och Illustrator, hanteras i AEM Assets och genomgår ett eget arbetsflöde för godkännande innan en färdig resurs genereras. Funktioner att utnyttja: [Anslutna resurser](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html?lang=en#overview-of-connected-assets) |
| 1 plats + 1 plats | Skapa separata program: 1 Endast webbplatser och 1 Endast webbplatser | 1 produktion + 1 fas, 1 utveckling<br>1 produktion + 1 fas, 1 utveckling | Implementering av multi-tenant-sajter. Flera sajter med ett eget releaseschema och särskilda utvecklings- och innehållsteam. *Vanliga exempel*: Två varumärken med dedikerade webbplatser och separata utvecklingsteam |


