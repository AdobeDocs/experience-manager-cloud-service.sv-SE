---
title: Använda regeluppsättningar för att omforma URL:er
description: Du kan distribuera regeluppsättningar i Dynamic Media för att omvandla URL:er. Regeluppsättningar är instruktioner skrivna i ett skriptspråk (t.ex. JavaScript) som utvärderar XML-data och utför vissa åtgärder om dessa data uppfyller vissa villkor.
translation-type: tm+mt
source-git-commit: 3a8f63c46e5604a9ce46250ac2d02cc95b473a7c
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 3%

---


# Använda regeluppsättningar för att omforma URL:er {#using-rulesets-to-transform-urls}

Du kan distribuera regeluppsättningar i Dynamic Media för att omvandla URL:er. Regeluppsättningar är instruktioner skrivna i ett skriptspråk (t.ex. JavaScript) som utvärderar XML-data och utför vissa åtgärder om dessa data uppfyller vissa villkor. Varje regel består av minst ett villkor och minst en åtgärd. En regel utvärderar XML-data mot villkoren, och om ett villkor är uppfyllt utförs rätt åtgärd. Exempel på regeluppsättningar är följande:

* Lägga till ett MIME-typsuffix. Många tjänster och webbplatser kräver bildsuffix, som att lägga till `.jpg` till en URL.
* Skapa en mappsökväg till URL:en för sökmotoroptimering.

   Se [Hur Adobe Dynamic Media Classic stöder SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Lägga till metadata i URL:en för sökmotoroptimering.

   Se [Hur Adobe Dynamic Media Classic stöder SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Ställa in innehållets disposition för att utlösa en hämtning.
* Förenkla bildhanteringen genom att ange URL:er för personalisering. Omvandla till exempel `rgb{XX,YY,ZZ}` till RTF-klar `\redXX\greenYY\blueZZ`

* Begär att vissa tecken ska kodas, till exempel `$`, `{` och `}`, och vissa tecken ska avkodas mot ImageServer. Facebook fungerar till exempel inte så bra med URL:er som innehåller specialtecken.

   Se [Ta bort specialtecken från URL:er](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

I Dynamic Media-sammanhang kan webbplatser som använder ett XML-baserat system för att hantera resursinformation överföra XML-filer till Dynamic Media. Du kan ange en av dessa filer som förbearbetningsregeluppsättningsfil för Dynamic Media-resurser. Den här filen omstrukturerar URL-protokollets standardformat så att det uppfyller affärslogiken i system som integreras med Dynamic Media. Du anger en XML-fil som ska fungera som sökväg till definitionsfilen för regeluppsättningen.

>[!CAUTION]
>
>Var försiktig när du använder linjaler. kan de förhindra att Dynamic Media-innehåll visas på din webbplats.

Det finns exempellinjaler som kan hjälpa dig att skapa en egen linjaluppsättning.
Se [Referens för regeluppsättning](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html).

Precis som när du skapar alla regeluppsättningar måste du se till att XML-filen är giltig innan du överför den med ett XML-valideringsprogram som xmlvalid.
Se även [Troubleshooting rule sets](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

Kontrollera också först att du testar regeluppsättningen i en staging-miljö som inte påverkar produktionsmiljön.
Produktionsmiljöer och staging-miljöer kräver normalt olika inloggningar.

Se [Adobe Dynamic Media Classic-datorprogrammet för inloggningsinformation](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

<!-- OBSOLETE CONTENT * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

Se även [Använda &quot;asset&quot; i stället för &quot;is&quot;-bilden i en regeluppsättning](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

**Så här distribuerar du XML-regeluppsättningar:**

1. Logga in på ditt Dynamic Media Classic-konto:

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   Dina autentiseringsuppgifter och din inloggning tillhandahölls av Adobe vid tidpunkten för etableringen. Om du inte har den här informationen kontaktar du teknisk support.

1. Överför regeluppsättningsfilen genom att göra följande:

   * Klicka på **[!UICONTROL Upload]** i fältet Global navigering.
   * På sidan **[!UICONTROL Upload]**, nära det övre vänstra hörnet, klickar du på **[!UICONTROL Browse]**.
   * Bläddra till regeluppsättningsfilen (XML) i dialogrutan **[!UICONTROL Open]**.
   * Markera filen och klicka sedan på **[!UICONTROL Open]**.
   * Till höger på sidan **[!UICONTROL Upload]** väljer du en målmapp för regeluppsättningsfilen.
   * Kontrollera att **[!UICONTROL Publish After Uploading]** är markerat nära sidans nederkant.
   * Klicka på **[!UICONTROL Submit Upload]** längst ned till höger på sidan.
   * Klicka på **[!UICONTROL Jobs]** i fältet Global navigering för att kontrollera överföringsjobbets status. När kolumnen **[!UICONTROL Status]** på sidan **[!UICONTROL Job]** säger Överför klar fortsätter du till nästa steg.

1. Klicka på **[!UICONTROL Setup > Application Setup > Publish Setup > Image Server]** i navigeringsfältet uppe på sidan.
1. På sidan **[!UICONTROL Image Server Publish]**, under gruppen **[!UICONTROL Catalog Management]**, letar du upp **[!UICONTROL Rule Set Definition File Path]** och klickar sedan på **[!UICONTROL Select]**.
1. På sidan **[!UICONTROL Select Rule Set Definition File (XML)]** bläddrar du till regeluppsättningsfilen och klickar sedan på **[!UICONTROL Select]** i den nedre högra hörnet av sidan.
1. Klicka på **[!UICONTROL Close]** längst ned till höger på sidan Inställningar.
1. Kör ett Image Server-publiceringsjobb.

   Regeluppsättningsvillkoren tillämpas på begäranden till Dynamic Media Image-servrar.

   Om du gör ändringar i regeluppsättningsfilen tillämpas ändringarna omedelbart när du överför och publicerar den uppdaterade regeluppsättningsfilen igen.

