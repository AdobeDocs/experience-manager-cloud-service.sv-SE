---
title: Kontrollerar domännamnsstatus
description: Lär dig hur du avgör om ditt anpassade domännamn har verifierats av Cloud Manager.
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: ba0226b5ad3852dd5f72dd7e0ace650035f5ac6a
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---


# Kontrollerar domännamnsstatus {#check-status}

Du kan fastställa statusen för ditt anpassade domännamn i Cloud Manager.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Miljö** från **Översikt** sida.

1. Klicka på **Domäninställningar** i den vänstra navigeringspanelen.

1. Klicka på **Status** -ikon för domännamnet.

Cloud Manager verifierar domänägarskap via TXT-värdet och visar ett av följande statusmeddelanden.

* **Domänverifieringen misslyckades** - TXT-värdet saknas eller har identifierats med fel.

   * Följ instruktionerna för att lösa problemet.
   * När du är klar måste du välja **Verifiera igen** -ikonen bredvid statusen.

* **Domänverifiering pågår** - Verifiering pågår.

   * Den här statusen visas vanligtvis när du har valt **Verifiera igen** -ikonen bredvid statusen.

* **Verifierad, distributionen misslyckades** - TXT-verifieringen lyckades, men CDN-distributionen misslyckades.

   * Kontakta i så fall din Adobe-representant.

* **Domänen har verifierats och distribuerats** - Den här statusen anger att ditt anpassade domännamn är klart att användas.

   * Nu är ditt anpassade domännamn klart för testning och kan hänvisas till molnhanterarens domännamn.
   * Se dokumentet [Konfigurera DNS-inställningar](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) om du vill veta mer.

* **Tar bort** - Borttagningen av ett anpassat domännamn pågår.

* **Borttagningen misslyckades** - Det gick inte att ta bort det anpassade domännamnet. Du måste försöka igen.

   * Se dokumentet [Hantera anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) om du vill veta mer.

Cloud Manager utlöser automatiskt en TXT-verifiering när du väljer **Spara** om kontrollsteg för **Lägg till anpassad domän** guide. För efterföljande verifieringar måste du aktivt markera ikonen för att verifiera igen bredvid statusen.

## Domännamnsfel {#domain-error}

I det här avsnittet förklaras de fel som du kan se och hur du löser dem.

**Domänen är inte installerad** - Du får det här felet under domänvalidering av TXT-posten även efter att du har kontrollerat att posten har uppdaterats korrekt.

**Felförklaring** - Låser snabbt en domän till det ursprungliga konto som registrerade den och inget annat konto kan registrera en underdomän utan att fråga om tillstånd. Dessutom kan du bara tilldela en API-domän och associerade underdomäner till en snabbast-tjänst och ett konto. Om du har ett befintligt Fast-konto som länkar samma index och underdomäner som används för dina AEM Cloud Service-domäner visas det här felet.

**Felupplösning** - Felet har åtgärdats enligt följande:

* Ta bort API:er och underdomäner från det befintliga kontot innan du installerar domänen i Cloud Manager. Använd det här alternativet om du vill länka apex-domänen och alla underdomäner till det AEM as a Cloud Service snabbkontot. Se [Arbeta med domäner i dokumentationen Snabbt](https://docs.fastly.com/en/guides/working-with-domains) om du vill ha mer information.

* Om din API-domän har flera underdomäner för AEM as a Cloud Service och icke-AEM as a Cloud Service webbplatser som du vill länka till olika Snabbt-konton kan du försöka installera domänen i Cloud Manager och om domäninstallationen misslyckas skapa en kundsupportbiljett med Snabbt så att vi kan följa med Snabbt å dina vägnar.

>[!NOTE]
>
>OBS! Vidarebefordra inte webbplatsens DNS till AEM as a Cloud Service IP-adresser om domänen inte installerades korrekt.

## Tidigare CDN-konfigurationer för anpassade domännamn {#pre-existing-cdn}

Om du har en befintlig CDN-konfiguration för dina anpassade domännamn visas ett informativt meddelande på **Anpassade domännamn** och **Miljö** -sidor, som uppmanar dig att lägga till dessa konfigurationer via användargränssnittet så att de visas och kan konfigureras i Cloud Manager.

Meddelandet försvinner när alla befintliga miljökonfigurationer migreras med användargränssnittet. Det kan ta 1-2 arbetsdagar innan meddelandet försvinner.

Se dokumentet [Lägga till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) för mer information.
