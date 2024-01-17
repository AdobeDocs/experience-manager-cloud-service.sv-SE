---
title: Hantera SSL-certifikat
description: Lär dig hur du använder Cloud Manager för att kontrollera statusen för dina SSL-certifikat och hur du redigerar, ersätter, uppdaterar och tar bort dem.
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
source-git-commit: 90250c13c5074422e24186baf78f84c56c9e3c4f
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---


# Hantera SSL-certifikat {#managing-ssl-certificates}

Lär dig hur du använder Cloud Manager för att kontrollera statusen för dina SSL-certifikat och hur du redigerar, ersätter, uppdaterar och tar bort dem.

## Kontrollera SSL-certifikatens status {#checking-status-an-ssl-certificate}

Statusen för dina SSL-certifikat kan snabbt förstås från SSL-certifikatsidan.

* **Grön** - Den här statusen anger att ditt certifikat är giltigt i minst 60 dagar från dagens datum.

* **Orange** - Den här statusen anger att ditt certifikat upphör att gälla om mindre än 60 dagar.
   * Det är dags att se till att du har en plan för att förnya certifikatet och ersätta det med användargränssnittet i Cloud Manager för att undvika eventuell webbplatsåtkomst eller avbrott.
   * Cloud Manager skickar regelbundna meddelanden i användargränssnittet för att informera dig om att certifikatet snart upphör att gälla.

* **Röd** - Den här statusen anger att SSL-certifikatet har upphört att gälla.

## Uppdatera ett SSL-certifikat {#update-ssl-certificate}

När ett certifikat upphör att gälla fungerar inte längre domäner som används med det utgångna certifikatet. Genom att uppdatera dina certifikat enligt följande steg ser du till att din domän fortsätter att fungera som du vill.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation
1. På **[Mina program](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** väljer du programmet.
1. Navigera till **Miljö** från **Ökning** sida.
1. Navigera till **SSL-certifikat** från **Miljö** skärm.
1. Du kan se en tabell med en rad för varje SSL-certifikat som har installerats i programmet. Klicka på ellipsknappen längst till höger i raden i certifikatet som du vill uppdatera och välj **Visa och uppdatera**.
1. Certifikatinformationen visas och kan uppdateras.
1. Kör pipeline för att distribuera det uppdaterade certifikatet.

>[!NOTE]
>
>En användare måste vara medlem i **Företagsägare** eller **Distributionshanteraren** roll för att uppdatera ett SSL-certifikat i Cloud Manager.

## Ersätta ett SSL-certifikat {#replace-ssl-certificate}

Ett SSL-certifikat kan ersättas med följande steg som beskrivs i avsnittet [Uppdaterar ett SSL-certifikat.](#update-ssl-certificate)

## Ta bort ett SSL-certifikat {#deleting-an-ssl-certificate}

Att ta bort certifikat från Cloud Manager är en permanent åtgärd som inte kan ångras. Som en god praxis rekommenderar Adobe att du sparar SSL-filer lokalt innan du tar bort dem i Cloud Manager.

I Cloud Manager kan du inte ta bort ett SSL-certifikat som har en eller flera domäner kopplade till sig. Alla associerade domäner måste tas bort innan SSL-certifikatet tas bort. Se [Hantera anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) om du vill veta mer.

Så här tar du bort ett SSL-certifikat.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.
1. Navigera till **Miljö** från **Ökning** sida.
1. Navigera till **SSL-certifikat** från **Miljö** skärm.
1. Du kan se en tabell med en rad för varje SSL-certifikat som har installerats i programmet. Klicka på ellipsen längst till höger i raden för det certifikat som du vill ta bort och markera **Ta bort**.
1. Bekräfta borttagningen i dialogrutan **Ta bort SSL-certifikat** -dialogrutan.
1. Kör pipeline för att ta bort distributionen av det borttagna certifikatet.

>[!NOTE]
>
>En användare måste vara medlem i **Företagsägare** eller **Distributionshanteraren** roll för att ta bort ett SSL-certifikat i Cloud Manager.

## Befintliga CDN-konfigurationer {#pre-existing-cdn}

Om du har en befintlig CDN-konfiguration för ditt SSL-certifikat visas ett informationsmeddelande på **SSL-certifikat** som uppmanar dig att lägga till dessa konfigurationer via användargränssnittet så att de är synliga och konfigurerbara i Cloud Manager.

Meddelandet försvinner när alla befintliga miljökonfigurationer migreras med användargränssnittet. Det kan ta 1-2 arbetsdagar innan meddelandet försvinner.

Se [Lägga till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) för mer information.

Ett liknande meddelande finns också på **IP TILLÅTELSELISTA** och **Miljö** sidor för miljöer som har befintliga CDN-konfigurationer för IP tillåtelselista eller anpassade domännamn.
