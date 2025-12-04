---
title: CDN i AEM AS A CLOUD SERVICE
description: Lär dig hur du använder det CDN som hanteras av AEM och hur du pekar ditt eget CDN mot det CDN som hanteras av AEM.
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
role: Admin
source-git-commit: 7f00e68eac0b1e0090bdb57a8188af7bbe21ad1b
workflow-type: tm+mt
source-wordcount: '1768'
ht-degree: 2%

---


# CDN i AEM AS A CLOUD SERVICE {#cdn}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="CDN i AEM AS A CLOUD SERVICE"
>abstract="AEM som Cloud Service levereras med ett inbyggt CDN. Dess huvudsakliga syfte är att minska latensen genom att leverera tillgängligt innehåll från CDN-noder nära webbläsaren. Det är helt managerat och konfigurerat för optimal prestanda i AEM-program."

AEM as a Cloud Service har ett integrerat CDN, som utformats för att minska latensen genom att leverera tillgängligt innehåll från kantnoder nära användarens webbläsare. Detta fullständigt hanterade CDN är optimerat för AEM programprestanda.

CDN som hanteras av AEM uppfyller de flesta kundernas krav på prestanda och säkerhet. För publiceringsnivån kan kunderna välja att dirigera trafik via sitt eget CDN, som de måste hantera. Det här alternativet är tillgängligt från fall till fall, särskilt när kunderna har befintliga integreringar med en CDN-leverantör som är svår att ersätta.

