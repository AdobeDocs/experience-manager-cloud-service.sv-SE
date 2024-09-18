---
title: Hantera anpassade domännamn
description: Lär dig hur du använder Cloud Manager för att visa, uppdatera, ersätta och ta bort anpassade domännamn.
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8e2fc0d4ee82e79d1a822a528b1a46acce3c192a
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---


# Hantera anpassade domännamn {#managing-custom-domain-names}

Med Cloud Manager kan du redigera, uppdatera, ersätta och ta bort egna domännamn.

## Redigera en anpassad domännamnskonfiguration {#view-and-update}

I Adobe Cloud Manager kanske du vill redigera en anpassad domännamnskonfiguration av följande skäl:

* **Växlingsmiljöer**: Om du vill använda rätt konfiguration beroende på om du levererar innehåll till slutanvändare (Publish) eller interna användare (författare).
* **Säkerhetsuppdateringar**: Om du vill uppgradera till ett nyare SSL-certifikat för förbättrad säkerhet eller kompatibilitet.
* **Ändrar distributionsstrategi**: För att säkerställa att rätt SSL-certifikat tillämpas på en viss miljö för korrekt kryptering och webbplatsåtkomst.

**Så här redigerar du en anpassad domännamnskonfiguration:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. I det övre vänstra hörnet av sidan klickar du på hamburgikonen för att visa den vänstra navigeringsmenyn.
1. Klicka på **CDN-konfigurationer** under rubriken **Tjänster**.
1. På sidan **CDN-konfigurationer** klickar du på ellipsen i slutet av en rad vars CDN du vill redigera.
1. Klicka på **Redigera**.
1. Gör följande i dialogrutan **Redigera CDN-konfiguration**:
   * I listrutan **Nivå** väljer du den nivå (Författare eller Publish) som du vill använda.
   * Välj det SSL-certifikat som du vill använda i listrutan **SSL-certifikat**.
1. Klicka på **Uppdatera**.


## Uppdatera ett anpassat domännamns SSL-certifikat {#update-cert}

Du kan följa [samma steg för att visa och uppdatera ett anpassat domännamn](#view-and-update) för att uppdatera ett anpassat domännamns SSL-certifikat.

>[!NOTE]
>
>SSL-certifikatet måste vara giltigt, [redan konfigurerat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md), och innehålla det anpassade domännamn som du uppdaterar.


## Ta bort ett anpassat domännamn {#deleting}

En användare med rollen **Business Owner** eller **Deployment Manager** kan använda Cloud Manager för att ta bort ett anpassat domännamn.

### Ta bort ett anpassat domännamn från alla associerade miljöer {#delete-cdn-all}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Gå till sidan **Domäninställningar** från skärmen **Översikt**.

1. Identifiera raden med det anpassade domännamn som du vill ta bort.

1. Klicka på ellipsknappen längst till höger på raden.

1. Välj **Ta bort**.

1. Bekräfta ditt bidrag.


### Ta bort ett anpassat domännamn från en viss miljö {#delete-cdn-specific}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.
1. Gå till skärmen **Miljö** från sidan **Översikt**.
1. Navigera från sidan **Miljö** till en informationsskärm om den miljö som är av intresse.
1. Identifiera raden med det anpassade domännamnet som du vill ta bort i tabellen över domännamn.
1. Klicka på ellipsknappen längst till höger på raden.
1. Välj **Ta bort**.
1. Bekräfta ditt bidrag.
