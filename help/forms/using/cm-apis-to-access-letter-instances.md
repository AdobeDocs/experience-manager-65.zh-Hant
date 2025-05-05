---
title: 存取信件例項的API
description: 探索API，並使用它們以程式設計方式存取AEM Forms環境中的信件例項。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: 9d43d9d4-5487-416c-b641-e807227ac056
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 1%

---

# 存取信件例項的API {#apis-to-access-letter-instances}

## 概觀 {#overview}

使用「通訊管理」的「建立通訊UI」，您可以儲存正在處理的信件例項草稿，並且有已提交的信件例項。

「通訊管理」會提供API，您可以使用這些API來建立清單介面，以處理已提交的信件例項或草稿。 API會列出並開啟代理程式的已提交和草稿信函例項，讓代理程式可以繼續處理草稿或已提交信函例項。

## 正在擷取字母例項 {#fetching-letter-instances}

Correspondence Management會公開API，以透過LetterInstanceService服務擷取信件例項。

| 方法 | 說明 |
|--- |--- |
| getAllLetterInstances | 根據輸入查詢引數擷取信件例項。 若要擷取所有信件例項，請將查詢引數傳入null。 |
| getLetterInstance | 根據信件例項ID擷取指定的信件例項。 |
| Lettinstanceexists | 檢查指定的名稱是否存在LetterInstance。 |

>[!NOTE]
>
>LetterInstanceService是OSGI服務，在Java中使用@Reference可擷取其執行個體™
>類別或sling.getService(LetterInstanceService。 類別)。

### 使用getAllLetterInstances {#using-nbsp-getallletterinstances}

以下API會根據查詢物件（已提交和草稿）來尋找信件例項。 如果查詢物件為Null，則會傳回所有信件例項。 此API傳回[LetterInstanceVO](https://helpx.adobe.com/tw/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html)物件的清單，這些物件可用於擷取信件執行個體的其他資訊。

**語法**： `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>參數</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>查詢</td>
   <td>查詢引數是用來尋找/篩選信件例項。 在此，查詢僅支援物件的頂層屬性/屬性。 查詢由陳述式組成，而且在Statement物件中使用的"attributeName"應該是Letter執行個體物件中的屬性名稱。<br /> </td>
  </tr>
 </tbody>
</table>

#### 範例1：擷取型別為SUBMITTED的所有字母例項 {#example-fetch-all-the-letter-instances-of-type-submitted}

下列程式碼會傳回已提交信件例項的清單。 若要只取得草稿，請將`LetterInstanceType.COMPLETE.name()`變更為`LetterInstanceType.DRAFT.name().`

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

#### 範例2：擷取使用者提交的所有信函例項，且信函例項型別為DRAFT {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

下列程式碼在相同查詢中有多個陳述式，可取得根據不同條件篩選的結果，例如使用者提交的信件例項（屬性提交者），以及letterInstanceType型別為DRAFT。

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

擷取由指定的字母例項ID所識別的信件例項。 如果執行個體ID不相符，則會傳回「 null 」。

**語法：** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### 正在驗證LetterInstance是否存在 {#verifying-if-letterinstance-exist}

檢查信件例項是否存在指定的名稱

**語法**： `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **引數** | **說明** |
|---|---|
| letterInstanceName | 您要檢查其是否存在的信件例項名稱。 |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## 開啟字母例項 {#opening-letter-instances}

信件例項可以是已提交或草稿型別。 開啟兩種信件例項型別會顯示不同的行為：

* 如果存在「已提交」信件例項，則會開啟代表該信件例項的PDF。 儲存在伺服器上的提交信件例項也包含dataXML和已處理的XDP，這可用於完成並進一步自訂使用案例，例如建立PDF/A。
* 如果存在「草稿」信件例項，則建立通訊UI會重新載入到與建立草稿時完全相同的先前狀態

### 開啟草稿字母例項  {#opening-draft-letter-instance-nbsp}

CCR UI支援cmLetterInstanceId引數，該引數可用來重新載入字母。

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>重新載入通訊時，您不必指定cmLetterId或cmLetterName/State/Version，因為提交的資料已包含重新載入通訊的所有詳細資訊。 RandomNo可用來避免瀏覽器快取問題，但您可以使用時間戳記當作隨機數。

### 開啟提交的字母例項 {#opening-submitted-letter-instance}

您可以使用字母例項ID直接開啟已提交的PDF：

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
