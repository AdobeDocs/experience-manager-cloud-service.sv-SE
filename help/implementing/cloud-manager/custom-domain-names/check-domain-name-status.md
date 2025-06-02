---
title: Kontrollera domännamnsstatus
description: Lär dig hur du verifierar att Cloud Manager har bekräftat ditt anpassade domännamn.
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 68da11037cb3572a6f869fe8bd6a898e0aad87ec
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%

---


# Kontrollera domännamnsstatus {#check-status}

Lär dig hur du verifierar att Cloud Manager har bekräftat ditt anpassade domännamn.

## Kontrollera status för ett anpassat domännamn {#how-to}

Innan du kontrollerar domännamnsstatusen i Cloud Manager ska du kontrollera att du redan har lagt till ett kundhanterat (OV/EV) SSL-certifikat för din anpassade domän enligt beskrivningen i [Lägg till ett kundhanterat SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md##add-customer-managed-ssl-cert).

**Så här kontrollerar du statusen för ett anpassat domännamn:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Gå till skärmen **Miljö** från sidan **Översikt**.

1. Klicka på **Domäninställningar** på den vänstra menyn.

1. Klicka på ikonen **Status** för domännamnet.

Statusinformationen visas. Din anpassade domän är klar att användas när statusen **Domänverifierad och distribuerad** visas. I [nästa avsnitt](#statuses) finns mer information om de olika statusvärdena och vad de innebär.

>[!NOTE]
>
>Om du använder ett *Adobe-hanterat (DV) SSL-certifikat* med domänen utlöser Cloud Manager automatiskt verifiering när du klickar på **Verifiera** i dialogrutan Verifiera domän när du [lägger till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).
>
>Om du planerar att använda ett **kundhanterat (OV/EV) SSL-certifikat** verifieras din domän *efter* att du [lagt till OV/EV SSL-certifikatet](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).


## Verifieringsstatus {#statuses}

Cloud Manager verifierar domänägarskap via det kundhanterade (OV/EV) SSL-certifikatet. När du är klar visas ett av följande statusmeddelanden:

| Status | Beskrivning |
| --- | --- |
| Domänverifieringen misslyckades | EV/OV-certifikatet som hanteras av kunden saknas eller identifieras med fel.<br> Följ instruktionerna i statusmeddelandet för att lösa problemet. När du är klar måste du markera ikonen **Verifiera igen** bredvid statusen. |
| Domänverifiering pågår | Verifiering pågår.<br>Den här statusen visas vanligtvis när du har valt ikonen **Verifiera igen** bredvid statusen. DNS-verifiering kan ta några timmar att behandla på grund av fördröjd DNS-spridning. |
| Verifierad - distributionen misslyckades | Verifieringen av EV/OV-certifikatet lyckades, men CDN-distributionen misslyckades.<br>Kontakta i så fall din Adobe-representant. |
| Domänen har verifierats och distribuerats | Den här statusen anger att ditt anpassade domännamn är klart att användas.<br>Nu är ditt anpassade domännamn klart för testning och ska peka på Cloud Manager domännamn. Mer information finns i [Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |
| Tar bort | Borttagningen av ett anpassat domännamn pågår. |
| Borttagningen misslyckades | Borttagningen av ett anpassat domännamn misslyckades och måste göras om.<br>Mer information finns i [Hantera anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md). |


## Domännamnsfel {#domain-error}

Följande är ett vanligt fel vid verifiering av domännamn och dess vanliga upplösning.

### Domänen är inte installerad {#domain-not-installed}

<!-- This error may occur during domain validation of the EV/OV certificate even after you have checked that the certificate has been updated appropriately. -->

När du försöker lägga till en domänmappning i Cloud Manager kan följande felmeddelande visas:

*Domänen är redan installerad på ett snabbkonto. Ta bort det först från den platsen innan du lägger till i Cloud Service.*

<!-- This message indicates that the domain is currently associated with a different Fastly account—typically outside of Adobe's control. To proceed, the domain must be disassociated from the other account before it can be added to the Adobe-managed Cloud Service. This issue usually occurs when the same domain is already mapped to a different origin in a non-Adobe Fastly configuration. -->

**Felorsak**
Låser snabbt en domän till det konto som först registrerar den, och andra konton måste begära behörighet att registrera en underdomän. Med Fastly kan du dessutom bara tilldela en apex-domän och associerade underdomäner till en fast tjänst och ett konto. Om du har ett befintligt Fast-konto som länkar samma index och underdomäner som används för dina AEM Cloud Service-domäner visas det här felet.

**Fellösning**
Felet är åtgärdat på följande sätt:

* Ta bort API:t och underdomänerna från det befintliga kontot innan du installerar domänen i Cloud Manager.

* Använd det här alternativet om du vill länka apex-domänen och alla underdomäner till AEM as a Cloud Service Fast-kontot. Mer information finns i [Arbeta med domäner](https://www.fastly.com/documentation/guides/getting-started/domains/working-with-domains/working-with-domains/) i Snabbt-dokumentationen.

* Om din huvuddomän har flera underdomäner för AEM as a Cloud Service- och icke-AEM-webbplatser som måste länka till olika Snabbt-konton, försöker du installera domänen i Cloud Manager. Den här processen hjälper till att hantera underdomänsanslutningar mellan olika snabbkonton. Om domäninstallationen misslyckas skapar du en kundsupportbiljett med Snabbt så att Adobe kan följa upp med Fastly å dina vägnar.

>[!TIP]
>
>Det tar vanligtvis 1-2 arbetsdagar att lösa problem med domändelegering med Fastly. Därför rekommenderar vi att du installerar domänerna långt innan de blir aktiva.

>[!NOTE]
>
>Vidarebefordra inte webbplatsens DNS till AEM as a Cloud Service IP om domänen inte installerades korrekt.

## Befintliga CDN-konfigurationer för anpassade domännamn {#pre-existing-cdn}

Om du redan har en CDN-konfiguration (Content Delivery Network) för dina anpassade domännamn visas ett informativt meddelande på sidorna **Anpassade domännamn** och **Miljö**. Det uppmuntrar dig att lägga till dessa konfigurationer via användargränssnittet så att de kan hanteras och visas inom Cloud Manager.

Meddelandet försvinner när alla befintliga miljökonfigurationer har migrerats med användargränssnittet. Det kan ta 1-2 arbetsdagar innan meddelandet försvinner.

Mer information finns i [Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

## Nästa steg {#next-steps}

När du har verifierat din domänstatus i Cloud Manager konfigurerar du DNS-inställningar genom att lägga till DNS-, CNAME- eller APEX-poster som pekar på AEM as a Cloud Service. Fortsätt till dokumentet [Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) om du vill fortsätta konfigurera ditt anpassade domännamn.
