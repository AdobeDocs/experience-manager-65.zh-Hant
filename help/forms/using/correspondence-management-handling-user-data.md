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

AEM Forms通信管理使您能夠建立、管理和簡化安全和個性化的客戶通信。 它為商業用戶提供了一個直觀的用戶介面，使用預先批准的內容塊和媒體元素建立對應。 有關建立對應的詳細資訊，請參見 [建立對應](/help/forms/using/create-correspondence.md)。

當業務用戶或代理將信件保存為草稿或提交時，信件實例將保存在儲存AEM庫中。 該信件實例包括通信資料和元資料。

>[!NOTE]
>
>在AEMForms6.5中，沒有現成的通信管理。 如果您正在從以前的AEM Forms版本升級，請安裝相容性軟體包並遷移您的通信管理資產，以繼續在AEM6.5Forms使用這些資產。 有關詳細資訊，請參見 [相容性包](/help/forms/using/compatibility-package.md)。

## 用戶資料和資料儲存 {#data}

僅當將發佈實例配置為管理信函實例時，AEM通信管理才會在儲存庫中儲存草稿和已提交信函的資料。 有關配置的詳細資訊，請參見 [通信管理配置屬性](/help/forms/using/cm-configuration-properties.md)。

根據為您的部署配置的資料儲存持久性AEM，草稿和提交的通信資料儲存在以下位置。

<table>
 <tbody>
  <tr>
   <td><p><strong>持久性類型</strong></p> </td>
   <td><p><strong>資料儲存</strong></p> </td>
   <td><p><strong>位置</strong></p> </td>
  </tr>
  <tr>
   <td><p>預設</p> </td>
   <td><p>反向AEM複製配置中指定的發佈實例和作者實例儲存庫</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code> </p> </td>
  </tr>
  <tr>
   <td><p>遠端</p> </td>
   <td><p>遠程AEM處理作者實例的儲存庫</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

在上述指定的存AEM儲庫位置：

* `[yyyy]/[mm]/[dd]` 是基於建立字母實例的日期的節點結構
* `[node-id]` 是分配給包含信件的資料夾的ID
* `[letter-instance-name]` 是保存或提交信件時指定的名稱

在 [字母實例名稱] 節點，將建立以下節點結構，並將每個字母實例的資料儲存在儲存AEM庫中：

| 節點 | 說明 |
|---|---|
| `extendedProperties` | 儲存字母實例的元資料屬性。 |
| `dataXML` | 以二進位格式儲存包含對應資料的可下載資料XML檔案。 |
| `processedXDP` | 包括用於建立已提交信函的XDP模板的詳細資訊。 此節點僅為已提交的對應建立。 |
| `submittedLetter` | 以可下載的二進位格式儲存提交的信函資料。 此節點僅為已提交的對應建立。 |

## 訪問和刪除用戶資料 {#access-and-delete-user-data}

您可以訪問已配置資料儲存中的草稿和已提交的通信資料，並在必要時刪除它。

### 訪問用戶資料 {#access-user-data}

通信管理提供了API，您可以使用這些API查找和訪問草稿和已提交的信函實例。 使用API，您可以使用信件實例ID或保存或提交信件的用戶查找和開啟信件實例。 有關詳細資訊，請參見 [訪問字母實例的API](/help/forms/using/cm-apis-to-access-letter-instances.md)。

或者，可以使用CRX DELite導航到AEM儲存庫中的字母實例。 請參閱 [用戶資料和資料儲存](/help/forms/using/correspondence-management-handling-user-data.md#data) 的子菜單。

### 刪除用戶資料 {#delete-user-data}

要查找包含特定用戶資料的字母實例，您可以：

* 如果信件實例名稱或保存草稿或提交信件的用戶已知，則使用信件管理API
* 使用AEM個人身份資訊（如電子郵件ID或名稱）進行儲存庫搜索，以查找儲存資訊的節點

要從系統中完全刪除草稿和提交的對AEM應中的用戶資料，必須從所有適用實例中手動刪除字母實例AEM節點。
