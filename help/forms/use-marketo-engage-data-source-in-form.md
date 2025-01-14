---
Title: How to configure Marketo Engage data for Adaptive Forms?
Description: Learn how to use Marketo Engage schema in Adaptive Forms.
Keywords: Use Marketo Engage data source in Adaptive Forms, How to connect a Marketo instance data source with form? , Connect a form to Marketo.
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 4656ec65-f1ad-4e97-8d93-25933cdc7f7b
source-git-commit: e46c5afac945620cc44e9064956848acecc786bf
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Konfigurera Marketo Engage-datakälla för befintlig adaptiv Forms

<span class="preview"> Funktionen är tillgänglig i ett program för tidig användning. Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

![Arbetsflöde](/help/forms/assets/workflow-marketo-2.png)

När du har skapat molntjänstkonfigurationen för att integrera Marketo Engage med befintliga AEM Forms kan du konfigurera datakällan för formulär.

Genom att konfigurera dataintegrering kan användarna ansluta till olika datakällor eller scheman. Genom att integrera med datakällan i Marketo Engage och använda den i olika formulär blir det lättare att hantera data. Om du vill utforska de användningsklara datakällor som stöds för ett adaptivt formulär kan du läsa artikeln [Konfigurera datakällor](/help/forms/configure-data-sources.md).

## Att tänka på när du konfigurerar Marketo Engage-datakällan för formulär

När du konfigurerar Marketo Engage för datakällor för formulär bör du tänka på följande:

* Det går inte att ansluta Edge Delivery Services från Forms till Marketo Engage.

## Krav för att använda datakällan Marketo Engage för formulär

Krav för att använda Marketo Engage-datakällan med formulär:

* Skapa [molntjänstkonfigurationen för att integrera Marketo Engage med formulär](/help/forms/integrate-form-to-marketo-engage.md).

## Hur konfigurerar man det befintliga adaptiva formuläret för datakällan i Marketo Engage?

>[!VIDEO](https://video.tv.adobe.com/v/3442871/marketo-aem-forms-aem-marketo-engage)

Så här konfigurerar du ett adaptivt formulär med datakällan Marketo Engage:
1. Logga in på din [!DNL Experience Manager Forms] Author-instans.

2. Öppna det adaptiva formuläret för redigering.
3. Öppna innehållsträdet och välj **[!UICONTROL Guide Container]**.
4. Klicka på ikonen för den adaptiva formulärbehållaren ![Egenskaper för den adaptiva formulärbehållaren](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare där du konfigurerar datakällan öppnas.
5. Öppna fliken **[!UICONTROL Data Model]** och välj en formulärmodell som **Koppling**.
6. Välj **[!UICONTROL Connector]** i listrutan.

7. När du har valt **[!UICONTROL Connector]** kan du välja molnkonfigurationen.

   ![Välj Marketo Connector](/help/forms/assets/select-marketo-connector.png)

   Baserat på den markerade Marketo Engage-konfigurationen visas formulärelementen på fliken **[!UICONTROL Data Model Objects]** i **[!UICONTROL Content Browser]** i sidlisten. Du kan dra och släppa dessa element för att skapa ett anpassat formulär.

   ![Marketo Data Source](/help/forms/assets/marketo-engage-data-source.png)

8. Klicka på **[!UICONTROL Done]**.

Du kan också redigera egenskaperna för det adaptiva formuläret för att ändra dess associerade konfiguration.

Det adaptiva formuläret har nu konfigurerats med datakällan från den anslutna Marketo Engage-instansen. Konfigurera den nu för att skicka data till Adobe Marketo Engage.

## Vanliga frågor och svar

**F: Vad händer när du ändrar formulärets koppling?**\
**A:** Om du ändrar formulärets koppling blir de befintliga bindningarna ogiltiga.

**F: Vilka tre åtgärder är tillgängliga i tjänsten Invoke i regelredigeraren för formulär som är integrerade med Marketo Engage?**\
**A:** De tre körklara åtgärderna i **Invoke Service** för formulär som är integrerade med Marketo Engage är:
* Synkronisera lead
* Hämta lead efter ID
* Hämta lead efter filtertyp

## Nästa steg

Nu har du konfigurerat datakällan Marketo Engage för Adaptiv Forms. Sedan kan du [konfigurera ett anpassat formulär så att data skickas till Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md).

## Relaterade artiklar

{{af-submit-action}}

## Se även

{{marketo-engage-see-also}}
