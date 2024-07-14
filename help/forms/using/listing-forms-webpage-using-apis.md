---
title: 使用API在網頁上列出表單
description: 以程式設計方式查詢Forms Manager以擷取經過篩選的表單清單，並在您自己的網頁上顯示。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
exl-id: cfca6656-d2db-476d-a734-7a1d1e44894e
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---

# 使用API在網頁上列出表單 {#listing-forms-on-a-web-page-using-apis}

AEM Forms提供REST型搜尋API，網頁開發人員可透過此API查詢及擷取符合搜尋條件的一組表單。 您可以使用API來根據各種篩選器搜尋表單。 回應物件包含表單屬性、屬性和轉譯器表單端點。

若要使用REST API搜尋表單，請使用下述查詢引數將GET要求傳送至位於`https://'[server]:[port]'/libs/fd/fm/content/manage.json`的伺服器。

## 查詢引數 {#query-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>屬性名稱<br /> </strong></td>
   <td><strong>說明<br /> </strong></td>
  </tr>
  <tr>
   <td>func<br /> </td>
   <td><p>指定要呼叫的函式。 若要搜尋表單，請將<code>func </code>屬性的值設定為<code>searchForms</code>。</p> <p>例如， <code class="code">
       URLParameterBuilder entityBuilder=new URLParameterBuilder ();
       entityBuilder.add("func", "searchForms");</code></p> <p><strong>注意：</strong> <em>此引數為必要引數。</em><br /> </p> </td>
  </tr>
  <tr>
   <td>appPath<br /> </td>
   <td><p>指定要搜尋表單的應用程式路徑。 依預設，appPath屬性會搜尋根節點層級的所有可用應用程式。<br /> </p> <p>您可以在單一搜尋查詢中指定多個應用程式路徑。 請使用垂直號(|)分隔多個路徑。 </p> </td>
  </tr>
  <tr>
   <td>剪下點<br /> </td>
   <td><p>指定要與資產一起擷取的屬性。 您可以使用星號(*)一次擷取所有屬性。 使用垂直號(|)運運算元指定多個屬性。 </p> <p>例如， <code>cutPoints=propertyName1|propertyName2|propertyName3</code></p> <p><strong>附註</strong>： </p>
    <ul>
     <li><em>系統一律會擷取ID、路徑和名稱等屬性。 </em></li>
     <li><em>每個資產都有不同的屬性集。 formUrl、pdfUrl和guideUrl等屬性不依賴於cutpoints屬性。 這些屬性視資產型別而定，系統會據以擷取。 </em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>關聯<br /> </td>
   <td>指定要與搜尋結果一起擷取的相關資產。 您可以選擇下列其中一個選項來擷取相關資產：
    <ul>
     <li><strong>NO_RELATION</strong>：不擷取相關資產。</li>
     <li><strong>IMMEDIATE</strong>：擷取與搜尋結果直接相關的資產。</li>
     <li><strong>ALL</strong>：擷取直接和間接相關的資產。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>maxSize</td>
   <td>指定要擷取的表單數上限。</td>
  </tr>
  <tr>
   <td>offset</td>
   <td>指定從開始起要略過的表單數目。</td>
  </tr>
  <tr>
   <td>returnCount</td>
   <td>指定是否傳回符合指定條件的搜尋結果。 </td>
  </tr>
  <tr>
   <td>陳述式</td>
   <td><p>指定陳述式清單。 查詢會在以JSON格式指定的陳述式清單上執行。 </p> <p>例如，</p> <p><code class="code">JSONArray statementArray=new JSONArray();
       JSONObject statement=new JSONObject();
       statement.put("name", "title");
       statement.put("value", "SimpleSurveyAF");
       statement.put("operator", "EQ"); statementArray.put(statement);</code></p> <p>在上述範例中， </p>
    <ul>
     <li><strong>name</strong>：指定要搜尋的屬性名稱。</li>
     <li><strong>value</strong>：指定要搜尋的屬性值。</li>
     <li><strong>運運算元</strong>：指定搜尋時要套用的運運算元。 支援下列運運算元：
      <ul>
       <li>EQ — 等於 </li>
       <li>NEQ — 不等於</li>
       <li>GT — 大於</li>
       <li>LT — 小於</li>
       <li>GTEQ — 大於或等於</li>
       <li>LTEQ — 小於或等於</li>
       <li>CONTAINS - A包含B，如果B是A的一部分</li>
       <li>全文 — 全文搜尋</li>
       <li>STARTSTWITH — 如果B是A的開頭部分，則A以B開頭</li>
       <li>ENDSWITH — 如果B是A的結尾部分，則A結尾為B</li>
       <li>LIKE — 實作LIKE運運算元</li>
       <li>AND — 合併多個陳述式</li>
      </ul> <p><strong>注意：</strong> <em>GT、LT、GTEQ和LTEQ運運算元適用於線性型別的屬性，例如LONG、DOUBLE和DATE。</em></p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>訂購<br /> </td>
   <td><p>指定搜尋結果的順序條件。 條件會以JSON格式定義。 您可以在多個欄位上排序搜尋結果。 結果會依查詢中欄位的出現順序排序。</p> <p>例如，</p> <p>若要擷取依標題屬性遞增順序排序的查詢結果，請新增下列引數： </p> <p><code class="code">JSONArray orderingsArray=new JSONArray();
       JSONObject orderings=new JSONObject();
       orderings.put("name", "title");
       orderings.put("criteria", "ASC");
       orderingsArray.put(orderings);
       entityBuilder.add("orderings", orderingsArray.toString());</code></p>
    <ul>
     <li><strong>name</strong>：指定要用來排序搜尋結果的屬性名稱。</li>
     <li><strong>criteria</strong>：指定結果的順序。 order屬性接受下列值：
      <ul>
       <li>ASC — 使用ASC以遞增順序排列結果。<br /> </li>
       <li>DES — 使用DES以遞減順序排列結果。</li>
      </ul> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>includeXdp</td>
   <td>指定是否要擷取二進位內容。 <code>includeXdp</code>屬性適用於<code>FORM</code>、<code>PDFFORM</code>和<code>PRINTFORM</code>型別的資產。</td>
  </tr>
  <tr>
   <td>assetType</td>
   <td>指定要從所有發佈的資產中擷取的資產型別。 使用垂直號(|)運運算元可指定多種資產型別。 有效的資產型別為FORM、PDF表單、PRINTFORM、RESOURCE和GUIDE。</td>
  </tr>
 </tbody>
