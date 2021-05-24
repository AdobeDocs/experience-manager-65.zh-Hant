---
title: 為查詢產生器實作自訂述詞求值器
seo-title: 為查詢產生器實作自訂述詞求值器
description: 「查詢產生器」提供了查詢內容存放庫的簡單方式
seo-description: 「查詢產生器」提供了查詢內容存放庫的簡單方式
uuid: e71be518-027c-4792-9e02-06405804d9d2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ef253905-87da-4fa2-9f6c-778f1b12bd58
docset: aem65
exl-id: 72cbe589-14a1-40f5-a7cb-8960f02e0ebb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---

# 為查詢產生器{#implementing-a-custom-predicate-evaluator-for-the-query-builder}實作自訂述詞求值器

本節說明如何實作自訂述詞求值器，以擴充[查詢產生器](/help/sites-developing/querybuilder-api.md)。

## 概覽 {#overview}

[查詢產生器](/help/sites-developing/querybuilder-api.md)提供了查詢內容存放庫的簡單方式。 CQ隨附一組可協助您處理資料的謂語評估器。

不過，您可能想要實作自訂述詞求值器來簡化查詢，該求值器會隱藏一些複雜性，並確保提供更好的語義。

自訂述詞也可以執行XPath不直接可能的其他操作，例如：

* 從某些服務中查找一些資料
* 根據計算自訂篩選

>[!NOTE]
>
>實作自訂述詞時，必須考量效能問題。

>[!NOTE]
>
>您可以在[查詢產生器](/help/sites-developing/querybuilder-api.md)區段中找到查詢範例。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-search-custom-predicate-evaluator專案](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
* 將專案下載為[a ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)

### 詳細資訊{#predicate-evaluator-in-detail}中的謂語求值器

謂語求值器處理某些謂語的求值，這些謂語是查詢的定義約束。

它會將較高層級的搜尋限制（例如「寬度> 200」）對應至符合實際內容模型(例如中繼資料/@width > 200)的特定JCR查詢。 或者，它可以手動篩選節點並檢查其限制。

>[!NOTE]
>
>有關`PredicateEvaluator`和`com.day.cq.search`包的詳細資訊，請參閱[Java文檔](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/search/package-summary.html)。

### 為複製元資料{#implementing-a-custom-predicate-evaluator-for-replication-metadata}實作自訂述詞求值器

例如，本節說明如何建立自訂述詞求值器，以根據復寫中繼資料來協助資料：

* `cq:lastReplicated` 儲存上次復寫動作的日期

* `cq:lastReplicatedBy` 會儲存觸發上次復寫動作之使用者的id

* `cq:lastReplicationAction` 儲存上次復寫動作（例如「啟用」、「停用」）

#### 使用預設謂詞求值器{#querying-replication-metadata-with-default-predicate-evaluators}查詢複製元資料

以下查詢將讀取自年初起由`admin`激活的`/content`分支中的節點清單。

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

此查詢有效，但難以讀取，並且未突出顯示三個複製屬性之間的關係。 實作自訂謂語求值器可降低此查詢的複雜度並改善其語義。

#### 目標 {#objectives}

`ReplicationPredicateEvaluator`的目標是使用下列語法支援上述查詢。

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

使用自訂述詞求值器將復寫中繼資料述詞分組，有助於建立有意義的查詢。

#### 更新Maven依賴項{#updating-maven-dependencies}

>[!NOTE]
>
>[如何使用Apache Maven](/help/sites-developing/ht-projects-maven.md)建立AEM專案，以記錄使用maven的新AEM專案的設定。

首先，您需要更新專案的Maven相依性。 `PredicateEvaluator`是`cq-search`工件的一部分，因此需要將其添加到Maven pom檔案中。

>[!NOTE]
>
>`cq-search`相依性的範圍設為`provided`，因為`cq-search`將由`OSGi`容器提供。

pom.xml

以下代碼段以[統一差異格式](https://en.wikipedia.org/wiki/Diff#Unified_format)顯示差異

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

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator) -  [pom.xml](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/raw/7aed6b35b4c8dd3655296e1b10cf40c0dd1eaa61/pom.xml)

#### 編寫ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

`cq-search`項目包含`AbstractPredicateEvaluator`抽象類。 可透過幾個步驟來擴充，以實作您自己的自訂述詞求值器`(PredicateEvaluator`)。

>[!NOTE]
>
>以下過程說明如何構建`Xpath`表達式以篩選資料。 另一個選項是實作`includes`方法，以依列選取資料。 如需詳細資訊，請參閱[Java檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html#includes28comdaycqsearchpredicatejavaxjcrqueryrowcomdaycqsearchevalevaluationcontext29)。

1. 建立擴展`com.day.cq.search.eval.AbstractPredicateEvaluator`的新Java類
1. 使用`@Component`為類加上注釋，如下所示

   src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

   以下代碼段以[統一差異格式](https://en.wikipedia.org/wiki/Diff#Unified_format)顯示差異

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

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator) -  [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/raw/ec70fac35fbd0d132e00c6066a204804e9cbe70f/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)

>[!NOTE]
>
>`factory`必須是以`com.day.cq.search.eval.PredicateEvaluator/`開頭並以自訂`PredicateEvaluator`名稱結尾的唯一字串。

>[!NOTE]
>
>`PredicateEvaluator`的名稱是謂語名稱，用於建立查詢。

1. 覆寫:

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   在覆寫方法中，您根據引數中提供的`Predicate`建立`Xpath`運算式。

### 復寫中繼資料的自訂謂語求值器範例{#example-of-a-custom-predicate-evalutor-for-replication-metadata}

此`PredicateEvaluator`的完整實施可能類似於以下類別。

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

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator) -  [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/blob/master/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)
