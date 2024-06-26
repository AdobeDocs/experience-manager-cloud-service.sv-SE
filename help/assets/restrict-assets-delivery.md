---
title: Begränsa leverans av resurser i Experience Manager
description: Lär dig hur du begränsar leverans av resurser i [!DNL Experience Manager].
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 0%

---

# Begränsa åtkomst till resurser i [!DNL Experience Manager] {#restrict-access-to-assets}

Med central resursstyrning i Experience Manager kan DAM-administratören eller varumärkeshanterarna hantera åtkomst till resurser. De kan begränsa åtkomsten genom att konfigurera roller för godkända resurser på redigeringssidan, särskilt på AEM as a Cloud Service författarinstans.

Användare [söka](search-assets-api.md) eller använder [leverans-URL:er](deliver-assets-apis.md) kan få åtkomst till begränsade resurser när auktoriseringsprocessen har slutförts.

![Begränsad åtkomst till resurser](/help/assets/assets/restricted-access.png)

## Begränsad leverans med en IMS-token {#restrict-delivery-ims-token}

I Experience Manager omfattar begränsad leverans via IMS två huvudsteg:

* Redigering
* Leverans

### Redigering {#authoring}

Du kan begränsa leveransen av resurser i [!DNL Experience Manager] baserat på roller. Så här konfigurerar du roller:

1. Gå till [!DNL Experience Manager] som DAM-administratör.
1. Välj den resurs som du vill konfigurera rollen för.
1. Navigera till **[!UICONTROL Properties]** > **[!UICONTROL Advanced]** och se till att **[!UICONTROL Roles]** fältet finns i [!UICONTROL Advanced Metadata] -fliken.

   ![Metadata för roller](/help/assets/assets/roles_metadata.jpg)
Om fältet inte är tillgängligt lägger du till fältet med följande steg:

   1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]**.
   1. Välj metadatamatchemat och klicka på **[!UICONTROL Edit _(e)_]**.
   1. Lägg till en **[!UICONTROL Multi Value Text]** fält från **[!UICONTROL Build Form]** -avsnittet på höger sida till avsnittet Metadata i formuläret.
   1. Klicka på det nya fältet och gör sedan följande uppdateringar i  **[!UICONTROL Settings]** panel:
      1. Ändra **[!UICONTROL Field Label]** till _Roller_.
      1. Uppdatera **[!UICONTROL Map to property]** till _./jcr:content/metadata/dam:roles_.

1. Hämta de IMS-grupper som ska läggas till i resursens rollmetadata. Så här hämtar du IMS-grupperna:
   1. Logga in på https://adminconsole.adobe.com/.
   1. Gå till respektive organisation och navigera till **[!UICONTROL User Groups]**.
   1. Välj **[!UICONTROL User Group]** du behöver lägga till och extrahera **[!UICONTROL orgID]** och **[!UICONTROL userGroupID]** från URL:en eller använd ditt Org ID, till exempel `{orgID}@AdobeOrg:{usergroupID}`.

