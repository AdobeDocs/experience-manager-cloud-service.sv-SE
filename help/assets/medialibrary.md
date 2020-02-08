---
title: AEM Assets vs. AEM MediaLibrary
description: Vanliga frågor och svar om AEM Assets och. AEM Media Library, inklusive skillnaderna mellan de båda.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Vanliga frågor om AEM Assets och AEM MediaLibrary {#aem-assets-vs-aem-medialibrary}

Adobe Experience Manager Assets (AEM) är en integrerad del av AEM-plattformen. Denna smidiga integrering ses som en stor fördel i AEM och säkerställer enhetlighet i innehållshanteringen och hög produktivitet för skribenter.

## Vad är AEM Assets? {#what-is-aem-assets}

AEM Assets är en applikation på AEM Platform som gör att våra kunder kan hantera sina digitala resurser (bilder, videor, dokument och ljudklipp) i en webbaserad databas. AEM Assets innehåller metadata-support, renderingar, Digital Asset Management Finder och administration via användargränssnittet.

## Vad är AEM Media Library? {#what-is-the-aem-media-library}

AEM Media Library är en utsedd del av AEM WCM-innehållslagringsplatsen där bilder och andra delade resurser lagras. Mediebiblioteket använder funktionerna för hantering av digitala resurser i AEM WCM.

## Vad får jag från AEM Assets som inte ingår i AEM WCM? {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

Unika funktioner som bara är tillgängliga för kunder som har AEM Assets är:

1. möjlighet att extrahera och redigera andra metadata än titel, taggar och beskrivning.
1. AEM Resurser Admin, som är tillgänglig från välkomstskärmen genom att klicka på den andra knappen bredvid webbplatsadministratören.
1. Alla arbetsflödessteg som rör Digital Asset Management, som AEM Assets Ingestition, AEM Assets Deletion, AEM Assets Sub-Asset-Handling, AEM Assets-metadataextrahering.
1. bibliotek som innehåller &quot;dam&quot; im-paketutrymme.

Dessa funktioner kräver en giltig licens för AEM Assets.

## Finns AEM Assets som separat paket? {#is-aem-assets-available-as-a-separate-package}

Nej. För att underlätta installation och driftsättning levereras alla AEM-program och tillägg i ett enda paket med alla funktioner inkluderade. Det innebär inte att du har behörighet att använda alla funktioner i paketet.

## Jag vill redigera metadata för digitala resurser. Behöver jag AEM Assets? {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

Om du planerar att redigera andra metadata än titel, beskrivning och taggar måste du licensiera AEM Assets.

## Jag vill använda kategoripredikatet på min webbplats. Behöver jag AEM Assets? {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

Ja, kategoripredikatet och alla andra komponenter som används i Geometrixx Press Center ingår i AEM Assets och kräver en AEM Assets-licens.

## Jag vill automatiskt ändra storlek på bilder vid import. Behöver jag AEM Assets? {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

Ja. Storleksändring och automatisk arbetsflödesdriven omvandling samt möjligheten att hantera renderingar ingår i AEM Assets och kräver en AEM Assets-licens.

## Jag vill ändra storlek på bilder med en anpassad bildkomponent. Behöver jag AEM Assets? {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

Bildkomponenten är en del av AEM WCM. Grafikbiblioteket som används av bildkomponenten (men även av AEM Assets) är en del av AEM-plattformen och kräver ingen AEM Assets-licens.

## Hur kan jag hindra mina användare från att använda AEM Assets om jag inte har licensierat någon AEM Assets? {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

Du kan ta bort alla AEM Assets-specifika arbetsflöden, komponenter, taxonomier, alternativ och AEM Assets-administratören från AEM. På så sätt förhindras användarna från att oavsiktligt använda AEM Resurser-funktioner som du inte licensierat.

## Jag vill lägga till bilder på en sida och vill beskära och ändra storlek på dessa bilder. Behöver jag AEM Assets? {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

I det här fallet behöver man inte köpa AEM Assets, inte ens mediebiblioteket behöver använda bilder på en webbplats eftersom den smarta bildkomponenten tillåter att bilder överförs direkt till sidan.

## En detaljerad lista över funktioner som är tillgängliga i AEM Assets vs Media Library {#listoffeatures}

**AEM Assets**

* Samlingar och ljusbord
* Avancerade metadataegenskaper och hantering
* Adobe Asset Link (anslut till Creative Cloud for enterprise)
* AEM-skrivbordsapp
* Bearbetar profiler
* InDesign-serverintegration
* Resursmallar och katalogproduktionsramverk
* Länkade resurser för Adobe Photoshop, Illustrator och InDesign
* Hantering av flerspråkiga resurser
* PIM-integrering
* Rights Management
* Stöd för Camera RAW
* Hantering och konfiguration av sökfaktorer
* Färdiga DAM-arbetsflöden (till exempel fotografering)
* Resursrapportering och analys:Resursinsikter
* 3D-resurshantering
* Anslutna resurser
* Varumärkesportal
* Självbetjäningsåtkomst
* Bläddra, söka och hämta
* Samlingar och mappdelning
* Administratörsverktyg
* Smarta taggar
* Visuell sökning
* Användargränssnitt för resursadministratör

**Mediebibliotek**

* Grundläggande metadataegenskaper
* Tagghantering
* Versionskontroll
* Statiska återgivningar
* Projekt, uppgifter, arbetsflödesredigering
* Aktivitetsström (tidslinje)
* Query Builder (API)
* Marketing Cloud-integrering
* Anpassning och tillägg av användargränssnitt
* Kommentarer och anteckningar