---
title: 自訂草稿和提交資料服務
seo-title: 自訂草稿和提交資料服務
description: AEM Forms依預設會將草稿和提交的最適化表單儲存在「發佈」例項的預設節點中。 不過，您可以設定AEM Forms的草稿和提交資料服務，以自訂草稿和已提交最適化表單的儲存。
seo-description: AEM Forms依預設會將草稿和提交的最適化表單儲存在「發佈」例項的預設節點中。 不過，您可以設定AEM Forms的草稿和提交資料服務，以自訂草稿和已提交最適化表單的儲存。
uuid: c3ec1708-3b11-4142-93f0-1cffb6643f34
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 602fd6a9-9a65-411c-8475-a4082a3fdee0
exl-id: ed10ef8c-7b9c-43cf-bea8-7cf9742a8cac
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# 自定義草稿和提交資料服務{#customizing-draft-and-submission-data-services}

## 概覽 {#overview}

AEM Forms可讓使用者將最適化表單儲存為草稿。 草稿功能可讓使用者選擇維護進行中表單。 然後，使用者可以隨時從任何裝置填妥並提交表單。

依預設，AEM Forms會將與草稿和提交相關聯的使用者資料儲存在`/content/forms/fp`節點的Publish執行個體上。

不過，AEM Forms入口網站元件提供的資料服務可讓您自訂為草稿和提交儲存使用者資料的實作。 例如，您可以將資料儲存在貴組織目前實作的資料存放區中。

若要自訂使用者資料的儲存，您需要實作[草稿資料](/help/forms/using/custom-draft-submission-data-services.md#p-draft-data-service-p)和[提交資料](/help/forms/using/custom-draft-submission-data-services.md#p-submission-data-service-p)服務。

## 必備條件 {#prerequisites}

* 啟用[Forms入口元件](/help/forms/using/enabling-forms-portal-components.md)
* 建立[forms portal頁面](/help/forms/using/creating-form-portal-page.md)
* 啟用[表單入口網站的最適化表單](/help/forms/using/draft-submission-component.md)
* 了解自訂儲存的[實作詳細資料](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## 草稿資料服務{#draft-data-service}

若要自訂使用者草稿資料的儲存，您需要提供`DraftAFDataService`介面所有方法的實作。

介面的下列程式碼範例中提供方法及其引數的說明：

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

## 提交資料服務{#submission-data-service}

若要自訂使用者提交資料的儲存，您需要提供`SubmittedAFDataService`介面所有方法的實作。

介面的下列程式碼範例中提供方法及其引數的說明：

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
