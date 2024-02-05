---
title: Registrera en transaktion för anpassade implementeringar
description: Använd TransactionRecorder-API:t för att registrera åtgärder som inte räknas som transaktioner automatiskt
feature: Adaptive Forms, Foundation Components
hide: true
hidefromtoc: true
source-git-commit: a1a87a27d73d7472ec02de37621123bbdd3876b4
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Registrera en transaktion för anpassade implementeringar {#record-a-transaction-for-custom-implementations}

Använd TransactionRecorder-API:t för att registrera åtgärder som inte räknas som transaktioner automatiskt.

Du kan använda anpassad kod för att skicka ett PDF-formulär. Eller så skickar du ett formulär med egna metoder i stället för att använda de skicka-metoder som finns i AEM Forms. Alla tidigare nämnda åtgärder och anpassade implementeringar av AEM Forms API:er räknas inte som transaktioner. AEM Forms tillhandahåller ett API, [TransactionRecorder](https://javadoc.io/doc/com.adobe.aem/aem-forms-sdk-api/latest/com/adobe/aem/transaction/core/ITransactionRecorder.html), för att registrera sådana åtgärder som transaktioner.

Om du vill registrera en transaktion skriver du [standardsäljare](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/store-and-retrieve-af-with-2fa/create-servlet.html?lang=en) och anropa en klientserver för att registrera en transaktion. Du kan anropa servleten med AJAX eller någon annan standardmetod.

## Exempel på kod på serversidan {#sample-server-sided-code}

Du kan använda exempelkoden nedan för att köra TransactionRecorder API från en Java™-klass med ett anpassat OSGi-paket.

```java
import com.adobe.aem.transaction.core.ITransactionRecorder;
import com.adobe.aem.transaction.core.model.TransactionRecord;
import com.adobe.aem.transaction.core.exception.TransactionException;
import com.adobe.aem.transaction.core.FormsTransactionConstants;

@Reference
private ITransactionRecorder transactionRecorder;

doPost (SlingHttpServletRequest request, SlingHttpServletResponse response) {
    transactionRecorder.startContext();
    TransactionRecord txRecord = extractTxRecordFromRequest(request); //extract transaction relevant data from request
    try {
        bool success = doBillableWork();
        if (success) {
            transactionRecorder.recordTransaction(txRecord);
        }
    } catch (Exception e) {
        //exception handling
    } finally {
        transactionRecorder.endContext();
    }
}

//Here, it is assumed that txInfo is passed in Stringified json form in the ajax call (in data parameter). You can pass txInfo from client in any way that you find suitable.
private TransactionRecord extractTxRecordFromRequest(SlingHttpServletRequest request) {
    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(request.getInputStream()));
    Map<String, Object> txDataMap = new HashMap<String, Object>();
    String txData = bufferedReader.readLine();
    JSONObject txInfo= new JSONObject(txData );
    try {
        String resourceType= txInfo.getString("resourceType");
        String transactionType = txInfo.getString("transactionType");
        Integer transactionCount = (Integer)txInfo.get("transactionCount");
        //Extract all the relevant tx record attributes similarly and pass them in Transaction Record constructor as per the java doc}
        return new TransactionRecord(transactionCount, transactionType, resourceType, ..);
    } catch (JSONException e) {
        //exception handling
    } finally {
        bufferedReader.close();
    }
}
```

## Exempel på kod på klientsidan {#sample-client-side-code}

Du kan använda exempelkoden nedan för att anropa den server som har `TransactionRecorder`API.

```javascript
$.ajax({
   type: 'POST',
   url: url, //servlet url
   contentType: 'application/json; UTF-8',
   data: JSON.stringify({transactionCount : 1,
                        transactionType: "SUBMIT",
                        resourceType: "FORM",
                        resourceSubType: "ADAPTIVE-FORM"}),
   success: successHandler,
   error: faultHandler
})
```

## Relaterade artiklar {#related-articles}

* [Fakturerbara API:er för transaktionsrapporter](/help/forms/transaction-reports-billable-apis.md)

