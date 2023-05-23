---
title: 在表單門戶上使用已提交表單的API
seo-title: APIs to work with submitted forms on forms portal
description: AEM Forms提供了API，您可以使用這些API來查詢表單門戶中提交的表單資料並對其執行操作。
seo-description: AEM Forms provides APIs that you can use to query and take actions on submitted forms data in forms portal.
uuid: c47c8392-e5a9-4c40-b65e-4a7f379a6b45
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish, developer-reference
discoiquuid: 9457effd-3595-452f-a976-ad9eda6dc909
feature: Forms Portal
exl-id: a685889e-5d24-471c-926d-dbb096792bc8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 7%

---

# 在表單門戶上使用已提交表單的API {#apis-to-work-with-submitted-forms-on-forms-portal}

AEM Forms提供了API，您可以使用這些API查詢通過表單門戶提交的表單資料。 此外，您還可以使用本文檔中介紹的API發佈注釋或更新已提交表單的屬性。

>[!NOTE]
>
>將調用API的用戶必須添加到審閱者組，如所述 [將提交審核者與表單關聯](/help/forms/using/adding-reviewers-form.md)。

## GET/content/forms/portal/submission.review.json?func=getFormsFormsSubmissionReview {#get-content-forms-portal-submission-review-json-func-getformsforsubmissionreview-br}

返回所有合格表單的清單。

### URL參數 {#url-parameters}

此API不需要其他參數。

### 回應 {#response}

響應對象包含JSON陣列，該陣列包含表單名稱及其儲存庫路徑。 響應的結構如下：

```json
[
 {formName: "<form name>",
 formPath: "<path to the form>" },
 {.....},
 ......]
```

### 範例 {#example}

**請求 URL**

```http
https://[host]:[port]/content/forms/portal/submission.review.json?func=getFormsForSubmissionReview
```

**回應**

```json
[{"formPath":"/content/dam/formsanddocuments/forms-review/form2","formName":"form2"},{"formPath":"/content/dam/formsanddocuments/forms-review/form1","formName":"form1"}]
```

## GET/content/forms/portal/submission.review.json?func=getAllSubmissions {#get-content-forms-portal-submission-review-json-func-getallsubmissions}

返回所有已提交表單的詳細資訊。 但是，可以使用URL參數來限制結果。

### URL參數 {#url-parameters-1}

在請求URL中指定以下參數：

<table>
 <tbody>
  <tr>
   <th>參數</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><code>formPath</code></td>
   <td>指定表單所在的CRX儲存庫路徑。 如果未指定表單路徑，則返回空響應。<br /> </td>
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
   <td>指定對結果排序的屬性。 預設值為 <strong>jcr：上次修改時間</strong>，根據上次修改的時間對結果排序。</td>
  </tr>
  <tr>
   <td><code>sort</code> <br /> (可選)</td>
   <td>指定對結果排序的順序。 預設值為 <strong>des</strong>，按降序排序。 可以指定 <code>asc</code> 按升序排序。</td>
  </tr>
  <tr>
   <td><code>cutPoints</code> <br /> (可選)</td>
   <td>指定要包含在結果中的表單屬性的逗號分隔清單。 預設屬性為：<br /> <code>formName</code>。 <code>formPath</code>。 <code>submitID</code>。 <code>formType</code>。 <code>jcr:lastModified</code>。 <code>owner</code></td>
  </tr>
  <tr>
   <td><code>search</code> <br /> (可選)</td>
   <td>在表單屬性中搜索指定的值，並返回具有匹配值的表單。 預設值為 <strong>""</strong>.</td>
  </tr>
 </tbody>
</table>

### 回應 {#response-1}

響應對象包含JSON陣列，該陣列包含指定表單的詳細資訊。 響應的結構如下：

```json
{
 total: "<total number of submissions>",
 items: [{ formName: "<name of the form>", formPath: "<path to the form>", owner: "<owner of the form>"},
 ....]}
```

### 範例 {#example-1}

**請求 URL**

```http
https://[host]:[port]/content/forms/portal/submission.review.json?func=getAllSubmissions&formPath=/content/dam/formsanddocuments/forms-review/form2
```

**回應**

```json
{"total":1,"items":[{"formName":"form2","formPath":"/content/dam/formsanddocuments/forms-review/form2","submitID":"1403037413508500","formType":"af","jcr:lastModified":"2015-11-05T17:52:32.243+05:30","owner":"admin"}]}
```

## POST/content/forms/portal/submission.review.json?func=addComment {#post-content-forms-portal-submission-review-json-func-addcomment-br}

向指定的提交實例添加註釋。

### URL參數 {#url-parameters-2}

在請求URL中指定以下參數：

| 參數 | 說明 |
|---|---|
| `submitID` | 指定與提交實例關聯的元資料ID。 |
| `Comment` | 指定要添加到指定提交實例的注釋的文本。 |

### 回應 {#response-2}

返回注釋成功發佈時的注釋ID。

### 範例 {#example-2}

**請求 URL**

```http
https://[host:'port'/content/forms/portal/submission.review.json?func=addComment&submitID=1403037413508500&comment=API+test+comment
```

**回應**

```java
1403873422601300
```

## GET/content/forms/portal/submission.review.json?func=getComments   {#get-content-forms-portal-submission-review-json-func-getcomments-nbsp}

返回在指定提交實例上發佈的所有注釋。

### URL參數 {#url-parameters-3}

在請求URL中指定以下參數：

| 參數 | 說明 |
|---|---|
| `submitID` | 指定提交實例的元資料ID。 |

### 回應 {#response-3}

響應對象包含JSON陣列，該陣列包含與指定提交ID關聯的所有注釋。 響應的結構如下：

```json
[{
 owner: "<name of the commenter>",
 comment: "<comment text>",
 time: "<time when the comment was posted>"},
 { }......]
```

### 範例 {#example-3}

**請求 URL**

```http
https://[host]:'port'/content/forms/portal/submission.review.json?func=getComments&submitID=1403037413508500
```

**回應**

```java
[{"owner":"fr1","comment":"API test comment","time":1446726988250}]
```

## POST/content/forms/portal/submission.review.json?func=updateSubmission {#post-content-forms-portal-submission-review-json-func-updatesubmission-br}

更新指定已提交表單實例的指定屬性的值。

### URL參數 {#url-parameters-4}

在請求URL中指定以下參數：

| 參數 | 說明 |
|---|---|
| `submitID` | 指定與提交實例關聯的元資料ID。 |
| `property` | 指定要更新的表單屬性。 |
| `value` | 指定要更新的表單屬性的值。 |

### 回應 {#response-4}

返回包含已發佈更新資訊的JSON對象。

### 範例 {#example-4}

**請求 URL**

```http
https://[host]:'port'/content/forms/portal/submission.review.json?func=updateSubmission&submitID=1403037413508500&value=sample_value&property=some_new_prop
```

**回應**

```json
{"formName":"form2","owner":"admin","jcr:lastModified":1446727516593,"path":"/content/forms/fp/admin/submit/metadata/1403037413508500.html","submitID":"1403037413508500","status":"submitted"}
```
