---
title: Hur skapar och hanterar man granskningar i blanketter?
description: Använd granskningsfunktionen för att lägga till granskare och låta granskare kommentera ett formulär.
topic-tags: forms-manager
feature: Adaptive Forms, Foundation Components
exl-id: 378049f8-bf21-4595-819d-ba5fba7023c0
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# Skapa och hantera granskningar av formulär{#creating-and-managing-reviews-to-forms}

<span class="preview"> Adobe rekommenderar att du använder den moderna och utbyggbara datainhämtningen [Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=sv-SE) för [att skapa nya adaptiva Forms](/help/forms/creating-adaptive-form-core-components.md) eller [att lägga till adaptiva Forms på AEM Sites-sidor](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs ett äldre tillvägagångssätt för att skapa adaptiva Forms med baskomponenter. </span>


| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/create-reviews-forms.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |

## Granska {#review}

En granskning är en mekanism som gör att en eller flera granskare kan kommentera i formulär.

## Konfigurera en granskning {#setting-up-a-review}

1. Navigera till formulärwebbläsaren och välj ett formulär som ska granskas.
1. Om formuläret inte har någon pågående granskning visas ikonen **Starta granskning** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) i åtgärdsfältet. Klicka på ikonen **Starta granskning** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) .
1. Ange följande information:

   * **Titel**: Obligatoriskt, kan innehålla alfanumeriska tecken, bindestreck och understreck.
   * **Beskrivning**: Valfritt, beskrivning av syftet/innehållet som ska granskas.
   * **Deadline**: Valfritt datum då granskningen avslutas. När tidsgränsen har passerats visas aktiviteten som&quot;Försenad&quot;.
   * **Namn på granskare**: Minst ett är obligatoriskt. Använd kombinationsrutan om du vill lägga till granskare, skriva en namnlista med alla matchande namn, markera ett namn och klicka på **Lägg till**. I nästa avsnitt på fliken **Granskare** visas namnen på alla granskare.

1. Klicka på **Start** för att starta en granskning.

   >[!NOTE]
   >
   >* Administratören kan komma åt alla grupper som är kopplade till formuläranvändarna.
   >* Tjänstanvändargruppen är inte tillgänglig för granskning.

### Åtgärder som inträffar när en granskning konfigureras {#actions-that-occur-when-a-review-is-set-up}

I det här avsnittet beskrivs vad som händer när en granskning skapas eller konfigureras.

1. En ny granskningsuppgift skapas och tilldelas den valda granskaren.
1. Alla granskare tilldelas en granskningsuppgift. Uppgiften visas i meddelandeavsnittet. Granskaren kan klicka på ett meddelande eller gå till Inkorgen för att visa uppgiften. Granskaren kan klicka för att öppna granskningsprocessen, visa formuläret och börja lägga till kommentarer.

   ![Aviseringsvarning för granskare](assets/review-notification-img.png)

   Aviseringsvarning för granskare

1. Kommentarsrutan är tillgänglig för granskarna av formuläret. Andra kan läsa kommentarerna, men inte lägga till egna.

## Hantera en granskning {#managing-a-review}

>[!NOTE]
>
>* Endast pågående granskningar kan ändras.
>* Fullständiga granskningar kan inte ändras.

1. Navigera till fliken Formulär och markera ett formulär.

1. Om ett formulär har en pågående granskning och du är initierare för granskningen, visas ikonen **Hantera granskning** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) i åtgärdsfältet. Det är bara granskningsinitieraren som kan hantera (uppdatera/avsluta) granskningen.

   Klicka på ikonen **Hantera granskning** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png).

   För andra användare än initieraren är ikonen Hantera granskning inaktiverad.

1. Nu får du en skärm som visar information:

   * **Granskningsnamn**: Det går inte att redigera.

   * **Granska beskrivning**: Kan redigeras.

   * **Tidsgräns för granskning**: Tillgänglig för redigering. Du kan ändra deadline till vilket datum och vilken tid som helst efter det aktuella datumet och den aktuella tiden.

   * **Granskare**: Kan redigeras. Du kan lägga till eller ta bort granskare. Om en uppgift är försenad kan du bara lägga till granskare efter att du har förlängt tidsgränsen efter det aktuella datumet.

1. Klicka på **Slut** om du vill avsluta granskningen.

### Åtgärder som inträffar när en granskning ändras {#actions-that-occur-when-a-review-is-modified}

I det här avsnittet beskrivs vad som händer på **Granska uppdatering/Slut**:

1. Om granskningsbeskrivningen ändras uppdateras motsvarande uppgift för granskarna och initieraren.
1. Om tidsgränsen för granskningen ändras uppdateras motsvarande uppgift för granskarna med det nya datumet.

1. Om en granskare tas bort:

   ![Tar bort en granskare](assets/removeduser.png)

   Ta bort en granskare

   1. Om den tilldelade aktiviteten är ofullständig avslutas den.
   1. Granskaren kan inte längre kommentera formuläret.

1. Om en granskare läggs till:

   ![Lägger till en granskare](assets/addedreviewer.png)

   Lägga till en granskare

   1. En granskningsåtgärd skapas och tilldelas den nya granskaren.
   1. Den nya granskaren kan lägga till kommentarer om formuläret.

1. När en granskning avslutas:

   1. **Granskare**: För varje granskare avslutas den ofullständiga aktiviteten som är relaterad till granskningen. Aktiviteten visas inte längre som Väntande i granskarens meddelandeavsnitt.
   1. **Initierare**: Aktiviteten som tilldelats granskningsinitieraren har markerats som slutförd. Aktiviteten tas bort från meddelandeavsnittet för granskningsinitieraren.
   1. **Alla**: Granskningen visas i avsnittet Tidigare granskningar. Inga fler kommentarer kan läggas till.

   ![granskningen har slutförts](assets/review-complete-imgg.png)


## Se även {#see-also}

{{see-also}}


<!--

>[!MORELIKETHIS]
>
>* [Associating submission reviewers with a form](/help/forms/adding-reviewers-form.md)

-->