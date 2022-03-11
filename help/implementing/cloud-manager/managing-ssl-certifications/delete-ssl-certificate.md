---
title: Ta bort ett SSL-certifikat - Hantera SSL-certifikat
description: Ta bort ett SSL-certifikat - Hantera SSL-certifikat
exl-id: 43f66871-cca4-4709-95d0-68aa715c0da2
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# Ta bort ett SSL-certifikat {#deleting-an-ssl-certificate}

>[!IMPORTANT]
>Att ta bort certifikat från Cloud Manager är en permanent åtgärd som inte kan ångras. Det bästa sättet är att spara alla nödvändiga SSL-filer lokalt innan de tas bort i användargränssnittet i Cloud Manager.

En användare måste ha rollen Business Owner eller Deployment Manager för att kunna ta bort ett SSL-certifikat i Cloud Manager. I Cloud Manager kan du inte ta bort ett SSL-certifikat som har en eller flera domäner kopplade till sig.  Alla associerade domäner måste tas bort innan SSL-certifikatet tas bort. Se [Ta bort ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) om du vill veta mer.

Följ stegen nedan för att ta bort ett SSL-certifikat:

1. Navigera till **SSL-certifikat** från **Miljö** sida.
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)
1. Identifiera raden där det SSL-certifikatnamn du vill ta bort finns med.
1. Välj **...** menyn längst till höger på raden.
1. Välj **Ta bort**.
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete01.png)
1. Bekräfta ditt bidrag från **Ta bort SSL-certifikat** -dialogrutan.
