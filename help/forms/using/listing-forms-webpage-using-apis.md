---
title: 使用API列出網頁上的表單
seo-title: Listing forms on a web page using APIs
description: 以程式設計方式查詢Forms Manager，以擷取已篩選的表單清單並顯示在您自己的網頁上。
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

# 使用API列出網頁上的表單 {#listing-forms-on-a-web-page-using-apis}

AEM Forms提供REST型搜尋API，網頁開發人員可使用此API來查詢及擷取符合搜尋條件的一組表單。 您可以使用API根據各種篩選條件來搜尋表單。 回應物件包含表單屬性、屬性，以及轉譯表單端點。

若要使用REST API搜尋表單，請傳送GET要求至 `https://'[server]:[port]'/libs/fd/fm/content/manage.json` 搭配查詢參數，如下所述。

## 查詢參數 {#query-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>屬性名稱<br /> </strong></td>
   <td><strong>說明<br /> </strong></td>
  </tr>
  <tr>
   <td>func<br /> </td>
   <td><p>指定要呼叫的函式。 若要搜尋表單，請設定 <code>func </code>屬性至 <code>searchForms</code>.</p> <p>例如， <code class="code">
       URLParameterBuilder entityBuilder=new URLParameterBuilder ();
       entityBuilder.add("func", "searchForms");</code></p> <p><strong>注意：</strong> <em>此參數為必填項。</em><br /> </p> </td>
  </tr>
  <tr>
   <td>appPath<br /> </td>
   <td><p>指定要搜索表單的應用程式路徑。 依預設， appPath屬性會搜尋根節點層級上可用的所有應用程式。<br /> </p> <p>您可以在單一搜尋查詢中指定多個應用程式路徑。 以垂直號(|)字元分隔多個路徑。 </p> </td>
  </tr>
  <tr>
   <td>cutPoints<br /> </td>
   <td><p>指定要使用資產擷取的屬性。 您可以使用星號(*)一次擷取所有屬性。 使用垂直號(|)運算子來指定多個屬性。 </p> <p>例如， <code>cutPoints=propertyName1|propertyName2|propertyName3</code></p> <p><strong>注意</strong>: </p>
    <ul>
     <li><em>系統一律會擷取id、路徑和名稱等屬性。 </em></li>
     <li><em>每個資產都有不同的屬性集。 formUrl、pdfUrl和guideUrl等屬性不依賴切換點屬性。 這些屬性取決於資產類型，並會據此擷取。 </em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>關係<br /> </td>
   <td>指定要擷取的相關資產以及搜尋結果。 您可以選擇下列其中一個選項來擷取相關資產：
    <ul>
     <li><strong>無關係</strong>:請勿擷取相關資產。</li>
     <li><strong>立即</strong>:擷取與搜尋結果直接相關的資產。</li>
     <li><strong>全部</strong>:擷取直接和間接相關的資產。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>maxSize</td>
   <td>指定要擷取的表單數量上限。</td>
  </tr>
  <tr>
   <td>偏移</td>
   <td>指定從頭開始要略過的表單數。</td>
  </tr>
  <tr>
   <td>returnCount</td>
   <td>指定是否返回與給定條件匹配的搜索結果。 </td>
  </tr>
  <tr>
   <td>語句</td>
   <td><p>指定語句清單。 查詢會在JSON格式中指定的陳述式清單上執行。 </p> <p>例如，</p> <p><code class="code">JSONArray statementArray=new JSONArray();
       JSONObject statement=new JSONObject();
       statement.put("name", "title");
       statement.put("value", "SimpleSurveyAF");
       statement.put("operator", "EQ"); statementArray.put(statement);</code></p> <p>在上述範例中， </p>
    <ul>
     <li><strong>名稱</strong>:指定要搜索的屬性名稱。</li>
     <li><strong>value</strong>:指定要搜索的屬性的值。</li>
     <li><strong>運算子</strong>:指定在搜索時應用的運算子。 支援下列運算子：
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
       <li>LIKE — 實作LIKE運算子</li>
       <li>AND — 合併多個陳述式</li>
      </ul> <p><strong>注意：</strong> <em>GT、LT、GTEQ和LTEQ運算子適用於線性類型的屬性，如LONG、DOUBLE和DATE。</em></p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>排序<br /> </td>
   <td><p>指定搜索結果的順序標準。 條件以JSON格式定義。 您可以對多個欄位上的搜尋結果進行排序。 查詢中顯示的欄位會依序排序結果。</p> <p>例如，</p> <p>若要以升序擷取依標題屬性排序的查詢結果，請新增下列參數： </p> <p><code class="code">JSONArray orderingsArray=new JSONArray();
       JSONObject orderings=new JSONObject();
       orderings.put("name", "title");
       orderings.put("criteria", "ASC");
       orderingsArray.put(orderings);
       entityBuilder.add("orderings", orderingsArray.toString());</code></p>
    <ul>
     <li><strong>名稱</strong>:指定用於排序搜索結果的屬性名稱。</li>
     <li><strong>條件</strong>:指定結果的順序。 order屬性接受以下值：
      <ul>
       <li>ASC — 使用ASC以升序排列結果。<br /> </li>
       <li>DES — 使用DES以降序排列結果。</li>
      </ul> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>includeXdp</td>
   <td>指定是否檢索二進位內容。 此 <code>includeXdp</code> 屬性適用於類型的資產 <code>FORM</code>, <code>PDFFORM</code>，和 <code>PRINTFORM</code>.</td>
  </tr>
  <tr>
   <td>assetType</td>
   <td>指定要從所有已發佈資產中擷取的資產類型。 使用垂直號(|)運算子來指定多個資產類型。 有效的資產類型包括FORM、PDFFORM、PRINTFORM、RESOURCE和GUIDE。</td>
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
* [使用API列出網頁上的表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](/help/forms/using/draft-submission-component.md)
* [自訂草稿和已提交表單的儲存](/help/forms/using/draft-submission-component.md)
* [將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md)
* [自訂表單入口網站元件的範本](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站發佈表單簡介](/help/forms/using/introduction-publishing-forms.md)
