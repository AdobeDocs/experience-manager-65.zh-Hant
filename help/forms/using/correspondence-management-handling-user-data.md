---
title: 信件管理 |處理使用者資料
seo-title: 信件管理 |處理使用者資料
description: 信件管理 |處理使用者資料
uuid: d5bb190b-d668-4da3-95da-b7705ad302d9
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 764d8e0d-604d-4c7b-89cd-7686ce5f03ff
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---


# 信件管理 |處理用戶資料{#correspondence-management-handling-user-data}

AEM Forms通信管理可讓您建立、管理和簡化安全且個人化的客戶通訊。 它提供直覺式使用者介面，讓商業使用者使用預先核准的內容區塊和媒體元素來建立通訊。 有關建立通信的詳細資訊，請參閱[建立通信](/help/forms/using/create-correspondence.md)。

當業務用戶或代理將通信保存為草稿或提交時，信件實例將保存在儲存庫AEM中。 字母實例包括對應資料和元資料。

>[!NOTE]
>
>在AEMForms6.5中，通信管理不是現成可用的。 如果您要從舊版AEM Forms升級，請安裝相容性套件並移轉您的通訊管理資產，以繼續在AEM6.5Forms使用。 有關詳細資訊，請參見[ Compatibility package](/help/forms/using/compatibility-package.md)。

## 用戶資料和資料儲存{#data}

僅當發佈實例配置為管理字母實例時，AEM通信管理才將草稿和已提交字母的資料儲存在儲存庫中。 有關配置的詳細資訊，請參見[Corresponce Management配置屬性](/help/forms/using/cm-configuration-properties.md)。

根據為部署配置的資料儲存持久性AEM，草稿和提交的通信資料儲存在以下位置。

<table>
 <tbody>
  <tr>
   <td><p><strong>持久性類型</strong></p> </td>
   <td><p><strong>資料儲存</strong></p> </td>
   <td><p><strong>位置</strong></p> </td>
  </tr>
  <tr>
   <td><p>預設</p> </td>
   <td><p>在反向複製AEM配置中指定的發佈實例和作者實例儲存庫</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code> </p> </td>
  </tr>
  <tr>
   <td><p>遠端</p> </td>
   <td><p>遠程處AEM理作者實例的儲存庫</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

在上述指定的存AEM儲庫位置：

* `[yyyy]/[mm]/[dd]` 是基於建立字母實例的日期的節點結構
* `[node-id]` 是指派給包含字母的資料夾的ID
* `[letter-instance-name]` 是儲存或送出信函時指定的名稱

在[letter-instance-name]節點下，將建立以下節點結構，並將每個letter實例的資料儲存在儲存庫AEM中：

| 節點 | 說明 |
|---|---|
| `extendedProperties` | 儲存字母實例的元資料屬性。 |
| `dataXML` | 以二進位格式儲存包含對應資料的可下載的dataXML檔案。 |
| `processedXDP` | 包含用於建立已提交信函的XDP模板的詳細資訊。 此節點僅為提交的通信建立。 |
| `submittedLetter` | 以可下載的二進位格式儲存提交的信函資料。 此節點僅為提交的通信建立。 |

## 存取和刪除使用者資料{#access-and-delete-user-data}

您可以存取已設定資料存放區中的草稿和已提交的對應資料，並視需要加以刪除。

### 訪問用戶資料{#access-user-data}

信件管理提供API，您可用來尋找及存取草稿和已提交的信件例項。 使用API，您可以使用字母實例ID或儲存或提交信件的使用者來尋找並開啟字母實例。 如需詳細資訊，請參閱[存取字母例項的API](/help/forms/using/cm-apis-to-access-letter-instances.md)。

或者，您也可以使用CRX DELite導航到存AEM儲庫中的字母實例。 有關儲存的資料和儲存庫位置的資訊，請參見[用戶資料和資料儲存](/help/forms/using/correspondence-management-handling-user-data.md#data)。

### 刪除用戶資料{#delete-user-data}

要查找包含特定用戶資料的字母實例，您可以：

* 如果信件實例名稱或保存草稿或提交信件的用戶已知，請使用信件管理API
* 使用電AEM子郵件ID或名稱等個人身份資訊進行儲存庫搜索，以查找儲存資訊的節點

要從系統中完全刪除草稿和提交的通信中AEM的用戶資料，必須從所有適用實例中手動刪除字母實例AEM節點。
