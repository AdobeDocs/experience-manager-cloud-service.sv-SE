---
title: Vanliga frågor och svar från Content Hub
description: Få svar på några av de vanligaste frågorna och svaren för Content Hub.
badgeSaas: label="AEM Assets" type="Positive" tooltip="Gäller AEM Assets)."
exl-id: 74b5c308-c1d3-4787-9f1f-f64cf09d298a
source-git-commit: 59f97fc6ded4274c27400f56b50b4a3329cc471a
workflow-type: tm+mt
source-wordcount: '1620'
ht-degree: 0%

---

# Vanliga frågor om Content Hub {#content-hub-frequently-asked-questions}

![Vanlig fråga från Content Hub](assets/content-hub-faqs.png)

## Vad är AEM Assets Content Hub? {#what-is-content-hub}

AEM Assets Content Hub ingår i Adobe Experience Manager Assets as a Cloud Service.

Med Content Hub kan större team enkelt hitta relevanta, godkända resurser via en intuitiv portal och snabbt anpassa dem efter sina behov.  Dessutom har Content Hub en funktion för intag som gör att dessa användare enkelt kan vara självbetjänade när de överför resurser till DAM. Detta är direkt anpassat till behovet av att organisationer skapar innehåll snabbare samtidigt som varumärkets enhetlighet och efterlevnad upprätthålls med lämpliga skyddsåtgärder.

<!--

## Why cannot I enable Content Hub on my Cloud Manager program/environment? {#cannot-enable-content-hub}

Content Hub is at this point is only available on AEM Cloud Manager Production programs, which include an Assets license (Assets Cloud Service, Assets Ultimate, Assets Prime). When you click [Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) to enable it, it is deployed and associated with the author production environment of AEM in that program. See [Deploy Content Hub](/help/assets/deploy-content-hub.md) for details and prerequisites.

-->

## Jag har aktiverat AEM Assets Content Hub i mitt produktionsprogram/i min produktionsmiljö, kan jag inaktivera det? {#can-i-disable-content-hub}

Om du aktiverar AEM Assets Content Hub i ett produktionsprogram blir det en del av produktionsinfrastrukturen. AEM Cloud Manager tillåter inte borttagning eller inaktivering av produktionsinfrastruktur för att minimera risken för att fel uppstår i produktionen.

Om du inte vill ge dina användare Content Hub när den väl har distribuerats ska du inte tilldela några användare till Content Hub produktprofil i Admin Console. Mer information finns i [Distribuera Content Hub](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile).

## Hur kan jag utvärdera AEM Assets Content Hub i min organisation? {#how-can-i-evaluate-content-hub}

AEM Assets Content Hub är en funktion som Adobe tillhandahåller och underhåller och inte har någon anpassad kod som skulle kräva typisk validering via dev/stage/production. Dessutom styrs åtkomsten till funktionen för användare av administratören, så du kan utvärdera den utan att visa den för alla användare.

Du kan utvärdera Content Hub utan att påverka användare/produktionsinnehåll som hanteras i AEM as a Cloud Service Assets. Ett utvärderingsförfarande kan se ut så här:

