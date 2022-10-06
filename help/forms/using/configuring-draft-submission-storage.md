---
title: 配置草稿和提交的儲存服務
seo-title: Configuring storage services for drafts and submissions
description: 了解如何為草稿和提交內容設定儲存空間
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

# 配置草稿和提交的儲存服務 {#configuring-storage-services-for-drafts-and-submissions}

## 總覽 {#overview}

透過AEM Forms，您可以儲存：

* **草稿**:進行中的表單，一般使用者可填寫並儲存以供稍後提交。

* **提交**:包含使用者提供資料的已提交表單。

AEM Forms入口網站資料和中繼資料服務提供草稿和提交的支援。 依預設，資料會儲存在發佈例項中，然後反向複製到已設定的製作例項，以便滲濾至其他發佈例項。

現有現成可用方法的問題在於，它會儲存發佈執行個體上的所有資料，包括可能是個人識別資訊(PII)的資料。

除了上述的預設方法外，您也可以選擇使用替代實作，將表單資料直接推送至處理，而非儲存於本機。 客戶若對於在發佈執行個體上儲存可能敏感的資料有疑慮，可選擇將資料傳送至處理伺服器的替代實施。 由於處理髮生在製作例項上，因此通常會保留在安全區域。

>[!NOTE]
>
>當您使用Forms Portal提交動作或啟用適用性表單中的「在表單入口網站中儲存資料」選項時，表單資料會儲存在AEM存放庫。 在生產環境中，建議不要將草稿或已提交的表單資料儲存在AEM存放庫中。 相反地，您必須將草稿和提交元件與安全的儲存體（如企業資料庫）整合，以儲存草稿和提交的表單資料。
>
>如需詳細資訊，請參閱 [將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md).

## 設定Forms Portal草稿和提交服務 {#configuring-forms-portal-drafts-and-submissions-services}

在AEM Web主控台設定中( `https://[host]:'port'/system/console/configMgr`)，按一下以開啟 **Forms入口網站草稿和提交設定** 在編輯模式中。

根據您的需求指定屬性的值，如下所述：

### 在發佈執行個體上儲存資料的現成可用服務 {#out-of-the-box-services-to-store-data-on-publish-instance}

資料會反向複製至已設定的製作執行個體。

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>值</th>
  </tr>
  <tr>
   <td>Forms入口網站草稿資料服務(草稿資料服務的識別碼(<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms入口網站草稿中繼資料服務（草稿中繼資料服務的識別碼）(<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal提交資料服務(提交資料服務的識別碼(<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal提交中繼資料服務(提交中繼資料服務的識別碼(<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td>
  </tr>
 </tbody>
</table>

### 在遠程處理實例上儲存資料的現成可用服務 {#out-of-the-box-services-to-store-data-on-remote-processing-instance}

資料會直接推送至已設定的遠端執行個體

<table>
 <tbody>
  <tr>
   <th>屬性</th>
   <th>值</th>
  </tr>
  <tr>
   <td>Forms入口網站草稿資料服務(草稿資料服務的識別碼(<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms入口網站草稿中繼資料服務（草稿中繼資料服務的識別碼）(<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal提交資料服務(提交資料服務的識別碼(<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal提交中繼資料服務(提交中繼資料服務的識別碼(<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

除了上述指定的配置外，還提供有關已配置遠程處理實例的資訊。

在AEM Web主控台設定中( `https://[host]:'port'/system/console/configMgr`)，按一下以開啟 **AEM DS設定服務** 在編輯模式中。 在「AEM DS設定服務」對話框中，提供有關處理伺服器URL、處理伺服器用戶名和密碼的資訊。

>[!NOTE]
>
>還提供了用於將用戶資料儲存在資料庫中的示例實現。 若要了解如何設定資料和中繼資料服務，以將使用者資料儲存在外部資料庫，請參閱 [將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md).
