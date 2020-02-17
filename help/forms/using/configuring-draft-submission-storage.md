---
title: 為草稿和提交配置儲存服務
seo-title: 為草稿和提交配置儲存服務
description: 瞭解如何設定草稿和提交的儲存空間
seo-description: 瞭解如何設定草稿和提交的儲存空間
uuid: 2f4efc07-312c-4908-8c91-84f4e6c5ad25
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6ebb6420-68b6-4abc-b298-c252db038416
translation-type: tm+mt
source-git-commit: f9ed171c188a4dfb71f12ae9c98105a4c1895542

---


# 為草稿和提交配置儲存服務 {#configuring-storage-services-for-drafts-and-submissions}

## 概覽 {#overview}

有了AEM Forms，您可以儲存：

* **草稿**:使用者可填寫並儲存的進行中表單，以供稍後提交。

* **提交**:已提交包含使用者提供資料的表單。

AEM Forms Portal資料和中繼資料服務可支援草稿和提交。 依預設，資料會儲存在發佈例項中，然後反向複製至已設定的作者例項，以便滲濾至其他發佈例項。

現有的現成方法的顧慮是，它會將所有資料儲存在發佈例項上，包括可以是個人識別資訊(PII)的資料。

除了上述預設方法外，還提供另一種實作方式，可直接將表單資料推送至處理，而非將表單資料儲存在本機。 擔心在發佈實例上儲存可能敏感資料的客戶可以選擇將資料傳送至處理伺服器的替代實施。 由於處理是在作者例項上進行，因此通常會維持在安全區。

>[!NOTE]
>
>當您使用Forms Portal提交動作或啟用以最適化表單形式在表單入口網站中儲存資料選項時，表單資料會儲存在AEM儲存庫中。 在生產環境中，建議您不要將草稿或提交的表單資料儲存在AEM儲存庫中。 您必須將草稿和提交元件與安全儲存（例如企業資料庫）整合，以儲存草稿和提交的表單資料。
>
>如需詳細資訊，請參 [閱將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md)。

## 設定Forms Portal草稿和提交服務 {#configuring-forms-portal-drafts-and-submissions-services}

在「AEM Web Console設定」( `https://[host]:[port]/system/console/configMgr`)中，按一下以編輯模 **式開啟「表單入口網站草稿和提交設定** 」。

根據您的需求指定屬性的值，如下所述：

### 立即可用的服務，將資料儲存在發佈例項上 {#out-of-the-box-services-to-store-data-on-publish-instance}

資料會反向複製至已設定的作者例項。

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>值</th>
  </tr>
  <tr>
   <td>Forms Portal Draft Data Service(草稿資料服務的識別碼(<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal草稿中繼資料服務(草稿中繼資料服務(<strong>draft.metadata.service</strong>)的識別碼)</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal提交資料服務(提交資料服務的識<strong>別碼(submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal提交中繼資料服務(提交中繼資料服務(<strong>submit.metadata.service</strong>)的識別碼)</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td>
  </tr>
 </tbody>
</table>

### 立即可用的服務，將資料儲存在遠端處理例項上 {#out-of-the-box-services-to-store-data-on-remote-processing-instance}

將資料直接推送到配置的遠程實例

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>值</th>
  </tr>
  <tr>
   <td>Forms Portal Draft Data Service(草稿資料服務的識別碼(<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal草稿中繼資料服務(草稿中繼資料服務(<strong>draft.metadata.service</strong>)的識別碼)</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal提交資料服務(提交資料服務的識<strong>別碼(submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal提交中繼資料服務(提交中繼資料服務(<strong>submit.metadata.service</strong>)的識別碼)</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

除了上述指定的配置外，請提供有關已配置遠程處理實例的資訊。

在「AEM Web Console設定」( `https://[host]:[port]/system/console/configMgr`)中，按一下以編輯模 **式開啟「AEM DS Settings Service** 」。 在「AEM DS設定服務」對話方塊中，提供有關處理伺服器URL、處理伺服器使用者名稱和密碼的資訊。

>[!NOTE]
>
>還提供了用於將用戶資料儲存在資料庫中的示例實現。 若要瞭解如何設定資料和中繼資料服務，以將使用者資料儲存在外部資料庫中，請參閱匯入草稿和提交元件與資料庫的 [範例](/help/forms/using/integrate-draft-submission-database.md)。

