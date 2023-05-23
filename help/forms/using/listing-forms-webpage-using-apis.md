---
title: 使用API在網頁上列出表單
seo-title: Listing forms on a web page using APIs
description: 以寫程式方式查詢Forms管理器以檢索已篩選的表單清單並在您自己的網頁上顯示。
seo-description: Programmatically query Forms Manager to retrieve a filtered list of forms and display on your own web pages.
uuid: e51cb2d4-816f-4e6d-a081-51e4999b00ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 515ceaf6-c132-4e1a-b3c6-5d2c1ccffa7c
exl-id: cfca6656-d2db-476d-a734-7a1d1e44894e
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 1%

---

# 使用API在網頁上列出表單 {#listing-forms-on-a-web-page-using-apis}

AEM Forms提供了基於REST的搜索API,Web開發人員可以使用該API查詢和檢索符合搜索標準的一組表單。 您可以使用API根據各種篩選器搜索表單。 響應對象包含表單屬性、屬性和呈現表單的端點。

要使用REST API搜索表單，請向伺服器發送GET請求，地址為 `https://'[server]:[port]'/libs/fd/fm/content/manage.json` 查詢參數。

## 查詢參數 {#query-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>屬性名稱<br /> </strong></td>
   <td><strong>說明<br /> </strong></td>
  </tr>
  <tr>
   <td>函式<br /> </td>
   <td><p>指定要調用的函式。 要搜索表單，請設定 <code>func </code>屬性 <code>searchForms</code>。</p> <p>例如， <code class="code">
       URLParameterBuilder entityBuilder=new URLParameterBuilder ();
       entityBuilder.add("func", "searchForms");</code></p> <p><strong>注：</strong> <em>此參數是必需的。</em><br /> </p> </td>
  </tr>
  <tr>
   <td>應用路徑<br /> </td>
   <td><p>指定搜索表單的應用程式路徑。 預設情況下，appPath屬性將搜索根節點級別上可用的所有應用程式。<br /> </p> <p>可以在單個搜索查詢中指定多個應用程式路徑。 使用管道(|)字元分隔多條路徑。 </p> </td>
  </tr>
  <tr>
   <td>剪切點<br /> </td>
   <td><p>指定要使用資產提取的屬性。 可以使用星號(*)一次獲取所有屬性。 使用管道(|)運算子指定多個屬性。 </p> <p>例如， <code>cutPoints=propertyName1|propertyName2|propertyName3</code></p> <p><strong>注意</strong>: </p>
    <ul>
     <li><em>始終讀取id、路徑和名稱等屬性。 </em></li>
     <li><em>每個資產都有不同的屬性集。 formUrl、pdfUrl和guideUrl等屬性不依賴於刀口屬性。 這些屬性取決於資產類型，並會相應讀取。 </em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>關係<br /> </td>
   <td>指定要隨搜索結果一起提取的相關資產。 您可以選擇以下選項之一來獲取相關資產：
    <ul>
     <li><strong>無關係(_R)</strong>:不提取相關資產。</li>
     <li><strong>立即</strong>:提取與搜索結果直接相關的資產。</li>
     <li><strong>全部</strong>:獲取直接和間接相關資產。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>最大大小</td>
   <td>指定要提取的最大表單數。</td>
  </tr>
  <tr>
   <td>偏移</td>
   <td>指定要從開始跳過的表單數。</td>
  </tr>
  <tr>
   <td>返回計數</td>
   <td>指定是否返回與給定條件匹配的搜索結果。 </td>
  </tr>
  <tr>
   <td>聲明</td>
   <td><p>指定語句清單。 查詢在JSON格式指定的語句清單上執行。 </p> <p>例如，</p> <p><code class="code">JSONArray statementArray=new JSONArray();
       JSONObject statement=new JSONObject();
       statement.put("name", "title");
       statement.put("value", "SimpleSurveyAF");
       statement.put("operator", "EQ"); statementArray.put(statement);</code></p> <p>在上例中， </p>
    <ul>
     <li><strong>名稱</strong>:指定要搜索的屬性的名稱。</li>
     <li><strong>值</strong>:指定要搜索的屬性的值。</li>
     <li><strong>算子</strong>:指定搜索時要應用的運算子。 支援以下運算子：
      <ul>
       <li>EQ — 等於 </li>
       <li>NEQ — 不等於</li>
       <li>GT — 大於</li>
       <li>LT — 小於</li>
       <li>GTEQ — 大於或等於</li>
       <li>LTEQ — 小於或等於</li>
       <li>CONTAINS — 如果B是A的一部分，則A包含B</li>
       <li>全文 — 全文搜索</li>
       <li>STARTSWITH — 如果B是A的開頭部分，則A以B開頭</li>
       <li>ENDSWITH — 如果B是A的結尾部分，則A以B結尾</li>
       <li>LIKE — 實現LIKE運算子</li>
       <li>AND — 合併多個語句</li>
      </ul> <p><strong>注：</strong> <em>GT、LT、GTEQ和LTEQ算子適用於線性類型如LONG、DOUBLE和DATE的性質。</em></p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>排序<br /> </td>
   <td><p>指定搜索結果的順序標準。 條件以JSON格式定義。 可以對多個欄位上的搜索結果進行排序。 結果按查詢中顯示欄位的順序排序。</p> <p>例如，</p> <p>要按升序檢索按title屬性排序的查詢結果，請添加以下參數： </p> <p><code class="code">JSONArray orderingsArray=new JSONArray();
       JSONObject orderings=new JSONObject();
       orderings.put("name", "title");
       orderings.put("criteria", "ASC");
       orderingsArray.put(orderings);
       entityBuilder.add("orderings", orderingsArray.toString());</code></p>
    <ul>
     <li><strong>名稱</strong>:指定用於排序搜索結果的屬性名稱。</li>
     <li><strong>標準</strong>:指定結果的順序。 訂單屬性接受以下值：
      <ul>
       <li>ASC — 使用ASC按升序排列結果。<br /> </li>
       <li>DES — 使用DES按降序排列結果。</li>
      </ul> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>包括Xdp</td>
   <td>指定是否檢索二進位內容。 的 <code>includeXdp</code> 屬性適用於類型的資產 <code>FORM</code>。 <code>PDFFORM</code>, <code>PRINTFORM</code>。</td>
  </tr>
  <tr>
   <td>資產類型</td>
   <td>指定要從所有已發佈資產中檢索的資產類型。 使用管道(|)運算子指定多個資產類型。 有效的資產類型有FORM、PDFFORM、PRINTFORM、RESOURCE和GUIDE。</td>
  </tr>
 </tbody>
</table>

## 示例請求 {#sample-request}

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

## 示例響應 {#sample-response}

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

* [啟用表單門戶元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單門戶頁](/help/forms/using/creating-form-portal-page.md)
* [使用API在網頁上列出表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自定義草稿和已提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自定義表單門戶元件的模板](/help/forms/using/customizing-templates-forms-portal-components.md)
* [門戶上發佈表單簡介](/help/forms/using/introduction-publishing-forms.md)
