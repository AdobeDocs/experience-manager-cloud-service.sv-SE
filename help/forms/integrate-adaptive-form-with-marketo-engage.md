---
Title: How to integrate Marketo Engage with AEM Forms using Form wizard?
Description: Learn how to integrate your Marketo Engage instance with AEM Forms using form wizard.
Keywords: How to connect a Marketo instance with form? , Connect a form to Marketo, Integrate a form with Marketo Engage, Integrate an Adaptive Form with a Marketo instance.
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 1fcba628-ffd8-416a-a8b5-76b35d4aabd4
source-git-commit: 10de700e5e4b352051b8b77dfd0825bb9b6e0219
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---

# Konfigurera ett nytt formulär som ska integreras med Marketo Engage

<span class="preview"> Funktionen är tillgänglig i ett program för tidig användning. Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

![Arbetsflöde](/help/forms/assets/workflow-marketo-4.png)

När du har skapat molntjänstkonfigurationen för integrering av Marketo Engage med AEM Forms kan du konfigurera ett adaptivt formulär som ska integreras med [Adobe Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home).

Du kan ansluta Marketo Engage till ett adaptivt formulär med hjälp av formulärguiden, som förenklar konfigurationsprocessen genom att vägleda dig genom varje steg. Här kan du välja mallar, format och datafält, samt ange datamappning för att säkerställa att formuläret är klart att kommunicera med Marketo Engage när det har skapats. Med hjälp av formulärguiden kan du även konfigurera det adaptiva formuläret så att data skickas direkt till Adobe Marketo Engage när det skickas.

## Att tänka på när du konfigurerar Marketo Engage-datakällan för formulär

När du konfigurerar Marketo Engage för datakällor för formulär bör du tänka på följande:

* Det går inte att ansluta Edge Delivery Services från Forms till Marketo Engage.

## Krav för att ansluta Marketo Engage till formulär

Krav för att ansluta Marketo Engage till formulär:

* Skapa [molntjänstkonfigurationen för att integrera Marketo Engage med formulär](/help/forms/integrate-form-to-marketo-engage.md).

## Hur konfigurerar man det nya adaptiva formuläret för integrering med Marketo Engage?

Så här konfigurerar du ett nytt adaptivt formulär som ska integreras med Marketo Engage:

1. Välj **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.

   ![Välj Forms och dokument](/help/forms/assets/select-forms.png)

1. Välj **[!UICONTROL Create]** > **[!UICONTROL Adaptive Forms]**. Guiden för att skapa formulär öppnas.

   ![Välj AF](/help/forms/assets/select-create-forms.png)

1. Välj en mall på fliken **[!UICONTROL Source]**

   ![Välj mallar](/help/forms/assets/select-template.png)

1. Välj temat från **[!UICONTROL Style]**.

   ![Välj tema](/help/forms/assets/select-form-theme.png)


1. På fliken **[!UICONTROL Data]** väljer du en datamodell som **Marketo Engage**.

1. Välj **[!UICONTROL Cloud Configuration]** i listrutan som visas i skärmens högra ruta.
Som standard visas alla fält i den associerade konfigurationen. I guiden kan du välja vilka fält som ska inkluderas i det anpassade formuläret med hjälp av kryssrutor.

   ![Välj datamodell](/help/forms/assets/select-marketo-data.png)

1. Välj Skicka-åtgärd som **[!UICONTROL Submit to Marketo]** på fliken **[!UICONTROL Submission]**.

   När du väljer datamodellen som **Marketo Engage** markeras åtgärden **Skicka till Marketo** automatiskt. Du kan välja en annan skickaåtgärd på fliken **[!UICONTROL Submission]**. Fliken **[!UICONTROL Submission]** visar alla tillgängliga skicka-åtgärder.

   ![Skicka till Marketo-engagemang](/help/forms/assets/select-marketo-engage.png)

1. Välj **[!UICONTROL Create]**. Ange titel, namn och plats för att spara det adaptiva formuläret.

   ![Skapa formulär](/help/forms/assets/create-marketo-form.png)

1. Välj **[!UICONTROL Create]**.

Det adaptiva formuläret har nu konfigurerats för att ansluta till instansen Marketo Engage. Du kan också redigera egenskaperna för det adaptiva formuläret för att ändra dess associerade konfiguration.

## Vanliga frågor och svar

**F: Kan du ändra skicka-åtgärden för formulär som har konfigurerats för att ansluta till Marketo Engage-schemat?**
**A:** Som standard är åtgärden **Skicka till Marketo** markerad när ett formulär har konfigurerats för att ansluta till schemat i Marketo Engage. Du kan dock ändra Skicka-åtgärden för formulären om det behövs.


**F: Vad händer när du ändrar formulärets koppling?**\
**A:** Om du ändrar formulärets koppling blir de befintliga bindningarna ogiltiga.

**F: Vilka tre åtgärder är tillgängliga i tjänsten Invoke i regelredigeraren för formulär som är integrerade med Marketo Engage?**\
**A:** De tre körklara åtgärderna i **Invoke Service** för formulär som är integrerade med Marketo Engage är:
* Synkronisera lead
* Hämta lead efter ID
* Hämta lead efter filtertyp

## Nästa steg

Du kan också ansluta ett adaptivt formulär till [Munchkin-biblioteket](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/setup/munchkin) för att spåra antalet besök, klick och formuläröverföringar.

## Relaterade artiklar

{{af-submit-action}}

## Se även

{{marketo-engage-see-also}}
