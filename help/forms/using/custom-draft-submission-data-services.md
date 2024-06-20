---
title: 自訂草稿和提交資料服務
description: 依預設，AEM Forms會將草稿和已提交的最適化表單儲存在Publish執行個體的預設節點中。 不過，您可以設定AEM Forms的草稿和提交資料服務，以自訂草稿和提交的最適化表單的儲存。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
exl-id: ed10ef8c-7b9c-43cf-bea8-7cf9742a8cac
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# 自訂草稿和提交資料服務 {#customizing-draft-and-submission-data-services}

## 概觀 {#overview}

AEM Forms可讓使用者將最適化表單儲存為草稿。 草稿功能為使用者提供了維護工作進行中表單的選項。 然後，使用者可以隨時從任何裝置完成並提交表單。

依預設，AEM Forms會將與草稿和提交相關聯的使用者資料儲存在的Publish執行個體上 `/content/forms/fp` 節點。

不過，AEM Forms Portal元件提供資料服務，可讓您自訂儲存草稿和提交之使用者資料的實作。 例如，您可以將資料儲存在組織目前實作的資料存放區中。

若要自訂使用者資料的儲存，您必須實作 [草稿資料](/help/forms/using/custom-draft-submission-data-services.md#p-draft-data-service-p) 和 [提交資料](/help/forms/using/custom-draft-submission-data-services.md#p-submission-data-service-p) 服務。

## 先決條件 {#prerequisites}

* 啟用 [Forms Portal元件](/help/forms/using/enabling-forms-portal-components.md)
* 建立 [Forms入口網站頁面](/help/forms/using/creating-form-portal-page.md)
* 啟用 [適用於Forms入口網站的最適化表單](/help/forms/using/draft-submission-component.md)
* 瞭解 [自訂儲存的實作詳細資料](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## 草稿資料服務 {#draft-data-service}

若要自訂使用者草稿資料的儲存，您必須提供以下所有方法的實作： `DraftAFDataService` 介面。

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
  * @param draftUserDataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID") if there is update
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

若要自訂使用者提交資料的儲存，您必須提供以下所有方法的實作： `SubmittedAFDataService` 介面。

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
