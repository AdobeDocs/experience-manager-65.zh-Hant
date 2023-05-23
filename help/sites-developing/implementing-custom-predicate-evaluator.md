---
title: 為查詢生成器實現自定義謂詞計算器
seo-title: Implementing a Custom Predicate Evaluator for the Query Builder
description: Query Builder提供了一種查詢內容儲存庫的簡單方法
seo-description: The Query Builder offers an easy way of querying the content repository
uuid: e71be518-027c-4792-9e02-06405804d9d2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ef253905-87da-4fa2-9f6c-778f1b12bd58
docset: aem65
exl-id: 72cbe589-14a1-40f5-a7cb-8960f02e0ebb
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 0%

---

# 為查詢生成器實現自定義謂詞計算器{#implementing-a-custom-predicate-evaluator-for-the-query-builder}

本節介紹如何擴展 [查詢生成器](/help/sites-developing/querybuilder-api.md) 實現自定義謂詞計算器。

## 概觀 {#overview}

的 [查詢生成器](/help/sites-developing/querybuilder-api.md) 提供了查詢內容儲存庫的簡單方法。 CQ附帶一組謂詞計算器，可幫助您處理資料。

但是，您可能希望通過實施自定義謂詞計算器來簡化查詢，該計算器隱藏了一些複雜性，並確保了更好的語義。

自定義謂語還可以執行XPath不直接可能執行的其他操作，例如：

* 從某些服務中查找一些資料
* 基於計算的自定義過濾

>[!NOTE]
>
>實施自定義謂詞時必須考慮效能問題。

>[!NOTE]
>
>您可以在 [查詢生成器](/help/sites-developing/querybuilder-api.md) 的子菜單。

GITHUB代碼

可以在GitHub上找到此頁的代碼

* [在GitHub上開啟aem-search-custom-predicate-evaluator項目](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
* 將項目下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)

### 詳細謂語計算器 {#predicate-evaluator-in-detail}

謂詞計算器處理某些謂詞的計算，這些謂詞是查詢的定義約束。

它將較高級別的搜索約束（如「寬度> 200」）映射到符合實際內容模型(例如元資料/@width > 200)的特定JCR查詢。 或者可以手動過濾節點並檢查其約束。

>[!NOTE]
>
>有關 `PredicateEvaluator` 和 `com.day.cq.search` 包請參閱 [Java文檔](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/search/package-summary.html)。

### 實現複製元資料的自定義謂詞計算器 {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

作為示例，本節介紹如何建立自定義謂詞計算器，以基於複製元資料幫助資料：

* `cq:lastReplicated` 儲存上次複製操作的日期

* `cq:lastReplicatedBy` 儲存觸發上次複製操作的用戶的ID

* `cq:lastReplicationAction` 儲存上次複製操作（如激活、停用）

#### 使用預設謂詞計算器查詢複製元資料 {#querying-replication-metadata-with-default-predicate-evaluators}

以下查詢將讀取中的節點清單 `/content` 被激活的分支 `admin` 從年初開始。

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

此查詢有效，但難於讀取，不會突出顯示三個複製屬性之間的關係。 實現自定義謂詞計算器將降低查詢的複雜度，提高查詢的語義。

#### 目標 {#objectives}

目標 `ReplicationPredicateEvaluator` 是使用以下語法支援上述查詢。

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

將複製元資料謂詞與自定義謂詞計算器分組有助於建立有意義的查詢。

#### 更新Maven依賴項 {#updating-maven-dependencies}

>[!NOTE]
>
>使用maven設定AEM新項目的記錄由 [如何使用Apache AEM Maven生成項目](/help/sites-developing/ht-projects-maven.md)。

首先，您需要更新項目的Maven依賴項。 的 `PredicateEvaluator` 是 `cq-search` 藏物，所以需要把它添加到你的Maven pom檔案。

>[!NOTE]
>
>範圍 `cq-search` 依賴關係設定為 `provided` 因為 `cq-search` 將由 `OSGi` 容器。

pom.xml

以下代碼段顯示差異，在 [統一差異格式](https://en.wikipedia.org/wiki/Diff#Unified_format)

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

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)- [pom.xml](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/raw/7aed6b35b4c8dd3655296e1b10cf40c0dd1eaa61/pom.xml)

#### 編寫ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

的 `cq-search` 項目包含 `AbstractPredicateEvaluator` 抽象類。 可以通過幾個步驟來擴展此功能，以實現您自己的自定義謂詞計算器 `(PredicateEvaluator`)。

>[!NOTE]
>
>以下過程說明如何生成 `Xpath` 用於篩選資料的表達式。 另一個選擇是實施 `includes` 按行選擇資料的方法。 查看 [Java文檔](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html#includes28comdaycqsearchpredicatejavaxjcrqueryrowcomdaycqsearchevalevaluationcontext29) 的子菜單。

1. 建立新的Java類，該類擴展 `com.day.cq.search.eval.AbstractPredicateEvaluator`
1. 使用 `@Component` 如下

   src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

   以下代碼段顯示差異，在 [統一差異格式](https://en.wikipedia.org/wiki/Diff#Unified_format)

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

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)- [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/raw/ec70fac35fbd0d132e00c6066a204804e9cbe70f/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)

>[!NOTE]
>
>的 `factory`必須是唯一字串，開頭為 `com.day.cq.search.eval.PredicateEvaluator/`以自定義名稱結尾 `PredicateEvaluator`。

>[!NOTE]
>
>名稱 `PredicateEvaluator` 是謂詞名稱，在生成查詢時使用。

1. 覆寫:

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   在覆蓋方法中，生成 `Xpath` 基於 `Predicate` 在論證中給出。

### 複製元資料的自定義謂詞計算器示例 {#example-of-a-custom-predicate-evalutor-for-replication-metadata}

全面實施 `PredicateEvaluator` 可能與以下類類似。

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

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)- [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/blob/master/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)
