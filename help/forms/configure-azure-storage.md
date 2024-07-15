---
title: Hur konfigurerar jag Azure-lagring?
description: Lär dig hur du integrerar formulär med Azure-lagringsservern.
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 606383b3-293c-43d2-9ba0-5843c4e0caa8
source-git-commit: 7b31a2ea016567979288c7a8e55ed5bf8dfc181d
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---

# Konfigurera [!DNL Azure]-lagring {#configure-azure-storage}


![dataintegrering](assets/data-integeration.png)

[[!DNL Experience Manager Forms] Dataintegrering](data-integration.md) tillhandahåller en [!DNL Azure] lagringskonfiguration för att integrera formulär med [!DNL Azure] lagringstjänster. Formulärdatamodellen (FDM) kan användas för att skapa adaptiv Forms som interagerar med [!DNL Azure]-servern för att aktivera affärsarbetsflöden. Till exempel:

* Skriv data i [!DNL Azure] när adaptiva formulär skickas.
* Skriv data i [!DNL Azure] via anpassade entiteter som definierats i formulärdatamodellen (FDM) och omvänt.
* Fråga [!DNL Azure]-servern efter data och fylla i Adaptiv Forms i förväg.
* Läs data från servern [!DNL Azure].

## Skapa lagringskonfiguration för [!DNL Azure] {#create-azure-storage-configuration}

Innan du utför de här stegen måste du se till att du har ett [!DNL Azure]-lagringskonto och en åtkomstnyckel för att auktorisera åtkomst till lagringskontot [!DNL Azure].

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure Storage]**.
1. Välj en mapp för att skapa konfigurationen och välj **[!UICONTROL Create]**.
1. Ange en rubrik för konfigurationen i fältet **[!UICONTROL Title]**.
1. Ange namnet på lagringskontot [!DNL Azure] i fältet **[!UICONTROL Azure Storage Account]**.
1. Ange nyckeln för åtkomst till Azure-lagringskontot i fältet **[!UICONTROL Azure Access Key]** och välj **[!UICONTROL Save]**.

## Skapa formulärdatamodell {#create-azure-form-data-model}

När du har skapat lagringskonfigurationen [!DNL Azure] kan du [skapa formulärdatamodellen](create-form-data-models.md). Ange mappen som innehåller konfigurationen [!DNL Azure] i fältet **[!UICONTROL Data Source Configuration]** när du skapar formulärdatamodellen (FDM). Du kan sedan välja konfigurationen från listan med konfigurationer som finns i det angivna mappnamnet.

### Lägg till [!DNL Azure] tjänster i formulärdatamodellen {#add-azure-services}

När du har skapat formulärets datamodell (FDM) och datamodellsobjekt kan du lägga till [!DNL Azure]-tjänster i formulärdatamodellen (FDM).

Så här lägger du till [!DNL Azure] tjänster:

1. I redigeringsläget markerar du tjänsterna i avsnittet **[!UICONTROL Services]** i den vänstra rutan och väljer **[!UICONTROL Add Selected]**. De valda tjänsterna visas på fliken **[!UICONTROL Services]** i FDM (Form Data Model).

   ![Lägg till markerade tjänster](assets/select-services.png)

1. Markera tjänsten och **[!UICONTROL Edit Properties]** på fliken **[!UICONTROL Services]**. Definiera tjänstens in- eller utdatamodellsobjekt baserat på tjänsten.

1. Välj **[!UICONTROL Save]** om du vill spara formulärdatamodellen (FDM).

   I följande tabell beskrivs de tillgängliga [!DNL Azure]-tjänsterna:

   <table>
    <tbody>
     <tr>
      <th><strong>Tjänstnamn</strong></th>
      <th><strong>Beskrivning</strong></th>
     </tr>
     <tr>
      <td>Hämta blob från Azure</td>
      <td>Hämta data som lagrats som en blob i Azure-lagringen med ett ID eller ett namn</td>
     </tr>
     <tr>
      <td>Hämta blob med binär URL från Azure</td>
      <td>Hämta data lagrade som en blob med URL för binärfiler i Azure-lagringsplatsen med ett ID eller ett namn</td>
     </tr>
     <tr>
      <td>Spara blob i Azure</td>
      <td>Använd ett blob-ID för att spara data i Azure-lagringen</td>
     </tr>
     <tr>
      <td>Uppdatera blob i Azure</td>
      <td>Använd ett blob-ID för att uppdatera data i Azure-lagringen</td>
     </tr>
     <tr>
      <td>Hämta lista över blob-ID:n från Azure</td>
      <td>Hämta en lista med blob-ID:n från Azure baserat på det nummer som har definierats i indatabegäran.</td>
     </tr>
     <tr>
      <td>Hämta SAS-URL:er för Blobs från Azure</td>
      <td>Hämta SAS-URL:er för Blobs från Azure baserat på Blob ID:n i indatabegäran.</td>
     </tr>
     <tr>
      <td>Ta bort blob från Azure</td>
      <td>Använd ett blob-ID för att ta bort data från Azure-lagring</td>
     </tr>
    </tbody>
   </table>

### Definiera en datamodellsobjektegenskap som en söknyckel {#define-data-model-object-as-metadata}

Så här definierar du en objektegenskap för datamodell som en söknyckel:

1. Markera datamodellens objektegenskap på fliken **[!UICONTROL Model]** och välj **[!UICONTROL Edit Properties]**.
1. Växla alternativet **[!UICONTROL Search Key]** till PÅ-läge. Det här alternativet är bara tillgängligt för primära datatyper.
1. Välj **[!UICONTROL Done]** och välj sedan **[!UICONTROL Save]** för att spara FDM (Form Data Model).

När du har definierat egenskaper för datamodellsobjekt som söknycklar lagras hash-värdena i Azure-indextaggar och Base64-kodade värden lagras i Azure-metadata.

>[!NOTE]
>
>Endast 10 söknycklar tillåts per Azure-enhet eftersom Azure bara tillåter 10 taggar per blob och egenskapsvärden som markerats som söknycklar lagras i Azure-indextaggar efter hashning.

<!--

>[!MORELIKETHIS]
>
>* [Configure data sources for AEM Forms](/help/forms/configure-data-sources.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)
>  [Add Forms Portal to an AEM Sites page](/help/forms/configure-forms-portal.md)

-->