---
title: 使用API列出網頁上的表格
seo-title: 使用API列出網頁上的表格
description: 以程式設計方式查詢Forms Manager，以擷取已篩選的表單清單並顯示在您自己的網頁上。
seo-description: 以程式設計方式查詢Forms Manager，以擷取已篩選的表單清單並顯示在您自己的網頁上。
uuid: e51cb2d4-816f-4e6d-a081-51e4999b00ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 515ceaf6-c132-4e1a-b3c6-5d2c1ccffa7c
translation-type: tm+mt
source-git-commit: db69c393fc44ca2fcb30f9fcb0c5ca456ba35ed5

---


# 使用API列出網頁上的表格 {#listing-forms-on-a-web-page-using-apis}

AEM Forms提供以REST為基礎的搜尋API，讓網頁開發人員可用來查詢和擷取符合搜尋准則的一組表單。 您可以使用API根據各種篩選條件來搜尋表單。 回應物件包含表單屬性、屬性和轉譯表單端點。

若要使用REST API搜尋表單，請使用下列所述的查詢參數，傳送GET `https://[server]:[port]/libs/fd/fm/content/manage.json` 要求至伺服器。

## Query parameters {#query-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>屬性名稱<br /> </strong></td>
   <td><strong>說明<br /> </strong></td>
  </tr>
  <tr>
   <td>函式<br /> </td>
   <td><p>指定要調用的函式。 要搜索表單，請將屬性的 <code>func </code>值設定為 <code>searchForms</code>。</p> <p>例如， <code class="code">
       URLParameterBuilder entityBuilder=new URLParameterBuilder ();
       entityBuilder.add("func", "searchForms");</code></p> <p><strong></strong> 注意：此參 <em>數為必填參數。</em><br /> </p> </td>
  </tr>
  <tr>
   <td>appPath<br /> </td>
   <td><p>指定用於搜索表單的應用程式路徑。 依預設，appPath屬性會搜尋根節點層級上所有可用的應用程式。<br /> </p> <p>您可以在單一搜尋查詢中指定多個應用程式路徑。 使用垂直號(|)字元分隔多個路徑。 </p> </td>
  </tr>
  <tr>
   <td>cutPoints<br /> </td>
   <td><p>指定要隨資產擷取的屬性。 您可以使用星號(*)一次擷取所有屬性。 使用垂直號(|)運算子指定多個屬性。 </p> <p>例如， <code>cutPoints=propertyName1|propertyName2|propertyName3</code></p> <p><strong>注意</strong>: </p>
    <ul>
     <li><em>一律會擷取ID、路徑和名稱等屬性。 </em></li>
     <li><em>每個資產都有不同的屬性集。 屬性（例如formUrl、pdfUrl和guideUrl）並不取決於切割點屬性。 這些屬性取決於資產類型，並據以提取。 </em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>關係<br /> </td>
   <td>指定要讀取的相關資產以及搜尋結果。 您可以選擇下列其中一個選項來擷取相關資產：
    <ul>
     <li><strong>NO_RELATION</strong>:請勿擷取相關資產。</li>
     <li><strong>立即</strong>:擷取與搜尋結果直接相關的資產。</li>
     <li><strong>全部</strong>:直接及間接相關資產。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>maxSize</td>
   <td>指定要讀取的表單數上限。</td>
  </tr>
  <tr>
   <td>偏移</td>
   <td>指定要從開始跳過的表單數。</td>
  </tr>
  <tr>
   <td>returnCount</td>
   <td>指定是否返回與給定條件匹配的搜索結果。 </td>
  </tr>
  <tr>
   <td>語句</td>
   <td><p>指定語句清單。 查詢會在JSON格式中指定的語句清單上執行。 </p> <p>例如，</p> <p><code class="code">JSONArray statementArray=new JSONArray();
       JSONObject statement=new JSONObject();
       statement.put("name", "title");
       statement.put("value", "SimpleSurveyAF");
       statement.put("operator", "EQ"); statementArray.put(statement);</code></p> <p>在上述範例中， </p>
    <ul>
     <li><strong>名稱</strong>:指定要搜索的屬性的名稱。</li>
     <li><strong>值</strong>:指定要搜索的屬性的值。</li>
     <li><strong>運算元</strong>:指定在搜索時應用的運算子。 支援下列運算子：
      <ul>
       <li>EQ —— 等於 </li>
       <li>NEQ —— 不等於</li>
       <li>GT —— 大於</li>
       <li>LT —— 小於</li>
       <li>GTEQ —— 大於或等於</li>
       <li>LTEQ —— 小於或等於</li>
       <li>CONTAINS - a包含B（如果B是A的一部分）</li>
       <li>FULLTEXT —— 全文搜尋</li>
       <li>STARTSWITH —— 如果B是A的開頭部分，則A以B開頭</li>
       <li>ENDSWITH —— 如果B是A的結尾部分，則A以B結尾</li>
       <li>LIKE —— 實作LIKE運算子</li>
       <li>AND —— 合併多個陳述式</li>
      </ul> <p><strong></strong> 注意： <em>GT、LT、GTEQ和LTEQ算子適用於線性類型的屬性，如LONG、DOUBLE和DATE。</em></p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>排序<br /> </td>
   <td><p>指定搜尋結果的順序標準。 標準以JSON格式定義。 您可以對多個欄位的搜尋結果排序。 結果按欄位在查詢中顯示的順序排序。</p> <p>例如，</p> <p>要檢索按標題屬性按升序排序的查詢結果，請添加以下參數： </p> <p><code class="code">JSONArray orderingsArray=new JSONArray();
       JSONObject orderings=new JSONObject();
       orderings.put("name", "title");
       orderings.put("criteria", "ASC");
       orderingsArray.put(orderings);
       entityBuilder.add("orderings", orderingsArray.toString());</code></p>
    <ul>
     <li><strong>名稱</strong>:指定用於排序搜索結果的屬性的名稱。</li>
     <li><strong>准則</strong>:指定結果的順序。 order屬性接受以下值：
      <ul>
       <li>ASC —— 使用ASC以升序排列結果。<br /> </li>
       <li>DES —— 使用DES以降序排列結果。</li>
      </ul> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>includeXdp</td>
   <td>指定是否檢索二進位內容。 該 <code>includeXdp</code> 屬性適用於類型、 <code>FORM</code>和 <code>PDFFORM</code>的資產 <code>PRINTFORM</code>。</td>
  </tr>
  <tr>
   <td>assetType</td>
   <td>指定要從所有已發佈資產擷取的資產類型。 使用垂直號(|)運算子指定多個資產類型。 有效的資產類型包括FORM、PDFFORM、PRINTFORM、RESOURCE和GUIDE。</td>
  </tr>
 </tbody>
</table>

## 請求範例 {#sample-request}

```
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
orderings:[{"name" :“lastModifiedDate“:”order”:”ASC”}]
```

## 範例回應 {#sample-response}

```
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

* [啟用表單入口元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單入口網頁](/help/forms/using/creating-form-portal-page.md)
* [使用API在網頁上列出表格](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自訂草稿和提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自訂表單入口元件的範本](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站上發佈表格簡介](/help/forms/using/introduction-publishing-forms.md)