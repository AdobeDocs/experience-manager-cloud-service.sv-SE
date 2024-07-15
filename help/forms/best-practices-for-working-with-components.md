---
title: Bästa praxis och viktiga punkter att komma ihåg när du arbetar med AEM adaptiva formulär.
description: Vissa bästa metoder och viktiga punkter att komma ihåg när du arbetar med adaptiva formulärkomponenter.
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---


# Bästa tillvägagångssätt vid arbete med komponenter{#best-practices-for-working-with-components}

Nedan följer några tips om hur du bäst kommer ihåg när du arbetar med adaptiva formulärkomponenter:

* Varje komponent har tillhörande egenskaper som styr dess utseende och funktion. Om du vill konfigurera egenskaperna för en komponent markerar du komponenten och väljer ![egenskaper](assets/Smock_Wrench_18_N.svg) för att öppna komponentegenskaperna i egenskapsläsaren.
* En komponent identifieras med sitt elementnamn. När du väljer ![egenskaper](assets/Smock_Wrench_18_N.svg) kan du ändra komponentens namn genom att ändra fältvärdet **[!UICONTROL Element Name]** i egenskapsläsaren. Endast bokstäver, siffror, bindestreck (-) och understreck (_) godkänns i fältet Elementnamn. Andra specialtecken tillåts inte och elementnamnet måste börja med en bokstav.

* Du kan ändra egenskapen Title för en komponent i ett adaptivt formulär i formulärredigeraren utan att öppna egenskapsgranskaren så länge titeln visas i formuläret. Så här gör du:

   1. Välj det här alternativet om du vill markera en komponent som har en **[!UICONTROL Title]**-egenskap och vars **[!UICONTROL Hide title]**-egenskap är inaktiverad.

   1. Välj ![Redigera ikon](assets/Smock_Edit_18_N.svg) om du vill göra titeln redigerbar.

   1. Ändra titeln och välj returtangenten eller markera var som helst utanför komponenten för att spara ändringarna. Markera Esc om du vill ignorera ändringarna.

* Vissa komponenter för anpassade formulär, som e-post och telefon, innehåller färdiga valideringsmönster. Du kan dock ange anpassad validering genom att uppdatera fältet **[!UICONTROL Validation Pattern]** under dragspelsfliken Mönster i komponentegenskaperna. Mer information om standardvalideringar finns i komponentbeskrivningarna i tabellen ovan.

* Anpassningsbara Forms-fält, t.ex. Numeric Box och Email, kan konfigureras så att de innehåller speciella HTML5-indatatyper. När de här fälten är i fokus på mobila enheter och surfplattor visas särskilda alfabet, siffror och tecken som används ofta för att mata in information i fälten. Det gör det lättare för användarna att ange information snabbt utan att behöva växla mellan teckenuppsättningar på knappsatsen. Om du vill tillåta specialiserade indata för en komponent aktiverar du kryssrutan **[!UICONTROL Use HTML Type Number]** i komponentegenskaperna.

* Du kan aktivera en textrutekomponent för att acceptera RTF. Om du vill aktivera RTF-text för en textruta aktiverar du kryssrutan **[!UICONTROL Allow Rich Text]** i komponentegenskaperna.

* Du kan aktivera komponenterna Textruta, E-post och Telefon för att autofylla värden för fält som namn, adress, kreditkort, telefon och e-post från informationen som lagras i webbläsarens autofyllningsinställningar. Om du vill aktivera den här funktionen väljer du **[!UICONTROL Enable Autofill]** i komponentegenskaperna och väljer en **[!UICONTROL Autofill Attribute]**. När en användare fyller i ett adaptivt formulär föreslås värdena från profilen för automatisk ifyllning i webbläsaren eller baserat på de värden som användaren tidigare fyllt i. Autofyll fungerar om autofyllningsinställningarna i användarens webbläsare är aktiverade.

* Ange värden för alternativknappar och kryssruteobjekt i formatet `{value}={text}` i komponentegenskaperna.
* Komponenten för bifogad fil tillåter som standard endast användare att bifoga en fil. Du kan dock konfigurera komponentegenskaperna så att de stöder flera bifogade filer. Om en användare dessutom bifogar flera filer med samma filnamn kan de bifogade filerna orsaka problem. Därför rekommenderar vi att du kopplar en unik identifierare till varje bifogad fil när formuläret skickas. Så här gör du:

   1. Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** på din [!DNL AEM Forms]-server.
   1. Sök efter och välj **[!UICONTROL Adaptive Forms Configuration Service]**.
   1. Aktivera **[!UICONTROL Make File Names Unique]** i dialogrutan Adaptiv Forms Configuration Service. Som standard är den inaktiverad.

* Om du vill att användare ska kunna koppla ett PDF med Safari-webbläsaren måste du se till att **application/pdf** läggs till i egenskapen Filtyper som stöds i den bifogade filkomponenten. Adaptiv Forms som skapats med tidigare [!DNL AEM Forms]-version kan innehålla **.pdf** i stället för **application/pdf** i egenskapen Filtyper som stöds.

>[!NOTE]
>
>Adaptiva formulärkomponenter har inte stöd för RTL-språk. Till exempel hebreiska.