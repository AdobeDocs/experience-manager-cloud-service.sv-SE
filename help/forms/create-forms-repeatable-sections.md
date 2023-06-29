---
title: Repeterbarhet i adaptiv form (kärnkomponenter)
description: Använd upprepningsfunktionen i panelkomponenterna för att upprepa liknande avsnitt i en adaptiv form.
role: Architect, Developer, Admin, User
source-git-commit: bf45e7b935c3e57c2ecf77d9391abda80ee4a761
workflow-type: tm+mt
source-wordcount: '1410'
ht-degree: 0%

---


# Skapa formulär med repeterbara avsnitt (kärnkomponenter) {#repeat-panel}


| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-forms-repeatable-sections.html?lang=en) |
| AEM as a Cloud Service | Den här artikeln |

Ett upprepningsbart avsnitt avser en del av ett formulär som kan dupliceras eller upprepas flera gånger för att samla in information för flera instanser av samma data.

Ta till exempel ett formulär som används för att samla in information om en persons arbetsupplevelse. Du kan ha ett upprepningsbart avsnitt där du kan hämta information om varje föregående jobb. Det repeterbara avsnittet innehåller vanligtvis fält som företagsnamn, befattning, anställningsdatum och ansvarsområden. Användaren kan lägga till flera instanser av det repeterbara avsnittet för att ange information om varje jobb som han/hon har utfört.

![Repeterbarhet](/help/forms/assets/repeatable-adaptive-form-example.gif)

I slutet av den här artikeln lär du dig att:

* Skapa ett upprepningsbart avsnitt i en adaptiv form
* Ange minsta eller högsta antal upprepningar för en adaptiv formulärkomponent
* Använd regelredigeraren för att konfigurera åtgärder för tillägg eller borttagning för repeterbara avsnitt

Du kan använda [Panel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html), [Dragspel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html), [Vågräta flikar](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html), eller [guide](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html) för att göra avsnitt i en adaptiv form repeterbara. Du kan lägga till underordnade komponenter till panelen, dragspelspanelen, vågräta flikar eller guidekomponenter för att skapa upprepningsbart avsnitt i ett formulär.


Exemplen i det här dokumentet är baserade på [Panel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html) -komponenten. Du kan utföra identiska steg för att göra [Dragspel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html), [Vågräta flikar](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html)och [guide](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html) komponenter repeterbara.

## Lägga till eller ta bort repeterbara avsnitt i ett formulär {#add-or-delete-repeatable-section-in-panel-container}

Om du vill upprepa en panel i formuläret eller ta bort repeterbara paneler använder formulärförfattaren en knappkomponent för att lägga till eller ta bort en instans av panelen. Så här lägger du till eller tar bort repeterbara avsnitt (paneler) i ett formulär:

