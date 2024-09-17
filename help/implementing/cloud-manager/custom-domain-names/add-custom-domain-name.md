---
title: Lägg till ett anpassat domännamn
description: Lär dig hur du lägger till ett anpassat domännamn med Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f45de13049f78f97b256235d9395695cb531c40d
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 0%

---


# Lägg till ett anpassat domännamn {#adding-cdn}

Lär dig hur du lägger till ett anpassat domännamn med Cloud Manager.

## Krav {#requirements}

Uppfyll dessa krav innan du lägger till ett anpassat domännamn i Cloud Manager.

* Du måste ha lagt till ett domän-SSL-certifikat för domänen som du vill lägga till innan du lägger till ett anpassat domännamn enligt beskrivningen i dokumentet [Lägg till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).
* Du måste ha rollen **Affärsägare** eller **Distributionshanterare** för att lägga till ett anpassat domännamn i Cloud Manager.
* Använd snabbast eller något annat CDN.

>[!IMPORTANT]
>
>Även om du använder ett CDN som inte är Adobe måste du lägga till domänen i Cloud Manager.

## Var ska jag lägga till egna domännamn? {#where-to-add-cdn}

Du kan lägga till ett eget domännamn från två platser i Cloud Manager:

* [Från sidan Domäninställningar](#adding-cdn-settings)
* [Från sidan Miljöer](#adding-cdn-environments)

När du lägger till ett anpassat domännamn hanteras domänen med det mest specifika, giltiga certifikatet. Om flera certifikat har samma domän väljs den senast uppdaterade versionen. Adobe rekommenderar att du hanterar certifikat så att det inte finns några överlappande domäner.

Stegen för de metoder som beskrivs i det här dokumentet baseras på Fast. Om du har använt ett annat CDN konfigurerar du din domän med det CDN som du har valt att använda.

## Lägg till ett anpassat domännamn från sidan Domäninställningar {#adding-cdn-settings}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Välj fliken **Domäninställningar** i den vänstra navigeringspanelen

   ![Fönstret Domäninställningar](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Klicka på **Lägg till domän** i det övre högra hörnet på sidan **Domäninställningar**.

1. I dialogrutan **Lägg till domän** anger du det anpassade domännamnet som du använder i fältet **Domännamn**.
Inkludera inte `http://`, `https://` eller mellanslag när du anger i din domän.

1. Klicka på **Skapa**.

1. I dialogrutan **Verifiera domän**, i **Vilken certifikattyp tänker du använda med den här domänen?**-listrutan och välj något av följande alternativ:

   | Certifikattyp | Beskrivning |
   | --- | --- |
   | Adobe-hanterat certifikat | Välj om du vill använda ett DV-certifikat (Domain Validation). Det här alternativet är idealiskt för de flesta fall och ger grundläggande domänvalidering. Adobe hanterar och förnyar certifikatet automatiskt. |
   | Kundhanterat certifikat | Välj om du vill använda ett EV/OV-certifikat. Det här alternativet ger bättre säkerhet med EV (Extended Validation) eller OV (Organization Validation). Använd om striktare verifiering, högre tillförlitlighetsnivåer eller anpassad kontroll över certifikaten krävs. |

1. Gör något av följande i dialogrutan **Verifiera domän**, baserat på den certifikattyp du valde:

   | Om du valde certifikattypen | Beskrivning |
   | --- | ---  |
   | Adobe-hanterat certifikat | Slutför de [Adobe hanterade certifikatstegen](#adobe-managed-cert-steps) innan du fortsätter till nästa steg. |
   | Kundhanterat certifikat | Slutför de [kundhanterade certifikatstegen](#customer-managed-cert-steps) innan du fortsätter till nästa steg. |

1. Klicka på **Verifiera**.

1. Du kan nu [lägga till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).

   >[!NOTE]
   >
   >Om du använder ett självhanterat SSL-certifikat och en självhanterad CDN-provider kan du hoppa över det här steget och gå direkt till [Lägg till en CDN-konfiguration](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md) när det är klart.


### Certifikatsteg som hanteras av Adobe {#adobe-managed-cert-steps}

Om du har valt certifikattypen *Adobe hanterat certifikat* utför du följande steg i dialogrutan **Verifiera domän**.

![certifikatsteg som hanteras av Adobe](/help/implementing/cloud-manager/assets/cdn/cdn-create-adobe-dv-cert.png)

Du måste lägga till och verifiera en CNAME för att kunna verifiera den domän som används.

När en `CNAME`- eller A-post har etablerats dirigeras all Internettrafik för domänen till den plats där den pekar. Om den platsen inte har etablerats för att betjäna trafiken uppstår ett driftstopp. Om innehållet inte har testats kan det finnas fel i det. Det här är orsaken till att det här steget alltid utförs när testningen är klar och du är redo att börja publicera.

Om du vill konfigurera de här inställningarna måste du kontrollera om en `CNAME`- eller en apex-post måste konfigureras så att den pekar ditt anpassade domännamn mot Cloud Manager domännamn. Följande avsnitt i det här dokumentet kan hjälpa dig att avgöra vilken typ av post som passar din DNS-konfiguration.

>[!NOTE]
>
>För CDN:er som hanteras av Adobe tillåts bara webbplatser med ACME-validering när DV-certifikat (Domain Validation) används.

#### Krav {#adobe-managed-cert-dv-requirements}

Uppfyll dessa krav innan du konfigurerar DNS-posterna.

* Identifiera din domänvärd eller registrator om du inte redan känner till den.
* Kan redigera DNS-posterna för organisationens domän eller kontakta lämplig person som kan göra det.
* Du måste redan ha verifierat ditt konfigurerade anpassade domännamn enligt beskrivningen i dokumentet [Kontrollera domännamnsstatus](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

#### CNAME-post {#adobe-managed-cert-cname-record}

Ett kanoniskt namn eller en CNAME-post är en typ av DNS-post som mappar ett aliasnamn till ett sant eller kanoniskt domännamn. CNAME-poster används vanligtvis för att mappa en underdomän som `www.example.com` till den domän som är värd för den underdomänens innehåll.

Logga in på din DNS-tjänstleverantör och skapa en `CNAME`-post för att peka ditt anpassade domännamn mot målet, som i följande tabell.

| CNAME | Anpassad domändämpningspunkt till mål |
| --- | --- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

#### APEX-post {#adobe-managed-cert-apex-record}

En domän är en anpassad domän som inte innehåller någon underdomän, till exempel `example.com`. En huvuddomän har konfigurerats med en `A`-, `ALIAS`- eller `ANAME`-post via din DNS-leverantör. Apex-domäner måste peka på specifika IP-adresser.

Lägg till följande `A`-poster i domänens DNS-inställningar via din domänleverantör.

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`


### Certifikatsteg som hanteras av kund {#customer-managed-cert-steps}

Om du valde certifikattypen *Kundhanterat certifikat* utför du följande steg i dialogrutan **Verifiera domän**.

![Kundhanterade certifikatsteg](/help/implementing/cloud-manager/assets/cdn/cdn-create-customer-cert.png)

Du måste lägga till och verifiera en TXT-post för att kunna verifiera den domän som används.

En textpost (kallas även TXT-post) är en typ av resurspost i DNS (Domain Name System). Du kan associera godtycklig text med ett värdnamn. Den här texten kan innehålla läsbara detaljer som server- eller nätverksinformation.

Cloud Manager använder en specifik TXT-post för att godkänna att en domän är värd för en CDN-tjänst. Skapa en DNS TXT-post i zonen som tillåter Cloud Manager att distribuera CDN-tjänsten med den anpassade domänen och associera den med serverdelstjänsten. Den här associationen står helt under din kontroll och godkänner att Cloud Manager skickar innehåll från tjänsten till en domän. Detta tillstånd får beviljas och återkallas. TXT-posten är specifik för domänen och Cloud Manager-miljön.

#### Krav {#customer-managed-cert-requirements}

Uppfyll dessa krav innan du lägger till en TXT-post.

* Identifiera din domänvärd eller registrator om du inte redan känner till den.
* Kan redigera DNS-posterna för organisationens domän eller kontakta lämplig person som kan göra det.
* Lägg först till ett anpassat domännamn enligt beskrivningen ovan i den här artikeln.

#### Lägg till en TXT-post för verifiering {#customer-managed-cert-verification}

1. I dialogrutan **Verifiera domän** visar Cloud Manager namnet och TXT-värdet som ska användas för verifiering. Kopiera det här värdet.

1. Logga in på din DNS-tjänstleverantör och hitta avsnittet med DNS-poster.

1. Lägg till `aemverification.[yourdomainname]` som **namn** för värdet och lägg till TXT-värdet exakt som det visas i fältet **Domännamn**.

   **Exempel på TXT-post**

   | Domän | Namn | TXT Value |
   | --- | --- | --- |
   | `example.com` | `_aemverification.example.com` | Kopiera hela värdet som visas i användargränssnittet i Cloud Manager. Det här värdet är specifikt för domänen och miljön. Till exempel:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
   | `www.example.com` | `_aemverification.www.example.com` | Kopiera hela värdet som visas i användargränssnittet i Cloud Manager. Det här värdet är specifikt för domänen och miljön. Till exempel:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

1. Spara TXT-posten till domänvärden.

#### Verifiera TXT-post {#customer-managed-cert-verify}

När du är klar kan du verifiera resultatet genom att köra följande kommando.

```shell
dig _aemverification.[yourdomainname] -t txt
```

Det förväntade resultatet ska visa det TXT-värde som anges på fliken **Verifiering** i dialogrutan **Lägg till domännamn** i Cloud Manager-gränssnittet.

Om din domän till exempel är `example.com` kör du:

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>Det finns flera [tillgängliga DNS-sökverktyg](https://www.ultratools.com/tools/dnsLookup). Google DoH kan användas för att leta upp TXT-postposter och identifiera om TXT-posten saknas eller är felaktig.

>[!NOTE]
>
>DNS-verifiering kan ta några timmar att behandla på grund av fördröjd DNS-spridning.
>
>Cloud Manager verifierar ägarskap och uppdaterar statusen som visas i tabellen Domäninställningar. Mer information finns i [Kontrollera det anpassade domännamnets status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

<!--
## Next Steps {#next-steps}

Now that you created your TXT entry, you can verify your domain name status. Proceed to the document [Checking Domain Name Status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) to continue setting up your custom domain name. -->

>[!TIP]
>
>TXT-posten och CNAME- eller A-posten kan anges samtidigt på den styrande DNS-servern, vilket sparar tid.
>
><!-- To do this, review the entire process of setting up a custom domain name as detailed in the document [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) taking special note of the document [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) and update your DNS settings appropriately. -->


## Lägg till ett anpassat domännamn från miljösidan {#adding-cdn-environments}

Stegen för att lägga till ett anpassat domännamn från sidan **Miljö** är desamma som när du [lägger till ett anpassat domännamn från sidan Domäninställningar](#adding-cdn-settings), men startpunkten skiljer sig åt. Följ de här stegen för att lägga till ett anpassat domännamn från sidan **Miljö**.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation och program.

1. Navigera till informationssidan **Miljöinformation** för den miljö som är av intresse.

   ![Ange domännamn på sidan Miljöinformation](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Använd tabellen **Domännamn** för att skicka det anpassade domännamnet.

   1. Ange det anpassade domännamnet.
   1. Välj SSL-certifikatet som är associerat med det här namnet i listrutan.
   1. Klicka på **+Lägg till**.

   ![Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Dialogrutan **Lägg till domännamn** öppnas på fliken **Domännamn**. Fortsätt på samma sätt som du gör för [att lägga till ett anpassat domännamn från sidan Domäninställningar](#adding-cdn-settings). —>
