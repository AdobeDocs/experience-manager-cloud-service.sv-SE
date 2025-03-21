---
title: Byt namn på och gruppera resurser om namn i  [!DNL Assets view]
description: Lär dig hur du byter namn på resurser gruppvis med det nya användargränssnittet i Assets (Assets-vyn). Det gör det möjligt att byta namn på flera resurser samtidigt.
role: User
exl-id: e041811b-0246-408f-9246-248da55f66a1
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Byt namn på resurs eller mapp i [!DNL Assets view] {#rename-single-asset-or-folder}

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

Att byta namn kan hjälpa till att ordna, kategorisera och identifiera resurser bättre utan att ändra dess innehåll eller plats. Med [!DNL Assets view] kan du byta namn på den valda resursen eller mappen.

Utför stegen nedan för att byta namn på en resurs eller mapp:

1. Leta reda på resursen eller mappen som du vill byta namn på.

1. Använd något av följande sätt för att byta namn på en resurs eller en mapp:

   * Markera resursen eller mappen och klicka på ikonen ![Byt namn](assets/do-not-localize/rename-icon.png) **[!UICONTROL Rename]** på den översta menyn.
   * Klicka på fler alternativ `...` för resursen eller mappen och välj **[!UICONTROL Rename]**.
   * Klicka på resursens eller mappens titel för att byta namn på den. Ange den nya texten i textrutan **Byt namn på resurs** och klicka på **Spara**. Den här funktionen är tillgänglig i stödraster-, galleri-, vattenfalls- och listvyerna.

## AI-baserade resurser - byt namn på massvis {#rename-bulk-assets-using-ai}

Med [!DNL Assets view] kan du byta namn på flera resurser samtidigt med hjälp av AI. AI-funktionen Byt namn gruppvis kan bara användas på filer, inte på mappar. Du kan markera flera filer samtidigt och döpa om dem alla samtidigt.

Följ stegen nedan om du vill byta namn på huvuddelen av resurserna samtidigt med hjälp av AI-genererade uppmaningar:

1. Markera flera resurser och klicka på **[!UICONTROL Bulk Rename]** på den översta menyn.

1. Lägg till uppmaningen som beskriver hur du vill byta namn på de markerade resurserna. Se [några exempel som illustrerar AI Bulk Rename](#examples-ai-bulk-rename).

1. Klicka på **[!UICONTROL Execute]** om du vill tillåta att AI byter namn på resurser så som anges i uppmaningen.

1. [Valfritt] Klicka på ikonen ![Ångra ](assets/do-not-localize/undo.svg) om du vill ångra eller avbryta den senaste åtgärden du utförde.

1. Kontrollera ändringarna i kolumnen [!UICONTROL New name preview] och klicka på **[!UICONTROL Save]**.

   ![Byt namn på flera AI-filer](assets/ai-bulk-rename.png)

## Några exempel som illustrerar AI Bulk Rename {#examples-ai-bulk-rename}

Nedan följer några exempel på hur du kan använda AI för att byta namn på resurser i grupp baserat på en AI-fråga:

* Lägg till 00, 01 osv. som prefix med dagens datum.
* Ändra alla filer till &quot;min-fil&quot; och lägg till ett ökande nummer.
* Ta bort prefixet och suffixet, behåll bara den mellersta delen av namnet.
* Lägg till 001, 002 osv. som prefix för filerna. och översätt till engelska.

>[!VIDEO](https://video.tv.adobe.com/v/3440975)

>[!NOTE]
>
> * Du kan inte konvertera känslolägesikoner till text.
> * Använd ett unikt namn för att undvika varningsmeddelanden när du byter namn på resurser. Du kan dock försöka igen med ett nytt namn.
> * Du kan också konvertera Unicode-tecken eller icke-alfanumeriska tecken till text.

## Nästa steg {#next-steps}

* [Titta på en video om hur du hanterar metadataformulär i Assets-vyn](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/configuring/metadata-forms.html)

* Ge produktfeedback med alternativet [!UICONTROL Feedback] som finns i användargränssnittet i Assets-vyn

* Ge feedback om dokumentationen med [!UICONTROL Edit this page] ![redigera sidan](assets/do-not-localize/edit-page.png) eller [!UICONTROL Log an issue] ![skapa ett GitHub-problem](assets/do-not-localize/github-issue.png) som är tillgängligt på den högra sidopanelen

* Kontakta [kundtjänst](https://experienceleague.adobe.com/?support-solution=General#support)
