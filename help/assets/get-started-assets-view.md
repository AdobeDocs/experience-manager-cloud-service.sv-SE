---
title: Kom igång med  [!DNL Assets View]
description: Så här kommer du åt, inloggningsupplevelsen av, användningsfall som stöds och kända problem i  [!DNL Assets View].
role: User, Leader
exl-id: 51ae6657-f6b5-44b0-a47f-451735ab0d01
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# Kom igång med Assets {#assets-view-get-started}

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

<!-- TBD: Make links for these steps. -->

Hantera dina digitala resurser med [!DNL Assets View] kräver endast tre enkla steg:

* **Steg 1**: [Överför](/help/assets/add-delete-assets-view.md) och [visa](/help/assets/navigate-assets-view.md) resurser.
* **Steg 2**: [Sök](/help/assets/search-assets-view.md) och [hämta](/help/assets/manage-organize-assets-view.md#download) resurser.
* **Steg 3**: [Hantera och ordna](/help/assets/manage-organize-assets-view.md) resurserna.

Om du vill använda [!DNL Assets View] loggar du in på [https://experience.adobe.com/#/assets](https://experience.adobe.com/#/assets). Välj `Company or School Account` när du loggar in. Kontakta organisationens administratör för att få åtkomst.

<!--In addition, more reference information that can be helpful is [understanding of the user interface](/help/assets/navigate-assets-view.md), [list of use cases](#use-cases), [supported file types](/help/assets/supported-file-formats-assets-view.md), and [known issues](/help/assets/release-notes.md#known-issues).
-->

## Öppna Assets-vyn {#access-assets-view}

Mer information om hur du kommer åt vyn Assets finns i [Så här kommer du åt vyn Assets](/help/assets/assets-view-introduction.md#how-to-access-assets-view).

## Konfigurera [!DNL Assets View] {#configuration}

Om du vill öppna inställningarna klickar du på avataren i det övre högra hörnet av användargränssnittet. Du kan växla mellan det ljusa och det mörka temat i lösningsinställningarna.

Om du är en del av olika organisationer kan du även ändra organisationen och få tillgång till dina konton i olika organisationer.

Om du vill ändra [!UICONTROL Experience Cloud preferences] klickar du på [!UICONTROL Preferences].

![Inställning för att växla mörkt och ljust tema](assets/theme-change.png)

>[!NOTE]
>
>Om du navigerar till Assets-vyn och ser ett `Network Error`-meddelande kontrollerar du att du har utfört instruktionerna som nämns i artikeln [Cross-Origin Resource Sharing (CORS) ](/help/headless/deployment/cross-origin-resource-sharing.md) .

## [!DNL Assets View] användningsfall {#use-cases}

De olika DAM-aktiviteterna (Digital Asset Management) som du kan utföra med [!DNL Assets View] visas nedan.

| Användaruppgifter | Funktionalitet och instruktionsinformation |
|-----|------|
| Bläddra bland och visa resurser | <ul> <li>[Bläddra i databasen](/help/assets/navigate-assets-view.md#view-assets-and-details) </li> <li> [Förhandsgranska en resurs](/help/assets/navigate-assets-view.md#preview-assets) <li> [Visa återgivningar av en resurs](/help/assets/add-delete-assets-view.md#renditions) </li> <li>[Visa versioner av en resurs](/help/assets/manage-organize-assets-view.md#view-versions)</li></ul> |
| Lägg till nya resurser | <ul> <li>[Överför nya resurser och mappar](/help/assets/add-delete-assets-view.md)</li> <li>[Övervaka överföringsförloppet och hantera överföringar](/help/assets/add-delete-assets-view.md#upload-progress)</li> <li>[Lös dubbletter](/help/assets/add-delete-assets-view.md)</li> </ul> |
| Uppdatera resurser eller relaterad information | <ul> <li>[Redigera bilder](/help/assets/edit-images-assets-view.md)</li> <li>[Skapa versioner](/help/assets/manage-organize-assets-view.md#create-versions) och [visa versioner](/help/assets/manage-organize-assets-view.md#view-versions)</li> <li>[Redigera bilder](/help/assets/edit-images-assets-view.md)</li> </ul> |
| Redigera resurser | <ul> <li>[Redigeringar i webbläsaren med Adobe Photoshop Express](/help/assets/edit-images-assets-view.md)</li> <li>[Beskär för en profil för sociala medier](/help/assets/edit-images-assets-view.md#crop-straighten-images)</li> <li>[Visa och hantera versioner](/help/assets/manage-organize-assets-view.md#view-versions)</li></ul></ul> |
| Sök efter resurser i databasen | <ul> <li>[Sök i en specifik mapp](/help/assets/search-assets-view.md#refine-search-results)</li> <li>[Sparade sökningar](/help/assets/search-assets-view.md#saved-search)</li> <li>[Sök efter nyligen visade resurser](/help/assets/search-assets-view.md)</li> <li>[Fulltextsökning](/help/assets/search-assets-view.md) |
| Hämta resurser | <ul> <li> [Förhandsgranska resurs](/help/assets/navigate-assets-view.md#preview-assets) </li> <li> [Hämta resurser](/help/assets/manage-organize-assets-view.md#download) <li> [Hämta återgivningar](/help/assets/add-delete-assets-view.md#renditions) </li></ul> |
| Metadataåtgärder | <ul> <li>[Visa detaljerade metadata](/help/assets/metadata-assets-view.md) </li> <li> [Uppdatera metadata](/help/assets/metadata-assets-view.md#update-metadata)</li> <li> [Skapa nytt metadataformulär](/help/assets/metadata-assets-view.md#metadata-forms) </li> </ul> |

## Nästa steg {#next-steps}

* [Titta på en video för att komma igång med Assets View](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/getting-started.html?lang=sv-SE)

* Ge produktfeedback med alternativet [!UICONTROL Feedback] som finns i användargränssnittet i Assets View

* Ge feedback om dokumentationen med [!UICONTROL Edit this page] ![redigera sidan](assets/do-not-localize/edit-page.png) eller [!UICONTROL Log an issue] ![skapa ett GitHub-problem](assets/do-not-localize/github-issue.png) som är tillgängligt på den högra sidopanelen

* Kontakta [kundtjänst](https://experienceleague.adobe.com/sv?support-solution=General#support)


<!--TBD: Merge the below rows in the table when the use cases are documented/available.

| How do I delete assets? | <ul> <li>[Delete assets](/help/assets/manage-organize.md)</li> <li>Recover deleted assets</li> <li>Permanently delete assets</li> </ul> |
| How do I share assets or find shared assets? | <ul> <li>Shared by me</li> <li>Shared with me</li> <li>Share for comments and review</li> <li>Unshare assets</li> </ul> |
| How do I collaborate with others and get my assets reviewed | <ul> <li>Share for review</li> <li>Provide comments. Resolve and filter comments</li> <li>Annotations on images</li> <li>Assign tasks to specific users and prioritize</li> </ul> |

-->

<!-- 

## ![feedback icon](assets/do-not-localize/feedback-icon.png) Provide product feedback {#provide-feedback}

Adobe welcomes feedback about the solution. To provide feedback without even switching your working application, use the [!UICONTROL Feedback] option in the user interface. It also lets you attach files such as screenshots or video recording of an issue.

  ![feedback option in the interface](assets/feedback-panel.png)

To provide feedback for documentation, click [!UICONTROL Edit this page] ![edit the page](assets/do-not-localize/edit-page.png) or [!UICONTROL Log an issue] ![create a GitHub issue](assets/do-not-localize/github-issue.png) from the right sidebar. You can do one of the following: 

* Make the content updates and submit a GitHub pull request.
* Create an issue or ticket in GitHub. Retain the automatically populated article name when creating an issue.

-->
<!--
>[!MORELIKETHIS]
>
>* [Understand the user interface](/help/assets/navigate-asssets-view.md).
>* [Release notes and known issues](/help/assets/release-notes.md).
>* [Supported file types](/help/assets/supported-file-formats.md).
-->
