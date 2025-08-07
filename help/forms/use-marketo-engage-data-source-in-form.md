---
Title: How to configure Marketo Engage data for Adaptive Forms?
Description: Learn how to use Marketo Engage schema in Adaptive Forms.
Keywords: Use Marketo Engage data source in Adaptive Forms, How to connect a Marketo instance data source with form? , Connect a form to Marketo.
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 4656ec65-f1ad-4e97-8d93-25933cdc7f7b
source-git-commit: dabf8029577c5fb6bb5eebdbf10d77f3d4d95a5d
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---

# Konfigurera Marketo Engage-datakälla för befintliga adaptiva Forms

<span class="preview"> Funktionen är tillgänglig i ett program för tidig användning. Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

![Arbetsflöde](/help/forms/assets/workflow-marketo-2.png)

När du har skapat molntjänstkonfigurationen för att integrera Marketo Engage med befintliga AEM Forms kan du konfigurera datakällan för formulär.

Genom att konfigurera dataintegrering kan användarna ansluta till olika datakällor eller scheman. Genom att integrera med Marketo Engage datakälla och använda den i olika formulär blir det lättare att hantera data. Om du vill utforska de användningsklara datakällor som stöds för ett adaptivt formulär kan du läsa artikeln [Konfigurera datakällor](/help/forms/configure-data-sources.md).

## Att tänka på när du konfigurerar Marketo Engage-datakällan för formulär

När du konfigurerar Marketo Engage datakälla för formulär bör du tänka på följande:

* Det går inte att ansluta Edge Delivery Services Forms till Marketo Engage.

## Krav för att använda Marketo Engage datakälla för formulär

Krav för att använda Marketo Engage datakälla med formulär:

* Skapa [molntjänstkonfigurationen för att integrera Marketo Engage med formulär](/help/forms/integrate-form-to-marketo-engage.md).

## Hur konfigurerar man det befintliga adaptiva formuläret för Marketo Engage datakälla?

>[!VIDEO](https://video.tv.adobe.com/v/3442871/marketo-aem-forms-aem-marketo-engage)

<span> Den här videon gäller endast för kärnkomponenter. Information om UE/Foundation Components finns i artikeln.</span>

>[!BEGINTABS]

>[!TAB Foundation Component]

Så här konfigurerar du ett adaptivt formulär baserat på Foundation-komponenter med Marketo Engage-datakällan:

1. Logga in på din [!DNL Experience Manager Forms] Author-instans.
1. Öppna det adaptiva formuläret för redigering och navigera till avsnittet **[!UICONTROL Data Model]** i egenskaperna för den adaptiva formulärbehållaren och välj en formulärmodell som **Koppling**.
1. Välj **[!UICONTROL Connector]** i listrutan.
1. När du har valt **[!UICONTROL Connector]** kan du välja molnkonfigurationen.

   ![Välj Marketo Connector](/help/forms/assets/select-marketo-connector-af1.png){width=50%, height=50%}

   Baserat på den valda Marketo Engage-konfigurationen visas formulärelementen på fliken **[!UICONTROL Data Model Objects]** i **[!UICONTROL Content Browser]** i sidlisten. Du kan dra och släppa dessa element för att skapa ett anpassat formulär.

   ![Marketo Data Source](/help/forms/assets/marketo-engage-data-source-af1.png){width=50%, height=50%}

1. Klicka på **[!UICONTROL Done]**.

Du kan också redigera egenskaperna för det adaptiva formuläret för att ändra dess associerade konfiguration.

Det adaptiva formuläret har nu konfigurerats med datakällan från den anslutna Marketo Engage-instansen. Konfigurera den nu för att skicka data till Adobe Marketo Engage.

>[!TAB Kärnkomponent]

Så här konfigurerar du ett adaptivt formulär baserat på kärnkomponenter med Marketo Engage datakälla:

1. Logga in på din [!DNL Experience Manager Forms] Author-instans.

1. Öppna det adaptiva formuläret för redigering.
1. Öppna innehållsträdet och välj **[!UICONTROL Guide Container]**.
1. Klicka på ikonen för den adaptiva formulärbehållaren ![Egenskaper för den adaptiva formulärbehållaren](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare där du konfigurerar datakällan öppnas.
1. Öppna fliken **[!UICONTROL Data Model]** och välj en formulärmodell som **Koppling**.
1. Välj **[!UICONTROL Connector]** i listrutan.

1. När du har valt **[!UICONTROL Connector]** kan du välja molnkonfigurationen.

   ![Välj Marketo Connector](/help/forms/assets/select-marketo-connector.png){width=50%, height=50%}

   Baserat på den valda Marketo Engage-konfigurationen visas formulärelementen på fliken **[!UICONTROL Data Model Objects]** i **[!UICONTROL Content Browser]** i sidlisten. Du kan dra och släppa dessa element för att skapa ett anpassat formulär.

   ![Marketo Data Source](/help/forms/assets/marketo-engage-data-source.png){width=50%, height=50%}

1. Klicka på **[!UICONTROL Done]**.

Du kan också redigera egenskaperna för det adaptiva formuläret för att ändra dess associerade konfiguration.

Det adaptiva formuläret har nu konfigurerats med datakällan från den anslutna Marketo Engage-instansen. Konfigurera den nu för att skicka data till Adobe Marketo Engage.

>[!TAB Universell redigerare]

Så här konfigurerar du ett adaptivt formulär som har skapats i Universal Editor med Marketo Engage-datakällan:

1. Öppna egenskaperna för formuläret för redigering.
1. Välj **[!UICONTROL Form Model]**.
1. Välj **Koppling** i **[!UICONTROL Form Model]**.
1. När du har valt **[!UICONTROL Connector]** kan du välja molnkonfigurationen.

   ![Välj Marketo Connector](/help/forms/assets/select-marketo-connector-ue.png)

1. Klicka på **[!UICONTROL Save & Close]**.

Baserat på den valda Marketo Engage-konfigurationen visas formulärelementen på fliken **[!UICONTROL Datasource]** i Content Browser på egenskapspanelen. Du kan dra och släppa dessa element för att skapa ett anpassat formulär.

![Marketo Data Source](/help/forms/assets/marketo-engage-data-source-ue.png)

Formuläret har nu konfigurerats med datakällan från den anslutna Marketo Engage-instansen. Konfigurera den nu för att skicka data till Adobe Marketo Engage.

>[!ENDTABS]

## Vanliga frågor och svar

**F: Vad händer när du ändrar formulärets koppling?**\
**A:** Om du ändrar formulärets koppling blir de befintliga bindningarna ogiltiga.

**F: Vilka tre åtgärder är tillgängliga i tjänsten Invoke i regelredigeraren för formulär som är integrerade med Marketo Engage?**\
**A:** De tre körklara åtgärderna i **Invoke Service** för formulär som är integrerade med Marketo Engage är:
* Synkronisera lead
* Hämta lead efter ID
* Hämta lead efter filtertyp

## Nästa steg

Nu har du konfigurerat Marketo Engage datakälla för Adaptive Forms. Sedan kan du [konfigurera ett anpassat formulär så att data skickas till Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md).

## Relaterade artiklar

{{af-submit-action}}

## Se även

{{marketo-engage-see-also}}
