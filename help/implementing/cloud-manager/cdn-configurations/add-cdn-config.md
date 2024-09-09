---
title: Lägg till en CDN-konfiguration
description: Lär dig hur du lägger till en CDN-konfiguration för en Edge Delivery-webbplats eller en Cloud Manager-miljö.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: e57a6ceb2482e61acabe928da0f539d26989985c
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# Lägga till en CDN-konfiguration {#add-cdn}

Du måste lägga till en CDN-konfiguration för att kunna konfigurera en domän med en SSL.

>
>
>För CDN:er som hanteras av Adobe tillåts endast webbplatser med ACME-validering när DV-certifikat används.

**Så här lägger du till en CDN-konfiguration:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Klicka på **CDN-konfigurationer**.

1. Klicka på **Lägg till** i det övre högra hörnet på sidan CDN-konfigurationer.

   ![Konfigurera CDN-dialogruta](/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)

1. Ange nödvändig information i dialogrutan **Konfigurera CDN**.

   * Gör något av följande i listrutan **Ursprung**:
      * **Platser:** Markera en Edge Delivery Services-plats.
      * **Miljö:** Markera en Cloud Service-miljö.
         * **Nivå:** Välj en **Publish** - eller **Förhandsgranska**-webbnivå för den valda miljön.
   * Välj din CDN-typ: **CDN som hanteras av Adobe** eller **Annan CDN-provider**.
   * Markera domänen.
   * Välj SSL-certifikatet. Krävs endast om du har valt **CDN** som Adobe som CDN-typ.

1. Klicka på **Spara**.




