---
title: Hur får man referensteman och mallar för AEM-blanketter?
description: AEM Forms innehåller exempel på adaptiva formulärteman, mallar och formulärdatamodeller som hjälper dig att snabbt skapa formulär.
feature: Adaptive Forms, Foundation Components
exl-id: 81588759-22da-4123-92fe-5ca97e97f1e4
role: User, Developer, Admin
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 0%

---

# Referensteman, mallar och formulärdatamodeller {#reference-themes-templates-and-data-models}


| Gäller för | Artikellänk |
| -------- | ---------------------------- |
| Adaptiv form baserad på kärnkomponenter | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) |
| Adaptiv form baserad på grundläggande komponenter | Den här artikeln |

>[!NOTE]
>
> Adobe rekommenderar att du använder den moderna och utbyggbara datainhämtningen [Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) för [att skapa nya adaptiva Forms](/help/forms/creating-adaptive-form-core-components.md) eller [lägga till adaptiva Forms på AEM Sites-sidor](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter.

AEM Forms as a Cloud Service har flera referensteman, mallar och formulärdatamodell (FDM) som hjälper dig att snabbt komma igång med att skapa adaptiva Forms. Du kan hämta [referensinnehållspaketet från programdistributionsportalen](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip) och använda [Package Manager](/help/implementing/developing/tools/package-manager.md) för att installera [referensinnehållspaketet](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip) i din produktions-, utvecklings- eller lokala utvecklingsmiljö för att hämta referensresurserna till din miljö.

De teman, mallar och formulärdatamodell (FDM) som ingår i referensinnehållspaketet är:


| Teman | Mallar | FDM (Form Data Model) |
|---------|----------|---------|
| Arbetsyta 3.0 | Grundläggande | Microsoft Dynamics 365 |
| Tranquil | Tom | Salesforce |
| Urbane |   |  |
| Ultramarin |  |  |
| Beryl |  |  |
| Sjukvård |  |   |
| FSI |   |   |

## Referensteman {#reference-themes}

Med [Teman](/help/forms/themes.md) kan du formatera formulär utan djupa kunskaper om CSS. Du kan hämta följande teman genom att installera [referensinnehållspaketet](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip):

* Beryl
* Arbetsyta 3.0
* Tranquil
* Urbane
* Ultramarin
* Sjukvård
* FSI (Finansiella tjänster och försäkringar)

Varje tema innehåller en unik och elegant stil som du kan använda för att skapa snygga, anpassningsbara formulär för användarna. Den innehåller en unik formatering för väljare som panel, textruta, numerisk ruta, alternativknapp, tabell och switch. Stilar i dessa teman baseras på krav. I ett visst scenario behöver du till exempel ett minimalistiskt tema med rena teckensnitt. Med Frihetstemat kan du få den där looken.

![Referensteman](assets/ref-themes.png)

Teman som ingår i det här paketet är responsiva, och format i dessa teman definieras för mobilskärmar och datorskärmar. De flesta moderna webbläsare på en mängd olika enheter kan återge formulär som används med något av dessa teman utan krångel.

Mer information om hur du installerar paketet finns i [Arbeta med paket](/help/implementing/developing/tools/package-manager.md).

## Beryl {#beryl}

Beryl-temat betonar användningen av bakgrundsbilder, genomskinlighet och stora, platta ikoner. På skärmbilden nedan ser du hur Beryl-temat ser ut och hur det kan förbättra formateringen av ditt formulär.

![Berytema](assets/beryl.png)

## Arbetsyta 3.0 {#canvas}

Canvas 3.0 är standardtemat för Adaptive Forms och betonar användningen av grundläggande färger, genomskinlighet och platta ikoner. På skärmbilden nedan ser du hur temat Canvas 3.0 ser ut.

![Berytema](assets/canvas.png)


## Tranquil {#tranquil}

Med det tillfälliga temat får du ljusa och mörka nyanser av det Tranquil-färgschemat för att framhäva olika komponenter i ett formulär. Alternativknappar, paneler och flikar får till exempel en annan grön ton.

![Transiärt tema](assets/tranquil.png)


## Urbane {#urbane}

Urbane-temat betonar ett minimalistiskt och funktionellt utseende på ditt formulär. När du använder Urbane-temat i ditt formulär ser du att komponenterna är platta. Panelerna får tunna konturer för att skapa ett modernt utseende.

![Urban-tema](assets/urbane.png)


## Ultramarin {#ultramarine}

Ultramarintemat använder djupa blå skuggor för att framhäva komponenter som tabbar, paneler, textrutor och knappar.

![Ultramarintema](assets/ultramarine.png)

## Sjukvård {#healthcare}

Hälsotemat använder djupa gröna skuggor för att framhäva komponenter som tabbar, paneler, textrutor och knappar.

![FSI-tema](assets/healthcare.png)


## FSI (Finansiella tjänster och försäkringar)

FSI-temat betonar ett minimalistiskt och funktionellt utseende på ditt formulär. När du använder FSI-temat i ditt formulär ser du att panelkomponenterna är gula.

![FSI-tema](assets/fsi.png)

## Referensmallar {#reference-templates}


Med [Mallar](/help/forms/themes.md) kan du definiera den inledande formulärstrukturen, innehållet och åtgärderna för dina formulär. Du kan hämta följande mallar genom att installera [referensinnehållspaketet](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip):

* Grundläggande
* Tom

Med den grundläggande mallen kan du snabbt skapa ett registreringsformulär. Du kan också använda den för att förhandsgranska funktionaliteten i adaptiva Forms Foundation-komponenter. Den innehåller en guidelayout för avsnitt-för-avsnitt-presentation av data. Använd mallen Tom för att börja skapa ett adaptivt formulär från en tom arbetsyta.


## FDM (Reference Form Data Model) {#reference-models}

Den adaptiva Forms kan sedan interagera med Microsoft Dynamics 365- och Salesforce-servrar för att möjliggöra arbetsflöden. Till exempel:

* Skriv data i Microsoft Dynamics 365 och Salesforce när ni skickar in adaptiva blanketter.
* Skriv data i Microsoft Dynamics 365 och Salesforce via anpassade entiteter som definierats i formulärdatamodellen (FDM) och omvänt.
* Fråga Microsoft Dynamics 365- och Salesforce-servern efter data och fylla i Adaptive Forms i förväg.
* Läs data från Microsoft Dynamics 365 och Salesforce-servern.

Du kan hämta följande formulärdatamodell (FDM) genom att installera [referensinnehållspaketet](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip):

* Microsoft® Dynamics 365
* Salesforce

Information om hur du använder dessa modeller finns i [Konfigurera molntjänsterna Microsoft Dynamics 365 och Salesforce](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=en#configure-dynamics-cloud-service)


## Se även {#see-also}

{{see-also}}