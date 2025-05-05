---
title: Begränsa leverans av resurser med Dynamic Media med OpenAPI-funktioner
description: Lär dig hur du begränsar materialdistributionen med OpenAPI-funktioner.
role: User
exl-id: 3fa0b75d-c8f5-4913-8be3-816b7fb73353
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 0%

---

# Begränsa leverans av resurser med Dynamic Media med OpenAPI-funktioner {#restrict-access-to-assets}

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

>[!AVAILABILITY]
>
>Dynamic Media med funktionsguiden OpenAPI finns nu i PDF-format. Ladda ned hela guiden och använd Adobe Acrobat AI Assistant för att besvara dina frågor.
>
>[!BADGE Dynamiska media med OpenAPI-funktioner - guide för PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

Med central resursstyrning i Experience Manager kan DAM-administratören eller varumärkeshanterarna hantera åtkomst till resurser som är tillgängliga via Dynamic Media med OpenAPI-funktioner. De kan begränsa leveransen av godkända resurser (ned till en enskild resurs) till utvalda [Adobe Identity Management System-användare (IMS) eller grupper](https://helpx.adobe.com/in/enterprise/using/users.html#user-mgt-strategy) genom att konfigurera vissa metadata för resurserna i AEM as a Cloud Service-författartjänsten.

När en mediefil har begränsats via Dynamic Media med OpenAPI:er får endast de (Adobe IMS-ombord) användare som har behörighet att använda mediefilen åtkomst. Användaren måste utnyttja funktionerna [Sök](search-assets-api.md) och [Leverans](deliver-assets-apis.md) i Dynamic Media med OpenAPI för att få åtkomst till resursen.

![Begränsad åtkomst till resurser](/help/assets/assets/restricted-access.png)

I Experience Manager Assets innebär begränsad leverans via IMS två huvudsteg:

* Redigering
* Leverans

## Redigering {#authoring}

### Begränsad leverans med en IMS Bearer-token {#restrict-delivery-ims-token}

Du kan begränsa leveransen av resurser inom [!DNL Experience Manager] baserat på IMS användar- och gruppidentifierare.

>[!NOTE]
>
>Den här funktionen är för närvarande inte självbetjäning. Om du vill begränsa resursleveransen för IMS [Users](https://helpx.adobe.com/in/enterprise/using/manage-directory-users.html) och [Groups](https://helpx.adobe.com/in/enterprise/using/user-groups.html) kan du kontakta ditt Enterprise Support-team för att få hjälp med hur du hämtar den information som krävs för att begränsa åtkomst från [Adobe Admin Console](https://adminconsole.adobe.com/)-portalen och hur du konfigurerar åtkomst i AEM as a Cloud Service författartjänst.

### Begränsa leverans av resurser med På- och Av-datum och tid {#restrict-delivery-assets-date-time}

DAM-författare kan också begränsa leveransen av resurser genom att definiera en På- eller Av-tid för aktivering som är tillgänglig i tillgångsegenskaperna.

Om du definierar en På-tid för aktivering av en resurs, genereras en leverans-URL för resursen vid den angivna tidpunkten. Resursen förblir inaktiv före den angivna tiden. På samma sätt, om du definierar en&quot;Av&quot;-tid för en resurs, inaktiveras resursen vid den angivna tidpunkten och leverans-URL:en för resursen slutar visa resursen.

Utför följande steg för att ställa in På- och Av-tid för resursen:

1. Markera resursen och klicka på **[!UICONTROL Properties]**.

1. I avsnittet **[!UICONTROL Scheduled (de) activation]** på fliken **[!UICONTROL Basic]** definierar du På-tid eller Av-tid baserat på dina krav.

På samma sätt kan du i Assets-vyn markera resursen och klicka på **[!UICONTROL Details]** för att visa resursegenskaper och definiera På-tid och Av-tid.

Fältet är tillgängligt i standardformuläret för metadata. Om resursen inte är baserad på standardmetadataschemat och fälten På tid och Fråntid inte är tillgängliga i resursegenskaperna utför du följande steg i administratörsvyn:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]**.
1. Markera metadataschemat och klicka på **[!UICONTROL Edit]**.
1. Lägg till ett **[!UICONTROL Date]**-fält från avsnittet **[!UICONTROL Build Form]** till höger i avsnittet Metadata i formuläret.
1. Klicka på det nya fältet och gör sedan följande uppdateringar på panelen **[!UICONTROL Settings]**:
   1. Ändra **[!UICONTROL Field Label]** till **I tid** eller **Från tid**.
   1. Uppdatera **[!UICONTROL Map to property]** till _./jcr:content/onTime_ för fältet **On Time** och _./jcr:content/offTime_ för fältet **Fråntid**.
1. Klicka på **[!UICONTROL Save]**.

Om resursen inte är baserad på standardmetadataschemat och fälten På tid och Av tid inte är tillgängliga i resursegenskaperna i Assets-vyn utför du följande steg:

1. Klicka på **[!UICONTROL Metadata Forms]** i avsnittet **[!UICONTROL Settings]**.
1. Markera metadataformuläret och klicka på **[!UICONTROL Edit]**.
1. Lägg till ett **[!UICONTROL Date]**-fält från avsnittet **[!UICONTROL Components]** i den vänstra rutan i formuläret.
1. Klicka på det nyligen tillagda fältet och ändra **[!UICONTROL Label]** till **I tid** eller **Från tid**.
1. Uppdatera **[!UICONTROL Metadata property]** till _./jcr:content/onTime_ för fältet **On Time** och _./jcr:content/offTime_ för fältet **Fråntid**.
1. Klicka på **[!UICONTROL Save]**.



## Leverans av begränsade tillgångar {#delivery-restricted-assets}

Leveransen av begränsade tillgångar baseras på lyckad auktorisering för åtkomst av resurser. Auktoriseringen sker antingen via [IMS Bearer-token](https://developer.adobe.com/developer-console/docs/guides/authentication/UserAuthentication/IMS/) (program för begäranden som initierats från [AEM Asset Selector](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector)) eller en säker cookie (om du har anpassade identitetsleverantörer konfigurerade för AEM Publish/Preview-tjänster och har konfigurerat skapande och inkludering av cookies på sidorna).

### Leverans för förfrågningar från AEM-författare eller resursväljare {#delivery-aem-author-asset-selector}

För att tillåta leverans av begränsade resurser om begäran skickas från AEM författartjänst eller AEM Resursväljare är en giltig IMS Bearer-token nödvändig.\
På både AEM Cloud-tjänstens författartjänster och resursväljare genereras och används IMS Bearer-token automatiskt för begäranden efter en lyckad inloggning.

>[!NOTE]
>
>Om du vill ha mer information om hur du aktiverar IMS-autentisering för AEM Asset Selector-baserade integreringar kan du kontakta Enterprise Support

1. För icke-resursväljarbaserade upplevelser stöder AEM as a Cloud Service och Dynamic Media med OpenAPI-funktioner för närvarande API-integreringar på serversidan och kan generera IMS Bearer-tokens.
   * Följ anvisningarna [här](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#the-server-to-server-flow) för att utföra service-to-server-API-integreringar som kan hämta IMS Bearer-tokens via [AEM as a Cloud Service Developer Console](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#crxde-lite-and-developer-console)
   * Under en begränsad tid kan lokal utvecklaråtkomst (inte avsedd för produktionsbruk), kortlivade IMS Bearer-token för den användare som autentiserats på [AEM as a Cloud Service Developer Console](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#crxde-lite-and-developer-console) genereras genom att följa instruktionerna [här](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis#developer-flow)

1. När du gör [API-begäranden för sökning](search-assets-api.md) och [leverans](deliver-assets-apis.md) lägger du till den erhållna IMS Bearer-token i HTTP-begärans **[!UICONTROL Authorization]**-huvud (se till att dess värde har prefixet **[!UICONTROL Bearer]**).

1. Om du vill validera åtkomstbegränsningen initierar du en leverans-API-begäran med och utan rubriken **[!UICONTROL Authorization]**.
   * Svaret genererar en `404`-felstatuskod om det inte finns någon IMS Bearer-token, eller om den angivna IMS Bearer-token inte tillhör användaren som beviljades åtkomst till resursen (antingen direkt eller via gruppmedlemskap).
   * Svaret ger en `200`-kod för lyckad status med resursens binära innehåll om IMS Bearer-token är en av de användare eller grupper som har beviljats åtkomst till resursen.

### Leverans för anpassade identitetsleverantörer i Publiceringstjänst {#delivery-custom-identity-provider}

AEM Sites, AEM Assets och Dynamic Media med OpenAPI-licenser kan användas tillsammans, vilket gör det möjligt att konfigurera begränsad leverans av resurser på webbplatser som använder AEM Publish eller Preview. Det säkra leveransflödet utnyttjar cookies i webbläsaren för att fastställa användarens åtkomst och att ha en anpassad domän för leveransnivå som är underdomän till publiceringsdomänen är en förutsättning för att det här användningsexemplet ska kunna implementeras. Om AEM Sites publicerings- och förhandsgranskningstjänster är konfigurerade att använda en [anpassad identitetsleverantör (IdP)](https://experienceleague.adobe.com/sv/docs/experience-manager-learn/cloud-service/authentication/saml-2-0), måste en ny cookie som kallas `delivery-token` kapslande användares gruppmedlemskap anges för autentisering av publiceringsdomänpostanvändarens autentisering. Leveransnivån extraherar auktoriseringsmaterialet från säker-cookie och validerar åtkomsten. Logga en [företagssupportbiljett](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities) om du vill ha mer information.
