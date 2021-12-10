---
title: Koppla granskare som skickar in svar till ett formulär
seo-title: Associating submission reviewers with a form
description: Lär dig hur du associerar granskare med ett formulär i [!DNL AEM Forms]. Associerade granskare granskar ett formulär som skickats via formulärportalen.
seo-description: Learn how to associate submission reviewers with a form in [!DNL AEM Forms]. Associated reviewers review a form submitted via forms portal.
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Koppla granskare som skickar in svar till ett formulär {#associating-submission-reviewers-with-a-form}

När du skapar ett formulär kan du ange vilka användare som ska granska inskickade formulär via formulärportalen och ge feedback. Din organisation kan samla in feedback och omarbeta de inskickade formulären.

[!DNL AEM Forms] I kan du associera en granskargrupp med ett formulär. Användare som läggs till i en granskningsgrupp i ett formulär kan se inskickade formulär och ge feedback.

Granskningsgrupper som tilldelats ett formulär kan bara granska inskickade svar från det angivna formuläret.

## Förutsättning {#prerequisite}

### Aktivera gruppegenskap för granskare som skickar in data för Adaptiv Forms med hjälp av schemaredigeraren för metadata {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

Om du vill associera en granskargrupp med ett formulär redigerar du metadatamodeller i Adaptive Forms. Som standard kan du inte lägga till en granskningsgrupp i ett skickat formulär.

Så här redigerar du metadataschema:

1. Klicka på under Experience Manager i författarläget **verktyg** > **Resurser** > **Metadata-scheman**.
1. Gå till Forms Schema **Forms** > **Forms i AEM.**

   Sidans URL är:

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. Välj **Adaptiv form** och klicka **Redigera**.
1. På sidan Redigera formulär klickar du på **Avancerat**.
1. Dra och släpp **Enkelradstext** som finns under Build Form.
1. Markera den tillagda textkomponenten för att se dess inställningar.

   Under Inställningar anger du `./jcr:content/metadata/form-submission-reviewer-group` i fältet Mappa till egenskap.

   Fältet för gruppen Skicka granskare i de avancerade egenskaperna i ditt adaptiva formulär aktiveras med det namn du anger under Fältetikett.

## Koppla granskare som skickar in svar till ett formulär {#associating-submission-reviewers-with-a-form-1}

Om du vill associera granskare med ett anpassat formulär skapar du en granskargrupp och lägger till användare. Lägg till den skapade granskargruppen under fältet för att skicka in formulär i formulärets avancerade egenskaper.
Med användargrupper kan du associera olika uppsättningar av granskare med olika adaptiva Forms. Den här funktionen förhindrar att obehöriga skickar in granskningar.

Innan du utför följande steg finns mer information i [Förutsättning](adding-reviewers-form.md#prerequisite).

Om du vill skapa en grupp och lägga till medlemmar i den går du till **verktyg** > **Operationer** > **Säkerhet** > **Grupper**.
Mer information finns i [Användaradministration och -tjänster](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html).
Se till att du lägger till gruppen som du skapar som medlem i den körklara användargruppen: **formulär-inskickning-granskare**. Den här användargruppen levereras med [!DNL AEM Forms]och det ser till att användare läggs till som granskare.

Så här associerar du användargrupper med ett anpassat formulär:

1. I redigeringsläget går du till **Forms** > **Forms och dokument**.
1. Använd alternativet **Välj **för att välja ett anpassat formulär och klicka på **Visa egenskaper**.
1. I fönstret Egenskaper i formuläret klickar du på **Redigera** och klicka sedan på **AVANCERAD**.
1. Ange gruppen i gruppfältet för granskare som ska skicka in och klicka på **Klar**.

   Gruppfältet för granskare som skickar in visas med det namn som du angav i det redigerade metadataschemat för Adaptive Forms.

>[!NOTE]
>
>Replikera användare och formulär för att säkerställa tillgänglighet för användare och formulär vid fjärrimplementering av [!DNL AEM Forms].
>
>Se till att alla användare replikeras som granskningsmedlemmar i användargrupperna i fjärrimplementeringen.

