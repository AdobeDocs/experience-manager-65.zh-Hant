---
title: 存取字母例項的API
seo-title: 存取字母例項的API
description: 瞭解如何使用API來存取字母例項。
seo-description: 瞭解如何使用API來存取字母例項。
uuid: e7fb7798-f49d-458f-87f5-22df5f3e7d10
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9c27f976-972a-4250-b56d-b84a7d72f8c8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 存取字母例項的API {#apis-to-access-letter-instances}

## 概覽 {#overview}

使用「通信管理」的「建立通信」UI，您可以在進行中保存信件實例的草稿，並且有提交的信件實例。

Commense Management提供API，您可使用這些API建立清單介面，以處理已提交的信函例項或草稿。 API列出並開啟座席的已提交和草稿字母實例，以便座席可以繼續處理草稿或已提交的字母實例。

## 提取字母實例 {#fetching-letter-instances}

Correponse Management會使API透過LetterInstanceService服務擷取字母例項。

| 方法 | 說明 |
|--- |--- |
| getAllLetterInstances | 根據輸入查詢參數讀取字母實例。 若要擷取所有字母例項，請將查詢參數傳遞為null。 |
| getLetterInstance | 根據字母實例Id讀取指定的字母實例。 |
| letterInstanceExists | 檢查給定名稱是否存在LetterInstance。 |

>[!NOTE]
>
>LetterInstanceService是OSGI服務，其實例可在Java中使用@Reference來擷取
>Class或sling.getService(LetterInstanceService)。 類)。

### 使用getAllLetterInstances {#using-nbsp-getallletterinstances}

下列API會根據查詢物件（已提交和草稿）來尋找字母例項。 如果查詢對象為空，則返回所有字母實例。 此API會傳回 [LetterInstanceVO物件清單](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html) ，可用來擷取字母執行個體的其他資訊

**語法**: `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>參數</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>查詢</td>
   <td>查詢參數用於查找／篩選Letter實例。 此處查詢僅支援對象的頂級屬性／屬性。 Query由語句組成，Statement對象中使用的"attributeName"應是Letter實例對象中屬性的名稱。<br /> </td>
  </tr>
 </tbody>
</table>

#### 範例1:獲取所有類型為SUBMITTED的字母實例 {#example-fetch-all-the-letter-instances-of-type-submitted}

下列程式碼會傳回已提交字母例項的清單。 若要只取得草稿，請將 `LetterInstanceType.COMPLETE.name()` 變更為 `LetterInstanceType.DRAFT.name().`

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

#### 範例2：擷取使用者提交的所有字母例項，字母例項類型為DRAFT {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

以下代碼在同一查詢中包含多個語句，以便根據用戶提交的字母實例（屬性提交者）等不同標準來過濾結果，並且letterInstanceType的類型為DRAFT。

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

提取由給定字母實例id標識的字母實例。 如果實例ID不匹配，則返回&#39;&#39;。

**** 語法： `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

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

## 開啟字母例項 {#opening-letter-instances}

Letter Instance可以是「已提交」或「草稿」類型。 開啟兩個字母實例類型會顯示不同的行為：

* 如果是「已提交的字母實例」，則會開啟表示字母實例的PDF。 保存在伺服器上的已提交信件例項也包含dataXML和已處理的XDP，可用來完成並進一步自訂使用案例，例如建立PDF/A。
* 如果是「草稿」字母實例，建立對應UI會重新載入至先前的狀態，就像建立草稿時一樣

### 開啟草稿字母實例 {#opening-draft-letter-instance-nbsp}

CCR UI支援cmLetterInstanceId參數，該參數可用於重新載入字母。

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>重裝通信時，您不必指定cmLetterId或cmLetterName/State/Version，因為提交的資料已經包含重新載入的通信的所有詳細資訊。 RandomNo用於避免瀏覽器快取問題，您可以使用時間戳記作為隨機數。

### 開啟已提交的信函實例 {#opening-submitted-letter-instance}

已提交的PDF可使用字母執行個體Id直接開啟：

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