Kunder som vill publicera på Edge Delivery Services-nivå kan dra nytta av Adobe hanterade CDN. Se [Hanterat CDN för Adobe](#aem-managed-cdn). <!-- CQDOC-21758, 5b -->


<!-- ERROR: NEITHER URL IS FOUND (HTTP ERROR 404) Also, see the following videos [Cloud 5 AEM CDN Part 1](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part1.html) and [Cloud 5 AEM CDN Part 2](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part2.html) for additional information about CDN in AEM as a Cloud Service. -->

## Hanterat CDN från Adobe {#aem-managed-cdn}

<!-- CQDOC-21758, 5a -->

För att förbereda dig för innehållsleverans med AEM inbyggda CDN via Cloud Manager självbetjäningsgränssnitt kan du utnyttja Adobe hanterade CDN-funktioner. Med den här funktionen kan du hantera CDN-hantering för självbetjäning, inklusive konfigurera och installera SSL-certifikat som DV-certifikat (Domain Validation) eller EV-/OV-certifikat (Extended/Organization Validation). Mer information om de här metoderna finns i:

* [EDGE DELIVERY SERVICES i CLOUD MANAGER](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)
* [Introduktion till anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
* [Introduktion till SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)
* [Konfigurera ett CDN](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md)

**Begränsa trafik**

Som standard kan all offentlig trafik för en AEM-hanterad CDN-installation gå vidare till publiceringstjänsten, både för produktionsmiljöer och icke-produktionsmiljöer (utveckling och stadium). Du kan begränsa trafiken till publiceringstjänsten för en viss miljö (t.ex. begränsa mellanlagring med ett intervall av IP-adresser) via Cloud Manager användargränssnitt.

Mer information finns i [Hantera IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

>[!CAUTION]
>
>AEM hanterade CDN hanterar endast förfrågningar från tillåtna IP-adresser. Om du pekar ditt eget CDN mot det CDN som hanteras av AEM måste du se till att IP-adresserna för ditt CDN ingår i IP Tillåtelselista.

### Konfigurera trafik på CDN {#cdn-configuring-cloud}

Du kan konfigurera trafiken vid CDN på olika sätt, bland annat:

* blockera skadlig trafik med [trafikfilterregler](/help/security/traffic-filter-rules-including-waf.md) (inklusive avancerade WAF-regler som kan licensieras)
* ändrar typen av [begäran och svar](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations)
* använder 301/302 [omdirigeringar på klientsidan](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors)
* deklarerar [ursprungliga väljare](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors) för att återföra proxy till andra objekt än AEM

Använd YAML-filer i Git för att konfigurera dessa funktioner. Använd dessutom Cloud Manager [Config Pipeline](/help/implementing/dispatcher/cdn-configuring-traffic.md) för att distribuera dem.

### Konfigurera CDN-felsidor {#cdn-error-pages}

Du kan konfigurera en CDN-felsida så att den ersätter standardsidan utan varumärke. Den här anpassade sidan visas om AEM inte är tillgängligt. Mer information finns i [Konfigurera CDN-felsidor](/help/implementing/dispatcher/cdn-error-pages.md).

### Rensa cachelagrat innehåll vid CDN {#purge-cdn}

Att ställa in TTL med HTTP-huvudet Cache-Control är ett effektivt sätt att balansera innehållets leveransprestanda och innehållets aktualitet. I scenarier där det är viktigt att leverera uppdaterat innehåll omedelbart kan det dock vara bra att rensa CDN-cachen direkt.

Läs om hur [konfigurerar en rensnings-API-token](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) och [rensar cachelagrat CDN-innehåll](/help/implementing/dispatcher/cdn-cache-purge.md).

### Grundläggande autentisering vid CDN {#basic-auth}

För användarvänliga autentiseringssituationer, inklusive affärsintressenter som granskar innehåll, skyddar du innehållet genom att visa en grundläggande autentiseringsdialog som kräver ett användarnamn och lösenord. [Läs mer](/help/implementing/dispatcher/cdn-credentials-authentication.md).

## Kundhanterad CDN pekar på AEM hanterade CDN {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="Customer CDN (eller proxy) pekar på AEM Managed CDN"
>abstract="AEM som Cloud Service erbjuder ett alternativ för kunder att använda sitt befintliga CDN. För publiceringsnivån kan kunderna även peka på det från sitt eget CDN, som de måste hantera. Detta scenario tillåts från fall till fall, baserat på att vissa krav uppfylls, inklusive, men inte begränsat till, den kund som har en äldre integrering med sin CDN-leverantör som är svår att överge."

Om en kund måste använda sitt befintliga CDN (eller någon annan omvänd proxy, till exempel en belastningsutjämnare eller en WAF), kan de hantera det och peka det mot det CDN som hanteras av AEM, förutsatt att följande uppfylls:

* Kunden måste ha ett befintligt CDN som är betungande att ersätta.
* Kunden måste hantera det.
* Kunden måste kunna konfigurera CDN så att det fungerar med AEM as a Cloud Service - se konfigurationsinstruktionerna nedan.
* Kunden måste ha tekniska CDN-experter som är i bruk om det uppstår några ärenderelaterade problem.
* Kunden måste utföra och klara ett lasttest innan han/hon kan börja producera.

Konfigurationsanvisningar:

1. Peka ditt CDN mot Adobe CDN:s ingress som ursprungsdomän. Exempel: `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. Ställ in SNI på Adobe CDN:s ingress.
1. Ange värdhuvudet som den ursprungliga domänen. Till exempel: `Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. Ange `X-Forwarded-Host`-huvudet med domännamnet så att AEM kan identifiera värdhuvudet. Till exempel: `X-Forwarded-Host:example.com`.
1. Ange `X-AEM-Edge-Key`. Värdet bör konfigureras med en Cloud Manager-konfigurationspipeline, vilket beskrivs i [den här artikeln](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

   * Behövs så att Adobe CDN kan validera källan för förfrågningarna och skicka `X-Forwarded-*`-huvudena till AEM-programmet. `X-Forwarded-For` används till exempel för att fastställa klient-IP. Det blir alltså den betrodda anroparen (det vill säga kundens hanterade CDN) som ansvarar för att `X-Forwarded-*`-huvudena är korrekta (se anteckningen nedan).
   * Du kan även blockera åtkomsten till Adobe CDN:s ingress när det inte finns någon `X-AEM-Edge-Key`. Informera Adobe om du behöver direktåtkomst till Adobe CDN:s ingress (blockeras).

I avsnittet [Exempel på CDN-leverantörskonfigurationer](#sample-configurations) finns konfigurationsexempel från ledande CDN-leverantörer.

Innan du godkänner direkttrafik bör du med Adobe kundsupport validera att hela trafikflödet fungerar korrekt.

När du har angett `X-AEM-Edge-Key` kan du testa att begäran dirigeras korrekt enligt följande.

I Linux®:

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

I Windows:

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com --header "X-Forwarded-Host: example.com" --header "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

>[!NOTE]
>
>När du använder ditt eget CDN behöver du inte installera domäner och certifikat i Cloud Manager. Routningen i Adobe CDN görs med standarddomänen `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com` som ska skickas i begärandehuvudet `Host`. Om begärandehuvudet `Host` skrivs över med ett anpassat domännamn kan begäran slussas genom Adobe CDN felaktigt eller resultera i 421 fel.

>[!NOTE]
>
>Kunder som hanterar sitt eget CDN bör säkerställa integriteten för de huvuden som skickas till AEM CDN. Vi rekommenderar till exempel att kunderna tar bort alla `X-Forwarded-*`-huvuden och anger dem som kända och kontrollerade värden. `X-Forwarded-For` bör till exempel innehålla klientens IP-adress, medan `X-Forwarded-Host` bör innehålla webbplatsens värd.

>[!NOTE]
>
>Sandlådeprogrammiljöer har inte stöd för ett CDN som kunden tillhandahåller.

Det extra hoppet mellan kundens CDN och AEM CDN behövs bara om det finns ett cacheminne. Genom att använda de strategier för cacheoptimering som beskrivs i den här artikeln bör tillägget av en kund-CDN endast medföra försumbar fördröjning.

Kundens CDN-konfiguration stöds för publiceringsnivån, men inte framför författarnivån.

### Felsökningskonfiguration

Om du vill felsöka en BYOCDN-konfiguration använder du huvudet `x-aem-debug` med värdet `edge=true`. Till exempel:

I Linux®:

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -v -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>" -H "x-aem-debug: edge=true"
```

I Windows:

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -v --header "X-Forwarded-Host: example.com" --header "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>" --header "x-aem-debug: edge=true"
```

Den här processen speglar vissa egenskaper som används i begäran i svarshuvudet `x-aem-debug`. Till exempel:

```
x-aem-debug: byocdn=true,edge=true,edge-auth=edge-auth,edge-key=edgeKey1,X-AEM-Edge-Key=set,host=publish-p87058-e257304-cmstg.adobeaemcloud.com,x-forwarded-host=wknd.site,adobe_unlocked_byocdn=true
```

Den här processen gör att du kan verifiera information som värdvärden, edge-autentiseringskonfiguration och det x-forward-host-rubrikvärdet. Den identifierar också om en kantnyckel är inställd och vilken tangent som används om det finns en matchning.

>[!NOTE]
>
>Du kan använda en Rapid Development Environment (RDE) för att distribuera och testa konfigurationen:
>
>* [Snabba utvecklingsmiljöer](/help/implementing/developing/introduction/rapid-development-environments.md)
>* [Så här använder du Rapid Development Environment](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use#deploy-configuration-yaml-files)

### Exempel på CDN-leverantörskonfigurationer {#sample-configurations}

Nedan visas flera konfigurationsexempel från flera ledande CDN-leverantörer.

**Akamai**

![Akamai1](assets/akamai1.png "Akamai")
![Akamai2](assets/akamai2.png "Akamai")

**Amazon CloudFront**

![CloudFront1](assets/cloudfront1.png "Amazon CloudFront")
![CloudFront2](assets/cloudfront2.png "Amazon CloudFront")

**Cloudflare**

![Cloudflare1](assets/cloudflare1.png "Cloudflare")
![Cloudflare2](assets/cloudflare2.png "Cloudflare")

### Vanliga fel {#common-errors}

De angivna exempelkonfigurationerna visar de basinställningar som behövs. En kundkonfiguration kan dock ha andra regler som påverkar hur du tar bort, redigerar eller ordnar om de rubriker som behövs för att AEM as a Cloud Service ska kunna betjäna trafiken. Nedan visas vanliga fel som inträffar när en kundhanterad CDN konfigureras för att peka mot AEM as a Cloud Service.

**Omdirigering till slutpunkten för publiceringstjänsten**

När en begäran tar emot ett 403 ej tillåtet svar betyder det att begäran saknar vissa obligatoriska rubriker. En vanlig orsak till detta är att CDN hanterar både API- och `www`-domäntrafik, men inte lägger till rätt rubrik för domänen `www`. Du kan lösa det här problemet genom att kontrollera AEM as a Cloud Service CDN-loggarna och verifiera begäranderubrikerna.

**Fel 421 Feldirigerad omdirigering**

Ett 421-fel med meddelandet `Requested host does not match any Subject Alternative Names (SANs) on TLS certificate` anger att HTTP `Host` inte matchar några värdar som finns i certifikatet. Det här problemet indikerar vanligtvis att antingen `Host` eller SNI-inställningen är fel. Kontrollera att både `Host`- och SNI-inställningarna pekar på värden för publish-p&lt;PROGRAM_ID>-e.adobeaemcloud.com.

**För många omdirigeringsslinga**

När en sida får en &quot;för många omdirigeringar&quot;-slinga läggs en del begärandehuvud till i CDN som matchar en omdirigering som tvingar den tillbaka till sig själv. Exempel:

* En CDN-regel skapas för att matcha antingen apex-domänen eller www-domänen och lägger endast till X-Forwarded-Host-huvudet i apex-domänen.
* En begäran om en apex-domän matchar den här CDN-regeln, som lägger till apex-domänen som X-Forwarded-Host-huvud.
* En begäran skickas till ursprungsläget där en omdirigering matchar värdhuvudet explicit för huvuddomänen (till exempel ^example.com).
* En omskrivningsregel utlöses, som skriver om begäran för den överordnade domänen till https med underdomänen www.
* Omdirigeringen skickas sedan till kundens kant, där CDN-regeln aktiveras på nytt och X-Forwarded-Host-huvudet för den överordnade domänen läggs till på nytt, inte www-underdomänen. Processen startar sedan om tills begäran misslyckas.

Du löser det här problemet genom att utvärdera din SSL-omdirigeringsstrategi, CDN-regler, omdirigerings- och omskrivningsregelkombinationer.

## Geolocation-rubriker {#geo-headers}

Det CDN som hanteras av AEM lägger till rubriker i varje begäran med:

* landskod: `x-aem-client-country`
* Kontinentalkod: `x-aem-client-continent`

>[!NOTE]
>
>Om det finns ett kundhanterat CDN återspeglar dessa rubriker platsen för kundens CDN-proxyserver snarare än den faktiska klienten. Kunderna bör hantera rubriker för geopositionering via sina egna CDN när de använder ett kundhanterat CDN.

Värdena för landskoderna är de Alpha-2-koder som beskrivs i [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1).

Värdena för kontinentkoderna är:

* AF Africa
* AN Antarktis
* AS Asien
* EU Europa
* NA Nordamerika
* OC Oceanien
* Sydamerika

Den här informationen är användbar för omdirigering till en annan URL utifrån den begärandes ursprungsland. Använd rubriken Variera för att cachelagra svar som är beroende av geoinformation. Omdirigeringar till en viss landningssida ska till exempel alltid innehålla `Vary: x-aem-client-country`. Om det behövs kan du använda `Cache-Control: private` för att förhindra cachelagring. Se även [Cachning](/help/implementing/dispatcher/caching.md#html-text).
