---
title: Introduktion till produktionsprogram
description: Lär dig vilka produktionsprogram som är och förslag på hur du konfigurerar dem.
exl-id: bb8d4a5a-b26a-4718-9327-149fedb87e6a
source-git-commit: d1b6ef646dd41ce48da37dc1fa99c374d3d231b1
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# Introduktion till produktionsprogram {#production-programs}

Ett produktionsprogram är avsett för ett team som är redo att börja skriva, bygga och testa kod i syfte att distribuera den för att hantera livstrafik.

Efter [skapa produktionsprogram,](creating-production-programs.md) a [guide för att skapa program](using-the-wizard.md) guidar användaren genom de val som görs beroende på vad användaren vill skapa programmet.

## Alternativ för att skapa program {#program-creation-options}

Ditt avtalsavtal med Adobe definierar antalet och typerna av lösningar som är tillgängliga för just er organisation när ni skapar produktionsprogram. Du har kontroll över hur du mappar tillgängliga lösningar till Cloud Manager-program.

I följande tabell beskrivs vanliga scenarier för tillgängliga lösningar och de typiska produktionsprogram som skapas utifrån dem.

| Tillgängliga lösningar | Programalternativ | Vad ingår? | När ska användas | Exempel |
|---------------------|-------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1 Platslösning | Skapa ett program som bara innehåller en plats | 1 produktion + 1 fas, 1 utveckling, 1 snabb utveckling | Ej tillämpligt | Ej tillämpligt |
| 1 Resurslösning | Skapa ett program som bara innehåller 1 resurser | 1 produktion + 1 fas, 1 utveckling, 1 snabb utveckling | Ej tillämpligt | Ej tillämpligt |
| 1 platser +1 resurser | Skapa ett program: <br>1 Sites &amp; Assets-program | 1 produktion + 1 fas, 2 utveckling, 2 snabb utveckling | När en majoritet av de digitala resurserna används som stöd för webbplatsimplementeringen.<br>I sådana fall är de flesta digitala resurser i ett färdigt tillstånd och klara att användas för upplevelser över flera kanaler via Sites.<br>Vanligtvis ansvarar ett team för att hantera innehåll för både platser och resurser. | Bilder som främst används för en webbplats.<br>PDF som ska distribueras via en intern portal som är inbyggd i AEM Sites. |
| 1 platser +1 resurser | Skapa separata program:<br>1 Endast site-program och 1 Endast Assets-program | 1 produktion + 1 fas, 1 utveckling, 1 snabb utveckling<br>1 produktion + 1 fas, 1 utveckling, 1 snabb utveckling | När många digitala resurser inte har direkt stöd för implementering av webbplatser.<br> I sådana fall finns resurserna i olika lägen, inklusive råfilstyper och pågående arbeten.<br>Ett dedikerat kreativt team hanterar digitalt material under sin egen livscykel och har separata arbetsflöden och releasecykler än Sites content management-teamet. | Raw-bilder från en fototagning lagras i Assets-programmet och endast ett fåtal används i Sites-implementeringen.<br>Ett stort antal filtyper i Creative Cloud, som Photoshop och Illustrator, hanteras i AEM Assets och genomgår ett eget arbetsflöde för godkännande innan en färdig resurs genereras.<br>Överväg att använda [Anslutna resurser](/help/assets/use-assets-across-connected-assets-instances.md#overview-of-connected-assets) i sådana fall. |
| 1 plats + 1 plats | Skapa separata program:<br>1 Endast webbplatser och 1 Endast webbplatser | 1 produktion + 1 fas, 1 utveckling, 1 snabb utveckling<br>1 produktion + 1 fas, 1 utveckling, 1 snabb utveckling | För implementering av multi-tenant-platser.<br>I sådana fall måste flera webbplatser med ett eget releaseschema och särskilda utvecklings- och innehållsteam hanteras. | Två varumärken med dedikerade webbplatser och separata utvecklingsteam |


>[!NOTE]
>
>Produktionsprogram [kan inte redigeras och inte tas bort.](editing-programs.md)
