---
title: Använda regeluppsättningar för att omforma URL:er
description: Du kan distribuera regeluppsättningar i Dynamic Media för att omvandla URL:er. Regeluppsättningar är instruktioner skrivna i ett skriptspråk (t.ex. JavaScript) som utvärderar XML-data och utför vissa åtgärder om dessa data uppfyller vissa villkor.
translation-type: tm+mt
source-git-commit: 1713cddf713afc24103a841a7dbae923941f6322
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 3%

---


# Använda regeluppsättningar för att omforma URL:er {#using-rulesets-to-transform-urls}

Du kan distribuera regeluppsättningar i Dynamic Media för att omvandla URL:er. Regeluppsättningar är instruktioner skrivna i ett skriptspråk (t.ex. JavaScript) som utvärderar XML-data och utför vissa åtgärder om dessa data uppfyller vissa villkor. Varje regel består av minst ett villkor och minst en åtgärd. En regel utvärderar XML-data mot villkoren, och om ett villkor är uppfyllt utförs rätt åtgärd. Exempel på regeluppsättningar är följande:

* Lägga till ett MIME-typsuffix. Många tjänster och webbplatser kräver bildsuffix, t.ex. tillägg `.jpg` till en URL.
* Skapa en mappsökväg till URL:en för sökmotoroptimering.

   Se [hur Adobe Scene7 Publishing System stöder SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Lägga till metadata i URL:en för sökmotoroptimering.

   Se [hur Adobe Scene7 Publishing System stöder SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Ställa in innehållets disposition för att utlösa en hämtning.
* Förenkla bildhanteringen genom att ange URL:er för personalisering. Omvandla `rgb{XX,YY,ZZ}` till RTF-klart `\redXX\greenYY\blueZZ`

* Begär att vissa tecken ska kodas, t.ex. `$`, `{`och `}`vissa tecken som ska avkodas mot ImageServer. Facebook fungerar till exempel inte så bra med URL:er som innehåller specialtecken.

   Se [Ta bort specialtecken från URL-adresser](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

När det gäller Dynamic Media kan webbplatser som använder ett XML-baserat system för att hantera resursinformation överföra XML-filer till Dynamic Media. Du kan ange en av dessa filer som förbearbetningsregeluppsättningsfil för att hantera Dynamic Media-resurser. Den här filen omstrukturerar standardformatet för URL-protokoll så att det uppfyller affärslogiken i system som integreras med Dynamic Media. Du anger en XML-fil som ska fungera som sökväg till definitionsfilen för regeluppsättningen.

>[!CAUTION]
>
>Var försiktig när du använder linjaler. kan de förhindra att dynamiskt medieinnehåll visas på webbplatsen.

Det finns exempellinjaler som kan hjälpa dig att skapa en egen linjaluppsättning.
Se Referens för [regeluppsättning](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html).

Precis som när du skapar alla regeluppsättningar måste du se till att XML-filen är giltig innan du överför den med ett XML-valideringsprogram som xmlvalid.
Se även [Felsökningsregeluppsättningar](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

Kontrollera också först att du testar regeluppsättningen i en staging-miljö som inte påverkar produktionsmiljön.
Produktionsmiljöer och staging-miljöer kräver normalt olika inloggningar.

* **Inloggningssida för NA-testmiljön** : [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **Inloggningssida för mellanlagringsmiljön** i EMEA: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **Inloggningssida för JAPAC-mellanlagringsmiljö** : [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/)

Se även [Använda&quot;resurs&quot; i stället för&quot;is&quot;-bild i en regeluppsättning](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

**Så här distribuerar du XML-regeluppsättningar:**

1. Logga in på ditt konto för Dynamic Media Classic:

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   Dina autentiseringsuppgifter och din inloggning tillhandahölls av Adobe vid tidpunkten för etableringen. Om du inte har den här informationen kontaktar du teknisk support.

1. Överför regeluppsättningsfilen genom att göra följande:

   * Klicka på i fältet Global navigering **[!UICONTROL Upload]**.
   * Klicka på på **[!UICONTROL Upload]** sidan i det övre vänstra hörnet **[!UICONTROL Browse]**.
   * Bläddra till regeluppsättningsfilen (XML) i dialogrutan **[!UICONTROL Open]** .
   * Markera filen och klicka sedan på **[!UICONTROL Open]**.
   * On the right side of the **[!UICONTROL Upload]** page, select a destination folder for the rule set file.
   * Kontrollera att **[!UICONTROL Publish After Uploading]** är markerat i närheten av sidans nederkant.
   * In the bottom right corner of the page, click **[!UICONTROL Submit Upload]**.
   * Klicka på i fältet Global navigering för **[!UICONTROL Jobs]** att kontrollera överföringsjobbets status. Fortsätt till nästa steg när **[!UICONTROL Status]** kolumnen på **[!UICONTROL Job]** sidan visar Överför klar.

1. Klicka på i navigeringsfältet uppe på sidan **[!UICONTROL Setup > Application Setup > Publish Setup > Image Server]**.
1. På sidan **[!UICONTROL Image Server Publish]**, under gruppen **[!UICONTROL Catalog Management]**, letar du upp **[!UICONTROL Rule Set Definition File Path]** och klickar sedan på **[!UICONTROL Select]**.
1. På sidan **[!UICONTROL Select Rule Set Definition File (XML)]** bläddrar du till regeluppsättningsfilen och klickar sedan på **[!UICONTROL Select]** i den nedre högra hörnet av sidan.
1. In the lower-right corner of the Setup page, click **[!UICONTROL Close]**.
1. Kör ett Image Server-publiceringsjobb.

   Regeluppsättningsvillkoren tillämpas på begäranden till dynamiska mediabildsservrar.

   Om du gör ändringar i regeluppsättningsfilen tillämpas ändringarna omedelbart när du överför och publicerar den uppdaterade regeluppsättningsfilen igen.

