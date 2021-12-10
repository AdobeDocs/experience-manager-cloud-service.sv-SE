---
title: Hur konfigurerar jag Azure-lagring?
description: Lär dig hur du integrerar formulär med Azure-lagringsservern.
exl-id: 606383b3-293c-43d2-9ba0-5843c4e0caa8
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---

# Konfigurera [!DNL Azure] lagring {#configure-azure-storage}

[[!DNL Experience Manager Forms] Dataintegrering](data-integration.md) ger en [!DNL Azure] lagringskonfiguration för att integrera formulär med [!DNL Azure] lagringstjänster. Formulärdatamodellen kan användas för att skapa adaptiv Forms som interagerar med [!DNL Azure] för att möjliggöra arbetsflöden. Till exempel:

* Skriv data i [!DNL Azure] om inlämning av anpassade blanketter.
* Skriv data i [!DNL Azure] via anpassade entiteter som definierats i formulärdatamodellen och vice versa.
* Fråga [!DNL Azure] för data och förifylla Adaptive Forms.
* Läs data från [!DNL Azure] server.

## Skapa [!DNL Azure] lagringskonfiguration {#create-azure-storage-configuration}

Innan du utför dessa steg måste du se till att du har en [!DNL Azure] lagringskonto och en åtkomstnyckel för att auktorisera åtkomst till [!DNL Azure] lagringskonto.

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure Storage]**.
1. Välj en mapp för att skapa konfigurationen och tryck på **[!UICONTROL Create]**.
1. Ange en rubrik för konfigurationen i dialogrutan **[!UICONTROL Title]** fält.
1. Ange namnet på [!DNL Azure] lagringskonto i **[!UICONTROL Azure Storage Account]** fält.
1. Ange nyckeln för åtkomst till Azure-lagringskontot i **[!UICONTROL Azure Access Key]** fält och knacka **[!UICONTROL Save]**.

## Skapa formulärdatamodell {#create-azure-form-data-model}

När du har skapat [!DNL Azure] lagringskonfiguration kan du [skapa formulärdatamodellen](create-form-data-models.md). Ange mappen som innehåller [!DNL Azure] i **[!UICONTROL Data Source Configuration]** när formulärdatamodellen skapades. Du kan sedan välja konfigurationen från listan med konfigurationer som finns i det angivna mappnamnet.

### Lägg till [!DNL Azure] tjänster till formulärdatamodellen {#add-azure-services}

När du har skapat objekten för formulärdatamodell och datamodell kan du lägga till [!DNL Azure] till formulärdatamodellen.

Lägg till [!DNL Azure] tjänster:

1. I redigeringsläget väljer du tjänsterna i **[!UICONTROL Services]** till vänster och tryck **[!UICONTROL Add Selected]**. De valda tjänsterna visas i **[!UICONTROL Services]** -fliken i formulärdatamodellen.

   ![Lägg till markerade tjänster](assets/select-services.png)

1. I **[!UICONTROL Services]** väljer du tjänsten och **[!UICONTROL Edit Properties]**. Definiera tjänstens in- eller utdatamodellsobjekt baserat på tjänsten.

1. Tryck **[!UICONTROL Save]** för att spara formulärdatamodellen.

   Följande tabell beskriver tillgängliga [!DNL Azure] tjänster:

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
      <td>Hämta en lista med blob-ID:n från Azure baserat på numret som definierats i indatabegäran.</td>
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

1. I **[!UICONTROL Model]** väljer du datamodellens objektegenskap och trycker **[!UICONTROL Edit Properties]**.
1. Byt **[!UICONTROL Search Key]** växla till ON-läge. Det här alternativet är bara tillgängligt för primära datatyper.
1. Tryck **[!UICONTROL Done]** och sedan trycka **[!UICONTROL Save]** för att spara formulärdatamodellen.

När du har definierat objektegenskaper för datamodell som söknycklar sparas nycklarna som metadata i Azure-lagringen.
