---
title: Kontrollera domännamnsstatus
description: Lär dig hur du verifierar att Cloud Manager har bekräftat ditt anpassade domännamn.
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ff8c7fb21b4d8bcf395d28c194a7351281eef45b
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---


# Kontrollera domännamnsstatus {#check-status}

Lär dig hur du verifierar att Cloud Manager har bekräftat ditt anpassade domännamn.

## Krav {#requirements}

Uppfyll dessa krav innan du kontrollerar domännamnsstatusen i Cloud Manager.

* Lägg först till ett EV/OV-certifikat för din anpassade domän enligt beskrivningen i dokumentet [Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

## Kontrollera statusen för ditt anpassade domännamn {#how-to}

Du kan avgöra statusen för ditt anpassade domännamn i Cloud Manager.

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

Cloud Manager verifierar domänägarskap via det kundhanterade certifikatet. När du är klar visas ett av följande statusmeddelanden:

| Status | Beskrivning |
| --- | --- |
| Domänverifieringen misslyckades | EV/OV-certifikatet som hanteras av kunden saknas eller identifieras med fel.<br> Följ instruktionerna i statusmeddelandet för att lösa problemet. När du är klar måste du markera ikonen **Verifiera igen** bredvid statusen. |
| Domänverifiering pågår | Verifiering pågår.<br>Den här statusen visas vanligtvis när du har valt ikonen **Verifiera igen** bredvid statusen. DNS-verifiering kan ta några timmar att behandla på grund av fördröjd DNS-spridning. |
| Verifierad - distributionen misslyckades | Verifieringen av EV/OV-certifikatet lyckades, men CDN-distributionen misslyckades.<br>Kontakta din Adobe-representant i sådana fall. |
| Domänen har verifierats och distribuerats | Den här statusen anger att ditt anpassade domännamn är klart att användas.<br>Nu är ditt anpassade domännamn klart för testning och ska peka på Cloud Manager domännamn. Mer information finns i [Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |
| Tar bort | Borttagningen av ett anpassat domännamn pågår. |
| Borttagningen misslyckades | Borttagningen av ett anpassat domännamn misslyckades och måste göras om.<br>Mer information finns i [Hantera anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md). |


## Domännamnsfel {#domain-error}

Nedan följer några vanliga verifieringsfel för domännamn och deras vanliga upplösning.

### Domänen är inte installerad {#domain-not-installed}

Detta fel kan uppstå under domänvalidering av EV/OV-certifikatet även efter att du har kontrollerat att certifikatet har uppdaterats korrekt.

#### Felorsak {#cause}

Låser snabbt en domän till det konto som först registrerar den, och andra konton måste begära behörighet att registrera en underdomän. Med Fastly kan du dessutom bara tilldela en apex-domän och associerade underdomäner till en fast tjänst och ett konto. Om du har ett befintligt Fast-konto som länkar samma index och underdomäner som används för dina AEM Cloud Service-domäner visas det här felet.

#### Fellösning {#resolution}

Felet är åtgärdat på följande sätt:

* Ta bort API:t och underdomänerna från det befintliga kontot innan du installerar domänen i Cloud Manager.

* Använd det här alternativet om du vill länka apex-domänen och alla underdomäner till AEM as a Cloud Service Fast-kontot. Mer information finns i [Arbeta med domäner i Snabbt-dokumentationen](https://docs.fastly.com/en/guides/working-with-domains).

* Om din API-domän har flera underdomäner för AEM as a Cloud Service och andra webbplatser än AEM som behöver länka till olika Snabbt-konton försöker du installera domänen i Cloud Manager. Den här processen hjälper till att hantera underdomänsanslutningar mellan olika snabbkonton. Om domäninstallationen misslyckas skapar du en kundsupportbiljett med Fastly så att Adobe kan följa upp med Fastly å dina vägnar.

>[!TIP]
>
>Det tar vanligtvis 1-2 arbetsdagar att lösa problem med domändelegering med Fastly. Därför rekommenderar vi att du installerar domänerna långt innan de publiceras.

>[!NOTE]
>
>Vidarebefordra inte webbplatsens DNS till AEM as a Cloud Service IP om domänen inte installerades korrekt.

## Befintliga CDN-konfigurationer för anpassade domännamn {#pre-existing-cdn}

Om du redan har en CDN-konfiguration för dina anpassade domännamn visas ett informativt meddelande på sidorna **Anpassade domännamn** och **Miljö**. Det uppmuntrar dig att lägga till dessa konfigurationer via användargränssnittet så att de kan hanteras och visas inom Cloud Manager.

Meddelandet försvinner när alla befintliga miljökonfigurationer har migrerats med användargränssnittet. Det kan ta 1-2 arbetsdagar innan meddelandet försvinner.

Mer information finns i [Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

## Nästa steg {#next-steps}

När du har verifierat din domänstatus i Cloud Manager konfigurerar du DNS-inställningar genom att lägga till DNS-, CNAME- eller APEX-poster som pekar på AEM as a Cloud Service. Fortsätt till dokumentet [Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) om du vill fortsätta konfigurera ditt anpassade domännamn.
