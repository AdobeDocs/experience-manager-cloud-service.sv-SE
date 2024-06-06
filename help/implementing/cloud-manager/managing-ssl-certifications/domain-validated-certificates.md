---
title: DV-certifikat (Domain Validated)
description: Lär dig hantera DV-certifikat (Domain Valided) i Cloud Manager.
source-git-commit: 5baeb4012e5aa82a8cd8710b18d9164583ede0bd
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---


# DV-certifikat (Domain Validated) {#domain-validated-certificates}

Lär dig hantera DV-certifikat (Domain Valided) i Cloud Manager.

>[!NOTE]
>
>Den här funktionen är bara tillgänglig för [det tidiga adopteringsprogrammet.](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)

## Introduktion {#introduction}

Med Cloud Manager kan du själv skapa och hantera ett DV-SSL-certifikat (Domain Valided). Detta ger er den snabbaste, enklaste och mest kostnadseffektiva lösningen för att skapa en säker webbplats för ert onlineföretag.

Domänvaliderade certifikat är tillgängliga för båda [produktion och sandlådeprogram.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## Lägga till en anpassad domän {#adding-domain}

Om du vill lägga till ett domänvaliderat (DV) certifikat måste du först konfigurera din anpassade domän. Processen är i stort sett densamma som beskrivs i dokumentet [Introduktion till anpassade domännamn.](/help/implementing/cloud-manager/custom-domain-names/introduction.md) Den funktionen har dock utökats något.

1. När du verifierar domänen kan du välja att använda certifikat som hanteras av Adobe eller självhanterade certifikat med domänen. Välj **Adobe-hanterat certifikat** för att lägga till ett DV-certifikat senare.

   ![Välj Adobe-hanterad](assets/verify-domain-dialog.png)

1. Om du vill använda ett certifikat som hanteras av Adobe måste du lägga till en CNAME-post i din DNS enligt beskrivningen i **Verifiera domän** -dialogrutan.

   ![Lägg till CNAME-post](assets/verify-domain-dialog-adobe-managed.png)

1. När domänen har skapats trycker eller klickar du på ellipsknappen i listan över domäner och väljer **Verifiera** för att verifiera domänen.

   ![Verifiera domän](assets/verify-domain.png)

## Lägga till ett DV-certifikat {#adding}

När du har konfigurerat din domän korrekt kan du lägga till ett DV-certifikat genom att trycka eller klicka på **Lägg till SSL-certifikat** i SSL Certificates-fönstret.

![Lägga till ett DC-certifikat](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

1. Välj alternativet **Hanterad av Adobe (DV)**.
1. Ange domännamnet i dialogrutan **Välj domäner** nedrullningsbar meny.
1. Tryck eller klicka **Spara**.

När certifikatet har lagts till har det en väntande status med ett gult varningstecken i namnet i **SSL-certifikat** -fönstret.

![Väntande DV-certifikat](assets/pending-dv-certificate.png)

När certifikatet har utfärdats markeras det med en grön bock i **SSL-certifikat** -fönstret.

![Utfärdat DV-certifikat](assets/issued-dv-certificate.png)

Mer information om hur du lägger till SSL-certifikat och SSL-certifikatfönstret finns i dokumentet [Lägger till ett SSL-certifikat.](add-ssl-certificate.md)

## Lägg till CDN-konfiguration {#add-cdn}

Detta steg måste slutföras för att en domän med en SSL ska kunna konfigureras med Fast CDN.

Följ de här stegen för att lägga till en CDN-konfiguration med hjälp av Cloud Manager.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation.

1. Välj **CDN-konfigurationer** och klicka eller peka **Lägg till** i verktygsfältet.

1. I **Konfigurera CDN** kan du ange nödvändig information.

   * Välj **Ursprung**. Detta kan vara:
      * En Cloud Service-miljö
      * En Edge Delivery Services-webbplats
   * Välj CDN-typ.
   * Markera domänen.
   * Välj SSL-certifikatet.
      * Krävs endast för CDN som hanteras av Adobe.

   ![Konfigurera CDN-dialogruta](assets/configure-cdn-dialog.png)

>
>
>För CDN:er som hanteras av Adobe tillåts endast webbplatser med ACME-validering när DV-certifikat används.
