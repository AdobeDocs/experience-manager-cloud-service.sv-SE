---
title: Lägg till ett anpassat domännamn
description: Lär dig hur du lägger till ett anpassat domännamn med Domäninställningar i Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d35610b204cc2e06fefa93e048c16940cf1c47c
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 0%

---


# Lägg till ett anpassat domännamn {#adding-custom-domain-name}

Lär dig hur du lägger till ett anpassat domännamn med **Domäninställningar** i Cloud Manager.

## Krav {#requirements}

Uppfyll dessa krav innan du lägger till ett anpassat domännamn i Cloud Manager.

* Du måste ha lagt till ett SSL-domäncertifikat för domänen som du vill lägga till *innan* lägger till ett anpassat domännamn enligt beskrivningen i dokumentet [Lägg till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).
* Du måste ha rollen **Affärsägare** eller **Distributionshanterare** för att lägga till ett anpassat domännamn i Cloud Manager.
* Använd det snabba nätverket eller något annat CDN (Content Delivery Network).

>[!IMPORTANT]
>
>Om du använder ett CDN som hanteras av Adobe måste du ändå lägga till din domän i Cloud Manager.

## Var ska jag lägga till egna domännamn? {#where-to-add-custom-domain-name}

Du kan lägga till ett anpassat domännamn från sidan [Domäninställningar](#adding-cdn-settings) i Cloud Manager.

När du lägger till ett anpassat domännamn hanteras domänen med det mest specifika, giltiga certifikatet. Om flera certifikat har samma domän väljs den senast uppdaterade versionen. Adobe rekommenderar att du hanterar certifikat så att det inte finns några överlappande domäner.

Stegen för de metoder som beskrivs i det här dokumentet baseras på Fast. Om du har använt ett annat CDN (Content Delivery Network) konfigurerar du din domän med det CDN som du har valt att använda.

## Lägg till ett anpassat domännamn {#adding-custom-domain-name-settings}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Klicka på ikonen ![Inställningar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Settings_18_N.svg) **Domäninställningar** på sidomenyn under **Tjänster**.

   ![Fönstret Domäninställningar](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Klicka på **Lägg till domän** i det övre högra hörnet på sidan **Domäninställningar**.

1. I dialogrutan **Lägg till domän** anger du det anpassade domännamnet som du använder i fältet **Domännamn**.
Ta inte med `http://`, `https://` eller blanksteg när du anger domännamnet.

   >[!NOTE]
   >
   >Om du behöver både `www`- och `non-www`-versioner av en domän måste du lägga till dem separat. Till exempel `example.com` och `www.example.com`.
   <!-- Marius Petria on SLACK tmp-skyline-cdn-certificates - Actually  my opinion is that this option should be explicit in UI (that was present in the initial mocks of the design but for some reason it was dropped). I think when adding a domain there should be a check mark to also add www.domain. When adding example.com Customer should be prompted with the following options: Do you also want to add www.example.com and have a redirect example.com -> www.example.com?Do you also want to add www.example.com and have a redirect www.example.com -> example.com? -->

1. Klicka på **Skapa**.

1. I dialogrutan **Verifiera domän**, i **Vilken certifikattyp tänker du använda med den här domänen?**-listrutan och välj något av följande alternativ:

   | Certifikattyp, alternativ | Beskrivning |
   | --- | --- |
   | Adobe hanterat (DV) SSL-certifikat | Välj den här certifikattypen om du vill använda ett DV-certifikat (Domain Validation). Det här alternativet är idealiskt för de flesta fall och ger grundläggande domänvalidering. Adobe hanterar och förnyar certifikatet automatiskt. |
   | SSL-certifikat som hanteras av kund (OV/EV) | Välj den här certifikattypen om du tänker använda ett EV/OV SSL-certifikat för att skydda domänen. Det här alternativet ger bättre säkerhet med OV (Organization Validation) eller EV (Extended Validation). Använd om striktare verifiering, högre tillförlitlighetsnivåer eller anpassad kontroll över certifikaten krävs. |

1. Gör något av följande i dialogrutan **Verifiera domän**, baserat på den certifikattyp du valde:

   | Om du valde certifikattypen | Beskrivning |
   | --- | ---  |
   | Adobe-hanterat certifikat | a. Slutför de [Adobe hanterade certifikatstegen](#adobe-managed-cert-steps) nedan. När du har slutfört stegen klickar du på **Verifiera** i dialogrutan **Verifiera domän**.<ul><li>DNS-verifiering kan ta några timmar att behandla på grund av fördröjd DNS-spridning.</li><li>Cloud Manager verifierar till slut ägarskap av domännamn och uppdaterar statusen i tabellen **Domäninställningar**. Mer information finns i [Kontrollera det anpassade domännamnets status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).</li>![Verifiera domänstatus](/help/implementing/cloud-manager/assets/domain-settings-verified.png)</li></ul>b. Du är nu redo att [lägga till ett Adobe-hanterat (DV) SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-adobe-managed-ssl-cert).</li></ul> |
   | Kundhanterat certifikat | a. Klicka på **OK**.<br>b. Du är nu redo att [lägga till ett SSL-certifikat som hanteras av kund (OV/EV) ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-customer-managed-ssl-cert) .<br>När du har lagt till certifikatet markeras ditt domännamn som verifierat i tabellen **Domäninställningar** . Mer information finns i [Kontrollera det anpassade domännamnets status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).</li></ul><br>![Verifiera domän för ett kundhanterat EV/OV-certifikat](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png) |

   >[!NOTE]
   >
   >Om du använder ditt eget kundhanterade SSL-certifikat (OV/EV eller DV) behöver du inte lägga till något SSL-certifikat. Den här regeln gäller också om du tänker använda ett kundhanterat CDN (Content Delivery Network) ***provider***. Gå i stället direkt till [Lägg till en CDN-konfiguration](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md) när du är klar.


### Adobe hanterade certifikatsteg {#adobe-managed-cert-steps}

Om du valde certifikattypen *Adobe hanterade certifikat* slutför du följande steg i dialogrutan **Verifiera domän**.

![Certifikatsteg som hanteras av Adobe](/help/implementing/cloud-manager/assets/cdn/cdn-create-adobe-dv-cert.png)

Du måste lägga till och verifiera en CNAME för att kunna verifiera den domän som används.

En `CNAME`-posttyp eller en `A`-posttyp dirigerar all Internettrafik för domänen till den plats där den pekar. Om den platsen inte har etablerats för att betjäna trafiken uppstår ett driftstopp. Om innehållet inte har testats kan det finnas fel i det. Det här är orsaken till att det här steget alltid utförs när testningen är klar och du är redo att börja publicera.

Om du vill konfigurera de här inställningarna måste du kontrollera om en `CNAME`- eller en apex-post måste konfigureras så att den pekar ditt anpassade domännamn mot Cloud Manager domännamn. Följande avsnitt i det här dokumentet kan hjälpa dig att avgöra vilken typ av post som passar din DNS-konfiguration.

>[!NOTE]
>
>För CDN som hanteras av Adobe tillåts endast webbplatser med ACME-validering när DV-certifikat (Domain Validation) används.

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

>[!TIP]
>
>*CNAME-posten* eller *En post* kan anges på den styrande DNS-servern för att spara tid.

<!--
![Customer managed certificate steps](/help/implementing/cloud-manager/assets/cdn/cdn-create-customer-cert.png)

To verify the domain in use, you are required to add and verify a TXT record.

A text record (also known as a TXT record) is a type of resource record in the Domain Name System (DNS). It lets you associate arbitrary text with a hostname. This text could include human-readable details like server or network information.

Cloud Manager uses a specific TXT record to authorize a domain to be hosted in a CDN service. Create a DNS TXT record in the zone that authorizes Cloud Manager to deploy the CDN service with the custom domain and associate it with the backend service. This association is entirely under your control and authorizes Cloud Manager to serve content from the service to a domain. This authorization may be granted and withdrawn. The TXT record is specific to the domain and the Cloud Manager environment.

#### Requirements {#customer-managed-cert-requirements}

Fulfill these requirements before adding a TXT record.

* Identify your domain host or registrar if you do not know it already.
* Be able to edit the DNS records for your organization's domain, or contact the appropriate person who can.
* First, add a custom domain name as described earlier in this article.

#### Add a TXT record for verification {#customer-managed-cert-verification}

1. In the **Verify domain** dialog box, Cloud Manager displays the name and TXT value to use for verification. Copy this value.

1. Log in to your DNS service provider and find the DNS records section. 

1. Add `aemverification.[yourdomainname]` as the **Name** of the value and add the TXT value exactly as it appears in the **Domain Name** field.

   **TXT record examples**

   | Domain | Name | TXT Value |
   | --- | --- | --- |
   | `example.com` | `_aemverification.example.com` | Copy the entire value displayed in the Cloud Manager UI. This value is specific to the domain and the environment. For example:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
   | `www.example.com` | `_aemverification.www.example.com` | Copy the entire value displayed in the Cloud Manager UI. This value is specific to the domain and the environment. For example:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

1. Save the TXT record to your domain host.

#### Verify TXT record {#customer-managed-cert-verify}

When you are done, you can verify the result by running the following command.

```shell
dig _aemverification.[yourdomainname] -t txt
```

The expected result should display the TXT value provided on the **Verification** tab of the **Add Domain Name** dialog of the Cloud Manager UI.

For example, if your domain is `example.com`, then run:

```shell
dig TXT _aemverification.example.com -t txt
```


>[!TIP]
>
>There are several [DNS lookup tools](https://www.ultratools.com/tools/dnsLookup) available. Google DoH can be used to look up TXT record entries and identify if the TXT record is missing or erroneous.

-->



<!--
## Next Steps {#next-steps}

Now that you created your TXT entry, you can verify your domain name status. Proceed to the document [Checking Domain Name Status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) to continue setting up your custom domain name. -->


><!-- The TXT entry and the CNAME or A Record can be set simultaneously on the governing DNS server, thus saving time. -->
>
><!-- To do this, review the entire process of setting up a custom domain name as detailed in the document [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) taking special note of the document [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) and update your DNS settings appropriately. -->


