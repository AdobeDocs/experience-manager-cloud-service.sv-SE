---
Title: How to configure submit action to Marketo Engage for forms?
Description: Learn how to configure the submit action of Adaptive Form to send data to Marketo Engage.
Keywords: Submit data to Marketo engage, Configure submit action as Submit to Marketo Engage
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 0683564b-1ac4-42b4-bc08-101c4fdef286
source-git-commit: ce4646d8db1870f8ec85faddeb4e0a6a04f4c46e
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---

# Konfigurera skicka-åtgärden till Marketo Engage för befintliga formulär

<span class="preview"> Funktionen är tillgänglig i ett program för tidig användning. Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

![Arbetsflöde](/help/forms/assets/workflow-marketo-3.png)

Adaptiv Forms-redigerare innehåller åtgärden **Skicka till Marketo Engage** som skickar adaptiva Forms-data till Adobe Marketo Engage för bearbetning. Du kan konfigurera ett befintligt adaptivt formulär så att data skickas till [Adobe Marketo Engage](https://experienceleague.adobe.com/sv/docs/marketo/using/home) när det skickas.

Det finns ett antal färdiga skickningsåtgärder för att hantera formuläröverföringar. Du kan läsa mer om de här alternativen i artikeln [Åtgärd för att skicka anpassade formulär](/help/forms/configure-submit-actions-core-components.md).

## Tänk på att skicka-åtgärd till Marketo Engage för formulär konfigureras

* Kontrollera att det adaptiva formuläret är konfigurerat med Marketo Engage datakälla för att skicka data till Marketo Engage när formuläret skickas. Du kan dock ändra skicka-åtgärden till alternativ, till exempel **Skicka till OneDrive** eller **Skicka till SharePoint**, även om formuläret har konfigurerats med Marketo Engage dataschema.

## Krav för att konfigurera skicka-åtgärden till Marketo Engage för befintligt formulär

Krav för att konfigurera skicka-åtgärden till Marketo Engage:

* Konfigurera [Marketo Engage-datakällan för adaptivt formulär](/help/forms/use-marketo-engage-data-source-in-form.md) och bind formulärelementen med Marketo Engage-fält.

## Hur konfigurerar jag skicka-åtgärden till Marketo Engage för befintliga formulär?

>[!VIDEO](https://video.tv.adobe.com/v/3442866/submit-action-marketo-engage-marketo-aem-aem-forms-engage)

>[!BEGINTABS]

>[!TAB Foundation Component]

Du kan konfigurera skickaåtgärden för ett adaptivt formulär baserat på Foundation-komponenter så att data skickas till Adobe Marketo Engage. Så här konfigurerar du skicka-åtgärden till Marketo Engage:

1. Logga in på din [!DNL Experience Manager Forms] Author-instans.
1. Öppna det adaptiva formuläret för redigering och navigera till avsnittet **[!UICONTROL Submission]** i egenskaperna för den adaptiva formulärbehållaren och välj en skicka-åtgärd som **Skicka till Marketo Engage**.
1. Klicka på **[!UICONTROL Done]**.

![Marketo Submit Action](/help/forms/assets/marketo-engage-submit-action-af.png){width=50%, height=50%}

När du har konfigurerat skicka-åtgärden för det adaptiva formuläret som **Skicka till Marketo Engage** kan du skicka data till Adobe Marketo Engage för bearbetning. Data kan användas för att analysera och optimera marknadsföringskampanjer, automatisera uppföljning av e-post och utlösa arbetsflöden baserat på inskickade formulär.

>[!TAB Kärnkomponent]

Du kan konfigurera skickaåtgärden för ett adaptivt formulär baserat på kärnkomponenter för att skicka data till Adobe Marketo Engage. Så här konfigurerar du skicka-åtgärden till Marketo Engage:

1. Öppna det adaptiva formuläret för redigering.
1. Öppna innehållsträdet och välj **[!UICONTROL Guide Container]**.
1. Klicka på ikonen för den adaptiva formulärbehållaren ![Egenskaper för den adaptiva formulärbehållaren](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare där du kan konfigurera skickaåtgärden öppnas.
1. Öppna fliken **[!UICONTROL Submission]** och välj en skicka-åtgärd som **Skicka till Marketo Engage**.
1. Klicka på **[!UICONTROL Done]**.

![Marketo Submit Action](/help/forms/assets/marketo-engage-submit-action.png){width=50%, height=50%}

När du har konfigurerat skicka-åtgärden för det adaptiva formuläret som **Skicka till Marketo Engage** kan du skicka data till Adobe Marketo Engage för bearbetning. Data kan användas för att analysera och optimera marknadsföringskampanjer, automatisera uppföljning av e-post och utlösa arbetsflöden baserat på inskickade formulär.

>[!TAB Universell redigerare]

Du kan konfigurera skickaåtgärden för ett adaptivt formulär som har skapats i Universal Editor så att data skickas till Adobe Marketo Engage. Så här konfigurerar du skicka-åtgärden till Marketo Engage:

1. Öppna det adaptiva formuläret för redigering.
1. Klicka på tillägget **Redigera formuläregenskaper** i redigeraren.
Dialogrutan **Formuläregenskaper** visas.

   >[!NOTE]
   >
   > * Om ikonen **Redigera formuläregenskaper** inte visas i det universella redigeringsgränssnittet aktiverar du tillägget **Redigera formuläregenskaper** i Extension Manager.
   > * Läs artikeln [Extension Manager Feature Highlights](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) om du vill veta hur du aktiverar eller inaktiverar tillägg i den universella redigeraren.

1. Klicka på fliken **Skicka** och välj åtgärden **[!UICONTROL Submit to Marketo Engage]** Skicka.

   ![Marketo Submit Action](/help/forms/assets/marketo-engage-submit-action-ue.png)

1. Klicka på **[!UICONTROL Save & Close]**.

När du har konfigurerat skicka-åtgärden för det adaptiva formuläret som **Skicka till Marketo Engage** kan du skicka data till Adobe Marketo Engage för bearbetning. Data kan användas för att analysera och optimera marknadsföringskampanjer, automatisera uppföljning av e-post och utlösa arbetsflöden baserat på inskickade formulär.

>[!ENDTABS]

## Vanlig fråga (FAQ)

**F: Kan du ändra skicka-åtgärden för formulär som har konfigurerats för att ansluta till Marketo Engage-schemat?**
**A:** Som standard är åtgärden **Skicka till Marketo** markerad när ett formulär har konfigurerats för att ansluta till Marketo Engage-schemat. Du kan dock ändra Skicka-åtgärden för formulären om det behövs.

## Nästa steg

Du kan också ansluta ett adaptivt formulär till [Munchkin-biblioteket](https://experienceleague.adobe.com/sv/docs/marketo/using/product-docs/administration/setup/munchkin) för att spåra antalet besök, klick och formuläröverföringar.

## Relaterade artiklar

{{af-submit-action}}

## Se även

{{marketo-engage-see-also}}
