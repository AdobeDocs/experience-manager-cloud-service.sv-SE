---
title: Vanliga frågor och svar från Content Hub
description: Få svar på några av de vanligaste frågorna och svaren för Content Hub.
exl-id: 74b5c308-c1d3-4787-9f1f-f64cf09d298a
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 0%

---

# Vanliga frågor om Content Hub {#content-hub-frequently-asked-questions}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime och Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets-integrering med Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI-utökningsbarhet</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Aktivera Dynamic Media Prime och Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Sök efter bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Metadata - bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamiska media med OpenAPI-funktioner</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets-dokumentation för utvecklare</b></a>
        </td>
    </tr>
</table>

![Vanlig fråga från Content Hub](assets/content-hub-faqs.png)

>[!AVAILABILITY]
>
>Content Hub Guide finns nu i PDF-format. Ladda ned hela guiden och använd Adobe Acrobat AI Assistant för att besvara dina frågor.
>
>[!BADGE Content Hub Guide PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

## Vad är Content Hub? {#what-is-content-hub}

Content Hub ingår i Adobe Experience Manager Assets as a Cloud Service.

Med Content Hub kan större team enkelt hitta relevanta, godkända resurser via en intuitiv portal och snabbt anpassa dem efter sina behov.  Dessutom har Content Hub en funktion för intag som gör att dessa användare enkelt kan vara självbetjänade när de överför resurser till DAM. Detta är direkt anpassat till behovet av att organisationer skapar innehåll snabbare samtidigt som varumärkets enhetlighet och efterlevnad upprätthålls med lämpliga skyddsåtgärder.

## Varför kan jag inte aktivera Content Hub i min Cloud Manager-miljö? {#cannot-enable-content-hub}

Content Hub finns endast i AEM Cloud Manager Production-program, som innehåller en Assets-licens (Assets Cloud Service, Assets Ultimate, Assets Prime). När du klickar på [Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) för att aktivera den distribueras den och kopplas till AEM redigeringsmiljö i det programmet. Mer information och krav finns i [Distribuera Content Hub](/help/assets/deploy-content-hub.md).

## Jag har aktiverat Content Hub i mitt produktionsprogram/i min produktionsmiljö, kan jag inaktivera det? {#can-i-disable-content-hub}

Om du aktiverar Content Hub i ett produktionsprogram blir det en del av produktionsinfrastrukturen. AEM Cloud Manager tillåter inte borttagning eller inaktivering av produktionsinfrastruktur för att minimera risken för att fel uppstår i produktionen.

Om du inte vill ge dina användare Content Hub när den väl har distribuerats ska du inte tilldela några användare till Content Hub produktprofil i Admin Console. Mer information finns i [Distribuera Content Hub](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile).

## Hur kan jag utvärdera Content Hub i min organisation, eftersom det bara är tillgängligt för produktionsprogram/produktionsmiljöer? {#how-can-i-evaluate-content-hub}

Content Hub är en funktion som Adobe tillhandahåller och underhåller, och den har ingen anpassad kod som skulle kräva typisk validering via dev/stage/production. Dessutom styrs åtkomsten till funktionen för användare av administratören, så du kan utvärdera den utan att visa den för alla användare.

Du kan utvärdera Content Hub utan att påverka användare/produktionsinnehåll som hanteras i AEM as a Cloud Service Assets. Ett utvärderingsförfarande kan se ut så här:

* [Aktivera Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) i produktionsmiljön (Cloud Manager-program)
* [Lägg till en AEM Administrator-användare](/help/assets/deploy-content-hub.md#onboard-content-hub-administrator) från författaren till Content Hub produktprofil.
* AEM Administrator [konfigurerar Content Hub](/help/assets/configure-content-hub-ui-options.md)
* AEM Administrator eller en AEM-användare på AEM-produktionsförfattaren [godkänner ett antal resurser för Content Hub](/help/assets/approve-assets-content-hub.md). Om du inte vill ändra något produktionsinnehåll i DAM kan du skapa en separat utvärderingsmapp i AEM-författarinstansen och överföra/tagga eller kopiera resurser från DAM till den.
* Admin Console-administratören lägger till [några utvalda användare](/help/assets/deploy-content-hub.md#onboard-content-hub-users) i Content Hub produktprofil, så att de kan starta utvärderingen.
* När utvärderingen är klar kan AEM-användare i författarinstansen ta bort godkännandet från testmaterialet, godkänna produktionsmaterialet för Content Hub och sedan Admin Console-administratören lägga till alla användare som behöver åtkomst till Content Hub och godkänt innehåll. Grattis, din Content Hub finns nu.

Det finns ett program för tidig åtkomst till Content Hub i sandlådeprogram och deras redigeringsmiljöer. Mer information finns i [Introduktion till sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md). Om du vill veta mer om programmet för tidig åtkomst kan du kontakta ditt Adobe-kontoteam.

Content Hub är ännu inte tillgängligt för icke-produktionsmiljöer (stage &amp; dev). Förväntad tillgänglighet för scen-/utvecklingsmiljöer för Assets Ultimate är mars 2025.

## Varför visas inga resurser när jag har loggat in på Content Hub? {#no-assets-in-content-hub}

De mediefiler som markerats som godkända i Assets as a Cloud Service är automatiskt tillgängliga i Content Hub. Om du inte kan se något material efter att du har loggat in på Content Hub godkänner du resurser med hjälp av AEM as a Cloud Service redigeringsmiljö och gör dem tillgängliga i Content Hub. Mer information finns i [Godkänn resurser för Content Hub](/help/assets/approve-assets-content-hub.md).

## Varför ser jag inte mina resurser som jag antingen överför direkt med Content Hub eller importerar från Dropbox- eller OneDrive-konton med Content Hub? {#no-assets-uploaded-from-content-hub}

Visningen av resurser som överförts med Content Hub beror på om du har aktiverat alternativet [Automatiskt godkännande](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub) som är tillgängligt i användargränssnittet för konfigurationen:

* Om alternativet **Automatiskt godkännande** är aktiverat blir de resurser som du överför med Content Hub automatiskt tillgängliga.

* Om växeln **Automatiskt godkännande** är inaktiverad visas inte de resurser som du överför med Content Hub automatiskt. Resurserna är tillgängliga i mappen `hydrated-assets` i din Assets as a Cloud Service-miljö. Navigera till mappen och [massredigera](/help/assets/approve-assets-content-hub.md) statusen för dessa resurser till `Approved` för de resurser som ska visas i Content Hub.

## Hur hittar man snabbt material som överförts med Content Hub i AEM as a Cloud Service-miljö? {#find-uploaded-assets-on-aem-cloud}

Du kan snabbt hitta resurser som överförts med Content Hub i AEM as a Cloud Service-miljö genom att:

1. Navigerar till mappen `hydrated-assets`.

1. Klicka på **[!UICONTROL Filters]** och ange **[!UICONTROL No Status]** i fältet **[!UICONTROL Asset Status]**.

1. Sorterar resurser med fältet **[!UICONTROL Modified Date]**.

## Varför visar jag inte redigeringsalternativet med Adobe Express på mitt resurskort för att kunna mixa om resurser och skapa nya varianter? {#edit-using-express-not-available}

Om du vill visa redigeringen med alternativet Adobe Express på resurskortet måste du ha Adobe Express-berättiganden förutom behörighet för [Content Hub-användare med behörighet att mixa om resurser till nya varianter](#onboard-content-hub-users-add-assets). Adobe Express måste driftsättas i samma organisation i Adobe Admin Console där Adobe Experience Manager är driftsatt.

## Kan jag konfigurera Content Hub så att min organisations varumärkesriktlinjer visas som en länk på startsidan? {#content-hub-setup-brand-guidelines}

Du kan lägga till anpassade länkar som separata flikar förutom standardflikarna Alla Assets, Samlingar och Insights på Content Hub hemsida. Mer information om hur du konfigurerar det finns i [Anpassade länkar](/help/assets/configure-content-hub-ui-options.md#configure-custom-links-content-hub).

## Finns det någon plan för att migrera befintliga Brand Portal-kunder till Content Hub? {#migration-brand-portal}

Adobe tillhandahåller migreringsstöd från Brand Portal till Content Hub som du kan använda genom att skapa en Adobe supportanmälan.

## Varför kan jag inte se produktinställningar/konfigurationsalternativ i Content Hub? {#ui-configuration-option-missing}

Du måste vara [Content Hub-administratör](/help/assets/deploy-content-hub.md##onboard-content-hub-administrator) för att få åtkomst till [konfigurationsanvändargränssnittet](/help/assets/configure-content-hub-ui-options.md). Om du har tilldelats produktprofilen AEM Administrators på produktionsförfattarinstansen i Adobe Admin Console och du fortfarande inte kan se konfigurationsalternativet, kontrollerar du att produktprofilen AEM Administrators inte byter namn. Mer information finns i [AEM as a Cloud Service Team- och produktprofiler](/help/onboarding/aem-cs-team-product-profiles.md).
