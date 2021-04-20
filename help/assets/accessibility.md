---
title: Hjälpmedel i [!DNL Experience Manager Assets]
description: Se hur tillgänglighetsfunktionerna i [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] kan hjälpa användare med funktionshinder.
contentOwner: AG
feature: Accessibility,Asset Management
role: Business Practitioner,Architect,Leader
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '1900'
ht-degree: 1%

---


<!--
Possible topics to cover in this article are below.

* Compile a list of enhancements done in the last ~1 year.
* Showcase a few prominent use cases (search?) in a screencast.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, etc.
* List all UIs that are keyboard navigable.
* Unified list of the product tasks supported, such as, search assets, download assets, add or editing metadata, use DM Viewers, etc.
* Do we need to add support matrix of user tasks with browser and screen reader combinations. Everything may not work in all browsers and/or using all screen readers.
* Any exceptions that users should be aware of. It may help to call out (it may be done in ACR) what tasks are NOT supported.
* CTAs – what's next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Link to a11y-specific online methods to report issues, seek support, or request enhancements, if any. Asked the a11y team on Slack.
-->

# Hjälpmedelsfunktioner i [!DNL Adobe Experience Manager Assets] som [!DNL Cloud Service] {#accessibility-in-aem-assets}

[!DNL Adobe Experience Manager] gör att skribenter och utgivare kan leverera fantastiska upplevelser på webben. Adobe strävar efter att inkludera personer som skapar funktionshinder genom att förbättra tillgängligheten för [!DNL Experience Manager]. Programmen har ständigt förbättrats för att uppfylla behoven hos alla typer av användare och följer världsstandarden som omfattar personer med nedsatt syn, hörsel, mobilitet eller andra funktionshinder.

[!DNL Experience Manager] publicerar överensstämmelseinformation som beskriver de standarder som den följer, beskriver tillgänglighetsfunktionerna i produkten och beskriver efterlevnadsnivån. Rapporterna om överensstämmelse för tillgänglighet hjälper [!DNL Experience Manager]-användare att förstå graden av efterlevnad av olika standarder. Tack vare förbättringarna i [!DNL Assets] kan alla användare använda gränssnitten enkelt via tangentbord, skärmläsare, förstoringsglaset och annan hjälpmedelsteknik.

[!DNL Experience Manager] ger olika nivåer av stöd för följande standarder:

