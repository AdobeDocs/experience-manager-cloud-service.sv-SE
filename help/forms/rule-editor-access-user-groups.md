---
title: Hur får man åtkomst till regelredigeraren för anpassade formulär för att välja användargrupper?
description: Det finns olika typer av användare med olika kunskaper som fungerar med Adaptive Forms. Lär dig hur du begränsar regelredigeringsåtkomsten för användare baserat på deras roll eller funktion.
feature: Adaptive Forms
role: User
level: Beginner, Intermediate
source-git-commit: d33c7278d16a8cce76c87b606ca09aa91f1c3563
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Bevilja regelredigeraråtkomst för valda användargrupper {#grant-rule-editor-access-to-select-user-groups}

## Översikt {#overview}

Det finns olika typer av användare med olika kunskaper som fungerar med Adaptive Forms. Expertanvändare kan ha rätt kunskaper för att arbeta med skript och komplexa regler, men det kan finnas grundläggande användare som bara behöver arbeta med layout och grundläggande egenskaper i Adaptive Forms.

[!DNL Experience Manager Forms] Med kan du begränsa regelredigerarens åtkomst till användare baserat på deras roll eller funktion. I inställningarna för Adaptive Forms Configuration Service kan du ange [användargrupper](forms-groups-privileges-tasks.md) som kan visa och komma åt regelredigeraren.

## Ange användargrupper som kan komma åt regelredigeraren {#specify-user-groups-that-can-access-rule-editor}

1. Logga in på [!DNL Experience Manager Forms] som administratör.
1. Klicka på i författarinstansen ![Adobe Experience Manager](assets/adobeexperiencemanager.png)Adobe Experience Manager > Verktyg ![hammare](assets/hammer-icon.svg) > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**. Webbkonsolen öppnas i ett nytt fönster.

   ![1-2](assets/1-2.png)

1. I [!UICONTROL Web Console] Fönster, leta upp och klicka **[!UICONTROL Adaptive Form Configuration Service]**. **[!UICONTROL Adaptive Form Configuration Service]** visas. Ändra inga värden och klicka **[!UICONTROL Save]**.

   Skapar en fil `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` i CRX-databasen.

1. Logga in på CRXDE som administratör. Öppna fil `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` för redigering.
1. Använd följande egenskap för att ange namnet på en grupp som kan komma åt regelredigeraren (till exempel RuleEditorsUserGroup) och klicka på **[!UICONTROL Save All]**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   Om du vill aktivera åtkomst för flera grupper anger du en lista med kommaseparerade värden:

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![Skapa användare](assets/create_user_new.png)

   När nu en användare som inte är en del av den angivna användargruppen (här    `RuleEditorsUserGroup`) trycker på ett fält och ikonen Redigera regel ( ![edit-rules1](assets/edit-rules1.png)) är inte tillgängligt i verktygsfältet Komponenter:

   ![componentsstoolbarwithre](assets/componentstoolbarwithre.png)

   Komponentverktygsfältet så som det visas för en användare med åtkomst till regelredigeraren:

   ![componentsstoolbarwithout](assets/componentstoolbarwithoutre.png)

   Komponentverktygsfältet så synligt som det är för en användare utan regelredigeringsåtkomst

   Instruktioner om hur du lägger till användare i grupper finns i [Användaradministration och -säkerhet](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html).

