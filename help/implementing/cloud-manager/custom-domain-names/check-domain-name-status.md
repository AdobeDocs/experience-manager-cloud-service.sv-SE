---
title: Kontrollerar domännamnsstatus
description: Lär dig hur du avgör om ditt anpassade domännamn har verifierats av Cloud Manager.
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---


# Kontrollerar domännamnsstatus {#check-status}

Lär dig hur du avgör om ditt anpassade domännamn har verifierats av Cloud Manager.

## Krav {#requirements}

Du måste uppfylla dessa krav innan du kontrollerar din domännamnsstatus i Cloud Manager.

* Du måste först lägga till en TXT-post för din anpassade domän enligt beskrivningen i dokumentet [Lägga till en TXT-post](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md).

## Kontrollera status för ditt anpassade domännamn {#how-to}

Du kan fastställa status för ditt anpassade domännamn i Cloud Manager.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Gå till skärmen **Miljö** från sidan **Översikt**.

1. Klicka på **Domäninställningar** i den vänstra navigeringspanelen.

1. Klicka på ikonen **Status** för domännamnet.

Statusinformationen visas. Din anpassade domän är klar att användas när statusen **Domänverifierad och distribuerad** visas. I [nästa avsnitt](#statuses) finns mer information om de olika statusvärdena och vad de innebär.

>[!NOTE]
>
>Cloud Manager utlöser automatiskt verifiering när du väljer **Skapa** i verifieringssteget i guiden **Lägg till anpassad domän** när du [lägger till ett nytt anpassat domännamn i Cloud Manager](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). För efterföljande verifieringar måste du aktivt markera ikonen för att verifiera igen bredvid statusen.

## Verifieringsstatus {#statuses}

Cloud Manager verifierar domänägarskap via [TXT-värdet](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) och visar ett av följande statusmeddelanden.

* **Domänverifieringen misslyckades** - TXT-värdet saknas eller har identifierats med fel.

   * Följ instruktionerna i statusmeddelandet för att lösa problemet.
   * När du är klar måste du markera ikonen **Verifiera igen** bredvid statusen.

* **Domänverifiering pågår** - Verifiering pågår.

   * Den här statusen visas vanligtvis när du har valt ikonen **Verifiera igen** bredvid statusen.
   * DNS-verifiering kan ta några timmar att behandla på grund av fördröjd DNS-spridning.

* **Verifierad, distributionen misslyckades** - TXT-verifieringen lyckades, men CDN-distributionen misslyckades.

   * Kontakta i så fall din Adobe-representant.

* **Domänen har verifierats och distribuerats** - Den här statusen anger att ditt anpassade domännamn är klart att användas.

   * Nu är ditt anpassade domännamn klart för testning och ska peka på Cloud Manager domännamn.
   * Mer information finns i [Konfigurera DNS-inställningar](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md).

* **Tar bort** - Ett anpassat domännamn tas bort.

* **Borttagningen misslyckades** - Det gick inte att ta bort det anpassade domännamnet. Ett nytt försök måste göras.

   * Mer information finns i [Hantera anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md).

## Domännamnsfel {#domain-error}

Nedan följer några vanliga verifieringsfel för domännamn och deras vanliga upplösning.

### Domänen är inte installerad {#domain-not-installed}

Det här felet kan inträffa under domänvalidering av TXT-posten även efter att du har kontrollerat att posten har uppdaterats korrekt.

#### Felorsak {#cause}

Låser snabbt en domän till det ursprungliga konto som registrerade den och inget annat konto kan registrera en underdomän utan att fråga om tillstånd. Med Fastly kan du dessutom bara tilldela en apex-domän och associerade underdomäner till en fast tjänst och ett konto. Om du har ett befintligt Fast-konto som länkar samma index och underdomäner som används för dina AEM Cloud Service-domäner visas det här felet.

#### Felmatchning {#resolution}

Felet är åtgärdat på följande sätt:

* Ta bort API:t och underdomänerna från det befintliga kontot innan du installerar domänen i Cloud Manager.

* Använd det här alternativet om du vill länka apex-domänen och alla underdomäner till AEM as a Cloud Service Fast-kontot. Mer information finns i [Arbeta med domäner i Snabbt-dokumentationen](https://docs.fastly.com/en/guides/working-with-domains).

* Om din huvuddomän har flera underdomäner för webbplatser från AEM as a Cloud Service och andra företag som du vill länka till olika Snabbt-konton kan du försöka installera domänen i Cloud Manager. Om domäninstallationen misslyckas skapar du en kundsupportbiljett med Fast så att Adobe kan följa med Fastly å dina vägnar.

>[!TIP]
>
>Det tar vanligtvis 1-2 arbetsdagar att lösa problem med domändelegering med Fastly. Därför rekommenderar vi att du installerar domänerna långt innan de publiceras.

>[!NOTE]
>
>Vidarebefordra inte webbplatsens DNS till AEM as a Cloud Service IP om domänen inte installerades korrekt.

## Befintliga CDN-konfigurationer för anpassade domännamn {#pre-existing-cdn}

Om du har en befintlig CDN-konfiguration för dina anpassade domännamn finns det ett informativt meddelande på sidorna **Anpassade domännamn** och **Miljö** som uppmanar dig att lägga till dessa konfigurationer via användargränssnittet så att de är synliga och konfigurerbara i Cloud Manager.

Meddelandet försvinner när alla befintliga miljökonfigurationer migreras med användargränssnittet. Det kan ta 1-2 arbetsdagar innan meddelandet försvinner.

Mer information finns i [Lägga till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

## Nästa steg {#next-steps}

När du har verifierat din domänstatus i Cloud Manager måste du konfigurera DNS-inställningar genom att lägga till DNS CNAME- eller APEX-poster som pekar på AEM as a Cloud Service. Fortsätt till dokumentet [Konfigurera DNS-inställningar](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) om du vill fortsätta konfigurera ditt anpassade domännamn.
