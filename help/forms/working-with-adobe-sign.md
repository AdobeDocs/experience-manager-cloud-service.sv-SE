---
title: Hur kan vi använda Adobe Sign i en adaptiv form?
description: Använd Adobe Sign i ett adaptivt formulär för att låta formulärmottagarna e-signera ett formulär från valfri enhet.
topic-tags: develop
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Intermediate
exl-id: cde9523e-5409-4edd-af0f-2c2575cc22ea
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '3071'
ht-degree: 0%

---

# Använd [!DNL Adobe Sign] i ett adaptivt formulär {#using-adobe-sign-in-an-adaptive-form}

<span class="preview"> Adobe rekommenderar att du använder den moderna och utbyggbara datainhämtningen [Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) för [att skapa nya adaptiva Forms](/help/forms/creating-adaptive-form-core-components.md) eller [att lägga till adaptiva Forms på AEM Sites-sidor](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter. </span>


| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/working-with-adobe-sign.html) |
| AEM as a Cloud Service | Den här artikeln |


[!DNL Adobe Sign] aktiverar e-signaturarbetsflöden för Adaptiv Forms. E-signaturer förbättrar arbetsflödena för att bearbeta dokument inom juridik, försäljning, löneadministration, personaladministration och andra områden.

I ett typiskt [!DNL Adobe Sign]- och Adaptivt Forms-scenario fyller en användare i ett adaptivt formulär som kan användas för en tjänst som kräver signaturer från en eller flera parter. Till exempel kräver en ansökan om inteckning och kreditkort juridiska signaturer från alla låntagare och medsökande. Om du vill aktivera arbetsflöden för elektroniska signaturer för liknande scenarier kan du integrera [!DNL Adobe Sign] med ett anpassat formulär. Ytterligare några exempel är: du kan använda [!DNL Adobe Sign] för att:

* Slut avtal från vilken enhet som helst med fullt automatiserade processer för förslag, offerter och kontrakt.
* Slutför HR-processerna snabbare och ge medarbetarna de digitala upplevelserna.
* Minska kontraktscyklerna och anlita era leverantörer snabbare.
* Skapa digitala arbetsflöden som automatiserar vanliga processer.

[!DNL Adobe Sign]-integrering med [!DNL AEM Forms] har stöd för:

