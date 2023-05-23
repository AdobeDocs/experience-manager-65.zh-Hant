---
title: 訪問字母實例的API
seo-title: APIs to access letter instances
description: 瞭解如何使用API訪問字母實例。
seo-description: Learn how to use APIs to access letter instances.
uuid: e7fb7798-f49d-458f-87f5-22df5f3e7d10
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9c27f976-972a-4250-b56d-b84a7d72f8c8
feature: Correspondence Management
exl-id: 9d43d9d4-5487-416c-b641-e807227ac056
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 1%

---

# 訪問字母實例的API {#apis-to-access-letter-instances}

## 概觀 {#overview}

使用「建立信件管理」的「建立信件UI」，您可以保存正在處理的信件實例的草稿，並且會提交信件實例。

Oracle Terment Management提供了API，您可以使用這些API構建清單介面以處理已提交的信函實例或草稿。 API清單並開啟代理的已提交和草稿信函實例，以便代理可以繼續處理草稿或已提交的信函實例。

## 正在提取字母實例 {#fetching-letter-instances}

Tergement Management公開API以通過LetterInstanceService服務獲取信函實例。

| 方法 | 說明 |
|--- |--- |
| getAllLetterInstances | 根據輸入查詢參數提取字母實例。 要提取所有字母實例，請將查詢參數傳遞為null。 |
| getLetterInstance | 根據字母實例ID讀取指定的字母實例。 |
| letterInstanceExists | 檢查給定名稱是否存在LetterInstance。 |

>[!NOTE]
>
>LetterInstanceService是OSGI服務，可以在Java中使用@Reference來檢索其實例
>Class或sling.getService(LetterInstanceService)。 類)。

### 使用getAllLetterInstances {#using-nbsp-getallletterinstances}

以下API基於查詢對象（已提交和草稿）查找字母實例。 如果查詢對象為null，則返回所有字母實例。 此API返回清單 [LetterInstanceVO](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html) 對象，用於提取字母實例的附加資訊

**語法**: `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>參數</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>查詢</td>
   <td>查詢參數用於查找/篩選Letter實例。 此處查詢僅支援對象的頂級屬性/屬性。 查詢由語句組成，Statement對象中使用的"attributeName"應是Letter實例對象中屬性的名稱。<br /> </td>
  </tr>
 </tbody>
</table>

#### 示例1:獲取所有類型為SUBMITTED的信函實例 {#example-fetch-all-the-letter-instances-of-type-submitted}

以下代碼返回已提交信函實例的清單。 要僅獲取草稿，請更改 `LetterInstanceType.COMPLETE.name()` 至 `LetterInstanceType.DRAFT.name().`

```java
@Reference
LetterInstanceService letterInstanceService;
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

#### 示例2：獲取用戶提交的所有字母實例，字母實例類型為DRAFT {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

以下代碼在同一查詢中具有多個語句，以根據用戶提交的字母實例（屬性提交者）等不同標準來過濾結果，並且letterInstanceType的類型為DRAFT。

```java
@Reference
LetterInstanceService letterInstanceService;

String submittedBy = "tglodman";
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);

Statement statementForSubmittedBy = new Statement();
statementForSubmittedBy .setAttributeName("submittedby");
statementForSubmittedBy .setOperator(Operator.EQUALS);
statementForSubmittedBy .setAttributeValue(submittedBy);
query.addStatement(statementForSubmittedBy );
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

### 使用getLetterInstance {#using-nbsp-getletterinstance}

提取由給定字母實例id標識的字母實例。 如果實例ID不匹配，則返回「空」。

**語法：** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### 驗證LetterInstance是否存在 {#verifying-if-letterinstance-exist}

檢查給定名稱是否存在字母實例

**語法**: `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **參數** | **說明** |
|---|---|
| letterInstanceName | 要檢查的字母實例的名稱是否存在。 |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## 期初字母實例 {#opening-letter-instances}

字母實例可以是「已提交」或「草稿」類型。 開啟這兩個字母實例類型顯示不同的行為：

* 如果是「已提交的信函實例」，則開啟表示該信函實例的PDF。 在伺服器上保留的已提交信件實例還包含dataXML和已處理的XDP，它可用於完成和進一步自定義使用案例，如建立PDF/A。
* 在「草稿」字母實例中，建立對應UI將重新載入到與建立草稿時相同的先前狀態

### 開啟草稿字母實例  {#opening-draft-letter-instance-nbsp}

CCR UI支援cmLetterInstanceId參數，該參數可用於重新載入字母。

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>重裝通信時，不必指定cmLetterId或cmLetterName/State/Version，因為已提交的資料已包含有關重新載入的通信的所有詳細資訊。 RandomNo用於避免瀏覽器快取問題，您可以將時間戳用作隨機數。

### 正在開啟已提交的信函實例 {#opening-submitted-letter-instance}

已提交PDF可以使用字母實例ID直接開啟：

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
