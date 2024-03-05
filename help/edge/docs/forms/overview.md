---
title: AEM Forms Edge Delivery Service - översikt
description: AEM Forms Edge Delivery Service har tagits fram för bästa prestanda och ger er möjlighet att förutse framtiden för smidig datainsamling och användarengagemang.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: d63d0f1152d0a23623c197924a44bc6b1e69fb42
workflow-type: tm+mt
source-wordcount: '1120'
ht-degree: 0%

---


# AEM Forms Edge Delivery Service

Effektivisera framtagningen av blanketter och få snabbare ifyllnad med Adobe AEM Forms Edge Delivery Service. Med denna kraftfulla, samverkande tjänst kan ni skapa formulär i företagsklass med enastående prestanda och visuella tilltalande funktioner. AEM prioriterar både användarupplevelsen och affärsmålen, vilket ger blixtsnabba laddningstider och fler slutförda formulär.

Du kan använda tjänsten för att:

* **Captivate-användare med enastående formulär**: Skapa enkelt komplexa och engagerande formulär med ett bibliotek med färdiga komponenter. Integrera enkelt reCAPTCHA, skicka formulär direkt till e-post och möjliggör smidiga filöverföringar för säkra lagringslösningar som Sharepoint, Azure Storage och Amazon S3. Du kan till och med skapa egna skräddarsydda blankettkomponenter för att förverkliga din unika vision.

* **Skapa digitala registreringsupplevelser med valfria verktyg**: Öka redigeringseffektiviteten genom att frikoppla innehållskällor. Nu kan du använda både dokumentbaserad redigering (Microsoft 365 och Google Workspace) och AEM (AEM Editors). Det innebär att du kan arbeta med flera innehållskällor på samma webbplats och använda de redigeringsverktyg du föredrar, till exempel Microsoft Excel, Google Sheets eller Adaptiv Forms Editor.

