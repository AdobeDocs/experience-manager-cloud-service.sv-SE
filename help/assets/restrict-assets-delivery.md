---
title: Begränsa leverans av resurser i Experience Manager
description: Lär dig hur du begränsar leverans av resurser i [!DNL Experience Manager].
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# Begränsa åtkomst till resurser i [!DNL Experience Manager] {#restrict-access-to-assets}

Med central resursstyrning i Experience Manager kan DAM-administratören eller varumärkeshanterarna hantera åtkomst till resurser. De kan begränsa åtkomsten genom att konfigurera roller för godkända resurser på redigeringssidan, särskilt på den AEM as a Cloud Service författarinstansen.

Användare [söka](search-assets-api.md) eller använder [leverans-URL:er](deliver-assets-apis.md) kan få åtkomst till begränsade resurser när auktoriseringsprocessen har slutförts.

![Begränsad åtkomst till resurser](/help/assets/assets/restricted-access.png)

## Begränsad leverans med en IMS-token {#restrict-delivery-ims-token}

I Experience Manager omfattar begränsad leverans via IMS två huvudsteg:

* Redigering
* Leverans

### Redigering {#authoring}

För att begränsa leveransen av resurser måste roller konfigureras för resurserna i [!DNL Experience Manager] eller [!DNL Experience Manager Assets]. Konfigurera roller i [!DNL Experience Manager]gör du så här:

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
   >I den nya resursvyn kan du bara ge åtkomst till mappnivån och exklusivt till grupper i stället för till enskilda användare. Läs mer om [hantera behörigheter i Experience Manager Assets](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

   >[!VIDEO](https://video.tv.adobe.com/v/3427429)

### Leverans av begränsade tillgångar {#delivery-restricted-assets}

Leveransen av begränsade tillgångar baseras på lyckad auktorisering för åtkomst av resurser. Auktoriseringen baseras antingen på en IMS-token om begäran skickas från en AEM författarinstans eller resursväljare, eller på en särskild cookie om du har anpassade identitetsleverantörer som är konfigurerade för din Publish- eller Preview-instans.

#### Leverans för AEM författare eller resursväljare {#delivery-aem-author-asset-selector}

För att möjliggöra leverans av begränsade resurser om begäran skickas från AEM författarinstans eller resursväljare är en giltig IMS-token nödvändig. Följ de här stegen:

1. [Generera en åtkomsttoken](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token).
   * Logga in på Dev Console för den AEM as a Cloud Service miljön.

   * Navigera till **[!UICONTROL Environment]** > **[!UICONTROL Integrations]** > **[!UICONTROL Local Token]** > **[!UICONTROL Get Local Development Token]** > **[!UICONTROL Copy accessToken value]**. Läs mer om [hur du får åtkomst till token och relaterade aspekter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token)

1. Integrera den erhållna åtkomsttoken med **[!UICONTROL Authorization]** header, se till att dess värde är prefix med **[!UICONTROL Bearer]**.

1. Validera åtkomsttoken genom att initiera en begäran. Det bör ge 404 fel om det inte finns någon IMS-åtkomsttoken, eller om den angivna åtkomsttoken saknar samma principer eller grupper som de som lagts till i resursens metadata.

#### Leverans för anpassade identitetsleverantörer {#delivery-custom-identity-provider}

Om en anpassad identitetsleverantör har konfigurerats för din Publish- eller Preview-instans kan du ange vilken grupp som måste ha tillgång till skyddade resurser i `groupMembership` under konfigurationsprocessen. När du loggar in på en anpassad identitetsleverantör via [SAML-integration](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0), `groupMembership` -attributet läses och används för att skapa en cookie som skickas i alla autentiseringsbegäranden, som liknar en IMS-token om en begäran AEM författaren eller resursväljaren skickas.

När en skyddad resurs är tillgänglig på en sida och en begäran görs till leverans-URL:en för att återge resursen, kontrollerar AEM rollerna som finns i cookien eller IMS-token och matchar den mot `dam:roles property` som används vid redigeringen av resursen. Om det finns en matchning visas resursen.