1. Lägg till grupp-ID i **[!UICONTROL Roles]** fält för resursegenskaper. <br>
Grupp-ID:n som definieras i **[!UICONTROL Roles]** -fältet är de enda användare som har åtkomst till resursen. Du kan också lägga till ID för IMS-klient och ID för IMS-profil i **[!UICONTROL Roles]** fält. Till exempel: `{orgId}@AdobeOrg:{profileId}`.

   >[!NOTE]
   >
   >I den nya vyn Assets kan du bara ge åtkomst till mappnivån, och exklusivt till grupper snarare än till enskilda användare. Läs mer om [hantera behörigheter i Experience Manager Assets](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

   >[!VIDEO](https://video.tv.adobe.com/v/3427429)

#### Begränsa leverans av resurser med På- och Av-datum och tid {#restrict-delivery-assets-date-time}

DAM-författare kan också begränsa leveransen av resurser genom att definiera en På- eller Av-tid för aktivering som är tillgänglig i tillgångsegenskaperna.

Om du definierar en På-tid för aktivering av en resurs, genereras en leverans-URL för resursen vid den angivna tidpunkten. Resursen förblir inaktiv före den angivna tiden. På samma sätt, om du definierar en&quot;Av&quot;-tid för en resurs, inaktiveras resursen vid den angivna tidpunkten och leverans-URL:en för resursen slutar visa resursen.

Utför följande steg för att ställa in På- och Av-tid för resursen:

1. Markera resursen och klicka på **[!UICONTROL Properties]**.

1. I **[!UICONTROL Scheduled (de) activation]** i **[!UICONTROL Basic]** definierar du På-tid eller Av-tid baserat på dina behov.

På samma sätt kan du i Assets-vyn markera resursen och klicka på **[!UICONTROL Details]** för att visa resursegenskaper och definiera På-tid och Av-tid.

Fältet är tillgängligt i standardformuläret för metadata. Om resursen inte är baserad på standardmetadataschemat och fälten På tid och Fråntid inte är tillgängliga i resursegenskaperna utför du följande steg i administratörsvyn:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]**.
1. Välj metadatamatchemat och klicka på **[!UICONTROL Edit]**.
1. Lägg till en **[!UICONTROL Date]** fält från **[!UICONTROL Build Form]** -avsnittet på höger sida till avsnittet Metadata i formuläret.
1. Klicka på det nya fältet och gör sedan följande uppdateringar i  **[!UICONTROL Settings]** panel:
   1. Ändra **[!UICONTROL Field Label]** till **I tid** eller **Fråntid**.
   1. Uppdatera **[!UICONTROL Map to property]** till _./jcr:content/onTime_ for **I tid** fält och _./jcr:content/offTime_ for **Fråntid** fält.
1. Klicka på **[!UICONTROL Save]**.

Om resursen inte är baserad på standardmetadataschemat och fälten På tid och Av tid inte är tillgängliga i resursegenskaperna i Assets-vyn utför du följande steg:

1. Klicka **[!UICONTROL Metadata Forms]** i **[!UICONTROL Settings]** -avsnitt.
1. Markera metadataformuläret och klicka på **[!UICONTROL Edit]**.
1. Lägg till en **[!UICONTROL Date]** fält från **[!UICONTROL Components]** till vänster i formuläret.
1. Klicka på det nya fältet och ändra **[!UICONTROL Label]** till **I tid** eller **Fråntid**.
1. Uppdatera **[!UICONTROL Metadata property]** till _./jcr:content/onTime_ for **I tid** fält och _./jcr:content/offTime_ for **Fråntid** fält.
1. Klicka på **[!UICONTROL Save]**.



### Leverans av begränsade tillgångar {#delivery-restricted-assets}

Leveransen av begränsade tillgångar baseras på lyckad auktorisering för åtkomst av resurser. Behörigheten baseras antingen på en IMS-token om begäran skickas från en AEM författarinstans eller resursväljare, eller på en särskild cookie om du har anpassade identitetsleverantörer som är konfigurerade för din Publish- eller Preview-instans.

#### Leverans för AEM eller resursväljare {#delivery-aem-author-asset-selector}

För att möjliggöra leverans av begränsade resurser om begäran skickas från AEM författarinstans eller resursväljare är en giltig IMS-token nödvändig. Följ de här stegen:

1. [Generera en åtkomsttoken](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token).
   * Logga in på Dev Console för din AEM as a Cloud Service-miljö.

   * Navigera till **[!UICONTROL Environment]** > **[!UICONTROL Integrations]** > **[!UICONTROL Local Token]** > **[!UICONTROL Get Local Development Token]** > **[!UICONTROL Copy accessToken value]**. Läs mer om [hur du får åtkomst till token och relaterade aspekter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)

1. Integrera den erhållna åtkomsttoken med **[!UICONTROL Authorization]** header, se till att dess värde är prefix med **[!UICONTROL Bearer]**.

1. Validera åtkomsttoken genom att initiera en begäran. Det bör ge 404 fel om det inte finns någon IMS-åtkomsttoken, eller om den angivna åtkomsttoken saknar samma principer eller grupper som de som lagts till i resursens metadata.

#### Leverans för anpassade identitetsleverantörer på Publish {#delivery-custom-identity-provider}

Om en anpassad identitetsleverantör har konfigurerats på din Publish- eller Preview-instans kan du ange vilken grupp som måste ha tillgång till skyddade resurser i `groupMembership` under konfigurationsprocessen. När du loggar in på en anpassad identitetsleverantör via [SAML-integration](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0), `groupMembership` -attributet läses och används för att skapa en cookie som skickas i alla autentiseringsbegäranden, som liknar en IMS-token om en begäran AEM författaren eller resursväljaren skickas.

När en skyddad resurs är tillgänglig på en sida och en begäran görs till leverans-URL:en för att återge resursen, kontrollerar AEM rollerna som finns i cookien eller IMS-token och matchar den mot `dam:roles property` som används vid redigeringen av resursen. Om det finns en matchning visas resursen.

>[!NOTE]
>
> I [supportanmälan för att aktivera Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities), anger begränsad leverans i användningsexemplet. Adobe Engineering kommer att hjälpa till med nödvändiga klargöranden och/eller upprätta processer för begränsad leverans.
