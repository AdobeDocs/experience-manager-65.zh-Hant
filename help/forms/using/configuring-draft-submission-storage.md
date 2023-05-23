---
title: 為草稿和提交配置儲存服務
seo-title: Configuring storage services for drafts and submissions
description: 瞭解如何配置草稿和提交的儲存
seo-description: Learn how to configure storage for drafts and submissions
uuid: 2f4efc07-312c-4908-8c91-84f4e6c5ad25
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6ebb6420-68b6-4abc-b298-c252db038416
exl-id: 51ca2844-91f0-453a-9b39-b876399ebecb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# 為草稿和提交配置儲存服務 {#configuring-storage-services-for-drafts-and-submissions}

## 概觀 {#overview}

對於AEM Forms，您可以儲存：

* **草稿**:最終用戶填寫並保存的在製品表格，以後提交。

* **提交**:已提交的表單包含用戶提供的資料。

AEM Forms門戶資料和元資料服務為草稿和提交提供支援。 預設情況下，資料儲存在發佈實例中，然後將其反向複製到已配置的作者實例中，以便可滲透到其他發佈實例。

現有現成的現成方法的關注點是，它儲存發佈實例上的所有資料，包括可以是個人識別資訊(PII)的資料。

除了上述預設方法之外，還提供了一種替代性實現，用於直接將表單資料推送到處理，而不是將其保存到本地。 對在發佈實例上儲存可能敏感的資料有顧慮的客戶可以選擇將資料發送到處理伺服器的替代實施。 由於處理過程發生在作者實例上，因此它通常停留在安全區域。

>[!NOTE]
>
>當您使用Forms門戶提交操作或以自適應形式啟用「在表單門戶中儲存資料」選項時，表單資料將儲存在儲存AEM庫中。 在生產環境中，建議不要將草稿或提交的表單資料儲存在儲存AEM庫中。 相反，您必須將草稿和提交元件與安全儲存（如企業資料庫）整合，以儲存草稿和提交的表單資料。
>
>有關詳細資訊，請參見 [將草稿和提交元件與資料庫整合的示例](/help/forms/using/integrate-draft-submission-database.md)。

## 配置Forms門戶草稿和提交服務 {#configuring-forms-portal-drafts-and-submissions-services}

在Web控AEM制台配置中( `https://[host]:'port'/system/console/configMgr`)，按一下開啟 **Forms門戶草稿和提交配置** 的子菜單。

根據您的要求指定屬性的值，如下所述：

### 在發佈實例上儲存資料的現成服務 {#out-of-the-box-services-to-store-data-on-publish-instance}

資料被反向複製到已配置的作者實例。

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>值</th>
  </tr>
  <tr>
   <td>Forms門戶草稿資料服務（草稿資料服務的標識符）<strong>draft.data.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms門戶草稿元資料服務（草稿元資料服務的標識符）<strong>draft.metadata.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms門戶提交資料服務(提交資料服務的標識符(<strong>submit.data.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms門戶提交元資料服務(提交元資料服務的標識符(<strong>submit.metadata.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td>
  </tr>
 </tbody>
</table>

### 在遠程處理實例上儲存資料的現成服務 {#out-of-the-box-services-to-store-data-on-remote-processing-instance}

資料將直接推送到已配置的遠程實例

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>值</th>
  </tr>
  <tr>
   <td>Forms門戶草稿資料服務（草稿資料服務的標識符）<strong>draft.data.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms門戶草稿元資料服務（草稿元資料服務的標識符）<strong>draft.metadata.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms門戶提交資料服務(提交資料服務的標識符(<strong>submit.data.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms門戶提交元資料服務(提交元資料服務的標識符(<strong>submit.metadata.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

除上面指定的配置外，請提供有關已配置遠程處理實例的資訊。

在Web控AEM制台配置中( `https://[host]:'port'/system/console/configMgr`)，按一下開啟 **AEM DS設定服務** 的子菜單。 在「AEMDS設定服務」對話框中，提供有關處理伺服器URL、處理伺服器用戶名和密碼的資訊。

>[!NOTE]
>
>還提供了用於將用戶資料儲存在資料庫中的示例實現。 要瞭解如何配置資料和元資料服務以在外部資料庫中儲存用戶資料，請參見 [將草稿和提交元件與資料庫整合的示例](/help/forms/using/integrate-draft-submission-database.md)。
