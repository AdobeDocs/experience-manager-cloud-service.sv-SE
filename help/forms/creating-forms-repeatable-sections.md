---
title: Skapa formulär med repeterbara avsnitt
seo-title: Creating forms with repeatable sections
description: Upprepningsbara avsnitt är paneler som kan läggas till eller tas bort dynamiskt i ett formulär.
seo-description: Repeatable sections are panels that can be dynamically added or removed to a form.
uuid: c3fa2aa4-a6b4-458e-8534-138e075290b1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 01724ca0-6901-45e7-b045-f44814ed574e
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 16%

---


# Skapa formulär med repeterbara avsnitt {#creating-forms-with-repeatable-sections}

Upprepningsbara avsnitt är paneler som kan läggas till eller tas bort dynamiskt i ett formulär.

När du t.ex. ansöker om ett jobb, ger den jobbsökande tidigare anställningsinformation som företagsnamn, roll, projekt och annan information. Information om alla arbetsgivare kräver olika men likartade sektioner. I ett sådant scenario tillhandahåller anställningsblanketten en arbetsgivaravdelning och ger även möjlighet att dynamiskt lägga till fler sådana avsnitt. Dessa avsnitt, som läggs till dynamiskt, kallas upprepningsbara avsnitt.

Du kan använda någon av följande metoder för att skapa repeterbara paneler:

## Använda Instanshanteraren via skript  {#using-instance-manager-via-scripts-nbsp}

1. Välj en panel i redigeringsläget och tryck sedan på ![cmppr](assets/cmppr.png). Aktivera under Egenskaper i sidofältet **[!UICONTROL Make Panel Repeatable]**. Ange värden för **[!UICONTROL Maximum]** och **[!UICONTROL Minimum]** fält.

   Fältet Maximum anger det maximala antalet gånger en panel kan visas på sidan. Du kan ange -1 i fältet Maximalt antal om du vill att panelen ska visas ett obegränsat antal gånger.

   Fältet Minimum anger det minsta antalet gånger en panel visas i formuläret. Om du anger fältet Minsta antal till noll senare kan du ta bort alla instanser via skript när återgivningen är klar.

   >[!NOTE]
   >
   >Om du vill skapa en panel som inte är upprepningsbar anger du ett värde i fältet Maximum och Minimum. Dragspelslayouten stöder inte -1 i fältet Maximalt antal. Du kan ange ett högt tal för att ge begreppet oändligt värde.

1. Panelens överordnade panel, som ska upprepas, bör innehålla knappar för att lägga till och ta bort för att hantera instanser av de repeterbara panelerna. Följ de här stegen för att infoga knappar i det överordnade objektet och aktivera skript på knapparna:

   1. Dra och släpp en knappkomponent från sidofältet till panelens överordnade objekt. Markera komponenten och tryck på ![edit-rules](assets/edit-rules.png). Reglerna för knappen öppnas i regelredigeraren.
   1. Klicka på **Skapa**.

      Välj **Visual Editor** på raden Formulärobjekt och -funktioner.

      1. Välj läge under WHEN i regelområdet **klickas**.
      1. Under THEN:

         * Om du vill skapa en knapp för panelen Lägg till väljer du **Lägg till instans** och dra och släpp panelen med ![växlingspanel](assets/toggle-side-panel.png) eller markera med **Släpp objekt eller välj här.**
         * Om du vill skapa en knapp för borttagningspanelen väljer du **Ta bort instans** och dra och släpp panelen med ![växlingspanel](assets/toggle-side-panel.png) eller markera med **Släpp objekt eller välj här.**

      Välj **Kodredigeraren** på raden Formulärobjekt och -funktioner. Klicka **Redigera regler** och i kodområdet:

      * Om du vill skapa en knapp för panelen Lägg till anger du `this.panel.instanceManager.addInstance()`
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
      >Du kan till exempel skapa ett adaptivt formulär med en upprepningsbar panel med en textruta. När du fyller i formuläret i förväg med tre repeterbara textrutor behöver du XML-koden nedan:
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
      >När alla instanser av en panel har tagits bort från ett adaptivt formulär kan du lägga till en instans av den borttagna panelen med syntaxen _panelName för att fånga instanshanteraren på panelen och använda instanshanterarens addInstance API för att lägga till den borttagna instansen. Till exempel _panelName.addInstance(). En instans av den borttagna panelen läggs till.