* [Aktivera Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) i produktionsmiljön (Cloud Manager-program)
* [Lägg till en AEM Administrator-användare](/help/assets/deploy-content-hub.md#onboard-content-hub-administrator) från författaren till Content Hub produktprofil.
* AEM Administrator [konfigurerar Content Hub](/help/assets/configure-content-hub-ui-options.md)
* AEM Administrator eller en AEM-användare på AEM-produktionsförfattaren [godkänner ett antal resurser för Content Hub](/help/assets/approve-assets-content-hub.md). Om du inte vill ändra något produktionsinnehåll i DAM kan du skapa en separat utvärderingsmapp i AEM-författarinstansen och överföra/tagga eller kopiera resurser från DAM till den.
* Admin Console-administratören lägger till [några utvalda användare](/help/assets/deploy-content-hub.md#onboard-content-hub-users) i Content Hub produktprofil, så att de kan starta utvärderingen.
* När utvärderingen är klar kan AEM-användare i författarinstansen ta bort godkännandet från testmaterialet, godkänna produktionsmaterialet för Content Hub och sedan Admin Console-administratören lägga till alla användare som behöver åtkomst till Content Hub och godkänt innehåll. Grattis, din Content Hub finns nu.

Det finns ett program för tidig åtkomst till Content Hub i sandlådeprogram och deras redigeringsmiljöer. Mer information finns i [Introduktion till sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md). Om du vill veta mer om programmet för tidig åtkomst kan du kontakta ditt Adobe-kontoteam.

## Varför visas inga mediefiler när jag har loggat in på AEM Assets Content Hub? {#no-assets-in-content-hub}

De mediefiler som markerats som godkända i Assets as a Cloud Service är automatiskt tillgängliga i Content Hub. Om du inte kan se något material efter att du har loggat in på Content Hub godkänner du resurser med hjälp av AEM as a Cloud Service redigeringsmiljö och gör dem tillgängliga i Content Hub. Mer information finns i [Godkänn resurser för Content Hub](/help/assets/approve-assets-content-hub.md).

## Varför ser jag inte mina resurser som jag antingen överför direkt med AEM Assets Content Hub eller importerar från Dropbox- eller OneDrive-konton med Content Hub? {#no-assets-uploaded-from-content-hub}

Hur resurser som överförts med AEM Assets Content Hub visas beror på om du har aktiverat alternativet [Automatiskt godkännande](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub) som är tillgängligt i användargränssnittet för konfigurationen:

* Om alternativet **Automatiskt godkännande** är aktiverat blir de resurser som du överför med Content Hub automatiskt tillgängliga.

* Om växeln **Automatiskt godkännande** är inaktiverad visas inte de resurser som du överför med Content Hub automatiskt. Resurserna är tillgängliga i mappen `hydrated-assets` i din Assets as a Cloud Service-miljö. Navigera till mappen och [massredigera](/help/assets/approve-assets-content-hub.md) statusen för dessa resurser till `Approved` för de resurser som ska visas i Content Hub.

## Hur hittar man snabbt material som överförts med AEM Assets Content Hub i AEM as a Cloud Service-miljö? {#find-uploaded-assets-on-aem-cloud}

Du kan snabbt hitta resurser som överförts med AEM Assets Content Hub i AEM as a Cloud Service-miljö genom att:

1. Navigerar till mappen `hydrated-assets`.

1. Klicka på **[!UICONTROL Filters]** och ange **[!UICONTROL No Status]** i fältet **[!UICONTROL Asset Status]**.

1. Sorterar resurser med fältet **[!UICONTROL Modified Date]**.

## Varför ser jag inte alternativet Redigera med Adobe Express på mitt resurskort för att kunna mixa om resurser och skapa nya varianter med AEM Assets Content Hub? {#edit-using-express-not-available}

Om du vill visa alternativet **Redigera med Adobe Express** på resurskortet i AEM Assets Content Hub måste användaren ha Adobe Express Enterprise- eller Teams-behörighet (se [abonnemang](https://www.adobe.com/express/pricing)) förutom behörighet för [Content Hub-användare med behörighet att mixa om resurser till nya varianter](#onboard-content-hub-users-add-assets).

Det finns några konfigurationer av hur användare tilldelas till [!DNL Content Hub] &amp; [!DNL Adobe Express]:

1. Organisationen har [Assets Ultimate](/help/assets/assets-ultimate-overview.md) eller [Assets Prime](/help/assets/assets-prime.md) licens och användaren tilldelas en av Experience Manager-profilerna i Admin Console som innehåller Adobe Express-berättigande (medarbetare eller Power-användare). Integreringen fungerar utan någon ytterligare konfiguration.

1. [!DNL Adobe Express] distribueras i samma [!DNL Adobe Admin Console] som [!DNL Experience Manager Assets] med [!DNL Content Hub]. Integreringen fungerar utan någon ytterligare konfiguration.

1. [!DNL Adobe Express] distribueras i en annan [!DNL Adobe Admin Console] än [!DNL Experience Manager Assets] med [!DNL Content Hub]. I det här fallet kan administratören av [!DNL Assets] konfigurera integreringen (se [&#x200B; dokumentation](/help/assets/connect-assets-with-creative-cloud.md)) för att integreringen ska fungera.

   >[!NOTE]
   >
   >Användaren som tilldelats Express- och Assets-produktprofiler i två Admin Consoles måste ha samma e-postadress och använda ett **Enterprise- eller School** -företagskonto, inte ett **Personal** -konto. Den idealiska konfigurationen är att ha båda Admin Consoles inställda som **Federated ID** med en förtroenderelation konfigurerad mellan dem, så att användaren får en sömlös inloggning. Vissa Express-planer (till exempel Express Teams) stöder inte Federated ID/enkel inloggning.

Utöver rätt produktbehörigheter kräver Adobe Express-integrering i Content Hub att den tilldelade användaren har minst [!UICONTROL Can Edit] behörigheter i Assets-redigeringsmiljön som driver Content Hub, i minst mapphierarkin **[!UICONTROL # /content/dam/hydrated-assets/]** , där Content Hub-användare kan spara innehåll som de skapat med Express. Se [Behörighetshantering](/help/security/touch-ui-principal-view.md) i administrationsvyn (Touch UI) eller en förenklad [behörighetshantering i Assets-vyn](https://experienceleague.adobe.com/sv/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

## Kan jag konfigurera AEM Assets Content Hub så att min organisations varumärkesriktlinjer visas som en länk på startsidan? {#content-hub-setup-brand-guidelines}

Du kan lägga till anpassade länkar som separata flikar förutom standardflikarna Alla Assets, Samlingar och Insights på AEM Assets Content Hub hemsida. Mer information om hur du konfigurerar det finns i [Anpassade länkar](/help/assets/configure-content-hub-ui-options.md#configure-custom-links-content-hub).

## Finns det någon plan för att migrera befintliga Brand Portal-kunder till AEM Assets Content Hub? {#migration-brand-portal}

Adobe tillhandahåller migreringsstöd från Brand Portal till AEM Assets Content Hub som du kan använda genom att skapa en Adobe supportanmälan.

## Varför kan jag inte se produktinställningar/konfigurationsalternativ i AEM Assets Content Hub? {#ui-configuration-option-missing}

Du måste vara en [Content Hub-administratör](/help/assets/configure-content-hub-ui-options.md) för att få åtkomst till [konfigurationsanvändargränssnittet](/help/assets/deploy-content-hub.md##onboard-content-hub-administrator) i AEM Assets Content Hub. Om du har tilldelats produktprofilen AEM Administrators på produktionsförfattarinstansen i Adobe Admin Console och du fortfarande inte kan se konfigurationsalternativet, kontrollerar du att produktprofilen AEM Administrators inte byter namn. Mer information finns i [AEM as a Cloud Service Team- och produktprofiler](/help/onboarding/aem-cs-team-product-profiles.md).

## Hur tillgodoser AEM Assets Content Hub Brand Portal begränsningar? {#content-hub-brand-portal-comparison}


Tabellen nedan visar de viktigaste skillnaderna mellan AEM Assets Content Hub och Brand Portal:

| Område | Funktion | Content Hub | Brand Portal |
|---|---|----|----|
| Konfigurera distributionsupplevelsen | Konfigurera metadata för filter, resursinformation och lägg till resurssida | ✓ | - |
|  | Konfigurera externa länkar från portalen | ✓ | - |
|  | Konfigurera banderollmeddelanden | ✓ | ✓ |
|  | Konfigurera banderollbild för varumärkning | ✓ | ✓ |
|  | Konfigurera primära och sekundära färger för användargränssnittet enligt varumärkeskraven | ✓ | - |
| Dela resurser från DAM | Dela ursprungliga godkända resurser från DAM | ✓ | ✓ |
|  | Godkända resursändringar synkroniserade automatiskt | ✓ | - |
| Söka och filtrera | Dynamiska filter (alternativen visas dynamiskt baserat på de resurser som visas) | ✓ | - |
|  | Sökhistorik | ✓ | - |
| Överföring av tillgångar | Lokal enhet | ✓ | ✓ |
|  | Lägg till konfigurerbara metadata när du överför resurser | ✓ | - |
| Hämta och återge | Hämta ursprunglig resurs | ✓ | ✓ |
|  | Dela och hämta statiska återgivningar från DAM | ✓ | ✓ |
|  | Hämta dynamiska renderingar (förinställningar och smarta beskärningar) | ✓ | ✓ |
|  | Möjlighet att begränsa visning och hämtning av utgångna resurser | ✓ | - |
| Länkdelning och samlingar | Länkresurs för inloggade användare | ✓ | ✓ |
|  | Offentliga samlingar | ✓ | ✓ |
|  | Sök i samlingar | ✓ | - |
|  | Anonym länkdelning | ✓ | ✓ |
|  | Privata samlingar | ✓ | ✓ |
| Behörigheter | ACL-baserade behörigheter | - | ✓ |
|  | Attributbaserad åtkomstkontroll | ✓ | - |
| Express-integrering | Redigera Content Hub Assets i Adobe Express och spara i DAM | ✓ | - |
| Kontrollpaneler och rapporter | Instrumentpanel för insikter | ✓ | - |
| Utbyggbarhet för användargränssnitt | Anpassade tilläggspunkter på sidan med tillgångsinformation | Begränsad tillgänglighet | - |
| Nyheter som kommer snart | Favoritsamlingar efter användare | ✓ | - |
|  | Fastnålade samlingar av administratör | ✓ | - |
|  | Semantisk sökning | ✓ | - |
|  | Lokaliserad sökning och visning av metadata | ✓ | - |

## Hur väljer jag en databas för att visa resurser endast för den valda miljön i AEM Assets Content Hub? {#select-repository-multiple-environments}

När du har konfigurerat AEM Assets Content Hub för produktion och andra lägre miljöer för samma program kan du välja databas och visa resurserna för den valda miljön. Utför följande steg:

1. Klicka på användarikonen i den högra rutan.

1. Välj **[!UICONTROL Product Settings]** i avsnittet **[!UICONTROL Select Repository]**.

1. Välj databasen i listrutan **[!UICONTROL Repository]** och klicka på **[!UICONTROL OK]** för att bekräfta.

   Content Hub visar nu resurser för den valda miljön.

## Hur visar AEM Assets Content Hub miniatyrbildsförhandsvisning för filtypen ZIP? {#thumbnail-preview-zip-file}

Om du vill ha en miniatyrbildsförhandsvisning för filtyper som ZIP i AEM Assets Content Hub kan du lägga till en återgivning med namnet `cq5dam.preview.jpg` eller `cq5dam.preview.png` i roten av sökvägen där ZIP-filen är tillgänglig i AEM as a Cloud Service-redigeringsmiljön.

Bilden som du lägger till som återgivning:

* Kan vara i JPG-, JPEG- eller PNG-format.

* Måste vara mindre än 50 MB

När det är tillgängligt visas bilden som förhandsvisningsminiatyrbild för ZIP-filen i Content Hub.