* Arbetsflöden för signering för en och flera användare
* Sekventiella och samtidiga signeringsarbetsflöden
* Signera formulär som anonym eller inloggad användare
* Dynamiska signeringsprocesser (integration med [!DNL AEM Forms]-arbetsflöde)
* Autentisering via kunskapsbas, telefon, sociala profiler och offentlig-ID
* Tilldela roller till alla mottagare av avtal. Adobe Sign för företags- och företagsservicenivåer har möjlighet att expandera [rollerna för avtalsmottagare](#addsignerstoanadaptiveform).

<!-- * In-form and out-of-form signing experiences -->

## Förutsättningar {#prerequisites}

Innan du använder [!DNL Adobe Sign] i ett adaptivt formulär:

* Kontrollera att [!DNL AEM Forms] as a Cloud Service har konfigurerats att använda Adobe Sign. Mer information finns i [Integrera Adobe Sign med [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).
* Håll listan över mottagare klar. Du måste ange minst en e-postadress för varje mottagare.

## Konfigurera [!DNL Adobe Sign] för ett adaptivt formulär {#configure-adobe-sign-for-an-adaptive-form}

Så här konfigurerar du [!DNL Adobe Sign] för ett anpassat formulär:

1. [Aktivera [!DNL Adobe Sign] för ett anpassat formulär](#enableadobsignforanadaptiveform)
1. [Lägg till [!DNL Adobe Sign] fält i ett anpassat formulär](#addadobesignfieldstoanadaptiveform)
1. [Markera [!DNL Adobe Sign] Cloud Service för ett anpassat formulär](#select-adobe-sign-cloud-service-and-signing-order)

1. [Lägg till  [!DNL Adobe Sign] mottagare i ett anpassat formulär](#addsignerstoanadaptiveform)
1. [Välj Skicka åtgärd för ett anpassat formulär](#selectsubmitactionforanadaptiveform)

![Mottagarinformation](assets/signer_details_new.png)

### Aktivera [!DNL Adobe Sign] för ett anpassat formulär  {#enableadobesign}

Du kan aktivera [!DNL Adobe Sign] för ett befintligt adaptivt formulär eller skapa ett [!DNL Adobe Sign]-aktiverat adaptivt formulär. Välj något av följande:

* [Skapa ett  [!DNL Adobe Sign] aktiverat anpassat formulär](#create-an-adaptive-form-for-adobe-sign)
* [Aktivera [!DNL Adobe Sign] för ett befintligt anpassat formulär](#editafsign).

#### Skapa ett adaptivt formulär för Adobe Sign {#create-an-adaptive-form-for-adobe-sign}

Så här skapar du ett signeringsaktiverat adaptivt formulär:

1. Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Välj **[!UICONTROL Create]** och välj **[!UICONTROL Adaptive Form]**. En lista med mallar visas. Välj en mall och välj **[!UICONTROL Next]**.
1. På fliken **[!UICONTROL Basic]**:

   1. Ange **[!UICONTROL Name]** och **[!UICONTROL Title]** för det adaptiva formuläret.

   1. Välj [konfigurationsbehållaren](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) som skapades när [integrerar [!DNL Adobe Sign] med [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

   Konfigurationsbehållaren innehåller de [!DNL Adobe Sign] Cloud Service som är konfigurerade för din miljö. Dessa tjänster kan väljas i redigeraren för adaptiva formulär.

1. Välj något av följande alternativ på fliken **[!UICONTROL Form Model]**:

   * Om du har en anpassad formulärmall och kräver ett dokument för post som är baserat på formulärmallen, markerar du alternativet **[!UICONTROL Associate form template as the Document of Record template]** och väljer en dokumentmall. När du använder alternativet visas endast de fält som är baserade på den associerade formulärmallen i de dokument som skickas för signering. Alla fält i det adaptiva formuläret visas inte.

   * Om du inte har någon anpassad formulärmall väljer du alternativet **[!UICONTROL Generate Document of Record]**. När du använder alternativet visas alla fält i det adaptiva formuläret i det dokument som skickas för signering.

1. Välj **[!UICONTROL Create.]** Ett signeringsaktiverat anpassat formulär skapas. Du kan lägga till dina [!DNL Adobe Sign]-fält i formuläret och skicka det för signering.

#### Aktivera [!DNL Adobe Sign] för ett anpassat formulär {#editafsign}

Så här använder du [!DNL Adobe Sign] i ett befintligt adaptivt formulär:

1. Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Markera det adaptiva formuläret och välj **[!UICONTROL Properties]**.
1. På fliken **[!UICONTROL Basic]** väljer du den [konfigurationsbehållare](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) som skapades när [!DNL Adobe Sign] integrerades med [!DNL AEM Forms].
1. Välj något av följande alternativ på fliken **[!UICONTROL Form Mode]**:

   * Om du har en anpassad formulärmall och kräver ett dokument för post som är baserat på formulärmallen, markerar du alternativet **[!UICONTROL Associate form template as the Document of Record template]** och väljer en dokumentmall. När du använder alternativet visas endast de fält som är baserade på den associerade formulärmallen i de dokument som skickas för signering. Alla fält i det adaptiva formuläret visas inte.

   * Om du inte har någon anpassad formulärmall väljer du alternativet **[!UICONTROL Generate Document of Record]**. När du använder alternativet visas alla fält i det adaptiva formuläret i det dokument som skickas för signering.

1. Välj **[!UICONTROL Save & Close]**. Det adaptiva formuläret har aktiverats för [!DNL Adobe Sign]. Nu kan du lägga till dina [!DNL Adobe Sign]-fält i formuläret och skicka det för signering.

### Lägg till [!DNL Adobe Sign] fält i ett anpassat formulär {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] har olika fält som kan placeras i ett anpassat formulär. Dessa fält accepterar olika typer av data som signaturer, initialer, företag eller titel och hjälper till att samla in extra information vid signering, tillsammans med signaturerna. Du kan använda [!DNL Adobe Sign]-blockkomponenten för att placera [!DNL Adobe Sign]-fält på olika platser i ett adaptivt formulär.

Så här lägger du till fält i ett adaptivt formulär och anpassar olika alternativ för dessa fält:

1. Dra och släpp **[!UICONTROL Adobe Sign Block]**-komponenten från komponentwebbläsaren till det adaptiva formuläret. Blockkomponenten [!DNL Adobe Sign] har alla [!DNL Adobe Sign]-fält som stöds. Som standard läggs ett **[!UICONTROL Signature]**-fält till i det adaptiva formuläret.

   ![Signeringsblock](assets/sign_block_new.png)

   Blocket [!DNL Adobe Sign] visas som standard inte i det publicerade adaptiva formuläret. Den är bara synlig i signeringsdokumenten. Du kan ändra synligheten för [!DNL Adobe Sign] block från egenskaperna för blockkomponenten [!DNL Adobe Sign].

   >[!NOTE]
   >
   >  * Det är inte obligatoriskt att använda [!DNL Adobe Sign]-block för att använda [!DNL Adobe Sign] i ett adaptivt formulär. Om du inte använder [!DNL Adobe Sign]-block och lägger till fält för mottagarna visas standardsignaturfältet längst ned i signeringsdokumenten.
   >  * Använd bara blocket [!DNL Adobe Sign] för de adaptiva Forms som automatiskt genererar arkivdokument. Om du använder en anpassad XDP för att generera ett postdokument eller ett formulärmallsbaserat anpassat formulär stöds inte [!DNL Adobe Sign]-block.


1. Markera komponenten **[!UICONTROL Adobe Sign Block]** och välj ikonen **[!UICONTROL Edit]** ![Redigera](assets/Smock_Edit_18_N.svg) . Här visas alternativ för att lägga till fält och formatera utseende för ett fält.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Markera och lägg till [!DNL Adobe Sign] fält. **B.** Expandera [!DNL Adobe Sign]-blocket till helskärmsläge

1. Välj ikonen **[!UICONTROL Adobe Sign]** Fält ![Adobe Sign](assets/adobesign.png) . Här visas alternativ för att markera och lägga till [!DNL Adobe Sign] fält.

   Expandera listrutan **[!UICONTROL Type]** för att markera ett [!DNL Adobe Sign]-fält och välj ikonen Klar ![Spara](assets/save_icon.svg) för att lägga till det markerade fältet i [!DNL Adobe Sign]-blocket. Listrutan **[!UICONTROL Type]** innehåller fälttyperna Signatur, Mottagarinformation och Datafält. [!DNL Adobe Sign]-integrering med AEM [!DNL Forms] supportfält visas endast i listrutan [!UICONTROL Type]. Mer information om [!DNL Adobe Sign] fält finns i [Adobe Sign-dokumentation](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   Du måste ange ett unikt namn för ett fält. Du kan också markera ett obligatoriskt fält genom att välja önskat alternativ. Förutom alternativet **[!UICONTROL Name]** och **[!UICONTROL Required]** har vissa [!DNL Adobe Sign]-fält fler alternativ. Till exempel mask och flera rader. Ange dessutom ett unikt namn för varje [!DNL Adobe Sign]-fält om fälten finns i samma eller olika [!DNL Adobe Sign]-block.

   Om du väljer **[!UICONTROL Digital Signature]** i listrutan kan du använda digitala signaturer i det adaptiva formuläret:

   * Online med molnsignaturer för att signera med ett [digitalt ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) som finns hos en betrodd tjänsteleverantör.
   * Hämta dokumentet lokalt med Adobe Acrobat eller Reader med ett smartkort, en USB-token eller ett filbaserat digitalt ID.

### Aktivera [!DNL Adobe Sign] för ett anpassat formulär {#enableadobsignforanadaptiveform}

[!DNL Adobe Sign] är inte aktiverat för ett anpassat formulär. Så här aktiverar du den:

1. Markera **[!UICONTROL Form Container]** i innehållsläsaren och välj ikonen **[!UICONTROL Configure]** ![configure](assets/Smock_Wrench_18_N.svg) . Egenskaper öppnas i webbläsaren och egenskaper för behållare för adaptiva formulär visas.
1. Utöka dragspelsfliken **[!UICONTROL Electronic Signature]** i egenskapswebbläsaren och välj alternativet **[!UICONTROL Enable Adobe Sign]**. Det aktiverar [!DNL Adobe Sign] för ett anpassat formulär.

### Markera Cloud Servicen [!DNL Adobe Sign] och signeringsordningen {#select-adobe-sign-cloud-service-and-signing-order}

Du kan konfigurera flera [!DNL Adobe Sign]-tjänster för en instans av AEM [!DNL Forms]. Det är tillrådligt att ha en separat uppsättning tjänster för varje funktion (personal, ekonomi med mera). Det gör det enklare att spåra och rapportera signerade dokument. En bank har till exempel flera avdelningar. Du kan ha en separat konfiguration för varje avdelning för bättre spårning av dokumenten.

Ett dokument kan också ha flera mottagare. En kreditkortsansökan kan t.ex. ha flera sökande. En bank kräver signaturer från alla sökande innan ansökan behandlas. För scenarier med flera mottagare kan du välja att signera dokumentet i sekventiell eller samtidig ordning.

Så här väljer du en Cloud Service och signeringsordning:

![Molntjänst](/help/forms/assets/adobe-sign-cloud-service.png)

1. Markera **[!UICONTROL Form Container]** i innehållsläsaren och välj ikonen **[!UICONTROL Configure]** ![configure](assets/Smock_Wrench_18_N.svg) . Egenskaper öppnas i webbläsaren och egenskaper för behållare för adaptiva formulär visas.
1. Utöka dragspelsfliken **[!UICONTROL Electronic Signature]** i egenskapswebbläsaren och välj alternativet **[!UICONTROL Enable Adobe Sign]**. Det aktiverar [!DNL Adobe Sign] för ett anpassat formulär.
1. Markera en Cloud Service i den redan konfigurerade listan med [!DNL Adobe Sign] Cloud Services.

   Om listan **[!UICONTROL Adobe Sign Cloud Service]** är tom följer du artikeln [Konfigurera [!DNL Adobe Sign] med [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md) för att konfigurera tjänsten.

   I listrutan visas de Cloud Service som finns i mappen `global` i Verktyg > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Listrutan innehåller dessutom en lista över Cloud Service som finns i den mapp som du har valt i fältet **[!UICONTROL Configuration Container]** när du skapar ett anpassat formulär.

1. Välj alternativet för att konfigurera skicka-åtgärden med **[!UICONTROL Submit the form]**. Du kan välja något av följande två alternativ:
   * **Skicka formuläret (och skicka avtalet för signering)**: Det här alternativet skickar formuläret direkt och skickar sedan formuläret för signering till mottagarna.
   * **Skicka formuläret (när alla mottagare har slutfört signeringsceremonin)**: Det här alternativet skickar bara Adaptiv Forms när alla signerare har slutfört signeringsprocessen. Du kan konfigurera intervallet för att kontrollera signeringsstatusen för alla signerare. Mer information finns i [Konfigurera [!DNL Adobe Acrobat Sign] schemaläggare](/help/forms/adobe-sign-integration-adaptive-forms.md#configure-dnl-adobe-acrobat-sign-scheduler-to-sync-the-signing-status).

1. Välj signeringsordning i dialogrutan **[!UICONTROL Recipients can complete]**. Mottagarna kan signera det adaptiva formuläret **[!UICONTROL Sequentially]** - en efter en annan mottagare, eller **[!UICONTROL Simultaneously]** - i valfri ordning.

   I tur och ordning får en mottagare avtalet i taget. När mottagaren har slutfört den tilldelade åtgärden skickas avtalet till nästa mottagare och så vidare.

   Alla mottagare får avtalet och kan agera parallellt i samma ordning.

1. Använd fältet för avtals-ID för att associera en bindef till avtals-ID (agreementId). Det lägger till avtals-ID i avsnittet afBoundData i skicka-data för schemabaserade formulär. Avtals-ID läggs också till i afSubmissionInfo-avsnittet i skickade data för alla Adobe Sign-aktiverade formulär. Du kan använda avtals-ID för att spåra avtalsstatus med hjälp av anpassad kod (kräver anpassad implementering).

   >[!NOTE]
   >
   > Om ett anpassat formulär skapas med en formulärdatamodell (FDM) visas fältet Avtals-ID i dialogrutan.

1. [Lägg till mottagare i ett anpassat formulär](working-with-adobe-sign.md#addsignerstoanadaptiveform) och välj ikonen Klar ![Spara](assets/save_icon.svg) för att spara ändringarna.

### Lägga till mottagare i ett anpassat formulär {#addsignerstoanadaptiveform}

Du kan ha en eller flera mottagare för ett Adobe Sign-avtal. När du lägger till en mottagare kan du även konfigurera autentiseringsinformation för mottagaren och välja om användaren och mottagaren är samma person. Utför följande steg för att lägga till och ange olika detaljer om en mottagare:

1. Markera **[!UICONTROL Form Container]** i innehållsläsaren och välj ikonen **[!UICONTROL Configure]** ![configure](assets/Smock_Wrench_18_N.svg) . Egenskapsläsaren öppnas med egenskaper för adaptiv formulärbehållare.
1. Utöka dragspelsfliken **[!UICONTROL Electronic Signature]** i egenskapswebbläsaren och välj alternativet **[!UICONTROL Enable Adobe Sign]**. Det aktiverar [!DNL Adobe Sign] för ett anpassat formulär.
1. Välj **[!UICONTROL Add Recipient]**. Den lägger till en mottagare i det adaptiva formuläret. Du kan lägga till flera mottagare i ett anpassat formulär. Alla mottagare får ett Adobe Sign-avtal när de skickar in det anpassade formuläret.
   ![telefoninformation](assets/recipient-settings.png)

1. Klicka på ikonen **[!UICONTROL Edit]** ![Redigera](assets/Smock_Edit_18_N.svg) för att ange följande information om mottagaren:

   * **[!UICONTROL Title]:** Ange en titel som unikt identifierar en mottagare.

   * **[!UICONTROL Is the recipient and the person filling the form same?]:** Välj **[!UICONTROL Yes]** om formuläranvändaren och den första mottagaren är samma person. <!-- If the option is set to **No,** then do not use the signature step component in the Adaptive Form. If the form contains a Signature Step component, then the field is automatically set to Yes. -->

   * **[!UICONTROL Recipient Role]:** Välj en mottagares roll. Adobe Sign för företags- och företagsnivåer har möjlighet att expandera [rollerna för avtalsmottagare](https://helpx.adobe.com/sign/using/set-up-signer-approver-roles.html), utöver bara **signeraren**, så att de bättre motsvarar deras arbetsflödesbehov.

   * **[!UICONTROL Recipient Email Address]:** Ange mottagarens e-postadress. Mottagaren får Adobe Sign-avtalet på den angivna e-postadressen. Du kan välja att använda en e-postadress som finns i ett formulärfält, i användarprofilen i Experience Manager för den inloggade användaren eller manuellt ange en e-postadress. Det är ett obligatoriskt steg.

     >[!NOTE]
     >
     >Kontrollera att e-postadressen för den första mottagaren eller den enda mottagaren (om det finns en enda mottagare) inte är identisk med det [!DNL Adobe Sign]-konto som används för att konfigurera AEM Cloud Service.

   * **[!UICONTROL Recipient Authentication Method]:** Ange metoden för att autentisera en mottagare innan du öppnar Adobe Sign-avtalet. Du kan välja mellan telefon, kunskapsbas, social ID-baserad autentisering och [Government ID](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html) för [!DNL Adobe Acrobat Sign]. För [!DNL Adobe Acrobat Sign for Government] kan du välja mellan telefon- och kunskapsbaserad autentisering.

   >[!NOTE]
   >
   >    * Som standard har den sociala identitetsbaserade autentiseringen ett alternativ för autentisering med Facebook, Google och LinkedIn. Du kan kontakta [!DNL Adobe Sign]-supporten för att aktivera andra leverantörer av social autentisering.
   >

   * **[!DNL Adobe Sign]fält att fylla i eller signera:** Välj [!DNL Adobe Sign] fält för mottagaren. Ett anpassat formulär kan ha flera [!DNL Adobe Sign] fält. Du kan välja att aktivera specifika fält för en mottagare. Fältet visar alla tillgängliga [!DNL Adobe Sign] block. När du markerar ett block markeras alla fält i blocket. Du kan använda X-ikonen för att avmarkera ett fält.

   ![mottagarinformation](assets/signer-details.png)

   Bilden ovan har två exempel på [!DNL Adobe Sign]-block: Personlig information och Office-information

   Välj ikonen ![Spara](assets/save_icon.svg) . Mottagaren läggs till.

### Välj Skicka åtgärd för ett anpassat formulär {#selectsubmitactionforanadaptiveform}

När du har lagt till [!DNL Adobe Sign]-fält i ett adaptivt formulär, aktiverat [!DNL Adobe Sign] från formulärbehållaren, markerat [!DNL Adobe Sign]-Cloud Service och lagt till Adobe Sign-avtalsmottagare, väljer du en lämplig överföringsåtgärd för det adaptiva formuläret. Mer information om adaptiva Forms-överföringsåtgärder finns i [Konfigurera Skicka-åtgärden](configuring-submit-actions.md).

Att signera och skicka ett formulär är oberoende av varandra. Överföring av anpassade formulär sker så snart ett Adobe Sign-avtal har skapats efter att en användare har skickat in ett formulär. [!DNL AEM Forms]-as a Cloud Service väntar inte på att mottagarna ska signera eller slutföra andra åtgärder för att skicka ett adaptivt formulär. Ett formulär skickas så snart en användare klickar på Skicka-knappen eller ett steg Sammanfattning visar sammanfattningen av formuläret.

Ett anpassat formulär som har aktiverats av [!DNL Adobe Sign] bäddar även in Adobe Sign-avtals-ID:t för att skicka data. Du kan använda avtals-ID för att spåra avtalsstatus med hjälp av anpassad kod (kräver anpassad implementering).

Adobe Sign avtals-ID (agreementId) ingår i överföringsdata i det adaptiva formuläret. Som standard finns avtals-ID i noden `afSubmissionInfo` för skickade data.

```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <afData>
      <afUnboundData>
         <data>
            <textbox1613455050902>ff</textbox1613455050902>
         </data>
      </afUnboundData>
      <afBoundData>
         <data xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/" />
      </afBoundData>
      <afSubmissionInfo>
         <lastFocusItem>guide[0].guide1[0].guideRootPanel[0].textbox1613455050902[0]</lastFocusItem>
         <stateOverrides />
         <signers>
            <signer0>
               <email />
            </signer0>
         </signers>
         <afPath>/content/dam/formsanddocuments/testsign</afPath>
         <afSubmissionTime>20210311031009</afSubmissionTime>
         <agreementId>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</agreementId>
      </afSubmissionInfo>
   </afData>
```

Du kan även associera en bindef till avtals-ID (agreementId). Det lägger till avtals-ID i avsnittet afBoundData för skickade data. I följande skickade data är avtals-ID till exempel bundet till noden `<userName>`:

```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <afData>
         <afUnboundData>
            <data />
         </afUnboundData>
         <afBoundData>
            <config xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
               <userName>3AAABLblqZhC2MWu7GFauKh45j_t2ih8mAtmbdIcNSl1HgQubhMJfDaDfylyN7NQiYRam_44ISKm45enIOafHqWZrdaxShf9r</userName>
               <dateOfBirth>0001-01-01</dateOfBirth>
            </config>
         </afBoundData>
         <afSubmissionInfo>
            <lastFocusItem>guide[0].guide1[0].guideRootPanel[0].projectDetails[0]</lastFocusItem>
            <stateOverrides />
            <signers>
               <signer0>
                  <email />
               </signer0>
            </signers>
            <afPath>/content/dam/formsanddocuments/testathon2021-1/gaurav/xsd-based</afPath>
            <afSubmissionTime>20210311095211</afSubmissionTime>
            <agreementId>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</agreementId>
         </afSubmissionInfo>
      </afData>
```

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the Adaptive Form is stored temporarily on Forms Portal. Adobe recommends using [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

Din formulärsigneringsupplevelse är klar. Du kan förhandsgranska formuläret för att verifiera signeringsprocessen. På det publicerade formuläret visas [!DNL Adobe Sign] blockeringsfält när en mottagare tar emot formuläret för signering via ett e-postmeddelande. När alternativet **[!UICONTROL When Is the recipient and the person filling the form same?]** är markerat som ja och villkoret är uppfyllt, omdirigeras användaren till Adobe Sign-avtalet efter inskickningar och användaren kan signera dokumentet omedelbart i stället för att vänta på att avtalet ska visas i e-postmeddelandet.

## Konfigurera molnsignaturer för ett adaptivt formulär {#configure-cloud-signatures-for-an-adaptive-form}

Molnbaserade digitala signaturer eller fjärrsignaturer är en ny generation digitala signaturer som fungerar på datorer, mobila enheter och webben - och som uppfyller de högsta efterlevnads- och säkerhetsnivåerna för mottagarautentisering. Du kan signera ett adaptivt formulär med molnbaserade digitala signaturer.

När du har [redigerat adaptiva formuläregenskaper för Adobe Sign](working-with-adobe-sign.md#enableadobesign) utför du följande steg för att lägga till molnsignaturfält i ett adaptivt formulär:

1. Dra och släpp **[!UICONTROL Adobe Sign Block]**-komponenten från komponentwebbläsaren till det adaptiva formuläret. Komponenten [!UICONTROL Adobe Sign Block] har alla [!DNL Adobe Sign]-fält som stöds. Som standard läggs ett **[!UICONTROL Signature]**-fält till i det adaptiva formuläret.

   ![Signeringsblock](assets/sign-block-new.png)

1. Markera komponenten **[!UICONTROL Adobe Sign Block]** och välj ikonen **[!UICONTROL Edit]** ![Redigera](assets/Smock_Edit_18_N.svg) . Här visas alternativ för att lägga till fält och formatera utseende för ett fält.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Markera och lägg till [!DNL Adobe Sign] fält. **B.** Expandera [!DNL Adobe Sign]-blocket till helskärmsläge

1. Välj ikonen **[!UICONTROL Adobe Sign Field]** ![Adobe Sign](assets/adobesign.png) . Här visas alternativ för att markera och lägga till [!DNL Adobe Sign] fält.

   Expandera det nedrullningsbara fältet **[!UICONTROL Type]** för att markera **[!UICONTROL Digital Signature]** och markera ikonen **[!UICONTROL Done]** för att lägga till det markerade fältet i blocket [!DNL Adobe Sign].

   ![Digitala signaturer](assets/digital_signatures_new.png)

   Du måste ange ett unikt namn för ett fält.

   Använd digitala signaturer i det adaptiva formuläret med:

   * Molnsignaturer: Signera med ett [digitalt ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) som finns hos en betrodd tjänsteleverantör.
   * Adobe Acrobat eller Reader: Hämta och öppna dokumentet med Adobe Acrobat eller Reader för signering med ett smartkort, en USB-token eller ett filbaserat digitalt ID.

     >[!NOTE]
     >
     > Digital signatur gäller även för [!DNL Adobe Acrobat Sign for Government], men du kan inte använda den med molnsignaturer.

   När du har lagt till fältet för molnsignatur i det adaptiva formuläret utför du följande steg för att slutföra konfigurationsprocessen:

   * [Aktivera Adobe Sign för ett adaptivt formulär](#enableadobsignforanadaptiveform)
   * [Välj Adobe Sign Cloud Service för ett adaptivt formulär](#selectadobesigncloudserviceforanadaptiveform)
   * [Lägga till mottagare i ett anpassat formulär](#addsignerstoanadaptiveform)
   * [Välj Skicka åtgärd för ett anpassat formulär](#selectsubmitactionforanadaptiveform)

### Konfigurera tacksidan eller sammanfattningssteget {#configure-the-thank-you-page-or-summary-step-component}

Komponenten **[!UICONTROL Summary Step]** skickar automatiskt formuläret, fyller i informationen på den anpassade sammanfattningssidan och visar sammanfattningen av det skickade formuläret. Komponenten Sammanfattningssteg får full bredd som är tillgänglig för formuläret. Vi rekommenderar att du inte har någon annan komponent i avsnittet som innehåller komponenten Sammanfattningssteg.

## Frågor och svar {#frequently-asked-questions}

**Q:** Du kan bädda in ett adaptivt formulär i ett annat adaptivt formulär. Kan det inbäddade adaptiva formuläret [!DNL Adobe Sign] aktiveras?
**Ans:** Nej, Experience Manager Forms stöder inte användning av ett adaptivt formulär som bäddar in ett [!DNL Adobe Sign] aktiverat adaptivt formulär för signering

**Q:** När jag skapar ett adaptivt formulär med den avancerade mallen och öppnar det för redigering visas felmeddelandet&quot;Elektronisk signatur eller mottagare är inte korrekt konfigurerade&quot;. visas. Hur löser jag felmeddelandet?
**Ans:** Adaptivt formulär som skapats med den avancerade mallen är konfigurerat att använda [!DNL Adobe Sign]. Lös felet genom att skapa och välja en [!DNL Adobe Sign]-molnkonfiguration och konfigurera en [!DNL Adobe Sign]-mottagare för det adaptiva formuläret.

**Q:** Kan jag använda [!DNL Adobe Sign]-texttaggar i en statisk textkomponent i ett adaptivt formulär?
**Ans:** Ja, du kan använda texttaggar i en textkomponent för att lägga till [!DNL Adobe Sign] fält i ett anpassat formulär som har aktiverats för dokumentformat (endast alternativet Automatiskt genererat postdokument). Mer information om proceduren och reglerna för att skapa en texttagg finns i [Adobe Sign Documentation](https://helpx.adobe.com/sign/using/text-tag.html). Dessutom har Adaptive Forms begränsat stöd för texttaggar. Du kan använda texttaggarna för att skapa endast de fält som stöds av [Adobe Sign Block](working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form).

## Felsökning {#troubleshoot}

### [!DNL Adobe Sign] avtalsfel {#adobe-sign-agreement-failures}

**Utgåva**
När [!DNL Adobe Sign] -tjänsten har konfigurerats för ett adaptivt formulär kan tjänsten inte skapa ett [!DNL Adobe Sign] -avtal för det underliggande adaptiva formuläret.

**Upplösning**

* Kontrollera [konfigurationen av Adobe Sign Cloud Service](adobe-sign-integration-adaptive-forms.md) som används i det adaptiva formuläret.
* Kontrollera att API-programmet på [!DNL Adobe Sign]-servern som används för att konfigurera [!DNL Adobe Sign]-Cloud Servicen har nödvändiga behörigheter.
* Om du använder flera [!DNL Adobe Sign]-Cloud Service pekar du **[!UICONTROL oAuth URL]** för alla tjänster på samma **[!UICONTROL Adobe Sign Shard]**.

* Använd separata e-postadresser för att konfigurera [!DNL Adobe Sign]-kontot och för den första eller enda mottagaren. E-postadressen till den första mottagaren eller den enda mottagaren (om det finns en enda mottagare) kan inte vara identisk med det [!DNL Adobe Sign]-konto som används för att konfigurera AEM Cloud Service.

>[!MORELIKETHIS]
>
>* [Integrera [!DNL Adobe Sign] med [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md)
>* [Bästa tillvägagångssätt för att använda [!DNL Adobe Sign] med Adaptiv Forms](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)


## Se även {#see-also}

{{see-also}}