* [Gör panelbehållaren upprepningsbar](#make-panel-container-repeatable)
* [Lägg till upprepningsbart avsnitt](#add-repeatable-section-using-instance-manager-via-scripts)
* [Ta bort repeterbara avsnitt](#delete-repeatable-section-using-instance-manager-via-scripts)

### Gör panelbehållaren upprepningsbar {#make-panel-container-repeatable}

![Fliken Tillgänglighet](/help/forms/assets/repeat-panel.png)

Så här gör du en panel upprepningsbar:
1. Välj en panelbehållare och tryck på ![cmppr](/help/forms/assets/cmppr.png).
1. Klicka på **upprepningspanel** och växla till **gör panelen upprepningsbar**.
1. Ange **minsta repetitioner** som krävs för minst repeterbara avsnitt kan du ange **minsta repetitioner** till noll för att inte hämta paneler eller för att ta bort de upprepade panelerna. Som standard är värdet för minsta repetition noll.
1. Ange **maximalt antal upprepningar** om du vill upprepa panelens antal gånger som krävs är värdet som standard oändligt.

   >[!NOTE]
   >
   > 
   > * Minsta repetition får inte vara -ve-värde.
   > * Om du vill skapa en panel som inte är upprepningsbar anger du ett värde för det högsta och lägsta fältet.

### Lägga till upprepningsbart avsnitt med instanshanteraren (via skript) {#add-repeatable-section-using-instance-manager-via-scripts}

Panelens överordnade objekt som ska upprepas bör innehålla en Lägg till-knapp för att hantera upprepad instans av panelen. Följ de här stegen för att infoga knappar i det överordnade objektet och aktivera skript på knapparna:

1. Lägg till en **knappkomponent** till panelens överordnade. I exempelvideon nedan är det en knappkomponent med etikettnamnet **Lägg till** och fältnamn **AddPanel**, används. Markera komponenten och tryck på ![edit-rules](/help/forms/assets/edit-rules.png). Reglerna för knappkomponenten öppnas i regelredigeraren.
1. Klicka på **Skapa**.

   Välj **Visual Editor** på raden Formulärobjekt och -funktioner.

   1. Välj läge under WHEN i regelområdet **klickas**.
   1. Under SEN väljer du **Lägg till instans** och dra och släpp panelen med ![växlingspanel](/help/forms/assets/toggle-side-panel.png) eller markera med **Släpp objekt eller välj här.**

   Välj **Kodredigeraren** på raden Formulärobjekt och -funktioner. Klicka **Redigera regler** och i kodområdet:

   * Om du vill skapa en knapp för panelen Lägg till anger du `this.panel.instanceManager.addInstance()`

   Klicka **Klar**.

>[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)


### Ta bort repeterbara avsnitt med instanshanteraren (via skript) {#delete-repeatable-section-using-instance-manager-via-scripts}

Panelens överordnade panel bör innehålla en borttagningsknapp för att ta bort en instans av de repeterbara panelerna. Följ de här stegen för att infoga knappar i det överordnade objektet och aktivera skript på knapparna för att ta bort repeterbara paneler:

1. Lägg till en **knappkomponent** till panelens överordnade, i videon nedan, en knappkomponent med etikettnamnet **delete** och fältnamn **DeletePanel** används. Markera komponenten och tryck på ![edit-rules](/help/forms/assets/edit-rules.png). Reglerna för knappkomponenten öppnas i regelredigeraren.
1. Klicka på **Skapa**.

   Välj **Visual Editor** på raden Formulärobjekt och -funktioner.

   1. I regelområdet, under WHEN **DeletePanel**, välj läge **klickas**.
   1. Under SEN väljer du **Ta bort instans** och dra och släpp panelen med ![växlingspanel](/help/forms/assets/toggle-side-panel.png) eller markera med **Släpp objekt eller välj här.**

   Välj **Kodredigeraren** på raden Formulärobjekt och -funktioner. Klicka **Redigera regler** och i kodområdet:

   * Om du vill skapa en knapp för borttagningspanelen anger du `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

   Klicka **Klar**.

>[!NOTE]
>
>Om ett fält tillhör en repeterbar panel kan du inte komma åt det direkt med dess namn i skripten. Om du vill komma åt fältet anger du den repeterbara instans som fältet tillhör med `instances` API in `InstanceManager`. Syntaxen som ska användas `instances` API in `InstanceManager` är:
>
>
>`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
>
>
>Du kan till exempel skapa ett anpassat formulär med en upprepningsbar panel med en textruta. När du fyller i formuläret i förväg med tre repeterbara textrutor behöver du XML-koden nedan:
>
>
>`<panel1><textbox1>AA1</panel1></textbox1>`
>
>
>`<panel1><textbox1>AA2</panel1></textbox1>`
>
>
>`<panel1><textbox1>AA3</panel1></textbox1>`
>
>
>Om du vill läsa AA1-data anger du:
>
>
>`Panel1.instanceManager.instances[0].textbox.value`
>
>
>Om du vill läsa AA2-data anger du:
>
>
>`Panel1.instanceManager.instances[1].textbox.value`
>
>
>Mer information finns i: Klass: InstanceManager#instances i [AEM Forms Java API-referens](https://adobe.com/go/learn_aemforms_documentation_63).

>[!NOTE]
>
> När alla instanser av en panel har tagits bort från ett adaptivt formulär kan du lägga till en instans av den borttagna panelen med syntaxen _panelName för att fånga instanshanteraren på panelen och använda instanshanterarens addInstance API för att lägga till den borttagna instansen. Till exempel _panelName.addInstance(). En instans av den borttagna panelen läggs till.

<!--
![panel-repeatability-video](/help/adaptive-forms/assets/panel-repeatability-video.mp4)
-->

<!--

## Using the accordion layout for the parent panel &nbsp; {#using-the-accordion-layout-for-the-parent-panel-nbsp}

A panel has various layouts options. The Layout for accordian design option has out of the box support for repeatable panels. Perform the following steps to repeatable panel with Layout for accordian design option:

1. On the parent of panel to be repeated, tap ![cmppr](assets/cmppr.png). You can see the properties in the sidebar. In the **Layout** drop-down, select **Accordion**.
1. On a panel, which is to be repeated, tap ![cmppr](assets/cmppr.png). You can see the panel properties in the sidebar. Enable the **Make Panel Repeatable** tab, and specify value for the **Maximum** and **Minimum** fields.

   Now, you can use the plus (+) and delete ( ![delete-panel](assets/delete-panel.png)) buttons to add and remove the panels.

-->

## Använda upprepade delformulär från formulärmallen (XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

Upprepningsbart delformulär liknar de repeterbara panelerna i Adaptiv Forms. Gör så här i AEM Forms Designer för att skapa ett upprepande delformulär:

1. Markera det överordnade delformuläret för det delformulär som du vill upprepa på paletten Hierarki.
1. Klicka på fliken Delformulär på paletten Objekt och välj Flödat i listan Innehåll.
1. Markera delformuläret som ska upprepas.
1. Klicka på fliken Delformulär på paletten Objekt och välj antingen Placerat eller Flödat i listan Innehåll.
1. Klicka på fliken Bindning och välj Upprepa delformulär för varje dataobjekt.
1. Om du vill ange det minsta antalet upprepningar väljer du Minsta antal och skriver ett tal i den associerade rutan. Om det här alternativet är inställt på 0 och inga data anges för objekten i delformuläret vid datasammanfogning, placeras inte delformuläret när formuläret återges.
1. Om du vill ange maximalt antal upprepningar av delformulär väljer du Max och skriver ett tal i den tillhörande rutan. Om du inte anger något värde i rutan Max är antalet delformulärrepetitioner obegränsat.
1. Om du vill ange ett visst antal upprepningar av delformulär, oavsett datamängd, väljer du Antal initialer och skriver ett tal i den tillhörande rutan. Om du väljer det här alternativet och antingen inga data är tillgängliga eller det finns färre data än det angivna värdet för antal initialer, placeras tomma instanser av delformuläret fortfarande i formuläret.
1. Lägg till två knappar i det överordnade delformuläret - en för att lägga till en instans och en för att ta bort en instans av det repeterbara delformuläret. Detaljerade anvisningar finns i [Bygg en åtgärd](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2).
1. Länka formulärmallen till det anpassade formuläret. Detaljerade anvisningar finns i [Skapa ett anpassat formulär baserat på en mall](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=en#create-an-adaptive-form-based-on-an-xfa-form-template).
1. Använd knapparna i steg 9 för att lägga till och ta bort delformulär.

Den bifogade ZIP-filen innehåller ett exempel på upprepningsbart delformulär.

[Hämta fil](/help/forms/assets/samplerepeatablesubform.zip)

## Använda upprepade inställningar för ett XML-schema (XSD) {#using-repeat-settings-of-an-xml-schema-xsd-br}

Du kan skapa upprepningsbara paneler från ett XML-schema och från egenskapen minOcCours &amp; maxOccurs för alla komplexa tytelement. Mer information om XML-schema finns i [Skapa anpassningsbara formulär med XML-schema som formulärmodell](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adaptive-form-xml-schema-form-model.html).

I följande kod visas `SampleType`I panelen används egenskapen minOcCours och maxOccurs.

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartDate" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```


## relaterade artiklar

* [Skapa ett adaptivt formulär](creating-adaptive-form-core-components.md)
* [Skapa stilar eller teman för formulären](using-themes-in-core-components.md)
* [Lägga till dynamiskt beteende i formulär med regelredigeraren](rule-editor.md)
* [Ange formulärlayout för olika skärmstorlekar och enhetstyper](/help/sites-cloud/authoring/features/responsive-layout.md)