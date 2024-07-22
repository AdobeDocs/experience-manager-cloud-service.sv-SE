---
title: Hantera SSL-certifikat
description: Lär dig hur du använder Cloud Manager för att kontrollera status för dina SSL-certifikat och hur du redigerar, ersätter, uppdaterar och tar bort dem.
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 35ac4cfb18e348281d2b126bdc3b292c84590f3a
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 0%

---


# Hantera SSL-certifikat {#managing-ssl-certificates}

Lär dig hur du använder Cloud Manager för att kontrollera status för dina SSL-certifikat och hur du redigerar, ersätter, uppdaterar och tar bort dem.

## Kontrollera SSL-certifikatens status {#checking-status-an-ssl-certificate}

Statusen för dina SSL-certifikat kan snabbt förstås från SSL-certifikatsidan.

* **Grön** - Den här statusen anger att ditt certifikat är giltigt i minst 14 dagar från dagens datum.

* **Orange** - Den här statusen anger att ditt certifikat upphör att gälla om mindre än 14 dagar.
   * Det är dags att se till att du har en plan för att förnya certifikatet och ersätta det med Cloud Manager användargränssnitt för att undvika eventuell webbplatsåtkomst och eventuella avbrott.
   * Cloud Manager skickar regelbundna meddelanden i användargränssnittet för att informera dig om att ett certifikat snart upphör att gälla.

* **Röd** - Den här statusen anger att SSL-certifikatet har upphört att gälla.

## Uppdatera ett SSL-certifikat {#update-ssl-certificate}

När ett certifikat upphör att gälla fungerar inte längre domäner som används med det utgångna certifikatet. Genom att uppdatera dina certifikat enligt följande steg ser du till att din domän fortsätter att fungera som du vill.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation
1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.
1. Gå till skärmen **Miljö** från sidan **Översikt**.
1. Navigera till skärmen **SSL-certifikat** från skärmen **Miljö**.
1. Du kan se en tabell med en rad för varje SSL-certifikat som har installerats i programmet. Klicka på ellipsknappen längst till höger i raden för det certifikat som du vill uppdatera och välj **Visa och uppdatera**.
1. Certifikatinformationen visas och kan uppdateras.
1. Spara ändringarna.

När du har sparat ändringarna tillämpas de automatiskt.

>[!NOTE]
>
>En användare måste vara medlem i rollen **Business Owner** eller **Deployment Manager** för att kunna uppdatera ett SSL-certifikat i Cloud Manager.

## Ersätta ett SSL-certifikat {#replace-ssl-certificate}

Ett SSL-certifikat kan ersättas med följande steg som beskrivs i avsnittet [Uppdatera ett SSL-certifikat.](#update-ssl-certificate)

## Ta bort ett SSL-certifikat {#deleting-an-ssl-certificate}

Att ta bort certifikat från Cloud Manager är en permanent åtgärd som inte kan ångras. Som en god praxis rekommenderar Adobe att du sparar SSL-filer lokalt innan du tar bort dem i Cloud Manager.

Cloud Manager tillåter inte att du tar bort ett SSL-certifikat som är kopplat till en eller flera domäner. Alla associerade domäner måste tas bort innan SSL-certifikatet tas bort. Mer information finns i [Hantera anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md).

Så här tar du bort ett SSL-certifikat.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.
1. Gå till skärmen **Miljö** från sidan **Översikt**.
1. Navigera till skärmen **SSL-certifikat** från skärmen **Miljö**.
1. Du kan se en tabell med en rad för varje SSL-certifikat som har installerats i programmet. Klicka på ellipsen längst till höger i raden för det certifikat som du vill ta bort och välj **Ta bort**.
1. Bekräfta borttagningen i dialogrutan **Ta bort SSL-certifikat**.
1. Kör pipeline för att ta bort distributionen av det borttagna certifikatet.

>[!NOTE]
>
>En användare måste vara medlem i rollen **Affärsägare** eller **Distributionshanterare** för att kunna ta bort ett SSL-certifikat i Cloud Manager.

## Befintliga CDN-konfigurationer {#pre-existing-cdn}

Om du har en befintlig CDN-konfiguration för ditt SSL-certifikat finns det ett informationsmeddelande på sidan **SSL-certifikat** som uppmanar dig att lägga till dessa konfigurationer via användargränssnittet så att de är synliga och konfigurerbara i Cloud Manager.

Meddelandet försvinner när alla befintliga miljökonfigurationer migreras med användargränssnittet. Det kan ta 1-2 arbetsdagar innan meddelandet försvinner.

Mer information finns i [Lägga till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).

Ett liknande meddelande visas även på sidorna **IP Tillåtelselista** och **Environment** för miljöer som har befintliga CDN-konfigurationer för IP tillåtelselista eller anpassade domännamn.
