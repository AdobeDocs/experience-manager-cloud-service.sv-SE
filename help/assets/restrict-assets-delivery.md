---
title: Begränsa leverans av resurser i Experience Manager
description: Lär dig hur du begränsar resursleveransen i  [!DNL Experience Manager].
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 0%

---

# Begränsa åtkomst till resurser i [!DNL Experience Manager] {#restrict-access-to-assets}

Med central resursstyrning i Experience Manager kan DAM-administratören eller varumärkeshanterarna hantera åtkomst till resurser. De kan begränsa åtkomsten genom att konfigurera roller för godkända resurser på redigeringssidan, särskilt på AEM as a Cloud Service författarinstans.

Användare [som söker](search-assets-api.md) eller använder [leverans-URL:er](deliver-assets-apis.md) kan få åtkomst till begränsade resurser när auktoriseringsprocessen har slutförts.

![Begränsad åtkomst till resurser](/help/assets/assets/restricted-access.png)

## Begränsad leverans med en IMS-token {#restrict-delivery-ims-token}

I Experience Manager omfattar begränsad leverans via IMS två huvudsteg:

* Redigering
* Leverans

### Redigering {#authoring}

Du kan begränsa leveransen av resurser inom [!DNL Experience Manager] baserat på roller. Så här konfigurerar du roller:

1. Gå till [!DNL Experience Manager] som DAM-administratör.
1. Välj den resurs som du vill konfigurera rollen för.
1. Navigera till **[!UICONTROL Properties]** > **[!UICONTROL Advanced]** och kontrollera att fältet **[!UICONTROL Roles]** finns på fliken [!UICONTROL Advanced Metadata].

   ![Metadata för roller](/help/assets/assets/roles_metadata.jpg)
Om fältet inte är tillgängligt lägger du till fältet med följande steg:

   1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]**.
   1. Markera metadataschemat och klicka på **[!UICONTROL Edit _(e)_]**.
   1. Lägg till ett **[!UICONTROL Multi Value Text]**-fält från avsnittet **[!UICONTROL Build Form]** till höger i avsnittet Metadata i formuläret.
   1. Klicka på det nya fältet och gör sedan följande uppdateringar på panelen **[!UICONTROL Settings]**:
      1. Ändra **[!UICONTROL Field Label]** till _Roller_.
      1. Uppdatera **[!UICONTROL Map to property]** till _./jcr:content/metadata/dam:roles_.

1. Hämta de IMS-grupper som ska läggas till i resursens rollmetadata. Så här hämtar du IMS-grupperna:
   1. Logga in på https://adminconsole.adobe.com/.
   1. Gå till din respektive organisation och navigera till **[!UICONTROL User Groups]**.
   1. Markera **[!UICONTROL User Group]** som du vill lägga till och extrahera **[!UICONTROL orgID]** och **[!UICONTROL userGroupID]** från URL:en eller använd ditt Org ID, till exempel `{orgID}@AdobeOrg:{usergroupID}`.

1. Lägg till grupp-ID i fältet **[!UICONTROL Roles]** i Resursegenskaper. <br>
Grupp-ID:n som definieras i fältet **[!UICONTROL Roles]** är de enda användare som har åtkomst till resursen. Du kan också lägga till ID för IMS-klient och ID för IMS-profil i fältet **[!UICONTROL Roles]**. Exempel: `{orgId}@AdobeOrg:{profileId}`.

   >[!NOTE]
   >
   >I den nya vyn Assets kan du bara ge åtkomst till mappnivån, och exklusivt till grupper snarare än till enskilda användare. Läs mer om att [hantera behörigheter i Experience Manager Assets](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

   >[!VIDEO](https://video.tv.adobe.com/v/3427429)

#### Begränsa leverans av resurser med På- och Av-datum och tid {#restrict-delivery-assets-date-time}

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



### Leverans av begränsade tillgångar {#delivery-restricted-assets}

Leveransen av begränsade tillgångar baseras på lyckad auktorisering för åtkomst av resurser. Behörigheten baseras antingen på en IMS-token om begäran skickas från en AEM författarinstans eller resursväljare, eller på en särskild cookie om du har anpassade identitetsleverantörer som är konfigurerade för din Publish- eller Preview-instans.

#### Leverans för AEM eller resursväljare {#delivery-aem-author-asset-selector}

För att möjliggöra leverans av begränsade resurser om begäran skickas från AEM författarinstans eller resursväljare är en giltig IMS-token nödvändig. Följ de här stegen:

1. [Generera en åtkomsttoken](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token).
   * Logga in på Dev Console för din AEM as a Cloud Service-miljö.

   * Navigera till **[!UICONTROL Environment]** > **[!UICONTROL Integrations]** > **[!UICONTROL Local Token]** > **[!UICONTROL Get Local Development Token]** > **[!UICONTROL Copy accessToken value]**. Läs mer om [hur du får åtkomst till token och relaterade aspekter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)

1. Integrera den erhållna åtkomsttoken i **[!UICONTROL Authorization]**-huvudet och kontrollera att dess värde är prefix med **[!UICONTROL Bearer]**.

1. Validera åtkomsttoken genom att initiera en begäran. Det bör ge 404 fel om det inte finns någon IMS-åtkomsttoken, eller om den angivna åtkomsttoken saknar samma principer eller grupper som de som lagts till i resursens metadata.

#### Leverans för anpassade identitetsleverantörer på Publish {#delivery-custom-identity-provider}

Om en anpassad identitetsleverantör har konfigurerats på din Publish- eller Preview-instans kan du ange vilken grupp som måste ha tillgång till skyddade resurser i attributet `groupMembership` under konfigurationsprocessen. När du loggar in på en anpassad identitetsleverantör via [SAML-integrering](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0) läses attributet `groupMembership` och används för att skapa en cookie, som skickas i alla autentiseringsbegäranden, på samma sätt som en IMS-token vid en begäran från AEM eller resursväljare.

När en skyddad resurs är tillgänglig på en sida och en begäran görs till leverans-URL:en för att återge resursen, kontrollerar AEM rollerna som finns i cookien eller IMS-token och matchar den mot `dam:roles property` som används vid redigeringen av resursen. Om det finns en matchning visas resursen.

>[!NOTE]
>
> I [supportanmälan för att aktivera Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md#how-to-enable-the-dynamic-media-with-openapi-capabilities) anger du begränsad leverans i användningsexemplet. Adobe Engineering kommer att hjälpa till med nödvändiga klargöranden och/eller upprätta processer för begränsad leverans.
