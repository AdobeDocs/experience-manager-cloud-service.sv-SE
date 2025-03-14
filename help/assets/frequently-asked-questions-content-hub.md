---
title: Vanliga frågor och svar från Content Hub
description: Få svar på några av de vanligaste frågorna och svaren för Content Hub.
exl-id: 74b5c308-c1d3-4787-9f1f-f64cf09d298a
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 0%

---

# Vanliga frågor om Content Hub {#content-hub-frequently-asked-questions}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Vanlig fråga från Content Hub](assets/content-hub-faqs.png)

>[!AVAILABILITY]
>
>Content Hub Guide finns nu i PDF-format. Ladda ned hela guiden och använd Adobe Acrobat AI Assistant för att besvara dina frågor.
>
>[!BADGE Content Hub Guide PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

## Vad är Content Hub? {#what-is-content-hub}

Content Hub är en del av Adobe Experience Manager Assets as a Cloud Service.

Med Content Hub kan större team enkelt hitta relevanta, godkända resurser via en intuitiv portal och snabbt anpassa dem efter sina behov.  Dessutom har Content Hub en funktion för intag som gör att dessa användare enkelt kan vara självbetjänade när de överför resurser till DAM. Detta är direkt anpassat till behovet av att organisationer skapar innehåll snabbare samtidigt som varumärkets enhetlighet och efterlevnad upprätthålls med lämpliga skyddsåtgärder.

## Varför kan jag inte aktivera Content Hub i min Cloud Manager-miljö? {#cannot-enable-content-hub}

Content Hub finns endast i AEM Cloud Manager Production-program, som innehåller en Assets-licens (Assets Cloud Service, Assets Ultimate, Assets Prime). När du klickar på [Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) för att aktivera det distribueras det och kopplas till författarproduktionsmiljön för AEM i det programmet. Mer information och krav finns i [Distribuera Content Hub](/help/assets/deploy-content-hub.md).

## Jag har aktiverat Content Hub i mitt produktionsprogram/i min produktionsmiljö, kan jag inaktivera det? {#can-i-disable-content-hub}

Om du aktiverar Content Hub i ett produktionsprogram blir det en del av produktionsinfrastrukturen. AEM Cloud Manager tillåter inte borttagning eller inaktivering av produktionsinfrastruktur för att minimera risken för att fel uppstår i produktionen.

Om du inte vill ge dina användare Content Hub när den väl har distribuerats ska du inte tilldela några användare till Content Hub produktprofil i Admin Console. Mer information finns i [Distribuera Content Hub](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile).

## Hur kan jag utvärdera Content Hub i min organisation, eftersom det bara är tillgängligt för produktionsprogram/produktionsmiljöer? {#how-can-i-evaluate-content-hub}

Content Hub är en funktion som Adobe tillhandahåller och underhåller och den har ingen anpassad kod som skulle kräva typisk validering via dev/stage/production. Dessutom styrs åtkomsten till funktionen för användare av administratören, så du kan utvärdera den utan att visa den för alla användare.

Du kan utvärdera Content Hub utan att påverka användare/produktionsinnehåll som hanteras i AEM as a Cloud Service Assets. Ett utvärderingsförfarande kan se ut så här:

* [Aktivera Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) i produktionsmiljön (Cloud Manager-program)
* [Lägg till en AEM administratörsanvändare](/help/assets/deploy-content-hub.md#onboard-content-hub-administrator) från författaren till Content Hub produktprofil.
* AEM [konfigurerar Content Hub](/help/assets/configure-content-hub-ui-options.md)
* AEM Administratör eller en AEM användare på AEM produktionsförfattare [godkänner ett antal resurser för Content Hub](/help/assets/approve-assets-content-hub.md). Om du inte vill ändra något produktionsinnehåll i DAM kan du skapa en separat utvärderingsmapp i den AEM författarinstansen och överföra/tagga eller kopiera resurser från DAM till den.
* Admin Console-administratören lägger till [några utvalda användare](/help/assets/deploy-content-hub.md#onboard-content-hub-users) i Content Hub produktprofil, så att de kan starta utvärderingen.
* När utvärderingen är klar kan AEM användare i författarinstansen ta bort godkännande från testresurser, godkänna produktionsresurser för Content Hub och sedan Admin Console-administratören lägga till alla användare som behöver tillgång till Content Hub och godkänt innehåll. Grattis, din Content Hub finns nu.

Det finns ett program för tidig åtkomst till Content Hub i sandlådeprogram och deras redigeringsmiljöer. Mer information finns i [Introduktion till sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md). Om du vill veta mer om programmet för tidig åtkomst kan du kontakta ditt kontoteam på Adobe.

Content Hub är ännu inte tillgängligt för icke-produktionsmiljöer (stage &amp; dev). Förväntad tillgänglighet för scen-/utvecklingsmiljöer för Assets Ultimate är mars 2025.

## Varför visas inga resurser när jag har loggat in på Content Hub? {#no-assets-in-content-hub}

De mediefiler som markerats som godkända i Assets as a Cloud Service är automatiskt tillgängliga i Content Hub. Om du inte kan se något material efter att du har loggat in på Content Hub godkänner du resurser med hjälp av AEM as a Cloud Service redigeringsmiljö och gör dem tillgängliga i Content Hub. Mer information finns i [Godkänn resurser för Content Hub](/help/assets/approve-assets-content-hub.md).

## Varför ser jag inte mina resurser som jag antingen överför direkt med Content Hub eller importerar från Dropbox eller OneDrive med Content Hub? {#no-assets-uploaded-from-content-hub}

Visningen av resurser som överförts med Content Hub beror på om du har aktiverat alternativet [Automatiskt godkännande](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub) som är tillgängligt i användargränssnittet för konfigurationen:

* Om alternativet **Automatiskt godkännande** är aktiverat blir de resurser som du överför med Content Hub automatiskt tillgängliga.

* Om växeln **Automatiskt godkännande** är inaktiverad visas inte de resurser som du överför med Content Hub automatiskt. Resurserna är tillgängliga i mappen `hydrated-assets` i din Assets as a Cloud Service-miljö. Navigera till mappen och [massredigera](/help/assets/approve-assets-content-hub.md) statusen för dessa resurser till `Approved` för de resurser som ska visas i Content Hub.

## Hur hittar man snabbt material som överförts med Content Hub i AEM as a Cloud Service-miljö? {#find-uploaded-assets-on-aem-cloud}

Du kan snabbt hitta resurser som överförts med Content Hub i AEM as a Cloud Service-miljö genom att:

1. Navigerar till mappen `hydrated-assets`.

1. Klicka på **[!UICONTROL Filters]** och ange **[!UICONTROL No Status]** i fältet **[!UICONTROL Asset Status]**.

1. Sorterar resurser med fältet **[!UICONTROL Modified Date]**.

## Varför visar jag inte alternativet Redigera med Adobe Express på mitt resurskort för att kunna mixa om resurser och skapa nya varianter? {#edit-using-express-not-available}

Om du vill visa redigeringsalternativet med Adobe Express på resurskortet måste du ha Adobe Express-rättigheter förutom behörighet för [Content Hub-användare med behörighet att mixa om resurser till nya varianter](#onboard-content-hub-users-add-assets). Adobe Express måste distribueras i samma organisation i Adobe Admin Console där Adobe Experience Manager är installerat.

## Kan jag konfigurera Content Hub så att min organisations varumärkesriktlinjer visas som en länk på startsidan? {#content-hub-setup-brand-guidelines}

Du kan lägga till anpassade länkar som separata flikar förutom standardflikarna Alla Assets, Samlingar och Insights på Content Hub hemsida. Mer information om hur du konfigurerar det finns i [Anpassade länkar](/help/assets/configure-content-hub-ui-options.md#configure-custom-links-content-hub).

## Finns det någon plan för att migrera befintliga Brand Portal-kunder till Content Hub? {#migration-brand-portal}

Adobe tillhandahåller migreringsstöd från Brand Portal till Content Hub som du kan använda genom att skapa en supportbiljett för Adobe.

## Varför kan jag inte se produktinställningar/konfigurationsalternativ i Content Hub? {#ui-configuration-option-missing}

Du måste vara [Content Hub-administratör](/help/assets/deploy-content-hub.md##onboard-content-hub-administrator) för att få åtkomst till [konfigurationsanvändargränssnittet](/help/assets/configure-content-hub-ui-options.md). Om du har tilldelats produktprofilen AEM administratörer på produktionsförfattarinstansen i Adobe Admin Console och du fortfarande inte kan se konfigurationsalternativet kontrollerar du att produktprofilen AEM administratörer inte byter namn. Mer information finns i [AEM as a Cloud Service Team- och produktprofiler](/help/onboarding/aem-cs-team-product-profiles.md).
