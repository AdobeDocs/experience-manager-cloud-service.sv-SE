---
title: Lägga till ett anpassat domännamn
description: Lägga till ett anpassat domännamn
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 98c137645351c86da8680a31b4929c588863a981
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---

# Lägga till ett anpassat domännamn {#adding-cdn}

En användare måste vara en Business Owner eller Deployment Manager för att kunna lägga till ett anpassat domännamn i Cloud Manager.

Följande steg skall utföras enligt tabellen nedan:

| Steg |  | Ansvarsområde | Läs mer |
|--- |--- |--- |---|
| Lägg till SLL-certifikat | Lägg till SLL-certifikat | Kund | [Lägga till ett SSL-certifikat](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) |
| Domänverifiering | Lägg till TXT-post | Kund | [Lägga till en TXT-post](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-text-record.html?lang=en) |
| Verifieringsstatus för domän |  | Kund |  |
|  | Status: Domänverifieringsfel | Kund | [Kontrollerar domännamnsstatus](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
|  | Status: Verifierad, distributionen misslyckades | Kontakta Adobe | [Kontrollerar domännamnsstatus](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
| Lägg till DNS-poster som pekar på AEM as a Cloud Service genom att lägga till CNAME- eller APEX-poster | Konfigurera DNS-inställningar | Kund | [Konfigurera DNS-inställningar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/configure-dns-settings.html?lang=en) |
| Kontrollera DNS-poststatus |  | Kund | [Kontrollerar DNS-poststatus](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | Status: DNS-status kunde inte hittas | Kund | [Kontrollerar DNS-poststatus](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | Status: DNS matchas felaktigt | Kund |  |


## Viktiga överväganden {#important-considerations}

* Innan du lägger till ett anpassat domännamn måste ett giltigt SSL-certifikat som innehåller det anpassade domännamnet installeras i ditt program. Se [Lägga till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) om du vill veta mer.

* Det går inte att lägga till domännamn i miljöer när det finns en aktuell pågående pipeline som är kopplad till dessa miljöer.

* Det går bara att lägga till ett domännamn åt gången. Anpassade domäner på författarsidan stöds inte.

* AEM as a Cloud Service stöder inte jokerteckendomäner.

* Varje Cloud Manager-miljö har plats för upp till 500 anpassade domäner per miljö.

* Samma domännamn kan inte användas i mer än en miljö.

## Lägga till ett anpassat domännamn från sidan Domäninställningar {#adding-cdn-settings}

Följ stegen nedan för att lägga till ett anpassat domännamn från sidan Domäninställningar:

1. Navigera till **Miljö** skärmbild från **Översikt** sida.

1. Klicka på **Domäninställningar** från den vänstra navigeringsmenyn.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Klicka på **Lägg till domän** knapp att öppna **Lägg till domännamn** -dialogrutan.

   ![](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. Ange det anpassade domännamnet i **Domännamn**.

   >[!NOTE]
   >Du bör inte inkludera `http://`, `https://`eller blanksteg när du anger i domänen.

1. Välj **Miljö** vars publiceringstjänst ska kopplas till domännamnet.

1. Välj tjänsten antingen som **Publicera** eller **Förhandsgranska**.

   >[!NOTE]
   >Anpassade domännamn stöds nu i Cloud Manager för webbplatser-program för både publicerings- och förhandsgranskningstjänster. Varje Cloud Manager-miljö har plats för upp till 500 anpassade domäner per miljö. Mer information om förhandsgranskningstjänsten finns i [Förhandsgranskningstjänst](/help/implementing/cloud-manager/manage-environments.md#preview-service).

1. Välj **Domän-SSL-certifikat** i listrutan och välj **Fortsätt**.

1. **Lägg till domännamn** visas. Du kommer nu till Verifiering av domännamn för miljöskärmen. Se [Lägga till en TXT-post](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) om du vill veta mer.

   Följ instruktionerna för att bevisa domänägarskap för din miljö:

1. Klicka på **Skapa**.
1. CDN-distributionen kräver ett giltigt SSL-certifikat och lyckad TXT-verifiering. Detta anges av statusen **Verifierat och distribuerat**.
Navigera till [Kontrollerar status för anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) om du vill veta mer om olika statusar och hur du kan ta itu med dem.

   >[!NOTE]
   >Det kan ta upp till några timmar att identifiera DNS-bevis på grund av fördröjd DNS-spridning. Cloud Manager kontrollerar ägarskap och uppdaterar statusen som visas i tabellen Domäninställningar. Mer information finns i Kontrollera domännamnsstatus.

## Lägga till ett anpassat domännamn från miljösidan {#adding-cdn-environments}

1. Navigera till miljöinformationssidan för att se om miljön är av intresse.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Använd indatafälten högst upp i tabellen Domännamn för att skicka det anpassade domännamnet och välj SSL-certifikatet i listrutan. Klicka på **+ Lägg till**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Kontrollera fälten från **Lägg till domännamn** och klicka **Fortsätt**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >Inkludera inte `http://`, `https://`eller blanksteg när du anger i domänen.

1. Domännamnsverifiering för din miljöskärm visas.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   Se [Domänverifiering](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) om du vill veta mer. Följ instruktionerna som följer för att bevisa att du är domänägare i din miljö.

1. Klicka på **Skapa**.

1. Distributionen av det anpassade domännamnet kräver ett giltigt SSL-certifikat och en lyckad TXT-verifiering. Detta anges av statusen **Verifierat och distribuerat**.

Nu är ditt anpassade domännamn klart för testning och en `CNAME` för att peka på det. Se [Domännamnsstatus](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) om du vill veta mer om olika statusar och hur du kan ta itu med dem.

>[!NOTE]
>Det kan ta upp till några timmar att identifiera DNS-bevis på grund av fördröjd DNS-spridning. Cloud Manager kontrollerar ägarskap och uppdaterar statusen som visas i tabellen Domäninställningar. Mer information finns i Kontrollera domännamnsstatus.
