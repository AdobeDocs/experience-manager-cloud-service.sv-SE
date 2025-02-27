---
title: Understanding Universal Editor - Developer Tutorial
description: Den här självstudiekursen hjälper dig att komma igång med Universal Editor-gränssnittet. Det vägleder dig att förstå användargränssnittet för att skapa egna Edge Delivery Services-formulär i Universell redigerare.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: 744f505c8e97b6ca6947b685ddb1eba41b370cfa
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 0%

---

# Exploring the Universal Editor (WYSIWYG) Interface

[Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) har ett enkelt, visuellt och intuitivt What You See Is What You Get-gränssnitt (WYSIWYG) för Adobe Edge Delivery Services Forms. Det har ett modernt gränssnitt med dra-och-släpp-funktioner för effektiv formulärutveckling.

![Användargränssnitt för Universal Editor](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## Understanding Universal Editor Interface

När formulärförfattaren redigerar formuläret med Universal Editor, öppnar konsolen ett interaktivt WYSIWYG-gränssnitt där användaren kan börja redigera formuläret.

>[!NOTE]
>
> Läs artikeln [Komma igång med Edge Delivery Services för AEM Forms med Universal Editor (WYSIWYG)](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md) om du vill lära dig hur du skapar formulär med den universella redigeraren.

![Användargränssnitt för Universal Editor](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

Gränssnittet för Universal Editor är uppdelat i fyra delar:

* **[A: Experience Cloud Header](#experience-cloud-header)**
* **[B: Verktygsfältet Universal Editor](#universal-editor-toolbar)**
* **[C: Egenskapspanelen](#properties-panel)**
* **[D: Redigeraren](#editor)**

### Experience Cloud Header

Experience Cloud-rubriken finns högst upp i konsolen. Här finns information om den aktuella platsen inom Experience Cloud. Du kan även navigera till andra Experience Cloud-program.

![Universal Editor Experience Cloud Header](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)


Låt oss förstå var och en av komponenterna.

* **Adobe Experience Cloud**

  Du kan klicka på länken **Adobe Experience Cloud** till vänster på skärmen för att navigera till roten i Experience Manager-lösningen och komma åt verktyg som Experience Manager Sites, Experience Manager Assets och Experience Manager Guides.

  ![Adobe Experience Manager](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager.png){width=50%,height=50%}

* **Organisationsnamn**

  **Organisationsnamnet** visar namnet på den IMS-organisation du är inloggad på. Du kan växla till en annan IMS-organisation om de har tillgång till andra organisationer genom att välja i listrutan. Det aktuella IMS-organisationsnamnet är till exempel `AEM Forms Internal01`.

  ![Organisation](/help/edge/docs/forms/universal-editor/assets/universal-editor-organization.png){width=50%,height=50%}


* **Hjälp**

  Hjälpikonen ger snabb åtkomst till utbildningsresurser och supportresurser. Formulärets författare kan även lägga till feedback i avsnittet **Hjälp**.
  ![Hjälp](/help/edge/docs/forms/universal-editor/assets/ue-help.png){width=50%,height=50%}


* **Meddelanden**

  Avsnittet **Meddelande** visar antalet för närvarande tilldelade ofullständiga meddelanden, förfrågningar och aktuella uppgifter i IMS-organisationen.

  ![Meddelande](/help/edge/docs/forms/universal-editor/assets/ue-notification.png){width=50%,height=50%}


* **Lösningar**

  Du kan växla till andra Experience Cloud-lösningar via länken **Lösningar** .
  ![Lösningar](/help/edge/docs/forms/universal-editor/assets/ue-solutions.png){width=50%,height=50%}


* **Författare**
Ikonen visar information om formulärförfattaren tillsammans med namnet på den IMS-organisation där författaren är inloggad.
  ![Författare](/help/edge/docs/forms/universal-editor/assets/ue-author.png){width=50%,height=50%}

### Verktygsfältet Universell redigerare

I verktygsfältet kan du navigera till och redigera andra formulär. De kan också publicera eller avpublicera formuläret, redigera formulärets egenskaper och öppna regelredigeraren.
![Verktygsfältet Universal Editor](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

Låt oss förstå var och en av komponenterna.

* **Hemknapp**
Med hemknappen kan du navigera till startsidan i Universella redigeringsprogram. Du kan också ange URL:en till det formulär som du vill redigera direkt i den universella redigeraren.
  ![Startsida för Universal Editor](/help/edge/docs/forms/universal-editor/assets/ue-home.png)



* **Platsfält**
I **platsfältet** visas adressen till det formulär som författaren redigerar. Du kan också ange en annan formulär-URL genom att klicka på platsfältet. Kortkommandon för att öppna platsfältet är tangent `l`.
  ![Platsfält](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png){width=50%,height=50%}



* **Regelredigeraren**

  **Regelredigeraren** erbjuder ett intuitivt visuellt gränssnitt för att skapa och hantera regler. Du kan lägga till dynamiskt formulärbeteende med regelredigeraren.

  ![Regelredigeraren](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

  >[!NOTE]
  >
  > * Tillägget Regelredigerare är inte aktiverat som standard i Universellt redigeringsprogram. Om du vill aktivera tillägget Regelredigerare skriver du till oss på [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) från ditt officiella e-post-id.
  > * Mer information om hur du skapar regler finns i artikeln [Introduktion till regelredigeraren i WYSIWYG Authoring](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md).

* **Redigera formuläregenskaper**
Du kan redigera formuläregenskaperna, till exempel formulärdatamodellen och publiceringsdatumet, genom att klicka på alternativet **Redigera formuläregenskaper** .
  ![Redigera formuläregenskaper](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)



* **Inställningar för autentiseringshuvud**
Med inställningarna för **autentiseringshuvudet** kan författaren ange en anpassad autentiseringshuvud för lokal utveckling.
  ![autentiseringsrubrik](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png){width=50%,height=50%}



* **Responsivt läge**
  Med alternativet **Responsivt läge** kan du definiera hur Universal Editor ska återge formuläret. Som standard öppnas redigeraren i en skrivbordslayout där höjd och bredd bestäms automatiskt av webbläsaren. Du kan också välja att emulera en mobil enhet och kontrollera hur formuläret visas på mobila enheter.

  ![Responsivt läge](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png){width=50%,height=50%}


* **Förhandsgranskningsläge**
I förhandsgranskningsläget visas formuläret i redigeraren exakt som det publiceras. Detta gör att författaren kan navigera i formuläret genom att klicka på länkar och knappar. När författaren är nöjd med redigeringarna kan han eller hon publicera formuläret för användare. Kortkommandon för att växla mellan redigerings- och förhandsgranskningsläge är `p`.
  ![Förhandsgranska](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

* **Öppna sida**
Med alternativet **Öppna sida** öppnas formuläret på en ny flik för förhandsgranskning. Kortkommandot för att öppna formuläret i förhandsgranskningsläge på en ny flik är `o`.
  ![Öppna sida](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

* **Publicera**

  Med knappen **Publicera** kan du göra formuläret tillgängligt för användare i realtid.
  ![Publicera](/help/edge/docs/forms/universal-editor/assets/ue-publish.png){width=50%,height=50%}

* **Ellips**
När författaren klickar på ellipsalternativet (..) visas alternativet **Avpublicera** . Du kan avpublicera ett formulär med alternativet **Avpublicera**.
  ![Ellips](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png){width=50%,height=50%}

### Egenskapspanelen

Panelen **Egenskaper** finns till höger om redigeraren. Här visas information om komponenten som är markerad i formulärets hierarki. Det är standardstrukturen när ingen komponent är markerad.
![panelen Nyansegenskaper](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png){width=50%,height=50%}


Låt oss förstå var och en av komponenterna.


* **Egenskapsläge**
I alternativet **Egenskaper** visas egenskaperna för den markerade komponenten i redigeraren. Bilden visar till exempel egenskaperna för den valda talindatakomponenten. Du kan ändra komponentens egenskaper med det här alternativet. Kortkommandot för att öppna komponentens egenskaper är `d`.

  ![ue-properties](/help/edge/docs/forms/universal-editor/assets/ue-properties.png){width=50%,height=50%}


* **Innehållsträd**
Alternativet **Innehållsträd** visar formulärets hierarki. När författaren klickar på ett objekt i innehållsträdet markeras det och rullas till den komponenten. Kortkommandon för att växla mellan vyn för innehållsträdet är tangenten `f`.

  ![Innehållsträdet](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png){width=50%,height=50%}


* **Generera variationer**
  **Generera variationer** använder artificiell intelligens för att skapa olika versioner av formulär baserat på specifika uppmaningar. Dessa instruktioner kan antingen tillhandahållas av Adobe eller utformas och hanteras av formulärförfattaren.

  ![variation](/help/edge/docs/forms/universal-editor/assets/ue-variations.png){width=50%,height=50%}


  >[!NOTE]
  >
  > Instruktioner om hur du använder Generera variationer för formulär finns i artikeln [Generera variationer](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)

* **Experimentation**:

  **Experimentation** avser tekniker som används för att testa olika variationer av formulär och layout för att optimera användarupplevelsen och prestandan.
  ![experimenterande](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png){width=50%,height=50%}


* **Personalization**
Alternativet **Personalization** konfigurerar inställningarna för att upprätta en anslutning mellan formulären och Adobe Experience Platform (AEP) som är en del av Adobe ekosystem eller externa program.
  ![Personalization](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png){width=50%,height=50%}


* **A/B-testning**:
  **A/B-testning** avser tekniker som används för att testa olika varianter av formulär och layout för att optimera användarupplevelsen och prestandan.
  ![A/B-testning](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png){width=50%,height=50%}



* **Aktivitetshantering**:
Med funktionen **Uppgiftshantering** kan du effektivisera arbetsflöden och förbättra samarbetet genom att låta team hantera, spåra och utföra uppgifter som rör anpassning och optimering av formulär
  ![aktivitetshantering](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png){width=50%,height=50%}

.
* **Innehållsutkast**

  Med alternativet **Innehållsutkast** kan du skapa utkast för RTF-element. Du kan skapa utkast med befintlig formulärtext eller från grunden. Du kan redigera eller ta bort utkast efter behov. Som standard visas bara tre utkast, men om du klickar på **Visa alla** visas resten.

  ![aktivitetshantering](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png){width=50%,height=50%}


* **Data Source**

  Med alternativet **Data Source** kan du konfigurera datakällor och välja dem när du skapar en formulärdatamodell (FDM). Den gör alla datamodellsobjekt, egenskaper och tjänster från de valda datakällorna tillgängliga för användning i formulärdatamodellen.
  ![Data Source](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png){width=50%,height=50%}

* **Lägg till**

  Alternativet **Lägg till** öppnar en listruta med komponenter som kan läggas till i den valda behållaren. I ett adaptivt formulär visas t.ex. de tillgängliga komponenter som kan läggas till i ett formulär i listan. Kortkommandot för att öppna komponentlistan är `a`.
  ![Lägg till ikon](/help/edge/docs/forms/universal-editor/assets/ue-add.png){width=50%,height=50%}

* **Duplicera**

  Alternativet **Duplicera** skapar en kopia av komponenten, som är markerad antingen i innehållsträdet eller i redigeraren.
  ![Duplicera ikon](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png){width=50%,height=50%}


* **Ta bort**
Med alternativet **Ta bort** tar du bort en komponent som är markerad i innehållsträdet eller redigeraren.

  ![Ta bort](/help/edge/docs/forms/universal-editor/assets/ue-delete.png){width=50%,height=50%}

### Redigerare

Med redigeraren kan du redigera formuläret, och formuläret som anges i platsfältet återges i redigeringsområdet. Om redigeraren är i förhandsgranskningsläge kan du navigera i formuläret med de tillgängliga knapparna och länkarna.
![Redigeraren](/help/edge/docs/forms/universal-editor/assets/ue-editor.png){width=50%,height=50%}

## Se även

{{universal-editor-see-also}}
