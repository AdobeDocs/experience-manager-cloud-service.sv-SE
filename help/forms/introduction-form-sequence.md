---
title: Hur skapar man en formulärsekvens i flera steg?
description: 'Med [!DNL Experience Manager Forms]kan du definiera en sekvens med formulärpaneler så att användarna kan navigera och fylla i ett anpassat formulär. Gå ett steg längre genom att använda fallbaserad metod som exempel för att skapa formulärsekvenser i flera steg. '
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 6b3f9131-db6b-451b-a932-b57d809222eb
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# Introduktion till formulärsekvenser i flera steg {#introduction-to-multi-step-form-sequence}

Med adaptiva Forms kan man enkelt skapa datainhämtning i flera steg. Den har inbyggt stöd för att skapa flera paneler och koppla ihop varje panel med olika navigeringsmönster. Formulärförfattare kan gruppera formulärfält i logiska avsnitt och representera en grupp som en panel. Den övergripande navigeringen mellan paneler styrs med hjälp av panellayouten. Författare kan välja att ordna paneler i olika layouter, t.ex. placera sekventiellt med hjälp av guidelayouten eller på ett tillfälligt sätt med hjälp av fliklayouten. Mer information om panellayouter finns i [Layoutfunktioner i Adaptive Forms](layout-capabilities-adaptive-forms.md).

I en typisk miljö för ifyllnad av formulär finns det fler steg än att bara hämta in data. En fullständig inlämning av formulär kan omfatta andra steg, som att signera formuläret digitalt, verifiera den information som fylls i formuläret, bearbeta betalningar och så vidare. Det skiljer sig från fall till fall.

Om ditt användningsfall kräver en uppsättning steg för datainhämtning eller det finns bestämmelser som kräver att vissa steg följs, [!DNL Experience Manager Forms] ger ett sätt att genomdriva den gemensamma strukturen i alla formulär. Den medföljande implementeringen av formulärstrukturen definierar stegsekvensen för ett formulär. ![Exempel på en formulärsekvens i flera steg](assets/formpipeline.png)

Exempel på en formulärsekvens i flera steg

Låt oss ta ett exempel där du måste skapa en sekvens för att fylla i, verifiera, signera och bekräfta ett formulär. Så här skapar du en sådan sekvens:

1. Definiera en formulärmall och lägg till en obligatorisk panel i den. Det ska finnas en panel för varje steg i sekvensen. Du kan dock inkludera underpaneler inuti en panel.

   I det här exemplet kan vi lägga till följande paneler:

   * **[!UICONTROL Fill]**: Den innehåller formulärfält för datainhämtning. Här kan du ta med kapslade underpaneler för att skapa avsnitt för olika typer av information, t.ex. personlig, familj, ekonomi osv.

   <!--* **[!UICONTROL Verify]**: It contains the **[!UICONTROL Verify]** component that can be used in an XFA-based Adaptive Form. It displays the information captured in the Fill panel in read-only mode for verification.-->


   * **[!UICONTROL E-sign]**: Den innehåller **[!UICONTROL Sign]** som kan användas i en XFA-baserad adaptiv form. Den tillhandahåller följande signeringstjänster:

      * Adobe Document Cloud eSign-tjänster
      * Klottra signaturer
   * **[!UICONTROL Confirmation]**: Den innehåller **[!UICONTROL Summary]** som visar ett meddelande som bekräftar att formuläret skickas när en användare har signerat formuläret och når steget Bekräfta (Sammanfattning) i sekvensen. Författare kan konfigurera texten i [!UICONTROL Summary] , visa ett tackmeddelande, visa en länk till det genererade PDF och så vidare.



1. Välj layouten för rotpanelen som **[!UICONTROL Wizard]**.
1. Slutför de återstående stegen för att skapa formulärmallen. <!-- For more information, see [Creating a custom Adaptive Form template](custom-adaptive-forms-templates.md). -->

När du har definierat formulärsekvensen i formulärmallen kan du använda den för att skapa formulär som har den grundläggande strukturen definierad som sekvensen på plats, även om du alltid kan anpassa formuläret efter dina behov.
