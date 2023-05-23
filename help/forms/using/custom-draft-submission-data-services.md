---
title: 自定義草稿和提交資料服務
seo-title: Customizing Draft and Submission data services
description: AEM Forms預設情況下，在「發佈」實例的預設節點中儲存草稿和提交的自適應表單。 但是，您可以配置AEM Forms的草稿和提交資料服務，以自定義草稿和提交的自適應表單的儲存。
seo-description: AEM Forms, by default, stores draft and submitted adaptive forms in a default node on the Publish instance. However, you can configure the draft and submission data services of AEM Forms to customize the storage of draft and submitted adaptive forms.
uuid: c3ec1708-3b11-4142-93f0-1cffb6643f34
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 602fd6a9-9a65-411c-8475-a4082a3fdee0
exl-id: ed10ef8c-7b9c-43cf-bea8-7cf9742a8cac
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# 自定義草稿和提交資料服務 {#customizing-draft-and-submission-data-services}

## 概觀 {#overview}

AEM Forms允許用戶將自適應表單另存為草稿。 草稿功能為用戶提供了維護正在進行表單的選項。 用戶隨後可以從任何設備完成並隨時提交表格。

預設情況下，AEM Forms將與草稿和提交關聯的用戶資料儲存在 `/content/forms/fp` 的下界。

但是，AEM Forms門戶元件提供資料服務，允許您定制為草稿和提交儲存用戶資料的實現。 例如，您可以將資料儲存在組織中當前實施的資料儲存中。

要自定義用戶資料的儲存，您需要 [草稿資料](/help/forms/using/custom-draft-submission-data-services.md#p-draft-data-service-p) 和 [提交資料](/help/forms/using/custom-draft-submission-data-services.md#p-submission-data-service-p) 服務。

## 必備條件 {#prerequisites}

* 啟用 [Forms門戶元件](/help/forms/using/enabling-forms-portal-components.md)
* 建立 [表單門戶頁](/help/forms/using/creating-form-portal-page.md)
* 啟用 [表單門戶的自適應表單](/help/forms/using/draft-submission-component.md)
* 學習 [定制儲存的實施詳細資訊](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## 草稿資料服務 {#draft-data-service}

要自定義用戶草稿資料的儲存，您需要為 `DraftAFDataService` 。

在介面的以下代碼示例中提供了方法及其參數的說明：

```java
public interface DraftAFDataService {

 /**
  * Deletes the user data stored against the ID passed as the argument
  *
  * @param draftDataID
  * @return status for the just occurred delete draft UserData operation
  * @throws FormsPortalException
  */
 public Boolean deleteAFDraftUserData (String draftDataID) throws FormsPortalException;

 /**
  * Saves user data provided in the argument map
  *
  * @param draftUserDataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID") in case of update
  * @return userData ID would be returned which needs to be saved in metadata node
  * @throws FormsPortalException
  */
 public String saveAFUserData (Map<String, Object> draftUserDataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as the argument
  *
  * @param Draft DataID
  * @return guideState (which would then be populated in adaptive form to reload the draft) which is stored against draftDataID
  * @throws FormsPortalException
  */
 public byte[] getAFDraftUserData(String draftDataID) throws FormsPortalException;

 /**
  * Saves the attachments for current adaptive form instance
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String saveAttachments(byte[] attachmentBytes) throws FormsPortalException;
}
```

## 提交資料服務 {#submission-data-service}

要自定義用戶提交資料的儲存，您需要提供對 `SubmittedAFDataService` 。

在介面的以下代碼示例中提供了方法及其參數的說明：

```java
public interface SubmittedAFDataService {

 /**
  * Submits the user data passed in argument map
  *
  * @param submittedAFUserdataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID")
  * @return userData ID is returned that needs to be saved in the metadata node
  * @throws FormsPortalException
  */
 public String submitAFUserData (Map<String, Object> submittedAFUserdataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as argument
  *
  * @param submitDataID
  * @return guideState which would be used to open DOR
  * @throws FormsPortalException
  */
 public byte[] getSubmittedAFUSerData(String submitDataID) throws FormsPortalException;

 /**
  * Deletes user data stored against the ID passed as argument
  *
  * @param Submit DataID
  * @return status of the delete operation on Submitted User data
  * @throws FormsPortalException
  */

 public Boolean deleteSubmittedAFUserData(String submitDataID) throws FormsPortalException;

 /**
  * Submits the attachment bytes passed as argument
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String submitAttachments(Object attachmentBytes) throws FormsPortalException;

}
```
