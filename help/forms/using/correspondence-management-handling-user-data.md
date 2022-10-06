---
title: 通信管理 |處理用戶資料
seo-title: Correspondence Management | Handling user data
description: 通信管理 |處理用戶資料
uuid: d5bb190b-d668-4da3-95da-b7705ad302d9
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 764d8e0d-604d-4c7b-89cd-7686ce5f03ff
role: Admin
exl-id: a0c6a02c-47a3-4e70-a14c-953ee016b8e4
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# 通信管理 |處理用戶資料 {#correspondence-management-handling-user-data}

AEM Forms通信管理可讓您建立、管理及簡化安全且個人化的客戶通訊。 它提供直覺式的使用者介面，供商務使用者使用預先核准的內容區塊和媒體元素來建立對應。 如需建立通信的詳細資訊，請參閱 [建立通信](/help/forms/using/create-correspondence.md).

當業務使用者或代理將信函儲存為草稿或提交時，信函例項會儲存在AEM存放庫中。 信函例項包含通信資料和中繼資料。

>[!NOTE]
>
>在AEM 6.5 Forms中，無法立即使用通信管理。 如果您從舊版AEM Forms升級，請安裝相容性套件並移轉通信管理資產，以繼續在AEM 6.5 Forms中使用。 如需詳細資訊，請參閱 [相容性套件](/help/forms/using/compatibility-package.md).

## 使用者資料和資料儲存 {#data}

只有在將發佈例項設定為管理信函例項時，通信管理才會將草稿和已提交信函的資料儲存在AEM存放庫中。 如需設定的詳細資訊，請參閱 [通信管理配置屬性](/help/forms/using/cm-configuration-properties.md).

根據為AEM部署設定的資料儲存持續性，草稿和已提交的通信資料會儲存在下列位置。

<table>
 <tbody>
  <tr>
   <td><p><strong>持久性類型</strong></p> </td>
   <td><p><strong>資料儲存</strong></p> </td>
   <td><p><strong>位置</strong></p> </td>
  </tr>
  <tr>
   <td><p>預設</p> </td>
   <td><p>反向復寫設定中指定的AEM發佈例項和製作例項存放庫</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code> </p> </td>
  </tr>
  <tr>
   <td><p>遠端</p> </td>
   <td><p>AEM遠端處理製作例項的存放庫</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

在上述指定的AEM存放庫位置：

* `[yyyy]/[mm]/[dd]` 是根據信函例項建立日期的節點結構
* `[node-id]` 是指派給包含信函之資料夾的ID
* `[letter-instance-name]` 是儲存或提交信函時指定的名稱

在 [letter-instance-name] 節點，則會建立下列節點結構，並將每個信函例項的資料儲存在AEM存放庫中：

| 節點 | 說明 |
|---|---|
| `extendedProperties` | 儲存信函例項的中繼資料屬性。 |
| `dataXML` | 以二進位格式儲存包含通信資料的可下載dataXML檔案。 |
| `processedXDP` | 包含用於建立已提交信函的XDP範本詳細資訊。 此節點僅針對提交的通信而建立。 |
| `submittedLetter` | 以可下載的二進位格式儲存已提交的信函資料。 此節點僅針對提交的通信而建立。 |

## 存取和刪除使用者資料 {#access-and-delete-user-data}

您可以在設定的資料存放區中存取草稿和已提交的通信資料，並視需要將其刪除。

### 存取使用者資料 {#access-user-data}

通信管理提供API，您可用來尋找及存取草稿和已提交信函例項。 您可以使用API，使用信函例項ID或儲存或提交信函的使用者來尋找和開啟信函例項。 如需詳細資訊，請參閱 [存取信函例項的API](/help/forms/using/cm-apis-to-access-letter-instances.md).

或者，您也可以使用CRX DELite導覽至AEM存放庫中的信函例項。 請參閱 [使用者資料和資料儲存](/help/forms/using/correspondence-management-handling-user-data.md#data) ，了解儲存的資料和儲存庫位置。

### 刪除使用者資料 {#delete-user-data}

若要尋找包含特定使用者資料的信函例項，您可以：

* 如果信函例項名稱或已儲存草稿或已提交信函的使用者已知，請使用通信管理API
* 使用AEM存放庫搜尋功能，使用個人識別資訊（例如電子郵件ID或名稱），尋找儲存資訊的節點

若要從AEM系統完全刪除草稿和已提交對應中的使用者資料，您必須從所有適用的AEM例項中手動刪除信函例項節點。