</table>

## 範例要求 {#sample-request}

```json
func : searchForms
appPath : /content/dam/formsanddocuments/MyApplication23
cutPoints : title|description|author|status|creationDate|lastModifiedDate|activationDate|expiryDate|tags|allowedRenderFormat|formmodel
relation : NO_RELATION
includeXdp : false
maxSize : 10
offset : 0
returnCount : true
statements: [{"name":"name","value":"*Claim.xdp","operator":"CONTAINS"},
                {"name":"","value":"Expense","operator":"FULLTEXT"},
                {"name":"description","value":"ABCD*","operator":"CONTAINS"},
                {"name":"status","value":"false","operator":"EQ"},
                {"name":"lastModifiedDate","value":"01/09/2013","operator":"GTEQ"},
                {"name":"lastModifiedDate","value":"01/18/2013","operator":"LTEQ"}]
orderings:[{"name" :"lastModifiedDate":"order":"ASC"}]
```

## 範例回應 {#sample-response}

```json
[
{"resultCount":2},
    {"assetType":"FORM","name":"ExpenseClaim.xdp","id":"509fa2d5-e3c9-407b-b8dc-fa0ba08eb0ce",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDEFGIJK","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"5477a127-8bbf-4cec-8f81-2689e5cb4a15",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/Image.gif","resourceSize":0}],
       "status":false,"creationDate":1358429845623,"lastModifiedDate":1358429846771},
{"assetType":"FORM","name":"ExpenseClaim.xdp","id":"4312239b-b666-4d36-95bc-641b3a39ddd4",
       "path":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDefghijklm","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"118a2e3f-7097-4d8c-85d1-651306de284a",
       "path":"/content/dam/formsanddocuments/MyApplication23/Image.gif","resourceSize":0}],"status":false,
       "creationDate":1358429856690,"lastModifiedDate":1358430109023}
]
```

## 相關文章

* [啟用表單入口網站元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單入口網站頁面](/help/forms/using/creating-form-portal-page.md)
* [使用API的網頁上列出表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自訂草稿和已提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md)
* [自訂Forms Portal元件的範本](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站上發佈表單簡介](/help/forms/using/introduction-publishing-forms.md)
