---
title: DV-certifikat (Domain Validated)
description: Lär dig hantera DV-certifikat (Domain Valided) i Cloud Manager.
exl-id: 7f2c71b6-15c3-4919-9f51-a3e26d0d48d4
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# DV-certifikat (Domain Validated) {#domain-validated-certificates}

Lär dig hantera DV-certifikat (Domain Valided) i Cloud Manager.

>[!NOTE]
>
>Den här funktionen är bara tillgänglig för [det tidiga adopterprogrammet.](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)

## Introduktion {#introduction}

Med Cloud Manager kan du själv skapa och hantera ett DV-SSL-certifikat (Domain Valided). Detta ger er den snabbaste, enklaste och mest kostnadseffektiva lösningen för att skapa en säker webbplats för ert onlineföretag.

Domänvaliderade certifikat är tillgängliga för både [produktion och sandlådeprogram.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## Lägga till en anpassad domän {#adding-domain}

Om du vill lägga till ett domänvaliderat (DV) certifikat måste du först konfigurera din anpassade domän. Processen är i stort sett densamma som beskrivs i dokumentet [Introduktion till anpassade domännamn.](/help/implementing/cloud-manager/custom-domain-names/introduction.md) Men den funktionen har utökats något.

1. När du verifierar domänen kan du välja att använda certifikat som hanteras av Adobe eller självhanterade certifikat med domänen. Välj **hanterat certifikat från Adobe** om du vill lägga till ett DV-certifikat senare.

   ![Välj Adobe-hanterad](assets/verify-domain-dialog.png)

1. Om du vill använda ett certifikat som hanteras av Adobe måste du lägga till en CNAME-post i din DNS enligt beskrivningen i dialogrutan **Verifiera domän**.

   ![Lägg till CNAME-post](assets/verify-domain-dialog-adobe-managed.png)

1. När domänen har skapats trycker eller klickar du på ellipsknappen i listan över domäner och väljer **Verifiera** för att verifiera domänen.

   ![Verifiera domän](assets/verify-domain.png)

## Lägga till ett DV-certifikat {#adding}

När du har konfigurerat din domän korrekt kan du lägga till ett DV-certifikat genom att trycka eller klicka på knappen **Lägg till SSL-certifikat** i fönstret SSL-certifikat.

![Lägger till ett DC-certifikat](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

1. Markera alternativet **Adobe hanterat (DV)**.
1. Ange domännamnet i listrutan **Välj domäner**.
1. Tryck eller klicka på **Spara**.

När certifikatet har lagts till har det en väntande status med ett gult varningstecken i namnet i fönstret **SSL-certifikat** .

![Väntande DV-certifikat](assets/pending-dv-certificate.png)

När certifikatet har utfärdats har det en grön bockmarkering i fönstret **SSL-certifikat**.

![Utfärdat DV-certifikat](assets/issued-dv-certificate.png)

Mer information om hur du lägger till SSL-certifikat och SSL-certifikatfönstret finns i dokumentet [Lägga till ett SSL-certifikat.](add-ssl-certificate.md)

## Lägg till CDN-konfiguration {#add-cdn}

Detta steg måste slutföras för att en domän med en SSL ska kunna konfigureras med Fast CDN.

Följ de här stegen för att lägga till en CDN-konfiguration med Cloud Manager.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj fliken **CDN-konfigurationer** och klicka eller tryck på **Lägg till** i verktygsfältet.

1. Ange nödvändig information i dialogrutan **Konfigurera CDN**.

   * Välj **Ursprung**. Detta kan vara:
      * En Cloud Service-miljö
      * En Edge Delivery Services-webbplats
   * Välj CDN-typ.
   * Markera domänen.
   * Välj SSL-certifikatet.
      * Krävs endast för CDN som hanteras av Adobe.

   ![Konfigurera CDN-dialogrutan](assets/configure-cdn-dialog.png)

>
>
>För CDN:er som hanteras av Adobe tillåts endast webbplatser med ACME-validering när DV-certifikat används.
