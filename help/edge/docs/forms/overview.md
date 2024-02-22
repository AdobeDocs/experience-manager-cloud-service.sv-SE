---
title: AEM Forms Edge Delivery Service - översikt
description: AEM Forms Edge Delivery Service har tagits fram för bästa prestanda och ger er möjlighet att förutse framtiden för smidig datainsamling och användarengagemang.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: bd8c4fbfd7f740baa6abd7a91fb8d1dcdaff6c28
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# AEM Forms Edge Delivery Service {#aem-forms-edge-delivery-service-overview}

AEM Forms Edge Delivery Service är en sammansättningsbar tjänst från Adobe som gör att du kan skapa och leverera effektiva webbformulär. Du kan använda tjänsten för att:

* **Skapa visuellt slagkraftiga formulär**: Gör intryck på den bleka, kakformsdesignen och fånga upp användarna med dynamiska, moderna former som speglar er varumärkesidentitet. Utnyttja färdiga komponenter eller skapa egna komponenter för att förverkliga din vision snabbt och enkelt.

* **Skapa formulär med perfekt fyr**: Bygg formulär som läses in och återges snabbt, även på långsamma internetanslutningar. Snabbare inläsningstider och optimerad användarupplevelse bidrar till snabbare ifyllnad av formulär och förbättrad konverteringsgrad.

* **Förenkla framtagning och inlämning**: Skapa formulär med välbekanta verktyg som Microsoft Excel eller Google Sheets i stället för med de traditionella redigeringsmiljöerna. Skicka blanketter direkt till Microsoft Excel- eller Google-ark och använd deras ekosystem för att enkelt bearbeta inlämnade data.


Den här sammansatta tjänsten är fristående från innehållskällan och ger flexibilitet när det gäller att skapa innehåll genom att användarna kan använda de redigeringsverktyg de föredrar.

![Utvecklingsverktyg för Edge Delivery-formulär](/help/edge/assets/edge-delivery-forms-authoring-tools.png)

De som skapar innehåll kan utnyttja de verktyg de känner sig hemma med, som Microsoft Excel eller Google Sheets (dokumentbaserad redigering), JSON-redigerare eller AEM Forms Adaptive Forms-redigerare för WYSIWYG-redigering (AEM Forms-projekt), för att utforma och skapa sina formulär.

>[!NOTE]
>
>
> WYSIWYG-redigeringsfunktionen och Cross Walk-områden är tillgängliga i tidiga adopter-program. Du kan skriva till aem-forms-early-adopter-program@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen.

## Börja med grunderna

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
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Lägga till valideringar i formulärfält" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Använd fältvalideringar</b>
        </a>
        <p>Minska antalet fel och frustration genom att kontrollera indata i blanketterna för korrekt formatering.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/form-fragments.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Använd formulärfragment i ett EDS-formulär" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Skapa formulärfragment</b>
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
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Använda format eller teman i ett formulär" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Anpassa ett tema</b>
        </a>
        <p>Skapa en enhetlig varumärkesbild genom att använda samma tema i alla formulär.</p>
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
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Skicka formulär" alt="Använd formulärfragment i ett EDS-formulär" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Skicka formulär till kalkylblad</b>
        </a>
        <p>Skicka formulär direkt till Microsoft Excel- eller Google-ark.</p>
    </div>
</div>


</br>









