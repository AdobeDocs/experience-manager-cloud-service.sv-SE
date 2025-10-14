---
title: Introduktion till produktionsprogram
description: Lär dig vilka produktionsprogram som är och förslag på hur du konfigurerar dem.
exl-id: bb8d4a5a-b26a-4718-9327-149fedb87e6a
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 2573eb5f8a8ff21a8e30b94287b554885cd1cd89
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---


# Introduktion till produktionsprogram {#production-programs}

Ett produktionsprogram är avsett för ett team som är redo att börja skriva, bygga och testa kod i syfte att distribuera den för att hantera livstrafik.

När du har [skapat produktionsprogrammet](creating-production-programs.md) guidar en [programskapandeguide](using-the-wizard.md) användaren genom de val som beror på vad användaren har för syfte med att skapa programmet.

## Alternativ för att skapa program {#program-creation-options}

Ditt avtalsavtal med Adobe definierar antalet och typerna av lösningar som är tillgängliga för just er organisation när ni skapar produktionsprogram. Du har kontroll över hur du mappar tillgängliga lösningar till Cloud Manager-program.

I följande tabell beskrivs vanliga scenarier för tillgängliga lösningar och de typiska produktionsprogram som skapas utifrån dem.

| Tillgängliga lösningar | Programalternativ | Vad ingår? | När ska användas | Exempel |
|---------------------|-------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1 Platslösning | Skapa ett program som bara innehåller en plats | 1 produktion + 1 fas, 1 utveckling, 1 snabb utveckling | Ej tillämpligt | Ej tillämpligt |
| 1 ASSETS | Skapa ett program som endast innehåller Assets | 1 produktion + 1 fas, 1 utveckling, 1 snabb utveckling | Ej tillämpligt | Ej tillämpligt |
| 1 sajter +1 Assets | Skapa ett program: <br>1 Sites &amp; Assets | 1 produktion + 1 fas, 2 utveckling, 2 snabb utveckling | När en majoritet av de digitala resurserna används som stöd för webbplatsimplementeringen.<br>I sådana fall är de flesta digitala resurser i ett färdigt tillstånd och klara att användas för flerkanalsupplevelser via webbplatser.<br>Vanligtvis ansvarar ett team för att hantera innehåll för både Sites och Assets. | Bilder som främst används för en webbplats.<br>En intern portal som byggts i AEM Sites distribuerar PDF. |
| 1 sajter +1 Assets | Skapa separata program:<br>1 Endast webbplatser och 1 program endast för Assets | 1 produktion + 1 fas, 1 utveckling, 1 snabb utveckling<br>1 produktion + 1 fas, 1 utveckling, 1 snabb utveckling | När många digitala resurser inte har direkt stöd för implementering av webbplatser.<br> I sådana fall finns resurser i olika lägen, inklusive råfilstyper och pågående arbeten.<br>Ett dedikerat kreativt team hanterar digitala resurser under sin egen livscykel och har separata arbetsflöden och releasecykler än Sites content management-teamet. | Raw-bilder från en fototagning lagras i Assets-programmet och endast ett fåtal används i Sites-implementeringen.<br>Ett stort antal filtyper i Creative Cloud, som Photoshop och Illustrator, hanteras i AEM Assets och genomgår ett eget arbetsflöde för godkännande innan en färdig resurs genereras.<br>Överväg att använda [Ansluten Assets](/help/assets/use-assets-across-connected-assets-instances.md#overview-of-connected-assets) i sådana fall. |
| 1 plats + 1 plats | Skapa separata program:<br>1 Endast platser och 1 Endast platser-program | 1 produktion + 1 fas, 1 utveckling, 1 snabb utveckling<br>1 produktion + 1 fas, 1 utveckling, 1 snabb utveckling | För implementeringar av multi-tenant-platser.<br>I sådana fall måste flera webbplatser med ett eget releaseschema samt dedikerade utvecklings- och innehållsteam hanteras. | Två varumärken med dedikerade webbplatser och separata utvecklingsteam |


>[!NOTE]
>
>Produktionsprogrammen [&#x200B; kan redigeras men inte tas bort](editing-programs.md).
