---
title: Översikt över AEM Forms-Edge Delivery Services
description: AEM Forms Edge Delivery Services som tagits fram för bästa prestanda och som gör det möjligt att förutse framtiden för smidig datainsamling och användarengagemang.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 0%

---

# AEM Forms-Edge Delivery Services

Effektivisera framtagningen av blanketter och få snabbare ifyllnad med Adobe AEM Forms-Edge Delivery Services. Dessa kraftfulla, sammanställbara tjänster gör att du kan skapa formulär i enterpriseklass med enastående prestanda och visuella fördelar. AEM prioriterar både användarupplevelsen och affärsmålen, vilket ger blixtsnabba laddningstider och ökad konvertering av formulär.

Du kan använda tjänsten för att:

* **Skapa enastående registreringsupplevelser**: Skapa registreringsupplevelser som läses in och återges snabbt, även på långsamma internetanslutningar. Snabbare inläsningstider och optimerad användarupplevelse bidrar till snabbare ifyllnad av formulär och förbättrad konverteringsgrad.

* **Skapa registreringsupplevelser med valfria verktyg**: Öka redigeringseffektiviteten genom att frikoppla innehållskällor. Använd båda **dokumentbaserad redigering** (Microsoft SharePoint eller Google Drive) och **AEM** (AEM). Det innebär att du kan arbeta med flera innehållskällor i samma formulär och använda de redigeringsverktyg du föredrar, till exempel Microsoft Excel, Google Sheets eller Adaptiv Forms Editor.

* **Använd utvecklarvänliga verktyg:** AEM Forms använder HTML, modern CSS och vanilj JavaScript för att skapa exceptionella upplevelser utan den vanliga overheadkostnaden. Utvecklare med grundläggande kunskaper i HTML, CSS och JS bör kunna bygga egna komponenter och behöver inte lära sig något specifikt språk eller ramverk. Du behöver inte vänta på en pipeline, checka in koden i Github och ändringarna är aktuella. Dessutom behövs ingen pipeline eller väntan, checka in koden i Github och ändringarna är live.


## Skapa en digital registreringsupplevelse

AEM Forms erbjuder båda **dokumentbaserad redigering** (Microsoft SharePoint eller Google Drive) och **AEM** (AEM). Du kan använda [Adaptivt Forms-block](/help/edge/docs/forms/create-forms.md) för att lägga till ett formulär på din Edge Delivery Services webbplats.


>[!BEGINTABS]

>[!TAB Dokumentbaserad redigering]

Dokumentbaserad redigering är ett mångsidigt alternativ som passar bra för att skapa enkla formulär med grundläggande funktioner. Det gör att du kan integrera olika indatatyper som textfält, listrutor och alternativknappar, vilket gör att du kan samla in användardata effektivt. Det innehåller en grundläggande version av regler för att lägga till dynamiskt beteende i formulär. De viktigaste funktionerna för dokumentbaserad redigering är:

