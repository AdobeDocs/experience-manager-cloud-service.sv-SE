---
title: Exportera till CSV
description: Exportera information om sidorna till en CSV-fil på det lokala systemet
exl-id: 818e927e-40b2-4ccb-bfb3-88284ad49829
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 18%

---

# Exportera till CSV {#export-to-csv}

**Skapa CSV-rapport** Med kan du exportera information om sidorna till en CSV-fil på det lokala systemet.

* Den hämtade filen anropas `export.csv`
* Innehållet beror på de egenskaper du väljer.
* Du kan definiera banan tillsammans med exportens djup.

>[!NOTE]
>
>Hämtningsfunktionen och standarddestinationen för webbläsaren används.

The **Skapa CSV-export** kan du välja:

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

Resultatet `export.csv` filen kan öppnas i Excel eller något annat kompatibelt program.

Så här skapar du en CSV-export:

1. Öppna **Webbplatser** navigera till önskad plats om det behövs.
   * Alternativet Skapa **CSV-rapport** är tillgängligt när du bläddrar i **Sites-konsolen** (i listvyn)
   * Det är ett alternativ i **Skapa** nedrullningsbar meny:

     ![Alternativet Skapa CSV](/help/sites-cloud/authoring/assets/csv-create.png)

1. I verktygsfältet väljer du **Skapa** och sedan **CSV-rapport** för att öppna guiden:

   ![CSV-exportalternativ](/help/sites-cloud/authoring/assets/csv-options.png)

1. Välj de egenskaper som ska exporteras.
1. Välj **Skapa**.
   ![Resultat av CSV-export i Excel](/help/sites-cloud/authoring/assets/csv-example.png)