## Använda dragspelslayouten för den överordnade panelen   {#using-the-accordion-layout-for-the-parent-panel-nbsp}

På en panel finns olika layoutalternativ. Alternativet Layout för dragspelsdesign har stöd för upprepningsbara paneler. Utför följande steg på en repeterbar panel med alternativet Layout för dragspelsdesign:

1. Tryck på den överordnade panelen för den panel som ska upprepas ![cmppr](assets/cmppr.png). Du kan se egenskaperna i sidlisten. I **Layout** nedrullningsbar meny, välja **Dragspel**.
1. Tryck på en panel som ska upprepas ![cmppr](assets/cmppr.png). Panelegenskaperna visas i sidofältet. Aktivera **Gör panelen upprepningsbar** och ange ett värde för **Maximal** och **Minimum** fält.

   Nu kan du använda plustecknet (+) och ta bort ( ![delete-panel](assets/delete-panel.png)) för att lägga till och ta bort paneler.

## Använda upprepade delformulär från formulärmallen (XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

Upprepningsbart delformulär liknar de repeterbara panelerna i Adaptiv Forms. I [!DNL AEM Forms] Designer gör följande för att skapa ett upprepande delformulär:

1. Välj överordnat delformulär till det delformulär du vill repetera på paletten Hierarki.
1. Välj Flödat i listan Innehåll på fliken Delformulär på paletten Objekt.
1. Välj det delformulär som skall repeteras.
1. Välj antingen Placerat eller Flödat i listan Innehåll på fliken Delformulär på paletten Objekt.
1. Klicka på bindningsfliken och välj att upprepa delformulär för varje dataobjekt.
1. Om du vill ange ett minsta antal upprepningar väljer du Minsta antal och skriver ett tal i tillhörande ruta. Om detta alternativ är 0, och inga data har angetts för objekten i delformuläret vid sammanslagningen, placeras delformuläret inte ut när formuläret återges.
1. Om du vill ange ett maximalt antal upprepningar väljer du Max antal och skriver ett tal i tillhörande ruta. Om du inte anger något värde i rutan Max är antalet delformulärrepetitioner obegränsat.
1. Om du vill ange ett visst antal upprepningar av delformuläret, oavsett datamängd, markerar du alternativet Startvärde och anger ett tal i rutan. Om detta alternativ valts och inga data eller färre data än det specificerade startvärdet finns, placeras ändå de tomma instanserna av delformuläret i formuläret.
1. Lägg till två knappar i det överordnade delformuläret - en för att lägga till en instans och en för att ta bort en instans av det repeterbara delformuläret. Detaljerade anvisningar finns i [Bygg en åtgärd](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2).
1. Länka formulärmallen till det anpassade formuläret. Detaljerade anvisningar finns i [Skapa ett anpassat formulär baserat på en mall](creating-adaptive-form.md#create-an-adaptive-form-based-on-a-template).
1. Använd knapparna i steg 9 för att lägga till och ta bort delformulär.

Den bifogade ZIP-filen innehåller ett exempel på upprepningsbart delformulär.

[Hämta fil](assets/samplerepeatablesubform.zip)

## Använda upprepade inställningar för ett XML-schema (XSD) {#using-repeat-settings-of-an-xml-schema-xsd-br}

Du kan skapa upprepningsbara paneler från ett XML-schema och från egenskapen minOcCours &amp; maxOccurs för alla komplexa tytelement. Mer information om XML-schema finns i [Skapa adaptiv Forms med XML-schema som formulärmodell](adaptive-form-xml-schema-form-model.md).

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

>[!NOTE]
>
>För icke-dragbar layout använder du adaptiva formulärknappskomponenter för att lägga till och ta bort instanser.
