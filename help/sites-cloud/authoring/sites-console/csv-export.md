---
title: Exportera till CSV
description: Exportera information om sidorna till en CSV-fil på det lokala systemet
exl-id: 818e927e-40b2-4ccb-bfb3-88284ad49829
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 14%

---

# Exportera till CSV {#export-to-csv}

Med **Skapa CSV-rapport** kan du exportera information om dina sidor till en CSV-fil på ditt lokala system.

* Den hämtade filen kallas `export.csv`
* Innehållet beror på de egenskaper du väljer.
* Du kan definiera banan tillsammans med exportens djup.

>[!NOTE]
>
>Hämtningsfunktionen och standarddestinationen för webbläsaren används.

Med guiden **Skapa CSV-export** kan du välja:

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

1. Öppna konsolen **Platser** och navigera till önskad plats om det behövs.
   * Alternativet Skapa **CSV-rapport** är tillgängligt när du bläddrar i **Sites-konsolen** (i listvyn)
   * Det är ett alternativ i listrutan **Skapa**:

     ![Skapa CSV-alternativ](/help/sites-cloud/authoring/assets/csv-create.png)

1. I verktygsfältet väljer du **Skapa** och sedan **CSV-rapport** för att öppna guiden:

   ![CSV-exportalternativ](/help/sites-cloud/authoring/assets/csv-options.png)

1. Välj de egenskaper som ska exporteras.
1. Välj **Skapa**.
   ![Resultatbaserad CSV-export i Excel](/help/sites-cloud/authoring/assets/csv-example.png)
