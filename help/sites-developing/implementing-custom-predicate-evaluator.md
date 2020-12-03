---
title: Implementing a Custom Predicate Evaluator for the Query Builder
seo-title: Implementing a Custom Predicate Evaluator for the Query Builder
description: Query Builder提供了查詢內容儲存庫的簡單方式
seo-description: Query Builder提供了查詢內容儲存庫的簡單方式
uuid: e71be518-027c-4792-9e02-06405804d9d2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ef253905-87da-4fa2-9f6c-778f1b12bd58
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---


# Implementing a Custom Predicate Evaluator for the Query Builder{#implementing-a-custom-predicate-evaluator-for-the-query-builder}

本節說明如何透過實作自訂謂詞評估器來擴充[查詢產生器](/help/sites-developing/querybuilder-api.md)。

## 概覽 {#overview}

[查詢產生器](/help/sites-developing/querybuilder-api.md)提供了查詢內容儲存庫的簡單方法。 CQ隨附一組謂詞評估器，可協助您處理資料。

但是，您可能希望通過實施自定義謂詞求值器來簡化查詢，該求值器隱藏某些複雜性並確保更好的語義。

自定義謂語也可以執行XPath無法直接執行的其他操作，例如：

* 從某些服務中查找一些資料
* 根據計算自訂篩選

>[!NOTE]
>
>實作自訂述詞時，必須考慮效能問題。

>[!NOTE]
>
>您可以在[Query Builder](/help/sites-developing/querybuilder-api.md)區段中找到查詢範例。

GITHUB代碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-search-custom-predicate-evaluator專案](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
* 將專案下載為[a ZIP file](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)

### Predicate Evaluator in Detail {#predicate-evaluator-in-detail}

謂語求值器可處理某些謂語的求值，這些謂語是查詢的定義約束。

它會將較高層級的搜尋限制（例如&quot;width > 200&quot;）對應至符合實際內容模型的特定JCR查詢（例如中繼資料/@width > 200）。 或者，它可以手動過濾節點並檢查其約束。

>[!NOTE]
>
>有關`PredicateEvaluator`和`com.day.cq.search`軟體包的詳細資訊，請參閱[ Java文檔](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/search/package-summary.html)。

### Implementing a Custom Predicate Evaluator for Replication Metadata {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

作為示例，本節介紹如何建立自定義謂詞評估器，該評估器幫助基於複製元資料的資料：

* `cq:lastReplicated` 儲存上次複製操作的日期

* `cq:lastReplicatedBy` 儲存觸發上次複製操作的用戶的ID

* `cq:lastReplicationAction` 儲存上次複製操作（如激活、停用）

#### 使用預設謂詞評估器查詢複製元資料{#querying-replication-metadata-with-default-predicate-evaluators}

以下查詢讀取`/content`分支中自年初開始由`admin`激活的節點清單。

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

此查詢是有效的，但很難讀取，並且不會突出顯示三個複製屬性之間的關係。 實作自訂謂詞評估器將降低查詢的複雜性並改善其語義。

#### 目標{#objectives}

`ReplicationPredicateEvaluator`的目標是使用下列語法支援上述查詢。

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

將複製元資料謂語與自定義謂詞求值器分組有助於建立有意義的查詢。

#### 更新Maven依賴項{#updating-maven-dependencies}

>[!NOTE]
>
>[如何使用Apache Maven](/help/sites-developing/ht-projects-maven.md)建立AEM專案，說明如何使用maven來設定新的AEM專案。

首先，您需要更新專案的Maven相依性。 `PredicateEvaluator`是`cq-search`對象的一部分，因此需要將其添加到Maven pom檔案中。

>[!NOTE]
>
>由於`OSGi`容器將提供`cq-search`，因此`cq-search`相依性的範圍被設定為`provided`。

pom.xml

以下程式碼片段顯示[unified diff format](https://en.wikipedia.org/wiki/Diff#Unified_format)的差異

```
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

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)-  [pom.xml](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/raw/7aed6b35b4c8dd3655296e1b10cf40c0dd1eaa61/pom.xml)

#### 正在寫入ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

`cq-search`項目包含`AbstractPredicateEvaluator`抽象類。 This can be extended with a few steps to implement your own custom predicate evaluator `(PredicateEvaluator`)。

>[!NOTE]
>
>下列程式說明如何建立`Xpath`運算式來篩選資料。 另一個選項是實施`includes`方法，該方法以行為基礎選擇資料。 如需詳細資訊，請參閱[Java檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html#includes28comdaycqsearchpredicatejavaxjcrqueryrowcomdaycqsearchevalevaluationcontext29)。

1. 建立擴展`com.day.cq.search.eval.AbstractPredicateEvaluator`的新Java類
1. 使用`@Component`類似下列的

   src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

   以下程式碼片段顯示[unified diff format](https://en.wikipedia.org/wiki/Diff#Unified_format)的差異

```
@@ -19,8 +19,11 @@
  */
 package com.adobe.aem.docs.search;

+import org.apache.felix.scr.annotations.Component;
+
 import com.day.cq.search.eval.AbstractPredicateEvaluator;

+@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")
 public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

 }
```

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)-  [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/raw/ec70fac35fbd0d132e00c6066a204804e9cbe70f/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)

>[!NOTE]
>
>`factory`必須是以`com.day.cq.search.eval.PredicateEvaluator/`開頭並以自訂`PredicateEvaluator`名稱結尾的唯一字串。

>[!NOTE]
>
>`PredicateEvaluator`的名稱是謂語名稱，用於構建查詢。

1. 覆寫：

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   在override方法中，您根據`Predicate`在引數中給定來建立`Xpath`運算式。

### 複製元資料的自定義謂詞評估器示例{#example-of-a-custom-predicate-evalutor-for-replication-metadata}

此`PredicateEvaluator`的完整實作可能類似於下列類別。

src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

```
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

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)-  [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/blob/master/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)
