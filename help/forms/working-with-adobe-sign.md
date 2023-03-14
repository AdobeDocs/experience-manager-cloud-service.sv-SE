---
title: Så här använder du [!DNL Adobe Sign] i adaptiv form?
description: Du kan aktivera e-signatur ([!DNL Adobe Sign]) för ett adaptivt formulär för att automatisera signeringsarbetsflöden, förenkla processerna med en eller flera signaturer samt för att elektroniskt signera formulär från mobila enheter.
topic-tags: develop
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: cde9523e-5409-4edd-af0f-2c2575cc22ea
source-git-commit: 3d713304512065819ed16bbc9604f2cf9d1cf43f
workflow-type: tm+mt
source-wordcount: '2903'
ht-degree: 0%

---


# Använda [!DNL Adobe Sign] i adaptiv form {#using-adobe-sign-in-an-adaptive-form}

[!DNL Adobe Sign] möjliggör e-signaturarbetsflöden för Adaptive Forms. E-signaturer förbättrar arbetsflödena för att bearbeta dokument inom juridik, försäljning, löneadministration, personaladministration och andra områden.

I en typisk [!DNL Adobe Sign] och Adaptiv Forms-scenario fyller en användare i ett adaptivt formulär som kan användas för en tjänst som kräver signaturer från en eller flera parter. Till exempel kräver en ansökan om inteckning och kreditkort juridiska signaturer från alla låntagare och medsökande. Om du vill aktivera arbetsflöden för elektroniska signaturer för liknande scenarier kan du integrera [!DNL Adobe Sign] med adaptiv form. Några exempel till är: [!DNL Adobe Sign] till:

* Slut avtal från vilken enhet som helst med fullt automatiserade processer för förslag, offerter och kontrakt.
* Slutför HR-processerna snabbare och ge medarbetarna de digitala upplevelserna.
* Minska kontraktscyklerna och anlita era leverantörer snabbare.
* Skapa digitala arbetsflöden som automatiserar vanliga processer.

[!DNL Adobe Sign] integrering med [!DNL AEM Forms] stöder:

