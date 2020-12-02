---
title: Exportera till CSV
description: Exportera information om sidorna till en CSV-fil på det lokala systemet
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 29%

---


# Exportera till CSV {#export-to-csv}

**Med Skapa CSV-** rapporter kan du exportera information om dina sidor till en CSV-fil på ditt lokala system.

* Den hämtade filen heter `export.csv`
* Innehållet beror på de egenskaper du väljer.
* Du kan definiera banan tillsammans med exportens djup.

>[!NOTE]
>
>Hämtningsfunktionen och standarddestinationen för webbläsaren används.

I guiden **Skapa CSV-export** kan du välja:

* Egenskaper att exportera
   * Metadata
      * Namn
      * Ändrad
      * Publicerad
      * Mall
      * Arbetsflöde
   * Översättning
      * Översatt
   * Analyser
      * Sidvyer
      * Unika besökare
      * Tid på sidan
* Djup
   * Överordnad sökväg
   * Endast direktunderordnade
   * Ytterligare nivåer av barn
   * Nivåer

Den resulterande `export.csv`-filen kan öppnas i Excel eller något annat kompatibelt program.

Så här skapar du en CSV-export:

1. Öppna konsolen **Sites** och navigera till önskad plats om det behövs.
   * Alternativet Skapa **CSV-rapport** är tillgängligt när du bläddrar i **Sites-konsolen** (i listvyn)
   * Det är ett alternativ i listrutan **Skapa**:

      ![Alternativet Skapa CSV](/help/sites-cloud/authoring/assets/csv-create.png)

1. I verktygsfältet väljer du **Skapa** och sedan **CSV-rapport** för att öppna guiden:

   ![CSV-exportalternativ](/help/sites-cloud/authoring/assets/csv-options.png)

1. Välj de egenskaper som ska exporteras.
1. Välj **Skapa**.
   ![Resultat av CSV-export i Excel](/help/sites-cloud/authoring/assets/csv-example.png)
