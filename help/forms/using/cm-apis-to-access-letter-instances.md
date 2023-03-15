---
title: 存取信函例項的API
seo-title: APIs to access letter instances
description: 了解如何使用API存取信函例項。
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

# 存取信函例項的API {#apis-to-access-letter-instances}

## 概觀 {#overview}

使用Correspondence Management的「建立通信UI」，您可以在進行中儲存信函例項的草稿，且會提交信函例項。

Correspondence Management提供您API，您可使用此API建立清單介面，以處理已提交的信函例項或草稿。 API清單和已開啟的已提交和已提交代理的信函實例草稿，以便代理可以繼續處理已提交或已提交的信函實例。

## 擷取信函例項 {#fetching-letter-instances}

通信管理會公開API，以透過LetterInstanceService服務擷取信函例項。

| 方法 | 說明 |
|--- |--- |
| getAllLetterInstances | 根據輸入查詢參數擷取信函例項。 若要擷取所有信函例項，請將查詢參數以null傳遞。 |
| getLetterInstance | 根據信函實例Id擷取指定的信函實例。 |
| letterInstanceExists | 檢查LetterInstance是否按給定名稱存在。 |

>[!NOTE]
>
>LetterInstanceService是OSGI服務，其例項可透過在Java中使@Reference來擷取
>類別或sling.getService(LetterInstanceService)。 類)。

### 使用getAllLetterInstances {#using-nbsp-getallletterinstances}

下列API會根據查詢物件（已提交和草稿）來尋找信函例項。 如果查詢對象為null，則返回所有字母實例。 此API會傳回 [LetterInstanceVO](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html) 對象，可用於提取字母實例的附加資訊

**語法**: `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>參數</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>查詢</td>
   <td>查詢參數用於尋找/篩選信函例項。 此處查詢僅支援對象的頂級屬性/屬性。 查詢由語句組成，Statement對象中使用的「attributeName」應為Letter實例對象中屬性的名稱。<br /> </td>
  </tr>
 </tbody>
</table>

#### 範例1:擷取SUBMITTED類型的所有信函例項 {#example-fetch-all-the-letter-instances-of-type-submitted}

下列程式碼會傳回已提交信函例項清單。 若要僅取得草稿，請變更 `LetterInstanceType.COMPLETE.name()` to `LetterInstanceType.DRAFT.name().`

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

#### 範例2：擷取使用者提交的所有信函例項，而信函例項類型為DRAFT {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

以下代碼在同一查詢中有多個語句，以獲取根據用戶提交的字母實例（由提交的屬性）等不同標準篩選的結果，並且letterInstanceType的類型為DRAFT。

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

擷取由指定信函例項id所識別的信函例項。 如果執行個體ID不相符，則會傳回「null」。

**語法：** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### 驗證LetterInstance是否存在 {#verifying-if-letterinstance-exist}

檢查字母實例是否按給定名稱存在

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

## 開頭字母實例 {#opening-letter-instances}

「信函例項」可為「已提交」或「草稿」類型。 開啟兩個信函例項類型會顯示不同行為：

* 在已提交信函例項中，會開啟代表信函例項的PDF。 保存在伺服器上的已提交信函例項也包含dataXML和已處理的XDP，可用來完成及進一步自訂使用案例，例如建立PDF/A。
* 若為草稿信函例項，建立通信UI會重新載入至與建立草稿期間完全相同的先前狀態

### 開啟信函草稿例項  {#opening-draft-letter-instance-nbsp}

CCR UI支援cmLetterInstanceId參數，該參數可用於重新載入信函。

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>重新載入通信時，不必指定cmLetterId或cmLetterName/State/Version，因為提交的資料已經包含有關重新載入的通信的所有詳細資訊。 RandomNo可用來避免瀏覽器快取問題，您可以使用時間戳記作為隨機數字。

### 開啟提交的信函實例 {#opening-submitted-letter-instance}

已提交的PDF可使用信函例項Id直接開啟：

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
