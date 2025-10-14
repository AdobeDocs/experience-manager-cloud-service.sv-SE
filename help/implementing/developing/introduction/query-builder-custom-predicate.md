---
title: Implementera en anpassad predikatutvärderare för Query Builder
description: AEM i Query Builder är ett enkelt och anpassningsbart sätt att fråga innehållsdatabasen
exl-id: 8c2f8c22-1851-4313-a1c9-10d6d9b65824
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# Implementera en anpassad predikatutvärderare för Query Builder {#implementing-a-custom-predicate-evaluator-for-the-query-builder}

I det här dokumentet beskrivs hur du utökar [Query Builder](query-builder-api.md) genom att implementera en anpassad predikatutvärderare.

## Ökning {#overview}

[Query Builder](query-builder-api.md) är ett enkelt sätt att fråga innehållsdatabasen. AEM innehåller [en uppsättning predikatutvärderare](#query-builder-predicates.md) som hjälper dig att fråga dina data.

Men du kanske vill förenkla dina frågor genom att implementera en anpassad predikatutvärderare som döljer komplexiteten och ger ett bättre semantiskt resultat.

Ett anpassat predikat kan även utföra andra saker som inte är direkt möjliga med XPath, till exempel:

* Hämta data från en annan tjänst
* Anpassad filtrering baserad på en beräkning

>[!NOTE]
>
>Prestandafrågor måste beaktas när du implementerar ett anpassat predikat.

>[!TIP]
>
>Du kan hitta exempel på frågor i [Query Builder](query-builder-api.md) -dokumentet.

>[!TIP]
>
>Koden för den här sidan finns på GitHub
>
>* [Öppna aem-search-custom-predikate-valuator-projekt på GitHub](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
>* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)

>[!NOTE]
>
>Den här länkade koden på GitHub och kodfragmenten i det här dokumentet tillhandahålls endast i demonstrationssyfte.

### Förutse utvärderaren i detalj {#predicate-evaluator-in-detail}

En predikatutvärderare hanterar utvärderingen av vissa predikat, vilket är definieringsbegränsningarna för en fråga.

Det mappar en sökbegränsning på högre nivå (till exempel `width>200`) till en specifik JCR-fråga som passar den faktiska innehållsmodellen (till exempel `metadata/@width > 200`). Det kan också filtrera noder manuellt och kontrollera deras begränsningar.

>[!TIP]
>
>Mer information om `PredicateEvaluator` och `com.day.cq.search`-paketet finns i [Java-dokumentationen](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html?com/day/cq/search/package-summary.html).

### Implementera en anpassad predikatutvärderare för replikeringsmetadata {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

I det här avsnittet beskrivs hur du skapar en anpassad predikatutvärderare som kan användas för data baserat på replikeringens metadata:

* `cq:lastReplicated` som lagrar datumet för den senaste replikeringsåtgärden
* `cq:lastReplicatedBy` som lagrar ID:t för användaren som utlöste den senaste replikeringsåtgärden
* `cq:lastReplicationAction` som lagrar den senaste replikeringsåtgärden (till exempel Aktivering, Inaktivering)

#### Frågar efter replikeringsmetadata med standardpredikatutvärderare {#querying-replication-metadata-with-default-predicate-evaluators}

Följande fråga hämtar listan med noder i grenen `/content` som har aktiverats av `admin` sedan årets början.

```xml
path=/content

1_property=cq:lastReplicatedBy
1_property.value=admin

2_property=cq:lastReplicationAction
2_property.value=Activate

daterange.property=cq:lastReplicated
daterange.lowerBound=2013-01-01T00:00:00.000+01:00
daterange.lowerOperation=>=
```

Frågan är giltig men svårläst och visar inte relationen mellan de tre replikeringsegenskaperna. Implementering av en anpassad predikatutvärderare minskar komplexiteten och förbättrar semantiken i frågan.

#### Mål {#objectives}

Målet för `ReplicationPredicateEvaluator` är att stöda ovanstående fråga med följande syntax.

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

Genom att gruppera metadata för replikering med en anpassad predikatutvärderare kan du skapa en meningsfull fråga.

#### Uppdaterar Maven Dependencies {#updating-maven-dependencies}

>[!TIP]
>
>Inställningen av nya AEM, inklusive att använda maven, förklaras i detalj i [WKND-självstudiekursen](develop-wknd-tutorial.md).

Först måste du uppdatera Maven-beroendena för ditt projekt. `PredicateEvaluator` är en del av `cq-search`-artefakten, så den måste läggas till i din Maven-pom-fil.

>[!NOTE]
>
>Omfånget för `cq-search`-beroendet är inställt på `provided` eftersom `cq-search` tillhandahålls av `OSGi`-behållaren.

Följande utdrag visar skillnaderna i filen `pom.xml` i formatet [unified diff](https://en.wikipedia.org/wiki/Diff#Unified_format)

```text
@@ -120,6 +120,12 @@
             <scope>provided</scope>
         <dependency>
+            <groupid>com.day.cq</groupid>
+            <artifactid>cq-search</artifactid>
+            <version>5.6.4</version>
+            <scope>provided</scope>
+        </dependency>
+        <dependency>
             <groupid>junit</groupid>
             <artifactid>junit</artifactid>
             <version>3.8.1</version></dependency>
```

#### Skriver ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

Projektet `cq-search` innehåller den abstrakta klassen `AbstractPredicateEvaluator`. Detta kan utökas med några steg för att implementera din egen anpassade predikatutvärderare `(PredicateEvaluator`).

>[!NOTE]
>
>I proceduren nedan beskrivs hur du skapar ett `Xpath`-uttryck för att filtrera data. Ett annat alternativ är att implementera metoden `includes` som markerar data på radbasis. Mer information finns i [Java-dokumentationen](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html).

1. Skapa en ny Java-klass som utökar `com.day.cq.search.eval.AbstractPredicateEvaluator`
1. Anteckna din klass med ett `@Component`-liknande utdrag som visas i [enhetligt format &#x200B;](https://en.wikipedia.org/wiki/Diff#Unified_format)

   ```text
   @@ -19,8 +19,11 @@
     */
    package com.adobe.aem.docs.search;
   
   +import org.apache.felix.scr.annotations.Component;
   +import com.day.cq.search.eval.AbstractPredicateEvaluator;
   
   +@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")
    public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {
   
    }
   ```

   >[!NOTE]
   >
   >`factory` måste vara en unik sträng som börjar med `com.day.cq.search.eval.PredicateEvaluator/` och slutar med namnet på din anpassade `PredicateEvaluator`.

   >[!NOTE]
   >
   >Namnet på `PredicateEvaluator` är predikatnamnet, som används när frågor skapas.

1. Åsidosätt:

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   I åsidosättningsmetoden skapar du ett `Xpath`-uttryck baserat på det `Predicate` som anges i argumentet.

### Exempel på en anpassad predikatutvärderare för replikeringsmetadata {#example-of-a-custom-predicate-evaluator-for-replication-metadata}

Den fullständiga implementeringen av `PredicateEvaluator` kan likna följande klass.

```java
/*
 * #%L
 * aem-docs-custom-predicate-evaluator
 * %%
 * Copyright (C) 2013 Adobe Research
 * %%
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 * #L%
 */

package com.adobe.aem.docs.search;

import org.apache.felix.scr.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.search.Predicate;
import com.day.cq.search.eval.AbstractPredicateEvaluator;
import com.day.cq.search.eval.EvaluationContext;

@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")

public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

    static final String PE_NAME = "replic";


    static final String PN_LAST_REPLICATED_BY = "cq:lastReplicatedBy";
    static final String PN_LAST_REPLICATED = "cq:lastReplicated";
    static final String PN_LAST_REPLICATED_ACTION = "cq:lastReplicationAction";

    static final String PREDICATE_BY = "by";
    static final String PREDICATE_SINCE = "since";
    static final String PREDICATE_SINCE_OP = " >= ";
    static final String PREDICATE_ACTION = "action";

    Logger log = LoggerFactory.getLogger(getClass());

    /**
     * Returns a XPath expression filtering by replication metadata.
     *
     * @see com.day.cq.search.eval.AbstractPredicateEvaluator#getXPathExpression(com.day.cq.search.Predicate,
     *      com.day.cq.search.eval.EvaluationContext)
     */

    @Override

    public String getXPathExpression(Predicate predicate,
            EvaluationContext context) {

        log.debug("predicate {}", predicate);

        String date = predicate.get(PREDICATE_SINCE);
        String user = predicate.get(PREDICATE_BY);
        String action = predicate.get(PREDICATE_ACTION);

        StringBuilder sb = new StringBuilder();

        if (date != null) {

            sb.append(PN_LAST_REPLICATED).append(PREDICATE_SINCE_OP);
            sb.append("xs:dateTime('").append(date).append("')");

        }

        if (user != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_BY);
            sb.append("='").append(user).append("'");

        }

        if (action != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_ACTION);
            sb.append("='").append(action).append("'");

        }

        String xpath = sb.toString();

        log.debug("xpath **{}**", xpath);

        return xpath;

    }

    /**
     * Add an and operator if the builder is not empty.
     *
     * @param sb a {@link StringBuilder} containing the query under construction
     */

    private void addAndOperator(StringBuilder sb) {

        if (sb.length() != 0) {

            sb.append(" and ");

        }

    }

}
```
