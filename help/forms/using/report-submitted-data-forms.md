---
title: 在表單入口網站上處理提交表單的API
seo-title: 在表單入口網站上處理提交表單的API
description: AEM Forms提供API，您可用來查詢表單入口網站中已提交表單資料並採取動作。
seo-description: AEM Forms提供API，您可用來查詢表單入口網站中已提交表單資料並採取動作。
uuid: c47c8392-e5a9-4c40-b65e-4a7f379a6b45
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
discoiquuid: 9457effd-3595-452f-a976-ad9eda6dc909
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 在表單入口網站上處理提交表單的API {#apis-to-work-with-submitted-forms-on-forms-portal}

AEM Forms提供API，您可用來查詢透過表單入口網站提交的表單資料。 此外，您也可以使用本檔案中說明的API，張貼意見或更新已提交表單的屬性。

>[!NOTE]
>
>將叫用API的使用者必須新增至審核者群組，如將提交審核者 [與表單建立關聯中所述](/help/forms/using/adding-reviewers-form.md)。

## GET /content/forms/portal/submission.review.json?func=getFormsForSubmissionReview {#get-content-forms-portal-submission-review-json-func-getformsforsubmissionreview-br}

傳回所有合格表單的清單。

### URL parameters {#url-parameters}

此API不需要其他參數。

### 回應 {#response}

回應物件包含JSON陣列，其中包含表單名稱及其儲存庫路徑。 響應的結構如下：

```
[
 {formName: "<form name>",
 formPath: "<path to the form>" },
 {.....},
 ......]
```

### 例如 {#example}

**請求URL**

```
https://[host]:[port]/content/forms/portal/submission.review.json?func=getFormsForSubmissionReview
```

**回應**

```java
[{"formPath":"/content/dam/formsanddocuments/forms-review/form2","formName":"form2"},{"formPath":"/content/dam/formsanddocuments/forms-review/form1","formName":"form1"}]
```

## GET /content/forms/portal/submission.review.json?func=getAllSubmissions {#get-content-forms-portal-submission-review-json-func-getallsubmissions}

傳回所有已提交表單的詳細資料。 不過，您可使用URL參數來限制結果。

### URL parameters {#url-parameters-1}

在請求URL中指定下列參數：

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>formPath</code></td>
   <td>指定表單所在的CRX儲存庫路徑。 如果您未指定表單路徑，則會傳回空回應。<br /> </td>
  </tr>
  <tr>
   <td><code>offset</code> (可選)</td>
   <td>指定結果集索引中的起始點。 預設值為 <strong>0</strong>。</td>
  </tr>
  <tr>
   <td><code>limit</code> (可選)</td>
   <td>限制結果數。 預設值為 <strong>30</strong>。</td>
  </tr>
  <tr>
   <td><code>orderby</code> <br /> (可選)</td>
   <td>指定對結果排序的屬性。 預設值為 <strong>jcr:lastModified</strong>，會根據上次修改的時間對結果排序。</td>
  </tr>
  <tr>
   <td><code>sort</code> <br /> (可選)</td>
   <td>指定排序結果的順序。 預設值為 <strong>desc</strong>，會以遞減順序排序結果。 您可以指定 <code>asc</code> 以遞增順序排序結果。</td>
  </tr>
  <tr>
   <td><code>cutPoints</code> <br /> (可選)</td>
   <td>指定要包含在結果中的表單屬性的逗號分隔清單。 <br /> 預設屬性為： <code>formName</code>, <code>formPath</code><code>submitID</code>, <code>formType</code>, <code>jcr:lastModified</code>, <code>owner</code></td>
  </tr>
  <tr>
   <td><code>search</code> <br /> (可選)</td>
   <td>在表單屬性中搜尋指定值，並傳回具有相符值的表單。 預設值為 <strong>""</strong>。</td>
  </tr>
 </tbody>
</table>

### 回應 {#response-1}

回應物件包含JSON陣列，其中包含指定表單的詳細資訊。 響應的結構如下：

```
{
 total: "<total number of submissions>",
 items: [{ formName: "<name of the form>", formPath: "<path to the form>", owner: "<owner of the form>"},
 ....]}
```

### 例如 {#example-1}

**請求URL**

```
https://[host]:[port]/content/forms/portal/submission.review.json?func=getAllSubmissions&formPath=/content/dam/formsanddocuments/forms-review/form2
```

**回應**

```java
{"total":1,"items":[{"formName":"form2","formPath":"/content/dam/formsanddocuments/forms-review/form2","submitID":"1403037413508500","formType":"af","jcr:lastModified":"2015-11-05T17:52:32.243+05:30","owner":"admin"}]}
```

## POST /content/forms/portal/submission.review.json?func=addComment {#post-content-forms-portal-submission-review-json-func-addcomment-br}

將注釋添加到指定的提交實例。

### URL parameters {#url-parameters-2}

在請求URL中指定下列參數：

| 參數 | 說明 |
|---|---|
| `submitID` | 指定與提交實例關聯的元資料ID。 |
| `Comment` | 指定要添加到指定提交實例的注釋文本。 |

### 回應 {#response-2}

傳回成功張貼留言的留言ID。

### 例如 {#example-2}

**請求URL**

```
https://[host:[port]/content/forms/portal/submission.review.json?func=addComment&submitID=1403037413508500&comment=API+test+comment
```

**回應**

```java
1403873422601300
```

## GET /content/forms/portal/submission.review.json?func=getComments {#get-content-forms-portal-submission-review-json-func-getcomments-nbsp}

傳回在指定的提交實例上張貼的所有注釋。

### URL parameters {#url-parameters-3}

在請求URL中指定下列參數：

| 參數 | 說明 |
|---|---|
| `submitID` | 指定提交實例的元資料ID。 |

### 回應 {#response-3}

回應物件包含JSON陣列，其中包含與指定之提交ID相關的所有註解。 響應的結構如下：

```
[{
 owner: "<name of the commenter>",
 comment: "<comment text>",
 time: "<time when the comment was posted>"},
 { }......]
```

### 例如 {#example-3}

**請求URL**

```
https://[host]:[port]/content/forms/portal/submission.review.json?func=getComments&submitID=1403037413508500
```

**回應**

```java
[{"owner":"fr1","comment":"API test comment","time":1446726988250}]
```

## POST /content/forms/portal/submission.review.json?func=updateSubmission {#post-content-forms-portal-submission-review-json-func-updatesubmission-br}

更新指定已提交表單實例的指定屬性的值。

### URL parameters {#url-parameters-4}

在請求URL中指定下列參數：

| 參數 | 說明 |
|---|---|
| `submitID` | 指定與提交實例關聯的元資料ID。 |
| `property` | 指定要更新的form屬性。 |
| `value` | 指定要更新的form屬性的值。 |

### 回應 {#response-4}

傳回JSON物件，其中包含已張貼更新的相關資訊。

### 例如 {#example-4}

**請求URL**

```
https://[host]:[port]/content/forms/portal/submission.review.json?func=updateSubmission&submitID=1403037413508500&value=sample_value&property=some_new_prop
```

**回應**

```java
{"formName":"form2","owner":"admin","jcr:lastModified":1446727516593,"path":"/content/forms/fp/admin/submit/metadata/1403037413508500.html","submitID":"1403037413508500","status":"submitted"}
```

