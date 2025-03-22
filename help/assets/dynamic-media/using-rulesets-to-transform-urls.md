---
title: Använd regeluppsättningar för att omforma URL:er
description: Lär dig hur du distribuerar regeluppsättningar i Dynamic Media för att omvandla URL:er. Regeluppsättningar är instruktioner skrivna i ett skriptspråk (t.ex. JavaScript) som utvärderar XML-data och utför vissa åtgärder om dessa data uppfyller vissa villkor.
contentOwner: Rick Brough
feature: Rulesets,Troubleshooting,Upload,Best Practices
role: User
exl-id: f8010125-ba89-406a-bede-f6aa2f858c70
source-git-commit: a495178529a0a4229095ea3a11f52b376c81715b
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---

# Använd regeluppsättningar för att omforma URL:er {#using-rulesets-to-transform-urls}

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

Du kan distribuera regeluppsättningar i Dynamic Media för att omvandla URL:er. Regeluppsättningar är instruktioner skrivna i ett skriptspråk (t.ex. JavaScript) som utvärderar XML-data och utför vissa åtgärder om dessa data uppfyller vissa villkor. Varje regel består av minst ett villkor och minst en åtgärd. En regel utvärderar XML-data mot villkoren, och om ett villkor är uppfyllt utförs rätt åtgärd. Exempel på regeluppsättningar är följande:

* Lägga till ett MIME-typsuffix. Många tjänster och webbplatser kräver bildsuffix, som att lägga till `.jpg` till en URL.
* Skapa en mappsökväg till URL:en för sökmotoroptimering (SEO).

  Se [Hur Adobe Dynamic Media Classic stöder SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Lägga till metadata i URL:en för sökmotoroptimering.

  Se [Hur Adobe Dynamic Media Classic stöder SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Ställa in innehållets disposition för att utlösa en hämtning.
* Förenkla bildhanteringen genom att ange URL:er för personalisering. Gör till exempel `rgb{XX,YY,ZZ}` till RTF-klar `\redXX\greenYY\blueZZ`

* Begär att vissa tecken ska kodas, till exempel `$`, `{` och `}`, och vissa tecken ska avkodas mot ImageServer. Facebook fungerar till exempel inte så bra med URL:er som innehåller specialtecken.

När det gäller Dynamic Media kan webbplatser som använder ett XML-baserat system för att hantera resursinformation överföra XML-filer till Dynamic Media. Du kan ange en av dessa filer som förbearbetningsregeluppsättningsfil för att hantera Dynamic Media-resurser. Den här filen omstrukturerar standardformatet för URL-protokoll så att det uppfyller företagslogiken i system som integreras med Dynamic Media. Du anger en XML-fil som ska fungera som sökväg till definitionsfilen för regeluppsättningen.

>[!CAUTION]
>
>Var försiktig när du använder regeluppsättningar. De kan förhindra att dynamiskt medieinnehåll visas på webbplatsen.

Det finns exempelregeluppsättningar som kan hjälpa dig att skapa en egen regeluppsättning.
Se [Referens för regeluppsättning](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference).

Precis som när du skapar alla regeluppsättningar måste du se till att XML-filen är giltig innan du överför den med ett XML-valideringsprogram som xmlvalid.

Kontrollera också först att du testar regeluppsättningen i en staging-miljö som inte påverkar produktionsmiljön.
Produktionsmiljöer och staging-miljöer kräver normalt olika inloggningar.

Se [Adobe Dynamic Media Classic-datorprogrammet för inloggningsinformation](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/getting-started/signing-out).

<!-- OBSOLETE CONTENT * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->



## Distribuera XML-regler {#deploy-xml-rule-sets}

1. Öppna [Dynamic Media Classic-datorprogrammet](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/getting-started/signing-out) och logga sedan in på ditt konto.

   Dina inloggningsuppgifter och inloggningsuppgifter tillhandahölls av Adobe vid tidpunkten för etableringen. Kontakta kundsupport om du inte har den här informationen.

1. Överför regeluppsättningsfilen genom att göra följande:

   * Välj **[!UICONTROL Upload]** i fältet Global navigering.
   * På sidan **[!UICONTROL Upload]**, nära det övre vänstra hörnet, väljer du **[!UICONTROL Browse]**.
   * Bläddra till regeluppsättningsfilen (XML) i dialogrutan **[!UICONTROL Open]**.
   * Markera filen och välj sedan **[!UICONTROL Open]**.
   * Till höger på sidan **[!UICONTROL Upload]** väljer du en målmapp för regeluppsättningsfilen.
   * Kontrollera att Publicera efter överföring är markerat längst ned på sidan.
   * Välj **[!UICONTROL Submit Upload]** längst ned till höger på sidan.
   * I fältet Global navigering väljer du **[!UICONTROL Jobs]** för att kontrollera överföringsjobbets status. När kolumnen **[!UICONTROL Status]** på sidan **[!UICONTROL Job]** säger Överföring klar fortsätter du till nästa steg.

1. Navigera till **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]** i navigeringsfältet uppe på sidan.
1. På sidan **[!UICONTROL Image Server Publish]**, under gruppen **[!UICONTROL Catalog Management]**, letar du reda på **[!UICONTROL Rule Set Definition File Path]** och väljer sedan **[!UICONTROL Select]**.
1. På sidan **[!UICONTROL Select Rule Set Definition File (XML)]** bläddrar du till regeluppsättningsfilen och väljer **[!UICONTROL Select]** i det nedre högra hörnet på sidan.
1. Välj **[!UICONTROL Close]** i det nedre högra hörnet på sidan Inställningar.
1. Kör ett Image Server-publiceringsjobb.

   Regeluppsättningsvillkoren tillämpas på begäranden till dynamiska mediabildsservrar.

   Om du ändrar regeluppsättningsfilen tillämpas ändringarna omedelbart när du överför och publicerar den uppdaterade regeluppsättningsfilen igen.
