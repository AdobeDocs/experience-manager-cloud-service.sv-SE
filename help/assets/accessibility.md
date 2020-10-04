---
title: Tillgänglighet i [!DNL Experience Manager Assets]
description: Se hur tillgänglighetsfunktionerna [!DNL Adobe Experience Manager] i en Cloud Service kan hjälpa användare med funktionshinder.
contentOwner: AG
translation-type: tm+mt
source-git-commit: d0be8ff6c8f9e0c37bd4dc9f66d80e19ab7e1508
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 1%

---


<!--
Original scope of this article for Core Assets for all a11y topics is around the following topics. This has changed since then but keeping this list of topics for posterity's sake.

* Convert the absolute doc links to relative links.
* Add an overview
* Compile a list of enhancements done in the last ~1 year.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, etc.)
* Specific user tasks supported, such as, download assets, datepicker, editing metadata, etc.
* Support matrix of user tasks with browsers and screen readers + OSes combinations
* Exceptions that users should be aware of.
* CTA – what is next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Examples of other a11y DX Docs from Elle.
  * Link to a11y-specific channels to report issues, seek support, or request enhancements, if any. Available info from Elle.
-->

# Accessibility in [!DNL Adobe Experience Manager Assets] as a Cloud Service {#accessibility-in-aem-assets}

Adobe strävar efter att ta fram produkter för alla användare, även för personer med funktionshinder. [!DNL Adobe Experience Manager] har ständigt förbättrats för att tillgodose behoven hos alla typer av användare. [!DNL Experience Manager] publicerar överensstämmelseinformation som beskriver de standarder som den följer, beskriver tillgänglighetsfunktionerna i produkten och beskriver efterlevnadsnivån. Det hjälper användarna att förstå hur stor följsamheten är.

[!DNL Adobe Experience Manager] ger olika nivåer av stöd för följande standarder:

