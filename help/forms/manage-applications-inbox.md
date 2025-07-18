---
title: Hur hanterar jag formulär, program och uppgifter i AEM Inbox?
description: Med AEM Inbox kan du starta Forms-centrerade arbetsflöden genom att skicka program och hantera uppgifter.
uuid: c6c0d8ea-743f-4852-99d1-69fd50a0994e
contentOwner: vishgupt
topic-tags: document_services, publish
discoiquuid: dd11fd83-3df1-4727-8340-8c5426812823
feature: Adaptive Forms
role: User
hide: true
hidefromtoc: true
exl-id: 92130660-9942-426f-ae2f-4f3300f9735c
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 0%

---

# Hantera Forms-program och -uppgifter i AEM Inbox{#manage-forms-applications-and-tasks-in-aem-inbox}

Ett av många sätt att starta eller utlösa ett Forms-centrerat arbetsflöde är genom program i AEM Inbox. Du måste skapa ett arbetsflödesprogram för att göra en Forms Workflow tillgänglig som ett program i Inbox. Mer information om arbetsflödesprogram och andra sätt att starta Forms-arbetsflöden finns i [Starta ett Forms-orienterat arbetsflöde i OSGi](aem-forms-workflow.md#launch).

Dessutom konsoliderar AEM Inbox meddelanden och uppgifter från olika AEM-komponenter, inklusive Forms-arbetsflöden. När en Forms Workflow som innehåller ett tilldelningssteg aktiveras, visas det associerade programmet som en uppgift i den tilldelades inkorg. Om den som tilldelats är en grupp visas uppgiften i Inkorgen för alla gruppmedlemmar tills en enskild person gör anspråk på eller delegerar uppgiften.

Användargränssnittet i Inkorgen innehåller lista- och kalendervyer för att visa uppgifter. Du kan också konfigurera visningsinställningarna. Du kan filtrera uppgifter baserat på olika parametrar. Mer information om visning och filter finns i [Inkorgen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html?lang=sv-SE#inbox-in-the-header).

Sammanfattningsvis kan du i Inkorgen skapa ett program och hantera tilldelade uppgifter.

>[!NOTE]
>
>Du måste vara medlem i gruppen [!DNL workflow-users] för att kunna använda AEM Inbox.

## Skapa program {#create-application}

1. Gå till AEM Inbox på https://&#39;[server]:[port]&#39;/aem/inbox.
1. Välj **[!UICONTROL Create > Application]** i Inkorgsgränssnittet. Sidan Välj program visas.
1. Välj ett program och klicka på **[!UICONTROL Create]**. Det adaptiva formulär som är associerat med programmet öppnas. Fyll i informationen i det adaptiva formuläret och välj **[!UICONTROL Submit]**. Det startar det associerade arbetsflödet och skapar en uppgift i den tilldelades inkorg.

## Hantera uppgifter {#manage-tasks}

När en Forms-arbetsflödesutlösare och du är tilldelad eller en del av den tilldelade gruppen, visas en uppgift i din Inkorg. Du kan visa uppgiftsinformation och utföra tillgängliga åtgärder för uppgiften inifrån Inkorgen.

### Anspråk eller delegera uppgifter {#claim-or-delegate-tasks}

Uppgifter som tilldelas en grupp visas i Inkorgen för alla gruppmedlemmar. Alla gruppmedlemmar kan göra anspråk på den uppgiften eller delegera den till en annan gruppmedlem. Så här gör du:

1. Välj det här alternativet om du vill välja en miniatyrbild av uppgiften. Alternativ för att öppna eller delegera uppgiften visas högst upp.

   ![select-task](assets/select-task.png)

1. Gör något av följande:

   * Välj **[!UICONTROL Delegate]** om du vill delegera uppgiften. Dialogrutan Delegera objekt öppnas. Välj en användare, lägg till en kommentar om du vill och välj **[!UICONTROL OK]**.

   ![delegat](assets/delegate.png)

   * Välj **[!UICONTROL Open]** om du vill göra anspråk på uppgiften. Dialogrutan Tilldela till mig själv öppnas. Välj **[!UICONTROL Proceed]** om du vill göra anspråk på uppgiften. Uppgiften visas med dig som tilldelad i din inkorg.

   ![anspråk](assets/claim.png)

### Visa information och utför åtgärder på uppgifter {#view-details-and-perform-actions-on-tasks}

När du öppnar en uppgift kan du visa uppgiftsinformation och utföra tillgängliga åtgärder. Vilka åtgärder som är tillgängliga för en uppgift definieras i steget Tilldela uppgift i det associerade Forms Workflow-programmet.

1. Välj det här alternativet om du vill välja en miniatyrbild av uppgiften. Alternativ för att öppna eller delegera den valda uppgiften visas högst upp.
1. Välj **Öppna** om du vill visa aktivitetsinformation och tillgängliga åtgärder. Den detaljerade uppgiftsvyn öppnas. I den här vyn kan du visa aktivitetsinformation och agera på en uppgift.

   >[!NOTE]
   >
   >Om en uppgift har tilldelats en grupp måste du göra anspråk på den för att den ska kunna öppnas i detaljerad vy.

![aktivitetsinformation](assets/task-details.png)

Den detaljerade uppgiftsvyn innehåller följande avsnitt:

* Uppgiftsinformation
* Formulär
* Information om arbetsflöde
* Verktygsfältet Åtgärder

#### Uppgiftsinformation {#task-details}

I avsnittet Uppgiftsinformation visas information om uppgiften. Vilken information som visas beror på konfigurationsinställningarna för [Tilldela aktivitetssteg](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html?lang=sv-SE#extending-aem) i arbetsflödet. I exemplet ovan visas beskrivning, status, startdatum och arbetsflöde som används för uppgiften. Det gör det även möjligt att bifoga en fil till uppgiften.

#### Formulär {#form}

Fliken Formulär i området för huvudinnehållet visar eventuella bifogade formulär och fältnivåbilagor.

#### Information om arbetsflöde {#workflow-details}

Fliken Arbetsflödesinformation överst visar förloppet för uppgiften genom olika steg i arbetsflödet. Här visas slutförda, aktuella och väntande faser för uppgiften. Stegen för ett arbetsflöde definieras i [Tilldela uppgiftssteg](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html?lang=sv-SE#extending-aem) i det associerade arbetsflödet.

Fliken visar också aktivitetshistorik för varje slutförd fas i arbetsflödet. Du kan välja **[!UICONTROL View Details]** för en slutförd fas om du vill veta mer om den scenen. Här visas kommentarer, formulär och uppgiftsbilagor, status, start- och slutdatum och så vidare, om uppgiften.

![arbetsflödesinformation](assets/workflow-details.png)

#### Verktygsfältet Åtgärder {#actions-toolbar}

Verktygsfältet Åtgärder visar alla tillgängliga alternativ för uppgiften. Medan Spara, Återställ och Delegera är standardåtgärder konfigureras andra tillgängliga åtgärder i [Tilldela aktivitetssteg](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html?lang=sv-SE#extending-aem). I exemplet ovan har Godkänn och Avvisa konfigurerats i arbetsflödet.

När du arbetar med uppgiften fortsätter den i arbetsflödet.

### Visa slutförda uppgifter {#view-completed-tasks}

I AEM Inbox visas endast aktiva uppgifter. Slutförda uppgifter visas inte i listan. Du kan emellertid använda inkorgsfilter för att filtrera uppgifter baserat på flera parametrar, till exempel uppgiftstyp, status, start- och slutdatum. Så här visar du slutförda uppgifter:

1. I AEM Inbox väljer du ![växlingspanel1](assets/toggle-side-panel1.png) för att öppna filterväljaren.
1. Välj dragspelet **[!UICONTROL Task Status]** och välj **[!UICONTROL Complete]**. Alla slutförda uppgifter visas.

   ![filter](assets/filter.png)

1. Välj om du vill välja en uppgift och klicka på **[!UICONTROL Open]**.

Aktiviteten öppnas och dokumentet eller det adaptiva formuläret som är kopplat till uppgiften visas. För Adaptiv form visar uppgiften det skrivskyddade adaptiva formuläret eller dess PDF Document of Record som konfigurerats på fliken Formulär/Dokument i arbetsflödessteget [Tilldela uppgift](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html?lang=sv-SE#extending-aem).

I avsnittet med aktivitetsinformation visas information om till exempel åtgärd, aktivitetsstatus, startdatum och slutdatum.

![slutförd-aktivitet](assets/completed-task.png)

Fliken **[!UICONTROL Workflow Details]** visar varje steg i arbetsflödet. Välj **[!UICONTROL View details]** om du vill få mer detaljerad information.

![completed-task-workflow](assets/completed-task-workflow.png)

## Felsökning {#troubleshooting-workflows}

### Det går inte att visa objekt relaterade till AEM Workflow i AEM Inbox {#unable-to-see-aem-worklow-items}

En arbetsflödesmodellägare kan inte visa objekt som är relaterade till AEM Workflow i AEM Inbox. Lös problemet genom att lägga till indexen nedan i din AEM-databas och återskapa indexet.

1. Använd någon av följande metoder för att lägga till index:

   * Skapa följande noder i CRX DE på `/oak:index/workflowDataLucene/indexRules/granite:InboxItem/properties` med respektive egenskaper enligt följande tabell:

     | Nod | Egenskap | Typ |
     |---|---|---|
     | sharedWith | sharedWith | STRÄNG |
     | låst | låst | BOOLEAN |
     | returnerade | returnerade | BOOLEAN |
     | allowInboxSharing | allowInboxSharing | BOOLEAN |
     | allowExplicitSharing | allowExplicitSharing | BOOLEAN |


   * Distribuera indexen via ett AEM-paket. Du kan använda ett [AEM Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=sv-SE) -projekt för att skapa ett distribuerbart AEM-paket. Använd följande exempelkod för att lägga till index i ett AEM Archetype-projekt:

   ```Java
      .property("sharedWith", "sharedWith").type(TYPENAME_STRING).propertyIndex()
      .property("locked", "locked").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("returned", "returned").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowInboxSharing", "allowInboxSharing").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowExplicitSharing", "allowExplicitSharing").type(TYPENAME_BOOLEAN).propertyIndex()
   ```

1. [Skapa ett egenskapsindex och ange det till true](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/queries-and-indexing.html?lang=sv-SE#the-property-index).

1. När du har konfigurerat index i CRX DE eller distribuerat via ett paket indexerar du om databasen.
