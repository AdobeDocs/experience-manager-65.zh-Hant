---
title: 為查詢產生器實作自訂述詞求值器
description: 查詢產生器提供查詢內容存放庫的簡單方式
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 72cbe589-14a1-40f5-a7cb-8960f02e0ebb
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# 為查詢產生器實作自訂述詞求值器{#implementing-a-custom-predicate-evaluator-for-the-query-builder}

本節說明如何延伸 [查詢產生器](/help/sites-developing/querybuilder-api.md) 實作自訂述詞求值器。

## 概觀 {#overview}

此 [查詢產生器](/help/sites-developing/querybuilder-api.md) 提供查詢內容存放庫的簡單方法。 CQ隨附一組述詞評估器，可協助您處理資料。

不過，您可能想要實作自訂述詞評估器來簡化查詢，該評估器會隱藏一些複雜度並確保更好的語意。

自訂述詞也可以執行其他不直接與XPath一起執行的動作，例如：

* 從某些服務查詢某些資料
* 根據計算的自訂篩選

>[!NOTE]
>
>實作自訂述詞時必須考慮效能問題。

>[!NOTE]
>
>您可在以下網址找到查詢範例： [查詢產生器](/help/sites-developing/querybuilder-api.md) 區段。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼。

* [在GitHub上開啟aem-search-custom-predicate-evaluator專案](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)

### 述詞求值器詳細資料 {#predicate-evaluator-in-detail}

述詞評估器處理特定述詞的評估，這些述詞是查詢的定義限制。

這會將較高層級的搜尋限制（例如「寬度> 200」）對應至符合實際內容模型的特定JCR查詢(例如，中繼資料/@width度> 200)。 或者，它可以手動篩選節點並檢查其限制。

>[!NOTE]
>
>如需關於的詳細資訊 `PredicateEvaluator` 和 `com.day.cq.search` 封裝，請參閱 [Java™檔案](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/search/package-summary.html).

### 實施復寫中繼資料的自訂述詞求值器 {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

本節以範例說明如何建立自訂述詞評估器，協助根據復寫中繼資料的資料：

* `cq:lastReplicated` 儲存上次復寫動作的日期

* `cq:lastReplicatedBy` 會儲存觸發上次復寫動作之使用者的id

* `cq:lastReplicationAction` 儲存上次的復寫動作（例如啟用、停用）

#### 使用預設述詞評估器查詢復寫中繼資料 {#querying-replication-metadata-with-default-predicate-evaluators}

以下查詢會擷取下列位置的節點清單： `/content` 已由啟用的分支 `admin` 從年初開始。

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

此查詢有效，但難以讀取，且不會強調三個復寫屬性之間的關係。 實作自訂述詞求值器可降低複雜性並改善此查詢的語意。

#### 目標 {#objectives}

的目標 `ReplicationPredicateEvaluator` 是使用下列語法支援上述查詢。

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

使用自訂述詞求值器將復寫中繼資料述詞分組，有助於建立有意義的查詢。

#### 更新Maven相依性 {#updating-maven-dependencies}

>[!NOTE]
>
>以下說明使用maven設定新Adobe Experience Manager (AEM)專案的說明檔案： [如何使用Apache Maven建置AEM專案](/help/sites-developing/ht-projects-maven.md).

首先，更新專案的Maven相依性。 此 `PredicateEvaluator` 是 `cq-search` 成品，因此必須將其新增至您的Maven pom.xml檔案。

>[!NOTE]
>
>範圍 `cq-search` 相依性已設定為 `provided` 因為 `cq-search` 由 `OSGi` 容器。

pom.xml

下列程式碼片段顯示 [統一的差異格式](https://en.wikipedia.org/wiki/Diff#Unified_format)

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

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator) - [pom.xml](https://raw.githubusercontent.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/7aed6b35b4c8dd3655296e1b10cf40c0dd1eaa61/pom.xml)

#### 正在寫入ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

此 `cq-search` 專案包含 `AbstractPredicateEvaluator` 抽象類別。 您只需幾個步驟即可擴充此功能，以實作您自己的自訂述詞評估器 `(PredicateEvaluator`)。

>[!NOTE]
>
>下列程式說明如何建置 `Xpath` 篩選資料的運算式。 另一個選項是實作 `includes` 以列為基礎選取資料的方法。 請參閱 [Java™檔案](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/search/eval/PredicateEvaluator.html#includes28comdaycqsearchpredicatejavaxjcrqueryrowcomdaycqsearchevalevaluationcontext29) 以取得詳細資訊。

1. 建立可擴充的Java™類別 `com.day.cq.search.eval.AbstractPredicateEvaluator`
1. 使用為課程加上註釋 `@Component` 如以下所示

   src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

   下列程式碼片段顯示 [統一的差異格式](https://en.wikipedia.org/wiki/Diff#Unified_format)

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

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator) - [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://raw.githubusercontent.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/ec70fac35fbd0d132e00c6066a204804e9cbe70f/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)

>[!NOTE]
>
>此 `factory`必須是唯一的字串，開頭為 `com.day.cq.search.eval.PredicateEvaluator/`結尾為您的自訂名稱 `PredicateEvaluator`.

>[!NOTE]
>
>的名稱 `PredicateEvaluator` 是建立查詢時使用的述詞名稱。

1. 覆寫：

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   在覆寫方法中，您建置 `Xpath` 運算式基礎為 `Predicate` 在引數中給出。

### 復寫中繼資料的自訂述詞求值器範例 {#example-of-a-custom-predicate-evalutor-for-replication-metadata}

此專案的完整實作 `PredicateEvaluator` 可能與以下類別類似。

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
 *      https://www.apache.org/licenses/LICENSE-2.0
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

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator) - [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/blob/master/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)
