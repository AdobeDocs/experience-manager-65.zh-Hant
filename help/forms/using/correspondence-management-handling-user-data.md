---
title: 通訊管理 | 處理使用者資料
description: 瞭解在Adobe Experience Manager Forms環境中通訊管理和處理使用者資料。
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
exl-id: a0c6a02c-47a3-4e70-a14c-953ee016b8e4
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Form Data Model
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# 通訊管理 | 處理使用者資料 {#correspondence-management-handling-user-data}

AEM Forms Correspondence Management可讓您建立、管理及簡化安全且個人化的客戶信函。 它提供直覺式使用者介面，供商業使用者使用預先核准的內容區塊和媒體元素來建立對應。 如需建立對應的詳細資訊，請參閱 [建立對應](/help/forms/using/create-correspondence.md).

當業務使用者或代理程式將通訊儲存為草稿或提交時，信件例項會儲存在AEM存放庫中。 信件例項包含通訊資料和中繼資料。

>[!NOTE]
>
>在AEM 6.5 Forms中，無法立即使用通訊管理。 如果您從舊版AEM Forms升級，請安裝相容性套件並移轉通訊管理資產，以繼續在AEM 6.5 Forms中使用。 如需詳細資訊，請參閱 [相容性套件](/help/forms/using/compatibility-package.md).

## 使用者資料和資料存放區 {#data}

只有當發佈執行個體設定為管理信函執行個體時，通訊管理才會將草稿和已提交信函的資料儲存在AEM存放庫中。 如需有關設定的詳細資訊，請參閱 [通訊管理設定屬性](/help/forms/using/cm-configuration-properties.md).

根據為您的AEM部署設定的資料存放區持續性，草稿和提交的通訊資料會儲存在以下位置。

<table>
 <tbody>
  <tr>
   <td><p><strong>持續性型別</strong></p> </td>
   <td><p><strong>資料存放區</strong></p> </td>
   <td><p><strong>位置</strong></p> </td>
  </tr>
  <tr>
   <td><p>預設</p> </td>
   <td><p>反向復寫設定中所指定的發佈執行個體和作者執行個體的AEM存放庫</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code><br /> </p> </td>
  </tr>
  <tr>
   <td><p>遠端</p> </td>
   <td><p>遠端處理作者例項的AEM存放庫</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

在上述指定的AEM存放庫位置：

* `[yyyy]/[mm]/[dd]` 是以信件例項的建立日期為基礎的節點結構
* `[node-id]` 是指派給包含字母的資料夾的ID
* `[letter-instance-name]` 是儲存或提交信函時指定的名稱

在 [letter-instance-name] 節點，則會建立下列節點結構，並將每個信件例項的資料儲存在AEM存放庫中：

| 節點 | 說明 |
|---|---|
| `extendedProperties` | 儲存信件例項的中繼資料屬性。 |
| `dataXML` | 以二進位格式儲存包含對應資料的可下載資料XML檔案。 |
| `processedXDP` | 包含用來建立已提交信函的XDP範本的詳細資訊。 此節點僅針對已提交的往來行建立。 |
| `submittedLetter` | 以可下載的二進位格式儲存提交的字母資料。 此節點僅針對已提交的往來行建立。 |

## 存取和刪除使用者資料 {#access-and-delete-user-data}

您可以存取已設定資料存放區中的草稿與已提交的通訊資料，並視需要刪除這些資料。

### 存取使用者資料 {#access-user-data}

通訊管理提供API，您可以使用這些API來尋找和存取草稿與已提交的信件例項。 使用API，您可以使用信件例項ID或儲存或提交信件的使用者來尋找和開啟信件例項。 如需詳細資訊，請參閱 [存取信件例項的API](/help/forms/using/cm-apis-to-access-letter-instances.md).

或者，您可以使用CRXDE Lite導覽至AEM存放庫中的信件例項。 另請參閱 [使用者資料和資料存放區](/help/forms/using/correspondence-management-handling-user-data.md#data) 以取得有關儲存資料和存放庫位置的資訊。

### 刪除使用者資料 {#delete-user-data}

若要尋找包含特定使用者資料的信件例項，您可以：

* 如果信函例項名稱或儲存草稿或提交信函的使用者已知，則使用信函管理API
* 使用電子郵件ID或名稱等個人識別資訊進行AEM存放庫搜尋，以尋找儲存資訊的節點

若要從AEM系統完全刪除草稿與已提交對映中的使用者資料，您必須從所有適用的AEM執行處理中手動刪除信函執行處理節點。
