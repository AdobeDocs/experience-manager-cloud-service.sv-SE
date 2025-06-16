---
title: Felsökning 403 Otillåtna fel vid inskickning av Edge Delivery Services-formulär
description: Lär dig att diagnostisera och åtgärda 403 Otillåtna fel när du skickar formulär från Edge Delivery Services till AEM Publish. Den här guiden innehåller vanliga orsaker, bland annat CORS, Dispatcher regler och problem med referensfilter.
feature: Edge Delivery Services
role: Admin, Developer
source-git-commit: 3130a6fa8a8b244707f6578034ab274f6038ced6
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 0%

---


# Felsökning 403 Otillåtna fel vid inskickning av Edge Delivery Services-formulär {#troubleshooting-403-forbidden-edge-delivery}

När du skickar formulär från Edge Delivery Services till AEM Publish kan du råka ut för ett **403-fel** som inte tillåts. Detta fel indikerar att servern vägrar att behandla begäran, vanligtvis på grund av säkerhetskonfigurationer. Den här artikeln hjälper dig att identifiera och lösa de vanligaste orsakerna till problemet.

## Problembeskrivning

Användarna får ett **403-fel** när de skickar formulär från Edge Delivery Services till AEM Publish. Felet visas som:

- HTTP-statuskod: 403
- Felmeddelande: &quot;Åtkomst nekad&quot; eller &quot;Åtkomst nekad&quot;
- Formuläröverföringen misslyckas utan att AEM inskickningsserver nås

Det här problemet uppstår ofta i Edge Delivery Services-integreringar där formulär som lagras på Edge-domäner (`.aem.live`, `.aem.page`, `.hlx.page`, `.hlx.live`) försöker skicka data till AEM Publish-instanser.

>[!IMPORTANT]
>
>Med obestridliga inställningar kan flera webbplatser lagras i samma databas. Varje webbplatsdomän måste läggas till individuellt i tillåtelselista för att formulärinskickningar ska fungera korrekt.
>
>**Exempel:**
>
>- Databas: `https://github.com/adobe/abc`
>- Plats 1: `main--abc--adobe.aem.live`
>- Plats 2: `main--abc1--adobe.aem.live`
>
>Båda domänerna måste ha separata tillåtelselista-poster för att formuläret ska kunna skickas från båda platserna.

## Vanliga orsaker och lösningar

Ett 403-fel som inte får användas när formulär skickas från Edge Delivery Services kan ha flera orsaker. Följ de här felsökningsstegen för att:

### 1. CORS (Cross-Origin Resource Sharing) Issues

**Symtomen:**

- Webbläsarkonsolen visar CORS-relaterade felmeddelanden
- På fliken Nätverk visas den begäran som blockeras innan servern nås
- Felmeddelanden med texten&quot;Cross Origin Request Blocked&quot;

**Diagnos:**

1. Open browser Developer Tools (F12)
2. Kontrollera fliken Konsol för CORS-felmeddelanden
3. Sök efter meddelanden som: `Access to fetch at 'https://publish-xxx.adobeaemcloud.com' from origin 'https://main--repo--owner.aem.live' has been blocked by CORS policy`

**Lösning:**
Konfigurera CORS-inställningar i AEM för att tillåta begäranden från dina specifika Edge Delivery-webbplatsdomäner:

```apache
# Developer Localhost
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Edge Delivery Sites - Add each site domain individually
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc--adobe\.aem\.live$)#" CORSTrusted=true
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc1--adobe\.aem\.live$)#" CORSTrusted=true

# Legacy Franklin domains (if still in use)
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

>[!NOTE]
>
>Ersätt `main--abc--adobe.aem.live` och `main--abc1--adobe.aem.live` med de faktiska webbplatsdomänerna. Varje plats som lagras från samma databas kräver en separat CORS-konfigurationspost.

Detaljerad CORS-konfiguration finns i [CORS-konfigurationsguiden](https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors).

### &#x200B;2. Dispatcher regler

**Symtomen:**

- 403-fel inträffar utan CORS-meddelanden i webbläsarkonsolen
- Begäran når servern men blockeras av Dispatcher
- Ett fel inträffar innan AEM programlager nås

**Diagnos:**

1. Kontrollera om URL:en för begäran matchar eventuella Dispatcher-filterregler
2. Granska Dispatcher-konfigurationen för `/filter` regler som kan blockera POST-begäranden
3. Verifiera att slutpunkten för formuläröverföring tillåts i Dispatcher-konfigurationen

**Lösning:**
Uppdatera Dispatcher-konfigurationen för att tillåta formuläröverföringsbegäranden:

1. Kontrollera att slutpunkter för POST-begäranden till formulärinskickning tillåts
2. Lägg till lämpliga filterregler för Edge Delivery-domäner
3. Kontrollera att sökvägen till överföringsservern inte är blockerad

Exempel på Dispatcher filterkonfiguration:

```apache
/filter {
  # Allow POST requests to form submission servlet
  /0100 { /type "allow" /method "POST" /url "/content/forms/af/*" }
  /0101 { /type "allow" /method "POST" /url "/adobe/forms/af/submit/*" }
  /0102 { /type "allow" /method "POST" /url "/content/forms/portal/submit/adaptiveform" }
}
```

### &#x200B;3. Problem med referensfilter

**Symtomen:**

- 403-fel utan CORS-problem i webbläsarkonsolen
- Begäran når AEM men avvisas av Sling Referer-filter
- Ett fel inträffar i AEM programlager

**Diagnos:**
Kontrollera AEM felloggar för refuseringsmeddelanden för referensfilter:

1. [Få åtkomst till AEM Cloud-tjänstloggar via Cloud Manager](/help/implementing/cloud-manager/manage-logs.md)
2. Sök efter poster i `aemerror.log` som innehåller:
   - &quot;Refererarfiltret avvisades&quot;
   - &quot;org.apache.sling.security.impl.ReferrerFilter&quot;
   - Meddelanden som indikerar fel vid referensvalidering

**Exempel på loggpost:**

```
[ERROR] org.apache.sling.security.impl.ReferrerFilter Referrer filter rejected request with referrer 'https://main--abc--adobe.aem.live' for POST /content/forms/af/submit
```

**Lösning:**
Konfigurera referensfiltret så att dina specifika Edge Delivery-webbplatsdomäner tillåts:

1. Skapa eller uppdatera OSGi-konfigurationsfilen: `org.apache.sling.security.impl.ReferrerFilter.cfg.json`

2. Lägg till följande konfiguration med dina specifika webbplatsdomäner:

   ```json
   {
     "allow.empty": false,
     "allow.hosts": [
       "main--abc--adobe.aem.live",
       "main--abc1--adobe.aem.live"
     ],
     "allow.hosts.regexp": [
       "https://.*\\.aem\\.live:443",
       "https://.*\\.aem\\.page:443",
       "https://.*\\.hlx\\.page:443",
       "https://.*\\.hlx\\.live:443"
     ],
     "filter.methods": [
       "POST",
       "PUT",
       "DELETE",
       "COPY",
       "MOVE"
     ],
     "exclude.agents.regexp": [
       ""
     ]
   }
   ```

3. Distribuera konfigurationen via Cloud Manager

>[!IMPORTANT]
>
>**Forrestless-inställningar:** Du måste lägga till varje platsdomän individuellt i arrayen `allow.hosts`. Det kanske inte räcker att bara använda regex-mönster för alla scenarier. Inkludera både specifika domäner och regex-mönster för omfattande täckning.

>[!WARNING]
>
>AEM referensfilter är inte en OSGi-konfigurationsfabrik, vilket innebär att endast en konfiguration är aktiv i en AEM-tjänst åt gången. Undvik när det är möjligt att lägga till anpassade inställningar för referensfilter, eftersom detta skriver över AEM egna konfigurationer och kan störa produktfunktioner.

## Diagnostiksteg

Följ de här stegen för att identifiera orsaken till ditt 403-fel:

### Steg 1: Kontrollera webbläsarkonsolen

1. Open browser Developer Tools (F12)
2. Navigera till fliken Konsol
3. Försök att skicka formulär
4. Leta efter CORS-relaterade felmeddelanden

**Om det finns CORS-fel:** Följ CORS-lösningen ovan.
**Om det inte finns några CORS-fel:** Fortsätt till steg 2.

### Steg 2: Kontrollera fliken Nätverk

1. Open browser Developer Tools (F12)
2. Navigera till fliken Nätverk
3. Försök att skicka formulär
4. Kontrollera information om misslyckade begäranden
5. Titta på svarsrubriker och status

**Om begäran inte når servern:** Sannolikt ett Dispatcher-problem.
**Om begäran når servern men misslyckas:** Troligen ett problem med referensfilter.

### Steg 3: Kontrollera AEM-loggar

1. Använd Cloud Manager
2. Navigera till miljöer → Din miljö → Loggar
3. Hämta eller visa `aemerror.log`
4. Söka efter poster runt tiden för formulärinlämning
5. Leta efter referensfilter eller säkerhetsrelaterade meddelanden

## Förebyggande och bästa metoder

### &#x200B;1. Korrekt konfiguration under installationen

- Konfigurera inställningar för CORS, Dispatcher och Referrer-filter under den första Edge Delivery Services-installationen
- **För varje ny plats:** Lägg till den specifika domänen i alla tillåtelselista (CORS, referensfilter)
- Testa formulärskickning i utvecklingsmiljö innan du publicerar

### &#x200B;2. Miljöspecifika konfigurationer

- Använd olika konfigurationer för utvecklings-, staging- och produktionsmiljöer
- Inkludera localhost-domäner för lokal utvecklingstestning
- **Dokumentera alla webbplatsdomäner** som behöver åtkomst till tillåtelselista för din databas

### &#x200B;3. Övervakning och loggning

- Ställ in loggövervakning för avvisningar av referensfilter
- Implementera korrekt felhantering i koden för att skicka formulär
- Använd webbläsarutvecklarverktygen under testningen

### &#x200B;4. Dokumentation och teamkunskap

- **Underhåll ett register** för alla webbplatsdomäner med samma databas
- Utvecklingsteamet för utbildning i felsökningssteg
- Underhåll en checklista för Edge Delivery Services formulärinställningar
- **Uppdatera tillåtelselista** när nya webbplatser skapas från befintliga databaser

## Platsdomänhantering för automatiska inställningar

Med Helix-5 och kraftlösa arkitekturer följer du dessa riktlinjer:

### När nya platser skapas

1. **Identifiera webbplatsdomänen** (t.ex. `main--newsite--adobe.aem.live`)
2. **Uppdatera CORS-konfigurationen** så att den nya domänen inkluderas
3. **Uppdatera referensfilter** så att den nya domänen inkluderas i `allow.hosts`
4. **Testa formulärskickning** från den nya webbplatsen
5. **Dokumentera den nya domänen** i platsregistret

### Namngivningsmönster för domäner

- Standardmönster: `{branch}--{site}--{owner}.aem.live`
- Varje webbplats får en unik domän även när samma databas delas
- Både `.aem.live` och `.aem.page` domäner kan användas

### Konfigurationshantering

- Använd specifika domänposter i `allow.hosts` för bättre säkerhet
- Tillägg med regex-mönster för bredare täckning
- Granska och uppdatera tillåtelselista regelbundet när webbplatser läggs till eller tas bort

## Ytterligare resurser

- [Filterkonfiguration för referent med AEM Headless](/help/headless/deployment/referrer-filter.md)
- [CORS - konfigurationsguide](https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)
- [Om resursdelning mellan ursprung](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)
- [Edge Delivery Services Forms Documentation](/help/edge/docs/forms/universal-editor/publish-forms.md)

## Relaterade ämnen

- [Konfigurera överföringsåtgärder](/help/forms/configuring-submit-actions.md)
- [Forms Submission Service](/help/forms/forms-submission-service.md)
- [Edge Delivery Services - översikt](/help/edge/overview.md)


**Behöver du mer hjälp?** Om du fortfarande får problem efter att du har följt dessa felsökningssteg kontaktar du Adobe kundsupport med:

- Dina specifika felmeddelanden
- Information om AEM Cloud-tjänstmiljö
- **Alla Edge Delivery Services-webbplatsdomäner** som behöver åtkomst för att skicka formulär
- Relevanta loggposter från tidpunkten för felet

**Behöver du mer hjälp?** Om du fortfarande får problem efter att du har följt dessa felsökningssteg kontaktar du Adobe kundsupport med:

- Dina specifika felmeddelanden
- Information om AEM Cloud-tjänstmiljö
- Edge Delivery Services domäninformation
- Relevanta loggposter från tidpunkten för felet
