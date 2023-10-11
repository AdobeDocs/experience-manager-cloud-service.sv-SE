---
title: Hur anropar jag tjänsten Form Data Model från Adaptive Forms med API:er?
description: Beskriver det invokeWebServices-API som du kan använda för att anropa webbtjänster som skrivits i WSDL från ett adaptivt formulärfält.
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
source-git-commit: d33c7278d16a8cce76c87b606ca09aa91f1c3563
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# API för att anropa tjänsten Form Data Model från Adaptive Forms {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## Översikt {#overview}

[!DNL AEM Forms] gör det möjligt för formulärförfattare att ytterligare förenkla och förbättra formulärifyllningen genom att anropa tjänster som konfigurerats i en formulärdatamodell inifrån ett adaptivt formulärfält. Om du vill anropa en datamodelltjänst kan du antingen skapa en regel i den visuella redigeraren eller ange ett JavaScript med `guidelib.dataIntegrationUtils.executeOperation` API i kodredigeraren för [regelredigerare](rule-editor.md).

Det här dokumentet fokuserar på att skriva ett JavaScript med `guidelib.dataIntegrationUtils.executeOperation` API för att anropa en tjänst.

## Använda API {#using-the-api}

The `guidelib.dataIntegrationUtils.executeOperation` API anropar en tjänst inifrån ett adaptivt formulärfält. API-syntaxen är följande:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

Strukturen för `guidelib.dataIntegrationUtils.executeOperation` API anger information om tjänståtgärden. Strukturen har följande syntax.

```javascript
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

API-strukturen anger följande information om tjänståtgärden.

<table>
 <tbody>
  <tr>
   <th>Parameter</th>
   <th>Beskrivning</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>Struktur för att ange identifierare för formulärdatamodell, åtgärdstitel och åtgärdsnamn</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>Anger databassökvägen till formulärdatamodellen inklusive dess namn</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>Anger namnet på den tjänståtgärd som ska köras</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>Kopplar ett eller flera formulärobjekt till indataargumenten för tjänståtgärden</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>Kopplar ett eller flera formulärobjekt till utdatavärden från tjänståtgärden för att fylla i formulärfält<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>Returnerar värden baserat på indataargumenten för serviceåtgärden. Det är en valfri parameter som används som en callback-funktion.<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>Visar ett felmeddelande om återanropsfunktionen lyckas inte visa utdatavärden baserat på indataargumenten. Det är en valfri parameter som används som en callback-funktion.<br /> </td>
  </tr>
 </tbody>
</table>

## Exempelskript för att anropa en tjänst {#sample-script-to-invoke-a-service}

Följande exempelskript använder `guidelib.dataIntegrationUtils.executeOperation` API för att anropa `getAccountById` tjänståtgärd konfigurerad i `employeeAccount` formulärdatamodell.

The `getAccountById` operationen tar värdet i `employeeID` formulärfält som indata för `empId` argument och returnerar medarbetarens namn, kontonummer och kontosaldo för motsvarande medarbetare. Utdatavärdena fylls i i de angivna formulärfälten. Värdet i `name` argumentet har fyllts i i `fullName` formulärelement och värde för `accountNumber` argument i `account` formulärelement.

```javascript
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

## Använda API:t med återanropsfunktionen {#using-the-api-callback}

Du kan även anropa tjänsten Form Data Model med `guidelib.dataIntegrationUtils.executeOperation` API med en återanropsfunktion. API-syntaxen är följande:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

Återanropsfunktionen kan ha `success` och `failure` callback-funktioner.

### Exempelskript med återanropsfunktioner för lyckade och misslyckade åtgärder {#callback-function-success-failure}

Följande exempelskript använder `guidelib.dataIntegrationUtils.executeOperation` API för att anropa `GETOrder` tjänståtgärd konfigurerad i `employeeOrder` formulärdatamodell.

The `GETOrder` operationen tar värdet i `Order ID` formulärfält som indata för `orderId` argument och returnerar orderkvantitetsvärdet i `success` callback-funktion.  Om `success` callback-funktionen returnerar inte orderkvantiteten, `failure` callback-funktionen visar `Error occured` meddelande.

>[!NOTE]
>
> Om du använder `success` callback-funktionen, utdatavärdena fylls inte i i de angivna formulärfälten.

```javascript
var operationInfo = {
    "formDataModelId": "/content/dam/formsanddocuments-fdm/employeeOrder",
    "operationTitle": "GETOrder",
    "operationName": "GETOrder"
};
var inputs = {
    "orderId" : Order ID
};
var outputs = {};
var success = function (wsdlOutput, textStatus, jqXHR) {
order_quantity.value = JSON.parse(wsdlOutput).quantity;
 };
var failure = function(){
alert('Error occured');
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, success, failure);
```
