---
title: Bästa tillvägagångssätt vid arbete med komponenter
seo-title: Best practices for working with components
description: Vissa bästa metoder och viktiga punkter att komma ihåg när du arbetar med adaptiva formulärkomponenter
seo-description: Some best practices and key points to remember when working with Adaptive Form components
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---


# Bästa tillvägagångssätt vid arbete med komponenter{#best-practices-for-working-with-components}

Nedan följer några tips om hur du bäst kommer ihåg när du arbetar med adaptiva formulärkomponenter:

* Varje komponent har tillhörande egenskaper som styr dess utseende och funktion. Konfigurera egenskaperna för en komponent genom att trycka på komponenten och trycka på ![egenskaper](assets/Smock_Wrench_18_N.svg) om du vill öppna komponentegenskaperna i egenskapsgranskaren.
* En komponent identifieras med sitt elementnamn. När du trycker ![egenskaper](assets/Smock_Wrench_18_N.svg)kan du ändra komponentens namn genom att ändra **[!UICONTROL Element Name]** fältvärdet i egenskapswebbläsaren. Endast bokstäver, siffror, bindestreck (-) och understreck (_) godkänns i fältet Elementnamn. Andra specialtecken tillåts inte och elementnamnet måste börja med en bokstav.

* Du kan ändra egenskapen Title för en komponent i ett adaptivt formulär i formulärredigeraren utan att öppna egenskapsgranskaren så länge titeln visas i formuläret. Så här gör du:

   1. Tryck för att markera en komponent som har en **[!UICONTROL Title]** egenskap och vars **[!UICONTROL Hide title]** egenskapen är inaktiverad.

   1. Tryck ![Ikonen Redigera](assets/Smock_Edit_18_N.svg) för att göra titeln redigerbar.

   1. Ändra titeln och tryck på Retur-tangenten eller var som helst utanför komponenten för att spara ändringarna. Tryck på Esc för att ignorera ändringarna.

* Vissa komponenter för anpassade formulär, som e-post och telefon, innehåller färdiga valideringsmönster. Du kan dock ange anpassad validering genom att uppdatera **[!UICONTROL Validation Pattern]** under mönsterdragspelet i komponentegenskaperna. Mer information om standardvalideringar finns i komponentbeskrivningarna i tabellen ovan.

* Anpassningsbara Forms-fält, t.ex. Numeric Box och Email, kan konfigureras så att de innehåller speciella HTML5-indatatyper. När de här fälten är i fokus på mobila enheter och surfplattor visas särskilda alfabet, siffror och tecken som är vanliga för inmatningsinformation i fälten. Det gör det lättare för användarna att ange information snabbt utan att behöva växla mellan teckenuppsättningar på knappsatsen. Om du vill tillåta specialindata för en komponent aktiverar du **[!UICONTROL Use HTML Type Number]** i komponentegenskaperna.

* Du kan aktivera en textrutekomponent för att acceptera RTF. Aktivera alternativet **[!UICONTROL Allow Rich Text]** i komponentegenskaperna.

* Du kan aktivera komponenterna Textruta, E-post och Telefon för att autofylla värden för fält som namn, adress, kreditkort, telefon och e-post från informationen som lagras i webbläsarens autofyllningsinställningar. Om du vill aktivera den här funktionen väljer du **[!UICONTROL Enable Autofill]** i komponentegenskaperna och markera en **[!UICONTROL Autofill Attribute]**. När en användare fyller i ett adaptivt formulär föreslås värdena från profilen för automatisk ifyllning i webbläsaren eller baserat på de värden som användaren tidigare fyllt i. Observera att Autofyll fungerar om autofyllningsinställningarna i användarens webbläsare är aktiverade.

* Ange värden för alternativknappar och kryssruteobjekt i `{value}={text}` format i komponentegenskaper.
* Komponenten för bifogad fil tillåter som standard att användaren bara kan bifoga en fil. Du kan dock konfigurera komponentegenskaperna så att de stöder flera bifogade filer. Om en användare dessutom bifogar flera filer med samma filnamn kan de bifogade filerna orsaka problem. Därför rekommenderar vi att du kopplar en unik identifierare till varje bifogad fil när formuläret skickas. Så här gör du:

   1. På [!DNL AEM Forms] server, navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
   1. Söka och trycka **[!UICONTROL Adaptive Forms Configuration Service]**.
   1. Aktivera **[!UICONTROL Make File Names Unique]**. Som standard är den inaktiverad.

* Om du vill att användare ska kunna bifoga ett PDF i webbläsaren Safari måste du se till att **application/pdf** läggs till i egenskapen Filtyper som stöds i den bifogade filkomponenten. Adaptiv Forms skapad med tidigare [!DNL AEM Forms] versionen kan innehålla **.pdf** i stället för **application/pdf** i egenskapen Filtyper som stöds.

>[!NOTE]
>
>Adaptiva formulärkomponenter har inte stöd för RTL-språk. Till exempel hebreiska.