* **[HTML5-baserade formulärfältskomponenter](/help/edge/docs/forms/form-components.md)**: Med AEM Forms Edge Delivery Services kan du skapa användarvänliga och interaktiva formulär med hjälp av formulärkomponenter baserade på HTML5 [indatatyper](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textområde</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">välj</a>och <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fältuppsättning</a>  -element. Dessa komponenter klarar olika typer av datainsamling och kan enkelt anpassas efter dina specifika behov.

* **Tillgänglighet**: Fälten i formulärblocket är tillgängliga. Varje etikett länkas med respektive indataelement och ID:n genereras automatiskt för länkning. Beskrivningar som är associerade med fält länkas via attributet aria-describedby. Tangentbordsnavigering med standardtangenterna Tabb/Skift + Tabb stöds.

* **[Stilar](/help/edge/docs/forms/style-theme-forms.md)**: Varje formulärfält har en fast HTML-struktur som enkelt kan dekoreras med anpassade CSS- eller JavaScript-filer. Väljare för målfält i CSS och JS tillhandahålls baserat på typ och namn. Du kan enkelt skapa nya väljare på grund av den standardiserade strukturen och stilen på formuläret.

* **Grundregler**: Skapa enkelt logik som justerar fältets synlighet, validering och beteende baserat på användarindata eller fördefinierade villkor. Regler är ett flexibelt och intuitivt sätt att lägga till intelligens i formulären, vilket säkerställer att de smidigt kan anpassas utifrån användarens indata.

* **Valideringar**: Innan formuläret skickas valideras det och ogiltiga fält markeras med felmeddelanden som visas för användaren. Adaptiva Forms-block har stöd för all formulärvalidering i HTML, som stöds av moderna webbläsare, och erbjuder ytterligare valideringsfunktioner som valideringsskript, filstorlek, filtyp, total filstorlek med mera.

* **Filöverföringar**: Du kan lägga till funktioner för bifogade filer i formulären. Oavsett om du behöver samla in dokument, bilder eller andra filer från användarna så är filöverföringen enkel. Med anpassade hanteringsalternativ tillgängliga kan du anpassa filöverföringsprocessen så att den passar dina specifika behov.

* **reCAPTCHA**: Dra nytta av den smidiga integreringen av Google reCAPTCHA i formulären med vårt OTB-stöd. Skydda era formulär mot bedrägliga aktiviteter, skräppost och missbruk, samtidigt som ni bibehåller en smidig och oavbruten användarupplevelse. Adaptivt Forms-block har stöd för reCaptcha V3 och reCaptcha Enterprise.

* **Skicka e-postmeddelanden när formulär skickas**: Eliminera krånglet med manuella uppföljningar och säkerställ snabb kommunikation med vår inbyggda e-postautomatisering för att skicka in formulär. Med den här integrerade lösningen kan ni enkelt meddela berörda parter, inklusive att skicka formulärdata, när någon fyller i ett formulär på webbplatsen. Inget behov av komplexa konfigurationer eller andra verktyg - det är klart att användas direkt.

>[!TAB AEM]

Med AEM kan du skapa mer komplexa och interaktiva formulär. Förutom funktionerna för dokumentbaserad redigering har AEM följande extrafunktioner:

* Avancerade regler: Definiera logiska åtgärder i formulären. Du kan använda regler för att villkorligt visa eller dölja formuläravsnitt, fylla i fält i förväg baserat på användarindata och utföra olika valideringar för att säkerställa dataintegriteten.

* Utbyggbarhet på serversidan: Utöka funktionaliteten i formulären genom att integrera dem med logik på serversidan. På så sätt kan du utföra komplexa beräkningar, interagera med externa system och automatisera specifika uppgifter baserat på användaråtgärder i formuläret.
* Effektivisera arbetsflöden och datahantering: Utnyttja kraften i AEM för att:
   * Utforma användarvänliga formulär med AEM redigerare.
   * Generera ett&quot;arkiveringsdokument&quot; för säker och manipuleringssäker arkivering av inskickade data.
   * Underlätta e-signering med Adobe Sign för en smidig och säker signeringsprocess.
   * Automatisera affärsprocesserna genom AEM arbetsflöden, aktivera åtgärder som bygger på inskickade formulär.
   * Integrera enkelt med olika datakällor, vilket möjliggör smidigt dataflöde och datautbyte.

>[!ENDTABS]








## Börja skapa formulär

<div>

<style>
    .card-container {
        width: calc(33.33% - 10px);;
        margin: 5px;
        border: 1px solid #ccc;
        border-radius: 5px;
        padding: 5px;
        box-sizing: border-box;
        transition: background-color 0.3s ease; /* Adding transition effect */
    }
    .card-container:hover {
        background-color: #f0f0f0; /* Changing background color on hover */
    }
</style>

<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: -5px;">
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md">
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Skapa ett formulär med hjälp av eds-formulär" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Skapa ett formulär med Google eller Microsoft Excel</b>
        </a>
        <p>Skapa formulär som läses in och återges snabbt och automatiskt flödar om på mobila enheter.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Skicka formulär" alt="Använd formulärfragment i ett EDS-formulär" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Skicka formulär till kalkylblad</b>
        </a>
        <p>Skicka formulär direkt till Microsoft Excel- eller Google-ark.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Använda format eller teman i ett formulär" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Anpassa ett tema</b>
        </a>
        <p>Skapa en enhetlig varumärkesbild genom att använda samma tema i alla formulär.</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Lägga till valideringar i formulärfält" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Använd fältvalideringar</b>
        </a>
        <p>Minska antalet fel och frustration genom att kontrollera indata i blanketterna för korrekt formatering.</p>
    </div> 
            <div class="card-container">
        <a href="/help/edge/docs/forms/rules-forms.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Använd regler för att lägga till dynamiskt beteende i ett formulär" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Använd regler för att lägga till dynamiskt beteende i ett formulär</b>
        </a>
        <p>Återanvänd förkonfigurerade fragment i flera formulär.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Översätta ett EDS-formulär" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Översätta ett formulär</b>
        </a>
        <p>Nå ut bättre med formulären och håll kostnaderna i schack.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Lägga till repeterbara avsnitt i ett EDS-formulär" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Lägga till repeterbara avsnitt</b>
        </a>
        <p>Skapa och lägg enkelt till repeterbara avsnitt i ett formulär.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="Skapa anpassade blankettkomponenter med JavaScript och CSS"  style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Skapa anpassade komponenter</b>
        </a>
        <p>Använd JavaScript och CSS som standard för att skapa komponenter och teman.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Använd reCAPTCHA i ett EDS-formulär" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Använd reCAPTCHA</b>
        </a>
        <p>Använd OTB reCAPTCHA-integrering för robust skydd för skräppost och robotar.</p>
    </div>


</div>


</br>