* Arbetsflöden för signering för en och flera användare
* Sekventiella och samtidiga signeringsarbetsflöden
* Signera formulär som anonym eller inloggad användare
* Dynamiska signeringsprocesser (integration med [!DNL AEM Forms] Arbetsflöde)
* Autentisering via kunskapsbas, telefon, sociala profiler och offentlig-ID
* Tilldela roller till alla mottagare av avtal. Adobe Sign för företag och företag har möjlighet att utöka [roller för mottagare av avtal](#addsignerstoanadaptiveform).

<!-- * In-form and out-of-form signing experiences -->

## Förutsättningar {#prerequisites}

Innan du använder [!DNL Adobe Sign] i adaptiv form:

* Se till att [!DNL AEM Forms] as a Cloud Service är konfigurerad att använda Adobe Sign. Mer information finns i [Integrera Adobe Sign med [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).
* Håll listan över mottagare klar. Du måste ange minst en e-postadress för varje mottagare.

## Konfigurera [!DNL Adobe Sign] för ett adaptivt formulär {#configure-adobe-sign-for-an-adaptive-form}

Konfigurera [!DNL Adobe Sign] för en adaptiv form:

1. [Aktivera [!DNL Adobe Sign] för ett adaptivt formulär](#enableadobsignforanadaptiveform)
1. [Lägg till [!DNL Adobe Sign] fält till ett adaptivt formulär](#addadobesignfieldstoanadaptiveform)
1. [Välj [!DNL Adobe Sign] Cloud Service för ett adaptivt formulär](#select-adobe-sign-cloud-service-and-signing-order)

1. [Lägg till [!DNL Adobe Sign] mottagare av ett adaptivt formulär](#addsignerstoanadaptiveform)
1. [Välj Skicka åtgärd för ett anpassat formulär](#selectsubmitactionforanadaptiveform)

![Mottagarinformation](assets/signer_details_new.png)

### Aktivera [!DNL Adobe Sign] för ett adaptivt formulär  {#enableadobesign}

Du kan aktivera [!DNL Adobe Sign] för ett befintligt adaptivt formulär eller skapa ett [!DNL Adobe Sign] aktiverad adaptiv form. Välj något av följande:

* [Skapa en [!DNL Adobe Sign] aktiverat adaptivt format](#create-an-adaptive-form-for-adobe-sign)
* [Aktivera [!DNL Adobe Sign] för ett befintligt adaptivt formulär](#editafsign).

#### Skapa ett adaptivt formulär för Adobe Sign {#create-an-adaptive-form-for-adobe-sign}

Så här skapar du ett signeringsaktiverat adaptivt formulär:

1. Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Tryck **[!UICONTROL Create]** och markera **[!UICONTROL Adaptive Form]**. En lista med mallar visas. Välj en mall och tryck på **[!UICONTROL Next]**.
1. I **[!UICONTROL Basic]** tab:

   1. Ange **[!UICONTROL Name]** och **[!UICONTROL Title]** för den adaptiva formen.

   1. Välj [konfigurationsbehållare](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) skapad [integrering [!DNL Adobe Sign] med [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).
   Konfigurationsbehållaren innehåller [!DNL Adobe Sign] Cloud Services som är konfigurerade för din miljö. Dessa tjänster kan väljas i redigeraren för adaptiva formulär.

1. I **[!UICONTROL Form Model]** väljer du något av följande alternativ:

   * Om du har en anpassad formulärmall och kräver ett postdokument som är baserat på formulärmallen väljer du **[!UICONTROL Associate form template as the Document of Record template]** och välj en dokumentmall. När du använder alternativet visas endast de fält som är baserade på den associerade formulärmallen i de dokument som skickas för signering. Alla fält i det adaptiva formuläret visas inte.

   * Om du inte har någon anpassad formulärmall väljer du **[!UICONTROL Generate Document of Record]** alternativ. När du använder alternativet visas alla fält i det adaptiva formuläret i det dokument som skickas för signering.

1. Tryck **[!UICONTROL Create.]** Ett signeringsaktiverat anpassat formulär skapas. Du kan lägga till [!DNL Adobe Sign] fält till formuläret och skicka det för signering.

#### Aktivera [!DNL Adobe Sign] för ett adaptivt formulär {#editafsign}

Används [!DNL Adobe Sign] i en befintlig adaptiv form:

1. Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Markera det adaptiva formuläret och tryck på **[!UICONTROL Properties]**.
1. I **[!UICONTROL Basic]** väljer du [konfigurationsbehållare](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) skapad vid integrering [!DNL Adobe Sign] med [!DNL AEM Forms].
1. I **[!UICONTROL Form Mode]** väljer du något av följande alternativ:

   * Om du har en anpassad formulärmall och kräver ett postdokument som är baserat på formulärmallen väljer du **[!UICONTROL Associate form template as the Document of Record template]** och välj en dokumentmall. När du använder alternativet visas endast de fält som är baserade på den associerade formulärmallen i de dokument som skickas för signering. Alla fält i det adaptiva formuläret visas inte.

   * Om du inte har någon anpassad formulärmall väljer du **[!UICONTROL Generate Document of Record]** alternativ. När du använder alternativet visas alla fält i det adaptiva formuläret i det dokument som skickas för signering.

1. Tryck på **[!UICONTROL Save & Close]**. Det adaptiva formuläret är aktiverat för [!DNL Adobe Sign]. Nu kan du lägga till [!DNL Adobe Sign] fält till formuläret och skicka det för signering.

### Lägg till [!DNL Adobe Sign] fält till ett adaptivt formulär {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] har olika fält som kan placeras i ett anpassat formulär. Dessa fält accepterar olika typer av data som signaturer, initialer, företag eller titel och hjälper till att samla in extra information vid signering, tillsammans med signaturerna. Du kan använda [!DNL Adobe Sign] Blockkomponent att montera [!DNL Adobe Sign] fält på olika platser i ett adaptivt formulär.

Så här lägger du till fält i ett adaptivt formulär och anpassar olika alternativ för dessa fält:

1. Dra och släppa **[!UICONTROL Adobe Sign Block]** från komponentens webbläsare till det adaptiva formuläret. The [!DNL Adobe Sign] Block-komponenten har alla funktioner som stöds [!DNL Adobe Sign] fält. Som standard läggs en **[!UICONTROL Signature]** till det adaptiva formuläret.

   ![Signeringsblock](assets/sign_block_new.png)

   Som standard är [!DNL Adobe Sign] Blocket visas inte i det publicerade adaptiva formuläret. Den visas bara i signeringsdokumenten. Du kan ändra synligheten för [!DNL Adobe Sign] Blockera från egenskaperna för [!DNL Adobe Sign] Blockkomponent.

   >[!NOTE]
   >
   >  * Använda [!DNL Adobe Sign] block är inte obligatoriskt att använda [!DNL Adobe Sign] i adaptiv form. Om du inte använder [!DNL Adobe Sign] blockera och lägga till fält för mottagarna, visas standardsignaturfältet längst ned i signeringsdokumenten.
   >  * Använd [!DNL Adobe Sign] blockera endast för de adaptiva Forms som automatiskt genererar arkivdokument. Om du använder en anpassad XDP för att generera ett postdokument eller ett formulärmallsbaserat anpassat formulär, [!DNL Adobe Sign] block stöds inte.



1. Välj **[!UICONTROL Adobe Sign Block]** och tryck på **[!UICONTROL Edit]** ![Redigera](assets/Smock_Edit_18_N.svg) ikon. Här visas alternativ för att lägga till fält och formatera utseende för ett fält.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **S.** Markera och lägg till [!DNL Adobe Sign] fält. **B.** Expandera [!DNL Adobe Sign] blockera till helskärmsläge

1. Tryck på **[!UICONTROL Adobe Sign]** Fält ![Adobe Sign](assets/adobesign.png) ikon. Här visas alternativ för att markera och lägga till [!DNL Adobe Sign] fält.

   Expandera **[!UICONTROL Type]** nedrullningsbart fält för att välja ett [!DNL Adobe Sign] och tryck på Klart ![Spara](assets/save_icon.svg) ikon för att lägga till det markerade fältet i [!DNL Adobe Sign] -block. The **[!UICONTROL Type]** nedrullningsbara fält innehåller signatur, mottagarinformation och datafälttyper. [!DNL Adobe Sign] integrering med AEM [!DNL Forms] supportfält som anges i [!UICONTROL Type] endast listrutan. Detaljerad information om [!DNL Adobe Sign] fält, se [Adobe Sign-dokumentation](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   Du måste ange ett unikt namn för ett fält. Du kan också markera ett obligatoriskt fält genom att välja önskat alternativ. Förutom **[!UICONTROL Name]** och **[!UICONTROL Required]** alternativ, vissa [!DNL Adobe Sign] har fler alternativ. Till exempel mask och flera rader. Ange dessutom ett unikt namn för varje [!DNL Adobe Sign] fält om fälten finns i samma eller olika [!DNL Adobe Sign] -block.

   Om du väljer **[!UICONTROL Digital Signature]** från listrutan kan du använda digitala signaturer i det adaptiva formuläret:

   * Online med molnsignaturer för att signera med en [digitalt ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) som hanteras av en betrodd tjänsteleverantör.
   * Hämta dokumentet lokalt med Adobe Acrobat eller Reader med ett smartkort, en USB-token eller ett filbaserat digitalt ID.

### Aktivera [!DNL Adobe Sign] för ett adaptivt formulär {#enableadobsignforanadaptiveform}

Ut ur lådan, [!DNL Adobe Sign] är inte aktiverat för ett adaptivt formulär. Så här aktiverar du den:

1. Tryck på **[!UICONTROL Form Container]** och trycker på **[!UICONTROL Configure]** ![konfigurera](assets/Smock_Wrench_18_N.svg) ikon. Egenskaper öppnas i webbläsaren och egenskaper för behållare för adaptiva formulär visas.
1. Utöka **[!UICONTROL Electronic Signature]** och välj **[!UICONTROL Enable Adobe Sign]** alternativ. Det gör att [!DNL Adobe Sign] för en adaptiv form.

### Välj [!DNL Adobe Sign] Cloud Service och signeringsordning {#select-adobe-sign-cloud-service-and-signing-order}

Du kan konfigurera flera [!DNL Adobe Sign] tjänster för en instans av AEM [!DNL Forms]. Det är tillrådligt att ha en separat uppsättning tjänster för varje funktion (personal, ekonomi med mera). Det gör det enklare att spåra och rapportera signerade dokument. En bank har till exempel flera avdelningar. Du kan ha en separat konfiguration för varje avdelning för bättre spårning av dokumenten.

Ett dokument kan också ha flera mottagare. En kreditkortsansökan kan till exempel ha flera sökande. En bank kräver signaturer från alla sökande innan ansökan behandlas. För scenarier med flera mottagare kan du välja att signera dokumentet i sekventiell eller samtidig ordning.

Så här väljer du en Cloud Service och signeringsordning:

![Molntjänst](assets/cloud-service.png)

1. Tryck på **[!UICONTROL Form Container]** och trycker på **[!UICONTROL Configure]** ![konfigurera](assets/Smock_Wrench_18_N.svg) ikon. Egenskaper öppnas i webbläsaren och egenskaper för behållare för adaptiva formulär visas.
1. Utöka **[!UICONTROL Electronic Signature]** och välj **[!UICONTROL Enable Adobe Sign]** alternativ. Det gör att [!DNL Adobe Sign] för en adaptiv form.
1. Markera en Cloud Service i den redan konfigurerade listan med [!DNL Adobe Sign] Cloud Services.

   Om **[!UICONTROL Adobe Sign Cloud Service]** listan är tom, följ [Konfigurera [!DNL Adobe Sign] med [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md) artikel för att konfigurera tjänsten.

   I listrutan visas de Cloud Services som finns i `global` mapp i Verktyg > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. I listrutan visas dessutom de Cloud Services som finns i den mapp som du har valt i **[!UICONTROL Configuration Container]** när du skapar ett adaptivt formulär.

1. Välj signeringsordning på menyn **[!UICONTROL Recipients can complete]** -dialogrutan. Mottagarna kan signera ett adaptivt formulär **[!UICONTROL Sequentially]** - en efter en annan mottagare, eller **[!UICONTROL Simultaneously]** - i valfri ordning.

   I tur och ordning får en mottagare Adobe Sign-avtalet i taget. När mottagaren har slutfört den tilldelade åtgärden skickas avtalet till nästa mottagare och så vidare.

   I samtidiga beställningar får alla mottagare Adobe Sign-avtalet och kan vidta åtgärder parallellt med varandra.

1. Använd fältet för avtals-ID för att associera en bindef till avtals-ID (agreementId). Det lägger till avtals-ID i avsnittet afBoundData i skicka-data för schemabaserade formulär. Avtals-ID läggs också till i afSubmissionInfo-avsnittet i skickade data för alla Adobe Sign-aktiverade formulär. Du kan använda avtals-ID för att spåra avtalsstatus med hjälp av anpassad kod (kräver anpassad implementering).

1. [Lägga till mottagare i ett anpassat formulär](working-with-adobe-sign.md#addsignerstoanadaptiveform) och tryck på Klart ![Spara](assets/save_icon.svg) om du vill spara ändringarna.

### Lägga till mottagare i ett anpassat formulär {#addsignerstoanadaptiveform}

Du kan ha en eller flera mottagare för ett Adobe Sign-avtal. När du lägger till en mottagare kan du även konfigurera autentiseringsinformation för mottagaren och välja om användaren och mottagaren är samma person. Utför följande steg för att lägga till och ange olika detaljer om en mottagare:

1. Tryck på **[!UICONTROL Form Container]** och trycker på **[!UICONTROL Configure]** ![konfigurera](assets/Smock_Wrench_18_N.svg) ikon. Egenskapsläsaren öppnas med egenskaper för adaptiv formulärbehållare.
1. Utöka **[!UICONTROL Electronic Signature]** och välj **[!UICONTROL Enable Adobe Sign]** alternativ. Det gör att [!DNL Adobe Sign] för en adaptiv form.
1. Tryck på **[!UICONTROL Add Recipient]**. Den lägger till en mottagare i det adaptiva formuläret. Du kan lägga till flera mottagare i ett anpassat formulär. Alla mottagare får ett Adobe Sign-avtal när de skickar in det anpassade formuläret.
   ![telefoninformation](assets/recipient-settings.png)

1. Klicka på **[!UICONTROL Edit]** ![Redigera](assets/Smock_Edit_18_N.svg) om du vill ange följande information om mottagaren:

   * **[!UICONTROL Title]:** Ange en rubrik som unikt identifierar en mottagare.

   * **[!UICONTROL Is the recipient and the person filling the form same?]:** Välj **[!UICONTROL Yes]**, om formuläranvändaren och den första mottagaren är samma person. <!-- If the option is set to **No,** then do not use the signature step component in the Adaptive Form. If the form contains a Signature Step component, then the field is automatically set to Yes. -->

   * **[!UICONTROL Recipient Role]:** Välj en mottagares roll. Adobe Sign för företag och företag har möjlighet att utöka [roller för mottagare av avtal](https://helpx.adobe.com/sign/using/set-up-signer-approver-roles.html)förutom **Signerare**, så att de bättre motsvarar arbetsflödets krav.

   * **[!UICONTROL Recipient Email Address]:** Ange mottagarens e-postadress. Mottagaren får Adobe Sign-avtalet på den angivna e-postadressen. Du kan välja att använda en e-postadress som finns i ett formulärfält, i användarprofilen i Experience Manager för den inloggade användaren eller manuellt ange en e-postadress. Det är ett obligatoriskt steg.

      >[!NOTE]
      >
      >Kontrollera att e-postadressen för den första mottagaren eller den enda mottagaren (om det finns en enda mottagare) inte är identisk med [!DNL Adobe Sign] konto som används för att konfigurera AEM Cloud-tjänster.

   * **[!UICONTROL Recipient Authentication Method]:** Ange metoden för att autentisera en mottagare innan du öppnar Adobe Sign-avtalet. Du kan välja mellan telefon, kunskapsbas, social ID-baserad autentisering och [Offentlig sektor](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html).
   >[!NOTE]
   >
   >    * Som standard har den sociala identitetsbaserade autentiseringen ett alternativ för att autentisera med Facebook, Google och LinkedIn. Du kan kontakta [!DNL Adobe Sign] stöd för att aktivera andra leverantörer av social autentisering.


   * **[!DNL Adobe Sign]fält som ska fyllas i eller signeras:** Välj [!DNL Adobe Sign] fält för mottagaren. Ett anpassat formulär kan ha flera [!DNL Adobe Sign] fält. Du kan välja att aktivera specifika fält för en mottagare. Fältet visar alla tillgängliga [!DNL Adobe Sign] Blockar. När du markerar ett block markeras alla fält i blocket. Du kan använda X-ikonen för att avmarkera ett fält.

   ![mottagarinformation](assets/signer-details.png)

   Bilden ovan har två exempel [!DNL Adobe Sign] Block: Personlig information och kontorsinformation

   Tryck på ![Spara](assets/save_icon.svg) ikon. Mottagaren läggs till.

### Välj Skicka åtgärd för ett anpassat formulär {#selectsubmitactionforanadaptiveform}

Efter dig lägger du till [!DNL Adobe Sign] fält till ett adaptivt formulär, aktivera [!DNL Adobe Sign] från formulärbehållare, välj [!DNL Adobe Sign] Cloud Service och lägg till mottagare av Adobe Sign-avtal genom att välja en lämplig Skicka-åtgärd för det anpassade formuläret. Detaljerad information om adaptiva Forms Submit Actions finns i [Konfigurera åtgärden Skicka](configuring-submit-actions.md).

Att signera och skicka ett formulär är oberoende av varandra. Överföring av anpassade formulär sker så snart ett Adobe Sign-avtal har skapats efter att en användare har skickat in ett formulär. [!DNL AEM Forms] as a Cloud Service väntar inte på att mottagarna ska signera eller slutföra andra åtgärder för att skicka ett adaptivt formulär. Ett formulär skickas så snart en användare klickar på Skicka-knappen eller ett steg Sammanfattning visar sammanfattningen av formuläret.

Dessutom kan [!DNL Adobe Sign] aktiverat anpassat formulär bäddar in Adobe Sign avtals-ID:t så att data skickas. Du kan använda avtals-ID för att spåra avtalsstatus med hjälp av anpassad kod (kräver anpassad implementering).

Adobe Sign avtals-ID (agreementId) ingår i överföringsdata i det adaptiva formuläret. Som standard finns avtals-ID i `afSubmissionInfo` nod för skickade data.

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

Du kan även associera en bindef till avtals-ID (agreementId). Det lägger till avtals-ID i avsnittet afBoundData för skickade data. I följande skickade data binds till exempel avtals-ID till `<userName>` nod:

```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <afData>
         <afUnboundData>
            <data />
         </afUnboundData>
         <afBoundData>
            <config xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
               <agreementID>3AAABLblqZhC2MWu7GFauKh45j_t2ih8mAtmbdIcNSl1HgQubhMJfDaDfylyN7NQiYRam_44ISKm45enIOafHqWZrdaxShf9r</agreementID>
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
>Data of the Adaptive Form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

Din formulärsigneringsupplevelse är klar. Du kan förhandsgranska formuläret för att verifiera signeringsprocessen. På det publicerade formuläret [!DNL Adobe Sign] Blockfält visas när en mottagare tar emot formuläret för signering via ett e-postmeddelande. När **[!UICONTROL When Is the recipient and the person filling the form same?]** om alternativet är markerat som ja och villkoret är uppfyllt, omdirigeras användaren till Adobe Sign-avtalet efter det att dokumentet har skickats och användaren kan signera dokumentet omedelbart i stället för att vänta på att avtalet ska visas i e-postmeddelandet.

## Konfigurera molnsignaturer för ett adaptivt formulär {#configure-cloud-signatures-for-an-adaptive-form}

Molnbaserade digitala signaturer eller fjärrsignaturer är en ny generation digitala signaturer som fungerar på datorer, mobila enheter och webben - och som uppfyller de högsta efterlevnads- och säkerhetsnivåerna för mottagarautentisering. Du kan signera ett adaptivt formulär med molnbaserade digitala signaturer.

Efter [redigera adaptiva formuläregenskaper för Adobe Sign](working-with-adobe-sign.md#enableadobesign)utför du följande steg för att lägga till molnsignaturfält i ett adaptivt formulär:

1. Dra och släppa **[!UICONTROL Adobe Sign Block]** från komponentens webbläsare till det adaptiva formuläret. The [!UICONTROL Adobe Sign Block] har alla komponenter som stöds [!DNL Adobe Sign] fält. Som standard läggs en **[!UICONTROL Signature]** till det adaptiva formuläret.

   ![Signeringsblock](assets/sign-block-new.png)

1. Välj **[!UICONTROL Adobe Sign Block]** och tryck på **[!UICONTROL Edit]** ![Redigera](assets/Smock_Edit_18_N.svg) ikon. Här visas alternativ för att lägga till fält och formatera utseende för ett fält.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **S.** Markera och lägg till [!DNL Adobe Sign] fält. **B.** Expandera [!DNL Adobe Sign] blockera till helskärmsläge

1. Tryck på **[!UICONTROL Adobe Sign Field]** ![Adobe Sign](assets/adobesign.png) ikon. Här visas alternativ för att markera och lägga till [!DNL Adobe Sign] fält.

   Expandera **[!UICONTROL Type]** nedrullningsbart fält att välja **[!UICONTROL Digital Signature]** och tryck på **[!UICONTROL Done]** ikon för att lägga till det markerade fältet i [!DNL Adobe Sign] -block.

   ![Elektroniska underskrifter](assets/digital_signatures_new.png)

   Du måste ange ett unikt namn för ett fält.

   Använd digitala signaturer i det adaptiva formuläret med:

   * Molnsignaturer: Signera med en [digitalt ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) som hanteras av en betrodd tjänsteleverantör.
   * Adobe Acrobat eller Reader: Hämta och öppna dokumentet med Adobe Acrobat eller Reader för att signera med ett smartkort, en USB-token eller ett filbaserat digitalt ID.

   När du har lagt till fältet för molnsignatur i det adaptiva formuläret utför du följande steg för att slutföra konfigurationsprocessen:

   * [Aktivera Adobe Sign för ett adaptivt formulär](#enableadobsignforanadaptiveform)
   * [Välj Adobe Sign Cloud Service för ett adaptivt formulär](#selectadobesigncloudserviceforanadaptiveform)
   * [Lägga till mottagare i ett anpassat formulär](#addsignerstoanadaptiveform)
   * [Välj Skicka åtgärd för ett anpassat formulär](#selectsubmitactionforanadaptiveform)


### Konfigurera tacksidan eller sammanfattningssteget {#configure-the-thank-you-page-or-summary-step-component}

The **[!UICONTROL Summary Step]** skickar automatiskt formuläret, fyller i informationen på den anpassade sammanfattningssidan och visar sammanfattningen av det skickade formuläret. Komponenten Sammanfattningssteg får full bredd som är tillgänglig för formuläret. Vi rekommenderar att du inte har någon annan komponent i avsnittet som innehåller komponenten Sammanfattningssteg.

## Vanliga frågor {#frequently-asked-questions}

**F:** Du kan bädda in ett anpassat formulär i ett annat anpassat formulär. Kan det inbäddade adaptiva formuläret [!DNL Adobe Sign] aktiverad?
**Ans:** Nej, Experience Manager Forms stöder inte användning av ett adaptivt formulär som bäddar in en [!DNL Adobe Sign] aktiverat anpassat formulär för signering

**F:** När jag skapar ett adaptivt formulär med den avancerade mallen och öppnar den för redigering visas felmeddelandet&quot;Elektronisk signatur eller mottagare är inte korrekt konfigurerade&quot;. visas. Hur löser jag felmeddelandet?
**Ans:** Anpassningsbart formulär som skapats med den avancerade mallen är konfigurerat att använda [!DNL Adobe Sign]. Lös felet genom att skapa och välja en [!DNL Adobe Sign] molnkonfiguration och konfigurera [!DNL Adobe Sign] mottagare av det adaptiva formuläret.

**F:** Kan jag använda [!DNL Adobe Sign] texttaggar i en statisk textkomponent i ett adaptivt formulär?
**Ans:** Ja, du kan använda texttaggar i en textkomponent för att lägga till [!DNL Adobe Sign] fält till ett dokument i en post (endast det automatiskt genererade alternativet för postdokument) aktiverat anpassat formulär. Mer information om proceduren och reglerna för att skapa en texttagg finns i [Adobe Sign Documentation](https://helpx.adobe.com/sign/using/text-tag.html). Dessutom har Adaptive Forms begränsat stöd för texttaggar. Du kan använda texttaggarna för att skapa endast de fält som [Adobe Sign Block](working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form) stöder.

## Felsök {#troubleshoot}

### [!DNL Adobe Sign] avtalsfel {#adobe-sign-agreement-failures}

**Problem**
När [!DNL Adobe Sign] tjänsten är konfigurerad för ett adaptivt formulär. Tjänsten kan inte skapa en [!DNL Adobe Sign] det underliggande adaptiva formuläret.

**Upplösning**

* Kontrollera [konfiguration av Adobe Sign Cloud Service](adobe-sign-integration-adaptive-forms.md) används i adaptiv form.
* Kontrollera att API-programmet [!DNL Adobe Sign] server som används för att konfigurera [!DNL Adobe Sign] Cloud Servicen har nödvändig behörighet.
* Om du använder flera [!DNL Adobe Sign] Cloud Services, peka på **[!UICONTROL oAuth URL]** av alla tjänster till samma **[!UICONTROL Adobe Sign Shard]**.

* Använd separata e-postadresser för att konfigurera [!DNL Adobe Sign] och för den första eller enda mottagaren. E-postadressen till den första mottagaren eller den enda mottagaren (om det finns en enda mottagare) kan inte vara identisk med [!DNL Adobe Sign] konto som används för att konfigurera AEM Cloud-tjänster.

## Relaterade artiklar {#related-articles}

* [Integrera [!DNL Adobe Sign] med [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md)
* [Bästa tillvägagångssätt för att använda [!DNL Adobe Sign] med Adaptiv Forms](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
