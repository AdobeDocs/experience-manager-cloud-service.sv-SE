---
Title: How to configure submit action to Marketo Engage for forms?
Description: Learn how to configure the submit action of Adaptive Form to send data to Marketo Engage.
Keywords: Submit data to Marketo engage, Configure submit action as Submit to Marketo Engage
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 0683564b-1ac4-42b4-bc08-101c4fdef286
source-git-commit: e46c5afac945620cc44e9064956848acecc786bf
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---

# Konfigurera skicka-åtgärden till Marketo Engage för befintliga formulär

<span class="preview"> Funktionen är tillgänglig i ett program för tidig användning. Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

![Arbetsflöde](/help/forms/assets/workflow-marketo-3.png)

Den adaptiva Forms-redigeraren innehåller åtgärden **Skicka till Marketo Engage** som skickar adaptiva Forms-data till Adobe Marketo Engage för bearbetning. Du kan konfigurera ett befintligt adaptivt formulär så att data skickas till [Adobe Marketo Engage](https://experienceleague.adobe.com/sv/docs/marketo/using/home) när det skickas.

Det finns ett antal färdiga skickningsåtgärder för att hantera formuläröverföringar. Du kan läsa mer om de här alternativen i artikeln [Åtgärd för att skicka anpassade formulär](/help/forms/configure-submit-actions-core-components.md).

## Tänk på att skicka-åtgärd till Marketo Engage för formulär konfigureras

* Kontrollera att det adaptiva formuläret är konfigurerat med datakällan Marketo Engage för att skicka data till Marketo Engage när formuläret skickas in. Du kan dock ändra skicka-åtgärden till alternativ, till exempel **Skicka till OneDrive** eller **Skicka till SharePoint**, även om formuläret har konfigurerats med dataramodet Marketo Engage.

## Krav för att konfigurera skicka-åtgärden till Marketo Engage för det befintliga formuläret

Krav för att konfigurera sändningsåtgärden till Marketo Engage:

* Konfigurera datakällan [Marketo Engage för det adaptiva formuläret](/help/forms/use-marketo-engage-data-source-in-form.md) och bind formulärelementen med Marketo Engage-fält.

## Hur konfigurerar jag skicka-åtgärden till Marketo Engage för befintliga formulär?

>[!VIDEO](https://video.tv.adobe.com/v/3442866/submit-action-marketo-engage-marketo-aem-aem-forms-engage)

Du kan konfigurera skickaåtgärden för ett adaptivt formulär så att data skickas till Adobe Marketo Engage. Så här konfigurerar du åtgärden skicka till Marketo Engage:

1. Öppna det adaptiva formuläret för redigering.
2. Öppna innehållsträdet och välj **[!UICONTROL Guide Container]**.
3. Klicka på ikonen för den adaptiva formulärbehållaren ![Egenskaper för den adaptiva formulärbehållaren](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare där du kan konfigurera skickaåtgärden öppnas.
4. Öppna fliken **[!UICONTROL Submission]** och välj en skicka-åtgärd som **Skicka till Marketo Engage**.
5. Klicka på **[!UICONTROL Done]**.

![Marketo Submit Action](/help/forms/assets/marketo-engage-submit-action.png){width=50%, height=50%}


När du har konfigurerat skicka-åtgärden för det adaptiva formuläret som **Skicka till Marketo Engage** kan du skicka data till Adobe Marketo Engage för bearbetning. Data kan användas för att analysera och optimera marknadsföringskampanjer, automatisera uppföljning av e-post och utlösa arbetsflöden baserat på inskickade formulär.

## Vanlig fråga (FAQ)

**F: Kan du ändra skicka-åtgärden för formulär som har konfigurerats för att ansluta till Marketo Engage-schemat?**
**A:** Som standard är åtgärden **Skicka till Marketo** markerad när ett formulär har konfigurerats för att ansluta till schemat i Marketo Engage. Du kan dock ändra Skicka-åtgärden för formulären om det behövs.

## Nästa steg

Du kan också ansluta ett adaptivt formulär till [Munchkin-biblioteket](https://experienceleague.adobe.com/sv/docs/marketo/using/product-docs/administration/setup/munchkin) för att spåra antalet besök, klick och formuläröverföringar.

## Relaterade artiklar

{{af-submit-action}}

## Se även

{{marketo-engage-see-also}}
