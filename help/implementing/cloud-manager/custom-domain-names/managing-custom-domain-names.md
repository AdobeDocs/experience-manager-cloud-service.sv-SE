---
title: Hantera anpassade domännamn
description: Lär dig hur du använder Cloud Manager för att visa, uppdatera, ersätta och ta bort anpassade domännamn.
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: bf519f03b9be56c46c1ca04420169eaf221478cc
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---


# Hantera anpassade domännamn {#managing-custom-domain-names}

Med Cloud Manager kan du redigera, uppdatera, ersätta, verifiera och ta bort anpassade domännamn.

## Redigera en anpassad domännamnskonfiguration {#view-and-update}

I Adobe Cloud Manager kanske du vill redigera en anpassad domännamnskonfiguration av följande skäl:

* **Växlingsmiljöer**: Om du vill använda rätt konfiguration beroende på om du levererar innehåll till slutanvändare (Publicera) eller interna användare (Författare).
* **Säkerhetsuppdateringar**: Om du vill uppgradera till ett nyare SSL-certifikat för förbättrad säkerhet eller kompatibilitet.
* **Ändrar distributionsstrategi**: För att säkerställa att rätt SSL-certifikat tillämpas på en viss miljö för korrekt kryptering och webbplatsåtkomst.

**Så här redigerar du en anpassad domännamnskonfiguration:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Klicka på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i det övre vänstra hörnet på sidan för att visa den vänstra menyn.

1. Klicka på ikonen **Sociala nätverk** ![Domänmappningar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) under rubriken **Tjänster**.

1. På sidan **Domänmappningar** klickar du på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i slutet av en rad vars CDN du vill redigera.

1. Klicka på **Redigera**.

1. Gör följande i dialogrutan **Redigera domänkonfiguration**:

   * Välj den nivå (Publicera eller Förhandsgranska) som du vill använda i listrutan **Nivå**.
   * Välj det SSL-certifikat som du vill använda i listrutan **SSL-certifikat**.

1. Klicka på **Uppdatera**.


## Uppdatera ett anpassat domännamns SSL-certifikat {#update-cert}

Följ samma steg ovan för att uppdatera ett anpassat domännamns SSL-certifikat.

>[!NOTE]
>
>SSL-certifikatet måste vara giltigt, [redan konfigurerat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md), och innehålla det anpassade domännamn som du uppdaterar.


## Verifiera ett eget domännamn {#verify-custom-domain-name}

Se även [Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Gå till sidan **Domäninställningar** från skärmen **Översikt**.

1. Identifiera raden i det anpassade domännamnet som du vill verifiera.

1. Klicka på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) längst till höger på raden.

1. Klicka på **Verifiera** i listrutan.

1. I dialogrutan **Verifiera domän**, i **Vilken certifikattyp tänker du använda med den här domänen?**-listrutan och välj något av följande alternativ:

   | Certifikattyp, alternativ | Beskrivning |
   | --- | --- |
   | Adobe hanterat (DV) SSL-certifikat | Välj den här certifikattypen om du vill använda ett DV-certifikat (Domain Validation). Det här alternativet är idealiskt för de flesta fall och ger grundläggande domänvalidering. Adobe hanterar och förnyar certifikatet automatiskt. |
   | SSL-certifikat som hanteras av kund (OV/EV) | Välj den här certifikattypen om du tänker använda ett EV/OV SSL-certifikat för att skydda domänen. Det här alternativet ger bättre säkerhet med OV (Organization Validation) eller EV (Extended Validation). Använd om striktare verifiering, högre tillförlitlighetsnivåer eller anpassad kontroll över certifikaten krävs. |

1. Gör något av följande i dialogrutan **Verifiera domän**, baserat på den certifikattyp du valde:

   | Om du valde certifikattypen | Beskrivning |
   | --- | ---  |
   | Adobe-hanterat certifikat | a. Slutför de [Adobe hanterade certifikatstegen](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-steps). När du har slutfört stegen i dialogrutan **Verifiera domän** klickar du på **Verifiera**.<ul><li>DNS-verifiering kan ta några timmar att behandla på grund av fördröjd DNS-spridning.</li><li>Cloud Manager verifierar till slut ägarskap av domännamn och uppdaterar statusen i tabellen **Domäninställningar**. Mer information finns i [Kontrollera det anpassade domännamnets status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).</li>![Verifiera domänstatus](/help/implementing/cloud-manager/assets/domain-settings-verified.png)</li></ul>b. Du är nu redo att [lägga till ett Adobe-hanterat (DV) SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-adobe-managed-ssl-cert).</li></ul> |
   | Kundhanterat certifikat | a. Klicka på **OK**.<br>b. Du är nu redo att [lägga till ett SSL-certifikat som hanteras av kund (OV/EV) ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-customer-managed-ssl-cert) .<br>När du har lagt till certifikatet markeras ditt domännamn som verifierat i tabellen **Domäninställningar** . Mer information finns i [Kontrollera det anpassade domännamnets status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).</li></ul><br>![Verifiera domän för ett kundhanterat EV/OV-certifikat](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png) |


## Ta bort ett anpassat domännamn från alla associerade miljöer {#deleting}

En användare med rollen **Business Owner** eller **Deployment Manager** kan använda Cloud Manager för att ta bort ett anpassat domännamn.

### Ta bort ett anpassat domännamn från alla associerade miljöer {#delete-cdn-all}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Gå till sidan **Domäninställningar** från skärmen **Översikt**.

1. Identifiera raden med det anpassade domännamn som du vill ta bort.

1. Klicka på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) längst till höger på raden.

1. Välj **Ta bort**.

1. Bekräfta ditt bidrag.


### Ta bort ett anpassat domännamn från en viss miljö {#delete-cdn-specific}

>[!WARNING]
>
>Ta bort domänens DNS-poster med din DNS-leverantör *innan* domänen i Cloud Manager tas bort. Övergivna (farliga) DNS-poster kan kapas och utgöra en säkerhetsrisk.

**Så här tar du bort ett anpassat domännamn från en viss miljö:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Gå till skärmen **Miljö** från sidan **Översikt**.

1. Navigera från sidan **Miljö** till en informationsskärm om den miljö som är av intresse.

1. Identifiera raden med det anpassade domännamnet som du vill ta bort i tabellen Domänmappningar.

1. Klicka på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) längst till höger på raden.

1. Välj **Ta bort**.

1. Bekräfta ditt bidrag.