* [Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [Reviderat avsnitt 508](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines).
* [WAI-ARIA](https://www.w3.org/WAI/standards-guidelines/aria/).
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549).

Om du vill få tillgång till rapporten med information om efterlevnadsnivåerna läser du [](https://www.adobe.com/accessibility/compliance.html) sidan Accessibility conformance reports (ACR) för alla Adobe-lösningar.

## Hjälpmedel {#at-support}

Användare med funktionshinder förlitar sig ofta på maskinvara och programvara för att få tillgång till webbinnehåll. Dessa verktyg kallas hjälpmedelstekniker. [!DNL Adobe Experience Manager Assets] arbeta med följande typer av hjälpmedelstekniker för att ge användarna support när de använder programvarans kärnfunktioner:

* Skärmläsare.
* Programvara för taligenkänning.
* Tangentbordsanvändning - navigering och genvägar.
* Hjälpmaskinvara, inklusive switchkontroller, uppdateringsbara blindskriftsskärmar och andra indataenheter.
* Förstoringsverktygen i användargränssnittet.

## [!DNL Experience Manager Assets] användningsfall som är tillgängliga {#accessible-assets-use-cases}

Tillgänglighetsfunktionerna uppfyller [!DNL Experience Manager]dessutom två viktiga krav från [!DNL Experience Manager] användarna och deras kunder.

För designers och kreatörer finns det funktioner för att skapa och publicera tillgängligt innehåll som i sin tur används av kunder och besökare på webbplatser. Innehållet kan användas av personer med funktionshinder med hjälp av hjälpmedelstekniker. Mer information finns i Riktlinjer för [webbhjälpmedel](/help/onboarding/accessibility/web-accessibility.md).

Dessutom [!DNL Experience Manager] kan användare och administratörer med funktionshinder få tillgång till användargränssnittet och kontrollerna för att skapa och hantera innehåll. Personer med funktionshinder kan använda hjälpmedelstekniker för att navigera, använda och hantera [!DNL Assets] funktioner.

De viktigaste funktionerna i [!DNL Assets] är mer tillgängliga än tidigare och uppdateras regelbundet för att förbättra efterlevnaden av globala standarder. CRUD-åtgärderna i Assets har en viss grad av inbyggda hjälpmedel. DAM-arbetsflöden som att lägga till, hantera, söka efter och distribuera resurser är tillgängliga med hjälp av kortkommandon, skärmläsartext, färgkontrast och så vidare.

## Stöd för användning av tangentbord {#keyboard-use}

Många element i användargränssnittet som är klickbara eller kan användas med en pekare kan också aktiveras med tangentbordet. Med ett tangentbord kan användarna fokusera på gränssnittselement och vidta lämpliga åtgärder. Användare kan använda kortkommandon direkt för att utlösa ett kommando eller en åtgärd utan att behöva fokusera på gränssnittselement och utlösa det med tangentbordet. Användarna kan till exempel öppna tidslinjen för en resurs på vänster sida genom att bläddra till gränssnittskontrollen med ett tangentbord och trycka på Retur och trycka på `alt + 2` kortkommandot.

<!-- TBD items:

* The button/menu to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the buttons like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### Kortkommandon i resurser {#keyboard-shortcuts}

<!-- TBD: Add here only those keyboard shortcuts that work for/with Assets. Do with Oct release.
-->

| Användargränssnitt eller scenario | Kortkommando | Åtgärd |
|---|---|---|
| Kolumnvy i Assets-användargränssnittet | Upp- och nedpilar | Navigera till filer och mappar i samma hierarki. |
| Kolumnvy i Assets-användargränssnittet | Vänster- och högerpilstangenter | Navigera till filer och mappar ovanför eller nedanför den aktuella mappen. |
| Bläddra bland mappar i resurser | `/` | Anropa sökning genom att öppna Omnissearch-rutan. |
| Resurskonsol | ` | Växla sidoskenor |
| Resurskonsol | Alt+1 | Öppna innehållsträdet. |
| Resurskonsol | Alt+2 | Öppna [!UICONTROL Navigation] siderail. |
| Resurskonsol | Alt+3 | Visning [!UICONTROL Timeline] av en vald resurs. |
| Resurskonsol | Alt+4 | Öppna Live Copy-referenser för den valda resursen. |
| Resurskonsol | Alt+5 | Anropa sökning och sökning i den markerade mappen. |
| Resursen eller mappen är markerad | Backsteg | Ta bort den markerade resursen eller mappen. |
| Resursen eller mappen är markerad | `p` | Öppna sidan Egenskaper för den valda resursen. |
| Resursen eller mappen är markerad | `e` | Redigera den valda resursen. |
| Resursen eller mappen är markerad | `m` | Flytta den markerade resursen. |
| Resursen eller mappen är markerad | Ctrl + C | Kopiera den markerade resursen. |
| Resursen eller mappen är markerad | Esc | Avmarkera markeringen. |
| Dialogrutan öppnas och är i fokus | Esc | Stäng dialogrutan. |
| I en mapp i DAM | Ctrl + V | Klistra in den kopierade resursen. |
| Resurskonsol | Ctrl+A | Markera alla resurser. |
| Egenskapssidor för resurs | Ctrl + S | Spara ändringar. |
| Resurskonsol | `?` | Visa en lista med kortkommandon. |

De flesta kortkommandon som gäller för [!DNL Experience Manager] konsoler gäller även för Resurser. Se [Kortkommandon för konsoler](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/essentials/keyboard-shortcuts.html). Se hur du [aktiverar eller inaktiverar kortkommandon](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md).

## Logga in och navigera i [!DNL Assets] användargränssnittet {#login}

Användare kan använda tangentbordet för att navigera till och fylla i inloggningsfältet för att logga in. Felmeddelandena på grund av felaktiga kombinationer av användarnamn och lösenord på inloggningssidan meddelas av skärmläsare varje gång felet inträffar.

Efter inloggning kan DAM-användare navigera till [!DNL Assets] användargränssnittet med tangentbordet. Tangentbordsnavigeringsordningen är från vänster till höger och uppifrån och ned. När du navigerar med ett tangentbord markeras alla alternativ som kan användas och som är i fokus med bättre färgkontrast och berättarrösten läggs till i skärmläsaren. Läget - utökat eller komprimerat - för de fokuserade alternativen på menyn presenteras av en skärmläsare.

Om en användare utökar alternativet för hjälp eller användarprofil från menyn visas rätt alternativ eller status av skärmläsaren. Om en användare utökar alternativet för användarprofil kan de tillgängliga alternativen väljas med ett tangentbord. En användare kan till exempel personifiera en annan användare. Alternativet för användargränssnittet och felmeddelandet

![Tangentbordsnavigering för de översta alternativen i användargränssnittet i Experience Manager](assets/keyboard-navigation-in-aem.gif)

*Bild: Navigera genom alternativen längst upp i användargränssnittet i Experience Manager med hjälp av`Tab`tangenten.*

Om en användare söker efter en sträng från [!UICONTROL Help] alternativet, meddelar en berättare att han/hon söker i hjälpen för att ange att en sökning pågår.

## Bläddra bland befintliga resurser och visa relaterad information {#browse}

I [!DNL Assets] användargränssnittet kan användare använda tangentbordet för att bläddra igenom listan med befintliga digitala resurser i DAM-databasen, förhandsgranska eller ladda ned en resurs, se genererade återgivningar, växla vy, se genererade återgivningar, se tidslinje och versionshistorik, se kommentarer och referenser samt visa och hantera metadata.

<!-- TBD: Not sure about the following list items mean:

In Experience Manager header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close button in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close button through keyboard press in version preview dialog. After fix, user can close dialog through close button using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

Följande funktioner förbättrar tillgängligheten när du bläddrar i resurskatalogen:

* Skärmläsaren meddelar textalternativ som avbildar ikonernas syfte eller funktion i stället för deras namn.
* Användare kan komma åt och fokusera alternativen för det interaktiva användargränssnittet i referenslistan med resurser med hjälp av tangentbordstangenter.
* Elementen på varje rad i listvyn presenteras som elementen på samma rad av skärmläsare.
* Användarfokus när du navigerar med `Tab` tangenten kan flyttas till stängningsalternativet i förhandsversionen.
* När du använder tangentbordet för att bläddra har de markerade alternativen för det användbara gränssnittet mer framträdande visuellt fokus med förbättrad kontrast. Det gör det fokuserade området mer identifierbart för användaren.
* Om du använder `Esc` tangenten för att ta bort snabbåtgärdsikonerna från miniatyrbildsvyn tas inte tangentbordsfokus bort från det senast fokuserade objektet.
* När en resurs är markerad kan du öppna referenslistan genom att trycka på Alt+4. Med hjälp av `Tab` tangenten kan användarna navigera genom referensposterna som inte är noll.
* Kommentarer om en resurs är tillgängliga på resursens tidslinje. Det går att komma åt via tangentbordet.
* Visningsinställningar i Experience Manager kan du nå med tangentbordet. Användaren kan navigera bland de tillgängliga kortstorlekarna med piltangenterna och välja och bläddra igenom för att ange andra element i den befintliga vyn Visa inställningar.

<!-- TBD: Gradually,  as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?

-->

## Hantera digitala resurser {#manage-assets}

Många resurshanteringsåtgärder, till exempel CRUD-åtgärder, hämtning av resurser och tillägg av metadata, är tillgängliga i olika grad. Med resurser kan du utföra åtgärderna med hjälp av olika hjälpmedelstekniker, till exempel en skärmläsare och ett tangentbord.

Se en videodemonstration av hur du använder ett tangentbord för att [bläddra i databasen och hämta en resurs](https://youtu.be/K3dgqMRQJys).

För metadataåtgärder som vanligtvis utförs av roller som marknadsförare och administratörer förbättrar följande funktioner tillgängligheten:

* [!UICONTROL Save & Close] på sidan Egenskaper för resurser kan nu öppnas med hjälp av tangentbordet.
* Skärmläsare meddelar alternativ för att ta bort de markerade taggarna på fliken Grundläggande i egenskapsknapparna för resurser för att ta bort de markerade taggarna.
* Dialogrutan för datumväljare kan användas med ett tangentbord. Datumväljaren används för att ställa in tider och tider.
* Dragningsfunktionen med tangentbordet fungerar på rätt sätt i metadatamodigeraren i bläddringsläge i skärmläsaren.
* En användare kan flytta fokus med tangentbordet till fältet Lägg till användare eller grupp under Stängd användargrupp på fliken Behörigheter i mappegenskaperna.

## Söka efter digitala resurser {#search-assets}

En snabb och smidig sökupplevelse av resurser ökar innehållets hastighet. Användningsexempel för snabb innehållshantering är en del av kärnfunktionaliteten [!DNL Assets] . Om du vill starta en sökning från omsökningsfältet kan användarna använda kortkommandon `/` eller använda `Tab` tillsammans med skärmläsare för att snabbt hitta sökalternativet. Skärmläsaren visar namnet på alternativet som [!UICONTROL Search Button] när fokus är på ![sökalternativet](assets/do-not-localize/search_icon.png)för sökalternativ. Användarna kan trycka på `Return` för att öppna rutan Sök. Skärmläsaren lägger inte bara till en berättarröst för det nyckelord som skrivs i sökrutan utan lägger även till en berättarröst för de förslag som ges av [!DNL Experience Manager Assets]. Användare kan använda en kombination av piltangenter `Return`och `Tab` för att komma åt de olika alternativen för att utlösa en sökning.

Sökfunktionen är mer tillgänglig med följande funktioner:

* Sidtitel, som är tillgänglig för en skärmläsare, hjälper dig att identifiera sidan som resursens söksida.
* Användare söker efter resurser inifrån sökfältet. Använd antingen tangentbordet eller kortkommandot `/` för att komma åt Omnissearch bar.
* Börja skriva söknyckelordet och använd tangentbordet för att välja automatiska förslag. Tryck på returtangenten för att acceptera en automatiskt föreslagen sträng och söka efter resurser för den.
* Skärmläsare kan identifiera och meddela kryssrutorna för blandade tillstånd (där kryssrutorna för första nivån inte markeras och genomstrykas om du inte markerar alla kapslade prefix) på panelen Filter när sökresultaten filtreras.
* Användarfokus flyttas till sökalternativen när Omnissökrutan har stängts.

Vid filtrering av sökresultat:

* Sökresultatsidan har en informativ titel som ger en bättre förståelse för skärmläsaranvändare.
* En skärmläsare meddelar alternativen i sökfiltret som utökningsbara dragspelspaneler.
* Förutsägelser med knappar för blandat läge meddelas av skärmläsare.

## Dela resurser {#share-assets}

<!-- TBD: Accessibility in DA, BP, AAL? Asked CCE team for AAL content?
-->

Följande funktioner förbättrar tillgängligheten när du delar resurser:

* En användare kan flytta fokus med tangentbordet i fältet Sök och lägg till e-postadress i dialogrutan för länkdelning.

* Skärmläsarna visas i dialogrutan för länkdelning när du navigerar i bläddringsläge.

   * Lägg inte till en berättarröst i tabellinformationen så fort dialogrutan har lästs in.
   * Kan navigera till alla förslag i listan.
   * Lägg till en berättarröst för de förslag som visas för fälten Lägg till e-postadress och Sök.

## Tillgänglighet i [!DNL Dynamic Media] {#dynamic-media-accessibility}

När du använder Dynamic Media kan följande funktioner göra den tillgänglig:

* En användare kan fokusera på `Flyout`, `InlineZoom`, `Shoppable_Banner`, `Zoom_dark`, `Zoom_light`och `ZoomVertical_dark`alternativ med hjälp av `ZoomVertical_light` nyckeln i visningsprogram för tillgångsinformation i `Tab` [!DNL Dynamic Media].

## Tillgänglig dokumentation {#accessible-docs}

[!DNL Experience Manager] innehåller tillgänglig dokumentation som kan användas av personer med funktionshinder. Följande hjälper till att göra innehåll tillgängligt för tillfället, medan Adobe fortsätter att förbättra mallen och innehållet:

* Skärmläsare kan läsa texten.
* Bilder och illustrationer har alternativ text tillgänglig.
* Tangentbordsnavigering är möjlig.
* Kontrastförhållanden hjälper till att lyfta fram vissa delar av dokumentationswebbplatsen.

<!-- 
## More resources for accessibility {#a11y-resources}

TBD: If anyone is aware of AEM-specific resources that help users leverage any accessibility features or use any assistive technology with AEM, please share or leave a link here.
-->

## Förbättringar i [!DNL Experience Manager Assets] releaser {#rn-fixes}

En lista med specifika förbättringar som gjorts i varje enskild release finns i [versionsinformationen](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/home.html) för respektive version.

>[!MORELIKETHIS]
>
>* [AEM för tillgänglighet](/help/onboarding/accessibility/web-accessibility.md)
>* [Överensstämmelserapporter för Adobe-lösningar](https://www.adobe.com/accessibility/compliance.html)