* **Bygg formulär med perfekt Lightroom-poäng**: Bygg formulär som läses in och återges snabbt, även på långsamma internetanslutningar. Snabbare inläsningstider och optimerad användarupplevelse bidrar till snabbare ifyllnad av formulär och förbättrad konverteringsgrad.

  <div>
    <style>
    .image-container {
    text-align: center; 
    }
    .image-container img {
        width: 100%; /* Set image width to 100% of the container 
    }
</style>
    <div class="image-container">
    <img src="/help/edge/assets/eds-forms-key-features.png" alt="EDS Forms Key features">
    </div>


</div>

<!--

<!--

    ![Enrollment forms](/help/edge/assets/enrollment-form.png)

* **Build forms with perfect lighthouse score**: Build forms that load and render quickly, even on slow internet connections. Faster loading times and optimized user experience contribute to higher form completion rates and improved conversion rates.

    ![perfect lighthouse score for your forms](/help/edge/assets/lighthouse-forms.png)

* **Create digital enrollment experiences with tools of your choice**: Increase authoring efficiency by decoupling content sources. Out of the box you can use both AEM authoring and document-based authoring. As such, you can work with multiple content sources on the same website and use your preferred authoring tools, such as Microsoft Excel, Google Sheets, or AEM Editors.

    ![Edge Delivery forms authoring tools](/help/edge/assets/edge-delivery-forms-authoring-tools.png)
    
<!--
* **Measure customer impact and deliver effective forms**: Use our RUM dashboards to visualize form performance and identify areas for improvement. Experiment with different versions and continuously optimize your forms for maximum effectiveness, ensuring you capture the data you need and drive better business outcomes.

* **Use Integrated services:** Use integrated services to streamline and empowers your users with a one-stop shop for managing their digital enrollment journeys. Use e-signatures, automated workflows, document of record (DoR), and seamless data integration, simplify the entire digital enrollment process, accelerate approvals, and optimizes your business workflows. 

    
    >[!NOTE]
    >[!NOTE]
    >
    >
    > WYSIWYG authoring capability, integrated services, and customer impact measuring features are available under early adopter program. You can write to aem-forms-early-adopter-program@adobe.com from your official email id to join the early adopter program and request access to the capability.

    -->

## Viktiga funktioner

* **HTML5-baserade formulärfältskomponenter**: Med AEM Forms Edge Delivery Service kan du skapa användarvänliga och interaktiva formulär med hjälp av formulärkomponenter baserade på HTML5 [indatatyper](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textområde</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">välj</a>och <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fältuppsättning</a>  -element. Dessa komponenter klarar olika typer av datainsamling och kan enkelt anpassas efter dina specifika behov.

* **Tillgänglighet**: Fälten i formulärblocket är tillgängliga. Varje etikett länkas med respektive indataelement och ID:n genereras automatiskt för länkning. Beskrivningar som är associerade med fält länkas via attributet aria-describedby. Tangentbordsnavigering med standardtangenterna Tabb/Skift + Tabb stöds.

* **Stilar**: Varje formulärfält har en fast HTML-struktur som enkelt kan dekoreras med anpassade CSS- eller JavaScript-filer. Väljare för målfält i CSS och JS tillhandahålls baserat på typ och namn. Du kan enkelt skapa nya väljare på grund av den standardiserade strukturen.

* **Regler**: Skapa enkelt logik som justerar fältets synlighet, validering och beteende baserat på användarindata eller fördefinierade villkor. Regler är ett flexibelt och intuitivt sätt att lägga till intelligens i formulären, vilket säkerställer att de smidigt kan anpassas utifrån användarens indata.

* **Valideringar**: Innan formuläret skickas valideras det och ogiltiga fält markeras med felmeddelanden som visas för användaren. Det finns olika mönster för att visa dessa fel.

Det finns några avancerade funktioner som är tillgängliga på begäran:

* **Filöverföringar**: Du kan lägga till funktioner för bifogade filer i formulären. Oavsett om du behöver samla in dokument, bilder eller andra filer från användarna så är filöverföringen enkel. Med anpassade hanteringsalternativ tillgängliga kan du anpassa filöverföringsprocessen så att den passar dina specifika behov.

* **reCAPTCHA**: Dra nytta av den smidiga integreringen av Google reCAPTCHA i formulären med vårt OTB-stöd. Skydda era formulär mot bedrägliga aktiviteter, skräppost och missbruk, samtidigt som ni bibehåller en smidig och oavbruten användarupplevelse.

* **Skicka e-postmeddelanden när formulär skickas**: Eliminera krånglet med manuella uppföljningar och säkerställ snabb kommunikation med vår inbyggda e-postautomatisering för att skicka in formulär. Med den här integrerade lösningen kan ni enkelt meddela berörda parter, inklusive att skicka formulärdata, när någon fyller i ett formulär på webbplatsen. Inget behov av komplexa konfigurationer eller andra verktyg - det är klart att användas direkt.


## Tillgängliga Forms-block

AEM Forms Edge Delivery Service erbjuder två typer av formulärblock som tillgodoser olika behov:

* **Grundläggande Forms Block**: Det här är ett mångsidigt alternativ som passar för att skapa enkla formulär med grundläggande funktioner. Det gör att du kan integrera olika indatatyper som textfält, listrutor och alternativknappar, vilket gör att du kan samla in användardata effektivt.

* **Adaptivt Forms-block**: Det här avancerade blocket frigör ytterligare funktioner utöver det grundläggande Forms-blocket så att du kan skapa mer komplexa och interaktiva formulär. Här följer en beskrivning av de viktigaste funktionerna:

   * Regler: Definiera logikbaserade åtgärder i formulären. Du kan använda regler för att villkorligt visa eller dölja formuläravsnitt, fylla i fält i förväg baserat på användarindata och utföra olika valideringar för att säkerställa dataintegriteten.

   * Utbyggbarhet på serversidan: Utöka funktionaliteten i formulären genom att integrera dem med logik på serversidan. På så sätt kan du utföra komplexa beräkningar, interagera med externa system och automatisera specifika uppgifter baserat på användaråtgärder i formuläret.

   * Korspromenad: Effektivisera arbetsflöden och datahantering: Utnyttja kraften i AEM för att:

      * Utforma användarvänliga formulär med AEM redigerare.

      * Generera ett&quot;arkiveringsdokument&quot; för säker och manipuleringssäker arkivering av inskickade data.

      * Underlätta e-signering med Adobe Sign för en smidig och säker signeringsprocess.

      * Automatisera affärsprocesserna genom AEM arbetsflöden, aktivera åtgärder som bygger på inskickade formulär.

      * Integrera enkelt med olika datakällor, vilket möjliggör smidigt dataflöde och datautbyte.

  För att använda Adaptive Forms Block krävs ytterligare en licens.

### Välja rätt Forms-block

Vilken typ av Forms Basic-block du väljer beror på dina specifika behov. Om du behöver en enkel lösning för att samla in grundläggande användarinformation är det grundläggande Forms-blocket perfekt. Men om formulären kräver invecklad logik, datahantering, integration med externa system eller smidiga arbetsflöden med AEM funktioner och **du har den licens som krävs** ger Adaptive Forms Block den kraft och flexibilitet som krävs för att uppnå era mål.


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









