---
title: Hantera SSL-certifikat
description: Lär dig hur du använder Cloud Manager för att kontrollera status för dina SSL-certifikat och hur du redigerar, ersätter, uppdaterar och tar bort dem.
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f0cf9fa7da7e89d42ab90dee0e8400b26f004574
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 0%

---


# Hantera SSL-certifikat {#managing-ssl-certificates}

Lär dig hur du använder Cloud Manager för att kontrollera status för dina SSL-certifikat och hur du redigerar, ersätter, uppdaterar och tar bort dem.

## Kontrollera SSL-certifikatens status {#checking-status-an-ssl-certificate}

Cloud Manager ger en översikt över statusen för alla certifikat för ditt program.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämpligt program.
1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.
1. Klicka på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i sidans övre vänstra hörn för att visa sidomenyn.
1. Under rubriken **Tjänster** klickar du på ![Lås stängda ikoner](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL-certifikat**.

Sidan **SSL-certifikat** ger status för dina SSL-certifikat.

| Status för SSL-certifikat | Beskrivning |
| --- | --- |
| Grön | Certifikatet är giltigt i minst 14 dagar från dagens datum. |
| Orange | Certifikatet upphör att gälla om mindre än 14 dagar.<br> ・ Kontrollera att du har en plan för att förnya certifikatet och ersätta det med Cloud Manager användargränssnitt för att undvika eventuell webbplatsåtkomst och eventuella avbrott.<br> ・ Cloud Manager skickar regelbundna meddelanden i användargränssnittet för att informera dig om att certifikatet snart upphör att gälla. |
| Röd | SSL-certifikatet har gått ut.<br>Se [Uppdatera ett SSL-certifikat som har gått ut och som har hanterats av en kund](#update-ssl-certificate) eller [Ta bort ett SSL-certifikat](#deleting-an-ssl-certificate). |

## Uppdatera ett kundhanterat SSL-certifikat som gått ut {#update-ssl-certificate}

När ett kundhanterat certifikat upphör att gälla fungerar inte längre domäner som används med det utgångna certifikatet. Genom att uppdatera dina certifikat kan du vara säker på att din domän fortsätter att fungera som du vill.

En användare måste vara medlem i rollen **Affärsägare** eller **Distributionshanterare** för att den här aktiviteten ska kunna slutföras.

**Så här uppdaterar du ett kundhanterat SSL-certifikat som upphört att gälla:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämpligt program.
1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.
1. Klicka på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i sidans övre vänstra hörn för att visa sidomenyn.
1. Under rubriken **Tjänster** klickar du på ![Lås stängda ikoner](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL-certifikat**.
1. Klicka på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) längst till höger på raden för det kundhanterade certifikat som du vill uppdatera och klicka sedan på **Visa och uppdatera**.

   ![Uppdatera en kundhanterad SSL-certifiering som upphört att gälla](/help/implementing/cloud-manager/assets/ssl/ssl-cert-update.png)

1. Gör följande i dialogrutan **Visa och uppdatera SSL-certifikat**:

   * (Valfritt) Skriv ett nytt namn i fältet **Certifikatnamn**.
   * Klistra in den nya certifikatinnehållsnyckeln i fältet **Certifikat**.
   * Uppdatera endast det här fältet i fältet **Privat nyckel** om du har gjort ändringar i certifikatet.
   * Klistra in certifikatkedjan i fältet **Certifikatkedja** (eller förtroendekedjan).

1. Klicka på **Uppdatera** om du vill spara ändringarna och använda dem automatiskt.


>[!NOTE]
>
>Om två eller flera SAN-certifikat täcker samma SAN-domänpost och ett av dem uppdateras, installeras det uppdaterade certifikatet för domänen.
>
>Mer information finns i [Felsöka SSL-certifikatproblem](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md#wrong-san-cert).

## Ersätta ett kundhanterat SSL-certifikat som gått ut {#replace-ssl-certificate}

Följ de steg som beskrivs i [Uppdatera ett SSL-certifikat som har upphört att gälla](#update-ssl-certificate) och ersätt ett kundhanterat SSL-certifikat som har upphört att gälla.

## Byta namn på ett SSL-certifikat som hanteras av Adobe (#rename-an-ssl-certificate)

Nedan följer några skäl till att du kanske vill byta namn på ett SSL-certifikat:

* **Förbättrad organisation**: Om du byter namn på certifikatet kan du klargöra dess syfte, till exempel identifiera vilken miljö (till exempel mellanlagring, produktion) eller domän det är avsett för.
* **Undvik förvirring**: Om du hanterar flera certifikat kan ett tydligt och beskrivande namn hjälpa till att förhindra misstag, som att tillämpa fel certifikat på fel domän.
* **Efterlevnad och granskning**: Det kan vara enklare att spåra certifikat med rätt namn av säkerhets- och granskningsskäl.

**Så här byter du namn på ett SSL-certifikat som hanteras av Adobe:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämpligt program.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Klicka på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i sidans övre vänstra hörn för att visa sidomenyn.

1. Under rubriken **Tjänster** klickar du på ![Lås stängda ikoner](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL-certifikat**.

1. På sidan **SSL-certifikat** klickar du på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i slutet av en rad vars **Adobe-hanterade** SSL-certifikat du vill byta namn på.

1. Klicka på **Byt namn** i listrutan.

1. Ange certifikatets nya namn i dialogrutan **Byt namn på DV-certifikat** i textfältet **Certifikatnamn**.

1. Klicka på **Byt namn**.


## Ta bort ett SSL-certifikat {#deleting-an-ssl-certificate}

Att ta bort SSL-certifikat som hanteras av Adobe eller hanteras av kund från Cloud Manager är en permanent åtgärd som inte kan ångras. Som en god praxis rekommenderar Adobe att du sparar SSL-filer lokalt innan du tar bort dem i Cloud Manager.

>[!NOTE]
>
>Du kan inte ta bort ett Adobe-hanterat SSL-certifikat som har en eller flera aktiva domäner kopplade till sig. Alla associerade aktiva domäner måste tas bort innan SSL-certifikatet tas bort. Mer information finns i [Hantera anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md).

En användare måste vara medlem i rollen **Affärsägare** eller **Distributionshanterare** för att den här aktiviteten ska kunna slutföras.

**Så här tar du bort ett SSL-certifikat:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämpligt program.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Klicka på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i sidans övre vänstra hörn för att visa sidomenyn.

1. Under rubriken **Tjänster** klickar du på ![Lås stängda ikoner](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL-certifikat**.

1. På sidan SSL-certifikat klickar du på ikonen ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) längst till höger i tabellraden för det certifikat du vill ta bort och sedan på **Ta bort**.

   Om **Delete** har en informationsikon som i bilden nedan kan du läsa anteckningen ovan.

   ![Ta bort knapp med informationsikon](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete-infoicon.png)

1. Klicka på **Ta bort** i dialogrutan **Ta bort SSL-certifikat** för att bekräfta borttagningen.

1. Kör pipeline för att ta bort distributionen av det borttagna certifikatet.


## Redan befintliga CDN-konfigurationer {#pre-existing-cdn}

Om du redan har en CDN-konfiguration för ditt SSL-certifikat visas ett informativt meddelande på sidan **SSL-certifikat**. Det uppmuntrar dig att lägga till dessa konfigurationer via användargränssnittet så att de är synliga och hanterbara i Cloud Manager.

Meddelandet försvinner när alla befintliga miljökonfigurationer har migrerats med användargränssnittet. Det kan ta en till två arbetsdagar innan meddelandet försvinner.

Mer information finns i [Lägg till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).

Ett liknande meddelande visas även på sidorna **IP Tillåtelselista** och **Environment** för miljöer som har befintliga CDN-konfigurationer för IP Tillåtelselista eller anpassade domännamn.