* [Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [Reviderad paragraf 508 i Rehabilitation Act](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines).
* [Accessibility Initiative - Accessible Rich Internet Applications (WAI-ARIA) av W3C](https://www.w3.org/WAI/standards-guidelines/aria/).
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549).

Om du vill läsa en rapport med information om efterlevnadsnivån läser du [Rapport om tillgänglighetsöverensstämmelse](https://www.adobe.com/accessibility/compliance.html) (ACR).

<!-- TBD: Add link after release.
To know how [!DNL Dynamic Media] is accessible, see [accessibility in [!DNL Dynamic Media]](/). -->

## Hjälpmedelstekniker {#at-support}

Användare med funktionshinder förlitar sig ofta på maskinvara och programvara för att få tillgång till webbinnehåll och använda programvaror. Dessa verktyg kallas hjälpmedelstekniker. [!DNL Experience Manager Assets] kan fungera med följande typer av hjälpmedelstekniker (AT) när du använder programmets huvudfunktioner:

* Skärmläsare och skärmförstorare.
* Programvara för taligenkänning.
* Tangentbordsanvändning - navigering och genvägar.
* Hjälpmaskinvara, inklusive switchkontroller, uppdateringsbara blindskriftsskärmar och andra indataenheter.
* Förstoringsverktygen i användargränssnittet.

## [!DNL Experience Manager Assets] användningsfall som är tillgängliga  {#accessible-assets-use-cases}

I [!DNL Experience Manager] uppfyller hjälpmedelsfunktionerna två viktiga krav för [!DNL Experience Manager]-användare och deras kunder.

* För designers och kreatörer finns det funktioner för att skapa och publicera tillgängligt innehåll som i sin tur används av kunder och besökare på webbplatser. Innehållet kan användas av personer med funktionshinder med hjälp av hjälpmedelstekniker. Mer information finns i [riktlinjer för webbhjälpmedel](/help/onboarding/accessibility/web-accessibility.md).
* [!DNL Experience Manager] gör det även möjligt för användare och administratörer med funktionshinder att få tillgång till användargränssnittet och kontrollerna för att skapa och hantera innehåll. Personer med funktionshinder kan använda hjälpmedelstekniker för att navigera, använda och hantera [!DNL Assets]-funktionen.

Kärnfunktionerna i [!DNL Assets] är mer tillgängliga än tidigare och uppdateras regelbundet för att förbättra efterlevnaden av globala standarder. CRUD-åtgärderna i [!DNL Assets] har en viss grad av inbyggt hjälpmedel. DAM-arbetsflöden som att lägga till, hantera, söka efter och distribuera resurser är tillgängliga med hjälp av kortkommandon, skärmläsartext, färgkontrast och så vidare.

## Stöd för användning av tangentbord {#keyboard-use}

Många element i användargränssnittet som är klickbara eller kan användas med en pekare kan också aktiveras med tangentbordet. Med ett tangentbord kan användarna fokusera på gränssnittselement och vidta lämpliga åtgärder. Användare kan använda kortkommandon direkt för att utlösa ett kommando eller en åtgärd utan att behöva fokusera på gränssnittselement och utlösa det med tangentbordet. Användare kan till exempel öppna tidslinjen för en resurs på vänster sida genom att bläddra till användargränssnittskontrollen med ett tangentbord och välja `Return` och välja kortkommando för `Alt + 2`.

<!-- TBD items:

* The button/menu to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the buttons like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### Kortkommandon i [!DNL Assets] {#keyboard-shortcuts}

Följande åtgärder i [!DNL Assets] fungerar med de angivna kortkommandona. De flesta kortkommandon som gäller för [!DNL Experience Manager]-konsoler gäller även för [!DNL Assets]. Se [kortkommandon för Konsoler](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md). Se hur du [aktiverar eller inaktiverar kortkommandona](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md).

| Användargränssnitt eller scenario | Kortkommando | Åtgärd |
|---|---|---|
| Kolumnvy i [!DNL Assets]-användargränssnitt | Upp- och nedpilar | Navigera till filer och mappar i samma hierarki. |
| Kolumnvy i [!DNL Assets]-användargränssnitt | Vänster- och högerpilstangenter | Navigera till filer och mappar ovanför eller nedanför den aktuella mappen. |
| Bläddra bland mappar i [!DNL Assets] | `/` | Anropa sökning genom att öppna Omnissearch-rutan. |
| [!DNL Assets] Konsol | ` | Växla sidoskenor |
| [!DNL Assets] Konsol | `Alt + 1` | Öppna innehållsträdet. |
| [!DNL Assets] Konsol | `Alt + 2` | Öppna [!UICONTROL Navigation] vänster skena. |
| [!DNL Assets] Konsol | `Alt + 3` | Visa [!UICONTROL Timeline] för en markerad resurs. |
| [!DNL Assets] Konsol | `Alt + 4` | Öppna Live Copy-referenser för den valda resursen. |
| [!DNL Assets] Konsol | `Alt + 5` | Anropa sökning och sökning i den markerade mappen. |
| Resursen eller mappen är markerad | Backsteg | Ta bort den markerade resursen eller mappen. |
| Resursen eller mappen är markerad | `p` | Öppna sidan Egenskaper för den valda resursen. |
| Resursen eller mappen är markerad | `e` | Redigera den valda resursen. |
| Resursen eller mappen är markerad | `m` | Flytta den markerade resursen. |
| Resursen eller mappen är markerad | `Ctrl + c` | Kopiera den markerade resursen. |
| Resursen eller mappen är markerad | `Esc` | Avbryt markeringen. |
| Dialogrutan öppnas och är i fokus | `Esc` | Stäng dialogrutan. |
| I en mapp i DAM | `Ctrl + v` | Klistra in den kopierade resursen. |
| [!DNL Assets] Konsol | `Ctrl + A` | Markera alla resurser. |
| Egenskapssidor för resurs | `Ctrl + S` | Spara ändringar. |
| [!DNL Assets] Konsol | `?` | Visa en lista med kortkommandon. |

## Logga in och navigera i [!DNL Assets]-användargränssnittet {#login}

Användare kan använda tangentbordet för att navigera till och fylla i inloggningsfältet för att logga in. Felmeddelandena på grund av felaktiga kombinationer av användarnamn och lösenord på inloggningssidan meddelas av skärmläsare varje gång felet inträffar.

Efter inloggning kan DAM-användare navigera i [!DNL Assets]-användargränssnittet med tangentbordet. Elementen i användargränssnittet, som vänsterkant, menyer, användarprofil, sökfält, filer och mappar samt inställningar för administration och konfiguration, kan navigeras med tangentbordet. Tangentbordsnavigeringsordningen är från vänster till höger och uppifrån och ned. När du navigerar med ett tangentbord markeras ett alternativ som kan användas när det är i fokus med bättre färgkontrast och berättas av en skärmläsare. Om det är lämpligt kommer läget - t.ex. utvidgat, komprimerat och blandat läge - för de fokuserade alternativen på menyn att meddelas av en skärmläsare. Syftet med det användbara alternativet tillkännages också av en skärmläsare i stället för, till exempel utseendet eller gränssnittsplaceringen.

Om en användare utökar alternativet för hjälp eller användarprofil från menyn visas rätt alternativ eller status av skärmläsaren. Om en användare utökar alternativet för användarprofil kan de tillgängliga alternativen väljas med ett tangentbord. En administratör kan till exempel personifiera en annan användare. Om en användare söker efter en sträng med alternativet [!UICONTROL Help], visas &quot;Hjälp för sökning&quot; som indikerar att en sökning pågår.

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## Bläddra bland resurser och visa relaterad information {#browse}

I [!DNL Assets]-användargränssnittet kan användare använda tangentbordet för att bläddra igenom listan över befintliga digitala resurser i DAM-databasen, förhandsgranska eller ladda ned en resurs, se genererade återgivningar, växla vyer, se genererade återgivningar, se tidslinje och versionshistorik, se kommentarer och referenser samt visa och hantera metadata.

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
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
* När du navigerar med `Tab`-tangenten kan fokus flyttas till stängningsalternativet i förhandsversionen.
* När du använder tangentbordet för att bläddra har de markerade alternativen för det användbara gränssnittet mer framträdande visuellt fokus med förbättrad kontrast. Det gör det fokuserade området mer identifierbart för användaren.
* Om du använder `Esc`-tangenten för att ta bort snabbikonerna från miniatyrbildsvyn tas inte tangentbordsfokus bort från det senast fokuserade objektet.
* När en resurs är markerad och du väljer kortkommandot `Alt + 4` öppnas listan [!UICONTROL References] i den vänstra listen. Med `Tab`-tangenten kan användare navigera genom referensposter som inte är noll. Att bläddra igenom enbart referensposter som inte är noll sparar både arbete och tangenttryckningar.
* Kommentarer om en resurs är tillgängliga på resursens tidslinje. Det är tillgängligt om du har åtkomst till den vänstra listen via ett tangentbord eller ett kortkommando.
* [!UICONTROL View Settings] som  [!DNL Experience Manager] är tillgängliga via tangentbordet. Användare kan navigera bland de tillgängliga kortstorlekarna med piltangenterna och välja och bläddra igenom för att ange andra element i den befintliga vyn Visa inställningar.

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## Hantera digitala resurser {#manage-assets}

Många resurshanteringsåtgärder, som CRUD-åtgärder, hämtning av resurser och tillägg av metadata, är tillgängliga i olika grader. [!DNL Assets] gör att du kan utföra åtgärderna med hjälp av olika hjälpmedelstekniker, till exempel en skärmläsare och ett tangentbord.

Se en videodemonstration av hur du använder ett tangentbord för att [bläddra i databasen och hämta en resurs](https://youtu.be/K3dgqMRQJys).

För metadataåtgärder som vanligtvis utförs av roller som marknadsförare och administratörer förbättrar följande funktioner tillgängligheten:

* [!UICONTROL Save & Close] kan du nu komma åt alternativ på  [!UICONTROL Properties] resurssidan med hjälp av tangentbordet.
* Skärmläsare meddelar alternativen för att ta bort de markerade taggarna på fliken [!UICONTROL Basic] för resursen [!UICONTROL Properties].
* Användare kan använda popup-dialogrutan Datumväljare med ett tangentbord. Användargränssnittselementet Datepicker används för att ställa in tider och tider och välja datum.
* Dragningsfunktionen med tangentbordet fungerar korrekt i [!UICONTROL Metadata Schema Editor] i skärmläsarläge.
* En användare kan flytta fokus med tangentbordet till fältet Lägg till användare eller grupp under [!UICONTROL Closed User Group] på fliken [!UICONTROL Permissions] i mappen [!UICONTROL Properties].

## Sök efter digitala resurser {#search-assets}

En snabb och smidig sökupplevelse av resurser ökar innehållets hastighet. Användningsexempel för innehållshastighet är en del av de centrala [!DNL Assets]-funktionerna. Om du vill starta en sökning från omsökningsfältet kan användarna använda kortkommandot `/` eller använda `Tab` tillsammans med skärmläsare för att snabbt hitta sökalternativet. Skärmläsaren anger namnet på alternativet som &quot;Sökknapp&quot; när sökalternativet ![sökalternativ](assets/do-not-localize/search_icon.png) är i fokus. Användarna kan välja `Return` för att öppna sökrutan. Skärmläsaren lägger inte bara till en berättarröst för det nyckelord som skrivs i sökrutan utan lägger även till en berättarröst för de förslag som ges av [!DNL Experience Manager Assets]. Användare kan använda en kombination av piltangenter, `Return` och `Tab` för att komma åt de olika alternativen för att utlösa en sökning.

Sökfunktionen är tillgänglig med följande funktioner:

* Sidtitel, som är tillgänglig för en skärmläsare, hjälper dig att identifiera sidan som resursens söksida.
* Användare söker efter resurser inifrån sökfältet. Användarna kan öppna den antingen via tangentbordsnavigering eller med kortkommandot `/`.
* Användarna kan börja skriva söknyckelordet och sedan välja de automatiska förslagen med piltangenterna. Det markerade förslaget kan väljas med `Return`-tangenten och resurser söks efter det valda förslaget.
* Skärmläsare kan identifiera och meddela kryssrutorna för blandade tillstånd (där kryssrutorna på första nivån inte markeras och genomstrykas om du inte markerar alla kapslade prefix) i panelen Filter när sökresultaten filtreras.
* Användarfokus flyttas till sökalternativen när Omnissökrutan har stängts.

Vid filtrering av sökresultat:

* Sökresultatsidan har en informativ titel som ger en bättre förståelse för skärmläsaranvändare.
* En skärmläsare meddelar alternativen i sökfiltret som utökningsbara dragspelspaneler.
* Prognoser med alternativ för blandat läge meddelas av skärmläsare.

## Dela resurser {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

Följande funktioner förbättrar tillgängligheten när du delar resurser:

* En användare kan flytta fokus med tangentbordet i fältet Sök och lägg till e-postadress i dialogrutan för länkdelning.

* Skärmläsarna visas i dialogrutan för länkdelning när du navigerar i bläddringsläge.

   * Lägg inte till en berättarröst i tabellinformationen så fort dialogrutan har lästs in.
   * Kan navigera till alla förslag i listan.
   * Lägg till en berättarröst för de förslag som visas för fälten Lägg till e-postadress och Sök.

## Tillgänglig dokumentation {#accessible-docs}

[!DNL Experience Manager] ger tillgänglig dokumentation som kan användas av personer med funktionshinder. Följande hjälper till att göra innehåll tillgängligt för tillfället, medan Adobe fortsätter att förbättra mallen och innehållet:

* Skärmläsare kan läsa texten.
* Bilder och illustrationer har alternativ text tillgänglig.
* Tangentbordsnavigering är möjlig.
* Kontrastförhållanden hjälper till att lyfta fram vissa delar av dokumentationswebbplatsen.

## Ge feedback {#a11y-feedback}

Använd följande metoder för att ge feedback, ställa frågor och begära produktförbättringar som rör tillgänglighet:

* Fyll i formuläret på [www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html).
* Skicka e-post till oss på access@adobe.com.

>[!MORELIKETHIS]
>
>* [Versionsinformation om förbättringar som gjorts i varje release](/help/release-notes/release-notes-cloud/release-notes-current.md).
>* [[!DNL Adobe Experience Manager] hjälpmedelsvägledning](/help/onboarding/accessibility/web-accessibility.md).
>* [Överensstämmelserapporter (ACR) och VPAT-listor för Adobe-lösningar](https://www.adobe.com/accessibility/compliance.html).

