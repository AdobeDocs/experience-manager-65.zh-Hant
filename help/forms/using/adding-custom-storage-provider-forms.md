---
title: 草稿和提交元件的自訂儲存
seo-title: 草稿和提交元件的自訂儲存
description: 瞭解如何自訂草稿和提交之使用者資料的儲存。
seo-description: 瞭解如何自訂草稿和提交之使用者資料的儲存。
uuid: ac2e80ee-a9c7-44e6-801e-fe5a840cb7f8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 154255e7-468a-42e6-a33d-eee691cf854d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 草稿和提交元件的自訂儲存 {#custom-storage-for-drafts-and-submissions-component}

## 概覽 {#overview}

AEM Forms可讓您將表單儲存為草稿。 草稿功能可讓您維護進行中的表單，您可以從任何裝置完成並稍後送出。

依預設，AEM Forms會將與表單草稿和提交相關聯的使用者資料儲存在「發佈」例 `/content/forms/fp` 項的節點中。 此外，AEM Forms入口元件也提供資料服務，您可使用這些服務來自訂將使用者資料儲存在草稿和提交檔案的實作。 例如，您可以將使用者資料儲存在資料儲存區。

## 必備條件  {#prerequisites}

* 啟用 [表單入口元件](/help/forms/using/enabling-forms-portal-components.md)
* 建立表 [單入口網頁](/help/forms/using/creating-form-portal-page.md)
* 為表單 [入口網站啟用最適化表單](/help/forms/using/draft-submission-component.md)
* 瞭解自 [訂儲存空間的實作詳細資訊](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## 草稿資料服務 {#draft-data-service}

若要自訂草稿的使用者資料儲存，您必須實作介面的所有方 `DraftDataService` 法。 下列范常式式碼說明方法和引數。

```java
/**
 * DraftDataService service will get/delete/save user data (attachments and form data) filled with a draft instance of Form
 */

public interface DraftDataService {

    /**
     * To save/modify user data for this userDataID, it will be null in case of creation
     * @param draftDataID: unique identifier associated with the form data
     * @param formName: name of the form whose draft is being saved
     * @param formData: user data associated with this draft
     * @return userdataID corresponding to which user data has been stored and which can be used later to retrieve this user data
     * @throws FormsPortalException
     */
    public String saveData (String draftDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Returns the user data stored against the ID passed as the argument
     * @param userDataID: unique data id for user data associated with a draft
     * @return user data associated with this data ID
     * @throws FormsPortalException
     */

    public byte[] getData (String userDataID) throws FormsPortalException;

    /**
     * To delete data associated with this draft
     * @param userDataID: unique data id for data associated with a draft
     * @return status of delete operation on data associated with this draft
     * @throws FormsPortalException
     */

    public boolean deleteData (String userDataID) throws FormsPortalException;

    /**
     * Saves the attachment for current form instance
     * @param attachmentsBytes: byte array of the attachment to be saved
     * @return unique id (attachmentID) for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment (byte[] attachmentBytes) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

## 提交資料服務 {#submission-data-service}

若要自訂提交的使用者資料儲存，您必須實作介面的所有方 `SubmitDataService` 法。 下列范常式式碼說明方法和引數。

```java
/**
 * SubmitDataService service will get/delete/submit user data (attachments and form data) filled with a submission of Form
 */
public interface SubmitDataService {

    /**
     * Submits the user data passed in argument map
     * @param userDataID, unique identifier associated with this user data
     * @param formName, name of the form whose draft is being submitted
     * @param formData, user data associated with this submission
     * @return userdataID, corresponding to which the user data has been stored and which can be used later to retrieve this data
     * @throws FormsPortalException
     */
    public String saveData (String userDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Submits the user data provided as byte array
     * @param id
     * @param data
     * @return id corresponding to saved data
     * @throws FormsPortalException
     */
    public String saveData (String id, byte[] data) throws FormsPortalException;

    /** Submits the user data provided as byte array asynchronously for the user name provided in the options map
     * @param data data to be saved in bytes
     * @param options map containing options that affect this save
     * @return id of the saved data instance
     */
    public String saveDataAsynchronusly(byte[] data, Map<String, Object> options) throws FormsPortalException;

    /**
     * Gets the user data stored against the ID passed as argument
     * @param userDataID: unique id associated with this user data for this submission
     * @return user data associated with this submission
     * @throws FormsPortalException
     */
    public byte[] getData(String userDataID) throws FormsPortalException;

    /**
     * Deletes user data stored against the userDataID
     * @param userDataID: unique id associated with this user data for this submission
     * @return status of the delete operation on this submission
     * @throws FormsPortalException
     */

    public boolean deleteData(String userDataID) throws FormsPortalException;

    /**
     * Submits the attachment bytes passed as argument
     * @param attachmentsBytes: would expect byte array of the attachment for this submission
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment(byte[] attachmentBytes) throws FormsPortalException;

    /** Submits the attachment bytes passed as argument asynchronously for the user id provided in options map.
     * @param attachmentBytes would expect byte array of the attachment for this submission
     * @param options map containing options that affect this save
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachmentAsynchronously(byte[] attachmentBytes, Map<String, Object> options) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: Unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

表單入口網站使用通用唯一識別碼(UUID)概念，為每個草稿和提交的表單產生唯一ID。 您也可以產生您自己的唯一ID。 您可以實作介面FPKeyGeneratorService、覆寫其方法，並開發自訂邏輯，為每個草稿和提交的表單產生自訂唯一ID。 此外，將自訂ID產生實作的服務排名設定為高於0。 它可確保使用自訂實作，而非預設實作。

```java
public interface FPKeyGeneratorService {
    /**
     * returns a unique id for draft and submission
     *
     * @param none
     * @return unique id in string format as per the implementation
     * @throws FormsPortalException
     */
    public String getUniqueId() throws FormsPortalException;
}
```

您可以使用下列附註來增加使用上述程式碼產生之自訂ID的服務排名：

`@Properties(value = { @Property(name = "service.ranking", intValue = 15) } )`

要使用上述注釋，請將以下內容導入項目：

```
import org.apache.felix.scr.annotations.Properties;
 import org.apache.felix.scr.annotations.Property;
```

