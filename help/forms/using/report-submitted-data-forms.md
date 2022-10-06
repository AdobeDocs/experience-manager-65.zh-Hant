---
title: 在表單入口網站上使用已提交表單的API
seo-title: APIs to work with submitted forms on forms portal
description: AEM Forms提供API，可用來在表單入口網站中查詢已提交的表單資料並採取動作。
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

# 在表單入口網站上使用已提交表單的API {#apis-to-work-with-submitted-forms-on-forms-portal}

AEM Forms提供API，供您用來查詢透過表單入口網站提交的表單資料。 此外，您也可以使用本檔案說明的API，張貼意見或更新已提交表單的屬性。

>[!NOTE]
>
>將叫用API的使用者必須新增至審核者群組，如 [將提交審核者與表單關聯](/help/forms/using/adding-reviewers-form.md).

## GET/content/forms/portal/submission.review.json?func=getFormsFormsSubmissionReview {#get-content-forms-portal-submission-review-json-func-getformsforsubmissionreview-br}

返回所有合格表單的清單。

### URL參數 {#url-parameters}

此API不需要其他參數。

### 回應 {#response}

回應物件包含JSON陣列，內含表單名稱及其存放庫路徑。 回應的結構如下：

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

傳回所有已提交表單的詳細資訊。 不過，您可以使用URL參數來限制結果。

### URL參數 {#url-parameters-1}

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
   <td>指定結果集索引中的起始點。 預設值為 <strong>0</strong>.</td>
  </tr>
  <tr>
   <td><code>limit</code> (可選)</td>
   <td>限制結果數。 預設值為 <strong>30</strong>.</td>
  </tr>
  <tr>
   <td><code>orderby</code> <br /> (可選)</td>
   <td>指定排序結果的屬性。 預設值為 <strong>jcr:lastModified</strong>，會根據上次修改的時間排序結果。</td>
  </tr>
  <tr>
   <td><code>sort</code> <br /> (可選)</td>
   <td>指定排序結果的順序。 預設值為 <strong>desc</strong>，排序會以降序排序。 您可以指定 <code>asc</code> 以升序排序結果。</td>
  </tr>
  <tr>
   <td><code>cutPoints</code> <br /> (可選)</td>
   <td>指定要包含在結果中的表單屬性清單（以逗號分隔）。 預設屬性為：<br /> <code>formName</code>, <code>formPath</code>, <code>submitID</code>, <code>formType</code>, <code>jcr:lastModified</code>, <code>owner</code></td>
  </tr>
  <tr>
   <td><code>search</code> <br /> (可選)</td>
   <td>在表單屬性中搜索指定值，並返回具有匹配值的表單。 預設值為 <strong>""</strong>.</td>
  </tr>
 </tbody>
</table>

### 回應 {#response-1}

回應物件包含JSON陣列，內含指定表單的詳細資訊。 回應的結構如下：

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

將注釋添加到指定的提交實例。

### URL參數 {#url-parameters-2}

在請求URL中指定下列參數：

| 參數 | 說明 |
|---|---|
| `submitID` | 指定與提交例項相關聯的中繼資料ID。 |
| `Comment` | 指定要添加到指定提交實例的注釋文本。 |

### 回應 {#response-2}

在成功張貼留言時傳回留言ID。

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

傳回張貼在指定提交例項上的所有留言。

### URL參數 {#url-parameters-3}

在請求URL中指定下列參數：

| 參數 | 說明 |
|---|---|
| `submitID` | 指定提交實例的元資料ID。 |

### 回應 {#response-3}

回應物件包含JSON陣列，包含與指定提交ID相關聯的所有註解。 回應的結構如下：

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

在請求URL中指定下列參數：

| 參數 | 說明 |
|---|---|
| `submitID` | 指定與提交例項相關聯的中繼資料ID。 |
| `property` | 指定要更新的表單屬性。 |
| `value` | 指定要更新的表單屬性的值。 |

### 回應 {#response-4}

傳回JSON物件，其中包含已張貼更新的相關資訊。

### 範例 {#example-4}

**請求 URL**

```http
https://[host]:'port'/content/forms/portal/submission.review.json?func=updateSubmission&submitID=1403037413508500&value=sample_value&property=some_new_prop
```

**回應**

```json
{"formName":"form2","owner":"admin","jcr:lastModified":1446727516593,"path":"/content/forms/fp/admin/submit/metadata/1403037413508500.html","submitID":"1403037413508500","status":"submitted"}
```
